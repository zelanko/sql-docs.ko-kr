---
title: DML 트리거 삭제 또는 해제 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a82950fc3e6f2e905fb615c0302d80281322ac5c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43104645"
---
# <a name="delete-or-disable-dml-triggers"></a>DML 트리거 삭제 또는 해제
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 DML 트리거를 삭제하거나 비활성화하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **DML 트리거를 삭제하거나 비활성화하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
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
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣습니다. [트리거를 만들려면](../../t-sql/statements/create-trigger-transact-sql.md) CREATE TRIGGER `Sales.bonus_reminder` 문을 실행합니다. 트리거를 삭제하려면 [DROP TRIGGER](../../t-sql/statements/drop-trigger-transact-sql.md) 문을 실행합니다.  
  
```sql  
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
  
```sql  
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
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣습니다. [트리거를 만들려면](../../t-sql/statements/create-trigger-transact-sql.md) CREATE TRIGGER `Sales.bonus_reminder` 문을 실행합니다. 트리거를 비활성화하거나 활성화려면 [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md) 및 [ENABLE TRIGGER](../../t-sql/statements/enable-trigger-transact-sql.md) 문을 각각 실행합니다.  
  
```sql  
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
  
```sql  
--Disable the trigger.  
USE AdventureWorks2012;  
GO  
DISABLE TRIGGER Sales.bonus_reminder ON Sales.SalesPersonQuotaHistory;  
GO  
  
```  
  
```sql  
--Enable the trigger.  
USE AdventureWorks2012;  
GO  
ENABLE TRIGGER Sales.bonus_reminder ON Sales.SalesPersonQuotaHistory;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [DML 트리거에 대한 정보 가져오기](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sys.triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
  
