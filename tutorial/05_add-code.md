<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="234af-101">Abra el archivo **Startup.CS** y elimine la línea siguiente para deshabilitar el redireccionamiento de SSL.</span><span class="sxs-lookup"><span data-stu-id="234af-101">Open the **Startup.cs** file and comment out the following line to disable ssl redirection.</span></span>

```csharp
//app.UseHttpsRedirection();
```

### <a name="add-model-classes"></a><span data-ttu-id="234af-102">Agregar clases de modelo</span><span class="sxs-lookup"><span data-stu-id="234af-102">Add model classes</span></span>

<span data-ttu-id="234af-103">La aplicación usa varias clases de modelo nuevas para (de) la serialización de mensajes desde o hacia Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="234af-103">The application uses several new model classes for (de)serialization of messages to/from the Microsoft Graph.</span></span>

<span data-ttu-id="234af-104">Haga clic con el botón secundario en el árbol de archivos del proyecto y seleccione **nueva carpeta**.</span><span class="sxs-lookup"><span data-stu-id="234af-104">Right-click in the project file tree and select **New Folder**.</span></span> <span data-ttu-id="234af-105">Asígnele el nombre **modelos** haga clic con el botón secundario en la carpeta **modelos** y agregue tres nuevos archivos:</span><span class="sxs-lookup"><span data-stu-id="234af-105">Name it **Models** Right-click the **Models** folder and add three new files:</span></span>

- <span data-ttu-id="234af-106">**Notification.cs**</span><span class="sxs-lookup"><span data-stu-id="234af-106">**Notification.cs**</span></span>
- <span data-ttu-id="234af-107">**ResourceData.cs**</span><span class="sxs-lookup"><span data-stu-id="234af-107">**ResourceData.cs**</span></span>
- <span data-ttu-id="234af-108">**MyConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="234af-108">**MyConfig.cs**</span></span>

<span data-ttu-id="234af-109">Reemplace el contenido de **Notification.CS** por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="234af-109">Replace the contents of **Notification.cs** with the following:</span></span>

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

<span data-ttu-id="234af-110">Reemplace el contenido de **ResourceData.CS** por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="234af-110">Replace the contents of **ResourceData.cs** with the following:</span></span>

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

<span data-ttu-id="234af-111">Reemplace el contenido de **MyConfig.CS** por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="234af-111">Replace the contents of **MyConfig.cs** with the following:</span></span>

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

<span data-ttu-id="234af-112">Abra el archivo **Startup.CS** y reemplace el contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="234af-112">Open the **Startup.cs** file and replace the contents with the following.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
    var config = new MyConfig();
    Configuration.Bind("MyConfig", config);
    services.AddSingleton(config);
}
```

<span data-ttu-id="234af-113">Abra el archivo **appSettings. JSON** y reemplace el contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="234af-113">Open the **appsettings.json** file and replace the content the following.</span></span>

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

<span data-ttu-id="234af-114">Reemplace las siguientes variables con los valores copiados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="234af-114">Replace the following variables with the values you copied earlier:</span></span>

    - <span data-ttu-id="234af-115">`<NGROK URL>`debe establecerse en la dirección URL https ngrok que copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="234af-115">`<NGROK URL>` should be set to the https ngrok url you copied earlier.</span></span>
    - <span data-ttu-id="234af-116">`<TENANT ID>`debe ser su identificador de inquilino de Office 365, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="234af-116">`<TENANT ID>` should be your Office 365 tenant id, for example.</span></span> <span data-ttu-id="234af-117">**contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="234af-117">**contoso.onmicrosoft.com**.</span></span>
    - <span data-ttu-id="234af-118">`<APP ID>`y `<APP SECRET>` debe ser el identificador de la aplicación y el secreto que copió anteriormente al crear el registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="234af-118">`<APP ID>` and `<APP SECRET>` should be the application id and secret you copied earlier when you created the application registration.</span></span>

### <a name="add-notification-controller"></a><span data-ttu-id="234af-119">Agregar controlador de notificación</span><span class="sxs-lookup"><span data-stu-id="234af-119">Add notification controller</span></span>

<span data-ttu-id="234af-120">La aplicación requiere un nuevo controlador para procesar la suscripción y la notificación.</span><span class="sxs-lookup"><span data-stu-id="234af-120">The application requires a new controller to process the subscription and notification.</span></span>

<span data-ttu-id="234af-121">Haga clic con el `Controllers` botón secundario en la carpeta, seleccione **nuevo archivo**y asigne el nombre **NotificationsController.CS**al controlador.</span><span class="sxs-lookup"><span data-stu-id="234af-121">Right-click the `Controllers` folder, select **New File**, and name the controller **NotificationsController.cs**.</span></span>

<span data-ttu-id="234af-122">Reemplace el contenido de **NotificationController.CS** por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="234af-122">Replace the contents of **NotificationController.cs** with the following:</span></span>

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

<span data-ttu-id="234af-123">**Guarde** todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="234af-123">**Save** all files.</span></span>