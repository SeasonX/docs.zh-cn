---
title: 如何发布符合 .NET Framework 准则的事件 - C# 编程指南
ms.date: 07/20/2015
helpviewer_keywords:
- events [C#], implementation guidelines
ms.assetid: 9310ae16-8627-44a2-b08c-05e5976202b1
ms.openlocfilehash: 0ae240d0c078b5eaa690f128c037ee2471325872
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2020
ms.locfileid: "75705335"
---
# <a name="how-to-publish-events-that-conform-to-net-framework-guidelines-c-programming-guide"></a>如何发布符合 .NET Framework 准则的事件（C# 编程指南）
下面的过程演示了如何将遵循标准 .NET Framework 模式的事件添加到类和结构中。 .NET Framework 类库中的所有事件均基于 <xref:System.EventHandler> 委托，定义如下：  
  
```csharp  
public delegate void EventHandler(object sender, EventArgs e);  
```  
  
> [!NOTE]
> .NET Framework 2.0 引入了泛型版本的委托 <xref:System.EventHandler%601>。 下例演示了如何使用这两个版本。  
  
 尽管定义的类中的事件可基于任何有效委托类型，甚至是返回值的委托，但一般还是建议使用 <xref:System.EventHandler> 使事件基于 .NET Framework 模式，如下例中所示。  
  
### <a name="to-publish-events-based-on-the-eventhandler-pattern"></a>发布基于 EventHandler 模式的事件  
  
1. （如果无需随事件一起发送自定义数据，请跳过此步骤转到步骤 3a。）将自定义数据的类声明为对发布服务器和订阅者类均可见的范围。 然后添加所需成员以保留自定义事件数据。 在此示例中，将返回一个简单的字符串。  
  
    ```csharp  
    public class CustomEventArgs : EventArgs  
    {  
        public CustomEventArgs(string s)  
        {  
            msg = s;  
        }  
        private string msg;  
        public string Message  
        {  
            get { return msg; }  
        }   
    }  
    ```  
  
2. （如果正在使用泛型版本 <xref:System.EventHandler%601>，请跳过此步骤。）声明发布类中的委托。 为以 EventHandler  结尾的委托命名。 第二个参数指定自定义 EventArgs 类型。  
  
    ```csharp  
    public delegate void CustomEventHandler(object sender, CustomEventArgs a);  
    ```  
  
3. 使用下列步骤之一来声明发布类中的事件。  
  
    1. 如果没有任何自定义 EventArgs 类，事件类型将为非泛型 EventHandler 委托。 你无需声明该委托，因为它已在创建 C# 项目时包括的 <xref:System> 命名空间中声明。 将以下代码添加到发布服务器类。  
  
        ```csharp  
        public event EventHandler RaiseCustomEvent;  
        ```  
  
    2. 如果使用非泛型版本 <xref:System.EventHandler> 并且具有派生自 <xref:System.EventArgs> 的自定义类，请声明发布类中的事件，并将步骤 2 中的委托用作类型。  
  
        ```csharp  
        public event CustomEventHandler RaiseCustomEvent;  
        ```  
  
    3. 如果使用泛型版本，则无需自定义委托。 而是在发布类中，将事件类型指定为 `EventHandler<CustomEventArgs>`，替换尖括号中自定义类的名称。  
  
        ```csharp  
        public event EventHandler<CustomEventArgs> RaiseCustomEvent;  
        ```  
  
## <a name="example"></a>示例  
 下例通过使用自定义 EventArgs 类和 <xref:System.EventHandler%601> 作为事件类型来演示之前的步骤。  
  
 [!code-csharp[csProgGuideEvents#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEvents/CS/Events.cs#2)]  
  
## <a name="see-also"></a>请参阅

- <xref:System.Delegate>
- [C# 编程指南](../index.md)
- [事件](./index.md)
- [委托](../delegates/index.md)
