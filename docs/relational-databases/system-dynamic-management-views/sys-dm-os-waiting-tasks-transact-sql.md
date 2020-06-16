---
title: sys. dm_os_waiting_tasks (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_waiting_tasks
- sys.dm_os_waiting_tasks_TSQL
- dm_os_waiting_tasks_TSQL
- sys.dm_os_waiting_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_waiting_tasks dynamic management view
ms.assetid: ca5e6844-368c-42e2-b187-6e5f5afc8df3
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0ab32f364725d11a606ac698fdefb7f9f95a312d
ms.sourcegitcommit: 05fdc50006a9abdda79c3a4685b075796068c4fa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84748250"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  특정 리소스에서 대기 중인 태스크의 대기 큐에 대한 정보를 반환합니다. 작업에 대 한 자세한 내용은 [스레드 및 태스크 아키텍처 가이드](../../relational-databases/thread-and-task-architecture-guide.md)를 참조 하세요.
   
> [!NOTE]  
> 또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_os_waiting_tasks**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|대기 중인 태스크의 주소입니다.|  
|**session_id**|**smallint**|태스크와 연결된 세션의 ID입니다.|  
|**exec_context_id**|**int**|태스크와 연결된 실행 컨텍스트의 ID입니다.|  
|**wait_duration_ms**|**bigint**|이 대기 유형에 대한 총 대기 시간(밀리초)입니다. 이 시간은 **signal_wait_time**포함 됩니다.|  
|**wait_type**|**nvarchar(60)**|대기 유형의 이름입니다.|  
|**resource_address**|**varbinary(8)**|태스크가 대기 중인 리소스의 주소입니다.|  
|**blocking_task_address**|**varbinary(8)**|현재 이 리소스를 보유하고 있는 태스크입니다.|  
|**blocking_session_id**|**smallint**|요청을 차단하고 있는 세션의 ID입니다. 이 열이 NULL이면 요청이 차단되지 않거나 차단 세션의 세션 정보를 사용할 수 없습니다(또는 식별할 수 없음).<br /><br /> -2 = 분리된 분산 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -3 = 지연된 복구 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -4 = 내부 래치 상태 전환 때문에 차단 래치 소유자의 세션 ID를 확인할 수 없습니다.|  
|**blocking_exec_context_id**|**int**|차단 태스크의 실행 컨텍스트 ID입니다.|  
|**resource_description**|**nvarchar (3072)**|사용 중인 리소스에 대한 설명입니다. 자세한 내용은 아래 목록을 참조하십시오.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="resource_description-column"></a>resource_description 열  
 resource_description 열에는 다음 값이 포함될 수 있습니다.  
  
 **스레드 풀 리소스 소유자:**  
  
-   threadpool id = scheduler\<hex-address>  
  
 **병렬 쿼리 리소스 소유자:**  
  
-   exchangeEvent id = {Port | Pipe} \<hex-address> WaitType = \<exchange-wait-type> nodeId =\<exchange-node-id>  
  
 **Exchange-wait-type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **잠금 리소스 소유자:**  
  
-   \<type-specific-description>id = lock \<lock-hex-address> mode = \<mode> associatedObjectId =\<associated-obj-id>  
  
     **\<type-specific-description>다음이 될 수 있습니다.**  
  
    -   데이터베이스: databaselock subresource = \<databaselock-subresource> dbid =\<db-id>  
  
    -   FILE: filelock fileid = \<file-id> subresource = \<filelock-subresource> dbid =\<db-id>  
  
    -   개체: objectlock lockPartition = \<lock-partition-id> objid = \<obj-id> subresource = \<objectlock-subresource> dbid =\<db-id>  
  
    -   PAGE: pagelock fileid = \<file-id> pageid = \<page-id> dbid = \<db-id> subresource =\<pagelock-subresource>  
  
    -   키: 키잠금을 hobtid = \<hobt-id> dbid =\<db-id>  
  
    -   익스텐트의 경우: extentlock fileid = \<file-id> pageid = \<page-id> dbid =\<db-id>  
  
    -   For RID: ridlock fileid = \<file-id> pageid = \<page-id> dbid =\<db-id>  
  
    -   응용 프로그램의 경우: applicationlock hash = \<hash> databaseprincipalid = \<role-id> dbid =\<db-id>  
  
    -   메타 데이터: metadatalock subresource = \<metadata-subresource> classid = \<metadatalock-description> dbid =\<db-id>  
  
    -   HOBT: hobtlock hobtid = \<hobt-id> subresource = \<hobt-subresource> dbid =\<db-id>  
  
    -   ALLOCATION_UNIT: allocunitlock hobtid = \<hobt-id> subresource = \<alloc-unit-subresource> dbid =\<db-id>  
  
     **\<mode>다음이 될 수 있습니다.**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **외부 리소스 소유자:**  
  
-   외부 ExternalResource =\<wait-type>  
  
 **일반 리소스 소유자:**  
  
-   TransactionMutex Transactionmutex 작업 영역 =\<workspace-id>  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **래치 리소스 소유자:**  
  
-   \<db-id>:\<file-id>:\<page-in-file>  
  
-   \<GUID>  
  
-   \<latch-class> (\<latch-address>)  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
 
## <a name="example"></a>예제
### <a name="a-identify-tasks-from-blocked-sessions"></a>A. 차단 세션에서 작업을 식별 합니다. 

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
```   

### <a name="b-view-waiting-tasks-per-connection"></a>B. 연결당 대기 작업 보기

```sql
SELECT st.text AS [SQL Text], c.connection_id, w.session_id, 
  w.wait_duration_ms, w.wait_type, w.resource_address, 
  w.blocking_session_id, w.resource_description, c.client_net_address, c.connect_time
FROM sys.dm_os_waiting_tasks AS w
INNER JOIN sys.dm_exec_connections AS c ON w.session_id = c.session_id 
CROSS APPLY (SELECT * FROM sys.dm_exec_sql_text(c.most_recent_sql_handle)) AS st 
              WHERE w.session_id > 50 AND w.wait_duration_ms > 0
ORDER BY c.connection_id, w.session_id
GO
```

### <a name="c-view-waiting-tasks-for-all-user-processes-with-additional-information"></a>C. 추가 정보를 사용 하 여 모든 사용자 프로세스에 대 한 대기 작업 보기

```sql
SELECT 'Waiting_tasks' AS [Information], owt.session_id,
    owt.wait_duration_ms, owt.wait_type, owt.blocking_session_id,
    owt.resource_description, es.program_name, est.text,
    est.dbid, eqp.query_plan, er.database_id, es.cpu_time,
    es.memory_usage*8 AS memory_usage_KB
FROM sys.dm_os_waiting_tasks owt
INNER JOIN sys.dm_exec_sessions es ON owt.session_id = es.session_id
INNER JOIN sys.dm_exec_requests er ON es.session_id = er.session_id
OUTER APPLY sys.dm_exec_sql_text (er.sql_handle) est
OUTER APPLY sys.dm_exec_query_plan (er.plan_handle) eqp
WHERE es.is_user_process = 1
ORDER BY owt.session_id;
GO
```
  
## <a name="see-also"></a>참고 항목  
[Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)      
[스레드 및 태스크 아키텍처 가이드](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
