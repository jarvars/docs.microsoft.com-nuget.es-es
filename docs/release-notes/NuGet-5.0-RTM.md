---
title: Notas de la versión de NuGet 5.0 RTM
description: Notas de la versión 5.0 de NuGet incluidos problemas conocidos, correcciones de errores, nuevas características y dcr.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921590"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="040cc-103">Notas de la versión 5.0 de NuGet</span><span class="sxs-lookup"><span data-stu-id="040cc-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="040cc-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="040cc-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="040cc-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="040cc-105">NuGet version</span></span> | <span data-ttu-id="040cc-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="040cc-106">Available in Visual Studio version</span></span>| <span data-ttu-id="040cc-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="040cc-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [**<span data-ttu-id="040cc-108">5.0.0</span><span class="sxs-lookup"><span data-stu-id="040cc-108">5.0.0</span></span>**](https://nuget.org/downloads) | [<span data-ttu-id="040cc-109">Visual Studio 2019 versión 16.0</span><span class="sxs-lookup"><span data-stu-id="040cc-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="040cc-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="040cc-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="040cc-111"><sup>1</sup>instalado con Visual Studio de 2019 con carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="040cc-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="040cc-112"><sup>2</sup>disponible como una instalación opcional con Visual Studio de 2019 con carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="040cc-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="040cc-113">Resumen: Novedades en 5.0</span><span class="sxs-lookup"><span data-stu-id="040cc-113">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="040cc-114">Soporte técnico para restaurar [filtra soluciones](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) en Visual Studio de 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="040cc-114">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* `BuildTransitive` <span data-ttu-id="040cc-115">carpeta permite paquetes transitiva contribuir destinos/propiedades al proyecto de host - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="040cc-115">folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="040cc-116">Mejor compatibilidad para escenarios de PackageReference en NuGet IV API - [#7005](https://github.com/NuGet/Home/issues/7005), [7493 #](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="040cc-116">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* `nuget.exe pack project.json` <span data-ttu-id="040cc-117">en desuso - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="040cc-117">has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="040cc-118">Complemento de proveedor de credenciales de gen. 1 se ha sustituido por [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) y pronto quedará en desuso - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="040cc-118">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="040cc-119">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="040cc-119">Issues fixed in this release</span></span>

**<span data-ttu-id="040cc-120">Errores</span><span class="sxs-lookup"><span data-stu-id="040cc-120">Bugs</span></span>**

* <span data-ttu-id="040cc-121">Cuando se realiza una restauración de NoOp, evitar \*. dgspec.json escritura en el directorio obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="040cc-121">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="040cc-122">Permisos de los archivos creados dentro de ~/.nuget son demasiado abiertos: [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="040cc-122">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* `dotnet list package --outdated` <span data-ttu-id="040cc-123">no funciona con orígenes que deben auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="040cc-123">doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="040cc-124">NuGet.VisualStudio.IVsPackageInstaller - que realiza la llamada en un proyecto con ningún paquete hace referencia siempre usa packages.config, incluso si el valor predeterminado se establece en PackageReference - [7005 #](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="040cc-124">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="040cc-125">PMC: Paquete de actualización reinstalar se produce un error ("no se encuentra el paquete") en paquetes elimine de la lista.</span><span class="sxs-lookup"><span data-stu-id="040cc-125">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="040cc-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="040cc-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="040cc-127">Agregar el aviso de terceros en nuestro repositorio y VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="040cc-127">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="040cc-128">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage debe instalar la versión más reciente cuando no hay ninguna versión dada - [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="040cc-128">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="040cc-129">--asistencia interactiva para dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="040cc-129">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="040cc-130">Al restaurar el archivo de bloqueo, no debería generarse NU1603 advertencia.</span><span class="sxs-lookup"><span data-stu-id="040cc-130">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="040cc-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="040cc-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="040cc-132">NuGet no debe imprimir la ruta de acceso del proyecto durante la restauración con registro mínimo - [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="040cc-132">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="040cc-133">--asistencia interactiva para dotnet quitar paquete - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="040cc-133">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="040cc-134">Agregar copia NuGet.Packaging.Core con TypeForwardedTo attrs - [7768 #](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="040cc-134">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="040cc-135">plugins_cache necesita una ruta de acceso más corta para funcionar bien - [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="040cc-135">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="040cc-136">Prefiere la ruta de acceso para la detección de msbuild si el usuario no solicitar versión de msbuild específicas - [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="040cc-136">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* `nuget.exe /?` <span data-ttu-id="040cc-137">debe enumerar las versiones correctas de msbuild - [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="040cc-137">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="040cc-138">NuGet.targets(498,5): error: No se encontró una parte de la ruta de acceso ' / tmp/NuGetScratch - en mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="040cc-138">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="040cc-139">restauración innecesariamente enumera el contenido de todas las versiones de paquete que se hace referencia en la caché del equipo - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="040cc-139">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="040cc-140">Detección automática de MSBuild siempre selecciona 16.0 después de obtener una vista previa en la instalación de VS 2019 - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="040cc-140">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="040cc-141">paquete de dotnet lista en una solución genera entradas duplicadas para framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="040cc-141">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="040cc-142">Excepción "el nombre de ruta de acceso vacía no es legal" cuando IVsPackageInstaller.InstallPackage que realiza la llamada en el antiguo proyectos y paquetes de la carpeta no existe.</span><span class="sxs-lookup"><span data-stu-id="040cc-142">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="040cc-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="040cc-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="040cc-144">nivel de detalle de MSBuild/t: Restore mínimo debe ser más mínimo - [4695 #](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="040cc-144">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="040cc-145">VS de 16.0 NuGet UI tiene pestañas ilegibles debido a problemas de color - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="040cc-145">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="040cc-146">NuGet.Core & NuGet.Clients License.txt aclaración - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="040cc-146">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="040cc-147">Restauración innecesariamente enumera la carpeta de paquetes global en intentar determinar el tipo - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="040cc-147">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="040cc-148">Errores de cumplimiento del archivo de bloqueo deberían aparecer en la ventana Lista de errores - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="040cc-148">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="040cc-149">Solucionar problemas de NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="040cc-149">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="040cc-150">Adaptarse a actualizar su instalación de MSBuild ubicación - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="040cc-150">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="040cc-151">NuGet.Build.Tasks.Pack debe ser una dependencia de desarrollo - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="040cc-151">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="040cc-152">Agregar paquete de punto de extensión para incluir depurar símbolos - [7234 #](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="040cc-152">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* `dotnet pack` <span data-ttu-id="040cc-153">debe conservar intervalo de versiones de dependencia en el nupkg creado (incluso si se usa la versión flotante) - [7232 #](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="040cc-153">should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* `dotnet restore` <span data-ttu-id="040cc-154">se produce un error en un origen autenticado cuando la configuración de nivel de usuario también tiene el origen: [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="040cc-154">fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="040cc-155">Módulo no debe restringir el conjunto de BuildActions para archivos de contenido - [7155 #](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="040cc-155">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="040cc-156">Mediante un ProjectReference que requiere AssetTargetFallback se realice correctamente, debería advertir.</span><span class="sxs-lookup"><span data-stu-id="040cc-156">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="040cc-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="040cc-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="040cc-158">Interbloqueo debido a problemas de subprocesamiento al llamar a CPS (CommonProjectSystem) - [7103 #](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="040cc-158">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* `dotnet add package` <span data-ttu-id="040cc-159">No usar credenciales desde la configuración global para un origen especificado en config local - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="040cc-159">doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="040cc-160">Problemas de subprocesamiento con MEF que se llama en async código rutas de acceso - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="040cc-160">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="040cc-161">De firma: error notificado dos veces y sin la pila de llamadas - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="040cc-161">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="040cc-162">Instalar un paquete firmado con certificado de firma de confianza debería mostrar el error - [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="040cc-162">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="040cc-163">Restauración de NuGet incorrectamente NOOP cuando 2 proyectos están compartiendo el directorio obj - [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="040cc-163">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="040cc-164">No se puede usar PAT con `dotnet restore` en Linux con paquetes de fuente autenticado - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="040cc-164">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="040cc-165">se produce un error en la restauración de dotnet debido a la amplia deshabilitado máquina fuente - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="040cc-165">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

**<span data-ttu-id="040cc-166">DCR</span><span class="sxs-lookup"><span data-stu-id="040cc-166">DCRs</span></span>**

* <span data-ttu-id="040cc-167">Advertir de su eliminación futura de "dotnet pack project.json" - [7928 #](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="040cc-167">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="040cc-168">Agregue una advertencia de desuso para Gen1 Credentials - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="040cc-168">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="040cc-169">Firma: Repositorio habilitado para requerir la comprobación de cliente de todos los paquetes como repositorio firmado: a través del recurso RepositorySignatures/5.0.0 - [7759 #](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="040cc-169">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="040cc-170">limitar número de solicitud de http por código fuente a través de NuGet.Config - [4538 #](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="040cc-170">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="040cc-171">NuGet debe tener como destino Net472 (para ayudar a la compilación de la extensión VSIX 16.0 limpieza) - [7143 #](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="040cc-171">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="040cc-172">PMC: Quitar comando OpenPackagePage - [7384 #](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="040cc-172">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="040cc-173">Asegúrese de NetCoreApp 3.0 se asignan a NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="040cc-173">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="040cc-174">Agregar compatibilidad de netstandard2.0 para paquetes NuGet.\* - [6516 #](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="040cc-174">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="040cc-175">Permitir que los autores de paquetes definir el comportamiento de compilación activos transitiva - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="040cc-175">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="040cc-176">Admite la característica de filtro de solución de VS de 2019.</span><span class="sxs-lookup"><span data-stu-id="040cc-176">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="040cc-177">También admite el proyecto no está en soluciones o proyectos descargados.</span><span class="sxs-lookup"><span data-stu-id="040cc-177">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="040cc-178">Primero deba restaurar una solución completa (a través de CLI o VS) - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="040cc-178">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="040cc-179">Los ensamblados de NuGet 5.0 requieren .NET 4.7.2 (a través de cambio TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="040cc-179">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="040cc-180">NuGetLicenseData desde NuGet.Packaging debe ser un tipo público.</span><span class="sxs-lookup"><span data-stu-id="040cc-180">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="040cc-181">Actualizar los metadatos de licencia ingerido desde spdx.</span><span class="sxs-lookup"><span data-stu-id="040cc-181">Update license metadata ingested from spdx.</span></span><span data-ttu-id="040cc-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="040cc-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="040cc-183">Quitar de la API de configuración obsoletas - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="040cc-183">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="040cc-184">Tiempos de espera de restauración de solución alternativa en sistemas con 1 cpu - [6742 #](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="040cc-184">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="040cc-185">NuGet prefiere la autenticación NTLM, incluso si no hay credenciales en NuGet.config: agregar la opción de configuración para filtrar los tipos de autenticación de credenciales: [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="040cc-185">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="040cc-186">Habilitar EmbedInteropTypes packagereference (capacidad de búsqueda de coincidencias Packages.Config) - [2365 #](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="040cc-186">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

**[<span data-ttu-id="040cc-187">Lista de todos los problemas corregidos en esta versión - 5.0 RTM</span><span class="sxs-lookup"><span data-stu-id="040cc-187">List of all issues fixed in this release - 5.0 RTM</span></span>](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="known-issues"></a><span data-ttu-id="040cc-188">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="040cc-188">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="040cc-189">Los paquetes en FallbackFolders instalados por el SDK de .NET Core de forma personalizada no superan la validación de firma.</span><span class="sxs-lookup"><span data-stu-id="040cc-189">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="040cc-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="040cc-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="040cc-191">Problema</span><span class="sxs-lookup"><span data-stu-id="040cc-191">Issue</span></span>
<span data-ttu-id="040cc-192">Cuando se usa dotnet.exe 2.x para restaurar un proyecto que tiene como destinos múltiples netcoreapp 1.x y netcoreapp 2.x, la carpeta de reserva se trata como una fuente de archivos.</span><span class="sxs-lookup"><span data-stu-id="040cc-192">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="040cc-193">Esto significa que, cuando se restaura, NuGet elegirá el paquete de la carpeta de reserva e intentará instalarlo en la carpeta de paquetes global y realizará la validación de firma habitual, lo cual produce un error.</span><span class="sxs-lookup"><span data-stu-id="040cc-193">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="040cc-194">Solución</span><span class="sxs-lookup"><span data-stu-id="040cc-194">Workaround</span></span>
<span data-ttu-id="040cc-195">Deshabilitar el uso de la carpeta reserva estableciendo el `RestoreAdditionalProjectSources` a nada:</span><span class="sxs-lookup"><span data-stu-id="040cc-195">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="040cc-196">Úselo con precaución ya que ahora se descargarán los paquetes que se restauraría desde la carpeta de reserva de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="040cc-196">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>