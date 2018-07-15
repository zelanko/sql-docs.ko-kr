---
title: '예제: 읽기-쓰기 파일의 온라인 복원(전체 복구 모델) | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- online restores [SQL Server], full recovery model
- restore sequences [SQL Server], online
ms.assetid: 0dbeda81-1464-44ba-9011-914900096368
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b139c9173a87e6b7c05c1abcf4d1a7e4c343ec4a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307943"
---
# <a name="example-online-restore-of-a-read-write-file-full-recovery-model"></a>예: 읽기-쓰기 파일의 온라인 복원(전체 복구 모델)
  이 항목에서는 여러 개의 파일 또는 파일 그룹이 있는 전체 복구 모델에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용을 다룹니다.  
  
 이 예에서는 전체 복구 모델을 사용하는 `adb`라는 데이터베이스에 3개의 파일 그룹이 포함되어 있습니다. 파일 그룹 `A` 는 읽기/쓰기가 가능하고 파일 그룹 `B` 와 파일 그룹 `C` 는 읽기 전용입니다. 처음에는 모든 파일 그룹이 온라인입니다.  
  
 파일 그룹 `a1` 에 손상된 파일 `A` 이 있으므로 데이터베이스 관리자는 데이터베이스를 온라인 상태로 유지하면서 이 파일을 복원하려고 합니다.  
  
> [!NOTE]  
>  단순 복구 모델에서는 온라인 상태에서 읽기/쓰기 데이터를 복원할 수 없습니다.  
  
## <a name="restore-sequences"></a>복원 시퀀스  
  
> [!NOTE]  
>  온라인 복원 시퀀스의 구문은 오프라인 복원 시퀀스의 구문과 동일합니다.  
  
1.  파일 `a1`의 온라인 복원  
  
    ```  
    RESTORE DATABASE adb FILE='a1' FROM backup   
    WITH NORECOVERY;  
    ```  
  
     이때 파일 a1은 RESTORING 상태이고 파일 그룹 A는 오프라인입니다.  
  
2.  파일을 복원한 후 데이터베이스 관리자는 파일이 오프라인 상태로 전환된 시점이 캡처되도록 새 로그 백업을 수행합니다.  
  
    ```  
    BACKUP LOG adb TO log_backup3;   
    ```  
  
3.  로그 백업의 온라인 복원  
  
     관리자는 복원된 파일 백업 이후에 수행된 로그 백업부터 시작하여 가장 최근의 로그 백업(2단계에서 수행한*log_backup3*)까지 모든 로그 백업을 복원합니다. 마지막 로그 백업이 복원되면 데이터베이스가 복구됩니다.  
  
    ```  
    RESTORE LOG adb FROM log_backup1 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup2 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY;  
    RESTORE LOG adb WITH RECOVERY;  
    ```  
  
     이제 파일 `a1` 은 온라인 상태입니다.  
  
## <a name="additional-examples"></a>추가 예  
  
-   [예제: 데이터베이스의 증분 복원&#40;단순 복구 모델&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;단순 복구 모델&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [예제: 읽기 전용 파일의 온라인 복원&#40;단순 복구 모델&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [예제: 데이터베이스의 증분 복원&#40;전체 복구 모델&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;전체 복구 모델&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [예제: 읽기 전용 파일 온라인 복원&#40;전체 복구 모델&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>관련 항목  
 [온라인 복원&#40;SQL Server&#41;](online-restore-sql-server.md)   
 [증분 복원&#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [복원 및 복구 개요&#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
