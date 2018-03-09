---
title: sys.database_query_store_options (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 46710eb543ae038d22052cd55b356df9458201e3
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="sysdatabasequerystoreoptions-transact-sql"></a>sys.database_query_store_options (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 데이터베이스에 대 한 쿼리 저장소 옵션을 반환합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|사용자가 명시적으로 설정 하는 쿼리 저장소의 원하는 작업 모드를 나타냅니다.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar(64)**|쿼리 저장소의 원하는 작업 모드에 대 한 텍스트 설명을:<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|쿼리 저장소의 작업 모드를 나타냅니다. 사용자가 필요한 원하는 상태의 목록 외에 실제 상태를 오류 상태로 될 수 있습니다.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = 오류|  
|**actual_state_desc**|**nvarchar(64)**|쿼리 저장소의 실제 작동 모드의 텍스트 설명입니다.<br />OFF<br />READ_ONLY<br />READ_WRITE<br />ERROR<br /><br /> 실제 상태가 필요한 상태에서 다른 하는 데 가지 상황이 있습니다.<br /><br /> 쿼리 저장소 읽기 / 쓰기 사용자가 지정 된 경우에 읽기 전용 모드에서 작동할 수 있습니다. 예를 들어 있는 데이터베이스가 읽기 전용 모드 또는 쿼리 저장소의 크기가 할당량을 초과 하는 경우 발생할 수 있습니다.<br /><br /> 매우 드물게 쿼리 저장소는 결국 오류 상태에서 내부 오류로 인해 합니다. 이 경우 쿼리 저장소를 실행 하 여 복구할 수 **sp_query_store_consistency_check** 영향을 받는 데이터베이스 내에서 프로시저를 저장 합니다.|  
|**readonly_reason**|**int**|경우는 **desired_state_desc** READ_WRITE입니다. 및 **actual_state_desc** READ_ONLY가 **readonly_reason** 반환 약간 쿼리 저장소에 이유를 나타내려면 매핑할 읽기 전용 모드입니다.<br /><br /> 1-데이터베이스가 읽기 전용 모드<br /><br /> 2-데이터베이스가 단일 사용자 모드<br /><br /> 4-데이터베이스가 응급 모드<br /><br /> 8-데이터베이스는 보조 복제본 (Always On 및 Azure에 적용 됩니다 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 지역 복제). 이 값에 대해서만 효과적으로 확인할 수 **읽을 수 있는** 보조 복제본<br /><br /> 65536-쿼리 저장소는 MAX_STORAGE_SIZE_MB 옵션으로 설정한 크기 제한에 도달 했습니다.<br /><br /> 131072-쿼리 저장소의 다른 문의 수에는 내부 메모리 제한에 도달 했습니다. 필요 하지 않은 쿼리를 제거 합니다. 쿼리 저장소를 읽기-쓰기 모드로 전송할 수 있도록 더 높은 서비스 계층으로 업그레이드 하십시오.<br />[!INCLUDE[ssSDS](../../includes/sssds-md.md)]에만 적용됩니다.<br /><br /> 262144 – 디스크에 유지 되도록 대기 중인 메모리에 항목의 크기에는 내부 메모리 제한에 도달 했습니다. 메모리에 항목은 디스크에 저장 될 때까지 일시적으로 읽기 전용 모드에서 쿼리 저장소가 됩니다. <br />[!INCLUDE[ssSDS](../../includes/sssds-md.md)]에만 적용됩니다.<br /><br />524288-데이터베이스에는 디스크 크기 제한에 도달 했습니다. 쿼리 저장소 이므로 사용자 데이터베이스의 일부 쿼리 저장소를 더 확장 없습니다 됨을 의미 하는 데이터베이스에 더 이상 사용 가능한 공간이 있을 경우 더 이상.<br />[!INCLUDE[ssSDS](../../includes/sssds-md.md)]에만 적용됩니다. <br /> <br /> 쿼리 저장소 작업을 전환 하려면 모드 다시 읽기 / 쓰기, 참조로 **확인 쿼리 저장소에서 쿼리 데이터가 계속 수집** 섹션 [쿼리 저장소에 대 한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md)합니다.|  
|**current_storage_size_mb**|**bigint**|쿼리 저장소의 디스크 크기를 메가바이트 단위로 합니다.|  
|**flush_interval_seconds**|**bigint**|디스크에 쿼리 저장소 데이터의 일반 플러시에 대 한 기간을 정의 합니다. 기본값은 900 (15 분)입니다.<br /><br /> 사용 하 여 변경 된 `ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)` 문.|  
|**interval_length_minutes**|**bigint**|통계 집계 간격입니다. 임의의 값이 허용 되지 않습니다. 다음 중 하나를 사용 하 여: 1, 5, 10, 15, 30, 60 및 1440 분입니다. 기본값은 60 분입니다.|  
|**max_storage_size_mb**|**bigint**|쿼리 저장소에 대 한 최대 디스크 크기입니다. 기본값은 100 MB입니다.<br />[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium Edition의 경우 기본값은 1Gb이고, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic Edition의 경우 기본값은 10Mb입니다.<br /><br /> 사용 하 여 변경 된 `ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)` 문.|  
|**stale_query_threshold_days**|**bigint**|정책 설정이 없는지를 쿼리 하는 일 수는 쿼리 저장소에 유지 됩니다. 기본값은 30입니다. 보존 정책을 사용 하지 않으려면 0으로 설정 합니다.<br />[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic 버전의 경우 기본값은 7일입니다.<br /><br /> 사용 하 여 변경 된 `ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )` 문.|  
|**max_plans_per_query**|**bigint**|저장 된 계획의 최대 수를 제한합니다. 기본값은 200입니다. 최대값에 도달 하면 쿼리 저장소는 해당 쿼리에 대 한 새 계획을 캡처를 중지 합니다. 설정을 0으로 캡처된 계획의 수와 관련 한 제한 사항을 제거합니다.<br /><br /> 사용 하 여 변경 된 `ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)` 문.|  
|**query_capture_mode**|**smallint**|현재 활성 쿼리 캡처 모드:<br /><br /> 1 = ALL-모든 쿼리가 캡처됩니다. 이 기본 구성 값에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).<br /><br /> 2 = 자동-실행 횟수 및 리소스 소비량에 따른 캡처 관련 쿼리 합니다. 이 기본 구성 값에 대 한 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.<br /><br /> 3 = NONE-새 쿼리 캡처가 중지 됩니다. 쿼리 저장소는 이미 캡처된 쿼리에 대 한 컴파일 및 런타임 통계를 수집 하도록 계속 됩니다. 사용 하 여이 구성을 신중 하 게 하므로 중요 한 쿼리 캡처를 놓칠 수 있습니다.|  
|**query_capture_mode_desc**|**nvarchar(60)**|쿼리 저장소의 기본 캡처 모드에 대 한 텍스트 설명을:<br /><br /> 모든 (에 대 한 기본 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])<br /><br /> 자동 (에 대 한 기본 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)])<br /><br /> 없음|  
|**size_based_cleanup_mode**|**smallint**|여부 정리를 자동으로 활성화할지 총 데이터 양이 최대 크기에 가까워 하는 경우를 제어 합니다.<br /><br /> 1 = OFF – 크기 기반된 정리를 자동으로 활성화 되지 않습니다.<br /><br /> 2 = 자동-크기 기반된 정리를 자동으로 활성화할지 디스크 사용률이 90%의 도달에 크기가 때 **max_storage_size_mb**합니다. 이것이 기본 구성 값입니다.<br /><br />크기 기반 정리 가장 비용이 많이 드는 주문과 가장 오래 된 쿼리를 먼저 제거합니다. Max_storage_size_mb의 약 80%로 중지합니다.|  
|**size_based_cleanup_mode_desc**|**smallint**|쿼리 저장소의 실제 크기 기반 정리 모드에 대 한 텍스트 설명을:<br /><br /> OFF <br /><br /> 자동 (기본값)|  
|**wait_stats_capture_mode**|**smallint**|쿼리 저장소 대기 통계의 캡처를 수행 하는지 여부를 제어 합니다. <br /><br /> 0 = OFF <br /><br /> 1 = ON<br /> **적용 대상**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|
|**wait_stats_mode_capture_desc**|**nvarchar(60)**|실제 대기 통계 캡처 모드에 대 한 텍스트 설명을: <br /><br /> OFF <br /><br /> ON (기본값)<br /> **적용 대상**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지| 
  
## <a name="permissions"></a>Permissions  
 필요는 **VIEW DATABASE STATE** 권한.  
  
## <a name="see-also"></a>관련 항목:  
 [sys.query_context_settings&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [쿼리 저장소 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
