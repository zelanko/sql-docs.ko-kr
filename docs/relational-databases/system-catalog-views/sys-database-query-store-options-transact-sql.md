---
title: sys. database_query_store_options (Transact-sql) | Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5f2c8189c19fbdf6dc9a83e62117da517322df86
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983166"
---
# <a name="sysdatabase_query_store_options-transact-sql"></a>sys. database_query_store_options (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  이 데이터베이스에 대 한 쿼리 저장소 옵션을 반환 합니다.  
  
**적용**대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|사용자가 명시적으로 설정한 쿼리 저장소의 원하는 작업 모드를 나타냅니다.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar(60)**|쿼리 저장소의 원하는 작업 모드에 대 한 텍스트 설명입니다.<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|쿼리 저장소의 작업 모드를 나타냅니다. 사용자가 요구 하는 필요한 상태 목록 외에도 실제 상태는 오류 상태가 될 수 있습니다.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = 오류|  
|**actual_state_desc**|**nvarchar(60)**|쿼리 저장소의 실제 작업 모드에 대 한 텍스트 설명입니다.<br />OFF<br />READ_ONLY<br />READ_WRITE<br />ERROR<br /><br /> 실제 상태가 원하는 상태와 다른 경우는 다음과 같습니다.<br />-데이터베이스를 읽기 전용 모드로 설정 하거나 쿼리 저장소 크기가 구성 된 할당량을 초과 하는 경우 사용자가 읽기/쓰기를 지정한 경우에도 읽기 전용 모드에서 쿼리 저장소 수 있습니다.<br />-극단적인 시나리오에서는 내부 오류로 인해 오류 상태를 입력할 수 쿼리 저장소. 이 문제가 발생 하는 경우 SQL 2017 이상에서 영향을 받는 데이터베이스의 `sp_query_store_consistency_check` 저장 프로시저를 실행 하 여 쿼리 저장소를 복구할 수 있습니다. `sp_query_store_consistency_check` 실행 중이 고 SQL 2016에 대해를 실행 하 여 데이터를 지워야 하는 경우 `ALTER DATABASE [YourDatabaseName] SET QUERY_STORE CLEAR ALL;`|  
|**readonly_reason**|**int**|**Desired_state_desc** READ_WRITE 되 고 **actual_state_desc** READ_ONLY 경우 readonly_reason가 readonly 모드에 있는 이유를 나타내는 비트 **맵을 반환 합니다** .<br /><br /> **1** -데이터베이스가 읽기 전용 모드입니다.<br /><br /> **2** -데이터베이스가 단일 사용자 모드입니다.<br /><br /> **4** -데이터베이스가 응급 모드입니다.<br /><br /> **8** -데이터베이스가 보조 복제본입니다 (Always On 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 지역에서 복제에 적용 됨). 이 값은 **읽기** 가능한 보조 복제본 에서만 효과적으로 관찰할 수 있습니다.<br /><br /> **65536** -쿼리 저장소 MAX_STORAGE_SIZE_MB 옵션에 설정 된 크기 제한에 도달 했습니다.<br /><br /> **131072** -쿼리 저장소의 다른 문 수가 내부 메모리 제한에 도달 했습니다. 읽기/쓰기 모드로 쿼리 저장소를 전송할 수 있도록 더 높은 서비스 계층으로 업그레이드 하거나 필요 하지 않은 쿼리를 제거 하는 것이 좋습니다.<br />**적용 대상:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]을 참조하세요.<br /><br /> **262144** -디스크에 유지 되기를 기다리는 메모리 내 항목의 크기가 내부 메모리 제한에 도달 했습니다. 쿼리 저장소는 메모리 내 항목이 디스크에 유지 될 때까지 일시적으로 읽기 전용 모드가 됩니다. <br />**적용 대상:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]을 참조하세요.<br /><br /> **524288** -데이터베이스가 디스크 크기 제한에 도달 했습니다. 쿼리 저장소은 사용자 데이터베이스의 일부 이므로 데이터베이스에 사용 가능한 공간이 더 이상 없는 경우 쿼리 저장소 더 이상 확장할 수 없습니다.<br />**적용 대상:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]을 참조하세요. <br /> <br /> 쿼리 저장소 작업 모드를 읽기/쓰기로 전환 하려면 쿼리 저장소를 사용 하 여 [모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md#Verify)의 **쿼리 데이터를 지속적으로 수집 쿼리 저장소 확인** 을 참조 하세요.|  
|**current_storage_size_mb**|**bigint**|디스크의 쿼리 저장소 크기 (mb)입니다.|  
|**flush_interval_seconds**|**bigint**|쿼리 저장소 데이터를 디스크에 정기적으로 플러시하는 기간 (초)입니다. 기본값은 **900** (15 분)입니다.<br /><br /> `ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)` 문을 사용 하 여 변경 합니다.|  
|**interval_length_minutes**|**bigint**|통계 집계 간격 (분)입니다. 임의 값은 허용 되지 않습니다. 다음 중 하나를 사용 합니다. 1, 5, 10, 15, 30, 60 및 1440 분 기본값은 **60** 분입니다.|  
|**max_storage_size_mb**|**bigint**|쿼리 저장소에 대 한 최대 디스크 크기 (mb)입니다. 기본값은 **100** MB입니다.<br />[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium edition의 경우 기본값은 1gb이 고 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic 버전의 경우 기본값은 10mb입니다.<br /><br /> `ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)` 문을 사용 하 여 변경 합니다.|  
|**stale_query_threshold_days**|**bigint**|정책 설정이 없는 쿼리가 쿼리 저장소에 유지 되는 일 수입니다. 기본값은 **30**입니다. 보존 정책을 사용 하지 않으려면 0으로 설정 합니다.<br />[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic 버전의 경우 기본값은 7일입니다.<br /><br /> `ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )` 문을 사용 하 여 변경 합니다.|  
|**max_plans_per_query**|**bigint**|저장 된 계획의 최대 수를 제한 합니다. 기본값은 **200**입니다. 최 댓 값에 도달 하면 쿼리 저장소 해당 쿼리에 대 한 새 계획의 캡처가 중지 됩니다. 를 0으로 설정 하면 캡처된 계획의 수와 관련 된 제한이 제거 됩니다.<br /><br /> `ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)` 문을 사용 하 여 변경 합니다.|  
|**query_capture_mode**|**smallint**|현재 활성 쿼리 캡처 모드:<br /><br /> **1** = 모두-모든 쿼리가 캡처됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상)에 대 한 기본 구성 값입니다.<br /><br /> 2 = 실행 수 및 리소스 소비량에 따라 관련 쿼리를 자동으로 캡처합니다. 이것이 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]에 대한 기본 구성 값입니다.<br /><br /> 3 = 없음-새 쿼리 캡처를 중지 합니다. Query Store는 이미 캡처된 쿼리에 대한 컴파일 및 런타임 통계를 계속 수집합니다. 중요 한 쿼리 캡처가 누락 될 수 있으므로이 구성을 신중 하 게 사용 합니다.|  
|**query_capture_mode_desc**|**nvarchar(60)**|쿼리 저장소의 실제 캡처 모드에 대 한 텍스트 설명입니다.<br /><br /> 모두 ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 기본값)<br /><br /> **AUTO** ([!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]의 기본값)<br /><br /> 없음|  
|**size_based_cleanup_mode**|**smallint**|총 데이터 양이 최대 크기에 가까워지면 정리가 자동으로 활성화될지 여부를 제어합니다.<br /><br /> 0 = 오프-크기 기반 정리가 자동으로 활성화 되지 않습니다.<br /><br /> **1** = 디스크의 크기가 *max_storage_size_mb*의 **90%** 에 도달 하면 자동 크기 조정 기반 정리가 자동으로 활성화 됩니다. 이것은 기본 구성 값입니다.<br /><br />크기 기반 정리는 가장 저렴하고 가장 오래된 쿼리를 먼저 제거합니다. *Max_storage_size_mb* 약 **80%** 에 도달 하면 중지 됩니다.|  
|**size_based_cleanup_mode_desc**|**nvarchar(60)**|쿼리 저장소의 실제 크기 기반 정리 모드에 대 한 텍스트 설명입니다.<br /><br /> OFF <br /> **AUTO** (기본값)|  
|**wait_stats_capture_mode**|**smallint**|쿼리 저장소 대기 통계의 캡처를 수행할지 여부를 제어 합니다. <br /><br /> 0 = OFF <br /> **1** = ON<br /> **적용 대상**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 이상|
|**wait_stats_capture_mode_desc**|**nvarchar(60)**|실제 대기 통계 캡처 모드에 대 한 텍스트 설명입니다. <br /><br /> OFF <br /> **켜** 않음 (기본값)<br /> **적용 대상**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 이상| 
  
## <a name="permissions"></a>사용 권한  
 `VIEW DATABASE STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [query_context_settings &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_plan &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [query_store_runtime_stats &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats_interval &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [fn_stmt_sql_handle_from_sql_stmt &#40;transact-sql&#41; ](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [Transact-sql 저장 프로시저 &#40;쿼리 저장소&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
