---
title: _AxlPublicKeyBlobToPublicKeyToken 函式
ms.date: 03/30/2017
api_name:
- _AxlPublicKeyBlobToPublicKeyToken
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: 2d92a746-d68c-4f53-a16e-727f071a2d80
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3e2459b4f91e7e189990b65fa4d7ca860ff73c51
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67741322"
---
# <a name="axlpublickeyblobtopublickeytoken-function"></a>\_AxlPublicKeyBlobToPublicKeyToken 函式
從 CSP PUBLICKEYBLOB 格式運算強式名稱公開金鑰語彙基元。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT _AxlPublicKeyBlobToPublicKeyToken (  
    [in]  PCCERT_CHAIN_CONTEXT   pCspPublicKeyBlob,  
    [out] LPWSTR                 *ppwszPublicKeyToken  
);  
```  
  
## <a name="parameters"></a>參數  
 `pCspPublicKeyBlob`  
 [in] CSP 公開金鑰 Blob。  
  
 `ppwszPublicKeyHash`  
 [out] WCHAR * 的指標，可接收十六進位編碼公開金鑰雜湊。  
  
## <a name="return-value"></a>傳回值  
 如果函式成功，會傳回 `S_OK`，否則會傳回 `S_FALSE`。  
  
## <a name="see-also"></a>另請參閱

- [Authenticode](../../../../docs/framework/unmanaged-api/authenticode/index.md)
