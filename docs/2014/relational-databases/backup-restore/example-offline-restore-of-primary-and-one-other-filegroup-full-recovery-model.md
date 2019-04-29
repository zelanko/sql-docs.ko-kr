---
title: '예: 주 서버와 다른 파일 그룹 (전체 복구 모델)의 오프 라인 복원 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- offline restores [SQL Server]
- restore sequences [SQL Server], offline
ms.assetid: 7d6c50eb-dc84-4d66-855a-0b5f1bd89737
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fec409bf6f391e14dd5e1a2b8b102df2fd00cfd4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62921758"
---
# <a name="example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model"></a>예: 주 서버와 다른 파일 그룹 (전체 복구 모델)의 오프 라인 복원
  이 항목에서는 전체 복구 모델에서 데이터베이스에 여러 개의 파일 그룹이 있는 경우와 관련된 내용을 다룹니다.  
  
 이 예에서 `adb` 라는 데이터베이스에 3개의 파일 그룹이 있습니다. 파일 그룹 `A` 및 `C` 는 읽기/쓰기가 가능하며 파일 그룹 `B` 는 읽기 전용입니다. 주 파일 그룹과 파일 그룹 `B` 는 손상되지만 파일 그룹 `A` 와 `C` 는 그대로 유지됩니다. 재해가 발생하기 전에 모든 파일 그룹은 온라인 상태였습니다.  
  
 데이터베이스 관리자가 주 파일 그룹과 파일 그룹 `B`를 복원 및 복구하려고 합니다. 데이터베이스에서 전체 복구 모델을 사용하고 있으므로 복원이 시작되기 전에 데이터베이스의 비상 로그 백업을 만들어야 합니다. 데이터베이스가 온라인 상태가 되면 파일 그룹 `A` 와 `C` 도 자동으로 온라인 상태가 됩니다.  
  
> [!NOTE]  
>  오프라인 복원 시퀀스는 읽기 전용 파일의 온라인 복원 시퀀스보다 단계 수가 적습니다. 예를 들어 참조 [예제: 읽기 전용 파일 온라인 복원 &#40;전체 복구 모델&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)합니다. 그러나 전체 데이터베이스는 시퀀스가 진행되는 동안 오프라인 상태입니다.  
  
## <a name="tail-log-backup"></a>비상 로그 백업  
 데이터베이스를 복원하기 전에 데이터베이스 관리자는 비상 로그 백업을 만들어야 합니다. 데이터베이스가 손상되었으므로 비상 로그 백업을 만들려면 NO_TRUNCATE 옵션을 사용해야 합니다.  
  
```  
BACKUP LOG adb TO tailLogBackup   
   WITH NORECOVERY, NO_TRUNCATE  
```  
  
 비상 로그 백업은 다음 복원 시퀀스에서 마지막으로 적용되는 백업입니다.  
  
## <a name="restore-sequence"></a>복원 시퀀스  
 주 파일 그룹과 파일 그룹 `B`를 복원하기 위해 데이터베이스 관리자는 다음과 같이 PARTIAL 옵션이 없는 복원 시퀀스를 사용합니다.  
  
```  
RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
WITH NORECOVERY  
RESTORE DATABASE adb FILEGROUP='B' FROM backup2   
WITH NORECOVERY  
RESTORE LOG adb FROM backup3 WITH NORECOVERY  
RESTORE LOG adb FROM backup4 WITH NORECOVERY  
RESTORE LOG adb FROM backup5 WITH NORECOVERY  
RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
```  
  
 복원되지 않은 파일은 자동으로 온라인 상태가 됩니다. 이제 모든 파일 그룹이 온라인 상태입니다.  
  
## <a name="see-also"></a>관련 항목  
 [온라인 복원&#40;SQL Server&#41;](online-restore-sql-server.md)   
 [증분 복원&#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [파일 복원&#40;전체 복구 모델&#41;](file-restores-full-recovery-model.md)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
