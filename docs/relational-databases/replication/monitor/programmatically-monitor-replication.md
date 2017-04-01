---
title: "프로그래밍 방식으로 복제 모니터링 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_replmonitorhelppublisher"
  - "sp_replmonitorhelpmergesessiondetail"
  - "성능 모니터링 [SQL Server 복제], 게시 상태"
  - "sp_replmonitorhelpmergesession"
  - "sp_replmonitorhelppublicationthresholds"
  - "성능 모니터링 [SQL Server 복제], 구독 상태"
  - "성능 모니터링 [SQL Server 복제], Transact-SQL 프로그래밍"
  - "sp_replmonitorsubscriptionpendingcmds"
  - "sp_replmonitorchangepublicationthreshold"
  - "트랜잭션 복제, 모니터링"
  - "sp_replmonitorhelppublication"
  - "sp_replmonitorhelpsubscription"
  - "성능 모니터링 [SQL Server 복제], 임계값 및 경고"
  - "병합 복제 모니터링 [SQL Server 복제]"
  - "스냅숏 복제 [SQL Server], 모니터링"
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 프로그래밍 방식으로 복제 모니터링
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
  
#### 배포자에서 게시자, 게시 및 구독을 모니터링하려면  
  
1.  배포 데이터베이스의 배포자에서 실행 [sp_replmonitorhelppublisher](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)합니다. 이렇게 하면 이 배포자를 사용하는 모든 게시자에 대한 모니터링 정보가 반환됩니다. 결과 집합을 단일 게시자로 제한하려면 **@publisher**를 지정합니다.  
  
2.  배포 데이터베이스의 배포자에서 실행 [sp_replmonitorhelppublication](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)합니다. 이렇게 하면 이 배포자를 사용하는 모든 게시에 대한 모니터링 정보가 반환됩니다. 결과 집합을 단일 게시자, 게시 또는 게시 된 데이터베이스를 제한 하려면 지정 **@publisher**, **@publication**, 또는 **@publisher_db**, 각각.  
  
3.  배포 데이터베이스의 배포자에서 실행 [sp_replmonitorhelpsubscription](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)합니다. 이렇게 하면 이 배포자를 사용하는 모든 구독에 대한 모니터링 정보가 반환됩니다. 결과 집합을 단일 게시자에 속하는 구독을 최소화 하려면 게시 또는 게시 된 데이터베이스 지정 **@publisher**, **@publication**, 또는 **@publisher_db**, 각각.  
  
#### 구독자에서 적용 대기 중인 트랜잭션 명령을 모니터링하려면  
  
1.  배포 데이터베이스의 배포자에서 실행 [sp_replmonitorsubscriptionpendingcmds](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md)합니다. 이렇게 하면 이 배포자를 사용하는 모든 구독에 대해 보류 중인 모든 명령의 모니터링 정보가 반환됩니다. 결과 집합을 단일 게시자에 속하는 구독에 대 한 보류 중인 명령을 제한 하려면 구독자, 게시 또는 게시 된 데이터베이스 지정 **@publisher**, **@subscriber**, **@publication**, 또는 **@publisher_db**, 각각.  
  
#### 업로드 또는 다운로드 대기 중인 병합 변경 내용을 모니터링하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)합니다. 이렇게 하면 구독자에 대해 복제 대기 중인 변경 내용에 대한 정보를 보여 주는 결과 집합이 반환됩니다. 결과 집합을 단일 게시 또는 아티클에 속하는 변경 내용으로 제한하려면 각각 **@publication** 또는 **@article**을 지정합니다.  
  
2.  구독 데이터베이스의 구독자에서 실행 [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)합니다. 이렇게 하면 게시자에 대해 복제 대기 중인 변경 내용에 대한 정보를 보여 주는 결과 집합이 반환됩니다. 결과 집합을 단일 게시 또는 아티클에 속하는 변경 내용으로 제한하려면 각각 **@publication** 또는 **@article**을 지정합니다.  
  
#### 병합 에이전트 세션을 모니터링하려면  
  
1.  배포 데이터베이스의 배포자에서 실행 [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)합니다. 모니터링 정보를 반환 합니다. 포함 하 여 **Session_id**, 이 배포자를 사용 하 여 모든 구독에 대 한 모든 병합 에이전트 세션에 있습니다. 가져올 수도 있습니다 **Session_id** 쿼리하여는 [MSmerge_sessions](../../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) 시스템 테이블입니다.  
  
2.  배포 데이터베이스의 배포자에서 실행 [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)합니다. 지정 된 **Session_id** 값에 1 단계에서 **@session_id**합니다. 이렇게 하면 해당 세션에 대한 세부 모니터링 정보가 표시됩니다.  
  
