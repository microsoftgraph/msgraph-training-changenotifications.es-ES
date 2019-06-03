<!-- markdownlint-disable MD002 MD041 -->

Abra el símbolo del sistema, vaya a un directorio donde tenga permisos para crear archivos y ejecute los siguientes comandos para crear una nueva aplicación de .NET Core WebApi.

```shell
dotnet new webapi -o msgraphapp
```

Una vez que el comando finalice, ejecute los comandos siguientes para asegurarse de que el nuevo proyecto se ejecuta correctamente.

```shell
cd msgraphapp
dotnet add package Microsoft.Identity.Client
dotnet add package Microsoft.Graph
dotnet run
```

La aplicación se iniciará y se generará:

```shell
Now listening on: http://localhost:5000
```

Si no ve este resultado o ve mensajes de error, es probable que haya un problema con el [SDK .net Core 2,2](https://dotnet.microsoft.com/download) instalado en el equipo de desarrollo que debe corregirse antes de continuar.

Detenga la aplicación que se está ejecutando presionando <kbd>Ctrl</kbd>+<kbd>C</kbd>.

Abra la aplicación en Visual Studio Code usando el siguiente comando:

```shell
code .
```

Cuando un cuadro de diálogo le pregunte si desea agregar los activos necesarios al proyecto, seleccione **sí**.
