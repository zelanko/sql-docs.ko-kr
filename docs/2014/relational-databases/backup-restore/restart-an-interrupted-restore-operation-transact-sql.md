---
title: 중단된 복원 작업 다시 시작(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interrupted restore operation
- restoring databases [SQL Server], restarting interrupted operation
- resetting options changed after backup
- database restores [SQL Server], restarting interrupted operation
- restarting interrupted restore operation
- restoring interrupted operation [SQL Server]
ms.assetid: 6413a07d-fd90-448d-8f29-12c5a1972618
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 65eb8e196b016bf3ae0595d7d0de87d67f67ace6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092869"
---
# <a name="restart-an-interrupted-restore-operation-transact-sql"></a>중단된 복원 작업 다시 시작(Transact-SQL)
  이 항목에서는 인터럽트된 복원 작업을 다시 시작하는 방법에 대해 설명합니다.  
  
### <a name="to-restart-an-interrupted-restore-operation"></a>중단된 복원 작업을 다시 시작하려면  
  
1.  인터럽트된 RESTORE 문을 다시 실행합니다. 이때 다음을 지정합니다.  
  
    -   원래 RESTORE 문에 사용한 것과 동일한 절  
  
    -   RESTART 절  
  
## <a name="example"></a>예제  
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
  
## <a name="see-also"></a>관련 항목  
 [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](complete-database-restores-full-recovery-model.md)   
 [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](complete-database-restores-simple-recovery-model.md)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
