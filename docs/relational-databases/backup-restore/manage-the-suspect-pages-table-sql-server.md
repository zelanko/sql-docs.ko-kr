---
title: Suspect_pages 테이블 관리(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- 824 (Database Engine error)
- restoring pages [SQL Server]
- pages [SQL Server], suspect
- pages [SQL Server], restoring
- suspect_pages system table
- suspect pages [SQL Server]
- restoring [SQL Server], pages
ms.assetid: f394d4bc-1518-4e61-97fc-bf184d972e2b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 053ea3fdc7ad56ef6b6c9c9992506cf07623cb5e
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67584017"
---
# <a name="manage-the-suspectpages-table-sql-server"></a>suspect_pages 테이블 관리(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] suspect_pages [!INCLUDE[tsql](../../includes/tsql-md.md)]테이블을 관리하는 방법에 대해 설명합니다. 주의 대상 페이지에 대한 정보를 유지 관리하는 데 사용되는 **suspect_pages** 테이블은 복원이 필요한지 여부를 결정하는 데 사용됩니다. [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) 테이블은 [msdb 데이터베이스](../../relational-databases/databases/msdb-database.md)에 상주합니다.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서 데이터 페이지를 읽으려고 할 때 다음 오류 중 하나가 발생하면 페이지가 "주의 대상"으로 간주됩니다.  
  
-   디스크 오류(특정 하드웨어 오류)와 같이 운영 체제에서 실행되는 CRC(순환 중복 검사)로 인해 발생하는 823 오류  
  
-   조각난 페이지(논리적 오류)와 같은 824 오류  
  
 모든 주의 대상 페이지의 페이지 ID는 **suspect_pages** 테이블에 기록됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 다음과 같은 정상적인 처리 중에 발생하는 모든 주의 대상 페이지를 기록합니다.  
  
-   쿼리에서 페이지를 읽어야 하는 경우  
  
-   DBCC CHECKDB 작업이 수행 중인 경우  
  
-   백업 작업이 수행 중인 경우  
  
 또한 복원 작업, DBCC 복구 작업 또는 데이터베이스 삭제 작업 동안 필요한 경우 **suspect_pages** 테이블이 업데이트됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 suspect_pages 테이블을 관리합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   **suspect_pages 테이블에 기록되는 오류**  
  
     **suspect_pages** 테이블은 824 오류가 발생하여 실패한 페이지당 하나의 행을 포함합니다(최대 1,000개 행까지). 다음 표에서는 **suspect_pages** 테이블의 **event_type** 열에 기록되는 오류를 보여 줍니다.  
  
    |오류 설명|**event_type** 값|  
    |-----------------------|---------------------------|  
    |운영 체제 CRC 오류로 인해 발생하는 823 오류 또는 잘못된 체크섬이나 조각난 페이지 이외의 824 오류(예: 잘못된 페이지 ID)|1|  
    |잘못된 체크섬|2|  
    |조각난 페이지|3|  
    |복원됨(페이지가 잘못된 것으로 표시된 후 복원됨)|4|  
    |복구됨(DBCC가 페이지를 복구함)|5|  
    |DBCC에 의해 할당 취소됨|7|  
  
     또한 **suspect_pages** 테이블에서 일시적인 오류를 기록합니다.  일시적인 오류의 원인으로는 I/O 오류(예: 케이블 연결 끊김) 또는 일시적으로 반복 체크섬 테스트에 실패한 페이지 등이 있습니다.  
  
-   **데이터베이스 엔진의 suspect_pages 테이블 업데이트 방법**  
  
     [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 **suspect_pages** 테이블에 대해 다음 동작을 수행합니다.  
  
    -   테이블이 꽉 차지 않았다면 824 오류가 발생할 때마다 업데이트되어 오류 발생이 표시되고 오류 카운터가 증가합니다. 페이지를 복구, 복원 또는 할당 취소하여 수정한 후에도 오류가 있으면 **number_of_errors** 수가 증가하고 해당 **last_update** 열이 업데이트됩니다.  
  
    -   나열된 페이지를 복원 또는 복구 작업으로 수정하면 **suspect_pages** 행이 업데이트되어 페이지가 복구(**event_type** = 5) 또는 복원(**event_type** = 4)되었음을 나타냅니다.  
  
    -   DBCC Check를 실행하면 오류가 없는 페이지는 복구(**event_type** = 5) 또는 할당 취소(**event_type** = 7)된 것으로 표시됩니다.  
  
-   **suspect_pages 테이블의 자동 업데이트**  
  
     데이터 파일에서 페이지를 읽으려는 시도가 다음 이유 중 하나로 실패하면 데이터베이스 미러링 파트너 또는 Always On 가용성 복제본이 **suspect_pages** 테이블을 업데이트합니다.  
  
    -   운영 체제 CRC 오류로 인해 발생하는 823 오류  
  
    -   824 오류(조각난 페이지와 같은 논리적 손상)  
  
     다음 동작을 수행하면 **suspect_pages** 테이블에서 행이 자동으로 업데이트됩니다.  
  
    -   DBCC CHECKDB REPAIR_ALLOW_DATA_LOSS는 **suspect_pages** 테이블을 업데이트하여 할당 취소되었거나 복구된 각 페이지를 표시합니다.  
  
    -   전체, 파일 또는 페이지 복원을 수행하면 페이지 항목이 복원된 것으로 표시됩니다.  
  
     다음 동작을 수행하면 **suspect_pages** 테이블에서 행이 자동으로 삭제됩니다.  
  
    -   ALTER DATABASE REMOVE FILE  
  
    -   DROP DATABASE  
  
-   **데이터베이스 관리자의 유지 관리 역할**  
  
     데이터베이스 관리자는 주로 오래된 행을 삭제함으로써 테이블을 관리할 책임이 있습니다. **suspect_pages** 테이블은 크기에 제한이 있으며 모두 채워지면 더 이상 새로운 오류가 기록되지 않습니다. 이 테이블이 꽉 차지 않게 하려면 데이터베이스 관리자나 시스템 관리자가 이 테이블에서 행을 삭제하여 오래된 항목을 수동으로 지워야 합니다. 따라서 **event_type** 이 복원됨 또는 복구됨인 행이나 **last_update** 값이 오래된 행을 주기적으로 삭제하거나 보관하는 것이 좋습니다.  
  
     suspect_pages 테이블에서 작업을 모니터링하기 위해 [Database Suspect Data Page 이벤트 클래스](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)를 사용할 수 있습니다. 일시적인 오류로 인해 행이 **suspect_pages** 테이블에 추가되기도 합니다. 그러나 많은 행이 이 테이블에 추가되는 경우 I/O 하위 시스템에 문제가 있을 수도 있습니다. 이 테이블에 추가되는 행 수가 갑자기 증가하는 경우에는 I/O 하위 시스템에 발생한 문제가 있는지 조사해 보는 것이 좋습니다.  
  
     데이터베이스 관리자는 또한 레코드를 삽입하거나 업데이트할 수 있습니다. 예를 들어 데이터베이스 관리자가 특정 주의 대상 페이지가 존재함을 알고 있지만 잠시 동안 해당 레코드를 보존하려는 경우 행 업데이트가 유용할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 **msdb** 에 대한 액세스 권한이 있는 사용자는 **suspect_pages** 테이블의 데이터를 읽을 수 있습니다. suspect_pages 테이블에 대한 UPDATE 권한이 있는 사용자는 레코드를 업데이트할 수 있습니다. **msdb** 의 **db_owner** 고정 데이터베이스 역할 또는 **sysadmin** 고정 서버 역할의 멤버는 레코드를 삽입, 업데이트 및 삭제할 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-manage-the-suspectpages-table"></a>suspect_pages 테이블을 관리하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결하고 해당 인스턴스를 확장한 다음 **데이터베이스**를 확장합니다.  
  
2.  **시스템 데이터베이스**, **msdb**, **테이블**및 **시스템 테이블**을 차례로 확장합니다.  
  
3.  **dbo.suspect_pages** 를 확장하고 **상위 200개 행 편집**을 마우스 오른쪽 단추로 클릭합니다.  
  
4.  쿼리 창에서 원하는 행을 편집, 업데이트 또는 삭제합니다.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-manage-the-suspectpages-table"></a>suspect_pages 테이블을 관리하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 `suspect_pages` 테이블에서 일부 행을 삭제합니다.  
  
```  
-- Delete restored, repaired, or deallocated pages.  
DELETE FROM msdb..suspect_pages  
   WHERE (event_type = 4 OR event_type = 5 OR event_type = 7);  
GO  
  
```  
  
 이 예에서는 `suspect_pages` 테이블에 있는 잘못된 페이지를 반환합니다.  
  
```  
-- Select nonspecific 824, bad checksum, and torn page errors.  
SELECT * FROM msdb..suspect_pages  
   WHERE (event_type = 1 OR event_type = 2 OR event_type = 3);  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
 [페이지 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [suspect_pages&#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
    
   
  
  



