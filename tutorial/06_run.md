<!-- markdownlint-disable MD002 MD041 -->

Seleccione **Depurar > iniciar** depuración para ejecutar la aplicación. Después de compilar la aplicación, se abrirá una ventana del explorador en una página de 404. Esto es correcto porque nuestra aplicación es una API y no una página web.

Para suscribirse a las notificaciones de cambios para los usuarios, `http://localhost:5000/api/notifications`navegue a la siguiente dirección URL. Si se ejecuta correctamente, verá el resultado que incluye un identificador de suscripción como el que se muestra a continuación:

```shell
Subscribed. Id: e2dbfbe1-160b-42b0-9b9f-8ab79bf8dfed
```

La aplicación ahora está suscrita para recibir notificaciones de Microsoft Graph cuando se realiza una actualización en los usuarios en el inquilino de Office 365.

Abra un explorador y visite el [centro de administración de Microsoft 365](https://admin.microsoft.com/AdminPortal). Inicie sesión con una cuenta de administrador. Seleccione **usuarios > usuarios activos**. Seleccione un usuario activo y seleccione **Editar** en su **información de contacto**. Actualice el valor del **teléfono móvil** con un número nuevo y seleccione **Guardar**.

![Captura de pantalla de los detalles del usuario](./images/03.png)

En la **consola** de depuración de Visual Studio verá que se ha recibido una notificación. A veces, esto puede tardar unos minutos en llegar. A continuación se muestra un ejemplo del resultado:

```shell
Received notification: 'Users/7a7fded6-0269-42c2-a0be-512d58da4463', 7a7fded6-0269-42c2-a0be-512d58da4463
```

Esto indica que la aplicación recibió correctamente la notificación de Microsoft Graph para el usuario especificado en el resultado. A continuación, puede usar esta información para consultar el gráfico para ver los detalles completos de los usuarios si desea sincronizar sus detalles en su aplicación.