3.  각 관심 세션에 대해 2단계를 반복합니다.  
  
#### 구독자에서 끌어오기 구독에 대한 병합 에이전트 세션을 모니터링하려면  
  
1.  구독 데이터베이스의 구독자에서 실행 [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)합니다. 지정된 된 구독에 대해 지정 **@publisher**, **@publication**, 및에 대 한 게시 데이터베이스의 이름을 **@publisher_db**합니다. 이렇게 하면 이 구독의 마지막 다섯 개 병합 에이전트 세션에 대한 모니터링 정보가 반환됩니다. 값을 확인 **Session_id** 결과에 관심이의 세션을 설정 합니다.  
  
2.  구독 데이터베이스의 구독자에서 실행 [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)합니다. 지정 된 **Session_id** 값에 1 단계에서 **@session_id**합니다. 이렇게 하면 해당 세션에 대한 세부 모니터링 정보가 표시됩니다.  
  
3.  각 관심 세션에 대해 2단계를 반복합니다.  
  
#### 게시에 대한 모니터 임계값 메트릭을 보거나 수정하려면  
  
1.  배포 데이터베이스의 배포자에서 실행 [sp_replmonitorhelppublicationthresholds](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)합니다. 이렇게 하면 이 배포자를 사용하는 모든 게시의 모니터링 임계값 집합이 반환됩니다. 결과 집합을 단일 게시 또는 단일 게시자 또는 게시 된 데이터베이스에 속한 게시에 대 한 임계값 모니터를 제한 하려면 지정 **@publisher**, **@publisher_db**, 또는 **@publication**, 각각. 값을 확인 **Metric_id** 변경 해야 하는 모든 임계값에 대 한 합니다. 자세한 내용은 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)를 참조하세요.  
  
2.  배포 데이터베이스의 배포자에서 실행 [sp_replmonitorchangepublicationthreshold](../../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md)합니다. 다음을 필요한 대로 지정합니다.  
  
    -    **Metric_id** 에 1 단계에서 얻은 값 **@metric_id**합니다.  
  
    -   **@value**에 모니터 임계값 메트릭의 새 값을 지정합니다.  
  
    -   이 임계값에 도달할 때 경고를 기록하려면 **@shouldalert** 에 값 **1** 을 지정하고, 경고가 필요하지 않은 경우 값 **0** 을 지정합니다.  
  
    -   모니터 임계값 메트릭을 사용하려면 **@mode** 에 값 **1** 을 지정하고 모니터 임계값 메트릭을 사용하지 않으려면 값 **2** 를 지정합니다.  
  
##  <a name="RMO"></a> RMO(복제 관리 개체)  
  
#### 구독자에서 병합 게시에 대한 구독을 모니터링하려면  
  
1.  사용 하 여 구독자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor> 클래스를 설정는 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> 구독 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 만든.  
  
3.  다음 메서드 중 하나를 호출하여 이 구독의 병합 에이전트 세션에 대한 정보가 반환되도록 합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -의 배열을 반환 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 최대 마지막 다섯 개 병합 에이전트 세션에 있는 정보 개체입니다. 참고는 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 관심 세션의 값입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -의 배열을 반환 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 지난 수 시간으로 전달 하는 동안 발생 한 병합 에이전트 세션에 대 한 정보를 사용 하 여 개체는 *시간* (최대 마지막 다섯 개 세션) 매개 변수입니다. 참고는 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 관심 세션의 값입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A> -반환 된 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 마지막 병합 에이전트 세션에 대 한 정보가 포함 된 개체입니다. 참고는 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 이 세션에 대 한 값입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A> -반환 된 <xref:System.Data.DataSet> 에 각 행에 하나씩 마지막 다섯 개 병합 에이전트 세션의 최대 정보로 개체입니다. 값을 확인는 **Session_id** 관심 세션의에 대 한 열입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A> -반환 된 <xref:System.Data.DataRow> 마지막 병합 에이전트 세션에 대 한 정보가 포함 된 개체입니다. 값을 확인는 **Session_id** 이 세션에 대 한 열입니다.  
  
4.  (선택 사항) 호출 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> 에 대 한 데이터를 새로 고치는 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 변수로 전달 된 개체 *mss* 호출 또는 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> 에 데이터를 새로 고치는 <xref:System.Data.DataRow> 변수로 전달 된 개체 *drRefresh*.  
  
