---
title: 匿名的記錄
description: 了解如何使用建構，並使用匿名的記錄，可協助進行資料操作語言功能。
ms.date: 06/12/2019
ms.openlocfilehash: e576210d4fb76ccfd09f8feb157ef4542aa94ccf
ms.sourcegitcommit: c4dfe37032c64a1fba2cc3d5947550d79f95e3b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/13/2019
ms.locfileid: "67041802"
---
# <a name="anonymous-records"></a>匿名的記錄

匿名的記錄是不需要使用前宣告的具名值的簡單彙總。 您可以將它們宣告為結構或參考類型上。 它們是預設的參考型別。

## <a name="syntax"></a>語法

下列範例示範匿名記錄語法。 項目分隔為`[item]`是選擇性的。

```fsharp
// Construct an anonymous record
let value-name = [struct] {| Label1: Type1; Label2: Type2; ...|}

// Use an anonymous record as a type parameter
let value-name = Type-Name<[struct] {| Label1: Type1; Label2: Type2; ...|}>

// Define a parameter with an anonymous record as input
let function-name (arg-name: [struct] {| Label1: Type1; Label2: Type2; ...|}) ...
```

## <a name="basic-usage"></a>基本使用方式

匿名記錄最適合想像成F#記錄不必具現化之前宣告的類型。

例如，這裡您可以使用函式互動的方式，會產生匿名的記錄：

```fsharp

open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let r = 2.0
let stats = getCircleStats r
printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
    r stats.Diameter stats.Area stats.Circumference
```

