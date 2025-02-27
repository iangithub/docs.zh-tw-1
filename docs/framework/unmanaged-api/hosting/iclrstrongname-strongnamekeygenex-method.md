---
title: ICLRStrongName::StrongNameKeyGenEx 方法
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameKeyGenEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameKeyGenEx
helpviewer_keywords:
- ICLRStrongName::StrongNameKeyGenEx method [.NET Framework hosting]
- StrongNameKeyGenEx method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 1f8b59d0-5b72-45b8-ab74-c2b43ffc806e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: acbf401ac2abb5ded151a48017a8a977cd0f4b71
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67747793"
---
# <a name="iclrstrongnamestrongnamekeygenex-method"></a>ICLRStrongName::StrongNameKeyGenEx 方法
會產生新公用/私密金鑰組以指定的金鑰大小，用於強式名稱。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT StrongNameKeyGenEx (  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  DWORD     dwFlags,  
    [in]  DWORD     dwKeySize,  
    [out] BYTE      **ppbKeyBlob,  
    [out] ULONG     *pcbKeyBlob  
);  
```  
  
## <a name="parameters"></a>參數  
 `wszKeyContainer`  
 [in]要求的金鑰容器名稱。 `wszKeyContainer` 必須是非空白字串或 null 來產生暫存名稱。  
  
 `dwFlags`  
 [in]值，指定是否要保留已註冊的金鑰。 支援下列值：  
  
- 0x00000000-時使用`wszKeyContainer`以產生暫時的金鑰容器名稱為 null。  
  
- 0x00000001 (`SN_LEAVE_KEY`)-指定應該向左註冊金鑰。  
  
 `dwKeySize`  
 [in]要求的大小，以位元的金鑰。  
  
 `ppbKeyBlob`  
 [out]傳回的 public/private 金鑰組。  
  
 `pcbKeyBlob`  
 [out]大小，以位元組為單位的`ppbKeyBlob`。  
  
## <a name="return-value"></a>傳回值  
 `S_OK` 如果這個方法順利完成否則，表示失敗的 HRESULT 值 (請參閱[常見的 HRESULT 值](https://go.microsoft.com/fwlink/?LinkId=213878)清單)。  
  
## <a name="remarks"></a>備註  
 .NET framework 1.0 和 1.1 版需要`dwKeySize`簽署組件以強式名稱; 1024 位元的 2.0 版新增 2048年位元金鑰的支援。  
  
 擷取索引鍵之後，您應該呼叫[iclrstrongname:: Strongnamefreebuffer](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamefreebuffer-method.md)方法來釋放配置的記憶體。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** MetaHost.h  
  
 **LIBRARY:** 包含做為 MSCorEE.dll 中的資源  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [StrongNameKeyGen 方法](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamekeygen-method.md)
- [ICLRStrongName 介面](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