5.  3단계에서 가져온 세션 ID를 사용하여 다음 메서드 중 하나를 호출합니다. 그러면 특정 세션에 대한 세부 정보가 반환됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A> -의 배열을 반환 <xref:Microsoft.SqlServer.Replication.MergeSessionDetail> 에서 제공 된 *SessionId*합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A> -반환 된 <xref:System.Data.DataSet> 지정 된 항목에 대 한 정보가 포함 된 개체 *SessionId*합니다.  
  
#### 배포자에서 모든 게시에 대한 복제 속성을 모니터링하려면  
  
1.  사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 만든 합니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다.  
  
5.  다음 메서드 중 하나 이상을 실행하여 이 배포자를 사용하는 모든 게시자에 대한 복제 정보가 반환되도록 합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A> -반환 된 <xref:System.Data.DataSet> 이 배포자의 모든 배포 에이전트에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A> -반환 된 <xref:System.Data.DataSet> 배포자에 저장 된 오류에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A> -반환 된 <xref:System.Data.DataSet> 배포자에서 모든 로그 판독기 에이전트에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A> -반환 된 <xref:System.Data.DataSet> 배포자에서 모든 병합 에이전트에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A> -반환 된 <xref:System.Data.DataSet> 배포자에서 모든 복제 에이전트에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A> -반환 된 <xref:System.Data.DataSet> 이 배포자의 모든 게시자에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A> -반환 된 <xref:System.Data.DataSet> 이 배포자를 사용 하는 게시자를 반환 하는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A> -반환 된 <xref:System.Data.DataSet> 배포자에서 모든 큐 판독기 에이전트에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A> -반환 된 <xref:System.Data.DataSet> 지정 된 큐 판독기 에이전트 및 세션에 대 한 세부 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A> -반환 된 <xref:System.Data.DataSet> 지정된 된 큐 판독기 에이전트에 대 한 세션 정보가 들어 있는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A> -반환 된 <xref:System.Data.DataSet> 배포자에서 모든 스냅숏 에이전트에 대 한 정보가 포함 된 개체입니다.  
  
#### 배포자에서 특정 게시자의 게시 속성을 모니터링하려면  
  
1.  사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  가져오기는 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 다음이 방법 중 하나에 개체입니다.  
  
    -   인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A> 게시자 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 만든 합니다. 호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 게시자 이름이 올바르게 정의되지 않았거나 해당 게시가 없는 것입니다.  
  
    -    <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection> 통해 액세스는 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A> 기존 속성 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> 개체입니다.  
  
3.  다음 메서드 중 하나 이상을 실행하여 이 배포자에 속해 있는 모든 게시에 대한 복제 정보가 반환되도록 합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A> -반환 된 <xref:System.Data.DataSet> 지정 된 배포 에이전트 및 세션에 대 한 세부 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A> -반환 된 <xref:System.Data.DataSet> 지정된 된 배포 에이전트에 대 한 세션 정보가 들어 있는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A> -반환 된 <xref:System.Data.DataSet> 지정된 된 오류에 대 한 오류 레코드 정보가 들어 있는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A> -반환 된 <xref:System.Data.DataSet> 지정 된 로그 판독기 에이전트 및 세션에 대 한 세부 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A> -반환 된 <xref:System.Data.DataSet> 지정된 된 로그 판독기 에이전트에 대 한 세션 정보가 들어 있는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A> -반환 된 <xref:System.Data.DataSet> 지정 된 병합 에이전트 및 세션에 대 한 세부 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A> -반환 된 <xref:System.Data.DataSet> 지정 된 병합 에이전트 및 세션에 대 한 추가 정보가 들어 있는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A> -반환 된 <xref:System.Data.DataSet> 지정된 된 병합 에이전트에 대 한 세션 정보가 들어 있는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A> -반환 된 <xref:System.Data.DataSet> 지정된 된 병합 에이전트에 대 한 추가 세션 정보가 들어 있는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A> -반환 된 <xref:System.Data.DataSet> 이 배포자의 모든 게시에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A> -반환 된 <xref:System.Data.DataSet> 이 배포자의 모든 게시에 대 한 추가 정보를 포함 하는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A> -반환 된 <xref:System.Data.DataSet> 지정 된 스냅숏 에이전트 및 세션에 대 한 세부 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A> -반환 된 <xref:System.Data.DataSet> 지정된 된 스냅숏 에이전트에 대 한 세션 정보가 들어 있는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A> -반환 된 <xref:System.Data.DataSet> 이 배포자의 게시에 대 한 모든 구독에 대 한 정보가 포함 된 개체입니다.  
  
#### 배포자에서 특정 게시의 속성을 모니터링하려면  
  
1.  사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  가져오기는 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 다음이 방법 중 하나에 개체입니다.  
  
    -   인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, 및 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 게시 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 만든 합니다. 호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 게시 속성이 올바르게 정의되지 않았거나 해당 게시가 없는 것입니다.  
  
    -    <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> 액세스 방법으로 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 기존 속성 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 개체입니다.  
  
