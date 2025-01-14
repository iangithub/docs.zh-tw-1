---
title: <shadowCopyVerifyByTimestamp> 項目
ms.date: 03/30/2017
helpviewer_keywords:
- <shadowCopyTimeStampVerification> element
- shadowCopyTimeStampVerification element
ms.assetid: 2f1648e5-997b-435e-a4f9-d236c574c66c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4187d266d82783ebb72073c1da92faff95352884
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66489387"
---
# <a name="shadowcopyverifybytimestamp-element"></a>\<shadowCopyVerifyByTimestamp> 項目
指定陰影複製是否使用.NET Framework 4 中導入的預設啟動行為，或會還原為舊版.NET Framework 的啟動行為。  
  
 \<組態 > 項目  
\<執行階段 > 項目  
\<shadowCopyVerifyByTimestamp> 項目  
  
## <a name="syntax"></a>語法  
  
```xml  
<shadowCopyVerifyByTimestamp enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列各節描述屬性、子項目和父項目。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|enabled|必要屬性。<br /><br /> 指定是否使用陰影複製的應用程式定義域時啟動，以判斷是否已更新組件陰影複製組件之前比較的組件時間戳記。|  
  
## <a name="enabled-attribute"></a>啟用屬性  
  
|值|描述|  
|-----------|-----------------|  
|true|在啟動時，複製 只有已更新，因此在上一次複製到陰影複製目錄的組件。 這是.NET Framework 4 的預設值。|  
|False|還原為舊版.NET Framework 的啟動行為是將在啟動的所有檔案都複製。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|`configuration`|通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。|  
|`runtime`|包含有關組件繫結和記憶體回收的資訊。|  
  
## <a name="remarks"></a>備註  
 從.NET Framework 4 開始，組件會陰影複製，只有當其時間戳記表示自上次在複製到陰影複製目錄後有所變更。 這可改善許多使用陰影複製，應用程式的啟動時間，如中所述[陰影複製組件](../../../../../docs/framework/app-domains/shadow-copy-assemblies.md)。 組件更新比例與頻率相當高的應用程式可能不會受益於這種行為變更。 在這種情況下，您可以使用此項目還原舊版 .NET Framework 的行為。  
  
## <a name="example"></a>範例  
 下列範例示範如何停用預設啟動行為的陰影複製在.NET Framework 4 中，並還原為舊版.NET Framework 的啟動行為。  
  
```xml  
<configuration>  
   <runtime>  
      <shadowCopyVerifyByTimestamp enabled="false" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱

- [執行階段設定結構描述](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [組態檔結構描述](../../../../../docs/framework/configure-apps/file-schema/index.md)
- [陰影複製組件](../../../../../docs/framework/app-domains/shadow-copy-assemblies.md)
