---
title: ICorDebugMDA::GetName 方法
ms.date: 03/30/2017
api_name:
- ICorDebugMDA.GetName
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMDA::GetName
helpviewer_keywords:
- ICorDebugMDA::GetName method [.NET Framework debugging]
- GetName method, ICorDebugMDA interface [.NET Framework debugging]
ms.assetid: 885bf5e8-00b7-4cd7-9d8d-e720d47918c4
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ca5d96e51c3809c6652d1a1fd75b80efb0b34222
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67761908"
---
# <a name="icordebugmdagetname-method"></a>ICorDebugMDA::GetName 方法
取得字串，包含由受管理的偵錯助理 (MDA) 的名稱[ICorDebugMDA](../../../../docs/framework/unmanaged-api/debugging/icordebugmda-interface.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetName (  
    [in] ULONG32   cchName,  
    [out] ULONG32  *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]  
        WCHAR      szName[]  
);  
```  
  
## <a name="parameters"></a>參數  
 `cchName`  
 [in] `szName` 陣列的大小。  
  
 `pcchName`  
 [out]名稱長度的指標。  
  
 `szName`  
 [out]用來儲存名稱的陣列。  
  
## <a name="remarks"></a>備註  
 MDA 名稱是唯一的值。 `GetName`方法是取得 XML 資料流，以及從結構描述為基礎的資料流中擷取名稱方便能替代方式。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorDebugMDA 介面](../../../../docs/framework/unmanaged-api/debugging/icordebugmda-interface.md)
- [診斷 Managed 偵錯助理的錯誤](../../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
