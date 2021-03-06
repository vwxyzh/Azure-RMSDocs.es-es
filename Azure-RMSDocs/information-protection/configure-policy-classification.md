---
title: "Configuración de las condiciones para la clasificación automática y recomendada en Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 80c201dcf316a5aa5e123645d47c6741f8b61f05


---

# Configuración de las condiciones para la clasificación automática y recomendada en Azure Information Protection

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Al configurar las condiciones de una etiqueta, puede asignar automáticamente la etiqueta a un documento o a un correo electrónico. También puede indicar a los usuarios que seleccionen la etiqueta que usted recomienda: 

- La clasificación automática se aplica a Word, Excel y PowerPoint cuando se guardan archivos, y a Outlook cuando se envían correos electrónicos. No se puede utilizar la clasificación automática para archivos que anteriormente se etiquetaron manualmente.
 
- La clasificación recomendada se aplica a Word, Excel y PowerPoint cuando se guardan archivos.

Al configurar condiciones, puede usar patrones predefinidos, como "Números de tarjeta de crédito" o "Número de la Seguridad Social de EE. UU.". O puede definir un patrón o una cadena personalizada como condición de una clasificación automática. Para más información sobre las condiciones, consulte la sección [Información sobre las condiciones integradas](#information-about-the-built-in-conditions).

Modo de evaluar varias condiciones cuando se aplican a más de una etiqueta:

1. Las etiquetas se ordenan para la evaluación, según la posición que especifique en la directiva: la etiqueta que se coloca al principio tiene la posición más baja (menos sensible) y la etiqueta que se coloca al final la más alta (más sensible).

2. Se aplica la etiqueta más sensible.
 
3. Se aplica la última etiqueta secundaria.

> [!TIP]
>Para conseguir la mejor experiencia de usuario y garantizar la continuidad empresarial, conviene comenzar con la clasificación recomendada al usuario, en lugar de la clasificación automática. Esta configuración ofrece a los usuarios la posibilidad de aceptar la acción de etiquetado o protección, o de reemplazar estas sugerencias si no resultan adecuadas para su documento o mensaje de correo electrónico.

Mensaje de ejemplo cuando se configura una condición para aplicar una etiqueta como acción recomendada, con una sugerencia de directiva personalizada:

![Detección y recomendación de Azure Information Protection](../media/info-protect-recommend-callouts.png)

En este ejemplo, el usuario puede hacer clic en **Cambiar ahora** para aplicar la etiqueta recomendada, o bien reemplazar la recomendación, cerrando la barra.

## Para configurar la clasificación automática o recomendada para una etiqueta

1. Si aún no lo ha hecho, inicie sesión en el [portal de Azure](https://portal.azure.com) y, después, navegue hasta la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Examinar** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la hoja **Azure Information Protection**, seleccione la etiqueta que quiere configurar para clasificación automática o recomendada.

3. En la hoja **Etiqueta**, en la sección **Configure conditions for automatically applying this label** (Configurar condiciones para aplicar esta etiqueta automáticamente), haga clic en **Agregar una nueva condición**(Add a new condition).

4. En la hoja **Condición**, seleccione **Built-in** (Integrada) si quiere usar una condición predefinida, o **Personalizada** si quiere especificar la suya propia, y luego haga clic en **Guardar**:

    - En **Built-in** (Integrada): seleccione entre las condiciones disponibles de la lista y luego elija el número mínimo de repeticiones y si la repetición debe tener un valor único para ser incluida en el recuento de repeticiones.
        
        Para más información sobre las reglas de detección de estas condiciones y algunos ejemplos, consulte la sección [Información sobre las condiciones integradas](#information-about-the-built-in-conditions).

    - En **Personalizada**: especifique un nombre y una frase para buscar coincidencia, sin comillas ni caracteres especiales. A continuación, especifique si la coincidencia será una expresión regular, si se usará distinción entre mayúsculas y minúsculas y el número mínimo de repeticiones, y si la repetición deberá tener un valor único para incluirse en el recuento de repeticiones.
        
    **Ejemplo de opciones de repeticiones**: seleccionará la opción integrada de número de la seguridad social y establecerá el número mínimo de repeticiones en 2. En un documento se muestra el mismo número de la seguridad social dos veces: si establece **Count occurrences with unique values only** (Contar solo las repeticiones con valores únicos) en **On** (Activado), la condición no se cumpliría; si establece esta opción en **Off** (Desactivado), la condición se cumpliría.

5. En la hoja **Etiqueta**, configure lo siguiente y luego haga clic en **Guardar**:

    - Elija clasificación automática o recomendada: en **Select how this label is applied: automatically or recommended to user** (Seleccionar cómo se aplica esta etiqueta: automáticamente o recomendado al usuario), seleccione **Automática** o **Recomendada**.

    - Especifique el texto del mensaje de usuario o de la sugerencia de directiva: mantenga el texto predeterminado o especifique su propia cadena.

6. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

## Información sobre las condiciones integradas

Durante el período de versión preliminar, puede seleccionar las siguientes condiciones:

- [Código SWIFT](#swift-code )

- [Número de la tarjeta de crédito](#credit-card-number )

- [Número de enrutamiento ABA](#aba-routing-number )

- [Número de la Seguridad Social (SSN) de EE. UU.](#usa-social-security-number-ssn)

- [Número de cuenta bancaria internacional (IBAN)](#international-banking-account-number-iban)


### Código SWIFT

Busque coincidencia con este tipo de información cuando el contenido incluya lo siguiente:  

1. Una de las siguientes frases: **swift**, **swiftnumber**, **swiftroutingnumber** 

2. Un código Swift, en un patrón con formato:  

    a. 4 letras (código del banco)  

    b. 2 letras (código de país)  

    c. 2 letras o dígitos (código de ubicación)  

    d. 3 letras o dígitos opcionales (código de sucursal)  


Ejemplos para prueba:

- **NEDSZAJJXXX Swiftroutingnumber**

- **NEDSZAJJ100 Swiftnumber** 

----


### Número de la tarjeta de crédito

Busque coincidencia con este tipo de información cuando el contenido incluya lo siguiente:  

- Un número de tarjeta de crédito válido, en un patrón con formato o sin formato, que pase la [comprobación de Luhn](https://wikipedia.org/wiki/Luhn_algorithm). Este tipo de información detecta tarjetas de todas las principales marcas del mundo, como Visa, MasterCard, Discover Card, American Express y Diners.

    - **Con formato**:
    
        - 16 dígitos: (dddd-dddd-dddd-dddd)  
        
    - **Sin formato**:
    
        - (dddddddddddddddd)  


Ejemplos para prueba:

- **4242-4242-4242-4242**

- **4242424242424242** 

----

### Número de enrutamiento ABA

Busque coincidencia con este tipo de información cuando el contenido incluya lo siguiente:  

1. Al menos una de las siguientes frases: **aba**, **rtn**, **número de enrutamiento** 

2. Un número de enrutamiento ABA, que incluye 9 dígitos que pueden estar en un patrón con formato o sin formato: 

    - **Con formato**: 
        
        a. Cuatro dígitos que comienzan con 0, 1, 2, 3, 6, 7 o 8 
        
        b. Un guión 
        
        c. Cuatro dígitos 
        
        d. Un guión 
        
        e. Un dígito 
        
        Ejemplo: 3456 9876 1 ABA 
        
    - **Sin formato**: 
        
        9 dígitos consecutivos que comienzan con 0, 1, 2, 3, 6, 7 o 8 
        
        Ejemplo: 345698761 RTN 
 

Ejemplos para prueba:

- **3456-9876-1 ABA**

- **345698761 RTN** 

----

### Número de la Seguridad Social (SSN) de EE. UU.

Busque coincidencia con este tipo de información cuando el contenido incluya lo siguiente:  

1. Al menos una de las siguientes frases: **ssn**, **seguridad social**, **ssid**, **ss#** 

2. Un número de la Seguridad Social: 9 dígitos, que pueden estar en un patrón con formato o sin formato:

    - **Con formato**: 
    
        - Nueve dígitos en el siguiente formato: dd-ddd-dddd o ddd dd dddd 
        
    - **Sin formato**: 
    
        - Nueve dígitos en el siguiente formato: ddddddddd 


Ejemplos para prueba:

- **SSN 123-45-6789**

- **N.º SS 123456789** 


----

### Número de cuenta bancaria internacional (IBAN)

Busque coincidencia con este tipo de información cuando el contenido incluya lo siguiente:  

1. La siguiente frase: **IBAN** 

2. Un número IBAN: comienza con un código de país (dos letras), le siguen dígitos de comprobación (dos) y luego el número bban (hasta 30 dígitos).


Ejemplos para prueba:

- **GB29 NWBK 6016 1331 9268 19 IBAN**


## Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configuración de la directiva de la organización).  






<!--HONumber=Aug16_HO2-->


