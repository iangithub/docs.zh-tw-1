---
title: IEnumDefinitionIdentity 介面
ms.date: 03/30/2017
api_name:
- IEnumDefinitionIdentity
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IEnumDefinitionIdentity
helpviewer_keywords:
- IEnumDefinitionIdentity interface [.NET Framework fusion]
ms.assetid: 8263e75d-251b-4abc-8a1a-c62884142232
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4bbd8476b7778de6d0023f3a8522a44be6626884
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67751523"
---
# <a name="ienumdefinitionidentity-interface"></a>IEnumDefinitionIdentity 介面
做為集合的列舉值`IDefinitionIdentity`物件。  
  
## <a name="syntax"></a>語法  
  
```cpp  
IEnumDefinitionIdentity : IUnknown {  
  
    HRESULT Clone (  
        [out] IEnumDefinitionIdentity **ppIEnumDefinitionIdentity  
    );  
  
    HRESULT Next (  
        [in]  ULONG               celt,  
        [out, length_is(celt), size_is(*pceltWritten)]  
              IDefinitionIdentity *rgpIDefinitionIdentity[],  
        [out] ULONG               *pceltWritten  
    );  
  
    HRESULT Reset ();  
  
    HRESULT Skip (  
        [in] ULONG celt  
    );  
  
};  
```  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|`IEnumDefinitionIdentity::Clone`|取得新的介面指標`IEnumDefinitionIdentity`物件，其中包含與這個相同的成員`IEnumDefinitionIdentity`。|  
|`IEnumDefinitionIdentity::Next`|取得指定的數目`IDefinitionIdentity`物件，從目前位置開始。|  
|`IEnumDefinitionIdentity::Reset`|將指令指標移至這個開頭`IEnumDefinitionIdentity`。|  
|`IEnumDefinitionIdentity::Skip`|將指令指標向前移的指定項目數，從目前位置開始。|  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** Isolation.h  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [融合介面](../../../../docs/framework/unmanaged-api/fusion/fusion-interfaces.md)
- [IDefinitionIdentity 介面](../../../../docs/framework/unmanaged-api/fusion/idefinitionidentity-interface.md)
