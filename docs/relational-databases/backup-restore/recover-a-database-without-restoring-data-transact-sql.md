---
title: "데이터를 복원하지 않고 데이터베이스 복구(Transact-SQL ) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- restoring [SQL Server], recovery-only
- recovery-only scenario [SQL Server]
- restoring databases [SQL Server], recovery-only
- recovery [SQL Server], recovery-only
- database recovery [SQL Server]
- database restores [SQL Server], recovery-only
- recovery [SQL Server], without restoring data
ms.assetid: 7e8fa620-315d-4e10-a718-23fa5171c09e
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9cf307382a1fcf763b80ddf5e4bc2aac87e7cf68
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="recover-a-database-without-restoring-data-transact-sql"></a>데이터를 복원하지 않고 데이터베이스 복구(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 일반적으로 데이터베이스가 복구되기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 있는 모든 데이터가 복원됩니다. 하지만 예를 들어 데이터베이스와 일치하는 읽기 전용 파일을 복원할 경우 복원 작업에서 백업을 실제로 복원하지 않고 데이터베이스를 복구할 수 있습니다. 이 작업을 *복구 전용 복원*이라고 합니다. 오프라인 데이터가 데이터베이스와 이미 일치하고 사용 가능한 상태로만 만들면 되는 경우 복구 전용 복원 작업은 데이터베이스 복구를 완료하고 데이터를 온라인으로 전환합니다.  
  
 복구 전용 복원은 전체 데이터베이스 또는 하나 이상의 파일 또는 파일 그룹에 대해 수행될 수 있습니다.  
  
## <a name="recovery-only-database-restore"></a>복구 전용 데이터베이스 복원  
 복구 전용 데이터베이스 복원은 다음 경우에 유용할 수 있습니다.  
  
-   복원 시퀀스에서 마지막 백업을 복원할 때 데이터베이스를 복구하지 않았으며 데이터베이스를 지금 복구하여 온라인 상태로 전환하려는 경우  
  
-   데이터베이스가 대기 모드에 있고 다른 로그 백업을 적용하지 않고 데이터베이스를 업데이트할 수 있게 하려는 경우  
  
 복구 전용 데이터베이스 복원의 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 구문은 다음과 같습니다.  
  
 RESTORE DATABASE *database_name* WITH RECOVERY  
  
> [!NOTE]  
>  FROM **=** \<*backup_device>* 절은 백업이 필요 없으므로 복구 전용 복원에 사용되지 않습니다.  
  
 **예제**  
  
 다음 예에서는 데이터를 복원하지 않고 복원 작업에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스를 복구합니다.  
  
```  
-- Restore database using WITH RECOVERY.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY  
```  
  
## <a name="recovery-only-file-restore"></a>복구 전용 파일 복원  
 복구 전용 파일 복원은 다음 경우에 유용할 수 있습니다.  
  
 데이터베이스가 증분 복원된 경우. 주 파일 그룹의 복원이 완료된 후 하나 이상의 복원되지 않은 파일이 새 데이터베이스 상태와 일치하는 경우입니다. 이는 이 파일이 읽기 전용이었기 때문일 수 있습니다. 이러한 파일은 복구만 하면 되며 따로 데이터를 복사할 필요가 없습니다.  
  
 복구 전용 복원 작업에 따라 오프라인 상태인 파일 그룹의 데이터는 온라인 상태로 전환되지만 데이터 복사, 다시 실행 또는 실행 취소 단계는 수행되지 않습니다. 복원 단계에 대한 자세한 내용은 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)를 참조하세요.  
  
 복구 전용 파일 복원의 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 구문은 다음과 같습니다.  
  
 RESTORE DATABASE *database_name* { FILE **=***logical_file_name* | FILEGROUP **=***logical_filegroup_name* }[ **,**...*n* ] WITH RECOVERY  
  
 **예제**  
  
 다음 예에서는 `SalesGroup2`데이터베이스의 보조 파일 그룹 `Sales` 에 있는 파일의 복구 전용 파일 복원에 대해 설명합니다. 주 파일 그룹은 이미 증분 복원의 초기 단계로 복원되었으며 `SalesGroup2` 는 복원된 주 파일 그룹과 일치합니다. 이 파일 그룹을 복구하고 파일 그룹을 온라인 상태로 만들려면 다음과 같은 단일 문만 필요합니다.  
  
```  
RESTORE DATABASE Sales FILEGROUP=SalesGroup2 WITH RECOVERY;  
```  
  
## <a name="examples-of-completing-a-piecemeal-restore-scenario-with-a-recovery-only-restore"></a>복구 전용 복원을 통한 증분 복원 시나리오 완료의 예  
 **단순 복구 모델**  
  
-   [예제: 데이터베이스의 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
 **전체 복구 모델**  
  
-   [예제: 데이터베이스의 증분 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  
## <a name="see-also"></a>참고 항목  
 [온라인 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [파일 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [파일 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
