---
title: "Tipos de aplicación | Azure RMS"
description: En este tema se cubren los tipos de aplicaciones que puede elegir crear como aplicaciones con derechos habilitados.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 97169FC3-1395-4433-A632-7B0F020FABFE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 872bb0c20db2ef8d661d321598a2b1fe61d69316
ms.openlocfilehash: a27d1921336a795df5a3c91b36b97846e74cca34


---

# Tipos de aplicación


En este tema se cubren los tipos de aplicaciones que puede elegir crear como aplicaciones con derechos habilitados.

Los siguientes tipos de aplicación son compatibles actualmente con Rights Management Services SDK 2.1

## Aplicaciones sencillas

Una aplicación sencilla podría ser una herramienta de línea de comandos creada para cifrar un archivo proporcionado. Para ver un ejemplo de una aplicación con derechos habilitados sencilla, consulte [IPCHelloWorld - an example application](how-to-build-your-first-application.md) (IPCHelloWorld: una aplicación de ejemplo).

### Aplicaciones en modo servidor

El *modo servidor* está pensado para aplicaciones no interactivas que consumen, protegen o procesan contenido con protección de RMS. Un ejemplo sería una aplicación de *prevención de pérdida de datos* que se ejecute como servicio en un servidor de archivos y proteja documentos confidenciales. Consulte [IpcDlp sample](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d) (ejemplo IpcDlp) para ver un ejemplo de este tipo de aplicación.

Si su aplicación usa el *modo servidor*, debe autenticarse en el servidor RMS de forma silenciosa. A diferencia del *modo cliente*, RMS SDK 2.1 no abrirá una petición de credenciales si no se autentica de forma silenciosa. Además, al ejecutarse en *modo servidor*, no es necesario ningún manifiesto de aplicación.

Para más información sobre cómo establecer el modo de seguridad de API, consulte [Establecimiento del modo de seguridad de API](setting-the-api-security-mode-api-mode.md).

### Aplicaciones cliente enriquecidas

Una aplicación cliente enriquecida permite a los usuarios ver y manipular datos a través de una interfaz gráfica de usuario (GUI). A menudo, los datos presentados en esta GUI son de gran valor y sensibles al robo o a la exposición accidental. La compatibilidad con la protección de la información suele mejorar los escenarios existentes, pero no es la principal motivación para desarrollar la aplicación.

Usar RMS SDK 2.1 con aplicaciones cliente enriquecidas le ayuda a:

-   Garantizar que estos datos siempre estén cifrados.

-   Impedir que los usuarios extraigan datos a un formato sin protección (por ejemplo, impedir el uso del portapapeles para copiar y pegar).

Microsoft Notepad es una aplicación cliente enriquecida sencilla. Microsoft Office es una aplicación cliente enriquecida más compleja.

Para más información sobre la protección de su aplicación, consulte [Understanding usage restrictions](understanding-usage-restrictions.md) (Descripción de las restricciones de uso).

## Temas relacionados

* [Ejemplo IpcDlp](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d)
* [IPCHelloWorld: una aplicación de ejemplo](how-to-build-your-first-application.md)
* [Establecimiento del modo de seguridad de API](setting-the-api-security-mode-api-mode.md)
* [Descripción de las restricciones de uso](understanding-usage-restrictions.md)



<!--HONumber=Jun16_HO4-->


