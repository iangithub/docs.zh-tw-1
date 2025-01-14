---
ms.openlocfilehash: fca31a98c2dd3427501b3c6bfe4f52fcec086709
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858392"
---
### <a name="product-versioning-changes-in-the-net-framework-46-and-later-versions"></a>.NET Framework 4.6 和更新版本中的產品版本變更

|   |   |
|---|---|
|詳細資料|舊版 .NET Framework (特別是 .NET Framework 4、4.5、4.5.1 和 4.5.2) 的產品版本已變更。以下是詳細的變更：<ul><li><code>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full</code> 機碼中的 <code>Version</code> 項目值已變更為 <code>4.6.xxxxx</code> (.NET Framework 4.6 及其小數點發行版本)，以及 <code>4.7.xxxxx</code> (.NET Framework 4.7 和 4.7.1)。 在 .NET Framework 4.5、4.5.1 和 4.5.2 中，其格式為 <code>4.5.xxxxx</code>。</li><li>.NET Framework 檔案的檔案和產品版本已從舊版配置 4.0.30319.x 變更為 4.6.X.0 (.NET Framework 4.6 及其小數點發行版本)，以及 4.7.X.0 (.NET Framework 4.7 和 4.7.1)。 當您以滑鼠右鍵按一下檔案後再檢視檔案的屬性時，會看到這些新值。</li><li>受控組件的 <xref:System.Reflection.AssemblyFileVersionAttribute> 和 <xref:System.Reflection.AssemblyInformationalVersionAttribute> 屬性，對於 .NET Framework 4.6 及其小數點發行版本，其 Version 值的格式為 4.6.X.0，對於 .NET Framework 4.7 和 4.7.1，格式則為 4.7.X.0。</li><li>在 .NET Framework 4.6、4.6.1、4.6.2、4.7 和 4.7.1 中，<xref:System.Environment.Version?displayProperty=nameWithType> 屬性會傳回固定的版本字串 <code>4.0.30319.42000</code>。 在 .NET Framework 4、4.5、4.5.1 和 4.5.2 中，其會以 <code>4.0.30319.xxxxx</code> 格式傳回版本字串 (例如 &quot;4.0.30319.18010&quot;)。 請注意，建議應用程式程式碼與 Environment.Version 屬性有任何新的相依性。</li></ul>如需詳細資訊，請參閱[如何：判斷安裝的 .NET Framework 版本](~/docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)。|
|建議|一般而言，應用程式需要具備可偵測 .NET Framework 的執行階段版本和安裝目錄等項目的建議技術：<ul><li>若要偵測 .NET Framework 的執行階段版本，請參閱[如何：判斷安裝的 .NET Framework 版本](~/docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)。</li><li>若要判斷 .NET Framework 的安裝路徑，請使用 <code>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full</code> 機碼中的 <code>InstallPath</code> 項目值。</li></ul> <blockquote> [!IMPORTANT] 子機碼名稱是 <code>NET Framework Setup</code>，不是 <code>.NET Framework Setup</code>。</blockquote> <ul><li>若要判斷 .NET Framework Common Language Runtime 的目錄路徑，請呼叫 <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeDirectory?displayProperty=nameWithType> 方法。</li><li>若要取得 CLR 版本，請呼叫 <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion?displayProperty=nameWithType> 方法。 針對 .NET Framework 4 及其小數點發行版本 (.NET Framework 4.5、4.5.1、4.5.2 以及 .NET Framework 4.6、4.6.1、4.6.2、4.7 和 4.7.1)，該方法會傳回字串 v4.0.30319。</li></ul>|
|範圍|次要|
|版本|4.6|
|類型|執行階段|

