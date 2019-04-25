---
title: DML 트리거 수정 또는 이름 바꾸기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- renaming triggers
- modifying triggers
- DML triggers, modifying
ms.assetid: c7317eec-c0e9-479e-a4a7-83b6b6c58d59
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 824ea1587955884f10a53579865d2029cc63eefc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62473224"
---
# <a name="modify-or-rename-dml-triggers"></a>DML 트리거 수정 또는 이름 바꾸기
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 DML 트리거를 수정하거나 이름을 바꾸는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **DML 트리거를 수정하거나 이름을 바꾸려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   트리거의 이름을 바꿀 때 트리거가 현재 데이터베이스에 있어야 하고 새 이름이 [식별자](../databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   트리거의 이름을 바꿀 때 [sp_rename](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql) 저장 프로시저를 사용하지 않는 것이 좋습니다. 개체 이름의 일부를 변경하면 스크립트나 저장 프로시저가 작동되지 않을 수 있습니다. 트리거의 이름을 변경해도 [sys.sql_modules](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql) 카탈로그 뷰의 definition 열에 있는 해당 개체 이름은 변경되지 않습니다. 대신 트리거를 삭제하고 다시 만드는 것이 좋습니다.  
  
-   DML 트리거가 참조하는 개체의 이름을 변경하면 트리거 텍스트에 새 개체 이름이 반영되도록 트리거를 수정해야 합니다. 따라서 개체 이름을 바꾸기 전에 먼저 개체의 종속성을 표시하여 영향을 받는 트리거가 있는지 확인해야 합니다.  
  
-   DML 트리거 정의를 암호화할 수도 있습니다.  
  
-   트리거의 종속성을 보려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 다음 함수와 카탈로그 뷰를 사용할 수 있습니다.  
  
    -   [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
    -   [sys.dm_sql_referenced_entities&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
    -   [sys.dm_sql_referencing_entities&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql)  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 DML 트리거를 변경하려면 트리거가 정의된 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-a-dml-trigger"></a>DML 트리거를 수정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  원하는 데이터베이스를 확장하고 **테이블**을 확장한 다음 수정할 트리거가 포함된 테이블을 확장합니다.  
  
3.  **트리거**를 확장하고 수정할 트리거를 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
4.  트리거를 수정한 다음 **실행**을 클릭합니다.  
  
#### <a name="to-rename-a-dml-trigger"></a>DML 트리거의 이름을 바꾸려면  
  
1.  이름을 바꿀[트리거를 삭제합니다](../triggers/dml-triggers.md) .  
  
2.  새 이름을 지정하여[트리거를 다시 만듭니다](../triggers/create-dml-triggers.md).  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-modify-a-trigger-using-alter-trigger"></a>ALTER TRIGGER를 사용하여 트리거를 수정하려면  
  
1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리에 붙여 넣습니다. 첫 번째 예를 실행하여 사용자가 `SalesPersonQuotaHistory` 테이블에 데이터를 추가 또는 변경하려고 시도하면 클라이언트로 사용자 정의 메시지를 인쇄하는 DML 트리거를 만듭니다. [ALTER TRIGGER](/sql/t-sql/statements/alter-trigger-transact-sql) 문을 실행하여 `INSERT` 작업에 대해서만 발생하도록 트리거를 수정합니다. 이 트리거는 테이블에 행을 삽입하거나 업데이트하는 사용자에게 `Compensation` 부서에도 해당 사실을 통지하도록 알려 줍니다.  
  
```sql  
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
USE AdventureWorks2012;  
GO  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
#### <a name="to-rename-a-trigger-using-drop-trigger-and-alter-trigger"></a>DROP TRIGGER 및 ALTER TRIGGER를 사용하여 트리거의 이름을 바꾸려면  
  
1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [DROP TRIGGER](/sql/t-sql/statements/drop-trigger-transact-sql) 및 [ALTER TRIGGER](/sql/t-sql/statements/alter-trigger-transact-sql) 문을 사용하여 `Sales.bonus_reminder` 트리거의 이름을 `Sales.bonus_reminder_2`로 바꿉니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder_2  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [CREATE TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DROP TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [ENABLE TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/enable-trigger-transact-sql)   
 [DISABLE TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/disable-trigger-transact-sql)   
 [EVENTDATA&#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)   
 [sp_rename&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql)   
 [ALTER TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [DML 트리거에 대한 정보 가져오기](../triggers/get-information-about-dml-triggers.md)   
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
  
  
