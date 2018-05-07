---
title: sys.dm_exec_requests (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_requests_TSQL
- sys.dm_exec_requests
- dm_exec_requests_TSQL
- dm_exec_requests
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_requests dynamic management view
ms.assetid: 4161dc57-f3e7-4492-8972-8cfb77b29643
caps.latest.revision: 67
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7ccde675a7a5efe64547c7ef45c8e1150d102603
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmexecrequests-transact-sql"></a>sys.dm_exec_requests(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행 중인 각 요청에 대한 정보를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외부의 코드(예: 확장 저장 프로시저 및 분산 쿼리)를 실행하려면 비선점형 스케줄러의 제어를 벗어나서 스레드를 실행해야 합니다. 작업자는 이 작업을 수행하기 위해 선점형 모드로 전환합니다. 이 동적 관리 뷰에서 반환된 시간 값은 선점형 모드에서 사용된 시간을 포함하지 않습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|이 요청과 관련된 세션의 ID입니다. Null을 허용하지 않습니다.|  
|request_id|**int**|요청의 ID입니다. 세션의 컨텍스트에서 고유합니다. Null을 허용하지 않습니다.|  
|start_time|**datetime**|요청이 도착한 타임스탬프입니다. Null을 허용하지 않습니다.|  
|상태|**nvarchar(30)**|요청의 상태입니다. 다음 중 하나일 수 있습니다.<br /><br /> 배경<br />실행 중<br />실행 가능<br />중지 중<br />일시 중지됨<br /><br /> Null을 허용하지 않습니다.|  
|command|**nvarchar(32)**|처리되고 있는 명령의 현재 유형을 식별합니다. 일반 명령 유형은 다음과 같습니다.<br /><br /> SELECT<br />INSERT<br />UPDATE<br />DELETE<br />BACKUP LOG<br />BACKUP DATABASE<br />DBCC<br />FOR<br /><br /> 요청 텍스트는 요청에 대한 해당 sql_handle과 함께 sys.dm_exec_sql_text를 사용하여 검색할 수 있습니다. 내부 시스템 프로세스는 수행하는 태스크 유형에 따라 명령을 설정합니다. 태스크는 다음과 같습니다.<br /><br /> LOCK MONITOR<br />CHECKPOINTLAZY<br />WRITER<br /><br /> Null을 허용하지 않습니다.|  
|sql_handle|**varbinary(64)**|요청에 대한 SQL 텍스트의 해시 맵입니다. Null을 허용합니다.|  
|statement_start_offset|**int**|현재 실행 중인 일괄 처리 또는 저장 프로시저에서 현재 실행 중인 문이 시작되는 위치까지의 문자 수입니다. sql_handle, statement_end_offset 및 sys.dm_exec_sql_text 동적 관리 함수와 함께 사용하여 요청에 대해 현재 실행 중인 문을 검색할 수 있습니다. Null을 허용합니다.|  
|statement_end_offset|**int**|현재 실행 중인 일괄 처리 또는 저장 프로시저에서 현재 실행 중인 문이 종료되는 위치까지의 문자 수입니다. sql_handle, statement_end_offset 및 sys.dm_exec_sql_text 동적 관리 함수와 함께 사용하여 요청에 대해 현재 실행 중인 문을 검색할 수 있습니다. Null을 허용합니다.|  
|plan_handle|**varbinary(64)**|SQL 실행을 위한 계획의 해시 맵입니다. Null을 허용합니다.|  
|database_id|**smallint**|요청을 실행 중인 대상 데이터베이스의 ID입니다. Null을 허용하지 않습니다.|  
|user_id|**int**|요청을 제출한 사용자의 ID입니다. Null을 허용하지 않습니다.|  
|connection_id|**uniqueidentifier**|요청이 도착한 연결의 ID입니다. Null을 허용합니다.|  
|blocking_session_id|**smallint**|요청을 차단하고 있는 세션의 ID입니다. 이 열이 NULL이면 요청이 차단되지 않거나 차단 세션의 세션 정보를 사용할 수 없습니다(또는 식별할 수 없음).<br /><br /> -2 = 분리된 분산 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -3 = 지연된 복구 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -4 = 내부 래치 상태 전환 때문에 현재 차단 래치 소유자의 세션 ID를 확인할 수 없습니다.|  
|wait_type|**nvarchar(60)**|요청이 현재 차단된 경우 이 열은 대기 유형을 반환합니다. Null을 허용합니다.<br /><br /> 대기 유형에 대 한 정보를 참조 하십시오. [sys.dm_os_wait_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)합니다.|  
|wait_time|**int**|요청이 현재 차단된 경우 이 열은 현재 대기의 기간(밀리초)을 반환합니다. Null을 허용하지 않습니다.|  
|last_wait_type|**nvarchar(60)**|이 요청이 이전에 차단된 경우 이 열은 마지막 대기의 유형을 반환합니다. Null을 허용하지 않습니다.|  
|wait_resource|**nvarchar(256)**|요청이 현재 차단된 경우 이 열은 요청이 현재 대기하고 있는 리소스를 반환합니다. Null을 허용하지 않습니다.|  
|open_transaction_count|**int**|이 요청에 대해 열린 트랜잭션 수입니다. Null을 허용하지 않습니다.|  
|open_resultset_count|**int**|이 요청에 대해 열린 결과 집합 수입니다. Null을 허용하지 않습니다.|  
|transaction_id|**bigint**|이 요청이 실행되는 트랜잭션의 ID입니다. Null을 허용하지 않습니다.|  
|context_info|**varbinary(128)**|세션의 CONTEXT_INFO 값입니다. Null을 허용합니다.|  
|percent_complete|**real**|다음 명령에 대한 작업 완료율입니다.<br /><br /> ALTER INDEX REORGANIZE<br />ALTER DATABASE의 AUTO_SHRINK 옵션<br />BACKUP DATABASE<br />DBCC CHECKDB<br />DBCC CHECKFILEGROUP<br />DBCC CHECKTABLE<br />DBCC INDEXDEFRAG<br />DBCC SHRINKDATABASE<br />DBCC SHRINKFILE<br />RECOVERY<br />RESTORE DATABASE<br />ROLLBACK<br />TDE ENCRYPTION<br /><br /> Null을 허용하지 않습니다.|  
|estimated_completion_time|**bigint**|내부용입니다. Null을 허용하지 않습니다.|  
|cpu_time|**int**|요청에 사용된 CPU 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|total_elapsed_time|**int**|요청이 도착한 이후 경과한 총 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|scheduler_id|**int**|이 요청을 예약하고 있는 스케줄러의 ID입니다. Null을 허용하지 않습니다.|  
|task_address|**varbinary(8)**|이 요청과 연관된 태스크에 할당된 메모리 주소입니다. Null을 허용합니다.|  
|reads|**bigint**|이 요청에서 수행된 읽기 수입니다. Null을 허용하지 않습니다.|  
|writes|**bigint**|이 요청에서 수행된 쓰기 수입니다. Null을 허용하지 않습니다.|  
|logical_reads|**bigint**|요청에서 수행된 논리적 읽기 수입니다. Null을 허용하지 않습니다.|  
|text_size|**int**|이 요청에 대한 TEXTSIZE 설정입니다. Null을 허용하지 않습니다.|  
|language|**nvarchar(128)**|요청에 대한 언어 설정입니다. Null을 허용합니다.|  
|date_format|**nvarchar(3)**|요청에 대한 DATEFORMAT 설정입니다. Null을 허용합니다.|  
|date_first|**smallint**|요청에 대한 DATEFIRST 설정입니다. Null을 허용하지 않습니다.|  
|quoted_identifier|**bit**|1 = QUOTED_IDENTIFIER가 요청에 대해 ON입니다. 그렇지 않으면 0입니다.<br /><br /> Null을 허용하지 않습니다.|  
|arithabort|**bit**|1 = ARITHABORT 설정이 요청에 대해 ON입니다. 그렇지 않으면 0입니다.<br /><br /> Null을 허용하지 않습니다.|  
|ansi_null_dflt_on|**bit**|1 = ANSI_NULL_DFLT_ON 설정이 요청에 대해 ON입니다. 그렇지 않으면 0입니다.<br /><br /> Null을 허용하지 않습니다.|  
|ansi_defaults|**bit**|1 = ANSI_DEFAULTS 설정이 요청에 대해 ON입니다. 그렇지 않으면 0입니다.<br /><br /> Null을 허용하지 않습니다.|  
|ansi_warnings|**bit**|1 = ANSI_WARNINGS 설정이 요청에 대해 ON입니다. 그렇지 않으면 0입니다.<br /><br /> Null을 허용하지 않습니다.|  
|ansi_padding|**bit**|1 = ANSI_PADDING 설정이 요청에 대해 ON입니다.<br /><br /> 그렇지 않으면 0입니다.<br /><br /> Null을 허용하지 않습니다.|  
|ansi_nulls|**bit**|1 = ANSI_NULLS 설정이 요청에 대해 ON입니다. 그렇지 않으면 0입니다.<br /><br /> Null을 허용하지 않습니다.|  
|concat_null_yields_null|**bit**|1 = CONCAT_NULL_YIELDS_NULL 설정이 요청에 대해 ON입니다. 그렇지 않으면 0입니다.<br /><br /> Null을 허용하지 않습니다.|  
|transaction_isolation_level|**smallint**|이 요청이 만들어진 트랜잭션의 격리 수준을 나타냅니다. Null을 허용하지 않습니다.<br /><br /> 0 = 지정되지 않음<br /><br /> 1 = 커밋되지 않은 읽기<br /><br /> 2 = 커밋된 읽기<br /><br /> 3 = 반복 읽기<br /><br /> 4 = 직렬화 가능<br /><br /> 5 = 스냅숏|  
|lock_timeout|**int**|이 요청에 대한 잠금 제한 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|deadlock_priority|**int**|요청에 대한 DEADLOCK_PRIORITY 설정입니다. Null을 허용하지 않습니다.|  
|row_count|**bigint**|이 요청에서 클라이언트에 반환된 행 수입니다. Null을 허용하지 않습니다.|  
|prev_error|**int**|요청이 실행되는 동안 마지막으로 발생한 오류입니다. Null을 허용하지 않습니다.|  
|nest_level|**int**|요청에서 실행되고 있는 코드의 현재 중첩 수준입니다. Null을 허용하지 않습니다.|  
|granted_query_memory|**int**|요청에서 쿼리의 실행에 할당된 페이지 수입니다. Null을 허용하지 않습니다.|  
|executing_managed_code|**bit**|특정 요청이 루틴, 유형 및 트리거 같은 공용 언어 런타임 개체를 현재 실행하고 있는지 나타냅니다. 공용 언어 런타임 개체가 스택에 있을 때 항상 설정되며 공용 언어 런타임 내에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 실행하는 동안에도 마찬가지입니다. Null을 허용하지 않습니다.|  
|group_id|**int**|이 쿼리가 속한 작업 그룹의 ID입니다. Null을 허용하지 않습니다.|  
|query_hash|**binary(8)**|쿼리에서 계산되는 이진 해시 값으로, 비슷한 논리를 가진 쿼리를 식별하는 데 사용됩니다. 쿼리 해시를 사용하여 리터럴 값만 다른 쿼리에 대한 집계 리소스 사용을 확인할 수 있습니다.|  
|query_plan_hash|**binary(8)**|쿼리 실행 계획에서 계산되는 이진 해시 값으로, 비슷한 쿼리 실행 계획을 식별하는 데 사용됩니다. 쿼리 계획 해시를 사용하여 비슷한 실행 계획을 가진 쿼리의 누적 비용을 찾을 수 있습니다.|  
|statement_sql_handle|**varbinary(64)**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 개별 쿼리의 SQL 핸들입니다. |  
|statement_context_id|**bigint**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> Sys.query_context_settings 선택적 외래 키입니다. |  
|dop |**int** |**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 쿼리의 병렬 처리 수준입니다. |  
|parallel_worker_count |**int** |**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 이 병렬 쿼리 하는 경우 예약 된 병렬 작업자 수입니다.  |  
|external_script_request_id |**uniqueidentifier** |**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 현재 요청과 연결 된 외부 스크립트 요청 ID입니다. |  
|is_resumable |**bit** |**적용 대상**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 요청이 다시 시작 가능한 인덱스 작업 인지를 나타냅니다. |  
  
## <a name="permissions"></a>Permissions  
 사용자에 게 있으면 `VIEW SERVER STATE` 서버 권한, 사용자는 확인할 실행 중인 모든 세션의 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 그렇지 않으면 현재 세션에만 표시 됩니다. `VIEW SERVER STATE` 부여 될 수 없지만 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 있으므로 `sys.dm_exec_requests` 은 항상 현재 연결으로 제한 합니다. 
  
## <a name="examples"></a>예  
  
### <a name="a-finding-the-query-text-for-a-running-batch"></a>1. 실행 중인 일괄 처리에 대한 쿼리 텍스트 찾기  
 다음 예에서는 `sys.dm_exec_requests`를 쿼리하여 필요한 쿼리를 찾고 출력에서 `sql_handle`을 복사합니다.  
  
```  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 그런 다음 문 텍스트를 가져오기 위해 복사한 `sql_handle`을 `sys.dm_exec_sql_text(sql_handle)` 시스템 함수와 함께 사용합니다.  
  
```  
SELECT * FROM sys.dm_exec_sql_text(< copied sql_handle >);  
GO  
```  
  
### <a name="b-finding-all-locks-that-a-running-batch-is-holding"></a>2. 실행 중인 일괄 처리에서 보유하고 있는 모든 잠금 찾기  
 다음 예제 쿼리에서 **sys.dm_exec_requests** 흥미로운 일괄 처리 및 복사를 찾으려면 해당 `transaction_id` 출력에서 합니다.  
  
```  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 그런 다음 잠금 정보를 찾기 위해 사용 하 여 복사 된 `transaction_id` 시스템 함수와 함께 **sys.dm_tran_locks**합니다.  
  
```  
SELECT * FROM sys.dm_tran_locks   
WHERE request_owner_type = N'TRANSACTION'   
    AND request_owner_id = < copied transaction_id >;  
GO  
```  
  
### <a name="c-finding-all-currently-blocked-requests"></a>3. 현재 차단된 모든 요청 찾기  
 다음 예제 쿼리에서 **sys.dm_exec_requests** 차단 된 요청에 대 한 정보를 찾을 수 있습니다.  
  
```  
SELECT session_id ,status ,blocking_session_id  
    ,wait_type ,wait_time ,wait_resource   
    ,transaction_id   
FROM sys.dm_exec_requests   
WHERE status = N'suspended';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_os_memory_clerks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)  
