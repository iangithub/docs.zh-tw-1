---
title: ICorDebugValue2::GetExactType 方法
ms.date: 03/30/2017
api_name:
- ICorDebugValue2.GetExactType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValue2::GetExactType
helpviewer_keywords:
- ICorDebugValue2::GetExactType method [.NET Framework debugging]
- GetExactType method [.NET Framework debugging]
ms.assetid: 8e9aae1b-d1b7-4b6e-b577-6faf36dcec85
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c28ff84b08802246d587bfa130ae5915177932ac
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67764300"
---
# <a name="icordebugvalue2getexacttype-method"></a>ICorDebugValue2::GetExactType 方法
若"ICorDebugType 」 物件，表示要取得的介面指標<xref:System.Type>此值。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetExactType (  
    [out] ICorDebugType   **ppType  
);  
```  
  
## <a name="parameters"></a>參數  
 `ppType`  
 [out]位址指標`ICorDebugType`物件，表示<xref:System.Type>的這個 「 ICorDebugValue2 」 物件所表示的值。  
  
## <a name="remarks"></a>備註  
 感知泛型`GetExactType`方法會取代兩者[icordebugobjectvalue:: Getclass](../../../../docs/framework/unmanaged-api/debugging/icordebugobjectvalue-getclass-method.md)並[icordebugvalue:: Gettype](../../../../docs/framework/unmanaged-api/debugging/icordebugvalue-gettype-method.md)方法，每個傳回值的型別相關資訊.  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱
