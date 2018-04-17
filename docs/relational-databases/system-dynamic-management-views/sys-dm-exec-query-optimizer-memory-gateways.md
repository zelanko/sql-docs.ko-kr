---
title: sys.dm_exec_query_optimizer_memory_gateways (Transact SQL) | Microsoft Docs
description: 동시 쿼리 최적화를 제한 하는 데 사용 되는 리소스 세마포의 현재 상태를 반환 합니다.
ms.custom: ''
ms.date: 04/06/2017
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
- dm_exec_query_optimizer_memory_gateways_TSQL
- dm_exec_query_optimizer_memory_gateways
- sys.dm_exec_query_optimizer_memory_gateways_TSQL
- sys.dm_exec_query_optimizer_memory_gateways
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_memory_gateways dynamic management view
author: josack
ms.author: josack
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 98e83cab69ca5346f1af7d8de41f3e2e666a5e16
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexecqueryoptimizermemorygateways-transact-sql"></a>sys.dm_exec_query_optimizer_memory_gateways (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

동시 쿼리 최적화를 제한 하는 데 사용 되는 리소스 세마포의 현재 상태를 반환 합니다.

|열|형식|Description|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|리소스 풀 ID에서 리소스 관리자|  
|**name**|**sysname**|컴파일 게이트 이름 (소규모, 중간 게이트웨이 큰 게이트웨이)|
|**max_count**|**int**|구성 된 최대 개수가 동시 컴파일|
|**active_count**|**int**|이 게이트에서 컴파일하여의 현재 수|
|**waiter_count**|**int**|이 게이트에 대 한 대기자 수|
|**threshold_factor**|**bigint**|쿼리 최적화에서 사용 하는 최대 메모리 부분을 정의 하는 임계값 비율입니다.  작은 게이트웨이에 대 한 threshold_factor 작은 게이트웨이에 액세스 하는 데 필요한 되기 전에 하나의 쿼리를 바이트 단위로 최대 최적화 프로그램 메모리 사용을 나타냅니다.  중간 규모 및 큰 게이트웨이에 대 한 threshold_factor이이 게이트에 사용할 수 있는 총 서버 메모리 부분을 보여 줍니다. 성문에 대 한 메모리 사용 임계값을 계산할 때 제수로 사용 됩니다.|
|**threshold**|**bigint**|다음 임계값 메모리 바이트입니다.  메모리 소비가이 임계값에 도달 하면이 게이트웨이에 대 한 액세스 권한을 얻으려고 쿼리가 필요 합니다.  "-1"이 게이트웨이에 대 한 액세스 권한을 얻으려고 쿼리가 필요 하지 않은 경우입니다.|
|**is_active**|**bit**|쿼리 여부 현재 게이트를 전달 하려면 필요한 지 여부.|


## <a name="permissions"></a>Permissions  
SQL Server는 서버에 대 한 VIEW SERVER STATE 권한이 필요합니다.

Azure SQL 데이터베이스는 데이터베이스에 VIEW DATABASE STATE 권한이 필요합니다.


## <a name="remarks"></a>주의  
SQL Server는 계층화 된 게이트웨이 방법을 사용 하 여 허용 된 동시 컴파일 수가 제한 됩니다.  포함 하 여 작은, 보통 및 크게 세 게이트웨이 사용 됩니다. 게이트웨이 방지 컴파일 더 큰 메모리 요구 소비자가 전체 메모리 리소스를 소모 합니다.

지연 된 컴파일에서 게이트웨이 결과에 대기합니다. 컴파일에서 지연, 외에도 제한 된 요청 유형 누적 대기 하는 관련된 RESOURCE_SEMAPHORE_QUERY_COMPILE 갖습니다. 하지만 RESOURCE_SEMAPHORE_QUERY_COMPILE 대기 유형으로 인해 쿼리 컴파일에 대 한 많은 양의 메모리를 사용 하는 해당 메모리에 도달 하거나 또는 충분 한 사용 가능한 메모리가 전반적으로 나타낼 수 있습니다 사용할 수 있는 특정 단위 게이트웨이 없습니다. 출력 **sys.dm_exec_query_optimizer_memory_gateways** 문제를 해결 하는 데 사용 될 경우 쿼리 실행 계획을 컴파일하는 데 메모리가 부족 합니다.  

## <a name="examples"></a>예  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>1. 리소스 세마포에 통계 보기  
이 SQL Server이 인스턴스에 대 한 현재 최적화 프로그램 메모리 게이트웨이 통계 무엇입니까?

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수 &#40;Transact SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[DBCC MEMORYSTATUS 명령을 사용 하 여 SQL Server 2005의 메모리 사용량을 모니터링 하는 방법](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[큰 쿼리 컴파일 RESOURCE_SEMAPHORE_QUERY_COMPILE SQL Server 2014에 대 한 대기](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
