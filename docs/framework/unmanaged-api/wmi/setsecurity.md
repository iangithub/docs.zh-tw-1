---
title: SetSecurity 函式 （Unmanaged API 參考）
description: SetSecurity 函式會擷取目前執行緒的模擬語彙基元。
ms.date: 11/06/2017
api_name:
- SetSecurity
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SetSecurity
helpviewer_keywords:
- SetSecurity function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a2cb71263201c86a93ca0bfbd783f2b8512055e6
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67783110"
---
# <a name="setsecurity-function"></a>SetSecurity 函式

擷取與目前執行緒關聯的模擬權杖。 

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>語法

```cpp
HRESULT SetSecurity (
   [out] boolean* pNeedToReset, 
   [out] HANDLE* pCurrentThreadToken
); 
```

## <a name="parameters"></a>參數

`pNeedToReset`\
[out]此函式傳回時，包含指標`boolean`，指出是否應藉由呼叫重設語彙基元[ResetSecurity](resetsecurity.md)函式。

`token`\
[out]此函式傳回時，包含目前執行緒相關聯的模擬語彙基元的控制代碼的指標。 其值可以是`null`是否與目前執行緒相關聯的語彙基元。 

## <a name="return-value"></a>傳回值

如果此函數成功，傳回的值是`S_OK`(0)。

如果函式失敗，傳回的值就會為非零的錯誤碼。 若要取得延伸錯誤資訊，請呼叫[GetErrorInfo](geterrorinfo.md)函式。

## <a name="requirements"></a>需求

 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。

 **標頭：** WMINet_Utils.idl

 **.NET framework 版本：** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>另請參閱

- [WMI 和效能計數器 （Unmanaged API 參考）](index.md)
