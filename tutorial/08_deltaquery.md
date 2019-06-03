<!-- markdownlint-disable MD002 MD041 -->

### <a name="query-for-changes"></a><span data-ttu-id="7efe6-101">Consulta de cambios</span><span class="sxs-lookup"><span data-stu-id="7efe6-101">Query for changes</span></span>

<span data-ttu-id="7efe6-102">Microsoft Graph ofrece la posibilidad de consultar los cambios realizados en un recurso determinado desde la última vez que se llamó a él.</span><span class="sxs-lookup"><span data-stu-id="7efe6-102">Microsoft Graph offers the ability to query for changes to a particular resource since you last called it.</span></span> <span data-ttu-id="7efe6-103">Usar esto combinado con las notificaciones de cambios es un método eficaz para garantizar que no se pierda ningún cambio en los recursos.</span><span class="sxs-lookup"><span data-stu-id="7efe6-103">Using this combined with Change Notifications is a robust method for ensuring you don't miss any changes to the resources.</span></span>

<span data-ttu-id="7efe6-104">Abra **NotificationsController.CS** y reemplace el `Post` método con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="7efe6-104">Open **NotificationsController.cs** and replace the `Post` method with the following code:</span></span>

```csharp
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

  // use deltaquery to query for all updates
  CheckForUpdates();

  return Ok();
}
```

<span data-ttu-id="7efe6-105">A `Post` continuación, el método `CheckForUpdates` llamará cuando se reciba una notificación.</span><span class="sxs-lookup"><span data-stu-id="7efe6-105">The `Post` method will now call `CheckForUpdates` when a notification is received.</span></span> <span data-ttu-id="7efe6-106">Debajo del `Post` método, agregue los dos nuevos métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7efe6-106">Below the `Post` method add the following two new methods:</span></span>

```csharp
private static object DeltaLink = null;

private static IUserDeltaCollectionPage lastPage = null;

private void CheckForUpdates()
{
  var graphClient = GetGraphClient();

  // get a page of users
  var users = GetUsers(graphClient, DeltaLink);

  OutputUsers(users);

  // go through all of the pages so that we can get the delta link on the last page.
  while (users.NextPageRequest != null)
  {
      users = users.NextPageRequest.GetAsync().Result;
      OutputUsers(users);
  }

  object deltaLink;

  if (users.AdditionalData.TryGetValue("@odata.deltaLink", out deltaLink))
  {
      DeltaLink = deltaLink;
  }
}

private void OutputUsers(IUserDeltaCollectionPage users)
{
  foreach(var user in users)
    {
      var message = $"User: {user.Id}, {user.GivenName} {user.Surname}";
      Console.WriteLine(message);
    }
}

private IUserDeltaCollectionPage GetUsers(GraphServiceClient graphClient, object deltaLink)
{
  IUserDeltaCollectionPage page;

  if(lastPage == null)
  {
    page = graphClient
      .Users
      .Delta()
      .Request()
      .GetAsync()
      .Result;

  }
  else
  {
    lastPage.InitializeNextPageRequest(graphClient, deltaLink.ToString());
    page = lastPage.NextPageRequest.GetAsync().Result;
  }

  lastPage = page;
  return page;
}
```

<span data-ttu-id="7efe6-107">El `CheckForUpdates` método llama al gráfico usando la dirección URL Delta y, a continuación, recorre los resultados hasta `deltalink` que encuentra un nuevo en la página final de los resultados.</span><span class="sxs-lookup"><span data-stu-id="7efe6-107">The `CheckForUpdates` method calls the graph using the delta url and then pages through the results until it finds a new `deltalink` on the final page of results.</span></span> <span data-ttu-id="7efe6-108">Almacena la dirección URL en la memoria hasta que se notifica de nuevo al código cuando se desencadena otra notificación.</span><span class="sxs-lookup"><span data-stu-id="7efe6-108">It stores the url in memory until the code is notified again when another notification is triggered.</span></span>

<span data-ttu-id="7efe6-109">**Guarde** todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="7efe6-109">**Save** all files.</span></span>

<span data-ttu-id="7efe6-110">Seleccione **Depurar > iniciar** depuración para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7efe6-110">Select **Debug > Start debugging** to run the application.</span></span> <span data-ttu-id="7efe6-111">Después de compilar la aplicación, se abrirá una ventana del explorador en una página de 404.</span><span class="sxs-lookup"><span data-stu-id="7efe6-111">After building the application a browser window will open to a 404 page.</span></span> <span data-ttu-id="7efe6-112">Esto es correcto porque nuestra aplicación es una API y no una página web.</span><span class="sxs-lookup"><span data-stu-id="7efe6-112">This is ok since our application is an API and not a webpage.</span></span>

<span data-ttu-id="7efe6-113">Para suscribirse a las notificaciones de cambios para los usuarios, `http://localhost:5000/api/notifications`navegue a la siguiente dirección URL.</span><span class="sxs-lookup"><span data-stu-id="7efe6-113">To subscribe for change notifications for users navigate to the following url `http://localhost:5000/api/notifications`.</span></span>

