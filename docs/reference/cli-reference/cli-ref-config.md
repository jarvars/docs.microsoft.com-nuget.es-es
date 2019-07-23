---
title: Comando de configuración de la CLI de NuGet
description: Referencia del comando de configuración de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 51c4c9937483e7f8a57356515c06a60c0f9e6f62
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327852"
---
# <a name="config-command-nuget-cli"></a>comando config (CLI de NuGet)

**Se aplica a:** todas &bullet; **las versiones compatibles**: todas

Obtiene o establece los valores de configuración de NuGet. Para obtener más uso, consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md). Para obtener más información sobre los nombres de clave permitidos, consulte la [Referencia del archivo de configuración de NuGet](../nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

donde `<name>` y`<value>` especifican un par clave-valor que se establecerá en la configuración. Puede especificar tantos pares como desee. Para quitar un valor, especifique el nombre y el `=` signo pero no el valor.

Para ver los nombres de clave permitidos, consulte la [Referencia del archivo de configuración de NuGet](../nuget-config-file.md).

En NuGet 3.4 +, `<value>` puede usar [variables de entorno](cli-ref-environment-variables.md).

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| AsPath | Devuelve el valor de configuración como una ruta de acceso `-Set` , que se omite cuando se usa. |
| ConfigFile | El archivo de configuración de NuGet que se va a modificar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el comando. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

### <a name="examples"></a>Ejemplos

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```