---
title: ICLRAppDomainResourceMonitor::GetCurrentAllocated 方法
ms.date: 03/30/2017
api_name:
- ICLRAppDomainResourceMonitor.GetCurrentAllocated
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAppDomainResourceMonitor::GetCurrentAllocated
helpviewer_keywords:
- GetCurrentAllocated method [.NET Framework hosting]
- ICLRAppDomainResourceMonitor::GetCurrentAllocated method [.NET Framework hosting]
ms.assetid: 7bab209c-efd4-44c2-af30-61abab0ae2fc
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 19aced41860002081caaf6436bad08f5f9a09e9a
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67766652"
---
# <a name="iclrappdomainresourcemonitorgetcurrentallocated-method"></a>ICLRAppDomainResourceMonitor::GetCurrentAllocated 方法
取得以位元組為單位，因為它已建立，但不減去已回收的記憶體已建立的應用程式定義域的所有記憶體配置的大小總計。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetCurrentAllocated([in]  DWORD dwAppDomainId,  
                            [out] ULONGLONG* pBytesAllocated);  
```  
  
## <a name="parameters"></a>參數  
 `dwAppDomainId`  
 [in]要求的應用程式定義域的識別碼。  
  
 `pBytesAllocated`  
 [out]所有記憶體配置的總大小指標。  
  
## <a name="return-value"></a>傳回值  
 這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|已成功完成命令。|  
|COR_E_APPDOMAINUNLOADED|應用程式定義域已卸載或不存在。|  
  
## <a name="remarks"></a>備註  
 這個方法相當於未受管理的受管理<xref:System.AppDomain.MonitoringTotalAllocatedMemorySize%2A?displayProperty=nameWithType>屬性。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** MetaHost.h  
  
 **LIBRARY:** 包含做為 MSCorEE.dll 中的資源  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICLRAppDomainResourceMonitor 介面](../../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md)
- [應用程式定義域資源監視](../../../../docs/standard/garbage-collection/app-domain-resource-monitoring.md)
- [裝載介面](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [裝載](../../../../docs/framework/unmanaged-api/hosting/index.md)
