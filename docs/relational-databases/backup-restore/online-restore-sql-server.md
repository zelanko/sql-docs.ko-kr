---
title: "온라인 복원(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- online restores [SQL Server]
- online restores [SQL Server], about online restores
ms.assetid: 7982a687-980a-4eb8-8e9f-6894148e7d8c
caps.latest.revision: "45"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3500b144cc3afb10c5ac12ee76e49dc11953623
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="online-restore-sql-server"></a>온라인 복원(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 온라인 복원은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition에서만 지원됩니다. 이 버전에서 기본적으로 파일, 페이지 또는 증분 복원은 온라인 상태입니다. 이 항목에서는 데이터베이스에 여러 개의 파일 또는 파일 그룹이 있는 경우 및 단순 복구 모델에서 데이터베이스에 읽기 전용 파일 그룹만 있는 경우와 관련된 내용을 다룹니다.  
  
 데이터베이스가 온라인 상태인 데이터 복원을 *온라인 복원*이라고 합니다. 데이터베이스는 주 파일 그룹이 온라인 상태일 때마다 하나 이상의 보조 파일 그룹이 오프라인 상태일 경우에도 온라인 상태로 간주됩니다. 복구 모델에서는 데이터베이스가 온라인 상태일 때 오프라인인 파일을 복원할 수 있습니다. 전체 복구 모델에서도 데이터베이스가 온라인 상태일 때 페이지를 복원할 수 있습니다.  
  
> [!NOTE]  
>  온라인 복원은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise에서 자동으로 수행되며 사용자 동작이 필요하지 않습니다. 온라인 복원을 사용하지 않으려면 복원을 시작하기 전에 데이터베이스를 오프라인 상태로 만듭니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [데이터베이스 또는 파일을 오프라인 상태로 만들기](#taking_db_or_file_offline)를 참조하세요.  
  
 온라인 파일 복원을 수행하는 동안 복원된 파일과 해당 파일 그룹은 오프라인 상태입니다. 온라인 복원을 시작할 때 이러한 모든 파일이 온라인 상태일 경우 첫 번째 복원 문은 해당 파일의 파일 그룹을 오프라인 상태로 만듭니다. 반대로 온라인 페이지 복원을 수행하는 동안에는 해당 페이지만 오프라인 상태입니다.  
  
 모든 온라인 복원 시나리오에서는 다음과 같은 기본 단계를 수행합니다.  
  
1.  데이터를 복원합니다.  
  
2.  최종 로그 복원에 WITH RECOVERY를 사용하여 로그를 복원합니다. 이러면 복원된 데이터가 온라인 상태가 됩니다.  
  
 롤백에 필요한 데이터가 시작 시 오프라인 상태여서 커밋되지 않은 트랜잭션을 롤백할 수 없는 경우가 있습니다. 이 경우에는 트랜잭션이 지연됩니다. 자세한 내용은 [지연된 트랜잭션&#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)에서 존재하지 않는 파일 그룹을 제거하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  데이터베이스가 현재 대량 로그 복구 모델을 사용하고 있을 경우 온라인 복원을 시작하기 전에 전체 복구 모델로 전환하는 것이 좋습니다. 자세한 내용은 [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  서버에 연결된 여러 장치로 백업을 수행한 경우에는 온라인 복원 중에 같은 수의 장치를 사용할 수 있어야 합니다.  
  
> [!CAUTION]  
>  스냅숏 백업을 사용하여 **Online Restore**을 수행할 수 없습니다. **스냅숏 백업**에 대한 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
## <a name="log-backups-for-online-restore"></a>온라인 복원용 로그 백업  
 온라인 복원에서 복구 지점은 복원되는 데이터가 오프라인 상태로 된 지점이거나 마지막으로 읽기 전용으로 된 지점입니다. 이 복구 지점을 포함하여 이 지점까지의 트랜잭션 로그 백업은 모두 사용할 수 있어야 합니다. 일반적으로 로그 백업은 파일을 복구한 후에 필요합니다. 단, 해당 데이터가 읽기 전용이 된 후에 수행된 데이터 백업에서 읽기 전용 데이터의 온라인 복원을 수행하는 중인 경우에는 로그 백업이 필요하지 않습니다.  
  
 일반적으로 복원 시퀀스를 시작한 이후에도 데이터베이스가 온라인 상태이면 트랜잭션 로그 백업을 수행할 수 있습니다. 마지막 로그 백업의 시점은 복원된 파일의 속성에 따라 다릅니다.  
  
-   온라인 읽기 전용 파일의 경우 첫 번째 복원 시퀀스 전이나 중간에 복구에 필요한 마지막 로그 백업을 수행할 수 있습니다. 읽기 전용 파일 그룹에서는 해당 파일 그룹이 읽기 전용이 된 이후에 데이터 또는 차등 백업을 수행한 경우 로그 백업이 필요 없습니다.  
  
    > [!NOTE]  
    >  위의 정보는 모든 오프라인 상태인 파일에도 적용할 수 있습니다.  
  
-   특별한 경우로 첫 번째 복원 문이 실행된 시점에서 온라인 상태였다가 해당 복원 문에 의해 자동으로 오프라인 상태가 된 읽기/쓰기 파일이 있습니다. 이 경우 반드시 첫 번째 *복원 순서* (데이터를 복원, 롤포워드 및 복구하는 하나 이상의 RESTORE 문의 순서) 중에 로그 백업을 수행해야 합니다. 일반적으로 이 로그 백업은 모든 전체 백업을 복원한 이후 그리고 데이터를 복구하기 이전에 발생해야 합니다. 그러나 특정 파일 그룹에 대한 파일 백업이 여러 개인 경우 로그 백업의 최소 시점은 해당 파일 그룹이 오프라인 상태가 된 후입니다. 이러한 데이터 복원 후 로그 백업은 파일이 오프라인 상태가 된 지점을 캡처합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 은 온라인 복원에 온라인 로그를 사용할 수 없으므로 이러한 데이터 복원 후 로그 백업이 필요합니다.  
  
    > [!NOTE]  
    >  복원 시퀀스 전에 파일을 수동으로 오프라인 상태로 만들 수도 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "데이터베이스 또는 파일을 오프라인 상태로 만들기"를 참조하세요.  
  
##  <a name="taking_db_or_file_offline"></a> 데이터베이스 또는 파일을 오프라인 상태로 만들기  
 온라인 복원을 사용하지 않으려면 복원 시퀀스를 시작하기 전에 다음 방법 중 하나를 사용하여 데이터베이스를 오프라인 상태로 만들 수 있습니다.  
  
-   복구 모델에서 다음 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문을 사용하여 데이터베이스를 오프라인 상태로 만들 수 있습니다.  
  
     ALTER DATABASE *database_name* SET OFFLINE  
  
-   또는 전체 복구 모델에서 다음 [BACKUP LOG](../../t-sql/statements/backup-transact-sql.md) 문을 사용하여 데이터베이스를 복원 중인 상태로 설정하여 파일이나 페이지 복원을 강제로 오프라인 상태로 만들 수 있습니다.  
  
     BACKUP LOG *database_name* WITH NORECOVERY  
  
 데이터베이스가 오프라인 상태를 유지하면 모든 복원은 오프라인 복원이 됩니다.  
  
## <a name="examples"></a>예  
  
> [!NOTE]  
>  온라인 복원 시퀀스의 구문은 오프라인 복원 시퀀스의 구문과 동일합니다.  
  
-   [예제: 데이터베이스의 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [예제: 읽기 전용 파일의 온라인 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [예제: 데이터베이스의 증분 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [예제: 읽기-쓰기 파일의 온라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [예제: 읽기 전용 파일 온라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [파일 및 파일 그룹 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [페이지 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)  
  
-   [suspect_pages 테이블 관리&#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
-   [데이터를 복원하지 않고 데이터베이스 복구&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
-   [존재하지 않는 파일 그룹 제거&#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [파일 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [파일 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [페이지 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
  
  
