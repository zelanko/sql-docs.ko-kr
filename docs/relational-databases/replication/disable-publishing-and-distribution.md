---
title: "게시 및 배포 해제 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- disabling publishing
- publishing [SQL Server replication], disabling
- distribution disabling [SQL Server replication]
- removing replication
- replication [SQL Server], removing
- disabling replication
- disabling distribution
ms.assetid: 6d4a1474-4d13-4826-8be2-80050fafa8a5
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 80f107b2855a1e3f2ca4821354021e94c76269d7
ms.lasthandoff: 04/11/2017

---
# <a name="disable-publishing-and-distribution"></a>게시 및 배포 해제
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 게시 및 배포를 해제하는 방법에 대해 설명합니다.  
  
 사용할 수 있는 기능은 다음과 같습니다.  
  
-   배포자에서 모든 배포 데이터베이스를 삭제합니다.  
  
-   배포자를 사용하는 모든 게시자를 해제하고 이 게시자의 게시를 모두 삭제합니다.  
  
-   게시에 대한 구독을 모두 삭제합니다. 게시 및 구독 데이터베이스의 데이터는 삭제되지 않지만 게시 데이터베이스에 대한 동기화 관계는 손실됩니다. 구독자의 데이터는 수동으로만 삭제할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [필수 구성 요소](#Prerequisites)  
  
-   **다음을 사용하여 게시 및 배포를 해제하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
  
-   게시 및 배포를 해제하려면 모든 배포 및 게시 데이터베이스가 온라인 상태여야 합니다. 배포 또는 게시 데이터베이스에 대한 *데이터베이스 스냅숏* 이 있는 경우 이 스냅숏을 먼저 삭제한 다음 게시 및 배포를 해제해야 합니다. 데이터베이스 스냅숏은 데이터베이스의 읽기 전용 오프라인 사본이며 복제 스냅숏과 연관되어 있지 않습니다. 자세한 내용은 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 게시 및 배포 해제 마법사를 사용하여 게시 및 배포를 해제합니다.  
  
#### <a name="to-disable-publishing-and-distribution"></a>게시 및 배포를 해제하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 해제할 게시자나 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **게시 및 배포 해제**를 클릭합니다.  
  
3.  게시 및 배포 해제 마법사의 단계를 완료합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 게시 및 배포를 프로그래밍 방식으로 해제할 수 있습니다.  
  
#### <a name="to-disable-publishing-and-distribution"></a>게시 및 배포를 해제하려면  
  
1.  모든 복제 관련 작업을 중지합니다. 작업 이름 목록은 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)의 "SQL Server 에이전트의 에이전트 보안" 섹션을 참조하세요.  
  
2.  구독 데이터베이스의 각 구독자에서 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 을 실행하여 데이터베이스에서 복제 개체를 제거합니다. 이 저장 프로시저는 배포자의 복제 작업은 제거하지 않습니다.  
  
3.  게시 데이터베이스의 게시자에서 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 을 실행하여 데이터베이스에서 복제 개체를 제거합니다.  
  
4.  게시자가 원격 배포자를 사용하는 경우 [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)를 실행합니다.  
  
5.  배포자에서 [sp_dropdistpublisher](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)를 실행합니다. 이 저장 프로시저는 배포자에 등록된 각 게시자에 대해 한 번만 실행해야 합니다.  
  
6.  배포자에서 [sp_dropdistributiondb](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md) 를 실행하여 배포 데이터베이스를 삭제합니다. 이 저장 프로시저는 배포자의 각 배포 데이터베이스에 대해 한 번만 실행해야 합니다. 그러면 배포 데이터베이스와 연결된 모든 큐 판독기 에이전트 작업도 제거됩니다.  
  
7.  배포자에서 [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md) 를 실행하여 서버에서 배포자 지정을 제거합니다.  
  
    > [!NOTE]  
    >  모든 복제 게시 및 배포 개체가 삭제되지 않은 상태로 [sp_dropdistpublisher](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md) 및 [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)를 실행하면 오류가 반환됩니다. 게시자 또는 배포자를 삭제할 때 모든 복제 관련 개체를 삭제하려면 **@no_checks** 를 **1**을 참조하세요. 게시자 또는 배포자가 오프라인이거나 연결할 수 없는 경우에는 **@ignore_distributor** 매개 변수를 **1** 로 설정하여 삭제할 수 있습니다. 그러나 삭제되지 않고 남은 모든 게시 및 배포 개체는 수동으로 제거해야 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 스크립트 예에서는 구독 데이터베이스에서 복제 개체를 제거합니다.  
  
 [!code-sql[HowTo#sp_removedbreplication](../../relational-databases/replication/codesnippet/tsql/disable-publishing-and-d_1.sql)]  
  
 다음 스크립트 예에서는 게시자 및 배포자 역할의 서버에서 게시 및 배포를 해제하고 배포 데이터베이스를 삭제합니다.  
  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/disable-publishing-and-d_2.sql)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
  
#### <a name="to-disable-publishing-and-distribution"></a>게시 및 배포를 해제하려면  
  
1.  배포자를 사용하는 게시에 대한 모든 구독을 제거합니다. 자세한 내용은 [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md) 및 [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md)를 참조하세요.  
  
2.  배포자를 사용하는 모든 게시를 제거하고 게시자와 배포자가 동일한 서버에 있는 경우에는 모든 데이터베이스에 대한 게시를 해제합니다. 자세한 내용은 [Delete a Publication](../../relational-databases/replication/publish/delete-a-publication.md)을 참조하세요.  
  
3.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> 속성을 지정하고 3단계의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 전달합니다.  
  
5.  (옵션) <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 속성을 얻고 게시자가 있는지 확인합니다. 이 메서드가 **false**를 반환하면 4단계에서 지정한 게시자 이름이 올바르지 않거나 이 배포자에서 게시자를 사용하지 않는 것입니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Remove%2A> 메서드를 호출합니다. 게시자와 배포자가 다른 서버에 있으며 게시자에 게시가 더 이상 존재하지 않는지 먼저 확인하지 않고 배포자에서 게시자를 제거해야 하는 경우 **force** 에 *true* 값을 전달합니다.  
  
7.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스의 인스턴스를 만듭니다. 3단계의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 전달합니다.  
  
8.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.UninstallDistributor%2A> 메서드를 호출합니다. 모든 로컬 게시 데이터베이스가 해제되었는지, 그리고 배포 데이터베이스가 제거되었는지 확인하지 않고 배포자의 모든 복제 개체를 제거하려면 **force** 에 *true* 값을 전달합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 다음 예에서는 배포자에서 게시 등록을 제거하고 배포 데이터베이스 삭제하며 배포자를 제거합니다.  
  
 [!code-cs[HowTo#rmo_DropDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropdistpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropdistpub)]  
  
 다음 예에서는 먼저 로컬 게시 데이터베이스를 해제하거나 배포 데이터베이스를 삭제하지 않고 배포자를 제거합니다.  
  
 [!code-cs[HowTo#rmo_DropDistPubForce](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropdistpubforce)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPubForce](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropdistpubforce)]  
  
## <a name="see-also"></a>참고 항목  
 [복제 관리 개체 개념](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [복제 시스템 저장 프로시저 개념](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
