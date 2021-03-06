---
title: "Protección de RMS con la infraestructura de clasificación de archivos (FCI) de Windows Server | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 1fc1835b60c4c75b81f106011849940ba2e77164
ms.openlocfilehash: afb00e010df25dea5f3c3cad23824f773de59b18


---

# Protección de RMS con la infraestructura de clasificación de archivos (FCI) de Windows Server

*Se aplica a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Use este artículo para obtener instrucciones y un script para utilizar el cliente de Rights Management (RMS) con la herramienta de protección de RMS para configurar el Administrador de recursos del servidor de archivos y la infraestructura de clasificación de archivos (FCI).

Esta solución le permite proteger automáticamente todos los archivos en una carpeta de un servidor de archivos que ejecuta Windows Server o bien proteger automáticamente archivos que cumplen criterios específicos. Por ejemplo, los archivos que se han clasificado como poseedores de información confidencial. Esta solución usa Azure Rights Management (Azure RMS) para proteger los archivos, de modo que debe tener esta tecnología implementada en su organización.

> [!NOTE]
> Aunque Azure RMS incluye un [conector](../deploy-use/deploy-rms-connector.md) que admite la infraestructura de clasificación de archivos, dicha solución admite solo la protección nativa (por ejemplo, archivos de Office).
> 
> Para admitir todos los tipos de archivo con infraestructura de clasificación de archivos, debe usar el módulo **Protección de RMS** de Windows PowerShell, tal como se describe en este artículo. Los cmdlets de protección de RMS, al igual que la aplicación de uso compartido de RMS, admite protección genérica, así como protección nativa, lo que significa que se pueden proteger todos los archivos. Para más información acerca de los diferentes niveles de protección, consulte la sección [Niveles de protección: nativo y genérico](sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic) en la [Guía de administrador de la aplicación de uso compartido Rights Management](sharing-app-admin-guide.md).

Las instrucciones siguientes sirven para Windows Server 2012 R2 o Windows Server 2012. Si ejecuta otras versiones compatibles de Windows, es posible que tenga que adaptar algunos de los pasos por las diferencias entre la versión de su sistema operativo y la descrita en este artículo.

## Requisitos previos de la protección de Azure RMS con FCI de Windows Server
Requisitos previos de estas instrucciones:

