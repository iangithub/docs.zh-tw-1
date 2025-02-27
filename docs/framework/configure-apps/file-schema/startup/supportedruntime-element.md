---
title: <supportedRuntime> 組態項目-.NET
ms.date: 04/02/2019
ms.custom: updateeachrelease
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#supportedRuntime
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/supportedRuntime
helpviewer_keywords:
- supportedRuntime element
- <supportedRuntime> element
ms.assetid: 1ae16e23-afbe-4de4-b413-bc457f37b69f
ms.openlocfilehash: 90bdd5b8c5fdebe2c5d7ec580975dc63144b2401
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66489308"
---
# <a name="supportedruntime-element"></a>\<Supportedruntime> > 項目

指定哪個 common language runtime 版本，並選擇性地應用程式的.NET Framework 版本支援。  

[\<configuration>](../configuration-element.md)  
&nbsp;&nbsp;[\<startup>](../startup/startup-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp; **\<supportedRuntime>**  

## <a name="syntax"></a>語法

```xml
<supportedRuntime version="runtime version" sku="sku id"/>
```

## <a name="attributes"></a>屬性

|屬性|描述|
|---------------|-----------------|
|**version**|選擇性屬性。<br /><br /> 字串值，用於指定這個應用程式支援的通用語言執行平台 (CLR) 版本。 有效值`version`屬性，請參閱[「 執行階段版本 」 值](#version)一節。 **注意：** 透過.NET Framework 3.5 中，「*執行階段版本*"值的形式*主要*。*次要*。*建置*。 從.NET Framework 4 中，只需要主要和次要版本號碼 (也就是"v4.0"而不是"v4.0.30319")。 建議使用較短的字串。|
|**sku**|選擇性屬性。<br /><br /> 字串值，指定庫存單位 (SKU)，進而指定哪些應用程式支援的.NET Framework 版本。<br /><br /> 從 .NET Framework 4.0 開始，建議使用 `sku` 屬性。  該屬性存在時，會指出應用程式作為目標的 .NET Framework 版本。<br /><br /> 如需 sku 屬性的有效值，請參閱[「 sku 識別碼 」 值](#sku)一節。|

## <a name="remarks"></a>備註

如果 **\<Supportedruntime> >** 項目不存在於應用程式組態檔，會使用用來建置應用程式的執行階段版本。

**\<Supportedruntime>** 項目應由使用 1.1 版或更新版本的執行階段所建置的所有應用程式。 若要只支援 1.0 版的執行階段所建置的應用程式必須使用[ \<Requiredruntime> >](../startup/requiredruntime-element.md)項目。

> [!NOTE]
> 如果您使用[CorBindToRuntimeByCfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md)函數來指定組態檔，您必須使用`<requiredRuntime>`的執行階段的所有版本的項目。 `<supportedRuntime>`當您使用時，便會忽略元素[CorBindToRuntimeByCfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md)。  
  
針對所支援執行階段為 .NET Framework 1.1 到 3.5 版本的應用程式，當支援多個執行階段版本時，第一個項目應該指定最常用的執行階段版本，而最後一個項目則指定最少用的版本。 針對支援的.NET Framework 4.0 或更新版本中，應用程式`version`屬性會指出 CLR 版本，也就是一般.NET Framework 4 和更新版本，而`sku`屬性表示的單一.NET Framework 版本，應用程式的目標。 

如果 **\<Supportedruntime> >** 項目`sku`屬性已出現在組態檔，並已安裝的.NET Framework 版本是較低，則指定的支援的版本，應用程式無法執行，而是會顯示訊息，要求您安裝支援的版本。 否則應用程式會嘗試在任何已安裝的版本上執行，但它可能會出現非預期行為如果不是與該版本完全相容。 (如需.NET Framework 版本之間的相容性差異，請參閱[.NET Framework 中的應用程式相容性](https://docs.microsoft.com/dotnet/framework/migration-guide/application-compatibility)。)因此，我們建議您更輕鬆的錯誤診斷的應用程式組態檔中包含這個項目。 （已建立新專案時，自動產生 Visual studio 的組態檔包含它）。
  
> [!NOTE]
> 如果您的應用程式使用舊版啟用路徑，例如[CorBindToRuntimeEx 函式](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)，和您想要這些路徑來啟動第 4 版的 clr，而不是較早的版本，或如果您的應用程式以.NET Framework 建置4 但具有相依性以舊版.NET Framework 建置的混合模式組件，它並不足以支援的執行階段清單中指定.NET Framework 4。 此外，在[\<啟動 > 項目](../startup/startup-element.md)在您的組態檔，您必須設定`useLegacyV2RuntimeActivationPolicy`屬性設定為`true`。 不過，將此屬性設定為`true`而建置的執行階段不使用.NET Framework 4 執行使用舊版.NET Framework 所建置的所有元件的方法。

建議您使用應用程式能夠執行的所有 .NET Framework 版本進行應用程式測試。

<a name="version"></a> 
## <a name="runtime-version-values"></a>「執行階段版本」值
`runtime`屬性會指定給定的應用程式需要的 Common Language Runtime (CLR) 版本。 請注意，所有的.NET Framework v4.x 版本指定`v4.0`CLR。 下表列出的有效值*執行階段版本*的值`version`屬性。

|.NET Framework 版本|`version` 屬性|
|----------------------------|-------------------------|
|1.0|"v1.0.3705"|
|1.1|"v1.1.4322"|
|2.0|"v2.0.50727"|
|3.0|"v2.0.50727"|
|3.5|"v2.0.50727"|
|4.0-4.8|"v4.0"|

## <a name="sku"></a> 「 sku 識別碼 」 值

`sku`屬性會使用目標 framework moniker (TFM)，以指出應用程式為目標，且要求要執行的.NET framework 版本。 下表列出支援的有效值`sku`屬性，從.NET Framework 4 開始。

|.NET Framework 版本|`sku` 屬性|
|----------------------------|---------------------|
|4.0|".NETFramework,Version=v4.0"|
|4.0，Client Profile|".NETFramework,Version=v4.0,Profile=Client"|
|4.0，平台更新 1|".NETFramework,Version=v4.0.1"|
|4.0，Client Profile，更新 1|".NETFramework,Version=v4.0.1,Profile=Client"|
|4.0，平台更新 2|".NETFramework,Version=v4.0.2"|
|4.0，Client Profile，更新 2|".NETFramework,Version=v4.0.2,Profile=Client"|
|4.0，平台更新 3|".NETFramework,Version=v4.0.3"|
|4.0，Client Profile，更新 3|".NETFramework,Version=v4.0.3,Profile=Client"|
|4.5|".NETFramework,Version=v4.5"|
|4.5.1|".NETFramework,Version=v4.5.1"|
|4.5.2|".NETFramework,Version=v4.5.2"|
|4.6|".NETFramework,Version=v4.6"|
|4.6.1|".NETFramework,Version=v4.6.1"|
|4.6.2|".NETFramework,Version=v4.6.2"|
|4.7|".NETFramework,Version=v4.7"|
|4.7.1|".NETFramework,Version=v4.7.1"|
|4.7.2|".NETFramework，版本 = v4.7.2"|
|4.8|".NETFramework,Version=v4.8"|

## <a name="example"></a>範例

下列範例將示範如何在設定檔中指定支援的執行階段版本。 組態檔會指出應用程式的目標.NET Framework 4.7。

```xml
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7" />
   </startup>
</configuration>
```

## <a name="configuration-file"></a>組態檔

這個項目可以在應用程式組態檔中使用。

## <a name="see-also"></a>另請參閱

- [啟動設定結構描述](../startup/index.md)
- [組態檔結構描述](../index.md)
- [同處理序並存執行](../../../deployment/in-process-side-by-side-execution.md)
