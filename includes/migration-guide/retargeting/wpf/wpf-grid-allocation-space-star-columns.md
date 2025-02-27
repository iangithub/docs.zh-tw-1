---
ms.openlocfilehash: 5d8c5dcadcea446a88e2ccaa73b1be91eea0956b
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859099"
---
### <a name="wpf-grid-allocation-of-space-to-star-columns"></a>star-column 空間的 WPF 方格配置

|   |   |
|---|---|
|詳細資料|從 .NET Framework 4.7 開始，WPF 取代了 <xref:System.Windows.Controls.Grid> 用來配置 *-column 空間的演算法。 在以下幾種情況下，這會使指派給 *-column 的實際寬度產生變化：<ul><li>當一或多個 *-column 也具有寬度下限或上限，因而會覆寫該資料行的按比例配置時。 (寬度下限可能衍生自明確的 MinWidth 宣告，或衍生自從資料行的內容取得的隱含下限。 寬度上限僅能明確地從 MaxWidth 宣告定義)。</li><li>當一或多個 *-column 宣告極大的 *-weight 時 (大於 10^298)。</li><li>當 *-weight 的差異足以發生浮點不穩定 (溢位、反向溢位、精確度失準) 時。</li><li>當版面配置進位已啟用，且有效顯示 DPI 夠高時。</li></ul>在前兩個狀況中，新演算法產生的寬度可能明顯不同於舊演算法產生的寬度；在最後一個狀況中，差異最多會是一或兩個像素。<p/>新的演算法修正了舊演算法中的數個錯誤：<ol><li>資料行的總配置可能會超過方格的寬度。 資料行的按比例共用若低於其大小下限，配置空間時就可能發生這個狀況。 此演算法會配置大小下限，因此，其他資料行的可用空間會減少。 如果沒有要配置的 *-column，總配置將會過大。</li><li>總配置的方格寬度可能會不足。 這是第 1 點的雙重問題，在為資料行配置空間時，若其按比例共用超過大小上限，但缺少可使用剩餘空間的 *-column 時，就會發生這個狀況。</li><li>兩個 *-column 的配置可能不是依其 *-weight 按比例分配。 相較於第 1 點/第 2 點，這是程度較輕的錯誤，在為 *-columns A、B 和 C (依此順序) 配置空間時，若 B 的按比例共用違反其下限 (或上限) 條件約束，就會發生這個狀況。 如上所述，這會使資料行 C 的可用的空間產生變化，可能會獲得較 A 更少 (或更多) 的比例配置，</li><li>權數極大 (&gt; 10^298) 的資料行一律會視為擁有 10 ^298 的權數。 它們之間 (及權數較小的資料行之間) 的比例差異則可忽略。</li><li>無法正確處理擁有無限權數的資料行。 [事實上，您無法將權數設為無限大，但這是人為限制。 配置程式碼會嘗試處理它，但成效不彰。]</li><li>避免溢位、反向溢位時的幾個小問題、精確度失準及類似的浮點數問題。</li><li>版面配置進位的調整在 DPI 足夠高的情況下不正確。</li></ol>新的演算法會產生符合下列準則的結果︰<p/>答： 指派給 *-column 的實際寬度永遠不會低於其寬度下限或高於其寬度上限。<br/>B. 對於尚未指派寬度下限或上限的每個 <em>-column，會依其 <em>-weight 按比例指派寬度。確切而言，若有兩個資料行分別使用寬度 x</em> 和 y</em> 宣告，而任一資料行均未配置其寬度下限和上限，則指派給資料行的實際寬度 v 和 w 所使用的比例相同：v / w == x / y。<br/>C. 配置給「按比例」*-column 的總寬度，等於配置給條件約束的資料行 (固定、自動及已配置寬度下限或上限的 *-column) 後的可用空間。 這可能是零，例如，若寬度下限的總和超過方格可用的寬度。<br/>D. 以上所述是就「理想」的版面配置而言。 當版面配置進位作用中時，實際寬度與理想寬度最多會相差一個像素。<br/>舊的演算法能實現 (A) 準則，卻無法實現上述狀況中的其他準則。<p/>本文中有關資料行和寬度的所有內容也適用於資料列和高度。|
|建議|根據預設，以 .NET Framework 4.7 開始的 .NET Framework 版本為目標的應用程式會看見新的演算法，而以 .NET Framework 4.6.2 或更舊版本為目標的應用程式會看見舊的演算法。<p/>若要覆寫預設值，請使用下列組態設定︰<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.Grid.StarDefinitionsCanExceedAvailableSpace=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>值 <code>true</code> 會選取舊的演算法，<code>false</code> 會選取新的演算法。|
|範圍|次要|
|版本|4.7|
|類型|正在重定目標|

