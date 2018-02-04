---
title: sys.fn_get_audit_file (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_get_audit_file_TSQL
- sys.fn_get_audit_file_TSQL
- fn_get_audit_file
- sys.fn_get_audit_file
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_get_audit_file function
- fn_get_audit_file function
ms.assetid: d6a78d14-bb1f-4987-b7b6-579ddd4167f5
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: efaffab66cba6d95d76d7c5371e43db1aca9f744
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysfngetauditfile-transact-sql"></a>sys.fn_get_audit_file(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 서버 감사에 의해 생성된 감사 파일로부터 정보를 반환합니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
fn_get_audit_file ( file_pattern,   
    { default | initial_file_name | NULL },   
    { default | audit_record_offset | NULL } )  
```  
  
## <a name="arguments"></a>인수  
 *file_pattern*  
 읽을 감사 파일 집합의 디렉터리나 경로와 파일 이름을 지정합니다. 형식이 **nvarchar (260)**합니다. 
 
 - **SQL Server**:
    
    이 인수에는 경로와 파일 이름이 모두 포함되어야 합니다. 드라이브 문자나 네트워크 공유를 경로로 사용할 수 있으며, 파일 이름에 와일드카드를 사용할 수 있습니다. 감사 파일 집합에서 여러 파일을 수집 하도록 단일 별표 (*)를 사용할 수 있습니다. 예를 들어  
  
    -   **\<경로 >\\ \***  수집-모든 지정 된 위치에 있는 파일을 감사 합니다.  
  
    -   **\<경로 > \LoginsAudit_{GUID}** 수집-모든 지정 된 이름 및 GUID 쌍 파일을 감사 합니다.  
  
    -   **\<경로 > \LoginsAudit_{GUID}_00_29384.sqlaudit** -특정 감사 파일을 수집 합니다.  
  
 - **Azure SQL 데이터베이스**:
 
    (저장소 끝점 및 컨테이너 포함) blob URL을 지정 하려면이 인수가 사용 됩니다. 별표 와일드 카드를 지원 하지 않는 동안에이 접두사로 시작 하는 여러 파일 (blob)을 수집 하도록 전체 blob 이름) (대신 부분 (blob) 파일 이름 접두사를 사용할 수 있습니다. 예를 들어
 
      - **\<Storage_endpoint\>/\<컨테이너\>/\<ServerName\>/\<DatabaseName\> /**  -특정 데이터베이스에 대 한 모든 감사 파일 (blob)을 수집 합니다.    
      
      - **\<Storage_endpoint\>/\<컨테이너\>/\<ServerName\>/\<DatabaseName\> / \<AuditName\>/\<CreationDate\>/\<FileName\>.xel** -특정 감사 파일 (blob)을 수집 합니다.
  
> [!NOTE]  
>  파일 이름 패턴 없이 경로를 전달하면 오류가 생성됩니다.  
  
 *initial_file_name*  
 감사 파일 집합에서 감사 레코드를 읽기 시작할 특정 파일의 경로와 이름을 지정합니다. 형식이 **nvarchar (260)**합니다.  
  
> [!NOTE]  
>  *initial_file_name* 인수에 유효한 항목이 또는 기본 있어야 합니다. | NULL 값입니다.  
  
 *audit_record_offset*  
 initial_file_name에 지정된 파일 기준의 오프셋을 지정합니다. 이 인수를 사용하면 함수가 지정된 오프셋 바로 다음에 있는 버퍼의 첫 번째 레코드에서 읽기를 시작합니다.  
  
> [!NOTE]  
>  *audit_record_offset* 인수에 유효한 항목이 또는 기본 있어야 합니다. | NULL 값입니다. 형식이 **bigint**합니다.  
  
## <a name="tables-returned"></a>반환된 테이블  
 다음 표에서는 이 함수가 반환할 수 있는 감사 파일 내용에 대해 설명합니다.  
  
|열 이름|유형|Description|  
|-----------------|----------|-----------------|  
|event_time|**datetime2**|감사 가능한 동작이 발생한 날짜 및 시간입니다. Null을 허용하지 않습니다.|  
|sequence_number|**int**|너무 커서 감사에 대한 쓰기 버퍼에 맞지 않는 단일 감사 레코드 내의 레코드 시퀀스를 추적합니다. Null을 허용하지 않습니다.|  
|action_id|**varchar(4)**|동작의 ID입니다. Null을 허용하지 않습니다.|  
|succeeded|**bit**|이벤트를 발생시킨 동작의 성공 여부를 나타냅니다. Null을 허용하지 않습니다. 로그인 이벤트를 제외한 모든 이벤트의 경우 작업이 아닌 권한 검사의 성공 또는 실패 여부만 보고합니다.<br /> 1 = 성공<br /> 0 = 실패|  
|permission_bitmask|**varbinary(16)**|일부 동작에서 이는 허용, 거부 또는 취소된 사용 권한입니다.|  
|is_column_permission|**bit**|열 수준 사용 권한임을 나타내는 플래그입니다. Null을 허용하지 않습니다. permission_bitmask가 0이면 0을 반환합니다.<br /> 1 = true<br /> 0 = false|  
|session_id|**smallint**|이벤트가 발생한 세션의 ID입니다. Null을 허용하지 않습니다.|  
|server_principal_id|**int**|동작을 수행한 로그인 컨텍스트의 ID입니다. Null을 허용하지 않습니다.|  
|database_principal_id|**int**|동작을 수행한 데이터베이스 사용자 컨텍스트의 ID입니다. Null을 허용하지 않습니다. 이것이 적용되지 않으면 0을 반환합니다(예: 서버 작업).|  
|target_server_principal_id|**int**|GRANT/DENY/REVOKE 작업이 수행되는 서버 보안 주체입니다. Null을 허용하지 않습니다. 적용되지 않으면 0을 반환합니다.|  
|target_database_principal_id|**int**|GRANT/DENY/REVOKE 작업이 수행되는 데이터베이스 보안 주체입니다. Null을 허용하지 않습니다. 적용되지 않으면 0을 반환합니다.|  
|object_id|**int**|감사가 수행된 대상 엔터티의 ID입니다. 여기에는 다음이 포함됩니다.<br /> 서버 개체<br /> 데이터베이스<br /> 데이터베이스 개체<br /> 스키마 개체<br /> Null을 허용하지 않습니다. 엔터티가 서버 자체이거나 개체 수준에서 감사가 수행되지 않으면 0을 반환합니다(예: 인증).|  
|class_type|**varchar(2)**|감사가 수행되는 감사 가능한 엔터티의 형식입니다. Null을 허용하지 않습니다.|  
|session_server_principal_name|**sysname**|세션에 대한 서버 보안 주체입니다. Null을 허용합니다.|  
|server_principal_name|**sysname**|현재 로그인입니다. Null을 허용합니다.|  
|server_principal_sid|**varbinary**|현재 로그인 SID입니다. Null을 허용합니다.|  
|database_principal_name|**sysname**|현재 사용자입니다. Null을 허용합니다. 사용할 수 없으면 NULL을 반환합니다.|  
|target_server_principal_name|**sysname**|동작의 대상 로그인입니다. Null을 허용합니다. 적용할 수 없으면 NULL을 반환합니다.|  
|target_server_principal_sid|**varbinary**|대상 로그인의 SID입니다. Null을 허용합니다. 적용할 수 없으면 NULL을 반환합니다.|  
|target_database_principal_name|**sysname**|동작의 대상 사용자입니다. Null을 허용합니다. 적용할 수 없으면 NULL을 반환합니다.|  
|server_instance_name|**sysname**|감사가 수행된 서버 인스턴스의 이름입니다. 표준 서버\인스턴스 형식을 사용합니다.|  
|database_name|**sysname**|동작이 수행된 데이터베이스 컨텍스트입니다. Null을 허용합니다. 서버 수준에서 수행되는 감사에 대해 NULL을 반환합니다.|  
|schema_name|**sysname**|동작이 수행된 스키마 컨텍스트입니다. Null을 허용합니다. 스키마 외부에서 수행되는 감사에 대해 NULL을 반환합니다.|  
|object_name|**sysname**|감사가 수행된 대상 엔터티의 이름입니다. 여기에는 다음이 포함됩니다.<br /> 서버 개체<br /> 데이터베이스<br /> 데이터베이스 개체<br /> 스키마 개체<br /> Null을 허용합니다. 엔터티가 서버 자체이거나 개체 수준에서 감사가 수행되지 않으면 Null을 반환합니다(예: 인증).|  
|statement|**nvarchar(4000)**|TSQL 문이 있는 경우 TSQL 문입니다. Null을 허용합니다. 적용할 수 없으면 NULL을 반환합니다.|  
|additional_information|**nvarchar(4000)**|단일 이벤트에만 적용되는 고유 정보가 XML로 반환됩니다. 감사 가능한 적은 수의 동작에 이 종류의 정보가 포함되어 있습니다.<br /><br /> TSQL 스택이 연결되어 있는 동작에 대해 단일 TSQL 스택 수준이 XML 형식으로 표시됩니다. 이 XML 형식은 다음과 같습니다.<br /><br /> `<tsql_stack><frame nest_level = '%u' database_name = '%.*s' schema_name = '%.*s' object_name = '%.*s' /></tsql_stack>`<br /><br /> 프레임 nest_level은 프레임의 현재 중첩 수준을 나타냅니다. 모듈 이름은 세 부분(database_name, schema_name, object_name)으로 된 형식으로 표시됩니다.  모듈 이름 처럼 잘못 된 xml 문자를 이스케이프 처리를 구문 분석 됩니다 `'\<'`, `'>'`, `'/'`, `'_x'`합니다. 로 이스케이프 됩니다 `_xHHHH\_`합니다. HHHH는 해당 문자에 대한 4자리 16진수 UCS-2 코드를 나타냅니다.<br /><br /> Null을 허용합니다. 이벤트에서 보고한 추가 정보가 없으면 NULL을 반환합니다.|  
|file_name|**varchar(260)**|레코드를 가져온 감사 로그 파일의 경로 및 이름입니다. Null을 허용하지 않습니다.|  
|audit_file_offset|**bigint**|감사 레코드가 포함된 파일의 버퍼 오프셋입니다. Null을 허용하지 않습니다.|  
|user_defined_event_id|**smallint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 사용자 정의 이벤트 id에 대 한 인수로 전달 된 **sp_audit_write**합니다. **NULL** 시스템 이벤트 (기본값)에 대 한 및 0이 아닌 사용자 정의 이벤트에 대 한 합니다. 자세한 내용은 참조 [sp_audit_write &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md).|  
|user_defined_information|**nvarchar(4000)**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 사용자가을에 기록 하려는 추가 정보를 기록 하는 데 사용 |사용 하 여 감사 로그는 **sp_audit_write** 저장 프로시저입니다.|  
|audit_schema_version |**int** | |  
|sequence_group_id |**varbinary** | SQL Server만 (2016부터 시작) |  
|transaction_id |**bigint** | SQL Server만 (2016부터 시작) |  
|client_ip |**nvarchar(128)** | Azure SQL DB + SQL Server (2017부터 시작) |  
|application_name |**nvarchar(128)** | Azure SQL DB + SQL Server (2017부터 시작) |  
|duration_milliseconds |**bigint** | Azure SQL DB에만 |  
|response_rows |**bigint** | Azure SQL DB에만 |  
|affected_rows |**bigint** | Azure SQL DB에만 |  
  
## <a name="remarks"></a>주의  
 경우는 *file_pattern* 인수에 전달 된 **fn_get_audit_file** 존재 하지 않는 파일 또는 경로 참조 하거나 파일이 감사 파일이 없으면는 **MSG_INVALID_AUDIT_FILE**오류 메시지가 반환 됩니다.  
  
## <a name="permissions"></a>Permissions  
 - **SQL Server**: 필요는 **제어 서버** 권한.  
 - **Azure SQL DB**: 필요는 **제어 데이터베이스** 권한.     
    - 서버 관리자는 서버의 모든 데이터베이스의 감사 로그에 액세스할 수 있습니다.
    - 비 서버 관리자는 현재 데이터베이스에서 감사 로그만 액세스할 수 있습니다.
    - 앞의 조건을 충족 하지 않는 blob 건너뜁니다 (건너뛴 blob 목록에에서 나타납니다 쿼리 출력 메시지)를 함수 액세스 허용 되는 blob 에서만에서 로그를 반환 합니다.  
  
## <a name="examples"></a>예

- **SQL Server**

  다음 예에서는 이름이 `\\serverName\Audit\HIPPA_AUDIT.sqlaudit`인 파일에서 읽습니다.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('\\serverName\Audit\HIPPA_AUDIT.sqlaudit',default,default);  
  GO  
  ```  

- **Azure SQL Database**

  이 예에서는 라는 파일에서 읽는 `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`:  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  이 예에서는 위와 하지만 추가 T-SQL 절과 함께 동일한 파일에서 읽습니다 (**TOP**, **ORDER BY**, 및 **여기서** 절에서 반환 된 감사 레코드를 필터링에 함수 사용):
  
  ```  
  SELECT TOP 10 * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default)
  WHERE server_principal_name = 'admin1'
  ORDER BY event_time
  GO
  ```  

  이 예제에서는 모든 감사 로그가로 시작 하는 서버에서 읽고 `Sh`: 
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```

감사를 만드는 방법에 대 한 전체 예제를 보려면 [SQL Server Audit &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)합니다.

Azure SQL 데이터베이스 감사를 설정에 대 한 자세한 내용은 참조 하십시오. [SQL 데이터베이스 감사 시작](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing)합니다.
  
## <a name="see-also"></a>관련 항목:  
 [서버 감사 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER audit&#40; Transact SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER audit&#40; Transact SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [SERVER AUDIT specification&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT specification&#40; Transact SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT specification&#40; Transact SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [DATABASE AUDIT specification&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT specification&#40; Transact SQL &#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT specification&#40; Transact SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER authorization&#40; Transact SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.server_audits&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [서버 감사 및 서버 감사 사양 만들기](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
