---
title: 工作流程<behavior> 的 <serviceBehaviors>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 6a4b718a-1b40-4957-935a-f6122819ab3c
ms.openlocfilehash: 99f98cba96ed924069ee14e1459e073ca88cd2b0
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67422975"
---
# <a name="behavior-of-servicebehaviors-of-workflow"></a>\<行為 > 的\<v > 工作流程
**行為**項目包含服務行為設定的集合。 每個行為由編製索引及其**名稱**。 服務可連結至每個透過名稱使用的行為**behaviorConfiguration**屬性[\<端點 >](../../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md)項目。 如此可允許端點共用通用行為組態，而不用重新定義設定。  
  
\<system.ServiceModel>  
\<behaviors>  
\<serviceBehaviors>  
\<behavior>  
  
## <a name="syntax"></a>語法  
  
```xml  
<system.ServiceModel>  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="String">
        <bufferReceive maxPendingMessagesPerChannel="Integer" />
        <etwTracking profileName="String" />
        <sendMessageChannelCache allowUnsafeCaching="Boolean">
          <channelSettings idleTimeout="TimeSpan" 
                           leaseTimeout="TimeSpan" 
                           maxItemsInCache="Integer" />
          <factorySettings idleTimeout="TimeSpan" 
                           leaseTimeout="TimeSpan" 
                           maxItemsInCache="Integer" />
        </sendMessageChannelCache>
        <sqlWorkflowInstanceStore connectionStringName="String" 
                                  hostLockRenewalPeriod="TimeSpan" 
                                  instanceCompletionAction="DeleteNothing/DeleteAll" 
                                  instanceEncodingAction="None/GZip" 
                                  instanceLockedExceptionAction="NoRetry/BasicRetry/AggressiveRetry" 
                                  runnableInstancesDetectionPeriod="TimeSpan" />
        <workflowIdle timeToPersist="TimeSpan" 
                      timeToUnload="TimeSpan" />
        <workflowUnhandledException action="Abandon/AbandonAndSuspend/Cancel/Terminate" />
      </behavior>
    </serviceBehaviors>  
  </behaviors>  
</system.ServiceModel>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列各節描述屬性、子項目和父項目。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|name|唯一的字串，其中包含行為的組態名稱。 這個值是使用者定義的字串，它必須是唯一的，因為它會充當項目的識別字串。|  
  
### <a name="child-elements"></a>子元素  
  
|項目|描述|  
|-------------|-----------------|  
|[\<bufferReceive>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/bufferreceive.md)|讓服務可以使用緩衝接收處理的服務行為，該處理可讓工作流程服務處理失序的訊息。|  
|[\<routing>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing-of-servicebehavior.md)|這個服務行為可讓服務能夠利用 ETW 追蹤使用<xref:System.Activities.Tracking.EtwTrackingParticipant>。|  
|[\<sendMessageChannelCache>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/sendmessagechannelcache.md)|服務行為可讓您自訂快取共用層級、 通道處理站快取的設定，以及傳送訊息至服務端點使用傳訊活動傳送的工作流程的通道快取的設定。|  
|[\<sqlWorkflowInstanceStore>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/sqlworkflowinstancestore.md)|可讓您設定的服務行為<xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>功能，支援的狀態資訊保存在 SQL Server 2005 或 SQL Server 2008 資料庫的工作流程服務執行個體。|  
|[\<workflowIdle>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflowidle.md)|這個服務行為可控制卸載及保存閒置工作流程執行個體的時間。|  
|[\<workflowInstanceManagement>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflowinstancemanagement.md)|可讓您指定設定的服務行為，這些設定會控制工作流程執行個體的執行方式，包括持續性、未處理的例外狀況行為和閒置行為。|  
|[\<workflowUnhandledException>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflowunhandledexception.md)|這個服務行為可讓您指定工作流程服務內發生未處理的例外狀況時要採取的動作。|  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<serviceBehaviors>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/servicebehaviors-of-workflow.md)|服務行為項目的集合。|
