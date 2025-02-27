---
title: WCF 安全性中的密碼編譯靈活性
ms.date: 03/30/2017
ms.assetid: c2c549e5-ac19-40c5-b686-8f67f52b6dbf
ms.openlocfilehash: b8e3b6dc62baf31901520d7f5edac0529e937016
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490947"
---
# <a name="cryptographic-agility-in-wcf-security"></a>WCF 安全性中的密碼編譯靈活性

此範例示範如何在提供的密碼編譯的敏捷式實作 Windows Communication Foundation (WCF) 用戶端和服務中的標準/自訂演算法中指定。 此範例是由下列專案所組成：

**Service**

這是自我裝載的 WCF 服務可實作`ICalculator`介面，並保護端點使用<xref:System.ServiceModel.WSHttpBinding>安全工作階段與可靠工作階段停用。 這項服務會定義自訂的 `SecurityAlgorithmSuite` 類別，以指定用於訊息安全性的密碼編譯演算法。

**用戶端**

這是在成功驗證之後存取服務的 WCF 用戶端。 它會叫用由 `ICalculator` 介面公開並且由服務實作的作業。 這個用戶端還會定義相同的自訂 `SecurityAlgorithmSuite` 類別，以指定用於訊息安全性的密碼編譯演算法。

## <a name="to-use-this-sample"></a>若要使用這個範例

1. Visual Studio 2012 中開啟 CryptoAgility.sln 方案。

2. 按下 CTRL+SHIFT+B 以建置方案。

3. 開啟檔案總管並巡覽至 \WCF\Basic\Security\CryptoAgility\Service\bin 目錄系統管理員權限執行 service.exe 檔，以滑鼠右鍵按一下 service.exe 並選取**系統管理員身分執行**。

4. 巡覽至 \WCF\Basic\Security\CryptoAgility\Client\bin 目錄，並正常執行 client.exe 檔。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[Windows Communication Foundation (WCF) 和.NET Framework 4 的 Windows Workflow Foundation (WF) 範例](https://go.microsoft.com/fwlink/?LinkId=150780)以下載所有 Windows Communication Foundation (WCF) 和[!INCLUDE[wf1](../../../../includes/wf1-md.md)]範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Security\CryptoAgility`

## <a name="see-also"></a>另請參閱

- [Windows Communication Foundation 安全性](../feature-details/security.md)
