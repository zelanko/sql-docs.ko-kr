---
title: 실행 계획 | Microsoft Docs
description: SQL Server 데이터베이스 엔진이 쿼리를 실행할 수 있도록 쿼리 최적화 프로그램이 만드는 실행 계획 또는 쿼리 계획에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- execution plan [SQL Server]
- query plan [SQL Server]
- query execution plans
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753f
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 9b0f95a4afa1397783547f2804d92dd3fc37b357
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457262"
---
# <a name="execution-plans"></a>실행 계획
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

쿼리를 실행하려면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은(는) 필요한 데이터에 액세스하는 가장 효율적인 방법을 결정하는 명령문을 분석해야 합니다. 이 분석은 쿼리 최적화 프로그램이라는 구성 요소에 의해 처리됩니다. 최적화 프로그램에 대한 입력은 쿼리, 데이터베이스 스키마(테이블 및 인덱스 정의) 및 데이터베이스 통계로 이루어집니다. 쿼리 최적화 프로그램의 출력은 쿼리 실행 계획이며 경우에 따라 쿼리 계획이나 실행 계획이라고 합니다.   

쿼리 실행 계획은 다음 사항을 정의합니다. 

- **원본 테이블이 액세스되는 순서**  
  일반적으로 데이터베이스 서버는 다양한 방법으로 기본 테이블에 액세스하여 결과 집합을 작성할 수 있습니다. 예를 들어 `SELECT` 문이 세 개의 테이블을 참조하는 경우 데이터베이스 서버는 먼저 `TableA`에 액세스하고, `TableA`의 데이터를 사용하여 `TableB`에서 일치하는 행을 추출한 후 `TableB`의 데이터를 사용하여 `TableC`에서 데이터를 추출합니다. 다음은 데이터베이스 서버가 테이블에 액세스할 수 있는 여러 순서입니다.  
  `TableC`, `TableB`, `TableA`또는  
  `TableB`, `TableA`, `TableC`또는  
  `TableB`, `TableC`, `TableA`또는  
  `TableC`, `TableA`, `TableB`  

- **각 테이블에서 데이터를 추출하는 데 사용하는 방법**  
  일반적으로 각 테이블의 데이터에 액세스하는 방법에는 여러 가지가 있습니다. 특정 키 값을 가진 몇몇 행만 필요한 경우 데이터베이스 서버는 인덱스를 사용할 수 있습니다. 테이블의 모든 행이 필요한 경우 데이터베이스 서버는 인덱스를 무시하고 테이블을 검색할 수 있습니다. 테이블의 모든 행이 필요하지만 키 열이 `ORDER BY`에 있는 인덱스가 있으면 테이블 검색 대신 인덱스 검색을 수행하여 다른 종류의 결과 집합을 저장할 수 있습니다. 테이블이 매우 작은 경우 테이블 검색은 거의 모든 테이블 액세스를 위한 가장 효율적인 방법일 수 있습니다.
  
- **계산 컴퓨팅에 사용되는 방법과 각 테이블의 데이터를 필터링, 집계, 정렬하는 방법**  
  데이터가 테이블에서 액세스되므로, 컴퓨팅 스칼라 값과 같은 데이터에 대한 계산 수행 방법과 쿼리 텍스트(예: `GROUP BY` 또는 `ORDER BY` 절을 사용하는 경우)와 데이터 필터링 방법(예: `WHERE` 또는 `HAVING` 절을 사용하는 경우)에 정의된 대로 데이터를 집계하고 정렬하는 방법에는 여러 가지가 있습니다.

> [!NOTE]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에는 실행 계획을 표시하는 세 가지 옵션이 있습니다.        
> -  ******[예상 실행 계획](../../relational-databases/performance/display-the-estimated-execution-plan.md)은 쿼리 최적화 프로그램에서 추정을 기반으로 생성한 컴파일된 계획입니다. 계획 캐시에 저장되는 쿼리 계획입니다.        
> -  ******[실제 실행 계획](../../relational-databases/performance/display-an-actual-execution-plan.md)은 컴파일된 계획 및 관련 [실행 컨텍스트](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)입니다. **쿼리 실행이 완료된 후** 사용할 수 있게 됩니다. 여기에는 실행 경고 또는 최신 버전 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]의 경우 실행 중에 사용된 경과 및 CPU 시간 같은 실제 런타임 정보가 포함됩니다.         
> -  ******[활성 쿼리 통계](../../relational-databases/performance/live-query-statistics.md)는 컴파일된 계획 및 관련 실행 컨텍스트입니다. **진행 중인 쿼리 실행**에 사용할 수 있으며 매초 업데이트됩니다. 여기에는 [연산자](../../relational-databases/showplan-logical-and-physical-operators-reference.md)를 통과하는 실제 행 수, 경과된 시간, 예상 쿼리 진행률 같은 실제 런타임 정보가 포함됩니다.

> [!TIP]
> 쿼리 처리 및 쿼리 실행 계획에 대한 자세한 내용은 쿼리 처리 아키텍처 가이드의 [SELECT 문 최적화](../../relational-databases/query-processing-architecture-guide.md#optimizing-select-statements) 및 [실행 계획 캐싱 및 다시 사용](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse) 섹션을 참조하세요.

## <a name="in-this-section"></a>섹션 내용  
[쿼리 프로파일링 인프라](../../relational-databases/performance/query-profiling-infrastructure.md)     
[실행 계획 표시 및 저장](../../relational-databases/performance/display-and-save-execution-plans.md)     
[실행 계획 비교 및 분석](../../relational-databases/performance/compare-and-analyze-execution-plans.md)     
[계획 지침](../../relational-databases/performance/plan-guides.md)     

## <a name="see-also"></a>참고 항목  
[성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
[성능 모니터링 및 튜닝 도구](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
[쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)    
[활성 쿼리 통계](../../relational-databases/performance/live-query-statistics.md)     
[작업 모니터](../../relational-databases/performance-monitor/activity-monitor.md)     
[쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
[sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
[sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
[추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
[실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)
