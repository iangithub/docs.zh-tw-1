---
title: 作法：投影匿名型別 (C#)
ms.date: 07/20/2015
ms.assetid: 5cb9be13-5ac4-4373-a034-b3520a5b2dec
ms.openlocfilehash: 68b008d70474c927a7911dc77e60afb634035b77
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66485135"
---
# <a name="how-to-project-an-anonymous-type-c"></a>作法：投影匿名型別 (C#)
在某些情況下，即使您知道您只會短期使用新型別，您可能還是想要將查詢規劃為該型別。 建立新型別只用於這個規劃太費工。 在此情況下，較有效率的方法為規劃匿名型別。 匿名型別可讓您定義類別，然後宣告並初始化該類別的物件，而不用提供類別一個名稱。  
  
 匿名型別為「元組」  之數學概念的 C# 實作。 數學術語「Tuple」源自於 single、double、triple、quadruple、quintuple、n-tuple 序列。 這表示有限的物件順序，每個都有特定的型別。 有時候，這稱為成對的名稱/值清單。 例如，[XML 範例檔：典型訂購單 (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-typical-purchase-order-linq-to-xml-1.md) XML 文件中的地址內容可能如下表示：  
  
```  
Name: Ellen Adams  
Street: 123 Maple Street  
City: Mill Valley  
State: CA  
Zip: 90952  
Country: USA  
```  
  
 當您建立匿名型別的執行個體時，將它視為建立順序 n 的 Tuple 比較方法。 如果您撰寫可在 `select` 子句中建立 Tuple 的查詢，該查詢會傳回 Tuple 的 `IEnumerable`。  
  
## <a name="example"></a>範例  
 在這個範例中，`select` 子句會規劃匿名型別。 然後，此範例會使用 `var` 來建立 `IEnumerable` 物件。 在 `foreach` 迴圈中，反覆運算變數會變成在查詢運算式中建立之匿名型別的執行個體。  
  
 此範例使用下列 XML 文件：[XML 範例檔：客戶和訂單 (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml-2.md)。  
  
```csharp  
XElement custOrd = XElement.Load("CustomersOrders.xml");  
var custList =  
    from el in custOrd.Element("Customers").Elements("Customer")  
    select new {  
        CustomerID = (string)el.Attribute("CustomerID"),  
        CompanyName = (string)el.Element("CompanyName"),  
        ContactName = (string)el.Element("ContactName")  
    };  
foreach (var cust in custList)  
    Console.WriteLine("{0}:{1}:{2}", cust.CustomerID, cust.CompanyName, cust.ContactName);  
```  
  
 此程式碼會產生下列輸出：  
  
```  
GREAL:Great Lakes Food Market:Howard Snyder  
HUNGC:Hungry Coyote Import Store:Yoshi Latimer  
LAZYK:Lazy K Kountry Store:John Steel  
LETSS:Let's Stop N Shop:Jaime Yorres  
```  
  