-   En cada servidor de archivos donde ejecutará el Administrador de recursos de archivos con la infraestructura de clasificación de archivos:

    -   Ha instalado el Administrador de recursos del servidor de archivos como uno de los servicios de rol para el rol Servicios de archivo.

    -   Ha identificado una carpeta local que contiene archivos para proteger con Rights Management. Por ejemplo, C:\FileShare.

    -   Ha instalado la herramienta de protección de RMS, incluidos los requisitos previos de la herramienta (como el cliente RMS) y de Azure RMS (como la cuenta principal de servicio). Para obtener más información, consulte [Cmdlets de protección de RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).

    -   Si desea cambiar el nivel predeterminado de protección de RMS (nativo o genérico) para las extensiones de nombre de archivo específicas, ha editado el registro como se describe en la página [Configuración de API de archivo](https://msdn.microsoft.com/library/dn197834%28v=vs.85%29.aspx) .

    -   Tiene conexión a Internet, con los ajustes del equipo configurados si es necesario para un servidor proxy. Por ejemplo: `netsh winhttp import proxy source=ie`

-   Ha configurado los requisitos previos adicionales de la implementación de Azure Rights Management, como se describe en [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx). En concreto, tiene los siguientes valores para conectarse a Azure RMS mediante el uso de una entidad de servicio:

    -   BposTenantId

    -   AppPrincipalId

    -   Clave simétrica

-   Ha sincronizado sus cuentas de usuario de Active Directory locales con Azure Active Directory u Office 365, incluyendo su dirección de correo electrónico. Esto es necesario para todos los usuarios que puedan necesitar acceder a los archivos después de que FCI y Azure RMS los hayan protegido. Si no realiza este paso (por ejemplo, en un entorno de prueba), existe la posibilidad de que se bloquee el acceso de los usuarios a estos archivos. Si necesita más información sobre la configuración de esta cuenta, consulte [Preparing for Azure Rights Management](../plan-design/prepare.md) (Preparación de Azure Rights Management).

-   Ha identificado la plantilla Rights Management para su utilización, que protegerá los archivos. Asegúrese de que conoce el identificador de esta plantilla usando el cmdlet [Get-RMSTemplate](https://msdn.microsoft.com/library/azure/mt433197.aspx) .

## Instrucciones para configurar FCI del Administrador de recursos del servidor de archivos para la protección de Azure RMS
Siga estas instrucciones para proteger automáticamente todos los archivos en una carpeta mediante un script de Windows PowerShell como una tarea personalizada. Lleve a cabo estos procedimientos en este orden:

1.  Guardar el script de Windows PowerShell

2.  Crear una propiedad de clasificación para Rights Management (RMS)

3.  Crear una regla de clasificación (clasificar para RMS)

4.  Configurar la programación de clasificación

5.  Crear una tarea de administración de archivos personalizada (proteger los archivos con RMS)

6.  Probar la configuración ejecutando manualmente la regla y la tarea

Al final de estas instrucciones, todos los archivos de su carpeta seleccionada se clasificarán con la propiedad personalizada de RMS y, a continuación, Rights Management protegerá estos archivos. Para una configuración más compleja que protege de forma selectiva algunos archivos y no otros, puede crear o usar una regla y una propiedad de clasificación diferentes con una tarea de administración de archivos que protege solo esos archivos.

### Guardar el script de Windows PowerShell

1.  Copie el contenido del [script de Windows PowerShell](fci-script.md) para la protección de Azure RMS con FCI del Administrador de recursos del servidor de archivos. Pegue el contenido del script y ponga al archivo el nombre **RMS-Protect-FCI.ps1** en su propio equipo.

2.  Revise el script y realice los cambios siguientes:

    -   Busque la siguiente cadena y reemplácela por su propio AppPrincipalId, que utiliza con el cmdlet [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) para conectarse a Azure RMS:

        ```
        <enter your AppPrincipalId here>
        ```
        Por ejemplo, es posible que el script tenga el aspecto siguiente:

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)]             [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   Busque la siguiente cadena y reemplácela por su propia clave simétrica, que utiliza con el cmdlet [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) para conectarse a Azure RMS:

        ```
        <enter your key here>
        ```
        Por ejemplo, es posible que el script tenga el aspecto siguiente:

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   Busque la siguiente cadena y reemplácela por su propio BposTenantId (identificador de inquilino), que utiliza con el cmdlet [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) para conectarse a Azure RMS:

        ```
        <enter your BposTenantId here>
        ```
        Por ejemplo, es posible que el script tenga el aspecto siguiente:

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

    -   Si su servidor ejecuta Windows Server 2012, es posible que tenga que cargar manualmente el módulo RMSProtection al principio del script. Agregue el siguiente comando (o equivalente si la carpeta "Archivos de programa" está en una unidad distinta de la unidad C:

        ```
        Import-Module "C:\Program Files\WindowsPowerShell\Modules\RMSProtection\RMSProtection.dll"
        ```

3.  Firme el script. Si no firma el script (más seguro), debe configurar Windows PowerShell en los servidores que lo ejecutan. Por ejemplo, ejecute una sesión de Windows PowerShell mediante la opción **Ejecutar como administrador** y escriba: **Set-ExecutionPolicy RemoteSigned**. Sin embargo, esta configuración permite la ejecución de todos los scripts sin firmar cuando se almacenan en este servidor (menos seguro).

    Para obtener más información acerca de la firma de scripts de Windows PowerShell, consulte [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) en la biblioteca de documentación de PowerShell.

4.  Guarde el archivo localmente en cada servidor de archivos que ejecute el Administrador de recursos de archivos con la infraestructura de clasificación de archivos. Por ejemplo, guarde el archivo en **C:\RMS-Protection**. Proteja este archivo mediante permisos NTFS para que los usuarios no autorizados no puedan modificarlo.

Ahora está listo para empezar a configurar el Administrador de recursos del servidor de archivos.

### Crear una propiedad de clasificación para Rights Management (RMS)

-   En el Administrador de recursos del servidor de archivos, en Administración de clasificaciones, cree una nueva propiedad local:

    -   **Nombre**: Escribir **RMS**

    -   **Descripción**:   Escribir **protección de Rights Management**

    -   **Tipo de propiedad**: seleccione **Sí/No**

    -   **Valor**: Seleccionar **Sí**

Ahora podemos crear una regla de clasificación que usa esta propiedad.

### Crear una regla de clasificación (clasificar para RMS)

-   Cree una nueva regla de clasificación:

    -   En la pestaña **General** :

        -   **Nombre**: Escribir **Clasificar para RMS**

        -   **Habilitado**: Mantenga el valor predeterminado, que es por lo que esta casilla de verificación está seleccionada.

        -   **Descripción**: escriba **Clasificar todos los archivos en la carpeta &lt;nombre de carpeta&gt; para Rights Management**.

            Reemplace *&lt;nombre de carpeta&gt;* por su nombre elegido para la carpeta. Por ejemplo, **clasifique todos los archivos en la carpeta C:\FileShare para Rights Management**.

        -   **Ámbito**: Agregue su carpeta elegida. Por ejemplo, **C:\FileShare**.

            No seleccione las casillas de verificación.

    -   En la pestaña **Clasificación** :

    -   **Método de clasificación**: Seleccionar **Clasificador de carpetas**

    -   **propiedad** : Seleccionar **RMS**

    -   **Valor**de la propiedad: Seleccionar **Sí**

Aunque puede ejecutar las reglas de clasificación manualmente, para las operaciones en curso, deseará que esta regla se ejecute en una programación de modo que los nuevos archivos se clasifiquen con la propiedad RMS.

### Configurar la programación de clasificación

-   En la pestaña **Clasificación automática** :

    -   **Habilitar programación fija**: Seleccione esta casilla de verificación.

    -   Configure la programación para que se ejecuten todas las reglas de clasificación, lo que incluye nuestra nueva regla para clasificar archivos con la propiedad RMS.

    -   **Permitir clasificación continua de nuevos archivos**: Seleccione esta casilla de verificación de modo que se clasifiquen nuevos archivos.

    -   Opcional: Realice cualquier otro cambios que desee, como configurar opciones para informes y notificaciones.

Ahora que ha completado la configuración de clasificación, está listo para configurar una tarea de administración para aplicar la protección de RMS a los archivos.

### Crear una tarea de administración de archivos personalizada (proteger los archivos con RMS)

-   En **Tareas de administración de archivos**, cree una nueva tarea de administración de archivos:

    -   En la pestaña **General** :

        -   **Nombre de la tarea**: Escribir **Proteger archivos con RMS**

        -   Mantener la casilla de verificación **Habilitar** seleccionada.

        -   **Descripción**: escriba **Proteger archivos en &lt;nombre de carpeta&gt; con Rights Management y una plantilla mediante un script de Windows PowerShell.**

            Reemplace *&lt;nombre de carpeta&gt;* por su nombre elegido para la carpeta. Por ejemplo, **Proteger archivos en C:\FileShare con Rights Management y una plantilla mediante un script de Windows PowerShell**.

        -   **Ámbito**: Seleccione su carpeta elegida. Por ejemplo, **C:\FileShare**.

            No seleccione las casillas de verificación.

    -   En la pestaña **Acción** :

        -   **Tipo**: Seleccionar **Personalizado**

        -   **Ejecutable**: Especifique lo siguiente:

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            Si Windows no está en la unidad C:, modifique esta ruta de acceso o vaya a este archivo.

        -   **Argumento**: especifique lo siguiente, proporcionando sus propios valores para &lt;ruta de acceso&gt; e &lt;identificador de plantilla&gt;:

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail [Source File Owner Email]"
            ```
            Por ejemplo, si ha copiado el script en C:\RMS-Protection y el identificador de plantilla que ha identificado en los requisitos previos es e6ee2481-26b9-45e5-b34a-f744eacd53b0, especifique lo siguiente:

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail [Source File Owner Email]"`

            En este comando, tanto **[Source File Path]** como **[Source File Owner Email]** son variables específicas de FCI, así que escríbalas exactamente como aparecen en el comando anterior. La primera la usa FCI para especificar automáticamente el archivo identificado en la carpeta y la segunda es para que FCI recupere automáticamente la dirección de correo electrónico del propietario designado del archivo identificado. Este comando se repite para cada archivo en la carpeta que, en nuestro ejemplo, es cada archivo de la carpeta C:\FileShare que, de forma adicional, tiene RMS como propiedad de clasificación de archivos.

            > [!NOTE]
            > El parámetro y el valor de **-OwnerMail [Source File Owner Email]** aseguran que el propietario original del archivo se designe propietario de Rights Management del archivo una vez que se proteja. Esto asegura que el propietario del archivo original tiene todos los derechos de Rights Management en sus propios archivos. Cuando un usuario de dominio crea archivos, la dirección de correo electrónico se recupera automáticamente desde Active Directory con el nombre de la cuenta de usuario de la propiedad Owner del archivo. Para ello, el servidor de archivos debe estar en el mismo dominio o dominio de confianza que el usuario.
            > 
            > Siempre que sea posible, asigne los propietarios originales a documentos protegidos para asegurarse de que estos usuarios continúan teniendo control total sobre los archivos que han creado. Sin embargo, si utiliza la variable [Source File Owner Email] como se ha hecho anteriormente y un archivo no tiene un usuario de dominio definido como propietario (por ejemplo, se utilizó una cuenta local para crear el archivo, por lo que el usuario aparece como SISTEMA), se producirá un error en el script.
            > 
            > Para los archivos que no tienen un usuario de dominio como propietario, puede copiar y guardar estos archivos usted mismo como usuario de dominio, de modo que se convierta en el propietario de solo estos archivos. O bien, si dispone de permisos, puede cambiar manualmente el propietario.  Como alternativa, puede especificar una dirección de correo electrónico concreta (como la suya propia o una dirección de grupo del departamento de TI) en lugar de la variable [Source File Owner Email], lo que significa que todos los archivos que proteja mediante este script utilizarán esta dirección de correo electrónico para definir el nuevo propietario.

    -   **Ejecutar el comando como**: Seleccionar **Sistema local**

    -   En la pestaña **Condición** :

        -   **propiedad**: Seleccionar **RMS**

        -   **Operador**: Seleccionar **Igual**

        -   **Valor**: Seleccionar **Sí**

    -   En la pestaña **Programación** :

        -   **Ejecutar en**: Configure su programación preferida.

            Conceda al script tiempo de sobra para completarse. Aunque esta solución protege todos los archivos de la carpeta, el script se ejecuta una vez para cada archivo cada vez. Aunque este proceso tarda más que proteger todos los archivos al mismo tiempo, lo que es compatible con la herramienta de protección de RMS, esta configuración de cada archivo para FCI es más eficaz. Por ejemplo, los archivos protegidos pueden tener distintos propietarios (conservar el propietario original) cuando utiliza la variable [Source File Owner Email] y esta acción de cada archivo será necesaria si posteriormente cambia la configuración para proteger archivos de forma selectiva en lugar de todos los archivos de una carpeta.

        -   **Ejecutarse continuamente en nuevos archivos**: Seleccione esta casilla de verificación.

### Probar la configuración ejecutando manualmente la regla y la tarea

1.  Ejecute la regla de clasificación:

    1.  Haga clic en **Reglas de clasificación** &gt; **Ejecutar clasificación con todas las reglas ahora**.

    2.  Haga clic en **Esperar a que termine la clasificación**y, a continuación, haga clic en **Aceptar**.

2.  Espere a que se cierre el cuadro de diálogo **Ejecutando clasificación** para cerrar y, a continuación, ver los resultados en el informe que se muestra automáticamente. Debe ver **1** para el campo **Propiedades** y el número de archivos de su carpeta. Confírmelo mediante el Explorador de archivos y comprobando las propiedades de archivos de su carpeta elegida. En la pestaña **Clasificación** ficha, debe ver **RMS** como nombre de la propiedad y **Sí** para su **Valor**.

3.  Ejecute la tarea de administración de archivos:

    1.  Haga clic en **Tareas de administración de archivos** &gt; **Proteger archivos con RMS** &gt; **Ejecutar tarea de administración de archivos ahora**.

    2.  Haga clic en **Esperar a que termine la clasificación**y, a continuación, haga clic en **Aceptar**.

4.  Espere a que se cierre el cuadro de diálogo **Ejecutando tarea de administración de archivos** para cerrar y, a continuación, ver los resultados en el informe que se muestra automáticamente. Debe ver el número de archivos que se encuentran en su carpeta elegida en el campo **Archivos** . Confirme que los archivos de su carpeta elegida están actualmente protegidos por RMS. Por ejemplo, si su carpeta elegida es C:\FileShare, escriba lo siguiente en una sesión de Windows PowerShell y confirme que no hay ningún archivo con el estado **Sin proteger**:

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > Algunas sugerencias para la solución de problemas:
    > 
    > -   Si ve **0** en el informe, en lugar del número de archivos de su carpeta, esto indica que el script no se ha ejecutado. En primer lugar, compruebe el propio script cargándolo en ISE de Windows PowerShell para validar el contenido del script e intenta ejecutarlo para ver si se muestra algún error. Sin argumentos especificados, el script intentará conectarse y autenticarse en Azure RMS.
    > 
    >     -   Si el script informa de que no ha podido conectarse a Azure RMS, compruebe los valores que muestra para la cuenta de entidad de servicio, que ha especificado en el script.  Para obtener más información sobre cómo crear esta cuenta de entidad de servicio, consulte el segundo requisito previo en [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)
    >     -   Si el script informa de que se puede conectar a Azure RMS, compruebe que se puede encontrar la plantilla especificada mediante la ejecución de [Get RMSTemplate](https://msdn.microsoft.com/library/mt433197.aspx) directamente desde Windows PowerShell en el servidor. Debería ver la plantilla especificada que se devuelve en los resultados.
    > -   Si el script por sí solo se ejecuta en ISE de Windows PowerShell sin errores, intente ejecutarlo como se indica a continuación en una sesión de PowerShell, especificando un nombre de archivo para proteger y sin el parámetro - OwnerEmail:
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '<full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   Si el script se ejecuta correctamente en esta sesión de Windows PowerShell, compruebe sus entradas para **Ejecutivo** y **Argumento** en la acción de tarea de administración de archivos.  Si ha especificado **-OwnerEmail [Source File Owner Email]**, pruebe a quitar este parámetro.
    > 
    >         Si la tarea de administración de archivos funciona correctamente sin **-OwnerEmail [Source File Owner Email]**, compruebe que los archivos no protegidos tienen un usuario de dominio que aparece como el propietario del archivo, en lugar de **SISTEMA**.  Para ello, utilice la pestaña **Seguridad** de las propiedades del archivo y haga clic en **Opciones avanzadas**. El valor de **propietario** se muestra inmediatamente después del **nombre** del archivo. Verifique también que el servidor de archivos esté en el mismo dominio o en un dominio de confianza para buscar la dirección de correo electrónico del usuario desde Servicios de dominio de Active Directory.
    > -   Si ve el número correcto de archivos en el informe, pero los archivos no están protegidos, intente proteger los archivos manualmente mediante el uso del cmdlet [Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) para ver si aparece algún error.

Cuando haya confirmado que estas tareas se ejecutan satisfactoriamente, puede cerrar el Administrador de recursos de archivo. Los archivos nuevos se protegerán automáticamente y todos los archivos se protegerán de nuevo cuando se ejecuten las programaciones. Volver a proteger los archivos garantiza que todos los cambios realizados en la plantilla se aplican a los archivos.


## Modificar las instrucciones para proteger archivos de forma selectiva
Cuando tenga las instrucciones anteriores funcionando, será muy fácil modificarlas para obtener una configuración más sofisticada. Por ejemplo, proteja archivos mediante el uso del mismo script, pero solo para los archivos que contienen información de identificación personal y seleccione quizás una plantilla con permisos más restrictivos.

Para ello, utilice una de las propiedades de clasificación integradas (por ejemplo, **Información de identificación personal**) o cree su propia nueva propiedad. A continuación, cree una nueva regla que utilice esta propiedad. Por ejemplo, puede seleccionar **Clasificador de contenido**, elija la propiedad **Información de identificación personal** con un valor de **Alto**y configure el modelo de expresiones o cadenas que identifica el archivo que se va a configurar para esta propiedad (como la cadena "**Fecha de nacimiento**").

Ahora todo lo que debe hacer es crear una nueva tarea de administración de archivos que utilice el mismo script, aunque quizás con una plantilla diferente, así como configurar la condición para la propiedad de clasificación que acaba de configurar. Por ejemplo, en lugar de la condición que hemos configurado previamente (propiedad**RMS** , **Igual**, **Sí**), seleccione la propiedad **Información de identificación personal** con el valor **Operador** establecido en **Igual** y el **Valor** de **Alto**.




<!--HONumber=Jun16_HO4-->


