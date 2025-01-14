---
title: 交易管理擴大規模
ms.date: 03/30/2017
ms.assetid: 1e96331e-31b6-4272-bbbd-29ed1e110460
ms.openlocfilehash: df2597d6fcce7fbd51f6f17bd42469cb7fcf3fdf
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2019
ms.locfileid: "67662453"
---
# <a name="transaction-management-escalation"></a>交易管理擴大規模
Windows 會裝載一組服務與模組，用以構成交易管理員。 交易管理員擴大規模說明了將交易從某個交易管理員的元件移轉到另一個元件上的處理序。  
  
 <xref:System.Transactions> 包含協調交易，最多涉及單一永久性資源或多個變動性資源的交易管理員元件。 由於交易管理員只使用應用程式內部的網域呼叫，因此可得到最佳效能。 開發人員不需要直接與交易管理員互動。 反之，<xref:System.Transactions> 命名空間會提供用來定義介面、泛型行為，與 Helper 類別的泛型基礎結構。  
  
 當您想要提供給其他應用程式定義域 （包含跨處理序與電腦界限） 中的物件交易的相同電腦上，<xref:System.Transactions>基礎結構會自動擴大由 Microsoft 管理交易分散式的交易協調器 (MSDTC)。 如果您登記了另一項永久性資源管理員，也會發生擴大規模的情況。 規模一旦擴大，交易在完成之前會一直維持在提升狀態下。  
  
 在 <xref:System.Transactions> 交易與 MSDTC 交易之間，有一種透過可提升單一階段登記 (PSPE) 提供的中繼交易型別。 PSPE 是 <xref:System.Transactions> 用來最佳化效能的另一種重要機制。 它能允許位於不同應用程式定義域、處理序或電腦上的遠端永久性茲原參與 <xref:System.Transactions> 交易，而不會擴大到 MSDTC 交易規模。 如需 PSPE 的詳細資訊，請參閱[編列的資源，在交易中的參與者](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md)。  
  
## <a name="how-escalation-is-initiated"></a>擴大規模的啟始方式  
 交易擴大規模會因為 MSDTC 駐留在不同的處理序中而降低效能，並在訊息於處理序之間傳遞時，將交易規模擴大到 MSDTC 結果。 若要改善效能，您應該延遲，或避免擴大到 MSDTC;因此，您需要知道如何及何時要起始擴大規模。  
  
 只要 <xref:System.Transactions> 基礎結構持續處理變動性資源與最多一個永久性資源以支援單一階段告知，<xref:System.Transactions> 基礎結構就會持續保有交易。 交易管理員只會提供自己駐留在相同應用程式定義域中，且不需要記錄 (將交易結果寫入磁碟) 的資源。 在下列情況下，如果 <xref:System.Transactions> 基礎結構將交易的擁有權轉移給 MSDTC，將導致擴大規模：  
  
- 交易中至少會登記一個不支援單一階段告知的永久性資源。  
  
- 交易中至少會登記兩個支援單一階段告知的永久性資源。 例如，登錄與 SQL Server 2005 的單一連線不會造成交易升級。 不過，每當您開啟第二個連接至 SQL Server 2005 資料庫，導致資料庫登記，<xref:System.Transactions>基礎結構會偵測它是在交易中，第二個永久性資源，並擴大到 MSDTC 交易。  
  
- 這時會叫用將交易「封送處理」到不同的應用程式定義域或不同的處理序的要求。 例如，跨應用程式定義域界限的交易物件序列化。 交易物件是由數值所封送處理，代表任何嘗試跨應用程式定義域界限將其傳送出去的動作 (即使處於相同的處理序中) 將導致交易物件的序列化。 您可以在使用 <xref:System.Transactions.Transaction> 做為參數的遠端方法上進行呼叫，或是嘗試存取遠端交易服務型元件，來傳送交易物件。 這項作業會序列化交易物件並導致規模擴大，如同當交易已經跨應用程式定義域序列化一樣。 接著此物件會被分配出去，這時本機交易管理員就不會有足夠的物件。  
  
 下表列出在擴大規模期間可擲回的所有可能例外狀況。  
  
|例外狀況類型|條件|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|使用相當於 <xref:System.Transactions.IsolationLevel.Snapshot> 的隔離等級來擴大交易規模的嘗試。|  
|<xref:System.Transactions.TransactionAbortedException>|交易管理員已關閉。|  
|<xref:System.Transactions.TransactionException>|擴大規模會失敗並中止應用程式。|
