---
title: 作法：尋找正前面的同層級項目 (XPath-LINQ to XML) (C#)
ms.date: 07/20/2015
ms.assetid: 74c06201-0b1b-4b5e-b3ac-0092980614e6
ms.openlocfilehash: 7d1d49f262b13f769ab1d28de8b75d214d8abe64
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66486722"
---
# <a name="how-to-find-the-immediate-preceding-sibling-xpath-linq-to-xml-c"></a>作法：尋找正前面的同層級項目 (XPath-LINQ to XML) (C#)
有時候您會想要尋找節點正前面的同層級。 由於前面同層級座標軸的位置性述詞語意 (Semantics) 在 XPath 中與 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 相反的這個差異，這是其中一個更有趣的比較。  
  
## <a name="example"></a>範例  
 在這個範例中，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查詢會使用 <xref:System.Linq.Enumerable.Last%2A> 運算子，尋找集合中由 <xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A> 傳回的最後一個節點。 相較之下，XPath 運算式會使用述詞搭配 1 這個值來尋找正前面的項目。  
  
```csharp  
XElement root = XElement.Parse(  
    @"<Root>  
    <Child1/>  
    <Child2/>  
    <Child3/>  
    <Child4/>  
</Root>");  
XElement child4 = root.Element("Child4");  
  
// LINQ to XML query  
XElement el1 =  
    child4  
    .ElementsBeforeSelf()  
    .Last();  
  
// XPath expression  
XElement el2 =  
    ((IEnumerable)child4  
                 .XPathEvaluate("preceding-sibling::*[1]"))  
                 .Cast<XElement>()  
                 .First();  
  
if (el1 == el2)  
    Console.WriteLine("Results are identical");  
else  
    Console.WriteLine("Results differ");  
Console.WriteLine(el1);  
```  
  
 這個範例會產生下列輸出：  
  
```  
Results are identical  
<Child3 />  
```  
