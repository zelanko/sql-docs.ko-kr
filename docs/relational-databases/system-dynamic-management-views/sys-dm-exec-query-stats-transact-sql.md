---
title: sys.dm_exec_query_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_query_stats_TSQL
- dm_exec_query_stats
- sys.dm_exec_query_stats
- sys.dm_exec_query_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_stats dynamic management view
ms.assetid: eb7b58b8-3508-4114-97c2-d877bcb12964
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8874b5ba3eca2f3e9d72874af7440934fc2ec20f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmexecquerystats-transact-sql"></a>sys.dm_exec_query_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  캐시 된 쿼리 계획에 대 한 집계 성능 통계를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이 뷰에는 캐시된 계획 내의 쿼리 문당 하나의 행이 포함되어 있습니다. 행의 유효 기간은 계획 자체와 연결되어 있습니다. 캐시에서 계획이 제거되면 이 뷰에서도 해당 행이 제거됩니다.  
  
> [!NOTE]
> 초기 쿼리 **sys.dm_exec_query_stats** 중인 서버에서 현재 실행 중인 작업이 있을 경우 부정확 한 결과가 나올 수 있습니다. 쿼리를 다시 실행하면 보다 정확한 결과를 확인할 수 있습니다.  
  
> [!NOTE]
> 이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_exec_query_stats**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**sql_handle**|**varbinary(64)**  |쿼리가 속하는 일괄 처리 또는 저장 프로시저를 참조하는 토큰입니다.<br /><br /> **sql_handle**함께 **statement_start_offset** 및 **statement_end_offset**는 호출 하 여 쿼리의 SQL 텍스트를 검색 하는 데 사용할 수는 **sys.dm_exec_sql _text** 동적 관리 함수입니다.|  
|**statement_start_offset**|**int**|0부터 시작하여 일괄 처리 또는 지속형 개체의 텍스트 내에서 행이 설명하는 쿼리의 시작 위치(바이트)를 나타냅니다.|  
|**statement_end_offset**|**int**|0부터 시작하여 일괄 처리 또는 지속형 개체의 텍스트 내에서 행이 설명하는 쿼리의 끝 위치(바이트)를 나타냅니다. 이전 버전에 대 한 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], 값이-1은 일괄 처리의 끝을 나타냅니다. 후행 주석은 더 이상 포함 됩니다.|  
|**plan_generation_num**|**bigint**|다시 컴파일한 후 계획의 인스턴스 간을 서로 구별하는 데 사용될 수 있는 시퀀스 번호입니다.|  
|**plan_handle**|**varbinary(64)**|쿼리가 속하는 컴파일된 계획을 참조하는 토큰입니다. 이 값에 전달할 수는 [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) 동적 관리 함수를 쿼리 계획을 가져옵니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0x000입니다.|  
|**creation_time**|**datetime**|이 계획이 컴파일된 시간입니다.|  
|**last_execution_time**|**datetime**|이 계획이 마지막으로 실행되기 시작한 시간입니다.|  
|**execution_count**|**bigint**|이 계획이 마지막으로 컴파일된 이후 실행된 횟수입니다.|  
|**total_worker_time**|**bigint**|이 계획이 컴파일된 이후 실행되는 데 사용된 총 CPU 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다.<br /><br /> 고유하게 컴파일된 저장 프로시저의 경우 1초 미만이 소요되는 실행이 많으면 **total_worker_time** 이 정확하지 않을 수 있습니다.|  
|**last_worker_time**|**bigint**|이 계획이 마지막으로 실행되었을 때 사용된 CPU 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다. <sup>1</sup>|  
|**min_worker_time**|**bigint**|단일 실행 중에 이 계획이 사용한 최소 CPU 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다. <sup>1</sup>|  
|**max_worker_time**|**bigint**|단일 실행 중에 이 계획이 사용한 최대 CPU 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|이 계획이 컴파일된 이후 실행될 때 수행된 총 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_physical_reads**|**bigint**|이 계획이 마지막으로 실행되었을 때 수행된 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_physical_reads**|**bigint**|단일 실행 중 이 계획에서 수행한 최소 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_physical_reads**|**bigint**|단일 실행 중 이 계획에서 수행한 최대 물리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_writes**|**bigint**|이 계획이 컴파일된 이후 실행될 때 수행된 총 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_writes**|**bigint**|계획이 마지막으로 실행될 때 변경된 버퍼 풀 페이지 수입니다. 페이지가 이미 변경된(수정된) 경우에는 쓰기 수가 계산되지 않습니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_writes**|**bigint**|단일 실행 중 이 계획에서 수행한 최소 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_writes**|**bigint**|단일 실행 중 이 계획에서 수행한 최대 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_reads**|**bigint**|이 계획이 컴파일된 이후 실행될 때 수행된 총 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_reads**|**bigint**|이 계획이 마지막으로 실행되었을 때 수행된 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_reads**|**bigint**|단일 실행 중 이 계획에서 수행한 최소 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_reads**|**bigint**|단일 실행 중 이 계획에서 수행한 최대 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_clr_time**|**bigint**|시간 안에 사용 된 (그러나 까지만 정확 밀리초), 마이크로초 단위로 보고 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 컴파일된 이후 실행 될 때이 계획의 공용 언어 런타임 (CLR) 개체입니다. CLR 개체는 저장 프로시저, 함수, 트리거, 유형 및 집계일 수 있습니다.|  
|**last_clr_time**|**bigint**|시간 (마이크로초) (않음 까지만 정확 밀리초) 내에서 사용한 보고 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 이 계획의 마지막 실행 중에 CLR 개체입니다. CLR 개체는 저장 프로시저, 함수, 트리거, 유형 및 집계일 수 있습니다.|  
|**min_clr_time**|**bigint**|단일 실행 중에 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 개체 내에서 이 계획이 사용한 최소 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다. CLR 개체는 저장 프로시저, 함수, 트리거, 유형 및 집계일 수 있습니다.|  
|**max_clr_time**|**bigint**|단일 실행 중에 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 내에서 이 계획이 사용한 최대 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다. CLR 개체는 저장 프로시저, 함수, 트리거, 유형 및 집계일 수 있습니다.|  
|**total_elapsed_time**|**bigint**|이 계획의 실행을 완료하는 데 소요된 총 경과 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다.|  
|**last_elapsed_time**|**bigint**|이 계획의 실행을 가장 최근에 완료하는 데 소요된 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다.|  
|**min_elapsed_time**|**bigint**|이 계획의 실행을 완료하는 데 소요된 최소 경과 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다.|  
|**max_elapsed_time**|**bigint**|이 계획의 실행을 완료하는 데 소요된 최대 경과 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다.|  
|**query_hash**|**Binary(8)**|쿼리에서 계산되는 이진 해시 값으로, 비슷한 논리를 가진 쿼리를 식별하는 데 사용됩니다. 쿼리 해시를 사용하여 리터럴 값만 다른 쿼리에 대한 집계 리소스 사용을 확인할 수 있습니다.|  
|**query_plan_hash**|**binary(8)**|쿼리 실행 계획에서 계산되는 이진 해시 값으로, 비슷한 쿼리 실행 계획을 식별하는 데 사용됩니다. 쿼리 계획 해시를 사용하여 비슷한 실행 계획을 가진 쿼리의 누적 비용을 찾을 수 있습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0x000입니다.|  
|**total_rows**|**bigint**|쿼리에서 반환한 총 이벤트 수입니다. null일 수 없습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_rows**|**bigint**|마지막 실행 쿼리에서 반환한 행 수입니다. null일 수 없습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_rows**|**bigint**|최소 적이 한 번 실행 하는 동안 쿼리에서 반환 된 행 수입니다. null일 수 없습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_rows**|**bigint**|적이 한 번 실행 하는 동안 쿼리에서 반환 된 행의 최대 수입니다. null일 수 없습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**statement_sql_handle**|**varbinary(64)**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 쿼리 저장소 상태에서 경우에 NULL이 아닌 값으로 채워진 및 해당 특정 쿼리에 대 한 통계를 수집 합니다.|  
|**statement_context_id**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 쿼리 저장소 상태에서 경우에 NULL이 아닌 값으로 채워진 및 해당 특정 쿼리에 대 한 통계를 수집 합니다.|  
|**total_dop**|**bigint**|병렬 처리 수준의 총 합계가이 계획이 컴파일된 이후 사용. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**last_dop**|**bigint**|이 계획이 마지막으로 실행 하는 경우 병렬 처리 수준입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**min_dop**|**bigint**|최소 병렬 처리 수준을이 계획을 적이 한 번 실행 하는 동안 사용. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**max_dop**|**bigint**|최대 병렬 처리 수준을이 계획을 적이 한 번 실행 하는 동안 사용. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**total_grant_kb**|**bigint**|예약 된 메모리의 총 양 (kb)이이 계획이 컴파일된 이후 받은 부여 합니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**last_grant_kb**|**bigint**|이 계획이 마지막으로 실행 하는 경우 예약 된 메모리의 양 (kb)에서 부여 합니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**min_grant_kb**|**bigint**|예약 된 메모리의 최소량 부여 KB 적이 한 번 실행 하는 동안 받은이 계획입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**max_grant_kb**|**bigint**|예약 된 메모리의 최대 크기 (kb)에서 적이 한 번 실행 하는 동안 받은이 계획을 부여 합니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**total_used_grant_kb**|**bigint**|이 계획이 컴파일된 이후 사용 (kb)에서 예약 된 메모리의 총 권한을 부여 합니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**last_used_grant_kb**|**bigint**|이 계획이 마지막으로 실행 하는 경우 KB의 사용 된 메모리 부여의 양입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**min_used_grant_kb**|**bigint**|사용 된 메모리의 최소량 부여 (kb) 한 번 실행 하는 동안 사용 되는이 계획입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**max_used_grant_kb**|**bigint**|사용 된 메모리의 최대 양 (kb)에서 한 번 실행 하는 동안 사용 되는이 계획을 부여 합니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**total_ideal_grant_kb**|**bigint**|이 계획이 컴파일된 이후 예상 kb에서 이상적인 메모리 부여의 총 양입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**last_ideal_grant_kb**|**bigint**|이 계획이 마지막으로 실행 될 때 이상적인 메모리 양 (kb)에서 부여 합니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**min_ideal_grant_kb**|**bigint**|최소한의 이상적인 메모리 부여이 계획 적이 한 번 실행 하는 동안 예상 KB입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**max_ideal_grant_kb**|**bigint**|이상적인 메모리의 최대 크기 (kb)이 계획 적이 한 번 실행 하는 동안 예상 권한을 부여 합니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**total_reserved_threads**|**bigint**|예약 된 병렬의 총 합계에이 계획이 컴파일된 이후 사용 스레드입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**last_reserved_threads**|**bigint**|이 계획이 마지막으로 실행 하는 경우 예약 된 병렬 스레드의 수입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**min_reserved_threads**|**bigint**|예약 된 병렬의 최소 수는 한 번 실행 하는 동안 사용 되는이 계획을 스레드입니다.  항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**max_reserved_threads**|**bigint**|예약 된 병렬의 최대 수에는 한 번 실행 하는 동안 사용 되는이 계획을 스레드입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**total_used_threads**|**bigint**|총 합계가이 계획이 컴파일된 이후 사용 병렬 스레드를 사용 합니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**last_used_threads**|**bigint**|이 계획이 마지막으로 실행 될 때 사용 되는 병렬 스레드의 수입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**min_used_threads**|**bigint**|이 계획 적이 한 번 실행 하는 동안 사용 되는 사용 되는 병렬 스레드의 최소 수입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**max_used_threads**|**bigint**|이 계획 적이 한 번 실행 하는 동안 사용 되는 사용 되는 병렬 스레드의 최대 수입니다. 항상 0을 메모리 액세스에 최적화 된 테이블을 쿼리 됩니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
|**total_columnstore_segment_reads**|**bigint**|쿼리가 읽은 columnstore 세그먼트의 총 합계입니다. null일 수 없습니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**last_columnstore_segment_reads**|**bigint**|쿼리의 마지막 실행에서 읽을 columnstore 세그먼트의 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**min_columnstore_segment_reads**|**bigint**|최소 한 번 실행 하는 동안 쿼리에 의해 지금까지 읽은 columnstore 세그먼트 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**max_columnstore_segment_reads**|**bigint**|한 번 실행 하는 동안 쿼리에 의해 지금까지 읽은 columnstore 세그먼트의 최대 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**total_columnstore_segment_skips**|**bigint**|총 합계는 쿼리에 의해 건너뛴 columnstore 세그먼트입니다. null일 수 없습니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**last_columnstore_segment_skips**|**bigint**|쿼리를 실행 하는 마지막으로 건너뛰는 columnstore 세그먼트의 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**min_columnstore_segment_skips**|**bigint**|적이 한 번 실행 하는 동안 건너뛴 쿼리에서 columnstore 세그먼트의 최소 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**max_columnstore_segment_skips**|**bigint**|적이 한 번 실행 하는 동안 건너뛴 쿼리에서 columnstore 세그먼트의 최대 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|
|**total_spills**|**bigint**|이 쿼리를 실행 하 여 유출 되 컴파일된 이후 페이지의 총 수입니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**last_spills**|**bigint**|쿼리가 실행 된 마지막 시간을 유출 하는 페이지 수입니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**min_spills**|**bigint**|단일 실행 중이 쿼리가 현재까지 유출 하는 페이지의 최소 수입니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**max_spills**|**bigint**|단일 실행 중이 쿼리가 현재까지 유출 하는 페이지의 최대 수입니다.<br /><br /> **적용 대상**: 부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**pdw_node_id**|**int**|이 배포에 있는 노드에 대 한 식별자입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]| 

