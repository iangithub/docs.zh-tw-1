---
title: AssemblyOptions 列舉
ms.date: 03/30/2017
api_name:
- AssemblyOptions
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- AssemblyOptions
helpviewer_keywords:
- Alink API, AssemblyOptions enumeration
- AssemblyOptions enumeration
ms.assetid: 84f83921-64cb-49e3-ac8b-22a0b77b18a8
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 324e30f6cbcaa1d1d81c7c03967dbb629d2cd6e9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67742274"
---
# <a name="assemblyoptions-enumeration"></a>AssemblyOptions 列舉
列舉組件的選項。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef enum _AssemblyOptions {  
    optAssemTitle = 0,  
    optAssemDescription,  
    optAssemConfig,  
    optAssemOS,  
    optAssemProcessor,  
    optAssemLocale,  
    optAssemVersion,  
    optAssemCompany,  
    optAssemProduct,  
    optAssemProductVersion,  
    optAssemCopyright,  
    optAssemTrademark,  
    optAssemKeyFile,  
    optAssemKeyName,  
    optAssemAlgID,  
    optAssemFlags,  
    optAssemHalfSign,  
    optAssemFileVersion,  
    optAssemSatelliteVer,  
    optLastAssemOption  
}   AssemblyOptions;  
```  
  
## <a name="fields"></a>欄位  
  
|欄位|說明|  
|-----------|-----------------|  
|optAssemTitle|字串-表示組件標題。|  
|optAssemDescription|字串-包含組件描述。|  
|optAssemConfig|字串-包含組件組態。|  
|optAssemOS|字串-編碼為:"dwOSPlatformId.dwOSMajorVersion.dwOSMinorVersion 」。|  
|optAssemProcessor|ULONG|  
|optAssemLocale|字串-包含組件的地區設定。|  
|optAssemVersion|字串-編碼為：「 Major.Minor.Build.Revision。 」|  
|optAssemCompany|字串-包含公司。|  
|optAssemProduct|字串-包含產品名稱。|  
|optAssemProductVersion|字串 (也稱為 InformationalVersion)。|  
|optAssemCopyright|字串-包含著作權資訊。|  
|optAssemTrademark|字串-包含商標資訊。|  
|optAssemKeyFile|字串 （檔案名稱）。|  
|optAssemKeyName|字串 （索引鍵名稱）。|  
|optAssemAlgID|ULONG|  
|optAssemFlags|ULONG|  
|optAssemHalfSign|Bool （也稱為 DelaySign）。|  
|optAssemFileVersion|字串-編碼為 「 Major.Minor.Build.Revision"-ProductVersion 相同。|  
|optAssemSatelliteVer|字串-編碼為"Major.Minor.Build.Revision 」。|  
|optLastAssemOption|元素數目的計數器。|  
  
## <a name="requirements"></a>需求  
 **標頭：** alink.h  
  
 **程式庫**: alink.dll  
  
## <a name="see-also"></a>另請參閱

- [Al.exe (組件連結器)](../../../../docs/framework/tools/al-exe-assembly-linker.md)
