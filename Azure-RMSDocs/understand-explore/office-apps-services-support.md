---
title: Aplicaciones y servicios de Office | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/30/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 99eb67f6296ad1782c787aabb73a28458c02f367
ms.openlocfilehash: affb37cc3b991609f5de51370485b10fed932421


---


# Aplicaciones y servicios de Office

*Se aplica a: Azure Rights Management, Office 365*

Las aplicaciones de Office de usuario final (como Word, Excel, PowerPoint y Outlook) y los servicios de Office (como Exchange y SharePoint) pueden utilizar Microsoft Azure Rights Management con la idea de proteger los datos de su organización.

## Aplicaciones de Office: Word, Excel, PowerPoint, Outlook
Estas aplicaciones admiten de forma nativa Rights Management mediante Information Rights Management (IRM) y permiten a los usuarios aplicar protección a un documento guardado o a un mensaje de correo electrónico que se enviará. Los usuarios pueden aplicar plantillas o, para Word, Excel y PowerPoint, pueden elegir configuraciones muy personalizadas para restricciones de acceso, derechos y uso. 

Por ejemplo, los usuarios pueden configurar un documento de Word para que solamente pueda acceder a él gente de la organización, o controlar si se puede editar una hoja de cálculo de Excel, si se restringe a solo lectura o si se impide que se pueda imprimir. Para archivos sujetos a limitación temporal, se puede configurar una fecha de caducidad (directamente por parte de los usuarios o aplicando una plantilla) en la que ya no se podrá acceder al archivo. Para Outlook, los usuarios pueden elegir la opción **No reenviar** con el fin de evitar la fuga de datos, además de elegir una plantilla.

## Exchange Online y Exchange Server
Cuando usas Exchange Online o Exchange Server, puedes utilizar la integración de Information Rights Management (IRM), que proporciona más soluciones de protección de la información:

-   **Exchange ActiveSync IRM** para que los dispositivos móviles puedan proteger y consumir mensajes de correo electrónico protegidos.

-   Compatibilidad de RMS con **Outlook Web App**, que se implementa de forma similar al cliente de Outlook, para que los usuarios puedan proteger mensajes de correo electrónico mediante plantillas o especificando opciones individuales. Y los usuarios pueden leer y usar los mensajes de correo electrónico protegidos que se les hayan enviado.

-   **Reglas de protección** para clientes de Outlook que un administrador configura para aplicar automáticamente plantillas RMS a mensajes de correo electrónico para destinatarios concretos. Por ejemplo, cuando se envían correos electrónicos internos a tu departamento legal, solo los miembros del departamento legal pueden leerlos y no se pueden reenviar. Los usuarios consultan la protección que se aplicará al mensaje de correo electrónico antes de enviarlo y, de forma predeterminada, pueden quitarla si deciden que no es necesaria. Los correos electrónicos se cifran antes de enviarlos. Para más información, consulte [Reglas de protección de Outlook](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) y [Creación de una regla de protección de Outlook](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) en la biblioteca de Exchange.

