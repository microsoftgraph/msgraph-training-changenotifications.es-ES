<!-- markdownlint-disable MD002 MD041 -->

Cree una configuración de inicio para depurar la aplicación en Visual Studio Code.

En Visual Studio Code, seleccione **Depurar > las configuraciones abiertas**.

  ![Screencast de VS código abrir configuraciones de lanzamiento](./images/vscode-debugapp-01.png)

Cuando se le pida que seleccione un entorno, seleccione **.net Core**.

  ![Screencast de VS Code Creating a Launch Configuration for .NET Core](./images/vscode-debugapp-02.png)

> [!NOTE]
> De forma predeterminada, la configuración de inicio principal de .NET abrirá un explorador y se desplazará a la dirección URL predeterminada de la aplicación cuando inicie el depurador. Para esta aplicación, en su lugar queremos navegar a la dirección URL NGrok. Si deja la configuración de lanzamiento como está, cada vez que depure la aplicación se mostrará una página rota. Solo puede cambiar la dirección URL o cambiar la configuración de inicio para que no inicie el explorador:

Actualice la configuración del inicio del depurador de Visual Studio:

  1. En Visual Studio Code, abra el archivo **. vscode/Launch. JSON**.
  1. Busque la siguiente sección en la configuración predeterminada:

      ```json
      "launchBrowser": {
        "enabled": true
      },
      ```

  1. Establezca la `enabled` propiedad en `false`.
  1. Guarde los cambios.

### <a name="test-the-application"></a>Pruebe la aplicación:

En Visual Studio Code, seleccione **Depurar > iniciar** depuración para ejecutar la aplicación. VS Code generará y pondrá en estrella la aplicación.

Una vez que vea lo siguiente en la ventana de la **consola** de depuración...

![Captura de pantalla de la consola de depuración de código de VS](./images/vscode-debugapp-03.png)

... Abra un explorador y vaya a **http://localhost:5000/api/notifications** para suscribirse a las notificaciones de cambios. Si se ejecuta correctamente, verá el resultado que incluye un identificador de suscripción como el que se muestra a continuación:

![Captura de pantalla de una suscripción correcta](./images/vscode-debugapp-04.png)

La aplicación ahora está suscrita para recibir notificaciones de Microsoft Graph cuando se realiza una actualización en los usuarios en el inquilino de Office 365.

Desencadenar una notificación:

1. Abra un explorador y vaya al [centro de administración de Microsoft 365https://admin.microsoft.com/AdminPortal)(](https://admin.microsoft.com/AdminPortal).
1. Si se le pide que inicie sesión, inicie sesión con una cuenta de administrador.
1. Seleccione **usuarios > usuarios activos**.

    ![Captura de pantalla del centro de administración de Microsoft 365](./images/vscode-debugapp-05.png)

1. Seleccione un usuario activo y seleccione **Editar** en su **información de contacto**.

    ![Captura de pantalla de los detalles de un usuario](./images/vscode-debugapp-06.png)

1. Actualice el valor del **número de teléfono** con un número nuevo y seleccione **Guardar**.

    En la **consola**de depuración de Visual Studio Code, verá que se ha recibido una notificación. A veces, esto puede tardar unos minutos en llegar. A continuación se muestra un ejemplo del resultado:

    ```shell
    Received notification: 'Users/7a7fded6-0269-42c2-a0be-512d58da4463', 7a7fded6-0269-42c2-a0be-512d58da4463
    ```

Esto indica que la aplicación recibió correctamente la notificación de Microsoft Graph para el usuario especificado en el resultado. A continuación, puede usar esta información para consultar a Microsoft Graph para ver los detalles completos de los usuarios si desea sincronizar sus detalles con la aplicación.