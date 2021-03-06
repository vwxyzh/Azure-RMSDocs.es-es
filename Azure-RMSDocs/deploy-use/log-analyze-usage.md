---
title: "Registro y análisis del uso de Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/05/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2082620eb152aa88af4141b88985adce22769168
ms.openlocfilehash: fbf614bf7b30165a78f6312267243ad6fdb81435


---

# Registro y análisis del uso de Azure Rights Management

*Se aplica a: Azure Rights Management, Office 365*

Use la información de este tema para comprender cómo puede usar el registro de uso con Azure Rights Management (Azure RMS). El servicio Azure Rights Management permite registrar todas las solicitudes que realice para su organización, lo que incluye solicitudes de usuarios, acciones llevadas a cabo por administradores de Rights Management en su organización y acciones llevadas a cabo por operadores de Microsoft para admitir su implementación de Azure Rights Management.

A continuación, puede usar estos registros de Azure Rights Management para admitir los siguientes escenarios empresariales:

-   **Analizar enfoques empresariales**

    Los registros generados por Azure Rights Management se pueden importar en un repositorio que elija (como una base de datos, un sistema de procesamiento analítico en línea (OLAP) o un sistema de asignar-reducir) para analizar la información y producir informes. Por ejemplo, podría notificar quién está accediendo a sus datos protegidos con RMS. Puede determinar a qué datos protegidos con RMS está accediendo la gente y desde dónde y desde qué dispositivos. Puede averiguar si estas personas logran leer contenido protegido. También puede identificar qué personas han leído un documento importante que estaba protegido.

-   **Supervisar para controlar el abuso**

    La información del registro de Azure Rights Management está a su disposición casi en tiempo real, de manera que puede supervisar de manera continua el uso que se haga en su empresa de Azure Rights Management. El 99,9% de los registros están disponibles en un plazo de 15 minutos de una acción iniciada por RMS.

    Por ejemplo, puede que desee que se le alerte de si surge un aumento repentino de las personas que leen datos protegidos por RMS fuera de las hora laborales estándar, lo que podrían indica que un usuario malintencionado está recopilando información para venderla a competidores. O bien, si el mismo usuario aparentemente accede a los datos desde dos direcciones IP diferentes dentro de un breve intervalo de tiempo, lo que podría indicar que se ha puesto en peligro una cuenta de usuario.

-   **Realizar análisis forenses**

    Si tiene una pérdida de información, es probable que se le pregunte quién accedió recientemente a documentos específicos y a qué información accedió la persona sospechosa. Puede responder a este tipo de preguntas con Azure Rights Management y los registros, porque las personas que usan el contenido protegido siempre deben obtener una licencia de Azure Rights Management para abrir documentos e imágenes que estén protegidos con Azure Rights Management, incluso en el caso de que dichos archivos se muevan por correo electrónico o se copien en unidades USB u otras unidades de almacenamiento. Esto significa que puede usar los registros de Azure Rights Management como el origen fundamental de la información para realizar el análisis forense cuando protege sus datos con Azure Rights Management.

> [!NOTE]
> Si solo está interesado en el registro de las tareas administrativas para Azure Rights Management y no desea realizar un seguimiento del modo en que los usuarios usan Rights Management, puede usar el cmdlet [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) de Windows PowerShell de Azure Rights Management.
> 
> También puede usar el Portal de Azure clásico para ver informes de uso de alto nivel que incluyen **Resumen de RMS**, **Usuarios activos de RMS**, **Plataformas de dispositivos RMS** y **Uso de aplicaciones de RMS**. Para tener acceso a estos informes desde el Portal de Azure clásico, haga clic en **Active Directory**, seleccione un directorio y ábralo y, luego, haga clic en **INFORMES**.

Use las secciones siguientes para más información sobre el registro de uso de Azure Rights Management.

## Habilitación del registro de uso de Azure Rights Management
A partir de febrero de 2016, el registro de uso de Azure Rights Management se habilita de forma predeterminada para todos los clientes. Esto se aplica a los clientes que han activado su servicio de Azure RMS antes de febrero de 2016 y a los clientes que han activado el servicio después de febrero de 2016. 

