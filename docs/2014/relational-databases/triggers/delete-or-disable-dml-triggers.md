---
title: DML 트리거 삭제 또는 해제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DML triggers, disabling
- removing DML triggers
- disabling DML triggers
- dropping DML triggers
- deleting DML triggers
- DML triggers, removing
ms.assetid: 0f97f953-33c5-4b26-afeb-db2a26ce38b4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8ed56b0d2c3ce14888f7856cadbcf1f1dc67a5ef
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52760695"
---
# <a name="delete-or-disable-dml-triggers"></a>DML 트리거 삭제 또는 해제
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 DML 트리거를 삭제하거나 비활성화하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **DML 트리거를 삭제하거나 비활성화하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   트리거를 삭제하면 현재 데이터베이스에서 트리거가 삭제됩니다. 트리거의 기반이 되는 테이블과 데이터는 영향을 받지 않습니다. 테이블을 삭제하면 테이블에 있는 트리거도 자동으로 삭제됩니다.  
  
-   트리거를 만들면 이 트리거는 기본적으로 활성화됩니다.  
  
-   트리거를 비활성화하면 트리거는 삭제되지 않고 현재 데이터베이스의 개체로 남아 있습니다. 그러나 해당 트리거가 프로그래밍된 INSERT, UPDATE 또는 DELETE 문이 실행될 때 트리거가 실행되지 않습니다. 트리거를 해제했다가 다시 설정할 수 있습니다. 트리거를 활성화하더라도 트리거를 다시 만드는 것은 아닙니다. 트리거는 원래 생성되었을 때와 동일하게 발생됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 DML 트리거를 삭제하려면 트리거가 정의된 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다.  
  
 DML 트리거를 비활성화하거나 활성화하려면 사용자에게 트리거가 만들어진 테이블 또는 뷰에 대한 ALTER 권한이 있어야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-dml-trigger"></a>DML 트리거를 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  원하는 데이터베이스를 확장하고 **테이블**을 확장한 다음 삭제할 트리거가 포함된 테이블을 확장합니다.  
  
3.  **트리거**를 확장하고 삭제할 트리거를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
4.  **개체 삭제** 대화 상자에서 삭제할 트리거를 확인한 다음 **확인**을 클릭합니다.  
  
#### <a name="to-disable-and-enable-a-dml-trigger"></a>DML 트리거를 비활성화하거나 활성화하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  원하는 데이터베이스를 확장하고 **테이블**을 확장한 다음 비활성화할 트리거가 포함된 테이블을 확장합니다.  
  
3.  **트리거**를 확장하고 비활성화할 트리거를 마우스 오른쪽 단추로 클릭한 다음 **사용 안 함**을 클릭합니다.  
  
4.  트리거를 활성화하려면 **사용**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-dml-trigger"></a>DML 트리거를 삭제하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣습니다. [트리거를 만들려면](/sql/t-sql/statements/create-trigger-transact-sql) CREATE TRIGGER `Sales.bonus_reminder` 문을 실행합니다. 트리거를 삭제하려면 [DROP TRIGGER](/sql/t-sql/statements/drop-trigger-transact-sql) 문을 실행합니다.  
  
```tsql  
--Create the trigger.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
```tsql  
--Delete the trigger.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('Sales.bonus_reminder', 'TR') IS NOT NULL  
   DROP TRIGGER Sales.bonus_reminder;  
GO  
  
```  
  
#### <a name="to-disable-and-enable-a-dml-trigger"></a>DML 트리거를 비활성화하거나 활성화하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣습니다. [트리거를 만들려면](/sql/t-sql/statements/create-trigger-transact-sql) CREATE TRIGGER `Sales.bonus_reminder` 문을 실행합니다. 트리거를 비활성화하거나 활성화려면 [DISABLE TRIGGER](/sql/t-sql/statements/disable-trigger-transact-sql) 및 [ENABLE TRIGGER](/sql/t-sql/statements/enable-trigger-transact-sql) 문을 각각 실행합니다.  
  
```tsql  
--Create the trigger.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
```tsql  
--Disable the trigger.  
USE AdventureWorks2012;  
GO  
DISABLE TRIGGER Sales.bonus_reminder ON Sales.SalesPersonQuotaHistory;  
GO  
  
```  
  
```tsql  
--Enable the trigger.  
USE AdventureWorks2012;  
GO  
ENABLE TRIGGER Sales.bonus_reminder ON Sales.SalesPersonQuotaHistory;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [ALTER TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DROP TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [ENABLE TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/enable-trigger-transact-sql)   
 [DISABLE TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/disable-trigger-transact-sql)   
 [EVENTDATA&#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)   
 [DML 트리거에 대한 정보 가져오기](dml-triggers.md)   
 [sp_help&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-transact-sql)   
 [sp_helptrigger&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptrigger-transact-sql)   
 [sys.triggers&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql)   
 [sys.trigger_events&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-trigger-events-transact-sql)   
 [sys.sql_modules&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)   
 [sys.assembly_modules&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)   
 [sys.server_triggers&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)   
 [sys.server_trigger_events&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)   
 [sys.server_sql_modules&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql)   
 [sys.server_assembly_modules&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)  
  
  
