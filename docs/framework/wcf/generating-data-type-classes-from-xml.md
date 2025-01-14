---
title: 從 XML 產生資料型別類型
ms.date: 03/30/2017
ms.assetid: e4e5e4e8-527f-44d1-92fa-8904a08784ea
ms.openlocfilehash: b99bb40105398dbd91b910c4a19828d069c3d9e7
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/30/2019
ms.locfileid: "66380213"
---
# <a name="generating-data-type-classes-from-xml"></a>從 XML 產生資料型別類型
.NET framework 4.5 還包括從 XML 產生資料類型類別的新功能。 本主題描述如何自動產生.NET 部落格 rss 摘要的 資料類型。  
  
### <a name="obtaining-the-xml-from-the-net-blog-rss-feed"></a>取得 XML.NET 部落格 rss 摘要  
  
1. 在 Internet Explorer 中，瀏覽至[.NET 部落格 RSS 摘要](https://devblogs.microsoft.com/dotnet/feed/)。  
  
2. 以滑鼠右鍵按一下  頁面上，然後選取**檢視原始檔**。  
  
3. 複製摘要的文字，按下**Ctrl + A**以選取所有文字，並**Ctrl + C**複製。  
  
### <a name="creating-the-data-types"></a>建立資料類型  
  
1. 開啟要使用 Proxy 的程式碼檔。 此檔案應該是.NET Framework 4.5 專案的一部分。  
  
2. 將游標放在檔案中任何現有類別以外的位置。  
  
3. 選取 **編輯**，**貼上特殊**，**貼上做為類別的 XML**。  
  
4. 類別，稱為`link`， `rss`， `rssChannel`， `rssChannelImage`，`rssChannelItem`和`rssChannelItemGuid`存取 RSS 摘要中的項目會建立具有必要的成員。  
  
### <a name="using-the-generated-classes"></a>使用產生的類別  
  
1. 這些類別一旦產生，就可以像其他類別一樣在程式碼中使用。 下列程式碼範例會傳回 `rssChannelImage` 類別的新執行個體。  
  
    ```  
    var channelImage = new rssChannelImage()   
    {   
        title = "MyImage",   
        link = "http://www.contoso.com/images/channelImage.jpg",   
        url = "http://www.contoso.com/entries/myEntry.html"   
    };  
    ```
