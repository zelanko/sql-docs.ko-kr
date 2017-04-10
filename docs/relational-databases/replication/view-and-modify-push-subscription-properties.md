---
title: "밀어넣기 구독 속성 보기 및 수정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "복제 속성 보기"
  - "밀어넣기 구독 [SQL Server 복제], 속성"
  - "구독 [SQL Server 복제], 밀어넣기"
  - "밀어넣기 구독 [SQL Server 복제], 수정"
  - "복제 속성 수정, 밀어넣기 구독"
  - "구독 수정, SQL Server Management Studio"
ms.assetid: 801d2995-7aa5-4626-906e-c8190758ec71
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 밀어넣기 구독 속성 보기 및 수정
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 밀어넣기 구독 속성을 보고 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 밀어넣기 구독 속성을 보고 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 다음 위치에서 게시자의 밀어넣기 구독 속성을 보고 수정합니다.  
  
-    **구독 속성-\< 게시자>: \< PublicationDatabase>** 대화 상자에서 사용할 수 있는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
  
-   **모든 구독** 탭 - 복제 모니터에서 사용 가능합니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다.  
  
#### Management Studio에서 밀어넣기 구독 속성을 보고 수정하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  적절 한 게시를 확장 하 고, 구독을 마우스 오른쪽 단추로 클릭 한 다음 클릭 한 다음 **속성**합니다.  
  
4.  필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
#### 복제 모니터에서 밀어넣기 구독 속성을 보고 수정하려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭합니다.  
  
3.  구독을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
4.  필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 밀어넣기 구독은 수정할 수 있으며 해당 속성은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 액세스할 수 있습니다. 사용되는 저장 프로시저는 구독이 속한 게시 유형에 따라 달라집니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 대한 밀어넣기 구독의 속성을 보려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)합니다. 이때 **@publication**및 **@subscriber**를 지정하고 **@article** 에 값 **all**을 지정합니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), 로 지정 하 여 **@subscriber**합니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 대한 밀어넣기 구독의 속성을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_changesubscriber](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md), 로 지정 하 여 **@subscriber** 변경할 구독자 속성에 대 한 모든 매개 변수입니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)합니다. 지정 **@publication**, **@subscriber**, **@destination_db**, 값이 **모든** 에 대 한 **@article**, 으로 변경 되는 구독 속성 **@property**, 및 새 값으로 **@value**합니다. 이렇게 하면 밀어넣기 구독의 보안 설정이 변경됩니다.  
  
3.  (선택 사항) 구독에 대 한 데이터 변환 서비스 (DTS) 패키지 속성을 변경 하려면 실행 [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md) 구독 데이터베이스의 구독자에서. **@jobid** 에 배포 에이전트 작업의 ID를 지정하고 다음과 같은 DTS 패키지 속성을 지정합니다.  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     이렇게 하면 구독의 DTS 패키지 속성이 변경됩니다.  
  
    > [!NOTE]  
    >  작업을 실행 하 여 ID를 가져올 수 있습니다 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)합니다.  
  
#### 병합 게시에 대한 밀어넣기 구독의 속성을 보려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)합니다. **@publication** 및 **@subscriber**를 지정합니다.  
  
2.  게시자에서 실행 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), 로 지정 하 여 **@subscriber**합니다.  
  
#### 병합 게시에 대한 밀어넣기 구독의 속성을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)합니다. 지정 **@publication**, **@subscriber**, **@subscriber_db**, 으로 변경 되는 구독 속성 **@property**, 및 새 값으로 **@value**합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 밀어넣기 구독 속성을 보거나 수정하는 데 사용되는 RMO 클래스는 밀어넣기 구독이 구독하는 게시의 유형에 따라 다릅니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 대한 밀어넣기 구독의 속성을 보거나 수정하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransSubscription> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, 및 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 속성입니다.  
  
4.  설정의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1 단계에서 만든는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 설정 합니다.  
  
5.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
6.  (선택 사항) 속성을 변경 하려면 중 하나에 대 한 새 값을 설정 된 <xref:Microsoft.SqlServer.Replication.TransSubscription> 속성을 설정할 수 있으며 다음이 호출 하는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드.  
  
7.  (선택 사항) 새 설정을 보려면 호출는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 메서드를 구독에 대 한 속성을 다시 로드 합니다.  
  
#### 병합 게시에 대한 밀어넣기 구독의 속성을 보거나 수정하려면  
  
1.  사용 하 여 구독자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, 및 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 속성입니다.  
  
4.  설정의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1 단계에서 만든는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 설정 합니다.  
  
5.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
6.  (선택 사항) 속성을 변경 하려면 중 하나에 대 한 새 값을 설정 된 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 속성을 설정할 수 있으며 다음이 호출 하는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드.  
  
7.  (선택 사항) 새 설정을 보려면 호출는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 메서드를 구독에 대 한 속성을 다시 로드 합니다.  
  
## 참고 항목  
 [정보 보기 및 구독 & #40;에 대 한 작업을 수행 합니다. 복제 모니터 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  