---
title: sys. dm_exec_query_parallel_workers (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 000dd995427f8eafec759688db1ab76a6546b789
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68263267"
---
# <a name="sysdm_exec_query_parallel_workers-transact-sql"></a>sys.dm_exec_query_parallel_workers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  노드당 작업자 가용성 정보를 반환 합니다.  
  
|속성|데이터 형식|Description|  
|----------|---------------|-----------------|  
|**node_id**|**int**|NUMA 노드 ID입니다.|  
|**scheduler_count**|**int**|이 노드의 스케줄러 수입니다.|  
|**max_worker_count**|**int**|병렬 쿼리에 대 한 최대 작업자 수입니다.|  
|**reserved_worker_count**|**int**|병렬 쿼리로 예약 된 작업자 수와 모든 요청에서 사용 하는 주 작업자 수| 
|**free_worker_count**|**int**|작업에 사용할 수 있는 작업자 수입니다.<br /><br />**참고:** 들어오는 모든 요청은 하나 이상의 작업자를 사용 하며이는 사용 가능한 작업자 수에서 뺍니다.  사용량이 많은 서버에서 사용 가능한 작업자 수가 음수가 될 수 있습니다.| 
|**used_worker_count**|**int**|병렬 쿼리에서 사용 하는 작업자 수입니다.|  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 권한이 `VIEW SERVER STATE` 필요 합니다.   
Premium [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 계층에서는 데이터베이스에 대 `VIEW DATABASE STATE` 한 권한이 필요 합니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
 
## <a name="examples"></a>예  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>A. 현재 병렬 작업자 가용성 보기  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;관련 동적 관리 뷰 및 함수 실행](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [dm_os_workers &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
