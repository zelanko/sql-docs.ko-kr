---
title: sys.dm_os_waiting_tasks (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_waiting_tasks
- sys.dm_os_waiting_tasks_TSQL
- dm_os_waiting_tasks_TSQL
- sys.dm_os_waiting_tasks
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_waiting_tasks dynamic management view
ms.assetid: ca5e6844-368c-42e2-b187-6e5f5afc8df3
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d8df7b1a31a649962f4074c936ff4310cf16a942
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmoswaitingtasks-transact-sql"></a>sys.dm_os_waiting_tasks(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  특정 리소스에서 대기 중인 태스크의 대기 큐에 대한 정보를 반환합니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_waiting_tasks**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary (8)**|대기 중인 태스크의 주소입니다.|  
|**session_id**|**smallint**|태스크와 연결된 세션의 ID입니다.|  
|**exec_context_id**|**int**|태스크와 연결된 실행 컨텍스트의 ID입니다.|  
|**wait_duration_ms**|**bigint**|이 대기 유형에 대한 총 대기 시간(밀리초)입니다. 이 시간은 포함 **signal_wait_time**합니다.|  
|**wait_type**|**nvarchar (60)**|대기 유형의 이름입니다.|  
|**resource_address**|**varbinary (8)**|태스크가 대기 중인 리소스의 주소입니다.|  
|**blocking_task_address**|**varbinary (8)**|현재 이 리소스를 보유하고 있는 태스크입니다.|  
|**blocking_session_id**|**smallint**|요청을 차단하고 있는 세션의 ID입니다. 이 열이 NULL이면 요청이 차단되지 않거나 차단 세션의 세션 정보를 사용할 수 없습니다(또는 식별할 수 없음).<br /><br /> -2 = 분리된 분산 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -3 = 지연된 복구 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -4 = 내부 래치 상태 전환 때문에 차단 래치 소유자의 세션 ID를 확인할 수 없습니다.|  
|**blocking_exec_context_id**|**int**|차단 태스크의 실행 컨텍스트 ID입니다.|  
|**resource_description**|**nvarchar(3072)**|사용 중인 리소스에 대한 설명입니다. 자세한 내용은 아래 목록을 참조하십시오.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="resourcedescription-column"></a>resource_description 열  
 Resource_description 열은 다음 값에 있습니다.  
  
 **스레드 풀 리소스 소유자:**  
  
-   스레드 풀 id = 스케줄러\<16 진수 주소 >  
  
 **병렬 쿼리 리소스 소유자:**  
  
-   exchangeEvent id = {포트 | 파이프}\<16 진수 주소 > WaitType =\<exchange-wait-유형 > nodeId =\<exchange 노드 id >  
  
 **Exchange-대기 유형:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **잠금 리소스 소유자:**  
  
-   \<형식 관련 설명 > id = 잠금\<잠금 16 진수 주소 > 모드 =\<모드 > associatedObjectId =\<연결-o b j-i d >  
  
     **\<형식 관련 설명 > 일 수 있습니다.**  
  
    -   Database: databaselock subresource =\<databaselock subresource > dbid =\<->  
  
    -   File: filelock fileid =\<파일-i d > subresource =\<filelock subresource > dbid =\<->  
  
    -   Object: objectlock lockPartition =\<잠금 파티션 id > objid =\<obj-i d > subresource =\<objectlock subresource > dbid =\<->  
  
    -   Page: pagelock fileid =\<파일-i d > pageid =\<페이지-i d > dbid =\<db-i d > subresource =\<pagelock subresource >  
  
    -   Key: keylock hobtid =\<hobt-i d > dbid =\<->  
  
    -   Extent: extentlock fileid =\<파일-i d > pageid =\<페이지-i d > dbid =\<->  
  
    -   RID: ridlock fileid =\<파일-i d > pageid =\<페이지-i d > dbid =\<->  
  
    -   Application: applicationlock 해시 =\<해시 > databasePrincipalId =\<역할-i d > dbid =\<->  
  
    -   메타 데이터: metadatalock subresource =\<metadata > classid =\<metadatalock 설명 > dbid =\<->  
  
    -   Hobt: hobtlock hobtid =\<hobt-i d > subresource =\<hobt subresource > dbid =\<->  
  
    -   Allocation_unit: allocunitlock hobtid =\<hobt-i d > subresource =\<alloc--i > dbid =\<->  
  
     **\<모드 > 일 수 있습니다.**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **외부 리소스 소유자:**  
  
-   외부 ExternalResource =\<대기 유형 >  
  
 **일반 리소스 소유자:**  
  
-   TransactionMutex TransactionInfo 작업 영역 =\<작업 영역 id >  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **래치 리소스 소유자:**  
  
-   \<->:\<파일-i d >:\<페이지 파일 >  
  
-   \<GUID >  
  
-   \<래치 클래스 > (\<래치 주소 >)  
  
## <a name="permissions"></a>Permissions  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 프리미엄 계층 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층 필요는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정.  
 
## <a name="example"></a>예제
이 예제에서는 차단된 세션을 식별 합니다.  실행 된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 의 쿼리할 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.
```tsql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>관련 항목:  
  [SQL Server 운영 체제 관련 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


