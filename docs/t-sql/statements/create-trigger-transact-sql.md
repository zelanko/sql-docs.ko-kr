---
title: CREATE TRIGGER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: mathoma
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE TRIGGER
- TRIGGER
- CREATE_TRIGGER_TSQL
- TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- recursive DML triggers [SQL Server]
- CREATE TRIGGER statement
- multiple triggers
- deferred name resolution, DML triggers
- DML triggers, creating
- nested triggers
- server-scoped triggers
- DDL triggers, creating
- triggers [SQL Server], creating
- database-scoped triggers [SQL Server]
ms.assetid: edeced03-decd-44c3-8c74-2c02f801d3e7
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2ee63ff261df82926fd67f5014c09f894160d14e
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53213742"
---
# <a name="create-trigger-transact-sql"></a>CREATE TRIGGER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

> [!div class="nextstepaction"]
> [SQL Server 문서 개선에 참여해주세요.](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

DML, DDL 또는 LOGON 트리거를 만듭니다. 트리거는 데이터베이스 서버에서 이벤트가 발생하면 자동으로 실행되는 특수한 종류의 저장 프로시저입니다. DML 트리거는 DML(데이터 조작 언어) 이벤트를 통해 데이터를 수정하려는 경우에 실행됩니다. DML 이벤트는 테이블이나 뷰에 대한 INSERT, UPDATE 또는 DELETE 문입니다. 테이블 행이 영향을 받는지 여부에 관계없이 유효한 이벤트가 발생할 때 이러한 트리거가 발생합니다. 자세한 내용은 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)을 참조하세요.  
  
 DDL 트리거는 다양한 DDL(데이터 정의 언어) 이벤트에 대한 응답으로 실행됩니다. 이러한 이벤트는 주로 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE, ALTER 및 DROP 문, DDL과 같은 작업을 수행하는 특정 시스템 저장 프로시저에 해당합니다. LOGON 트리거는 사용자 세션이 설정될 때 발생하는 LOGON 이벤트에 대한 응답으로 실행됩니다. 트리거는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문으로 직접 만들거나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR(공용 언어 런타임)에서 만들어지고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 업로드되는 어셈블리의 메서드로 만들 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하면 특정 문에 대한 여러 트리거를 만들 수 있습니다.  
  
> [!IMPORTANT]  
>  사용 권한 수준을 높이고 트리거를 실행하더라도 트리거 내의 악성 코드가 실행될 수 있습니다. 이런 위협을 완화하는 방법에 대한 자세한 내용 [트리거 보안 관리](../../relational-databases/triggers/manage-trigger-security.md)를 참조하세요.  
  
> [!NOTE]  
>  이 항목에서는 .NET Framework CLR을 SQL Server에 통합하는 방법에 대해 설명합니다. Azure SQL Database에는 CLR 통합이 적용되지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
``` 
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table | view }   
[ WITH <dml_trigger_option> [ ,...n ] ]  
{ FOR | AFTER | INSTEAD OF }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
[ WITH APPEND ]  
[ NOT FOR REPLICATION ]   
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME <method specifier [ ; ] > }  
  
<dml_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
```  
  
``` 
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a 
-- table (DML Trigger on memory-optimized tables)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table }   
[ WITH <dml_trigger_option> [ ,...n ] ]  
{ FOR | AFTER }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
AS { sql_statement  [ ; ] [ ,...n ] }  
  
<dml_trigger_option> ::=  
    [ NATIVE_COMPILATION ]  
    [ SCHEMABINDING ]  
    [ EXECUTE AS Clause ]  
  
```  
  
``` 
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, 
-- REVOKE or UPDATE statement (DDL Trigger)  
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON { ALL SERVER | DATABASE }   
[ WITH <ddl_trigger_option> [ ,...n ] ]  
{ FOR | AFTER } { event_type | event_group } [ ,...n ]  
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  [ ; ] }  
  
<ddl_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Trigger on a LOGON event (Logon Trigger)  
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON ALL SERVER   
[ WITH <logon_trigger_option> [ ,...n ] ]  
{ FOR| AFTER } LOGON    
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  [ ; ] }  
  
<logon_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
```  
  
## <a name="syntax"></a>구문  
  
``` 
-- Azure SQL Database Syntax   
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table | view }   
 [ WITH <dml_trigger_option> [ ,...n ] ]   
{ FOR | AFTER | INSTEAD OF }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
  AS { sql_statement  [ ; ] [ ,...n ] [ ; ] > }  
  
<dml_trigger_option> ::=   
        [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Azure SQL Database Syntax  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, 
-- REVOKE, or UPDATE STATISTICS statement (DDL Trigger)   
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON { DATABASE }   
 [ WITH <ddl_trigger_option> [ ,...n ] ]   
{ FOR | AFTER } { event_type | event_group } [ ,...n ]   
AS { sql_statement  [ ; ] [ ,...n ]  [ ; ] }  
  
<ddl_trigger_option> ::=   
    [ EXECUTE AS Clause ]  
```  
  
