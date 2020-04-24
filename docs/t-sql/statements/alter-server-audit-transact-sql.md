---
title: ALTER SERVER AUDIT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_AUDIT_TSQL
- ALTER SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
- ALTER SERVER AUDIT statement
ms.assetid: 63426d31-7a5c-4378-aa9e-afcf4f64ceb3
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b06029185eeae67fa251d8c23927208deaba328a
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81631863"
---
# <a name="alter-server-audit--transact-sql"></a>ALTER SERVER AUDIT(Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 기능을 사용하여 서버 감사 개체를 변경합니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ALTER SERVER AUDIT audit_name  
{  
    [ TO { { FILE ( <file_options> [, ...n] ) } | APPLICATION_LOG | SECURITY_LOG } | URL]  
    [ WITH ( <audit_options> [ , ...n] ) ]   
    [ WHERE <predicate_expression> ]  
}  
| REMOVE WHERE  
| MODIFY NAME = new_audit_name  
[ ; ]  
  
<file_options>::=  
{  
      FILEPATH = 'os_file_path'   
    | MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED }   
    | MAX_ROLLOVER_FILES = { integer | UNLIMITED }   
    | MAX_FILES = integer   
    | RESERVE_DISK_SPACE = { ON | OFF }   
}  
  
<audit_options>::=  
{  
      QUEUE_DELAY = integer   
    | ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }   
    | STATE = = { ON | OFF }   
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
 TO { FILE | APPLICATION_LOG | SECURITY |URL}  
 감사 대상의 위치를 결정합니다. 이 옵션은 이진 파일, Windows 애플리케이션 로그 또는 Windows 보안 로그가 될 수 있습니다.  

> [!IMPORTANT]
> Azure SQL Database 관리되는 인스턴스에서 SQL Audit은 서버 수준에서 작동하며 Azure Blob Storage에 `.xel` 파일을 저장합니다.
  
 FILEPATH **= ‘** _os\_파일\_경로_ **’**  
 감사 내역의 경로입니다. 파일 이름은 감사 이름과 감사 GUID를 기준으로 생성됩니다.  
  
 MAXSIZE **=** _최대\_크기_  
 감사 파일이 증가할 수 있는 최대 크기를 지정합니다. *max_size* 값은 뒤에 **MB**, **GB**, **TB**가 나오는 정수이거나 **UNLIMITED**여야 합니다. *max_size*에 대해 지정할 수 있는 최소 크기는 2**MB**이고 최대 크기는 2,147,483,647**TB**입니다. **UNLIMITED**를 지정하는 경우 디스크가 꽉 찰 때까지 파일이 증가합니다. 2MB보다 작은 값을 지정하면 MSG_MAXSIZE_TOO_SMALL 오류가 발생합니다. 기본값은 **UNLIMITED**입니다.  
  
 MAX_ROLLOVER_FILES **=** _integer_ | **UNLIMITED**  
 파일 시스템에 보관할 최대 파일 수를 지정합니다. MAX_ROLLOVER_FILES=0으로 설정하면 롤오버 파일이 무제한으로 만들어집니다. 기본값은 0입니다. 지정할 수 있는 최대 파일 수는 2,147,483,647입니다.  
  
 MAX_FILES =*integer*  
 만들 수 있는 최대 감사 파일 수를 지정합니다. 이 제한에 도달하는 경우 첫 파일로 롤오버하지 않습니다. MAX_FILES 제한에 도달하면 추가 감사 이벤트를 생성하는 동작이 실패하며 오류가 발생합니다.  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상  
  
 RESERVE_DISK_SPACE **=** { ON | OFF }  
 이 옵션은 디스크의 파일을 MAXSIZE 값으로 미리 할당하며, MAXSIZE가 UNLIMITED가 아닌 경우에만 적용됩니다. 기본값은 OFF입니다.  
  
 QUEUE_DELAY **=** _integer_  
 감사 동작이 강제 처리되기 전까지 허용되는 시간(밀리초)을 지정합니다. 값이 0인 경우 동기 배달을 나타냅니다. 설정 가능한 최소 쿼리 지연 값은 1000입니다. 이 값은 1초에 해당하며 기본값입니다. 최대값은 2,147,483,647로 2,147,483.647초 또는 24일, 20시간, 31분, 23.647초에 해당합니다. 잘못된 수를 지정하면 MSG_INVALID_QUEUE_DELAY 오류가 발생합니다.  
  
 ON_FAILURE **=** { CONTINUE | SHUTDOWN | FAIL_OPERATION}  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 감사 로그에 쓸 수 없는 경우 대상에 쓰기 작업을 수행하는 인스턴스가 실패하는지, 계속되는지 또는 중지되는지를 나타냅니다.  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업을 계속합니다. 감사 레코드는 보존되지 않습니다. 감사는 계속해서 이벤트 기록을 시도하며 실패 조건이 해결되면 재개됩니다. 계속 옵션을 선택하면 감사되지 않는 작업이 허용되어 보안 정책을 위반할 수 있습니다. 전체 감사를 유지 관리하는 것보다 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 작업을 계속하는 것이 더 중요하면 이 옵션을 사용하십시오.  
  
