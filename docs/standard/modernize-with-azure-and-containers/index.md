---
title: 現代化現有.NET 應用程式與 Azure 的雲端和 Windows 容器 （第 2 版）
description: 了解如何隨即轉移和現代化現有應用程式到 Azure 雲端及與本電子書的容器。
ms.date: 04/28/2018
ms.openlocfilehash: 4e632fcfbb8904a9def3fdad992286055c5df4f0
ms.sourcegitcommit: 6472349821dbe202d01182bc2cfe9d7176eaaa6c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67870603"
---
# <a name="modernize-existing-net-applications-with-azure-cloud-and-windows-containers-2nd-edition"></a>將現有.NET 應用程式與 Azure 雲端和 Windows 容器現代化 （第 2 版）

![現代化的.NET 應用程式指南的封面影像。](./media/index/web-application-guide-cover-image.png)

發行者  
Microsoft Corporation  
Microsoft Press 及 Microsoft DevDiv 部門  
One Microsoft Way  
Redmond, Washington 98052-6399  

Copyright © 2018 by Microsoft Corporation  

著作權所有，並保留一切權利。 本書內容的任何部分在未經過發行者書面許可下，不得以任何形式或透過任何方式進行重製。

這本書是透過 microsoft 的多個管道以電子書 （電子書） 的形式免費提供例如<https://dot.net/architecture>。

若您對本書有相關問題，請傳送電子郵件到 [dotnet-architecture-ebooks-feedback@service.microsoft.com](mailto:dotnet-architecture-ebooks-feedback@service.microsoft.com?subject=Feedback%20for%20.NET%20Container%20&%20Microservices%20Architecture%20book)

本書依照「現況」提供，代表作者的觀點和意見。 檢視、 意見和這本書，包括 URL 及其他網際網路網站參考資料，以表示的資訊可能會變更恕不另行通知。

此處所描述的一些範例僅供說明，純屬虛構。 任何實際關聯或連結純屬巧合。

Microsoft 與列於 <https://www.microsoft.com>「商標」網頁的商標是 Microsoft 集團的商標。 所有其他商標皆屬於其各自擁有者的財產。

作者:
> **Cesar de la Torre**，資深 PM，.NET 產品小組，Microsoft corp.

參與者和檢閱者：
> **Scott Hunter**，Microsoft .NET 小組合夥人暨 PM 主管  
> **Paul Yuknewicz**，Microsoft Visual Studio Tools 小組首席 PM 經理  
> **Lisa Guthrie**，資深 PM，Microsoft Visual Studio Tools 小組  
> **Ankit Asthana**，Microsoft .NET 小組 PM 總經理  
> **Unai Zorrilla**，Plain Concepts 開發人員主管  
> **Javier Valero**，Grupo Solutio 營運長  

## <a name="introduction"></a>簡介

當您決定要現代化您的 web 應用程式或服務，並將它們移至雲端時，不一定完全重新架構您的應用程式。 重新架構應用程式，使用微服務等進階的方法不見得永遠可行因為成本與時間限制。 根據應用程式類型，重新架構應用程式也不可能需要。 為了讓組織的雲端移轉策略發揮最高成本效益，考量您的業務需求與應用程式需求便成了重要的一環。 您必須判斷：

- 哪些應用程式需要轉換或重新架構。

- 哪些應用程式只需要進行部分修改。

- 哪些應用程式沒辦法直接「隨即轉移」到雲端。

## <a name="about-this-guide"></a>關於本指南

本指南主要著重在初步現代化現有的 Microsoft.NET Framework web 或服務導向應用程式，這表示將工作負載移至較新或較現代的環境中，而不需要大幅變更應用程式的程式碼的動作和基本架構。 

本指南也會反白顯示您的應用程式移到雲端和部分使用一組特定的新技術和方法，例如 Windows 容器和相關的計算平台在 Azure 中支援 Windows 容器現代化應用程式的優點。

