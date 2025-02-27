---
title: 查詢結果
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: bcd7b699-4e50-4523-8c33-2f54a103d94e
ms.openlocfilehash: 165fb1524daa781c29037bf1c9cb2b3013504177
ms.sourcegitcommit: b5c59eaaf8bf48ef3ec259f228cb328d6d4c0ceb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2019
ms.locfileid: "67539747"
---
# <a name="query-results"></a>查詢結果
LINQ to Entities 查詢會轉換成命令樹，並執行之後，查詢結果會通常會傳回做為下列其中一項：  
  
- 零個或多個具型別實體物件的集合，或是概念模型中複雜類型的投影。  
  
- 概念模型支援的 CLR 型別。  
  
- 內嵌集合。  
  
- 匿名型別。  
  
 針對資料來源執行查詢之後，便會將結果具體化成為 CLR 型別，然後傳回用戶端。 所有物件具體化都是由 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 執行。 因為無法在 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 與 CLR 之間對應而產生的任何錯誤，都將導致物件具體化期間擲回例外狀況。  
  
 如果查詢執行傳回基本概念模型型別，結果將由獨立且從 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 中斷連接的 CLR 型別構成。 但是，如果查詢傳回以 <xref:System.Data.Objects.ObjectQuery%601> 表示的具型別實體物件集合，這些型別將會由此內容物件追蹤。 （例如子/父集合、 變更追蹤、 多型，等等） 的所有物件行為都會如同[!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)]。 這項功能可以依照 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 中所定義的能力使用。 如需詳細資訊，請參閱 <<c0> [ 使用物件](../../../../../../docs/framework/data/adonet/ef/working-with-objects.md)。  
  
 從查詢傳回的結構型別 (例如匿名型別和可為 null 的複雜類型) 可能是 `null` 值。 所傳回實體的 <xref:System.Data.Objects.DataClasses.EntityCollection%601> 屬性也可能是 `null` 值。 投影 `null` 值之實體的屬性集合就可能產生這種情況，例如在沒有項目的 <xref:System.Linq.Queryable.FirstOrDefault%2A> 上呼叫 <xref:System.Data.Objects.ObjectQuery%601>。  
  
 在某些情況下，查詢看起來好像會在執行期間產生具體化結果，但是查詢是要在伺服器上執行，所以實體物件永遠也不會在 CLR 中具體化。 如果您需要用到物件具體化的副作用，這種情況將會造成問題。  
  
 以下範例包含具有 `MyContact` 屬性的自訂類別 `LastName`。 當 `LastName` 屬性設定之後，`count` 變數就會累加。 如果您執行以下兩個查詢，第一個查詢會累加 `count`，但第二個查詢則不會。 這是因為在第二個查詢中 `LastName` 屬性是從結果投影的，而且根本沒有建立 `MyContact` 類別，因為在存放區上執行此查詢並不要用到它。  
  
 [!code-csharp[DP L2E Materialization Example#MaterializationSideEffects](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Materialization Example/CS/Program.cs#materializationsideeffects)]
 [!code-vb[DP L2E Materialization Example#MaterializationSideEffects](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Materialization Example/VB/Module1.vb#materializationsideeffects)]  
  
 [!code-csharp[DP L2E Materialization Example#MyContactClass](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Materialization Example/CS/Program.cs#mycontactclass)]
 [!code-vb[DP L2E Materialization Example#MyContactClass](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Materialization Example/VB/Module1.vb#mycontactclass)]
