---
title: dotnet pack 命令
description: dotnet pack 命令可为 .NET Core 项目创建 NuGet 包。
ms.date: 08/08/2019
ms.openlocfilehash: 057d1029e5c933912c43c178b6db8a8498f2ed57
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2020
ms.locfileid: "76734121"
---
# <a name="dotnet-pack"></a>dotnet pack

 本文适用于：✔️ .NET Core 1.x SDK 及更高版本

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>“属性”

`dotnet pack` - 将代码打包到 NuGet 包。

## <a name="synopsis"></a>摘要

```dotnetcli
dotnet pack [<PROJECT>|<SOLUTION>] [-c|--configuration] [--force] [--include-source] [--include-symbols] [--interactive]
    [--no-build] [--no-dependencies] [--no-restore] [--nologo] [-o|--output] [--runtime] [-s|--serviceable]
    [-v|--verbosity] [--version-suffix]
dotnet pack [-h|--help]
```

## <a name="description"></a>描述

`dotnet pack` 命令生成项目并创建 NuGet 包。 该命令的结果是一个 NuGet 包，也就是一个 .nupkg 文件  。

如果要生成包含调试符号的包，可以使用以下两个选项：

- `--include-symbols`：该选项用于创建符号包。
- `--include-source`：该选项用于创建带有 `src` 文件夹的符号包，该文件夹包含源文件。

将被打包项目的 NuGet 依赖项添加到 *.nuspec* 文件，以便在安装包时可以进行正确解析。 项目到项目的引用不会打包到项目内。 目前，如果具有项目到项目的依赖项，则每个项目均必须包含一个包。

默认情况下，`dotnet pack` 先构建项目。 如果希望避免此行为，则传递 `--no-build` 选项。 此选项在持续集成 (CI) 生成方案中通常非常有用，你可以知道代码是之前生成的。

可向 `dotnet pack` 命令提供 MSBuild 属性，用于打包进程。 有关详细信息，请参阅 [NuGet 元数据属性](csproj.md#nuget-metadata-properties)和 [MSBuild 命令行引用](/visualstudio/msbuild/msbuild-command-line-reference)。 [示例](#examples)部分介绍了如何在不同的情况下使用 MSBuild -p 开关。

默认情况下，Web 项目不可打包。 若要覆盖默认行为，请将以下属性添加到 .csproj  文件中：

```xml
<PropertyGroup>
   <IsPackable>true</IsPackable>
</PropertyGroup>
```

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="arguments"></a>自变量

`PROJECT | SOLUTION`

  要打包的项目或解决方案。 它可能是 [csproj](csproj.md) 文件、解决方案文件或目录的路径。 如果未指定，此命令会搜索当前目录，以获取项目文件或解决方案文件。

## <a name="options"></a>选项

- **`-c|--configuration {Debug|Release}`**

  定义生成配置。 默认值为 `Debug`。

- **`--force`**

  强制解析所有依赖项，即使上次还原已成功，也不例外。 指定此标记等同于删除 project.assets.json 文件  。 自 .NET Core 2.0 SDK 起可用的选项。

- **`-h|--help`**

  打印出有关命令的简短帮助。

- **`--include-source`**

  除输出目录中的常规 NuGet 包外，还包括调试符号 NuGet 包。 源文件包括在符号包内的 `src` 文件夹中。

- **`--include-symbols`**

  除输出目录中的常规 NuGet 包外，还包括调试符号 NuGet 包。

- **`--interactive`**

  允许命令停止并等待用户输入或操作（例如，完成身份验证）。 自 .NET Core 3.0 SDK 起可用。

- **`--no-build`**

  打包前不生成项目。 还将隐式设置 `--no-restore` 标记。

- **`--no-dependencies`**

  忽略项目间引用，仅还原根项目。 自 .NET Core 2.0 SDK 起可用的选项。

- **`--no-restore`**

  运行此命令时不执行隐式还原。 自 .NET Core 2.0 SDK 起可用的选项。

- **`--nologo`**

  不显示启动版权标志或版权消息。 自 .NET Core 3.0 SDK 起可用。

- **`-o|--output <OUTPUT_DIRECTORY>`**

  将生成的包放置在指定目录。

- **`--runtime <RUNTIME_IDENTIFIER>`**

  指定要为其还原包的目标运行时。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。 自 .NET Core 2.0 SDK 起可用的选项。

- **`-s|--serviceable`**

  设置包中可用的标志。 有关详细信息，请参阅 [.NET 博客：.NET 4.5.1 支持 .NET NuGet 库的 Microsoft 安全更新](https://aka.ms/nupkgservicing)。

- **`--version-suffix <VERSION_SUFFIX>`**

  定义项目中 `$(VersionSuffix)` MSBuild 属性的值。

- **`-v|--verbosity <LEVEL>`**

  设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

## <a name="examples"></a>示例

- 打包当前目录中的项目：

  ```dotnetcli
  dotnet pack
  ```

- 打包 `app1` 项目：

  ```dotnetcli
  dotnet pack ~/projects/app1/project.csproj
  ```

- 打包当前目录中的项目并将生成的包放置到 `nupkgs` 文件夹：

  ```dotnetcli
  dotnet pack --output nupkgs
  ```

- 将当前目录中的项目打包到 `nupkgs` 文件夹并跳过生成步骤：

  ```dotnetcli
  dotnet pack --no-build --output nupkgs
  ```

- 将项目的版本后缀配置为 *.csproj* 文件中的 `<VersionSuffix>$(VersionSuffix)</VersionSuffix>`，使用给定的后缀打包当前项目，并更新生成的程序包版本：

  ```dotnetcli
  dotnet pack --version-suffix "ci-1234"
  ```

- 使用 `PackageVersion` MSBuild 属性将包版本设置为 `2.1.0`：

  ```dotnetcli
  dotnet pack -p:PackageVersion=2.1.0
  ```

- 打包特定[目标框架](../../standard/frameworks.md)的项目：

  ```dotnetcli
  dotnet pack -p:TargetFrameworks=net45
  ```

- 打包项目，并使用特定运行时 (Windows 10) 进行还原操作（.NET Core SDK 2.0 及更高版本）：

  ```dotnetcli
  dotnet pack --runtime win10-x64
  ```

- 使用 [.nuspec 文件](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-using-a-nuspec)打包项目：

  ```dotnetcli
  dotnet pack ~/projects/app1/project.csproj -p:NuspecFile=~/projects/app1/project.nuspec -p:NuspecBasePath=~/projects/app1/nuget
  ```
