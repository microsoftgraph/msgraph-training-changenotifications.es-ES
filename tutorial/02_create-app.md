<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="05abd-101">En este ejercicio, creará un nuevo registro de aplicaciones Web de Azure AD con el centro de administración de Azure Active Directory y otorgará el consentimiento del administrador a los ámbitos de permiso necesarios.</span><span class="sxs-lookup"><span data-stu-id="05abd-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center and grant administrator consent to the required permission scopes.</span></span>

1. <span data-ttu-id="05abd-102">Abra un explorador y vaya al [centro de administración de Azure Active Directory](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05abd-102">Open a browser and navigate to the [Azure Active Directory admin center](https://portal.azure.com).</span></span> <span data-ttu-id="05abd-103">Inicie sesión con una **cuenta profesional o educativa**.</span><span class="sxs-lookup"><span data-stu-id="05abd-103">Login using a **Work or School Account**.</span></span>

1. <span data-ttu-id="05abd-104">Seleccione **Azure Active Directory** en el panel de navegación izquierdo y seleccione **Registros de aplicaciones (versión preliminar)** en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="05abd-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations (Preview)** under **Manage**.</span></span>

    ![<span data-ttu-id="05abd-105">Una captura de pantalla de los registros de la aplicación</span><span class="sxs-lookup"><span data-stu-id="05abd-105">A screenshot of the App registrations</span></span> ](./images/01.png)

1. <span data-ttu-id="05abd-106">Seleccione **Nuevo registro**.</span><span class="sxs-lookup"><span data-stu-id="05abd-106">Select **New registration**.</span></span> <span data-ttu-id="05abd-107">En la página **Registrar una aplicación**, establezca los valores siguientes.</span><span class="sxs-lookup"><span data-stu-id="05abd-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="05abd-108">Establezca **Nombre** como `GraphNotificationTutorial`.</span><span class="sxs-lookup"><span data-stu-id="05abd-108">Set **Name** to `GraphNotificationTutorial`.</span></span>
    - <span data-ttu-id="05abd-109">Establezca **Tipos de cuenta admitidos** en **Cuentas en cualquier directorio de organización y cuentas personales de Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="05abd-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="05abd-110">En **URI de redirección**, establezca la primera lista desplegable en `Web` y establezca el valor `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="05abd-110">Under **Redirect URI**, set the first drop-down to `Web` and set the value to `http://localhost`.</span></span>

    ![Captura de pantalla de la página registrar una aplicación](./images/02.png)

1. <span data-ttu-id="05abd-112">Seleccione **registrar**.</span><span class="sxs-lookup"><span data-stu-id="05abd-112">Select **Register**.</span></span> <span data-ttu-id="05abd-113">En la página **GraphNotificationTutorial** , copie el valor del identificador de la **aplicación (cliente)** y el **identificador del directorio (tenant)** guárdelos, los necesitará en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="05abd-113">On the **GraphNotificationTutorial** page, copy the value of the **Application (client) ID** and **Directory (tenant) ID** save it, you will need them in the next step.</span></span>

    ![Captura de pantalla del identificador de la aplicación del nuevo registro de la aplicación](./images/03.png)

1. <span data-ttu-id="05abd-115">Seleccione **Certificados y secretos** en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="05abd-115">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="05abd-116">Seleccione **nuevo secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="05abd-116">Select **New client secret**.</span></span> <span data-ttu-id="05abd-117">Escriba un valor en **Descripción** y seleccione una de las opciones para **Expires** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="05abd-117">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

    ![Captura de pantalla del cuadro de diálogo Agregar un secreto de cliente](./images/04.png)

1. <span data-ttu-id="05abd-119">Copie el valor del secreto de cliente antes de salir de esta página.</span><span class="sxs-lookup"><span data-stu-id="05abd-119">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="05abd-120">Lo necesitará en el siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="05abd-120">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="05abd-121">El secreto de cliente no se vuelve a mostrar, así que asegúrese de copiarlo en este momento.</span><span class="sxs-lookup"><span data-stu-id="05abd-121">This client secret is never shown again, so make sure you copy it now.</span></span>

    ![Captura de pantalla del secreto de cliente recién agregado](./images/05.png)

1. <span data-ttu-id="05abd-123">Seleccione **permisos de API** en **administrar**.</span><span class="sxs-lookup"><span data-stu-id="05abd-123">Select **API Permissions** under **Manage**.</span></span> <span data-ttu-id="05abd-124">**Agregue un permiso** y seleccione **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="05abd-124">**Add a permission** and select **Microsoft Graph**.</span></span> <span data-ttu-id="05abd-125">Seleccione **permiso de aplicación** y expanda **usuario** y seleccione el ámbito **User. ReadWrite. All** .</span><span class="sxs-lookup"><span data-stu-id="05abd-125">Select **Application Permission** and expand **User** and select the **User.ReadWrite.All** scope.</span></span> <span data-ttu-id="05abd-126">Seleccione **Agregar permisos** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="05abd-126">Select **Add permissions** to save your changes.</span></span>

    ![Captura de pantalla del secreto de cliente recién agregado](./images/06.png)

<span data-ttu-id="05abd-128">La aplicación solicita un permiso de aplicación con el ámbito **User. ReadWrite. All** .</span><span class="sxs-lookup"><span data-stu-id="05abd-128">The application requests an application permission with the **User.ReadWrite.All** scope.</span></span> <span data-ttu-id="05abd-129">Este permiso requiere consentimiento administrativo.</span><span class="sxs-lookup"><span data-stu-id="05abd-129">This permission requires administrative consent.</span></span>

<span data-ttu-id="05abd-130">Seleccione **conceder consentimiento de administrador para contoso** y, a continuación, seleccione **sí** para aceptar el consentimiento de esta aplicación y conceder a la aplicación acceso a su inquilino mediante los ámbitos especificados.</span><span class="sxs-lookup"><span data-stu-id="05abd-130">Select **Grant admin consent for Contoso** and then select **Yes** to consent this application and grant the application access to your tenant using the scopes you specified.</span></span>

![Captura de pantalla de inicio de sesión](./images/07.png)
