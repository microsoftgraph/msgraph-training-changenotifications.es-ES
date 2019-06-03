<!-- markdownlint-disable MD002 MD041 -->

Este tutorial le enseña a crear una aplicación principal .NET que use la API de Microsoft Graph para recibir notificaciones (webhooks) cuando una cuenta de usuario cambia en Azure Active Directory (Azure AD) y realizar consultas mediante la API de consulta Delta para recibir todos los cambios al usuario. cuentas desde que se realizó la última consulta.

> [!TIP]
> Si prefiere descargar solo el tutorial completo, puede descargar o clonar el repositorio de [GitHub](https://github.com/microsoftgraph/msgraph-training-changenotifications).

## <a name="prerequisites"></a>Requisitos previos

Antes de iniciar este tutorial, debe tener instalado [.net Core 2,2 SDK](https://dotnet.microsoft.com/download) y [Visual Studio Code](https://code.visualstudio.com/) en el equipo de desarrollo. Si no están instalados, visite los vínculos anteriores de opciones de descarga.

> [!NOTE]
> Este tutorial se ha escrito con .NET Core versión 2,2. Los pasos de esta guía pueden funcionar con otras versiones, pero no se han probado.

## <a name="feedback"></a>Comentarios

Envíe sus comentarios sobre este tutorial en el [repositorio de github](https://github.com/microsoftgraph/msgraph-training-changenotifications).