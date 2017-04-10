---
title: "예제: 읽기 전용 파일 온라인 복원(전체 복구 모델) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "전체 복구 모델 [SQL Server], 복원 예제"
  - "온라인 복원 [SQL Server], 전체 복구 모델"
  - "복원 시퀀스 [SQL Server], 온라인"
ms.assetid: 7ea2d2af-086f-48dc-9636-38dc194c7090
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 26
---
# 예제: 읽기 전용 파일 온라인 복원(전체 복구 모델)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 여러 개의 파일 또는 파일 그룹이 있는 전체 복구 모델에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용을 다룹니다.  
  
 이 예에서는 전체 복구 모델을 사용하는 `adb`라는 데이터베이스에 3개의 파일 그룹이 포함되어 있습니다. 파일 그룹 `A`는 읽기/쓰기가 가능하고 파일 그룹 `B`와 파일 그룹 `C`는 읽기 전용입니다. 처음에는 모든 파일 그룹이 온라인입니다.  
  
 `b1` 데이터베이스의 파일 그룹 `B`에 있는 읽기 전용 파일 `adb`을 복원해야 합니다. 파일이 읽기 전용 상태가 된 이후 백업이 수행되었으므로 로그 백업은 필요하지 않습니다. 파일 그룹 `B`는 복원 기간 중 오프라인 상태가 되지만 나머지 데이터베이스는 온라인 상태가 유지됩니다.  
  
## 복원 시퀀스  
  
> [!NOTE]  
>  온라인 복원 시퀀스의 구문은 오프라인 복원 시퀀스의 구문과 동일합니다.  
  
 데이터베이스 관리자는 다음 복원 시퀀스에 따라 파일을 복원할 수 있습니다.  
  
```  
RESTORE DATABASE adb FILE='b1' FROM filegroup_B_backup  
WITH RECOVERY   
```  
  
 이제 파일 그룹 B가 온라인입니다.  
  
## 추가 예  
  
-   [예제: 데이터베이스의 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [예제: 읽기 전용 파일의 온라인 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [예제: 데이터베이스의 증분 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [예제: 읽기-쓰기 파일의 온라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
## 참고 항목  
 [온라인 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [파일 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [RESTORE&#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
  