---
title: 命名空間 - C# 程式設計手冊
ms.custom: seodec18
ms.date: 08/21/2018
helpviewer_keywords:
- C# language, namespaces
- namespaces [C#]
ms.assetid: b1c4ab46-3fad-4ffa-9deb-dd50a2d8c65a
ms.openlocfilehash: 893ac7bbfcfe159787789238c3142f34ac7ecf35
ms.sourcegitcommit: 10986410e59ff29f2ec55c6759bde3eb4d1a00cb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66423296"
---
# <a name="namespaces-c-programming-guide"></a>命名空間 (C# 程式設計手冊)

C# 程式設計大量使用命名空間的原因有兩個。 首先，.NET Framework 會使用命名空間組織其多種類別，如下所示：  
  
 [!code-csharp[csProgGuide#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#22)]  
  
`System` 是命名空間，而 `Console` 是該命名空間中的類別。 您可以使用 `using` 關鍵字，如此就不需要完整名稱，如下列範例所示：  
  
 [!code-csharp[csProgGuide#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/using.cs#1)]  
  
 [!code-csharp[csProgGuide#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#25)]  
  
如需詳細資訊，請參閱 [using 指示詞](../../language-reference/keywords/using-directive.md)。  
  
其次，宣告您自己的命名空間，將有助於在較大型的程式設計專案中控制類別和方法名稱的範圍。 請使用 [namespace](../../language-reference/keywords/namespace.md) 關鍵字宣告命名空間，如下列範例所示：  
  
 [!code-csharp[csProgGuideNamespaces#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces.cs#6)]

命名空間的名稱必須是有效的 C# [識別碼名稱](../inside-a-program/identifier-names.md)。

## <a name="namespaces-overview"></a>命名空間概觀  

命名空間具有下列屬性：  
  
- 命名空間可組織大型程式碼專案。  
- 命名空間會使用 `.` 運算子分隔。  
- `using` 指示詞讓您不需要指定每個類別的命名空間名稱。  
- `global` 命名空間是「根」命名空間：`global::System` 一律會參考 .NET <xref:System> 命名空間。  

## <a name="c-language-specification"></a>C# 語言規格

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [C# 程式設計指南](../index.md)
- [使用命名空間](using-namespaces.md)
- [如何：使用全域命名空間別名](how-to-use-the-global-namespace-alias.md)
- [如何：使用 My 命名空間](how-to-use-the-my-namespace.md)
- [識別碼名稱](../inside-a-program/identifier-names.md)
- [using 指示詞](../../language-reference/keywords/using-directive.md)
- [::運算子](../../language-reference/operators/namespace-alias-qualifer.md)
