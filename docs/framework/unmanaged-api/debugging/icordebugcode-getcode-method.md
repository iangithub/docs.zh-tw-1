---
title: ICorDebugCode::GetCode 方法
ms.date: 03/30/2017
api_name:
- ICorDebugCode.GetCode
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::GetCode
helpviewer_keywords:
- ICorDebugCode::GetCode method [.NET Framework debugging]
- GetCode method, ICorDebugCode interface [.NET Framework debugging]
ms.assetid: 7137e3d1-1dad-48d8-8c37-16ac816534d3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e18097dd380ee354e5652886544d40da074f1230
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67747619"
---
# <a name="icordebugcodegetcode-method"></a>ICorDebugCode::GetCode 方法
取得指定的函式，針對 反組譯碼格式化的所有程式碼。 這個方法已被取代，在.NET Framework 2.0 版。 使用[ICorDebugCode2::GetCodeChunks](../../../../docs/framework/unmanaged-api/debugging/icordebugcode2-getcodechunks-method.md)改。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetCode (  
    [in] ULONG32     startOffset,   
    [in] ULONG32     endOffset,  
    [in] ULONG32     cBufferAlloc,  
    [out, size_is(cBufferAlloc),  
        length_is(*pcBufferSize)] BYTE buffer[],  
    [out] ULONG32    *pcBufferSize  
);  
```  
  
## <a name="parameters"></a>參數  
 `startOffset`  
 [in]函式開頭位移。  
  
 `endOffset`  
 [in]函式結尾的位移。  
  
 `cBufferAlloc`  
 [in]大小`buffer`到程式碼會傳回陣列。  
  
 `buffer`  
 [out]陣列，將在其中傳回的程式碼。  
  
 `pcBufferSize`  
 [out]傳回的位元組數。  
  
## <a name="remarks"></a>備註  
 如果函式的程式碼，而且已經分割成多個區塊，串連這些區塊是以遞增的原生位移的順序。 不會檢查指令界限。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** 1.1, 1.0  
  
## <a name="see-also"></a>另請參閱

- [GetCodeChunks 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugcode2-getcodechunks-method.md)