-   **Reglas de transporte** que un administrador configura para aplicar automáticamente plantillas de RMS a mensajes de correo electrónico en función de propiedades como el remitente, el destinatario, el asunto del mensaje y el contenido. Dichas reglas son similares en concepto a las reglas de protección, pero no permiten a los usuarios quitar la protección. Se pueden aplicar a Outlook Web Access y a correos electrónicos enviados mediante dispositivos móviles, y no cifra mensajes de correo electrónico antes de que el cliente los envíe. Para más información, consulte [Creación de una regla de protección de transporte](https://technet.microsoft.com/library/dd302432.aspx) en la biblioteca de Exchange.

-   **Directivas de prevención de la pérdida de datos (DLP)** que contienen conjuntos de condiciones para filtrar mensajes de correo electrónico y tomar medidas para tratar de evitar la pérdida de contenido confidencial (por ejemplo, información personal o de tarjetas de crédito). Las sugerencias de las directivas se pueden usar cuando se detectan datos sensibles, para alertar a los usuarios de que es posible que sea necesario aplicar protección de la información, en función de la información del mensaje de correo electrónico. Para más información, consulte [Prevención de pérdida de datos](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) en la biblioteca de Exchange.

-   **Cifrado de mensajes de Office 365** que usa reglas de transporte para enviar correos electrónicos cifrados a personas que están fuera de su compañía y que leen el correo en un explorador con una interfaz similar a la de Outlook Web App. Puedes personalizar el texto de aviso y el texto de cabecera en los correos electrónicos cifrados de tu compañía e, incluso, agregar el logotipo de la compañía. Para más información, consulte [Cifrado de mensajes de Office 365](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx) en el sitio web de Office.

Si usas Exchange Server, puedes utilizar las funciones de protección de la información con [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] implementando el conector RMS, que actúa como un transmisor entre tus servidores locales y el servicio en la nube de RMS. Para más información, consulte [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## SharePoint Online y SharePoint Server
Cuando usas SharePoint Online y SharePoint Server, puedes utilizar la integración Information Rights Management (IRM), que permite a los administradores proteger listas o bibliotecas para que cuando un usuario consulte un documento, el archivo esté protegido para que solo personas autorizadas puedan verlo y usarlo según las directivas de protección de la información que hayas especificado. Por ejemplo, el archivo podría ser de solo lectura, deshabilitar el copiado del texto, evitar que se guarde una copia local e impedir que se pueda imprimir.

Para listas y bibliotecas, la protección de la información siempre se aplica por un administrador, nunca por un usuario final. Y se aplica en el nivel de la lista o la biblioteca para todos los documentos de ese contenedor, en lugar de en archivos individuales.  Si utiliza SharePoint Online, los usuarios también pueden aplicar IRM a su biblioteca de OneDrive para la Empresa.

En primer lugar, el servicio IRM se debe habilitar para SharePoint. A continuación, especifique Information Rights Management para una biblioteca. En el caso de SharePoint Online y OneDrive para la Empresa, los usuarios pueden especificar también Information Rights Management para su biblioteca de OneDrive para la Empresa. SharePoint no usa plantillas de directiva de derechos, aunque hay valores de configuración de SharePoint que se pueden seleccionar que coinciden estrechamente con la configuración que se puede especificar en las plantillas.

Si usas SharePoint Server, puedes utilizar las funciones de protección de la información con [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] implementando el conector RMS, que actúa como una retransmisión entre tus servidores locales y el servicio en la nube de RMS. Para más información, consulte [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).

> [!NOTE]
> Actualmente, hay algunas limitaciones al utilizar IRM con SharePoint:
> 
> -   No puede usar las plantillas predeterminadas o personalizadas que se administran en el Portal de Azure clásico.
> -   Los archivos que tienen una extensión de nombre de archivo .PPDF para archivos PDF protegidos no se admiten. Los archivos que tienen una extensión de nombre de archivo .PDF y que han sido protegidos forma nativa por RMS se admiten cuando se utiliza un lector PDF que admita RMS de forma nativa.
> -   Dado que Office en dispositivos móviles no admite aún RMS, estos dispositivos deben utilizar un explorador para ver los archivos que han sido protegidos con RMS, y los archivos son de solo lectura.

Azure RMS aplica el uso de restricciones y cifrado de datos para documentos cuando se descargan de SharePoint y no cuando el documento se crea primero en SharePoint o se carga en la biblioteca. Para obtener información sobre cómo se protegen los documentos antes de descargarse, consulte [Cifrado de datos en OneDrive para la Empresa y SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) en la documentación de SharePoint.

Para obtener más información acerca del uso de Azure RMS con SharePoint, vea la siguiente entrada del blog de Office: [What’s New with Information Rights Management in SharePoint and SharePoint Online](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)(Novedades de Information Rights Management en SharePoint y SharePoint Online)

## Pasos siguientes

Para ver la compatibilidad de otras aplicaciones y servicios con Azure Rights Management, consulte [Compatibilidad de las aplicaciones con Azure Rights Management](applications-support.md).


<!--HONumber=Jul16_HO3-->


