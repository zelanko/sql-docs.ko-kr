---
title: sys. fn_get_audit_file (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 02/19/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current||=azure-sqldw-latest
ms.openlocfilehash: 4d280a00eb9d972cea510ae650c4598561b77fef
ms.sourcegitcommit: 822d4b3cfa53269535500a3db5877a82b5076728
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87988781"
---
# <a name="sysfn_get_audit_file-transact-sql"></a>sys.fn_get_audit_file(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]    

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 서버 감사에 의해 생성된 감사 파일로부터 정보를 반환합니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
fn_get_audit_file ( file_pattern,   
    { default | initial_file_name | NULL },   
    { default | audit_record_offset | NULL } )  
```  
  
## <a name="arguments"></a>인수  
 *file_pattern*  
 읽을 감사 파일 집합의 디렉터리나 경로와 파일 이름을 지정합니다. 형식이 **nvarchar (260)** 입니다. 
 
 - **SQL Server**:
    
    이 인수에는 경로와 파일 이름이 모두 포함되어야 합니다. 드라이브 문자나 네트워크 공유를 경로로 사용할 수 있으며, 파일 이름에 와일드카드를 사용할 수 있습니다. 단일 별표 (*)를 사용 하 여 감사 파일 집합에서 여러 파일을 수집할 수 있습니다. 예:  
  
    -   **\<path>\\\***-지정 된 위치에 있는 모든 감사 파일을 수집 합니다.  
  
    -   ** \<path> \ LOGINSAUDIT_ {guid}***-지정 된 이름 및 GUID 쌍을 가진 모든 감사 파일을 수집 합니다.  
  
    -   ** \<path> \ LOGINSAUDIT_ {GUID} _00_29384. sqlaudit** -특정 감사 파일을 수집 합니다.  
  
 - **Azure SQL Database**:
 
    이 인수는 blob URL (저장소 끝점 및 컨테이너 포함)을 지정 하는 데 사용 됩니다. 별표 와일드 카드를 지원 하지 않는 경우 전체 blob 이름 대신 부분 파일 (blob) 이름 접두사를 사용 하 여이 접두사로 시작 하는 여러 파일 (blob)을 수집할 수 있습니다. 예:
 
      - **\<Storage_endpoint\>/\<Container\>/\<ServerName\>/\<DatabaseName\>/**-특정 데이터베이스에 대 한 모든 감사 파일 (blob)을 수집 합니다.    
      
      - ** \<Storage_endpoint\> / \<Container\> / \<ServerName\> / \<DatabaseName\> / \<AuditName\> / \<CreationDate\> / \<FileName\> . xel** -특정 감사 파일 (blob)을 수집 합니다.
  
> [!NOTE]  
>  파일 이름 패턴 없이 경로를 전달하면 오류가 생성됩니다.  
  
 *initial_file_name*  
 감사 파일 집합에서 감사 레코드를 읽기 시작할 특정 파일의 경로와 이름을 지정합니다. 형식이 **nvarchar (260)** 입니다.  
  
> [!NOTE]  
>  *Initial_file_name* 인수는 유효한 항목을 포함 하거나 기본값 |을 포함 해야 합니다. NULL 값입니다.  
  
 *audit_record_offset*  
 initial_file_name에 지정된 파일 기준의 오프셋을 지정합니다. 이 인수를 사용하면 함수가 지정된 오프셋 바로 다음에 있는 버퍼의 첫 번째 레코드에서 읽기를 시작합니다.  
  
> [!NOTE]  
>  *Audit_record_offset* 인수는 유효한 항목을 포함 하거나 기본값 |을 포함 해야 합니다. NULL 값입니다. **Bigint**유형입니다.  
  
## <a name="tables-returned"></a>반환된 테이블  
 다음 표에서는 이 함수가 반환할 수 있는 감사 파일 내용에 대해 설명합니다.  
  
| 열 이름 | Type | 설명 |  
|-------------|------|-------------|  
| action_id | **varchar(4)** | 동작의 ID입니다. Null을 허용하지 않습니다. |  
| additional_information | **nvarchar(4000)** | 단일 이벤트에만 적용되는 고유 정보가 XML로 반환됩니다. 감사 가능한 적은 수의 동작에 이 종류의 정보가 포함되어 있습니다.<br /><br /> TSQL 스택이 연결되어 있는 동작에 대해 단일 TSQL 스택 수준이 XML 형식으로 표시됩니다. 이 XML 형식은 다음과 같습니다.<br /><br /> `<tsql_stack><frame nest_level = '%u' database_name = '%.*s' schema_name = '%.*s' object_name = '%.*s' /></tsql_stack>`<br /><br /> 프레임 nest_level은 프레임의 현재 중첩 수준을 나타냅니다. 모듈 이름은 세 부분(database_name, schema_name, object_name)으로 된 형식으로 표시됩니다.  ,,,와 같은 잘못 된 xml 문자를 이스케이프 하기 위해 모듈 이름이 구문 분석 됩니다 `'\<'` `'>'` `'/'` `'_x'` . 로 이스케이프 됩니다 `_xHHHH\_` . HHHH는 해당 문자에 대한 4자리 16진수 UCS-2 코드를 나타냅니다.<br /><br /> Null을 허용합니다. 이벤트에서 보고한 추가 정보가 없으면 NULL을 반환합니다. |
| affected_rows | **bigint** | **적용 대상**: Azure SQL Database에만<br /><br /> 실행 된 문의 영향을 받는 행의 수입니다. |  
| application_name | **nvarchar(128)** | **적용 대상**: Azure SQL Database + SQL Server (2017부터 시작)<br /><br /> 감사 이벤트를 발생 시킨 문을 실행 한 클라이언트 응용 프로그램의 이름입니다. |  
| audit_file_offset | **bigint** | **적용 대상**: SQL Server에만<br /><br /> 감사 레코드가 포함된 파일의 버퍼 오프셋입니다. Null을 허용하지 않습니다. |  
| audit_schema_version | **int** | 항상 1 |  
| class_type | **varchar(2)** | 감사가 수행되는 감사 가능한 엔터티의 형식입니다. Null을 허용하지 않습니다. |  
| client_ip | **nvarchar(128)** | **적용 대상**: Azure SQL Database + SQL Server (2017부터 시작)<br /><br />  클라이언트 응용 프로그램의 원본 IP |  
| connection_id | GUID | **적용**대상: AZURE SQL DATABASE 및 SQL Managed Instance<br /><br /> 서버에 있는 연결의 ID입니다. |
| data_sensitivity_information | nvarchar(4000) | **적용 대상**: Azure SQL Database에만<br /><br /> 데이터베이스의 분류 된 열을 기반으로 감사 된 쿼리에서 반환 되는 정보 유형 및 민감도 레이블입니다. [Azure SQL Database 데이터 검색 및 분류](https://docs.microsoft.com/azure/sql-database/sql-database-data-discovery-and-classification) 에 대 한 자세한 정보 |
| database_name | **sysname** | 동작이 수행된 데이터베이스 컨텍스트입니다. Null을 허용합니다. 서버 수준에서 발생 하는 감사에 대해 NULL을 반환 합니다. |  
| database_principal_id | **int** |동작을 수행한 데이터베이스 사용자 컨텍스트의 ID입니다. Null을 허용하지 않습니다. 이것이 적용되지 않으면 0을 반환합니다(예: 서버 작업).|
| database_principal_name | **sysname** | 현재 사용자입니다. Null을 허용합니다. 사용할 수 없으면 NULL을 반환합니다. |  
| duration_milliseconds | **bigint** | **적용**대상: AZURE SQL DATABASE 및 SQL Managed Instance<br /><br /> 쿼리 실행 기간 (밀리초) |
| event_time | **datetime2** | 감사 가능한 동작이 발생한 날짜 및 시간입니다. Null을 허용하지 않습니다. |  
| file_name | **varchar(260)** | 레코드를 가져온 감사 로그 파일의 경로 및 이름입니다. Null을 허용하지 않습니다. |
| is_column_permission | **bit** | 열 수준 사용 권한임을 나타내는 플래그입니다. Null을 허용하지 않습니다. permission_bitmask가 0이면 0을 반환합니다.<br /> 1 = true<br /> 0 = false |
| object_id | **int** | 감사가 수행된 대상 엔터티의 ID입니다. 여기에는 다음이 포함됩니다.<br /> 서버 개체<br /> 데이터베이스<br /> 데이터베이스 개체<br /> 스키마 개체<br /> Null을 허용하지 않습니다. 엔터티가 서버 자체이거나 개체 수준에서 감사가 수행되지 않으면 0을 반환합니다(예: 인증). |  
| object_name | **sysname** | 감사가 수행된 대상 엔터티의 이름입니다. 여기에는 다음이 포함됩니다.<br /> 서버 개체<br /> 데이터베이스<br /> 데이터베이스 개체<br /> 스키마 개체<br /> Null을 허용합니다. 엔터티가 서버 자체이거나 개체 수준에서 감사가 수행되지 않으면 Null을 반환합니다(예: 인증). |
| permission_bitmask | **varbinary(16)** | 일부 동작에서 이는 허용, 거부 또는 취소된 사용 권한입니다. |
| response_rows | **bigint** | **적용**대상: AZURE SQL DATABASE 및 SQL Managed Instance<br /><br /> 결과 집합에 반환 되는 행의 수입니다. |  
| schema_name | **sysname** | 동작이 수행된 스키마 컨텍스트입니다. Null을 허용합니다. 스키마 외부에서 발생 하는 감사에 대해 NULL을 반환 합니다. |  
| sequence_group_id | **varbinary** | **적용 대상**: SQL Server에만 (2016부터)<br /><br />  고유 식별자 |  
| sequence_number | **int** | 너무 커서 감사에 대한 쓰기 버퍼에 맞지 않는 단일 감사 레코드 내의 레코드 시퀀스를 추적합니다. Null을 허용하지 않습니다. |  
| server_instance_name | **sysname** | 감사가 수행된 서버 인스턴스의 이름입니다. 표준 서버\인스턴스 형식을 사용합니다. |  
| server_principal_id | **int** | 동작을 수행한 로그인 컨텍스트의 ID입니다. Null을 허용하지 않습니다. |  
| server_principal_name | **sysname** | 현재 로그인입니다. Null을 허용합니다. |  
| server_principal_sid | **varbinary** | 현재 로그인 SID입니다. Null을 허용합니다. |  
| session_id | **smallint** | 이벤트가 발생한 세션의 ID입니다. Null을 허용하지 않습니다. |  
| session_server_principal_name | **sysname** | 세션에 대한 서버 보안 주체입니다. Null을 허용합니다. |  
| statement | **nvarchar(4000)** | TSQL 문이 있는 경우 TSQL 문입니다. Null을 허용합니다. 적용할 수 없으면 NULL을 반환합니다. |  
| 성공 | **bit** | 이벤트를 발생시킨 동작의 성공 여부를 나타냅니다. Null을 허용하지 않습니다. 로그인 이벤트를 제외한 모든 이벤트의 경우 작업이 아닌 권한 검사의 성공 또는 실패 여부만 보고합니다.<br /> 1 = 성공<br /> 0 = 실패 |
| target_database_principal_id | **int** | GRANT/DENY/REVOKE 작업이 수행되는 데이터베이스 보안 주체입니다. Null을 허용하지 않습니다. 적용되지 않으면 0을 반환합니다. |  
| target_database_principal_name | **sysname** | 동작의 대상 사용자입니다. Null을 허용합니다. 적용할 수 없으면 NULL을 반환합니다. |  
| target_server_principal_id | **int** | GRANT/DENY/REVOKE 작업이 수행되는 서버 보안 주체입니다. Null을 허용하지 않습니다. 적용되지 않으면 0을 반환합니다. |  
| target_server_principal_name | **sysname** | 동작의 대상 로그인입니다. Null을 허용합니다. 적용할 수 없으면 NULL을 반환합니다. |  
| target_server_principal_sid | **varbinary** | 대상 로그인의 SID입니다. Null을 허용합니다. 적용할 수 없으면 NULL을 반환합니다. |  
| transaction_id | **bigint** | **적용 대상**: SQL Server에만 (2016부터)<br /><br /> 단일 트랜잭션에서 여러 감사 이벤트를 식별 하는 고유 식별자 |  
| user_defined_event_id | **smallint** | **적용**대상: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, Azure SQL Database 및 SQL Managed Instance<br /><br /> **Sp_audit_write**에 인수로 전달 되는 사용자 정의 이벤트 id입니다. 시스템 이벤트 (기본값)의 경우 **NULL** 이 고 사용자 정의 이벤트의 경우 0이 아닙니다. 자세한 내용은 [sp_audit_write &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md)를 참조 하세요. |  
| user_defined_information | **nvarchar(4000)** | **적용**대상: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, Azure SQL Database 및 SQL Managed Instance<br /><br /> 사용자가 **sp_audit_write** 저장 프로시저를 사용 하 여 감사 로그에 기록 하려는 추가 정보를 기록 하는 데 사용 됩니다. |  

  
## <a name="remarks"></a>설명  
 **Fn_get_audit_file** 에 전달 된 *file_pattern* 인수가 존재 하지 않는 경로 또는 파일을 참조 하거나 파일이 감사 파일이 아니면 **MSG_INVALID_AUDIT_FILE** 오류 메시지가 반환 됩니다.  
  
## <a name="permissions"></a>사용 권한

- **SQL Server**: **CONTROL Server** 권한이 필요 합니다.  
- **Azure SQL Database**: **CONTROL Database** 권한이 필요 합니다.     
  - 서버 관리자는 서버에 있는 모든 데이터베이스의 감사 로그에 액세스할 수 있습니다.
  - 이외 서버 관리자는 현재 데이터베이스의 감사 로그에만 액세스할 수 있습니다.
  - 위의 조건을 충족 하지 않는 blob은 건너뜁니다 (건너뛴 blob 목록이 쿼리 출력 메시지에 표시 됨) .이 함수는 액세스가 허용 된 blob 에서만 로그를 반환 합니다.  
  
## <a name="examples"></a>예

- **SQL Server**

  다음 예에서는 이름이 `\\serverName\Audit\HIPAA_AUDIT.sqlaudit`인 파일에서 읽습니다.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('\\serverName\Audit\HIPAA_AUDIT.sqlaudit',default,default);  
  GO  
  ```  

- **Azure SQL Database**

  이 예제에서는 이름이 인 파일에서 읽습니다 `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel` .  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  이 예에서는 위와 동일한 파일에서 읽기를 하지만 함수에서 반환 된 감사 레코드를 필터링 하기 위한 추가 T-sql 절 (**TOP**, **ORDER BY**및 **WHERE** 절)을 사용 합니다.
  
  ```  
  SELECT TOP 10 * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default)
  WHERE server_principal_name = 'admin1'
  ORDER BY event_time
  GO
  ```  

  이 예에서는로 시작 하는 서버에서 모든 감사 로그를 읽습니다 `Sh` . 
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```

감사를 만드는 방법에 대한 전체 예에 대해서는 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)를 참조하십시오.

Azure SQL Database 감사를 설정 하는 방법에 대 한 자세한 내용은 [SQL Database 감사 시작](https://docs.microsoft.com/azure/sql-database/sql-database-auditing)을 참조 하세요.
  
## <a name="see-also"></a>참고 항목  
 [서버 감사 &#40;Transact-sql&#41;만들기](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
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
  
  
