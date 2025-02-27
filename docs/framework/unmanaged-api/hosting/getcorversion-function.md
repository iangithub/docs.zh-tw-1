---
title: GetCORVersion 函式
ms.date: 03/30/2017
api_name:
- GetCORVersion
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetCORVersion
helpviewer_keywords:
- GetCORVersion function [.NET Framework hosting]
ms.assetid: 2f09cd37-bf3a-4cc5-87b0-adc42a7eed31
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fe5525fc29bc01bb84f7f2997d115eec12d72b13
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67736281"
---
# <a name="getcorversion-function"></a>GetCORVersion 函式
傳回 common language runtime (CLR) 在目前的處理序中執行的版本號碼。  
  
 此函式已被取代，在.NET Framework 4。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetCORVersion (  
    [in] LPWSTR  pbuffer,  
    [in]  DWORD   cchBuffer,   
    [out] DWORD*  dwlength  
);   
```  
  
## <a name="parameters"></a>參數  
 `pbuffer`  
 CLR 會傳回字串，指定目前已載入到處理序的執行階段版本的緩衝區指標。 傳回的字串會採用相同的格式字串傳遞至[CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)，例如"v1.0.1216 」。 如果執行階段尚未載入到處理序，則函數會傳回最新版本的執行階段電腦上安裝適當的目錄資訊。  
  
 `cchBuffer`  
 字元數 (`WCHAR`s)，可以保留在`pbuffer`。  
  
 `dwLength`  
 中實際傳回的字元數的指標`pbuffer`。 如果`pbuffer`為 null 指標，執行階段傳回 E_POINTER。 如果字元數大於的長度`pbuffer`，執行階段會傳回 ERROR_INSUFFICIENT_BUFFER。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** MSCorEE.h  
  
 **LIBRARY:** MSCorEE.dll  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [已被取代的 CLR 裝載函式](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
