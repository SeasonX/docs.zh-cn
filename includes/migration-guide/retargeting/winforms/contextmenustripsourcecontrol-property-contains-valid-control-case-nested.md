---
ms.openlocfilehash: f1a1eab471d46f018a8e0d0cf787d487cf67c11e
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59773999"
---
### <a name="contextmenustripsourcecontrol-property-contains-a-valid-control-in-the-case-of-nested-toolstripmenuitems"></a>存在嵌套 ToolStripMenuItems 时，ContextMenuStrip.SourceControl 属性包含有效控件

|   |   |
|---|---|
|详细信息|在 .NET Framework 4.7.1 和更早版本中，用户从嵌套 <xref:System.Windows.Forms.ToolStripMenuItem> 控件中打开菜单时，<xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType> 属性会错误地返回 null。 在 .NET Framework 4.7.2 及更高版本中，<xref:System.Windows.Forms.ContextMenuStrip.SourceControl> 属性始终设置为实际的源代码管理。|
|建议|<strong>如何选择启用或选择弃用这些更改</strong> 为使应用程序从这些更改获益，它必须在 .NET Framework 4.7.2 或更高版本上运行。 此应用程序可通过以下任何一种方式从这些更改中获益：<ul><li>它面向 .NET Framework 4.7.2。 对于面向 .NET Framework 4.7.2 或更高版本的 Windows 窗体应用程序，此更改将默认启用。</li><li>它面向 .NET Framework 4.7.1 或更早版本，通过向 app.config 文件的 <code>&lt;runtime&gt;</code> 部分添加以下 [AppContext 开关](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)并将其设置为 <code>false</code>，可选择弃用旧版辅助功能行为，如下例所示。</li></ul><pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Forms.UseLegacyContextMenuStripSourceControlValue=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>面向 .NET Framework 4.7.2 或更高版本并希望保留旧版行为的应用程序，可通过将此 AppContext 开关显式设置为 <code>true</code> 来选择启用旧版源代码管理值。|
|范围|边缘|
|版本|4.7.2|
|类型|重定目标|
|受影响的 API|<ul><li><xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType></li></ul>|