> [!NOTE]
> <sup>1</sup> 고유 하 게 컴파일된 저장된 프로시저에 대 한 통계 컬렉션을 설정 하면 작업자 시간이 밀리초 단위로 수집 합니다. 쿼리 보다 작거나 1 밀리초를 실행 하는 경우 값은 0이 됩니다.  
  
## <a name="permissions"></a>Permissions  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 프리미엄 계층 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층 필요는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정.
  
## <a name="remarks"></a>주의  
 쿼리가 완료되면 뷰의 통계가 업데이트됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-finding-the-top-n-queries"></a>1. TOP N 쿼리 찾기  
 다음 예에서는 평균 CLR 시간을 기준으로 상위 5개의 쿼리에 대한 정보를 반환합니다. 이 예에서는 논리적으로 동일한 쿼리를 누적 리소스 소비량에 따라 그룹화할 수 있도록 쿼리 해시에 따라 쿼리를 집계합니다.  
  
```sql  
SELECT TOP 5 query_stats.query_hash AS "Query Hash",   
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",  
    MIN(query_stats.statement_text) AS "Statement Text"  
FROM   
    (SELECT QS.*,   
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,  
    ((CASE statement_end_offset   
        WHEN -1 THEN DATALENGTH(ST.text)  
        ELSE QS.statement_end_offset END   
            - QS.statement_start_offset)/2) + 1) AS statement_text  
     FROM sys.dm_exec_query_stats AS QS  
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats  
GROUP BY query_stats.query_hash  
ORDER BY 2 DESC;  
```  
  
