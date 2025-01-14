---
title: CorDebugMappingResult 列舉
ms.date: 03/30/2017
api_name:
- CorDebugMappingResult
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugMappingResult
helpviewer_keywords:
- CorDebugMappingResult enumeration [.NET Framework debugging]
ms.assetid: 701281dd-2936-45c8-a1f0-3bf7332b093b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c2042d0936359a85d203375c42be0d8a096f004e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739757"
---
# <a name="cordebugmappingresult-enumeration"></a>CorDebugMappingResult 列舉
提供如何取得指令指標 (IP) 值的詳細資料。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef enum CorDebugMappingResult {  
    MAPPING_PROLOG              = 0x1,  
    MAPPING_EPILOG              = 0x2,  
    MAPPING_NO_INFO             = 0x4,  
    MAPPING_UNMAPPED_ADDRESS    = 0x8,  
    MAPPING_EXACT               = 0x10,  
    MAPPING_APPROXIMATE         = 0x20,  
} CorDebugMappingResult;  
```  
  
## <a name="members"></a>成員  
  
|成員|描述|  
|------------|-----------------|  
|`MAPPING_PROLOG`|原生程式碼是在初構中，因此 IP 值為 0。|  
|`MAPPING_EPILOG`|原生程式碼是終解中，因此 IP 值是方法的最後一個指令的位址。|  
|`MAPPING_NO_INFO`|對應不未提供任何資訊的方法，因此 IP 值為 0。|  
|`MAPPING_UNMAPPED_ADDRESS`|雖然此方法的對應資訊，但目前的地址無法對應到 Microsoft intermediate language (MSIL) 程式碼。 IP 的值為 0。|  
|`MAPPING_EXACT`|方法會對應至 MSIL 程式碼完全或框架已解譯，因此 IP 值正確無誤。|  
|`MAPPING_APPROXIMATE`|已成功對應方法，但 IP 值可能只是近似。|  
  
## <a name="remarks"></a>備註  
 您可以使用[icordebugilframe:: Getip](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe-getip-method.md)方法，以取得指令指標的值。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [偵錯列舉](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
