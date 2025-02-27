---
title: ICorProfilerCallback::ThreadDestroyed 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ThreadDestroyed
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ThreadDestroyed
helpviewer_keywords:
- ThreadDestroyed method [.NET Framework profiling]
- ICorProfilerCallback::ThreadDestroyed method [.NET Framework profiling]
ms.assetid: 4c2b66fd-0595-40a3-8931-f9c4fff97ac8
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f114d32432cccd88e36ff76ed49c610bd03f873e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67747007"
---
# <a name="icorprofilercallbackthreaddestroyed-method"></a>ICorProfilerCallback::ThreadDestroyed 方法
通知分析工具已終結執行緒。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT ThreadDestroyed(  
    [in] ThreadID threadId);  
```  
  
## <a name="parameters"></a>參數  
 `threadId`  
 [in]已終結執行緒的識別碼。  
  
## <a name="remarks"></a>備註  
 `threadId`值不再有效當時的這個呼叫。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl, CorProf.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerCallback 介面](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ThreadCreated 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-threadcreated-method.md)
