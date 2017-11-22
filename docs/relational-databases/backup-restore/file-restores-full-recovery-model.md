---
title: "파일 복원(전체 복구 모델) | Microsoft 문서"
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
- file restores [SQL Server]
- full recovery model [SQL Server], performing restores
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- file restores [SQL Server], full recovery model
- restoring files [SQL Server], full recovery model
- Transact-SQL restore sequence
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: d2236a2a-4cf1-4c3f-b542-f73f6096e15c
caps.latest.revision: "42"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76ea0e7617daabdbbf140546e9e08d5f0016a2b2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="file-restores-full-recovery-model"></a>파일 복원(전체 복구 모델)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 전체 또는 대량 로드 복구 모델에서 데이터베이스에 여러 개의 파일 또는 파일 그룹이 있는 경우와 관련된 내용을 다룹니다.  
  
 파일 복원의 목표는 전체 데이터베이스를 복원하지 않고 하나 이상의 손상된 파일을 복원하는 것입니다. 파일 복원 시나리오는 해당 데이터를 복사하고 롤포워드하고 복구하는 단일 복원 시퀀스로 이루어집니다.  
  
 복원 중인 파일 그룹이 읽기/쓰기가 가능한 경우 손상되지 않은 로그 백업 체인은 마지막 데이터 또는 차등 백업이 복원된 후에 적용해야 합니다. 이를 통해 파일 그룹을 로그 파일에 있는 현재 활성 로그 레코드의 로그 레코드로 가져옵니다. 일반적으로 복구 지점은 로그의 후반부이지만 반드시 그런 것은 아닙니다.  
  
 복원 중인 파일 그룹이 읽기 전용인 경우 일반적으로 로그 백업을 적용할 필요가 없으므로 건너뜁니다. 파일이 읽기 전용 상태가 된 이후에 백업이 수행되면 마지막 백업이 복원되고 롤포워드가 대상 지점에서 정지됩니다.  
  
 파일 복원 시나리오는 다음과 같습니다.  
  
-   오프라인 파일 복원  
  
     *오프라인 파일 복원*에서 손상된 파일 또는 파일 그룹이 복원되는 동안 데이터베이스는 오프라인 상태입니다. 복원 시퀀스의 마지막에 데이터베이스는 온라인 상태가 됩니다.  
  
     모든 버전의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 오프라인 파일 복원을 지원합니다.  
  
-   온라인 파일 복원  
  
     *온라인 파일 복원*의 경우 데이터베이스가 복원 시점에 온라인 상태이면 파일 복원 중에 온라인 상태로 유지됩니다. 그러나 파일을 복원할 각 파일 그룹은 복원 작업 중에 오프라인 상태입니다. 오프라인 파일 그룹의 모든 파일이 복구되면 파일 그룹이 자동으로 온라인 상태가 됩니다.  
  
     온라인 페이지 및 파일 복원 지원에 대한 자세한 내용은 [SQL Server 2016의 버전과 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요. 온라인 복원에 대한 자세한 내용은 [온라인 복원(SQL Server)](../../relational-databases/backup-restore/online-restore-sql-server.md)을 참조하세요.
  
    > [!TIP]  
    >  파일 복원을 위해 데이터베이스를 오프라인 상태로 전환하려면 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) 문인 ALTER DATABASE *database_name* SET OFFLINE을 실행하여 복원 시퀀스를 시작하기 전에 데이터베이스를 오프라인으로 설정합니다.  
  
  
##  <a name="Overview"></a> 파일 백업에서 손상된 파일 복원  
  
1.  하나 이상의 손상된 파일을 복원하려면 먼저 [비상 로그 백업](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 만듭니다.  
  
     로그가 손상된 경우에는 비상 로그 백상을 만들 수 없으며 데이터베이스 전체를 복원해야 합니다.  
  
     트랜잭션 로그를 백업하는 방법은 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)을 참조하세요.  
  
    > [!IMPORTANT]  
    >  오프라인 파일을 복원하려면 이 파일을 복원하기 전에 비상 로그 백업을 수행해야 합니다. 온라인 파일을 복원하려면 이 파일을 복원한 후에 로그 백업을 수행해야 합니다. 이러한 로그 백업은 파일을 데이터베이스의 나머지 부분과 일치하는 상태로 복구해야 하기 때문에 필요합니다.  
  
