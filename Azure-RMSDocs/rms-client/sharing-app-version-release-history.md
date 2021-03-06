---
title: "Aplicación Rights Management sharing&colon; Historial de publicación de versiones | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e1b7dedd8556f3ccdb1642681cc4e1e5b1d09ccf
ms.openlocfilehash: ee2860da964b52bc41c0aea219110453f024b954


---

# Aplicación de uso compartido Rights Management Historial de publicación de versiones

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

El equipo de Rights Management actualiza periódicamente la aplicación para uso compartido de Rights Management con correcciones y nuevas funcionalidades. Use la información siguiente para ver las novedades o los cambios de una versión. La versión más reciente aparece en primer lugar.

No se enumeran las versiones anteriores al 1 de enero de 2015.

> [!NOTE]
> Si tiene comentarios o alguna pregunta sobre la aplicación de uso compartido de RMS, envíe un mensaje de correo electrónico a [AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question).

## Versión 1.0.2217.0

**Lanzamiento**: 13/07/2016

**Correcciones**:

- Los usuarios de organizaciones que usan la federación y Multi-Factor Authentication ya no reciben el error 0x800704DC al proteger el contenido.



## Versión 1.0.2191.0
**Lanzamiento**: 16/06/2016

**Correcciones**:

- Ahora, el sitio de seguimiento de documentos muestra el número correcto de vistas de cada documento al que se realiza el seguimiento.

- Ahora se muestran como disponibles a los usuarios las plantillas para todas las configuraciones regionales.

- Después de usar el uso compartido seguro de un archivo de PowerPoint, los cambios en la versión local del archivo se guardan correctamente.

- Pequeño número de errores menores y mejoras de los mensajes de error.


## Versión 1.0.2004.0
**Lanzamiento**: 11/12/2015

**Correcciones**:

-   Solo el propietario del archivo y las personas con niveles de permisos de **Copropietario** pueden desproteger archivos. Anteriormente, el propietario y las personas con niveles de permisos de **Coautor** y **Copropietario** podían desproteger archivos.

-   Protección nativa para archivos **.tif** (además de archivos .tiff), para generar un archivo **.ptif** de solo lectura protegido por RMS.

-   Mejoras para los mensajes de error (precisión y claridad).

-   Mejoras de rendimiento para cifrar y descifrar el contenido.

**Nuevas características**:

-   Soporte para instalación por parte de usuarios que no sean administradores para que los usuarios estándar puedan instalar la aplicación de uso compartido RMS.

    Hay algunas restricciones para los usuarios estándar que ejecuten Office 2010. Para más información, consulte la sección [Si no es administrador local y usa Office 2010](install-sharing-app.md#if-you-are-not-a-local-administrator-and-use-office-2010) en las instrucciones para el usuario de [Descarga e instalación de la aplicación Rights Management sharing](install-sharing-app.md).

## Versión 1.0.1908.0
**Lanzamiento**: 16/09/2015

**Correcciones**:

-   Compatibilidad con Multi-Factor Authentication (MFA) para Azure RMS, que también elimina la dependencia del Ayudante para el inicio de sesión de Microsoft en aplicaciones que usan la autenticación moderna.

    Para más información, consulte la sección [Multi-Factor Authentication (MFA) y Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms) en [Requisitos de Azure Rights Management](../get-started/requirements-azure-rms.md).

## Versión 1.0.1784.0
**Lanzamiento**: 30/07/2015

**Correcciones**:

-   El intervalo de actualización predeterminado para las plantillas de directiva de derechos se reduce de 7 días a 1 día.

-   Número reducido de regresiones y errores menores.

## Versión 1.0.1770.0
**Lanzamiento**: 25/04/2015

**Correcciones**:

-   Ahora, solo los propietarios y los copropietarios pueden quitar la protección. Los coautores no pueden quitar la protección.

-   Ahora se pueden proteger los archivos que están en un recurso compartido de red.

**Nuevas características**:

-   Compatibilidad con la revocación y el seguimiento de documentos. Para más información, consulte [Seguimiento y revocación de documentos cuando se usa la aplicación RMS sharing](sharing-app-track-revoke.md).

-   Compatibilidad con plantillas al elegir **Uso compartido seguro**:

    -   ahora puede seleccionar plantillas.

    -   En lugar del control deslizante, verá un cuadro de lista que incluye las plantillas y los permisos personalizados.

    -   Ya no verá las opciones **Permitir consumo en todos los dispositivos** y **Aplicar restricciones de uso**. En su lugar, se activa automáticamente **Protección genérica** , en función del tipo de archivo.

    Para más información, consulte [Opciones de cuadro de diálogo para la aplicación Rights Management sharing](sharing-app-dialog-box.md).

## Versión 1.0.1667.0
**Lanzamiento**: 19/01/2015

**Correcciones**:

-   Compatibilidad con fuentes del idioma chino en el visor de PPDF de la aplicación de uso compartido de RMS.

-   Control de errores y mensajería mejorados.

-   Corrección de un problema con la notificación de actualización automática cuando hay una versión más reciente de la aplicación disponible para descargar.

**Nuevas características**:

-   **Compatibilidad con varios dominios de correo electrónico dentro de su organización**: Si usa AD RMS y los usuarios de su organización tienen varios dominios de correo electrónico, esta actualización permite que los usuarios consuman contenido que protegieron los usuarios de la organización en otros dominios. Para más información, consulte la sección [Solo AD RMS: Compatibilidad con varios dominios de correo electrónico dentro de su organización](sharing-app-admin-guide.md#ad-rms-only-support-for-multiple-email-domains-within-your-organization) de la [Guía del administrador de la aplicación Microsoft Rights Management sharing](sharing-app-admin-guide.md).




<!--HONumber=Jul16_HO3-->


