---
title: ExportNestedType 方法
ms.date: 03/30/2017
api_name:
- IALink.ExportNestedType
- ExportNestedType
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ExportNestedType
helpviewer_keywords:
- ExportNestedType method
ms.assetid: dec7df60-4d30-47c8-99db-72e0419e5f76
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 7dfaedad48291ac09f6959bc7b314ae0d9da76e5
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67742052"
---
# <a name="exportnestedtype-method"></a>ExportNestedType 方法
指定巢狀型別為可匯出。 [ExportType 方法](../../../../docs/framework/unmanaged-api/alink/exporttype-method.md)也可以匯出巢狀類型，但這個方法會比較快。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT ExportNestedType(  
    mdAssembly      AssemblyID,  
    mdToken         FileToken,  
    mdTypeDef       TypeToken,  
    mdExportedType  ParentType,  
    LPCWSTR         pszTypename,  
    DWORD           dwFlags,  
    mdExportedType* pType  
) PURE;   
```  
  
## <a name="parameters"></a>參數  
 `AssemblyID`  
 若要從匯出的組件識別碼。  
  
 `FileToken`  
 檔案的語彙基元或組件的檔案，定義成可匯出的型別。  
  
 `TypeToken`  
 可匯出型別的型別語彙基元。  
  
 `ParentType`  
 父型別的權杖。  
  
 `pszTypename`  
 若要匯出的完整型別名稱。  
  
 `dwFlags`  
 `ComType` 這類旗標`tdPublic`或`tdNested`。 這個值可能會傳遞至[DefineExportedType 方法](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-defineexportedtype-method.md)。  
  
 `pType`  
 接收匯出之類型的語彙基元。  
  
## <a name="return-value"></a>傳回值  
 如果方法成功，則會傳回 S_OK。  
  
## <a name="requirements"></a>需求  
 需要 alink.h  
  
## <a name="see-also"></a>另請參閱

- [IALink 介面](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [IALink2 介面](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)
- [ALink API](../../../../docs/framework/unmanaged-api/alink/index.md)
