---
description: sys.dm_exec_sessions(Transact-SQL)
title: sys. dm_exec_sessions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_sessions_TSQL
- sys.dm_exec_sessions
- dm_exec_sessions
- sys.dm_exec_sessions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_sessions dynamic management view
ms.assetid: 2b7e8e0c-eea0-431e-819f-8ccd12ec8cfa
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d160be9c71c75e58a892f4b43494046b293caeb6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539452"
---
# <a name="sysdm_exec_sessions-transact-sql"></a>sys.dm_exec_sessions(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 인증된 세션당 행 하나를 반환합니다. sys.dm_exec_sessions는 모든 활성 사용자 연결 및 내부 태스크에 대한 정보를 표시하는 서버 범위 뷰입니다. 이 정보에는 클라이언트 버전, 클라이언트 프로그램 이름, 클라이언트 로그인 시간, 로그인 사용자, 현재 세션 설정 등이 포함됩니다. sys.dm_exec_sessions를 사용하여 우선 현재 시스템 로드를 보고 원하는 세션을 확인한 다음 다른 동적 관리 뷰 또는 동적 관리 함수를 사용하여 해당 세션에 대한 자세한 내용을 볼 수 있습니다.  
  
 Dm_exec_connections, dm_exec_sessions 및 sys. dm_exec_requests 동적 관리 뷰는 [sys.sys프로세스](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) 시스템 테이블에 매핑됩니다.  
  
> **참고:** 또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_exec_sessions**을 사용 합니다.  
  
