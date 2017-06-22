---
title: "프로그래밍 방식으로 복제 모니터링 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- sp_replmonitorhelppublisher
- sp_replmonitorhelpmergesessiondetail
- monitoring performance [SQL Server replication], publication status
- sp_replmonitorhelpmergesession
- sp_replmonitorhelppublicationthresholds
- monitoring performance [SQL Server replication], subscription status
- monitoring performance [SQL Server replication], Transact-SQL programming
- sp_replmonitorsubscriptionpendingcmds
- sp_replmonitorchangepublicationthreshold
- transactional replication, monitoring
- sp_replmonitorhelppublication
- sp_replmonitorhelpsubscription
- monitoring performance [SQL Server replication], thresholds and warnings
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b05b9c5af4ff9ed8626773fc6714c2c05f1605b2
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="programmatically-monitor-replication"></a>프로그래밍 방식으로 복제 모니터링
  복제 모니터는 복제 토폴로지를 모니터링하는 데 사용할 수 있는 그래픽 도구입니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 복제 저장 프로시저 또는 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 동일한 모니터링 데이터에 액세스할 수 있습니다. 이러한 개체를 사용하면 다음 태스크를 프로그래밍할 수 있습니다.  
  
-   게시자, 게시 및 구독의 상태 모니터링  
  
-   하나 이상의 구독자에서 병합 에이전트 세션 모니터링  
  
-   하나 이상의 구독자에서 적용 대기 중인 트랜잭션 명령 모니터링  
  
-   게시에 개입이 필요한 시기를 결정하는 임계값 메트릭 정의  
  
