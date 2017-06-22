---
title: "파일 복원(단순 복구 모델) | Microsoft 문서"
ms.custom: 
ms.date: 03/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- file restores [SQL Server]
- simple recovery model [SQL Server]
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- Transact-SQL restore sequence
- restoring files [SQL Server], simple recovery model
- file restores [SQL Server], simple recovery model
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: b6d07386-7c6f-4cc6-be32-93289adbd3d6
caps.latest.revision: 57
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5fdd6a65718ab54c60fcea09317146aa2342e517
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="file-restores-simple-recovery-model"></a>파일 복원(단순 복구 모델)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 하나 이상의 읽기 전용 보조 파일 그룹이 있는 단순 모델 데이터베이스와 관련된 내용을 다룹니다.  
  
 파일 복원의 목표는 전체 데이터베이스를 복원하지 않고 하나 이상의 손상된 파일을 복원하는 것입니다. 단순 복구 모델에서 파일 백업은 읽기 전용 파일에만 지원됩니다. 데이터베이스 또는 부분 백업 복원 시 항상 주 파일 그룹 및 읽기/쓰기 보조 파일 그룹이 함께 복원됩니다.  
  
 파일 복원 시나리오는 다음과 같습니다.  
  
-   오프라인 파일 복원  
  
     *오프라인 파일 복원*에서 손상된 파일 또는 파일 그룹이 복원되는 동안 데이터베이스는 오프라인 상태입니다. 복원 시퀀스의 마지막에 데이터베이스는 온라인 상태가 됩니다.  
  
     모든 버전의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 오프라인 파일 복원을 지원합니다.  
  
-   온라인 파일 복원  
  
     *온라인 파일 복원*의 경우 데이터베이스가 복원 시점에 온라인 상태이면 파일 복원 중에 온라인 상태로 유지됩니다. 그러나 파일을 복원할 각 파일 그룹은 복원 작업 중에 오프라인 상태입니다. 오프라인 파일 그룹의 모든 파일이 복구되면 파일 그룹이 자동으로 온라인 상태가 됩니다.  
  
     온라인 페이지 및 파일 복원 지원에 대한 자세한 내용은 [데이터베이스 엔진 기능 및 태스크](http://msdn.microsoft.com/library/d9efe145-3306-4d61-bd77-e2af43e19c34)를 참조하세요. 온라인 복원에 대한 자세한 내용은 [온라인 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)을 참조하세요.  
  
    > [!TIP]  
    >  파일 복원을 위해 데이터베이스를 오프라인 상태로 전환하려면 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) 문인 ALTER DATABASE *database_name* SET OFFLINE을 실행하여 복원 시퀀스를 시작하기 전에 데이터베이스를 오프라인으로 설정합니다.  
  
 **항목 내용**  
  
-   [단순 복구 모델의 파일 및 파일 그룹 복원 개요](#Overview)  
  
-   [관련 태스크](#RelatedTasks)  
  
##  <a name="Overview"></a> 단순 복구 모델의 파일 및 파일 그룹 복원 개요  
 파일 복원 시나리오는 다음과 같이 올바른 데이터를 복사, 롤포워드 및 복구하는 단일 복원 시퀀스로 구성됩니다.  
  
1.  가장 최근의 파일 백업에서 각각의 손상된 파일을 복원합니다.  
  
2.  복원된 각 파일에 대한 가장 최근의 차등 파일 백업을 복원하고 데이터베이스를 복구합니다.  
  
### <a name="transact-sql-steps-for-file-restore-sequence-simple-recovery-model"></a>파일 복원 시퀀스의 Transact-SQL 단계(단순 복구 모델)  
 이 섹션에서는 단순 파일 복원 시퀀스에 대한 필수 [!INCLUDE[tsql](../../includes/tsql-md.md)][RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 옵션을 보여 줍니다. 이 용도와 관련 없는 구문 및 세부 사항은 생략됩니다.  
  
 복원 시퀀스는 두 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문만 포함됩니다. 첫 번째 문은 WITH NORECOVERY를 사용하여 보조 파일인 `A`파일을 복원합니다. 두 번째 작업에서는 다른 백업 장치에서 WITH RECOVERY를 사용하여 `B` 및 `C` 파일을 복원합니다.  
  
1.  RESTORE DATABASE *database* FILE **=***name_of_file_A*  
  
     FROM *file_backup_of_file_A*  
  
     WITH NORECOVERY**;**  
  
2.  RESTORE DATABASE *database* FILE **=***name_of_file_B***,***name_of_file_C*  
  
     FROM *file_backup_of_files_B_and_C*  
  
     WITH RECOVERY**;**  
  
### <a name="examples"></a>예  
  
-   [예제: 읽기 전용 파일의 온라인 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [예제: 주 파일 그룹 및 다른 파일 그룹의 오프라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **파일과 파일 그룹을 복원하려면**  
  
-   [기존 파일에서 파일 및 파일 그룹 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [파일 및 파일 그룹 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [파일 및 파일 그룹 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Restore.SqlRestore 메서드(서버)(SMO)](http://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.restore.sqlrestore.aspx)   
  
## <a name="see-also"></a>참고 항목  
 [백업 및 복원: 상호 운용성 및 공존성&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [전체 파일 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
