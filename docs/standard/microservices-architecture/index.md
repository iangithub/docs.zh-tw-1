---
title: .NET 微服務。 容器化 .NET 應用程式的架構
description: 容器化 .NET 應用程式的 .NET 微服務架構 | 微服務是模組化的獨立可部署服務。 適用於 Linux 與 Windows 的 Docker 容器，可統合服務及其相依性到單一個單位，簡化部署及測試，然後即可於隔離的環境中執行。
ms.date: 01/07/2019
ms.openlocfilehash: fe69dcec58ae1d1eed23a49fadbee378ec129990
ms.sourcegitcommit: 5e05f983e63d5bbd8c0b246d02c6e4f23d2fc1db
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2019
ms.locfileid: "67152012"
---
# <a name="net-microservices-architecture-for-containerized-net-applications"></a>.NET 微服務：容器化 .NET 應用程式的架構

![書籍封面](./media/cover-small.png)

**版本 v2.2** - 更新至 ASP.NET Core 2.2

本指南介紹如何開發微服務應用程式及使用容器進行管理， 並討論使用 .NET Core 和 Docker 容器的架構設計和實作方法。 

為了讓您更輕鬆地開始使用，本指南將重點放在您可以探索的容器化和微服務應用程式。 此參考應用程式位於 [eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers) GitHub 存放庫中。

## <a name="action-links"></a>動作連結