|열 이름|데이터 형식|설명 및 버전별 정보|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|각각의 기본 활성 연결과 연결된 세션을 식별합니다. Null을 허용하지 않습니다.|  
|login_time|**datetime**|세션이 설정된 시간입니다. Null을 허용하지 않습니다. 이 DMV를 쿼리할 때 로그인을 완료 하지 않은 세션은 로그인 시간으로 표시 됩니다 `1900-01-01` .|  
|host_name|**nvarchar(128)**|세션에 따라 달라지는 클라이언트 워크스테이션의 이름입니다. 내부 세션에 대한 값은 NULL입니다. Null을 허용합니다.<br /><br /> **보안 정보:** 클라이언트 응용 프로그램은 워크스테이션 이름을 제공 하며 부정확 한 데이터를 제공할 수 있습니다. HOST_NAME을 보안 용도로는 사용하지 마세요.|  
|program_name|**nvarchar(128)**|세션을 시작한 클라이언트 프로그램의 이름입니다. 내부 세션에 대한 값은 NULL입니다. Null을 허용합니다.|  
|host_process_id|**int**|세션을 시작한 클라이언트 프로그램의 프로세스 ID입니다. 내부 세션에 대한 값은 NULL입니다. Null을 허용합니다.|  
|client_version|**int**|클라이언트가 서버에 연결하는 데 사용하는 TDS 프로토콜 버전의 인터페이스입니다. 내부 세션에 대한 값은 NULL입니다. Null을 허용합니다.|  
|client_interface_name|**nvarchar(32)**|클라이언트에서 서버와 통신 하는 데 사용 하는 라이브러리/드라이버의 이름입니다. 내부 세션에 대한 값은 NULL입니다. Null을 허용합니다.|  
|security_id|**varbinary(85)**|로그인과 연결된 Microsoft Windows 보안 ID입니다. Null을 허용하지 않습니다.|  
|login_name|**nvarchar(128)**|현재 세션을 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름입니다. 세션을 만든 원래 로그인 이름은 original_login_name을 참조하십시오. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인증 된 로그인 이름 또는 Windows 인증 된 도메인 사용자 이름일 수 있습니다. Null을 허용하지 않습니다.|  
|nt_domain|**nvarchar(128)**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 세션에서 Windows 인증 또는 트러스트된 연결을 사용하는 경우 클라이언트의 Windows 도메인입니다. 내부 세션 및 비도메인 사용자에 대한 값은 NULL입니다. Null을 허용합니다.|  
|nt_user_name|**nvarchar(128)**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 세션에서 Windows 인증 또는 트러스트된 연결을 사용하는 경우 클라이언트의 Windows 사용자 이름입니다. 내부 세션 및 비도메인 사용자에 대한 값은 NULL입니다. Null을 허용합니다.|  
|상태|**nvarchar(30)**|세션 상태입니다. 가능한 값은 다음과 같습니다.<br /><br /> **실행 중** - 현재 하나 이상의 요청을 실행 중입니다.<br /><br /> **중지 중** - 현재 실행 중인 요청이 없습니다.<br /><br /> 연결 풀링은 현재 사전 로그인 상태 이므로 **유휴** 상태에서 세션이 다시 설정 되었습니다.<br /><br /> **Preconnect** - 세션은 리소스 관리자의 분류자에 있습니다.<br /><br /> Null을 허용하지 않습니다.|  
|context_info|**varbinary(128)**|세션의 CONTEXT_INFO 값입니다. 컨텍스트 정보는 [set CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md) 문을 사용 하 여 사용자가 설정 합니다. Null을 허용합니다.|  
|cpu_time|**int**|이 세션에서 사용한 CPU 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|memory_usage|**int**|이 세션에서 사용한 8KB 메모리 페이지 수입니다. Null을 허용하지 않습니다.|  
|total_scheduled_time|**int**|세션(세션 내 요청)이 실행되도록 예약된 총 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|total_elapsed_time|**int**|세션을 설정한 후 경과된 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|endpoint_id|**int**|세션과 연관된 엔드포인트의 ID입니다. Null을 허용하지 않습니다.|  
|last_request_start_time|**datetime**|세션에서 마지막 요청이 시작된 시간입니다. 여기에는 현재 실행 중인 요청이 포함됩니다. Null을 허용하지 않습니다.|  
|last_request_end_time|**datetime**|세션에서 마지막 요청이 완료된 시간입니다. Null을 허용합니다.|  
|reads|**bigint**|이 세션을 수행하는 동안 해당 세션의 요청에 의해 수행된 읽기 수입니다. Null을 허용하지 않습니다.|  
|writes|**bigint**|이 세션을 수행하는 동안 해당 세션의 요청에 의해 수행된 쓰기 수입니다. Null을 허용하지 않습니다.|  
|logical_reads|**bigint**|세션에서 수행된 논리적 읽기 수입니다. Null을 허용하지 않습니다.|  
|is_user_process|**bit**|시스템 세션인 경우에는 0이고, 그렇지 않으면 1입니다. Null을 허용하지 않습니다.|  
|text_size|**int**|세션에 대한 TEXTSIZE 설정입니다. Null을 허용하지 않습니다.|  
|language|**nvarchar(128)**|세션에 대한 LANGUAGE 설정입니다. Null을 허용합니다.|  
|date_format|**nvarchar (3)**|세션에 대한 DATEFORMAT 설정입니다. Null을 허용합니다.|  
|date_first|**smallint**|세션에 대한 DATEFIRST 설정입니다. Null을 허용하지 않습니다.|  
|quoted_identifier|**bit**|세션에 대한 QUOTED_IDENTIFIER 설정입니다. Null을 허용하지 않습니다.|  
|arithabort|**bit**|세션에 대한 ARITHABORT 설정입니다. Null을 허용하지 않습니다.|  
|ansi_null_dflt_on|**bit**|세션에 대한 ANSI_NULL_DFLT_ON 설정입니다. Null을 허용하지 않습니다.|  
|ansi_defaults|**bit**|세션에 대한 ANSI_DEFAULTS 설정입니다. Null을 허용하지 않습니다.|  
|ansi_warnings|**bit**|세션에 대한 ANSI_WARNINGS 설정입니다. Null을 허용하지 않습니다.|  
|ansi_padding|**bit**|세션에 대한 ANSI_PADDING 설정입니다. Null을 허용하지 않습니다.|  
|ansi_nulls|**bit**|세션에 대한 ANSI_NULLS 설정입니다. Null을 허용하지 않습니다.|  
|concat_null_yields_null|**bit**|세션에 대한 CONCAT_NULL_YIELDS_NULL 설정입니다. Null을 허용하지 않습니다.|  
|transaction_isolation_level|**smallint**|세션의 트랜잭션 격리 수준입니다.<br /><br /> 0 = 지정되지 않음<br /><br /> 1 = ReadUncommitted<br /><br /> 2 = 커밋된 읽기<br /><br /> 3 = RepeatableRead<br /><br /> 4 = 직렬화 가능<br /><br /> 5 = 스냅샷<br /><br /> Null을 허용하지 않습니다.|  
|lock_timeout|**int**|세션에 대한 LOCK_TIMEOUT 설정입니다. 값은 밀리초 단위입니다. Null을 허용하지 않습니다.|  
|deadlock_priority|**int**|세션에 대한 DEADLOCK_PRIORITY 설정입니다. Null을 허용하지 않습니다.|  
|row_count|**bigint**|세션에서 지금까지 반환된 행 수입니다. Null을 허용하지 않습니다.|  
|prev_error|**int**|세션에서 반환된 마지막 오류의 ID입니다. Null을 허용하지 않습니다.|  
|original_security_id|**varbinary(85)**|original_login_name과 연결된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 보안 ID입니다. Null을 허용하지 않습니다.|  
|original_login_name|**nvarchar(128)**|클라이언트가 이 세션을 만드는 데 사용한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인 이름, Windows 인증 도메인 사용자 이름 또는 포함된 데이터베이스 사용자일 수 있습니다. 초기 연결 이후 세션에서 암시적 또는 명시적인 많은 컨텍스트 전환이 수행되었을 수 있습니다. 예를 들어 [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) 를 사용 하는 경우입니다. Null을 허용하지 않습니다.|  
|last_successful_logon|**datetime**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 현재 세션이 시작되기 전에 original_login_name에 대해 마지막으로 성공한 로그온 시간입니다.|  
|last_unsuccessful_logon|**datetime**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 현재 세션이 시작되기 전에 original_login_name에 대해 마지막으로 실패한 로그온 시간입니다.|  
|unsuccessful_logons|**bigint**|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> original_login_name에 대해 last_successful_logon과 login_time 사이에 실패한 로그온 시도 횟수입니다.|  
|group_id|**int**|이 세션이 속한 작업 그룹의 ID입니다. Null을 허용하지 않습니다.|  
|database_id|**smallint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 각 세션에 대한 현재 데이터베이스의 ID입니다.|  
|authenticating_database_id|**int**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 보안 주체를 인증하는 데이터베이스의 ID입니다. 로그인의 경우 값이 0이 됩니다. 포함된 데이터베이스 사용자의 경우 값은 포함된 데이터베이스의 데이터베이스 ID가 됩니다.|  
|open_transaction_count|**int**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 세션당 열린 트랜잭션 수입니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
|page_server_reads|**bigint**|**적용 대상**: Azure SQL Database hyperscale<br /><br /> 이 세션 중에이 세션의 요청에 의해 수행 된 페이지 서버 읽기 수입니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
누구나 자신의 세션 정보를 볼 수 있습니다.  
** [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] :** `VIEW SERVER STATE` [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 서버의 모든 세션을 보려면에 대 한 권한이 필요 합니다.  
** [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] :** 를 사용 `VIEW DATABASE STATE` 하 여 현재 데이터베이스에 대 한 모든 연결을 확인 합니다. `VIEW DATABASE STATE` 데이터베이스에서를 부여할 수 없습니다 `master` . 
  
  
## <a name="remarks"></a>설명  
 **Common criteria 호환성 사용** 서버 구성 옵션을 설정 하면 다음 열에 로그온 통계가 표시 됩니다.  
  
-   last_successful_logon  
  
-   last_unsuccessful_logon  
  
-   unsuccessful_logons  
  
 이 옵션이 설정되지 않은 경우 이러한 열에 Null 값이 반환됩니다. 이 서버 구성 옵션을 설정 하는 방법에 대 한 자세한 내용은 [common criteria 호환성 사용 서버 구성 옵션](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)을 참조 하세요.  
 
 
 Azure SQL Database에 대 한 관리 연결에는 인증 된 세션별 하나의 행이 표시 됩니다. 결과 집합에 표시 되는 "sa" 세션은 세션의 사용자 할당량에 영향을 주지 않습니다. 관리자가 아닌 연결에는 해당 데이터베이스 사용자 세션과 관련 된 정보만 표시 됩니다.
 
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|시작|대상|열 이름/APPLY|관계|  
|----------|--------|---------------|------------------|  
|sys.dm_exec_sessions|[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|session_id|일 대 영 또는 일 대 다|  
|sys.dm_exec_sessions|[sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)|session_id|일 대 영 또는 일 대 다|  
|sys.dm_exec_sessions|[sys.dm_tran_session_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)|session_id|일 대 영 또는 일 대 다|  
|sys.dm_exec_sessions|[dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)(session_id &#124; 0)|session_id CROSS APPLY<br /><br /> OUTER APPLY|일 대 영 또는 일 대 다|  
|sys.dm_exec_sessions|[sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)|session_id|일대일|  
  
## <a name="examples"></a>예제  
  
### <a name="a-finding-users-that-are-connected-to-the-server"></a>A. 서버에 연결된 사용자 찾기  
 다음 예에서는 서버에 연결되는 사용자를 찾고 각 사용자에 대한 세션 수를 반환합니다.  
  
```sql  
SELECT login_name ,COUNT(session_id) AS session_count   
FROM sys.dm_exec_sessions   
GROUP BY login_name;  
```  
  
### <a name="b-finding-long-running-cursors"></a>B. 장기 실행 커서 찾기  
 다음 예에서는 지정한 시간을 초과하여 열려 있는 커서, 해당 커서를 만든 사람 및 해당 커서가 있는 세션을 찾습니다.  
  
```sql  
USE master;  
GO  
SELECT creation_time ,cursor_id   
    ,name ,c.session_id ,login_name   
FROM sys.dm_exec_cursors(0) AS c   
JOIN sys.dm_exec_sessions AS s   
   ON c.session_id = s.session_id   
WHERE DATEDIFF(mi, c.creation_time, GETDATE()) > 5;  
```  
  
### <a name="c-finding-idle-sessions-that-have-open-transactions"></a>C. 열려 있는 트랜잭션이 있는 유휴 세션 찾기  
 다음 예에서는 열려 있는 트랜잭션이 있는 유휴 세션을 찾습니다. 유휴 세션은 현재 실행되고 있는 요청이 없는 세션입니다.  
  
```sql  
SELECT s.*   
FROM sys.dm_exec_sessions AS s  
WHERE EXISTS   
    (  
    SELECT *   
    FROM sys.dm_tran_session_transactions AS t  
    WHERE t.session_id = s.session_id  
    )  
    AND NOT EXISTS   
    (  
    SELECT *   
    FROM sys.dm_exec_requests AS r  
    WHERE r.session_id = s.session_id  
    );  
```  
  
### <a name="d-finding-information-about-a-queries-own-connection"></a>D. 쿼리 자체 연결에 대한 정보 찾기  
 쿼리 자체 연결에 대한 정보를 수집하는 일반 쿼리입니다.  
  
```sql  
SELECT   
    c.session_id, c.net_transport, c.encrypt_option,   
    c.auth_scheme, s.host_name, s.program_name,   
    s.client_interface_name, s.login_name, s.nt_domain,   
    s.nt_user_name, s.original_login_name, c.connect_time,   
    s.login_time   
FROM sys.dm_exec_connections AS c  
JOIN sys.dm_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = @@SPID;  
```  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  



