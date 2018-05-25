---
title: sys.dm_exec_query_parallel_workers (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_parallel_workers_TSQL
- dm_exec_query_parallel_workers
- sys.dm_exec_query_parallel_workers_TSQL
- sys.dm_exec_query_parallel_workers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_parallel_workers dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9f
caps.latest.revision: 1
author: pelopes
ms.author: pelopes
manager: ajayj
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f2bc4634a5e2fddb4a3c8eda009eb28019089596
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmexecqueryparallelworkers-transact-sql"></a>sys.dm_exec_query_parallel_workers (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  노드당 반환 작업자 가용성 정보입니다.  
  
|이름|데이터 형식|Description|  
|----------|---------------|-----------------|  
|**node_id**|**int**|NUMA 노드 id입니다.|  
|**scheduler_count**|**int**|이 노드의 스케줄러 수입니다.|  
|**max_worker_count**|**int**|병렬 쿼리에 대 한 작업자의 최대 수입니다.|  
|**reserved_worker_count**|**int**|모든 요청에서 사용 되는 주 작업자 수 및 병렬 쿼리에 예약 작업자의 수입니다.| 
|**free_worker_count**|**int**|작업에 사용할 수 있는 작업자 수입니다.<br /><br />**참고:** 들어오는 모든 요청 소비 1 명 이상 작업자에 사용 가능한 작업자 수에서 뺍니다.  있기 무료 작업자 수 과도 하 게 로드 하는 서버에 음수를 수 있습니다.| 
|**used_worker_count**|**int**|병렬 쿼리에 사용 된 작업자 수입니다.|  
  
## <a name="permissions"></a>Permissions  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   
 
## <a name="examples"></a>예  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>1. 현재 병렬 작업자 가용성 보기  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_os_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