* 以您選擇的格式下載這本電子書：| [PDF](https://aka.ms/microservicesebook) | [MOBI](https://www.microsoft.com/net/download/thank-you/microservices-architecture-ebook-mobi) | [EPUB](https://www.microsoft.com/net/download/thank-you/microservices-architecture-ebook-epub) |

* 複製/派生 [GitHub 上的 eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers) 參考應用程式
 
* 觀賞 [Channel 9 上的介紹影片](https://aka.ms/microservices-video)

* 立即了解[微服務架構](https://aka.ms/MicroservicesArchitecture)

## <a name="introduction"></a>簡介

企業透過容器，逐漸實現成本節約、解決部署問題，以及改善 DevOps 和生產環境作業。 Microsoft 藉由建立 Azure Kubernetes Service 和 Azure Service Fabric 等產品，以及藉由與 Docker、Mesosphere 和 Kubernetes 等業界領導者合作，不斷為 Windows 和 Linux 創新容器。 這些產品提供容器解決方案，可協助公司以雲端速度和規模建置及部署應用程式，而不論其選擇的平台或工具為何。

Docker 成為容器產業的既定標準，並受到 Windows 和 Linux 生態系統中最重要廠商的支援 (Microsoft 是其中一個支援 Docker 的主要雲端廠商)。未來，Docker 可能會在雲端或內部部署的任何資料中心廣泛運用。

此外，[微服務](https://martinfowler.com/articles/microservices.html)架構已躍升為分散式關鍵任務應用程式的重要方法。 在微服務架構中，應用程式會建置在一組可獨立開發、測試、部署及設定版本的服務之上。

## <a name="about-this-guide"></a>關於本指南

本指南介紹如何開發微服務應用程式及使用容器進行管理， 並討論使用 .NET Core 和 Docker 容器的架構設計和實作方法。 為了讓您更輕鬆地開始使用容器和微服務，本指南將重點放在您可以探索的容器化和微服務應用程式。 此範例應用程式位於 [eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers) GitHub 存放庫中。

此指南提供主要在開發環境層級的基本開發和架構指引，並著重於兩項技術：Docker 與 .NET Core。 我們的用意是讓您在思考應用程式設計，但不想要將重點放在生產環境的基礎結構 (雲端或內部部署) 時，可以閱讀本指南。 稍後，當您建立可實際執行的應用程式時，您將會制定基礎結構的相關決策。 因此，本指南與基礎結構無關，而是偏重開發環境。

研讀本指南之後，您的下一個步驟是了解 Microsoft Azure 上可實際執行的微服務。

## <a name="version"></a>版本

本指南已經過修訂，涵蓋了 **.NET Core 2.2** 版，加上許多和 .NET Core 2.2 同時期， 同一波科技「浪潮」相關的更新 (亦即 Azure 加上其他第三方技術)。 這也是同步將書籍版本更新為 **2.2** 版的原因。 

## <a name="what-this-guide-does-not-cover"></a>本指南未涵蓋的內容

本指南的重點不在應用程式生命週期、DevOps、CI/CD 管線或小組合作。 補充性指南 [Containerized Docker Application Lifecycle with Microsoft Platform and Tools](https://aka.ms/dockerlifecycleebook) (Microsoft 平台和工具的容器化 Docker 應用程式生命週期) 會以該主題為重點。 目前的指南也不提供 Azure 基礎結構的實作詳細資料，例如特定 Orchestrator 的相關資訊。

### <a name="additional-resources"></a>其他資源

- **Microsoft 平台和工具的容器化 Docker 應用程式生命週期** (可下載的電子書)  
    <https://aka.ms/dockerlifecycleebook>

## <a name="who-should-use-this-guide"></a>誰應該使用本指南

本指南的撰寫對象是剛接觸 Docker 應用程式開發和微服務架構的開發人員和解決方案架構師。 如果您想要了解如何使用 Microsoft 開發技術 (特別是 .NET Core) 和 Docker 容器，來架構、設計及實作概念證明應用程式，則本指南很適合您。

如果您是技術決策者 (例如企業架構師)，想概括了解架構和技術，再決定要選取哪個方法以用於新的現代化分散式應用程式，您也會發現本指南很實用。

### <a name="how-to-use-this-guide"></a>如何使用本指南

本指南的第一部分介紹 Docker 容器、討論如何在 .NET Core 和 .NET Framework 之間選擇開發架構，並提供微服務概觀。 此內容適用於需要概觀但重點不在程式碼實作詳細資料的架構師和技術決策者。

本指南的第二部分以 [Docker 應用程式的開發程序](./docker-application-development-process/index.md)一節開頭， 並將重點放在使用 .NET Core 和 Docker 實作應用程式的開發和微服務模式。 本節對於想要專注於程式碼、模式和實作詳細資料的開發人員和架構師最為重要。

## <a name="related-microservice-and-container-based-reference-application-eshoponcontainers"></a>相關微服務和容器參考應用程式：eShopOnContainers

eShopOnContainers 應用程式是 .NET Core 和微服務的開放原始碼參考應用程式，專為使用 Docker 容器進行部署所設計。 此應用程式是由多個子系統所組成，包括數個電子商店 UI 前端 (Web MVC 應用程式、Web SPA 和原生行動應用程式)。 它也包含用來執行所有必要伺服器端作業的後端微服務和容器。 

應用程式的目的是要展示架構模式。 **這不是用於生產環境的範本**，無法用來啟動真實世界應用程式。 事實上，應用程式永久處於 beta 版狀態，因為在出現可能有興趣的新技術時，也會使用它來進行測試。

## <a name="send-us-your-feedback"></a>將您的意見反應傳送給我們！

本指南的撰寫目的是為了協助您了解 .NET 中的容器化應用程式和微服務架構。 本指南和相關參考應用程式會不斷改進，因此歡迎您提供寶貴的意見反應！ 如果您對如何改進本指南有任何意見，請傳送到：

[dotnet-architecture-ebooks-feedback@service.microsoft.com](mailto:dotnet-architecture-ebooks-feedback@service.microsoft.com)

## <a name="credits"></a>參與名單

共同作者：

> **Cesar de la Torre**，Sr. Microsoft Corp. .NET 產品小組 PM
>
> **Bill Wagner**，Sr. Microsoft Corp. C+E 內容開發人員
>
> **Mike Rousos**，Microsoft DevDiv CAT 小組首席軟體工程師

編輯者：

> **Mike Pope**
>
> **Steve Hoag**

參與者和檢閱者：

> **Jeffrey Ritcher**，Microsoft Azure 小組合作夥伴軟體工程師
>
> **Jimmy Bogard**，Headspring 首席架構師
>
> **Udi Dahan**，Particular Software 創辦人暨執行長
>
> **Jimmy Nilsson**，Factor10 共同創辦人暨執行長
>
> **Glenn Condron**，Sr. ASP.NET 小組計畫經理
>
> **Mark Fussell**，Microsoft Azure Service Fabric 小組 PM 主管
>
> **Diego Vega**，Microsoft Entity Framework 小組 PM 主管
>
> **Barry Dorrans**，Sr. 安全性計畫經理
>
> **Rowan Miller**，Sr. Microsoft 計畫經理
>
> **Ankit Asthana**，Microsoft .NET 小組 PM 總經理
>
> **Scott Hunter**，Microsoft .NET 小組合夥人暨 PM 主管
>
> **Nish Anil**，Microsoft NET 小組資深方案經理
>
> **Dylan Reisenberger**，Polly 架構師暨開發部門主管
>
> **Steve "ardalis" Smith** - 軟體架構設計人員和講師 - [Ardalis.com](https://ardalis.com)
>
> **Ian Cooper**，Brighter 程式碼架構師
>
> **Unai Zorrilla**，Plain Concepts 架構師暨開發部門主管
>
> **Eduard Tomas**，Plain Concepts 開發部門主管
>
> **Ramon Tomas**，Plain Concepts 開發人員
>
> **David Sanz**，Plain Concepts 開發人員
>
> **Javier Valero**，Grupo Solutio 營運長
>
> **Pierre Millet**，Sr. Microsoft 顧問
>
> **Michael Friis**，Docker Inc. 產品經理
>
> **Charles Lowell**，Microsoft VS CAT 小組軟體工程師
>
> **Miguel Veloso**，Sr. 圖靈挑戰顧問

## <a name="copyright"></a>Copyright

下載：<https://aka.ms/microservicesebook>

發行者

Microsoft 開發人員部門 .NET 和 Visual Studio 產品小組

Microsoft Corporation 部門

One Microsoft Way

Redmond, Washington 98052-6399

Copyright © 2019 by Microsoft Corporation

著作權所有，並保留一切權利。 本書內容的任何部分在未經過發行者書面許可下，不得以任何形式或透過任何方式進行重製或傳送。

本書是以「現況」提供，代表作者的觀點和意見。 本書中所述之觀點、意見與資訊 (包括 URL 及其他網際網路網站參考) 可能會隨時變更，恕不另行通知。

此處所描述的一些範例僅供說明，純屬虛構。 任何實際關聯或連結純屬巧合。

Microsoft 與列於 <https://www.microsoft.com> 「商標」網頁的商標是 Microsoft 集團的商標。

Mac 與 macOS 是 Apple Inc. 的商標。

Docker 鯨魚標誌是 Docker, Inc. 的註冊商標。使用需要許可。

所有其他商標和標誌屬於其各自擁有者的財產。

>[!div class="step-by-step"]
>[下一步](container-docker-introduction/index.md)
