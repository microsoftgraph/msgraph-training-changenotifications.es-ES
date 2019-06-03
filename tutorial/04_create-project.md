<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="78f1c-101">Abra el símbolo del sistema, vaya a un directorio donde tenga permisos para crear archivos y ejecute los siguientes comandos para crear una nueva aplicación de .NET Core WebApi.</span><span class="sxs-lookup"><span data-stu-id="78f1c-101">Open your command prompt, navigate to a directory where you have rights to create files, and run the following commands to create a new .NET Core WebApi app.</span></span>

```shell
dotnet new webapi -o msgraphapp
```

<span data-ttu-id="78f1c-102">Una vez que el comando finalice, ejecute los comandos siguientes para asegurarse de que el nuevo proyecto se ejecuta correctamente.</span><span class="sxs-lookup"><span data-stu-id="78f1c-102">Once the command finishes, run the following commands to ensure your new project runs correctly.</span></span>

```shell
cd msgraphapp
dotnet add package Microsoft.Identity.Client
dotnet add package Microsoft.Graph
dotnet run
```

<span data-ttu-id="78f1c-103">La aplicación se iniciará y se generará:</span><span class="sxs-lookup"><span data-stu-id="78f1c-103">The application will start and output:</span></span>

```shell
Now listening on: http://localhost:5000
```

<span data-ttu-id="78f1c-104">Si no ve este resultado o ve mensajes de error, es probable que haya un problema con el [SDK .net Core 2,2](https://dotnet.microsoft.com/download) instalado en el equipo de desarrollo que debe corregirse antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="78f1c-104">If you don't see this output, or you see error messages, there is likely a problem with the [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download) installed on your development machine that needs to be fixed before continuing.</span></span>

<span data-ttu-id="78f1c-105">Detenga la aplicación que se está ejecutando presionando <kbd>Ctrl</kbd>+<kbd>C</kbd>.</span><span class="sxs-lookup"><span data-stu-id="78f1c-105">Stop the application running by pressing <kbd>CTRL</kbd>+<kbd>C</kbd>.</span></span>

<span data-ttu-id="78f1c-106">Abra la aplicación en Visual Studio Code usando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="78f1c-106">Open the application in Visual Studio Code using the following command:</span></span>

```shell
code .
```

<span data-ttu-id="78f1c-107">Cuando un cuadro de diálogo le pregunte si desea agregar los activos necesarios al proyecto, seleccione **sí**.</span><span class="sxs-lookup"><span data-stu-id="78f1c-107">When a dialog box asks if you want to add required assets to the project, select **Yes**.</span></span>
