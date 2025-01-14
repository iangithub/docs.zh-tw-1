---
title: 逐步解說：操作資料 (C#)
ms.date: 03/30/2017
ms.assetid: 24adfbe0-0ad6-449f-997d-8808e0770d2e
ms.openlocfilehash: 2d45861569bc4a8b57427b01e107f87809203e11
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67742741"
---
# <a name="walkthrough-manipulating-data-c"></a>逐步解說：操作資料 (C#)
本逐步解說針對加入、修改和刪除資料庫中的資料，提供基本的端對端 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 案例。 您將使用範例 Northwind 資料庫的複本來加入客戶、變更客戶名稱，以及刪除訂單。  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 本逐步解說的內容是依據 Visual C# 開發設定所撰寫的。  
  
## <a name="prerequisites"></a>必要條件  
 本逐步解說需要下列項目：  
  
- 本逐步解說會使用專用資料夾 ("c:\linqtest6") 來保存檔案。 請先建立這個資料夾，再開始逐步解說。  
  
- Northwind 範例資料庫。  
  
     如果您的開發電腦上沒有這個資料庫，則可以從 Microsoft 下載網站下載。 如需相關指示，請參閱 <<c0> [ 下載範例資料庫](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)。 下載資料庫之後，請將 northwnd.mdf 檔案複製至 c:\linqtest6 資料夾。  
  
- 會從 Northwind 資料庫產生 C# 程式碼檔案。  
  
     您可以使用物件關聯式設計工具或 SQLMetal 工具來產生這個檔案。 本逐步解說是使用 SQLMetal 工具，以下列命令列所撰寫：  
  
     **sqlmetal /code:"c:\linqtest6\northwind.cs" /language:csharp "C:\linqtest6\northwnd.mdf" /pluralize**  
  
     如需詳細資訊，請參閱 [SqlMetal.exe (程式碼產生工具)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)。  
  
## <a name="overview"></a>總覽  
 此逐步解說包含六個主要工作：  
  
- 建立[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]Visual Studio 中的方案。  
  
- 將資料庫程式碼檔案加入至專案。  
  
- 建立新的客戶物件。  
  
- 修改客戶的連絡人名稱。  
  
- 刪除訂單。  
  
- 將這些變更送出至 Northwind 資料庫。  
  
## <a name="creating-a-linq-to-sql-solution"></a>建立 LINQ to SQL 方案  
 在第一個工作中，您會建立包含必要的參考，以建置並執行 Visual Studio 方案[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]專案。  
  
#### <a name="to-create-a-linq-to-sql-solution"></a>若要建立 LINQ to SQL 方案  
  
1. 在 Visual Studio**檔案**功能表上，指向**新增**，然後按一下**專案**。  
  
2. 在 [**專案類型**] 窗格中的**新增專案**] 對話方塊中，按一下 [ **Visual C#** 。  
  
3. 按一下 [範本]  窗格中的 [主控台應用程式]  。  
  
4. 在 **名稱**方塊中，輸入**LinqDataManipulationApp**。  
  
5. 在 **位置**方塊中，確認您要儲存專案檔。  
  
6. 按一下 [確定 **Deploying Office Solutions**]。  
  
## <a name="adding-linq-references-and-directives"></a>加入 LINQ 參考和指示詞  
 本逐步解說使用的組件，可能在您的專案中預設為不安裝。 如果 System.Data.Linq 未列為專案中的參考，請按照下列步驟所述將它加入：  
  
#### <a name="to-add-systemdatalinq"></a>若要加入 System.Data.Linq  
  
1. 在 **方案總管 中**，以滑鼠右鍵按一下**參考**，然後按一下 **加入參考**。  
  
2. 在 **加入參考** 對話方塊中，按一下 **.NET**按一下 System.Data.Linq 組件，然後按一下 **確定**。  
  
     組件隨即加入至專案。  
  
3. 將下列指示詞加在 Program.cs 的上方：  
  
     [!code-csharp[DLinqWalk3CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#1)]  
  
## <a name="adding-the-northwind-code-file-to-the-project"></a>將 Northwind 程式碼檔案加入至專案  
 這些步驟假設您已使用 SQLMetal 工具，從 Northwind 範例資料庫產生程式碼檔案。 如需詳細資訊，請參閱本逐步解說稍早的「必要條件」一節。  
  
#### <a name="to-add-the-northwind-code-file-to-the-project"></a>若要將 Northwind 程式碼檔案加入至專案  
  
1. 在 **專案**功能表上，按一下**加入現有項目**。  
  
2. 在 [**加入現有項目**] 對話方塊中，巡覽至 c:\linqtest6\northwind.cs，，，然後按一下**新增**。  
  
     northwind.cs 檔案會加入至專案。  
  
## <a name="setting-up-the-database-connection"></a>設定資料庫連接  
 請先測試與資料庫的連接。 請特別注意，資料庫 Northwnd 沒有字母 i。 如果在後續步驟發生錯誤，則請檢閱 northwind.cs 檔案，以判斷 Northwind 部分類別的拼法。  
  
#### <a name="to-set-up-and-test-the-database-connection"></a>若要設定和測試資料庫連接  
  
1. 將下列程式碼輸入或貼入 Program 類別的 `Main` 方法：  
  
     [!code-csharp[DLinqWalk3CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#2)]  
  
2. 按 F5，立即測試應用程式。  
  
     A**主控台**視窗隨即開啟。  
  
     您可以藉由按下 Enter 以關閉應用程式**主控台** 視窗中，或按一下**停止偵錯**在 Visual Studio**偵錯**功能表。  
  
## <a name="creating-a-new-entity"></a>建立新的實體  
 建立新的實體十分簡單。 您可以使用 `Customer` 關鍵字，建立物件 (如 `new`)。  
  
 在本節和下列各節中，您變更的只是本機快取。 在本逐步解說最後呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 之前，都不會將變更傳送至資料庫。  
  
#### <a name="to-add-a-new-customer-entity-object"></a>若要加入新的 Customer 實體物件  
  
1. 在 `Customer` 方法的 `Console.ReadLine();` 前面加入下列程式碼，建立新的 `Main`：  
  
     [!code-csharp[DLinqWalk3CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#3)]  
  
2. 按 F5 對方案進行偵錯。  
  
3. 中按 Enter 鍵**主控台**視窗以停止偵錯並繼續進行本逐步解說。  
  
## <a name="updating-an-entity"></a>更新實體  
 在下列步驟中，您會擷取 `Customer` 物件，並修改它的其中一個屬性。  
  
#### <a name="to-change-the-name-of-a-customer"></a>若要變更 Customer 的名稱  
  
- 將下列程式碼加入至 `Console.ReadLine();` 的上方：  
  
     [!code-csharp[DLinqWalk3CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#4)]  
  
## <a name="deleting-an-entity"></a>刪除實體  
 您可以使用同一個客戶物件，刪除第一份訂單。  
  
 在下列程式碼中，會示範如何中斷資料列之間的關聯性 (Relationship)，以及如何刪除資料庫中的資料列。 將下列程式碼加入至 `Console.ReadLine` 的前面，以查看如何刪除物件：  
  
#### <a name="to-delete-a-row"></a>若要刪除資料列  
  
- 將下列程式碼加入至 `Console.ReadLine();` 的正上方：  
  
     [!code-csharp[DLinqWalk3CS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#5)]  
  
## <a name="submitting-changes-to-the-database"></a>將變更送出至資料庫  
 建立、更新和刪除物件的最終必要步驟是實際將變更送出至資料庫。 沒有這個步驟，所進行的變更只是針對本機，並不會出現在查詢結果中。  
  
#### <a name="to-submit-changes-to-the-database"></a>若要將變更送出至資料庫  
  
1. 將下列程式碼插入至 `Console.ReadLine` 的正上方：  
  
     [!code-csharp[DLinqWalk3CS#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#6)]  
  
2. 將下列程式碼插入至 `SubmitChanges` 的後面，以顯示送出變更之前和之後的效果：  
  
     [!code-csharp[DLinqWalk3CS#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#7)]  
  
3. 按 F5 對方案進行偵錯。  
  
4. 中按 Enter 鍵**主控台**關閉應用程式的視窗。  
  
> [!NOTE]
>  送出變更以加入新的客戶之後，無法再照原狀執行這個方案。 若要重新執行方案，請變更要加入的客戶名稱和客戶識別碼。  
  
## <a name="see-also"></a>另請參閱

- [依逐步解說學習](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)
