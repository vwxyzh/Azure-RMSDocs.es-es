---
title: "Comparación entre Azure Rights Management y AD RMS | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 67129d6cdac124947fc07aa4d42523686227752e
ms.openlocfilehash: ce79ec40cbd8ca3796a17920d27dc3872cd40842


---

# Comparación entre Azure Rights Management y AD RMS

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management, Office 365*

Si conoce o desarrolló con anterioridad Active Directory Rights Management Services (AD RMS), es posible que se pregunte qué similitudes tiene con [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) en cuanto a funcionalidades y requisitos. 

Algunas de las principales diferencias en Azure RMS:

- **No es necesaria una infraestructura de servidor**: Azure RMS no requiere los servidores y certificados PKI adicionales que necesita AD RMS, ya que Microsoft Azure se encarga de esto automáticamente. En consecuencia, esta solución en la nube es más rápida de implementar y fácil de mantener.

- **Autenticación basada en la nube**: Azure RMS usa Azure AD para la autenticación, tanto para los usuarios internos como para los usuarios de otras organizaciones. Esto significa que los usuarios móviles se pueden autenticar incluso cuando no están conectados a la red interna y es más fácil compartir contenido protegido con usuarios de otras organizaciones. Muchas organizaciones ya tienen cuentas de usuario en Azure AD porque ejecutan servicios de Azure o disponen de Office 365. Pero, de no ser así, RMS para usuarios permite a los usuarios crear una cuenta gratuita. Para compartir contenido protegido por AD RMS con otra organización debe configurar relaciones de confianza explícitas con cada organización.

- **Compatibilidad integrada con dispositivos móviles**: no se necesita ningún cambio de implementación para que Azure RMS admita dispositivos móviles y equipos Mac. Para admitir estos dispositivos con AD RMS, debe instalar la extensión para dispositivos móviles, configurar AD FS para la federación y crear registros adicionales para el servicio DNS público.

- **Plantillas predeterminadas**: Azure RMS crea dos plantillas predeterminadas en cuanto se activa el servicio, lo que facilita empezar a proteger datos importantes de inmediato. No hay plantillas predeterminadas para AD RMS.

- **Plantillas de departamento**: Azure RMS admite plantillas de departamento como valor de configuración para las plantillas adicionales que cree. Este valor de configuración permite especificar qué usuarios ven la plantilla en sus aplicaciones cliente (por ejemplo, en aplicaciones de Office), lo que les permite seleccionar fácilmente la directiva correcta que defina para los diferentes grupos de usuarios. AD RMS no es compatible con las plantillas de departamento.

- **Seguimiento de documentos, revocación y notificación por correo electrónico**: Azure RMS admite estas características con la aplicación de RMS sharing, mientras que AD RMS no las admite.


Además, dado que Azure RMS es un servicio en la nube, puede entregar correcciones y características nuevas más rápidamente que una solución local basada en servidor. No hay características nuevas planeadas para AD RMS en Windows Server 2016.

