---
title: 게시 및 배포 해제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- disabling publishing
- publishing [SQL Server replication], disabling
- distribution disabling [SQL Server replication]
- removing replication
- replication [SQL Server], removing
- disabling replication
- disabling distribution
ms.assetid: 6d4a1474-4d13-4826-8be2-80050fafa8a5
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0ec2381b96818d038c7e40b71a4e56b1c4d415af
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37313493"
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
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   게시 및 배포를 해제하려면 모든 배포 및 게시 데이터베이스가 온라인 상태여야 합니다. 배포 또는 게시 데이터베이스에 대한 *데이터베이스 스냅숏* 이 있는 경우 이 스냅숏을 먼저 삭제한 다음 게시 및 배포를 해제해야 합니다. 데이터베이스 스냅숏은 데이터베이스의 읽기 전용 오프라인 사본이며 복제 스냅숏과 연관되어 있지 않습니다. 자세한 내용은 [데이터베이스 스냅숏&#40;SQL Server&#41;](../databases/database-snapshots-sql-server.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 게시 및 배포 해제 마법사를 사용하여 게시 및 배포를 해제합니다.  
  
#### <a name="to-disable-publishing-and-distribution"></a>게시 및 배포를 해제하려면  
  
1.   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 해제할 게시자나 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **게시 및 배포 해제**를 클릭합니다.  
  
3.  게시 및 배포 해제 마법사의 단계를 완료합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 게시 및 배포를 프로그래밍 방식으로 해제할 수 있습니다.  
  
#### <a name="to-disable-publishing-and-distribution"></a>게시 및 배포를 해제하려면  
  
1.  모든 복제 관련 작업을 중지합니다. 작업 이름 목록은 [복제 에이전트 보안 모델](security/replication-agent-security-model.md)의 "SQL Server 에이전트의 에이전트 보안" 섹션을 참조하세요.  
  
2.  구독 데이터베이스의 각 구독자에서 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 을 실행하여 데이터베이스에서 복제 개체를 제거합니다. 이 저장 프로시저는 배포자의 복제 작업은 제거하지 않습니다.  
  
3.  게시 데이터베이스의 게시자에서 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 을 실행하여 데이터베이스에서 복제 개체를 제거합니다.  
  
4.  게시자가 원격 배포자를 사용하는 경우 [sp_dropdistributor](/sql/relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql)를 실행합니다.  
  
5.  배포자에서 [sp_dropdistpublisher](/sql/relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql)를 실행합니다. 이 저장 프로시저는 배포자에 등록된 각 게시자에 대해 한 번만 실행해야 합니다.  
  
6.  배포자에서 [sp_dropdistributiondb](/sql/relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql) 를 실행하여 배포 데이터베이스를 삭제합니다. 이 저장 프로시저는 배포자의 각 배포 데이터베이스에 대해 한 번만 실행해야 합니다. 그러면 배포 데이터베이스와 연결된 모든 큐 판독기 에이전트 작업도 제거됩니다.  
  
7.  배포자에서 [sp_dropdistributor](/sql/relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql) 를 실행하여 서버에서 배포자 지정을 제거합니다.  
  
    > [!NOTE]  
    >  모든 복제 게시 및 배포 개체가 삭제되지 않은 상태로 [sp_dropdistpublisher](/sql/relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql) 및 [sp_dropdistributor](/sql/relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql)를 실행하면 오류가 반환됩니다. 게시자 또는 배포자를 삭제할 때 모든 복제 관련 개체를 삭제하려면 **@no_checks** 를 **1**을 참조하세요. 게시자 또는 배포자가 오프라인이거나 연결할 수 없는 경우에는 **@ignore_distributor** 매개 변수를 **1** 로 설정하여 삭제할 수 있습니다. 그러나 삭제되지 않고 남은 모든 게시 및 배포 개체는 수동으로 제거해야 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 스크립트 예에서는 구독 데이터베이스에서 복제 개체를 제거합니다.  
  
 [!code-sql[HowTo#sp_removedbreplication](../../snippets/tsql/SQL15/replication/howto/tsql/dropdistpub.sql#sp_removedbreplication)]  
  
 다음 스크립트 예에서는 게시자 및 배포자 역할의 서버에서 게시 및 배포를 해제하고 배포 데이터베이스를 삭제합니다.  
  
 [!code-sql[HowTo#sp_DropDistPub](../../snippets/tsql/SQL15/replication/howto/tsql/dropdistpub.sql#sp_dropdistpub)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
  
#### <a name="to-disable-publishing-and-distribution"></a>게시 및 배포를 해제하려면  
  
1.  배포자를 사용하는 게시에 대한 모든 구독을 제거합니다. 자세한 내용은 [Delete a Pull Subscription](delete-a-pull-subscription.md) 및 [Delete a Push Subscription](delete-a-push-subscription.md)를 참조하세요.  
  
2.  배포자를 사용하는 모든 게시를 제거하고 게시자와 배포자가 동일한 서버에 있는 경우에는 모든 데이터베이스에 대한 게시를 해제합니다. 자세한 내용은 [Delete a Publication](publish/delete-a-publication.md)을 참조하세요.  
  
3.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> 속성을 지정하고 3단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 전달합니다.  
  
5.  필요에 따라 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 속성을 얻고 게시자가 있는지 확인합니다. 이 메서드가 반환 하는 경우 `false`, 4 단계에서 지정한 게시자 이름이 잘못 되었습니다. 또는이 배포자에서 게시자를 사용 되지 않습니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Remove%2A> 메서드를 호출합니다. 값을 전달 `true` 에 대 한 *강제로* 게시자 및 배포자가 다른 서버에 있으며 게시자에 게시가 더 이상 존재 하는 확인 하지 않고 배포자에서 제거 해야 하는 경우는 게시자입니다.  
  
7.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스의 인스턴스를 만듭니다. 3단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 전달합니다.  
  
8.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.UninstallDistributor%2A> 메서드를 호출합니다. 값을 전달 `true` 에 대 한 *강제로* 를 먼저 확인 하지 않고 배포자의 모든 로컬 게시 데이터베이스가 해제 되었는지, 그리고 배포 데이터베이스가 제거 되었는지 여부를 지정 하는 모든 복제 개체를 제거 합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 다음 예에서는 배포자에서 게시 등록을 제거하고 배포 데이터베이스 삭제하며 배포자를 제거합니다.  
  
 [!code-csharp[HowTo#rmo_DropDistPub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropdistpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropdistpub)]  
  
 다음 예에서는 먼저 로컬 게시 데이터베이스를 해제하거나 배포 데이터베이스를 삭제하지 않고 배포자를 제거합니다.  
  
 [!code-csharp[HowTo#rmo_DropDistPubForce](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropdistpubforce)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPubForce](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropdistpubforce)]  
  
## <a name="see-also"></a>관련 항목  
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [복제 시스템 저장 프로시저 개념](concepts/replication-system-stored-procedures-concepts.md)  
  
  
