---
title: sys. dm_pdw_nodes_exec_query_profiles (Transact-sql) | Microsoft Docs
description: 쿼리가 실행 되는 동안 실시간 데이터 웨어하우스 쿼리 진행률을 모니터링 하는 데 사용할 수 있는 동적 관리 뷰입니다.
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7237e7f7b49916e09f4a8c5cab0d7d49486cb971
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73145658"
---
# <a name="sysdm_pdw_nodes_exec_query_profiles-transact-sql"></a>sys. dm_pdw_nodes_exec_query_profiles (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

쿼리가 실행 되는 동안 실시간 데이터 웨어하우스 쿼리 진행률을 모니터링 합니다.   
  
## <a name="table-returned"></a>반환 된 테이블  
반환된 카운터는 연산자 및 스레드 기준입니다. 결과는 동적 이며 쿼리가 완료 될 때만 출력을 만드는 것 `SET STATISTICS XML ON` 과 같은 기존 옵션의 결과와 일치 하지 않습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 ID입니다.|
|session_id|**smallint**|이 쿼리가 실행되는 세션을 식별합니다. dm_exec_sessions.session_id를 참조합니다.|  
|request_id|**int**|대상 요청을 식별합니다. dm_exec_sessions.request_id를 참조합니다.|  
|sql_handle|**varbinary (64)**|쿼리가 속하는 일괄 처리 또는 저장 프로시저를 고유 하 게 식별 하는 토큰입니다. dm_exec_query_stats.sql_handle을 참조합니다.|  
|plan_handle|**varbinary (64)**|실행 된 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 하는 토큰 이며 계획 캐시에 있거나 현재 실행 중인 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 합니다. Plan_handle dm_exec_query_stats 참조 합니다.|  
|physical_operator_name|**nvarchar(256)**|물리적 연산자 이름입니다.|  
|node_id|**int**|쿼리 트리에서 연산자 노드를 식별합니다.|  
|thread_id|**int**|동일한 쿼리 연산자 노드에 속하는 (병렬 쿼리)에 대한 스레드를 구분합니다.|  
|task_address|**varbinary(8)**|이 스레드가 사용하는 SQLOS 작업을 식별합니다. dm_os_tasks.task_address를 참조합니다.|  
|row_count|**bigint**|지금까지 연산자에서 반환한 행 수입니다.|  
|rewind_count|**bigint**|지금까지의 되감기 횟수입니다.|  
|rebind_count|**bigint**|지금까지의 다시 바인딩 횟수입니다.|  
|end_of_scan_count|**bigint**|지금까지의 검색 끝 수입니다.|  
|estimate_row_count|**bigint**|예상 행 수입니다. estimated_row_count를 실제 row_count와 비교하는 것이 유용할 수 있습니다.|  
|first_active_time|**bigint**|연산자가 밀리초 단위로 처음 호출된 시간입니다.|  
|last_active_time|**bigint**|연산자가 밀리초 단위로 마지막 호출된 시간입니다.|  
|open_time|**bigint**|열린 때의 타임스탬프입니다(밀리초).|  
|first_row_time|**bigint**|첫 번째 행이 열린 타임스탬프입니다(밀리초).|  
|last_row_time|**bigint**|마지막 행이 열린 타임스탬프입니다(밀리초).|  
|close_time|**bigint**|닫을 때의 타임스탬프입니다(밀리초).|  
|elapsed_time_ms|**bigint**|지금까지 대상 노드의 작업에서 사용한 총 경과 시간 (밀리초)입니다.|  
|cpu_time_ms|**bigint**|지금까지 대상 노드의 작업에서 사용 하는 총 CPU 시간 (밀리초)입니다.|  
|database_id|**smallint**|읽기 및 쓰기를 수행하는 개체가 포함된 데이터베이스의 ID입니다.|  
|object_id|**int**|읽기 및 쓰기를 수행하는 개체의 ID입니다. sys.objects.object_id를 참조합니다.|  
|index_id|**int**|행 집합이 열린 인덱스입니다(있는 경우).|  
|scan_count|**bigint**|지금까지의 테이블/인덱스 검색 수 입니다.|  
|logical_read_count|**bigint**|지금까지의 논리적 읽기 수입니다.|  
|physical_read_count|**bigint**|지금까지의 물리적 읽기 수입니다.|  
|read_ahead_count|**bigint**|지금까지의 read-ahead 수입니다.|  
|write_page_count|**bigint**|실수로 인한 지금까지의 페이지 쓰기 수입니다.|  
|lob_logical_read_count|**bigint**|지금까지의 LOB 논리적 읽기 수입니다.|  
|lob_physical_read_count|**bigint**|지금까지의 LOB 물리적 읽기 수입니다.|  
|lob_read_ahead_count|**bigint**|지금까지의 LOB read-ahead 수입니다.|  
|segment_read_count|**int**|지금까지의 세그먼트 read-ahead 수입니다.|  
|segment_skip_count|**int**|지금까지 생략된 세그먼트 수입니다.| 
|actual_read_row_count|**bigint**|잔여 조건자를 적용 하기 전에 연산자가 읽은 행 수입니다.| 
|estimated_read_row_count|**bigint**|**적용 대상:** [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] S p 1 부터는 <br/>나머지 조건자가 적용 되기 전에 연산자에서 읽을 수 있는 것으로 예상 되는 행 수입니다.|  
  
## <a name="remarks"></a>설명  
[Dm_exec_query_profiles](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql?view=sql-server-ver15) 적용 됩니다.  

## <a name="permissions"></a>사용 권한  
 서버에 대한 `VIEW SERVER STATE` 권한이 필요합니다.  

## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
   

 ## <a name="next-steps"></a>다음 단계
 더 많은 개발 팁은 [SQL Data Warehouse 개발 개요](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)를 참조하세요.
