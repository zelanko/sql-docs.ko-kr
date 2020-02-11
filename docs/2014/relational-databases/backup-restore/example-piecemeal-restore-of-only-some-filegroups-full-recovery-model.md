---
title: '예제: 일부 파일 그룹만 증분 복원(전체 복구 모델) | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: bced4b54-e819-472b-b784-c72e14e72a0b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a3ea7a4c7d9189ace988ef57f25e99d61a4273dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62876163"
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-full-recovery-model"></a>예제: 일부 파일 그룹만 증분 복원(전체 복구 모델)
  이 항목에서는 여러 개의 파일 또는 파일 그룹이 있는 전체 복구 모델에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용을 다룹니다.  
  
 증분 복원 시퀀스는 주 파일 그룹에서 시작하여 모든 읽기/쓰기 파일 그룹, 보조 파일 그룹의 순서로 파일 그룹 수준에서 데이터베이스를 복원하고 복구합니다.  
  
 이 예에서는 전체 복구 모델을 사용하는 `adb`라는 데이터베이스에 3개의 파일 그룹이 포함되어 있습니다. 파일 그룹 `A` 는 읽기/쓰기가 가능하고 파일 그룹 `B` 와 파일 그룹 `C` 는 읽기 전용입니다. 처음에는 모든 파일 그룹이 온라인입니다.  
  
 데이터베이스 `B` 의 주 파일 그룹 및 파일 그룹 `adb` 가 손상된 것으로 나타납니다. 주 파일 그룹은 크기가 작으므로 빠르게 복원할 수 있습니다. 데이터베이스 관리자는 증분 복원 시퀀스를 사용하여 이들을 복원하기로 결정합니다. 우선 주 파일 그룹과 다음 트랜잭션 로그를 복원하고 데이터베이스를 복구합니다.  
  
 손상되지 않은 파일 그룹 `A` 와 `C` 에는 중요한 데이터가 들어 있습니다. 그러므로 가능한 빨리 온라인 상태로 만들기 위해 다음으로 이들을 복구합니다. 마지막으로 손상된 보조 파일 그룹 `B`를 복원하고 복구합니다.  
  
## <a name="restore-sequences"></a>복원 시퀀스  
  
> [!NOTE]  
>  온라인 복원 시퀀스의 구문은 오프라인 복원 시퀀스의 구문과 동일합니다.  
  
1.  데이터베이스 `adb`의 비상 로그 백업을 만듭니다. 이 단계는 데이터베이스 복구 지점을 사용하여 손상되지 않은 파일 그룹 `A` 와 `C` 를 최신 상태로 유지하는 데 필요합니다.  
  
    ```  
    BACKUP LOG adb TO tailLogBackup WITH NORECOVERY  
    ```  
  
2.  주 파일 그룹을 부분 복원합니다.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup   
    WITH PARTIAL, NORECOVERY  
    RESTORE LOG adb FROM backup1 WITH NORECOVERY  
    RESTORE LOG adb FROM backup2 WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     이 시점에서 주 파일 그룹은 온라인입니다. 파일 그룹 `A`, `B`및 `C` 의 파일은 복구 보류 상태이고 파일 그룹은 오프라인 상태입니다.  
  
3.  파일 그룹 `A` 및 `C`를 온라인 복원합니다.  
  
     데이터가 손상되지 않았으므로 이 파일 그룹을 백업에서 복원할 필요는 없지만 복구하여 온라인 상태로 만들어야 합니다.  
  
     데이터베이스 관리자가 `A` 와 `C` 를 즉시 복구합니다.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A', FILEGROUP='C' WITH RECOVERY  
    ```  
  
     이 시점에서 주 파일 그룹 및 파일 그룹 `A` 와 `C` 가 온라인입니다. 파일 그룹 `B` 의 파일은 복구가 보류된 상태이며 파일 그룹은 오프라인입니다.  
  
4.  파일 그룹 `B`를 온라인 복원합니다.  
  
     파일 그룹 `B` 의 파일은 이후 언제든지 복원할 수 있습니다.  
  
    > [!NOTE]  
    >  파일 그룹 `B` 는 파일 그룹이 읽기 전용이 된 후 백업했으므로 이러한 파일을 롤포워드할 필요가 없습니다.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY  
    ```  
  
     이제 모든 파일 그룹이 온라인입니다.  
  
## <a name="additional-examples"></a>추가 예  
  
-   [예제: 데이터베이스의 증분 복원&#40;단순 복구 모델&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;단순 복구 모델&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [예제: 읽기 전용 파일의 온라인 복원&#40;단순 복구 모델&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [예제: 데이터베이스의 증분 복원&#40;전체 복구 모델&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [예제: 읽기-쓰기 파일의 온라인 복원&#40;전체 복구 모델&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [예제: 읽기 전용 파일 온라인 복원&#40;전체 복구 모델&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [온라인 복원&#40;SQL Server&#41;](online-restore-sql-server.md)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [증분 복원&#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
