---
title: CREATE SERVER AUDIT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_SERVER_AUDIT_TSQL
- SERVER AUDIT
- SERVER_AUDIT_TSQL
- CREATE SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- CREATE SERVER AUDIT statement
- audits [SQL Server], creating
ms.assetid: 1c321680-562e-41f1-8eb1-e7fa5ae45cc5
caps.latest.revision: 44
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 85ee3b6a5f674a9d4ee63cb54ffca867abca1f04
ms.sourcegitcommit: d8e3da95f5a2b7d3997d63c53e722d494b878eec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2018
ms.locfileid: "44171745"
---
# <a name="create-server-audit-transact-sql"></a>CREATE SERVER AUDIT(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit를 사용하여 서버 감사 개체를 만듭니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE SERVER AUDIT audit_name  
{  
    TO { [ FILE (<file_options> [ , ...n ] ) ] | APPLICATION_LOG | SECURITY_LOG | URL}  
    [ WITH ( <audit_options> [ , ...n ] ) ]   
    [ WHERE <predicate_expression> ]  
}  
[ ; ]  
  
<file_options>::=  
{  
        FILEPATH = 'os_file_path'  
    [ , MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED } ]  
    [ , { MAX_ROLLOVER_FILES = { integer | UNLIMITED } } | { MAX_FILES = integer } ]  
    [ , RESERVE_DISK_SPACE = { ON | OFF } ]   
}  
  
<audit_options>::=  
{  
    [   QUEUE_DELAY = integer ]  
    [ , ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION } ]  
    [ , AUDIT_GUID = uniqueidentifier ]  
}  
  
<predicate_expression>::=  
{  
    [NOT ] <predicate_factor>   
    [ { AND | OR } [NOT ] { <predicate_factor> } ]   
    [,...n ]  
}  
  
<predicate_factor>::=   
    event_field_name { = | < > | ! = | > | > = | < | < = } { number | ' string ' }  
