---
title: "Cómo depurar una aplicación con derechos habilitados | Azure RMS"
description: "En el siguiente tema se muestra cómo depurar la aplicación y utilizar el registro de eventos de Windows."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6F6C7651-6A6E-45DD-A0C5-F036F803249B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 29e856e3e9990f81a791c533ddad5a332093d5d3
ms.openlocfilehash: c00ce9829ce4150cfef74ecd972450b3d787f312


---

# Depuración de una aplicación con derechos habilitados

En el siguiente tema se muestra cómo depurar la aplicación y utilizar el registro de eventos de Windows.

## Depuración de la aplicación

En Rights Management Services SDK 2.1, las comprobaciones contra la depuración en la versión de desarrollador de nuestro tiempo de ejecución están deshabilitadas.

Puede activar el seguimiento de depuración utilizando la siguiente clave del Registro. (Para desactivar el seguimiento de depuración, cambie el valor a 0). No se necesita nada más para la depuración en esta versión.


```
HKEY_LOCAL_MACHINE
   SOFTWARE
      Microsoft
         MSIPC
            "Trace" = 00000001
            Data type
            dword
```

### Registro de aplicaciones mediante el registro de eventos de Windows

El nombre del registro de eventos es "Microsoft-RMS-MSIPC/Debug". Esto significa que, en el Visor de eventos de Windows, el registro aparece como "Registros de aplicaciones y servicios\\Microsoft\\RMS\\MSIPC\\Debug".

**Nota:** El registro está habilitado de forma predeterminada y establecido en el nivel de detalle 3.

 

Para cambiar la configuración de la característica de registro, puede utilizar la interfaz de usuario del Visor de eventos de Windows o Wevtutil, una herramienta de línea de comandos integrada en Windows.

Mediante la interfaz Wevtutil, puede controlar el nivel de detalle del registro.

En este momento, se admiten 3 niveles de registro:

-   Nivel 2: Error
-   Nivel 3: Advertencia
-   Nivel 4: Información

Por ejemplo, el siguiente comando habilitará el registro de eventos de MSIPC y establecerá el nivel de detalle en Información.

**wevtutil sl Microsoft-RMS-MSIPC/Debug /e:true /l:4**

**Nota:** En el Visor de eventos de Windows Event Viewer, en el menú **Ver**, seleccione **Mostrar registros analíticos y de depuración** para que se muestre el registro MSIPC Debug.

 

## Temas relacionados

 

 



<!--HONumber=Jun16_HO4-->


