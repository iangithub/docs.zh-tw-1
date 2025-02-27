---
title: Managed 執行緒處理
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], about threading
- managed threading
ms.assetid: 7b46a7d9-c6f1-46d1-a947-ae97471bba87
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f51920bceef6e83af4f6ef029eb49ae495a58b9b
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490852"
---
# <a name="managed-threading"></a>Managed 執行緒處理
不論您開發的是搭載一或多個處理器的電腦，即使應用程式目前正在執行其他工作，您還是希望應用程式能以最快速度與使用者互動。 使用多執行緒的執行是一種讓應用程式能迅速回應使用者，同時能夠在使用者事件之間或甚至在使用者事件當中善用處理器的強大方法。 雖然本節將介紹執行緒處理的基本概念，但是重點會放在 Managed 執行緒處理概念和如何使用 Managed 執行緒處理。  
  
> [!NOTE]
>  從 .NET Framework 4 開始，多執行緒的程式設計已透過 <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 類別、[平行 LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)、<xref:System.Collections.Concurrent?displayProperty=nameWithType> 命名空間中的新並行集合類別，以及以工作 (而非執行緒) 概念為基礎的新程式設計模型，而做出大幅簡化。 如需詳細資訊，請參閱[平行程式設計](../../../docs/standard/parallel-programming/index.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [Managed 執行緒處理的基本概念](../../../docs/standard/threading/managed-threading-basics.md)  
 提供 Managed 執行緒處理的概觀，並討論何時使用多個執行緒。  
  
 [使用執行緒和執行緒處理](../../../docs/standard/threading/using-threads-and-threading.md)  
 說明如何建立、啟動、暫停、繼續和中止執行緒。  
  
 [Managed 執行緒處理的最佳實施方針](../../../docs/standard/threading/managed-threading-best-practices.md)  
 討論同步處理的層級、如何避免死結和競爭條件，以及其他執行緒處理問題。  
  
 [執行緒物件和功能](../../../docs/standard/threading/threading-objects-and-features.md)  
 描述可用來同步執行緒活動的 Managed 類別，以及在不同執行緒上存取的物件資料，並提供執行緒集區執行緒的概觀。  
  
## <a name="reference"></a>參考資料  
 <xref:System.Threading>  
 包含使用和同步 Managed 執行緒的類別。  
  
 <xref:System.Collections.Concurrent>  
 包含可安全用於多個執行緒的集合類別。  
  
 <xref:System.Threading.Tasks>  
 包含建立和排程並行處理工作的類別。  
  
## <a name="related-sections"></a>相關章節  
 [應用程式定義域](../../../docs/framework/app-domains/application-domains.md)  
 提供應用程式定義域的概觀及通用語言基礎結構如何使用它們。  
  
 [Asynchronous File I/O](../../../docs/standard/io/asynchronous-file-i-o.md)  
 描述非同步 I/O 的效能利益和基本作業。  
  
 [工作式非同步模式 (TAP)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)  
 提供 .NET 中非同步程式設計建議模式的概觀。  
  
 [非同步呼叫同步方法](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)  
 說明如何使用內建的委派功能在執行緒集區執行緒上呼叫方法。  
  
 [平行程式設計](../../../docs/standard/parallel-programming/index.md)  
 描述平行程式設計程式庫，簡化應用程式中多個執行緒的用法。  
  
 [平行 LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)  
 描述以平行方式執行查詢的系統，以善用多個處理器。
