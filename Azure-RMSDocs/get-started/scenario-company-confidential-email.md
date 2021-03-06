---
title: "Escenario: Enviar un correo electrónico confidencial de la empresa | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 950799e9-2289-48c7-b95a-f54a8ead520a
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: b6f3b06485dda81be2a36035fea7477f4061a8e9


---

# Escenario: Enviar un correo electrónico confidencial de la empresa

*Se aplica a: Azure Rights Management, Office 365*

En este escenario y en la documentación de usuario correspondiente se usa Azure Rights Management para que cualquier usuario de la organización pueda enviar de forma segura comunicaciones de correo electrónico que no se pueden leer fuera de la organización. Por ejemplo, si el mensaje de correo se reenviara a alguien de otra organización o a una cuenta de correo electrónico personal. Los correos electrónicos y los datos adjuntos estarán protegidos por Azure Rights Management y por una plantilla que los usuarios seleccionan en el cliente de correo electrónico.

La forma más sencilla de reproducir este escenario consiste en usar una de las plantillas predeterminadas integradas que restringen automáticamente el acceso a todos los usuarios de la organización. Pero, si fuera necesario restringir más aún, puede crear una plantilla personalizada que, por ejemplo, limite el acceso a un subconjunto de usuarios o que tenga otras restricciones, como que sea de solo lectura, que tenga una fecha de caducidad o que tenga el botón Reenviar deshabilitado en el cliente de correo electrónico.

> [!IMPORTANT]
> En este escenario, aunque puede quitar el botón **Reenviar** directamente de la plantilla personalizada que configure (lo que hará que este botón se deshabilite en el cliente de correo electrónico), esta configuración no impedirá que los usuarios puedan compartir el correo electrónico con otro usuario autorizado. El destinatario puede guardar el correo (y los datos adjuntos) y, luego, compartir la información empleando otros mecanismos de uso compartido.
> 
> Por ejemplo, Juan envía un correo electrónico a Isabel mediante una plantilla personalizada que aplica los permisos personalizados Guardar archivo y Editar contenido al grupo de marketing, pero no incluye el permiso Reenviar. Aunque Isabel no puede reenviar el correo electrónico a otros usuarios, sí puede guardarlo (así como los datos adjuntos) en una unidad USB o en un recurso compartido del servidor de archivos, de forma que cualquier miembro del grupo de marketing pueda leerlos y modificarlos si tiene acceso a estos archivos. Los usuarios que no estén en el grupo de marketing no podrán abrir el contenido.

Las instrucciones son adecuadas para el conjunto de circunstancias siguiente:

-   Un usuario de la organización quiere compartir información con otras personas dentro de la organización, pero tal información no debe compartirse fuera de la organización.

-   La información que se va a compartir puede estar en el mensaje de correo o en los datos adjuntos.

-   Los usuarios deben seleccionar manualmente la plantilla desde sus clientes de correo electrónico.

## Instrucciones de implementación
![Instrucciones para el administrador para la implementación rápida de Azure RMS](../media/AzRMS_AdminBanner.png)

Asegúrese de que se cumplen los siguientes requisitos antes de pasar a la documentación del usuario.

## Requisitos para este escenario
Para que las instrucciones de este escenario funcionen, debe cumplir lo siguiente:

