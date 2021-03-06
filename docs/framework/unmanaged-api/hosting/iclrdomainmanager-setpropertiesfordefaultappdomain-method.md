---
title: ICLRDomainManager::SetPropertiesForDefaultAppDomain 方法
ms.date: 03/30/2017
api_name:
- ICLRDomainManager.SetPropertiesForDefaultAppDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDomainManager::SetPropertiesForDefaultAppDomain
helpviewer_keywords:
- ICLRDomainManager::SetPropertiesForDefaultAppDomain method [.NET Framework hosting]
- SetPropertiesForDefaultAppDomain method [.NET Framework hosting]
ms.assetid: 43e61c4b-c435-45ec-9ef6-c68403aa4200
ms.openlocfilehash: 37919be2d0ebd7d243615bc5845b0781ac13e574
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73129314"
---
# <a name="iclrdomainmanagersetpropertiesfordefaultappdomain-method"></a>ICLRDomainManager::SetPropertiesForDefaultAppDomain 方法
设置将用于初始化默认应用程序域的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT SetPropertiesForDefaultAppDomain(  
    [in] DWORD nProperties,  
    [in] LPCWSTR *pwszPropertyNames,  
    [in] LPCWSTR *pwszPropertyValues  
);  
```  
  
## <a name="parameters"></a>参数  
 `nProperties`  
 中`pwszPropertyNames` 和 `pwszPropertyValues`中的条目数。  
  
 `pwszPropertyNames`  
 中属性名称的数组; 如果没有属性，则为 null。 目前，此方法识别的唯一属性名称为 "PARTIAL_TRUST_VISIBLE_ASSEMBLIES"。  
  
 `pwszPropertyValues`  
 中属性值的数组; 如果没有属性，则为 null。  
  
## <a name="return-value"></a>返回值  
 此方法返回以下特定 HRESULT 以及表示方法失败的 HRESULT 错误。  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|该方法已成功完成。|  
|HRESULT_FROM_WIN32(ERROR_UNKNOWN_PROPERTY)|`pwszPropertyNames` 包含此方法无法识别的属性名称。|  
  
## <a name="remarks"></a>备注  
 "PARTIAL_TRUST_VISIBLE_ASSEMBLIES" 的属性值是一个程序集列表，其中包含具有 <xref:System.Security.PartialTrustVisibilityLevel.NotVisibleByDefault?displayProperty=nameWithType> 标志的条件 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> （APTCA）特性，在默认应用程序域中对部分受信任的调用方可见。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MetaHost  
  
 **库：** 作为资源包括在 Mscoree.dll 中  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [承载](../../../../docs/framework/unmanaged-api/hosting/index.md)
- [ICLRDomainManager 接口](../../../../docs/framework/unmanaged-api/hosting/iclrdomainmanager-interface.md)
