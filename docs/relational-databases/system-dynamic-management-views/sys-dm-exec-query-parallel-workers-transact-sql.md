---
title: sys.dm_exec_query_parallel_workers (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: pelopes
ms.author: pelopes
manager: ajayj
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1ff6dee668cd6bc93d9a3c74ae4b3e25cbe99be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63013151"
---
# <a name="sysdmexecqueryparallelworkers-transact-sql"></a>sys.dm_exec_query_parallel_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  노드당 반환 작업자 가용성 정보입니다.  
  
|이름|데이터 형식|Description|  
|----------|---------------|-----------------|  
|**node_id**|**int**|NUMA 노드 id입니다.|  
|**scheduler_count**|**int**|이 노드의 스케줄러 수입니다.|  
|**max_worker_count**|**int**|병렬 쿼리에 대 한 작업자의 최대 수입니다.|  
|**reserved_worker_count**|**int**|모든 요청에서 사용 되는 기본 작업자 수를 더한 병렬 쿼리에서 예약 된 작업자 수입니다.| 
|**free_worker_count**|**int**|작업에 사용할 수 있는 작업자의 수입니다.<br /><br />**참고:** 들어오는 모든 요청에서 사용 가능한 작업자 수를 뺍니다는 1 개 이상 작업자를 사용 합니다.  사용 가능한 작업자 수가 과도 하 게 로드 서버의 음수 있음을 가능성이 있습니다.| 
|**used_worker_count**|**int**|병렬 쿼리에서 사용 되는 작업자 수입니다.|  
  
## <a name="permissions"></a>사용 권한  

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
 
## <a name="examples"></a>예  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>1\. 현재 병렬 작업자 가용성 확인  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_os_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
