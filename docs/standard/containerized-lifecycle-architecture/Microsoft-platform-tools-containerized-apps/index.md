---
title: 容器化應用程式的 Microsoft 平台和工具簡介
description: 了解支援 Docker 應用程式生命週期的 Microsoft 供應項目。
ms.date: 02/15/2019
ms.openlocfilehash: 6907528a5d7ff354a312e7575531b9c608cb479f
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/13/2019
ms.locfileid: "66195589"
---
# <a name="introduction-to-the-microsoft-platform-andtools-for-containerized-apps"></a>容器化應用程式的 Microsoft 平台和工具簡介

*願景：建立具可調適性、企業級的容器化應用程式生命週期 (橫跨您的開發、IT 作業及生產管理)。*

圖 3-1 顯示依工作類型分類的 Docker 應用程式生命週期中的主要部分，而工作類型是由多個小組 (應用程式開發、DevOps 基礎結構程序以及 IT 管理和作業) 所衍生。 通常，在企業中，負責每個區域之「人物代表」的設定檔會不同。 就是他們的技術。

![Microsoft 工具。 針對開發/設計工作負載：適用於 Windows 的 Docker 引擎、VS 和 VS Code、.NET Core、Azure Kubernetes Service。 針對建置/測試/傳送工作負載：Azure DevOps、Team Foundation Server、Docker CLI、Azure Kubernetes Service。 針對執行/監視/管理工作負載：Azure 監視器、Azure 入口網站 Azure Kubernetes Services、Service Fabric、其他協調器。](./media/image1.png)

**圖 3-1** 使用 Microsoft 平台和工具之容器化 Docker 應用程式生命週期中的主要部分

容器化 Docker 生命週期工作流程一開始是根據「預設產品選項」所規定，輕鬆地讓開發人員更快速地開始使用，但它是基礎，且實際上必須為開放式架構；因此，它會是彈性工作流程，可調整為來自每個組織或企業的不同內容。 工作流程基礎結構 (元件和產品) 必須具有足夠的彈性，才能涵蓋每家公司未來將要有的環境，即使可以將開發或 DevOps 產品切換成其他開發或 DevOps 產品也是一樣。 此彈性、開放性以及平台和基礎結構中各種技術就是容器化 Docker 應用程式的 Microsoft 優先順序，如下列各章所述。

表 3-1 示範容器化 Docker 應用程式的 Microsoft DevOps 意圖是提供開放式 DevOps 工作流程，讓您可以選擇要用於每個階段的產品 (Microsoft 或協力廠商)，同時提供簡化工作流程以提供已連線「預設產品」；因此，您可以快速地開始使用 Docker 應用程式的企業級 DevOps 工作流程。

**表 3-1.** 開放給任何技術的 DevOps 工作流程

| 主機 | Microsoft 技術 | 協力廠商 - Azure 插入式 |
| ---------------------------| ----------------------------------------------------| --------------------------------------------------------------------------------|
| Docker 應用程式的平台   | • Microsoft Visual Studio 和 Visual Studio Code<br /> • .NET<br /> • Microsoft Azure Kubernetes Service (AKS)<br /> • Azure Service Fabric<br /> • Azure Container Registry<br /> | • 任何程式碼編輯器 (例如，Sublime)<br /> • 任何語言 (Node.js、Java、Go 等等)<br /> • 任何協調器和排程器<br /> • 任何 Docker 登錄<br /> |
| Docker 應用程式的 DevOps     | • Azure DevOps Services<br /> • Microsoft Team Foundation Server<br /> • Azure Kubernetes Service (AKS)<br /> • Azure Service Fabric<br /> | • GitHub、Git、Subversion 等等<br /> • Jenkins、Chef、Puppet、Velocity、CircleCI、TravisCI 等等<br /> • 內部部署 Docker Datacenter、Docker Swarm、Mesos DC/OS、Kubernetes 等等<br /> |
| 管理和監視  | • Azure 監視器 | • Marathon、Chronos 等等<br />|

表 3-1 中所定義之容器化 Docker 應用程式的 Microsoft 平台和工具，包含下列元件：