## <a name="arguments"></a>인수
OR ALTER  
 **적용 대상**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터 시작) 
  
 이미 있는 경우에만 트리거를 조건부로 변경합니다. 
  
 *schema_name*  
 DML 트리거가 속한 스키마의 이름입니다. DML 트리거는 트리거가 생성된 테이블 또는 뷰의 스키마로 한정됩니다. *schema_name*은 DDL 또는 LOGON 트리거에 대해 지정될 수 없습니다.  
  
 *trigger_name*  
 트리거의 이름입니다. *trigger_name*이 # 또는 ##로 시작할 수 없는 경우를 제외하고 *trigger_name*은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  
  
 *table* | *view*  
 DML 트리거가 실행되는 테이블 또는 뷰이며 트리거 테이블 또는 트리거 뷰라고도 합니다. 테이블 또는 뷰의 정규화된 이름을 지정하는 것은 옵션입니다. 뷰는 INSTEAD OF 트리거에서만 참조될 수 있습니다. 로컬 또는 전역 임시 테이블에는 DML 트리거를 정의할 수 없습니다.  
  
 DATABASE  
 현재 데이터베이스에 DDL 트리거의 해당 범위를 적용합니다. 지정하면 현재 데이터베이스에서 *event_type* 또는 *event_group*이 발생할 때마다 트리거가 실행됩니다.  
  
 ALL SERVER  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 현재 서버에 DDL 또는 LOGON 트리거의 범위를 적용합니다. 지정하면 현재 서버의 어디에서든 *event_type* 또는 *event_group*이 발생할 때마다 트리거가 실행됩니다.  
  
 WITH ENCRYPTION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 CREATE TRIGGER 문의 텍스트를 난독 처리합니다. WITH ENCRYPTION을 사용하면 트리거가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제의 일부로 게시되지 않도록 방지할 수 있습니다. CLR 트리거에 대해서는 WITH ENCRYPTION을 지정할 수 없습니다.  
  
 EXECUTE AS  
 트리거가 실행되는 보안 컨텍스트를 지정합니다. 이를 통해 트리거에서 참조되는 모든 데이터베이스 개체에 대한 사용 권한 유효성을 검사하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 사용하는 사용자 계정을 제어할 수 있습니다.  
  
 이 옵션은 메모리 최적화 테이블의 트리거에 필요합니다.  
  
 자세한 내용은 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)을 참조하세요.  
  
 NATIVE_COMPILATION  
 트리거가 고유하게 컴파일되었음을 나타냅니다.  
  
 이 옵션은 메모리 최적화 테이블의 트리거에 필요합니다.  
  
 SCHEMABINDING  
 트리거에서 참조되는 테이블을 삭제 또는 변경할 수 없도록 보장합니다.  
  
 이 옵션은 메모리 최적화 테이블의 트리거에 필요하며 기존 테이블의 트리거에는 지원되지 않습니다.  
  
 FOR | AFTER  
 AFTER는 DML 트리거를 시작하는 SQL 문에서 지정한 모든 작업이 성공적으로 실행되었을 때만 트리거가 실행되도록 지정합니다. 모든 참조 연계 동작 및 제약 조건 검사도 이 트리거가 실행되기 전에 성공해야 합니다.  
  
 지정된 키워드가 FOR뿐인 경우에는 AFTER가 기본값입니다.  
  
 뷰에 대해서는 AFTER 트리거를 정의할 수 없습니다.  
  
 INSTEAD OF  
 트리거를 시작하는 SQL 문 *대신* DML 트리거가 실행되도록 지정합니다. 즉, 트리거를 시작하는 문의 동작을 재정의합니다. DDL 또는 LOGON 트리거에 대해서는 INSTEAD OF를 지정할 수 없습니다.  
  
 테이블이나 뷰에 대해 INSERT, UPDATE 또는 DELETE 문당 INSTEAD OF 트리거를 하나만 정의할 수 있습니다. 그러나 고유한 INSTEAD OF 트리거가 있는 각 뷰에 대해 뷰를 정의할 수 있습니다.  
  
 WITH CHECK OPTION을 사용하는 업데이트 가능한 뷰에는 INSTEAD OF 트리거를 사용할 수 없습니다. WITH CHECK OPTION이 지정된 업데이트할 수 있는 뷰에 INSTEAD OF 트리거를 추가하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류가 발생하기 때문에, INSTEAD OF 트리거를 정의하기 전에 ALTER VIEW를 사용하여 해당 옵션을 제거해야 합니다.  
  
 { [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }  
 이 테이블이나 뷰에 수행될 경우 DML 트리거를 활성화하는 데이터 수정 문을 지정합니다. 적어도 하나의 옵션을 지정해야 합니다. 트리거 정의에서는 이러한 옵션을 순서에 관계없이 어떤 방법으로도 조합할 수 있습니다.  
  
 INSTEAD OF 트리거의 경우 ON DELETE 연계 동작을 지정하는 참조 관계가 있는 테이블에 대해서는 DELETE 옵션을 사용할 수 없습니다. 마찬가지로 연계 동작인 ON UPDATE를 지정하는 참조 관계가 있는 테이블에 대해서도 UPDATE 옵션이 허용되지 않습니다.  
  
 WITH APPEND  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]까지  
  
 기존 유형의 추가 트리거를 반드시 추가하도록 지정합니다. INSTEAD OF 트리거가 사용되거나 AFTER 트리거가 명시적으로 지정된 경우에는 WITH APPEND를 사용할 수 없습니다. WITH APPEND는 FOR가 INSTEAD OF 또는 AFTER 없이 지정되어 있는 경우에만 이전 버전과의 호환성을 위해 사용할 수 있습니다. EXTERNAL NAME이 지정된 경우(트리거가 CLR 트리거인 경우)에는 WITH APPEND를 지정할 수 없습니다.  
  
 *event_type*  
 실행된 후에 DDL 트리거가 실행되도록 하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 이벤트의 이름입니다. DDL 트리거에 유효한 이벤트는 [DDL 이벤트](../../relational-databases/triggers/ddl-events.md)에 나열되어 있습니다.  
  
 *event_group*  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 이벤트의 미리 정의된 그룹 이름입니다. *event_group*에 속한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 이벤트가 실행된 후에 DDL 트리거가 실행됩니다. DDL 트리거에 유효한 이벤트 그룹은 [DDL 이벤트 그룹](../../relational-databases/triggers/ddl-event-groups.md)에 나열되어 있습니다.  
  
 CREATE TRIGGER 실행이 완료된 후 *event_group*은 해당 이벤트 유형을 sys.trigger_events 카탈로그 뷰에 추가하여 매크로 역할을 합니다.  
  
 NOT FOR REPLICATION  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 복제 에이전트가 트리거와 연관된 테이블을 수정할 때 트리거를 실행할 수 없다는 것을 나타냅니다.  
  
 *sql_statement*  
 트리거 조건 및 동작입니다. 트리거 조건은 시도된 DML, DDL 또는 LOGON 이벤트가 트리거 동작을 수행하게 하는지 여부를 결정하는 추가 조건을 지정합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 지정된 트리거 동작은 해당 작업이 시도될 때 적용됩니다.  
  
 일부 예외가 있지만 트리거는 수와 종류에 관계없이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 포함할 수 있습니다. 자세한 내용은 설명 부분을 참조하세요. 트리거는 데이터 수정 또는 정의 문을 기반으로 하여 데이터를 확인하거나 변경하도록 설계되었습니다. 따라서 데이터를 사용자에게 반환해서는 안 됩니다. 트리거 내의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 [흐름 제어 언어](~/t-sql/language-elements/control-of-flow.md)가 포함되는 경우가 많습니다.  
  
 DML 트리거는 deleted 및 inserted 논리(개념) 테이블을 사용합니다. 이러한 테이블은 구조적으로 트리거가 정의되어 있는 테이블(사용자 동작이 수행되는 테이블)과 유사합니다. deleted 및 inserted 테이블에는 사용자 동작으로 변경될 수 있는 행의 이전 값과 새 값이 유지됩니다. 예를 들어, `deleted` 테이블의 모든 값을 검색하려면 다음을 사용합니다.  
  
