---
title: sys. dm_exec_query_optimizer_memory_gateways (Transact-sql)
description: 동시 쿼리 최적화를 제한 하는 데 사용 되는 리소스 세마포에 대 한 현재 상태를 반환 합니다.
ms.custom: seo-dt-2019
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
ms.openlocfilehash: 5720617f6652a8acb1ab8b6daf0e5e8919a86f8b
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165004"
---
# <a name="sysdm_exec_query_optimizer_memory_gateways-transact-sql"></a>sys. dm_exec_query_optimizer_memory_gateways (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

동시 쿼리 최적화를 제한 하는 데 사용 되는 리소스 세마포에 대 한 현재 상태를 반환 합니다.

|열|유형|설명|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|Resource Governor의 리소스 풀 ID|  
|**name**|**sysname**|컴파일 게이트 이름 (소형 게이트웨이, 중형 게이트웨이, 빅 게이트웨이)|
|**max_count**|**int**|구성 된 최대 동시 컴파일 수|
|**active_count**|**int**|이 게이트에서 현재 활성화 된 컴파일 수입니다.|
|**waiter_count**|**int**|이 게이트의 대기자 수입니다.|
|**threshold_factor**|**bigint**|쿼리 최적화에 사용 되는 최대 메모리 부분을 정의 하는 임계값 비율입니다.  작은 게이트웨이의 경우, threshold_factor는 작은 게이트웨이에 대 한 액세스 권한을 얻기 위해 필요한 한 쿼리의 최대 최적화 프로그램 메모리 사용량 (바이트)을 나타냅니다.  중간 규모 및 대규모 게이트웨이의 경우이 게이트에 사용할 수 있는 총 서버 메모리의 일부를 threshold_factor 표시 합니다. 이는 출입문의 메모리 사용 임계값을 계산할 때 제 수로 사용 됩니다.|
|**threshold**|**bigint**|다음 임계값 메모리 (바이트)입니다.  해당 메모리 소비가이 임계값에 도달 하는 경우이 게이트웨이에 대 한 액세스 권한을 얻으려면 쿼리가 필요 합니다.  쿼리가이 게이트웨이에 대 한 액세스 권한을 얻는 데 필요 하지 않은 경우에는 "-1"입니다.|
|**is_active**|**bit**|쿼리가 현재 게이트를 전달 하는 데 필요한 지 여부를 나타냅니다.|


## <a name="permissions"></a>사용 권한  
SQL Server 서버에 대 한 VIEW SERVER STATE 권한이 필요 합니다.

Azure SQL Database 데이터베이스에 대 한 VIEW DATABASE STATE 권한이 필요 합니다.


## <a name="remarks"></a>Remarks  
SQL Server는 계층화 된 게이트웨이 방법을 사용 하 여 허용 되는 동시 컴파일 수를 제한 합니다.  Small, medium, big을 포함 하 여 세 개의 게이트웨이가 사용 됩니다. 게이트웨이를 통해 더 큰 컴파일 메모리를 필요로 하는 소비자에의 한 전체 메모리 리소스가 소모 되는 것을 방지할 수 있습니다.

지연 된 컴파일이 발생 하면 게이트웨이를 대기 합니다. 컴파일 지연 외에도 제한 된 요청에는 연결 된 RESOURCE_SEMAPHORE_QUERY_COMPILE 대기 유형이 누적 됩니다. RESOURCE_SEMAPHORE_QUERY_COMPILE 대기 유형은 쿼리가 많은 양의 메모리를 컴파일하는 데 사용 중이거나 메모리가 고갈 되었거나 전체적으로 사용 가능한 메모리가 충분 하다는 것을 나타낼 수 있습니다. 게이트웨이가 모두 사용 되었습니다. **Dm_exec_query_optimizer_memory_gateways** 의 출력을 사용 하 여 쿼리 실행 계획을 컴파일하는 데 필요한 메모리가 부족 한 시나리오를 해결할 수 있습니다.  

## <a name="examples"></a>예  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>A. 리소스 세마포에 대 한 통계 보기  
이 SQL Server 인스턴스에 대 한 현재 최적화 프로그램 메모리 게이트웨이 통계는 무엇 인가요?

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[DBCC MEMORYSTATUS 명령을 사용 하 여 SQL Server 2005
에서 메모리 사용량을 모니터링 하는 방법](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005) [SQL Server 2014에서 RESOURCE_SEMAPHORE_QUERY_COMPILE에 대 한 대량 쿼리 컴파일 대기](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