<span data-ttu-id="7efe6-114">Abra un explorador y visite el [centro de administración de Microsoft 365](https://admin.microsoft.com/AdminPortal).</span><span class="sxs-lookup"><span data-stu-id="7efe6-114">Open a browser and visit the [Microsoft 365 admin center](https://admin.microsoft.com/AdminPortal).</span></span> <span data-ttu-id="7efe6-115">Inicie sesión con una cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="7efe6-115">Sign-in using an administrator account.</span></span> <span data-ttu-id="7efe6-116">Seleccione **usuarios > usuarios activos**.</span><span class="sxs-lookup"><span data-stu-id="7efe6-116">Select **Users > Active users**.</span></span> <span data-ttu-id="7efe6-117">Seleccione un usuario activo y seleccione **Editar** en su **información de contacto**.</span><span class="sxs-lookup"><span data-stu-id="7efe6-117">Select an active user and select **Edit** for their **Contact information**.</span></span> <span data-ttu-id="7efe6-118">Actualice el valor del **teléfono móvil** con un número nuevo y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7efe6-118">Update the **Mobile phone** value with a new number and Select **Save**.</span></span>

![Captura de pantalla de los detalles del usuario](./images/10.png)

<span data-ttu-id="7efe6-120">Espere a que se reciba la notificación como se indica en la **consola** de depuración de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="7efe6-120">Wait for the notification to be received as indicated in the **DEBUG CONSOLE** as follows:</span></span>

```shell
Received notification: 'Users/7a7fded6-0269-42c2-a0be-512d58da4463', 7a7fded6-0269-42c2-a0be-512d58da4463
```

<span data-ttu-id="7efe6-121">La aplicación iniciará una consulta Delta con el gráfico para obtener todos los usuarios y cerrará algunos detalles en el resultado de la consola.</span><span class="sxs-lookup"><span data-stu-id="7efe6-121">The application will now initiate a delta query with the graph to get all the users and log out some of their details to the console output.</span></span>

```shell
User: 19e429d2-541a-4e0b-9873-6dff9f48fabe, Allan Deyoung
User: 05501e79-f527-4913-aabf-e535646d7ffa, Christie Cline
User: fecac4be-76e7-48ec-99df-df745854aa9c, Debra Berger
User: 4095c5c4-b960-43b9-ba53-ef806d169f3e, Diego Siciliani
User: b1246157-482f-420c-992c-fc26cbff74a5, Emily Braun
User: c2b510b7-1f76-4f75-a9c1-b3176b68d7ca, Enrico Cattaneo
User: 6ec9bd4b-fc6a-4653-a291-70d3809f2610, Grady Archie
User: b6924afe-cb7f-45a3-a904-c9d5d56e06ea, Henrietta Mueller
User: 0ee8d076-4f13-4e1a-a961-eac2b29c0ef6, Irvin Sayers
User: 31f66f05-ac9b-4723-9b5d-8f381f5a6e25, Isaiah Langer
User: 7ee95e20-247d-43ef-b368-d19d96550c81, Johanna Lorenz
User: b2fa93ac-19a0-499b-b1b6-afa76c44a301, Joni Sherman
User: 01db13c5-74fc-470a-8e45-d6d736f8a35b, Jordan Miller
User: fb0b8363-4126-4c34-8185-c998ff697a60, Lee Gu
User: ee75e249-a4c1-487b-a03a-5a170c2aa33f, Lidia Holloway
User: 5449bd61-cc63-40b9-b0a8-e83720eeefba, Lynne Robbins
User: 7ce295c3-25fa-4d79-8122-9a87d15e2438, Miriam Graham
User: 737fe0a7-0b67-47dc-b7a6-9cfc07870705, Nestor Wilke
User: a1572b58-35cd-41a0-804a-732bd978df3e, Patti Fernandez
User: 7275e1c4-5698-446c-8d1d-fa8b0503c78a, Pradeep Gupta
User: 96ab25eb-6b69-4481-9d28-7b01cf367170, Megan Bowen
User: 846327fa-e6d6-4a82-89ad-5fd313bff0cc, Alex Wilber
User: 200e4c7a-b778-436c-8690-7a6398e5fe6e, MOD Administrator
User: 7a7fded6-0269-42c2-a0be-512d58da4463, Adele Vance
User: 752f0102-90f2-4b8d-ae98-79dee995e35e,   Removed?:deleted
User: 4887248a-6b48-4ba5-bdd5-fed89d8ea6a0,   Removed?:deleted
User: e538b2d5-6481-4a90-a20a-21ad55ce4c1d,   Removed?:deleted
User: bc5994d9-4404-4a14-8fb0-46b8dccca0ad,   Removed?:deleted
User: d4e3a3e0-72e9-41a6-9538-c23e10a16122,   Removed?:deleted
Got deltalink
```

<span data-ttu-id="7efe6-122">En el portal de administración de usuarios vuelva a editar el usuario y **guárdelo** con otro número de teléfono móvil.</span><span class="sxs-lookup"><span data-stu-id="7efe6-122">In the user management portal edit the user again and **Save** again using a different mobile phone number.</span></span>

<span data-ttu-id="7efe6-123">La aplicación recibirá otra notificación y volverá a consultar el gráfico con el último vínculo Delta que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="7efe6-123">The application will receive another notification and will query the graph again using the last delta link it received.</span></span> <span data-ttu-id="7efe6-124">Sin embargo, en esta ocasión verá que solo el usuario modificado se ha devuelto en los resultados.</span><span class="sxs-lookup"><span data-stu-id="7efe6-124">However, this time you will notice that only the modified user was returned in the results.</span></span>

```shell
User: 7a7fded6-0269-42c2-a0be-512d58da4463, Adele Vance
```

<span data-ttu-id="7efe6-125">Con esta combinación de notificaciones con la consulta de Delta puede estar seguro de que no perderá ninguna actualización a un recurso.</span><span class="sxs-lookup"><span data-stu-id="7efe6-125">Using this combination of notifications with delta query you can be assured you wont miss any updates to a resource.</span></span> <span data-ttu-id="7efe6-126">Las notificaciones pueden perderse debido a problemas de conexión temporales, pero la próxima vez que la aplicación obtenga una notificación, tomará todos los cambios desde la última consulta correcta.</span><span class="sxs-lookup"><span data-stu-id="7efe6-126">Notifications may be missed due to transient connection issues, however the next time your application gets a notification it will pick up all the changes since the last successful query.</span></span>
