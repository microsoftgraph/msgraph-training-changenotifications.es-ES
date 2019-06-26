<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="0869b-101">En este ejercicio, creará un nuevo registro de aplicaciones Web de Azure AD con el centro de administración de Azure Active Directory y otorgará el consentimiento del administrador a los ámbitos de permiso necesarios.</span><span class="sxs-lookup"><span data-stu-id="0869b-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center and grant administrator consent to the required permission scopes.</span></span>

1. <span data-ttu-id="0869b-102">Abra un explorador y vaya al [centro de administración de Azure Active Directoryhttps://aad.portal.azure.com)(](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0869b-102">Open a browser and navigate to the [Azure Active Directory admin center (https://aad.portal.azure.com)](https://aad.portal.azure.com).</span></span> <span data-ttu-id="0869b-103">Inicie sesión con una **cuenta profesional o educativa**.</span><span class="sxs-lookup"><span data-stu-id="0869b-103">Login using a **Work or School Account**.</span></span>

1. <span data-ttu-id="0869b-104">Seleccione **Azure Active Directory** en el panel de navegación de la izquierda y, después, seleccione **registros de aplicaciones** en **administrar**.</span><span class="sxs-lookup"><span data-stu-id="0869b-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![Captura de pantalla de los registros de aplicaciones](./images/aad-portal-home.png)

1. <span data-ttu-id="0869b-106">Seleccione **Nuevo registro**.</span><span class="sxs-lookup"><span data-stu-id="0869b-106">Select **New registration**.</span></span> <span data-ttu-id="0869b-107">En la página **registrar una aplicación**</span><span class="sxs-lookup"><span data-stu-id="0869b-107">On the **Register an application** page</span></span>

    ![Captura de pantalla de la página de registros de aplicaciones](./images/aad-portal-newapp.png)

    <span data-ttu-id="0869b-109">Establezca los valores de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="0869b-109">Set the values as follows:</span></span>

    - <span data-ttu-id="0869b-110">**Nombre**: GraphNotificationTutorial</span><span class="sxs-lookup"><span data-stu-id="0869b-110">**Name**: GraphNotificationTutorial</span></span>
    - <span data-ttu-id="0869b-111">**Tipos de cuenta compatibles**: cuentas de cualquier directorio de la organización y cuentas personales de Microsoft</span><span class="sxs-lookup"><span data-stu-id="0869b-111">**Supported account types**: Accounts in any organizational directory and personal Microsoft accounts</span></span>
    - <span data-ttu-id="0869b-112">**URI**de redireccionamiento: > Webhttp://localhost</span><span class="sxs-lookup"><span data-stu-id="0869b-112">**Redirect URI**: Web > http://localhost</span></span>

    ![Captura de pantalla de la página registrar una aplicación](./images/aad-portal-newapp-01.png)

    <span data-ttu-id="0869b-114">Seleccione **registrar**.</span><span class="sxs-lookup"><span data-stu-id="0869b-114">Select **Register**.</span></span>

1. <span data-ttu-id="0869b-115">En la página **GraphNotificationTutorial** , copie el valor del identificador de la **aplicación (cliente)** y el **identificador del directorio (tenant)** guárdelos, los necesitará en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="0869b-115">On the **GraphNotificationTutorial** page, copy the value of the **Application (client) ID** and **Directory (tenant) ID** save it, you will need them in the next step.</span></span>

    ![Captura de pantalla del identificador de aplicación del nuevo registro de la aplicación](./images/aad-portal-newapp-details.png)

1. <span data-ttu-id="0869b-117">Seleccione **administrar certificados de > & secretos**.</span><span class="sxs-lookup"><span data-stu-id="0869b-117">Select **Manage > Certificates & secrets**.</span></span> 

    <span data-ttu-id="0869b-118">Seleccione **nuevo secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="0869b-118">Select **New client secret**.</span></span>

    <span data-ttu-id="0869b-119">Escriba un valor en **Descripción** y seleccione una de las opciones para **Expires** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0869b-119">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

    ![Captura de pantalla del cuadro de diálogo Agregar un secreto de cliente](./images/aad-portal-newapp-secret.png)

    ![Captura de pantalla del cuadro de diálogo Agregar un secreto de cliente](./images/aad-portal-newapp-secret-02.png)

1. <span data-ttu-id="0869b-122">Copie el valor del secreto de cliente antes de salir de esta página.</span><span class="sxs-lookup"><span data-stu-id="0869b-122">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="0869b-123">Lo necesitará en el siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="0869b-123">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0869b-124">El secreto de cliente no se vuelve a mostrar, así que asegúrese de copiarlo en este momento.</span><span class="sxs-lookup"><span data-stu-id="0869b-124">This client secret is never shown again, so make sure you copy it now.</span></span>

    ![Captura de pantalla del secreto de cliente recién agregado](./images/aad-portal-newapp-secret-03.png)

1. <span data-ttu-id="0869b-126">Seleccione **administrar permisos**de la API de >.</span><span class="sxs-lookup"><span data-stu-id="0869b-126">Select **Manage > API Permissions**.</span></span>

    <span data-ttu-id="0869b-127">Seleccione **Agregar un permiso** y seleccione **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="0869b-127">Select **Add a permission** and select **Microsoft Graph**.</span></span>

    ![Captura de pantalla que selecciona el servicio Microsoft Graph](./images/aad-portal-newapp-graphscope.png)

    <span data-ttu-id="0869b-129">Seleccione **permiso de aplicación**, expanda el grupo de **usuarios** y seleccione **User. ReadWrite. All** Scope.</span><span class="sxs-lookup"><span data-stu-id="0869b-129">Select **Application Permission**, expand the **User** group and select **User.ReadWrite.All** scope.</span></span>

    <span data-ttu-id="0869b-130">Seleccione **Agregar permisos** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="0869b-130">Select **Add permissions** to save your changes.</span></span>

    ![Captura de pantalla que selecciona el ámbito de Microsoft Graph](./images/aad-portal-newapp-graphscope-02.png)

    ![Captura de pantalla del secreto de cliente recién agregado](./images/aad-portal-newapp-graphscope-03.png)

<span data-ttu-id="0869b-133">La aplicación solicita un permiso de aplicación con el ámbito **User. ReadWrite. All** .</span><span class="sxs-lookup"><span data-stu-id="0869b-133">The application requests an application permission with the **User.ReadWrite.All** scope.</span></span> <span data-ttu-id="0869b-134">Este permiso requiere consentimiento administrativo.</span><span class="sxs-lookup"><span data-stu-id="0869b-134">This permission requires administrative consent.</span></span>

<span data-ttu-id="0869b-135">Seleccione **conceder consentimiento de administrador para contoso**y, a continuación, seleccione **sí** para aceptar la aplicación y conceder a la aplicación acceso a su inquilino mediante los ámbitos especificados.</span><span class="sxs-lookup"><span data-stu-id="0869b-135">Select **Grant admin consent for Contoso**, then select **Yes** to consent this application and grant the application access to your tenant using the scopes you specified.</span></span>

![Captura de pantalla con consentimiento de administrador aprobado](./images/aad-portal-newapp-graphscope-04.png)
