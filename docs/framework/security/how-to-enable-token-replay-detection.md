---
title: 如何：啟用權杖重新執行偵測
ms.date: 03/30/2017
ms.assetid: 5a9f5771-f5f6-4100-8501-406aa20d731a
author: BrucePerlerMS
ms.openlocfilehash: 0149bf424751a0c95337743b02465629826d9686
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2019
ms.locfileid: "64625855"
---
# <a name="how-to-enable-token-replay-detection"></a>如何：啟用權杖重新執行偵測
## <a name="applies-to"></a>適用於  
  
- Microsoft® Windows® Identity Foundation (WIF)  
  
- ASP.NET® Web Forms  
  
## <a name="summary"></a>總結  
 此操作說明提供了在使用 WIF 的 ASP.NET 應用程式中啟用權杖重新執行偵測的詳細逐步程序。 還提供了一些指示，說明如何測試應用程式來確認已啟用權杖重新執行偵測。 這篇使用方法文章並沒有提供建立 Security Token Service (STS) 的詳細指示，而是使用識別和存取工具隨附的「開發 STS」。 「開發 STS」並不會執行實際的驗證，而只是用於測試用途。 您必須安裝識別和存取工具才能完成這篇使用方法文章。 它可以從下列位置下載：[身分識別和存取工具](https://go.microsoft.com/fwlink/?LinkID=245849)  
  
## <a name="contents"></a>內容  
  
- 目標  
  
- 總覽  
  
- 步驟摘要  
  
- 步驟 1 – 建立簡單的 ASP.NET Web Forms 應用程式並啟用重新執行偵測  
  
- 步驟 2 – 測試方案  
  
## <a name="objectives"></a>目標  
  
- 建立從身分識別與存取工具使用 WIF 和開發 STS 的簡單 ASP.NET 應用程式  
  
- 啟用權杖重新執行偵測，並確認它能夠正常運作  
  
## <a name="overview"></a>總覽  
 當用戶端嘗試以用戶端已使用之 STS 權杖向信賴憑證者進行驗證時，就會發生重新執行攻擊。 為了協助避免這種攻擊，WIF 會包含先前所使用之 STS 權杖的重新執行偵測快取。 啟用時，重新執行偵測會檢查傳入要求的權杖，並確認先前是否已使用該權杖。 如果已使用該權杖，就會拒絕要求並擲回 <xref:System.IdentityModel.Tokens.SecurityTokenReplayDetectedException> 例外狀況。  
  
 下列步驟示範啟用重新執行偵測所需的組態變更。  
  
## <a name="summary-of-steps"></a>步驟摘要  
  
- 步驟 1 – 建立簡單的 ASP.NET Web Forms 應用程式並啟用重新執行偵測  
  
- 步驟 2 – 測試方案  
  
## <a name="step-1--create-a-simple-aspnet-web-forms-application-and-enable-replay-detection"></a>步驟 1 – 建立簡單的 ASP.NET Web Forms 應用程式並啟用重新執行偵測  
 在此步驟中，您將建立新的 ASP.NET Web Forms 應用程式，並修改 *Web.config* 檔案以啟用重新執行偵測。  
  
#### <a name="to-create-a-simple-aspnet-application"></a>建立簡單的 ASP.NET 應用程式  
  
1. 啟動 Visual Studio，並依序按一下 [檔案]  、[新增]  和 [專案]  。  
  
2. 在 [新增專案]  視窗中，按一下 [ASP.NET Web Forms 應用程式]  。  
  
3. 在 [名稱]  中，輸入 `TestApp`，然後按 [確定]  。  
  
4. 以滑鼠右鍵按一下方案總管  底下的 [TestApp]  專案，然後選取 [身分識別與存取]  。  
  
5. [身分識別與存取]  視窗隨即出現。 在 [提供者]  底下，選取 [Test your application with the Local Development STS] (使用本機開發 STS 測試應用程式}  ，然後按一下 [套用]  。  
  
6. 將下列 **\<tokenReplayDetection>** 項目加入至 *Web.config* 組態檔中緊接在 **\<system.identityModel>** 和 **\<identityConfiguration>** 項目後面的位置，如下所示：  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration>  
            <tokenReplayDetection enabled="true"/>  
    ```  
  
## <a name="step-2--test-your-solution"></a>步驟 2 – 測試方案  
 在此步驟中，您將測試啟用 WIF 的 ASP.NET 應用程式來確認已啟用重新執行偵測。  
  
#### <a name="to-test-your-wif-enabled-aspnet-application-for-replay-detection"></a>測試啟用 WIF 的 ASP.NET 應用程式的重新執行偵測  
  
1. 按 **F5** 鍵執行方案。 您應該會看到預設的 ASP.NET 首頁，並且會以使用者名稱 *Terry* (這是開發 STS 傳回的預設使用者) 自動進行驗證。  
  
2. 請按瀏覽器的**上一頁**按鈕。 您應該會看到 **'/' 應用程式中的伺服器錯誤**頁面描述如下：*ID1062:用於偵測重新執行：語彙基元：'System.IdentityModel.Tokens.SamlSecurityToken'* ，後面接著*AssertionId*並*簽發者*。  
  
     因為在偵測到權杖重新執行時，會擲回 <xref:System.IdentityModel.Tokens.SecurityTokenReplayDetectedException> 類型的例外狀況，所以您會看到此錯誤頁面。 發生此錯誤的原因是您在權杖第一次出現時，嘗試重新傳送初始 POST 要求。 **上一頁**按鈕不會造成後續的伺服器要求發生這種行為。
