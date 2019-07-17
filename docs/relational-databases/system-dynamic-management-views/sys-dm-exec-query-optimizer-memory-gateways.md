---
title: sys.dm_exec_query_optimizer_memory_gateways (TRANSACT-SQL) | Microsoft Docs
description: 리소스 세마포에 동시 쿼리 최적화를 제한 하는 데의 현재 상태를 반환 합니다.
ms.custom: ''
ms.date: 04/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cf134f630e4112f0cef87b7138b92fc83959e230
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097671"
---
# <a name="sysdmexecqueryoptimizermemorygateways-transact-sql"></a>sys.dm_exec_query_optimizer_memory_gateways (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

리소스 세마포에 동시 쿼리 최적화를 제한 하는 데의 현재 상태를 반환 합니다.

|Column|type|설명|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|리소스 관리자에서 리소스 풀 ID|  
|**name**|**sysname**|게이트 이름 (소규모, 중간 게이트웨이 큰 게이트웨이) 컴파일|
|**max_count**|**int**|구성 된 최대 수가 동시 컴파일합니다|
|**active_count**|**int**|이 게이트의 컴파일의 현재 수|
|**waiter_count**|**int**|이 게이트에 대 한 대기자 수|
|**threshold_factor**|**bigint**|쿼리 최적화를 사용한 최대 메모리 부분을 정의 하는 임계값 비율입니다.  작은 게이트웨이에 대 한 threshold_factor 작은 게이트웨이에 대 한 액세스를 확보 하는 데 필요한 되기 전에 하나의 쿼리에 대 한 바이트의 최대 최적화 프로그램 메모리 사용을 나타냅니다.  중간 규모 및 대규모 게이트웨이의 threshold_factor이이 게이트에 대 한 사용할 수 있는 총 서버 메모리 부분을 보여 줍니다. 출입문에 대 한 메모리 사용 임계값을 계산할 때 제수로 사용 됩니다.|
|**threshold**|**bigint**|다음 임계값 메모리 바이트입니다.  쿼리는 메모리 소비가이 임계값에 도달 하면이 gateway에 대 한 액세스를 확보 해야 합니다.  "-1"이이 gateway에 대 한 액세스 권한을 얻으려고 쿼리가 필요 하지 않은 경우입니다.|
|**is_active**|**bit**|여부 쿼리 여부 현재 게이트를 통과 해야 합니다.|


## <a name="permissions"></a>사용 권한  
SQL Server 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.

Azure SQL Database에는 데이터베이스에는 VIEW DATABASE STATE 권한이 필요합니다.


## <a name="remarks"></a>설명  
SQL Server는 계층화 된 게이트웨이 방법을 사용 하 여 허용 된 동시 컴파일 수를 제한 합니다.  소, 포함 및 큰 세 개의 게이트웨이 사용 됩니다. 게이트웨이 도움말 큰 컴파일 메모리 필요한 소비자가 전체 메모리 리소스 소진을 방지 합니다.

지연 된 컴파일 게이트웨이 결과에서 대기합니다. 컴파일에서 지연 하는 것 외에도 스로틀 된 요청 유형 누적 대기 하는 연결된 RESOURCE_SEMAPHORE_QUERY_COMPILE 해야 합니다. 쿼리 컴파일에 대 한 많은 양의 메모리를 사용 하는 및 메모리 부족 또는 또는 충분 한 사용 가능한 메모리가 전반적으로 RESOURCE_SEMAPHORE_QUERY_COMPILE 대기 유형을 나타낼 수 있지만 사용 가능한 특정 단위 게이트웨이 모두 사용 했습니다. 출력 **sys.dm_exec_query_optimizer_memory_gateways** 시나리오 문제 해결에 사용할 수 있었던 다음 쿼리 실행 계획을 컴파일하는 데 메모리가 부족 합니다.  

## <a name="examples"></a>예  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>A. 리소스 세마포에 통계 보기  
SQL Server의이 인스턴스에 대 한 현재 최적화 프로그램 메모리 게이트웨이 통계 이란?

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[DBCC MEMORYSTATUS 명령을 사용 하 여 SQL Server 2005에서 메모리 사용량을 모니터링 하는 방법](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[SQL Server 2014에서 RESOURCE_SEMAPHORE_QUERY_COMPILE에서 큰 쿼리 컴파일을 대기](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
