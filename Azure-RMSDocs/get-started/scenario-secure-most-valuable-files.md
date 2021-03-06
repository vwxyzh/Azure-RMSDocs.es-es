---
title: 'Escenario: Proteger (algunos) archivos de gran valor | Azure RMS'
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 95f1844a-612c-4e67-bbe6-4b6b92295221
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: d4325fb8a0b27d0a8d4fd7451b9d11d10153ed8d


---

# Escenario: Proteger (algunos) archivos de gran valor

*Se aplica a: Azure Rights Management, Office 365*

En este escenario y en la documentación de usuario correspondiente se usa Azure Rights Management para proteger manualmente y de forma personalizada unos pocos archivos que se han identificado como los más valiosos, lo que garantiza el máximo nivel de protección frente a accesos no autorizados. Suelen ser archivos a los que solo algunas personas deben poder tener acceso. Así, recetas detalladas de productos alimenticios de la firma de su empresa o planes de adquisición que no deben hacerse públicos hasta una fecha concreta.

Las instrucciones son adecuadas para el conjunto de circunstancias siguiente:

-   Ha identificado el pequeño conjunto de archivos que hay que proteger.

-   Los archivos están en uno de los formatos de archivo de Office compatibles con Rights Management. Si los archivos están en otros formatos de archivo (por ejemplo, archivos de CAD), asegúrese de que estos formatos son compatibles con Azure RMS y de que implementa aplicaciones que admiten Azure RMS de forma nativa. Para más información, vea [How Applications Support Azure Rights Management](https://technet.microsoft.com/library/jj585004.aspx) (Cómo admiten las aplicaciones Azure Rights Management).

-   Los archivos contienen información extremadamente confidencial a la que solo debe acceder unas pocas personas.

-   Requerir una conexión a Internet para autorizar cada acceso individual a un archivo es una exigencia asumible para estas personas, ya que reporta una mayor seguridad.

-   Estas personas no tienen un requisito expreso de compartir esta información con los demás, pero sí pueden modificar la información y guardar esos cambios.

-   El administrador debe poder realizar un seguimiento de quién tiene acceso a los archivos y cuándo para, de este modo, revocar el acceso si fuera necesario.

## Instrucciones de implementación
![Instrucciones para el administrador para la implementación rápida de Azure RMS](../media/AzRMS_AdminBanner.png)

Asegúrese de que se cumplen los siguientes requisitos y, luego, siga las instrucciones de los procedimientos correspondientes antes de pasar a la documentación del usuario.

## Requisitos para este escenario
Para que este escenario funcione, debe disponer de lo siguiente:

|Requisito|Si necesita más información|
|---------------|--------------------------------|
|Preparó las cuentas y los grupos para Office 365 o Azure Active Directory:<br /><br />- Un grupo habilitado para correo denominado **Acceso con privilegios**, compuesto por las pocas personas que deben tener acceso a estos documentos altamente confidenciales<br /><br />- Un grupo habilitado para correo denominado **Administradores de cumplimiento de TI**, compuesto por las personas encargadas de las tareas de exhibición de documentos electrónicos, auditoría y supervisión<br /><br />- Un grupo habilitado para correo denominado **Administradores de RMS**, del que todos los administradores que configuran Azure RMS son miembros|[Preparación de Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Azure Rights Management no está activado|[Activar Rights Management de Azure](https://technet.microsoft.com/library/jj658941.aspx)|
|Configuró una plantilla personalizada tal y como se describe a continuación|[Configuración de plantillas personalizadas para Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|La aplicación Rights Management sharing se implementa en el equipo de Windows para que estos archivos se puedan proteger de forma local, como se describe en la siguiente sección.|[Descargar e instalar la aplicación para uso compartido de Rights Management](https://technet.microsoft.com/library/dn574734%28v=ws.10%29.aspx)|
|Los usuarios autorizados tienen una versión mínima de Office 2013.|Si tienen Office 2010, también deben instalar la aplicación Rights Management sharing.|
|La suscripción de Azure RMS incluye el seguimiento de documentos|Si la suscripción de Azure RMS no incluye la revocación y el seguimiento de documentos, no podrá usar el sitio de seguimiento de documentos para ver quién tiene acceso a ellos y revocar el acceso en caso necesario. En tal caso, adquiera una suscripción que admita el seguimiento de documentos o asuma esta limitación. Conviene considerar también el uso de las funciones de [registro de uso](https://technet.microsoft.com/library/dn529121.aspx) de Azure RMS (que proporcionan información como, por ejemplo, quién ha tenido acceso a cada archivo y cuándo) con objeto de poder detectar posibles comportamientos sospechosos.<br /><br />Para comprobar la compatibilidad de la suscripción: [Comparación de las ofertas de Rights Management Services (RMS)](https://technet.microsoft.com/dn858608).|

### Para configurar la plantilla personalizada

1.  En el Portal de Azure clásico, cree una plantilla personalizada para Azure Rights Management que contenga estos valores y configuraciones:

    -   Nombre: **Acceso con privilegios**

    -   Permisos: conceda al grupo habilitado para correo **Acceso con privilegios** el permiso **Coautor**

    -   Ámbito: seleccione los grupos habilitados para correo **Acceso con privilegios**, **Administradores de cumplimiento de TI** y **Administradores de RMS**.

    -   Acceso sin conexión: **el contenido está disponible solo con conexión a Internet**

2.  Publique la nueva plantilla.

### Para proteger los archivos localmente

1.  En el Explorador de archivos, vaya a la primera carpeta que contenga archivos que quiere proteger:

    -   Seleccione la carpeta si va a proteger todos los archivos que hay en ella.

    -   Si solo va a proteger algunos archivos de la carpeta, selecciónelos mediante selección múltiple.

2.  Haga clic con el botón derecho, seleccione **Proteger con RMS** y, después, seleccione **Protección local**.

3.  Seleccione **Acceso con privilegios**.

4.  Puede que se le soliciten las credenciales. Espere a que los archivos se protejan y, después, haga clic en **Cerrar** cuando vea la página que indica que **los archivos se protegieron**.

5.  Si tiene más archivos que proteger en otras carpetas, repita los pasos del 1 al 4 en cada carpeta.

Para más información sobre cómo proteger archivos localmente, vea [Proteger un archivo en un dispositivo (protección en contexto) mediante la aplicación de uso compartido Rights Management](https://technet.microsoft.com/library/dn574733%28v=ws.10%29.aspx).

> [!TIP]
> Si el número de archivos que va a proteger es demasiado elevado para hacerlo manualmente, sopese la posibilidad de usar la [herramienta de protección de RMS](https://www.microsoft.com/en-us/download/details.aspx?id=47256) para protegerlos masivamente con la plantilla.

### Para supervisar (y, si es necesario, revocar) el acceso a archivos

1.  En el Explorador de archivos, haga clic con el botón derecho en el archivo protegido, seleccione **Proteger con RMS** y, luego, seleccione **Hacer seguimiento de uso**.

2.  Si se le pide, inicie sesión para tener acceso al sitio de seguimiento de documentos.

3.  Compruebe quién ha tenido acceso al archivo y a los otros archivos protegidos, prestando especial atención a los intentos infructuosos, que pueden ser indicativos de un comportamiento sospechoso. Si lo considera apropiado, puede revocar el acceso a cada archivo.

## Instrucciones de la documentación del usuario
No hay instrucciones específicas para los usuarios sobre este escenario, ya que estos archivos no requieren ninguna acción especial por su parte. Es usted quien ha protegido los archivos y quien los va a supervisar. Con todo, conviene informar a estos usuarios y a los correspondientes canales de soporte de qué archivos están protegidos y cómo esto puede restringir el uso de los documentos. Por ejemplo, si un usuario no autorizado no dispone de conexión a Internet, no podrá abrir el archivo.

Con la siguiente plantilla, copie y pegue el anuncio en una comunicación dirigida a sus usuarios finales y realice estas modificaciones:

1.  Proporcione los nombres reales de los archivos o use una referencia clara que los usuarios autorizados puedan comprender.

2.  Reemplace *&lt;detalles de contacto&gt;* por instrucciones sobre cómo estos usuarios pueden ponerse en contacto con el departamento de soporte técnico o con el departamento de TI mediante un canal de soporte escalado a la altura de la importancia de estos documentos. Por ejemplo, indique un número de teléfono disponible las 24 horas para llamadas de soporte técnico de gravedad alta.

3.  Haga los cambios que quiera en este anuncio y, después, envíelo a estos usuarios.

En la documentación de ejemplo se muestra cómo ven los usuarios este anuncio tras las personalizaciones.

![Documentación de usuario de la plantilla para la implementación rápida de Azure RMS](../media/AzRMS_UsersBanner.png)

### Anuncio de TI: Protección de documentos ultrasecretos de &lt;nombre de la organización&gt;
Ahora los siguientes archivos tienen aplicado un nivel muy alto de protección, de forma que solo los &lt;usuarios restringidos&gt; pueden tener acceso a ellos y modificarlos. Para proteger estos archivos frente a un acceso no autorizado, las aplicaciones le pedirán una autorización cada vez que los abra, por lo que ahora debe tener una conexión a Internet para abrirlos y es posible que se le pidan las credenciales:

-   &lt;documento ultrasecreto, tipo o ubicación 1&gt;

-   &lt;documento ultrasecreto, tipo o ubicación 2&gt;

-   &lt;documento ultrasecreto, tipo o ubicación 3&gt;

**¿Necesita ayuda?**

-   Si no se puede tener acceso a estos archivos o si nota cambios sospechosos en ellos, &lt;acción y detalles de contacto&gt;.

#### Documentación de usuario personalizada de ejemplo
![Documentación de usuario de ejemplo para la implementación rápida de Azure RMS](../media/AzRMS_ExampleBanner.png)

##### Anuncio de TI: Proteger documentos ultrasecretos de VanArsdel
Ahora los siguientes archivos tienen aplicado un nivel muy alto de protección, de forma que solo los usuarios incluidos en la línea Para de este mensaje pueden tener acceso a ellos y modificarlos. Para proteger estos archivos frente a un acceso no autorizado, las aplicaciones le pedirán una autorización cada vez que los abra, por lo que ahora debe tener una conexión a Internet para abrirlos y es posible que se le pidan las credenciales:

-   Especificaciones de diseño para el nombre en código "Mercury"

-   Especificaciones de diseño para el nombre en código "Jupiter"

-   Especificaciones de diseño para el nombre en código "Saturn"

-   Especificaciones de diseño para el nombre en código "Neptune"

**¿Necesita ayuda?**

-   Si no puede tener acceso a estos archivos o si nota cambios sospechosos en ellos, llame a la línea de asignación de nivel de soporte (disponible ininterrumpidamente), que encontrará en un mensaje de correo protegido enviado por el departamento de TI.




<!--HONumber=Jul16_HO3-->