```sql  
SELECT * FROM deleted;  
```  
  
 자세한 내용은 [inserted 및 deleted 테이블 사용](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)을 참조하세요.  
  
 DDL 및 LOGON 트리거는 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md) 함수를 사용하여 트리거를 시작하는 이벤트에 대한 정보를 캡처합니다. 자세한 내용은 [EVENTDATA 함수 사용](../../relational-databases/triggers/use-the-eventdata-function.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 테이블 또는 뷰에 대한 INSTEAD OF 트리거를 통해 **text**, **ntext** 또는 **image** 열을 업데이트할 수 있습니다.  
  
> [!IMPORTANT]
>  **ntext**, **text** 및 **image** 데이터 형식은 이후 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 제거됩니다. 향후 개발 작업에서는 이 데이터 형식을 사용하지 않도록 하고 현재 이 데이터 형식을 사용하는 애플리케이션은 수정하세요. 대신 [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)및 [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) 를 사용합니다. AFTER 및 INSTEAD OF 트리거는 모두 inserted 및 deleted 테이블에서 **varchar(MAX)**, **nvarchar(MAX)** 및 **varbinary(MAX)** 데이터를 지원합니다.  
  
 메모리 최적화 테이블의 트리거의 경우, 최상위 수준에서 허용되는 *sql_statement*는 ATOMIC 블록뿐입니다. ATOMIC 블록 내에서 허용되는 T-SQL은 네이티브 프로시저 내에서 허용되는 T-SQL로 제한됩니다.  
  
 \< method_specifier > **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 CLR 트리거의 경우 트리거와 바인딩할 어셈블리의 메서드를 지정합니다. 이 메서드는 인수가 없어야 하며 void를 반환해야 합니다. *class_name*은 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자여야 하며 어셈블리 표시 유형이 있는 어셈블리의 클래스로 존재해야 합니다. 클래스가 마침표 '.'를 사용하여 네임스페이스 부분을 구분하는 네임스페이스로 한정된 이름을 가질 경우 클래스 이름은 [ ] 또는 " " 구분 기호를 사용하여 구분되어야 합니다. 클래스는 중첩 클래스일 수 없습니다.  
  
> [!NOTE]  
>  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 CLR 코드 실행 기능은 해제됩니다. 관리 코드 모듈을 참조하는 데이터베이스 개체를 만들고 변경하고 삭제할 수 있지만, 이러한 참조는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용하여 [clr enabled 옵션](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)을 설정하지 않는 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 실행되지 않습니다.  
  
## <a name="remarks-for-dml-triggers"></a>DML 트리거 설명  
 DML 트리거는 비즈니스 규칙 및 데이터 무결성을 적용하는 데 자주 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 ALTER TABLE 및 CREATE TABLE 문을 통해 DRI(선언적 참조 무결성)를 제공하지만 DRI는 데이터베이스 간 참조 무결성은 제공하지 않습니다. 참조 무결성은 테이블의 기본 키와 외래 키 간의 관계에 대한 규칙을 말합니다. 참조 무결성을 강제 적용하려면 ALTER TABLE 및 CREATE TABLE에서 PRIMARY KEY 및 FOREIGN KEY 제약 조건을 사용하세요. 제약 조건이 트리거 테이블에 있는 경우에는 INSTEAD OF 트리거가 실행된 후와 AFTER 트리거가 실행되기 전에 제약 조건이 확인됩니다. 제약 조건을 위반하면 INSTEAD OF 트리거 동작이 롤백되고 AFTER 트리거가 실행되지 않습니다.  
  
 sp_settriggerorder를 사용하여 테이블에서 실행할 처음 및 마지막 AFTER 트리거를 지정할 수 있습니다. 테이블에서 각각의 INSERT, UPDATE 및 DELETE 작업에 대해 처음 및 마지막 AFTER 트리거를 각각 하나만 정의할 수 있습니다. 동일한 테이블에 다른 AFTER 트리거가 있는 경우 임의로 실행됩니다.  
  
 ALTER TRIGGER 문에서 첫 번째 트리거나 마지막 트리거를 변경하면 수정된 트리거에 설정된 첫 번째 또는 마지막 특성은 삭제되며 sp_settriggerorder를 사용하여 순서 값을 다시 설정해야 합니다.  
  
 AFTER 트리거는 트리거를 시작하는 SQL 문이 성공적으로 실행된 후에만 실행됩니다. 또한 업데이트 또는 삭제된 개체와 관련된 모든 참조 연계 동작과 제약 조건 확인이 성공적으로 수행되어야 합니다. AFTER 트리거는 동일한 테이블에서 INSTEAD OF 트리거를 재귀적으로 실행합니다.  
  
 테이블에 정의된 INSTEAD OF 트리거가 테이블에 대해 보통 INSTEAD OF 트리거를 다시 시작하는 문을 실행하면 트리거가 재귀적으로 호출되지 않습니다. 그 대신 테이블에 INSTEAD OF 트리거가 없는 것처럼 처리되어 제약 조건 작업 및 AFTER 트리거 실행 체인을 시작합니다. 예를 들어, 트리거가 테이블에 대해 INSTEAD OF INSERT 트리거로 정의되고 트리거가 동일한 테이블에서 INSERT 문을 실행하면 INSTEAD OF 트리거에서 실행하는 INSERT 문이 트리거를 다시 호출하지 않습니다. 트리거가 실행하는 INSERT 문은 제약 조건 동작을 수행하고 테이블에 대해 정의된 AFTER INSERT 트리거를 실행하는 프로세스를 시작합니다.  
  
 뷰에 정의된 INSTEAD OF 트리거가 뷰에 대해 보통 INSTEAD OF 트리거를 다시 시작하는 문을 실행하면 트리거가 재귀적으로 호출되지 않습니다. 그 대신 문이 뷰의 원본인 기준 테이블에 대한 수정으로 확인됩니다. 이런 경우 뷰 정의는 업데이트할 수 있는 뷰에 대한 모든 제한을 충족해야 합니다. 업데이트할 수 있는 뷰에 대한 정의는 [뷰를 통해 데이터 수정](../../relational-databases/views/modify-data-through-a-view.md)을 참조하세요.  
  
 예를 들어, 트리거가 뷰에 대해 INSTEAD OF UPDATE 트리거로 정의되고 트리거가 같은 뷰를 참조하는 UPDATE 문을 실행하면 INSTEAD OF 트리거가 실행하는 UPDATE 문은 트리거를 다시 호출하지 않습니다. 트리거가 실행하는 UPDATE는 뷰에 대해 뷰에 INSTEAD OF 트리거가 없는 것처럼 처리됩니다. UPDATE에 의해 변경된 열은 단일 기준 테이블로 확인되어야 합니다. 원본으로 사용하는 기준 테이블을 수정할 때마다 제약 조건 적용 및 테이블에 대해 정의된 AFTER 트리거 시작 체인을 시작합니다.  
  
### <a name="testing-for-update-or-insert-actions-to-specific-columns"></a>특정 열에 대한 UPDATE 또는 INSERT 동작 테스트  
 특정 열에 대한 UPDATE 또는 INSERT 수정 사항을 기반으로 특정 동작을 수행하도록 [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거를 디자인할 수 있습니다. 이를 위해서는 트리거 본문에 [UPDATE()](../../t-sql/functions/update-trigger-functions-transact-sql.md) 또는 [COLUMNS_UPDATED](../../t-sql/functions/columns-updated-transact-sql.md)를 사용합니다. UPDATE()는 열 하나에 대한 UPDATE 또는 INSERT 시도를 테스트하고, COLUMNS_UPDATED는 여러 열에 수행되는 UPDATE 또는 INSERT 동작을 테스트한 다음 삽입되거나 업데이트된 열을 나타내는 비트 패턴을 반환합니다.  
  
### <a name="trigger-limitations"></a>트리거 제한  
 CREATE TRIGGER는 일괄 처리의 첫 번째 문이어야 하며 한 테이블에만 적용될 수 있습니다.  
  
 트리거는 현재 데이터베이스에서만 만들어집니다. 그러나 트리거는 현재 데이터베이스 밖의 개체도 참조할 수 있습니다.  
  
 트리거를 한정하기 위해 트리거 스키마 이름을 지정한 경우에는 같은 방법으로 테이블 이름을 한정하세요.  
  
 같은 CREATE TRIGGER 문에서 둘 이상의 사용자 작업(예: INSERT 및 UPDATE)에 대해 같은 트리거 동작을 정의할 수 있습니다.  
  
 연계 DELETE/UPDATE 동작에 대해 외래 키가 정의된 테이블에 대해서는 INSTEAD OF DELETE/UPDATE 트리거를 정의할 수 없습니다.  
  
 트리거 내부에서 SET 문을 지정할 수 있습니다. 선택된 SET 옵션은 트리거 실행 중에만 적용되며 실행이 끝나면 이전 설정으로 돌아갑니다.  
  
 트리거가 실행되면 저장 프로시저와 마찬가지로 호출하는 응용 프로그램에 결과가 반환됩니다. 트리거 실행으로 인해 응용 프로그램에 결과가 반환되는 것을 방지하려면 결과를 반환하는 SELECT 문이나 트리거에서 변수 할당을 수행하는 문을 포함하지 마세요. 사용자에게 결과를 반환하는 SELECT 문이나 변수 할당을 수행하는 문을 포함하는 트리거는 특수하게 처리해야 합니다. 이렇게 반환된 결과는 트리거 테이블을 수정할 수 있도록 허용된 모든 응용 프로그램에 기록되어야 합니다. 트리거에서 변수를 할당해야 하는 경우에는 트리거 시작 부분에 SET NOCOUNT 문을 사용하여 모든 결과 집합이 반환되지 않게 하세요.  
  
 TRUNCATE TABLE 문은 사실상 DELETE 문과 같지만 이 작업은 개별 행 삭제를 로그하지 않으므로 트리거를 실행하지 않습니다. 하지만 TRUNCATE TABLE 문 실행 권한이 있는 사용자 외에는 이 문이 DELETE 트리거를 실수로 방해하는 것을 염려할 필요가 없습니다.  
  
 WRITETEXT 문은 기록 여부에 관계없이 트리거를 활성화하지 않습니다.  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 DML 트리거에서 사용할 수 없습니다.  
  
||||  
|-|-|-|  
|ALTER DATABASE|CREATE DATABASE|DROP DATABASE|  
|RESTORE DATABASE|RESTORE LOG|RECONFIGURE|  
  
 또한 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 트리거를 실행하는 동작의 대상인 테이블이나 뷰에 사용될 경우 DML 트리거 본문에 사용할 수 없습니다.  
  
||||  
|-|-|-|  
|CREATE INDEX(CREATE SPATIAL INDEX 및 CREATE XML INDEX 포함)|ALTER INDEX|DROP  INDEX|  
|DBCC DBREINDEX|ALTER PARTITION FUNCTION|DROP TABLE|  
|다음 용도로 사용하는 ALTER TABLE<br /><br /> 열 추가, 수정 또는 삭제<br /><br /> 파티션 전환<br /><br /> PRIMARY KEY 또는 UNIQUE 제약 조건 추가 또는 삭제|||  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 시스템 테이블에 대한 사용자 정의 트리거를 지원하지 않기 때문에 시스템 테이블에 대한 사용자 정의 트리거를 만들지 않는 것이 좋습니다. 

### <a name="optimizing-dml-triggers"></a>DML 트리거 최적화
 트랜잭션(묵시적, 또는 그 외)에서 작업을 트리거하고, 열려 있는 동안 리소스를 잠급니다. 트랜잭션이 확인(COMMIT 사용)되거나 거부(ROLLBACK 사용)될 때까지 잠금 상태가 유지됩니다. 트리거 실행 기간이 길수록 다른 프로세스가 차단될 가능성이 높아집니다. 따라서 가능하면 해당 기간을 줄이는 방법으로 트리거를 작성해야 합니다. 이 작업을 수행하는 한 가지 방법은 DML 문이 0개 행을 변경할 때 트리거를 해제하는 것입니다. 

행을 변경하지 않는 명령에 대해 트리거를 해제하려면 [ROWCOUNT_BIG](../functions/rowcount-big-transact-sql.md) 시스템 변수를 사용합니다. 

이는 다음 T-SQL 코드 조각을 사용하여 수행할 수 있으며, 각 DML 트리거의 시작에 표시되어야 합니다.

```sql
IF (ROWCOUNT_BIG() = 0)
RETURN;
```
  
  
## <a name="remarks-for-ddl-triggers"></a>DDL 트리거에 대한 설명  
 DDL 트리거는 표준 트리거와 마찬가지로 이벤트에 대한 응답으로 저장 프로시저를 실행합니다. 하지만 표준 트리거와 달리 테이블이나 뷰의 UPDATE, INSERT 또는 DELETE 문에 대한 응답으로 실행되는 것이 아니라 기본적으로 DDL(데이터 정의 언어) 문에 대한 응답으로 실행됩니다. 이러한 DDL 문에는 CREATE, ALTER, DROP, GRANT, DENY, REVOKE 및 UPDATE STATISTICS 문이 포함됩니다. DDL과 같은 작업을 수행하는 특정 시스템 저장 프로시저에서 DDL 트리거가 발생할 수도 있습니다.  
  
> [!IMPORTANT]  
>  DDL 트리거를 테스트하여 시스템 저장 프로시저 실행에 대한 응답을 확인합니다. 예를 들어 CREATE TYPE 문과 sp_addtype 및 sp_rename 저장 프로시저는 모두 CREATE_TYPE 이벤트에서 생성되는 DDL 트리거를 발생시킵니다.  
  
 DDL 트리거에 대한 자세한 내용은 [DDL 트리거](../../relational-databases/triggers/ddl-triggers.md)를 참조하세요.  
  
 DDL 트리거는 로컬 또는 전역 임시 테이블과 저장 프로시저에 영향을 주는 이벤트에 대한 응답으로 실행되지 않습니다.  
  
 DDL 트리거는 DML 트리거와 달리 스키마로 범위가 한정되지 않습니다. DDL 트리거에 대한 메타데이터를 쿼리하는 데 OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY 및 OBJECTPROPERTYEX와 같은 함수는 사용할 수 없습니다. 대신 카탈로그 뷰를 사용하세요. 자세한 내용은 [DDL 트리거에 대한 정보 가져오기](../../relational-databases/triggers/get-information-about-ddl-triggers.md)를 참조하세요.  
  
> [!NOTE]  
>  서버 범위 DDL 트리거는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기의 **Triggers** 폴더에 나타납니다. 이 폴더는 **서버 개체** 폴더 아래에 있습니다. 데이터베이스 범위 DDL 트리거는 **Database Triggers** 폴더에 나타납니다. 이 폴더는 해당 데이터베이스의 **프로그래밍 기능** 폴더 아래에 있습니다.  
  
## <a name="logon-triggers"></a>LOGON 트리거  
 LOGON 트리거는 LOGON 이벤트에 대한 응답으로 저장 프로시저를 실행합니다. 이 이벤트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 사용자 세션이 설정된 경우 발생합니다. LOGON 트리거는 로그인의 인증 단계가 완료되었지만 사용자 세션이 실제로 설정되기 전에 발생합니다. 따라서 오류 메시지 및 PRINT 문의 메시지와 같이 일반적으로 사용자에게 전달되는 모든 트리거 내 발생 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그로 전달됩니다. 자세한 내용은 [LOGON 트리거](../../relational-databases/triggers/logon-triggers.md)를 참조하세요.  
  
 인증에 실패할 경우 LOGON 트리거는 실행되지 않습니다.  
  
 분산 트랜잭션은 로그온 트리거에서 지원되지 않습니다. 분산 트랜잭션이 포함된 로그온 트리거가 발생되면 오류 3969가 반환됩니다.  
  
### <a name="disabling-a-logon-trigger"></a>로그온 트리거 비활성화  
 로그온 트리거를 사용하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] sysadmin **고정 서버 역할의 멤버를 비롯한 모든 사용자에 대해** 에 성공적으로 연결하지 못하도록 효과적으로 차단할 수 있습니다. 로그온 트리거가 연결을 차단 중인 경우 **sysadmin** 고정 서버 역할의 멤버는 관리자 전용 연결을 사용하거나 최소 구성 모드(-f)로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 시작하여 연결할 수 있습니다. 자세한 내용은 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)을(를) 참조하세요.  
  