下列範例會在與前一個`printCircleStats`採用匿名的記錄，做為輸入的函式：

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let printCircleStats r (stats: {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

呼叫`printCircleStats`與任何匿名的記錄型別沒有相同的 「 圖形 」，因為在輸入型別將無法編譯：

```fsharp
printCircleStats r {| Diameter = 2.0; Area = 4.0; MyCircumference = 12.566371 |}
// Two anonymous record types have mismatched sets of field names
// '["Area"; "Circumference"; "Diameter"]' and '["Area"; "Diameter"; "MyCircumference"]'
```

## <a name="struct-anonymous-records"></a>匿名結構的記錄

匿名記錄也可以定義與選擇性結構`struct`關鍵字。 下列範例會擴大上一個產生和取用結構匿名的記錄：

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    // Note that the keyword comes before the '{| |}' brace pair
    struct {| Area = a; Circumference = c; Diameter = d |}

// the 'struct' keyword also comes before the '{| |}' brace pair when declaring the parameter type
let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

### <a name="structness-inference"></a>Structness 推斷

結構匿名記錄也可讓 「 structness 推斷 」，您不需要指定`struct`呼叫位置的關鍵字。 在此範例中，您 elide`struct`關鍵字時呼叫`printCircleStats`:

```fsharp

let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

printCircleStats r {| Area = 4.0; Circumference = 12.6; Diameter = 12.6 |}
```

反向模式-指定`struct`時輸入的類型不是結構匿名的記錄集，將無法編譯。

## <a name="embedding-anonymous-records-within-other-types"></a>內嵌在其他類型的匿名資料錄

它適合用來宣告[差別聯集](discriminated-unions.md)大小寫不會有記錄。 但是，如果相同的已區分的聯集類型的記錄中的資料，您必須定義所有型別為相互遞迴。 使用匿名的記錄，可避免這項限制。 以下是範例類型和函式該模式會透過它比對：

```fsharp
type FullName = { FirstName: string; LastName: string }

// Note that using a named for Manager and Executive would require mutually recursive definitions.
type Employee =
    | Engineer of FullName
    | Manager of {| Name: FullName; Reports: Employee list |}
    | Executive of {| Name: FullName; Reports: Employee list; Assistant: Employee |}

let getFirstName e =
    match e with
    | Engineer fullName -> fullName.FirstName
    | Manager m -> m.Name.FirstName
    | Executive ex -> ex.Name.FirstName
```

## <a name="copy-and-update-expressions"></a>複製並更新運算式

匿名記錄支援建構函式與[複製並更新運算式](copy-and-update-record-expressions.md)。 例如，以下是如何建構複製現有的匿名資料錄的新執行個體資料：

```fsharp
let data = {| X = 1; Y = 2 |}
let data' = {| data with Y = 3 |}
```

不過，與不同的具名記錄，是匿名的記錄可讓您建構完全不同的形式複製與並更新運算式。 下列範例會採用前一個範例相同的匿名記錄，並將它擴充到新的匿名記錄：

```fsharp
let data = {| X = 1; Y = 2 |}
let expandedData = {| data with Z = 3 |} // Gives {| X=1; Y=2; Z=3 |}
```

此外，也可以建構匿名的記錄，從執行個體的具名記錄：

```fsharp
type R = { X: int }
let data = { X = 1 }
let data' = {| data with Y = 2 |} // Gives {| X=1; Y=2 |}
```

您也可以在參考和結構的匿名記錄來回複製資料：

```fsharp
// Copy data from a reference record into a struct anonymous record
type R1 = { X: int }
let r1 = { X = 1 }

let data1 = struct {| r1 with Y = 1 |}

// Copy data from a struct record into a reference anonymous record
[<Struct>]
type R2 = { X: int }
let r2 = { X = 1 }

let data2 = {| r1 with Y = 1 |}

// Copy the reference anonymous record data into a struct anonymous record
let data3 = struct {| data2 with Z = r2.X |}
```

## <a name="properties-of-anonymous-records"></a>匿名記錄的屬性

匿名記錄都有許多是必要項目完全了解如何使用的特性。

### <a name="anonymous-records-are-nominal"></a>匿名記錄是名義上

匿名記錄[名義型別](https://en.wikipedia.org/wiki/Nominal_type_system)。 它們是最佳的想法，因為名為[記錄](records.md)類型 （也就是也名義） 不需要預付的宣告。

請考慮下列範例使用兩個匿名記錄宣告：

```fsharp
let x = {| X = 1 |}
let y = {| Y = 1 |}
```

`x`和`y`值具有不同的類型，並與彼此不相容。 它們不是可比較相等，故無法比較。 為了說明這點，認為是具名的記錄相等的：

```fsharp
type X = { X: int }
type Y = { Y: int }

let x = { X = 1 }
let y = { Y = 1 }
```

沒有任何關於匿名記錄有關類型的對應項或比較時，相較於其具名的記錄對等項目本質上不同。

### <a name="anonymous-records-use-structural-equality-and-comparison"></a>匿名的記錄，請使用結構化相等和比較

記錄類型，例如匿名的記錄是結構上相等和比較。 這只是如果所有構成類型都支援相等和比較，例如具有 record 類型則為 true。 若要支援等號比較時，兩個匿名的記錄必須相同的 「 圖形 」。

```fsharp
{| a = 1+1 |} = {| a = 2 |} // true
{| a = 1+1 |} > {| a = 1 |} // true

// error FS0001: Two anonymous record types have mismatched sets of field names '["a"]' and '["a"; "b"]'
{| a = 1 + 1 |} = {| a = 2;  b = 1|}
```

### <a name="anonymous-records-are-serializable"></a>匿名記錄都是可序列化

正如同您可以使用具名的記錄，您可以將序列化匿名的記錄。 以下是範例使用[Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/):

```fsharp
open Newtonsoft.Json

let phillip = {| name="Phillip"; age=28 |}
JsonConvert.SerializeObject(phillip)

let phillip = JsonConvert.DeserializeObject<{|name: string; age: int|}>(str)
printfn "Name: %s Age: %d" phillip.name phillip.age
```

匿名記錄可用於透過網路而不需要定義您序列化/還原序列化的型別最前面位置的網域傳送輕量的資料。

### <a name="anonymous-records-interoperate-with-c-anonymous-types"></a>匿名的記錄與交互操作C#匿名型別

您可使用.NET API，需要使用[C#匿名型別](../../csharp/programming-guide/classes-and-structs/anonymous-types.md)。 C#匿名型別是 trivial 使用匿名的記錄與交互操作。 下列範例示範如何使用匿名的記錄來呼叫[LINQ](../../csharp/programming-guide/concepts/linq/index.md)需要匿名型別多載：

```fsharp
open System.Linq

let names = [ "Ana"; "Felipe"; "Emilia"]
let nameGrouping = names.Select(fun n -> {| Name = n; FirstLetter = n.[0] |})
for ng in nameGrouping do
    printfn "%s has first letter %c" ng.Name ng.FirstLetter
```

有許多用於整個.NET 需要傳遞匿名類型中使用之其他 Api。 匿名的記錄會加以使用的工具。

## <a name="limitations"></a>限制

匿名記錄其使用方式中有一些限制。 有些是將它們的設計原本就，但有些則是適合變更。

### <a name="limitations-with-pattern-matching"></a>模式比對的限制

匿名記錄並不支援模式比對，不同於已命名的記錄。 有三個原因：

1. 模式必須以帳戶為匿名的記錄，不同於已命名的記錄類型的每個欄位。 這是因為匿名的記錄不支援結構化的子型別，它們名義型別。
2. (1)，因為沒有任何能夠在模式比對運算式中，有其他模式因為每個不同的模式會代表不同匿名的記錄類型。
3. (3)，因為任何匿名的記錄模式會比使用 「 點 」 標記法的更多詳細資料。

沒有開啟的語言建議[允許在模式比對限制內容](https://github.com/fsharp/fslang-suggestions/issues/713)。

### <a name="limitations-with-mutability"></a>可變動性的限制

不是目前可以定義具有匿名記錄`mutable`資料。 沒有[開啟語言建議](https://github.com/fsharp/fslang-suggestions/issues/732)允許可變動的資料。

### <a name="limitations-with-struct-anonymous-records"></a>具有匿名結構的記錄限制

不可以宣告結構匿名的記錄，當做`IsByRefLike`或`IsReadOnly`。 沒有[開啟語言建議](https://github.com/fsharp/fslang-suggestions/issues/712)若要針對`IsByRefLike`和`IsReadOnly`匿名的記錄。
