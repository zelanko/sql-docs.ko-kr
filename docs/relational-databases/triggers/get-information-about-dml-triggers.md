---
title: "DML 트리거에 대한 정보 가져오기 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- metadata [SQL Server], triggers
- viewing DML triggers
- DML triggers, metadata
- displaying DML triggers
- status information [SQL Server], triggers
- DML triggers, viewing
ms.assetid: 37574aac-181d-4aca-a2cc-8abff64237dc
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0cafdf4bc0fb8fcc9fdb8465b77f8c5dc757698
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="get-information-about-dml-triggers"></a>DML 트리거에 대한 정보 가져오기
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 DML 트리거에 대한 정보를 얻는 방법에 대해 설명합니다. 이 정보에는 테이블에 있는 트리거의 유형, 이름, 소유자 및 작성 또는 수정 날짜가 포함될 수 있습니다. 트리거를 만들었을 때 암호화하지 않은 경우 트리거의 정의를 얻을 수 있습니다. 이 정의를 사용하여 테이블에 정의된 트리거가 해당 테이블에 어떠한 영향을 주는지를 이해할 수 있습니다. 또한 특정 트리거가 사용하는 개체를 찾을 수 있습니다. 이 정보를 사용하면 데이터베이스에서 변경되거나 삭제될 때 트리거에 영향을 주는 개체를 식별할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **DML 트리거에 대한 정보를 얻으려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 **sys.sql.modules**, **sys.object**, **sys.triggers**, **sys.events**, **sys.trigger_events**  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
 OBJECT_DEFINITION, OBJECTPROPERTY, **sp_helptext**  
 **public** 역할의 멤버 자격이 필요합니다. 개체 소유자나 ALTER, CONTROL, TAKE OWNERSHIP 또는 VIEW DEFINITION 권한 중 하나를 부여받은 사람은 사용자 개체의 정의를 볼 수 있습니다. 이 권한은 **db_owner**, **db_ddladmin**및 **db_securityadmin** 고정 데이터베이스 역할의 멤버가 암시적으로 보유합니다.  
  
 **sys.sql_expression_dependencies**  
 데이터베이스에 대한 VIEW DEFINITION 권한과 데이터베이스의 **sys.sql_expression_dependencies** 에 대한 SELECT 권한이 필요합니다. 기본적으로 SELECT 권한은 **db_owner** 고정 데이터베이스 역할의 멤버에게만 부여됩니다. SELECT와 VIEW DEFINITION 권한을 다른 사용자에게 부여하면 피부여자는 데이터베이스의 모든 종속성을 볼 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-the-definition-of-a-dml-trigger"></a>DML 트리거의 정의를 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  원하는 데이터베이스를 확장하고 **테이블**을 확장한 다음 정의를 볼 트리거가 포함된 테이블을 확장합니다.  
  
3.  **트리거**를 확장하고 원하는 트리거를 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다. DML 트리거의 정의가 쿼리 창에 나타납니다.  
  
#### <a name="to-view-the-dependencies-of-a-dml-trigger"></a>DML 트리거의 종속성을 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  원하는 데이터베이스를 확장하고 **테이블**을 확장한 다음 보려는 트리거와 해당 종속성이 포함된 테이블을 확장합니다.  
  
3.  **트리거**를 확장하고 원하는 트리거를 마우스 오른쪽 단추로 클릭한 다음 **종속성 보기**를 클릭합니다.  
  
4.  **개체 종속성** 창에서 DML 트리거에 종속되는 개체를 보려면 **\<DML 트리거 이름>에 종속된 개체**를 선택합니다. 개체가 **종속성** 영역에 나타납니다.  
  
     DML이 종속되는 개체를 보려면 **\<DML 트리거 이름>이(가) 종속된 개체**를 선택합니다. 개체가 **종속성** 영역에 나타납니다. 각 노드를 확장하여 모든 개체를 표시합니다.  
  
5.  **종속성** 영역에 나타나는 개체에 대한 정보를 얻으려면 개체를 클릭합니다. **선택한 개체** 필드에서 **이름**, **유형**및 **종속성 유형** 상자에 정보가 제공됩니다.  
  
6.  **개체 종속성** 창을 닫으려면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-the-definition-of-a-dml-trigger"></a>DML 트리거의 정의를 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예 중 하나를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 각 예에서는 `iuPerson` 트리거의 정의를 보는 방법을 보여 줍니다.  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT definition   
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID(N'Person.iuPerson');   
GO  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'Person.iuPerson')) AS ObjectDefinition;   
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
EXEC sp_helptext 'Person.iuPerson'  
GO  
  
```  
  
#### <a name="to-view-the-dependencies-of-a-dml-trigger"></a>DML 트리거의 종속성을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예 중 하나를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 각 예에서는 `iuPerson` 트리거의 종속성을 보는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;   
GO  
SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc, referenced_class_desc,   
    referenced_server_name, referenced_database_name, referenced_schema_name,   
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,   
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referencing_id = OBJECT_ID(N'Person.iuPerson');   
GO  
  
```  
  
#### <a name="to-view-information-about-dml-triggers-in-the-database"></a>데이터베이스의 DML 트리거에 대한 정보를 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예 중 하나를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 각 예에서는 데이터베이스에서 DML 트리거(`TR`)에 대한 정보를 보는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;   
GO  
SELECT  name, parent_id, create_date, modify_date, is_instead_of_trigger  
FROM sys.triggers  
WHERE type = 'TR';   
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT  name, object_id, schema_id, parent_object_id, type_desc, create_date, modify_date, is_published  
FROM sys.objects  
WHERE type = 'TR';   
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT OBJECTPROPERTY(OBJECT_ID(N'Person.iuPerson'), 'ExecIsInsteadOfTrigger');   
GO  
  
```  
  
#### <a name="to-view-information-about-events-that-fire-a-dml-trigger"></a>DML 트리거를 실행하는 이벤트에 대한 정보를 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예 중 하나를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 각 예에서는 `iuPerson` 트리거를 실행하는 이벤트를 보는 방법을 보여 줍니다.  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT object_id, type, type_desc, is_trigger_event, event_group_type, event_group_type_desc   
FROM sys.events  
WHERE object_id = OBJECT_ID('Person.iuPerson');   
GO  
```  
  
```tsql  
USE AdventureWorks2012;   
GO   
SELECT object_id, type,is_first, is_last  
FROM sys.trigger_events  
WHERE object_id = OBJECT_ID('Person.iuPerson');   
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
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
 [OBJECTPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [OBJECT_DEFINITION&#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)  
  
  