## <a name="general-trigger-considerations"></a>일반적인 트리거 고려 사항  
  
### <a name="returning-results"></a>결과 반환  
 이후 버전의 SQL Server에서는 트리거에서 결과를 반환하는 기능이 제거됩니다. 결과 집합을 반환하는 트리거는 트리거가 작동하지 않는 애플리케이션에 예기치 않은 동작을 유발할 수도 있습니다. 향후 개발 작업에서는 트리거에서 결과 집합을 반환하지 않도록 하고 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 트리거가 결과 집합을 반환하지 않도록 하려면 [disallow results from triggers 옵션](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md)을 1로 설정합니다.  
  
 LOGON 트리거는 결과 집합 반환을 항상 허용하지 않으며 이 동작은 구성할 수 없습니다. LOGON 트리거가 결과 집합을 생성할 경우 트리거가 실행되지 않고 트리거를 실행한 로그인 시도가 거부됩니다.  
  
### <a name="multiple-triggers"></a>다중 트리거  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 각 DML, DDL 또는 LOGON 이벤트에 대해 다중 트리거를 만들 수 있습니다. 예를 들어, CREATE TRIGGER FOR UPDATE가 이미 UPDATE 트리거가 있는 테이블에 대해 실행된 경우에는 추가 업데이트 트리거가 만들어집니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 각 테이블에서 DELETE, INSERT 또는 UPDATE 데이터 수정 이벤트 각각에 대해 트리거를 하나만 만들 수 있었습니다.  
  