Para obtener más información y conocer otras diferencias, consulte en la tabla siguiente una comparación en paralelo de las características y las ventajas de Azure RMS y AD RMS. Si tiene preguntas acerca de una comparación específica de la seguridad, consulte la sección [Controles criptográficos para firmas y cifrado](compare-azure-rms-ad-rms.md#cryptographic-controls-for-signing-and-encryption) en este artículo.

> [!NOTE]
> Para facilitar esta comparación, parte de la información que se encuentra aquí se repite de[ Requirements for Azure Rights Management](../get-started/requirements-azure-rms.md) (Requisitos para Azure Rights Management). Use este artículo para obtener soporte más específico e información de la versión para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

|Azure RMS|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Admite capacidades de Information Rights Management (IRM) en servicios de Microsoft Online, como Exchange Online y SharePoint Online, así como Office 365.<br /><br />También admite productos de servidor de Microsoft locales, como Exchange Server, SharePoint Server y servidores de archivos que ejecutan Windows Server e Infraestructura de clasificación de archivos (FCI).|Admite productos de servidor de Microsoft locales, como Exchange Server, SharePoint Server y servidores de archivos que ejecutan Windows Server e Infraestructura de clasificación de archivos (FCI).|
|Habilita la confianza implícita entre organizaciones y usuarios de cualquier organización. De este modo, el contenido protegido puede compartirse entre usuarios dentro de la misma organización o entre organizaciones cuando se dispone de [!INCLUDE[o365_1](../includes/o365_1_md.md)] o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], o si los usuarios se registran en RMS para usuarios.|La confianza debe definirse explícitamente en una relación directa de punto a punto entre dos organizaciones mediante el uso de dominios de usuario de confianza (TUD) o confianzas federadas que creas mediante Active Directory Federation Services (AD FS).|
|Proporciona dos plantillas de directivas de derechos predeterminadas que restringen el acceso al contenido a tu propia organización; una que proporciona vista de solo lectura de contenido protegido, y la otra que permite escribir o modificar permisos para el contenido protegido.<br /><br />También puede crear sus propias plantillas personalizadas, incluidas plantillas de departamentos, visibles tan solo para un subconjunto de usuarios. Para más información, consulte [Configuración de plantillas personalizadas para Azure Rights Management](../deploy-use/configure-custom-templates.md).<br /><br />Además, los usuarios pueden definir su propio conjunto de permisos si las plantillas no son suficientes.|No hay plantillas de directivas de derechos predeterminadas, por lo que deberá crearlas y distribuirlas. Para obtener más información, consulte [Consideraciones de la plantilla de directivas para AD RMS](http://go.microsoft.com/fwlink/?LinkId=154765).<br /><br />Además, los usuarios pueden definir su propio conjunto de permisos si las plantillas no son suficientes.|
|La versión mínima compatible de Microsoft Office es Office 2010, que requiere la [aplicación RMS sharing](../rms-client/sharing-app-windows.md).<br /><br />Microsoft Office para Mac:<br /><br />- Microsoft Office para Mac 2016: compatible<br /><br />- Microsoft Office para Mac 2011: no compatible|La versión mínima compatible de Microsoft Office es Office 2007.<br /><br />Microsoft Office para Mac:<br /><br />- Microsoft Office para Mac 2016: compatible<br /><br />- Microsoft Office para Mac 2011: compatible|
|Admite la [aplicación RMS sharing](../rms-client/sharing-app-windows.md) para Windows, equipos Mac y dispositivos móviles.<br /><br />Además, la aplicación de uso compartido de RMS admite lo siguiente:<br /><br />- Uso compartido con personas de otra organización.<br /><br />- Notificación por correo electrónico, que permite al remitente saber cuándo alguien intenta abrir un archivo adjunto protegido.<br /><br />- Un sitio de seguimiento de documentos para los usuarios, que incluye la capacidad de revocar un documento.|Admite la [aplicación RMS sharing](../rms-client/sharing-app-windows.md) para Windows, equipos Mac y dispositivos móviles. Sin embargo, el uso compartido no es compatible con compartir con personas de otra organización, la notificación por correo electrónico o el sitio de seguimiento de documentos y la capacidad de los usuarios de revocar documentos.|
|Todos los tipos de archivo se pueden proteger con [protección genérica o nativa cuando se usa la aplicación RMS sharing](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic).<br /><br />Para otras aplicaciones, vea la tabla de [Requisitos de Azure RMS: aplicaciones](../get-started/requirements-applications.md).|Todos los tipos de archivo se pueden proteger con [protección genérica o nativa cuando se usa la aplicación RMS sharing](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic).<br /><br />Para otras aplicaciones, vea la tabla de [Requisitos de Azure RMS: aplicaciones](../get-started/requirements-applications.md).|
|La versión mínima compatible del cliente Windows es Windows 7.|La versión mínima compatible del cliente Windows es Windows Vista Service Pack 2.|
|El dispositivo móvil es compatible, entre otros, con Windows Phone, Android, iOS y Windows RT.<br /><br />El soporte del correo electrónico mediante Exchange ActiveSync IRM también es compatible en todas las plataformas de dispositivos móviles que admiten este protocolo.|La compatibilidad de dispositivos móviles incluye Windows Phone, Android, iOS y Windows RT, y requiere la [Extensión de Active Directory Rights Management Services para dispositivos móviles](http://technet.microsoft.com/library/dn673574.aspx).<br /><br />El soporte del correo electrónico mediante Exchange ActiveSync IRM es compatible en todas las plataformas de dispositivos móviles que admiten este protocolo.|
|Admite Multi-Factor Authentication (MFA) para equipos y dispositivos móviles.<br /><br />Para más información, consulte [Multi-factor authentication (MFA) and Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms) (Multi-factor Authentication (MFA) y Azure RMS).|Admite la autenticación de tarjeta inteligente si IIS está configurado para solicitar certificados.|
|Es compatible con el Modo criptográfico 2 sin otra configuración adicional, lo que proporciona una mayor seguridad para longitudes de clave y algoritmos de cifrado.<br /><br />Para más información, consulte la sección [Controles criptográficos para firmas y cifrado](#cryptographic-controls-for-signing-and-encryption) de este artículo y [Modos criptográficos de AD RMS](http://go.microsoft.com/fwlink/?LinkId=266659).|Es compatible con el Modo criptográfico 1 de forma predeterminada y precisa configuración adicional para admitir el Modo criptográfico 2 para obtener una mayor seguridad.<br /><br />Para más información, consulte la sección [Controles criptográficos para firmas y cifrado](#cryptographic-controls-for-signing-and-encryption) de este artículo y [Modos criptográficos de AD RMS](http://go.microsoft.com/fwlink/?LinkId=266659).|
|Admite la migración desde AD RMS e incluso, si se requiere, a AD RMS:<br /><br />- [Migración desde AD RMS a Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)<br /><br />- [Retirada y desactivación de Azure Rights Management](../deploy-use/decommission-deactivate.md)|Admite la migración desde Azure RMS y a Azure RMS:<br /><br />- [Retirada y desactivación de Azure Rights Management](../deploy-use/decommission-deactivate.md)<br /><br />- [Migración desde AD RMS a Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)|
|Requiere una licencia de RMS para proteger el contenido. No se requieren licencias de RMS para consumir el contenido que ha protegido Azure RMS (incluye usuarios de otra organización).<br /><br />Para información, consulte la sección [Cloud subscriptions that support Azure RMS](../get-started/requirements-subscriptions.md) (Suscripciones en la nube que son compatibles con Azure RMS).|Requiere una licencia de RMS para proteger el contenido y para consumir el contenido que ha protegido AD RMS.<br /><br />Para obtener más información acerca de licencias de AD RMS, consulte [Licencias de acceso de cliente y licencias de administración](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) , donde encontrará información general, pero si desea información más específica, póngase en contacto con un partner o representante de Microsoft.|

## Controles criptográficos para firmas y cifrado
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] usa siempre RSA 2048 para toda la criptografía de claves públicas y SHA 256 para operaciones de firma. En comparación, AD RMS admite RSA 1024 y RSA 2048, y SHA 1 o SHA 256 para operaciones de firma.

Tanto [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] como AD RMS usan AES 128 para cifrado simétrico.

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] cumple con FIPS 140-2 cuando la clave de inquilino la crea y la administra Microsoft (de forma predeterminada), o si la administra usted mismo (lo que se conoce como BYOK). Para más información sobre la administración de la clave de inquilino, consulte [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

## Pasos siguientes
Si quiere migrar de AD RMS a Azure RMS, consulte [Migración desde AD RMS a Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).





<!--HONumber=Jul16_HO3-->


