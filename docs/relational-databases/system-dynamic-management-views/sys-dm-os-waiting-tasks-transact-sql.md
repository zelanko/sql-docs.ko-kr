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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0a89a48fa960812ee955cd3b7ecb30069161f61
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72260383"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  특정 리소스에서 대기 중인 태스크의 대기 큐에 대한 정보를 반환합니다. 작업에 대 한 자세한 내용은 [스레드 및 태스크 아키텍처 가이드](../../relational-databases/thread-and-task-architecture-guide.md)를 참조 하세요.
   
> [!NOTE]  
>  또는 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서이를 호출 하려면 이름 **sys. dm_pdw_nodes_os_waiting_tasks**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|대기 중인 태스크의 주소입니다.|  
|**session_id**|**smallint**|태스크와 연결된 세션의 ID입니다.|  
|**exec_context_id**|**int**|태스크와 연결된 실행 컨텍스트의 ID입니다.|  
|**wait_duration_ms**|**bigint**|이 대기 유형에 대한 총 대기 시간(밀리초)입니다. 이 시간은 **signal_wait_time**포함 됩니다.|  
|**wait_type**|**nvarchar (60)**|대기 형식 이름|  
|**resource_address**|**varbinary(8)**|태스크가 대기 중인 리소스의 주소입니다.|  
|**blocking_task_address**|**varbinary(8)**|현재 이 리소스를 보유하고 있는 태스크입니다.|  
|**blocking_session_id**|**smallint**|요청을 차단하고 있는 세션의 ID입니다. 이 열이 NULL이면 요청이 차단되지 않거나 차단 세션의 세션 정보를 사용할 수 없습니다(또는 식별할 수 없음).<br /><br /> -2 = 분리된 분산 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -3 = 지연된 복구 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -4 = 내부 래치 상태 전환 때문에 차단 래치 소유자의 세션 ID를 확인할 수 없습니다.|  
|**blocking_exec_context_id**|**int**|차단 태스크의 실행 컨텍스트 ID입니다.|  
|**resource_description**|**nvarchar (3072)**|사용 중인 리소스에 대한 설명입니다. 자세한 내용은 아래 목록을 참조하십시오.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="resource_description-column"></a>resource_description 열  
 resource_description 열에는 다음 값이 포함될 수 있습니다.  
  
 **스레드 풀 리소스 소유자:**  
  
-   threadpool id = scheduler\<16 진수 주소>  
  
 **병렬 쿼리 리소스 소유자:**  
  
-   exchangeEvent id = {Port | Pipe}\<Hex> WaitType =\<exchange-Wait-type> nodeId =\<exchange-node-id>  
  
 **Exchange-wait-type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **잠금 리소스 소유자:**  
  
-   \<유형별-설명> id = lock\<lock-address> mode =\<mode> associatedObjectId =\<연결 된 obj-id>  
  
     **\<유형별 설명> 다음이 될 수 있습니다.**  
  
    -   데이터베이스: databaselock subresource =\<databaselock-subresource> dbid =\<db-id>  
  
    -   파일: filelock fileid =\<파일 id> subresource =\<filelock-subresource> dbid =\<db-id>  
  
    -   개체\<: Objectlock lockpartition = objid = obj-id> =\<obj> subresource =\<objectlock-subresource> dbid =\<db-id>  
  
    -   PAGE\<lock fileid = file-id> pageid =\<page-id> dbid =\<db-id> subresource =\<pagelock-subresource>  
  
    -   키: 키잠금을 hobtid =\<hobt> dbid =\<db-id>  
  
    -   익스텐트의 경우: extentlock fileid =\<파일 id> pageid =\<페이지 id> dbid =\<db-id>  
  
    -   RID: ridlock fileid =\<파일 id> pageid =\<페이지 id> dbid =\<db-id>  
  
    -   응용 프로그램의 경우: applicationlock\<hash = Hash> databaseprincipalid =\<역할-id>\<dbid = db-id>  
  
    -   메타 데이터: metadatalock subresource =\<METADATA-subresource> classid =\<metadatalock-description> dbid =\<db-id>  
  
    -   HOBT: hobtlock hobtid =\<HOBT> subresource =\<HOBT-subresource> dbid =\<db-id>  
  
    -   ALLOCATION_UNIT: allocunit lock hobtid =\<hobt> 하위 리소스 =\<할당-단위-하위 리소스> dbid =\<db-id>  
  
     **\<모드> 다음이 될 수 있습니다.**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **외부 리소스 소유자:**  
  
-   외부 ExternalResource =\<대기 유형>  
  
 **일반 리소스 소유자:**  
  
-   TransactionMutex Transactionmutex 작업 영역\<= 작업 영역 id>  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **래치 리소스 소유자:**  
  
-   \<db-library>:\<파일-id>:\<페이지 내 파일>  
  
-   \<GUID>  
  
-   \<래치 클래스> (\<래치 주소>)  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 권한이 `VIEW SERVER STATE` 필요 합니다.   
Premium [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 계층에서는 데이터베이스에 대 `VIEW DATABASE STATE` 한 권한이 필요 합니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
 
## <a name="example"></a>예제
이 예에서는 차단 된 세션을 식별 합니다. 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]쿼리 [!INCLUDE[tsql](../../includes/tsql-md.md)] 를 실행 합니다.

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>참고 항목  
[Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)      
[스레드 및 태스크 아키텍처 가이드](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