### <a name="b-returning-row-count-aggregates-for-a-query"></a>2. 쿼리에 대한 행 개수 집계 반환  
 다음 예에서는 쿼리에 대한 행 개수 집계 정보(합계 행, 최소 행, 최대 행 및 마지막 행)를 반환합니다.  
  
```sql  
SELECT qs.execution_count,  
    SUBSTRING(qt.text,qs.statement_start_offset/2 +1,   
                 (CASE WHEN qs.statement_end_offset = -1   
                       THEN LEN(CONVERT(nvarchar(max), qt.text)) * 2   
                       ELSE qs.statement_end_offset end -  
                            qs.statement_start_offset  
                 )/2  
             ) AS query_text,   
     qt.dbid, dbname= DB_NAME (qt.dbid), qt.objectid,   
     qs.total_rows, qs.last_rows, qs.min_rows, qs.max_rows  
FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS qt   
WHERE qt.text like '%SELECT%'   
ORDER BY qs.execution_count DESC;  
```  
  
## <a name="see-also"></a>참고 항목  
[실행 관련 동적 관리 뷰 및 함수 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)    
[sys.dm_exec_sql_text &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)    
[sys.dm_exec_query_plan &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[sys.dm_exec_procedure_stats&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)     
[sys.dm_exec_trigger_stats &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)     
[sys.dm_exec_cached_plans&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  


