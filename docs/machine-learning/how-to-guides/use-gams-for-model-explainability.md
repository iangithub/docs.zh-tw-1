---
title: 將一般化累加模型與圖形函式用於模型可解釋性
description: 在 ML.NET 中針對模型可解釋性使用一般化累加模型與圖形函式
ms.date: 03/05/2019
ms.custom: mvc,how-to
ms.openlocfilehash: ef56f737a2ad0cba616e32229ac3a395146fb6d2
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662135"
---
# <a name="use-generalized-additive-models-and-shape-functions-for-model-explainability-in-mlnet"></a>在 ML.NET 中針對模型可解釋性使用一般化累加模型與圖形函式

> [!NOTE]
> 本主題涉及 ML.NET，此功能目前為公開預覽版，因此内容可能會有變更。 如需詳細資訊，請瀏覽 [ML.NET 簡介](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet) (英文)。

本操作說明與關聯的範例目前是使用 **ML.NET 0.10 版**。 如需詳細資訊，請參閱 [dotnet/machinelearning GitHub 存放庫](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes) \(英文\) 中的版本資訊。

在建立機器學習模型時，模型通常不足以直接用來進行預測。 一般來說，機器學習開發人員、決策者，以及受該模型影響的人員需要了解機器學習模型如何做出決策，以及哪些特徵會影響其效能。 **一般化加法模型 (GAM)** 用於 Microsoft 內部的模型可解釋性，以協助機器學習開發人員建立可由其他人輕鬆解譯的高容量模型。

GAM 是屬於線性模型的一種**可解譯模型**類別，此項在非線性函數中稱為「形狀函數」的單一變數。 線性模型可輕鬆地解譯，但因為特徵的模型學習函式取代了單一加權，它們能夠建立比單一線性模型更複雜的關聯性。 產生的 GAM 預測工具具有截距項，代表訓練集上的平均預測，以及代表與平均預測偏差的形狀函數。 形狀函數可以直接檢查，來查看針對不同特徵值的模型回應，並視覺化如程式碼範例結尾所建立的下列圖表。 ML.NET 中的 GAM 訓練工具使用淺層梯度提升決策樹 (例如樹墩) 來學習無母數形狀函數，並且以 Lou、Caruana 和 Gehrke 的[適用於分類和迴歸的可理解模型](https://www.cs.cornell.edu/~yinlou/papers/lou-kdd12.pdf) \(英文\) 中所述的方法為基礎。

```csharp
// Train the Generalized Additive Model
var fitPipeline = pipeline.Fit(data);
var gamModel = fitPipeline.LastTransformer.Model;

// The intercept for Generalize Additive Models represent the average prediction for the training data
var intercept = gamModel.Intercept;
Console.WriteLine($"Average predicted cost: {intercept:0.00}");

// Get the column names from the training set
var columnNames = data.Schema.AsEnumerable()
    .Select(column => column.Name) // Get the column names
    .Where(name => name != "MedianHomeValue") // Drop the Label
    .ToArray();

// Get the index of a variable from the training data
var myFeatureIndex = columnNames.ToList().FindIndex(str => str.Equals("MyFeature"));

// The shape functions represent the deviation from the average prediction as a function of the feature value
// It is represented by a discrete set of bins
// First, get the array of bin upper bounds from the model for this feature
var myFeatureBins = gamModel.GetBinUpperBounds(myFeatureIndex);
// Then get the array of bin weights; these are the effect size for each bin
var myFeatureWeights = gamModel.GetBinEffects(myFeatureIndex);

// Write out the shape function for the feature (see the following figure for what this looks like)
for (int i = 0; i < myFeatureBins.Length; i++)
{
    Console.WriteLine($"x < {myFeatureBins[i]:0.00} => {myFeatureWeights[i]:0.000}");
}
```

![一般化加法模型形狀函數圖表](./media/use-gams-for-model-explainability/gam-shape-function-graph.png)

如需如何定型 GAM 模型和檢查與解譯結果的範例，請參閱 [dotnet/machinelearning GitHub 存放庫](https://github.com/dotnet/machinelearning/blob/master/docs/samples/Microsoft.ML.Samples/Dynamic/GeneralizedAdditiveModels.cs) \(英文\)。
