---
title: 匿名函式 - C# 程式設計指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [C#], as anonymous functions
- anonymous functions [C#]
- anonymous methods [C#]
ms.assetid: 6ce3f04d-0c71-4728-9127-634c7e9a8365
ms.openlocfilehash: 338f4b34a5de84d4ce2eb9e0bd6f4c9ebe360fa4
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65584273"
---
# <a name="anonymous-functions-c-programming-guide"></a>匿名函式 (C# 程式設計手冊)
匿名函式是可用於任何需要委派類型之處的「內嵌」陳述式或運算式。 您可以使用它來初始化具名委派，或改將它傳遞給具名委派類型作為方法參數。  
  
 有兩種類型的匿名函式，將在下列主題中個別進行討論︰  
  
- [Lambda 運算式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)。  
  
- [匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)  
  
    > [!NOTE]
    >  Lambda 運算式可以繫結至運算式樹狀結構，也可以繫結至委派。  
  
## <a name="the-evolution-of-delegates-in-c"></a>C\# 中的委派演進
 在 C# 1.0 中，您已使用該程式碼中其他地方所定義的方法明確初始化委派，來建立委派執行個體。 C# 2.0 引進匿名方法概念，用來撰寫可在委派引動過程中執行的未命名內嵌陳述式區塊。 C# 3.0 引進 Lambda 運算式，這在概念上與匿名方法類似，但更易懂且更簡潔。 這兩個功能統稱為「匿名函式」。 一般而言，以 .NET Framework 3.5 版和更新版本為目標的應用程式應該使用 Lambda 運算式。  
  
 下列範例示範從 C# 1.0 到 C# 3.0 的委派建立演進：  
  
 [!code-csharp[csProgGuideLINQ#65](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#65)]  
  
## <a name="c-language-specification"></a>C# 語言規格  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [陳述式、運算式和運算子](../../../csharp/programming-guide/statements-expressions-operators/index.md)
- [Lambda 運算式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)
- [委派](../../../csharp/programming-guide/delegates/index.md)
- [運算式樹狀結構 (C#)](../concepts/expression-trees/index.md)
