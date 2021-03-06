---
title: "Script de Windows PowerShell para la protección de Azure RMS con FCI del Administrador de recursos del servidor de archivos | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ae6d8d0f-4ebc-43fe-a1f6-26b690fd83d0
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: a1771c37bffa2af60773a5befdd35c14f684c942


---

# Script de Windows PowerShell para la protección de Azure RMS con FCI del Administrador de recursos del servidor de archivos

*Se aplica a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Esta página contiene el script de ejemplo para copiar y editar, como se describe en [RMS protection with Windows Server File Classification Infrastructure](configure-fci.md) (Protección de RMS con la infraestructura de clasificación de archivos de Windows Server).

*&#42;&#42;Aviso de declinación de responsabilidades&#42;&#42;: este script de ejemplo no es compatible con ningún servicio o programa de soporte técnico estándar de Microsoft. Este script*
*de ejemplo se proporciona TAL CUAL sin garantía de ningún tipo.*

```
<#
.SYNOPSIS 
     Helper script to protect all file types with Azure RMS and FCI.
.DESCRIPTION
     Protect files with Azure RMS and Windows Server FCI, using an RMS template ID.   
#>
param(
            [Parameter(Mandatory = $false)]
            [ValidateScript({ If($_ -eq "") {$true} else { if (Test-Path -Path $_ -PathType Leaf) {$true} else {throw "Can't find file specified"} } })]
            [string]$File,

            [Parameter(Mandatory = $false)]
            [string]$TemplateID,

            [Parameter(Mandatory = $false)]
            [string]$OwnerMail,

            [Parameter(Mandatory = $false)]
            [string]$AppPrincipalId = "<enter your AppPrincipalId here>",

            [Parameter(Mandatory = $false)]
            [string]$SymmetricKey = "<enter your key here>",

            [Parameter(Mandatory = $false)]
            [string]$BposTenantId = "<enter your BposTenantId here>"
) 

# script information
[String] $Script:Version = 'version 1.0' 
[String] $Script:Name = "RMS-Protect-FCI.ps1"

#global working variables
[switch] $Script:isScriptProcess = $False # Controls the script process. If false, the script gracefully stops running.

#**Functions (general helper)***************************************
function Get-ScriptName(){ 

    return $MyInvocation.ScriptName.Substring($MyInvocation.ScriptName.LastIndexOf('\') + 1, $MyInvocation.ScriptName.LastIndexOf('.') - $MyInvocation.ScriptName.LastIndexOf('\') - 1)
}

#**Functions (script specific)**************************************

function Check-Module{

    param ([String]$Module = $(Throw "Module name not specified"))

    [bool]$isResult = $False

    #try to load the module
    if (get-module -list -name $Module) {
        import-module $Module

        if (get-module -name $Module ) {

            $isResult = $True
        } else {
            $isResult = $False
        } 

    } else {
            $isResult = $False
    }
    return $isResult
}

function Protect-File ($ffile, $ftemplateId, $fownermail) {

    [bool] $returnValue = $false
    try {
        If ($OwnerMail -eq $null -or $OwnerMail -eq "") {
            $protectReturn = Protect-RMSFile -File $ffile -TemplateID $ftemplateId
            $returnValue = $true
            Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId")
        } else {
            $protectReturn = Protect-RMSFile -File $ffile -TemplateID $ftemplateId -OwnerEmail $fownermail
            $returnValue = $true
            Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId, set Owner: $fownermail")
        }
    } catch {
        Write-Host ( "ERROR" + "During protection of file: $ffile with Template: $ftemplateId")
            }
    return $returnValue
}

function Set-RMSConnection ($fappId, $fkey, $fbposId) {

    [bool] $returnValue = $false
    try {
               Set-RMSServerAuthentication -AppPrincipalId $fappId -Key $fkey -BposTenantId $fbposId
        Write-Host ("Information: " + "Connected to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId")
        $returnValue = $true
    } catch {
        Write-Host ("ERROR" + "During connection to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId")

    }
    return $returnValue
}

#**Main Script (Script)*********************************************
Write-Host ("-== " + $Script:Name + " " + $Version + " ==-")

$Script:isScriptProcess = $True

# Validate Azure RMS connection by checking the module and then connection
if ($Script:isScriptProcess) {
        if (Check-Module -Module RMSProtection){
        $Script:isScriptProcess = $True
    } else {

        Write-Host ("The RMSProtection module is not loaded") -foregroundcolor "yellow" -backgroundcolor "black"            
        $Script:isScriptProcess = $False
    }
}

if ($Script:isScriptProcess) {
    #Write-Host ("Try to connect to Azure RMS with AppId: $AppPrincipalId and BPOSID: $BposTenantId" )  
    if (Set-RMSConnection $AppPrincipalId $SymmetricKey $BposTenantId) {
        Write-Host ("Connected to Azure RMS")

    } else {
        Write-Host ("Couldn't connect to Azure RMS") -foregroundcolor "yellow" -backgroundcolor "black"
        $Script:isScriptProcess = $False
    }
}

#  Start working loop
if ($Script:isScriptProcess) {
    if ( !(($File -eq $null) -or ($File -eq "")) ) {
        if (!(Protect-File -ffile $File -ftemplateId $TemplateID -fownermail $OwnerMail)) {
            $Script:isScriptProcess = $False           
        }
    }
}

# Closing
if (!$Script:isScriptProcess) { Write-Host "ERROR occurred during script process" -foregroundcolor "red" -backgroundcolor "black"}
write-host ("-== " + $Script:Name + " " + $Version + "  ==-")
if (!$Script:isScriptProcess) { exit(-1) } else {exit(0)}
```

---

Volver a [RMS protection with Windows Server File Classification Infrastructure](configure-fci.md) (Protección de RMS con la infraestructura de clasificación de archivos de Windows Server).



<!--HONumber=Jun16_HO4-->


