---
title: base 關鍵字 - C# 參考
ms.custom: seodec18
description: 了解 base 關鍵字，該關鍵字可用來存取 C# 衍生類別中基底類別的成員。
ms.date: 07/20/2015
f1_keywords:
- base
- BaseClass.BaseClass
- base_CSharpKeyword
helpviewer_keywords:
- base keyword [C#]
ms.assetid: 8b645dbe-1a33-49b8-8716-1c401f9a5ea5
ms.openlocfilehash: 2ef0d07aed595fa630459171482e0b0849aed877
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2019
ms.locfileid: "67401600"
---
# <a name="base-c-reference"></a>base (C# 參考)

`base` 關鍵字是用來存取衍生類別中基底類別的成員︰

- 對已由另一個方法覆寫的基底類別來呼叫方法。

- 指定應該在建立衍生類別的執行個體時呼叫的基底類別建構函式。

僅允許在建構函式、執行個體方法或執行個體屬性存取子中進行基底類別存取。

從靜態方法使用 `base` 關鍵字是錯誤的。

所存取的基底類別是類別宣告中所指定的基底類別。 例如，如果您指定 `class ClassB : ClassA`，則不論 ClassA 的基底類別為何，都會從 ClassB 存取 ClassA 成員。

## <a name="example"></a>範例

在此範例中，基底類別 `Person` 和衍生類別 `Employee` 都會有名為 `Getinfo` 的方法。 使用 `base` 關鍵字，即可從衍生類別對基底類別呼叫 `Getinfo` 方法。

[!code-csharp[csrefKeywordsAccess#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsAccess/CS/csrefKeywordsAccess.cs#1)]

如需其他範例，請參閱 [new](new-modifier.md)、[virtual](virtual.md) 和 [override](override.md)。

## <a name="example"></a>範例

這個範例示範如何指定在建立衍生類別的執行個體時呼叫的基底類別建構函式。

[!code-csharp[csrefKeywordsAccess#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsAccess/CS/csrefKeywordsAccess.cs#2)]

## <a name="c-language-specification"></a>C# 語言規格

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>另請參閱

- [C# 參考](../../../csharp/language-reference/index.md)
- [C# 程式設計指南](../../../csharp/programming-guide/index.md)
- [C# 關鍵字](../../../csharp/language-reference/keywords/index.md)
- [this](../../../csharp/language-reference/keywords/this.md)
