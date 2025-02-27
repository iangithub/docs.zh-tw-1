---
title: ICorProfilerInfo::GetModuleMetaData 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetModuleMetaData
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetModuleMetaData
helpviewer_keywords:
- GetModuleMetaData method [.NET Framework profiling]
- ICorProfilerInfo::GetModuleMetaData method [.NET Framework profiling]
ms.assetid: 7a439d92-348a-44dd-b60f-cad7cba56379
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2e63cf698e41e70084c9b71bdf58d7ac60723d53
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782783"
---
# <a name="icorprofilerinfogetmodulemetadata-method"></a>ICorProfilerInfo::GetModuleMetaData 方法
取得對應至指定的模組的中繼資料介面執行個體。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetModuleMetaData(  
    [in]  ModuleID moduleId,  
    [in]  DWORD    dwOpenFlags,  
    [in]  REFIID   riid,  
    [out] IUnknown **ppOut);  
```  
  
## <a name="parameters"></a>參數  
 `moduleId`  
 [in]對應介面執行個體之模組識別碼。  
  
 `dwOpenFlags`  
 [in]值為[CorOpenFlags](../../../../docs/framework/unmanaged-api/metadata/coropenflags-enumeration.md)列舉，指定開啟資訊清單檔案的模式。 只有`ofRead`，`ofWrite`和`ofNoTransform`個位元都是有效。  
  
 `riid`  
 [in]參考識別碼 (GUID) 會擷取其執行個體的中繼資料介面。 請參閱[中繼資料介面](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)介面的清單。  
  
 `ppOut`  
 [out]中繼資料介面執行個體的位址指標。  
  
## <a name="remarks"></a>備註  
 您可能會要求在讀取/寫入模式中開啟的中繼資料，但這會導致較慢的中繼資料執行的程式，從編譯器所顯示的一樣，因為變更無法最佳化中繼資料。  
  
 一些模組 （例如資源模組） 會有任何中繼資料。 在這些情況下，`GetModuleMetaData`會傳回 S_FALSE 和在 null 值的 HRESULT 值 *`ppOut`。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl, CorProf.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerInfo 介面](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
