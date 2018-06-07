---
title: Referencia de PowerShell de NuGet Register-TabExpansion
description: Referencia de comandos de PowerShell de Register-TabExpansion en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8011c0e6aa951a32114d460803c493810964a7e0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818423"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (consola de administrador de paquetes en Visual Studio)

*Disponible solo en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*

Registra una expansión de pestañas para los parámetros del comando especificado, de forma que cuando se usa la ficha al escribir un comando, los valores expandidos aparecen como opciones disponibles para el parámetro en cuestión. Se sobrescriben las expansiones anteriores para el comando.

## <a name="syntax"></a>Sintaxis

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| nombre | (Obligatorio) El comando que se va a registrar las expansiones. -Nombre propio modificador es opcional. |
| de esquema JSON | (Obligatorio) Un objeto que describe el argumento en la sintaxis `@{'<parameter>' = {'<value1>', '<value2>', ...}}` donde `<parameter>` es el nombre del parámetro para modificar y cada uno de ellos `<value>` proporciona una expansión específica. Se aceptan las comillas simples y dobles. |

Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Register-TabExpansion` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

Considere la posibilidad de una solución que contiene los nombres de tres proyectos EventManager, utilidades y SpecialParser. El programador usa con frecuencia el `Update-Package` comando en momentos diferentes a cada uno de esos proyectos. Busca conveniente tener la `Update-Package` comandos proporcionan expansiones de finalización automática para el `-ProjectName` argumento, por lo que no necesita escribir un nombre de proyecto cada vez. 

El siguiente comando, a continuación, registra los nombres de tres proyectos como una expansión de la `-ProjectName` parámetro:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

A continuación, puede escribir el programador `Update-Package -ProjectName `, presione la tecla Tab y vea las expansiones ofrecidas como opciones de finalización automática:

![Ejemplo del uso de registro TabExpansion](media/Register-TabExpansion-Example.png)