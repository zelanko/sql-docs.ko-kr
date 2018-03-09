---
title: "예제: 데이터베이스의 증분 복원(전체 복구 모델) | Microsoft 문서"
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
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: 0a84892d-2f7a-4e77-b2d0-d68b95595210
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67fa86a5deee054be0ca2b5228102975a6fdd19c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="example-piecemeal-restore-of-database-full-recovery-model"></a>예제: 데이터베이스의 증분 복원(전체 복구 모델)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  증분 복원 시퀀스는 주 파일 그룹에서 시작하여 모든 읽기/쓰기가 가능한 모든 보조 파일 그룹의 순서로 파일 그룹 수준에서 데이터베이스를 복원하고 복구합니다.  
  
 이 예에서 `adb` 데이터베이스는 재해 발생 후 새 컴퓨터에 복원됩니다. 데이터베이스에서 전체 복구 모델을 사용하고 있으므로 복원이 시작되기 전에 데이터베이스의 비상 로그 백업을 만들어야 합니다. 재해가 발생하기 전에 모든 파일 그룹은 온라인 상태입니다. 파일 그룹 `B` 는 읽기 전용입니다. 모든 보조 파일 그룹이 복원되어야 합니다. 단, 복원은 `A` (가장 중요), `C`, `B`와 같은 중요도 순으로 이루어져야 합니다. 이 예에서는 비상 로그 백업을 포함하여 4개의 로그 백업이 있습니다.  
  
## <a name="tail-log-backup"></a>비상 로그 백업  
 데이터베이스를 복원하기 전에 데이터베이스 관리자는 비상 로그 백업을 만들어야 합니다. 데이터베이스가 손상되었으므로 비상 로그 백업을 만들려면 NO_TRUNCATE 옵션을 사용해야 합니다.  
  
```  
BACKUP LOG adb TO tailLogBackup WITH NORECOVERY, NO_TRUNCATE  
```  
  
 비상 로그 백업은 다음 복원 시퀀스에서 마지막으로 적용되는 백업입니다.  
  
## <a name="restore-sequences"></a>복원 시퀀스  
  
> [!NOTE]  
>  온라인 복원 시퀀스의 구문은 오프라인 복원 시퀀스의 구문과 동일합니다.  
  
1.  주 파일 그룹과 보조 파일 그룹 `A`를 부분 복원합니다.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
       WITH PARTIAL, NORECOVERY  
    RESTORE DATABASE adb FILEGROUP='A' FROM backup2   
       WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
2.  파일 그룹 `C`를 온라인 복원합니다.  
  
     이때 주 파일 그룹과 보조 파일 그룹 `A` 는 온라인입니다. 파일 그룹 `B` 와 `C` 의 모든 파일은 복구가 보류된 상태이며 파일 그룹은 오프라인입니다.  
  
     1단계에서 마지막 `RESTORE LOG` 문의 메시지는 파일 그룹 `C` 를 사용할 수 없어 이 파일 그룹에 관련된 트랜잭션 롤백이 지연되었음을 나타냅니다. 일반적인 작업은 계속할 수 있지만 이러한 트랜잭션에 의해 잠금이 유지되며 롤백이 완료되기 전에는 로그 잘림이 발생하지 않습니다.  
  
     두 번째 복원 시퀀스에서 데이터베이스 관리자는 파일 그룹 `C`를 복원합니다.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' FROM backup2a WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     이 시점에서 주 파일 그룹 및 파일 그룹 `A` 와 `C` 가 온라인입니다. 파일 그룹 `B` 의 파일은 복구가 보류된 상태이며 파일 그룹은 오프라인입니다. 지연된 트랜잭션이 해결되고 로그 잘림이 발생합니다.  
  
3.  파일 그룹 `B`를 온라인 복원합니다.  
  
     3번째 복원 시퀀스에서 데이터베이스 관리자는 파일 그룹 `B`를 복원합니다. 파일 그룹 `B` 는 파일 그룹이 읽기 전용이 된 후 백업했으므로 복구 중에 롤포워드할 필요가 없습니다.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup2b WITH RECOVERY  
    ```  
  
     이제 모든 파일 그룹이 온라인입니다.  
  
## <a name="additional-examples"></a>추가 예  
  
-   [예제: 데이터베이스의 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [예제: 읽기 전용 파일의 온라인 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [예제: 읽기-쓰기 파일의 온라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [예제: 읽기 전용 파일 온라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [온라인 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
