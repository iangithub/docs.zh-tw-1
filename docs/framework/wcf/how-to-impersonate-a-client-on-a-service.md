---
title: 作法：在服務上模擬用戶端
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, impersonation
- impersonation
- WCF, security
ms.assetid: 431db851-a75b-4009-9fe2-247243d810d3
ms.openlocfilehash: 3dd40efe27687b048984c4592db0d3787d061eeb
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2019
ms.locfileid: "67402328"
---
# <a name="how-to-impersonate-a-client-on-a-service"></a>作法：在服務上模擬用戶端
模擬的 Windows Communication Foundation (WCF) 服務上的用戶端，可讓服務代表用戶端執行動作。 關於存取控制清單 (ACL) 檢查的動作，例如存取機器上的目錄和檔案或存取 SQL Server 資料庫，請根據用戶端使用者帳戶檢查 ACL。 本主題說明在 Windows 網域中啟用用戶端以設定用戶端模擬等級所需的基本步驟。 如需此文件的實用範例，請參閱 [Impersonating the Client](../../../docs/framework/wcf/samples/impersonating-the-client.md)。 如需有關用戶端模擬的詳細資訊，請參閱 <<c0> [ 委派和模擬](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)。  
  
> [!NOTE]
>  用戶端和服務在相同電腦上執行，且用戶端在系統帳戶下執行時 (也就是 `Local System` 或 `Network Service`)，以可設定狀態的安全性內容權杖建立安全的工作階段時無法模擬用戶端。 WinForms 或主控台應用程式通常在目前登入的帳戶下執行，因此根據預設值可以模擬該帳戶。 不過，當用戶端 ASP.NET 網頁和該頁面裝載於 IIS 6.0 或 IIS 7.0 中，則用戶端未執行`Network Service`預設帳戶。 所有支援安全工作階段的系統提供繫結預設為使用沒有狀態的安全性內容權杖。 不過，如果用戶端是 ASP.NET 網頁，並使用以可設定狀態的安全性內容權杖的安全工作階段，就無法模擬該用戶端。 如需使用安全工作階段的可設定狀態的安全性內容權杖的詳細資訊，請參閱[How to:建立安全性內容權杖的安全工作階段](../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)。  
  
### <a name="to-enable-impersonation-of-a-client-from-a-cached-windows-token-on-a-service"></a>若要從服務上的快取 Windows 權杖啟用用戶端模擬  
  
1. 建立服務。 如需此基本程序的教學課程，請參閱 [Getting Started Tutorial](../../../docs/framework/wcf/getting-started-tutorial.md)。  
  
2. 使用運用 Windows 驗證並建立工作階段的繫結，例如 <xref:System.ServiceModel.NetTcpBinding> 或 <xref:System.ServiceModel.WSHttpBinding>。  
  
3. 建立服務的介面實作時，將 <xref:System.ServiceModel.OperationBehaviorAttribute> 類別套用至需要用戶端模擬的方法。 將 <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> 屬性設定為 <xref:System.ServiceModel.ImpersonationOption.Required>。  
  
     [!code-csharp[c_SimpleImpersonation#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_simpleimpersonation/cs/source.cs#2)]
     [!code-vb[c_SimpleImpersonation#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_simpleimpersonation/vb/source.vb#2)]  
  
### <a name="to-set-the-allowed-impersonation-level-on-the-client"></a>若要設定用戶端上的允許模擬等級  
  
1. 使用 [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)建立服務用戶端程式碼。 如需詳細資訊，請參閱 <<c0> [ 使用 WCF 用戶端存取服務](../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md)。  
  
2. 建立 WCF 用戶端之後, 設定<xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A>的屬性<xref:System.ServiceModel.Security.WindowsClientCredential>類別的其中一個<xref:System.Security.Principal.TokenImpersonationLevel>列舉值。  
  
    > [!NOTE]
    >  若要使用 <xref:System.Security.Principal.TokenImpersonationLevel.Delegation>，必須使用交涉的 Kerberos 驗證 (有時稱為 *multi-leg* 或 *multi-step* Kerberos)。 如需如何實作此的說明，請參閱 <<c0> [ 安全性的最佳做法](../../../docs/framework/wcf/feature-details/best-practices-for-security-in-wcf.md)。  
  
     [!code-csharp[c_SimpleImpersonation#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_simpleimpersonation/cs/source.cs#1)]
     [!code-vb[c_SimpleImpersonation#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_simpleimpersonation/vb/source.vb#1)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.OperationBehaviorAttribute>
- <xref:System.Security.Principal.TokenImpersonationLevel>
- [模擬用戶端](../../../docs/framework/wcf/samples/impersonating-the-client.md)
- [委派和模擬](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)
