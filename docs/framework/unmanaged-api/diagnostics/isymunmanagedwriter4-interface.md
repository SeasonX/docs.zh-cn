---
title: ISymUnmanagedWriter4 接口
ms.date: 03/30/2017
ms.assetid: 4af5e8c0-987d-405e-b934-8b9e70fcae6e
ms.openlocfilehash: a656777461c50b5a1593917278eb54abda982dc2
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73134569"
---
# <a name="isymunmanagedwriter4-interface"></a>ISymUnmanagedWriter4 接口
ISymUnmanagedWriter4 接口。  
  
## <a name="syntax"></a>语法  
  
```idl  
[object,uuid(BC7E3F53-F458-4C23-9DBD-A189E6E96594),pointer_default(unique)]interface ISymUnmanagedWriter4 : ISymUnmanagedWriter3  
```  
  
## <a name="methods"></a>方法  
 此接口包含下列方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetDebugInfoWithPadding 方法](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter4-getdebuginfowithpadding-method.md)|与[GetDebugInfo 方法](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-getdebuginfo-method.md)相同，不同之处在于，在终止 null 字符后使用零填充路径字符串，使字符串数据成为固定大小的 `MAX_PATH`。 仅当路径字符串长度本身小于 `MAX_PATH`时才会提供填充。<br /><br /> 这样可以更轻松地编写不同 PE 文件的工具。|  
  
## <a name="requirements"></a>要求  
 **标头：** CorSym，CorSym  
  
## <a name="see-also"></a>请参阅

- [诊断符号存储区接口](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedWriter3 接口](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter3-interface.md)
