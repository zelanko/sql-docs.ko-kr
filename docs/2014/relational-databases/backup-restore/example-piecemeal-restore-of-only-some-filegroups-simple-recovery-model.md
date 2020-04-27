---
title: '예제: 일부 파일 그룹만 증분 복원(단순 복구 모델) | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: d7ad026c-5355-4308-9560-0dc843940d4f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7cdc7e6c036a38ac40eb8c7bb2495b1ed5a3e6e7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62922036"
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model"></a>예: 일부 파일 그룹만 증분 복원(단순 복구 모델)
  이 항목에서는 읽기 전용 파일 그룹이 있는 단순 복구 모델에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용을 다룹니다.  
  
 증분 복원 시퀀스는 주 파일 그룹에서 시작하여 모든 읽기/쓰기 파일 그룹, 보조 파일 그룹의 순서로 파일 그룹 수준에서 데이터베이스를 복원하고 복구합니다.  
  
 이 예에서는 단순 복구 모델을 사용하는 `adb`라는 데이터베이스에 3개의 파일 그룹이 포함되어 있습니다. 파일 그룹 `A` 는 읽기/쓰기가 가능하고 파일 그룹 `B` 와 파일 그룹 `C` 는 읽기 전용입니다. 처음에는 모든 파일 그룹이 온라인입니다.  
  
 `B` 데이터베이스의 주 파일 그룹 및 파일 그룹 `adb` 가 손상된 것으로 나타나자 데이터베이스 관리자는 증분 복원 시퀀스를 사용하여 이를 복원하기로 합니다. 단순 복구 모델에서는 읽기/쓰기가 가능한 모든 파일 그룹을 같은 부분 백업에서 복원해야 합니다. 파일 그룹 `A` 는 손상되지 않았지만 데이터베이스가 마지막 부분 백업 끝에서 정의된 지정 시간으로 복원되어 일관성을 유지할 수 있도록 주 파일 그룹으로 복원되어야 합니다. 파일 그룹 `C` 는 손상되지 않았지만 온라인 상태로 만들려면 복구해야 합니다. 파일 그룹 `B`는 손상되었지만 포함된 데이터는 파일 그룹 `C`의 데이터보다 중요성이 낮습니다. 따라서 파일 그룹 `B` 를 마지막에 복원합니다.  
  
## <a name="restore-sequences"></a>복원 시퀀스  
  
> [!NOTE]  
>  온라인 복원 시퀀스의 구문은 오프라인 복원 시퀀스의 구문과 동일합니다.  
  
1.  주 파일 그룹 및 파일 그룹 `A` 를 부분 백업에서 부분 복원  
  
    ```  
    RESTORE DATABASE adb READ_WRITE_FILEGROUPS FROM partial_backup   
    WITH PARTIAL, RECOVERY  
    ```  
  
     이 시점에서 주 파일 그룹과 파일 그룹 `A` 가 온라인입니다. 파일 그룹 `B` 와 `C` 의 파일 복구는 보류 중이며 파일 그룹은 오프라인입니다.  
  
2.  파일 그룹 `C`의 온라인 복구  
  
     파일 그룹 `C` 는 앞서 복원된 부분 백업이 파일 그룹 `C` 가 읽기 전용이 된 이후에 만든 것이기 때문에 복원 시 데이터베이스를 이전 상태로 만드는 경우에도 일관성이 유지됩니다. 데이터베이스 관리자는 파일 그룹 `C`를 복원하지 않고 복구하여 온라인 상태로 만듭니다.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' WITH RECOVERY  
    ```  
  
     이 시점에서 주 파일 그룹 및 파일 그룹 `A` 와 `C` 가 온라인입니다. filegroupB의 파일은 해당 파일 그룹이 오프라인 상태이므로 복구 보류 중 상태를 유지합니다.  
  
3.  파일 그룹 `B.`  
  
     파일 그룹 `B` 의 파일은 반드시 복원해야 합니다. 데이터베이스 관리자는 파일 그룹 `B` 가 읽기 전용이 된 후와 부분 백업 전에 만든 백업으로 파일 그룹 `B` 를 복원합니다.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup   
    WITH RECOVERY  
    ```  
  
     이제 모든 파일 그룹이 온라인입니다.  
  
## <a name="additional-examples"></a>추가 예  
  
-   [예제: 데이터베이스의 증분 복원&#40;단순 복구 모델&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [예제: 읽기 전용 파일의 온라인 복원&#40;단순 복구 모델&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [예제: 데이터베이스의 증분 복원&#40;전체 복구 모델&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;전체 복구 모델&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [예제: 읽기-쓰기 파일의 온라인 복원&#40;전체 복구 모델&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [예제: 읽기 전용 파일 온라인 복원&#40;전체 복구 모델&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>참고 항목  
 [온라인 복원&#40;SQL Server&#41;](online-restore-sql-server.md)   
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [증분 복원&#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
