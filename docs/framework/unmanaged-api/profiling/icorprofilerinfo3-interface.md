---
title: ICorProfilerInfo3 介面
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3
helpviewer_keywords:
- ICorProfilerInfo3 interface [.NET Framework profiling]
ms.assetid: 044a262f-0fa7-485d-b0c1-64cdc359c654
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bb0944829d9f33277fdf53ad78cc37878336434f
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66486957"
---
# <a name="icorprofilerinfo3-interface"></a>ICorProfilerInfo3 介面
提供程式碼分析工具用於和 Common Language Runtime (CLR) 通訊，以控制事件監視以及要求資訊的方法。 `ICorProfilerInfo3`介面是擴充功能[ICorProfilerInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)介面。 它提供.NET Framework 4 及更新版本中支援的新方法。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[EnumJITedFunctions 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enumjitedfunctions-method.md)|傳回所有先前 JIT 編譯函式的列舉。|  
|[EnumModules 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enummodules-method.md)|傳回提供循序逐一查看 Managed 模組集合方法的列舉，其中該模組被載入至應用程式中。|  
|[GetAppDomainsContainingModule 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getappdomainscontainingmodule-method.md)|取得已載入指定模組之應用程式定義域的識別項。|  
|[GetFunctionEnter3Info 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionenter3info-method.md)|提供給分析工具所報告的函式之堆疊框架和引數資訊[FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md)函式; lze vyvolat pouze během`FunctionEnter3WithInfo`回呼。|  
|[GetFunctionLeave3Info 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionleave3info-method.md)|提供的堆疊框架和傳回值的函式報告給分析工具所[FunctionLeave3WithInfo 函式](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md)函式; lze vyvolat pouze během`FunctionLeave3WithInfo`回呼。|  
|[GetFunctionTailcall3Info 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctiontailcall3info-method.md)|提供給分析工具所報告的函式的堆疊框架[FunctionTailcall3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md)函式; lze vyvolat pouze během`FunctionTailcall3WithInfo`回呼。|  
|[GetModuleInfo2 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getmoduleinfo2-method.md)|提供模組 ID，傳回該模組的檔案名稱、此模組父代組件的 ID 和描述模組屬性的位元遮罩。|  
|[GetRuntimeInformation 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getruntimeinformation-method.md)|提供有關正在分析之執行階段的版本資訊。|  
|[GetStringLayout2 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getstringlayout2-method.md)|取得字串物件配置的相關資訊。|  
|[GetThreadStaticAddress2 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getthreadstaticaddress2-method.md)|取得指定執行緒靜態欄位的位址，這位於指定之執行緒和應用程式定義域的範圍內。|  
|[RequestProfilerDetach 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-requestprofilerdetach-method.md)|指示該執行階段中斷與分析工具的連結。|  
|[SetEnterLeaveFunctionHooks3 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3-method.md)|指定程式碼剖析工具實作函式會呼叫[FunctionEnter3](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md)， [FunctionLeave3](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md)，並[FunctionTailcall3](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md)函式。|  
|[SetEnterLeaveFunctionHooks3WithInfo 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)|指定程式碼剖析工具實作函式會呼叫[FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md)， [FunctionLeave3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md)，並[FunctionTailcall3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md)managed 函式的攔截程序。|  
|[SetFunctionIDMapper2 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setfunctionidmapper2-method.md)|指定將被呼叫來對應 `FunctionID` 值到替代值的程式碼剖析工具實作函式，這會被傳遞至分析工具函式進入/離開的攔截。 此方法擴充[icorprofilerinfo:: Setfunctionidmapper](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)以程式碼剖析工具可用來區分執行階段的參數。|  
  
## <a name="remarks"></a>備註  
 藉由使用無限制執行緒模型，CLR 會實作 `ICorProfilerInfo3` 介面的方法。 每個方法會傳回 HRESULT，表示成功或失敗。 如需可能的傳回程式碼清單，請參閱 CorError.h 檔案。  
  
 CLR 會傳遞`ICorProfilerInfo3`每個程式碼分析工具在初始化期間，使用分析工具的實作的介面[icorprofilercallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)或[ICorProfilerCallback3::InitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md)方法。 然後程式碼分析工具可以呼叫 `ICorProfilerInfo3` 方法，以取得在 CLR 控制下執行的 Managed 程式碼之資訊。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl, CorProf.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [分析介面](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [ICorProfilerInfo 介面](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
