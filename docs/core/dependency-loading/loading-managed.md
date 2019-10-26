---
title: 托管程序集加载算法 - .NET Core
description: .NET Core 中托管程序集加载算法的详细信息说明
ms.date: 08/09/2019
author: sdmaclea
ms.author: stmaclea
ms.openlocfilehash: bf95cbd0eebed064f0198ae9b0f7a4288a938f8a
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "72303628"
---
# <a name="managed-assembly-loading-algorithm"></a><span data-ttu-id="bc183-103">托管程序集加载算法</span><span class="sxs-lookup"><span data-stu-id="bc183-103">Managed assembly loading algorithm</span></span>

<span data-ttu-id="bc183-104">托管程序集与涉及不同阶段的算法一起定位并加载。</span><span class="sxs-lookup"><span data-stu-id="bc183-104">Managed assemblies are located and loaded with an algorithm involving various stages.</span></span>

<span data-ttu-id="bc183-105">除附属程序集和 `WinRT` 程序集之外的所有托管程序集都使用相同算法。</span><span class="sxs-lookup"><span data-stu-id="bc183-105">All managed assemblies except satellite assemblies and `WinRT` assemblies use the same algorithm.</span></span>

## <a name="when-are-managed-assemblies-loaded"></a><span data-ttu-id="bc183-106">何时加载托管程序集？</span><span class="sxs-lookup"><span data-stu-id="bc183-106">When are managed assemblies loaded?</span></span>

<span data-ttu-id="bc183-107">触发托管程序集加载的最常见机制是静态程序集引用。</span><span class="sxs-lookup"><span data-stu-id="bc183-107">The most common mechanism to trigger a managed assembly load is a static assembly reference.</span></span> <span data-ttu-id="bc183-108">每当代码使用在另一个程序集中定义的类型时，编译器都会插入这些引用。</span><span class="sxs-lookup"><span data-stu-id="bc183-108">These references are inserted by the compiler whenever code uses a type defined in another assembly.</span></span> <span data-ttu-id="bc183-109">根据运行时的需要加载这些程序集 (`load-by-name`)。</span><span class="sxs-lookup"><span data-stu-id="bc183-109">These assemblies are loaded (`load-by-name`) as needed by the runtime.</span></span>

<span data-ttu-id="bc183-110">直接使用特定的 API 也将触发加载：</span><span class="sxs-lookup"><span data-stu-id="bc183-110">The direct use of specific APIs will also trigger loads:</span></span>