### <a name="recursive-triggers"></a>재귀 트리거  
 ALTER DATABASE를 사용하여 RECURSIVE_TRIGGERS 설정을 활성화한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 재귀적 트리거 호출을 사용할 수 있습니다.  
  
 재귀 트리거를 사용하면 다음 유형의 재귀 호출을 실행할 수 있습니다.  
  
-   간접 재귀  
  
     간접 재귀에서는 응용 프로그램이 T1 테이블을 업데이트하면 TR1 트리거가 실행되어 T2 테이블을 업데이트합니다. 그런 다음 T2 트리거가 실행되어 T1 테이블을 업데이트합니다.  
  
-   직접 재귀  
  
     직접 재귀에서는 응용 프로그램이 T1 테이블을 업데이트하면 TR1 트리거가 실행되어 T1 테이블을 업데이트합니다. T1 테이블이 업데이트되었으므로 TR1이 다시 실행되고 이런 식으로 계속됩니다.  
  
 간접 트리거 재귀와 직접 트리거 재귀를 모두 사용하는 다음 예에서는 두 업데이트 트리거 TR1 및 TR2가 T1 테이블에 정의되어 있다고 가정합니다. TR1 트리거는 T1 테이블을 재귀적으로 업데이트합니다. UPDATE 문은 각 TR1 및 TR2를 한 번 실행합니다. 또한 TR1을 실행하면 재귀적으로 TR1이 실행된 다음 TR2가 실행됩니다. 특정 트리거에 대한 inserted 및 deleted 테이블에는 트리거를 호출한 UPDATE 문에만 해당되는 행이 포함됩니다.  
  
