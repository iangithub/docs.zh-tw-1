---
title: ICorProfilerCallback::JITInlining 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITInlining
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITInlining
helpviewer_keywords:
- JITInlining method [.NET Framework profiling]
- ICorProfilerCallback::JITInlining method [.NET Framework profiling]
ms.assetid: c2f45801-dd38-4b78-b6b7-64397dc73f83
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 82af06837ead9a00923c23d4ce145015308fbbf7
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782795"
---
# <a name="icorprofilercallbackjitinlining-method"></a>ICorProfilerCallback::JITInlining 方法
通知分析工具，在 just-in-time (JIT) 編譯器插入符合另一個函式的函式。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT JITInlining(  
    [in]  FunctionID callerId,  
    [in]  FunctionID calleeId,  
    [out] BOOL      *pfShouldInline);  
```  
  
## <a name="parameters"></a>參數  
 `callerId`  
 [in]在其中函式的識別碼`calleeId`函式會插入。  
  
 `calleeId`  
 [in]要插入函式的識別碼。  
  
 `pfShouldInline`  
 [out]`true`允許發生; 插入，否則為`false`。  
  
## <a name="remarks"></a>備註  
 分析工具可以設定`pfShouldInline`要`false`若要避免`calleeId`函式插入`callerId`函式。 此外，分析工具可以全域使用停用內嵌插入 COR_PRF_DISABLE_INLINING 值[COR_PRF_MONITOR](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md)列舉型別。  
  
 插入函式內嵌不會引發事件進入或離開。 因此，必須設定分析工具`pfShouldInline`至`false`才能產生精確的 callgraph。 設定`pfShouldInline`至`false`會影響效能，因為內嵌插入通常會增加速度和減少的插入方法的不同 JIT 編譯事件。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl, CorProf.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerCallback 介面](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
