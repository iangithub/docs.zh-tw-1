---
title: ICLRStrongName::StrongNameSignatureVerificationFromImage 方法
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureVerificationFromImage
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureVerificationFromImage
helpviewer_keywords:
- ICLRStrongName::StrongNameSignatureVerificationFromImage method [.NET Framework hosting]
- StrongNameSignatureVerificationFromImage method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: da91c138-ee30-4fd4-a040-464d97d7e41a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 21aeceff72ea6222992cb6f3d055ed6f71cda9bf
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67759250"
---
# <a name="iclrstrongnamestrongnamesignatureverificationfromimage-method"></a>ICLRStrongName::StrongNameSignatureVerificationFromImage 方法
驗證已對應到記憶體的組件對關聯的公開金鑰而言有效。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT StrongNameSignatureVerificationFromImage (  
    [in]  BYTE    *pbBase,  
    [in]  DWORD   dwLength,  
    [in]  DWORD   dwInFlags,  
    [out] DWORD   *pdwOutFlags  
);  
```  
  
## <a name="parameters"></a>參數  
 `pbBase`  
 [in]對應的組件資訊清單的相對虛擬位址。  
  
 `dwLength`  
 [in]以位元組為單位，對應的映像的大小。  
  
 `dwInFlags`  
 [in]影響驗證行為的旗標。 支援下列值：  
  
- `SN_INFLAG_FORCE_VER` (0x00000001)-強制執行驗證，即使它是需要覆寫登錄設定。  
  
- `SN_INFLAG_INSTALL` (0x00000002)-指定此映像上執行的第一次驗證。  
  
- `SN_INFLAG_ADMIN_ACCESS` (0x00000004)-指定快取可讓具有系統管理權限的使用者存取。  
  
- `SN_INFLAG_USER_ACCESS` (0x00000008)-指定的組件都是僅供目前的使用者存取。  
  
- `SN_INFLAG_ALL_ACCESS` (0x00000010)-指定快取會提供任何保證的存取限制。  
  
- `SN_INFLAG_RUNTIME` (0x80000000)-保留給內部偵錯。  
  
 `pdwOutFlags`  
 [out]其他輸出資訊之旗標。 支援下列值：  
  
- `SN_OUTFLAG_WAS_VERIFIED` (0x00000001)-此值設為`false`，指定驗證成功，因為登錄設定。  
  
## <a name="return-value"></a>傳回值  
 `S_OK` 如果這個方法順利完成否則，表示失敗的 HRESULT 值 (請參閱[常見的 HRESULT 值](https://go.microsoft.com/fwlink/?LinkId=213878)清單)。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** MetaHost.h  
  
 **LIBRARY:** 包含做為 MSCorEE.dll 中的資源  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICLRStrongName 介面](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
