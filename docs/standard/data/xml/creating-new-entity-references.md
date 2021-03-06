---
title: 创建新实体引用
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: a42f81b3-0403-4e34-b346-7d2129804e54
ms.openlocfilehash: 8c81aae89bbe5979dffdc47a369349bd2b3f2df7
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2020
ms.locfileid: "75710981"
---
# <a name="creating-new-entity-references"></a>创建新实体引用
CreateEntityReference 方法新建 XmlEntityReference 节点。 XML 文档对象模型 (DOM) 查看是否已声明了引用的实体名称。 如果已声明，从实体声明节点复制 XmlEntityReference 节点的子节点。 如果没有匹配的实体声明，则附加一个空的文本节点作为实体引用节点的唯一子级。 由于 XmlEntityReference 节点的子节点是其他节点的副本，因此这些子节点是只读的，无法修改。  
  
 当复制节点时，在实体引用所处的范围内可能存在一个命名空间。 此命名空间影响生成的任何元素或属性节点的配置。  
  
> [!NOTE]
> 仅当将 EntityReference 节点插入文档时，DOM 才将子节点添加到 EntityReference。 新建的 EntityReference 节点没有子节点。  
  
 尽管 XmlDataDocument 是 XmlDocument 的派生类，但 XmlDataDocument 不支持创建实体引用。 这是因为 EntityReference 子级是只读的。 EntityReference 节点的子级可以跨越多个区域。 在这种情况下，行中与包含 EntityReference 一部分的区域关联的部分是只读的。  
  
## <a name="see-also"></a>另请参阅

- [XML 文档对象模型 (DOM)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
