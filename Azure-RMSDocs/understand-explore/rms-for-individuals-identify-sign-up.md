---
title: "Cómo averiguar si los usuarios se suscribieron para obtener RMS para usuarios | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: e577366be26f7296079751e72fb6531b9e28c504


---


# Cómo averiguar si los usuarios se suscribieron para obtener RMS para usuarios

*Se aplica a: Azure Rights Management*

Como administrador, ¿cómo sabes si tus usuarios se han registrado para RMS para usuarios? Puede usar uno de estos métodos o combinarlos según su criterio:

-   Pregunte a los usuarios cómo protegen archivos muy confidenciales, especialmente cuando colaboran con otras personas de fuera de la organización.

-   Si tiene una suscripción de Azure para su organización, use el cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) para ver si **RIGHTSMANAGEMENT_ADHOC** se devuelve como una de las suscripciones. Si es así, se trata de la suscripción RMS para usuarios que se concedió a la organización, con un conjunto de unidades activas disponibles para los usuarios que utilicen el proceso de suscripción de autoservicio.

-   Use una solución de administración de sistemas, como System Center Configuration Manager, para inventariar el software instalado y el software en uso. La aplicación de Rights Management sharing se ejecuta mediante el programa **ipviewer.exe** y se puede [descargar e instalar la aplicación](http://go.microsoft.com/fwlink/?LinkId=303970) gratis para identificar otras características sobre esta aplicación que luego usará para el inventario de software.

-   Manténgase atento a las extensiones de nombre de archivos creadas por la aplicación de uso compartido Rights Management. Las extensiones del nombre de archivo .pfile y .ppdf son el ejemplo más notorio, pero hay otros archivos que cambian su extensión de nombre de archivo cuando están protegidos de forma nativa por Rights Management. Para más información, consulte la sección [Tipos de archivo y extensiones de nombre de archivo compatibles](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) en la [Guía del administrador de la aplicación de Rights Management sharing](http://technet.microsoft.com/library/dn339003.aspx).




<!--HONumber=Jun16_HO4-->


