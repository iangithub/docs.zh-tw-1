---
title: WCF Web HTTP 程式設計模型概觀
ms.date: 03/30/2017
ms.assetid: 381fdc3a-6e6c-4890-87fe-91cca6f4b476
ms.openlocfilehash: d4908eb75324d4316ea615d1a0acc286750752e7
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487711"
---
# <a name="wcf-web-http-programming-model-overview"></a>WCF Web HTTP 程式設計模型概觀
Windows Communication Foundation (WCF) WEB HTTP 程式設計模型提供建置 wcf WEB HTTP 服務所需的基本項目。 WCF WEB HTTP 服務設計用來存取最廣泛的可能的用戶端，包括網頁瀏覽器，並具有下列獨特的需求：  
  
- **Uri 和 URI 處理**Uri 在 WEB HTTP 服務的設計中扮演重要角色。 WCF WEB HTTP 程式設計模型運用<xref:System.UriTemplate>和<xref:System.UriTemplateTable>類別來提供 URI 處理能力。  
  
- **GET 和 POST 作業的支援**WEB HTTP 服務還運用了 GET 動詞來擷取資料，除了各種叫用的資料修改與遠端叫用的動詞命令。 WCF WEB HTTP 程式設計模型運用<xref:System.ServiceModel.Web.WebGetAttribute>和<xref:System.ServiceModel.Web.WebInvokeAttribute>建立的關聯服務作業同時與 GET 及其他 HTTP 動詞命令，例如 PUT、 POST、 和刪除。  
  
- **多個資料格式**Web 樣式服務能夠處理許多種類的資料，包括 SOAP 訊息。 WCF WEB HTTP 程式設計模型運用<xref:System.ServiceModel.WebHttpBinding>和<xref:System.ServiceModel.Description.WebHttpBehavior>來支援許多不同的資料格式，包括 XML 文件、 JSON 資料物件和的二進位內容，例如影像、 視訊檔案或純文字資料流。  
  
 WCF WEB HTTP 程式設計模型延伸來涵蓋 Web 樣式案例，包括 WEB HTTP 服務、 AJAX 和 JSON 服務，以及新聞訂閱 (ATOM/RSS) 摘要的 WCF 範圍。 如需 AJAX 和 JSON 服務的詳細資訊，請參閱[AJAX 整合與 JSON 支援](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)。 如需有關新聞訂閱的詳細資訊，請參閱[WCF 新聞訂閱概觀](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)。  
  
 可從 WEB HTTP 服務傳回的資料型別沒有額外的限制。 WEB HTTP 服務作業可傳回任何可序列化型別。 因為 WEB HTTP 服務作業可由 Web 瀏覽器叫用，所以可在 URL 中指定的資料型別具有一項限制。 如需預設支援哪些類型的詳細資訊請參閱 < **UriTemplate 查詢字串參數和 Url**下一節。 您可以提供自己的 T:System.ServiceModel.Dispatcher.QueryStringConverter 實作來變更預設行為，其中指定如何將 URL 中指定的參數轉換成實際的參數型別。 如需詳細資訊，請參閱<xref:System.ServiceModel.Dispatcher.QueryStringConverter>。  
  
> [!CAUTION]
>  使用 WCF WEB HTTP 程式設計模型撰寫的服務不會使用 SOAP 訊息。 因為未使用 SOAP，則無法使用由 WCF 所提供的安全性功能。 不過，您可透過以 HTTPS 裝載服務的方式來使用傳輸型安全性。 如需有關 WCF 安全性的詳細資訊，請參閱[安全性概觀](../../../../docs/framework/wcf/feature-details/security-overview.md)  
  
