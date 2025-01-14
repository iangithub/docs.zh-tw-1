---
title: ADO.NET 資料集
ms.date: 03/30/2017
ms.assetid: 82b641bb-6001-4512-bf1a-2830acdd92ab
ms.openlocfilehash: da6fb7bbe82e37787615518fa74a0d84bf95758f
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2019
ms.locfileid: "67504266"
---
# <a name="adonet-datasets"></a>ADO.NET 資料集
<xref:System.Data.DataSet>物件是支援的核心已中斷連線，分散式資料案例的 ADO.NET。 **資料集**是提供與資料來源無關的一致性關聯式程式設計模型的資料常駐記憶體表示法。 它可與多個不同的資料來源一起使用、與 XML 資料一起使用，或管理應用程式的本機資料。 **資料集**表示一組完整的資料，包括相關的資料表、 條件約束及資料表間的關聯性。 如下圖所示**資料集**物件模型。  
  
 ![ADO.Net 圖形](../../../../docs/framework/data/adonet/media/ado-1-bpuedev11.png "ado_1_bpuedev11")  
DataSet 物件模型  
  
 在方法與物件**資料集**與關聯式資料庫模型中一致。  
  
 **資料集**也可以保存及重新載入其內容為 XML，以及其與 XML 結構描述定義語言 (XSD) 結構描述的結構描述。 如需詳細資訊，請參閱[在 DataSet 中使用 XML](../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)。  
  
## <a name="the-datatablecollection"></a>DataTableCollection  
 ADO.NET**資料集**包含零個或多個資料表所表示的集合<xref:System.Data.DataTable>物件。 <xref:System.Data.DataTableCollection>包含所有**DataTable**中的物件**DataSet**。  
  
 A **DataTable**中所定義<xref:System.Data>命名空間和表示記憶體常駐資料的單一資料表。 它包含由 <xref:System.Data.DataColumnCollection> 所表示的資料行集合，以及由 <xref:System.Data.ConstraintCollection> 所表示的條件約束，它們共同定義資料表的結構描述。 A **DataTable**也會包含所代表的資料列集合<xref:System.Data.DataRowCollection>，其中包含資料表中的資料。 連同其目前狀態一起，<xref:System.Data.DataRow> 還保留其目前及原始版本，以識別儲存在資料列中之值的變更。  
  
## <a name="the-dataview-class"></a>DataView 類別  
 <xref:System.Data.DataView> 允許您為儲存在 <xref:System.Data.DataTable> 內的資料建立不同的檢視，這是資料繫結應用程式中常用的功能。 您可以使用 <xref:System.Data.DataView>，以不同排序次序公開 (Expose) 資料表中的資料，而且可以按照資料列狀態或根據篩選條件運算式來篩選資料。 如需詳細資訊，請參閱 < [Dataview](../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)。  
  
## <a name="the-datarelationcollection"></a>DataRelationCollection  
 A**資料集**包含在關聯性及其<xref:System.Data.DataRelationCollection>物件。 關聯性，由<xref:System.Data.DataRelation>物件，將資料列，其中一**DataTable**在另一個資料列**DataTable**。 關聯性類似於在關聯式資料庫中，主索引鍵資料行與外部索引鍵資料行之間存在的聯結路徑。 A **DataRelation**識別的兩個資料表中的相符資料行**DataSet**。  
  
 關聯性可讓從一個資料表瀏覽到另一個**資料集**。 基本項目**DataRelation**是關聯性名稱、 相關，資料表的名稱和相關的資料行，每個資料表中。 藉由將 <xref:System.Data.DataColumn> 物件的陣列指定為索引鍵資料行，可在每個資料表中建立多個資料行的關聯性。 當您將加入的關聯性<xref:System.Data.DataRelationCollection>，您可以選擇性地加入**UniqueKeyConstraint**並**ForeignKeyConstraint**變更相關的資料行時，強制執行完整性條件約束值。  
  
 如需詳細資訊，請參閱 <<c0> [ 新增 Datarelation](../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-datarelations.md)。  
  
## <a name="xml"></a>XML  
 您可以填寫**資料集**從 XML 資料流或文件。 您可以使用 XML 資料流或文件提供給**資料集**資料、 結構描述資訊，或兩者。 從 XML 資料流或文件所提供的資訊可以結合現有的資料或結構描述資訊中已存在**資料集**。 如需詳細資訊，請參閱[在 DataSet 中使用 XML](../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)。  
  
## <a name="extendedproperties"></a>ExtendedProperties  
 **資料集**， **DataTable**，並**DataColumn**都**ExtendedProperties**屬性。 **ExtendedProperties**已**PropertyCollection**您可以在其中放置自訂資訊，例如 SELECT 陳述式，用來產生結果集或產生資料時的時間。 **ExtendedProperties**集合永續存在的結構描述資訊**DataSet**。  
  
## <a name="linq-to-dataset"></a>LINQ to DataSet  
 LINQ to DataSet 提供語言整合查詢儲存在 DataSet 的中斷連接資料的功能。 LINQ to DataSet 會使用標準[!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]語法，並使用 Visual Studio IDE 時提供編譯時間語法檢查、 靜態型別和 IntelliSense 支援。  
  
 如需詳細資訊，請參閱 [LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset.md)。  
  
## <a name="see-also"></a>另請參閱

- [ADO.NET 概觀](../../../../docs/framework/data/adonet/ado-net-overview.md)
- [DataSet、DataTable 和 DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)
- [在 ADO.NET 中擷取和修改資料](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)
- [ADO.NET Managed 提供者和 DataSet 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=217917)
