<!-- markdownlint-disable MD002 MD041 -->

En este ejercicio, creará un nuevo registro de aplicaciones Web de Azure AD con el centro de administración de Azure Active Directory y otorgará el consentimiento del administrador a los ámbitos de permiso necesarios.

1. Abra un explorador y vaya al [centro de administración de Azure Active Directory](https://portal.azure.com). Inicie sesión con una **cuenta profesional o educativa**.

1. Seleccione **Azure Active Directory** en el panel de navegación izquierdo y seleccione **Registros de aplicaciones (versión preliminar)** en **Administrar**.

    ![Una captura de pantalla de los registros de la aplicación ](./images/01.png)

1. Seleccione **Nuevo registro**. En la página **Registrar una aplicación**, establezca los valores siguientes.

    - Establezca **Nombre** como `GraphNotificationTutorial`.
    - Establezca **Tipos de cuenta admitidos** en **Cuentas en cualquier directorio de organización y cuentas personales de Microsoft**.
    - En **URI de redirección**, establezca la primera lista desplegable en `Web` y establezca el valor `http://localhost`.

    ![Captura de pantalla de la página registrar una aplicación](./images/02.png)

1. Seleccione **registrar**. En la página **GraphNotificationTutorial** , copie el valor del identificador de la **aplicación (cliente)** y el **identificador del directorio (tenant)** guárdelos, los necesitará en el paso siguiente.

    ![Captura de pantalla del identificador de la aplicación del nuevo registro de la aplicación](./images/03.png)

1. Seleccione **Certificados y secretos** en **Administrar**. Seleccione **nuevo secreto de cliente**. Escriba un valor en **Descripción** y seleccione una de las opciones para **Expires** y seleccione **Agregar**.

    ![Captura de pantalla del cuadro de diálogo Agregar un secreto de cliente](./images/04.png)

1. Copie el valor del secreto de cliente antes de salir de esta página. Lo necesitará en el siguiente paso.

    > [!IMPORTANT]
    > El secreto de cliente no se vuelve a mostrar, así que asegúrese de copiarlo en este momento.

    ![Captura de pantalla del secreto de cliente recién agregado](./images/05.png)

1. Seleccione **permisos de API** en **administrar**. **Agregue un permiso** y seleccione **Microsoft Graph**. Seleccione **permiso de aplicación** y expanda **usuario** y seleccione el ámbito **User. ReadWrite. All** . Seleccione **Agregar permisos** para guardar los cambios.

    ![Captura de pantalla del secreto de cliente recién agregado](./images/06.png)

La aplicación solicita un permiso de aplicación con el ámbito **User. ReadWrite. All** . Este permiso requiere consentimiento administrativo.

Seleccione **conceder consentimiento de administrador para contoso** y, a continuación, seleccione **sí** para aceptar el consentimiento de esta aplicación y conceder a la aplicación acceso a su inquilino mediante los ámbitos especificados.

![Captura de pantalla de inicio de sesión](./images/07.png)