> [!WARNING]
>  安裝適用於 IIS 的 WebDAV 延伸模組可能會導致 Web HTTP 服務傳回 HTTP 405 錯誤，因為 WebDAV 延伸模組會嘗試處理所有 PUT 要求。 若要解決此問題，您可以解除安裝 WebDAV 延伸模組或停用網站的 WebDAV 延伸模組。 如需詳細資訊，請參閱[IIS 和 WebDav](https://learn.iis.net/page.aspx/357/webdav-for-iis-70/)  
  
## <a name="uri-processing-with-uritemplate-and-uritemplatetable"></a>使用 UriTemplate 和 UriTemplateTable 來進行 URI 處理  
 URI 範本提供一個有效的語法，以便表示大量結構上類似的 URI 集合。 例如，下列範本會表示以 "a" 開頭及以 "c" 結尾的所有三段式 URI 集合 (不論是否有中繼區段：a/{segment}/c)。  
  
 此範本會說明類似下列的 URI：  
  
- a/x/c  
  
- a/y/c  
  
- a/z/c  
  
- 等等。  
  
 在此範本中，大括號標記法 ("{segment}") 表示變數區段，而不是常值。  
  
 .NET Framework 提供可以使用 <xref:System.UriTemplate> 這種 URI 範本的應用程式開發介面。 `UriTemplates` 可讓您執行下列作業：  
  
- 您可以呼叫其中一個`Bind`方法的參數來產生一組*完全封閉式 URI* ，符合的範本。 意思就是，URI 範本中的所有變數都會以實際值來取代。  
  
- 您可以使用候選 URI 來呼叫 `Match`()，以便透過範本將候選 URI 切割為自身的構成部分，並傳回包含不同的 URI (已依據範本中的變數加上標籤) 部分的字典。  
  
- `Bind`() 和 `Match`() 都是反向值，因此您可以呼叫 `Match`( `Bind`( x ) ) 並從一開始的相同環境重新開始。  
  
 在許多情況下 (特別是在伺服器上，需要根據 URI 將要求分派到服務作業時) 您都想要追蹤資料結構中可以獨立處理每一個包含的範本的 <xref:System.UriTemplate> 物件集合。 <xref:System.UriTemplateTable> 表示一組 URI 範本，並且依據一組指定的範本及候選 URI 選取最佳對象。 這不是屬於任何特定的網路堆疊 （包含 WCF） 讓您可以在必要時使用它。  
  
 WCF 服務模型會透過 <xref:System.UriTemplate> 和 <xref:System.UriTemplateTable> 將服務作業與 <xref:System.UriTemplate> 所描述的 URI 集合關聯在一起。 服務作業會透過 <xref:System.UriTemplate> 或 <xref:System.ServiceModel.Web.WebGetAttribute>，與 <xref:System.ServiceModel.Web.WebInvokeAttribute> 產生關聯。 如需詳細資訊<xref:System.UriTemplate>並<xref:System.UriTemplateTable>，請參閱[UriTemplate 與 UriTemplateTable](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md)  
  
## <a name="webget-and-webinvoke-attributes"></a>WebGet 和 WebInvoke 屬性  
 WCF WEB HTTP 服務，讓使用擷取動詞 (例如 HTTP GET) 除了各種叫用動詞 （例如 HTTP POST、 PUT 和 DELETE）。 WCF WEB HTTP 程式設計模型可讓服務開發人員，同時控制 URI 範本和其服務作業相關聯的動詞<xref:System.ServiceModel.Web.WebGetAttribute>和<xref:System.ServiceModel.Web.WebInvokeAttribute>。 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute> 可讓您控制個別作業如何繫結至 URI 及與這些 URI 相關聯的 HTTP 方法。 例如，在下列程式碼中新增 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute>。  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It"  
  
  [WebGet]  
  Customer GetCustomer():  
  
  //"Do It"  
    [WebInvoke]  
  Customer UpdateCustomerName( string id,   
                               string newName );  
}  
```  
  
 先前的程式碼可讓您進行下列 HTTP 要求。  
  
 `GET /GetCustomer`  
  
 `POST /UpdateCustomerName`  
  
 <xref:System.ServiceModel.Web.WebInvokeAttribute> 會預設為 POST，但是您還是可以用它來控制其他動詞。  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It" -> HTTP GET  
    [WebGet( UriTemplate="customers/{id}" )]  
  Customer GetCustomer( string id ):  
  
  //"Do It" -> HTTP PUT  
  [WebInvoke( UriTemplate="customers/{id}", Method="PUT" )]  
  Customer UpdateCustomer( string id, Customer newCustomer );  
}  
```  
  
 若要查看使用 WCF WEB HTTP 程式設計模型的 WCF 服務的完整範例，請參閱[How to:建立基本 WCF Web HTTP 服務](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-wcf-web-http-service.md)  
  
## <a name="uritemplate-query-string-parameters-and-urls"></a>UriTemplate 查詢字串參數和 URL  
 您可以輸入與服務作業關聯的 URL，透過網頁瀏覽器呼叫 Web 樣式服務。 這些服務作業可接受的查詢字串參數，必須在 URL 中以字串格式指定。 下表說明可由 URL 傳遞的型別及採用的格式。  
  
