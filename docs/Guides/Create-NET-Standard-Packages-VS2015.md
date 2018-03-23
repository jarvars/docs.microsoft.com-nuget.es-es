---
title: Crear paquetes de NuGet de .NET Standard con Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Tutorial completo para crear paquetes de NuGet de .NET Standard mediante NuGet 3.x y Visual Studio 2015.
keywords: "crear un paquete, paquetes de .NET Standard, tabla de asignación de .NET Standard"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: abf6a56cbc84bdd066e31e77c7883825a8456144
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Crear paquetes de .NET Standard con Visual Studio 2015

*Se aplica a NuGet 3.x. Vea [Creación y publicación de un paquete de .NET Standard](../quickstart/create-and-publish-a-package-using-visual-studio.md) para trabajar con NuGet 4.x+.*

La [biblioteca .NET Standard](/dotnet/articles/standard/library) es una especificación formal de las API de .NET diseñada para estar disponible en todos los runtimes de .NET, lo que establece mayor uniformidad en el ecosistema de .NET. La biblioteca de .NET Standard define un conjunto uniforme de API de BCL (biblioteca de clases base) para que todas las plataformas de .NET lo implementen, independientemente de la carga de trabajo. Permite a los desarrolladores generar código que se pueda usar en todos los runtimes de .NET y reduce, si no las elimina, las directivas de compilación condicional específicas de la plataforma en código compartido.

En esta guía se describe la creación de un paquete NuGet que tiene como destino la biblioteca de .NET Standard 1.4. Dicha biblioteca funcionará en .NET Framework 4.6.1, Plataforma universal de Windows 10, .NET Core y Mono/Xamarin. Para más información, vea la [tabla de asignación de .NET Standard](#net-standard-mapping-table), que aparece más adelante en este tema.

## <a name="prerequisites"></a>Requisitos previos

1. Visual Studio 2015 Update 3
1. [SDK de .NET Core](https://www.microsoft.com/net/download/)
1. CLI de NuGet. Descargue la versión más reciente de nuget.exe desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en una ubicación de su elección. Después, agregue esa ubicación a la variable de entorno PATH si aún no está.

    > [!Note]
    > nuget.exe es la propia herramienta de la CLI, no un instalador, por lo que debe asegurarse de guardar el archivo descargado desde el explorador en lugar de ejecutarlo.

## <a name="create-the-class-library-project"></a>Crear el proyecto de biblioteca de clases

1. En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > Windows**, seleccione **Biblioteca de clases (portable)**, cambie el nombre a AppLogger y haga clic en Aceptar.

    ![Crear otro proyecto de biblioteca de clases](media/NetStandard-NewProject.png)

1. En el cuadro de diálogo **Agregar Biblioteca de clases portable** que aparece, seleccione las opciones `.NET Framework 4.6` y `ASP.NET Core 1.0`.

1. Haga clic con el botón derecho en `AppLogger (Portable)` en el Explorador de soluciones, seleccione **Propiedades**, seleccione la pestaña **Biblioteca** y, luego, haga clic en **Usar como destino la plataforma del estándar .NET** en la sección **Destino**. Se le pedirá que lo confirme. Después, podrá seleccionar `.NET Standard 1.4` en la lista desplegable:

    ![Establecer el destino en .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Haga clic en la pestaña **Compilar**, cambie la **configuración** a `Release` y active la casilla de **Archivo de documentación XML**.

1. Agregue el código al componente, por ejemplo:

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Establezca la configuración en Liberar, compile el proyecto y compruebe que los archivos DLL y XML se crean dentro de la carpeta `bin\Release`.

## <a name="create-and-update-the-nuspec-file"></a>Crear y actualizar el archivo .nuspec

1. Abra un símbolo del sistema, vaya a la carpeta que contiene la carpeta `AppLogger.csproj` (que está un nivel por debajo de la ubicación del archivo `.sln`) y ejecute el comando `spec` de NuGet para crear el archivo `AppLogger.nuspec` inicial:

    ```cli
    nuget spec
    ```

1. Abra `AppLogger.nuspec` en un editor y actualícelo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado. El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. Agregue ensamblados de referencia al archivo `.nuspec`, es decir, el archivo DLL de la biblioteca y el archivo XML de IntelliSense:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. Haga clic con el botón derecho en la solución y seleccione **Compilar solución** para generar todos los archivos del paquete.

### <a name="declaring-dependencies"></a>Declarar dependencias

Si tiene dependencias en otros paquetes de NuGet, muéstrelos en una lista en el elemento `<dependencies>` del manifiesto con elementos `<group>`. Por ejemplo, para declarar una dependencia en NewtonSoft.Json 8.0.3 o en una versión posterior, agregue lo siguiente:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

La sintaxis del atributo *version* aquí indica que la versión 8.0.3 o una versión posterior es aceptable. Para especificar distintos intervalos de versiones, vea [Control de versiones de paquetes](../reference/package-versioning.md).

### <a name="adding-a-readme"></a>Agregar un archivo Léame

Cree el archivo `readme.txt`, colóquelo en la carpeta raíz del proyecto y haga referencia a él en el archivo `.nuspec`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```

Visual Studio muestra `readme.txt` cuando el paquete se instala en un proyecto. El archivo no se muestra cuando se instala en los proyectos de .NET Core, o para paquetes que se instalan como una dependencia.

## <a name="package-the-component"></a>Empaquetar el componente

Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está listo para ejecutar el comando `pack`:

```cli
nuget pack AppLogger.nuspec
```

Esto generará `AppLogger.YOUR_NAME.1.0.0.nupkg`. Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, se ve el contenido siguiente:

![Explorador de paquetes NuGet en el que se muestra el paquete AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta. También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.

Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar paquetes](../create-packages/publish-a-package.md).

Tenga en cuenta que `pack` requiere Mono 4.4.2 en Mac OS X y no funciona en los sistemas Linux. En los equipos Mac, también debe convertir los nombres de las rutas de acceso de Windows del archivo `.nuspec` a las rutas de acceso de estilo Unix.

## <a name="net-standard-mapping-table"></a>Tabla de asignación de .NET Standard

| Nombre de la plataforma | Alias |
| --- | --- |
| Estándar .NET | netstandard | 1.0 | 1.1 | 1.2 | 1.3 | 1.4 | 1.5 | 1.6 |
| Núcleo de .NET | netcoreapp | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; | 1.0 |
| .NET Framework | net | 4.5 | 4.5.1 | 4.6 | 4.6.1 | 4.6.2 | 4.6.3 |
| Plataformas Mono/Xamarin | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; |
| Plataforma universal de Windows | uap | &#x2192; | &#x2192; | &#x2192; | &#x2192; |10.0 |
| Windows | win| &#x2192; | 8.0 | 8.1 |
| Windows Phone | wpa| &#x2192;| &#x2192; | 8.1 |
| Windows Phone Silverlight | wp | 8.0 |

## <a name="related-topics"></a>Temas relacionados

- [Referencia de .nuspec](../reference/nuspec.md)
- [Compatibilidad con varias versiones de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Incluir propiedades y destinos de MSBuild en un paquete](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Creación de paquetes localizados](../create-packages/creating-localized-packages.md)
- [Paquetes de símbolos](../create-packages/symbol-packages.md)
- [Control de versiones del paquete](../reference/package-versioning.md)
- [Documentación de la biblioteca de .NET Standard](/dotnet/articles/standard/library)
- [Portabilidad a .NET Core desde .NET Framework](/dotnet/articles/core/porting/index)