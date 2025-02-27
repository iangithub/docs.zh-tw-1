---
title: C# 與 Visual Studio Code 使用者入門
description: 了解如何在 C# 中使用 Visual Studio Code 建立並偵錯您的第一個 .NET Core 應用程式。
author: kendrahavens
ms.date: 12/05/2018
ms.custom: seodec18
ms.openlocfilehash: 1268a943d7cbf1033531a6c51f42c6fd672eaed3
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2019
ms.locfileid: "67401843"
---
# <a name="get-started-with-c-and-visual-studio-code"></a>C# 與 Visual Studio Code 使用者入門

.NET Core 提供快速且模組化的平台，可建立在 Windows、Linux 和 macOS 上執行的應用程式。 搭配使用 Visual Studio Code 與 C# 擴充功能，以取得具備 C# IntelliSense (智慧型程式碼完成) 與偵錯完整支援的強大編輯體驗。

## <a name="prerequisites"></a>必要條件

1. 安裝 [Visual Studio Code (英文)](https://code.visualstudio.com/)。
2. 安裝 [.NET Core SDK (英文)](https://www.microsoft.com/net/download/core)。
3. 安裝適用於 Visual Studio Code 的 [C# 擴充功能](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) \(英文\)。 如需如何在 Visual Studio Code 上安裝擴充功能的詳細資訊，請參閱 [VS Code 擴充功能市集](https://code.visualstudio.com/docs/editor/extension-gallery) \(英文\)。

## <a name="hello-world"></a>Hello World

讓我們在 .NET Core 上開始進行簡單的 "Hello World" 程式：

1. 開啟專案：

    * 開啟 Visual Studio Code。
    * 按一下左側功能表上的 [檔案總管] 圖示，然後按一下 [開啟資料夾]  。
    * 從主要功能表中選取 [檔案]   > [開啟資料夾]  ，以開啟您想要放置 C# 專案的資料夾，然後按一下 [選取資料夾]  。 針對本範例，我們將為專案建立一個名為 *HelloWorld* 的資料夾。

      ![Visual Studio Code 開啟資料夾](media/with-visual-studio-code/vs-code-open-folder.png)

2. 初始化 C# 專案：
    * 從主要功能表中選取 [檢視]   > [整合式終端機]  ，以從 Visual Studio Code 開啟 [整合式終端機]。
    * 在終端機視窗中，輸入 `dotnet new console`。
    * 此命令會在您的資料夾中建立已撰寫簡單 "Hello World" 程式的 `Program.cs` 檔案，以及名為 `HelloWorld.csproj` 的 C# 專案檔。

      ![DotNet 新增命令](media/with-visual-studio-code/dotnet-new-command.png)

3. 解析組建資產：

    * 針對 **.NET Core 1.x**，鍵入 `dotnet restore`。 執行 `dotnet restore` 可讓您存取建置專案所需的必要 .NET Core 封裝。

      ![DotNet 還原命令](media/with-visual-studio-code/dotnet-restore-command.png)

      [!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

4. 執行 "Hello World" 程式︰

    * 輸入 `dotnet run`。

      ![DotNet 執行命令](media/with-visual-studio-code/dotnet-run-command.png)

您也可以觀看簡短的影片教學課程，以取得 [Windows (英文)](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core)、[macOS (英文)](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core-on-MacOS) 或 [Linux (英文)](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-Csharp-dotnet-Core-Ubuntu) 上的進一步設定說明。

## <a name="debug"></a>偵錯

1. 按一下 *Program.cs* 來開啟它。 在 Visual Studio Code 中第一次開啟 C# 檔案時，會在編輯器中載入 [OmniSharp](https://www.omnisharp.net/)。

    ![開啟 Program.cs 檔案](media/with-visual-studio-code/open-program-cs.png)

2. Visual Studio Code 應該會提示您新增遺失的資產，以建置和偵錯您的應用程式。 選取 [是]  。

    ![遺失資產的提示](media/with-visual-studio-code/missing-assets.png)

3. 若要開啟 [偵錯] 檢視，請按一下左側功能表上的 [偵錯] 圖示。

    ![在 Visual Studio Code 中開啟 [偵錯] 索引標籤](media/with-visual-studio-code/open-debug-tab.png)

4. 尋找窗格頂端的綠色箭頭。 請確定它旁邊的下拉式清單已選取 `.NET Core Launch (console)`。

    ![在 Visual Studio Code 中選取 .NET Core](media/with-visual-studio-code/select-net-core.png)

5. 按一下第 9 行旁邊的 [編輯器邊界]  (編輯器中行號左側空白處)，將中斷點新增至您的專案，或將文字游標移至編輯器中的第 9 行，然後按 <kbd>F9</kbd> 鍵。

    ![設定中斷點](media/with-visual-studio-code/set-breakpoint-vs-code.png)

6. 若要開始偵錯，請選取 <kbd>F5</kbd> 或綠色箭頭。 當偵錯程式到達您在上一個步驟中設定的中斷點時，它會停止您程式的執行。
    * 進行偵錯時，您可以在左上角窗格中檢視您的本機變數或使用偵錯主控台。

7. 選取頂端的藍色箭頭以繼續偵錯，或選取頂端的紅色正方形以停止偵錯。

    ![在 Visual Studio Code 中執行和偵錯](media/with-visual-studio-code/run-debug-vs-code.png)

> [!TIP]
> 如需在 Visual Studio Code 中使用 OmniSharp 進行 .NET Core 偵錯的詳細資訊與疑難排解祕訣，請參閱 [Instructions for setting up the .NET Core debugger](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md) (設定 .NET Core 偵錯工具的指示)。

## <a name="add-a-class"></a>新增類別

1. 若要新增類別，請在「VSCode 總管」中按一下滑鼠右鍵，然後選取 [新增檔案]  。 這會在您於 VSCode 中開啟的資料夾內新增檔案。
2. 將檔案命名為 `MyClass.cs`。 您必須在結尾加上 `.cs` 副檔名來儲存它，系統才能將它辨識為 csharp 檔案。
3. 新增下方程式碼來建立您的第一個類別。 請務必包含正確的命名空間，如此您才能夠從 `Program.cs` 檔案參考它。

    ``` csharp
    using System;

    namespace HelloWorld
    {
        public class MyClass
        {
            public string ReturnMessage()
            {
                return "Happy coding!";
            }
        }
    }
    ```

4. 新增下方程式碼以從 `Program.cs` 中的主要方法呼叫您的新類別。

    ```csharp
    using System;
    
    namespace HelloWorld
    {
        class Program
        {
            static void Main(string[] args)
            {
                MyClass c1 = new MyClass();
                Console.WriteLine($"Hello World! {c1.ReturnMessage()}");
            }
        }
    }
    ```

5. 儲存變更，然後重新執行您的程式。 應該會顯示含有所附加字串的新訊息。

    ```console
    > dotnet run
    Hello World! Happy coding!
    ```

## <a name="faq"></a>常見問題集

### <a name="im-missing-required-assets-to-build-and-debug-c-in-visual-studio-code-my-debugger-says-no-configuration"></a>我缺少在 Visual Studio Code 中建置及偵錯 C# 所需的資產。 我的偵錯工具顯示「沒有組態」。

Visual Studio Code C# 延伸模組可為您產生用於建置和偵錯的資產。 Visual Studio Code 會在您第一次開啟 C# 專案時，提示您產生這些資產。 如果您當時未產生資產，仍可以透過開啟 [命令選擇區] ([檢視] > [命令選擇區]  )，然後鍵入 ">.NET:Generate Assets for Build and Debug" 來執行此命令。 選取此選項會產生您所需的 .vscode、launch.json 和 tasks.json 組態檔。

## <a name="see-also"></a>另請參閱

- [設定 Visual Studio Code (英文)](https://code.visualstudio.com/docs/setup/setup-overview)
- [在 Visual Studio Code 中偵錯 (英文)](https://code.visualstudio.com/Docs/editor/debugging)
