---
ms.openlocfilehash: 640af1f9814b31ad0b431a8317244a94250a65cc
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859113"
---
### <a name="sslstream-supports-tls-alerts"></a>SslStream 支援 TLS 警示

|   |   |
|---|---|
|詳細資料|失敗的 TLS 信號交換之後，第一個 I/O 讀取/寫入作業將會擲回 <xref:System.IO.IOException?displayProperty=name> 與內部 <xref:System.ComponentModel.Win32Exception?displayProperty=name> 例外狀況。 <xref:System.ComponentModel.Win32Exception?displayProperty=name> 的 <xref:System.ComponentModel.Win32Exception.NativeErrorCode?displayProperty=name> 程式碼可以使用 [TLS 與 SSL 警示適用的安全通道文件](https://docs.microsoft.com/windows/desktop/SecAuthN/schannel-error-codes-for-tls-and-ssl-alerts)。如需詳細資訊，請參閱 [RFC 2246：7.2.2 節「錯誤警示」](https://tools.ietf.org/html/rfc2246#section-7.2.2) \(英文\)。 <br/>.NET Framework 4.6.2 和更早版本的行為是如果另一方交握失敗，傳輸通道 (通常是 TCP 連線) 會在寫入或讀取期間逾時，並在之後立即拒絕連線。|
|建議|呼叫網路 I/O API (例如 <xref:System.IO.Stream.Read(System.Byte[],System.Int32,System.Int32)>/<xref:System.IO.Stream.Write(System.Byte[],System.Int32,System.Int32)>) 的應用程式，應該處理 <xref:System.IO.IOException> 或 <xref:System.TimeoutException?displayProperty=name>。<br/>從 .NET Framework 4.7 開始，預設會啟用 TLS 警示功能。 以 .NET Framework 4.0 到 4.6.2 版為目標且在 .NET Framework 4.7 或更高版本的系統上執行的應用程式，會停用此功能以保留相容性。 <br/>若為在 .NET Framework 4.7 或更新版本上執行之 .NET Framework 4.6 和更新版本的應用程式，您可以使用下列組態 API 來啟用或停用此功能。<ul><li>以程式設計的方式：</li></ul>必須是應用程式執行的第一件事，因為 ServicePointManager 只會初始化一次：<pre><code class="lang-csharp">AppContext.SetSwitch(&quot;TestSwitch.LocalAppContext.DisableCaching&quot;, true);&#13;&#10;AppContext.SetSwitch(&quot;Switch.System.Net.DontEnableTlsAlerts&quot;, true); // Set to &#39;false&#39; to enable the feature in .NET Framework 4.6 - 4.6.2.&#13;&#10;</code></pre><ul><li>AppConfig：</li></ul><pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Net.DontEnableTlsAlerts=true&quot;/&gt;&#13;&#10;&lt;!-- Set to &#39;false&#39; to enable the feature in .NET Framework 4.6 - 4.6.2. --&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre><ul><li>登錄機碼 (電腦全域)：</li></ul>將值設定為 <code>false</code>，以在 .NET Framework 4.6 - 4.6.2 中啟用功能。<ul><li>關鍵字：HKLM\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\AppContext\Switch.System.Net.DontEnableTlsAlerts</li><li>類型：String</li><li>值：&quot;True&quot;</li></ul>|
|範圍|Edge|
|版本|4.7|
|類型|正在重定目標|
|受影響的 API|<ul><li><xref:System.Net.Security.SslStream?displayProperty=nameWithType></li><li><xref:System.Net.WebRequest?displayProperty=nameWithType></li><li><xref:System.Net.HttpWebRequest?displayProperty=nameWithType></li><li><xref:System.Net.FtpWebRequest?displayProperty=nameWithType></li><li><xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType></li><li><xref:System.Net.Http?displayProperty=nameWithType></li></ul>|