|類型|格式|  
|----------|------------|  
|<xref:System.Byte>|0 - 255|  
|<xref:System.SByte>|-128 - 127|  
|<xref:System.Int16>|-32768 - 32767|  
|<xref:System.Int32>|-2,147,483,648 - 2,147,483,647|  
|<xref:System.Int64>|-9,223,372,036,854,775,808 - 9,223,372,036,854,775,807|  
|<xref:System.UInt16>|0 - 65535|  
|<xref:System.UInt32>|0 - 4,294,967,295|  
|<xref:System.UInt64>|0 - 18,446,744,073,709,551,615|  
|<xref:System.Single>|-3.402823e38 - 3.402823e38 (不需要指數標記法)|  
|<xref:System.Double>|-1.79769313486232e308 - 1.79769313486232e308 (不需要指數標記法)|  
|<xref:System.Char>|任何單一字元|  
|<xref:System.Decimal>|標準標記法中任何一個小數 (不含指數)|  
|<xref:System.Boolean>|True 或 False (不區分大小寫)|  
|<xref:System.String>|任何字串 (不支援 null 字串且不會進行逸出)|  
|<xref:System.DateTime>|MM/DD/YYYY<br /><br /> MM/DD/YYYY HH:MM:SS [AM&#124;PM]<br /><br /> 月/日/年<br /><br /> 月份日期年 hh: mm: [上午&#124;PM]|  
|<xref:System.TimeSpan>|DD.HH:MM:SS<br /><br /> 其中 DD = 天數，HH = 小時，MM = 分鐘，SS = 秒數|  
|<xref:System.Guid>|GUID，例如：<br /><br /> 936DA01F-9ABD-4d9d-80C7-02AF85C822A8|  
|<xref:System.DateTimeOffset>|MM/DD/YYYY HH:MM:SS MM:SS<br /><br /> 其中 DD = 天數，HH = 小時，MM = 分鐘，SS = 秒數|  
|列舉|列舉值，依下列程式碼示範的方式定義列舉。<br /><br /> `public enum Days{ Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };`<br /><br /> 任何個別的列舉值 (或其對應的整數值) 都可以在查詢字串中指定。|  
|具有可以在型別和字串表示之間相互轉換之 `TypeConverterAttribute` 的型別。|取決於型別轉換子。|  
  
## <a name="formats-and-the-wcf-web-http-programming-model"></a>格式與 WCF WEB HTTP 程式設計模型  
 WCF WEB HTTP 程式設計模型的新功能可與許多不同的資料格式一起運作。 在繫結層，<xref:System.ServiceModel.WebHttpBinding> 可以讀取並寫入下列不同種類的資料：  
  
- XML  
  
- JSON  
  
- 不透明的二進位資料流  
  
 這表示 WCF WEB HTTP 程式設計模型可以處理任何類型的資料，但您可能對程式設計<xref:System.IO.Stream>。  
  
 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)]支援 JSON 資料 (AJAX) 以及新聞訂閱摘要 (包括 ATOM 和 RSS)。 如需這些功能的詳細資訊，請參閱[WCF Web HTTP 格式化](../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md)[WCF 新聞訂閱概觀](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)並[AJAX 整合與 JSON 支援](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)。  
  
## <a name="wcf-web-http-programming-model-and-security"></a>WCF WEB HTTP 程式設計模型和安全性  
 因為 WCF WEB HTTP 程式設計模型不支援 WS-* 通訊協定，來保護 WCF WEB HTTP 服務的唯一方法是運用 SSL 透過 HTTPS 公開服務。 如需設定 IIS 7.0 與 SSL 的詳細資訊，請參閱[如何在 IIS 中實作 SSL](https://go.microsoft.com/fwlink/?LinkId=131613)  
  
## <a name="troubleshooting-the-wcf-web-http-programming-model"></a>WCF WEB HTTP 程式設計模型疑難排解  
 當呼叫 WCF WEB HTTP 服務以使用 <xref:System.ServiceModel.Channels.ChannelFactoryBase%601> 建立通道時，<xref:System.ServiceModel.Description.WebHttpBehavior> 會使用組態檔中設定的 <xref:System.ServiceModel.EndpointAddress>，即便傳遞至 <xref:System.ServiceModel.EndpointAddress> 的 <xref:System.ServiceModel.Channels.ChannelFactoryBase%601> 是另一個值亦然。  
  
## <a name="see-also"></a>另請參閱

- [WCF 摘要整合](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)
- [WCF Web HTTP 程式設計物件模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)
- [WCF Web HTTP 程式設計模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