SHUTDOWN  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 어떤 이유로든 감사 대상에 데이터를 쓰지 못하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스가 강제 종료됩니다. `ALTER` 문을 실행하는 로그인은 `SHUTDOWN` 내에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 권한이 있어야 합니다. `SHUTDOWN` 권한이 실행중인 로그인에서 나중에 취소된 경우에도 종료 동작은 지속됩니다. 사용자에게 이 권한이 없으면 명령문은 실패하고 감사는 수정되지 않습니다. 감사 실패로 인해 시스템 무결성 또는 보안이 손상될 수 있는 경우 이 옵션을 사용하십시오. 자세한 내용은 [SHUTDOWN](../../t-sql/language-elements/shutdown-transact-sql.md)을 참조하세요. 
  
 FAIL_OPERATION  
 감사된 이벤트를 발생시키는 데이터베이스 동작이 실패합니다. 감사된 이벤트를 발생시키지 않는 동작은 계속할 수 있지만 감사된 이벤트는 발생할 수 없습니다. 감사는 계속해서 이벤트 기록을 시도하며 실패 조건이 해결되면 재개됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 모든 권한을 얻는 것보다 전체 감사를 유지 관리하는 것이 더 중요하면 이 옵션을 사용하십시오.  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상   
  
 STATE **=** { ON | OFF }  
 레코드 수집에서 감사를 설정하거나 해제합니다. 실행 중인 감사의 상태를 ON에서 OFF로 변경하면 감사가 중지되었다는 감사 항목, 감사를 중지한 보안 주체 및 감사가 중지된 시간이 생성됩니다.  
  
 MODIFY NAME = *new_audit_name*  
 감사 이름을 변경합니다. 다른 옵션과 함께 사용할 수 없습니다.  
  
 predicate_expression  
 이벤트 처리 여부를 확인하는 데 사용할 조건자 식을 지정합니다. 조건자 식은 3000자로 제한되며 문자열 인수를 제한합니다.  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상  
  
 event_field_name  
 조건자 원본을 식별하는 이벤트 필드의 이름입니다. 감사 필드는 [sys.fn_get_audit_file&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)에 설명되어 있습니다. `file_name` 및 `audit_file_offset`을 제외한 모든 필드를 감사할 수 있습니다.  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상  
  
 number  
 **decimal**을 포함한 모든 숫자 유형입니다. 단, 사용 가능한 실제 메모리가 부족한 경우나 값이 너무 커서 64비트 정수로 표현할 수 없는 숫자는 제외됩니다.  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상  
  
 ' string '  
 조건자 비교에 필요한 ANSI 또는 유니코드 문자열입니다. 조건자 비교 함수에 대해서는 암시적 문자열 유형 변환이 수행되지 않습니다. 잘못된 유형을 전달하면 오류가 발생합니다.  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상  
  
## <a name="remarks"></a>설명  
 ALTER AUDIT를 호출할 때는 TO, WITH 또는 MODIFY NAME 절 중 하나 이상을 지정해야 합니다.  
  
 감사를 변경하려면 감사 상태를 OFF 옵션으로 설정해야 합니다. 감사가 STATE=OFF 외의 옵션으로 설정되었을 때 ALTER AUDIT를 실행하면 MSG_NEED_AUDIT_DISABLED 오류 메시지가 표시됩니다.  
  
 감사를 중지하지 않고 감사 사양을 추가, 변경 및 제거할 수 있습니다.  
  
 감사를 만든 후에는 감사의 GUID를 변경할 수 없습니다.  
 
 사용자 트랜잭션 내에서는 **ALTER SERVER AUDIT** 문을 사용할 수 없습니다.
 
## <a name="permissions"></a>사용 권한  
 서버 감사 보안 주체를 생성, 변경 또는 삭제하려면 ALTER ANY SERVER AUDIT 또는 CONTROL SERVER 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-a-server-audit-name"></a>A. 서버 감사 이름 변경  
 다음 예에서는 서버 감사 이름 `HIPAA_Audit`를 `HIPAA_Audit_Old`로 변경합니다.  
  
```  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
MODIFY NAME = HIPAA_Audit_Old;  
GO  
ALTER SERVER AUDIT HIPAA_Audit_Old  
WITH (STATE = ON);  
GO  
```  
  
### <a name="b-changing-a-server-audit-target"></a>B. 서버 감사 대상 변경  
 다음 예에서는 `HIPAA_Audit`라는 서버 감사를 파일 대상으로 변경합니다.  
  
```  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
TO FILE (FILEPATH ='\\SQLPROD_1\Audit\',  
          MAXSIZE = 1000 MB,  
          RESERVE_DISK_SPACE=OFF)  
WITH (QUEUE_DELAY = 1000,  
       ON_FAILURE = CONTINUE);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = ON);  
GO  
```  
  
### <a name="c-changing-a-server-audit-where-clause"></a>C. 서버 감사 WHERE 절 변경  
 다음 예에서는 [CREATE SERVER AUDIT&#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)의 예 C에서 만든 WHERE 절을 수정합니다. 새 WHERE 절은 사용자 정의 이벤트가 27인 경우 필터링합니다.  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
WHERE user_defined_event_id = 27;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="d-removing-a-where-clause"></a>D. WHERE 절 제거  
 다음 예에서는 WHERE 절 조건자 식을 제거합니다.  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
REMOVE WHERE;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="e-renaming-a-server-audit"></a>E. 서버 감사 이름 바꾸기  
 다음 예에서는 서버 감사 이름을 `FilterForSensitiveData`에서 `AuditDataAccess`로 변경합니다.  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
MODIFY NAME = AuditDataAccess;  
GO  
ALTER SERVER AUDIT [AuditDataAccess] WITH (STATE = ON);  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
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
 [서버 감사 및 서버 감사 사양 만들기](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