2.  각 손상된 파일을 해당 파일의 최신 백업에서 복원합니다.  
  
3.  복원된 각 파일에 대한 가장 최근의 차등 파일 백업(있을 경우)을 복원합니다.  
  
4.  복원 파일 중 가장 오래된 것을 포함하는 백업부터 시작하여 1단계에서 만든 비상 로그 백업까지 트랜잭션 로그 백업을 순서대로 복원합니다.  
  
     파일 백업 후에는 생성된 트랜잭션 로그 백업을 복원하여 데이터베이스와 일치하는 상태로 만들어야 합니다. 트랜잭션 로그 백업은 복원 파일에 적용된 변경 내용만 적용하므로 빨리 롤포워드할 수 있습니다. 손상되지 않은 파일은 복사되지 않고 롤포워드되므로 개별 파일 복원이 전체 데이터베이스 복원보다 나을 수 있습니다. 하지만 전체 로그 백업 체인은 읽기가 가능해야 합니다.  
  
5.  데이터베이스를 복구합니다.  
  
> [!NOTE]  
>  파일 백업은 지정 시간 이전의 시점으로 데이터베이스를 복원하는 데 사용될 수 있습니다. 이렇게 하려면 파일 백업의 전체 세트를 복원한 후 최근 복원된 파일 백업 다음에 있는 대상 지점에 이를 때까지 순서대로 트랜잭션 로그 백업을 복원해야 합니다. 지정 시간 복구에 대한 자세한 내용은 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)을 참조하세요.  
  
## <a name="transact-sql-restore-sequence-for-an-offline-file-restore-full-recovery-model"></a>오프라인 파일 복원을 위한 Transact-SQL 복원 시퀀스(전체 복구 모델)  
 파일 복원 시나리오는 해당 데이터를 복사하고 롤포워드하고 복구하는 단일 복원 시퀀스로 이루어집니다.  
  
 이 섹션에서는 파일 복원 시퀀스에 대한 필수 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 옵션을 보여 줍니다. 이 용도와 관련 없는 구문 및 세부 사항은 생략됩니다.  
  
 다음 예에서는 WITH NORECOVERY를 사용하여 두 개의 보조 파일 `A` 와 `B`를 오프라인 복원하는 경우를 보여 줍니다. 그런 다음 두 개의 로그 백업에 NORECOVERY를 적용한 다음 WITH RECOVERY를 사용하여 복원되는 비상 로그 백업을 실행합니다.  
  
> [!NOTE]  
>  다음 예에서는 파일을 오프라인으로 전환하여 복원 시퀀스를 시작하고 비상 로그 백업을 만듭니다.  
  
```  
--Take the file offline.  
ALTER DATABASE database_name MODIFY FILE SET OFFLINE;  
-- Back up the currently active transaction log.  
BACKUP LOG database_name  
   TO <tail_log_backup>  
   WITH NORECOVERY;  
GO   
-- Restore the files.  
RESTORE DATABASE database_name FILE=name   
   FROM <file_backup_of_file_A>   
   WITH NORECOVERY;  
RESTORE DATABASE database_name FILE=<name> ......  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
-- Restore the log backups.  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <tail_log_backup>   
   WITH RECOVERY;  
```  
  
## <a name="examples"></a>예  
  
-   [예제: 읽기-쓰기 파일의 온라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [예제: 읽기 전용 파일 온라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
-   [예제: 주 파일 그룹 및 다른 파일 그룹의 오프라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **파일과 파일 그룹을 복원하려면**  
  
-   [새 위치로 파일 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [파일 및 파일 그룹 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
  
## <a name="see-also"></a>참고 항목  
 [백업 및 복원: 상호 운용성 및 공존성&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [전체 파일 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
