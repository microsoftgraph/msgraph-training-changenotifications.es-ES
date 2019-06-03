<!-- markdownlint-disable MD002 MD041 -->

Las suscripciones de las notificaciones expiran y deben renovarse de forma periódica.

Abra **NotificationsController.CS** y reemplace el `Get()` método con el código siguiente:

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

Agregue la siguiente instrucción using en la parte superior del archivo.

```csharp
using System.Threading;
```

Este código anterior agrega un temporizador en segundo plano que se activará cada 15 segundos y comprobará las suscripciones para ver si han expirado.

Agregue los siguientes métodos nuevos:

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

El `CheckSubscriptions` temporizador llama al método cada 15 segundos. Para el uso de producción, debe establecerse en un valor más razonable para reducir el número de llamadas innecesarias a Graph. El `RenewSubscription` método renueva una suscripción y solo se llama si una suscripción va a expirar en los próximos dos minutos.

Seleccione **Depurar > iniciar** depuración para ejecutar la aplicación. Navegue a la siguiente dirección `*http://localhost:5000/api/notifications` URL para registrar una nueva suscripción.

Verá el siguiente resultado en la `DEBUG OUTPUT` ventana de Visual Studio Code aproximadamente cada 15 segundos.  Este es el temporizador que comprueba la suscripción para la expiración.

```shell
Checking subscriptions 12:32:51.882
Current subscription count 1
```

Espere unos minutos y verá lo siguiente cuando sea necesario renovar la suscripción:

```shell
Renewed subscription: 07ca62cd-1a1b-453c-be7b-4d196b3c6b5b, New Expiration: 3/10/2019 7:43:22 PM +00:00
```

Esto indica que la suscripción se renovó y muestra la nueva hora de expiración.