|<span data-ttu-id="bc183-111">API</span><span class="sxs-lookup"><span data-stu-id="bc183-111">API</span></span>  |<span data-ttu-id="bc183-112">说明</span><span class="sxs-lookup"><span data-stu-id="bc183-112">Description</span></span>  |<span data-ttu-id="bc183-113">`Active` <xref:System.Runtime.Loader.AssemblyLoadContext></span><span class="sxs-lookup"><span data-stu-id="bc183-113">`Active` <xref:System.Runtime.Loader.AssemblyLoadContext></span></span> |
|---------|---------|---------|
|<xref:System.Runtime.Loader.AssemblyLoadContext.LoadFromAssemblyName%2A?displayProperty=nameWithType>|`Load-by-name`|<span data-ttu-id="bc183-114">[this](../../csharp/language-reference/keywords/this.md) 实例。</span><span class="sxs-lookup"><span data-stu-id="bc183-114">The [this](../../csharp/language-reference/keywords/this.md) instance.</span></span>|
|<xref:System.Runtime.Loader.AssemblyLoadContext.LoadFromAssemblyPath%2A?displayProperty=nameWithType><p><xref:System.Runtime.Loader.AssemblyLoadContext.LoadFromNativeImagePath%2A?displayProperty=nameWithType>|<span data-ttu-id="bc183-115">从路径加载。</span><span class="sxs-lookup"><span data-stu-id="bc183-115">Load from path.</span></span>|<span data-ttu-id="bc183-116">[this](../../csharp/language-reference/keywords/this.md) 实例。</span><span class="sxs-lookup"><span data-stu-id="bc183-116">The [this](../../csharp/language-reference/keywords/this.md) instance.</span></span>|
<xref:System.Runtime.Loader.AssemblyLoadContext.LoadFromStream%2A?displayProperty=nameWithType>|<span data-ttu-id="bc183-117">从对象加载。</span><span class="sxs-lookup"><span data-stu-id="bc183-117">Load from object.</span></span>|<span data-ttu-id="bc183-118">[this](../../csharp/language-reference/keywords/this.md) 实例。</span><span class="sxs-lookup"><span data-stu-id="bc183-118">The [this](../../csharp/language-reference/keywords/this.md) instance.</span></span>|
|<xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType>|<span data-ttu-id="bc183-119">在新的 <xref:System.Runtime.Loader.AssemblyLoadContext> 实例中从路径加载</span><span class="sxs-lookup"><span data-stu-id="bc183-119">Load from path in a new <xref:System.Runtime.Loader.AssemblyLoadContext> instance</span></span>|<span data-ttu-id="bc183-120">新的 <xref:System.Runtime.Loader.AssemblyLoadContext> 实例。</span><span class="sxs-lookup"><span data-stu-id="bc183-120">The new <xref:System.Runtime.Loader.AssemblyLoadContext> instance.</span></span>|
<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>|<span data-ttu-id="bc183-121">在 <xref:System.Runtime.Loader.AssemblyLoadContext.Default%2A?displayProperty=nameWithType> 实例中从路径加载。</span><span class="sxs-lookup"><span data-stu-id="bc183-121">Load from path in the <xref:System.Runtime.Loader.AssemblyLoadContext.Default%2A?displayProperty=nameWithType> instance.</span></span><p><span data-ttu-id="bc183-122">向 <xref:System.Runtime.Loader.AssemblyLoadContext.Default%2A?displayProperty=nameWithType> 添加 <xref:System.Runtime.Loader.AssemblyLoadContext.Resolving> 处理程序。</span><span class="sxs-lookup"><span data-stu-id="bc183-122">Adds a <xref:System.Runtime.Loader.AssemblyLoadContext.Resolving> handler to <xref:System.Runtime.Loader.AssemblyLoadContext.Default%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="bc183-123">处理程序将从其目录加载程序集的依赖项。</span><span class="sxs-lookup"><span data-stu-id="bc183-123">The handler will load the assembly's dependencies from its directory.</span></span>|<span data-ttu-id="bc183-124"><xref:System.Runtime.Loader.AssemblyLoadContext.Default%2A?displayProperty=nameWithType> 实例。</span><span class="sxs-lookup"><span data-stu-id="bc183-124">The <xref:System.Runtime.Loader.AssemblyLoadContext.Default%2A?displayProperty=nameWithType> instance.</span></span>|
|<xref:System.Reflection.Assembly.Load(System.Reflection.AssemblyName)?displayProperty=nameWithType><p><xref:System.Reflection.Assembly.Load(System.String)?displayProperty=nameWithType><p><xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType>|<span data-ttu-id="bc183-125">`Load-by-name`。</span><span class="sxs-lookup"><span data-stu-id="bc183-125">`Load-by-name`.</span></span>|<span data-ttu-id="bc183-126">从调用方推断。</span><span class="sxs-lookup"><span data-stu-id="bc183-126">Inferred from caller.</span></span><p><span data-ttu-id="bc183-127">首选 <xref:System.Runtime.Loader.AssemblyLoadContext> 方法。</span><span class="sxs-lookup"><span data-stu-id="bc183-127">Prefer <xref:System.Runtime.Loader.AssemblyLoadContext> methods.</span></span>|
|<xref:System.Reflection.Assembly.Load(System.Byte[])?displayProperty=nameWithType><p><xref:System.Reflection.Assembly.Load(System.Byte[],System.Byte[])?displayProperty=nameWithType>|<span data-ttu-id="bc183-128">从对象加载。</span><span class="sxs-lookup"><span data-stu-id="bc183-128">Load from object.</span></span>|<span data-ttu-id="bc183-129">从调用方推断。</span><span class="sxs-lookup"><span data-stu-id="bc183-129">Inferred from caller.</span></span><p><span data-ttu-id="bc183-130">首选 <xref:System.Runtime.Loader.AssemblyLoadContext> 方法。</span><span class="sxs-lookup"><span data-stu-id="bc183-130">Prefer <xref:System.Runtime.Loader.AssemblyLoadContext> methods.</span></span>|
<xref:System.Type.GetType(System.String)?displayProperty=nameWithType><p><xref:System.Type.GetType(System.String,System.Boolean)?displayProperty=nameWithType><p><xref:System.Type.GetType(System.String,System.Boolean,System.Boolean)?displayProperty=nameWithType>|<span data-ttu-id="bc183-131">`Load-by-name`。</span><span class="sxs-lookup"><span data-stu-id="bc183-131">`Load-by-name`.</span></span>|<span data-ttu-id="bc183-132">从调用方推断。</span><span class="sxs-lookup"><span data-stu-id="bc183-132">Inferred from caller.</span></span><p><span data-ttu-id="bc183-133">首选使用 `assemblyResolver` 参数的 <xref:System.Type.GetType%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="bc183-133">Prefer <xref:System.Type.GetType%2A?displayProperty=nameWithType> methods with an `assemblyResolver` argument.</span></span>|
<xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType>|<span data-ttu-id="bc183-134">如果类型 `name` 描述程序集限定的泛型类型，则触发 `Load-by-name`。</span><span class="sxs-lookup"><span data-stu-id="bc183-134">If type `name` describes an assembly qualified generic type, trigger a `Load-by-name`.</span></span>|<span data-ttu-id="bc183-135">从调用方推断。</span><span class="sxs-lookup"><span data-stu-id="bc183-135">Inferred from caller.</span></span><p><span data-ttu-id="bc183-136">使用程序集限定的类型名称时，首选 <xref:System.Type.GetType%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="bc183-136">Prefer <xref:System.Type.GetType%2A?displayProperty=nameWithType> when using assembly qualified type names.</span></span>|
<xref:System.Activator.CreateInstance(System.String,System.String)?displayProperty=nameWithType><p><xref:System.Activator.CreateInstance(System.String,System.String,System.Object[])?displayProperty=nameWithType><p><xref:System.Activator.CreateInstance(System.String,System.String,System.Boolean,System.Reflection.BindingFlags,System.Reflection.Binder,System.Object[],System.Globalization.CultureInfo,System.Object[])?displayProperty=nameWithType>|<span data-ttu-id="bc183-137">`Load-by-name`。</span><span class="sxs-lookup"><span data-stu-id="bc183-137">`Load-by-name`.</span></span>|<span data-ttu-id="bc183-138">从调用方推断。</span><span class="sxs-lookup"><span data-stu-id="bc183-138">Inferred from caller.</span></span><p><span data-ttu-id="bc183-139">首选采用 <xref:System.Type> 参数的 <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="bc183-139">Prefer <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType> methods taking a <xref:System.Type> argument.</span></span>|