|Requisito|Si necesita más información|
|---------------|--------------------------------|
|Ha preparado cuantas y grupos para Office 365 o Azure Active Directory|[Preparación de Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Microsoft administra su clave de inquilino de Azure Rights Management; no se usa BYOK|[Planeación e implementación de la clave de inquilino de Azure Rights Management](https://technet.microsoft.com/library/dn440580.aspx)|
|Azure Rights Management no está activado|[Activar Rights Management de Azure](https://technet.microsoft.com/library/jj658941.aspx)|
|Uno de los siguientes:<br /><br />- Exchange Online está habilitado para Azure Rights Management<br /><br />- El conector RMS está instalado y configurado para Exchange local|Para Exchange Online: expanda la sección **Exchange Online: IRM Configuration** (Exchange Online: Configuración de IRM) del tema [Configuring Applications for Azure Rights Management](https://technet.microsoft.com/library/jj585031.aspx) (Configuración de aplicaciones para Azure Rights Management).<br /><br />Para Exchange local: [Deploying the Azure Rights Management connector](https://technet.microsoft.com/library/dn375964.aspx) (Implementación del conector de Azure Rights Management).|
|No ha archivado la plantilla predeterminada de Azure Rights Management **&lt;organización&gt; - Confidencial**. O bien, ha configurado una plantilla personalizada para este propósito, porque necesita una configuración más restrictiva o que solo un subconjunto de usuarios de la organización pueda leer los mensajes de correo electrónico protegidos.|[Configuración de plantillas personalizadas para Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)<br /><br />Sugerencia: si necesita una configuración de directiva de uso más restrictiva para todos los usuarios de la organización, copie y modifique una de las plantillas predeterminadas, en lugar de crear una plantilla desde cero.<br /><br />Las plantillas actualizadas no se actualizan inmediatamente para los clientes de correo electrónico en este escenario. Para más información, vea la sección sobre cómo [actualizar plantillas para usuarios](https://technet.microsoft.com/library/dn642472.aspx) del artículo de configuración de plantillas.|
|Los usuarios que envían el correo electrónico protegido tienen Outlook 2013, Outlook 2016 u Outlook Web Access.<br /><br />Los usuarios que reciben el correo electrónico tienen un cliente de correo electrónico que admite Azure Rights Management.|Puede usar Outlook 2010, pero deberá [instalar la aplicación Rights Management sharing para Windows](https://technet.microsoft.com/library/dn339003.aspx) y ajustar las instrucciones de usuario según corresponda.<br /><br />Para ver una lista de clientes de correo electrónico que admiten Azure Rights Management, vea la columna de **correo electrónico** de la tabla de [funciones de dispositivos de cliente](https://technet.microsoft.com/library/dn655136.aspx) del artículo [Requirements for Azure Rights Management](https://technet.microsoft.com/library/dn655136.aspx) (Requisitos de Azure Rights Management).|

## Instrucciones de la documentación del usuario
Con la siguiente plantilla, copie y pegue las instrucciones de usuario en una comunicación dirigida a sus usuarios finales y realice estas modificaciones para reflejar su entorno:

1.  Reemplace todas las instancias de *&lt;nombre de la organización&gt;* por el nombre de su organización.

2.  Reemplace todas las instancias de *&lt;nombre de la organización - Confidencial&gt;* por el nombre de la plantilla predeterminada o personalizada.

3.  Reemplace las capturas de pantalla para que muestren los nombres de plantilla de su organización.

4.  Reemplace *&lt;detalles de contacto&gt;* por instrucciones sobre cómo los usuarios pueden ponerse en contacto con el departamento de soporte técnico, por ejemplo, un vínculo de sitio web, una dirección de correo electrónico o un número de teléfono.

5.  **Otras modificaciones que pueden interesarle:**

    -   Si resulta práctico limitar las instrucciones a un único cliente de correo electrónico, considere la posibilidad de hacerlo por motivos de simplicidad y elimine el otro conjunto de instrucciones.

    -   Si usa una plantilla personalizada en lugar de la plantilla predeterminada sugerida, revise el lenguaje usado según corresponda:

        -   Haga que el título sea más específico.

        -   Especifique los usuarios o grupos que se van a seleccionar en el paso 1.

        -   Especifique el nombre de la plantilla personalizada en el paso 2.

        -   Modifique el último párrafo para explicar las restricciones que tendrán los destinatarios.

6.  Haga los cambios que quiera en este conjunto de instrucciones y, después, envíelo a estos usuarios.

7.  Dado que algunos clientes no admiten Rights Management, tendrá que proporcionar instrucciones y recomendaciones para los destinatarios de estos mensajes de correo electrónico protegidos. Esta información se basará en qué dispositivos y aplicaciones de correo electrónico se usan en su organización y en las preferencias que tenga. Por ejemplo, recomiende a los usuarios de iOS que lean los correos electrónicos protegidos con Outlook para iPad y iPhone, en lugar de con el cliente de correo de iOS nativo.

    Para más información sobre los clientes de correo electrónico, vea la columna de **correo electrónico** de la tabla de [funciones de dispositivos de cliente](https://technet.microsoft.com/library/dn655136.aspx) del artículo [Requirements for Azure Rights Management](https://technet.microsoft.com/library/dn655136.aspx) (Requisitos de Azure Rights Management).

En la documentación de ejemplo se muestra el aspecto de estas instrucciones para los usuarios tras sus personalizaciones.

![Documentación de usuario de la plantilla para la implementación rápida de Azure RMS](../media/AzRMS_UsersBanner.png)

### Procedimiento para enviar correos electrónicos que contienen información confidencial de la empresa mediante Outlook

1.  En Outlook, cree un mensaje de correo, agregue los datos adjuntos que quiera incluir y, después, seleccione usuarios o grupos de *&lt;nombre de la organización&gt;*.

2.  En la pestaña **OPCIONES**, haga clic en **Permiso** y seleccione **&lt;nombre de la organización - Confidencial&gt;**:

    ![Captura de pantalla sobre cómo enviar correos electrónicos que contienen información confidencial de la empresa mediante Outlook](../media/AzRMS_OutlookTemplate.PNG)

3.  Envíe el mensaje.

### Procedimiento para enviar correos electrónicos que contienen información confidencial de la empresa mediante Outlook Web App

1.  En Outlook Web App, cree un mensaje de correo, agregue los datos adjuntos que quiera incluir y, después, seleccione usuarios o grupos de *&lt;nombre de la organización&gt;* en la libreta de direcciones.

2.  Haga clic en **…**, elija **Establecer permisos** y, después, seleccione **&lt;nombre de la organización - Confidencial&gt;**:

    ![Captura de pantalla sobre cómo enviar correos electrónicos que contienen información confidencial de la empresa mediante Outlook Web App](../media/AzRMS_OWATemplate.png)

3.  Envíe el mensaje.

Cuando alguien incluido en las líneas **Para**, **CC** o **CCO** reciba este correo electrónico, puede que tenga que autenticarse para poder leer el mensaje, a fin de constatar que es un usuario de *&lt;nombre de la organización&gt;*. En otras ocasiones, los usuarios no tendrán que autenticarse porque ya lo han hecho.

Los destinatarios a los que envíe el correo electrónico podrán reenviarlo a otras personas, pero solo los usuarios de *&lt;nombre de la organización&gt;* podrán leerlo. Si adjunta un documento de Office, tendrá la misma protección, aun cuando esos datos adjuntos se guarden con un nombre diferente en otra ubicación. Los usuarios autenticados correctamente pueden copiar y pegar desde el correo electrónico o desde los datos adjuntos, así como imprimirlos. Si necesita una protección más restrictiva que impida acciones como las anteriores, póngase en contacto con el departamento de soporte técnico.

**¿Necesita ayuda?**

-   Póngase en contacto con el departamento de soporte técnico:

    -   *&lt;detalles de contacto&gt;*

### Documentación de usuario personalizada de ejemplo
![Documentación de usuario de ejemplo para la implementación rápida de Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Procedimiento para enviar correos electrónicos que contienen información confidencial de la empresa mediante Outlook

1.  En Outlook, cree un mensaje de correo, agregue los datos adjuntos que quiera incluir y, después, seleccione usuarios o grupos de VanArsdel de la libreta de direcciones.

2.  En la pestaña **OPCIONES**, haga clic en **Permiso** y, luego, seleccione **VanArsdel, Ltd - Confidencial**:

    ![Captura de pantalla sobre cómo enviar correos electrónicos que contienen información confidencial de la empresa mediante Outlook](../media/AzRMS_OutlookTemplate.PNG)

3.  Envíe el mensaje.

#### Procedimiento para enviar correos electrónicos que contienen información confidencial de la empresa mediante Outlook Web App

1.  En Outlook Web App, cree un mensaje de correo, agregue los datos adjuntos que quiera incluir y, después, seleccione usuarios o grupos de VanArsdel de la libreta de direcciones.

2.  Haga clic en **…**, haga clic en **Establecer permisos** y, después, seleccione **VanArsdel, Ltd - Confidencial**:

    ![Captura de pantalla sobre cómo enviar correos electrónicos que contienen información confidencial de la empresa mediante Outlook Web App](../media/AzRMS_OWATemplate.png)

3.  Envíe el mensaje.

Cuando alguien incluido en las líneas **Para**, **CC** o **CCO** reciba este correo electrónico, puede que tenga que autenticarse para poder leer el mensaje, a fin de constatar que es un usuario de VanArsdel, Ltd. En otras ocasiones, los usuarios no tendrán que autenticarse porque ya lo han hecho.

Los destinatarios a los que envíe el correo electrónico podrán reenviarlo a otras personas, pero solo los usuarios de VanArsdel podrán leerlo. Si adjunta un documento de Office, tendrá la misma protección, aun cuando esos datos adjuntos se guarden con un nombre diferente en otra ubicación. Los usuarios autenticados correctamente pueden copiar y pegar desde el correo electrónico o desde los datos adjuntos, así como imprimirlos. Si necesita una protección más restrictiva que impida acciones como las anteriores, póngase en contacto con el departamento de soporte técnico.

**¿Necesita ayuda?**

-   Póngase en contacto con el departamento de soporte técnico:

    -   Correo electrónico: helpdesk@vanarsdelltd.com




<!--HONumber=Jul16_HO3-->


