---
title: 現用模式
description: 了解如何使用作用中的模式來定義細分輸入的資料中的具名資料分割F#程式設計語言。
ms.date: 05/16/2016
ms.openlocfilehash: 25ab255574390d3761fe788aeb413c8ee04fda2a
ms.sourcegitcommit: d8ebe0ee198f5d38387a80ba50f395386779334f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66690417"
---
# <a name="active-patterns"></a>現用模式

*作用中的模式*可讓您定義細分輸入的資料的具名資料分割，以便您可以使用這些名稱的模式比對運算式，就像您一樣的已區分的聯集。 您可以使用作用中的模式，以自訂方式分解每個部分的資料。

## <a name="syntax"></a>語法

```fsharp
// Active pattern of one choice.
let (|identifier|) [arguments] valueToMatch= expression

// Active Pattern with multiple choices.
// Uses a FSharp.Core.Choice<_,...,_> based on the number of case names. In F#, the limitation n <= 7 applies.
let (|identifer1|identifier2|...|) valueToMatch = expression

// Partial active pattern definition.
// Uses a FSharp.Core.option<_> to represent if the type is satisfied at the call site.
let (|identifier|_|) [arguments ] valueToMatch = expression
```

## <a name="remarks"></a>備註

在先前語法中的識別項是名稱由輸入資料的資料分割*引數*，或者，換句話說，一組引數的所有值的子集的名稱。 在使用中模式定義中可以有最多七個資料分割。 *運算式*描述用來將資料分解成表單。 您可以使用中模式，定義來定義規則，來判斷哪一個具名的資料分割的引數屬於所提供的值。 (| 和 |) 符號指*香蕉*並建立此類型的 let 繫結的函式會呼叫*作用中的辨識器*。

例如，請考慮下列的使用中模式，以引數。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5001.fs)]

您可以使用中模式的模式比對運算式，如下列範例所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5002.fs)]

此程式的輸出如下所示：

```
7 is odd
11 is odd
32 is even
```

現用模式的另一個用途是將分解以多種方式，例如當相同的基礎資料有可能的各種表示相互轉換的資料類型。 比方說，`Color`物件無法分解成 RGB 或 HSB 表示法。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5003.fs)]

上述程式的輸出如下所示：

```
Red
 Red: 255 Green: 0 Blue: 0
 Hue: 360.000000 Saturation: 1.000000 Brightness: 0.500000
Black
 Red: 0 Green: 0 Blue: 0
 Hue: 0.000000 Saturation: 0.000000 Brightness: 0.000000
White
 Red: 255 Green: 255 Blue: 255
 Hue: 0.000000 Saturation: 0.000000 Brightness: 1.000000
Gray
 Red: 128 Green: 128 Blue: 128
 Hue: 0.000000 Saturation: 0.000000 Brightness: 0.501961
BlanchedAlmond
 Red: 255 Green: 235 Blue: 205
 Hue: 36.000000 Saturation: 1.000000 Brightness: 0.901961
```

在組合，使用作用中模式的這兩種方式可讓您將資料分割將資料分解為適當的表單並最方便的計算表單中的適當資料上執行適當的計算。

產生的模式比對運算式可讓以便利的方式非常清楚易讀、 可大幅簡化的潛在複雜分支與資料分析程式碼所寫入的資料。

## <a name="partial-active-patterns"></a>部分作用中的模式

有時候，您需要資料分割的輸入空間的組件。 在此情況下，您撰寫一組部分模式，其中符合某些輸入，但無法符合其他輸入。 永遠不會產生值的使用中模式稱為*部分作用中的模式*; 它們有傳回值，選項類型。 若要定義部分的使用中模式，您可以使用萬用字元 (\_) 的內部香蕉的模式清單結尾。 下列程式碼說明如何使用部分中的模式。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5004.fs)]

上述範例的輸出如下所示：

```
1.100000 : Floating point
0 : Integer
0.000000 : Floating point
10 : Integer
Something else : Not matched.
```

在使用部分作用中的模式時，有時個別選擇可以是脫離或互斥，但它們不一定要是。 在下列範例中，模式平方和 Cube 的模式不是脫離的因為一些數字是平方和 cube，例如 64。 下列程式會使用 AND 模式結合的正方形和立方體的模式。 它印出所有的整數，最多 1000 個的同時平方和 cube，以及會只有 cube。 

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5005.fs)]

其輸出如下：

```
1 is a cube and a square
8 is a cube
27 is a cube
64 is a cube and a square
125 is a cube
216 is a cube
343 is a cube
512 is a cube
729 is a cube and a square
1000 is a cube
```

## <a name="parameterized-active-patterns"></a>參數化現用模式

作用中的模式一定會採用要比對的項目至少一個引數，但它們可能需要額外的引數，在此情況下名稱*參數化現用模式*套用。 其他引數可讓特製化的一般模式。 比方說，作用中的模式使用規則運算式剖析字串通常包含規則運算式做為額外的參數，如下列程式碼，這也會使用部分的現用模式`Integer`先前的程式碼範例中所定義。 在此範例中，使用規則運算式進行各種不同的日期格式的字串會提供給自訂一般 ParseRegex 現用模式。 整數中的模式用來比對的字串轉換成可以傳遞給 DateTime 建構函式的整數。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5006.fs)]

先前的程式碼的輸出如下所示：

```
12/22/2008 12:00:00 AM 1/1/2009 12:00:00 AM 1/15/2008 12:00:00 AM 12/28/1995 12:00:00 AM
```

作用中的模式不只限於模式比對運算式，您也可以使用它們可讓繫結上。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5007.fs)]

先前的程式碼的輸出如下所示：

```
Hello, random citizen!
Hello, George!
```

## <a name="see-also"></a>另請參閱

- [F# 語言參考](index.md)
- [比對運算式](match-expressions.md)
