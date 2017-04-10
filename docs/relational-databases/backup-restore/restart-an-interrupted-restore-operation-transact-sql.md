---
title: "중단된 복원 작업 다시 시작(Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "중단된 복원 작업"
  - "데이터베이스 복원 [SQL Server], 중단된 작업 다시 시작"
  - "백업 후에 변경된 옵션 다시 설정"
  - "데이터베이스 복원 [SQL Server], 중단된 작업 다시 시작"
  - "중단된 복원 작업 다시 시작"
  - "중단된 작업 복원 [SQL Server]"
ms.assetid: 6413a07d-fd90-448d-8f29-12c5a1972618
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# 중단된 복원 작업 다시 시작(Transact-SQL)
  이 항목에서는 인터럽트된 복원 작업을 다시 시작하는 방법에 대해 설명합니다.  
  
### 중단된 복원 작업을 다시 시작하려면  
  
1.  인터럽트된 RESTORE 문을 다시 실행합니다. 이때 다음을 지정합니다.  
  
    -   원래 RESTORE 문에 사용한 것과 동일한 절  
  
    -   RESTART 절  
  
## 예제  
 다음은 중단된 복원 작업을 다시 시작하는 예제입니다.  
  
```tsql  
-- Restore a full database backup of the AdventureWorks database.  
RESTORE DATABASE AdventureWorks  
   FROM DISK = 'C:\AdventureWorks.bck'  
GO  
-- The restore operation halted prematurely.  
-- Repeat the original RESTORE statement specifying WITH RESTART.  
RESTORE DATABASE AdventureWorks   
   FROM DISK = 'C:\AdventureWorks.bck'  
   WITH RESTART  
GO  
```  
  
## 참고 항목  
 [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [RESTORE&#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
  