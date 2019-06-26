<!-- markdownlint-disable MD002 MD041 -->

Para que Microsoft Graph envíe notificaciones a la aplicación que se ejecuta en el equipo de desarrollo, debe usar una herramienta como ngrok para realizar el túnel de llamadas desde Internet a su equipo de desarrollo. Ngrok permite que las llamadas desde Internet se dirijan a la aplicación que se ejecuta localmente sin necesidad de crear reglas de Firewall.

Antes de continuar, debe tener [ngrok](https://ngrok.com) instalado en el equipo de desarrollo. Si no tiene ngrok, visite el vínculo anterior para ver las opciones de descarga e instrucciones.

Ejecute ngrok ejecutando lo siguiente desde la línea de comandos:

```shell
ngrok http 5000
```

Se iniciará ngrok y se realizará un túnel de las solicitudes de una dirección URL de ngrok externa a su equipo de desarrollo en el puerto 5000.

Copie la dirección de reenvío https. En el ejemplo siguiente sería `https://787b8292.ngrok.io`. Lo necesitará más adelante.

> [!IMPORTANT]
> Cada vez que se reinicie ngrok, se generará una nueva dirección y tendrá que volver a copiarla.

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
