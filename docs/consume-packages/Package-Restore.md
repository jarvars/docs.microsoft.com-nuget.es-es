---
title: Restauración de paquetes NuGet
description: Una descripción de cómo NuGet restaura paquetes de los que depende un proyecto, incluido cómo deshabilitar la restauración y la restricción de versiones.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 34da7f5800671f03df6728e0b948c560f73fd13c
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817052"
---
# <a name="package-restore"></a><span data-ttu-id="8aa18-103">Restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="8aa18-103">Package Restore</span></span>

<span data-ttu-id="8aa18-104">Para promover un entorno de desarrollo más limpio y reducir el tamaño del repositorio, **Restauración de paquetes** NuGet instala todas las dependencias del proyecto tal y como aparecen en el archivo de proyecto o en `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8aa18-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all a project's dependencies as listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="8aa18-105">Visual Studio puede restaurar los paquetes automáticamente al compilar un proyecto.</span><span class="sxs-lookup"><span data-stu-id="8aa18-105">Visual Studio can restore packages automatically when a project is built.</span></span> <span data-ttu-id="8aa18-106">Los comandos `dotnet build` y `dotnet run`(.NET Core 2.0 y versiones posteriores) también realizan una restauración automática.</span><span class="sxs-lookup"><span data-stu-id="8aa18-106">The `dotnet build` and `dotnet run` commands (.NET Core 2.0+) also perform an automatic restore.</span></span> <span data-ttu-id="8aa18-107">También puede restaurar los paquetes siempre que quiera a través de Visual Studio, `nuget restore`, `dotnet restore` y xbuild en Mono.</span><span class="sxs-lookup"><span data-stu-id="8aa18-107">You can also restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="8aa18-108">La restauración de paquetes se asegura de que todas las dependencia de un proyecto estén disponibles sin almacenar los paquetes de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="8aa18-108">Package restore makes sure that all a project's dependencies are available without storing those packages in source control.</span></span> <span data-ttu-id="8aa18-109">Vea [Paquetes y control de código fuente](../consume-packages/packages-and-source-control.md) sobre cómo configurar el repositorio para excluir los archivos binarios del paquete.</span><span class="sxs-lookup"><span data-stu-id="8aa18-109">See [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries.</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="8aa18-110">Información general sobre restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="8aa18-110">Package restore overview</span></span>

<span data-ttu-id="8aa18-111">Al restaurar paquetes, se instalan primero las dependencias directas de un proyecto según sea necesario y luego se instalan todas las dependencias de los paquetes a lo largo del gráfico de dependencias completo.</span><span class="sxs-lookup"><span data-stu-id="8aa18-111">Restoring packages first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="8aa18-112">Si un paquete no está ya instalado, NuGet primero intenta recuperarlo desde la [caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="8aa18-112">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="8aa18-113">Si el paquete no está en la memoria caché, NuGet intenta descargarlo y almacenarlo en caché en todos los orígenes habilitados (vea [Configuración del comportamiento de NuGet](Configuring-NuGet-Behavior.md); los orígenes también aparecen en la lista **Herramientas > Opciones > Administrador de paquetes NuGet > Orígenes del paquete** en Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="8aa18-113">If the package is not in the cache, NuGet then attempts to download the package from all enabled sources (see [Configuring NuGet behavior](Configuring-NuGet-Behavior.md); sources also appear in the  **Tools > Options > NuGet Package Manager > Package Sources** list in Visual Studio).</span></span> <span data-ttu-id="8aa18-114">Durante la restauración, NuGet omite el orden de los orígenes de paquetes y usará el paquete del origen que primero responda a las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="8aa18-114">During restore, NuGet ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span>

> [!Note]
> <span data-ttu-id="8aa18-115">NuGet no indica un error al restaurar un paquete hasta que se han comprobado todos los orígenes.</span><span class="sxs-lookup"><span data-stu-id="8aa18-115">NuGet does not indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="8aa18-116">En ese momento, NuGet solo informa del error del último origen de la lista.</span><span class="sxs-lookup"><span data-stu-id="8aa18-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="8aa18-117">El error implica que el paquete no estaba presente en *ninguno* de los otros orígenes, aunque los errores no se muestran para cada uno de esos orígenes de forma individual.</span><span class="sxs-lookup"><span data-stu-id="8aa18-117">The error implies that the package wasn't present on *any* of the other sources, even though errors are not shown for each of those sources individually.</span></span>

<span data-ttu-id="8aa18-118">La restauración de paquetes se activa de las maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="8aa18-118">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="8aa18-119">**CLI de dotnet**: use el comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), que restaura los paquetes incluidos en el archivo de proyecto (vea [PackageReference](../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="8aa18-119">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="8aa18-120">Con .NET Core 2.0 y versiones posteriores, la restauración se realiza automáticamente con `dotnet build` y `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="8aa18-120">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="8aa18-121">**Interfaz de usuario del Administrador de paquetes (Visual Studio en Windows)**: los paquetes se restauran automáticamente al crear un proyecto a partir de una plantilla y al compilar un proyecto (sujeto a la opción descrita en [Habilitar y deshabilitar la restauración de paquetes](#enabling-and-disabling-package-restore)).</span><span class="sxs-lookup"><span data-stu-id="8aa18-121">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="8aa18-122">En NuGet 4.0 y versiones posteriores, la restauración también se produce automáticamente al realizar cambios en un proyecto basado en el SDK de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="8aa18-122">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="8aa18-123">Para la restauración manual, haga clic con el botón derecho en la solución en el Explorador de soluciones y seleccione **Restaurar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8aa18-123">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="8aa18-124">Si uno o varios paquetes siguen sin estar instalados correctamente (lo que significa que el Explorador de soluciones muestra un icono de error), use la interfaz de usuario del Administrador de paquetes para desinstalar y reinstalar los paquetes afectados.</span><span class="sxs-lookup"><span data-stu-id="8aa18-124">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="8aa18-125">Vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md)</span><span class="sxs-lookup"><span data-stu-id="8aa18-125">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="8aa18-126">Si ve el error "Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo" o "Uno o varios paquetes de NuGet se deben restaurar, pero no pudieron restaurarse porque no se ha concedido el consentimiento", active la restauración automática mediante las instrucciones descritas en [Habilitar y deshabilitar la restauración de paquetes](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="8aa18-126">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span> <span data-ttu-id="8aa18-127">Vea también [Solución de errores de restauración de paquetes](Package-restore-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8aa18-127">Also see [Package restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

- <span data-ttu-id="8aa18-128">**CLI de NuGet**: use el comando [nuget restore](../tools/cli-ref-restore.md), que restaura los paquetes incluidos en el archivo de proyecto o en `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8aa18-128">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file or in `packages.config`.</span></span> <span data-ttu-id="8aa18-129">También puede especificar un archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="8aa18-129">You can also specify a solution file.</span></span>

- <span data-ttu-id="8aa18-130">**MSBuild**: use el comando [msbuild /t:restore](../reference/msbuild-targets.md#restore-target), que restaura los paquetes incluidos en el archivo de proyecto (solo PackageReference).</span><span class="sxs-lookup"><span data-stu-id="8aa18-130">**MSBuild**: use the [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (PackageReference only).</span></span> <span data-ttu-id="8aa18-131">Disponible solo en 4.x y versiones posteriores y MSBuild 15.1 y versiones posteriores, que se incluyen con Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="8aa18-131">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="8aa18-132">`nuget restore` y `dotnet restore` usan este comando para los proyectos aplicables.</span><span class="sxs-lookup"><span data-stu-id="8aa18-132">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="8aa18-133">**Visual Studio Team Services**: al crear una definición de compilación en Team Services, incluya la tarea [Restaurar NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) o [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) (Restaurar .NET Core) en la definición antes de cualquier tarea de compilación.</span><span class="sxs-lookup"><span data-stu-id="8aa18-133">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="8aa18-134">Esta tarea se incluye de forma predeterminada en una serie de plantillas de compilación.</span><span class="sxs-lookup"><span data-stu-id="8aa18-134">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="8aa18-135">**Team Foundation Server**: TFS 2013 con TFS 2013 y versiones posteriores, los paquetes se restauran automáticamente de forma predeterminada durante la compilación, siempre que se use una plantilla de Team Build para TFS 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="8aa18-135">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="8aa18-136">Para la versión anterior de TFS, puede incluir un paso de compilación que invoque una de las opciones de restauración de línea de comandos anteriores.</span><span class="sxs-lookup"><span data-stu-id="8aa18-136">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="8aa18-137">También tiene la posibilidad de migrar la plantilla de compilación a TFS 2013.</span><span class="sxs-lookup"><span data-stu-id="8aa18-137">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="8aa18-138">Para obtener más información, vea el [tutorial sobre restauración de paquetes con Team Foundation Build](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="8aa18-138">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="8aa18-139">Habilitar y deshabilitar la restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="8aa18-139">Enabling and disabling package restore</span></span>

<span data-ttu-id="8aa18-140">La restauración de paquetes se habilita principalmente a través de **Herramientas > Opciones > Administrador de paquetes NuGet** en Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="8aa18-140">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Control de los comportamientos de restauración de paquetes a través de las opciones del Administrador de paquetes NuGet](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="8aa18-142">**Permitir a NuGet descargar los paquetes que falten**: controla todas las formas de restauración de paquetes cambiando la opción `packageRestore/enabled` en el archivo `NuGet.Config` como se muestra aquí (`%AppData%\NuGet\NuGet.Config` en Windows, `~/.nuget/NuGet/NuGet.Config` en Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="8aa18-142">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="8aa18-143">En Visual Studio, este valor permite que funcione el comando **Restaurar paquetes NuGet** en el menú contextual de la solución.</span><span class="sxs-lookup"><span data-stu-id="8aa18-143">In Visual Studio, this setting allows the **Restore NuGet Packages** command on the solution's context menu to work.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="8aa18-144">La opción `packageRestore/enabled` se puede invalidar de forma global estableciendo una variable de entorno denominada **EnableNuGetPackageRestore** con un valor de TRUE o FALSE antes de iniciar Visual Studio o una compilación.</span><span class="sxs-lookup"><span data-stu-id="8aa18-144">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="8aa18-145">**Comprobar automáticamente los paquetes que falten durante la compilación en Visual Studio**: controla la restauración automática cambiando el ajuste `packageRestore/automatic` en el archivo `NuGet.Config` tal y como se muestra aquí (`%AppData%\NuGet\NuGet.Config` en Windows, `~/.nuget/NuGet/NuGet.Config` en Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="8aa18-145">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="8aa18-146">Cuando se establece esta opción, al ejecutar una compilación de Visual Studio se restauran automáticamente todos los paquetes que falten.</span><span class="sxs-lookup"><span data-stu-id="8aa18-146">When this option is set, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="8aa18-147">La opción no afecta a las compilaciones que se ejecutan desde la línea de comandos con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="8aa18-147">The option does not affect builds run from the command line using MSBuild.</span></span>

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="8aa18-148">Como referencia, vea el [archivo de configuración de NuGet: sección packageRestore](../reference/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="8aa18-148">For reference, see the [NuGet config file - packageRestore section](../reference/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="8aa18-149">En algunos casos, es posible que un desarrollador o una empresa quiera habilitar o deshabilitar la restauración de paquetes para todos los usuarios de un equipo.</span><span class="sxs-lookup"><span data-stu-id="8aa18-149">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="8aa18-150">Para ello, agregue la misma configuración anterior al archivo de configuración global de NuGet que se encuentra en `%ProgramData%\NuGet\Config` (Windows, posiblemente en una carpeta `\{IDE}\{Version}\{SKU}\` específica para Visual Studio) o `~/.local/share` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="8aa18-150">To do this, add the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config` (Windows, potentially under a specific `\{IDE}\{Version}\{SKU}\` folder for Visual Studio) or `~/.local/share` (Mac/Linux).</span></span> <span data-ttu-id="8aa18-151">Después, los usuarios individuales pueden habilitar la restauración de forma selectiva cuando sea necesario en un nivel de proyecto.</span><span class="sxs-lookup"><span data-stu-id="8aa18-151">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="8aa18-152">Vea [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) para obtener información exacta sobre cómo prioriza NuGet varios archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="8aa18-152">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

> [!Important]
> <span data-ttu-id="8aa18-153">Si edita el valor `packageRestore` directamente en `nuget.config`, debe reiniciar Visual Studio para que el cuadro de diálogo de opciones muestre los valores actuales.</span><span class="sxs-lookup"><span data-stu-id="8aa18-153">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="8aa18-154">Restricción de versiones de paquetes con la restauración</span><span class="sxs-lookup"><span data-stu-id="8aa18-154">Constraining package versions with restore</span></span>

<span data-ttu-id="8aa18-155">Cuando NuGet restaure paquetes por cualquier método, respetará las restricciones especificadas en `packages.config` o el archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="8aa18-155">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="8aa18-156">`packages.config`: especifique un intervalo de versiones en la propiedad `allowedVersion` de la dependencia.</span><span class="sxs-lookup"><span data-stu-id="8aa18-156">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="8aa18-157">Vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="8aa18-157">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="8aa18-158">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8aa18-158">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="8aa18-159">Archivo de proyecto (PackageReference): especifique un intervalo de versiones directamente con el número de versión de la dependencia.</span><span class="sxs-lookup"><span data-stu-id="8aa18-159">Project file (PackageReference): Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="8aa18-160">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8aa18-160">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="8aa18-161">En todos los casos, use la notación que se describe en [Package versioning](../reference/package-versioning.md) (Control de versiones de paquetes).</span><span class="sxs-lookup"><span data-stu-id="8aa18-161">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="forcing-restore-from-package-sources"></a><span data-ttu-id="8aa18-162">Forzamiento de la restauración a partir de orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="8aa18-162">Forcing restore from package sources</span></span>

<span data-ttu-id="8aa18-163">De forma predeterminada, las operaciones de restauración de NuGet usan paquetes de las carpetas *global-packages* y *http-cache*, que se describen en [Administración de paquetes globales y carpetas de caché](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="8aa18-163">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="8aa18-164">Para evitar el uso de la carpeta *global-packages*, realice una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="8aa18-164">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="8aa18-165">Borre la carpeta con `nuget locals global-packages -clear` o `dotnet nuget locals global-packages --clear`.</span><span class="sxs-lookup"><span data-stu-id="8aa18-165">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`</span></span>
- <span data-ttu-id="8aa18-166">Cambie temporalmente la ubicación de la carpeta *global-packages* antes de la operación de restauración con uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8aa18-166">Temporarily change the location of the *global-packages* folder before the restore operation using one of the following methods:</span></span>
  - <span data-ttu-id="8aa18-167">Establezca la variable de entorno NUGET_PACKAGES en otra carpeta.</span><span class="sxs-lookup"><span data-stu-id="8aa18-167">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="8aa18-168">Crear un `NuGet.Config` archivo que establezca `globalPackagesFolder` (si se usa PackageReference) o `repositoryPath` (si se usa `packages.config`) en otra carpeta (vea [valores de configuración](../reference/nuget-config-file.md#config-section)).</span><span class="sxs-lookup"><span data-stu-id="8aa18-168">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder (see [configuration settings](../reference/nuget-config-file.md#config-section)</span></span>
  - <span data-ttu-id="8aa18-169">Solo MSBuild: especifique otra carpeta con la propiedad `RestorePackagesPath`.</span><span class="sxs-lookup"><span data-stu-id="8aa18-169">MSBuild only: specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="8aa18-170">Para evitar el uso de la memoria caché para los orígenes HTTP, realice una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="8aa18-170">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="8aa18-171">Use la opción `-NoCache` con `nuget restore` o la opción `--no-cache` con `dotnet restore`.</span><span class="sxs-lookup"><span data-stu-id="8aa18-171">Use the `-NoCache` option with `nuget restore` or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="8aa18-172">Estas opciones no afectan a las operaciones de restauración a través del la consola o la interfaz de usuario del Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8aa18-172">These options do not affect restore operations through the Visual Studio Package Manager UI or Console.</span></span>
- <span data-ttu-id="8aa18-173">Borre la memoria caché con `nuget locals http-cache -clear` o `dotnet nuget locals http-cache --clear`.</span><span class="sxs-lookup"><span data-stu-id="8aa18-173">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="8aa18-174">Establezca temporalmente la variable de entorno NUGET_HTTP_CACHE_PATH en otra carpeta.</span><span class="sxs-lookup"><span data-stu-id="8aa18-174">Temporarily set of the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8aa18-175">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="8aa18-175">Troubleshooting</span></span>

<span data-ttu-id="8aa18-176">Vea [Solucionar problemas de errores de restauración de paquetes en Visual Studio](package-restore-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8aa18-176">See [Troubleshooting package restore](package-restore-troubleshooting.md).</span></span>