> [!NOTE]
> Ni el almacenamiento de registro ni la funcionalidad de la característica de registro generan costos adicionales.
> 
> Si usó el registro de uso para Azure RMS antes de febrero de 2016, precisó de una suscripción a Azure y de almacenamiento suficiente en Azure, lo que ya no sucede.



## Cómo acceder a los registros de uso de Azure Rights Management y usarlos
Azure Rights Management escribe registros en su cuenta de almacenamiento de Azure como una serie de blobs. Cada blob contiene uno o más registros, en formato de registro extendido W3C. Los nombres de blob son números, en el orden en que se crearon. La sección [Cómo interpretar los registros de uso de Azure Rights Management](#how-to-interpret-your-azure-rights-management-usage-logs) que aparece más adelante en este documento contiene más información acerca del contenido del registro y su creación.

Puede que los registros tarden en aparecer en su cuenta de almacenamiento después de realizar alguna acción de Azure Rights Management. La mayoría de los registros aparecen en 15 minutos. Recomendamos que descargue los registros en el almacenamiento local, como una carpeta local, una base de datos o un repositorio de asignar-reducir.

Para descargar sus registros de uso, usará el módulo de administración de Azure RMS para Windows PowerShell. Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md). Si ha descargado anteriormente este módulo de Windows PowerShell, ejecute el siguiente comando para comprobar que su número de versión es **2.4.0.0**: como mínimo: `(Get-Module aadrm -ListAvailable).Version` 

### Descargar sus registros de uso mediante PowerShell

1.  Inicie Windows PowerShell con la opción **Ejecutar como administrador** y use el cmdlet [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) para conectarse al servicio de Azure Rights Management:

    ```
    Connect-AadrmService
    ```
    
2.  Ejecute el siguiente comando para descargar los registros para una fecha específica: 

    ```
    Get-AadrmUserLog -Path <location> -fordate <date>
    ```

    Por ejemplo, después de crear una carpeta denominada Registros en la unidad E:
    
    * Para descargar registros para una fecha específica (por ejemplo, 01/02/2016), ejecute el siguiente comando: `Get-AadrmUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * Para descargar registros para un intervalo de fechas (por ejemplo, de 01/02/2016 a 14/02/2016), ejecute el siguiente comando: `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

Al especificar solo el día, como en nuestros ejemplos, se supone que la hora es 00:00:00 en su hora local y que luego se convierte a UTC. Al especificar una hora con sus parámetros -fromdate o -todate (por ejemplo, -fordate "2/1/2016 15:00:00"), esa fecha y hora se convierten a UTC. A partir de ese momento, el comando Get-AadrmUserLog obtiene los registros para ese período UTC.

No puede especificar menos de un día entero para la descarga.

De forma predeterminada, este cmdlet usa tres subprocesos para descargar los registros. Si tiene ancho de banda de red suficiente y desea reducir el tiempo necesario para descargar los registros, use el parámetro -NumberOfThreads, que admite un valor entre 1 y 32. Por ejemplo, si ejecuta el siguiente comando, el cmdlet genera 10 subprocesos para descargar los registros: `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> Puede agrupar todos los archivos de registro descargados en un formato CSV mediante el uso del [Analizador del registro de Microsoft](https://www.microsoft.com/download/details.aspx?id=24659), una herramienta para realizar conversiones entre diversos formatos de archivo conocidos. También puede usar esta herramienta para convertir datos al formato SYSLOG o importarlo a un base de datos. Una vez que haya instalado la herramienta, ejecute `LogParser.exe /?` para obtener ayuda e información para usar esta herramienta. 
>
> Por ejemplo, puede ejecutar el siguiente comando para importar todas la información en un formato de archivo .log: `logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

#### Si ha habilitado manualmente el registro de uso de Azure RMS antes del cambio de registro (22 de febrero de 2016)


