---
title: 使用设计器防止 DataGridView 控件中添加和删除行
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], preventing row addition or deletion
ms.assetid: a17722bd-9400-41e6-8dcc-c9c151f0a749
ms.openlocfilehash: cc9aff0f15d1bd6de5c469ee7069a99f3360837a
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2020
ms.locfileid: "76728708"
---
# <a name="how-to-prevent-row-addition-and-deletion-in-the-windows-forms-datagridview-control-using-the-designer"></a>如何：使用设计器防止在 Windows 窗体 DataGridView 控件中添加和删除行
有时想要阻止用户在 <xref:System.Windows.Forms.DataGridView> 控件中输入新的数据行或删除现有行。 新行在控件底部的新记录的特殊行中输入。 禁用行添加后，不会显示新记录的行。 然后，您可以通过禁用行删除和单元格编辑来使控件完全只读。

 下面的过程需要一个**Windows 应用程序**项目，其中包含一个包含 <xref:System.Windows.Forms.DataGridView> 控件的窗体。 有关设置此类项目的信息，请参阅[如何：创建 Windows 窗体应用程序项目](/visualstudio/ide/step-1-create-a-windows-forms-application-project)和[如何：将控件添加到 Windows 窗体](how-to-add-controls-to-windows-forms.md)。

## <a name="to-prevent-row-addition-and-deletion"></a>禁止添加和删除行

- 单击 <xref:System.Windows.Forms.DataGridView> 控件右上角的智能标记标志符号（![智能标记标志符号](./media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph")），然后清除 "**启用添加**" 和 "**启用删除**" 复选框。

    > [!NOTE]
    > 若要使控件完全只读，请清除 "**启用编辑**" 复选框。

## <a name="see-also"></a>另请参阅

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A?displayProperty=nameWithType>
- [如何：创建 Windows 窗体应用程序项目](/visualstudio/ide/step-1-create-a-windows-forms-application-project)
- [如何：向 Windows 窗体添加控件](how-to-add-controls-to-windows-forms.md)
