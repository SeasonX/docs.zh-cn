---
title: 响应 CheckBox 单击
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Click event [Windows Forms], CheckBox control
- CheckBox control [Windows Forms], Click events
- events [Windows Forms], Click events
- double-clicks
- check boxes [Windows Forms], responding to events
ms.assetid: c39f901e-8899-43b6-aa31-939cbf7089fb
ms.openlocfilehash: ba2afb52939a6274978ce725dac19b5622419b99
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2020
ms.locfileid: "76735665"
---
# <a name="how-to-respond-to-windows-forms-checkbox-clicks"></a>如何： 响应 Windows 窗体复选框单击
每当用户单击 Windows 窗体 <xref:System.Windows.Forms.CheckBox> 控制时，将发生 <xref:System.Windows.Forms.Control.Click> 事件。 您可以对应用程序进行编程，根据复选框的状态执行某些操作。  
  
### <a name="to-respond-to-checkbox-clicks"></a>响应复选框单击  
  
1. 在 <xref:System.Windows.Forms.Control.Click> 事件处理程序中，使用 <xref:System.Windows.Forms.CheckBox.Checked%2A> 属性来确定控件的状态，并执行任何必要的操作。  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       ' The CheckBox control's Text property is changed each time the   
       ' control is clicked, indicating a checked or unchecked state.  
       If CheckBox1.Checked = True Then  
          CheckBox1.Text = "Checked"  
       Else  
          CheckBox1.Text = "Unchecked"  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       // The CheckBox control's Text property is changed each time the   
       // control is clicked, indicating a checked or unchecked state.  
       if (checkBox1.Checked)  
       {  
          checkBox1.Text = "Checked";  
       }  
       else  
       {  
          checkBox1.Text = "Unchecked";  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if (checkBox1->Checked)  
          {  
             checkBox1->Text = "Checked";  
          }  
          else  
          {  
             checkBox1->Text = "Unchecked";  
          }  
       }  
    ```  
  
    > [!NOTE]
    > 如果用户尝试双击 <xref:System.Windows.Forms.CheckBox> 控件，则每次单击都将单独处理;也就是说，<xref:System.Windows.Forms.CheckBox> 控件不支持双击事件。  
  
    > [!NOTE]
    > 当 `true` <xref:System.Windows.Forms.CheckBox.AutoCheck%2A> 属性（默认值）时，当单击 <xref:System.Windows.Forms.CheckBox> 时，将自动选择或清除。 否则，必须在发生 <xref:System.Windows.Forms.Control.Click> 事件时手动设置 <xref:System.Windows.Forms.CheckBox.Checked%2A> 属性。  
  
     你还可以使用 <xref:System.Windows.Forms.CheckBox> 控件确定操作过程。  
  
### <a name="to-determine-a-course-of-action-when-a-check-box-is-clicked"></a>单击复选框时确定操作过程  
  
1. 使用 case 语句查询 <xref:System.Windows.Forms.CheckBox.CheckState%2A> 属性的值以确定操作过程。 如果将 <xref:System.Windows.Forms.CheckBox.ThreeState%2A> 属性设置为 `true`，则 <xref:System.Windows.Forms.CheckBox.CheckState%2A> 属性可能会返回三个可能的值，这些值表示要检查的框、未选中的框或第三个不确定状态，在此状态下，将显示一个灰显外观，指示选项不可用。  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       Select Case CheckBox1.CheckState  
          Case CheckState.Checked  
             ' Code for checked state.  
          Case CheckState.Unchecked  
             ' Code for unchecked state.  
          Case CheckState.Indeterminate  
             ' Code for indeterminate state.  
       End Select   
    End Sub  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       switch(checkBox1.CheckState)  
       {  
          case CheckState.Checked:  
             // Code for checked state.  
             break;  
          case CheckState.Unchecked:  
             // Code for unchecked state.  
             break;  
          case CheckState.Indeterminate:  
             // Code for indeterminate state.  
             break;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          switch(checkBox1->CheckState) {  
             case CheckState::Checked:  
                // Code for checked state.  
                break;  
             case CheckState::Unchecked:  
                // Code for unchecked state.  
                break;  
             case CheckState::Indeterminate:  
                // Code for indeterminate state.  
                break;  
          }  
       }  
    ```  
  
    > [!NOTE]
    > 当 <xref:System.Windows.Forms.CheckBox.ThreeState%2A> 属性设置为 `true`时，<xref:System.Windows.Forms.CheckBox.Checked%2A> 属性返回 <xref:System.Windows.Forms.CheckState.Checked> 和 <xref:System.Windows.Forms.CheckState.Indeterminate>的 `true`。  
  
## <a name="see-also"></a>另请参阅

- <xref:System.Windows.Forms.CheckBox>
- [CheckBox 控件概述](checkbox-control-overview-windows-forms.md)
- [如何：使用 Windows 窗体 CheckBox 控件设置选项](how-to-set-options-with-windows-forms-checkbox-controls.md)
- [CheckBox 控件](checkbox-control-windows-forms.md)
