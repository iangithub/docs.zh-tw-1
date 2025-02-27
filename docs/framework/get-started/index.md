---
title: .NET Framework 使用者入門
ms.custom: updateeachrelease
ms.date: 04/02/2019
helpviewer_keywords:
- .NET Framework, getting started
- getting started [.NET Framework]
ms.assetid: c693fd34-88fe-4d90-b332-19eeadf3b7e7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 16e20214981bb5c0f96b26f34be99026aac19266
ms.sourcegitcommit: d8ebe0ee198f5d38387a80ba50f395386779334f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66690197"
---
# <a name="get-started-with-the-net-framework"></a>.NET Framework 使用者入門

.NET Framework 是執行階段的執行環境，負責管理以 .NET Framework 為目標的應用程式。 其由通用語言執行平台及廣大的類別庫組成，前者提供記憶體管理和其他系統服務，後者則能讓程式設計人員將強固、可靠的程式碼善用於應用程式開發的所有主要領域。

> [!NOTE] 
> .NET Framework 只能在 Windows 系統上使用。 您可以在 Windows、MacOS 和 Linux 上使用 [.NET Core](../../core/index.md) 來執行應用程式。 

## <a name="Introducing"></a> 什麼是 .NET Framework？

.NET Framework 是適用於 Windows 的 受控執行環境，可為執行中的應用程式提供多樣的服務。 其由兩個主要元件組成：通用語言執行平台 (CLR) 和 .NET Framework 類別庫，前者是負責處理執行中應用程式的執行引擎，後者提供通過測試、可重複使用的程式碼程式庫，讓開發人員可從自己的應用程式中呼叫。 .NET Framework 提供給執行中應用程式的服務包括：

- 記憶體管理。 在許多程式設計語言中，程式設計人員負責配置和釋放記憶體，以及處理物件存留期。 在 .NET Framework 應用程式中，CLR 會代表應用程式提供這些服務。

- 一般型別系統。 在傳統的程式語言中，基本型別是由編譯器所定義，這會讓跨語言互通性變得很複雜。 在 .NET Framework 中，基底型別是由 .NET Framework 型別系統所定義，可在所有以 .NET Framework 為目標的語言之間通用。

- 廣泛類別庫。 程式設計人員不再需要撰寫大量的程式碼來處理常見的低階程式設計作業，而能夠使用 .NET Framework 類別庫中可立即存取的類型程式庫及其成員來完成這項工作。

- 開發架構和技術。 .NET Framework 包含特定應用程式開發領域所需的程式庫，例如 Web 應用程式所需的 ASP.NET、資料存取所需的 ADO.NET、服務導向應用程式所需的 Windows Communication Foundation，以及 Windows 傳統型應用程式所需的 Windows Presentation Foundation。

- 語言互通性。 以 .NET Framework 為目標的語言編譯器會發出名為通用中間語言 (CIL) 的中繼程式碼，這個程式碼接著會在執行階段由通用語言執行平台進行編譯。 有了此功能，使用某一種語言撰寫的常式就能供其他語言存取，而程式設計人員也能使用自己慣用的語言專心建立應用程式。

- 版本相容性。 在極少數例外狀況下，使用某一特定 .NET Framework 版本開發的應用程式可不經修改直接在較新的版本上執行。

- 並存執行。 .NET Framework 允許同一部電腦上存在多個版本的 Common Language Runtime，藉此協助解決版本衝突。 這表示，多個應用程式版本不僅可共存，應用程式也可以建置時使用的 .NET Framework 版本上執行。 並存執行適用於.NET Framework 版本群組 1.0/1.1、2.0/3.0/3.5 和 4/4.5.x/4.6.x/4.7.x/4.8。

- 多目標。 將目標設為 [.NET Standard](../../standard/net-standard.md)，開發人員就能建立可在該標準版本所支援的多個 .NET Framework 平台上運作的類別庫。 例如，以 .NET Standard 2.0 為目標的類別庫，可由目標為 .NET Framework 4.6.1、.NET Core 2.0 和 UWP 10.0.16299 的應用程式使用。 

<a name="ForUsers"></a>
## <a name="the-net-framework-for-users"></a>適用於使用者的 .NET Framework

如果您並未開發而是使用 .NET Framework 應用程式，就不需要具備任何有關 .NET Framework 或其作業的特定知識。 大致上，.NET Framework 對使用者而言是完全不存在的。

如果您使用的是 Windows 作業系統，您的電腦上可能已經安裝了 .NET Framework。 此外，如果您安裝的應用程式需要 .NET Framework，應用程式的安裝程式可能會在您的電腦上安裝特定的 .NET Framework 版本。 在某些情況下，您可能會看到對話方塊，要求您安裝 .NET Framework。 如果在出現這個對話方塊時您剛好嘗試執行應用程式，而且電腦也可以存取網際網路，則可以前往網頁安裝缺少的 .NET Framework 版本。 如需詳細資訊，請參閱[安裝指南](../install/index.md)。