## <a name="path-to-the-cloud-for-existing-net-applications"></a>現有 .NET 應用程式前往雲端的路徑

組織通常會選擇移至雲端以提升其應用程式的靈活度與速度。 您可以在數分內於雲端設置上千個伺服器 (VM)，相較之下，設置內部部署伺服器通常需要幾個禮拜的時間。

將應用程式移轉到雲端並沒有一體適用的策略。 適合您的移轉策略取決於組織的需求與優先順序，以及所要移轉的應用程式種類。 並非所有應用程式都適合移至平台即服務 ([PaaS](https://azure.microsoft.com/overview/what-is-paas/)) 模型，或是開發[雲端原生](https://www.gartner.com/doc/3181919/architect-design-cloudnative-applications)應用程式模型。 在許多情況下，您可以根據業務需求，使用分階或累進式方法將資產移至雲端。

現代應用程式，具有最佳長期靈活度和組織的值，您可能會受益於投資*雲端原生*應用程式架構。 不過，對於現有的應用程式或舊版的資產，關鍵在於花費最少的時間和金錢 （沒有重新架構或程式碼變更），將其移至雲端，以實現最大收益。

圖 1-1 呈現了您採取累進方式將現有的 .NET 應用程式移至雲端時，可以採用的路徑。

 ![現有 .NET 應用程式及服務的現代化路徑](./media/image1-1.png)

> **圖 1-1**。 現有 .NET 應用程式及服務的現代化路徑

每個移轉方法都有其優點及使用理由。 在將應用程式移至雲端時，您可以選擇單一方法，也可以從多種方法中擷取某些元件。 個別應用程式並不侷限於單一方法或成熟度。 比方說，一般混合方法會有某些內部部署元件，再加上雲端中的其他元件。

定義和每個應用程式成熟度等級的簡短說明如下所示：

**等級 1:雲端基礎結構準備妥當**應用程式：在此移轉方法中，您只是移轉或重新裝載您目前的內部部署應用程式，基礎結構即服務 ([IaaS](https://azure.microsoft.com/overview/what-is-iaas/)) 平台。 您的應用程式結構和以前幾乎相同，但您現已將其部署到雲端中的 VM。
這個簡單的移轉類型通常稱為在業界"原封不動移轉。 」

**等級 2:雲端最佳化**應用程式：在此層級，並仍不需要重新架構或改變重大的程式碼，您可以取得使用現代化的技術，例如容器和其他雲端管理的服務在雲端中執行您的應用程式的其他優點。 您可藉由精簡企業開發營運 (DevOps) 程序來增加應用程式的靈活度，加快出貨速度。 使用 Docker 引擎為基礎的 Windows 容器等技術來達到此目的。 容器會移除在多個階段部署時，會將應用程式相依性所造成的不便。 在此成熟度模型中，您可以部署在 IaaS 上的容器，或同時使用其他的 PaaS 雲端管理的服務相關的資料庫，快取即服務、 監視以及持續整合/持續部署 (CI/CD) 管線。

第三等級的成熟度是雲端的終極目標，但對大多數應用程式而言並非必要，且非本指南的主要重點：

**等級 3:雲端原生**應用程式：此移轉方法通常是由商務需求和現代化的任務關鍵性應用程式的目標所驅動。 在此等級中，您可使用 PaaS 服務將您的應用程式移至 PaaS 運算平台上。 您可以實作[雲端原生](https://www.gartner.com/doc/3181919/architect-design-cloudnative-applications)應用程式及微服務架構，來發展具長期靈活度的應用程式，以及擴展新界限。 這種類型的現代化通常需要專為雲端設計的架構。 尤其在移至雲端原生應用程式及微服務式模型的時候，通常會需要撰寫新的程式碼。 這項方法可協助您取得在整合型及內部部署應用程式環境中難以達到的優點。

表 1-1 描述了選擇各項移轉或現代化方法的主要優點及理由。

| **雲端基礎結構就緒** <br /> *隨即轉移* | **Cloud-Optimized** <br /> *現代化* | **Cloud-Native** <br /> *現代化、 重建和重寫* |
|---|---|---|
| **應用程式的計算目標** |
| 在 Azure 中部署到 VM 的應用程式 | 龐大且單一的體系或多層式架構應用程式部署至 Azure App Service、 Azure 容器執行個體 (ACI)、 Vm 與容器或 AKS (Azure Kubernetes Service) | Azure Kubernetes Service (AKS) 和/或無伺服器 Azure 函式為基礎的微服務的容器化微服務。 |
| **資料目標** |
| SQL 或 VM 上的任何關聯式資料庫 | Azure SQL Database 受控執行個體或另一個在雲端中受管理的資料庫。 | 每個微服務，根據 Azure SQL Database、 Azure Cosmos DB 或另一部受管理的資料庫，在雲端中的罰鍰粒紋資料庫 |
| **優點**|
| <li>任何重新架構，任何新的程式碼 <li> 以最少心力快速移轉 <li> Azure 中支援的最普及選項 <li> 保證基本可用性 <li> 移至雲端後更容易現代化 | <li> 任何重新架構 <li> 最少的程式碼/組態變更 <li> 因容器而獲得改善的部署及 DevOps 發行靈活度 <li> 增加密度並降低部署成本 <li> 應用程式及相依性的可攜性 <li> 裝載目標的彈性：PaaS 方法或 IaaS | <li> 架構設計人員的雲端，您會獲得最佳的優點從雲端，但需要新的程式碼 <li> 微服務雲端原生方法 <li> 現代任務關鍵性應用程式，雲端彈性高度可擴充 <li> 完整受控的服務 <li> 經最佳化以調整規模 <li> 為子系統的自主靈活度最佳化 <li> 建基於部署及 DevOps |
| **挑戰** |
| <li> 除了轉入營業費用或關閉資料中心之外，雲端價值較低 <li> 什麼被管理：沒有 OS 或中介軟體修補;可能會使用基礎結構解決方案，例如 Terraform、 Spinnaker 或 Puppet | <li> 容器化是額外的步驟中學習曲線，開發人員和 IT 作業 <li> DevOps 與 CI/CD 管線通常是 '必須' 這種方法。 如果沒有目前存在於組織的文化特性中，它可能是其他的挑戰| <li> 針對雲端原生應用程式和微服務架構需要彌補重新架構，而且通常需要重大的程式碼重構或重寫現代化時 （增加的時間及開支）|
> **表 1-1。** 現有 .NET 應用程式及服務現代化路徑的優點與挑戰

### <a name="key-technologies-and-architectures-by-maturity-level"></a>依成熟度等級分階的主要技術及架構

.NET Framework 應用程式最初從 2001 年年底推出的 .NET Framework 1.0 版開始。 之後，公司移往了更新的版本 (例如 2.0、3.5 及 .NET 4.x)。 這些應用程式在 Windows Server 和 Internet Information Server (IIS) 上執行，並使用關聯式資料庫中的，例如 SQL Server、 Oracle、 MySQL 或任何其他 RDBMS。

如今，大多數現有的 .NET 應用程式可能以 .NET Framework 4.x 甚至是 .NET Framework 3.5 為基礎，且使用 ASP.NET MVC、ASP.NET Web Forms、ASP.NET Web API、Windows Communication Foundation (WCF)、ASP.NET SignalR 及 ASP.NET Web Pages 等 Web 架構。 這些已建立的 .NET Framework 技術相依於 Windows。 若您只是想移轉舊版應用程式，而且希望將對應用程式基礎結構產生的變更降至最低，該相依性是重要的考慮因素。

圖 1-2 顯示了在三個雲端成熟度等級中，各自使用的主要技術及架構樣式：

![各個成熟度等級將現有 .NET Web 應用程式現代化時使用的主要技術](./media/image1-2.png)

> **圖 1-2。** 將現有 .NET Web 應用程式現代化時，各個成熟度等級使用的主要技術

圖 1-2 強調了大多數常見案例，然而在架構方面有可能會出現許多混合變化。 比方說，成熟度模型不僅適用現有 Web 應用程式中的整合型架構，也適用於服務導向、多層式架構 (N-Tier) 及其他架構樣式變化。 較高的焦點或上一個或另一個結構類型和相關的技術的百分比決定您的應用程式的整體成熟度層級。

現代化程序中的每個成熟度等級都與下列主要技術和方法相關：

- **雲端基礎結構準備妥當**（重新裝載或基本原封不動移轉）：第一個步驟中，許多組織只想要快速執行的雲端移轉策略。 在此情況下，重新裝載的應用程式。 大多數重新裝載作業都能透過使用 [Azure Migrate](https://aka.ms/azuremigrate) 自動執行，此服務會提供必要的指導、深入解析及機制，協助您透過 [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) 及 [Azure 資料庫移轉服務](https://azure.microsoft.com/campaigns/database-migration/)等雲端工具移轉到雲端。 您也可以手動設定重新裝載，使您能在將舊版應用程式移至雲端時，了解有關您資產的基礎結構詳細資料。 例如，您可以在 Azure 中移動您 Vm 的應用程式幾乎需要修改，可能與只是小幅度設定變更。 在此情況中的網路功能與內部部署環境相似，特別是當您在 Azure 中建立虛擬網路的時候。

- **雲端最佳化**（管理服務和 Windows 容器）：此模型是關乎少數的重要部署最佳化，以取得一些顯著的優點從雲端，而不需要變更應用程式的核心架構。 基本步驟是將 [Windows 容器](https://docs.microsoft.com/virtualization/windowscontainers/about/)支援新增至您現有的 .NET Framework 應用程式。 這個重要的步驟 （容器化） 並不需要碰觸的程式碼，整體投入隨即轉移，所以 淺。 您可以使用 [Image2Docker](https://github.com/docker/communitytools-image2docker-win)、Visual Studio 以及 Visual Studio Tools for [Docker](https://www.docker.com/)。 Visual Studio 會自動選擇 ASP.NET 應用程式及 Windows 容器映像的智慧型預設。 這些工具提供了迅速的內部迴圈，以及容器到 Azure 的快速路徑， 並改善您部署到多個環境時的靈活度。 然後，移至生產環境，您可以部署 Windows 容器[Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/)， [Azure Container Instances (ACI)](https://azure.microsoft.com/services/container-instances/)，和 Windows Server 2016 和容器，如果您偏好使用的 Azure VmIaaS 方法。 對於更複雜的多容器應用程式，請考慮使用等協調器[Azure Kubernetes Service (AKS/ACS)](https://azure.microsoft.com/services/container-service/)。 

在初步現代化，您也可以新增資產從雲端，例如監視之類的工具[Azure Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview);搭配使用您的應用程式生命週期的 CI/CD 管線[Azure DevOps 服務](https://azure.microsoft.com/services/devops/); 和在 Azure 中使用的許多詳細資料資源服務。 比方說，您可以修改原先使用傳統 [ASP.NET Web Forms](https://www.asp.net/web-forms) 或 [ASP.NET MVC](https://www.asp.net/mvc) 開發的整合型 Web 應用程式，而您現在可以使用 Windows 容器進行部署。 當您使用 Windows 容器時，也應該將資料移轉到 [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/)中的資料庫，這完全不需要變更您應用程式的核心架構。

- **雲端原生**:導入，您應該考量架構[雲端原生](https://www.gartner.com/doc/3181919/architect-design-cloudnative-applications)應用程式時您的目標大型且複雜的應用程式使用不同的微服務可處理多個獨立的開發小組開發和部署自主性。 此外，由於每個微服務 granularized 與延展性。 這些架構的方法遇到非常重要的挑戰與複雜性，但可以大幅簡化使用雲端 PaaS 及協調器，像是[Azure Kubernetes Service (AKS/ACS)](https://azure.microsoft.com/services/container-service/) （受控 Kubernetes） 和[Azure Functions](https://azure.microsoft.com/services/functions/)無伺服器的方法。 （例如微服務和無伺服器） 的所有這些方法通常需要您的雲端架構，並撰寫新程式碼 — 適用於特定的 PaaS 平台的程式碼或符合特定的架構，例如微服務的程式碼。

圖 1-3 顯示了您可在每個成熟度等級使用的內部技術：

![每個現代化成熟度等級的內部技術](./media/image1-3.png)

> **圖 1-3。** 每個現代化成熟度等級的內部技術

## <a name="lift-and-shift-scenario"></a>原形移轉案例

對於隨即轉移，請記得您可以在應用程式案例中使用多種不同的隨即轉移變化。 如果您只重新裝載應用程式，可能會產生圖 1-4 中的情形，也就是您只在應用程式及資料庫伺服器使用雲端中的 VM。

![雲端中的單純 IaaS 案例範例](./media/image1-4.png)

> **圖 1-4**。 雲端中的單純 IaaS 案例範例

## <a name="modernization-scenarios"></a>現代化的案例

現代化的情況下，您可能使用純雲端最佳化使用的應用程式項目僅來自該成熟度等級。 或者，您可能會有一些項目中繼狀態應用程式從雲端基礎結構準備妥當與從雲端最佳化的其他項目 (一個 「 挑選 」 或混合的模型)，像 圖 1-5。

![有 IaaS 上的資料庫、DevOps 及容器化資產的範例「挑選」案例](./media/image1-5.png)

> **圖 1-5。** 有 IaaS 上的資料庫、DevOps 及容器化資產的範例「挑選」案例

接下來，理想的案例，許多現有的.NET Framework 應用程式，若要移轉，您可以將移轉至雲端最佳化的應用程式，以些許功夫換取顯著的優點。 這個方法也會為您安排雲端原生為可能的未來發展。 範例請見圖 1-6。

![範例雲端最佳化應用程式案例中，使用 Windows 容器及受控的服務](./media/image1-6.png)

> **圖 1-6。** 範例雲端最佳化應用程式案例中，使用 Windows 容器及受控的服務

更進一步地說，您可以藉由新增特定案例的幾個微服務擴充您現有的雲端最佳化應用程式。 這會將您部分雲端原生的模型，也就是不存在的指導方針的主要重點的層級。

## <a name="what-this-guide-does-not-cover"></a>本指南未涵蓋的內容

本指南涵蓋一部份的特定範例案例，如圖 1-7 所示。 本指南著重於只隨即轉移案例，而最後，在雲端最佳化的模型上。 在雲端最佳化模型中，.NET Framework 應用程式現代化使用 Windows 容器，再加上額外的元件，例如監視和 CI/CD 管線。 若要以快速且具彈性的方式將應用程式部署到雲端，每項元件都是不可或缺的要素。

![本指南並未涵蓋雲端原生](./media/image1-7.png)

> **圖 1-7。** 本指南並未涵蓋雲端原生

本指南的重點很明確。 它會顯示您可達到現有.NET 應用程式，原形重新架構，而不必變更程式碼的路徑。 最後，它會顯示您如何讓您的應用程式雲端最佳化。

本指南不會示範如何建立雲端原生應用程式，例如發展到微服務架構。 若要重新架構您的應用程式，或建立微服務為基礎的全新應用程式，請參閱電子書[.NET 微服務：容器化.NET 應用程式架構](https://aka.ms/microservicesebook)。

### <a name="additional-resources"></a>其他資源

- **容器化 Docker 應用程式生命週期，Microsoft 平台和工具**（可下載的電子書） \
  <https://aka.ms/dockerlifecycleebook>

- **.NET 微服務：容器化.NET 應用程式架構**（可下載的電子書） \
  <https://aka.ms/microservicesebook>

- **架構現代化 web 應用程式使用 ASP.NET Core 和 Azure** （可下載的電子書） \
  <https://aka.ms/webappebook>

## <a name="who-should-use-this-guide"></a>誰應該使用本指南

本指南是針對開發人員和想要現代化現有的 ASP.NET web 應用程式或 WCF 服務以.NET Framework 中，提供改良的靈活性，出貨與發行應用程式為基礎的方案架構設計人員所撰寫。

如果您是技術決策者，例如企業架構設計師，或是只想大略了解使用 Windows 容器及使用 Microsoft Azure 部署到雲端有何優點的開發部門主管，這篇指南也會很實用。

## <a name="how-to-use-this-guide"></a>如何使用本指南

本指南說明了「原因」：吸引您將現有應用程式現代化的誘因，以及將應用程式移往雲端時，使用 Windows 容器所能獲得的具體效益。 本指南前幾個章節中的內容專為想了解概要，但不需要專注在實作及技術性、逐步詳細資料的架構設計師與技術決策者設計而成。

本指南的最後一章導入了多個逐步解說，重點放在特定部署案例上。 本指南會提供較短版本的逐步解說中，以概述案例並反白顯示它們的優點。 完整的逐步解說會向下切入安裝及實作細節，並以一組 [Wiki 文章](https://github.com/dotnet-architecture/eShopModernizing/wiki)的形式發佈到與範本應用程式所在的相同 [GitHub 存放區](https://github.com/dotnet-architecture/eShopModernizing)中 (會在下一節中提到)。 想要專注在實作細節的開發人員與架構師，可能會對最後一章與 GitHub 上的逐步 Wiki 解說較有興趣。

## <a name="sample-apps-for-modernizing-legacy-apps-eshopmodernizing"></a>將舊版應用程式現代化的範例應用程式：eShopModernizing

GitHub 上的 [eShopModernizing](https://github.com/dotnet-architecture/eShopModernizing) 存放庫提供兩個模擬舊版整合型 Web 應用程式的範例應用程式。 使用 ASP.NET MVC; 開發 web 應用程式使用 ASP.NET Web Form 開發的第二個 web 應用程式和第三個應用程式是多層式架構應用程式與 WinForms 用戶端桌面應用程式取用 WCF 服務後端。 所有這些應用程式是以傳統的.NET Framework 為基礎。 因為這些範例程式理應是要現代化的現有/舊版 .NET Framework 應用程式，所以不會使用 .NET Core 或 ASP.NET Core。

這些範例應用程式有第二個版本，使用現代化的程式碼，而且這是相當簡單。 應用程式版本間最主要的差異在於，第二個版本使用了 Windows 容器作為部署選項。 第二個版本也多了一些附加功能，像是用來管理影像的 Azure 儲存體 Blob、用來管理安全性的 Azure Active Directory，以及用來監視與稽核應用程式的 Azure Application Insights。

## <a name="send-your-feedback"></a>傳送您的意見反應

本指南是撰寫可協助您了解改善及現代化現有.NET web 應用程式的選項。 本指南與相關範例應用程式將會不斷更新。 您的意見反應為 褖畫惎 ！ 如果您對如何改進本指南有任何意見，請傳送到 [dotnet-architecture-ebooks-feedback@service.microsoft.com](mailto:dotnet-architecture-ebooks-feedback@service.microsoft.com?subject=Feedback%20for%20.NET%20Container%20&%20Microservices%20Architecture%20book)。

>[!div class="step-by-step"]
>[下一個](lift-and-shift-existing-apps-azure-iaas.md)
