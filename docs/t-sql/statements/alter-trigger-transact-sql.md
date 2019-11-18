---
title: ALTER TRIGGER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER TRIGGER
- ALTER_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, modifying
- triggers [SQL Server], modifying
- modifying triggers
- ALTER TRIGGER statement
- DML triggers, modifying
ms.assetid: 2a99c7c1-ac2f-4637-aa7c-3d1bf514e500
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5e8523831fd181c17bd8fcff1698d85f46c824e2
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983323"
---
# <a name="alter-trigger-transact-sql"></a>ALTER TRIGGER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  이전에 CREATE TRIGGER 문을 사용해 만든 DML, DDL 또는 LOGON 트리거의 정의를 수정합니다. 트리거는 CREATE TRIGGER를 사용하여 만듭니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문으로 직접 만들거나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR(공용 언어 런타임)에서 만들어지고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 업로드되는 어셈블리의 메서드로 만들 수 있습니다. ALTER TRIGGER 문에 사용되는 매개 변수에 대한 자세한 내용은 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  

ALTER TRIGGER schema_name.trigger_name   
ON  ( table | view )   
[ WITH <dml_trigger_option> [ ,...n ] ]  
 ( FOR | AFTER | INSTEAD OF )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
[ NOT FOR REPLICATION ]   
AS { sql_statement [ ; ] [ ...n ] | EXTERNAL NAME <method specifier>   
[ ; ] }   
  
<dml_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ <EXECUTE AS Clause> ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table 
-- (DML Trigger on memory-optimized tables)  

ALTER TRIGGER schema_name.trigger_name   
ON  ( table  )   
[ WITH <dml_trigger_option> [ ,...n ] ]  
 ( FOR | AFTER )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
AS { sql_statement [ ; ] [ ...n ] }   
  
<dml_trigger_option> ::=  
    [ NATIVE_COMPILATION ]  
    [ SCHEMABINDING ]  
    [ <EXECUTE AS Clause> ]  
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE, 
-- or UPDATE statement (DDL Trigger)  
  
ALTER TRIGGER trigger_name   
ON { DATABASE | ALL SERVER }   
[ WITH <ddl_trigger_option> [ ,...n ] ]  
{ FOR | AFTER } { event_type [ ,...n ] | event_group }   
AS { sql_statement [ ; ] | EXTERNAL NAME <method specifier>   
[ ; ] }  
}   
  
<ddl_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ <EXECUTE AS Clause> ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
-- Trigger on a LOGON event (Logon Trigger)  

ALTER TRIGGER trigger_name   
ON ALL SERVER   
[ WITH <logon_trigger_option> [ ,...n ] ]  
{ FOR| AFTER } LOGON   
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  
  [ ; ] }  
  
<logon_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
```  
  
```  
-- Azure SQL Database Syntax   
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)   
  
ALTER TRIGGER schema_name. trigger_name   
ON (table | view )   
 [ WITH <dml_trigger_option> [ ,...n ] ]   
 ( FOR | AFTER | INSTEAD OF )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
AS { sql_statement [ ; ] [...n ] }   
  
<dml_trigger_option> ::=   
    [ <EXECUTE AS Clause> ]   
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE, or UPDATE statement (DDL Trigger)   
  
ALTER TRIGGER trigger_name   
ON { DATABASE }   
 [ WITH <ddl_trigger_option> [ ,...n ] ]   
{ FOR | AFTER } { event_type [ ,...n ] | event_group }   
AS { sql_statement   
[ ; ] }  
}   
  
<ddl_trigger_option> ::=   
    [ <EXECUTE AS Clause> ]  
