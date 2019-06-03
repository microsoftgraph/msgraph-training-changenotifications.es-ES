<!-- markdownlint-disable MD002 MD041 -->

Abra el archivo **Startup.CS** y elimine la línea siguiente para deshabilitar el redireccionamiento de SSL.

```csharp
//app.UseHttpsRedirection();
```

### <a name="add-model-classes"></a>Agregar clases de modelo

La aplicación usa varias clases de modelo nuevas para (de) la serialización de mensajes desde o hacia Microsoft Graph.

Haga clic con el botón secundario en el árbol de archivos del proyecto y seleccione **nueva carpeta**. Asígnele el nombre **modelos** haga clic con el botón secundario en la carpeta **modelos** y agregue tres nuevos archivos:

- **Notification.cs**
- **ResourceData.cs**
- **MyConfig.cs**

Reemplace el contenido de **Notification.CS** por lo siguiente:

```csharp
using Newtonsoft.Json;
using System;

namespace msgraphapp.Models
{
  public class Notifications
  {
    [JsonProperty(PropertyName = "value")]
    public Notification[] Items { get; set; }
  }

  // A change notification.
  public class Notification
  {
    // The type of change.
    [JsonProperty(PropertyName = "changeType")]
    public string ChangeType { get; set; }

    // The client state used to verify that the notification is from Microsoft Graph. Compare the value received with the notification to the value you sent with the subscription request.
    [JsonProperty(PropertyName = "clientState")]
    public string ClientState { get; set; }

    // The endpoint of the resource that changed. For example, a message uses the format ../Users/{user-id}/Messages/{message-id}
    [JsonProperty(PropertyName = "resource")]
    public string Resource { get; set; }

    // The UTC date and time when the webhooks subscription expires.
    [JsonProperty(PropertyName = "subscriptionExpirationDateTime")]
    public DateTimeOffset SubscriptionExpirationDateTime { get; set; }

    // The unique identifier for the webhooks subscription.
    [JsonProperty(PropertyName = "subscriptionId")]
    public string SubscriptionId { get; set; }

    // Properties of the changed resource.
    [JsonProperty(PropertyName = "resourceData")]
    public ResourceData ResourceData { get; set; }
  }
}
```

Reemplace el contenido de **ResourceData.CS** por lo siguiente:

```csharp
using Newtonsoft.Json;

namespace msgraphapp.Models
{
  public class ResourceData
  {
    // The ID of the resource.
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }

    // The OData etag property.
    [JsonProperty(PropertyName = "@odata.etag")]
    public string ODataEtag { get; set; }

    // The OData ID of the resource. This is the same value as the resource property.
    [JsonProperty(PropertyName = "@odata.id")]
    public string ODataId { get; set; }

    // The OData type of the resource: "#Microsoft.Graph.Message", "#Microsoft.Graph.Event", or "#Microsoft.Graph.Contact".
    [JsonProperty(PropertyName = "@odata.type")]
    public string ODataType { get; set; }
  }
}
```

Reemplace el contenido de **MyConfig.CS** por lo siguiente:

```csharp
namespace msgraphapp
{
    public class MyConfig
    {
        public string AppId { get; set; }
        public string AppSecret { get; set; }
        public string TenantId { get; set; }
        public string Ngrok { get; set; }
    }
}
```

Abra el archivo **Startup.CS** y reemplace el contenido por lo siguiente.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
    var config = new MyConfig();
    Configuration.Bind("MyConfig", config);
    services.AddSingleton(config);
}
```

Abra el archivo **appSettings. JSON** y reemplace el contenido por lo siguiente.

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "MyConfig":
  {
    "AppId": "<APP ID>",
    "AppSecret": "<APP SECRET>",
    "TenantId": "<TENANT ID>",
    "Ngrok": "<NGROK URL>"
  }
}
```

Reemplace las siguientes variables con los valores copiados anteriormente:

    - `<NGROK URL>`debe establecerse en la dirección URL https ngrok que copió anteriormente.
    - `<TENANT ID>`debe ser su identificador de inquilino de Office 365, por ejemplo. **contoso.onmicrosoft.com**.
    - `<APP ID>`y `<APP SECRET>` debe ser el identificador de la aplicación y el secreto que copió anteriormente al crear el registro de la aplicación.

### <a name="add-notification-controller"></a>Agregar controlador de notificación

La aplicación requiere un nuevo controlador para procesar la suscripción y la notificación.

Haga clic con el `Controllers` botón secundario en la carpeta, seleccione **nuevo archivo**y asigne el nombre **NotificationsController.CS**al controlador.

Reemplace el contenido de **NotificationController.CS** por lo siguiente:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using msgraphapp.Models;
using Newtonsoft.Json;
using System.Net;
using System.Net.Http.Formatting;
using System.Threading;
using Microsoft.Graph;
using Microsoft.Identity.Client;
using System.Net.Http.Headers;

namespace msgraphapp.Controllers
{
  [Route("api/[controller]")]
  [ApiController]
  public class NotificationsController : ControllerBase
  {
    private readonly MyConfig config;

    public NotificationsController(MyConfig config)
    {
      this.config = config;
    }

    [HttpGet]
    public ActionResult<string> Get()
    {
      var graphServiceClient = GetGraphClient();

      var sub = new Microsoft.Graph.Subscription();
      sub.ChangeType = "updated";
      sub.NotificationUrl = config.Ngrok + "/api/notifications";
      sub.Resource = "/users";
      sub.ExpirationDateTime = DateTime.UtcNow.AddMinutes(5);
      sub.ClientState = "SecretClientState";

      var newSubscription = graphServiceClient
        .Subscriptions
        .Request()
        .AddAsync(sub).Result;

      return $"Subscribed. Id: {newSubscription.Id}, Expiration: {newSubscription.ExpirationDateTime}";
    }

    public ActionResult<string> Post([FromQuery]string validationToken = null)
    {
      // handle validation
      if(!string.IsNullOrEmpty(validationToken))
      {
        Console.WriteLine($"Received Token: '{validationToken}'");
        return Ok(validationToken);
      }

      // handle notifications
      using (StreamReader reader = new StreamReader(Request.Body))
      {
        string content = reader.ReadToEnd();

        Console.WriteLine(content);

        var notifications = JsonConvert.DeserializeObject<Notifications>(content);

        foreach(var notification in notifications.Items)
        {
          Console.WriteLine($"Received notification: '{notification.Resource}', {notification.ResourceData?.Id}");
        }
      }

      return Ok();
    }

    private GraphServiceClient GetGraphClient()
    {
      var graphClient = new GraphServiceClient(new DelegateAuthenticationProvider((requestMessage) => {

          // get an access token for Graph
          var accessToken = GetAccessToken().Result;

          requestMessage
              .Headers
              .Authorization = new AuthenticationHeaderValue("bearer", accessToken);

          return Task.FromResult(0);
      }));

      return graphClient;
    }

    private async Task<string> GetAccessToken()
    {
        ClientCredential clientCredentials = new ClientCredential(secret: config.AppSecret);

        var app = new ConfidentialClientApplication(
            clientId: config.AppId,
            authority: $"https://login.microsoftonline.com/{config.TenantId}",
            redirectUri: "https://daemon",
            clientCredential: clientCredentials,
            userTokenCache: null,
            appTokenCache: new TokenCache()
        );

        string[] scopes = new string[] { "https://graph.microsoft.com/.default" };

        var result = await app.AcquireTokenForClientAsync(scopes);

        return result.AccessToken;
    }
  }
}
```

**Guarde** todos los archivos.