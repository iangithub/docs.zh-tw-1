---
title: IMetaDataImport::GetMemberRefProps 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMemberRefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMemberRefProps
helpviewer_keywords:
- GetMemberRefProps method [.NET Framework metadata]
- IMetaDataImport::GetMemberRefProps method [.NET Framework metadata]
ms.assetid: 0ea73055-ece0-4151-a094-414c88ef8941
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fadc54d74ce6027bd021e148a14cb0c432eb41fe
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782349"
---
# <a name="imetadataimportgetmemberrefprops-method"></a>IMetaDataImport::GetMemberRefProps 方法
取得與指定語彙基元所參考成員相關聯的中繼資料。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetMemberRefProps (  
   [in]  mdMemberRef       mr,   
   [out] mdToken           *ptk,   
   [out] LPWSTR            szMember,   
   [in]  ULONG             cchMember,   
   [out] ULONG             *pchMember,   
   [out] PCCOR_SIGNATURE   *ppvSigBlob,   
   [out] ULONG             *pbSig   
);  
```  
  
## <a name="parameters"></a>參數  
 `mr`  
 [in]若要傳回相關聯的中繼資料的 MemberRef 語彙基元。  
  
 `ptk`  
 [out]TypeDef TypeRef 或 TypeSpec 語彙基元，代表宣告的成員或 ModuleRef 語彙基元，代表宣告的成員或代表該成員 MethodDef 的模組類別的類別。  
  
 `szMember`  
 [out]針對成員名稱的字串緩衝區。  
  
 `cchMember`  
 [in]所要求的大小，以寬字元為單位的`szMember`。  
  
 `pchMember`  
 [out]寬字元在傳回的大小`szMember`。  
  
 `ppvSibBlob`  
 [out]指標，該成員的二進位中繼資料簽章。  
  
 `pbSig`  
 [out]以位元組為單位的大小`ppvSigBlob`。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** Cor.h  
  
 **LIBRARY:** 包含做為 MsCorEE.dll 中的資源  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [IMetaDataImport 介面](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 介面](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
