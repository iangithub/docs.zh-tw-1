---
title: IAssemblyCache::UninstallAssembly 方法
ms.date: 03/30/2017
api_name:
- IAssemblyCache.UninstallAssembly
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyCache::UninstallAssembly
helpviewer_keywords:
- UninstallAssembly method [.NET Framework fusion]
- IAssemblyCache::UninstallAssembly method [.NET Framework fusion]
ms.assetid: 973b2c44-8dfc-40c1-9035-10f4846627e9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 531f9167a931d6b972e47e120950197bed11c07e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67778712"
---
# <a name="iassemblycacheuninstallassembly-method"></a>IAssemblyCache::UninstallAssembly 方法
從全域組件快取，解除安裝指定的組件。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT UninstallAssembly (  
    [in] DWORD dwFlags,  
    [in] LPCWSTR pszAssemblyName,  
    [in] LPCFUSION_INSTALL_REFERENCE pRefData,  
    [out, optional] ULONG *pulDisposition  
);  
```  
  
## <a name="parameters"></a>參數  
 `dwFlags`  
 [in]支援下列值： 旗標。  
  
 `pszAssemblyName`  
 [in]若要解除安裝組件的名稱。  
  
 `pRefData`  
 [in]A [FUSION_INSTALL_REFERENCE](../../../../docs/framework/unmanaged-api/fusion/fusion-install-reference-structure.md)包含組件之安裝資料的結構。  
  
 `pulDisposition`  
 [out，optional]其中包括下列： 配置值。 可能的值包括下列各項：  
  
- IASSEMBLYCACHE_UNINSTALL_DISPOSITION_UNINSTALLED (1)  
  
- IASSEMBLYCACHE_UNINSTALL_DISPOSITION_STILL_IN_USE (2)  
  
- IASSEMBLYCACHE_UNINSTALL_DISPOSITION_ALREADY_UNINSTALLED (3)  
  
- IASSEMBLYCACHE_UNINSTALL_DISPOSITION_DELETE_PENDING (4)  
  
- IASSEMBLYCACHE_UNINSTALL_DISPOSITION_HAS_INSTALL_REFERENCES (5)  
  
- IASSEMBLYCACHE_UNINSTALL_DISPOSITION_REFERENCE_NOT_FOUND (6)  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** Fusion.h  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [IAssemblyCache 介面](../../../../docs/framework/unmanaged-api/fusion/iassemblycache-interface.md)
