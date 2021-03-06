---
title: "Implementación del conector de Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e31656e417a0861d33deb2436d2e4b596a7512a7
ms.openlocfilehash: 6b9b3b039ba2de0de174a134768afd763d26b5dd


---

# Implementación del conector de Azure Rights Management

*Se aplica a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Use esta información para aprender más sobre el conector de Azure Rights Management (RMS) y sobre cómo puede usarlo para proporcionar protección de la información con implementaciones locales existentes que usan Microsoft Exchange Server, Microsoft SharePoint Server, o servidores de archivo que ejecutan Windows Server y usan la funcionalidad de la Infraestructura de clasificación de archivos (FCI) del Administrador de recursos del servidor de archivos.

> [!TIP]
> Para ver un escenario de ejemplo de alto nivel con capturas de pantalla, consulte la sección [Automatically protecting files on file servers running Windows Server and File Classification Infrastructure](../understand-explore/what-admins-users-see.md#automatically-protecting-files-on-file-servers-running-windows-server-and-file-classification-infrastructure) (Protección de archivos automática en servidores de archivos que ejecutan Windows Server y la infraestructura de clasificación de archivos) del artículo [Azure RMS in action](../understand-explore/what-admins-users-see.md) (Azure RMS en acción).

## Visión general del conector Rights Management de Microsoft
El conector Rights Management (RMS) de Microsoft le permite habilitar rápidamente servidores locales existentes para usar su funcionalidad de Information Rights Management (IRM) con el servicio Rights Management de Microsoft basado en la nube (Azure RMS). Con esta funcionalidad, los TI y los usuarios pueden proteger fácilmente documentos e imágenes tanto dentro como fuera de la organización, sin tener que instalar más infraestructuras o establecer relaciones de confianza con otras organizaciones. Puede usar este conector incluso si algunos de los usuarios se conectan a servicios en línea, en un escenario híbrido. Por ejemplo, los buzones de algunos usuarios usan Exchange Online y los buzones de otros usuarios usan Exchange Server. Después de instalar el conector RMS, todos los usuarios pueden proteger y consumir mensajes de correo electrónico y archivos adjuntos con Azure RMS, y la protección de la información funciona sin problemas entre las dos configuraciones de implementación.

El conector de RMS es un servicio de tamaño reducido que se instala en servidores locales que ejecutan Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2. Además de ejecutar el conector en equipos físicos, también puede ejecutarlo en máquinas virtuales, incluidas las máquinas virtuales de IaaS de Azure. Después de que instalar y configurar el conector, actúa como una interfaz de comunicaciones (una retransmisión) entre servidores locales y el servicio en la nube.

Si administra su propia clave de inquilino para Azure RMS (el escenario "traiga su propia clave" o BYOK), el conector de RMS y los servidores locales que lo usan no tienen acceso al módulo de seguridad de hardware (HSM) que contiene la clave de inquilino. Esto se debe a que todas las operaciones criptográficas que utilizan la clave de inquilino se ejecutan en Azure RMS y no a nivel local.

![Introducción a la arquitectura de conector RMS](../media/RMS_connector.png)

El conector de RMS admite los siguientes servidores locales: Exchange Server, SharePoint Server y servidores de archivos que ejecutan Windows Server y usan la infraestructura de clasificación de archivos para clasificar y aplicar directivas en documentos de Office de una carpeta. Si desea proteger todos los tipos de archivos mediante la clasificación de archivos, no use el conector RMS, sino los [cmdlets de protección de RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE]
> Para más información sobre las versiones compatibles de estos servidores locales, consulte [On-premises servers that support Azure RMS](..\get-started\requirements-servers.md) (Servidores locales que admiten Azure RMS).

Use la información siguiente como ayuda para planear, instalar y configurar el conector de RMS. A continuación, debe modificar la configuración después de la instalación para que sus servidores puedan usar el conector.

-   [Requisitos previos para el conector RMS](deploy-rms-connector.md#prerequisites-for-the-rms-connector)

-   **Paso 1:** [Instalación del conector de RMS](install-configure-rms-connector.md#installing-the-rms-connector)

-   **Paso 2:** [Especificación de credenciales](install-configure-rms-connector.md#entering-credentials)

-   **Paso 3:** [Autorización de los servidores para usar el conector de RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **Paso 4:** [Configuración del equilibrio de carga y alta disponibilidad](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

-   Opcional: [Configuración del conector de RMS para usar HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

-   Opcional: [Configuración del conector de RMS para un servidor proxy web](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

-   Opcional: [Instalación de la herramienta de administración del conector de RMS en equipos administrativos](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **Paso 5:** [Configuración de servidores para usar el conector de RMS](configure-servers-rms-connector.md)

    -   [Configuración de un servidor Exchange para usar el conector](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [Configuración de un servidor SharePoint para usar el conector](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [Configuración de un servidor de archivos para que la Infraestructura de clasificación de archivos use el conector](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## Requisitos previos para el conector RMS
Antes de instalar el conector RMS, asegúrese de que se cumplen los requisitos siguientes.

|Requisito|Más información|
|---------------|--------------------|
|El servicio Rights Management (RMS) está activado|[Activar Rights Management de Azure](activate-service.md)|
|Sincronización de directorios entre los bosques de Active Directory locales y Azure Active Directory|Tras activar RMS, se debe configurar Azure Active Directory para trabajar con los usuarios y grupos de tu base de datos de Active Directory.<br /><br />**Importante**: debe realizar este paso de sincronización de directorios para que el conector de RMS funcione, incluso en una red de prueba. Aunque puede usar Office 365 y Azure Active Directory mediante cuentas que crea manualmente en Azure Active Directory, este conector requiere que las cuentas de Azure Active Directory se sincronicen con Servicios de dominio de Active Directory; la sincronización de contraseñas manual no es suficiente.<br /><br />Para obtener más información, vea los recursos siguientes:<br /><br />[Integración de las identidades locales con Azure Active Directory](/active-directory/active-directory-aadconnect)<br /><br />[Comparación de las herramientas de integración de directorios de identidad híbrida](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison)|
|Opcional pero recomendable:<br /><br />Habilitar la federación entre los Active Directory y Azure Active Directory locales|Puede habilitar la federación de identidades entre sus directorios locales y Azure Active Directory. Esta configuración habilita una experiencia de usuario más sencilla mediante un único inicio de sesión en el servicio RMS. Sin un inicio de sesión único, a los usuarios se les piden sus credenciales para que puedan usar el contenido protegido por derechos.<br /><br />Para obtener información para configurar la federación mediante Active Directory Federation Services (AD FS) entre los Servicios de dominio Active Directory y Azure Active Directory, vea la [Lista de comprobación: Usar AD FS para implementar y administrar inicios de sesión únicos](http://technet.microsoft.com/library/jj205462.aspx) en la biblioteca de Windows Server.|
|Dos equipos miembro como mínimo en los que instalar el conector RMS:<br /><br />- Un equipo virtual o físico de 64 bits ejecuta uno de los siguientes sistemas operativos: Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2.<br /><br />- Como mínimo 1 GB de RAM.<br /><br />- Un mínimo de 64 GB de espacio en disco.<br /><br />- Como mínimo una interfaz de red.<br /><br />- Acceso a Internet a través de un firewall (o proxy web) que no precise autenticación.<br /><br />- Debe encontrarse en un bosque o dominio que confíe en otros bosques de la organización que contengan instalaciones de servidores de Exchange o SharePoint que quiera usar con el conector RMS.|Para la tolerancia a errores y alta disponibilidad, debe instalar el conector RMS como mínimo en dos equipos.<br /><br />**Sugerencia**: Si utiliza Outlook Web Access o dispositivos móviles que emplean Exchange ActiveSync IRM y es fundamental mantener el acceso a correos electrónicos y archivos adjuntos protegidos por Azure RMS, se recomienda implementar un grupo de servidores de conector de carga equilibrada para garantizar una alta disponibilidad.<br /><br />No necesita servidores dedicados para ejecutar el conector pero debe instalarlo en un ordenador independiente respecto a los servidores que usarán el conector.<br /><br />**Importante**: No instale el conector en un equipo que ejecute Exchange Server, SharePoint Server o un servidor de archivos que esté configurado para la infraestructura de clasificación de archivos si quiere usar la funcionalidad desde estos servicios con Azure RMS. Además, no instale este conector en un controlador de dominio.|

## Pasos siguientes

Vaya a [Instalación y configuración del conector de Azure Rights Management](install-configure-rms-connector.md).


<!--HONumber=Jun16_HO4-->


