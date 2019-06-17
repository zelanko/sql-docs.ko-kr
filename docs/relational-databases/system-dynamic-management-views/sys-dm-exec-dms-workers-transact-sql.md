---
title: sys.dm_exec_dms_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_workers management view
- sys.dm_exec_dms_workers management view
ms.assetid: f468da29-78c3-4f10-8a3c-17905bbf46f2
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8a31b03208eba573fc6bd50f2348733ef0a07c2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63013320"
---
# <a name="sysdmexecdmsworkers-transact-sql"></a>sys.dm_exec_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  DMS 단계를 완료 하는 모든 작업자에 대 한 정보를 보유 합니다.  
  
 이 보기에는 지난 1000 개의 요청 및 활성 요청에 대 한 데이터 표시 활성 요청은이 보기에 있는 데이터를 갖습니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|쿼리는이 DMS 작업자와 일부 of.request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 형성 합니다.||  
|step_index|**int**|이 DMS 작업자의 일부인 단계를 쿼리 합니다.|단계 인덱스를 참조 하세요 [sys.dm_exec_distributed_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)합니다.|  
|dms_step_index|**int**|이 작업 자가 실행 되는 DMS 계획의 단계입니다.|참조 [sys.dm_exec_dms_workers (Transact SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|**int**|작업자에서 실행 되는 노드.|참조 [sys.dm_exec_compute_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)합니다.|  
|distribution_id|**int**|||  
|유형|**nvarcha(32)**|||  
|상태|**nvarchar(32)**|이 단계는 상태|'보류 중', 'Running', 'Complete', '실패 'UndoFailed', 'PendingCancel', ' 취소 '를 '취소', '중단'|  
|bytes_per_sec|**bigint**|||  
|bytes_processed|**bigint**|||  
|rows_processed|**bigint**|||  
|start_time|**datetime**|단계 실행 시작 된 시간|더 작은 또는 현재 같음 및 크거나 end_compile_time이이 단계 속해 있는 쿼리.|  
|end_time|**datetime**|이 단계 실행이 완료, 취소 되었거나 실패 한 시간입니다.|더 작은 또는 현재 같음 및 크거나 start_time, 큐에 대기 또는 실행의 현재 단계에 대 한 NULL로 설정 합니다.|  
|total_elapsed_time|**int**|총 쿼리 단계가 실행 된를 밀리초 단위로 시간|0 사이의 start_time 및 end_time 간의 차이입니다. 큐에 대기 중인된 단계에 대 한 0입니다.|  
|cpu_time|**bigint**|||  
|query_time|**int**|||  
|buffers_available|**int**|||  
|dms_cpid|**int**|||  
|sql_spid|**int**|||  
|error_id|**nvarchar(36)**|||  
|source_info|**nvarchar(4000)**|||  
|destination_info|**nvarchar(4000)**|||  
|command|**nvarchar(4000)**|||  
  
## <a name="see-also"></a>관련 항목  
 [PolyBase 동적 관리 뷰를 사용 하 여 문제 해결](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