Si ha usado el registro de uso antes del cambio de registro, tendrá registros de uso en su cuenta de almacenamiento de Azure configurada. Microsoft no copiará estos registros de su cuenta de almacenamiento a la nueva cuenta de almacenamiento administrada de Azure RMS como parte de este cambio de registro. Es responsable de administrar el ciclo de vida de los registros generados anteriormente y puede usar el cmdlet [Get-AadrmUsageLog](https://msdn.microsoft.com/library/dn629401.aspx) para descargar sus registros antiguos. Por ejemplo:

- Para descargar todos los registros disponibles en su carpeta E:\logs: `Get-AadrmUsageLog -Path "E:\Logs"`
    
- Para descargar un intervalo específico de blobs: `Get-AadrmUsageLog –Path "E:\Logs" –FromCounter 1024 –ToCounter 2047`

Tenga en cuenta que no tiene que descargar registros con el cmdlet Get-AadrmUsageLog si se aplica algo de lo siguiente:

-  Activó Azure Rights Management el 22 de febrero de 2016 o antes, pero no habilitó la característica de registro de uso.

- Ha activado Azure Rights Management después del 22 de febrero de 2016.

## Interpretación de los registros de uso de Azure Rights Management
Use la siguiente información como ayuda para interpretar los registros de uso de Azure Rights Management.

### La secuencia de registro
Azure Rights Management escribe los registros como una serie de blobs. 

Cada entrada en el registro tiene una marca de tiempo UTC. Dado que Azure Rights Management se ejecuta en varios servidores de varios centros de datos, a veces puede parecer que los registros estén fuera de secuencia, aunque estén ordenados por su marca de tiempo. Sin embargo, la diferencia es mínima y generalmente se encuentra en un margen de un minuto. En la mayoría de los casos, este asunto no sería un problema para análisis de registros.

### El formato del blob
Cada blob está en formato de registro extendido W3C. Empieza por las siguientes dos líneas:

**#Software: RMS**

**#Versión: 1.1**

La primera línea identifica que se trata de registros de Azure Rights Management. La segunda línea identifica que el resto del blob sigue la especificación de la versión 1.1. Recomendamos que las aplicaciones que analicen estos registros comprueben estas dos líneas antes de continuar analizando el resto del blob.

La tercera enumera una lista de nombres de campos separados por pestañas:

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip            admin-action            acting-as-user**

Cada una de las líneas posteriores es un registro. Los valores de los campos se encuentran en el mismo orden que la línea anterior y están separados por pestañas. Use la siguiente tabla para interpretar los campos.

|Nombre de campo|Tipo de datos W3C|Descripción|Valor de ejemplo|
|--------------|-----------------|---------------|-----------------|
|date|Fecha|Fecha UTC cuando se realizó el servicio de la solicitud.<br /><br />El origen es el reloj local del servidor que realizó el servicio de la solicitud.|2013-06-25|
|time|Hora|Hora UTC en formato de 24 hora cuando se realizó el servicio de la solicitud.<br /><br />El origen es el reloj local del servidor que realizó el servicio de la solicitud.|21:59:28|
|row-id|Texto|GUID único para este registro. Si un valor no está presente, use el valor del identificador de correlación para identificar la entrada.<br /><br />Este valor es útil cuando agrega registros o copia registros en otro formato.|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|request-type|Nombre|Nombre de la API de RMS que se solicitó.|AcquireLicense|
|user-id|Cadena|El usuario que realizó la solicitud.<br /><br />El valor se incluye entre comillas únicas. Las llamadas de una clave de inquilino administrada por usted (BYOK) tienen un valor de **"**, que también se aplica cuando los tipos de solicitud son anónimos.|‘joe@contoso.com’|
|result|String|'Success' si se ha proporcionado la solicitud correctamente.<br /><br />El tipo de error entre comillas si se produjo un error de la solicitud.|'Success'|
|correlation-id|Texto|GUID que es común entre el registro del cliente de RMS y el registro del servidor para una solicitud proporcionada.<br /><br />Este valor puede ser útil para ayudar a solucionar problemas del cliente.|cab52088-8925-4371-be34-4b71a3112356|
|content-id|Texto|GUID, entre llaves, que identifica el contenido protegido (por ejemplo, un documento).<br /><br />Este campo tiene un valor solo si request-type es AcquireLicense y está en blanco para todos los demás tipos de solicitudes.|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|owner-email|Cadena|Dirección de correo electrónico del propietario del documento.|alice@contoso.com|
|issuer|Cadena|Dirección de correo electrónico del emisor del documento.|alice@contoso.com (o) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|template-id|String|Identificador de la plantilla que se usa para proteger el documento.|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|file-name|String|Nombre de archivo del documento que se ha protegido. <br /><br />Actualmente, algunos archivos (como documentos de Office) se muestran como GUID en lugar del nombre de archivo real.|TopSecretDocument.docx|
|date-published|Fecha|Fecha en la que se ha protegido el documento.|2015-10-15T21:37:00|
|c-info|Cadena|Información acerca de la plataforma del cliente que está realizando la solicitud.<br /><br />La cadena específica varía, en función de la aplicación (por ejemplo, el sistema operativo o el explorador).|'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64'|
|c-ip|Address|Dirección IP del cliente que realiza la solicitud.|64.51.202.144|


#### Excepciones para el campo user-id
Aunque el campo user-id suele indicar el usuario que hay realizado la solicitud, hay dos excepciones en las que el valor no se asigna a un usuario real:

-   El valor **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;region&gt;.aadrm.com'**.

    Esto indica que un servicio de Office 365, como Exchange Online o SharePoint Online, está realizando la solicitud. En la cadena, *&lt;YourTenantID&gt;* es el GUID de su inquilino y *&lt;region&gt;* es la región donde se registra el inquilino. Por ejemplo, **na** representa a Norteamérica, **eu** representa a Europa y **ap** representa a Asia.

-   Si está usando el conector RMS.

    Las solicitudes de este conector se registran con el nombre de entidad de servicio de **Aadrm_S-1-7-0**, que se genera automáticamente al instalar el conector RMS.

#### Tipos de solicitudes típicas
Hay muchos tipos de solicitudes de Azure Rights Management, pero en la tabla siguiente se identifican algunos de los tipos que normalmente se usan más.

|Tipo de solicitud|Descripción|
|----------------|---------------|
|AcquireLicense|Un cliente solicita desde un equipo basado en Windows una licencia para contenido protegido con RMS.|
|AcquirePreLicense|Un cliente, en nombre del usuario, solicita una licencia para contenido protegido con RMS.|
|AcquireTemplates|Se ha realizado una llamada para adquirir plantillas basadas en identificadores de plantilla.|
|AcquireTemplateInformation|Se ha realizado una llamada para obtener los identificadores de la plantilla del servicio.|
|AddTemplate|Se realiza una llamada desde el Portal de Azure clásico para agregar una plantilla.|
|AllDocsCsv|Se realiza una llamada desde el sitio de seguimiento de documentos para descargar el archivo CSV de la página **Todos los documentos**.|
|BECreateEndUserLicenseV1|Se realiza una llamada desde un dispositivo móvil para crear una licencia de usuario final.|
|BEGetAllTemplatesV1|Se realiza una llamada desde un dispositivo móvil (back-end) para obtener todas las plantillas.|
|Certify|El cliente está certificando el contenido para la protección.|
|KMSPDecrypt|El cliente está intentando descifrar el contenido protegido con RMS. Solo se aplica a una clave de inquilino administrada por el cliente (BYOK).|
|DeleteTemplateById|Se realiza una llamada desde el Portal de Azure clásico para eliminar una plantilla por identificador de plantilla.|
|DocumentEventsCsv|Se realiza una llamada desde el sitio de seguimiento de documentos para descargar el archivo CSV de un solo documento.|
|ExportTemplateById|Se realiza una llamada desde el Portal de Azure clásico para exportar una plantilla en función de un identificador de plantilla.|
|FECreateEndUserLicenseV1|Similar a la solicitud AcquireLicense pero desde dispositivos móviles.|
|FECreatePublishingLicenseV1|Lo mismo que Certify y GetClientLicensorCert combinados, desde clientes móviles.|
|FEGetAllTemplates|Se realiza una llamada desde un dispositivo móvil (front-end) para obtener las plantillas.|
|GetAllDocs|Se realiza una llamada desde el sitio de seguimiento de documentos para cargar la página **Todos los documentos** para un usuario, o buscar todos los documentos del inquilino. Use este valor con los campos admin-action y acting-as-admin:<br /><br />- admin-action está vacío: un usuario ve la página **Todos los documentos** de sus propios documentos.<br /><br />- admin-action es true y acting-as-user está vacío: un administrador ve todos los documentos de su inquilino.<br /><br />- admin-action es true y acting-as-user no está vacío: un administrador ve la página **Todos los documentos** de un usuario.|
|GetAllTemplates|Se realiza una llamada desde el Portal de Azure clásico para obtener todas las plantillas.|
|GetClientLicensorCert|El cliente está solicitando un certificado de publicación (que se utiliza posteriormente para proteger contenido) desde un equipo con Windows.|
|GetConfiguration|Se llama a un cmdlet de Azure PowerShell para obtener la configuración del inquilino de Azure RMS.|
|GetConnectorAuthorizations|Se realiza una llamada desde los conectores de RMS para obtener su configuración de la nube.|
|GetRecipients|Se realiza una llamada desde el sitio de seguimiento de documentos para ir a la vista de lista de un solo documento.|
|GetSingle|Se realiza una llamada desde el sitio de seguimiento de documentos para ir a la página de un **solo documento**.|
|GetTenantFunctionalState|El Portal de Azure clásico está comprobando si Azure RMS está activado.|
|GetTemplateById|Se realiza una llamada desde el Portal de Azure clásico para obtener una plantilla especificando un identificador de plantilla.|
|ExportTemplateById|Se está realizando una llamada desde el Portal de Azure clásico para exportar una plantilla especificando un identificador de plantilla.|
|FindServiceLocationsForUser|Se realiza una llamada para consultar las direcciones URL, que se usan para llamar a Certify o AcquireLicense.|
|LoadEventsForMap|Se realiza una llamada desde el sitio de seguimiento de documentos para ir a la vista de mapa de un solo documento.|
|LoadEventsForSummary|Se realiza una llamada desde el sitio de seguimiento de documentos para ir a la vista Escala de tiempo de un solo documento.|
|LoadEventsForTimeline|Se realiza una llamada desde el sitio de seguimiento de documentos para ir a la vista de mapa de un solo documento.|
|ImportTemplate|Se realiza una llamada desde el Portal de Azure clásico para importar una plantilla.|
|RevokeAccess|Se realiza una llamada desde el sitio de seguimiento de documentos para revocar un documento.|
|SearchUsers |Se realiza una llamada desde el sitio de seguimiento de documentos para buscar todos los usuarios de un inquilino.|
|ServerCertify|Se realiza una llamada desde un cliente habilitado para RMS (como SharePoint) para certificar el servidor.|
|SetUsageLogFeatureState|Se realiza una llamada para habilitar el registro de uso.|
|SetUsageLogStorageAccount|Se realiza una llamada para especificar la ubicación de los registros de Azure RMS.|
|SignDigest|Se realiza una llamada cuando se usa una clave con la intención de firmar. Suele llamarse una vez por cada elemento AcquireLicence (o FECreateEndUserLicenseV1), Certify y GetClientLicensorCert (o FECreatePublishingLicenseV1).|
|UpdateNotificationSettings|Se realiza una llamada desde el sitio de seguimiento de documentos para cambiar la configuración de notificaciones de un solo documento.|
|UpdateTemplate|Se realiza una llamada desde el Portal de Azure clásico para actualizar una plantilla existente.|



## Referencia de Windows PowerShell
A partir de febrero de 2016, el único cmdlet de Windows PowerShell que necesita para el registro de uso de Azure RMS es [Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx). 

Antes de este cambio, fueron necesarios los siguientes cmdlet para los registros de uso de Azure RMS y ahora están en desuso:  

-   [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Si tiene registros en su propio almacenamiento de Azure desde antes del cambio de registro de Azure RMS, puede descargarlos con estos cmdlet más antiguos, usando Get-AadrmUsageLog y Get-AadrmUsageLogLastCounterValue, como antes. Sin embargo, todos los nuevos registros de uso se escribirán en el nuevo almacenamiento de Azure RMS y deben descargarse con Get-AadrmUserLog.

Para más información acerca de cómo usar Windows PowerShell para Azure Rights Management, consulte [Administración de Azure Rights Management mediante Windows PowerShell](administer-powershell.md).






<!--HONumber=Aug16_HO1-->


