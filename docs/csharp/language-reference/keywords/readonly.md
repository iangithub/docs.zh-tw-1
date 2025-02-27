---
title: readonly 關鍵字 - C# 參考
ms.custom: seodec18
ms.date: 06/21/2018
f1_keywords:
- readonly_CSharpKeyword
- readonly
helpviewer_keywords:
- readonly keyword [C#]
ms.assetid: 2f8081f6-0de2-4903-898d-99696c48d2f4
ms.openlocfilehash: 4a51bb0e854de127c632c28f613a7602bf09f432
ms.sourcegitcommit: 127343afce8422bfa944c8b0c4ecc8f79f653255
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2019
ms.locfileid: "67348016"
---
# <a name="readonly-c-reference"></a>readonly (C# 參考)

`readonly` 關鍵字是可以在三種內容中使用的修飾詞：

- 在[欄位宣告](#readonly-field-example)中，`readonly` 表示只有在宣告中或相同類別的建構函式中，才能對欄位進行指派。 可以在欄位宣告及建構函式中指派及多次重新指派 readonly 欄位。 
  
  當建構函式結束之後，便無法指派 `readonly` 欄位。 這對實值型別及參考型別分別具有不同的含意：
  
  - 由於實值型別會直接包含其資料，因此具有 `readonly` 實值型別的欄位是不可變的。 
  - 由於參考型別包含針對其資料的參考，因此 `readonly` 參考型別的欄位必須一律參考相同的物件。 該物件並非不可變的。 `readonly` 修飾詞可防止欄位被不同的參考型別執行個體取代。 不過，修飾詞並無法防止欄位的執行個體資料經由唯讀欄位被修改。

  > [!WARNING]
  > 包含可變動參考型別之外部可見唯讀欄位的外部可見類型是個潛在的安全性弱點，並可能會觸發警告 [CA2104](/visualstudio/code-quality/ca2104-do-not-declare-read-only-mutable-reference-types)：「不要宣告唯讀的可變動參考類型。」

- 在 [`readonly struct` 定義](#readonly-struct-example)中，`readonly` 表示 `struct` 是不可變的。
- 在 [`ref readonly` 方法傳回](#ref-readonly-return-example)中，`readonly` 修飾詞表示方法會傳回參考且不允許寫入到該參考。

最後兩種內容已新增到 C# 7.2。

## <a name="readonly-field-example"></a>唯讀欄位範例

在此範例中，無法變更 `ChangeYear`方法中的 `year` 欄位值，即使它在類別建構函式中獲指派值也是一樣︰

[!code-csharp[Readonly Field example](~/samples/snippets/csharp/keywords/ReadonlyKeywordExamples.cs#ReadonlyField)]

您只能在下列內容中將值指派給 `readonly` 欄位︰

- 在宣告中初始化變數時，例如︰

  ```csharp
  public readonly int y = 5;
  ```

- 在包含執行個體欄位宣告的類別執行個體建構函式。
- 在包含靜態欄位宣告的類別靜態建構函式。

這些建構函式內容也是唯一可將 `readonly` 欄位當做 [out](out-parameter-modifier.md) 或 [ref](ref.md) 參數有效傳遞的內容。

> [!NOTE]
> `readonly` 關鍵字與 [const](const.md) 關鍵字不同。 `const` 欄位只能在欄位的宣告中初始化。 您可以在欄位宣告及任何建構函式中，多次指派 `readonly` 欄位。 因此，`readonly` 欄位可能會因使用的建構函式而有不同的值。 此外，雖然 `const` 欄位是編譯時間常數，但是 `readonly` 欄位可用於執行階段常數，如下列範例所示：
>
> ```csharp
> public static readonly uint timeStamp = (uint)DateTime.Now.Ticks;
> ```

[!code-csharp[Initialize readonly Field example](~/samples/snippets/csharp/keywords/ReadonlyKeywordExamples.cs#InitReadonlyField)]

在上述範例中，如果您使用如下範例的陳述式：

```csharp
p2.y = 66;        // Error
```

則會收到編譯器錯誤訊息：

`A readonly field cannot be assigned to (except in a constructor or a variable initializer)`

## <a name="readonly-struct-example"></a>唯讀結構範例

`struct` 定義上的 `readonly` 修飾詞會宣告 struct 是**不可變**。 `struct` 的每個執行個體欄位必須標記為 `readonly`，如下列範例所示：

[!code-csharp[readonly struct example](~/samples/snippets/csharp/keywords/ReadonlyKeywordExamples.cs#ReadonlyStruct)]

上述範例會使用[唯讀自動屬性](../../properties.md#read-only)來宣告其儲存體。 它會指示編譯器建立 `readonly` 支援這些屬性的欄位。 您也可以直接宣告 `readonly` 欄位：

```csharp
public readonly struct Point
{
    public readonly double X;
    public readonly double Y;

    public Point(double x, double y) => (X, Y) = (x, y);

    public override string ToString() => $"({X}, {Y})";
}
```

加入未標記為 `readonly` 的欄位會產生編譯器錯誤 `CS8340`：「唯讀結構的執行個體欄位必須為唯讀。」

## <a name="ref-readonly-return-example"></a>參考唯讀傳回範例

`ref return` 上的 `readonly` 修飾詞指出傳回的參考不能修改。 下列範例會傳回對來源的參考。 它會使用 `readonly` 修飾詞來表示呼叫端無法修改來源：

[!code-csharp[readonly struct example](~/samples/snippets/csharp/keywords/ReadonlyKeywordExamples.cs#ReadonlyReturn)]
傳回的型別不一定得是 `readonly struct`。 可由 `ref` 傳回的任何類型，都可以由 `ref readonly` 傳回。

## <a name="c-language-specification"></a>C# 語言規格

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>另請參閱

- [C# 參考](../index.md)
- [C# 程式設計指南](../../programming-guide/index.md)
- [C# 關鍵字](index.md)
- [修飾詞](modifiers.md)
- [const](const.md)
- [欄位](../../programming-guide/classes-and-structs/fields.md)
