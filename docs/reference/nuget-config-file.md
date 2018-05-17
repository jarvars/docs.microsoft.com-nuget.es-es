---
title: Referencia del archivo NuGet.config
description: Referencia del archivo NuGet.Config en la que se incluyen las secciones config, bindingRedirects, packageRestore, solution y packageSource.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: e57d17c5bf393a05b8915b9a1a7af0b659a04716
ms.sourcegitcommit: 055248d790051774c892b220eca12015babbd668
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="2aae7-103">referencia de NuGet.config</span><span class="sxs-lookup"><span data-stu-id="2aae7-103">nuget.config reference</span></span>

<span data-ttu-id="2aae7-104">El comportamiento de NuGet se controla mediante la configuración en diferentes archivos `NuGet.Config`, como se describe en [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="2aae7-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="2aae7-105">`nuget.config` es un archivo XML que contiene un nodo `<configuration>` de nivel superior, que contiene los elementos de sección que se describen en este tema.</span><span class="sxs-lookup"><span data-stu-id="2aae7-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="2aae7-106">Cada sección contiene cero o más elementos `<add>` con atributos `key` y `value`.</span><span class="sxs-lookup"><span data-stu-id="2aae7-106">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="2aae7-107">Vea el [archivo de configuración de ejemplo](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="2aae7-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="2aae7-108">Los nombres de opción distinguen mayúsculas de minúsculas, y los valores pueden usar [variables de entorno](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="2aae7-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="2aae7-109">En este tema:</span><span class="sxs-lookup"><span data-stu-id="2aae7-109">In this topic:</span></span>

- [<span data-ttu-id="2aae7-110">Sección config</span><span class="sxs-lookup"><span data-stu-id="2aae7-110">config section</span></span>](#config-section)
- [<span data-ttu-id="2aae7-111">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="2aae7-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="2aae7-112">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="2aae7-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="2aae7-113">Sección solution</span><span class="sxs-lookup"><span data-stu-id="2aae7-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="2aae7-114">[Secciones de origen del paquete](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="2aae7-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="2aae7-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="2aae7-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="2aae7-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="2aae7-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="2aae7-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="2aae7-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="2aae7-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="2aae7-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="2aae7-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="2aae7-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="2aae7-120">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="2aae7-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="2aae7-121">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2aae7-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="2aae7-122">Sección config</span><span class="sxs-lookup"><span data-stu-id="2aae7-122">config section</span></span>

<span data-ttu-id="2aae7-123">Contiene varios valores de configuración, que se pueden establecer mediante el [comando `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="2aae7-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="2aae7-124">`dependencyVersion` y `repositoryPath` solo se aplican a proyectos mediante `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="2aae7-124">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="2aae7-125">`globalPackagesFolder` se aplica solo a los proyectos con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="2aae7-125">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="2aae7-126">Key</span><span class="sxs-lookup"><span data-stu-id="2aae7-126">Key</span></span> | <span data-ttu-id="2aae7-127">Valor</span><span class="sxs-lookup"><span data-stu-id="2aae7-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2aae7-128">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="2aae7-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="2aae7-129">El valor predeterminado `DependencyVersion` para la instalación, restauración y actualización del paquete, cuando no se especifica directamente el modificador `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="2aae7-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="2aae7-130">Este valor también se usa en la interfaz de usuario del Administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="2aae7-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="2aae7-131">Los valores son `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="2aae7-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="2aae7-132">globalPackagesFolder (solo mediante PackageReference de proyectos)</span><span class="sxs-lookup"><span data-stu-id="2aae7-132">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="2aae7-133">La ubicación de la carpeta de paquetes global predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2aae7-133">The location of the default global packages folder.</span></span> <span data-ttu-id="2aae7-134">El valor predeterminado es `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac o Linux).</span><span class="sxs-lookup"><span data-stu-id="2aae7-134">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="2aae7-135">Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2aae7-135">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="2aae7-136">Esta configuración se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="2aae7-136">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="2aae7-137">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="2aae7-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="2aae7-138">La ubicación en la que se van a instalar los paquetes NuGet en lugar de la carpeta `$(Solutiondir)/packages` predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2aae7-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="2aae7-139">Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2aae7-139">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="2aae7-140">Esta configuración se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="2aae7-140">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="2aae7-141">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="2aae7-141">defaultPushSource</span></span> | <span data-ttu-id="2aae7-142">Identifica la dirección URL o ruta de acceso de origen del paquete que se debe usar como valor predeterminado si no se encuentra ningún otro origen del paquete para una operación.</span><span class="sxs-lookup"><span data-stu-id="2aae7-142">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="2aae7-143">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="2aae7-143">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="2aae7-144">Configuración de proxy que se usa al conectarse a orígenes de paquetes; `http_proxy` debe tener el formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="2aae7-144">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="2aae7-145">Las contraseñas están cifradas y no se pueden agregar de forma manual.</span><span class="sxs-lookup"><span data-stu-id="2aae7-145">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="2aae7-146">Para `no_proxy`, el valor es una lista separada por comas de dominios que omiten el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="2aae7-146">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="2aae7-147">Como alternativa, puede usar las variables de entorno http_proxy y no_proxy para esos valores.</span><span class="sxs-lookup"><span data-stu-id="2aae7-147">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="2aae7-148">Para obtener más información, vea [Configuración de proxy de NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="2aae7-148">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="2aae7-149">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="2aae7-149">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="2aae7-150">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="2aae7-150">bindingRedirects section</span></span>

<span data-ttu-id="2aae7-151">Configura si NuGet realiza redirecciones de enlaces automáticas cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="2aae7-151">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="2aae7-152">Key</span><span class="sxs-lookup"><span data-stu-id="2aae7-152">Key</span></span> | <span data-ttu-id="2aae7-153">Valor</span><span class="sxs-lookup"><span data-stu-id="2aae7-153">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2aae7-154">skip</span><span class="sxs-lookup"><span data-stu-id="2aae7-154">skip</span></span> | <span data-ttu-id="2aae7-155">Un valor booleano que indica si se omiten las redirecciones de enlaces automáticas.</span><span class="sxs-lookup"><span data-stu-id="2aae7-155">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="2aae7-156">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="2aae7-156">The default is false.</span></span> |

<span data-ttu-id="2aae7-157">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="2aae7-157">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="2aae7-158">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="2aae7-158">packageRestore section</span></span>

<span data-ttu-id="2aae7-159">Controla la restauración del paquete durante las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="2aae7-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="2aae7-160">Key</span><span class="sxs-lookup"><span data-stu-id="2aae7-160">Key</span></span> | <span data-ttu-id="2aae7-161">Valor</span><span class="sxs-lookup"><span data-stu-id="2aae7-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2aae7-162">enabled</span><span class="sxs-lookup"><span data-stu-id="2aae7-162">enabled</span></span> | <span data-ttu-id="2aae7-163">Un valor booleano que indica si NuGet puede realizar la restauración automática.</span><span class="sxs-lookup"><span data-stu-id="2aae7-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="2aae7-164">También se puede establecer la variable de entorno `EnableNuGetPackageRestore` con un valor de `True` en lugar de establecer esta clave en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="2aae7-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="2aae7-165">automáticamente</span><span class="sxs-lookup"><span data-stu-id="2aae7-165">automatic</span></span> | <span data-ttu-id="2aae7-166">Un valor booleano que indica si NuGet debe comprobar los paquetes que faltan durante una compilación.</span><span class="sxs-lookup"><span data-stu-id="2aae7-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="2aae7-167">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="2aae7-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="2aae7-168">Sección solution</span><span class="sxs-lookup"><span data-stu-id="2aae7-168">solution section</span></span>

<span data-ttu-id="2aae7-169">Controla si la carpeta `packages` de una solución se incluye en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="2aae7-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="2aae7-170">En esta sección solo funciona en los archivos `nuget.config` de la carpeta de una solución.</span><span class="sxs-lookup"><span data-stu-id="2aae7-170">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="2aae7-171">Key</span><span class="sxs-lookup"><span data-stu-id="2aae7-171">Key</span></span> | <span data-ttu-id="2aae7-172">Valor</span><span class="sxs-lookup"><span data-stu-id="2aae7-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2aae7-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="2aae7-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="2aae7-174">Un valor booleano que indica si se debe ignorar la carpeta de paquetes cuando se trabaja con el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="2aae7-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="2aae7-175">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="2aae7-175">The default value is false.</span></span> |

<span data-ttu-id="2aae7-176">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="2aae7-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="2aae7-177">Secciones de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="2aae7-177">Package source sections</span></span>

<span data-ttu-id="2aae7-178">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` y `disabledPackageSources` trabajan de manera conjunta para configurar el funcionamiento de NuGet con repositorios de paquetes durante las operaciones de instalación, restauración y actualización.</span><span class="sxs-lookup"><span data-stu-id="2aae7-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="2aae7-179">Normalmente se usa el [comando `nuget sources`](../tools/cli-ref-sources.md) para administrar estos valores, excepto para `apikeys` que se administra con el [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="2aae7-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="2aae7-180">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="2aae7-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="2aae7-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="2aae7-181">packageSources</span></span>

<span data-ttu-id="2aae7-182">Enumera todos los orígenes de paquetes conocidos.</span><span class="sxs-lookup"><span data-stu-id="2aae7-182">Lists all known package sources.</span></span> <span data-ttu-id="2aae7-183">El orden se omite durante las operaciones de restauración y con cualquier proyecto con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="2aae7-183">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="2aae7-184">NuGet respeta el orden de los orígenes de instalación y las operaciones de actualización con proyectos mediante `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="2aae7-184">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="2aae7-185">Key</span><span class="sxs-lookup"><span data-stu-id="2aae7-185">Key</span></span> | <span data-ttu-id="2aae7-186">Valor</span><span class="sxs-lookup"><span data-stu-id="2aae7-186">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2aae7-187">(nombre para asignar al origen del paquete)</span><span class="sxs-lookup"><span data-stu-id="2aae7-187">(name to assign to the package source)</span></span> | <span data-ttu-id="2aae7-188">La ruta de acceso o dirección URL del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="2aae7-188">The path or URL of the package source.</span></span> |

<span data-ttu-id="2aae7-189">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="2aae7-189">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="2aae7-190">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="2aae7-190">packageSourceCredentials</span></span>

<span data-ttu-id="2aae7-191">Almacena nombres de usuario y contraseñas para los orígenes, normalmente especificados con los modificadores `-username` y `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="2aae7-191">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="2aae7-192">Las contraseñas se cifran de forma predeterminada a menos que también se use la opción `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="2aae7-192">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="2aae7-193">Key</span><span class="sxs-lookup"><span data-stu-id="2aae7-193">Key</span></span> | <span data-ttu-id="2aae7-194">Valor</span><span class="sxs-lookup"><span data-stu-id="2aae7-194">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2aae7-195">username</span><span class="sxs-lookup"><span data-stu-id="2aae7-195">username</span></span> | <span data-ttu-id="2aae7-196">El nombre de usuario para el origen en texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="2aae7-196">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="2aae7-197">contraseña</span><span class="sxs-lookup"><span data-stu-id="2aae7-197">password</span></span> | <span data-ttu-id="2aae7-198">La contraseña cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="2aae7-198">The encrypted password for the source.</span></span> |
| <span data-ttu-id="2aae7-199">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="2aae7-199">cleartextpassword</span></span> | <span data-ttu-id="2aae7-200">La contraseña no cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="2aae7-200">The unencrypted password for the source.</span></span> |

<span data-ttu-id="2aae7-201">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="2aae7-201">**Example:**</span></span>

<span data-ttu-id="2aae7-202">En el archivo de configuración, el elemento `<packageSourceCredentials>` contiene nodos secundarios para cada nombre de origen aplicable (los espacios en el nombre se reemplazan por `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="2aae7-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="2aae7-203">Es decir, para los orígenes denominados "Contoso" y "Test Source", el archivo de configuración contiene lo siguiente cuando se usan contraseñas cifradas:</span><span class="sxs-lookup"><span data-stu-id="2aae7-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="2aae7-204">Cuando se usan contraseñas sin cifrar:</span><span class="sxs-lookup"><span data-stu-id="2aae7-204">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="2aae7-205">apikeys</span><span class="sxs-lookup"><span data-stu-id="2aae7-205">apikeys</span></span>

<span data-ttu-id="2aae7-206">Almacena claves para los orígenes en los que se usa autenticación de clave de API, como se establece mediante el [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="2aae7-206">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="2aae7-207">Key</span><span class="sxs-lookup"><span data-stu-id="2aae7-207">Key</span></span> | <span data-ttu-id="2aae7-208">Valor</span><span class="sxs-lookup"><span data-stu-id="2aae7-208">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2aae7-209">(dirección URL de origen)</span><span class="sxs-lookup"><span data-stu-id="2aae7-209">(source URL)</span></span> | <span data-ttu-id="2aae7-210">La clave de API cifrada.</span><span class="sxs-lookup"><span data-stu-id="2aae7-210">The encrypted API key.</span></span> |

<span data-ttu-id="2aae7-211">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="2aae7-211">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="2aae7-212">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="2aae7-212">disabledPackageSources</span></span>

<span data-ttu-id="2aae7-213">Orígenes actualmente deshabilitados identificados.</span><span class="sxs-lookup"><span data-stu-id="2aae7-213">Identified currently disabled sources.</span></span> <span data-ttu-id="2aae7-214">Puede estar vacía.</span><span class="sxs-lookup"><span data-stu-id="2aae7-214">May be empty.</span></span>

| <span data-ttu-id="2aae7-215">Key</span><span class="sxs-lookup"><span data-stu-id="2aae7-215">Key</span></span> | <span data-ttu-id="2aae7-216">Valor</span><span class="sxs-lookup"><span data-stu-id="2aae7-216">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2aae7-217">(nombre del origen)</span><span class="sxs-lookup"><span data-stu-id="2aae7-217">(name of source)</span></span> | <span data-ttu-id="2aae7-218">Un valor booleano que indica si el origen está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="2aae7-218">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="2aae7-219">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="2aae7-219">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="2aae7-220">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="2aae7-220">activePackageSource</span></span>

<span data-ttu-id="2aae7-221">*(solo para 2.x; en desuso en 3.x y versiones posteriores)*</span><span class="sxs-lookup"><span data-stu-id="2aae7-221">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="2aae7-222">Identifica al origen actualmente activo o indica la suma de todos los orígenes.</span><span class="sxs-lookup"><span data-stu-id="2aae7-222">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="2aae7-223">Key</span><span class="sxs-lookup"><span data-stu-id="2aae7-223">Key</span></span> | <span data-ttu-id="2aae7-224">Valor</span><span class="sxs-lookup"><span data-stu-id="2aae7-224">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2aae7-225">(nombre del origen) o `All`</span><span class="sxs-lookup"><span data-stu-id="2aae7-225">(name of source) or `All`</span></span> | <span data-ttu-id="2aae7-226">Si la clave es el nombre de un origen, el valor es la ruta de acceso o la dirección URL del origen.</span><span class="sxs-lookup"><span data-stu-id="2aae7-226">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="2aae7-227">Si es `All`, el valor debe ser `(Aggregate source)` para combinar todos los orígenes de paquetes que no estén deshabilitados.</span><span class="sxs-lookup"><span data-stu-id="2aae7-227">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="2aae7-228">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="2aae7-228">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="2aae7-229">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="2aae7-229">Using environment variables</span></span>

<span data-ttu-id="2aae7-230">Puede usar variables de entorno en valores `nuget.config` (NuGet 3.4 o versiones posteriores) para aplicar la configuración en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2aae7-230">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="2aae7-231">Por ejemplo, si la variable de entorno `HOME` en Windows se establece en `c:\users\username`, el valor de `%HOME%\NuGetRepository` en el archivo de configuración se resuelve como `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="2aae7-231">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="2aae7-232">De forma similar, si `HOME` en Mac/Linux se establece en `/home/myStuff`, `%HOME%/NuGetRepository` en el archivo de configuración se resuelve como `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="2aae7-232">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="2aae7-233">Si no se encuentra una variable de entorno, NuGet usa el valor literal del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="2aae7-233">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="2aae7-234">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2aae7-234">Example config file</span></span>

<span data-ttu-id="2aae7-235">A continuación se muestra un archivo `nuget.config` de ejemplo en el que se ilustran varios valores:</span><span class="sxs-lookup"><span data-stu-id="2aae7-235">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>
</configuration>
```