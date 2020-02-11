---
title: sys. query_store_runtime_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
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
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0bd7f1870a88ae2050445050565e0f268f4d9b0e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70148292"
---
# <a name="sysquery_store_runtime_stats-transact-sql"></a>sys. query_store_runtime_stats (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  쿼리에 대 한 런타임 실행 통계 정보에 대 한 정보를 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|**Plan_id**, **execution_type** 및 **runtime_stats_interval_id**에 대 한 런타임 실행 통계를 나타내는 행의 식별자입니다. 이전 런타임 통계 간격에 대해서만 고유 합니다. 현재 활성 간격의 경우 **plan_id**에서 참조 하는 계획에 대 한 런타임 통계를 나타내는 여러 행이 **execution_type**표시 되는 실행 유형과 함께 있을 수 있습니다. 일반적으로 한 행은 디스크에 플러시된 런타임 통계를 나타내고 다른 하나는 메모리 내 상태를 나타냅니다. 따라서 모든 간격에 대 한 실제 상태를 가져오려면 메트릭을 집계 하 고 **plan_id**, **execution_type** 및 **runtime_stats_interval_id**를 기준으로 그룹화 해야 합니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**plan_id**|**bigint**|외래 키입니다. [Transact-sql&#41;&#40;query_store_plan ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)에 조인 합니다.|  
|**runtime_stats_interval_id**|**bigint**|외래 키입니다. [Transact-sql&#41;&#40;query_store_runtime_stats_interval ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)에 조인 합니다.|  
|**execution_type**|**tinyint**|쿼리 실행 유형을 결정 합니다.<br /><br /> 0-일반 실행 (완료 됨)<br /><br /> 3-클라이언트에서 시작한 실행 중단<br /><br /> 4-예외 실행 중단|  
|**execution_type_desc**|**nvarchar(128)**|실행 형식 필드에 대 한 텍스트 설명입니다.<br /><br /> 0-일반<br /><br /> 3-중단 됨<br /><br /> 4-예외|  
|**first_execution_time**|**datetimeoffset**|집계 간격 내의 쿼리 계획에 대 한 첫 번째 실행 시간입니다. 이는 쿼리 실행의 종료 시간을 나타냅니다.|  
|**last_execution_time**|**datetimeoffset**|집계 간격 내의 쿼리 계획에 대 한 마지막 실행 시간입니다. 이는 쿼리 실행의 종료 시간을 나타냅니다.|  
|**count_executions**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 총 실행 수입니다.|  
|**avg_duration**|**float**|집계 간격 (마이크로초 단위로 보고) 내의 쿼리 계획에 대 한 평균 기간입니다.|  
|**last_duration**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 마지막 기간 (마이크로초 단위)입니다.|  
|**min_duration**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최소 기간 (마이크로초 단위)입니다.|  
|**max_duration**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최대 기간 (마이크로초 단위)입니다.|  
|**stdev_duration**|**float**|집계 간격 내의 쿼리 계획에 대 한 기간 표준 편차 (마이크로초 단위로 보고 됨)|  
|**avg_cpu_time**|**float**|집계 간격 내의 쿼리 계획에 대 한 평균 CPU 시간 (마이크로초 단위)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_cpu_time**|**bigint**|집계 간격 (마이크로초 단위로 보고 됨) 내의 쿼리 계획에 대 한 마지막 CPU 시간입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**min_cpu_time**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최소 CPU 시간 (마이크로초 단위)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**max_cpu_time**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최대 CPU 시간 (마이크로초 단위)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**stdev_cpu_time**|**float**|집계 간격 내의 쿼리 계획에 대 한 CPU 시간 표준 편차 (마이크로초 단위로 보고 됨)<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**avg_logical_io_reads**|**float**|집계 간격 내의 쿼리 계획에 대 한 평균 논리적 i/o 읽기 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_logical_io_reads**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 마지막 논리적 i/o 읽기 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**min_logical_io_reads**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최소 논리적 i/o 읽기 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**max_logical_io_reads**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최대 논리적 i/o 읽기 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**stdev_logical_io_reads**|**float**|집계 간격 내의 쿼리 계획에 대 한 논리적 i/o의 수를 읽습니다. (8KB 페이지 읽기 수로 표시 됨).<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**avg_logical_io_writes**|**float**|집계 간격 내의 쿼리 계획에 대 한 평균 논리적 i/o 쓰기 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_logical_io_writes**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 마지막 논리적 i/o 쓰기 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**min_logical_io_writes**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최소 논리적 i/o 쓰기 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**max_logical_io_writes**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최대 논리적 i/o 쓰기 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**stdev_logical_io_writes**|**float**|집계 간격 내의 쿼리 계획에 대 한 논리 i/o의 표준 편차 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**avg_physical_io_reads**|**float**|집계 간격 내의 쿼리 계획에 대 한 실제 i/o 읽기 수입니다 (8KB 페이지 읽기 수로 표시 됨).<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_physical_io_reads**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 실제 실제 i/o 읽기 수 (8KB 페이지 읽기 수로 표시 됨)<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**min_physical_io_reads**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 물리적 i/o 읽기의 최소 수입니다 (8KB 페이지 읽기 수로 표시 됨).<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**max_physical_io_reads**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 실제 i/o 읽기의 최대 수입니다 (8KB 페이지 읽기 수로 표시 됨).<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**stdev_physical_io_reads**|**float**|실제 i/o 수는 집계 간격 내의 쿼리 계획에 대 한 표준 편차를 읽습니다 (8KB 페이지 읽기 수로 표시 됨).<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**avg_clr_time**|**float**|집계 간격 내의 쿼리 계획에 대 한 평균 CLR 시간 (마이크로초 단위)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_clr_time**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 마지막 CLR 시간 (마이크로초 단위)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**min_clr_time**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최소 CLR 시간 (마이크로초 단위)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**max_clr_time**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최대 CLR 시간 (마이크로초 단위)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**stdev_clr_time**|**float**|집계 간격 내의 쿼리 계획에 대 한 CLR 시간 표준 편차 (마이크로초 단위로 보고 됨)<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**avg_dop**|**float**|집계 간격 내의 쿼리 계획에 대 한 평균 DOP (병렬 처리 수준)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_dop**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 마지막 DOP (병렬 처리 수준)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**min_dop**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최소 DOP (병렬 처리 수준)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**max_dop**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최대 DOP (병렬 처리 수준)입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**stdev_dop**|**float**|집계 간격 내의 쿼리 계획에 대 한 DOP (병렬 처리 수준) 표준 편차<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**avg_query_max_used_memory**|**float**|집계 간격 내의 쿼리 계획에 대 한 평균 메모리 부여 (8kb 페이지 수로 보고 됨)입니다. 고유 하 게 컴파일된 메모리 액세스에 최적화 된 프로시저를 사용 하는 쿼리의 경우 항상 0입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_query_max_used_memory**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 마지막 메모리 부여 (8kb 페이지 수로 보고 됨)입니다. 고유 하 게 컴파일된 메모리 액세스에 최적화 된 프로시저를 사용 하는 쿼리의 경우 항상 0입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**min_query_max_used_memory**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최소 메모리 부여 (8kb 페이지 수로 보고 됨)입니다. 고유 하 게 컴파일된 메모리 액세스에 최적화 된 프로시저를 사용 하는 쿼리의 경우 항상 0입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**max_query_max_used_memory**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최대 메모리 부여 (8kb 페이지 수로 보고 됨) 고유 하 게 컴파일된 메모리 액세스에 최적화 된 프로시저를 사용 하는 쿼리의 경우 항상 0입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**stdev_query_max_used_memory**|**float**|집계 간격 내의 쿼리 계획에 대 한 메모리 부여 표준 편차 (8kb 페이지 수로 보고 됨) 고유 하 게 컴파일된 메모리 액세스에 최적화 된 프로시저를 사용 하는 쿼리의 경우 항상 0입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**avg_rowcount**|**float**|집계 간격 내의 쿼리 계획에 대해 반환 되는 평균 행 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_rowcount**|**bigint**|집계 간격 내의 쿼리 계획을 마지막으로 실행 했을 때 반환 된 행 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**min_rowcount**|**bigint**|집계 간격 내의 쿼리 계획에 대해 반환 되는 최소 행 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**max_rowcount**|**bigint**|집계 간격 내의 쿼리 계획에 대해 반환 되는 최대 행 수입니다.|  
|**stdev_rowcount**|**float**|집계 간격 내의 쿼리 계획에 대 한 반환 된 행 표준 편차 수입니다.|
|**avg_log_bytes_used**|**float**|집계 간격 내에서 쿼리 계획에 사용 되는 데이터베이스 로그의 평균 바이트 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**last_log_bytes_used**|**bigint**|집계 간격 내의 쿼리 계획을 마지막으로 실행 하는 데 사용 되는 데이터베이스 로그의 바이트 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**min_log_bytes_used**|**bigint**|집계 간격 내에서 쿼리 계획에 사용 되는 데이터베이스 로그의 최소 바이트 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**max_log_bytes_used**|**bigint**|집계 간격 내에서 쿼리 계획에 사용 되는 데이터베이스 로그의 최대 바이트 수입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|
|**stdev_log_bytes_used**|**float**|집계 간격 내에서 쿼리 계획에 사용 되는 데이터베이스 로그의 바이트 수에 대 한 표준 편차입니다.<br/>**참고:** Azure SQL Data Warehouse는 항상 0을 반환 합니다.|  
|**avg_tempdb_space_used**|**float**|집계 간격 내의 쿼리 계획에 대 한 평균 페이지 읽기 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br><br/>**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|
|**last_tempdb_space_used**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 마지막 페이지 읽기 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br><br/>**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|
|**min_tempdb_space_used**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최소 페이지 읽기 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br><br/>**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|
|**max_tempdb_space_used**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 최대 페이지 읽기 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br><br/>**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|
|**stdev_tempdb_space_used**|**float**|페이지 수는 집계 간격 내의 쿼리 계획에 대 한 표준 편차를 읽습니다. (8KB 페이지 읽기 수로 표시 됨).<br><br/>**적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (부터 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|
|**avg_page_server_io_reads**|**float**|집계 간격 내의 쿼리 계획에 대 한 페이지 서버 i/o 읽기의 평균 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br><br/>**적용 대상:** Azure SQL Database Hyperscale</br>**참고:** Azure SQL Data Warehouse Azure SQL DB, MI (비 hyperscale)는 항상 0을 반환 합니다.|
|**last_page_server_io_reads**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 페이지 서버 i/o 읽기의 마지막 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br><br/>**적용 대상:** Azure SQL Database Hyperscale</br>**참고:** Azure SQL Data Warehouse Azure SQL DB, MI (비 hyperscale)는 항상 0을 반환 합니다.|
|**min_page_server_io_reads**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 페이지 서버 i/o 읽기의 최소 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br><br/>**적용 대상:** Azure SQL Database Hyperscale</br>**참고:** Azure SQL Data Warehouse Azure SQL DB, MI (비 hyperscale)는 항상 0을 반환 합니다.|
|**max_page_server_io_reads**|**bigint**|집계 간격 내의 쿼리 계획에 대 한 페이지 서버 i/o 읽기의 최대 수입니다. (8KB 페이지 읽기 수로 표시 됨).<br><br/>**적용 대상:** Azure SQL Database Hyperscale</br>**참고:** Azure SQL Data Warehouse Azure SQL DB, MI (비 hyperscale)는 항상 0을 반환 합니다.|
|**stdev_page_server_io_reads**|**float**|페이지 서버 i/o 수 집계 간격 내의 쿼리 계획에 대 한 표준 편차를 읽습니다. (8KB 페이지 읽기 수로 표시 됨).<br><br/>**적용 대상:** Azure SQL Database Hyperscale</br>**참고:** Azure SQL Data Warehouse Azure SQL DB, MI (비 hyperscale)는 항상 0을 반환 합니다.|
  
## <a name="permissions"></a>사용 권한  
`VIEW DATABASE STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_context_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [query_store_wait_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)    
 [쿼리 저장소에 대한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md)   
  
