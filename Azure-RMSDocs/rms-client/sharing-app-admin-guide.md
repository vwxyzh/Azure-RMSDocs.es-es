---
title: "Guía del administrador de la aplicación Microsoft Rights Management sharing | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/05/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7cf74355aa39928fd66a4be13a9b65428da7480
ms.openlocfilehash: 08226cd930f90bc7c9cda4c65315ee6472fbcf52


---


# Guía de administrador de la aplicación de uso compartido Rights Management

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*


Use la siguiente información si es responsable de la aplicación Microsoft Rights Management sharing en una red de empresa, o si desea más información técnica que la que aparece en [Manual del usuario de la aplicación Rights Management sharing](sharing-app-user-guide.md) o en [FAQ for Microsoft Rights Management Sharing Application for Windows](http://go.microsoft.com/fwlink/?LinkId=303971) (Preguntas más frecuentes sobre la aplicación Microsoft Rights Management sharing para Windows):

La aplicación RMS resulta más adecuada para trabajar con Azure RMS, puesto que esta configuración de implementación admite el envío de datos adjuntos protegidos a los usuarios de otra organización, así como opciones tales como notificaciones por correo electrónico y seguimiento de documentos con revocación.  Sin embargo, también funciona con la versión local, AD RMS, pero con algunas limitaciones. Para ver una comparación exhaustiva de las características que son compatibles con Azure RMS y AD RMS, consulte [Comparación entre Azure Rights Management y AD RMS](../understand-explore/compare-azure-rms-ad-rms.md). Si tiene AD RMS y quiere migrar a Azure RMS, consulte [Migración desde AD RMS a Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

Para obtener información técnica general sobre la aplicación Rights Management sharing, información sobre la protección nativa y genérica, los tipos de archivo compatibles, las extensiones de nombres de archivo y sobre cómo cambiar el nivel de protección predeterminado, vea [Información general técnica de la aplicación Microsoft Rights Management sharing](sharing-app-admin-guide-technical.md). 

## Implementación automática de la aplicación Microsoft Rights Management sharing
La versión de Windows de la aplicación RMS sharing admite una instalación con scripts, lo que la convierte en adecuada para las implementaciones empresariales.

Los únicos requisitos previos para las instalaciones son que los equipos ejecuten una versión mínima de Windows 7 Service Pack 1 y que esté instalado Microsoft Framework, versión mínima 4.0. Si necesita instalar Microsoft .NET Framework 4.0, puede [descargarlo para la instalación desde el Centro de descarga de Microsoft](http://www.microsoft.com/download/details.aspx?id=17718).

### Para descargar la aplicación RMS sharing para la implementación automática

1.  Vaya a la página [Aplicación Microsoft Rights Management sharing para Windows](http://www.microsoft.com/download/details.aspx?id=40857) en el Centro de descarga de Microsoft y haga clic en **Descargar**.

2.  Seleccione y descargue los archivos que necesita. Hay dos paquetes de instalación del cliente: uno para Windows de 64 bits (Microsoft Rights Management sharing application x64.zip) y otro para Windows de 32 bits (Microsoft Rights Management sharing application x86.zip).

3.  Extraiga los archivos de los paquetes de instalación comprimidos, por ejemplo, haciendo doble clic en ellos. A continuación, copie los archivos extraídos en una ubicación de red a la que puedan tener acceso los equipos cliente.

Los paquetes de instalación de la aplicación RMS sharing admiten distintos escenarios de implementación e incluyen lo siguiente:

|Descripción|Escenario de implementación|
|---------------|-----------------------|
|Microsoft Online Services - Ayudante para el inicio de sesión|Office 2010 y Azure RMS<br /><br />Office 2013 y Azure RMS si no ha instalado la [actualización del 9 de junio de 2015 para Office 2013](https://support.microsoft.com/kb/3054853) (KB3054853)|
|Revisión para Office (KB 2596501)|Office 2010 y Azure RMS<br /><br />Office 2010 y Active Directory RMS|
|Revisión para permitir que el cliente de AD RMS 1.0 funcione con Azure RMS (KB 2843630 KB)|Office 2010 y Azure RMS<br /><br />Office 2010 y Active Directory RMS|
|El cliente de AD RMS y la aplicación RMS sharing|Office 2016 u Office 2013 y Azure RMS o Active Directory RMS<br /><br />Office 2010 y Azure RMS<br /><br />Office 2010 y Active Directory RMS<br /><br />Aplicación RMS sharing y solo el complemento de Office|
|Complemento de Office para la cinta de opciones|Office 2016 u Office 2013 y Azure RMS o Active Directory RMS<br /><br />Office 2010 y Azure RMS<br /><br />Office 2010 y Active Directory RMS<br /><br />Aplicación RMS sharing y solo el complemento de Office|
|Herramienta de preparación de Azure Active Directory Rights Management|Office 2010 y Azure RMS|
Use los siguientes procedimientos para identificar los comandos necesarios para implementar la aplicación RMS sharing en estos escenarios de implementación:

-   **Office 2016 u Office 2013 y Azure RMS o Active Directory RMS**

    Los usuarios ejecutan Office 2016 u Office 2013, su organización usa Azure RMS o Active Directory RMS y los usuarios colaborar con otras organizaciones que usan Azure RMS o Active Directory RMS.

-   **Office 2010 y Azure RMS**

    Los usuarios ejecutan Office 2010, su organización usa Azure RMS o Active Directory RMS y los usuarios colaboran con otras organizaciones que usan Azure RMS o Active Directory RMS.

-   **Office 2010 y Active Directory RMS**

    Los usuarios ejecutan Office 2010, su organización usa Azure RMS o Active Directory RMS y los usuarios colaboran con otras organizaciones que usan Azure RMS o Active Directory RMS.

-   **Aplicación RMS sharing y solo el complemento de Office**

    Los usuarios ejecutan Office 2016, Office 2013 u Office 2010, su organización usa Azure RMS o Active Directory RMS y los usuarios no necesitan colaboran con otras organizaciones que usan Azure RMS. Esta instalación le permite instalar solamente la aplicación de uso compartido y el complemento de Office.

> [!NOTE]
> En estos casos, si su organización ejecuta AD RMS, los usuarios pueden recibir contenido protegido de otras organizaciones que usan Azure RMS, pero los usuarios no pueden enviar contenido protegido a los usuarios de una organización que usa Azure RMS. Sin embargo, si su organización ejecuta Azure RMS, los usuarios pueden enviar y recibir contenido protegido de otras organizaciones.

Para completar la instalación de cada procedimiento, debe reiniciar el equipo. Puede iniciar un reinicio automático con un comando como **shutdown /i**.

### Para implementar la aplicación RMS sharing para Office 2016 u Office 2013 y Azure RMS o Active Directory RMS

-   En cada equipo en el que quiera instalar la aplicación RMS sharing y los componentes relacionados, ejecute el siguiente comando con privilegios elevados:

    ```
    setup.exe /s
    ```

Para comprobar que la instalación se realizó correctamente, consulte la sección [Comprobación de que la instalación se ha realizado correctamente](#verifying-installation-success) de este artículo.

### Para implementar la aplicación RMS sharing para Office 2010 y Azure RMS

1.  Debe ser el administrador global del inquilino de Office 365 o Azure Active Directory para poder obtener la dirección URL del servicio de certificación de su organización mediante la ejecución de la herramienta de preparación Azure Active Directory Rights Management. Debe ejecutar esta herramienta solo una vez, en un único equipo. Usará la dirección URL del servicio de certificación al instalar la aplicación RMS sharing en cada equipo:

    1.  Inicie sesión un equipo con una cuenta de administrador local.

    2.  En ese equipo, [descargue e instale el Ayudante para el inicio de sesión de Microsoft Online](http://www.microsoft.com/download/details.aspx?id=28177).

    3.  Ejecute el siguiente comando para mostrar en la pantalla la dirección URL del servicio de certificación, que luego puede copiar y guardar para el siguiente paso:

        -   Para Windows 8.1 y Windows 8, 64 bits:

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Para Windows 8.1 y Windows 8, 32 bits:

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Para Windows 7, 64 bits:

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > Este comando podría solicitarle que especifique sus credenciales de Azure. Si el equipo no está unido a un dominio, se le pedirán. Si el equipo está unido a un dominio, es posible que la herramienta pueda usar las credenciales almacenadas en caché.

2.  En cada equipo en el que vaya a instalar la aplicación RMS sharing, ejecute el siguiente comando una vez con privilegios elevados:

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  En cada uno de los equipos en que vaya a instalar la aplicación RMS sharing, todos aquellos que los utilicen deben ejecutar el siguiente comando (no necesita privilegios elevados). Esto se puede hacer de diferentes maneras, como por ejemplo, pedir al usuario que ejecute el comando (desde un vínculo en un mensaje de correo electrónico o un vínculo en el portal del servicio de asistencia), o bien puede agregarlo a su script de inicio de sesión:

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

Para comprobar que la instalación se realizó correctamente, consulte la sección [Comprobación de que la instalación se ha realizado correctamente](#verifying-installation-success) de este artículo.

### Para implementar la aplicación RMS sharing para Office 2010 y Active Directory RMS

1.  En cada equipo en el que vaya a instalar la aplicación RMS sharing y los componentes relacionados, ejecute el siguiente comando con privilegios elevados:

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  En cada equipo en el que vaya a instalar la aplicación RMS sharing y los componentes relacionados, ejecute el siguiente comando (no necesita privilegios elevados). Esto se puede hacer de diferentes maneras, como por ejemplo, pedir al usuario que ejecute el comando (desde un vínculo en un mensaje de correo electrónico o un vínculo en el portal del servicio de asistencia), o bien puede agregarlo a su script de inicio de sesión:

    -   Para Windows 10, Windows 8.1 y Windows 8, 64 bits:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   Para Windows 10, Windows 8.1 y Windows 8, 32 bits:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   Para Windows 7, 64 bits:

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

Para comprobar que la instalación se realizó correctamente, consulte la sección [Comprobación de que la instalación se ha realizado correctamente](#verifying-installation-success) de este artículo.

### Para instalar la aplicación RMS sharing y solo el complemento de Office

1.  Instale el cliente de AD RMS y la aplicación RMS sharing mediante el siguiente comando:

    -   Para Windows de 64 bits:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   Para Windows de 32 bits:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    Por ejemplo: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Instale el complemento para Office con los siguientes comandos:

    -   Para la versión de 64 bits de Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   Para la versión de 32 bits de Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    Por ejemplo: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

Para comprobar que la instalación se realizó correctamente, consulte la sección [Comprobación de que la instalación se ha realizado correctamente](#verifying-installation-success) de este artículo.

## Comprobación de que la instalación se ha realizado correctamente
Puede usar los archivos de registro de instalación para comprobar si la instalación se realizó correctamente.

### Para comprobar que la instalación de la aplicación RMS sharing para Office 2016 u Office 2013 y Azure RMS o Active Directory RMS se ha realizado correctamente

-   Para comprobar que el comando Setup.exe se ha ejecutado correctamente, busque en cada equipo el archivo de registro de instalación **RMInstaller.log** en la carpeta *%temp%\RMS_installer_&lt;guid&gt;* y, luego, identifique el código de salida.

    Una instalación correcta tiene un código de salida de 0 y cualquier otro número indica un error en la instalación.

    Nombre de archivo de registro de ejemplo: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

### Para comprobar que la instalación de la aplicación RMS sharing para Office 2010 y Azure RMS se ha realizado correctamente

1.  Para comprobar que el comando Setup.exe se ha ejecutado correctamente, busque en cada equipo el archivo de registro de instalación **RMInstaller.log** en la carpeta *%temp%\RMS_installer_&lt;guid&gt;* y, luego, identifique el código de salida.

    Una instalación correcta tiene un código de salida de 0 y cualquier otro número indica un error en la instalación.

    Nombre de archivo de registro de ejemplo: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Para comprobar que el comando RMSSetup.exe se ha ejecutado correctamente, el usuario debe tener los siguientes archivos creados en su carpeta *%localappdata%\microsoft\drm*:

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   GIC-&#42;.drm

    Ejemplo de un archivo CLC-&#42;.drm:

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf;k5b11;k4a10;kac15;k29b2b6980f4c}.drm**

### Para comprobar que la instalación de la aplicación RMS sharing para Office 2010 y Active Directory RMS se ha realizado correctamente

1.  Para comprobar que el comando Setup.exe se ha ejecutado correctamente, busque en cada equipo el archivo de registro de instalación en la carpeta *%temp%\RMS_installer_&lt;guid&gt;* e identifique el código de salida.

    Una instalación correcta tiene un código de salida de 0 y cualquier otro número indica un error en la instalación.

    Nombre de archivo de registro de ejemplo: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Para comprobar que el comando aadrmprep.exe se ha ejecutado correctamente, busque en cada equipo el siguiente texto en el archivo de registro de instalación: **aadrmprep.exe exited with status SUCCESS**

    > [!NOTE]
    > En ocasiones, la instalación puede ejecutarse dos veces; la primera vez resulta incorrecta y la segunda correcta.

    Si desea comprobar manualmente los cambios que hace esta herramienta en el Registro, son los siguientes:

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationPágina principalRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationPágina principalRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @="&lt;certification url&gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        DefaultUser="&lt;default_user&gt;"

### Para comprobar que la instalación de la aplicación RMS sharing y solo el complemento de Office se ha realizado correctamente

1.  Para comprobar que el comando Setup_ipviewer.exe se ha ejecutado correctamente, busque el siguiente texto en el archivo de registro de instalación: **Resultado de la instalación: 0**

    Líneas de ejemplo de una instalación correcta:

    **MSI (s) (F0:B8) [14:19:57:854]: Producto: Cliente de Active Directory Rights Management Services 2.1 -- La instalación se completó correctamente.**

    **MSI (s) (F0:B8) [14:19:57:854]: Windows Installer instaló el producto. Nombre del producto: Cliente de Active Directory Rights Management Services 2.1. Product Version: 1.0.1179.1. Product Language: 1033. Fabricante: Microsoft Corporation Resultado de la instalación: 0.**

2.  Para comprobar que el complemento de Office se ha ejecutado correctamente en cada equipo, busque el siguiente texto en el archivo de registro de instalación: **Resultado de la instalación: 0**

    Líneas de ejemplo de una instalación correcta:

    **MSI (s) (9C:88) [18:49:04:007]: Producto: Complementos de Office para Microsoft RMS -- La instalación se completó correctamente.**

    **MSI (s) (9C:88) [18:49:04:007]: Windows Installer instaló el producto. Nombre del producto: Complementos de Office para Microsoft RMS. Product Version: 1.0.7. Product Language: 1033. Fabricante: Microsoft. Resultado de la instalación: 0.**

## Comandos de desinstalación
No todos los comandos de instalación necesarios para estas implementaciones admiten un comando de desinstalación. Puede desinstalar el cliente de AD RMS y la aplicación sharing, y también puede desinstalar el complemento de Office. Use los siguientes comandos para desinstalar estos elementos.

### Para desinstalar el cliente de AD RMS y la aplicación RMS sharing

-   Use los comandos siguientes:

    -   Para Windows de 64 bits:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   Para Windows de 32 bits:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

### Para desinstalar el complemento de Office

-   Use los comandos siguientes:

    -   Para la versión de 64 bits de Office:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   Para la versión de Office de 32 bits:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

## Supresión de actualizaciones automáticas
De forma predeterminada, los usuarios reciben una notificación si hay una versión posterior de la aplicación RMS sharing y se les pide que la descarguen. Puede suprimir esta notificación realizando el siguiente cambio en el Registro:

1.  Navegue a **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** y, si no aparece ya ahí, cree una nueva clave denominada **RmsSharingApp**.

2.  Seleccione **RmsSharingApp**, cree un nuevo valor DWORD de **AllowUpdatePrompt**y establezca el valor en **0**.

Dado que la aplicación RMS sharing no es compatible con WSUS, puede usar la siguiente técnica para probar las nuevas versiones de dicha aplicación antes de implementarla para todos los usuarios:

1.  En los equipos de todos los usuarios, ejecute un script para suprimir las actualizaciones automáticas. En los equipos que usan los administradores para probar nuevas versiones, no ejecute este script.

2.  Cuando hay disponible una nueva versión, los administradores la descargan y la prueban.

3.  Cuando la prueba está completa y los posibles problemas se han resuelto, implemente la versión más reciente para todos los usuarios mediante las instrucciones de implementación automática de esta guía.

## Solo Azure RMS: configuración del seguimiento de documentos
Si tiene una [suscripción que admite el seguimiento de documentos](https://technet.microsoft.com/dn858608), el sitio de seguimiento de documentos está habilitado de manera predeterminada para todos los usuarios de su organización.  El seguimiento de documentos mostrará información, como las direcciones de correo electrónico de las personas que intentaron acceder a documentos protegidos que los usuarios compartieron, cuándo estas personas intentaron obtener acceso a ellos y su ubicación. Si mostrar esta información está prohibido en su organización debido a los requisitos de privacidad, puede deshabilitar el acceso al sitio de seguimiento de documentos mediante el cmdlet [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032). Puede volver a habilitar el acceso al sitio en cualquier momento, mediante [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037), así como comprobar si el acceso está actualmente habilitado o deshabilitado mediante [Get AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

Para ejecutar estos cmdlets, debe tener como mínimo la versión **2.3.0.0** del módulo Azure RMS para Windows PowerShell.  Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

> [!TIP]
> Si ya ha descargado e instalado el módulo anteriormente, compruebe el número de versión. Para ello, ejecute: `(Get-Module aadrm –ListAvailable).Version`

Las direcciones URL siguientes se usan para el seguimiento de documentos y se deben permitir (por ejemplo, agregarlas a sus sitios de confianza si está usando Internet Explorer con seguridad mejorada):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > Esta dirección URL es para mapas de Bing.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

### Realizar un seguimiento y revocar documentos para usuarios

Cuando los usuarios inician sesión en el sitio de seguimiento de documentos, pueden realizar un seguimiento y revocar documentos que han compartido mediante la aplicación RMS sharing. Al iniciar sesión como administrador de Azure RMS (administrador global), puede hacer clic en el icono de administración en la parte superior derecha de la página, que cambia al modo de administrador para que pueda ver los documentos que han compartido los usuarios de la organización.

Las acciones que realiza en el modo de administrador se auditan y registran en los archivos de registro de uso y debe confirmar para continuar. Para obtener más información sobre este registro, consulte la sección siguiente.

Cuando está en el modo de administrador, puede buscar por usuario o documento. Si quiere buscar por usuario, verá todos los documentos que ha compartido el usuario especificado. Si quiere buscar por documento, verá todos los usuarios de la organización que han compartido ese documento. Después, puede profundizar en los resultados de búsqueda para realizar un seguimiento de los documentos que han compartido los usuarios y revocar estos documentos, si es necesario. 

Para salir del modo de administrador, haga clic en la **X** junto a **Salir del modo de administrador**.

Para obtener instrucciones sobre cómo usar el sitio de seguimiento de documentos, consulte [Seguimiento y revocación de documentos](sharing-app-track-revoke.md) en el manual del usuario.



### Registro de uso del sitio de seguimiento de documentos

Dos campos de los archivos de registro de uso se aplican al seguimiento de documentos: **AdminAction** y **ActingAsUser**.

**AdminAction**: este campo tiene un valor de true cuando un administrador usa el sitio de seguimiento de documentos en modo de administrador, por ejemplo, para revocar un documento en nombre de un usuario o para ver cuándo se ha compartido. Este campo está vacío cuando un usuario inicia sesión en el sitio de seguimiento de documentos.

**ActingAsUser**: cuando el campo AdminAction es true, este campo contiene el nombre de usuario del que el administrador actúa en nombre, como la búsqueda de usuario o propietario del documento. Este campo está vacío cuando un usuario inicia sesión en el sitio de seguimiento de documentos. 

También hay tipos de solicitudes que registran cómo los usuarios y administradores usan el sitio de seguimiento de documentos. Por ejemplo, **RevokeAccess** es el tipo de solicitud cuando un usuario o un administrador en nombre de un usuario ha revocado un documento en el sitio de seguimiento de documentos. Use este tipo de solicitud en combinación con el campo AdminAction para determinar si el usuario ha revocado su propio documento (el campo AdminAction está vacío) o un administrador ha revocado un documento en nombre de un usuario (el campo AdminAction es true).


Para más información sobre el registro de uso, consulte [Registro y análisis del uso de Azure Rights Management](../deploy-use/log-analyze-usage.md)

## Solo AD RMS: Compatibilidad con varios dominios de correo electrónico dentro de su organización
Si usa AD RMS y los usuarios de su organización tienen varios dominios de correo electrónico, quizás como resultado de una fusión o adquisición, debe realizar la siguiente modificación en el Registro:

1.  Navegue a **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** y, si no aparece ya ahí, cree una nueva clave denominada **RmsSharingApp**.

2.  Seleccione **RmsSharingApp**, cree un valor de cadena múltiple denominado **FederatedDomains** y agregue los dominios y todos los subdominios que usa la organización. No se admiten caracteres comodín.

    Por ejemplo: La compañía Coho Vineyard &amp; Winery tiene un dominio de correo electrónico estándar de **cohovineyardandwinery.com**, pero como resultado de fusiones, también usan los dominios de correo electrónico **cohowinery.com**, **eastcoast.cohowinery.com** y **cohovineyard**. Para el valor **FederatedDomains**, el administrador escribe: **cohowinery.com; eastcoast.cohowinery.com; cohovineyard**

Si no realiza este cambio en el Registro, los usuarios no podrán consumir contenido que han protegido otros usuarios de su organización. Esta modificación del Registro no es necesaria si usa Azure RMS.


## Pasos siguientes
Para obtener información técnica adicional que incluye la explicación de la diferencia entre los niveles de protección (nativa y genérica), los tipos de archivo y las extensiones de nombre de archivo, y cómo cambiar el nivel de protección predeterminado, consulte [Technical overview for the Rights Management sharing application](sharing-app-admin-guide-technical.md) (Introducción técnica a la aplicación Rights Management sharing).




<!--HONumber=Aug16_HO1-->