3.  다음 메서드 중 하나 이상을 실행하여 이 게시에 대한 정보가 반환되도록 합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A> -반환 된 <xref:System.Data.DataSet> 지정된 된 오류에 대 한 오류 레코드가 들어 있는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A> -반환 된 <xref:System.Data.DataSet> 이 게시에 대 한 로그 판독기 에이전트에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> -반환는 <xref:System.Data.DataSet> 이 게시에 대 한 모니터 경고 임계값에 대 한 정보가 포함 된 개체를 설정 합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A> -반환 된 <xref:System.Data.DataSet> 이 게시에서 사용 하는 큐 판독기 에이전트에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A> -반환 된 <xref:System.Data.DataSet> 이 게시에 대 한 스냅숏 에이전트에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A> -반환 된 <xref:System.Data.DataSet> 이 게시에 대 한 구독에 대 한 정보가 포함 된 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A> -반환 된 <xref:System.Data.DataSet> 제공 된에 따라이 게시에 대 한 구독에 대 한 추가 정보를 포함 하는 개체 <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption>합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> -반환 된 <xref:System.Data.DataSet> 지정 된 추적 프로그램 토큰에 대 한 대기 시간 정보를 포함 하는 개체입니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> -반환 된 <xref:System.Data.DataSet> 이 게시에 삽입 된 모든 추적 프로그램 토큰에 대 한 정보가 포함 된 개체입니다.  
  
#### 구독자에서 적용 대기 중인 트랜잭션 명령을 모니터링하려면  
  
1.  사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  가져오기는 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 다음이 방법 중 하나에 개체입니다.  
  
    -   인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, 및 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 게시 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 만든 합니다. 호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 게시 속성이 올바르게 정의되지 않았거나 해당 게시가 없는 것입니다.  
  
    -    <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> 액세스 방법으로 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 기존 속성 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 개체입니다.  
  
3.  실행 된 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A> 반환 하는 <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> 개체입니다.  
  
4.  이 속성을 사용 하 여 <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> 보류 중인 명령의 예상된 수 및 해당 명령의 배달을 완료 하는 데 걸리는 시간의 길이 결정 하는 개체입니다.  
  
#### 게시의 모니터 경고 임계값을 설정하려면  
  
1.  사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  가져오기는 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 다음이 방법 중 하나에 개체입니다.  
  
    -   인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, 및 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 게시 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 만든 합니다. 호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 게시 속성이 올바르게 정의되지 않았거나 해당 게시가 없는 것입니다.  
  
    -    <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> 액세스 방법으로 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 기존 속성 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 개체입니다.  
  
3.  실행 된 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> 메서드. 반환 된 현재 임계값 설정을 <xref:System.Collections.ArrayList> 의 <xref:Microsoft.SqlServer.Replication.MonitorThreshold> 개체입니다.  
  
4.  실행 된 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A> 메서드. 다음 매개 변수를 전달합니다.  
  
    -   *metricID* - <xref:System.Int32> 다음 테이블에서 모니터링 임계값 메트릭을 나타내는 값입니다.  
  
        |값|설명|  
        |-----------|-----------------|  
        |1|**만료** -트랜잭션 게시에 대 한 구독의 만료가 임박 했는지 모니터링 합니다.|  
        |2|**대기 시간** -트랜잭션 게시에 대 한 구독 성능에 대 한 모니터.|  
        |4|**mergeexpiration** -병합 게시에 대 한 구독의 만료가 임박 했는지 모니터링 합니다.|  
        |5|**mergeslowrunduration** -저대역폭 (전화 접속) 연결을 통한 병합 동기화의 기간을 모니터링 합니다.|  
        |6|**mergefastrunduration** -고대역폭 (LAN) 연결을 통한 병합 동기화의 기간을 모니터링 합니다.|  
        |7|**mergefastrunspeed** -고대역폭 (LAN) 연결을 통한 병합 동기화의 동기화 속도 모니터링 합니다.|  
        |8|**mergeslowrunspeed** -저대역폭 (전화 접속) 연결을 통한 병합 동기화의 동기화 속도 모니터링 합니다.|  
  
    -   *사용 하도록 설정* - <xref:System.Boolean> 게시에 대해 메트릭이 사용 되는지 여부를 나타내는 값입니다.  
  
    -   *thresholdValue* -임계값을 설정 하는 정수 값입니다.  
  
    -   *shouldAlert* -이 임계값에서 경고를 생성할지 여부를 나타내는 정수입니다.  
  
  