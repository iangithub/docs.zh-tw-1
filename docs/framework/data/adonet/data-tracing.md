---
title: ADO.NET 中的資料追蹤
ms.date: 03/30/2017
ms.assetid: a6a752a5-d2a9-4335-a382-b58690ccb79f
ms.openlocfilehash: 120a9e2a817401ba04e0dce8052caecb83115e0e
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66489529"
---
# <a name="data-tracing-in-adonet"></a>ADO.NET 中的資料追蹤

ADO.NET 具備內建資料追蹤功能的.NET 資料提供者所支援的 SQL Server、 Oracle、 OLE DB 和 ODBC，以及 ADO.NET <xref:System.Data.DataSet>，和 SQL Server 網路通訊協定。

追蹤資料存取 API 呼叫可協助診斷下列問題：

- 用戶端程式與資料庫之間的結構描述不符。

- 無法使用資料庫或網路程式庫發生問題。

- SQL 錯誤，該 SQL 是硬式編碼或應用程式所產生的。

- 錯誤的程式設計邏輯。

- 多個 ADO.NET 元件之間，或 ADO.NET 與您本身的元件之間互動所發生的問題。

為了支援不同的追蹤技術，我們製作了可擴充的追蹤，讓開發人員追蹤任何應用程式堆疊層級的問題。 雖然追蹤不是 ADO.NET 的特有功能，但 Microsoft 提供者可利用通用的追蹤和檢測應用程式開發介面。

如需有關設定和在 ADO.NET 中設定 managed 的追蹤的詳細資訊，請參閱[追蹤資料存取](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10))。

## <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>存取擴充事件記錄中的診斷資訊

在 .NET Framework Data Provider for SQL Server，資料存取追蹤 ([資料存取追蹤](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10))) 已經更新，以方便您更輕鬆地從相互關聯用戶端事件與診斷資訊，例如連線失敗伺服器連接信號緩衝區與應用程式效能資訊的擴充的事件記錄檔中。 如需有關讀取擴充的事件記錄檔的詳細資訊，請參閱[檢視事件工作階段資料](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/hh710068(v=sql.110))。

ADO.NET 會傳送用戶端連接 ID 以進行連接作業。 如果連線失敗，您可以存取連接信號緩衝區 ([連線疑難排解 SQL Server 2008 中與連接信號緩衝區](https://go.microsoft.com/fwlink/?LinkId=207752))，並尋找`ClientConnectionID`欄位，並取得相關診斷資訊連接失敗。 只有在發生錯誤時，用戶端連接 ID 才會記錄在信號緩衝區中 (如果在傳送登入前封包之前連接失敗，就不會產生用戶端連接 ID)。用戶端連接 ID 是 16 個位元組的 GUID。 如果在擴充事件工作階段中將 `client_connection_id` 動作加入到事件中，您還可以在擴充事件目標輸出中尋找用戶端連接 ID。 如需進一步的用戶端驅動程式診斷協助，您可以啟用資料存取追蹤並傳回連接命令，同時觀察資料存取追蹤當中的 `ClientConnectionID` 欄位。

您可以使用 `SqlConnection.ClientConnectionID` 屬性，以程式設計方式取得用戶端連接 ID。

成功建立連接的 `ClientConnectionID` 物件可取得 <xref:System.Data.SqlClient.SqlConnection>。 如果連接嘗試失敗，可能可以透過 `ClientConnectionID` 取得 `SqlException.ToString`。

ADO.NET 也會傳送特定執行緒活動 ID。 如果工作階段啟動 TRACK_CAUSALITY 選項啟用擴充的事件工作階段中擷取的活動識別碼。 若要解決與使用中連接相關的效能問題，您可以從用戶端的資料存取追蹤 (`ActivityID`欄位) 取得活動 ID，然後在擴充事件記錄中找到活動 ID。 擴充事件記錄中的活動 ID 是 16 個位元組的 GUID (和用戶端連接 ID 的 GUID 不同)，並且附加一個四位元組的序號。 序列號代表要求在執行緒中的順序，並且表示該執行緒的批次和 RPC 陳述式的相對順序。 啟用資料存取追蹤功能，而且開啟資料存取追蹤組態字詞中的第 18 個位元時，目前會選擇性地傳送 SQL 批次陳述式和 RPC 要求的 `ActivityID`。

以下是使用 TRANSACT-SQL 啟動擴充的事件工作階段，將會儲存在信號緩衝區，並將記錄從 RPC 和批次作業上的用戶端傳送的活動識別碼的範例。

```sql
create event session MySession on server
add event connectivity_ring_buffer_recorded,
add event sql_statement_starting (action (client_connection_id)),
add event sql_statement_completed (action (client_connection_id)),
add event rpc_starting (action (client_connection_id)),
add event rpc_completed (action (client_connection_id))
add target ring_buffer with (track_causality=on)
```

## <a name="see-also"></a>另請參閱

- [以 .NET Framework 進行網路追蹤](../../../../docs/framework/network-programming/network-tracing.md)
- [追蹤和檢測應用程式](../../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)
- [ADO.NET Managed 提供者和 DataSet 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=217917)
