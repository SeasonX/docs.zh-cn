---
title: <system.web> 元素（网络设置）
ms.date: 03/30/2017
helpviewer_keywords:
- Web.config configuration file [ASP.NET]
- system.Web element
- <system.Web> element
- ASP.NET configuration system
- configuration files [ASP.NET]
ms.assetid: 24c4cf4f-ad32-42b2-b040-8e4549e2855e
ms.openlocfilehash: 5c5c857d4494b6d78b819e56bae4213abc5e2035
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699096"
---
# <a name="systemweb-element-web-settings"></a>\<system.web > 元素（Web 设置）
包含有关 ASP.NET 承载层如何管理进程范围的行为的信息。  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp;&nbsp; **\<system.web >**  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.web>  
</system.web>  
```  
  
## <a name="attributes-and-elements"></a>属性和元素  

下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>Attributes  

无。  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|[\<applicationPool>](applicationpool-element-web-settings.md)|为 aspnet 文件中的 IIS 应用程序池指定配置设置。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[\<configuration>](../configuration-element.md)|指定公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
  
## <a name="remarks"></a>备注  

`system.web` 元素及其子 `applicationPool` 元素已添加到 .NET Framework 3.5 SP1 中的 .NET Framework。 在集成模式下运行 IIS 7.0 或更高版本时，此元素组合可让你配置 ASP.NET 管理线程的方式，以及在 ASP.NET 托管在 IIS 应用程序池中时，如何将请求排队。 如果在经典或 ISAPI 模式下运行 IIS 7.0 或更高版本，则将忽略这些设置。  
  
## <a name="example"></a>示例  

下面的示例演示当 ASP.NET 托管在 IIS 应用程序池中时，如何在 ASP.NET 文件中配置进程范围行为。 该示例假设 IIS 在集成模式下运行，并且该应用程序正在使用 .NET Framework 3.5 SP1 或更高版本。 此行为不会在早于 .NET Framework 3.5 SP1 的 .NET Framework 版本中发生。 示例中的值为默认值。  
  
```xml  
<configuration>  
  <system.web>  
    <applicationPool   
        maxConcurrentRequestsPerCPU="5000"   
        maxConcurrentThreadsPerCPU="0"   
        requestQueueLimit="5000" />  
  </system.web>  
</configuration>  
```  
  
## <a name="element-information"></a>元素信息  
  
|||  
|-|-|  
|命名空间||  
|架构名称||  
|验证文件||  
|可以为空||  
  
## <a name="see-also"></a>另请参阅

- [\<applicationPool> 元素（Web 设置）](applicationpool-element-web-settings.md)
