---
title: 明確數值轉換表 - C# 參考
ms.custom: seodec18
ms.date: 09/06/2018
helpviewer_keywords:
- conversions [C#], explicit numeric
- numeric conversions [C#], explicit
- explicit numeric conversion [C#]
- numeric data types [C#]
- types [C#], explicit numeric conversions
- type conversion [C#], explicit numeric
ms.assetid: f3bb9e76-6b92-4df7-bc36-f866c24e1dfd
ms.openlocfilehash: d1533872850a953a38800aaeac85b9e6e565d374
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2019
ms.locfileid: "67661373"
---
# <a name="explicit-numeric-conversions-table-c-reference"></a>明確數值轉換表 (C# 參考)

下表顯示 .NET 數字類型間預先定義的明確轉換不含有[隱含轉換](implicit-numeric-conversions-table.md)。

|從|以|  
|----------|--------|  
|[sbyte](../builtin-types/integral-numeric-types.md)|`byte`、`ushort`、`uint`、`ulong` 或 `char`|  
|[byte](../builtin-types/integral-numeric-types.md)|`sbyte` 或 `char`|  
|[short](../builtin-types/integral-numeric-types.md)|`sbyte`、`byte`、`ushort`、`uint`、`ulong` 或 `char`|  
|[ushort](../builtin-types/integral-numeric-types.md)|`sbyte`、`byte`、`short` 或 `char`|  
|[int](../builtin-types/integral-numeric-types.md)|`sbyte`、`byte`、`short`、`ushort`、`uint`、`ulong` 或 `char`。|  
|[uint](../builtin-types/integral-numeric-types.md)|`sbyte`、`byte`、`short`、`ushort`、`int` 或 `char`|  
|[long](../builtin-types/integral-numeric-types.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`ulong` 或 `char`|  
|[ulong](../builtin-types/integral-numeric-types.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long` 或 `char`|  
|[char](char.md)|`sbyte`、 `byte`或 `short`|  
|[float](../builtin-types/floating-point-numeric-types.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char` 或 `decimal`。|  
|[double](../builtin-types/floating-point-numeric-types.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float` 或 `decimal`。|  
|[decimal](../builtin-types/floating-point-numeric-types.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float` 或 `double`。|  
  
## <a name="remarks"></a>備註  
  
- 明確的數值轉換可能會造成有效位數遺失或導致擲回例外狀況，通常為 <xref:System.OverflowException>。  

- 將整數型別的值轉換為另一個整數型別時，結果取決於溢位[檢查內容](checked-and-unchecked.md)。 在已檢查的內容中，如果來源值在目標類型的範圍內，轉換將會成功。 否則會擲回 <xref:System.OverflowException>。 在未檢查的內容中，轉換一律會成功，並按照如下所示繼續進行：

  - 如果來源類型大於目的地類型，會藉由捨棄其「額外」最高有效位元，來截斷來源值。 然後會將結果視為目標類型的值。

  - 如果來源類型小於目標類型，則來源值可以是正負號擴充或零擴充，以使其與目標類型的大小相同。 如果來源類型帶正負號，則會使用正負號擴充；如果來源類型不帶正負號，則會使用零擴充。 然後會將結果視為目標類型的值。

  - 如果來源類型與目標類型的大小相同，則來源值將視為目標類型的值。
  
- 當您將 `decimal` 值轉換為整數型別時，這個值會捨入到最接近整數值的零。 如果產生的整數值超出目的地類型的範圍，就會擲回 <xref:System.OverflowException>。  
  
- 當您將 `double` 或 `float` 值轉換為整數型別時，這個值會往零的方向捨入到最接近的整數值。 如果產生的整數值超出目的地類型的範圍，結果隨溢位[檢查內容](checked-and-unchecked.md)而異。 在已檢查的內容中會擲回 <xref:System.OverflowException>，而在未經檢查的內容中，結果是目的地類型的未指定值。  
  
- 當您將 `double` 轉換成 `float` 時，`double` 值會捨入到最接近 `float` 值。 如果 `double` 值太小或太大以致不符合目的地類型，結果會是零或無限大。  
  
- 當您將 `float` 或 `double` 轉換成 `decimal` 時，來源值會轉換成 `decimal` 表示，必要時捨入到最接近第 28 個小數位數後的數字。 視來源值的值而定，可能會發生下列一種結果：  

  - 如果來源值太小無法以 `decimal` 表示，結果就會變成零。  

  - 如果來源值是 NaN (不是數字)、無限大或太大，無法以 `decimal` 表示，就會擲回 <xref:System.OverflowException>。  
  
- 當您將 `decimal` 轉換成 `float` 或 `double` 時，`decimal` 值會捨入到最接近 `double` 或 `float` 值。  
  
 如需明確轉換的詳細資訊，請參閱 [C# 語言規格](../language-specification/index.md)的[明確轉換](~/_csharplang/spec/conversions.md#explicit-conversions)一節。
  
## <a name="see-also"></a>另請參閱

- [C# 參考](../index.md)
- [轉換和類型轉換](../../programming-guide/types/casting-and-type-conversions.md)
- [() 運算子](../operators/type-testing-and-conversion-operators.md#cast-operator-)
- [整數型別](../builtin-types/integral-numeric-types.md)
- [浮點數類型表](../builtin-types/floating-point-numeric-types.md)
- [內建型別表](built-in-types-table.md)
- [隱含數值轉換表](implicit-numeric-conversions-table.md)
