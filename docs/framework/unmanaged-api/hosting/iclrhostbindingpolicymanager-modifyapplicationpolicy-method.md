---
title: ICLRHostBindingPolicyManager::ModifyApplicationPolicy 方法
ms.date: 03/30/2017
api_name:
- ICLRHostBindingPolicyManager.ModifyApplicationPolicy
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRHostBindingPolicyManager::ModifyApplicationPolicy
helpviewer_keywords:
- ICLRHostBindingPolicyManager::ModifyApplicationPolicy method [.NET Framework hosting]
- ModifyApplicationPolicy method [.NET Framework hosting]
ms.assetid: d82d633e-cce6-427c-8b02-8227e34e12ba
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0a9e438e6dd436303cd6f7aa60c779179b5d3c04
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779662"
---
# <a name="iclrhostbindingpolicymanagermodifyapplicationpolicy-method"></a>ICLRHostBindingPolicyManager::ModifyApplicationPolicy 方法
指定之組件，會修改繫結原則，並建立原則的新版本。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT  ModifyApplicationPolicy (  
    [in] LPCWSTR     pwzSourceAssemblyIdentity,   
    [in] LPCWSTR     pwzTargetAssemblyIdentity,  
    [in] BYTE       *pbApplicationPolicy,  
    [in] DWORD       cbAppPolicySize,  
    [in] DWORD       dwPolicyModifyFlags,  
    [out, size_is(*pcbNewAppPolicySize)] BYTE *pbNewApplicationPolicy,   
    [in, out] DWORD *pcbNewAppPolicySize  
);  
```  
  
## <a name="parameters"></a>參數  
 `pwzSourceAssemblyIdentity`  
 [in]若要修改的組件身分識別。  
  
 `pwzTargetAssemblyIdentity`  
 [in]新的身分識別修改過的組件。  
  
 `pbApplicationPolicy`  
 [in]包含要修改的組件的繫結原則資料緩衝區的指標。  
  
 `cbAppPolicySize`  
 [in]要被取代的繫結原則的大小。  
  
 `dwPolicyModifyFlags`  
 [in]邏輯 OR 結合[EHostBindingPolicyModifyFlags](../../../../docs/framework/unmanaged-api/hosting/ehostbindingpolicymodifyflags-enumeration.md)值，表示重新導向的控制項。  
  
 `pbNewApplicationPolicy`  
 [out]包含新的原則資料繫結的緩衝區指標。  
  
 `pcbNewAppPolicySize`  
 [in、 out]新的繫結原則緩衝區的大小指標。  
  
## <a name="return-value"></a>傳回值  
  
|HRESULT|說明|  
|-------------|-----------------|  
|S_OK|已成功修改原則。|  
|E_INVALIDARG|`pwzSourceAssemblyIdentity` 或`pwzTargetAssemblyIdentity`是 null 參考。|  
|ERROR_INSUFFICIENT_BUFFER|`pbNewApplicationPolicy` 為太小。|  
|HOST_E_CLRNOTAVAILABLE|Common language runtime (CLR) 尚未載入到處理程序，或 CLR 處於的狀態不能在其中執行 managed 程式碼，或程序呼叫成功。|  
|HOST_E_TIMEOUT|呼叫已逾時。|  
|HOST_E_NOT_OWNER|呼叫端未擁有鎖定。|  
|HOST_E_ABANDONED|事件已取消時已封鎖的執行緒或 fiber 等候它。|  
|E_FAIL|發生未知的嚴重錯誤。 方法會傳回 E_FAIL 之後，CLR 不再使用舊的處理序內。 若要裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。|  
  
## <a name="remarks"></a>備註  
 `ModifyApplicationPolicy`兩次呼叫方法。 第一次呼叫都應該提供 null 值`pbNewApplicationPolicy`參數。 此呼叫會傳回與所需值`pcbNewAppPolicySize`。 第二次呼叫應該提供此值`pcbNewAppPolicySize`，並指向該大小的緩衝區`pbNewApplicationPolicy`。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** MSCorEE.h  
  
 **LIBRARY:** 包含做為 MSCorEE.dll 中的資源  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICLRHostBindingPolicyManager 介面](../../../../docs/framework/unmanaged-api/hosting/iclrhostbindingpolicymanager-interface.md)
