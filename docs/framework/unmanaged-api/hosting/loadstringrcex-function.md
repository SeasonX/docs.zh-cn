---
title: LoadStringRCEx 函数
ms.date: 03/30/2017
api_name:
- LoadStringRCEx
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- LoadStringRCEx
helpviewer_keywords:
- LoadStringRCEx function [.NET Framework hosting]
ms.assetid: bc789636-ca14-4f07-8f77-9305874d7495
topic_type:
- apiref
ms.openlocfilehash: 68332aee895f012bcf6ab6a72936c8dddc7f28a0
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73122036"
---
# <a name="loadstringrcex-function"></a>LoadStringRCEx 函数
将 HRESULT 值转换为指定区域性的适当错误消息。  
  
 此函数已在 .NET Framework 4 中弃用。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT LoadStringRCEx (  
    [in]  LCID    lcid,   
    [in]  UINT    iResouceID,   
    [out] LPWSTR  szBuffer,   
    [in]  int     iMax,   
    [in]  int     bQuiet,   
    [out] int    *pcwchUsed  
);  
```  
  
## <a name="parameters"></a>参数  
 `lcid`  
 中区域性标识符。 传递-1，以便 `lcid` 使用默认区域性。  
  
 `iResourceID`  
 中HRESULT。  
  
 `szBuffer`  
 弄一个缓冲区，其中包含成功完成后的错误消息。  
  
 `iMax`  
 中错误消息缓冲区的大小。  
  
 `bQuiet`  
 中掉.  
  
 `pcwchUsed`  
 弄指向错误消息长度的指针。  
  
## <a name="return-value"></a>返回值  
 除以下值外，此方法还返回 Winerror.h 中定义的标准 COM 错误代码。  
  
|返回代码|描述|  
|-----------------|-----------------|  
|S_OK|该方法已成功完成。|  
|E_INVALIDARG|`szBuffer` 为 null 或 `iMax` 为零（0）。|  
  
## <a name="remarks"></a>备注  
 如果该方法未成功完成，`szBuffer` 将包含空字符串。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Mscoree.dll  
  
 **库：** Mscoree.dll  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- <xref:System.Globalization.CultureInfo.LCID%2A?displayProperty=nameWithType>
- [LoadStringRC 函数](../../../../docs/framework/unmanaged-api/hosting/loadstringrc-function.md)
- [弃用的 CLR 承载函数](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
