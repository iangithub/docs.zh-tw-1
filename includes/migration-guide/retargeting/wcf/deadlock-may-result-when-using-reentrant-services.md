---
ms.openlocfilehash: 0aaa0ad0e0e3cbd23de287b3b79a8c209143544e
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859265"
---
### <a name="deadlock-may-result-when-using-reentrant-services"></a>使用可重新進入服務時，可能會造成死結

|   |   |
|---|---|
|詳細資料|可重新進入服務可能會造成死結，將服務的執行個體限制為一次執行一個執行緒。 容易發生此問題的服務在其程式碼中會有下列 <xref:System.ServiceModel.ServiceBehaviorAttribute>：<pre><code class="lang-csharp">[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Reentrant)]&#13;&#10;</code></pre>|
|建議|若要解決此問題，您可執行以下動作：<ul><li>將服務的並行模式設為 <xref:System.ServiceModel.ConcurrencyMode.Single?displayProperty=nameWithType> 或 &lt;System.ServiceModel.ConcurrencyMode.Multiple?displayProperty=nameWithType&gt;。 例如：</li></ul><pre><code class="lang-csharp">[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Single)]&#13;&#10;</code></pre><ul><li>安裝 .NET Framework 4.6.2 的最新更新，或升級至更新版本的 .NET Framework。 這會停用 <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType> 中的 <xref:System.Threading.ExecutionContext> 流程。 這是可設定的行為；相當於在您的組態檔中新增下列應用程式設定：</li></ul><pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;Switch.System.ServiceModel.DisableOperationContextAsyncFlow&quot; value=&quot;true&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>Rentrant 服務的值 <code>Switch.System.ServiceModel.DisableOperationContextAsyncFlow</code> 絕對不可設定為 <code>false</code>。|
|範圍|次要|
|版本|4.6.2|
|類型|正在重定目標|
|受影響的 API|<ul><li><xref:System.ServiceModel.ServiceBehaviorAttribute?displayProperty=nameWithType></li><li><xref:System.ServiceModel.ConcurrencyMode.Reentrant?displayProperty=nameWithType></li></ul>|

