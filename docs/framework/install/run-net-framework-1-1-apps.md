---
title: 在 Windows 8、Windows 8.1 或 Windows 10 上執行 .NET Framework 1.1 應用程式
ms.date: 05/26/2017
helpviewer_keywords:
- Windows 8, running .NET Framework 1.1 apps
- .NET Framework 1.1, running on Windows 8
ms.assetid: fb14e195-fea5-4561-b9a8-60a67283edb9
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3ad78c9a277af23eebe357ef986ea59d16bb444e
ms.sourcegitcommit: 34593b4d0be779699d38a9949d6aec11561657ec
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2019
ms.locfileid: "66833741"
---
# <a name="run-net-framework-11-apps-on-windows-8-windows-81-or-windows-10"></a>在 Windows 8、Windows 8.1 或 Windows 10 上執行 .NET Framework 1.1 應用程式

[!INCLUDE[win8](../../../includes/win8-md.md)]、[!INCLUDE[win81](../../../includes/win81-md.md)]、[!INCLUDE[winserver8](../../../includes/winserver8-md.md)]、[!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] 或 Windows 10 作業系統不支援 .NET Framework 1.1。 在某些情況下，會將 .NET Framework 1.1 明確視為執行應用程式所需的必要項。 在這些情況下，您應該連絡您的獨立軟體廠商 (ISV) 將應用程式升級，以便在 .NET Framework 3.5 SP1 或更新版本上執行。 如需其他資訊，請參閱[從 .NET Framework 1.1 移轉](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md)。

## <a name="install-the-net-framework-11-from-a-cd-or-download-center"></a>從光碟或下載中心安裝 .NET Framework 1.1

在 [!INCLUDE[win8](../../../includes/win8-md.md)]、[!INCLUDE[win81](../../../includes/win81-md.md)]、[!INCLUDE[winserver8](../../../includes/winserver8-md.md)]、[!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] 或 Windows 10 上無法手動安裝 .NET Framework 1.1。 它不再受支援。 如果您嘗試安裝該套件，即會顯示下面錯誤訊息：「安裝程式無法繼續，因為這個 .NET Framework 版本與之前安裝的版本不相容」。 若要解決這個問題，請安裝 [.NET Framework 3.5 SP1](https://www.microsoft.com/download/details.aspx?id=22)。 此版本包含 .NET Framework 2.0 (.NET Framework 1.1 的下一版)，[!INCLUDE[win8](../../../includes/win8-md.md)]、[!INCLUDE[win81](../../../includes/win81-md.md)] 及 Windows 10 全都支援此版本。 您一定要先嘗試安裝應用程式，判斷它是否會自動更新為較新版本的 .NET Framework。 如果沒有，請連絡您的 ISV 以取得應用程式更新。

## <a name="see-also"></a>另請參閱

- [從 .NET Framework 1.1 移轉](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md)
- [在 Windows 10、Windows 8.1 及 Windows 8 上安裝 .NET Framework 3.5](../../../docs/framework/install/dotnet-35-windows-10.md)
