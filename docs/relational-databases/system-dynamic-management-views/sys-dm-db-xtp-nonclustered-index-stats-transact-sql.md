---
title: sys.dm_db_xtp_nonclustered_index_stats (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_nonclustered_index_stats_TSQL
- dm_db_xtp_nonclustered_index_stats
- sys.dm_db_xtp_nonclustered_index_stats_TSQL
- sys.dm_db_xtp_nonclustered_index_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_nonclustered_index_stats
ms.assetid: d55ba31c-296c-419b-9c4b-c126e0a3d156
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 24a1987e4a7f45630ea85c8048ccf912ff15d463
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbxtpnonclusteredindexstats-transact-sql"></a>sys.dm_db_xtp_nonclustered_index_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  sys.dm_db_xtp_nonclustered_index_stats에는 메모리 최적화 테이블의 비클러스터형 인덱스에서 작업에 대한 통계가 포함됩니다. sys.dm_db_xtp_nonclustered_index_stats에는 현재 데이터베이스의 메모리 최적화 테이블에서 각각의 비클러스터형 인덱스의 행 하나가 포함됩니다.  
  
 메모리 내 인덱스 구조를 만들 때 sys.dm_db_xtp_nonclustered_index_stats에 반영된 통계가 수집됩니다. 데이터베이스 다시 시작 시 메모리 내 인덱스 구조가 다시 만들어집니다.  
  
 sys.dm_db_xtp_nonclustered_index_stats를 사용하여 DML 작업 중 및 데이터베이스가 온라인이 될 경우 인덱스 작업을 이해하고 모니터링합니다. 메모리 최적화 테이블이 있는 데이터베이스를 다시 시작하면 메모리에 한 번에 한 행을 삽입하여 인덱스가 작성됩니다. 페이지 분할, 병합 및 통합 수는 데이터베이스가 온라인이 될 때 인덱스 작성을 완료한 작업을 이해하는 데 도움이 될 수 있습니다. 일련의 DML 작업 이전 및 이후에 이 횟수를 확인할 수도 있습니다.  
  
 다시 시도 횟수가 많으면 동시성 오류가 발생할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원을 호출합니다.  
  
 메모리 액세스에 최적화 된 비클러스터형 인덱스에 대 한 자세한 내용은 참조 [SQL Server 메모리 내 OLTP 내부 개요](http://t.co/T6zToWc6y6), 17 페이지입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|개체의 ID입니다.|  
|xtp_object_id|**bigint**|메모리 액세스에 최적화 된 테이블의 ID입니다.|  
|index_id|**int**|인덱스의 ID입니다.|  
|delta_pages|**bigint**|트리의 이 인덱스에 대한 델타 페이지 수입니다.|  
|internal_pages|**bigint**|내부적으로만 사용할 수 있습니다. 트리의 이 인덱스에 대한 내부 페이지 수입니다.|  
|leaf_pages|**bigint**|트리의 이 인덱스에 대한 리프 페이지 수입니다.|  
|outstanding_retired_nodes|**bigint**|내부적으로만 사용할 수 있습니다. 내부 구조의 이 인덱스에 대한 전체 노드 수입니다.|  
|page_update_count|**bigint**|인덱스에서 페이지를 업데이트하는 누적 작업 수입니다.|  
|page_update_retry_count|**bigint**|인덱스에서 페이지를 업데이트하는 작업의 누적된 다시 시도 횟수입니다.|  
|page_consolidation_count|**bigint**|인덱스의 누적 페이지 통합 수입니다.|  
|page_consolidation_retry_count|**bigint**|페이지 통합 작업의 누적 재시도 횟수입니다.|  
|page_split_count|**bigint**|인덱스에서 페이지 분할 작업의 누적된 횟수입니다.|  
|page_split_retry_count|**bigint**|페이지 분할 작업의 누적 재시도 횟수입니다.|  
|key_split_count|**bigint**|인덱스의 누적 키 분할 횟수입니다.|  
|key_split_retry_count|**bigint**|키 분할 작업의 누적 재시도 횟수입니다.|  
|page_merge_count|**bigint**|인덱스에서 페이지 병합 작업의 누적된 횟수입니다.|  
|page_merge_retry_count|**bigint**|페이지 병합 작업의 누적 재시도 횟수입니다.|  
|key_merge_count|**bigint**|인덱스에서 키 병합 작업의 누적된 횟수입니다.|  
|key_merge_retry_count|**bigint**|키 병합 작업의 누적 재시도 횟수입니다.|  
  
## <a name="permissions"></a>Permissions  
 현재 데이터베이스에 대해 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [메모리 액세스에 최적화 된 테이블 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
