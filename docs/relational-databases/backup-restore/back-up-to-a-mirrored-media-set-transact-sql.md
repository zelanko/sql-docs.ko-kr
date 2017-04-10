---
title: "미러된 미디어 세트에 백업(TRANSACT-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# 미러된 미디어 세트에 백업(TRANSACT-SQL)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 백업할 때 [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) 문을 사용하여 미러된 미디어 세트를 지정하는 방법에 대해 설명합니다. BACKUP 문에서 TO 절에 첫 번째 미러를 지정합니다. 그런 다음 해당 MIRROR TO 절에 각 미러를 지정합니다. TO절과 MIRROR TO 절은 같은 개수와 유형의 백업 장치를 지정해야 합니다.  
  
## 예제  
 다음 예에서는 이전 그림에 표시된 미러된 미디어 세트를 만들고 두 미러 모두에 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 백업합니다.  
  
```  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
    FORMAT,  
    MEDIANAME = 'AdventureWorks2012Set1';  
GO  
```  
  
## 관련 태스크  
 **미러된 백업에서 복원하려면**  
  
-   [RESTORE&#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
## 참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [미러된 백업 미디어 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)  
  
  