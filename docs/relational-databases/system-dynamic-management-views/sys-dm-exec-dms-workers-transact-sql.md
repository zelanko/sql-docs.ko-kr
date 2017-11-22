---
title: sys.dm_exec_dms_workers (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS
dev_langs: TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_workers management view
- sys.dm_exec_dms_workers management view
ms.assetid: f468da29-78c3-4f10-8a3c-17905bbf46f2
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b5677eb04a9a5809c2caf25d37edd288e4b1efbc
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecdmsworkers-transact-sql"></a>sys.dm_exec_dms_workers (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  DMS 단계를 완료 하는 모든 작업자에 대 한 정보를 보유 합니다.  
  
 이 보기에서 지난 1000 개의 요청 및 활성 요청;에 대 한 데이터를 표시합니다. 활성 요청이이 보기에 있는 데이터를 항상 포함 됩니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar (32)**|쿼리이 DMS 작업자는 일부 of.request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 형성 합니다.||  
|step_index|**int**|이 DMS 작업자의 일부인 단계를 쿼리 합니다.|단계 인덱스를 참조 하십시오. [sys.dm_exec_distributed_request_steps&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|dms_step_index|**int**|이 작업 자가 실행 되는 DMS 계획의 단계입니다.|참조 [sys.dm_exec_dms_workers (Transact SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|**int**|작업자에서 실행 되는 노드.|참조 [sys.dm_exec_compute_nodes&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|**int**|||  
|형식|**nvarcha(32)**|||  
|상태|**nvarchar (32)**|이 단계는 상태|'보류 중인', '실행 중', 'Complete', '실패', 'UndoFailed', 'PendingCancel', ' 취소 ', '취소', '중단'|  
|bytes_per_sec|**bigint**|||  
|bytes_processed|**bigint**|||  
|rows_processed|**bigint**|||  
|start_time|**datetime**|단계 실행 시작 된 시간|더 작은 또는 현재 시간 및 크거나 end_compile_time이이 단계 속해 있는 쿼리 합니다.|  
|end_time|**datetime**|이 단계 실행을 완료, 취소 되었거나 실패 시간입니다.|더 작은 또는 현재 시간 및 크거나 start_time, 실행의 현재 단계에 대 한 NULL로 설정 하거나 큐에 대기 합니다.|  
|total_elapsed_time|**int**|시간 쿼리 단계가 실행 되는, (밀리초)|0 사이의 start_time 및 end_time 간의 차이입니다. 큐에 대기 중인된 단계에 대 한 0입니다.|  
|cpu_time|**bigint**|||  
|query_time|**int**|||  
|buffers_available|**int**|||  
|dms_cpid|**int**|||  
|sql_spid|**int**|||  
|error_id|**nvarchar(36)**|||  
|가 source_info|**nvarchar(4000)**|||  
|destination_info|**nvarchar(4000)**|||  
|command|**nvarchar(4000)**|||  
  
## <a name="see-also"></a>관련 항목:  
 [PolyBase 동적 관리 뷰를 사용한 문제 해결](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련된 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