## <a name="algorithm"></a><span data-ttu-id="bc183-140">算法</span><span class="sxs-lookup"><span data-stu-id="bc183-140">Algorithm</span></span>

<span data-ttu-id="bc183-141">以下算法描述运行时如何加载托管程序集。</span><span class="sxs-lookup"><span data-stu-id="bc183-141">The following algorithm describes how the runtime loads a managed assembly.</span></span>

1. <span data-ttu-id="bc183-142">确定 `active` <xref:System.Runtime.Loader.AssemblyLoadContext>。</span><span class="sxs-lookup"><span data-stu-id="bc183-142">Determine the `active` <xref:System.Runtime.Loader.AssemblyLoadContext>.</span></span>

    - <span data-ttu-id="bc183-143">对于静态程序集引用，`active` <xref:System.Runtime.Loader.AssemblyLoadContext> 是已加载引用程序集的实例。</span><span class="sxs-lookup"><span data-stu-id="bc183-143">For a static assembly reference, the `active` <xref:System.Runtime.Loader.AssemblyLoadContext> is the instance that loaded the referring assembly.</span></span>
    - <span data-ttu-id="bc183-144">首选 API 使 `active` <xref:System.Runtime.Loader.AssemblyLoadContext> 显式。</span><span class="sxs-lookup"><span data-stu-id="bc183-144">Preferred APIs make the `active` <xref:System.Runtime.Loader.AssemblyLoadContext> explicit.</span></span>
    - <span data-ttu-id="bc183-145">其他 API 推断 `active` <xref:System.Runtime.Loader.AssemblyLoadContext>。</span><span class="sxs-lookup"><span data-stu-id="bc183-145">Other APIs infer the `active` <xref:System.Runtime.Loader.AssemblyLoadContext>.</span></span> <span data-ttu-id="bc183-146">对于这些 API，将使用 <xref:System.Runtime.Loader.AssemblyLoadContext.CurrentContextualReflectionContext?displayProperty=nameWithType> 属性。</span><span class="sxs-lookup"><span data-stu-id="bc183-146">For these APIs, the <xref:System.Runtime.Loader.AssemblyLoadContext.CurrentContextualReflectionContext?displayProperty=nameWithType> property is used.</span></span> <span data-ttu-id="bc183-147">如果其值为 `null`，则使用推断的 <xref:System.Runtime.Loader.AssemblyLoadContext> 实例。</span><span class="sxs-lookup"><span data-stu-id="bc183-147">If its value is `null`, then the inferred <xref:System.Runtime.Loader.AssemblyLoadContext> instance is used.</span></span>
    - <span data-ttu-id="bc183-148">请见上表。</span><span class="sxs-lookup"><span data-stu-id="bc183-148">See table above.</span></span>

