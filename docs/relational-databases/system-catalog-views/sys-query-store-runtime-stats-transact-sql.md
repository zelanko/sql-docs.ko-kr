---
title: sys.query_store_runtime_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dd25f70c7cf3d34a4411cc15802437d97f5f8190
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66462731"
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>sys.query_store_runtime_stats (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  쿼리에 대 한 런타임 실행 통계 정보에 대 한 정보를 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|에 대 한 런타임 실행 통계를 나타내는 행의 식별자를 **plan_id**를 **execution_type** 하 고 **runtime_stats_interval_id**합니다. 이 지난 런타임 통계 간격 동안만 고유 합니다. 현재 활성 간격에 대 한 있을 수 있습니다 여러 행에서 참조 하는 계획에 대 한 런타임 통계를 나타내는 **plan_id**를 나타내는 실행 형식과 **execution_type**합니다. 일반적으로 행이 하나씩 나타냅니다 플러시되는 런타임 통계를 디스크에 다른 (s) 메모리 내 상태를 나타냅니다. 따라서 간격에 대 한 실제 상태를 가져오려는 해야 집계 메트릭을 그룹화 **plan_id**를 **execution_type** 하 고 **runtime_stats_interval_id**합니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**plan_id**|**bigint**|외래 키입니다. 에 조인 [sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)합니다.|  
|**runtime_stats_interval_id**|**bigint**|외래 키입니다. 에 조인 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)합니다.|  
|**execution_type**|**tinyint**|쿼리 실행의 유형을 결정 합니다.<br /><br /> 0-일반 실행 (완료)<br /><br /> 3-클라이언트에서 시작한 실행을 중단 했습니다.<br /><br /> 4-예외 실행이 중단 됨|  
|**execution_type_desc**|**nvarchar(128)**|실행 형식 필드의 텍스트 설명:<br /><br /> 0-일반<br /><br /> 3-중단<br /><br /> 4 -  Exception|  
|**first_execution_time**|**datetimeoffset**|집계 간격 내에서 쿼리 계획에 대 한 첫 번째 실행 시간입니다. 쿼리 실행의 종료 시간을 나타냅니다.|  
|**last_execution_time**|**datetimeoffset**|집계 간격 내에서 쿼리에 대해 마지막 실행 시간을 계획 합니다. 쿼리 실행의 종료 시간을 나타냅니다.|  
|**count_executions**|**bigint**|집계 간격 내에서 쿼리 계획에 대 한 실행의 총 수입니다.|  
|**avg_duration**|**float**|평균 기간 (마이크로초 단위로 보고) 집계 간격 내에서 쿼리 계획에 대 한 합니다.|  
|**last_duration**|**bigint**|쿼리에 대 한 마지막 기간 (마이크로초 단위로 보고) 집계 간격 내에서 계획 합니다.|  
|**min_duration**|**bigint**|집계 간격 (마이크로초 단위로 보고) 내에서 쿼리 계획에 대 한 최소 기간입니다.|  
|**max_duration**|**bigint**|집계 간격 (마이크로초 단위로 보고) 내에서 쿼리 계획에 대 한 최대 기간입니다.|  
|**stdev_duration**|**float**|기간 (마이크로초 단위로 보고) 집계 간격 내에서 쿼리 계획에 대 한 표준 편차입니다.|  
|**avg_cpu_time**|**float**|CPU 시간 (마이크로초 단위로 보고) 집계 간격 내에서 쿼리 계획에 대 한 평균입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**last_cpu_time**|**bigint**|쿼리에 대해 마지막 CPU 시간 (마이크로초 단위로 보고) 집계 간격 내에서 계획 합니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**min_cpu_time**|**bigint**|집계 간격 (마이크로초 단위로 보고) 내에서 쿼리 계획에 대 한 최소 CPU 시간입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**max_cpu_time**|**bigint**|최대 CPU 시간 (마이크로초 단위로 보고) 집계 간격 내에서 쿼리 계획입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**stdev_cpu_time**|**float**|집계 간격 (마이크로초 단위로 보고) 내에서 쿼리 계획에 대 한 CPU 시간 표준 편차입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**avg_logical_io_reads**|**float**|집계 간격 내에서 쿼리 계획에 대 한 평균 논리적 IO 수를 읽습니다. (8KB 페이지 읽기 수로 표현 됨).<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**last_logical_io_reads**|**bigint**|집계 간격 내에서 쿼리 계획에 대 한 마지막 논리적 IO 수를 읽습니다. (8KB 페이지 읽기 수로 표현 됨).<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**min_logical_io_reads**|**bigint**|집계 간격 내에서 쿼리 계획에 대 한 최소 논리적 IO 수를 읽습니다. (8KB 페이지 읽기 수로 표현 됨).<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**max_logical_io_reads**|**bigint**|집계 간격 내에서 쿼리 계획에 대 한 최대 논리적 IO 수를 읽습니다. (8KB 페이지 읽기 수로 표현 됨).<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**stdev_logical_io_reads**|**float**|논리적 io 수 집계 간격 내에서 쿼리 계획에 대 한 표준 편차를 읽습니다. (8KB 페이지 읽기 수로 표현 됨).<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**avg_logical_io_writes**|**float**|평균 논리적 io 집계 간격 내에서 쿼리 계획에 씁니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**last_logical_io_writes**|**bigint**|마지막 논리적 IO 쓰기 수 집계 간격 내에서 쿼리 계획에 대 한 합니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**min_logical_io_writes**|**bigint**|최소 논리적 IO 쓰기 수 집계 간격 내에서 쿼리 계획에 대 한 합니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**max_logical_io_writes**|**bigint**|최대 논리적 IO 집계 간격 내에서 쿼리 계획에 씁니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**stdev_logical_io_writes**|**float**|논리적 io 수 집계 간격 내에서 쿼리 계획에 대 한 표준 편차를 씁니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**avg_physical_io_reads**|**float**|집계 간격 (8KB 페이지 읽기 수로 표현 됨) 내에서 쿼리 계획에 대 한 평균 물리적 IO 읽습니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**last_physical_io_reads**|**bigint**|마지막 물리적 IO 읽기 수 (8KB 페이지 읽기 수로 표현) 집계 간격 내에서 쿼리 계획에 대 한 합니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**min_physical_io_reads**|**bigint**|집계 간격 (8KB 페이지 읽기 수로 표현 됨) 내에서 쿼리 계획에 대 한 물리적 IO의 최소 수를 읽습니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**max_physical_io_reads**|**bigint**|집계 간격 (8KB 페이지 읽기 수로 표현 됨) 내에서 쿼리 계획에 대 한 최대 물리적 IO 읽습니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**stdev_physical_io_reads**|**float**|물리적 IO 읽기 수 (8KB 페이지 읽기 수로 표현) 집계 간격 내에서 쿼리 계획에 대 한 표준 편차입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**avg_clr_time**|**float**|CLR 시간 (마이크로초 단위로 보고) 집계 간격 내에서 쿼리 계획에 대 한 평균입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**last_clr_time**|**bigint**|쿼리에 대해 마지막 CLR 시간 (마이크로초 단위로 보고) 집계 간격 내에서 계획 합니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**min_clr_time**|**bigint**|집계 간격 (마이크로초 단위로 보고) 내에서 쿼리 계획에 대 한 최소 CLR 시간입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**max_clr_time**|**bigint**|집계 간격 (마이크로초 단위로 보고) 내에서 쿼리 계획에 대 한 최대 CLR 시간입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**stdev_clr_time**|**float**|집계 간격 (마이크로초 단위로 보고) 내에서 쿼리 계획에 대 한 CLR 시간 표준 편차입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**avg_dop**|**float**|집계 간격 내에서 쿼리 계획에 대 한 평균 DOP (병렬 처리 수준).<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**last_dop**|**bigint**|집계 간격 내에서 쿼리 계획에 대 한 DOP (병렬 처리 수준)를 지속 합니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**min_dop**|**bigint**|집계 간격 내에서 쿼리 계획에 대 한 최소 DOP (병렬 처리 수준).<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**max_dop**|**bigint**|집계 간격 내에서 쿼리 계획에 대 한 최대 DOP (병렬 처리 수준).<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**stdev_dop**|**float**|집계 간격 내에서 쿼리 계획에 대 한 표준 편차를 DOP (병렬 처리 수준)입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**avg_query_max_used_memory**|**float**|평균 메모리 부여 (8KB 페이지 수로 보고) 집계 간격 내에서 쿼리 계획에 대 한 합니다. 항상 0 기본적으로 사용 하는 쿼리 메모리 액세스에 최적화 된 프로시저 컴파일됩니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**last_query_max_used_memory**|**bigint**|마지막 메모리 부여 (8KB 페이지 수로 보고) 집계 간격 내에서 쿼리 계획에 대 한 합니다. 항상 0 기본적으로 사용 하는 쿼리 메모리 액세스에 최적화 된 프로시저 컴파일됩니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**min_query_max_used_memory**|**bigint**|최소 메모리 부여 (8KB 페이지 수로 보고) 집계 간격 내에서 쿼리 계획에 대 한 합니다. 항상 0 기본적으로 사용 하는 쿼리 메모리 액세스에 최적화 된 프로시저 컴파일됩니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**max_query_max_used_memory**|**bigint**|최대 메모리 부여 (8KB 페이지 수로 보고) 집계 간격 내에서 쿼리 계획을 위해. 항상 0 기본적으로 사용 하는 쿼리 메모리 액세스에 최적화 된 프로시저 컴파일됩니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**stdev_query_max_used_memory**|**float**|메모리 집계 간격 내에서 쿼리 계획에 대 한 표준 편차 (8KB 페이지 수로 보고 됨)를 부여 합니다. 항상 0 기본적으로 사용 하는 쿼리 메모리 액세스에 최적화 된 프로시저 컴파일됩니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**avg_rowcount**|**float**|평균 집계 간격 내에서 쿼리 계획에 대 한 반환 된 행 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**last_rowcount**|**bigint**|마지막 집계 간격 내에서 쿼리 계획을 실행 하 여 반환 된 행 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**min_rowcount**|**bigint**|쿼리에 대해 반환 되는 행의 최소 수 집계 기간 내의 계획.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**max_rowcount**|**bigint**|집계 기간 내 쿼리에 대해 반환 되는 행의 최대 수를 계획합니다.|  
|**stdev_rowcount**|**float**|집계 기간 내에서 쿼리 계획에 대 한 표준 편차를 반환 되는 행 수입니다.|
|**avg_log_bytes_used**|**float**|평균 집계 간격 내에서 쿼리 계획을 사용 하는 데이터베이스 로그 바이트 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**last_log_bytes_used**|**bigint**|마지막 집계 간격 내에서 쿼리 계획을 실행 하 여 사용 하는 데이터베이스 로그 바이트 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**min_log_bytes_used**|**bigint**|최소 집계 간격 내에서 쿼리 계획을 사용 하는 데이터베이스 로그 바이트 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**max_log_bytes_used**|**bigint**|최대 집계 간격 내에서 쿼리 계획을 사용 하는 데이터베이스 로그 바이트 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|
|**stdev_log_bytes_used**|**float**|표준 편차 집계 간격 내에서 쿼리 계획을 사용 하는 데이터베이스 로그 바이트 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 영 (0)를 항상 반환 됩니다.|  
|**avg_page_server_io_reads**|**float**|집계 간격 내에서 쿼리 계획에 대 한 페이지의 평균 server IO 읽기 수입니다. (8KB 페이지 읽기 수로 표현 됨).<br><br/>**참고:** 적용 대상: Azure SQL Database 대규모</br> Azure SQL Data Warehouse, Azure SQL DB, MI (비 대규모) 항상 0을 반환 합니다.|
|**last_page_server_io_reads**|**bigint**|집계 간격 내에서 쿼리 계획에 대 한 마지막 페이지 서버 IO 수를 읽습니다. (8KB 페이지 읽기 수로 표현 됨).<br><br/>**참고:** 적용 대상: Azure SQL Database 대규모 </br> Azure SQL Data Warehouse, Azure SQL DB, MI (비 대규모) 항상 0을 반환 합니다.|
|**min_page_server_io_reads**|**bigint**|집계 간격 내에서 쿼리 계획에 대 한 페이지의 최소 서버 IO 읽기 수입니다. (8KB 페이지 읽기 수로 표현 됨).<br><br/>**참고:** 적용 대상: Azure SQL Database 대규모 </br> Azure SQL Data Warehouse, Azure SQL DB, MI (비 대규모) 항상 0을 반환 합니다.|
|**max_page_server_io_reads**|**bigint**|집계 간격 내에서 쿼리 계획에 대 한 최대 페이지 서버 IO 읽기 수입니다. (8KB 페이지 읽기 수로 표현 됨).<br><br/>**참고:** 적용 대상: Azure SQL Database 대규모 </br> Azure SQL Data Warehouse, Azure SQL DB, MI (비 대규모) 항상 0을 반환 합니다.|
|**stdev_page_server_io_reads**|**float**|페이지 서버 IO 수가 집계 간격 내에서 쿼리 계획에 대 한 표준 편차를 읽습니다. (8KB 페이지 읽기 수로 표현 됨).<br><br/>**참고:** 적용 대상: Azure SQL Database 대규모 </br> Azure SQL Data Warehouse, Azure SQL DB, MI (비 대규모) 항상 0을 반환 합니다.|
  
## <a name="permissions"></a>사용 권한  
 필요 합니다 **VIEW DATABASE STATE** 권한.  
  
## <a name="see-also"></a>관련 항목  
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [쿼리 저장소 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
