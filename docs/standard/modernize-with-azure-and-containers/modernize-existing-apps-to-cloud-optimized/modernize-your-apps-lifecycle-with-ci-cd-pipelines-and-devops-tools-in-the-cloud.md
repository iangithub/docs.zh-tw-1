---
title: 在雲端中使用 CI/CD 管線和 DevOps 工具將應用程式生命週期現代化
description: 將現有的.NET 應用程式使用 Azure 雲端和 Windows 容器現代化 |現代化您的應用程式生命週期 CI/CD 管線與雲端中的 DevOps 工具
ms.date: 04/30/2018
ms.openlocfilehash: fb4bfab4a891e9c8a73867f18cb8249775f9b7b9
ms.sourcegitcommit: 34593b4d0be779699d38a9949d6aec11561657ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2019
ms.locfileid: "66833962"
---
# <a name="modernize-your-apps-lifecycle-with-cicd-pipelines-and-devops-tools-in-the-cloud"></a>在雲端中使用 CI/CD 管線和 DevOps 工具將應用程式生命週期現代化

現今的企業需要速度很快即可具競爭力的市場中發揮創意。 交付高品質、 現代化應用程式需要 DevOps 工具和程序會實作這個持續的循環的創新的關鍵。 使用適當的 DevOps 工具，開發人員可以簡化持續部署，並更快速創新的應用程式傳遞給的使用者。

雖然持續整合和部署作法全都堅實的建立，容器的簡介會介紹新的考量，特別是當您正在使用多容器應用程式。

Azure 的 DevOps 服務支援持續整合和多容器應用程式部署到各種不同的環境，透過的官方 Azure DevOps 服務部署工作：

- [For Containers 中部署為 Azure Web 應用程式](https://docs.microsoft.com/azure/devops/pipelines/apps/cd/deploy-docker-webapp?view=azure-devops)

- [部署至 Azure Container Service-Kubernetes](https://docs.microsoft.com/azure/devops/build-release/apps/cd/azure/deploy-container-kubernetes)

但是您也可以部署到[Docker Swarm](https://blogs.msdn.microsoft.com/jcorioland/2016/11/29/full-ci-cd-pipeline-to-deploy-multi-containers-application-on-azure-container-service-docker-swarm-using-visual-studio-team-services/)或 DC/OS 使用 Azure DevOps 服務指令碼為基礎的工作。

若要繼續加速部署靈活度，這些工具會提供絕佳的開發到測試-至-生產部署容器工作負載，使用您選擇的開發和 CI/CD 解決方案體驗。

圖 4 到 12 個顯示持續部署管線，以部署至 Azure Container Service 中 Kubernetes 叢集。

![Azure 的 DevOps 服務持續部署管線，將部署到 Kubernetes 叢集](./media/image12.png)

> **圖 4 到 12 個。** Azure 的 DevOps 服務持續部署管線，將部署到 Kubernetes 叢集

>[!div class="step-by-step"]
>[上一頁](modernize-your-apps-with-monitoring-and-telemetry.md)
>[下一頁](migrate-to-hybrid-cloud-scenarios.md)
