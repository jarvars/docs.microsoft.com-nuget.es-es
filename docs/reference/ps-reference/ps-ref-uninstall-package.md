---
title: Referencia de PowerShell de Uninstall-Package de NuGet
description: Referencia de Uninstall-Package comando de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237132"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (consola del administrador de paquetes en Visual Studio)

*En este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando genérico de Uninstall-Package de PowerShell, consulte la [referencia de PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Quita un paquete de un proyecto y, opcionalmente, quita sus dependencias. Si existen otros paquetes que dependen de este paquete, el comando fallará a menos que se especifique la opción –Force.

## <a name="syntax"></a>Sintaxis

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Si existen otros paquetes que dependen de este paquete, el comando fallará a menos que se especifique la opción –Force.

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Identificador | Desee Identificador del paquete que se va a desinstalar. El propio modificador-ID es opcional. |
| Versión | Versión del paquete que se va a desinstalar, que tiene como valor predeterminado la versión instalada actualmente. |
| RemoveDependencies | Desinstale el paquete y sus dependencias no usadas. Es decir, si alguna dependencia tiene otro paquete que depende de ella, se omite. |
| ProjectName | Proyecto desde el que se va a desinstalar el paquete. el valor predeterminado es el proyecto predeterminado. |
| Force | Fuerza la desinstalación de un paquete, aunque otros paquetes dependan de él. |
| WhatIf | Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la desinstalación. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Uninstall-Package` admite los siguientes [parámetros comunes de PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```