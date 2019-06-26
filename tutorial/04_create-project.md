<!-- markdownlint-disable MD002 MD041 -->

Abra el símbolo del sistema, vaya a un directorio donde tenga permisos para crear su proyecto y ejecute el siguiente comando para crear una nueva aplicación de .NET Core WebApi:

```shell
dotnet new webapi -o msgraphapp
```

Después de crear la aplicación, ejecute los siguientes comandos para asegurarse de que el nuevo proyecto se ejecute correctamente.

  ```shell
  cd msgraphapp
  dotnet add package Microsoft.Identity.Client
  dotnet add package Microsoft.Graph
  dotnet run
  ```

  La aplicación se iniciará y dará como resultado lo siguiente:

  ```shell
  info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0] ...
  info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[58] ...
  warn: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[35] ...
  info: Microsoft.AspNetCore.DataProtection.Repositories.FileSystemXmlRepository[39] ...
  Hosting environment: Development
  Content root path: /Users/ac/_play/graphchangenotifications/msgraphapp
  Now listening on: https://localhost:5001
  Now listening on: http://localhost:5000
  Application started. Press Ctrl+C to shut down.
  ```

Detenga la aplicación que se está ejecutando presionando <kbd>Ctrl</kbd>+<kbd>C</kbd>.

Abra la aplicación en Visual Studio Code usando el siguiente comando:

```shell
code .
```

Si Visual Studio Code muestra un cuadro de diálogo que le pregunta si desea agregar los activos necesarios al proyecto, seleccione **sí**.
