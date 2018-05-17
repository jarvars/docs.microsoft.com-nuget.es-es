---
title: Cómo empaquetar controles de UWP con NuGet
description: Cómo controlar los paquetes de NuGet que contienen controles de UWP, incluidos los metadatos necesarios y los archivos auxiliares de los diseñadores de Visual Studio y Blend.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/14/2018
ms.topic: tutorial
ms.openlocfilehash: 963846e857c8757176e4fbe1cd60c92a7397ba01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="99512-103">Crear controles de UWP como paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="99512-103">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="99512-104">Con Visual Studio 2017 puede sacar partido de las capacidades agregadas para los controles de UWP que se suministran en los paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="99512-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="99512-105">En esta guía se describen estas capacidades con el [ejemplo ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="99512-105">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="99512-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="99512-106">Prerequisites</span></span>

1. <span data-ttu-id="99512-107">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="99512-107">Visual Studio 2017</span></span>
1. <span data-ttu-id="99512-108">Comprender cómo [crear paquetes UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="99512-108">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="99512-109">Agregar compatibilidad con el cuadro de herramientas/panel de recursos para los controles XAML</span><span class="sxs-lookup"><span data-stu-id="99512-109">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="99512-110">Para que un control XAML aparezca en el cuadro de herramientas del diseñador XAML de Visual Studio y en el panel Recursos de Blend, cree un archivo `VisualStudioToolsManifest.xml` en la raíz de la carpeta `tools` del proyecto del paquete.</span><span class="sxs-lookup"><span data-stu-id="99512-110">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="99512-111">Este archivo no es necesario si no necesita que el control aparezca en el cuadro de herramientas o en el panel Recursos.</span><span class="sxs-lookup"><span data-stu-id="99512-111">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="99512-112">La estructura del archivo es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="99512-112">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="99512-113">donde:</span><span class="sxs-lookup"><span data-stu-id="99512-113">where:</span></span>

- <span data-ttu-id="99512-114">*your_package_file*: nombre del archivo de control, como `ManagedPackage.winmd` ("ManagedPackage" es un nombre arbitrario usado para este ejemplo y no tiene ningún otro significado).</span><span class="sxs-lookup"><span data-stu-id="99512-114">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="99512-115">*vs_category*: etiqueta del grupo en el que debe aparecer el control en el cuadro de herramientas del diseñador de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99512-115">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="99512-116">Se necesita una `VSCategory` para que el control aparezca en el cuadro de herramientas.</span><span class="sxs-lookup"><span data-stu-id="99512-116">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="99512-117">*blend_category*: etiqueta del grupo en el que debe aparecer el control en el panel Recursos del diseñador de Blend.</span><span class="sxs-lookup"><span data-stu-id="99512-117">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="99512-118">Se necesita una `BlendCategory` para que el control aparezca en Recursos.</span><span class="sxs-lookup"><span data-stu-id="99512-118">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="99512-119">*type_full_name_n*: nombre completo de cada control, incluido el espacio de nombres (por ejemplo, `ManagedPackage.MyCustomControl`).</span><span class="sxs-lookup"><span data-stu-id="99512-119">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="99512-120">Tenga en cuenta que el formato de puntos se usa tanto para los tipos administrados como para los tipos nativos.</span><span class="sxs-lookup"><span data-stu-id="99512-120">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="99512-121">En escenarios más avanzados también puede incluir varios elementos `<File>` dentro de `<FileList>` cuando un único paquete contenga varios ensamblados de control.</span><span class="sxs-lookup"><span data-stu-id="99512-121">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="99512-122">También puede tener varios nodos `<ToolboxItems>` dentro de un único elemento `<File>` si quiere organizar los controles en categorías distintas.</span><span class="sxs-lookup"><span data-stu-id="99512-122">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="99512-123">En el ejemplo siguiente, el control implementado en `ManagedPackage.winmd` aparecerá en Visual Studio y en Blend en un grupo denominado "Managed Package" (Paquete administrado) y "MyCustomControl" aparecerá en ese grupo.</span><span class="sxs-lookup"><span data-stu-id="99512-123">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="99512-124">Todos estos nombres son arbitrarios.</span><span class="sxs-lookup"><span data-stu-id="99512-124">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Control de ejemplo tal y como aparece en Visual Studio](media/UWP-control-vs-toolbox.png)

![Control de ejemplo tal y como aparece en Blend](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="99512-127">Debe especificar explícitamente todos los controles que quiera ver en el panel Recursos o en el cuadro de herramientas.</span><span class="sxs-lookup"><span data-stu-id="99512-127">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="99512-128">Asegúrese de especificarlos con el formato `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="99512-128">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="99512-129">Agregar iconos personalizados a los controles</span><span class="sxs-lookup"><span data-stu-id="99512-129">Add custom icons to your controls</span></span>

<span data-ttu-id="99512-130">Para mostrar un icono personalizado en el panel Recursos o en el cuadro de herramientas, agregue una imagen a su proyecto o al proyecto `design.dll` correspondiente con el nombre "Namespace.ControlName.extension" y establezca la acción de compilación en "Recurso incrustado".</span><span class="sxs-lookup"><span data-stu-id="99512-130">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="99512-131">Los formatos compatibles son `.png`, `.jpg`, `.jpeg`, `.gif` y `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="99512-131">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="99512-132">El tamaño de imagen recomendado es de 64 por 64 píxeles.</span><span class="sxs-lookup"><span data-stu-id="99512-132">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="99512-133">En el ejemplo siguiente, el proyecto contiene un archivo de imagen denominado "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="99512-133">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Establecer un icono personalizado en un proyecto](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="99512-135">Para los controles nativos, debe colocar el icono como recurso en el proyecto `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="99512-135">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="99512-136">Compatibilidad con versiones específicas de la plataforma de Windows</span><span class="sxs-lookup"><span data-stu-id="99512-136">Support specific Windows platform versions</span></span>

<span data-ttu-id="99512-137">Los paquetes UWP tienen una versión de la plataforma de destino (TPV) y una versión mínima de la plataforma de destino (TPMinV) que definen los límites superior e inferior de la versión del sistema operativo en el que se puede instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99512-137">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="99512-138">Además, la TPV especifica la versión del SDK en el que se ha compilado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99512-138">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="99512-139">Sea consciente de estas propiedades al crear un paquete UWP: si usa API fuera de los límites de las versiones de la plataforma definidas en la aplicación, se producirá un error en la compilación o se producirá un error en la aplicación en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="99512-139">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="99512-140">Por ejemplo, supongamos que ha establecido la TPMinV del paquete de controles en Windows 10 Anniversary Edition (10.0; compilación 14393). Quiere asegurarse de que el paquete se consume solo en proyectos UWP que coinciden con ese límite inferior.</span><span class="sxs-lookup"><span data-stu-id="99512-140">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="99512-141">Para que los proyectos de UWP puedan consumir el paquete, debe empaquetar los controles con los nombres de carpeta siguientes:</span><span class="sxs-lookup"><span data-stu-id="99512-141">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0\*
    \ref\uap10.0\*

<span data-ttu-id="99512-142">Para forzar la comprobación de TPMinV adecuada, cree un [archivo de destinos de MSBuild](/visualstudio/msbuild/msbuild-targets) y empaquételo en `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing ` (reemplace <your_assembly_name> con el nombre del ensamblado en cuestión).</span><span class="sxs-lookup"><span data-stu-id="99512-142">To enforce the appropriate TPMinV check, create an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) and package it under the `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing `<your_assembly_name>\` with the name of your specific assembly.</span></span>

<span data-ttu-id="99512-143">Aquí se muestra un ejemplo del aspecto que debería tener el archivo de destinos:</span><span class="sxs-lookup"><span data-stu-id="99512-143">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="99512-144">Agregar compatibilidad en tiempo de diseño</span><span class="sxs-lookup"><span data-stu-id="99512-144">Add design-time support</span></span>

<span data-ttu-id="99512-145">Para configurar la ubicación donde se mostrarán las propiedades del control en el inspector de propiedad, agregarán adornos personalizados, etc., coloque el archivo `design.dll` dentro de la carpeta `lib\uap10.0\Design`, según corresponda con la plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="99512-145">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="99512-146">Además, para asegurarse de que la característica **[Editar plantilla > Editar una copia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funciona, debe incluir el archivo `Generic.xaml` y todos los diccionarios de recursos que fusione en la carpeta `<your_assembly_name>\Themes` (una vez más, usando el nombre de ensamblado real).</span><span class="sxs-lookup"><span data-stu-id="99512-146">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="99512-147">(este archivo no influye en el comportamiento en tiempo de ejecución de un control). La estructura de carpetas podría aparecer así:</span><span class="sxs-lookup"><span data-stu-id="99512-147">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="99512-148">De forma predeterminada, las propiedades del control se mostrarán en la categoría Varios del inspector de propiedad.</span><span class="sxs-lookup"><span data-stu-id="99512-148">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="99512-149">Usar cadenas y recursos</span><span class="sxs-lookup"><span data-stu-id="99512-149">Use strings and resources</span></span>

<span data-ttu-id="99512-150">Puede insertar recursos de cadena (`.resw`) en el paquete, que el control o el proyecto UWP de consumo pueden usar. Para ello, establezca la propiedad **Acción de compilación** del archivo `.resw` en **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="99512-150">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="99512-151">Para ver un ejemplo, vea [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) en el ejemplo de ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="99512-151">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="99512-152">Contenido del paquete (por ejemplo, imágenes)</span><span class="sxs-lookup"><span data-stu-id="99512-152">Package content such as images</span></span>

<span data-ttu-id="99512-153">Para empaquetar contenido, como las imágenes que el control o el proyecto UWP de consumo pueden usar, coloque dichos archivos en la carpeta `lib\uap10.0`.</span><span class="sxs-lookup"><span data-stu-id="99512-153">To package content such as images that can be used by your control or the consuming UWP project, place those files within the `lib\uap10.0` folder.</span></span>

<span data-ttu-id="99512-154">También puede crear un [archivo de destinos de MSBuild](/visualstudio/msbuild/msbuild-targets) para asegurarse de que el recurso se copia en la carpeta de salida del proyecto de consumo:</span><span class="sxs-lookup"><span data-stu-id="99512-154">You may also author an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="99512-155">Vea también</span><span class="sxs-lookup"><span data-stu-id="99512-155">See also</span></span>

- [<span data-ttu-id="99512-156">Crear paquetes UWP</span><span class="sxs-lookup"><span data-stu-id="99512-156">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="99512-157">Ejemplo de ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="99512-157">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)