- **Docker 應用程式開發的平台**：服務的開發，或構成「應用程式」的服務集合。 開發平台提供開發人員在 將其程式碼推送至共用程式碼存放庫之前所需的所有工作。 開發服務 (部署為容器) 類似於不使用 Docker 開發相同的應用程式或服務。 您可以繼續使用偏好語言 (.NET、Node.js、Go 等) 和偏好編輯器或 IDE (例如 Visual Studio 或 Visual Studio Code)。 不過，您可以開發 Docker 環境中的服務，而不需要將 Docker 視為部署目的地。 您可以在本機建置、執行、測試和偵錯容器中的程式碼，並在開發階段提供目的地環境。 透過在本機提供目的地環境，Docker 容器設定項目將有助於大幅改善 DevOps 生命週期。 Visual Studio 和 Visual Studio Code 的延伸模組可以整合開發程序內的 Docker 容器。

- **Docker 應用程式的 DevOps**：建立 Docker 應用程式的開發人員可以使用 [Azure DevOps Services](https://azure.microsoft.com/services/devops/) 或任何其他協力廠商產品 (例如 Jenkins) 來建置完整的自動化應用程式生命週期管理 (ALM)。

  使用 Azure DevOps Services，開發人員可以針對快速反覆的處理序建立焦點所在容器的 DevOps，而此處理序涵蓋任何位置的原始碼控制 (Azure DevOps Services-Git、GitHub、任何遠端 Git 存放庫或 Subversion)、持續整合 (CI)、內部單元測試、容器/服務間整合測試、持續傳遞 (CD) 和發行管理 (RM)。 開發人員也可以將其 Docker 應用程式從預備和生產環境的開發到 Azure Kubernetes Service (AKS) 的發行予以自動化。

- **管理和監視** IT 可以使用數種方法來管理及監視生產應用程式和服務，將這兩種檢視方式整合成統一的體驗。

  - **Azure 入口網站** 如果您使用開放原始碼協調器，則 Azure Kubernetes Service (AKS)、Service Fabric 和其他協調器可協助您設定及維護 Docker 環境。 如果您要使用 Azure Service Fabric，則 Service Fabric Explorer 工具可讓您視覺化和設定叢集。

  - **Docker 工具** 您可以使用熟悉的工具來管理容器應用程式。 不需要變更現有 Docker 管理做法，即可將容器工作負載移至雲端。 使用您已熟悉並透過所選擇協調器的標準 API 端點所連線的應用程式管理工具。 您也可以使用其他協力廠商工具來管理 Docker 應用程式 (例如 Docker Datacenter) 甚至是 CLI Docker 工具。 

    即使您熟悉 Linux 命令，也可以使用 Microsoft Windows 和 PowerShell 搭配 Linux 子系統命令列和在此 Linux 子系統功能上執行的產品 (Docker、Kubernetes...) 用戶端來管理容器應用程式。 您將在本書稍後進一步了解如何透過常用的 Microsoft Windows OS 使用 Linux 子系統下的這些工具。

  - **開放原始碼工具** 因為 AKS 會公開協調流程引擎的標準 API 端點，所以最常用工具會與 AKS 相容，且在大部分情況下可立即使用 (包含視覺化檢視、監視、命令列工具，甚至是未來可用的工具)。

  - **Azure 監視器**是 Azure 的解決方案，可監視生產環境的各個方面。 您可以監視生產 Docker 應用程式，只要將其 SDK 設定至您的服務，讓您能夠從應用程式取得系統產生的記錄資料即可。

因此，Microsoft 會提供端對端容器化 Docker 應用程式生命週期的完整基礎。 不過，它是「產品和技術的集合，可讓您選擇性地選取並與現有工具和處理序整合」。 廣泛方式的彈性以及功能深度的強度讓 Microsoft 十分適合進行容器化 Docker 應用程式開發。

>[!div class="step-by-step"]
>[上一頁](../Docker-application-lifecycle/containers-foundation-for-devops-collaboration.md)
>[下一頁](../design-develop-containerized-apps/index.md)
