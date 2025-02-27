---
title: IHostThreadPoolManager::GetMaxThreads 方法
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager.GetMaxThreads
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager::GetMaxThreads
helpviewer_keywords:
- IHostThreadPoolManager::GetMaxThreads method [.NET Framework hosting]
- GetMaxThreads method, IHostThreadPoolManager interface [.NET Framework hosting]
ms.assetid: db268876-6178-4a81-aca3-318ee7f96001
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1d5b865906f797c25783c4d8a306dc91769ef9a9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67749285"
---
# <a name="ihostthreadpoolmanagergetmaxthreads-method"></a>IHostThreadPoolManager::GetMaxThreads 方法
執行緒集區中，同時取得主機維護執行緒的數目上限。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetMaxThreads (  
    [out] DWORD *pdwMaxWorkerThreads  
);  
```  
  
## <a name="parameters"></a>參數  
 `pdwMaxWorkerThreads`  
 [out]指標的主控件保留在執行緒集區中的執行緒數目上限。  
  
## <a name="return-value"></a>傳回值  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|`GetMaxThreads` 已成功傳回。|  
|HOST_E_CLRNOTAVAILABLE|Common language runtime (CLR (尚未載入處理序，或 CLR 處於狀態在它無法執行 managed 程式碼或處理程序呼叫成功。|  
|HOST_E_TIMEOUT|呼叫已逾時。|  
|HOST_E_NOT_OWNER|呼叫端未擁有鎖定。|  
|HOST_E_ABANDONED|事件已取消時已封鎖的執行緒或 fiber 等候它。|  
|E_FAIL|發生未知的嚴重錯誤。 方法會傳回 E_FAIL CLR 已不再可在此程序中使用。 若要裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。|  
|E_NOTIMPL|主機並未提供的實作`GetMaxThreads`。|  
  
## <a name="remarks"></a>備註  
 CLR 會呼叫`GetMaxThreads`來判斷執行緒集區中的執行緒總數。 [GetAvailableThreads](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-getavailablethreads-method.md)方法會取得目前未處理的工作項目中的執行緒數目。 傳回值的所有要求`pdwMaxWorkerThreads`參數保留已排入佇列，直到執行緒變成可用。  
  
 如果主機並未提供的實作`GetMaxThreads`，它應該會傳回 E_NOTIMPL 的 HRESULT 值。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** MSCorEE.h  
  
 **LIBRARY:** 包含做為 MSCorEE.dll 中的資源  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Threading.ThreadPool.GetMaxThreads%2A>
- <xref:System.Threading.ThreadPool>
- [GetMinThreads 方法](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-getminthreads-method.md)
- [SetMaxThreads 方法](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-setmaxthreads-method.md)
- [IHostThreadPoolManager 介面](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-interface.md)