```  
  
## <a name="arguments"></a>인수  
 TO { FILE | APPLICATION_LOG | SECURITY_LOG | URL  
 감사 대상의 위치를 결정합니다. 이 옵션은 이진 파일, Windows 응용 프로그램 로그 또는 Windows 보안 로그입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 Windows 보안 로그에 쓸 수 없습니다. 자세한 내용은 [보안 로그에 SQL Server Audit 이벤트 쓰기](../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)를 참조하세요.  

> [!IMPORTANT]
> Azure SQL Database Managed Instance에서 SQL Audit은 서버 수준에서 작동하며 Azure Blob Storage에 `.xel` 파일을 저장합니다.
  
 FILEPATH ='*os_file_path*'  
 감사 로그의 경로입니다. 파일 이름은 감사 이름과 감사 GUID를 기준으로 생성됩니다.  
  
 MAXSIZE = { *max_size }*  
 감사 파일이 증가할 수 있는 최대 크기를 지정합니다. *max_size* 값은 뒤에 MB, GB, TB가 나오는 정수이거나 UNLIMITED여야 합니다. *max_size*에 대해 지정할 수 있는 최소 크기는 2MB이고 최대 크기는 2,147,483,647 TB입니다. UNLIMITED를 지정하는 경우 디스크가 꽉 찰 때까지 파일이 증가합니다. 0도 UNLIMITED를 나타냅니다. 2MB보다 작은 값을 지정하면 MSG_MAXSIZE_TOO_SMALL 오류가 발생합니다. 기본값은 UNLIMITED입니다.  
  
 MAX_ROLLOVER_FILES =*{ integer* | UNLIMITED }  
 현재 파일 외에 파일 시스템에 보관할 최대 파일 수를 지정합니다. *MAX_ROLLOVER_FILES* 값은 정수 또는 UNLIMITED여야 합니다. 기본값은 UNLIMITED입니다. 이 매개 변수는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 다시 시작되거나 감사가 해제된 후 다시 활성화되어 감사가 다시 시작될 때마다 평가되거나 MAXSIZE에 도달하여 새 파일이 필요할 때 평가됩니다. *MAX_ROLLOVER_FILES*가 평가될 때 파일 수가 *MAX_ROLLOVER_FILES* 설정을 초과하면 가장 오래된 파일부터 삭제됩니다. 따라서 *MAX_ROLLOVER_FILES* 설정이 0이면 *MAX_ROLLOVER_FILES* 설정이 평가될 때마다 새 파일이 만들어집니다. *MAX_ROLLOVER_FILES* 설정이 평가될 때 파일이 한 개만 자동으로 삭제되므로 *MAX_ROLLOVER_FILES*의 값이 감소될 때 파일 수는 오래된 파일을 수동으로 삭제하지 않는 한 줄어들지 않습니다. 지정할 수 있는 최대 파일 수는 2,147,483,647입니다.  
  
 MAX_FILES =*integer*  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 만들 수 있는 최대 감사 파일 수를 지정합니다. 이 제한에 도달하는 경우 첫 파일로 롤오버하지 않습니다. MAX_FILES 제한에 도달하면 추가 감사 이벤트를 생성하는 동작이 실패하며 오류가 발생합니다.  
  
 RESERVE_DISK_SPACE = { ON | OFF }  
 이 옵션은 디스크의 파일을 MAXSIZE 값으로 미리 할당하며, MAXSIZE가 UNLIMITED가 아닌 경우에만 적용됩니다. 기본값은 OFF입니다.  
  
 QUEUE_DELAY =*integer*  
 감사 동작이 강제 처리되기 전까지 허용되는 시간(밀리초)을 지정합니다. 값이 0인 경우 동기 배달을 나타냅니다. 설정 가능한 최소 쿼리 지연 값은 1000입니다. 이 값은 1초에 해당하며 기본값입니다. 최대값은 2,147,483,647로 2,147,483.647초 또는 24일, 20시간, 31분, 23.647초에 해당합니다. 잘못된 수를 지정하면 MSG_INVALID_QUEUE_DELAY 오류가 발생합니다.  
  
 ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }  
 대상에서 감사 로그에 쓸 수 없는 경우 대상에 쓰기 작업을 수행하는 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실패하는지, 계속되는지 또는 중지되는지를 나타냅니다. 기본값은 CONTINUE입니다.  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업을 계속합니다. 감사 레코드는 보존되지 않습니다. 감사는 계속해서 이벤트 기록을 시도하며 실패 조건이 해결되면 재개됩니다. 계속 옵션을 선택하면 감사되지 않는 작업이 허용되어 보안 정책을 위반할 수 있습니다. 전체 감사를 유지 관리하는 것보다 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 작업을 계속하는 것이 더 중요하면 이 옵션을 사용하십시오.  
  
SHUTDOWN  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 어떤 이유로든 감사 대상에 데이터를 쓰지 못하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스가 강제 종료됩니다. `CREATE SERVER AUDIT` 문을 실행하는 로그인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에 `SHUTDOWN` 권한이 있어야 합니다. `SHUTDOWN` 권한이 실행중인 로그인에서 나중에 취소된 경우에도 종료 동작은 지속됩니다. 사용자에게 이 권한이 없으면 문은 실패하고 감사는 생성되지 않습니다. 감사 실패로 인해 시스템 무결성 또는 보안이 손상될 수 있는 경우 이 옵션을 사용하십시오. 자세한 내용은 [SHUTDOWN](../../t-sql/language-elements/shutdown-transact-sql.md)을 참조하세요.  
  
 FAIL_OPERATION  
 감사된 이벤트를 발생시키는 데이터베이스 동작이 실패합니다. 감사된 이벤트를 발생시키지 않는 동작은 계속할 수 있지만 감사된 이벤트는 발생할 수 없습니다. 감사는 계속해서 이벤트 기록을 시도하며 실패 조건이 해결되면 재개됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 모든 권한을 얻는 것보다 전체 감사를 유지 관리하는 것이 더 중요하면 이 옵션을 사용하십시오.  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

 AUDIT_GUID =*uniqueidentifier*  
 데이터베이스 미러링과 같은 시나리오를 지원하려면 미러된 데이터베이스에서 찾은 GUID와 일치하는 특정 GUID가 감사에 필요합니다. 감사가 만들어진 후에는 이 GUID를 수정할 수 없습니다.  
  
 predicate_expression  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 이벤트 처리 여부를 확인하는 데 사용할 조건자 식을 지정합니다. 조건자 식은 3000자로 제한되며 문자열 인수를 제한합니다.  
  
 event_field_name  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 조건자 원본을 식별하는 이벤트 필드의 이름입니다. 감사 필드는 [sys.fn_get_audit_file&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)에 설명되어 있습니다. `file_name`, `audit_file_offset` 및 `event_time`을 제외한 모든 필드를 필터링할 수 있습니다.  

> [!NOTE]  
>  in sys.fn_get_audit_file에서 `action_id` 및 `class_type` 필드의 형식이 **varchar**인 경우에는 필터링에 대한 조건자 원본인 경우 숫자와 함께만 사용할 수 있습니다. `class_type`과 함께 사용할 값의 목록을 얻으려면 다음 쿼리를 실행합니다.  
> ```sql
> SELECT spt.[name], spt.[number]
> FROM   [master].[dbo].[spt_values] spt
> WHERE  spt.[type] = N'EOD'
> ORDER BY spt.[name];
> ```


 number  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 **decimal**을 포함한 모든 숫자 유형입니다. 단, 사용 가능한 실제 메모리가 부족한 경우나 값이 너무 커서 64비트 정수로 표현할 수 없는 숫자는 제외됩니다.  
  
 ' string '  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 조건자 비교에 필요한 ANSI 또는 유니코드 문자열입니다. 조건자 비교 함수에 대해서는 암시적 문자열 유형 변환이 수행되지 않습니다. 잘못된 유형을 전달하면 오류가 발생합니다.  
  
## <a name="remarks"></a>Remarks  
 서버 감사를 처음 만들 때는 사용할 수 없는 상태입니다.  
  
 CREATE SERVER AUDIT 문은 트랜잭션 범위 내에 있습니다. 트랜잭션이 롤백되면 이 문도 롤백됩니다.  
  
## <a name="permissions"></a>Permissions  
 서버 감사를 생성, 변경 또는 삭제하려면 보안 주체에게 ALTER ANY SERVER AUDIT 또는 CONTROL SERVER 권한이 있어야 합니다.  
  
 감사 정보를 파일에 저장할 때 변조를 방지하기 위해 파일 위치에 대한 액세스를 제한합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-server-audit-with-a-file-target"></a>1. 파일 대상을 사용하여 서버 감사 만들기  
 다음 예에서는 이진 파일을 대상으로 사용하고 옵션 없이 `HIPPA_Audit`라는 서버 감사를 만듭니다.  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
```  
  
