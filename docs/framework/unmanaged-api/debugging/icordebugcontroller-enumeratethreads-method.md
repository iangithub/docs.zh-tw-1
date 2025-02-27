---
title: ICorDebugController::EnumerateThreads 方法
ms.date: 03/30/2017
api_name:
- ICorDebugController.EnumerateThreads
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::EnumerateThreads
helpviewer_keywords:
- ICorDebugController::EnumerateThreads method [.NET Framework debugging]
- EnumerateThreads method [.NET Framework debugging]
ms.assetid: 73f536f6-4668-4a4a-b3e4-ac7df862d5be
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 73b84179717e4b96a5c3637b85ae936a23bbf42d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67748862"
---
# <a name="icordebugcontrollerenumeratethreads-method"></a>ICorDebugController::EnumerateThreads 方法
取得作用中的 managed 執行緒處理序中的列舉值。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT EnumerateThreads (  
    [out] ICorDebugThreadEnum **ppThreads  
);  
```  
  
## <a name="parameters"></a>參數  
 `ppThreads`  
 [out]「 ICorDebugThreadEnum 」 物件，表示作用中的程序中的所有 managed 執行緒的列舉值的位址指標。  
  
## <a name="remarks"></a>備註  
 執行緒會被視為作用中後[icordebugmanagedcallback:: Createthread](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-createthread-method.md)分派回呼之前[icordebugmanagedcallback:: Exitthread](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-exitthread-method.md)分派回呼. Managed 的執行緒不一定能任何受控的框架上其堆疊。 執行緒可以列舉甚至[icordebugmanagedcallback:: Createprocess](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-createprocess-method.md)回呼。 列舉型別自然會是空的。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱
