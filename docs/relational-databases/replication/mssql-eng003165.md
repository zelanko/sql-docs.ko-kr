---
title: "MSSQL_ENG003165 | Microsoft 문서"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG003165 error
ms.assetid: 707d33dd-644e-4cc9-ac51-dddd49031530
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e30a1f4e1b16b9f4a6435125fe6311d6bffe0a77
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqleng003165"></a>MSSQL_ENG003165
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3165|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|데이터베이스 '%ls'이(가) 복원되었지만 복제가 복원/제거되는 동안 오류가 발생했습니다. 데이터베이스가 오프라인 상태로 남아 있습니다. SQL Server 온라인 설명서의 MSSQL_ENG003165 항목을 참조하십시오.|  
  
## <a name="explanation"></a>설명  
 이 오류는 복제된 데이터베이스의 백업을 복원하는 동안 문제가 발생하는 경우 발생합니다.  
  
-   백업을 수행한 데이터베이스와 서버로 해당 백업을 복원하는 경우 이 오류는 복제 설정을 제대로 복원하지 못했음을 나타냅니다.  
  
-   백업을 다른 데이터베이스나 서버로 복원하는 경우 이 오류는 복제 설정을 제대로 제거하지 못했음을 나타냅니다. 데이터베이스나 서버가 다른 경우에는 기본적으로 복제 설정이 제거됩니다.  
  
 이 오류의 원인은 복원된 데이터베이스와 복제 메타데이터 **msdb**, **master**또는 배포 데이터베이스가 포함된 하나 이상의 시스템 데이터베이스의 상태가 일치하지 않기 때문일 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 문제를 해결하려면 다음을 수행하십시오.  
  
1.  예를 들면 `ALTER DATABASE AdventureWorks SET ONLINE`과 같이 ALTER DATABASE를 실행하여 데이터베이스를 온라인 상태로 만듭니다. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요. 복제 설정을 유지하려면 2단계로 이동하고, 그렇지 않은 경우에는 3단계로 이동합니다.  
  
2.  [sp_restoredbreplication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-restoredbreplication-transact-sql.md)을 실행합니다. 이 저장 프로시저가 성공적으로 실행되면 복원이 완료됩니다. 성공적으로 실행되지 않으면 3단계로 이동합니다.  
  
3.  [sp_removedbreplication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 실행하여 모든 복제 설정을 제거합니다.  
  
     필요한 경우 복제를 다시 구성합니다. 복제 토폴로지를 권장 사항대로 스크립팅한 경우에는 스크립트를 사용하여 토폴로지를 다시 구성합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [복제된 데이터베이스 백업 및 복원](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
