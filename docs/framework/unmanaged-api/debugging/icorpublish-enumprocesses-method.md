---
title: ICorPublish::EnumProcesses 方法
ms.date: 03/30/2017
api_name:
- ICorPublish.EnumProcesses
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublish::EnumProcesses
helpviewer_keywords:
- ICorPublish::EnumProcesses method [.NET Framework debugging]
- EnumProcesses method [.NET Framework debugging]
ms.assetid: 4ae765f0-93b2-4b6f-aea1-7b0cf44e04a7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1804a14c1197148afbffb5ec2cb4f29cb9ff019e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67774563"
---
# <a name="icorpublishenumprocesses-method"></a>ICorPublish::EnumProcesses 方法
取得此電腦上執行的受管理處理程序中的列舉值。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT EnumProcesses (  
    [in] COR_PUB_ENUMPROCESS       Type,  
    [out] ICorPublishProcessEnum   **ppIEnum  
);  
```  
  
## <a name="parameters"></a>參數  
 `Type`  
 值為[COR_PUB_ENUMPROCESS](../../../../docs/framework/unmanaged-api/debugging/cor-pub-enumprocess-enumeration.md)列舉，指定要擷取的程序的類型。 在目前的版本中，只有 COR_PUB_MANAGEDONLY 是有效的。  
  
 `ppIEnum`  
 位址指標[ICorPublishProcessEnum](../../../../docs/framework/unmanaged-api/debugging/icorpublishprocessenum-interface.md)是列舉值的處理程序的執行個體。  
  
## <a name="remarks"></a>備註  
 處理序的列舉值的集合為基礎之處理序正在執行時的快照集`EnumProcesses`呼叫方法。 列舉值將不會包含任何處理序終止之前或之後啟動`EnumProcesses`呼叫。  
  
 `EnumProcesses`可能會超過一次呼叫方法，這[ICorPublish](../../../../docs/framework/unmanaged-api/debugging/icorpublish-interface.md)建立新的最新集合的程序的執行個體。 現有的集合將不會受到的後續呼叫`EnumProcesses`方法。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorPub.idl CorPub.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorPublish 介面](../../../../docs/framework/unmanaged-api/debugging/icorpublish-interface.md)