一般而言，您不應該將電腦上已安裝的 .NET Framework 版本解除安裝。 不這麼做的原因有兩個：

- 如果您使用的應用程式使用特定版本的 .NET Framework，移除該版本可能會造成應用程式無法執行。

- 有些 .NET Framework 版本是舊版的就地更新。 例如，.NET Framework 3.5 是 2.0 版的就地更新，而 .NET Framework 4.8 是 4 到 4.7.2 版的就地更新。 如需詳細資訊，請參閱 [.NET Framework 版本和相依性](../migration-guide/versions-and-dependencies.md)。

在 Windows 8 之前的 Windows 版本中，如果選擇移除 .NET Framework，請一律使用 [控制台] 中的 [程式和功能]  將它解除安裝。 請勿手動移除任何 .NET Framework 版本。 在 Windows 8 (含) 以上版本中，.NET Framework 是作業系統元件，無法單獨解除安裝。

請注意，多個 .NET Framework 版本可以同時在單一電腦上並存。 這表示，您不需要解除安裝舊版，就可以直接安裝新版。

## <a name="ForDevelopers"></a> 適用於開發人員的 .NET Framework

如果您是開發人員，可以選擇任何支援 .NET Framework 的程式設計語言來建立應用程式。 由於 .NET Framework 提供語言獨立性和互通性，因此不論開發時使用的語言為何，您都可以與其他 .NET Framework 應用程式和元件互動。

若要開發 .NET Framework 應用程式或元件，請執行下列步驟：

1. 如果未在作業系統上預先安裝，請安裝要當成應用程式目標的 .NET Framework 版本。 最近的生產版本是 .NET Framework 4.8。 它已預先安裝在 Windows 10 May 2019 Update 上，在舊版 Windows 作業系統上則必須自行下載。 如需 .NET Framework 系統需求，請參閱[系統需求](system-requirements.md)。 如需安裝其他 .NET Framework 版本的資訊，請參閱[安裝指南](../install/guide-for-developers.md)。 其他.NET Framework 套件會在頻外發行，也就是在任何定期或排程發行週期以外輪流發行。 如需這些套件的資訊，請參閱 [.NET Framework 和不定期發行](the-net-framework-and-out-of-band-releases.md)。

2. 選取您要用來開發應用程式且 .NET Framework 也支援的語言。 有多種語言可供選擇，包括 Microsoft 的 [Visual Basic](../../visual-basic/index.md)[C#](../../csharp/index.md)、[F#](../../fsharp/index.md) 及 [C++/CLI](/cpp/dotnet/dotnet-programming-with-cpp-cli-visual-cpp)。 (可讓您開發 .NET Framework 應用程式的程式設計語言會遵循[通用語言基礎結構 (CLI) 規格](https://visualstudio.microsoft.com/license-terms/ecma-c-common-language-infrastructure-standards/))。

3. 選取並安裝要用來建立應用程式，且支援所選程式設計語言的開發環境。 適用於 .NET Framework 應用程式的 Microsoft 整合式開發環境 (IDE) 為 [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)。 並有多個版本可供使用。

如需開發以 .NET Framework 為目標之應用程式的詳細資訊，請參閱[開發指南](../development-guide.md)。

## <a name="related-articles"></a>相關文章

| 標題 | 說明 |
| ----- |------------ |
| [概觀](overview.md) | 替建置以 .NET Framework 為目標之應用程式的開發人員提供詳細資訊。 |
| [安裝指南 (英文)](../install/index.md) | 提供安裝 .NET Framework 的相關資訊。 |  
| [.NET Framework 和不定期發行](the-net-framework-and-out-of-band-releases.md) | 描述 .NET Framework 的頻外發行以及如何將其運用在您的應用程式中。 |
| [系統需求](system-requirements.md) | 列出執行 .NET Framework 的硬體與軟體需求。 |
| [.NET Core 和開放原始碼](net-core-and-open-source.md) | 描述 .NET Core 的相關 .NET Framework 功能，以及如何存取開放原始碼 .NET Core 專案。 |
| [.NET Core 文件](../../core/index.md) | 提供適用於 .NET Core 的概念性及 API 參考文件。 |
| [.NET Standard](../../standard/net-standard.md) | 討論 .NET Standard，這是個別 .NET 實作支援的版本化規格，以保證在多個平台上都能使用一組一致的 API。

## <a name="see-also"></a>另請參閱

- [.NET Framework 指南](../index.md)
- [新功能](../whats-new/index.md)
- [.NET API 瀏覽器](../../../api/index.md)
- [開發指南](../development-guide.md)
