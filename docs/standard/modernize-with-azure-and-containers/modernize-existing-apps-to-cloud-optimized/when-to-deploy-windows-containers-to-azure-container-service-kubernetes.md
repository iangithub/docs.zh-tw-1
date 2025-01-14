---
title: 將 Windows 容器部署至 Azure Container Service (亦即 Kubernetes) 的時機
description: 將現有的.NET 應用程式使用 Azure 雲端和 Windows 容器現代化 |將 Windows 容器部署至 Azure Container Service (亦即 Kubernetes) 的時機
ms.date: 04/30/2018
ms.openlocfilehash: 903082deba635dd0dfc22d0186fbc589f8d05b92
ms.sourcegitcommit: 904b98d8d706f0e2d5ceaa00ce17ffbd92adfb88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66758560"
---
# <a name="when-to-deploy-windows-containers-to-azure-container-service-that-is-kubernetes"></a>將 Windows 容器部署至 Azure Container Service (亦即 Kubernetes) 的時機

Azure Container Service 的最佳化組態受歡迎的開放原始碼工具和技術特別適用於 Azure。 您取得開啟的方案，可提供適用於您容器和應用程式組態的可攜性。 您選取大小、 主機數量及協調工具。 Azure Container Service 會為您處理基礎結構。

如果您已經使用 Kubernetes、 Docker Swarm 或 DC/OS 等的開放原始碼協調器，您不需要變更您現有的管理作法，將容器工作負載移至雲端。 使用您已經熟悉的應用程式管理工具，並透過標準 API 端點連線，為您選擇的 orchestrator。

如果您使用 Linux 的 Docker 容器，但可能只會處於預覽狀態適用於 Windows 容器，所有這些 orchestrator 是成熟的環境。

例如，在 Kubernetes 中，支援容器是原生 （第一等公民），因此在 Kubernetes 上使用 Windows 容器也很有效 （在 ACS 中 2018 年初起為預覽版）。

重要事項：進化版和 「 多個 PaaS"kubernetes 的 ACS (Azure Container Service) 的版本不 AKS (Azure Kubernetes Service)，不過，自 Q2 2018 起，仍不支援 Windows 容器，但它即將推出支援。

>[!div class="step-by-step"]
>[上一頁](when-to-deploy-windows-containers-to-azure-container-instances-ACI.md)
>[下一頁](choosing-azure-compute-options-for-container-based-applications.md)
