---
title: '데이터베이스 복원: 실패 지점 - 전체 복구'
description: 이 문서에서는 전체 복구 모델 또는 대량 로그된 복구 모델을 사용하는 데이터베이스의 실패 지점으로 SQL Server 데이터베이스를 복원하는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- point of failure [SQL Server]
- restoring databases [SQL Server], point of failure
- database restores [SQL Server], point of failure
ms.assetid: 04106e18-bbf7-4a5e-a2e1-3d65319814d5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e63d8c84b455fbcf991485486bb7bb197032827a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737713"
---
# <a name="restore-database-to-point-of-failure---full-recovery"></a>실패 지점으로 데이터베이스 복원 - 전체 복구
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 실패한 지점으로 복원하는 방법에 대해 설명합니다. 이 항목은 전체 복구 모델 또는 대량 로그 복구 모델을 사용하는 데이터베이스에만 해당됩니다.  
  
### <a name="to-restore-to-the-point-of-failure"></a>실패한 지점으로 복원하려면  
  
1.  다음의 기본 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 문을 실행하여 비상 로그를 백업합니다.  
  
    ```  
    BACKUP LOG <database_name> TO <backup_device>   
       WITH NORECOVERY, NO_TRUNCATE;  
    ```  
  
2.  다음의 기본 [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md) 문을 실행하여 전체 데이터베이스 백업을 복원합니다.  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
3.  필요에 따라 다음의 기본 RESTORE DATABASE 문을 실행하여 차등 데이터베이스 백업을 복원합니다.  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
4.  RESTORE LOG 문에 WITH NORECOVERY를 지정하여 1단계에서 만든 비상 로그 백업을 포함하는 각 트랜잭션 로그를 적용합니다.  
  
    ```  
    RESTORE LOG <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
5.  다음의 RESTORE DATABASE 문을 실행하여 데이터베이스를 복구합니다.  

    ```  
    RESTORE DATABASE <database_name>   
       WITH RECOVERY;  
    ```  
  
## <a name="example"></a>예제  
 예를 실행하려면 우선 다음 준비를 완료해야 합니다.  
  
1.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 기본 복구 모델은 단순 복구 모델입니다. 이 복구 모델에서는 실패한 지점에 대한 복원을 지원하지 않으므로 다음의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ALTER DATABASE [문을 실행하여 전체 복구 모델을 사용하도록](../../t-sql/statements/alter-database-transact-sql.md) 를 설정합니다.  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
    ```  
  
2.  다음 BACKUP 문을 사용하여 데이터베이스의 전체 데이터베이스 백업을 만듭니다.  
  
    ```  
    BACKUP DATABASE AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Data.bck';  
    ```  
  
3.  일상적인 로그 백업 생성:  
  
    ```  
    BACKUP LOG AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Log.bck';  
    ```  
  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 비상 로그 백업을 만든 후 이전에 만들어진 백업을 복원합니다. 이 단계에서는 로그 디스크에 액세스할 수 있다고 가정합니다.  
  
 우선 이 예에서는 활성 로그를 캡처하는 데이터베이스의 비상 로그 백업을 만들고 데이터베이스를 복원 중인 상태로 둡니다. 그런 다음 데이터베이스 백업을 복원하고 이전에 만든 일상적인 로그 백업을 적용한 후 비상 로그 백업을 적용합니다. 끝으로 별도의 단계로 데이터베이스를 복구합니다.  
  
> [!NOTE]  
>  기본 동작은 최종 백업을 복원하는 문의 일부로 데이터베이스를 복구하는 것입니다.  
  
```  
/* Example of restoring a to the point of failure */  
-- Step 1: Create a tail-log backup by using WITH NORECOVERY.  
BACKUP LOG AdventureWorks2012  
   TO DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 2: Restore the full database backup.  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Data.bck'  
   WITH NORECOVERY;  
GO  
-- Step 3: Restore the first transaction log backup.  
RESTORE LOG AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 4: Restore the tail-log backup.  
RESTORE LOG AdventureWorks2012  
   FROM  DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 5: Recover the database.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
