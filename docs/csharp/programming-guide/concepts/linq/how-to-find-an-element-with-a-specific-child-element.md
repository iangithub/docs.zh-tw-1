---
title: 作法：尋找具有特定子項目的項目 (C#)
ms.date: 07/20/2015
ms.assetid: 00cf5555-374e-4369-bf93-7bd2e7f21db3
ms.openlocfilehash: 71068774b93581fdd82a0fe57651bc7780ca1ef1
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66485566"
---
# <a name="how-to-find-an-element-with-a-specific-child-element-c"></a>作法：尋找具有特定子項目的項目 (C#)
本主題顯示如何利用特定的值尋找具有子項目的特定項目。  
  
## <a name="example"></a>範例  
 此範例會利用 "Examp2.EXE" 這個值，尋找具有 `Test` 子項目的 `CommandLine` 項目。  
  
 此範例使用下列 XML 文件：[XML 範例檔：測試組態 (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-test-configuration-linq-to-xml.md)。  
  
```csharp  
XElement root = XElement.Load("TestConfig.xml");  
IEnumerable<XElement> tests =  
    from el in root.Elements("Test")  
    where (string)el.Element("CommandLine") == "Examp2.EXE"  
    select el;  
foreach (XElement el in tests)  
    Console.WriteLine((string)el.Attribute("TestId"));  
```  
  
 此程式碼會產生下列輸出：  
  
```  
0002  
0006  
```  
  
## <a name="example"></a>範例  
 下列範例顯示命名空間中之 XML 的相同查詢。 如需詳細資訊，請參閱[處理 XML 命名空間 (C#)](../../../../csharp/programming-guide/concepts/linq/namespaces-overview-linq-to-xml.md)。  
  
 此範例使用下列 XML 文件：[XML 範例檔：測試命名空間中的組態](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-test-configuration-in-a-namespace1.md)。  
  
```csharp  
XElement root = XElement.Load("TestConfigInNamespace.xml");  
XNamespace ad = "http://www.adatum.com";  
IEnumerable<XElement> tests =  
    from el in root.Elements(ad + "Test")  
    where (string)el.Element(ad + "CommandLine") == "Examp2.EXE"  
    select el;  
foreach (XElement el in tests)  
    Console.WriteLine((string)el.Attribute("TestId"));  
```  
  
 此程式碼會產生下列輸出：  
  
```  
0002  
0006  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Xml.Linq.XElement.Attribute%2A>
- <xref:System.Xml.Linq.XContainer.Elements%2A>
- [標準查詢運算子概觀 (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [投影作業 (C#)](../../../../csharp/programming-guide/concepts/linq/projection-operations.md)
