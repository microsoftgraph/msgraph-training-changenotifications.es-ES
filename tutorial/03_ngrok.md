<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="636e8-101">Para que Microsoft Graph envíe notificaciones a la aplicación que se ejecuta en el equipo de desarrollo, debe usar una herramienta como ngrok para realizar el túnel de llamadas desde Internet a su equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="636e8-101">In order for the Microsoft Graph to send notifications to your application running on your development machine you need to use a tool such as ngrok to tunnel calls from the internet to your development machine.</span></span> <span data-ttu-id="636e8-102">Ngrok permite que las llamadas desde Internet se dirijan a la aplicación que se ejecuta localmente sin necesidad de crear reglas de Firewall.</span><span class="sxs-lookup"><span data-stu-id="636e8-102">Ngrok allows calls from the internet to be directed to your application running locally without needing to create firewall rules.</span></span>

<span data-ttu-id="636e8-103">Antes de continuar, debe tener [ngrok](https://ngrok.com) instalado en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="636e8-103">Before you continue you should have [ngrok](https://ngrok.com) installed on your development machine.</span></span> <span data-ttu-id="636e8-104">Si no tiene ngrok, visite el vínculo anterior para ver las opciones de descarga e instrucciones.</span><span class="sxs-lookup"><span data-stu-id="636e8-104">If you do not have ngrok, visit the previous link for download options and instructions.</span></span>

<span data-ttu-id="636e8-105">Ejecute ngrok ejecutando lo siguiente desde la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="636e8-105">Run ngrok by executing the following from the command line:</span></span>

```shell
ngrok http 5000
```

<span data-ttu-id="636e8-106">Se iniciará ngrok y se realizará un túnel de las solicitudes de una dirección URL de ngrok externa a su equipo de desarrollo en el puerto 5000.</span><span class="sxs-lookup"><span data-stu-id="636e8-106">This will start ngrok and will tunnel requests from an external ngrok url to your development machine on port 5000.</span></span>

<span data-ttu-id="636e8-107">Copie la dirección de reenvío https.</span><span class="sxs-lookup"><span data-stu-id="636e8-107">Copy the https forwarding address.</span></span> <span data-ttu-id="636e8-108">En el ejemplo siguiente sería `https://787b8292.ngrok.io`.</span><span class="sxs-lookup"><span data-stu-id="636e8-108">In the example below that would be `https://787b8292.ngrok.io`.</span></span> <span data-ttu-id="636e8-109">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="636e8-109">You will need this later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="636e8-110">Cada vez que se reinicie ngrok, se generará una nueva dirección y tendrá que volver a copiarla.</span><span class="sxs-lookup"><span data-stu-id="636e8-110">Each time ngrok is restarted a new address will be generated and you will need to copy it again.</span></span>

```shell
ngrok by @inconshreveable

Session Status                online
Account                       ???? ???? (Plan: Free)
Version                       2.3.15
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    http://787b8292.ngrok.io -> http://localhost:5000
Forwarding                    https://787b8292.ngrok.io -> http://localhost:5000

Connections                   ttl     opn     rt1     rt5     p50     p90
                              0       0       0.00    0.00    0.00    0.00
```
