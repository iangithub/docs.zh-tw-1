---
title: Web 服務泛型序列化技術範例
ms.date: 03/30/2017
ms.assetid: cdc15ea4-f678-4729-8ebe-188ae720bef7
ms.openlocfilehash: b4aa9c21fa2bafce16e93a5d2479b17946dba41b
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490763"
---
# <a name="web-services-generics-serialization-technology-sample"></a>Web 服務泛型序列化技術範例
[下載範例](https://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Xml%20Serialization/GenericsSerialization.zip.exe)  
  
 此範例顯示如何在 ASP.NET Web 服務中使用及控制泛型的序列化。  
  
### <a name="to-build-the-sample-using-visual-studio"></a>若要使用 Visual Studio 建置範例  
  
1. 開啟 Visual Studio，然後從 [檔案]  功能表中選取 [新網站]  。  
  
2. 在 [新網站]  對話方塊的左窗格中選取想要的程式設計語言，再從右窗格中選取 [ASP.NET Web 服務]  。  
  
3. 按一下 [瀏覽]  並巡覽至 \CS\GenericsService 子目錄。  
  
4. 選取 Service.asmx，在 Visual Studio 中開啟該檔案。  
  
5. 在 [ **建置** ] 功能表上，按一下 [ **建置方案**]。  
  
> [!NOTE]
>  此清單中的前五個步驟是選擇性的。 .NET Framework 執行階段會在第一次要求服務時，自動產生 Web 服務。  
  
> [!NOTE]
>  以下為建置範例的必要步驟。  
  
1. 開啟檔案總管並巡覽至 \CS 子目錄。  
  
2. 以滑鼠右鍵按一下 GenericsService 子目錄的圖示，然後選取 [共用和安全性]  。  
  
3. 在 [Web 共用]  索引標籤中，選取 [共用此資料夾]  。  
  
> [!IMPORTANT]
>  記下 [別名]  窗格中列出的虛擬目錄名稱，因為執行範例時會需要這個名稱。  
  
### <a name="to-build-the-sample-using-internet-information-services"></a>若要使用網際網路資訊服務建置範例  
  
1. 開啟 [網際網路資訊服務]  管理嵌入式管理單元，並展開 [網站]  。  
  
2. 以滑鼠左鍵按一下 [預設的網站]  ，然後依序選取 [新增]  、[虛擬目錄]  以建立 [虛擬目錄建立精靈]  。  
  
3. 按 [下一步]  ，輸入虛擬目錄的公用別名，再按 [下一步]  。  
  
4. 輸入儲存範例所在目錄的路徑 (通常是 \CS\GenericsService 子目錄)，然後按 [下一步]  。 按 [下一步]  完成精靈。  
  
> [!IMPORTANT]
>  記下 [別名]  窗格中列出的虛擬目錄名稱，因為執行範例時會需要這個名稱。  
  
### <a name="to-run-the-sample"></a>若要執行範例  
  
1. 開啟瀏覽器視窗，並選取網址列。  
  
2. 型別`http://localhost/[virtual directory]/Service.asmx`，其中`[virtual directory]`代表建置範例時所建立的虛擬目錄。  
  
## <a name="remarks"></a>備註  
 範例會顯示預設的 ASP.NET 網頁，其中包含 Web 服務定義的連結。 除了修改 Web 服務的原始程式碼之外，您還可以自訂顯示內容。 如需詳細資訊，請參閱[建置 XML Web Service 用戶端](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w3h45ebk(v=vs.100))。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Collections.Generic>
- <xref:System.Web.Services>
- <xref:System.Xml.Serialization>
- [序列化](../../../docs/standard/serialization/index.md)
- [使用 ASP.NET 和 XML Web Service 用戶端建立的 XML Web Service](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7bkzywba(v=vs.100))
