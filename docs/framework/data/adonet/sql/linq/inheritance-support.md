---
title: 繼承支援
ms.date: 03/30/2017
ms.assetid: 19bb2794-b4e7-402e-8307-1d1517381a08
ms.openlocfilehash: 576fa896364d603f2cdbb7b6532e3efc3cd6f674
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67743080"
---
# <a name="inheritance-support"></a>繼承支援
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支援*單一資料表對應*。 換句話說，完整的繼承階層架構 (Inheritance Hierarchy) 會儲存在單一資料庫資料表中。 這張資料表包含整個階層架構中所有可能之資料行的平面聯集 (聯集是指將兩張原始資料表中的資料列集結，並去除重複資料列後所得到的單一資料表結果)。如果資料行不適用於資料列所代表之執行個體的型別，則該資料列中的該資料行會是 null。  
  
 單一資料表對應策略是最簡單的繼承表示，並且可以在許多不同類別的查詢中提供良好的效能特性。  
  
 若要在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中實作這個對應，則必須在繼承階層架構的根類別中指定屬性 (Attribute) 和屬性的屬性 (Attribute Property)。 如需詳細資訊，請參閱[如何：對應繼承階層架構](../../../../../../docs/framework/data/adonet/sql/linq/how-to-map-inheritance-hierarchies.md)。  
  
 使用 Visual Studio 的開發人員也可以使用物件關聯式設計工具來對應繼承階層架構。  
  
## <a name="see-also"></a>另請參閱

- [背景資訊](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)
