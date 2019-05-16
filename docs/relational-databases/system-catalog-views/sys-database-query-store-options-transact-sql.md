---
title: sys.database_query_store_options (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DATABASE_QUERY_STORE_OPTIONS_TSQL
- DATABASE_QUERY_STORE_OPTIONS
- SYS.DATABASE_QUERY_STORE_OPTIONS_TSQL
- SYS.DATABASE_QUERY_STORE_OPTIONS
dev_langs:
- TSQL
helpviewer_keywords:
- database_query_store_options catalog view
- sys.database_query_store_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 02f1d456e7b2e6849bd179a4cb42d862e3d06d03
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725136"
---
# <a name="sysdatabasequerystoreoptions-transact-sql"></a>sys.database_query_store_options (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  이 데이터베이스에 대 한 쿼리 저장소 옵션을 반환 합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|사용자가 명시적으로 설정 되는 쿼리 저장소의 원하는 작업 모드를 나타냅니다.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar(60)**|쿼리 저장소의 원하는 작업 모드의 텍스트 설명:<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|쿼리 저장소의 작업 모드를 나타냅니다. 사용자가 필요한 원하는 상태의 목록 외에도 실제 상태는 오류 상태를 수 있습니다.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = ERROR|  
|**actual_state_desc**|**nvarchar(60)**|쿼리 저장소의 실제 작업 모드의 텍스트 설명입니다.<br />OFF<br />READ_ONLY<br />READ_WRITE<br />ERROR<br /><br /> 실제 상태가 필요한 상태에서 다른 경우가 있습니다.<br />-데이터베이스 읽기 전용 모드로 설정 된 경우, 쿼리 저장소 크기가 구성 된 할당량을 초과 하는 경우 쿼리 저장소는 읽기 / 쓰기 사용자가 지정 된 경우에 읽기 전용 모드에서 작동할 수 있습니다.<br />-극단적인 시나리오에서 쿼리 저장소 내부 오류로 인해 오류 상태를 입력할 수 있습니다. 쿼리 저장소를 실행 하 여 복구할 수 있습니다 SQL 2017 이상 버전에서는 이런 경우는 `sp_query_store_consistency_check` 영향을 받는 데이터베이스에서 저장 프로시저입니다. 실행 하는 경우 `sp_query_store_consistency_check` 작동 하지 않는 SQL 2016를 실행 하 여 데이터의 선택을 취소 해야 하 고 `ALTER DATABASE [YourDatabaseName] SET QUERY_STORE CLEAR ALL;`|  
|**readonly_reason**|**int**|경우는 **desired_state_desc** READ_WRITE입니다와 **actual_state_desc** READ_ONLY,입니다 **readonly_reason** 반환 쿼리 저장소에 이유를 나타내려면 매핑할 약간 읽기 전용 모드입니다.<br /><br /> **1** -데이터베이스가 읽기 전용 모드<br /><br /> **2** -데이터베이스가 단일 사용자 모드<br /><br /> **4** -데이터베이스가 응급 모드<br /><br /> **8** -데이터베이스가 보조 복제본 (Always On에 적용 됩니다 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 지역에서 복제). 이 값에만 효과적으로 확인할 수 있습니다 **읽을 수 있는** 보조 복제본<br /><br /> **65536** -쿼리 저장소 MAX_STORAGE_SIZE_MB 옵션으로 설정 된 크기 제한에 도달 했습니다.<br /><br /> **131072** -쿼리 저장소에서 다른 문 수에는 내부 메모리 제한에 도달 했습니다. 필요 하지 않은 쿼리를 제거 하거나 쿼리 저장소를 읽기-쓰기 모드로 전송할 수 있도록 더 높은 서비스 계층으로 업그레이드 하는 것이 좋습니다.<br />**적용 대상:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]을 참조하세요.<br /><br /> **262144** -디스크에 유지 하려고 대기 하는 메모리 내 항목의 크기에는 내부 메모리 제한에 도달 했습니다. 쿼리 저장소 디스크에 유지 되는 메모리 내 항목이 때까지 일시적으로 읽기 전용 모드로 됩니다. <br />**적용 대상:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]을 참조하세요.<br /><br /> **524288** -데이터베이스에는 디스크 크기 제한에 도달 했습니다. 쿼리 저장소 이므로 사용자 데이터베이스에 포함 하는 것을 의미 하는 데이터베이스에 더 이상 사용 가능한 공간이 쿼리 저장소가 더 커질 수 없습니다 더 이상.<br />**적용 대상:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]을 참조하세요. <br /> <br /> 쿼리 저장소 작업을 전환할 모드로 다시 읽기 / 쓰기를 참조 하십시오 **확인 쿼리 저장소에서 쿼리 데이터가 계속 수집** 부분 [쿼리 저장소 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md#Verify)합니다.|  
|**current_storage_size_mb**|**bigint**|쿼리 저장소의 디스크 크기를 메가바이트에서입니다.|  
|**flush_interval_seconds**|**bigint**|일반 쿼리 저장소 데이터를 디스크에 플러시하기 (초)에서에 대 한 기간입니다. 기본값은 **900** (15 분)입니다.<br /><br /> 사용 하 여 변경 된 `ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)` 문입니다.|  
|**interval_length_minutes**|**bigint**|통계 집계 간격 (분)입니다. 임의의 값이 허용 되지 않습니다. 다음 중 하나를 사용합니다. 1, 5, 10, 15, 30, 60 및 1440 분. 기본값은 **60** 분입니다.|  
|**max_storage_size_mb**|**bigint**|최대 디스크 크기 (mb)의 쿼리 저장소입니다. 기본값은 **100** MB입니다.<br />에 대 한 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium edition의 경우 기본값은 1GB 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic edition의 경우 기본값은 10MB입니다.<br /><br /> 사용 하 여 변경 된 `ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)` 문입니다.|  
|**stale_query_threshold_days**|**bigint**|정책 설정이 없는지를 사용 하 여 쿼리 하는 일 수는 쿼리 저장소에 보관 됩니다. 기본값은 **30**합니다. 보존 정책을 사용 하지 않으려면 0으로 설정 합니다.<br />[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic 버전의 경우 기본값은 7일입니다.<br /><br /> 사용 하 여 변경 된 `ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )` 문입니다.|  
|**max_plans_per_query**|**bigint**|저장 된 계획의 최대 수를 제한합니다. 기본값은 **200**합니다. 최 댓 값에 도달 하는 경우 쿼리 저장소는 쿼리에 대 한 새 계획을 캡처를 중지 합니다. 캡처된 계획의 수와 관련 하 여 제한 사항을 제거 하는 0으로 설정 합니다.<br /><br /> 사용 하 여 변경 된 `ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)` 문입니다.|  
|**query_capture_mode**|**smallint**|현재 활성 쿼리 캡처 모드:<br /><br /> **1** = ALL-모든 쿼리가 캡처됩니다. 에 대 한 기본 구성 값을 이것이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).<br /><br /> 2 = AUTO-실행 횟수 및 리소스 사용량을 기준으로 관련 쿼리를 캡처합니다. 이것이 기본 구성 값에 대 한 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.<br /><br /> 3 = NONE-새 쿼리 캡처가 중지 됩니다. Query Store는 이미 캡처된 쿼리에 대한 컴파일 및 런타임 통계를 계속 수집합니다. 사용 하 여이 구성을 신중 하 게 하므로 중요 한 쿼리 캡처를 놓칠 수 있습니다.|  
|**query_capture_mode_desc**|**nvarchar(60)**|쿼리 저장소 캡처 모드의 텍스트 설명:<br /><br /> 모든 (에 대 한 기본 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])<br /><br /> **자동** (기본값 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)])<br /><br /> 없음|  
|**size_based_cleanup_mode**|**smallint**|총 데이터 양이 최대 크기에 가까워지면 정리가 자동으로 활성화될지 여부를 제어합니다.<br /><br /> 0 = OFF-크기 기반 정리를 자동으로 활성화 되지 않습니다.<br /><br /> **1** = AUTO-디스크 크기에 도달 하면 크기 기반 정리 자동으로 활성화 됩니다 **90%** 의 *max_storage_size_mb*합니다. 이것은 기본 구성 값입니다.<br /><br />크기 기반 정리는 가장 저렴하고 가장 오래된 쿼리를 먼저 제거합니다. 약 중지 되기 **80%** 의 *max_storage_size_mb* 에 도달 합니다.|  
|**size_based_cleanup_mode_desc**|**nvarchar(60)**|쿼리 저장소의 실제 크기 기반 정리 모드의 텍스트 설명:<br /><br /> OFF <br /> **자동** (기본값)|  
|**wait_stats_capture_mode**|**smallint**|쿼리 저장소 대기 통계의 캡처를 수행 하는지 여부를 제어 합니다. <br /><br /> 0 = OFF <br /> **1** = ON<br /> **적용 대상**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|
|**wait_stats_capture_mode_desc**|**nvarchar(60)**|실제 대기 통계 캡처 모드의 텍스트 설명: <br /><br /> OFF <br /> **ON** (기본값)<br /> **적용 대상**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
  
## <a name="permissions"></a>사용 권한  
 `VIEW DATABASE STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.query_context_settings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [쿼리 저장소 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