> [!NOTE]  
>  위 동작은 ALTER DATABASE를 사용하여 RECURSIVE_TRIGGERS 설정을 활성화한 경우에만 실행됩니다. 특정 이벤트에 정의된 다중 트리거의 실행 순서는 정해져 있지 않습니다. 각 트리거는 반드시 자기를 포함해야 합니다.  
  
 RECURSIVE_TRIGGERS 설정을 비활성화하면 직접 재귀만 금지됩니다. 간접 재귀도 비활성화하려면 sp_configure를 사용하여 nested triggers 서버 옵션을 0으로 설정합니다.  
  
 트리거 중 하나가 ROLLBACK TRANSACTION을 수행하는 경우에는 중첩 수준에 관계없이 더 이상 트리거가 실행되지 않습니다.  
  
### <a name="nested-triggers"></a>중첩 트리거  
 트리거는 최대 32 수준까지 중첩될 수 있습니다. 트리거가 있는 테이블을 다른 트리거가 변경하는 경우에는 두 번째 트리거가 활성화되고 이어서 세 번째 트리거가 호출되는 방식으로 진행됩니다. 체인 내의 한 트리거가 무한 루프를 시작하면 중첩 수준이 초과되고 트리거가 취소됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거에서 CLR 루틴, 유형 또는 집계를 참조하여 관리 코드를 실행하는 경우 이러한 참조는 32 수준 중첩 제한에서 한 수준으로 계산됩니다. 관리 코드 내에서 호출된 메서드는 이 제한에 따라 계산되지 않습니다.  
  
 중첩 트리거를 비활성화하려면 sp_configure의 nested triggers 옵션을 0(off)으로 설정하십시오. 기본 구성은 중첩 트리거를 허용합니다. 중첩된 트리거가 해제된 경우 ALTER DATABASE를 사용하여 설정된 RECURSIVE_TRIGGERS 설정에 관계없이 재귀 트리거도 비활성화됩니다.  
  
 INSTEAD OF 트리거 내부에 중첩된 첫 번째 AFTER 트리거는 **중첩된 트리거** 서버 구성 옵션이 0으로 설정되어 있는 경우에도 실행됩니다. 그러나 이 설정에서는 이후의 AFTER 트리거는 발생하지 않습니다. 중첩 트리거에 대한 애플리케이션을 검토하여 **중첩된 트리거** 서버 구성 옵션이 0으로 설정된 경우 이 새 동작과 관련된 비즈니스 규칙을 애플리케이션이 여전히 준수하는지 확인한 다음, 적절하게 수정하는 것이 좋습니다.  
  
