<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="c7da3-101">Las suscripciones de las notificaciones expiran y deben renovarse de forma periódica.</span><span class="sxs-lookup"><span data-stu-id="c7da3-101">Subscriptions for notifications expire and need to be renewed periodically.</span></span>

<span data-ttu-id="c7da3-102">Abra **NotificationsController.CS** y reemplace el `Get()` método con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7da3-102">Open **NotificationsController.cs** and replace the `Get()` method with the following code:</span></span>

```csharp
private static Dictionary<string, Subscription> Subscriptions = new Dictionary<string, Subscription>();
private static Timer subscriptionTimer = null;

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

  Subscriptions[newSubscription.Id] = newSubscription;

  if(subscriptionTimer == null)
  {
      subscriptionTimer = new Timer(CheckSubscriptions, null, 5000, 15000);
  }

  return $"Subscribed. Id: {newSubscription.Id}, Expiration: {newSubscription.ExpirationDateTime}";
}
```

<span data-ttu-id="c7da3-103">Agregue la siguiente instrucción using en la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="c7da3-103">Add the following using statement at the top of the file.</span></span>

```csharp
using System.Threading;
```

<span data-ttu-id="c7da3-104">Este código anterior agrega un temporizador en segundo plano que se activará cada 15 segundos y comprobará las suscripciones para ver si han expirado.</span><span class="sxs-lookup"><span data-stu-id="c7da3-104">This code above adds a background timer that will fire every 15 seconds and check subscriptions to see if they have expired.</span></span>

<span data-ttu-id="c7da3-105">Agregue los siguientes métodos nuevos:</span><span class="sxs-lookup"><span data-stu-id="c7da3-105">Add the following new methods:</span></span>

```csharp
private void CheckSubscriptions(Object stateInfo)
{
  AutoResetEvent autoEvent = (AutoResetEvent)stateInfo;

  Console.WriteLine($"Checking subscriptions {DateTime.Now.ToString("h:mm:ss.fff")}");
  Console.WriteLine($"Current subscription count {Subscriptions.Count()}");

  foreach(var subscription in Subscriptions)
  {
    // if the subscription expires in the next 2 min, renew it
    if(subscription.Value.ExpirationDateTime < DateTime.UtcNow.AddMinutes(2))
    {
      RenewSubscription(subscription.Value);
    }
  }
}

private void RenewSubscription(Subscription subscription)
{
  Console.WriteLine($"Current subscription: {subscription.Id}, Expiration: {subscription.ExpirationDateTime}");

  var graphServiceClient = GetGraphClient();

  subscription.ExpirationDateTime = DateTime.UtcNow.AddMinutes(5);

  var foo = graphServiceClient
    .Subscriptions[subscription.Id]
    .Request()
    .UpdateAsync(subscription).Result;

  Console.WriteLine($"Renewed subscription: {subscription.Id}, New Expiration: {subscription.ExpirationDateTime}");
}
```

<span data-ttu-id="c7da3-106">El `CheckSubscriptions` temporizador llama al método cada 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="c7da3-106">The `CheckSubscriptions` method is called every 15 seconds by the timer.</span></span> <span data-ttu-id="c7da3-107">Para el uso de producción, debe establecerse en un valor más razonable para reducir el número de llamadas innecesarias a Graph.</span><span class="sxs-lookup"><span data-stu-id="c7da3-107">For production use this should be set to a more reasonable value to reduce the number of unnecessary calls to Graph.</span></span> <span data-ttu-id="c7da3-108">El `RenewSubscription` método renueva una suscripción y solo se llama si una suscripción va a expirar en los próximos dos minutos.</span><span class="sxs-lookup"><span data-stu-id="c7da3-108">The `RenewSubscription` method renews a subscription and is only called if a subscription is going to expire in the next two minutes.</span></span>

<span data-ttu-id="c7da3-109">Seleccione **Depurar > iniciar** depuración para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7da3-109">Select **Debug > Start debugging** to run the application.</span></span> <span data-ttu-id="c7da3-110">Navegue a la siguiente dirección `*http://localhost:5000/api/notifications` URL para registrar una nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="c7da3-110">Navigate to the following url `*http://localhost:5000/api/notifications` to register a new subscription.</span></span>

<span data-ttu-id="c7da3-111">Verá el siguiente resultado en la `DEBUG OUTPUT` ventana de Visual Studio Code aproximadamente cada 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="c7da3-111">You will see the following output in the `DEBUG OUTPUT` window of Visual Studio Code approximately every 15 seconds.</span></span>  <span data-ttu-id="c7da3-112">Este es el temporizador que comprueba la suscripción para la expiración.</span><span class="sxs-lookup"><span data-stu-id="c7da3-112">This is the timer checking the subscription for expiry.</span></span>

```shell
Checking subscriptions 12:32:51.882
Current subscription count 1
```

<span data-ttu-id="c7da3-113">Espere unos minutos y verá lo siguiente cuando sea necesario renovar la suscripción:</span><span class="sxs-lookup"><span data-stu-id="c7da3-113">Wait a few minutes and you will see the following when the subscription needs renewing:</span></span>

```shell
Renewed subscription: 07ca62cd-1a1b-453c-be7b-4d196b3c6b5b, New Expiration: 3/10/2019 7:43:22 PM +00:00
```

<span data-ttu-id="c7da3-114">Esto indica que la suscripción se renovó y muestra la nueva hora de expiración.</span><span class="sxs-lookup"><span data-stu-id="c7da3-114">This indicates that the subscription was renewed and shows the new expiry time.</span></span>
