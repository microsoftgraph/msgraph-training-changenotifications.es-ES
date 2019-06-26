<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="56c47-101">Abra el símbolo del sistema, vaya a un directorio donde tenga permisos para crear su proyecto y ejecute el siguiente comando para crear una nueva aplicación de .NET Core WebApi:</span><span class="sxs-lookup"><span data-stu-id="56c47-101">Open your command prompt, navigate to a directory where you have rights to create your project, and run the following command to create a new .NET Core WebApi app:</span></span>

```shell
dotnet new webapi -o msgraphapp
```

<span data-ttu-id="56c47-102">Después de crear la aplicación, ejecute los siguientes comandos para asegurarse de que el nuevo proyecto se ejecute correctamente.</span><span class="sxs-lookup"><span data-stu-id="56c47-102">After creating the application, run the following commands to ensure your new project runs correctly.</span></span>

  ```shell
  cd msgraphapp
  dotnet add package Microsoft.Identity.Client
  dotnet add package Microsoft.Graph
  dotnet run
  ```

  <span data-ttu-id="56c47-103">La aplicación se iniciará y dará como resultado lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="56c47-103">The application will start and output the following:</span></span>

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

<span data-ttu-id="56c47-104">Detenga la aplicación que se está ejecutando presionando <kbd>Ctrl</kbd>+<kbd>C</kbd>.</span><span class="sxs-lookup"><span data-stu-id="56c47-104">Stop the application running by pressing <kbd>CTRL</kbd>+<kbd>C</kbd>.</span></span>

<span data-ttu-id="56c47-105">Abra la aplicación en Visual Studio Code usando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="56c47-105">Open the application in Visual Studio Code using the following command:</span></span>

```shell
code .
```

<span data-ttu-id="56c47-106">Si Visual Studio Code muestra un cuadro de diálogo que le pregunta si desea agregar los activos necesarios al proyecto, seleccione **sí**.</span><span class="sxs-lookup"><span data-stu-id="56c47-106">If Visual Studio code displays a dialog box asking if you want to add required assets to the project, select **Yes**.</span></span>
