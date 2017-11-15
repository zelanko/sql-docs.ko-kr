---
title: "스냅숏 및 트랜잭션 복제의 백업 및 복원 전략 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backups [SQL Server replication], snapshot replication
- restoring [SQL Server replication], transactional replication
- snapshot replication [SQL Server], backup and restore
- restoring [SQL Server replication], snapshot replication
- recovery [SQL Server replication], transactional replication
- transactional replication, backup and restore
- recovery [SQL Server replication], snapshot replication
- sync with backup [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: a8afcdbc-55db-4916-a219-19454f561f9e
caps.latest.revision: "59"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 215580bbf9feec36fbbdb972ecb2aad6a422a196
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication"></a>스냅숏 및 트랜잭션 복제의 백업 및 복원을 위한 전략
  스냅숏 및 트랜잭션 복제에 대한 백업 및 복원 전략을 설계할 때 다음 세 가지 영역을 고려해야 합니다.  
  
-   백업할 데이터베이스  
  
-   트랜잭션 복제에 대한 백업 설정  
  
-   데이터베이스를 복원하는 데 필요한 단계. 이 단계는 선택한 복제 유형 및 옵션에 따라 달라집니다.  
  
 이 항목에서는 다음 3개의 섹션에서 각 영역을 설명합니다. Oracle 게시에 대한 백업 및 복원에 대한 자세한 내용은 [Oracle 게시자 백업 및 복원](../../../relational-databases/replication/non-sql/backup-and-restore-for-oracle-publishers.md)을 참조하세요.  
  
## <a name="backing-up-databases"></a>데이터베이스 백업  
 스냅숏 및 트랜잭션 복제의 경우 다음 데이터베이스를 정기적으로 백업해야 합니다.  
  
-   게시자의 게시 데이터베이스  
  
-   배포자의 배포 데이터베이스  
  
-   각 구독자의 구독 데이터베이스  
  
-   게시자, 배포자 및 모든 구독자의 **master** 및 **msdb** 시스템 데이터베이스. 이러한 데이터베이스는 각각 그리고 관련 복제 데이터베이스와 동시에 백업되어야 합니다. 예를 들어 게시 데이터베이스를 백업할 때는 게시자의 **master** 및 **msdb** 데이터베이스를 동시에 백업합니다. 게시 데이터베이스를 복원한 경우에는 **master** 및 **msdb** 데이터베이스의 복제 구성 및 설정이 게시 데이터베이스와 일치하는지 확인해야 합니다.  
  
 정기적인 로그 백업을 수행할 경우 모든 복제 관련 변경 내용은 로그 백업에 캡처됩니다. 로그 백업을 수행하지 않는 경우 복제와 관련된 설정이 변경될 때마다 백업을 수행해야 합니다. 자세한 내용은 [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md)을 참조하세요.  
  
## <a name="backup-settings-for-transactional-replication"></a>트랜잭션 복제에 대한 백업 설정  
 트랜잭션 복제 과정에는 배포 데이터베이스 및 게시 데이터베이스에 설정할 수 있는 **sync with backup** 옵션이 사용됩니다.  
  
-   배포 데이터베이스에는 이 옵션을 항상 설정하는 것이 좋습니다.  
  
     배포 데이터베이스에 이 옵션을 설정하면 게시 데이터베이스 로그의 트랜잭션은 배포 데이터베이스에서 백업될 때까지 잘리지 않습니다. 배포 데이터베이스는 마지막 백업으로 복원할 수 있으며 손실된 트랜잭션은 게시 데이터베이스에서 배포 데이터베이스로 배달됩니다. 복제는 아무런 영향 없이 계속됩니다.  
  
     배포 데이터베이스에 이 옵션을 설정해도 복제 지연 시간에는 영향을 주지 않습니다. 그러나 배포 데이터베이스의 해당 트랜잭션이 백업될 때까지 게시 데이터베이스의 로그 잘라내기가 지연됩니다. 이로 인해 게시 데이터베이스에 더 큰 트랜잭션 로그가 만들어질 수 있습니다.  
  
-   응용 프로그램에서 추가 대기 시간을 허용할 수 있는 경우 게시 데이터베이스에 이 옵션을 설정하는 것이 좋습니다.  
  
     게시 데이터베이스에 이 옵션을 설정하면 트랜잭션은 게시 데이터베이스에서 백업될 때까지 배포 데이터베이스로 배달되지 않습니다. 그러면 복원된 게시 데이터베이스에 없는 트랜잭션이 배포 데이터베이스에 있을 수 없으므로 게시자에서 마지막 게시 데이터베이스 백업을 복원할 수 있습니다.  
  
     트랜잭션이 게시자에서 백업될 때까지 배포 데이터베이스로 배달될 수 없으므로 지연 시간 및 처리량에 영향을 받습니다. 예를 들어 트랜잭션 로그가 5분마다 백업되는 경우에는 트랜잭션이 게시자에서 커밋된 후 배포 데이터베이스와 구독자로 차례로 배달되기까지 5분의 추가 대기 시간이 발생합니다.  
  
    > [!NOTE]  
    >  **sync with backup** 옵션을 사용하면 게시 데이터베이스와 배포 데이터베이스 간의 일관성을 유지할 수 있지만 데이터가 손실될 수도 있습니다. 예를 들어 트랜잭션 로그가 손실되는 경우 마지막 트랜잭션 로그 백업 이후에 커밋된 트랜잭션은 게시 데이터베이스 또는 배포 데이터베이스에서 사용할 수 없습니다. 이 동작은 복제되지 않는 데이터베이스에서도 같습니다.  
  
 **sync with backup 옵션을 설정하려면**  
  
-   복제 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 프로그래밍: [트랜잭션 복제에 대해 통합 백업 사용&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)  
  
## <a name="restoring-databases-involved-in-replication"></a>복제와 관련된 데이터베이스 복원  
 최근 백업을 사용할 수 있는 상태에서 적절한 단계를 수행하면 복제 토폴로지의 모든 데이터베이스를 복원할 수 있습니다. 게시 데이터베이스의 복원 단계는 사용된 복제 유형 및 옵션에 따라 다르지만 다른 모든 데이터베이스의 복원 단계는 유형 및 옵션과 상관이 없습니다.  
  
 복제에서는 복제된 데이터베이스를 백업이 생성된 서버 및 데이터베이스로 복원할 수 있습니다. 복제된 데이터베이스의 백업을 다른 서버 또는 데이터베이스로 복원할 경우 복제 설정은 유지되지 않습니다. 이 경우 백업 복원 후 모든 게시 및 구독을 다시 만들어야 합니다.  
  
### <a name="publisher"></a>게시자  
 다음과 같은 복제 유형에 대한 복원 단계가 제공됩니다.  
  
-   스냅숏 복제  
  
-   읽기 전용 트랜잭션 복제  
  
-   구독 업데이트가 있는 트랜잭션 복제  
  
-   피어 투 피어 트랜잭션 복제  
  
 이 4가지 복제에 대한 **msdb** 데이터베이스 및 **master** 데이터베이스(이 섹션에서 함께 설명됨)의 복원은 모두 동일합니다.  
  
#### <a name="publication-database-snapshot-replication"></a>게시 데이터베이스: 스냅숏 복제  
  
1.  게시 데이터베이스의 최신 백업을 복원합니다. 2단계로 이동합니다.  
  
2.  게시 데이터베이스 백업이 모든 게시 및 구독에 대한 최신 구성을 포함하고 있는지 확인합니다. 그렇다면 복원이 완료된 것이며, 그렇지 않으면 3단계로 이동합니다.  
  
3.  게시자, 배포자 및 구독자에서 복제 구성을 제거한 후 구성을 다시 만듭니다. 이 단계로 복원이 완료됩니다.  
  
     복제를 제거하는 방법은 [sp_removedbreplication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 참조하세요.  
  
#### <a name="publication-database-read-only-transactional-replication"></a>게시 데이터베이스: 읽기 전용 트랜잭션 복제  
  
1.  게시 데이터베이스의 최신 백업을 복원합니다. 2단계로 이동합니다.  
  
2.  실패하기 전에 게시 데이터베이스에 **sync with backup** 옵션을 설정했는지 확인합니다. 옵션을 설정했으면 3단계로 이동하고, 그렇지 않으면 5단계로 이동합니다.  
  
     옵션이 설정되어 있으면 `SELECT DATABASEPROPERTYEX('<PublicationDatabaseName>', 'IsSyncWithBackup')` 쿼리가 '1'을 반환합니다.  
  
3.  복원된 백업이 완료되었으며 최신 상태인지 확인합니다. 또한 모든 게시 및 구독에 대한 최신 구성을 포함하고 있는지 확인합니다. 그렇다면 복원이 완료된 것이며, 그렇지 않으면 4단계로 이동합니다.  
  
4.  복원된 게시 데이터베이스의 구성 정보가 최신 상태가 아닙니다. 따라서 배포 데이터베이스의 처리 중인 모든 명령이 구독자에 배포되었는지 확인한 다음 복제 구성을 삭제하고 다시 만들어야 합니다.  
  
    1.  모든 구독자가 배포 데이터베이스의 처리 중인 명령과 동기화될 때까지 배포 에이전트를 실행합니다. 복제 모니터에서 **배포되지 않은 명령** 탭을 사용하거나 배포 데이터베이스에서 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 뷰를 쿼리하여 모든 명령이 구독자에 배달되었는지 확인합니다. b 단계로 이동합니다.  
  
         배포 에이전트를 실행하는 방법은 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 및 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
         명령을 확인하는 방법은 [배포 데이터베이스의 복제된 명령 및 기타 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) 및 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
    2.  게시자, 배포자 및 구독자에서 복제 구성을 제거한 후 구성을 다시 만듭니다. 구독을 다시 만들 때 구독자에 이미 데이터가 있다고 지정합니다. 이로써 복원이 완료됩니다.  
  
         복제를 제거하는 방법은 [sp_removedbreplication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 참조하세요.  
  
         구독자에 이미 데이터가 있다고 지정하는 방법은 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)를 참조하십시오.  
  
5.  게시 데이터베이스에 **sync with backup** 옵션이 설정되지 않아서 복원된 백업에 포함되지 않은 트랜잭션이 배포자 및 구독자에 배달되었을 수 있습니다. 배포 데이터베이스의 처리 중인 모든 명령이 구독자에 배달되었는지 확인한 다음 복원된 백업에 포함되지 않은 모든 트랜잭션을 게시 데이터베이스에 수동으로 적용해야 합니다.  
  
    > [!IMPORTANT]  
    >  이 과정을 수행하면 게시된 테이블이 백업에서 복원된 다른 비게시 테이블보다 더 최신 시점으로 복원될 수 있습니다.  
  
    1.  모든 구독자가 배포 데이터베이스의 처리 중인 명령과 동기화될 때까지 배포 에이전트를 실행합니다. 복제 모니터에서 **배포되지 않은 명령** 탭을 사용하거나 배포 데이터베이스에서 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 뷰를 쿼리하여 모든 명령이 구독자에 배달되었는지 확인합니다. b 단계로 이동합니다.  
  
         배포 에이전트를 실행하는 방법은 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 및 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
         명령을 확인하는 방법은 [배포 데이터베이스의 복제된 명령 및 기타 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) 및 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
    2.  [tablediff 유틸리티](../../../tools/tablediff-utility.md) 또는 다른 도구를 사용하여 게시자를 구독자와 수동으로 동기화합니다. 이렇게 하면 게시 데이터베이스 백업에 포함되지 않은 데이터를 구독 데이터베이스에서 복구할 수 있습니다. c 단계로 이동합니다.  
  
         **tablediff** 유틸리티에 대한 자세한 내용은 [복제된 테이블의 차이점 비교&#40;복제 프로그래밍&#41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)를 참조하세요.  
  
    3.  복원된 백업이 완료되었으며 최신 상태인지 확인합니다. 또한 모든 게시 및 구독에 대한 최신 구성을 포함하고 있는지 확인합니다. 그렇다면 저장 프로시저 [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) 를 실행하여 게시자 메타데이터를 배포자 메타데이터와 다시 동기화합니다. 이로써 복원이 완료됩니다. 그렇지 않으면 d 단계로 이동합니다.  
  
    4.  게시자, 배포자 및 구독자에서 복제 구성을 제거한 후 구성을 다시 만듭니다. 구독을 다시 만들 때 구독자에 이미 데이터가 있다고 지정합니다. 이로써 복원이 완료됩니다.  
  
         복제를 제거하는 방법은 [sp_removedbreplication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 참조하세요.  
  
         구독자에 이미 데이터가 있다고 지정하는 방법은 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)를 참조하십시오.  
  
#### <a name="publication-database-transactional-replication-with-updating-subscriptions"></a>게시 데이터베이스: 구독 업데이트가 있는 트랜잭션 복제  
  
1.  게시 데이터베이스의 최신 백업을 복원합니다. 2단계로 이동합니다.  
  
2.  모든 구독자가 배포 데이터베이스의 처리 중인 명령과 동기화될 때까지 배포 에이전트를 실행합니다. 복제 모니터에서 **배포되지 않은 명령** 탭을 사용하거나 배포 데이터베이스에서 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 뷰를 쿼리하여 모든 명령이 구독자에 배달되었는지 확인합니다. 3단계로 이동합니다.  
  
     배포 에이전트를 실행하는 방법은 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 및 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
     명령을 확인하는 방법은 [배포 데이터베이스의 복제된 명령 및 기타 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) 및 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
3.  지연 업데이트 구독을 사용하는 경우 각 구독자에 연결하고 구독 데이터베이스에 있는 [MSreplication_queue&#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msreplication-queue-transact-sql.md) 테이블의 모든 행을 삭제합니다. 4단계로 이동합니다.  
  
    > [!NOTE]  
    >  지연 업데이트 구독을 사용하고 있으며 테이블에 ID 열이 있는 경우 복원 후에 올바른 ID 범위가 지정되었는지 확인해야 합니다. 자세한 내용은 [ID 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.  
  
4.  배포 데이터베이스의 처리 중인 모든 명령이 구독자에 배달되었는지 확인한 다음 복원된 백업에 포함되지 않은 모든 트랜잭션을 게시 데이터베이스에 수동으로 적용해야 합니다.  
  
    > [!IMPORTANT]  
    >  이 과정을 수행하면 게시된 테이블이 백업에서 복원된 다른 비게시 테이블보다 더 최신 시점으로 복원될 수 있습니다.  
  
    1.  모든 구독자가 배포 데이터베이스의 처리 중인 명령과 동기화될 때까지 배포 에이전트를 실행합니다. 복제 모니터를 사용하거나 배포 데이터베이스에서 [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) 뷰를 쿼리하여 모든 명령이 구독자에 배달되었는지 확인합니다. b 단계로 이동합니다.  
  
    2.  [tablediff Utility](../../../tools/tablediff-utility.md) 또는 다른 도구를 사용하여 게시자를 구독자와 수동으로 동기화합니다. 이렇게 하면 게시 데이터베이스 백업에 포함되지 않은 데이터를 구독 데이터베이스에서 복구할 수 있습니다. c 단계로 이동합니다.  
  
         **tablediff** 유틸리티에 대한 자세한 내용은 [복제된 테이블의 차이점 비교&#40;복제 프로그래밍&#41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)를 참조하세요.  
  
    3.  복원된 백업이 완료되었으며 최신 상태인지 확인합니다. 또한 모든 게시 및 구독에 대한 최신 구성을 포함하고 있는지 확인합니다. 그렇다면 저장 프로시저 [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) 를 실행하여 게시자 메타데이터를 배포자 메타데이터와 다시 동기화합니다. 이로써 복원이 완료됩니다. 그렇지 않으면 d 단계로 이동합니다.  
  
    4.  게시자, 배포자 및 구독자에서 복제 구성을 제거한 후 구성을 다시 만듭니다. 구독을 다시 만들 때 구독자에 이미 데이터가 있다고 지정합니다. 이로써 복원이 완료됩니다.  
  
         복제를 제거하는 방법은 [sp_removedbreplication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 참조하세요.  
  
         구독자에 이미 데이터가 있다고 지정하는 방법은 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)를 참조하십시오.  
  
#### <a name="publication-database-peer-to-peer-transactional-replication"></a>게시 데이터베이스: 피어 투 피어 트랜잭션 복제  
 다음 단계에서 게시 데이터베이스 **A**, **B**및 **C** 는 피어 투 피어 트랜잭션 복제 토폴로지에 있습니다. **A** 및 **C** 데이터베이스는 온라인 상태이며 제대로 작동하고 있습니다. **B** 데이터베이스는 복원될 데이터베이스입니다. 여기에서 설명하는 절차, 특히 7, 10 및 11단계는 피어 투 피어 토폴로지에 노드를 추가하는 데 필요한 절차와 매우 비슷합니다. 이러한 단계를 가장 간단하게 수행하려면 피어 투 피어 토폴로지 구성 마법사를 사용하면 되지만, 저장 프로시저를 사용할 수도 있습니다.  
  
1.  배포 에이전트를 실행하여 **A** 및 **C** 데이터베이스의 구독을 동기화합니다. 2단계로 이동합니다.  
  
     배포 에이전트를 실행하는 방법은 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 및 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
2.  **B**에서 사용하는 배포 데이터베이스를 아직 사용할 수 있는 경우 배포 에이전트를 실행하여 **B** 데이터베이스와 **A** 데이터베이스 간의 구독과 B 데이터베이스와 **C** 데이터베이스 간의 구독을 동기화합니다. 3단계로 이동합니다.  
  
3.  **B**에 대한 배포 데이터베이스에서 [sp_removedistpublisherdbreplication](../../../relational-databases/system-stored-procedures/sp-removedistpublisherdbreplication-transact-sql.md)을 실행하여 **B**에서 사용하는 배포 데이터베이스의 메타데이터를 제거합니다. 4단계로 이동합니다.  
  
4.  **A** 및 **C** 데이터베이스에서 **B** 데이터베이스의 게시에 대한 구독을 삭제합니다. 5단계로 이동합니다.  
  
     구독 삭제 방법은 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)을 참조하십시오.  
  
5.  **A** 데이터베이스의 로그 백업 또는 전체 백업을 수행합니다. 6단계로 이동합니다.  
  
6.  **A** 데이터베이스의 백업을 **B** 데이터베이스에 복원합니다. 이제 **B** 데이터베이스에는 **A** 데이터베이스의 데이터는 있지만 복제 구성은 없습니다. 백업을 다른 서버로 복원하면 복제가 제거되므로 이 경우 **B** 데이터베이스에서 복제가 제거된 것입니다. 7단계로 이동합니다.  
  
7.  **B** 데이터베이스에 게시를 다시 만든 후 **A** 데이터베이스와 **B** 데이터베이스 간에 구독을 다시 만듭니다. **C** 데이터베이스와 관련된 구독은 이후 단계에서 처리합니다.  
  
    1.  **B** 데이터베이스에 게시를 다시 만듭니다. b 단계로 이동합니다.  
  
    2.  구독자에 이미 데이터가 있음을 지정하여 **B** 데이터베이스에서 **A**데이터베이스의 게시에 대한 구독을 다시 만들고 해당 구독이 백업으로 초기화되도록 지정합니다. 즉, **sp_addsubscription** 의 **@sync_type** 매개 변수에 [initialize with backup](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)값을 지정합니다. c 단계로 이동합니다.  
  
    3.  구독자에 이미 데이터가 있음을 지정하여 **A** 데이터베이스에서 **B**데이터베이스의 게시에 대한 구독을 다시 만들고 해당 구독자에 이미 데이터가 있다고 지정합니다. 즉, **sp_addsubscription** 의 **@sync_type** 매개 변수에 [initialize with backup](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)값을 지정합니다. 8단계로 이동합니다.  
  
8.  배포 에이전트를 실행하여 **A** 및 **B** 데이터베이스의 구독을 동기화합니다. 게시된 테이블에 ID 열이 있으면 9단계로 이동합니다. 그렇지 않은 경우에는 10단계로 이동합니다.  
  
9. 복원 후에 **A** 데이터베이스의 각 테이블에 할당한 ID 범위는 **B** 데이터베이스에서도 사용됩니다. 복원된 **B** 데이터베이스가 실패한 **B** 데이터베이스의 모든 변경 내용(**A** 데이터베이스와 **C** 데이터베이스로 전파됨)을 받았는지 확인한 다음 각 테이블의 ID 범위에 대한 초기값을 다시 설정합니다.  
  
    1.  **B** 데이터베이스에서 [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)를 실행하고 출력 매개 변수 **@request_id**를 검색합니다. b 단계로 이동합니다.  
  
    2.  기본적으로 배포 에이전트는 연속적으로 실행되도록 설정되므로 토큰이 모든 노드로 자동 전송됩니다. 배포 에이전트가 연속 모드로 실행되지 않을 경우에는 에이전트를 실행합니다. 자세한 내용은 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 또는 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)를 참조하세요. c 단계로 이동합니다.  
  
    3.  [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)를 실행하고 b 단계에서 검색한 **@request_id** 값을 지정합니다. 모든 노드가 피어 요청을 받았음을 표시할 때까지 기다립니다. d 단계로 이동합니다.  
  
    4.  [DBCC CHECKIDENT](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md) 를 통해 **B** 데이터베이스에 있는 각 테이블의 ID 범위에 대한 초기값을 다시 설정하여 적절한 범위가 사용되도록 합니다. 10단계로 이동합니다.  
  
     ID 범위 관리 방법은 [ID 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)의 "ID 범위 수동 관리를 위한 범위 할당" 섹션을 참조하세요.  
  
10. 이 시점에서 **B** 데이터베이스와 **C** 데이터베이스는 직접 연결되어 있지 않지만 **A** 데이터베이스를 통해 변경 내용을 받습니다. 토폴로지에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]가 실행되는 노드가 들어 있으면 11단계로 이동하고, 그렇지 않으면 12단계로 이동합니다.  
  
11. 시스템을 정지하고 **B** 및 **C** 데이터베이스 간에 구독을 다시 만듭니다. 시스템 정지 과정에서는 모든 노드에서 게시된 테이블에 대한 작업을 중지하고 각 노드가 다른 모든 노드의 변경 내용을 받았는지 확인합니다.  
  
    1.  피어 투 피어 토폴로지의 게시된 테이블에 대한 모든 작업을 중지합니다. b 단계로 이동합니다.  
  
    2.  **B** 데이터베이스에서 [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)를 실행하고 출력 매개 변수 **@request_id**를 검색합니다. c 단계로 이동합니다.  
  
    3.  기본적으로 배포 에이전트는 연속적으로 실행되도록 설정되므로 토큰이 모든 노드로 자동 전송됩니다. 배포 에이전트가 연속 모드로 실행되지 않을 경우에는 에이전트를 실행합니다. d 단계로 이동합니다.  
  
    4.  [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)를 실행하고 b 단계에서 검색한 **@request_id** 값을 지정합니다. 모든 노드가 피어 요청을 받았음을 표시할 때까지 기다립니다. e 단계로 이동합니다.  
  
    5.  구독자에 이미 데이터가 있음을 지정하여 **B** 데이터베이스에서 **C**데이터베이스의 게시에 대한 구독을 다시 만듭니다. b 단계로 이동합니다.  
  
    6.  구독자에게 이미 데이터가 있음을 지정하여 **C** 데이터베이스에서 **B**데이터베이스의 게시에 대한 구독을 다시 만듭니다. 13단계로 이동합니다.  
  
12. **B** 데이터베이스와 **C**데이터베이스 간에 구독을 다시 만듭니다.  
  
    1.  **B**데이터베이스에서 [MSpeer_lsns](../../../relational-databases/system-tables/mspeer-lsns-transact-sql.md) 테이블을 쿼리하여 **B** 데이터베이스에서 **C**데이터베이스로부터 받은 최신 트랜잭션의 LSN(로그 시퀀스 번호)을 검색합니다.  
  
    2.  구독자에 이미 데이터가 있음을 지정하여 **B** 데이터베이스에서 **C**데이터베이스의 게시에 대한 구독을 다시 만들고 LSN을 기반으로 구독이 초기화되도록 지정합니다. 즉, **sp_addsubscription** 의 **@sync_type** 매개 변수에 [initialize with backup](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)값을 지정합니다. b 단계로 이동합니다.  
  
    3.  구독자에게 이미 데이터가 있음을 지정하여 **C** 데이터베이스에서 **B**데이터베이스의 게시에 대한 구독을 다시 만듭니다. 13단계로 이동합니다.  
  
13. 배포 에이전트를 실행하여 **B** 및 **C** 데이터베이스의 구독을 동기화합니다. 이로써 복원이 완료됩니다.  
  
#### <a name="msdb-database-publisher"></a>msdb 데이터베이스(게시자)  
  
1.  **msdb** 데이터베이스의 최신 백업을 복원합니다.  
  
2.  복원된 백업이 완료되었으며 최신 상태인지 확인합니다. 또한 모든 게시 및 구독에 대한 최신 구성을 포함하고 있는지 확인합니다. 그렇다면 복구가 완료된 것이며 그렇지 않으면 3단계로 이동합니다.  
  
3.  복제 스크립트에서 구독 정리 작업을 다시 만듭니다. 복구가 완료되었습니다.  
  
#### <a name="master-database-publisher"></a>master 데이터베이스(게시자)  
  
1.  **master** 데이터베이스의 최신 백업을 복원합니다.  
  
2.  해당 데이터베이스의 복제 구성 및 설정이 게시 데이터베이스의 복제 구성 및 설정과 일치하는지 확인합니다.  
  
### <a name="databases-at-the-distributor"></a>배포자의 데이터베이스  
  
#### <a name="distribution-database"></a>배포 데이터베이스  
  
1.  배포 데이터베이스의 최신 백업을 복원합니다.  
  
2.  실패하기 전에 배포 데이터베이스에 **sync with backup** 옵션을 설정했는지 확인합니다. 그렇다면 3단계로 이동하고, 그렇지 않으면 4단계로 이동합니다.  
  
     옵션이 설정되어 있으면 `SELECT DATABASEPROPERTYEX('<DistributionDatabaseName>', 'IsSyncWithBackup')` 쿼리가 '1'을 반환합니다.  
  
3.  복원된 백업이 완료되었으며 최신 상태인지 확인합니다. 또한 모든 게시 및 구독에 대한 최신 구성을 포함하고 있는지 확인합니다. 그렇다면 복구가 완료된 것이며 그렇지 않으면 4단계로 이동합니다.  
  
4.  복원된 배포 데이터베이스의 구성 정보가 최신 상태가 아니거나 배포 데이터베이스에 **sync with backup** 옵션이 설정되지 않았습니다. 복원 후 게시자에서 커밋되었지만 구독자로 배달되지 않은 트랜잭션이 배포 데이터베이스에는 없을 수도 있습니다. 복제를 삭제하고 다시 만든 다음 유효성 검사를 실행합니다.  
  
    1.  게시자, 배포자 및 구독자에서 복제 구성을 제거한 후 구성을 다시 만듭니다. 구독을 다시 만들 때 구독자에 이미 데이터가 있다고 지정합니다. b 단계로 이동합니다.  
  
         복제를 제거하는 방법은 [sp_removedbreplication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 참조하세요.  
  
         구독자에 이미 데이터가 있다고 지정하는 방법은 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)를 참조하십시오.  
  
    2.  모든 게시의 유효성을 검사하도록 표시합니다. 유효성 검사에 실패한 모든 구독을 다시 초기화합니다. 복구가 완료되었습니다.  
  
         유효성 검사에 대한 자세한 내용은 [Validate Replicated Data](../../../relational-databases/replication/validate-replicated-data.md)를 참조하십시오. 다시 초기화에 대한 자세한 내용은 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)를 참조하세요.  
  
#### <a name="msdb-database-distributor"></a>msdb 데이터베이스(배포자)  
  
1.  **msdb** 데이터베이스의 최신 백업을 복원합니다.  
  
2.  복원된 백업이 완료되었으며 최신 상태인지 확인합니다. 또한 모든 게시 및 구독에 대한 최신 구성을 포함하고 있는지 확인합니다. 그렇다면 복구가 완료된 것이며 그렇지 않으면 3단계로 이동합니다.  
  
3.  게시자, 배포자 및 구독자에서 복제 구성을 제거한 후 구성을 다시 만듭니다. 구독을 다시 만들 때 구독자에 이미 데이터가 있다고 지정합니다. 4단계로 이동합니다.  
  
     복제를 제거하는 방법은 [sp_removedbreplication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 참조하세요.  
  
     구독자에 이미 데이터가 있다고 지정하는 방법은 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)를 참조하십시오.  
  
4.  모든 게시의 유효성을 검사하도록 표시합니다. 유효성 검사에 실패한 모든 구독을 다시 초기화합니다. 복구가 완료되었습니다.  
  
     유효성 검사에 대한 자세한 내용은 [Validate Replicated Data](../../../relational-databases/replication/validate-replicated-data.md)를 참조하십시오. 다시 초기화에 대한 자세한 내용은 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)를 참조하세요.  
  
#### <a name="master-database-distributor"></a>master 데이터베이스(배포자)  
  
1.  **master** 데이터베이스의 최신 백업을 복원합니다.  
  
2.  해당 데이터베이스의 복제 구성 및 설정이 게시 데이터베이스의 복제 구성 및 설정과 일치하는지 확인합니다.  
  
### <a name="databases-at-the-subscriber"></a>구독자의 데이터베이스  
  
#### <a name="subscription-database"></a>구독 데이터베이스  
  
1.  최신 구독 데이터베이스 백업이 배포 데이터베이스의 최소 배포 보존 기간 설정보다 최신인지 확인합니다. 이를 통해 배포자에 구독자를 최신 상태로 만들기 위해 필요한 명령이 모두 있는지 여부를 확인합니다. 그렇다면 2단계로 이동합니다. 그렇지 않으면 구독을 다시 초기화합니다. 복구가 완료되었습니다.  
  
     최대 배포 보존 기간 설정을 확인하려면 [sp_helpdistributiondb](../../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) 를 실행하고 **max_distretention** 열의 값을 검색합니다. 이 값은 시간 단위로 표시됩니다.  
  
     구독을 다시 초기화하는 방법은 [Reinitialize a Subscription](../../../relational-databases/replication/reinitialize-a-subscription.md)를 참조하십시오.  
  
2.  최신 구독 데이터베이스 백업을 복원합니다. 3단계로 이동합니다.  
  
3.  구독 데이터베이스에 밀어넣기 구독만 있는 경우 4단계로 이동합니다. 구독 데이터베이스에 끌어오기 구독이 있는 경우에는 구독 정보가 최신 정보인지, 이 데이터베이스에 오류 발생 시 설정된 테이블과 옵션이 모두 포함되어 있는지 확인합니다. 그렇다면 4단계로 이동합니다. 그렇지 않으면 구독을 다시 초기화합니다. 복구가 완료되었습니다.  
  
4.  구독자를 동기화하려면 배포 에이전트를 실행합니다. 복구가 완료되었습니다.  
  
     배포 에이전트를 실행하는 방법은 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 및 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
#### <a name="msdb-database-subscriber"></a>msdb 데이터베이스(구독자)  
  
1.  **msdb** 데이터베이스의 최신 백업을 복원합니다. 이 구독자에서 끌어오기 구독이 사용되는지 확인합니다. 그렇지 않으면 복원이 완료된 것입니다. 그렇다면 2단계로 이동합니다.  
  
2.  복원된 백업이 완료되었으며 최신 상태인지 확인합니다. 또한 모든 게시 및 구독에 대한 최신 구성을 포함하고 있는지 확인합니다. 그렇다면 복구가 완료된 것이며 그렇지 않으면 3단계로 이동합니다.  
  
3.  끌어오기 구독을 삭제하고 다시 만듭니다. 구독을 다시 만들 때 구독자에 이미 데이터가 있다고 지정합니다. 이로써 복원이 완료됩니다.  
  
     구독 삭제 방법은 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)을 참조하십시오.  
  
     구독자에 이미 데이터가 있다고 지정하는 방법은 [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md)를 참조하십시오.  
  
#### <a name="master-database-subscriber"></a>master 데이터베이스(구독자)  
  
1.  **master** 데이터베이스의 최신 백업을 복원합니다.  
  
2.  해당 데이터베이스의 복제 구성 및 설정이 게시 데이터베이스의 복제 구성 및 설정과 일치하는지 확인합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 데이터베이스 백업 및 복원](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [복제된 데이터베이스 백업 및 복원](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [배포 구성](../../../relational-databases/replication/configure-distribution.md)   
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)   
 [구독 초기화](../../../relational-databases/replication/initialize-a-subscription.md)   
 [데이터 동기화](../../../relational-databases/replication/synchronize-data.md)  
  
  