2. <span data-ttu-id="bc183-149">对于 `Load-by-name` 方法，活动 <xref:System.Runtime.Loader.AssemblyLoadContext> 将加载程序集。</span><span class="sxs-lookup"><span data-stu-id="bc183-149">For the `Load-by-name` methods, the active <xref:System.Runtime.Loader.AssemblyLoadContext> loads the assembly.</span></span> <span data-ttu-id="bc183-150">通过以下方式按优先级排序：</span><span class="sxs-lookup"><span data-stu-id="bc183-150">In priority order by:</span></span>
    - <span data-ttu-id="bc183-151">检查其 `cache-by-name`。</span><span class="sxs-lookup"><span data-stu-id="bc183-151">Checking its `cache-by-name`.</span></span>

    - <span data-ttu-id="bc183-152">调用 <xref:System.Runtime.Loader.AssemblyLoadContext.Load%2A?displayProperty=nameWithType> 函数。</span><span class="sxs-lookup"><span data-stu-id="bc183-152">Calling the <xref:System.Runtime.Loader.AssemblyLoadContext.Load%2A?displayProperty=nameWithType> function.</span></span>

    - <span data-ttu-id="bc183-153">检查 <xref:System.Runtime.Loader.AssemblyLoadContext.Default%2A?displayProperty=nameWithType> 实例的缓存并运行[托管程序集默认探测](default-probing.md#managed-assembly-default-probing)逻辑。</span><span class="sxs-lookup"><span data-stu-id="bc183-153">Checking the <xref:System.Runtime.Loader.AssemblyLoadContext.Default%2A?displayProperty=nameWithType> instances' cache and running [managed assembly default probing](default-probing.md#managed-assembly-default-probing) logic.</span></span>

    - <span data-ttu-id="bc183-154">引发 AssemblyLoadContext 活动的 <xref:System.Runtime.Loader.AssemblyLoadContext.Resolving?displayProperty=nameWithType> 事件。</span><span class="sxs-lookup"><span data-stu-id="bc183-154">Raising the <xref:System.Runtime.Loader.AssemblyLoadContext.Resolving?displayProperty=nameWithType> event for the active AssemblyLoadContext.</span></span>

    - <span data-ttu-id="bc183-155">引发 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 事件。</span><span class="sxs-lookup"><span data-stu-id="bc183-155">Raising the <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> event.</span></span>

3. <span data-ttu-id="bc183-156">对于其他类型的加载，`active` <xref:System.Runtime.Loader.AssemblyLoadContext> 加载程序集。</span><span class="sxs-lookup"><span data-stu-id="bc183-156">For the other types of loads, the `active` <xref:System.Runtime.Loader.AssemblyLoadContext> loads the assembly.</span></span> <span data-ttu-id="bc183-157">通过以下方式按优先级排序：</span><span class="sxs-lookup"><span data-stu-id="bc183-157">In priority order by:</span></span>
    - <span data-ttu-id="bc183-158">检查其 `cache-by-name`。</span><span class="sxs-lookup"><span data-stu-id="bc183-158">Checking its `cache-by-name`.</span></span>

    - <span data-ttu-id="bc183-159">从指定的路径或原始程序集对象加载。</span><span class="sxs-lookup"><span data-stu-id="bc183-159">Loading from the specified path or raw assembly object.</span></span>

4. <span data-ttu-id="bc183-160">在任一情况下，如果新加载了一个程序集，则：</span><span class="sxs-lookup"><span data-stu-id="bc183-160">In either case, if an assembly is newly loaded, then:</span></span>
   - <span data-ttu-id="bc183-161">引发 <xref:System.AppDomain.AssemblyLoad?displayProperty=nameWithType> 事件。</span><span class="sxs-lookup"><span data-stu-id="bc183-161">The <xref:System.AppDomain.AssemblyLoad?displayProperty=nameWithType> event is raised.</span></span>
   - <span data-ttu-id="bc183-162">将引用添加到程序集的 <xref:System.Runtime.Loader.AssemblyLoadContext> 实例的 `cache-by-name`。</span><span class="sxs-lookup"><span data-stu-id="bc183-162">A reference is added to the assembly's <xref:System.Runtime.Loader.AssemblyLoadContext> instance's `cache-by-name`.</span></span>

5. <span data-ttu-id="bc183-163">如果找到了程序集，则会根据需要将引用添加到 `active` <xref:System.Runtime.Loader.AssemblyLoadContext> 实例的 `cache-by-name` 中。</span><span class="sxs-lookup"><span data-stu-id="bc183-163">If the assembly is found, a reference is added as needed to the `active` <xref:System.Runtime.Loader.AssemblyLoadContext> instance's `cache-by-name`.</span></span>