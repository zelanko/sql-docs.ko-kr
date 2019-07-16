---
title: sys.dm_os_waiting_tasks (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f6ce0fa8270a05d8c3385cbc7b5c25edeaa84bc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899642"
---
# <a name="sysdmoswaitingtasks-transact-sql"></a>sys.dm_os_waiting_tasks(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  특정 리소스에서 대기 중인 태스크의 대기 큐에 대한 정보를 반환합니다.  
  
> [!NOTE]  
>  이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_waiting_tasks**합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|대기 중인 태스크의 주소입니다.|  
|**session_id**|**smallint**|태스크와 연결된 세션의 ID입니다.|  
|**exec_context_id**|**int**|태스크와 연결된 실행 컨텍스트의 ID입니다.|  
|**wait_duration_ms**|**bigint**|이 대기 유형에 대한 총 대기 시간(밀리초)입니다. 이 시간은 포함 **signal_wait_time**합니다.|  
|**wait_type**|**nvarchar(60)**|대기 유형의 이름입니다.|  
|**resource_address**|**varbinary(8)**|태스크가 대기 중인 리소스의 주소입니다.|  
|**blocking_task_address**|**varbinary(8)**|현재 이 리소스를 보유하고 있는 태스크입니다.|  
|**blocking_session_id**|**smallint**|요청을 차단하고 있는 세션의 ID입니다. 이 열이 NULL이면 요청이 차단되지 않거나 차단 세션의 세션 정보를 사용할 수 없습니다(또는 식별할 수 없음).<br /><br /> -2 = 분리된 분산 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -3 = 지연된 복구 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -4 = 내부 래치 상태 전환 때문에 차단 래치 소유자의 세션 ID를 확인할 수 없습니다.|  
|**blocking_exec_context_id**|**int**|차단 태스크의 실행 컨텍스트 ID입니다.|  
|**resource_description**|**nvarchar(3072)**|사용 중인 리소스에 대한 설명입니다. 자세한 내용은 아래 목록을 참조하십시오.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="resourcedescription-column"></a>resource_description 열  
 Resource_description 열 다음의 가능한 값에 있습니다.  
  
 **스레드 풀 리소스 소유자:**  
  
-   threadpool id=scheduler\<hex-address>  
  
 **병렬 쿼리 리소스 소유자:**  
  
-   exchangeEvent id={Port|Pipe}\<hex-address> WaitType=\<exchange-wait-type> nodeId=\<exchange-node-id>  
  
 **Exchange-wait-type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **잠금 리소스 소유자:**  
  
-   \<type-specific-description> id=lock\<lock-hex-address> mode=\<mode> associatedObjectId=\<associated-obj-id>  
  
     **\<형식 관련 설명 > 일 수 있습니다.**  
  
    -   Database: databaselock subresource =\<databaselock subresource > dbid =\<db id >  
  
    -   File: filelock fileid =\<파일-i d > subresource =\<filelock subresource > dbid =\<db id >  
  
    -   개체: objectlock lockPartition =\<잠금 파티션 id > objid =\<obj-i d > subresource =\<objectlock subresource > dbid =\<db id >  
  
    -   Page: pagelock fileid =\<파일-i d > pageid =\<페이지 id > dbid =\<db-i d > subresource =\<pagelock subresource >  
  
    -   Key: keylock hobtid =\<hobt id > dbid =\<db id >  
  
    -   Extent: extentlock fileid =\<파일-i d > pageid =\<페이지-i d > dbid =\<db id >  
  
    -   RID: ridlock fileid =\<파일-i d > pageid =\<페이지-i d > dbid =\<db id >  
  
    -   Application: applicationlock 해시 =\<해시 > databasePrincipalId =\<역할-i d > dbid =\<db id >  
  
    -   메타 데이터: metadatalock subresource =\<메타 데이터 subresource > classid =\<metadatalock 설명 > dbid =\<db id >  
  
    -   HOBT: hobtlock hobtid =\<hobt-i d > subresource =\<hobt subresource > dbid =\<db id >  
  
    -   Allocation_unit: allocunitlock hobtid =\<hobt-i d > subresource =\<alloc-단위-subresource > dbid =\<db id >  
  
     **\<모드 > 일 수 있습니다.**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **외부 리소스 소유자:**  
  
-   외부 ExternalResource =\<대기 유형 >  
  
 **일반 리소스 소유자:**  
  
-   TransactionMutex TransactionInfo Workspace=\<workspace-id>  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **래치 리소스 소유자:**  
  
-   \<db-id>:\<file-id>:\<page-in-file>  
  
-   \<GUID>  
  
-   \<래치 클래스 > (\<래치 주소 >)  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]에서 데이터베이스에 대한 `VIEW DATABASE STATE` 권한이 필요합니다.   
 
## <a name="example"></a>예제
이 예제에서는 차단된 세션을 식별 합니다.  실행 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.
```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>관련 항목  
  [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