### <a name="b-creating-a-server-audit-with-a-windows-application-log-target-with-options"></a>2. Windows 응용 프로그램 로그 대상과 옵션을 사용하여 서버 감사 만들기  
 다음 예에서는 Windows 응용 프로그램 로그에 대한 대상 집합을 사용하여 `HIPPA_Audit`라는 서버 감사를 만듭니다. 큐가 1초마다 기록되고 실패 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔진을 종료합니다.  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO APPLICATION_LOG  
    WITH ( QUEUE_DELAY = 1000,  ON_FAILURE = SHUTDOWN);  
```  
  
###  <a name="ExampleWhere"></a> 3. WHERE 절을 포함하는 서버 감사 만들기  
 다음 예에서는 데이터베이스 하나, 스키마 하나 및 테이블 두 개를 만듭니다. `DataSchema.SensitiveData`라는 테이블은 기밀 데이터를 포함하며, 테이블에 대한 액세스가 감사에 기록되어야 합니다. `DataSchema.GeneralData`라는 테이블은 기밀 데이터를 포함하지 않습니다. 데이터베이스 감사 사양은 `DataSchema` 스키마의 모든 개체에 대한 액세스를 감사합니다. 서버 감사를 `SensitiveData` 테이블로만 제한하는 WHERE 절을 사용하여 서버 감사를 만듭니다. 서버 감사에서는 감사 폴더가 `C:\SQLAudit`에 있다고 가정합니다.  
  
```sql  
CREATE DATABASE TestDB;  
GO  
USE TestDB;  
GO  
CREATE SCHEMA DataSchema;  
GO  
CREATE TABLE DataSchema.GeneralData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
CREATE TABLE DataSchema.SensitiveData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
-- Create the server audit in the master database  
USE master;  
GO  
CREATE SERVER AUDIT AuditDataAccess  
    TO FILE ( FILEPATH ='C:\SQLAudit\' )  
    WHERE object_name = 'SensitiveData' ;  
GO  
ALTER SERVER AUDIT AuditDataAccess WITH (STATE = ON);  
GO  
-- Create the database audit specification in the TestDB database  
USE TestDB;  
GO  
CREATE DATABASE AUDIT SPECIFICATION [FilterForSensitiveData]  
FOR SERVER AUDIT [AuditDataAccess]   
ADD (SELECT ON SCHEMA::[DataSchema] BY [public])  
WITH (STATE = ON);  
GO  
-- Trigger the audit event by selecting from tables  
SELECT ID, DataField FROM DataSchema.GeneralData;  
SELECT ID, DataField FROM DataSchema.SensitiveData;  
GO  
-- Check the audit for the filtered content  
SELECT * FROM fn_get_audit_file('C:\SQLAudit\AuditDataAccess_*.sqlaudit',default,default);  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [서버 감사 및 서버 감사 사양 만들기](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
