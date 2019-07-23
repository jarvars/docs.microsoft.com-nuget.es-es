---
title: Comando de reflejo de la CLI de NuGet
description: Referencia del comando de reflejo Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327672"
---
# <a name="mirror-command-nuget-cli"></a>Comando mirror (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles** de publicación de paquetes: desusados en 3,2 +

Refleja un paquete y sus dependencias de los repositorios de origen especificados en el repositorio de destino.

> [!NOTE]
> Para habilitar este comando para las versiones de NuGet anteriores a 3,2 [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), vaya a, seleccione la versión estable `NuGet.ServerExtensions.dll` más `Nuget-Signed.exe` reciente, descargue y en el disco `Nuget-Signed.exe` local `nuget.exe` y cambie el nombre a.

## <a name="usage"></a>Uso

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

donde `<packageID>` es el paquete que se va a `<configFilePath>` reflejar, `packages.config` o identifica el archivo que muestra los paquetes que se van a reflejar.

Especifica el repositorio de origen y `<publishUrlTarget>` especifica el repositorio de destino. `<listUrlTarget>`

Si el repositorio de destino se `https://machine/repo` encuentra en que ejecuta [NuGet. Server](../../hosting-packages/nuget-server.md), la lista y las direcciones URL `https://machine/repo/nuget` de `https://machine/repo/api/v2/package`inserciones serán y, respectivamente.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| ApiKey | La clave de API para el repositorio de destino. Si no está presente, se usa el especificado en el archivo de configuración`%AppData%\NuGet\NuGet.Config` ((Windows) `~/.nuget/NuGet/NuGet.Config` o (Mac/Linux)). |
| Help | Muestra información de ayuda para el comando. |
| NoCache | Impide que NuGet use paquetes almacenados en caché. Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Registra lo que se haría pero no realiza las acciones; supone que las operaciones de inserciones se han realizado correctamente. |
| Versión preliminar | Incluye paquetes de versión preliminar en la operación de creación de reflejo. |
| source | Una lista de orígenes de paquetes que se van a reflejar. Si no se especifican orígenes, se usan los definidos en el archivo de configuración (vea ApiKey anterior), de forma predeterminada se usa nuget.org si no se especifica ninguno. |
| Tiempo de espera | Especifica el tiempo de espera, en segundos, para insertar en un servidor. El valor predeterminado es 300 segundos (5 minutos). |
| `Version` | Versión del paquete que se va a instalar. Si no se especifica, la versión más reciente está reflejada. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```