### <a name="deferred-name-resolution"></a>지연된 이름 확인  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저, 트리거 및 일괄 처리에서는 컴파일 시간에 존재하지 않는 테이블을 참조할 수 있습니다. 이 기능을 지연된 이름 확인이라고 합니다.  
  
## <a name="permissions"></a>Permissions  
 DML 트리거를 만들려면 트리거를 만들 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
 서버 범위(ON ALL SERVER)의 DDL 트리거 또는 LOGON 트리거를 만들려면 해당 서버에 대한 CONTROL SERVER 권한이 필요합니다. 데이터베이스 범위(ON DATABASE)의 DDL 트리거를 만들려면 현재 데이터베이스에 대한 ALTER ANY DATABASE DDL TRIGGER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-a-dml-trigger-with-a-reminder-message"></a>1. 미리 알림 메시지로 DML 트리거 사용  
 다음 DML 트리거는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Customer` 테이블에 데이터를 추가하거나 변경하려고 할 때 클라이언트에 메시지를 출력합니다.  
  
```sql  
CREATE TRIGGER reminder1  
ON Sales.Customer  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Customer Relations', 16, 10);  
GO  
```  
  
### <a name="b-using-a-dml-trigger-with-a-reminder-e-mail-message"></a>2. 미리 알림 전자 메일 메시지로 DML 트리거 사용  
 다음 예에서는 `MaryM` 테이블이 변경될 때 지정한 사람(`Customer`)에게 전자 메일 메시지를 보냅니다.  
  
```sql  
CREATE TRIGGER reminder2  
ON Sales.Customer  
AFTER INSERT, UPDATE, DELETE   
AS  
   EXEC msdb.dbo.sp_send_dbmail  
        @profile_name = 'AdventureWorks2012 Administrator',  
        @recipients = 'danw@Adventure-Works.com',  
        @body = 'Don''t forget to print a report for the sales force.',  
        @subject = 'Reminder';  
