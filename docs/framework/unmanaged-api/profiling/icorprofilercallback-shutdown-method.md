---
title: ICorProfilerCallback::Shutdown 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.Shutdown
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::Shutdown
helpviewer_keywords:
- ICorProfilerCallback::Shutdown method [.NET Framework profiling]
- Shutdown method [.NET Framework profiling]
ms.assetid: 1ea194f0-a331-4855-a2ce-37393b8e5f84
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9d63dd911a5f674a3ce0b02ec78de443c7aebf84
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67747167"
---
# <a name="icorprofilercallbackshutdown-method"></a>ICorProfilerCallback::Shutdown 方法
通知應用程式正在關閉分析工具。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT Shutdown();  
```  
  
## <a name="remarks"></a>備註  
 分析工具程式碼無法安全地呼叫方法[ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)介面之後`Shutdown`呼叫方法。 呼叫任何`ICorProfilerInfo`方法會導致未定義的行為之後,`Shutdown`方法會傳回。 特定的不可變事件仍然可能發生之後關機;分析工具應該謹慎地發生這種情況時，立即傳回。  
  
 `Shutdown`正在分析 managed 應用程式啟動為 managed 程式碼時，才會呼叫方法 （也就是初始堆疊上的框架處理程序管理）。 如果應用程式啟動為 unmanaged 程式碼，但稍後開始運用 managed 程式碼，藉此建立的執行個體的 common language runtime (CLR)，然後`Shutdown`將不會呼叫。 在這些情況下，分析工具應該在其文件庫中包含`DllMain`釋放任何資源，並執行清除其資料，例如排清到磁碟等的追蹤處理常式，它會使用 DLL_PROCESS_DETACH 值。  
  
 一般情況下，分析工具必須應付非預期的關機。 比方說，可能會停止處理程序的 Win32 的`TerminateProcess`（Winbase.h 中宣告） 的方法。 在其他情況下，CLR 將會中止特定 managed 的執行緒 （背景執行緒），而不進行有條理的解構郵件傳遞它們。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl, CorProf.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerCallback 介面](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [Initialize 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)
