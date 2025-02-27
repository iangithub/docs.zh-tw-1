---
title: 多型 - C# 程式設計手冊
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, polymorphism
- polymorphism [C#]
ms.assetid: 086af969-29a5-4ce8-a993-0b7d53839dab
ms.openlocfilehash: a7cd450fbc2e0a5acd32675ab2c6b46dc2c92757
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2019
ms.locfileid: "67398373"
---
# <a name="polymorphism-c-programming-guide"></a>多型 (C# 程式設計手冊)
多型通常是指物件導向程式設計的第三個重要部分，其重要性僅次於封裝和繼承。 多型在希臘文中表示「多種形狀」，可分成下列兩方面：  
  
- 在執行階段，衍生類別物件可視為方法參數和集合或陣列等位置中的基底類別物件。 發生此情況時，物件的宣告類型與其執行階段類型將不再相同。  
  
- 基底類別可以定義和實作 [virtual](../../../csharp/language-reference/keywords/virtual.md)「方法」  ，而衍生類別可以[覆寫](../../../csharp/language-reference/keywords/override.md)這些方法，換句話說，衍生類別會提供自己的定義和實作。 在執行階段，當用戶端程式碼呼叫方法時，CLR 會查詢物件的執行階段類型，然後叫用虛擬方法的覆寫。 因此，在您的原始程式碼中，您可以在基底類別上呼叫方法，然後執行衍生類別版本的方法。  
  
 虛擬方法可讓您以一致的方式來使用相關物件群組。 例如，假設您有一個繪圖應用程式，可讓使用者在繪圖介面上建立各種圖形。 您不知道使用者將在編譯時期建立哪一種圖形。 但是，應用程式必須追蹤所建立的所有不同圖形類型，並且必須根據使用者滑鼠動作來更新圖形。 您可以使用多型，分兩個基本步驟來解決這個問題：  
  
1. 建立類別階層架構，其中每個特定圖形類別都是衍生自一個通用基底類別。  
  
2. 使用虛擬方法，透過對基底類別方法發出單一呼叫，在任何衍生類別上叫用適當的方法。  
  
 首先，建立稱為 `Shape` 的基底類別，以及 `Rectangle`、`Circle` 和 `Triangle` 等衍生類別。 將稱為 `Shape` 的虛擬方法提供給 `Draw` 類別，然後在每個衍生類別中覆寫此方法，以繪製該類別代表的特定圖形。 建立 `List<Shape>` 物件並加入 Circle、Triangle 和 Rectangle。 若要更新繪圖介面，請使用 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 迴圈逐一查看清單，並在清單中的每個 `Shape` 物件上呼叫 `Draw` 方法。 即使清單中的每個物件都有 `Shape` 的宣告類型，會叫用的是執行階段類型 (每個衍生類別中之方法的覆寫版本)。  
  
 [!code-csharp[csProgGuideInheritance#50](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#50)]  
  
 在 C# 中，所有類型都是多型類型，因為所有類型 (包括使用者定義的類型) 都是繼承自 <xref:System.Object>。  
  
## <a name="polymorphism-overview"></a>多型概觀  
  
### <a name="virtual-members"></a>虛擬成員  
 當衍生類別從基底類別繼承時，會取得基底類別的所有方法、欄位、屬性和事件。 衍生類別的設計工具可選擇是否要  
  
- 覆寫在基底類別中的虛擬成員  
  
- 繼承最近的基底類別方法，而不加以覆寫  
  
- 定義隱藏基底類別實作的成員之新的非虛擬實作  
  
 只有在基底類別成員宣告為 [virtual](../../../csharp/language-reference/keywords/virtual.md) 或 [abstract](../../../csharp/language-reference/keywords/abstract.md) 時，衍生類別才能覆寫基底類別成員。 衍生成員必須使用 [override](../../../csharp/language-reference/keywords/override.md) 關鍵字明確指出方法預定會參與虛擬引動過程。 下列程式碼提供一個範例：  
  
 [!code-csharp[csProgGuideInheritance#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#20)]  
  
 欄位不可為虛擬，只有方法、屬性、事件和索引子可以是虛擬。 當衍生類別覆寫虛擬成員時，即使將該類別的執行個體當做基底類別的執行個體來存取，也會呼叫該成員。 下列程式碼提供一個範例：  
  
 [!code-csharp[csProgGuideInheritance#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#21)]  
  
 虛擬方法和屬性可讓衍生類別不需要使用方法的基底類別實作，即可擴充基底類別。 如需詳細資訊，請參閱[使用 Override 和 New 關鍵字進行版本控制](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md)。 介面是用來定義將其實作保留給衍生類別之一個方法或一組方法的另一種做法。 如需詳細資訊，請參閱[介面](../../../csharp/programming-guide/interfaces/index.md)。  
  
### <a name="hiding-base-class-members-with-new-members"></a>使用新成員隱藏基底類別成員  
 如果您想讓衍生成員使用與基底類別中成員相同的名稱，但不想讓該成員參與虛擬引動過程，則可以使用 [new](../../../csharp/language-reference/keywords/new-modifier.md) 關鍵字。 `new` 關鍵字會放置在要取代之類別成員的傳回類型前面。 下列程式碼提供一個範例：  
  
 [!code-csharp[csProgGuideInheritance#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#18)]  
  
 您仍然可以透過將衍生類別執行個體轉換成基底類別執行個體，從用戶端程式碼存取隱藏的基底類別成員。 例如：  
  
 [!code-csharp[csProgGuideInheritance#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#19)]  
  
### <a name="preventing-derived-classes-from-overriding-virtual-members"></a>防止衍生類別覆寫虛擬成員  
 虛擬成員會無限期保持為虛擬，而不論在虛擬成員與原本宣告的類別之間已宣告多少類別。 如果類別 A 宣告一個虛擬成員，類別 B 衍生自 A，而類別 C 又衍生自 B，則類別 C 會繼承虛擬成員，且不論類別 B 是否宣告該成員的覆寫，類別 C 都可以選擇覆寫該成員。 下列程式碼提供一個範例：  
  
 [!code-csharp[csProgGuideInheritance#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#22)]  
  
 衍生類別可以透過將覆寫宣告為 [sealed](../../../csharp/language-reference/keywords/sealed.md)，來停止虛擬繼承。 若要執行這項操作，您必須在類別成員宣告中的 `sealed` 關鍵字前面放置 `override` 關鍵字。 下列程式碼提供一個範例：  
  
 [!code-csharp[csProgGuideInheritance#24](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#24)]  
  
 在上述範例中，`DoWork` 方法對衍生自 C 的任何類別不再是虛擬。對 C 執行個體而言，它仍然是虛擬，即使它們轉換成類型 B 或類型 A 也是一樣。使用 `new` 關鍵字，可以將密封方法取代為衍生類別，如下列範例所示：  
  
 [!code-csharp[csProgGuideInheritance#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#25)]  
  
 在這個範例中，如果使用類型 D 的變數在 D 上呼叫 `DoWork`，則會呼叫新的 `DoWork`。 如果使用類型 C、B 或 A 的變數來存取 D 的執行個體，對 `DoWork` 的呼叫會遵循虛擬繼承的原則，並將這些呼叫路由傳送至類別 C 上的 `DoWork` 實作。  
  
### <a name="accessing-base-class-virtual-members-from-derived-classes"></a>從衍生類別存取基底類別虛擬成員  
 已取代或覆寫方法或屬性的衍生類別，仍可使用 `base` 關鍵字存取基底類別上的方法或屬性。 下列程式碼提供一個範例：  
  
 [!code-csharp[csProgGuideInheritance#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#26)]  
  
 如需詳細資訊，請參閱 [base](../../../csharp/language-reference/keywords/base.md)。  
  
> [!NOTE]
>  建議虛擬成員使用 `base`，在其所擁有的實作中呼叫其基底類別實作。 允許發生基底類別行為，可讓衍生類別集中實作衍生類別的特定行為。 如果不呼叫基底類別實作，則衍生類別可自行決定是否要讓其行為與基底類別的行為相容。  
  
## <a name="in-this-section"></a>本節內容  
  
- [使用 Override 和 New 關鍵字進行版本控制](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md)  
  
- [了解使用 Override 和 New 關鍵字的時機](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md)  
  
- [如何：覆寫 ToString 方法](../../../csharp/programming-guide/classes-and-structs/how-to-override-the-tostring-method.md)  
  
## <a name="see-also"></a>另請參閱

- [C# 程式設計指南](../../../csharp/programming-guide/index.md)
- [繼承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)
- [抽象和密封類別以及類別成員](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)
- [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)
- [事件](../../../csharp/programming-guide/events/index.md)
- [屬性](../../../csharp/programming-guide/classes-and-structs/properties.md)
- [索引子](../../../csharp/programming-guide/indexers/index.md)
- [型別](../../../csharp/programming-guide/types/index.md)
