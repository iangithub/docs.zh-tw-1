---
title: 使用部分方法加入商務邏輯
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3a73991e-fd4e-4610-93fb-7ced4dc6b7f9
ms.openlocfilehash: ed440f3315fc25e82b648f21410acb7a2c2a08f9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67743675"
---
# <a name="adding-business-logic-by-using-partial-methods"></a>使用部分方法加入商務邏輯
您可以自訂 Visual Basic 和C#產生的程式碼，在您[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]使用的專案*部分方法*。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 產生的程式碼會將簽章定義成部分方法的一部分。 如果您想實作此方法，可以加入自己的部分方法。 如果您未加入自己的實作 (Implementation)，則編譯器 (Compiler) 會捨棄部分方法簽章並呼叫 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中的預設方法。  
  
> [!NOTE]
>  如果您使用 Visual Studio，您可以使用物件關聯式設計工具，將驗證和其他自訂項目加入至實體類別。  
  
 例如，Northwind 範例資料庫中 `Customer` 類別的預設對應包含下列部分方法：  
  
 [!code-csharp[DLinqOverrideDefault#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#2)]
 [!code-vb[DLinqOverrideDefault#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#2)]  
  
 您可以將下列程式碼加入至自己的部分 `Customer` 類別，進而實作自己的方法：  
  
 [!code-csharp[DLinqOverrideDefault#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/Program.cs#3)]
 [!code-vb[DLinqOverrideDefault#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/Module1.vb#3)]  
  
 這種方法通常會用於[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]覆寫預設方法，如`Insert`， `Update`， `Delete`，以及先驗證物件生命週期事件期間的屬性。  
  
 如需詳細資訊，請參閱 <<c0> [ 部分方法](~/docs/visual-basic/programming-guide/language-features/procedures/partial-methods.md)(Visual Basic) 或[partial （方法） (C#參考)](~/docs/csharp/language-reference/keywords/partial-method.md) (C#)。</c0>  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>說明  
 下列範例會先顯示 `ExampleClass`，因為它可能是由程式碼產生工具 (例如 SQLMetal) 所定義，然後顯示您如何僅實作其中一種方法。  
  
### <a name="code"></a>程式碼  
 [!code-csharp[DLinqSubmittingChanges#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#4)]
 [!code-vb[DLinqSubmittingChanges#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#4)]  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>描述  
 下列範例會使用 `Shipper` 和 `Order` 實體 (Entity) 之間的關聯性 (Relationship)。 請注意部分方法中的 `InsertShipper` 和 `DeleteShipper` 方法。 這些方法會覆寫所提供的預設部分方法[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]對應。  
  
### <a name="code"></a>程式碼  
 [!code-csharp[DLinqOverrideDefault#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#1)]
 [!code-vb[DLinqOverrideDefault#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#1)]  
  
## <a name="see-also"></a>另請參閱

- [變更和提交資料](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)
- [自訂插入、更新和刪除作業](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)
