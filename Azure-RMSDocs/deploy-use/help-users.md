---
title: Ayuda a los usuarios para proteger archivos mediante Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b6dcd8bb1091e9c484e02042adbf993381581a9d
ms.openlocfilehash: d48616cb638522e6cda61e7ae96db9480fc14099


---

# Ayuda a los usuarios para proteger archivos mediante Azure Rights Management

*Se aplica a: Azure Rights Management, Office 365*

Una vez haya implementado y configurado Azure Rights Management (RMS) para su organización, ofrezca ayuda y orientación para los usuarios, los administradores y su servicio de asistencia:

-   **Información del usuario final:**

    Indique a los usuarios cómo y cuándo proteger documentos y mensajes de correo electrónico que contengan información confidencial. Siempre que sea posible, proporcione esta información en sus flujos de trabajo existentes, para que puedan incorporar los pasos adicionales a un proceso ya conocido, en lugar de introducir completamente nuevos procesos. Asegúrese de informarle de los beneficios (y de los riesgos) específicos para su negocios, así como de proporcionar orientación para cuándo deben proteger archivos y mensajes de correo electrónico. Si ha configurado [plantillas personalizadas](configure-custom-templates.md), ofrezca instrucciones sobre cuál elegir si el nombre de la plantilla y la descripción no es suficiente para que elijan la correcta.

    > [!TIP]
    > Vídeos de ejemplo para usuarios finales:
    >
    > -   [Experiencia del usuario con Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)
    > -   [Revocación y seguimiento de documentos de Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Información del administrador:**

    Algunas aplicaciones aplican automáticamente protección de la información, mediante directivas y configuración que los administradores establecen. Para estas aplicaciones, puede que tenga que proporcionar instrucciones para otros administradores que administran estas aplicaciones y servicios. Para más información, consulte [How applications support Azure Rights Management](../understand-explore/applications-support.md) (Compatibilidad de las aplicaciones con Azure Rights Management) y [Configuring applications for Azure Rights Management](configure-applications.md) (Configuración de las aplicaciones para Azure Rights Management).

-   **Información del servicio de asistencia**

    Una de las herramientas más útiles para el servicio de asistencia es [RMSAnalyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Los operadores del servicio de asistencia pueden ejecutarlo con la opción de administrador de Azure RMS, y pueden pedir a los usuarios que lo ejecuten con la opción de usuario de Azure RMS. Esta herramienta no solo puede ayudar a identificar problemas, sino también a corregir los problemas que encuentre y, si todavía no se han solucionado, anotar los registros de seguimiento.

    Si hay solicitudes legítimas para tener derechos completos de acceso a documentos protegidos, por ejemplo, una solicitud del departamento legal o de un administrador después de que un empleado ha dejado la organización, asegúrese de que el servicio de asistencia tenga procesos para solicitar esto mediante la [característica de superusuario](configure-super-users.md)de Azure RMS.

    Además, estos son algunos de los problemas típicos que podrían notificar los usuarios:

    -   **Ayuda de inicio de sesión:**

        A los usuarios se les puede solicitar credenciales cuando Azure RMS tenga que autenticar un usuario y no pueda usar credenciales en caché. Serán la cuenta profesional o educativa del usuario y la contraseña que están asociadas con su inquilino de Office 365 o de Azure Active Directory. No será una cuenta Microsoft (anteriormente Microsoft Live ID) o su cuenta de correo electrónico personal porque no están admitidas actualmente por Azure RMS. Proporcione a los usuarios y al servicio de asistencia instrucciones acerca de qué cuenta se utilizará cuando a los usuarios se les solicite credenciales cuando usen estas aplicaciones con Azure RMS.

    -   **Problemas de protección o consumo de contenido:**

        Asegúrese de que los usuarios tengan las instrucciones apropiadas para las aplicaciones que usan y que estén usando aplicaciones y dispositivos que sean compatibles con Azure RMS. Para más información sobre dispositivos y aplicaciones compatibles, consulte [Requirements for Azure Rights Management](../get-started/requirements-azure-rms.md) (Requisitos para Azure Rights Management).

        Si los usuarios ven un error al intentar proteger o consumir contenido, pídales que ejecuten [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) como usuarios de Azure RMS.

        Si los usuarios informan de que pueden abrir contenido protegido, pero no tiene los derechos que necesitan, pedirles que ejecuten [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) como usuarios de Azure RMS y que descarguen y vean las plantillas. De este modo se confirmará que han descargado correctamente las plantillas y qué derechos proporcionan las plantillas. El problema puede ser que el usuario no está en el grupo correcto que se configura para la plantilla, o que es necesario volver a configurar la plantilla para el usuario.

Use las secciones siguientes para información específica de aplicación a fin de ayudar a los usuarios a proteger documentos y mensajes de correo electrónico confidenciales.

## Usar la protección de información con la aplicación de uso compartido de Rights Management
La aplicación de uso compartido de Rights Management (RMS) se requiere para que los usuarios protejan y consuman contenido protegido si usan Office 2010 pero también se recomienda para todos los equipos y dispositivos móviles que admiten Azure RMS.

Además de facilitar a los usuarios la protección de documentos importantes, la aplicación de uso compartido de RMS permite a los usuarios realizar el seguimiento de los documentos que han protegido y, si es necesario, revocar el acceso a ellos.

Para obtener instrucciones de uso de esta aplicación para equipos con Windows, consulte [Rights Management sharing application user guide](../rms-client/sharing-app-user-guide.md) (Manual de usuario de la aplicación Rights Management sharing).

Para dispositivos móviles, consulte las [preguntas más frecuentes sobre la aplicación Microsoft Rights Management sharing para plataformas móviles](http://technet.microsoft.com/dn451248).

> [!TIP]
> Para ver un escenario de ejemplo de alto nivel con capturas de pantalla, consulte [Uso compartido seguro de datos adjuntos con los usuarios móviles](../understand-explore/what-admins-users-see.md#users-safely-share-attachments-with-mobile-users).

## Uso de protección de la información con Office 365, Office 2016 u Office 2013
Si está usando Azure RMS y no ha instalado la aplicación Rights Management sharing, los usuarios no verán el botón **Uso compartido protegido** en la cinta de opciones o **Protección local** del Explorador de archivos que les facilita la protección de archivos. Para estos usuarios, debe seguir instrucciones similares a las siguientes.

> [!TIP]
> Para buscar ayuda específica de la aplicación e instrucciones para usar protección de la información con estas aplicaciones, busque **IRM** y el nombre y la versión de la aplicación.

#### Para proteger un documento en Word 2013

1.  Dentro de Microsoft Word, cree un nuevo documento.

2.  En el menú **Archivo** , haga clic en **Información**, elija **Proteger documento**y haga clic en **Restringir el acceso**. Después elija una plantilla para aplicar de inmediato los permisos de uso correspondientes o elija **Restringir el acceso** y seleccione usted mismo los permisos de uso.

    > [!NOTE]
    > Si esta es la primera vez que ha usado Rights Management, se pondrá en contacto con el servicio de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] y se le solicitarán las credenciales para configurar el cliente de Office IRM.

3.  Guarde el documento.

Cuando otros usuarios abran el documento, se les autenticará primero. Si no está autenticados para abrir el documento, el documento no se abrirá. Si están autorizados para abrir el documento, se abrirá con los derechos de uso restringidos que se especificaron para ese usuario. Por ejemplo, un derecho de uso de Solo vista no permite al usuario editar o guardar el documento, aunque se copie primero a otra ubicación. Los derechos de uso se muestran en la parte superior del documento mediante una pancarta de restricción. La pancarta puede mostrar los permisos que se aplican al documento o puede proporcionar un vínculo para mostrarlos.

#### Para proteger un mensaje de correo electrónico con Outlook 2013 y Exchange Online

1.  Dentro de Outlook, cree un nuevo mensaje de correo electrónico para un destinatario dentro de la organización.

2.  En la pestaña **OPCIONES** , haga clic en **Permiso**y seleccione una opción. Por ejemplo: **No reenviar**, **&lt;Nombre de empresa&gt; - Confidencial** o **&lt;Nombre de empresa&gt; - Solo vista confidencial**.

3.  Envíe el mensaje.

De manera similar a la visualización de un documento protegido, cuando los destinatarios reciben el mensaje de correo electrónico, se autentican en primer lugar. Si están autorizados para ver el mensaje de correo electrónico, se abrirá con los derechos de uso restringidos que se especificaron para ese usuario. Por ejemplo, si seleccionó **No reenviar**, el botón Reenviar no está disponible en la cinta de opciones.

#### Para proteger un mensaje de correo electrónico con Outlook Web App

1.  Dentro de Outlook Web Ap, cree un nuevo mensaje de correo electrónico para un destinatario dentro de la organización.

2.  Haga clic en  **...**, elija **Establecer permisos**y seleccione una opción. Por ejemplo: **No reenviar**, **No responder a todos**, **&lt;Nombre de empresa&gt; - Confidencial** o **&lt;Nombre de empresa&gt; - Solo vista confidencial**.

3.  Envíe el mensaje.

De manera similar a la visualización de un documento protegido, cuando los destinatarios reciben el mensaje de correo electrónico, se autentican en primer lugar. Si están autorizados para ver el mensaje de correo electrónico, se abrirá con los derechos de uso restringidos que se especificaron para ese usuario. Por ejemplo, si seleccionó **No responder a todos**, la opción **RESPONDER A TODOS** no está disponible en la ventana del mensaje.





<!--HONumber=Jul16_HO3-->