```  
  
## <a name="arguments"></a>인수  
 *schema_name*  
 DML 트리거가 속한 스키마의 이름입니다. DML 트리거는 트리거가 생성된 테이블 또는 뷰의 스키마로 한정됩니다. *schema**_name*은 DML 트리거 및 해당 테이블 또는 뷰가 기본 스키마에 속하는 경우에만 선택 사항입니다. *schema_name*은 DDL 또는 LOGON 트리거에 대해 지정될 수 없습니다.  
  
 *trigger_name*  
 수정할 기존 트리거입니다.  
  
 *table* | *view*  
 DML 트리거가 실행되는 테이블 또는 뷰입니다. 필요에 따라 테이블 또는 뷰의 정규화된 이름을 지정할 수 있습니다.  
  
 DATABASE  
 현재 데이터베이스에 DDL 트리거의 해당 범위를 적용합니다. 지정하면 현재 데이터베이스에서 *event_type* 또는 *event_group*이 발생할 때마다 트리거가 실행됩니다.  
  
 ALL SERVER  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 현재 서버에 DDL 또는 LOGON 트리거의 범위를 적용합니다. 지정하면 현재 서버의 어디에서든 *event_type* 또는 *event_group*이 발생할 때마다 트리거가 실행됩니다.  
  
 WITH ENCRYPTION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 ALTER TRIGGER 문의 텍스트가 포함된 sys.syscommentssys.sql_modules 항목을 암호화합니다. WITH ENCRYPTION을 사용하면 트리거가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제의 일부로 게시되지 않도록 방지할 수 있습니다. CLR 트리거에 대해서는 WITH ENCRYPTION을 지정할 수 없습니다.  
  
> [!NOTE]  
>  WITH ENCRYPTION 설정으로 트리거를 만든 경우 옵션의 설정 상태를 유지하기 위해서는 반드시 ALTER TRIGGER 문에 다시 설정을 포함시켜야 합니다.  
  
 EXECUTE AS  
 트리거가 실행되는 보안 컨텍스트를 지정합니다. 트리거가 참조하는 데이터베이스 개체에 대한 사용 권한의 유효성을 검사하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 사용하는 사용자 계정을 제어할 수 있도록 합니다.  
  
 자세한 내용은 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)을 참조하세요.  
  
 NATIVE_COMPILATION  
 트리거가 고유하게 컴파일되었음을 나타냅니다.  
  
 이 옵션은 메모리 최적화 테이블의 트리거에 필요합니다.  
  
 SCHEMABINDING  
 트리거에서 참조되는 테이블을 삭제 또는 변경할 수 없도록 보장합니다.  
  
 이 옵션은 메모리 최적화 테이블의 트리거에 필요하며 기존 테이블의 트리거에는 지원되지 않습니다.  
  
 AFTER  
 트리거를 시작하는 SQL 문이 성공적으로 실행된 후에만 트리거가 실행되도록 지정합니다. 또한 이 트리거가 실행되기 전에 모든 참조 연계 동작과 제약 조건 검사가 제대로 수행되어야 합니다.  
  
 FOR 키워드만 지정된 경우 AFTER가 기본값입니다.  
  
 DML AFTER 트리거는 테이블에만 정의될 수 있습니다.  
  
 INSTEAD OF  
 트리거를 시작하는 SQL 문 대신 DML 트리거가 실행되도록 지정합니다. 즉, 트리거를 시작하는 문의 동작을 재정의합니다. DDL 또는 LOGON 트리거에 대해서는 INSTEAD OF를 지정할 수 없습니다.  
  
 테이블이나 뷰에 대해 INSERT, UPDATE 또는 DELETE 문당 INSTEAD OF 트리거를 하나만 정의할 수 있습니다. 그러나 고유한 INSTEAD OF 트리거가 있는 각 뷰에 대해 뷰를 정의할 수 있습니다.  
  
 WITH CHECK OPTION을 사용하여 작성된 뷰에는 INSTEAD OF 트리거를 사용할 수 없습니다. WITH CHECK OPTION이 지정된 뷰에 INSTEAD OF 트리거를 추가하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류가 발생합니다. 사용자는 INSTEAD OF 트리거를 정의하기 전에 반드시 ALTER VIEW를 사용하여 해당 옵션을 제거해야 합니다.  
  
 { [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] } | { [INSERT ] [ , ] [ UPDATE ] }  
 현재 테이블 또는 뷰에 데이터 수정 문 실행을 시도할 경우 DML 트리거를 활성화하도록 지정합니다. 적어도 하나의 옵션을 지정해야 합니다. 순서에 상관없이 어떤 방법으로도 옵션을 조합할 수 있습니다. 둘 이상의 옵션을 지정한 경우에는 옵션을 쉼표로 분리하세요.  
  
 INSTEAD OF 트리거의 경우 ON DELETE 연계 동작을 지정하는 참조 관계가 있는 테이블에 대해서는 DELETE 옵션을 사용할 수 없습니다. 마찬가지로 연계 동작인 ON UPDATE를 지정하는 참조 관계가 있는 테이블에 대해서도 UPDATE 옵션이 허용되지 않습니다. 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
 *event_type*  
 실행된 후에 DDL 트리거가 실행되도록 하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 이벤트의 이름입니다. DDL 트리거에 유효한 이벤트는 [DDL 이벤트](../../relational-databases/triggers/ddl-events.md)에 나열되어 있습니다.  
  
 *event_group*  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 이벤트의 미리 정의된 그룹 이름입니다. *event_group*에 속한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 이벤트가 실행된 후에 DDL 트리거가 실행됩니다. DDL 트리거에 유효한 이벤트 그룹은 [DDL 이벤트 그룹](../../relational-databases/triggers/ddl-event-groups.md)에 나열되어 있습니다. ALTER TRIGGER 실행이 끝난 후, *event_group*은 처리할 이벤트 유형을 sys.trigger_events 카탈로그 뷰에 추가하여 매크로로 작동합니다.  
  
 NOT FOR REPLICATION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 복제 에이전트가 트리거와 연관된 테이블을 수정할 때 트리거를 실행할 수 없음을 나타냅니다.  
  
 *sql_statement*  
 트리거 조건 및 동작입니다.  
  
 메모리 최적화 테이블의 트리거의 경우, 최상위 수준에서 허용되는 *sql_statement*는 ATOMIC 블록뿐입니다. ATOMIC 블록 내에서 허용되는 T-SQL은 네이티브 프로시저 내에서 허용되는 T-SQL로 제한됩니다.  
  
 EXTERNAL NAME \<method_specifier>  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 트리거와 바인딩할 어셈블리의 메서드를 지정합니다. 이 메서드는 인수가 없어야 하며 void를 반환해야 합니다. *class_name*은 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자여야 하며 어셈블리 표시 유형이 있는 어셈블리의 클래스로 존재해야 합니다. 클래스는 중첩 클래스일 수 없습니다.  
  
## <a name="remarks"></a>Remarks  
 ALTER TRIGGER에 대한 자세한 내용은 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)의 설명 부분을 참조하세요.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 EXTERNAL_NAME 및 ON_ALL_SERVER 옵션을 사용할 수 없습니다.  
  
## <a name="dml-triggers"></a>DML 트리거  
 ALTER TRIGGER는 테이블과 뷰의 INSTEAD OF 트리거를 통해 수동으로 업데이트할 수 있는 뷰를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 모든 종류의 트리거(AFTER, INSTEAD-OF)에 대해 동일한 방식으로 ALTER TRIGGER를 적용합니다.  
  
 sp_settriggerorder를 사용하여 테이블에서 실행할 처음 및 마지막 AFTER 트리거를 지정할 수 있습니다. 하나의 테이블에는 처음 및 마지막 AFTER 트리거를 하나씩만 지정할 수 있습니다. 동일한 테이블에 다른 AFTER 트리거가 있는 경우 임의로 실행됩니다.  
  
 ALTER TRIGGER 문에서 첫 번째 트리거나 마지막 트리거를 변경하면 수정된 트리거에 설정된 첫 번째 또는 마지막 특성은 삭제되며 sp_settriggerorder를 사용하여 순서 값을 다시 설정해야 합니다.  
  
 AFTER 트리거는 트리거를 시작하는 SQL 문이 성공적으로 실행된 후에만 실행됩니다. 또한 업데이트 또는 삭제된 개체와 관련된 모든 참조 연계 동작과 제약 조건 확인이 성공적으로 수행되어야 합니다. AFTER 트리거 작업은 트리거를 시작하는 문의 효과와 문에 의해 발생하는 모든 참조 연계 UPDATE 및 DELETE 동작의 효과를 확인합니다.  
  
 부모 테이블의 DELETE 시 CASCADE 결과가 자식 테이블이나 참조하는 테이블에 대한 DELETE 동작이며 자식 테이블에 DELETE 시 INSTEAD OF 트리거가 정의되어 있으면 트리거가 무시되고 DELETE 작업이 실행됩니다.  
  
## <a name="ddl-triggers"></a>DDL 트리거  
 DDL 트리거는 DML 트리거와 달리 스키마로 범위가 한정되지 않습니다. 따라서 DDL 트리거에 대한 메타데이터를 쿼리할 때는 OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY 및 OBJECTPROPERTY(EX)를 사용할 수 없습니다. 대신 카탈로그 뷰를 사용하세요. 자세한 내용은 [DDL 트리거에 대한 정보 가져오기](../../relational-databases/triggers/get-information-about-ddl-triggers.md)를 참조하세요.  
  
## <a name="logon-triggers"></a>LOGON 트리거  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서는 LOGON 이벤트에 대한 트리거를 지원하지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 DML 트리거를 변경하려면 트리거가 정의된 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다.  
  
 서버 범위(ON ALL SERVER)로 정의된 DDL 트리거 또는 LOGON 트리거를 변경하려면 해당 서버에 대한 CONTROL SERVER 권한이 필요합니다. 데이터베이스 범위(ON DATABASE)로 정의된 DDL 트리거를 변경하려면 현재 데이터베이스에 대한 ALTER ANY DATABASE DDL TRIGGER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 사용자가 `SalesPersonQuotaHistory` 테이블에 데이터를 추가 또는 변경하려고 시도하면 클라이언트에 사용자 정의 메시지를 인쇄하는 AdventureWorks 2012 데이터베이스의 DML 트리거를 만드는 방법을 보여 줍니다. 그런 다음 `ALTER TRIGGER` 작업에만 해당 트리거를 적용하도록 `INSERT`를 사용하여 트리거를 수정합니다. 이 트리거는 테이블에 행을 삽입하거나 업데이트하는 사용자에게 `Compensation` 부서에도 해당 사실을 통지하도록 알려 줍니다.  
  
```  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  

-- Now, change the trigger.  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [DROP TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_helptrigger&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [저장 프로시저 만들기](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [트랜잭션](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [DML 트리거에 대한 정보 가져오기](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [DDL 트리거에 대한 정보 가져오기](../../relational-databases/triggers/get-information-about-ddl-triggers.md)   
 [sys.triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)   
 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
