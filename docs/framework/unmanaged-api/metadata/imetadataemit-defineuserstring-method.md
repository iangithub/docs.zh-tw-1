---
title: IMetaDataEmit::DefineUserString 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineUserString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineUserString
helpviewer_keywords:
- DefineUserString method [.NET Framework metadata]
- IMetaDataEmit::DefineUserString method [.NET Framework metadata]
ms.assetid: 88fb7ef3-bbdf-429c-b678-c9c153456461
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 25e35fd9afd2ce4dc60e23ccd64e0630a008bf39
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777429"
---
# <a name="imetadataemitdefineuserstring-method"></a>IMetaDataEmit::DefineUserString 方法
取得指定的常值字串的中繼資料語彙基元。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT DefineUserString (   
    [in]  LPCWSTR     szString,   
    [in]  ULONG       cchString,   
    [out] mdString    *pstk   
);  
```  
  
## <a name="parameters"></a>參數  
 `szString`  
 [in]要儲存的使用者字串。  
  
 `cchString`  
 [in]中的寬字元的計數`szString`。  
  
 `pstk`  
 [out]指派的字串權杖。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** Cor.h  
  
 **LIBRARY:** 做為 MSCorEE.dll 中的資源  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [IMetaDataEmit 介面](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 介面](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
