---
title: 使用索引和範圍探索資料範圍
description: 此進階教學課程將教導您使用索引和範圍探索資料，以檢查連續資料集的配量。
ms.date: 04/19/2019
ms.custom: mvc
ms.openlocfilehash: 118d3c9ccad98ec02195c2b5e26a2ca203990adf
ms.sourcegitcommit: 682c64df0322c7bda016f8bfea8954e9b31f1990
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2019
ms.locfileid: "65557191"
---
# <a name="indices-and-ranges"></a>索引和範圍

範圍和索引提供簡潔的語法，以存取 <xref:System.Array>、<xref:System.Span%601> 或 <xref:System.ReadOnlySpan%601> 的單一項目或範圍。 這些功能提供更簡潔且清楚的語法來存取序列中單一項目或項目範圍。

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 使用序列中範圍的語法。
> * 了解每個序列開始和結束的設計決策。
> * 了解 <xref:System.Index> 和 <xref:System.Range> 類型的案例。

## <a name="language-support-for-indices-and-ranges"></a>索引和範圍的語言支援

此語言支援仰賴兩個新的型別與兩個新的運算子。
- <xref:System.Index?displayProperty=nameWithType> 代表序列的索引。
- `^` 運算子，它會指定索引相對於序列結尾。
- <xref:System.Range?displayProperty=nameWithType> 代表序列的子範圍。
- Range 運算子 (`..`)，它會指定範圍的開頭與結尾作為其運算子。

讓我們從索引的規則開始。 假設有一個陣列 `sequence`。 `0` 索引與 `sequence[0]` 相同。 `^0` 索引與 `sequence[sequence.Length]` 相同。 請注意，`sequence[^0]` 會擲回例外狀況，就樣 `sequence[sequence.Length]` 會這樣做一樣。 針對任何數字 `n`，索引 `^n` 與 `sequence[sequence.Length - n]` 相同。

```csharp-interactive
string[] words = new string[]
{
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumped",   // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2
    "dog"       // 8                   ^1
};              // 9 (or words.Length) ^0
```

您可以使用 `^1` 索引擷取最後一個字。 將下列程式碼新增於初始設定下方：

[!code-csharp[LastIndex](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastIndex)]

指定範圍「開頭」與「結尾」的範圍。 範圍具有排除性，這表示「結尾」不包含在範圍內。 範圍 `[0..^0]` 代整個範圍，就像 `[0..sequence.Length]` 代表整個範圍一樣。 

下列程式碼會建立具有 "quick"、"brown" 和 "fox" 字組的子範圍。 其會包含 `words[1]` 到 `words[3]`。 項目 `words[4]` 不在範圍內。 將下列程式碼新增至相同的方法。 複製並貼在互動式視窗的底部。

[!code-csharp[Range](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Range)]

下列程式碼會建立具有 "lazy" 和 "dog" 的子範圍。 其包含 `words[^2]` 及 `words[^1]`。 未包含結尾索引 `words[^0]`。 同時新增下列程式碼：

[!code-csharp[LastRange](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastRange)]

下列範例會建立不限定開始、結束或兩者的範圍：

[!code-csharp[PartialRange](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_PartialRanges)]

您也可以將範圍或索引宣告為變數。 然後即可在 `[` 和 `]` 字元內使用變數：

[!code-csharp[IndexRangeTypes](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_RangeIndexTypes)]

下列範例顯示這些選擇的許多原因。 修改 `x`、`y` 和 `z` 以嘗試不同的組合。 在您實驗時，請使用 `x` 小於 `y`，且 `y` 小於 `z` 的有效組合值。 在新方法中新增下列程式碼。 嘗試不同的組合：

[!code-csharp[SemanticsExamples](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Semantics)]

## <a name="scenarios-for-indices-and-ranges"></a>索引和範圍的案例

當您希望對整個序列的子範圍執行某些分析時，您會經常使用範圍和索引。 在準確讀取牽涉的子範圍時，新語法較清晰。 區域函式 `MovingAverage` 採用 <xref:System.Range> 作為其引數。 然後，方法在計算最小值、最大值和平均值時，僅會列舉該範圍。 請在您的專案中嘗試下列程式碼：

[!code-csharp[MovingAverages](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_MovingAverage)]

您可以從 [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/RangesIndexes) 存放庫下載完整的程式碼。
