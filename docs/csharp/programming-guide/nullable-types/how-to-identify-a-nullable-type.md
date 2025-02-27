---
title: 作法：識別可為 Null 的型別 - C# 程式設計指南
ms.custom: seodec18
description: 了解如何判斷某個類型或執行個體是否屬於可為 Null 的型別
ms.date: 09/24/2018
helpviewer_keywords:
- nullable types [C#], identifying
ms.assetid: d4b67ee2-66e8-40c1-ae9d-545d32c71387
ms.openlocfilehash: 73017b8f4c4c046b428d5270a2ef0241c565b07d
ms.sourcegitcommit: a970268118ea61ce14207e0916e17243546a491f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/21/2019
ms.locfileid: "67307038"
---
# <a name="how-to-identify-a-nullable-type-c-programming-guide"></a>作法：識別可為 Null 的型別 (C# 程式設計指南)

下列範例示範如何判斷 <xref:System.Type?displayProperty=nameWithType> 執行個體是否代表封閉式泛型可為 Null 的型別，也就是，<xref:System.Nullable%601?displayProperty=nameWithType> 型別具有指定的型別參數 `T`：

[!code-csharp-interactive[whether Type is nullable](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#1)]

如範例所示，您使用 [typeof](../../language-reference/operators/type-testing-and-conversion-operators.md#typeof-operator) 運算子來建立 <xref:System.Type?displayProperty=nameWithType> 物件。  
  
如果您想要判斷某個執行個體是否屬於可為 Null 的型別，請勿使用 <xref:System.Object.GetType%2A?displayProperty=nameWithType> 方法透過上述程式碼來測試 <xref:System.Type> 執行個體。 當您在可為 Null 的型別執行個體上呼叫 <xref:System.Object.GetType%2A?displayProperty=nameWithType> 方法時，該執行個體會 [Boxing](using-nullable-types.md#boxing-and-unboxing) 處理為 <xref:System.Object>。 由於對可為 Null 型別的非 Null 執行個體進行 Boxing 處理相當於對基礎類型的值進行 Boxing 處理，因此 <xref:System.Object.GetType%2A> 會傳回<xref:System.Type> 物件，代表可為 Null 型別的基礎型別：

[!code-csharp-interactive[GetType example](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#2)]

請勿使用 [is](../../language-reference/keywords/is.md) 運算子來判斷某個執行個體是否屬於可為 Null 的型別。 如下列範例所示，您無法使用 `is` 運算子來區別可為 Null 型別及其基礎類型的執行個體類型：

[!code-csharp-interactive[is operator example](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#3)]

您可以使用下列範例所示的程式碼來判斷某個執行個體是否屬於可為 Null 的型別：

[!code-csharp-interactive[whether an instance is of a nullable type](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#4)]
  
## <a name="see-also"></a>另請參閱

- [可為 Null 的型別](index.md)
- [使用可為 Null 的型別](using-nullable-types.md)
- <xref:System.Nullable.GetUnderlyingType%2A>
