---
title: 在 Visual Studio 2017 中使用 .NET Core 測試 .NET Standard 類別程式庫
description: 為您的 .NET Core 類別庫建立單元測試專案。 藉由單元測試確認您的 .NET Core 類別庫運作正常。
author: BillWagner
ms.author: wiwagn
ms.date: 08/07/2017
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet, seodoc18
ms.openlocfilehash: 32593465c1a161aa1293b7b233539fa930c7e1d8
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2019
ms.locfileid: "67402200"
---
# <a name="test-a-net-standard-library-with-net-core-in-visual-studio-2017"></a>在 Visual Studio 2017 中使用 .NET Core 測試 .NET Standard 程式庫

於[在 Visual Studio 2017 中使用 C# 和 .NET Core 建置 .NET Standard 程式庫](library-with-visual-studio.md)或[在 Visual Studio 2017 中使用 Visual Basic 和 .NET Core 建置 .NET Standard 程式庫](vb-library-with-visual-studio.md)中，您建立了一個將擴充方法新增至 <xref:System.String> 類別的簡易類別庫。 現在我們將建立單元測試，確定它如預期般運作。 我們會將我們的單元測試專案加入在上一篇文章中建立的方案。

## <a name="creating-a-unit-test-project"></a>建立單元測試專案

若要建立單元測試專案，請執行下列作業︰

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. 在方案總管  中，開啟 **ClassLibraryProject** 方案節點的內容功能表，然後選取 [新增]   >  [新增專案]  。

1. 在 [新增專案]  對話方塊中，選取 [Visual C#]  節點。 然後選取後面跟著 [MSTest 測試專案 (.NET Core)]  專案範本的 [.NET Core]  節點。 在 **[名稱]** 文字方塊中，輸入 "StringLibraryTest" 作為專案名稱。 選取 [確定]  以建立單元測試專案。

   ![顯示單元測試專案的 [新增專案] 對話方塊 - C#](./media/testing-library-with-visual-studio/create-new-test-project.png)

   > [!NOTE]  
   > 除了 MSTest 測試專案之外，您也可以使用 Visual Studio 建立適用於 .NET Core 的 xUnit 測試專案。

1. Visual Studio 會建立專案，並在程式碼視窗中開啟 *UnitTest1.cs* 檔案。

   ![單元測試專案類別和方法的 Visual Studio 程式碼視窗 - C#](./media/testing-library-with-visual-studio/unit-test-editor-window.png)

   單元測試範本建立的原始程式碼會執行下列動作︰

   * 它會匯入 <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=nameWithType> 命名空間，其中包含用於單元測試的類型。

   * 它會將 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> 屬性套用至 `UnitTest1` 類別。 執行單元測試時，在測試類別中標示 \[TestMethod\] 屬性的每個測試方法都將自動執行。

   * 它會套用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 屬性，以將 `TestMethod1` 定義為在執行單元測試時自動執行的測試方法。

1. 在 **方案總管** 中，以滑鼠右鍵按一下 **StringLibraryTest** 專案的 **[相依性]** 節點，然後從內容功能表中選取 **[新增參考]** 。

   ![StringLibraryTest 相依性的操作功能表 - C#](./media/testing-library-with-visual-studio/add-reference-context-menu.png)

1. 在 **[參考管理員]** 對話方塊中，展開 **[專案]** 節點並核取 **[StringLibrary]** 旁的方塊。 將參考新增至 `StringLibrary` 組件，可讓編譯器找出 **StringLibrary** 方法。 選取 [確定]  按鈕。 這會在您的類別庫專案 `StringLibrary` 中新增參考。

   ![Visual Studio 新增專案參考對話方塊](./media/testing-library-with-visual-studio/project-reference-manager.png)
# <a name="visual-basictabvb"></a>[Visual Basic](#tab/vb) 
1. 在方案總管  中，開啟 **ClassLibraryProject** 方案節點的內容功能表，然後選取 [新增]   >  [新增專案]  。

1. 在 [新增專案]  對話方塊中，選取 [Visual Basic]  節點。 然後選取後面跟著 [MSTest 測試專案 (.NET Core)]  專案範本的 [.NET Core]  節點。 在 **[名稱]** 文字方塊中，輸入 "StringLibraryTest" 作為專案名稱。 選取 [確定]  以建立單元測試專案。

   ![顯示單元測試專案的 [新增專案] 對話方塊 - Visual Basic](./media/testing-library-with-visual-studio/vb-create-new-test-project.png)

   > [!NOTE]  
   > 除了 MSTest 測試專案之外，您也可以使用 Visual Studio 建立適用於 .NET Core 的 xUnit 測試專案。

1. Visual Studio 會建立專案，並在程式碼視窗中開啟 *UnitTest1.vb* 檔案。

   ![單元測試專案類別和方法的 Visual Studio 程式碼視窗 - Visual Basic](./media/testing-library-with-visual-studio/vb-unit-test-editor-window.png)

   單元測試範本建立的原始程式碼會執行下列動作︰

   * 它會匯入 <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=nameWithType> 命名空間，其中包含用於單元測試的類型。

   * 它會將 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute>) 屬性套用至 `UnitTest1` 類別。 執行單元測試時，在測試類別中標示 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 屬性的每個測試方法都將自動執行。

   * 它會套用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 屬性，以將 `TestMethod1` 定義為在執行單元測試時自動執行的測試方法。

1. 在 **方案總管** 中，以滑鼠右鍵按一下 **StringLibraryTest** 專案的 **[相依性]** 節點，然後從內容功能表中選取 **[新增參考]** 。

   ![StringLibraryTest 相依性的內容功能表](./media/testing-library-with-visual-studio/add-reference-context-menu.png)

1. 在 [參考管理員]  對話方塊中，展開 [專案]  節點並核取 [StringLibrary]  旁的方塊。 將參考新增至 `StringLibrary` 組件，可讓編譯器找出 **StringLibrary** 方法。 選取 [確定]  按鈕。 這會在您的類別庫專案 `StringLibrary` 中新增參考。

   ![Visual Studio 新增專案參考對話方塊 - Visual Basic](./media/testing-library-with-visual-studio/project-reference-manager.png)
---

## <a name="adding-and-running-unit-test-methods"></a>新增和執行單元測試方法

Visual Studio 執行單元測試時，會執行單元測試類別 (即套用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute> 屬性的類別) 中標示 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 屬性的每個方法。 測試方法會在發生第一次失敗時或方法中包含的所有測試均成功時結束。

最常見的測試會呼叫 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> 類別的成員。 許多判斷提示方法都至少包括兩個參數，一個是預期的測試結果，另一個是實際的測試結果。 它最常呼叫的一些方法如下表所示。

Assert 方法 | 功能
--- | ---
`Assert.AreEqual` | 驗證兩個值或物件相等。 如果值或物件不相等，判斷提示就會失敗。
`Assert.AreSame` | 驗證兩個物件變數參考相同的物件。 如果變數參考不同的物件，判斷提示就會失敗。
`Assert.IsFalse` | 驗證條件為 `false`。 如果條件為 `true`，判斷提示就會失敗。
`Assert.IsNotNull` | 驗證物件不是 `null`。 如果物件為 `null`，判斷提示就會失敗。

您也可以將 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute> 屬性套用到測試方法。 指出測試方法預期擲回的例外狀況類型。 如果沒有擲回指定的例外狀況，測試便會失敗。

在測試 `StringLibrary.StartsWithUpper` 方法時，您想提供幾個以大寫字元開頭的字串。 您預期此方法在這些情況下傳回 `true`，因此您可以呼叫 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue%2A> 方法。 同樣地，您想提供幾個開頭不是大寫字元的字串。 您預期此方法在這些情況下傳回 `false`，因此您可以呼叫 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse%2A> 方法。

因為您的程式庫方法會處理字串，您也想確定它會成功處理[空字串 (`String.Empty`)](xref:System.String.Empty)，這是不包含任何字元且其 <xref:System.String.Length> 為 0 的有效字串和尚未初始化的 `null` 字串。 如果在 <xref:System.String> 執行個體上呼叫 `StartsWithUpper` 做為擴充方法，它將無法傳遞 `null` 字串。 不過，您也可以將其作為靜態方法來直接呼叫，並傳遞單一 <xref:System.String> 引數。

您會定義三個方法，每個方法會針對字串陣列中的每個項目重複呼叫其 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> 方法。 因為測試方法會在發生第一次失敗時立即失敗，您將呼叫一個方法多載，以便傳遞一個字串來指示在方法呼叫中使用的字串值。

建立測試方法：

# <a name="ctabcsharp"></a>[C#](#tab/csharp) 
1. 在 *UnitTest1.cs* 程式碼視窗中，以下列程式碼取代程式碼：

   [!CODE-csharp[Test#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/testlib1.cs)]

   請注意，您在 `TestStartsWithUpper` 方法中的大寫字元測試包含希臘文大寫字母 alpha (U+0391) 和斯拉夫文大寫字母 EM (U+041C)，`TestDoesNotStartWithUpper` 方法中的小寫字元測試包含希臘文小寫字母 alpha (U+03B1) 和斯拉夫文小寫字母 Ghe (U+0433)。

1. 在功能表列上，選取 [檔案]   >  [將 UnitTest1.cs As 另存為]  。 在 **[另存新檔]** 對話方塊中，選擇 **[儲存]** 按鈕旁的箭號，然後選擇 **[以編碼方式儲存]** 。

   ![Visual Studio [另存新檔] 對話方塊 - C#](./media/testing-library-with-visual-studio/save-file-as-dialog.png)
# <a name="visual-basictabvb"></a>[Visual Basic](#tab/vb) 
1. 在 *UnitTest1.vb* 程式碼視窗中，以下列程式碼取代程式碼：

    [!CODE-vb[Test#1](../../../samples/snippets/core/tutorials/vb-library-with-visual-studio/testlib.vb)]

   請注意，您在 `TestStartsWithUpper` 方法中的大寫字元測試包含希臘文大寫字母 alpha (U+0391) 和斯拉夫文大寫字母 EM (U+041C)，`TestDoesNotStartWithUpper` 方法中的小寫字元測試包含希臘文小寫字母 alpha (U+03B1) 和斯拉夫文小寫字母 Ghe (U+0433)。

1. 在功能表列上，選取 [檔案]   > [將 UnitTest1.vb 另存為]  。 在 **[另存新檔]** 對話方塊中，選擇 **[儲存]** 按鈕旁的箭號，然後選擇 **[以編碼方式儲存]** 。

   ![Visual Studio [另存新檔] 對話方塊 - Visual Basic](./media/testing-library-with-visual-studio/save-file-as-dialog.png)
---

1. 在 **[確認另存新檔]** 對話方塊中，選擇 **[是]** 按鈕以儲存檔案。

1. 在 **[進階儲存選項]** 對話方塊的，選取 **[編碼]** 下拉式清單中選擇 **[Unicode (UTF-8 有簽章) - 字碼頁 65001]** ，然後選擇 **[確定]** 。

   ![Visual Studio [進階儲存選項] 對話方塊](./media/testing-library-with-visual-studio/advanced-save-options.png)

   如果您無法將您的原始程式碼儲存為 UTF8 編碼檔案，Visual Studio 可能會將它儲存為 ASCII 檔案。 發生該情況時，執行階段無法正確解碼 ASCII 範圍之外的 UTF8 字元，因此測試結果將不精確。

1. 在功能表列上，選擇 **[測試]**  >  **[執行]**  >  **[所有測試]** 。 [測試總管]  視窗隨即開啟並顯示測試成功執行。 這三項測試都會列在 [通過的測試]  區段中，而 [摘要]  區段則報告測試回合的結果。

   ![測試總管視窗，其中包含通過的測試](./media/testing-library-with-visual-studio/test-explorer-window.png)

## <a name="handling-test-failures"></a>處理測試失敗

您的測試回合未失敗，但將它稍微變更，使其中一個測試方法失敗：

1. 修改 `TestDoesNotStartWithUpper` 方法中的 `words` 陣列，以包含字串「錯誤」。 您不需要儲存檔案，因為當組建方案以執行測試時，Visual Studio 會自動儲存開啟的檔案。

   ```csharp
   string[] words = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " };
   ```

   ```vb
   Dim words() As String = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " }

   ```

1. 從功能表列中，選取 [測試]   >  [執行]   >  [所有測試]  來執行測試。 [測試總管]  視窗表示兩個測試成功，而且有一項失敗。

   ![測試總管視窗，其中包含失敗的測試](./media/testing-library-with-visual-studio/failed-test-window.png)

1. 在 **[失敗的測試]** 區段中選擇失敗的測試 `TestDoesNotStartWith`。 [測試總管]  視窗會顯示判斷提示產生的訊息："Assert.IsFalse failed. Expected for 'Error': false; actual:True" (Assert.IsFalse 失敗。預期為 'Error'：false；實際為：True)。 因為發生失敗，陣列中 "Error" 之後的所有字串並未經過測試。

   ![[測試總管] 視窗顯示「為 False」的判斷提示失敗](./media/testing-library-with-visual-studio/failed-test-detail.png)

1. 復原您在步驟 1 中所做的修改，並移除字串 "Error"。 重新執行該測試，測試將會通過。

## <a name="testing-the-release-version-of-the-library"></a>測試程式庫的發行版本

您已針對偵錯版本的程式庫執行測試。 既然您的測試全部通過，並已充分測試過您的程式庫，您應針對程式庫的發行組建執行更多時間的測試。 許多因素 (包括編譯器最佳化) 有時會在偵錯和發行組建之間導致不同的行為。

測試發行組建︰

1. 在 Visual Studio 工具列中，將組建組態從 [偵錯]  變更為 [發行]  。

   ![醒目提示 [發行] 組建的 Visual Studio 工具列](./media/testing-library-with-visual-studio/visual-studio-toolbar-release.png)

1. 在 **方案總管** 中，以滑鼠右鍵按一下 **StringLibrary** 專案，然後從內容功能表中選取 **[組建]** 以重新編譯程式庫。

   ![StringLibrary 操作功能表和建置命令](./media/testing-library-with-visual-studio/build-library-context-menu.png)

1. 從功能表列中，選擇 [測試]   >  [執行]   >  [所有測試]  來執行單元測試。 所有測試皆通過。

既然您已經完成程式庫測試，下一步是將它提供給呼叫端。 您可以將它與一或多個應用程式搭售，或是將將它發佈為 NuGet 套件。 如需詳細資訊，請參閱[使用 .NET Standard 類別庫](./consuming-library-with-visual-studio.md)。
