# <a name="microsoft-graph-training-module---using-change-notifications-and-track-changes-with-microsoft-graph"></a><span data-ttu-id="19a48-101">Módulo de aprendizaje de Microsoft Graph: uso de notificaciones de cambios y control de cambios con Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="19a48-101">Microsoft Graph Training Module - Using Change Notifications and Track Changes with Microsoft Graph</span></span>

<span data-ttu-id="19a48-102">Este módulo le presentará cómo trabajar con notificaciones de cambio (webhooks) & realizar un seguimiento de los cambios (consulta Delta) en Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="19a48-102">This module will introduce you to working with change notifications (webhooks) & track changes (delta query) in the Microsoft Graph.</span></span>

## <a name="lab---change-notifications-and-track-changes-with-the-microsoft-graph"></a><span data-ttu-id="19a48-103">Laboratorio: cambiar las notificaciones y realizar un seguimiento de los cambios con Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="19a48-103">Lab - Change Notifications and Track Changes with the Microsoft Graph</span></span>

<span data-ttu-id="19a48-104">En este laboratorio, creará una aplicación de consola principal de .NET que recibirá notificaciones de cambios de Microsoft Graph cuando se realice una actualización en una cuenta de usuario en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19a48-104">In this lab you will create a .NET Core console application that receives change notifications from the Microsoft Graph when an update is made to a users account in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="19a48-105">La aplicación administrará la suscripción de notificación de cambios y usará el control de cambios en Microsoft Graph para asegurarse de que no se pierden cambios.</span><span class="sxs-lookup"><span data-stu-id="19a48-105">The application will managed the Change Notification subscription and use Track Changes in the Microsoft Graph to ensure no changes are missed.</span></span>

- [<span data-ttu-id="19a48-106">Manual de laboratorio</span><span class="sxs-lookup"><span data-stu-id="19a48-106">Lab Manual</span></span>](./Lab.md)

## <a name="demos"></a><span data-ttu-id="19a48-107">Demostraciones</span><span class="sxs-lookup"><span data-stu-id="19a48-107">Demos</span></span>

- [<span data-ttu-id="19a48-108">Crear una aplicación .NET Core</span><span class="sxs-lookup"><span data-stu-id="19a48-108">Create a .NET Core app</span></span>](./demos/01-create-application)
- [<span data-ttu-id="19a48-109">Agregar ciclo de vida de suscripción</span><span class="sxs-lookup"><span data-stu-id="19a48-109">Add Subscription Lifecycle</span></span>](./demos/02-subscription-management)
- [<span data-ttu-id="19a48-110">Agregar control de cambios</span><span class="sxs-lookup"><span data-stu-id="19a48-110">Add Track Changes</span></span>](./demos/03-track-changes)

## <a name="watch-the-module"></a><span data-ttu-id="19a48-111">Ver el módulo</span><span class="sxs-lookup"><span data-stu-id="19a48-111">Watch the module</span></span>

<span data-ttu-id="19a48-112">Este módulo se ha registrado y está disponible en el canal de YouTube de desarrollo de Office: notificaciones de [cambios y seguimiento de cambios con Microsoft Graph](https://youtu.be/MvJ15BHTdHA)</span><span class="sxs-lookup"><span data-stu-id="19a48-112">This module has been recorded and is available in the Office Development YouTube channel: [Change Notifications and Track Changes with the Microsoft Graph](https://youtu.be/MvJ15BHTdHA)</span></span>

## <a name="contributors"></a><span data-ttu-id="19a48-113">Colaboradores</span><span class="sxs-lookup"><span data-stu-id="19a48-113">Contributors</span></span>

| <span data-ttu-id="19a48-114">Roles</span><span class="sxs-lookup"><span data-stu-id="19a48-114">Roles</span></span>                | <span data-ttu-id="19a48-115">Autores (es)</span><span class="sxs-lookup"><span data-stu-id="19a48-115">Author(s)</span></span>                                               |
| -------------------- | ------------------------------------------------------- |
| <span data-ttu-id="19a48-116">Manuales de laboratorio/diapositivas</span><span class="sxs-lookup"><span data-stu-id="19a48-116">Lab Manuals / Slides</span></span> | <span data-ttu-id="19a48-117">Andrew Connell (MVP de Microsoft, Voitanos) @andrewconnell</span><span class="sxs-lookup"><span data-stu-id="19a48-117">Andrew Connell (Microsoft MVP, Voitanos) @andrewconnell</span></span> |
| <span data-ttu-id="19a48-118">Patrocinador/soporte técnico</span><span class="sxs-lookup"><span data-stu-id="19a48-118">Sponsor / Support</span></span>    | <span data-ttu-id="19a48-119">Jeremy Thake (Microsoft) @jthake</span><span class="sxs-lookup"><span data-stu-id="19a48-119">Jeremy Thake (Microsoft) @jthake</span></span>                        |

## <a name="version-history"></a><span data-ttu-id="19a48-120">Historial de versiones</span><span class="sxs-lookup"><span data-stu-id="19a48-120">Version history</span></span>

| <span data-ttu-id="19a48-121">Versión</span><span class="sxs-lookup"><span data-stu-id="19a48-121">Version</span></span> | <span data-ttu-id="19a48-122">Fecha</span><span class="sxs-lookup"><span data-stu-id="19a48-122">Date</span></span>           | <span data-ttu-id="19a48-123">Comentarios</span><span class="sxs-lookup"><span data-stu-id="19a48-123">Comments</span></span>             |
| ------- | -------------- | -------------------- |
| <span data-ttu-id="19a48-124">1.1</span><span class="sxs-lookup"><span data-stu-id="19a48-124">1.1</span></span>     | <span data-ttu-id="19a48-125">9 de abril de 2019</span><span class="sxs-lookup"><span data-stu-id="19a48-125">April 9, 2019</span></span> | <span data-ttu-id="19a48-126">Vínculo de screencast agregado</span><span class="sxs-lookup"><span data-stu-id="19a48-126">Added screencast link</span></span> |
| <span data-ttu-id="19a48-127">1.0</span><span class="sxs-lookup"><span data-stu-id="19a48-127">1.0</span></span>     | <span data-ttu-id="19a48-128">14 de marzo de 2019</span><span class="sxs-lookup"><span data-stu-id="19a48-128">March 14, 2019</span></span> | <span data-ttu-id="19a48-129">Nuevo módulo enviado</span><span class="sxs-lookup"><span data-stu-id="19a48-129">New module submitted</span></span> |

## <a name="disclaimer"></a><span data-ttu-id="19a48-130">Aviso de declinación de responsabilidades</span><span class="sxs-lookup"><span data-stu-id="19a48-130">Disclaimer</span></span>

<span data-ttu-id="19a48-131">**Este código se proporciona _tal cual_ sin garantías de ningún tipo, ya sea expresa o implícita, incluidas las garantías implícitas de idoneidad para un fin determinado, comerciabilidad o ausencia de infracción.**</span><span class="sxs-lookup"><span data-stu-id="19a48-131">**THIS CODE IS PROVIDED _AS IS_ WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.**</span></span>

<img src="https://telemetry.sharepointpnp.com/msgraph-training-changenotifications" />
