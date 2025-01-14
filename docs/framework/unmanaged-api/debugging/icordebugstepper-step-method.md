---
title: ICorDebugStepper::Step 方法
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.Step
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::Step
helpviewer_keywords:
- Step method, ICorDebugStepper interface [.NET Framework debugging]
- ICorDebugStepper::Step method [.NET Framework debugging]
ms.assetid: 38c1940b-ada1-40ba-8295-4c0833744e1e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9d0f601c4b454b55edc5fa25eb2ee33d491009b9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67760576"
---
# <a name="icordebugstepperstep-method"></a>ICorDebugStepper::Step 方法
導致此 ICorDebugStepper 單一步驟及其包含的執行緒，以及 （選擇性） 若要繼續單一位逐步執行會在執行緒內呼叫的函式。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT Step (  
    [in] BOOL   bStepIn  
);  
```  
  
## <a name="parameters"></a>參數  
 `bStepIn`  
 [in]若要設定`true`逐步執行至呼叫執行緒內的函式。 若要設定`false`進入函式。  
  
## <a name="remarks"></a>備註  
 Common language runtime 在這個步進框架中執行下一個 managed 的指令時，就會完成的步驟。 如果`Step`是步進上呼叫，這不是在 managed 程式碼、 執行緒所執行的下一個 managed 程式碼指令時，步驟就會完成。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **LIBRARY:** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
