---
title: ICorProfilerInfo::GetObjectSize 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetObjectSize
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetObjectSize
helpviewer_keywords:
- GetObjectSize method [.NET Framework profiling]
- ICorProfilerInfo::GetObjectSize method [.NET Framework profiling]
ms.assetid: 9f02e763-73f7-42cb-a41c-f78499d9482c
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: cd337ca6d7b03ad22f178c9c7084cfa2585da73c
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782755"
---
# <a name="icorprofilerinfogetobjectsize-method"></a>ICorProfilerInfo::GetObjectSize 方法
取得指定之物件的大小。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetObjectSize(  
    [in]  ObjectID objectId,  
    [out] ULONG  *pcSize);  
```  
  
## <a name="parameters"></a>參數  
 `objectId`  
 [in]物件的識別碼。  
  
 `pcSize`  
 [out]物件的大小，以位元組為單位的指標。  
  
## <a name="remarks"></a>備註  
  
> [!IMPORTANT]
>  這個方法已過時。 它會傳回 COR_E_OVERFLOW 物件大於 4 GB 64 位元平台上。 使用[ICorProfilerInfo4::GetObjectSize2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getobjectsize2-method.md)方法改為。  
  
 不同的物件相同的類型通常會有相同的大小。 不過，某些類型，例如陣列或字串，可能會有不同的大小，為每個物件。  
  
 所傳回的大小`GetObjectSize`方法不包含在記憶體回收堆積上物件之後，可能會出現任何對齊填補。 如果您使用`GetObjectSize`方法前進 object 物件在記憶體回收堆積，新增以手動方式，視需要填補的對齊方式。  
  
- 在 32 位元 Windows COR_PRF_GC_GEN_0、 COR_PRF_GC_GEN_1 和 COR_PRF_GC_GEN_2 使用 4 位元組對齊，而 COR_PRF_GC_LARGE_OBJECT_HEAP 會使用 8 位元組對齊。  
  
- 在 64 位元 Windows 上的對齊方式一定是 8 個位元組。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl, CorProf.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerInfo 介面](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
