---
title: StrongNameErrorInfo 函式
ms.date: 03/30/2017
api_name:
- StrongNameErrorInfo
api_location:
- mscoree.dll
- mscorsn.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameErrorInfo
helpviewer_keywords:
- StrongNameErrorInfo function [.NET Framework strong naming]
ms.assetid: e91bf8c3-7c26-4732-938e-2e5b04abfc99
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a6f495500b087b9e24936acd414f1aff463d7f64
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781066"
---
# <a name="strongnameerrorinfo-function"></a>StrongNameErrorInfo 函式
取得由其中一強式名稱函式所引發的最後一個錯誤代碼。  
  
 此函式已被取代。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT StrongNameErrorInfo ();   
```  
  
## <a name="return-value"></a>傳回值  
 最後一個設定 COM 錯誤碼的其中一個強式名稱的函式。  
  
## <a name="remarks"></a>備註  
 大部分的強式名稱的方法會傳回簡單`true`或`false`成功完成的指示。 使用`StrongNameErrorInfo`函式來擷取指定強式名稱的函式所產生的最後一個錯誤的 HRESULT。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** StrongName.h  
  
 **LIBRARY:** 包含做為 MsCorEE.dll 中的資源  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
