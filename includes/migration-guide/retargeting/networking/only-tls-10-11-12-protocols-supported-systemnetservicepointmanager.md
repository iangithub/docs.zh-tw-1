---
ms.openlocfilehash: 2a8f20bef8e865235b857014e6d24c625c851d83
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804533"
---
### <a name="only-tls-10-11-and-12-protocols-supported-in-systemnetservicepointmanager-and-systemnetsecuritysslstream"></a>在 System.Net.ServicePointManager 和 System.Net.Security.SslStream 只支援 Tls 1.0、1.1 及 1.2 通訊協定

|   |   |
|---|---|
|詳細資料|從 .NET Framework 4.6 開始，只有 <xref:System.Net.ServicePointManager> 和 <xref:System.Net.Security.SslStream> 類別可以使用下列三種通訊協定之一：Tls1.0、Tls1.1 或 Tls1.2。 不支援 SSL3.0 通訊協定與 RC4 編碼器。|
|建議|建議的緩和措施是將伺服器端應用程式升級至 Tls1.0、Tls1.1 或 Tls1.2。 如果這並不可行，或是用戶端應用程式已中斷，則可使用 <xref:System.AppContext?displayProperty=name> 類別搭配下列兩種方式之一，停用這項功能：<ol><li>以程式設計方式設定 <xref:System.AppContext?displayProperty=name> 的相容性參數，如[這裡](https://devblogs.microsoft.com/dotnet/net-announcements-at-build-2015/#dotnet46)所述。</li><li>將下列程式行加入至 app.config 檔案的 <code>&lt;runtime&gt;</code> 區段：</li></ol><pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.System.Net.DontEnableSchUseStrongCrypto=true&quot;/&gt;&#13;&#10;</code></pre>|
|範圍|次要|
|版本|4.6|
|類型|正在重定目標|
|受影響的 API|<ul><li><xref:System.Net.SecurityProtocolType.Ssl3?displayProperty=nameWithType></li><li><xref:System.Security.Authentication.SslProtocols.None?displayProperty=nameWithType></li><li><xref:System.Security.Authentication.SslProtocols.Ssl2?displayProperty=nameWithType></li><li><xref:System.Security.Authentication.SslProtocols.Ssl3?displayProperty=nameWithType></li></ul>|

