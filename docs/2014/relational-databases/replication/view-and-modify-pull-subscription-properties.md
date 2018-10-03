---
title: 끌어오기 구독 속성 보기 및 수정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- modifying subscriptions
- viewing replication properties
- modifying replication properties, pull subscriptions
- pull subscriptions [SQL Server replication], modifying
- subscriptions [SQL Server replication], pull
- pull subscriptions [SQL Server replication], properties
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab2dd19449e83468063e3e191c816cf1cfe4c755
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112953"
---
# <a name="view-and-modify-pull-subscription-properties"></a>끌어오기 구독 속성 보기 및 수정
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 끌어오기 구독 속성을 보고 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **끌어오기 구독 속성을 보고 수정하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **구독 속성 - \<Publisher>: \<PublicationDatabase>** 대화 상자의 게시자 또는 구독자에서 끌어오기 구독 속성을 볼 수 있으며, 이 대화 상자는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 제공됩니다. 구독자에서 더 많은 속성을 볼 수 있으며 구독자에서 속성을 수정할 수 있습니다. 복제 모니터에서 사용 가능한 **모든 구독** 탭의 게시자에서 속성을 볼 수도 있습니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](monitor/start-the-replication-monitor.md)을 참조하세요.  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-management-studio"></a>Management Studio의 게시자에서 끌어오기 구독 속성을 보려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  해당 게시를 확장하고 구독을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  속성을 점검한 다음 **확인**을 클릭합니다.  
  
#### <a name="to-view-and-modify-pull-subscription-properties-from-the-subscriber-in-management-studio"></a>Management Studio의 구독자에서 끌어오기 구독 속성을 보고 수정하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-replication-monitor"></a>복제 모니터의 게시자에서 끌어오기 구독 속성을 보려면  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭합니다.  
  
3.  해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  속성을 점검한 다음 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 끌어오기 구독은 수정할 수 있으며 속성은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 액세스할 수 있습니다. 사용되는 저장 프로시저는 구독이 속한 게시 유형에 따라 달라집니다.  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 대한 끌어오기 구독의 속성을 보려면  
  
1.  구독자에서 [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql)을 실행합니다. **@publisher**, **@publisher_db**및 **@publication**를 지정합니다. 이렇게 하면 구독자의 시스템 테이블에 저장된 구독에 대한 정보가 반환됩니다.  
  
2.  게시자에서 [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)를 실행합니다. **@publisher**, **@publisher_db**, **@publication**를 지정하고 **@publication_type**에 다음 값 중 하나를 지정합니다.  
  
    -   **0** - 구독이 트랜잭션 게시에 속합니다.  
  
    -   **1** - 구독이 스냅숏 게시에 속합니다.  
  
3.  게시자에서 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)을 실행합니다. 이때 **@publication** 및 **@subscriber**에서 사용 가능합니다.  
  
4.  게시자에서 [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)를 실행하고 **@subscriber**에서 제공됩니다. 이렇게 하면 구독자에 대한 정보가 표시됩니다.  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 대한 끌어오기 구독의 속성을 변경하려면  
  
1.  구독자에서 [@publisher](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql)를 실행하고 **@publisher**또는 RMO(복제 관리 개체)를 사용하여 **@publisher_db**또는 RMO(복제 관리 개체)를 사용하여 **@publication**에 **0** (트랜잭션) 또는 **1** (스냅숏) 값을 지정하고 변경되는 구독 속성을 **@publication_type**로, 새 값을 **@property**로 지정하고 **@value**에서 제공됩니다.  
  
2.  (옵션) 구독 데이터베이스의 구독자에서 [sp_changesubscriptiondtsinfo](/sql/relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql)를 실행합니다. **@jobid**에 배포 에이전트의 ID와 다음의 DTS(데이터 변환 서비스) 패키지 속성을 지정합니다.  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     이렇게 하면 구독의 DTS 패키지 속성이 변경됩니다.  
  
    > [!NOTE]  
    >  작업 ID는 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)을 실행하여 얻을 수 있습니다.  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 대한 끌어오기 구독의 속성을 보려면  
  
1.  구독자에서 [sp_helpmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql)을 실행합니다. **@publisher**, **@publisher_db** 및 **@publication**를 지정합니다.  
  
2.  게시자에서 [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)를 실행합니다. **@publisher**, **@publisher_db**, **@publication**을 지정하고 **@publication_type**에 대해 값 2를 지정합니다.  
  
3.  게시자에서 [sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql) 을 실행하여 구독 정보를 표시합니다. 특정 구독에 대한 정보를 반환하려면 **@publication**또는 RMO(복제 관리 개체)를 사용하여 **@subscriber**를 지정하고 **@subscription_type** 에 **@subscription_type**에서 제공됩니다.  
  
4.  게시자에서 [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)를 실행하고 **@subscriber**에서 제공됩니다. 이렇게 하면 구독자에 대한 정보가 표시됩니다.  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 대한 끌어오기 구독의 속성을 변경하려면  
  
1.  구독자에서 [sp_changemergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql)을 실행합니다. 이때 **@publication**, **@publisher**, **@publisher_db**, **@property**로 변경할 구독 속성, **@value**로 새 값을 지정합니다.  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 끌어오기 구독 속성을 보거나 수정하는 데 사용되는 RMO 클래스는 끌어오기 구독을 구독하는 게시 유형에 따라 다릅니다.  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 대한 끌어오기 구독의 속성을 보거나 수정하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>및 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 속성을 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성에 대해 1단계에서 만든 연결을 설정합니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 반환 하는 경우 `false`, 3 단계에서 구독 속성이 올바르게 정의 되지 또는 서버에는 구독이 존재 하지 않습니다.  
  
6.  (옵션) 속성을 변경하려면 설정할 수 있는 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 속성 중 하나에 대해 새 값을 설정한 다음 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 호출합니다.  
  
7.  (옵션) 새 설정을 보려면 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 메서드를 호출하여 아티클 속성을 다시 로드합니다.  
  
8.  모든 연결을 닫습니다.  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 대한 끌어오기 구독의 속성을 보거나 수정하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>및 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 속성을 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성에 대해 1단계에서 만든 연결을 설정합니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 반환 하는 경우 `false`, 3 단계에서 구독 속성이 올바르게 정의 되지 또는 서버에는 구독이 존재 하지 않습니다.  
  
6.  (옵션) 속성을 변경하려면 설정할 수 있는 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 속성 중 하나에 대해 새 값을 설정한 다음 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 호출합니다.  
  
7.  (옵션) 새 설정을 보려면 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 메서드를 호출하여 아티클 속성을 다시 로드합니다.  
  
8.  모든 연결을 닫습니다.  
  
## <a name="see-also"></a>관련 항목  
 [구독에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [복제 보안을 위한 최선의 구현 방법](security/replication-security-best-practices.md)   
 [게시 구독](subscribe-to-publications.md)  
  
  
