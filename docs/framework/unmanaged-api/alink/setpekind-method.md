---
title: SetPEKind 方法
ms.date: 03/30/2017
api_name:
- IALink2.SetPEKind
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- SetPEKind
helpviewer_keywords:
- SetPEKind method
ms.assetid: 050e77ee-3014-45c0-9e29-2ebe29347b0d
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8fc581904351443f4368a68a653fd39b3548999a
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67741424"
---
# <a name="setpekind-method"></a>SetPEKind 方法
決定可攜式執行檔的類型，特定電腦或機器無關。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT SetPEKind(  
    mdAssembly AssemblyID,  
    mdToken FileToken,  
    DWORD dwPEKind,  
    DWORD dwMachine  
) PURE;   
```  
  
## <a name="parameters"></a>參數  
 `AssemblyID`  
 組件的識別碼。  
  
 `FileToken`  
 PE 型別為其設定的檔的語彙基元。 可以是 NULL，如果`AssemblyID`不會指出未繫結的 netmodule。  
  
 `dwPEKind`  
 PE 所指定的型別[CorPEKind 列舉](../../../../docs/framework/unmanaged-api/metadata/corpekind-enumeration.md)。  
  
 `dwMachine`  
 目標電腦架構，NT 標頭中所示。  
  
## <a name="return-value"></a>傳回值  
 如果方法成功，則會傳回 S_OK。  
  
## <a name="requirements"></a>需求  
 需要 alink.h。  
  
## <a name="see-also"></a>另請參閱

- [GetPEKind 方法](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getpekind-method.md)
- [IALink2 介面](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)
- [IALink 介面](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [ALink API](../../../../docs/framework/unmanaged-api/alink/index.md)
