---
title: sys. dm_exec_query_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a4fba10bd080c4b97cd38a7330611bed51f3d225
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73982648"
---
# <a name="sysdm_exec_query_stats-transact-sql"></a>sys.dm_exec_query_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 캐시된 쿼리 계획에 대한 집계 성능 통계를 반환합니다. 이 뷰에는 캐시된 계획 내의 쿼리 문당 하나의 행이 포함되어 있습니다. 행의 유효 기간은 계획 자체와 연결되어 있습니다. 캐시에서 계획이 제거되면 이 뷰에서도 해당 행이 제거됩니다.  
  
> [!NOTE]
> - 데이터는 완료 된 쿼리만 반영 하 고 아직 진행 중인 쿼리는 반영 하지 않으므로, **dm_exec_query_stats** 의 결과는 각 실행에 따라 달라질 수 있습니다.
> - 또는 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서이를 호출 하려면 이름 **sys. dm_pdw_nodes_exec_query_stats**을 사용 합니다.    

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**sql_handle**|**varbinary (64)**  |쿼리가 속하는 일괄 처리 또는 저장 프로시저를 고유 하 게 식별 하는 토큰입니다.<br /><br /> **statement_start_offset** 및 **statement_end_offset**와 함께 **sql_handle**를 사용 하 여 **dm_exec_sql_text** 동적 관리 함수를 호출 하 여 쿼리의 sql 텍스트를 검색할 수 있습니다.|  
|**statement_start_offset**|**int**|0부터 시작하여 일괄 처리 또는 지속형 개체의 텍스트 내에서 행이 설명하는 쿼리의 시작 위치(바이트)를 나타냅니다.|  
|**statement_end_offset**|**int**|0부터 시작하여 일괄 처리 또는 지속형 개체의 텍스트 내에서 행이 설명하는 쿼리의 끝 위치(바이트)를 나타냅니다. 이전 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]버전의 경우 값-1은 일괄 처리의 끝을 나타냅니다. 후행 주석은 더 이상 포함 되지 않습니다.|  
|**plan_generation_num**|**bigint**|다시 컴파일한 후 계획의 인스턴스 간을 서로 구별하는 데 사용될 수 있는 시퀀스 번호입니다.|  
|**plan_handle**|**varbinary (64)**|실행 된 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 하는 토큰 이며 계획 캐시에 있거나 현재 실행 중인 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 합니다. 이 값은 [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) 동적 관리 함수로 전달되어 쿼리 계획을 가져올 수 있습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0x000입니다.|  
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
|**last_logical_writes**|**bigint**|가장 최근에 계획 실행을 완료 하는 동안 변경 된 버퍼 풀 페이지 수입니다.<br /><br />페이지를 읽은 후에는 페이지가 처음 수정 될 때만 변경 됩니다. 페이지가 변경 되 면이 숫자가 증가 합니다. 이미 더티 페이지를 이후에 수정 해도이 숫자에는 영향을 주지 않습니다.<br /><br />메모리 최적화 테이블을 쿼리 하는 경우이 숫자는 항상 0입니다.|  
|**min_logical_writes**|**bigint**|단일 실행 중 이 계획에서 수행한 최소 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_writes**|**bigint**|단일 실행 중 이 계획에서 수행한 최대 논리적 쓰기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_logical_reads**|**bigint**|이 계획이 컴파일된 이후 실행될 때 수행된 총 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_logical_reads**|**bigint**|이 계획이 마지막으로 실행되었을 때 수행된 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_logical_reads**|**bigint**|단일 실행 중 이 계획에서 수행한 최소 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_logical_reads**|**bigint**|단일 실행 중 이 계획에서 수행한 최대 논리적 읽기 수입니다.<br /><br /> 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**total_clr_time**|**bigint**|이 계획이 컴파일된 이후 실행 될 때 CLR (공용 언어 런타임) 개체 내 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 에서 사용 되는 시간 (마이크로초 단위로 보고 되지만 밀리초 단위 까지만 정확 함)입니다. CLR 개체는 저장 프로시저, 함수, 트리거, 유형 및 집계일 수 있습니다.|  
|**last_clr_time**|**bigint**|이 계획을 마지막으로 실행하는 동안 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 개체 내에서 실행에 사용한 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다. CLR 개체는 저장 프로시저, 함수, 트리거, 유형 및 집계일 수 있습니다.|  
|**min_clr_time**|**bigint**|단일 실행 중에 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 개체 내에서 이 계획이 사용한 최소 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다. CLR 개체는 저장 프로시저, 함수, 트리거, 유형 및 집계일 수 있습니다.|  
|**max_clr_time**|**bigint**|단일 실행 중에 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 내에서 이 계획이 사용한 최대 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다. CLR 개체는 저장 프로시저, 함수, 트리거, 유형 및 집계일 수 있습니다.|  
|**total_elapsed_time**|**bigint**|이 계획의 실행을 완료하는 데 소요된 총 경과 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다.|  
|**last_elapsed_time**|**bigint**|이 계획의 실행을 가장 최근에 완료하는 데 소요된 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다.|  
|**min_elapsed_time**|**bigint**|이 계획의 실행을 완료하는 데 소요된 최소 경과 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다.|  
|**max_elapsed_time**|**bigint**|이 계획의 실행을 완료하는 데 소요된 최대 경과 시간(마이크로초 단위로 보고되지만 밀리초 단위까지만 정확함)입니다.|  
|**query_hash**|**Binary (8)**|쿼리에서 계산되는 이진 해시 값으로, 비슷한 논리를 가진 쿼리를 식별하는 데 사용됩니다. 쿼리 해시를 사용하여 리터럴 값만 다른 쿼리에 대한 집계 리소스 사용을 확인할 수 있습니다.|  
|**query_plan_hash**|**binary (8)**|쿼리 실행 계획에서 계산되는 이진 해시 값으로, 비슷한 쿼리 실행 계획을 식별하는 데 사용됩니다. 쿼리 계획 해시를 사용하여 비슷한 실행 계획을 가진 쿼리의 누적 비용을 찾을 수 있습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0x000입니다.|  
|**total_rows**|**bigint**|쿼리에서 반환한 총 이벤트 수입니다. null일 수 없습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**last_rows**|**bigint**|마지막 실행 쿼리에서 반환한 행 수입니다. null일 수 없습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**min_rows**|**bigint**|한 번 실행 하는 동안 쿼리에서 반환한 최소 행 수입니다. null일 수 없습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**max_rows**|**bigint**|한 번 실행 하는 동안 쿼리에서 반환 된 최대 행 수입니다. null일 수 없습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저에서 메모리 최적화 테이블을 쿼리하는 경우 항상 0입니다.|  
|**statement_sql_handle**|**varbinary (64)**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상<br /><br /> 쿼리 저장소 설정 되 고 특정 쿼리에 대 한 통계를 수집 하는 경우에만 NULL이 아닌 값으로 채워집니다.|  
|**statement_context_id**|**bigint**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상<br /><br /> 쿼리 저장소 설정 되 고 특정 쿼리에 대 한 통계를 수집 하는 경우에만 NULL이 아닌 값으로 채워집니다.|  
|**total_dop**|**bigint**|이 계획이 컴파일된 이후 사용 된 병렬 처리 수준 합계입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**last_dop**|**bigint**|이 계획을 마지막으로 실행 한 경우의 병렬 처리 수준입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**min_dop**|**bigint**|이 계획을 실행 하는 동안 사용 된 최소 병렬 처리 수준입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**max_dop**|**bigint**|한 번의 실행 중이 계획에 사용 된 최대 병렬 처리 수준입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**total_grant_kb**|**bigint**|이 계획을 컴파일한 후 받은 총 예약 된 메모리 (KB)입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**last_grant_kb**|**bigint**|이 계획이 마지막으로 실행 된 경우 예약 된 메모리 부여 크기 (KB)입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**min_grant_kb**|**bigint**|이 계획을 실행 하는 동안 받은 최소 예약 된 메모리 부여 크기 (KB)입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**max_grant_kb**|**bigint**|이 계획을 실행 하는 동안 받은 최대 예약 된 메모리 부여 크기 (KB)입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**total_used_grant_kb**|**bigint**|이 계획을 컴파일한 이후 사용 된 예약 된 메모리의 총 크기 (KB)입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**last_used_grant_kb**|**bigint**|이 계획을 마지막으로 실행 한 경우 사용 된 메모리 부여 크기 (KB)입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**min_used_grant_kb**|**bigint**|사용 된 최소 메모리 부여 크기 (KB)입니다 .이 계획은 한 번 실행 중에 사용 된 것입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**max_used_grant_kb**|**bigint**|이 계획을 실행 하는 동안 사용 된 사용 된 최대 메모리 부여 크기 (KB)입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**total_ideal_grant_kb**|**bigint**|이 계획을 컴파일한 이후 예상 되는 이상적인 메모리 부여의 총 크기 (KB)입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**last_ideal_grant_kb**|**bigint**|이 계획을 마지막으로 실행 한 경우 이상적인 메모리 부여 크기 (KB)입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**min_ideal_grant_kb**|**bigint**|이 계획을 실행 하는 동안 예상 되는 이상적인 메모리 부여의 최소 크기 (KB)입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**max_ideal_grant_kb**|**bigint**|이 계획을 실행 하는 동안 예상 되는 이상적인 메모리 부여의 최대 크기 (KB)입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**total_reserved_threads**|**bigint**|이 계획이 컴파일된 이후 사용 된 예약 된 병렬 스레드의 총 합계입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**last_reserved_threads**|**bigint**|이 계획이 마지막으로 실행 될 때 예약 된 병렬 스레드 수입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**min_reserved_threads**|**bigint**|이 계획을 실행 하는 동안 사용 된 예약 병렬 스레드의 최소 수입니다.  메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**max_reserved_threads**|**bigint**|이 계획을 실행 하는 동안 사용 된 예약 병렬 스레드의 최대 수입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**total_used_threads**|**bigint**|이 계획이 컴파일된 이후 사용 된 사용 된 병렬 스레드의 총 합계입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**last_used_threads**|**bigint**|이 계획이 마지막으로 실행 될 때 사용 된 병렬 스레드의 수입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**min_used_threads**|**bigint**|이 계획을 실행 하는 동안 사용한 병렬 스레드의 최소 수입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**max_used_threads**|**bigint**|이 계획을 실행 하는 동안 사용한 병렬 스레드의 최대 수입니다. 메모리 최적화 테이블을 쿼리 하는 경우 항상 0입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상|  
|**total_columnstore_segment_reads**|**bigint**|쿼리에서 읽은 columnstore 세그먼트의 총 합계입니다. null일 수 없습니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|    
|**last_columnstore_segment_reads**|**bigint**|쿼리를 마지막으로 실행 했을 때 읽은 columnstore 세그먼트의 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|    
|**min_columnstore_segment_reads**|**bigint**|한 번의 실행 중에 쿼리에서 읽은 최소 columnstore 세그먼트 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|    
|**max_columnstore_segment_reads**|**bigint**|한 번의 실행 중에 쿼리에서 읽은 columnstore 세그먼트의 최대 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|    
|**total_columnstore_segment_skips**|**bigint**|쿼리에서 건너뛴 columnstore 세그먼트의 총 합계입니다. null일 수 없습니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|    
|**last_columnstore_segment_skips**|**bigint**|쿼리를 마지막으로 실행 한 후 건너뛴 columnstore 세그먼트 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|    
|**min_columnstore_segment_skips**|**bigint**|한 번의 실행 중에 쿼리에서 건너뛴 columnstore 세그먼트의 최소 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|    
|**max_columnstore_segment_skips**|**bigint**|한 번의 실행 중에 쿼리에서 건너뛴 columnstore 세그먼트의 최대 수입니다. null일 수 없습니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|
|**total_spills**|**bigint**|이 쿼리가 컴파일된 이후 실행 될 때 발생 한 총 페이지 수입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|  
|**last_spills**|**bigint**|쿼리가 마지막으로 실행 되었을 때의 페이지 수입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|  
|**min_spills**|**bigint**|단일 실행 중이 쿼리가 분산 한 최소 페이지 수입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|  
|**max_spills**|**bigint**|단일 실행 중이 쿼리가 분산 한 최대 페이지 수입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터 시작|  
|**pdw_node_id**|**int**|이 배포가 설정 된 노드의 식별자입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]| 
|**total_page_server_reads**|**bigint**|이 계획이 컴파일된 이후 실행 될 때 수행 된 원격 페이지 서버 읽기의 총 수입니다.<br /><br /> **적용 대상:** Azure SQL DB Hyperscale |  
|**last_page_server_reads**|**bigint**|계획이 마지막으로 실행 되었을 때 수행 된 원격 페이지 서버 읽기 수입니다.<br /><br /> **적용 대상:** Azure SQL DB Hyperscale |  
|**min_page_server_reads**|**bigint**|단일 실행 중이 계획에서 수행한 최소 원격 페이지 서버 읽기 수입니다.<br /><br /> **적용 대상:** Azure SQL DB Hyperscale |  
|**max_page_server_reads**|**bigint**|단일 실행 중이 계획에서 수행한 최대 원격 페이지 서버 읽기 수입니다.<br /><br /> **적용 대상:** Azure SQL DB Hyperscale |  
> [!NOTE]
> <sup>1</sup> 통계 수집을 사용 하는 경우 고유 하 게 컴파일된 저장 프로시저의 경우 작업자 시간이 밀리초 단위로 수집 됩니다. 쿼리가 1 밀리초 미만으로 실행 되는 경우 값은 0이 됩니다.  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 권한이 `VIEW SERVER STATE` 필요 합니다.   
Premium [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 계층에서는 데이터베이스에 대 `VIEW DATABASE STATE` 한 권한이 필요 합니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
   
## <a name="remarks"></a>설명  
 쿼리가 완료되면 뷰의 통계가 업데이트됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-finding-the-top-n-queries"></a>A. TOP N 쿼리 찾기  
 다음 예제는 평균 CPU 시간별로 상위 5개의 쿼리에 대한 정보를 반환합니다. 이 예에서는 논리적으로 동일한 쿼리를 누적 리소스 소비량에 따라 그룹화할 수 있도록 쿼리 해시에 따라 쿼리를 집계합니다.  
  
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
  
### <a name="b-returning-row-count-aggregates-for-a-query"></a>B. 쿼리에 대한 행 개수 집계 반환  
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
[Transact-sql&#41;&#40;관련 동적 관리 뷰 및 함수 실행](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)    
[dm_exec_sql_text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)    
[dm_exec_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[dm_exec_procedure_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)     
[dm_exec_trigger_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)     
[sys.dm_exec_cached_plans&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  


