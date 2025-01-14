---
title: $ - 字串內插補點 - C# 參考
ms.custom: seodec18
description: 字串內插補點提供比傳統字串複合格式化更容易讀取且方便的語法來格式化字串輸出。
ms.date: 04/29/2019
f1_keywords:
- $_CSharpKeyword
- $
helpviewer_keywords:
- $ special character [C#]
- $ language element [C#]
- string interpolation [C#]
- interpolated string [C#]
author: pkulikov
ms.author: ronpet
ms.openlocfilehash: bc27eedcf1957a109a9bcb80cf9a49e9606921fd
ms.sourcegitcommit: 26f4a7697c32978f6a328c89dc4ea87034065989
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2019
ms.locfileid: "66251005"
---
# <a name="---string-interpolation-c-reference"></a>$ - 字串內插補點 (C# 參考)

`$` 特殊字元會將字串常值識別為「字串內插補點」。 插入字串是可能包含「內插補點運算式」的字串常值。 將插入字串解析為結果字串時，會將具有內插補點運算式之項目取代為運算式結果的字串表示。 C# 6 和更新版本的語言中有提供這項功能。

字串插補在建立格式化字串時，是比[字串複合格式化](../../../standard/base-types/composite-formatting.md)功能更容易理解且方便的語法。 下列範例會使用這兩項功能，產生相同的輸出：

[!code-csharp-interactive[compare with composite formatting](~/samples/snippets/csharp/language-reference/tokens/string-interpolation.cs#1)]

## <a name="structure-of-an-interpolated-string"></a>插入字串的結構

若要將字串常值識別為插入字串，請在其前面加上 `$` 符號。 字串常值開頭的 `$` 與 `"` 之間不能有空白字元。 這樣做會導致編譯時期錯誤。

具有內插補點運算式的項目結構如下所示：

```
{<interpolationExpression>[,<alignment>][:<formatString>]}
```

在方括號中的元素是選擇性的元素。 下表說明每個元素：

|元素|說明|
|-------------|-----------------|
|`interpolationExpression`|產生要格式化之結果的運算式。 `null` 結果的字串表示是 <xref:System.String.Empty?displayProperty=nameWithType>。|
|`alignment`|常數的運算式，其值定義內插補點運算式結果之字串表示的字元數下限。 如果是正數，則字串表示是靠右對齊；如果是負數，它是靠左對齊。 如需詳細資訊，請參閱[對齊元件](../../../standard/base-types/composite-formatting.md#alignment-component)。|
|`formatString`|運算式結果的類型所支援的格式字串。 如需詳細資訊，請參閱[格式字串元件](../../../standard/base-types/composite-formatting.md#format-string-component)。|

下列範例會使用上述的選擇性格式化元件：

[!code-csharp-interactive[specify alignment and format string](~/samples/snippets/csharp/language-reference/tokens/string-interpolation.cs#2)]

## <a name="special-characters"></a>特殊字元

若要在插入字串所產生的文字中包含大括弧 "{" 或 "}"，請使用雙大括弧 "{{" 或 "}}"。 如需詳細資訊，請參閱[逸出大括號](../../../standard/base-types/composite-formatting.md#escaping-braces)。

因為冒號 (":")　在內插補點運算式項目中具有特殊意義，為了在內插補點運算式中使用[條件運算子](../operators/conditional-operator.md)，請用括弧括住運算式。

下列範例示範如何在結果字串中包含大括弧以及如何在內插補點運算式中使用條件運算子：

[!code-csharp-interactive[example with ternary conditional operator](~/samples/snippets/csharp/language-reference/tokens/string-interpolation.cs#3)]

逐字插入字串以 `$` 字元為開頭，後面接著 `@` 字元。 如需逐字字串的詳細資訊，請參閱[字串](../keywords/string.md)和[逐字識別碼](verbatim.md)主題。

> [!NOTE]
> `$` 語彙基元必須出現在逐字內插字串中的 `@` 語彙基元之前。

## <a name="implicit-conversions-and-specifying-iformatprovider-implementation"></a>隱含轉換和指定 `IFormatProvider` 實作

有三個來自插入字串的隱含轉換：

1. 將插入字串轉換成插入字串解析結果的 <xref:System.String> 執行個體，且內插補點運算式項目取代為其結果的格式正確字串表示。 這項轉換會使用目前文化特性。

1. 將插入字串轉換成 <xref:System.FormattableString> 執行個體，以代表複合格式字串，並將運算式結果格式化。 那可讓您從單一 <xref:System.FormattableString> 執行個體建立多個具有特定文化特性內容的結果字串。 若要執行此工作，請呼叫下列的其中一個方法：

      - 產生 <xref:System.Globalization.CultureInfo.CurrentCulture> 的結果字串的 <xref:System.FormattableString.ToString> 多載。
      - 產生 <xref:System.Globalization.CultureInfo.InvariantCulture> 的結果字串的 <xref:System.FormattableString.Invariant%2A> 方法。
      - 產生指定文化特性的結果字串的 <xref:System.FormattableString.ToString(System.IFormatProvider)> 方法。

    您也可以使用 <xref:System.FormattableString.ToString(System.IFormatProvider)> 方法，提供 <xref:System.IFormatProvider> 介面的使用者定義實作以支援自訂格式。 如需詳細資訊，請參閱[使用 ICustomFormatter 的自訂格式](../../../standard/base-types/formatting-types.md#custom-formatting-with-icustomformatter)。

1. 將插入字串轉換成 <xref:System.IFormattable> 執行個體，也可讓您從單一 <xref:System.IFormattable> 執行個體建立多個具有特定文化特性內容的結果字串。

下列範例會使用隱含轉換成 <xref:System.FormattableString>，來建立文化特性特定結果字串：

[!code-csharp-interactive[create culture-specific result strings](~/samples/snippets/csharp/language-reference/tokens/string-interpolation.cs#4)]

## <a name="additional-resources"></a>其他資源

如果您是字串插補的新手，請參閱 [C# 中的字串插補](../../tutorials/exploration/interpolated-strings.yml)互動式教學課程。 您也可以查看其他教學課程：[C# 中的字串插值](../../tutorials/string-interpolation.md)，其中示範如何使用內插字串來產生格式化的字串。

## <a name="compilation-of-interpolated-strings"></a>內插字串的編譯

如果內插字串的類型為 `string`，它通常會轉換成 <xref:System.String.Format%2A?displayProperty=nameWithType> 方法呼叫。 如果分析的行為相當於串連，編譯器可以將 <xref:System.String.Format%2A?displayProperty=nameWithType> 取代為 <xref:System.String.Concat%2A?displayProperty=nameWithType>。

如果內插字串的類型為 <xref:System.IFormattable> 或 <xref:System.FormattableString>，編譯器會產生 <xref:System.Runtime.CompilerServices.FormattableStringFactory.Create%2A?displayProperty=nameWithType> 方法的呼叫。

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[內插字串](~/_csharplang/spec/expressions.md#interpolated-strings)一節。

## <a name="see-also"></a>另請參閱

- <xref:System.String.Format%2A?displayProperty=nameWithType>
- <xref:System.FormattableString?displayProperty=nameWithType>
- <xref:System.IFormattable?displayProperty=nameWithType>
- [複合格式](../../../standard/base-types/composite-formatting.md)
- [格式化數值結果表](../keywords/formatting-numeric-results-table.md)
- [字串](../../programming-guide/strings/index.md)
- [C# 程式設計指南](../../programming-guide/index.md)
- [C# 特殊字元](index.md)
- [C# 參考](../index.md)