GO  
```  
  
### <a name="c-using-a-dml-after-trigger-to-enforce-a-business-rule-between-the-purchaseorderheader-and-vendor-tables"></a>3. PurchaseOrderHeader와 Vendor 테이블 간에 업무 규칙을 적용하는 DML AFTER 트리거 사용  
 CHECK 제약 조건은 열 수준 또는 테이블 수준 제약 조건이 정의된 열만 참조할 수 있으므로 모든 상호 테이블 제약 조건(이 경우 업무 규칙)을 트리거로 정의해야 합니다.  
  
 다음 예에서는 AdventureWorks2012 데이터베이스에서 DML 트리거를 만듭니다. 이 트리거는 `PurchaseOrderHeader` 테이블에 새 구매 주문을 삽입하려고 할 때 공급업체의 신용 등급이 양호한지(5가 아닌지) 확인합니다. 공급업체의 신용 등급을 가져오려면 `Vendor` 테이블을 참조해야 합니다. 신용 등급이 너무 낮으면 메시지가 표시되고 삽입이 실행되지 않습니다.  
  
```sql  
-- This trigger prevents a row from being inserted in the Purchasing.PurchaseOrderHeader 
-- table when the credit rating of the specified vendor is set to 5 (below average).  
  
CREATE TRIGGER Purchasing.LowCredit ON Purchasing.PurchaseOrderHeader  
AFTER INSERT  
AS  
IF (@@ROWCOUNT_BIG  = 0)
RETURN;
IF EXISTS (SELECT *  
           FROM Purchasing.PurchaseOrderHeader AS p   
           JOIN inserted AS i   
           ON p.PurchaseOrderID = i.PurchaseOrderID   
           JOIN Purchasing.Vendor AS v   
           ON v.BusinessEntityID = p.VendorID  
           WHERE v.CreditRating = 5  
          )  
BEGIN  
RAISERROR ('A vendor''s credit rating is too low to accept new  
purchase orders.', 16, 1);  
ROLLBACK TRANSACTION;  
RETURN   
END;  
GO  
  
-- This statement attempts to insert a row into the PurchaseOrderHeader table  
-- for a vendor that has a below average credit rating.  
-- The AFTER INSERT trigger is fired and the INSERT transaction is rolled back.  
  
INSERT INTO Purchasing.PurchaseOrderHeader (RevisionNumber, Status, EmployeeID,  
VendorID, ShipMethodID, OrderDate, ShipDate, SubTotal, TaxAmt, Freight)  
VALUES (  
2  
,3  
,261  
,1652  
,4  
,GETDATE()  
,GETDATE()  
,44594.55  
,3567.564  
,1114.8638 );  
GO  
  
```  
  
### <a name="d-using-a-database-scoped-ddl-trigger"></a>D. 데이터베이스 범위 DDL 트리거 사용  
 다음 예에서는 DDL 트리거를 사용하여 데이터베이스에서 동의어가 삭제되지 않도록 방지합니다.  
  
```sql  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_SYNONYM  
AS   
IF (@@ROWCOUNT = 0)
RETURN;
   RAISERROR ('You must disable Trigger "safety" to drop synonyms!',10, 1)  
   ROLLBACK  
GO  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
### <a name="e-using-a-server-scoped-ddl-trigger"></a>E. 서버 범위 DDL 트리거 사용  
 다음 예에서는 DDL 트리거를 사용하여 현재 서버 인스턴스에서 CREATE DATABASE 이벤트가 발생할 경우 메시지를 출력하고 `EVENTDATA` 함수를 사용하여 해당 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 텍스트를 검색합니다. DDL 트리거에 EVENTDATA를 사용하는 추가 예는 [EVENTDATA 함수 사용](../../relational-databases/triggers/use-the-eventdata-function.md)을 참조하세요.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```sql  
CREATE TRIGGER ddl_trig_database   
ON ALL SERVER   
FOR CREATE_DATABASE   
AS   
    PRINT 'Database Created.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
GO  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
```  
  
### <a name="f-using-a-logon-trigger"></a>F. LOGON 트리거 사용  
 다음 예에서는 LOGON 트리거가 *login_test* 로그인의 멤버로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로그인을 시도할 때 해당 로그인에서 이미 3개의 사용자 세션이 실행 중일 경우 해당 시도를 거부합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```sql  
USE master;  
GO  
CREATE LOGIN login_test WITH PASSWORD = '3KHJ6dhx(0xVYsdf' MUST_CHANGE,  
    CHECK_EXPIRATION = ON;  
GO  
GRANT VIEW SERVER STATE TO login_test;  
GO  
CREATE TRIGGER connection_limit_trigger  
ON ALL SERVER WITH EXECUTE AS 'login_test'  
FOR LOGON  
AS  
BEGIN  
IF ORIGINAL_LOGIN()= 'login_test' AND  
    (SELECT COUNT(*) FROM sys.dm_exec_sessions  
            WHERE is_user_process = 1 AND  
                original_login_name = 'login_test') > 3  
    ROLLBACK;  
END;  
  
```  
  
### <a name="g-viewing-the-events-that-cause-a-trigger-to-fire"></a>G. 트리거를 발생시킨 이벤트 보기  
 다음 예에서는 `sys.triggers` 및 `sys.trigger_events` 카탈로그 뷰를 쿼리하여 `safety` 트리거를 발생시킨 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 이벤트를 확인합니다. `safety` 트리거는 위에 있는 'D' 예제에서 생성됩니다.  
  
```sql  
SELECT TE.*  
FROM sys.trigger_events AS TE  
JOIN sys.triggers AS T ON T.object_id = TE.object_id  
WHERE T.parent_class = 0 AND T.name = 'safety';  
GO  
```  

    

## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [COLUMNS_UPDATED&#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [TRIGGER_NESTLEVEL&#40;Transact-SQL&#41;](../../t-sql/functions/trigger-nestlevel-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.dm_sql_referenced_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helptext&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_settriggerorder&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md)   
 [UPDATE&#40;&#41;&#40;Transact-SQL&#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)   
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
  
  


