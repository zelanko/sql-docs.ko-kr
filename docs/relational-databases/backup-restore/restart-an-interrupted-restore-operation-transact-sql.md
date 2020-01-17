---
title: 중단된 복원 다시 시작(Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- interrupted restore operation
- restoring databases [SQL Server], restarting interrupted operation
- resetting options changed after backup
- database restores [SQL Server], restarting interrupted operation
- restarting interrupted restore operation
- restoring interrupted operation [SQL Server]
ms.assetid: 6413a07d-fd90-448d-8f29-12c5a1972618
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 49b2cd932ea40e2f45010785edcd033b8530d6bd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244358"
---
# <a name="restart-an-interrupted-restore-operation-transact-sql"></a>중단된 복원 작업 다시 시작(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 인터럽트된 복원 작업을 다시 시작하는 방법에 대해 설명합니다.  
  
### <a name="to-restart-an-interrupted-restore-operation"></a>중단된 복원 작업을 다시 시작하려면  
  
1.  인터럽트된 RESTORE 문을 다시 실행합니다. 이때 다음을 지정합니다.  
  
    -   원래 RESTORE 문에 사용한 것과 동일한 절  
  
    -   RESTART 절  
  
## <a name="example"></a>예제  
 다음은 중단된 복원 작업을 다시 시작하는 예제입니다.  
  
```sql  
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
  
## <a name="see-also"></a>참고 항목  
 [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