-   추적 프로그램 토큰의 상태 모니터링.  
  
 **항목 내용**  
  
 [Transact-SQL](#Tsql)  
  
 [RMO(복제 관리 개체)](#RMO)  
  
##  <a name="Tsql"></a> Transact-SQL  
  
#### <a name="to-monitor-publishers-publications-and-subscriptions-from-the-distributor"></a>배포자에서 게시자, 게시 및 구독을 모니터링하려면  
  
1.  배포 데이터베이스의 배포자에서 [sp_replmonitorhelppublisher](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)를 실행합니다. 이렇게 하면 이 배포자를 사용하는 모든 게시자에 대한 모니터링 정보가 반환됩니다. 결과 집합을 단일 게시자로 제한하려면 **@publisher**를 실행합니다.  
  
2.  배포 데이터베이스의 배포자에서 [sp_replmonitorhelppublication](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)을 실행합니다. 이렇게 하면 이 배포자를 사용하는 모든 게시에 대한 모니터링 정보가 반환됩니다. 결과 집합을 단일 게시자, 게시 또는 게시된 데이터베이스로 제한하려면 각각 **@publisher**, **@publication**또는 **@publisher_db**를 지정합니다.  
  
3.  배포 데이터베이스의 배포자에서 [sp_replmonitorhelpsubscription](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)을 실행합니다. 이렇게 하면 이 배포자를 사용하는 모든 구독에 대한 모니터링 정보가 반환됩니다. 결과 집합을 단일 게시자, 게시 또는 게시된 데이터베이스에 속하는 구독으로 제한하려면 각각 **@publisher**, **@publication**또는 **@publisher_db**를 지정합니다.  
  
#### <a name="to-monitor-transactional-commands-waiting-to-be-applied-at-the-subscriber"></a>구독자에서 적용 대기 중인 트랜잭션 명령을 모니터링하려면  
  
1.  배포 데이터베이스의 배포자에서 [sp_replmonitorsubscriptionpendingcmds](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md)를 실행합니다. 이렇게 하면 이 배포자를 사용하는 모든 구독에 대해 보류 중인 모든 명령의 모니터링 정보가 반환됩니다. 결과 집합을 단일 게시자, 구독자, 게시 또는 게시된 데이터베이스에 속하는 구독에 대해 보류 중인 명령으로 제한하려면 각각 **@publisher**, **@subscriber**, **@publication**또는 **@publisher_db**를 지정합니다.  
  
#### <a name="to-monitor-merge-changes-waiting-to-be-uploaded-or-downloaded"></a>업로드 또는 다운로드 대기 중인 병합 변경 내용을 모니터링하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)를 실행합니다. 이렇게 하면 구독자에 대해 복제 대기 중인 변경 내용에 대한 정보를 보여 주는 결과 집합이 반환됩니다. 결과 집합을 단일 게시 또는 아티클에 속하는 변경 내용으로 제한하려면 각각 **@publication** 또는 **@article**를 지정합니다.  
  
2.  구독 데이터베이스의 구독자에서 [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)를 실행합니다. 이렇게 하면 게시자에 대해 복제 대기 중인 변경 내용에 대한 정보를 보여 주는 결과 집합이 반환됩니다. 결과 집합을 단일 게시 또는 아티클에 속하는 변경 내용으로 제한하려면 각각 **@publication** 또는 **@article**를 지정합니다.  
  
#### <a name="to-monitor-merge-agent-sessions"></a>병합 에이전트 세션을 모니터링하려면  
  
1.  배포 데이터베이스의 배포자에서 [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)을 실행합니다. 이렇게 하면 이 배포자를 사용하는 모든 구독의 모든 병합 에이전트 세션에 대해 **Session_id**를 포함한 모니터링 정보가 반환됩니다. **MSmerge_sessions** 시스템 테이블을 쿼리하여 [Session_id](../../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) 를 얻을 수도 있습니다.  
  
2.  배포 데이터베이스의 배포자에서 [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)을 실행합니다. **@session_id**에 1단계에서 얻은 **Session_id** 값을 지정합니다. 이렇게 하면 해당 세션에 대한 세부 모니터링 정보가 표시됩니다.  
  
3.  각 관심 세션에 대해 2단계를 반복합니다.  
  
#### <a name="to-monitor-merge-agent-sessions-for-pull-subscriptions-from-the-subscriber"></a>구독자에서 끌어오기 구독에 대한 병합 에이전트 세션을 모니터링하려면  
  
1.  구독 데이터베이스의 구독자에서 [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)을 실행합니다. 지정된 구독에 대해 **@publisher**, **@publication**을 지정하고 **@publisher_db**를 실행합니다. 이렇게 하면 이 구독의 마지막 다섯 개 병합 에이전트 세션에 대한 모니터링 정보가 반환됩니다. 결과 집합에 있는 관심 세션의 **Session_id** 값을 확인합니다.  
  
2.  구독 데이터베이스의 구독자에서 [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)을 실행합니다. **@session_id**에 1단계에서 얻은 **Session_id** 값을 지정합니다. 이렇게 하면 해당 세션에 대한 세부 모니터링 정보가 표시됩니다.  
  
3.  각 관심 세션에 대해 2단계를 반복합니다.  
  
#### <a name="to-view-and-modify-the-monitor-threshold-metrics-for-a-publication"></a>게시에 대한 모니터 임계값 메트릭을 보거나 수정하려면  
  
1.  배포 데이터베이스의 배포자에서 [sp_replmonitorhelppublicationthresholds](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)를 실행합니다. 이렇게 하면 이 배포자를 사용하는 모든 게시의 모니터링 임계값 집합이 반환됩니다. 결과 집합을 단일 게시자 또는 게시된 데이터베이스에 속하는 게시에 대한 모니터 임계값으로 제한하거나 단일 게시로 제한하려면 각각 **@publisher**, **@publisher_db**또는 **@publication**를 지정합니다. 변경해야 하는 임계값에 대한 **Metric_id** 값을 확인합니다. 자세한 내용은 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)를 참조하세요.  
  
2.  배포 데이터베이스의 배포자에서 [sp_replmonitorchangepublicationthreshold](../../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md)를 실행합니다. 다음을 필요한 대로 지정합니다.  
  
    -   **@metric_id**에 1단계에서 얻은 **Metric_id** 값을 지정합니다.  
  
    -   **@value**에 모니터 임계값 메트릭의 새 값을 지정합니다.  
  
    -   이 임계값에 도달할 때 경고를 기록하려면 **@shouldalert** 에 값 **@shouldalert** 을 지정하고, 경고가 필요하지 않은 경우 값 **0** 을 지정합니다.  
  
    -   이 임계값에 도달할 때 경고를 기록하려면 **@shouldalert** 에 값 **@mode** 을 지정하고 모니터 임계값 메트릭을 사용하지 않으려면 값 **2** 를 지정합니다.  
  
##  <a name="RMO"></a> RMO(복제 관리 개체)  
  
#### <a name="to-monitor-a-subscription-to-a-merge-publication-at-the-subscriber"></a>구독자에서 병합 게시에 대한 구독을 모니터링하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  Create an instance of the <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor> 클래스의 인스턴스를 만들고 구독에 대한 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> 속성을 설정하며 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>으로 설정합니다.  
  
3.  다음 메서드 중 하나를 호출하여 이 구독의 병합 에이전트 세션에 대한 정보가 반환되도록 합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> - 최대 마지막 다섯 개 병합 에이전트 세션에 대한 정보가 포함된 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 개체의 배열을 반환합니다. 관심 세션의 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 값을 확인합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> - *hours* 매개 변수로 전달한 시간 동안 발생한 병합 에이전트 세션(최대 마지막 다섯 개 세션)에 대한 정보가 포함된 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 개체의 배열을 반환합니다. 관심 세션의 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 값을 확인합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A> - 마지막 병합 에이전트 세션에 대한 정보가 포함된 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 개체를 반환합니다. 이 세션의 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 값을 확인합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A> - 최대 마지막 다섯 개 병합 에이전트 세션에 대한 정보가 각 행에 하나씩 포함된 <xref:System.Data.DataSet> 개체를 반환합니다. 관심 세션의 **Session_id** 열 값을 확인합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A> - 마지막 병합 에이전트 세션에 대한 정보가 포함된 <xref:System.Data.DataRow> 개체를 반환합니다. 이 세션의 **Session_id** 열 값을 확인합니다.  
  
4.  (옵션) <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A>를 호출하여 *mss*로 전달된 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 개체에 대한 데이터를 새로 고치거나 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A>를 호출하여 *drRefresh*로 전달된 <xref:System.Data.DataRow> 개체의 데이터를 새로 고칩니다.  
  
5.  3단계에서 가져온 세션 ID를 사용하여 다음 메서드 중 하나를 호출합니다. 그러면 특정 세션에 대한 세부 정보가 반환됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A> - 제공된 *SessionId*에 대한 <xref:Microsoft.SqlServer.Replication.MergeSessionDetail> 개체의 배열을 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A> - 지정된 *SessionId*에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
#### <a name="to-monitor-replication-properties-for-all-publications-at-a-distributor"></a>배포자에서 모든 게시에 대한 복제 속성을 모니터링하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>으로 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다.  
  
5.  다음 메서드 중 하나 이상을 실행하여 이 배포자를 사용하는 모든 게시자에 대한 복제 정보가 반환되도록 합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A> - 이 배포자의 모든 배포 에이전트에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A> - 배포자에 저장된 오류에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A> - 배포자의 모든 로그 판독기 에이전트에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A> - 배포자의 모든 병합 에이전트에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A> - 배포자의 다른 모든 복제 에이전트에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A> - 이 배포자의 모든 게시자에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A> - 이 배포자를 사용하는 게시자를 반환하는 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A> - 배포자의 모든 큐 판독기 에이전트에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A> - 지정된 큐 판독기 에이전트 및 세션에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A> - 지정된 큐 판독기 에이전트에 대한 세션 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A> - 배포자의 모든 스냅숏 에이전트에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
#### <a name="to-monitor-publication-properties-for-a-specific-publisher-at-the-distributor"></a>배포자에서 특정 게시자의 게시 속성을 모니터링하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
2.  다음 방법 중 하나로 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 개체를 가져옵니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 클래스의 인스턴스를 만듭니다. 게시자에 대해 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>으로 설정합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 게시자 이름이 올바르게 정의되지 않았거나 해당 게시가 없는 것입니다.  
  
    -   기존 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> 개체의 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A> 속성을 통해 액세스한 <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection>에서 가져옵니다.  
  
3.  다음 메서드 중 하나 이상을 실행하여 이 배포자에 속해 있는 모든 게시에 대한 복제 정보가 반환되도록 합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A> - 지정된 배포 에이전트 및 세션에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A> - 지정된 배포 에이전트에 대한 세션 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A> - 지정된 오류에 대한 오류 레코드 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A> - 지정된 로그 판독기 에이전트 및 세션에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A> - 지정된 로그 판독기 에이전트에 대한 세션 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A> - 지정된 병합 에이전트 및 세션에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A> - 지정된 병합 에이전트 및 세션에 대한 추가 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A> - 지정된 병합 에이전트에 대한 세션 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A> - 지정된 병합 에이전트에 대한 추가 세션 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A> - 이 배포자의 모든 게시에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A> - 이 배포자의 모든 게시에 대한 추가 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A> - 지정된 스냅숏 에이전트 및 세션에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A> - 지정된 스냅숏 에이전트에 대한 세션 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A> - 이 배포자의 게시에 대한 모든 구독 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
#### <a name="to-monitor-properties-for-a-specific-publication-at-the-distributor"></a>배포자에서 특정 게시의 속성을 모니터링하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
2.  다음 방법 중 하나로 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 개체를 가져옵니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> 및 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>으로 설정합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 게시 속성이 올바르게 정의되지 않았거나 해당 게시가 없는 것입니다.  
  
    -   기존 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 개체의 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 속성을 통해 액세스한 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection>에서 가져옵니다.  
  
3.  다음 메서드 중 하나 이상을 실행하여 이 게시에 대한 정보가 반환되도록 합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A> - 지정된 오류에 대한 오류 레코드가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A> - 이 게시의 로그 판독기 에이전트에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> - 이 게시의 모니터 경고 임계값 집합에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A> - 이 게시에서 사용하는 큐 판독기 에이전트에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A> - 이 게시의 스냅숏 에이전트에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A> - 이 게시에 대한 구독 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A> - 제공된 <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption>에 따라 이 게시에 대한 구독과 관련된 추가 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> - 지정된 추적 프로그램 토큰에 대한 대기 시간 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> - 이 게시에 삽입된 모든 추적 프로그램 토큰에 대한 정보가 포함된 <xref:System.Data.DataSet> 개체를 반환합니다.  
  
#### <a name="to-monitor-transactional-commands-that-are-waiting-to-be-applied-at-the-subscriber"></a>구독자에서 적용 대기 중인 트랜잭션 명령을 모니터링하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
2.  다음 방법 중 하나로 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 개체를 가져옵니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> 및 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>으로 설정합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 게시 속성이 올바르게 정의되지 않았거나 해당 게시가 없는 것입니다.  
  
    -   기존 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 개체의 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 속성을 통해 액세스한 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection>에서 가져옵니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A> 메서드를 실행하여 <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> 개체를 반환합니다.  
  
4.  이 <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> 개체의 속성을 사용하여 보류 중인 명령의 예상 개수와 해당 명령의 배달을 완료하는 데 소요될 시간을 확인합니다.  
  
#### <a name="to-set-the-monitor-warning-thresholds-for-a-publication"></a>게시의 모니터 경고 임계값을 설정하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
2.  다음 방법 중 하나로 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 개체를 가져옵니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> 및 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>으로 설정합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 게시 속성이 올바르게 정의되지 않았거나 해당 게시가 없는 것입니다.  
  
    -   기존 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 개체의 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 속성을 통해 액세스한 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection>에서 가져옵니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> 메서드를 실행합니다. <xref:Microsoft.SqlServer.Replication.MonitorThreshold> 개체의 반환된 <xref:System.Collections.ArrayList>에서 현재 임계값 설정을 확인합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A> 메서드를 실행합니다. 다음 매개 변수를 전달합니다.  
  
    -   *metricID* - 다음 표에서 모니터링 임계값 메트릭을 나타내는 <xref:System.Int32> 값입니다.  
  
        |Value|설명|  
        |-----------|-----------------|  
        |@shouldalert|**expiration** - 트랜잭션 게시에 대한 구독의 만료가 임박했는지 모니터링합니다.|  
        |2|**latency** - 트랜잭션 게시에 대한 구독의 성능을 모니터링합니다.|  
        |4|**mergeexpiration** - 병합 게시에 대한 구독의 만료가 임박했는지 모니터링합니다.|  
        |5|**mergeslowrunduration** - 저대역폭(전화 접속) 연결을 통한 병합 동기화의 기간을 모니터링합니다.|  
        |6|**mergefastrunduration** - 고대역폭(LAN) 연결을 통한 병합 동기화의 기간을 모니터링합니다.|  
        |7|**mergefastrunspeed** - 고대역폭(LAN) 연결을 통한 병합 동기화의 동기화 속도를 모니터링합니다.|  
        |8|**mergeslowrunspeed** - 저대역폭(전화 접속) 연결을 통한 병합 동기화의 동기화 속도를 모니터링합니다.|  
  
    -   *enable* - 게시에 메트릭을 사용할 수 있는지 여부를 나타내는 <xref:System.Boolean> 값입니다.  
  
    -   *thresholdValue* - 임계값을 설정하는 정수 값입니다.  
  
    -   *shouldAlert* - 이 임계값에서 경고를 생성할지 여부를 나타내는 정수입니다.  
  
  
