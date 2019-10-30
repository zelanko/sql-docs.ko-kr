---
title: SQL Server 2019의 새로운 기능 | Microsoft Docs
ms.date: 08/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bb83237e33f477468cd58ea8a692970268bf1d66
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72807477"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 새로운 기능

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 이전 릴리스를 토대로 하여 SQL Server로 구축되었으며 개발 언어, 데이터 형식, 온-프레미스 또는 클라우드, 운영 체제를 선택할 수 있는 플랫폼으로 개선되었습니다.

이 문서에서는 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 새로운 기능 및 향상된 기능을 요약합니다.

자세한 내용 및 알려진 문제에 대해서는 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 릴리스 정보](sql-server-ver15-release-notes.md)를 참조하세요.

**[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 통해 최상의 환경에 맞는 [최신 도구](what-s-new-in-sql-server-ver15-prerelease.md#tools)를 사용해 보세요.**

>[!NOTE]
>콘텐츠는 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 릴리스 후보에 게시됩니다. 릴리스 후보는 시험판 소프트웨어입니다. 정보는 변경될 수 있습니다. 지원 시나리오에 대한 자세한 내용은 [지원](#support)을 참조하세요.
>
>이 릴리스에는 이전에 CTP(커뮤니티 기술 미리 보기) 릴리스를 통해 발표된 개선 사항이 포함되어 있습니다. 개선 사항에는 기능, 수정된 버그, 향상된 보안 및 최적화된 성능이 추가되었습니다. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 릴리스 후보 이전의 CTP 릴리스에서 도입되었거나 개선된 기능 목록은 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 알림 보관](what-s-new-in-sql-server-ver15-prerelease.md)을 참조하세요.

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서 [!INCLUDE[sql-server](../includes/ssnoversion-md.md)]용 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]를 소개합니다. 또한 SQL Server 데이터베이스 엔진, SQL Server Analysis Services, SQL Server Machine Learning Services, SQL Server on Linux 및 SQL Server Master Data Services에 대한 추가 기능과 개선 사항을 제공합니다.

다음 섹션에서는 이러한 기능에 대한 개요를 제공합니다.

## <a name="data-virtualization-and-includebig-data-clusters-2019includesssbigdataclusters-ver15md"></a>데이터 가상화 및 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]

오늘날의 기업은 회사 전체의 고립된 데이터 원본에 호스트된, 점점 증가하는 데이터 세트로 구성된 광범위한 데이터 자산을 관리하는 경우가 많습니다. 기계 학습 및 AI 기능을 포함하여 큰 데이터 세트 작업을 위한 완전한 환경을 제공하는 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]로 모든 데이터에서 거의 실시간으로 인사이트를 얻을 수 있습니다.

| 새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
| 확장 가능한 빅 데이터 솔루션 | Kubernetes에서 실행되는 SQL Server, Spark 및 HDFS 컨테이너의 [확장 가능한 클러스터 배포](../big-data-cluster/deploy-get-started.md) <br/><br/> Transact-SQL 또는 Spark에서 빅 데이터 읽기, 쓰기 및 처리<br/><br/> 고용량 빅 데이터를 사용하여 가치 높은 관계형 데이터를 쉽게 조합 및 분석<br/><br/>외부 데이터 원본 쿼리<br/><br/>SQL Server에서 관리하는 HDFS에 빅 데이터 저장<br/><br/>클러스터를 통해 여러 외부 데이터 원본에서 데이터 쿼리<br/><br/> AI, 기계 학습 및 기타 분석 작업에 데이터 사용<br/><br/> [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]에서 [애플리케이션 배포 및 실행](../big-data-cluster/concept-application-deployment.md) <br/><br/> SQL Server 마스터 인스턴스는 Always On 가용성 그룹 기술을 사용하여 모든 데이터베이스에 대해 고가용성 및 재해 복구를 제공합니다.<br/>|
|Polybase를 사용한 데이터 가상화 | 외부 테이블을 사용하여 외부 SQL Server, Oracle, Teradata, MongoDB 및 ODBC 데이터 원본의 데이터를 쿼리하며, 이제 [UTF-8 인코딩을 지원](../relational-databases/collations/collation-and-unicode-support.md)합니다. 자세한 내용은 [PolyBase란?](../relational-databases/polybase/polybase-guide.md)을 참조하세요.|
| &nbsp; | &nbsp; |

자세한 내용은 [SQL Server란?[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]](../big-data-cluster/big-data-cluster-overview.md)을 참조하세요.

CTP([[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]) 알림 보관](what-s-new-in-sql-server-ver15-prerelease.md)에는 이 기능의 모든 이전 CTP 릴리스에 대해 발표되고 변경된 기능 목록이 포함되어 있습니다.

## <a name="intelligent-database"></a>지능형 데이터베이스

### <a name="intelligent-query-processing"></a>지능형 쿼리 처리

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|행 모드 메모리 부여 피드백 |일괄 처리 및 행 모드 연산자의 메모리 부여 크기를 둘 다 조정하여 일괄 처리 모드 메모리 부여 피드백 기능을 확장합니다. 이렇게 하면 과도한 권한 부여를 자동으로 수정하여 메모리 낭비와 동시성을 줄일 수 있으며, 디스크에 많은 비용이 들 수 있는 부족한 메모리 부여를 수정할 수 있습니다. [행 모드 메모리 부여 피드백](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback)을 참조하세요. |
|테이블 변수 지연 컴파일|테이블 변수를 참조하는 쿼리의 계획 품질 및 전체 성능을 개선합니다. 최적화 및 초기 컴파일 중에 이 기능은 실제 테이블 변수 행 수를 기반으로 하는 카디널리티 예측을 전파합니다. 이 정확한 행 수 정보는 다운스트림 계획 작업을 최적화합니다. [테이블 변수 지연 컴파일](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation)을 참조하세요. |
|`APPROX_COUNT_DISTINCT `를 사용한 대략적인 쿼리 처리|절대 정밀도가 중요하지 않지만 응답성이 중요한 시나리오의 경우 `APPROX_COUNT_DISTINCT`는 뛰어난 동시성을 위해 `COUNT(DISTINCT())`보다 적은 리소스를 사용하여 대규모 데이터 세트에서 집계합니다. [대략적인 쿼리 처리](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)를 참조하세요.|
|rowstore의 일괄 처리 모드|rowstore의 일괄 처리 모드는 columnstore 인덱스를 요구하지 않고도 일괄 처리 모드를 실행할 수 있습니다. 일괄 처리 모드 실행은 분석 워크로드 중에 CPU를 더욱 효율적으로 사용하지만 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]까지는 쿼리에 columnstore 인덱스를 사용하는 작업이 포함된 경우에만 사용되었습니다. 그러나 일부 애플리케이션은 columnstore 인덱스에서 지원되지 않는 기능을 사용할 수 있으므로 일괄 처리 모드를 활용할 수 없습니다. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]부터는 쿼리에 모든 유형의 인덱스(rowstore 또는 columnstore)를 사용하여 작업을 포함하는 적격 분석 워크로드에서 일괄 처리 모드를 사용할 수 있습니다. [rowstore의 일괄 처리 모드](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore)를 참조하세요. |
|스칼라 UDF 인라인 처리|자동으로 스칼라 UDF를 관계식으로 변환하고 이를 호출 SQL 쿼리에 포함합니다. 이 변환은 스칼라 UDF를 활용하는 워크로드의 성능을 개선합니다. [스칼라 UDF 인라인 처리](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining)를 참조하세요.|
| &nbsp; | &nbsp; |


### <a name="in-memory-database"></a>메모리 내 데이터베이스

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|하이브리드 버퍼 풀| [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 새 기능으로, PMEM(영구 메모리) 디바이스의 데이터베이스 파일에 있는 데이터베이스 페이지를 필요 시 바로 액세스합니다. [하이브리드 버퍼 풀](../database-engine/configure-windows/hybrid-buffer-pool.md)을 참조하세요.|
|메모리 최적화 TempDB 메타데이터| [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 [메모리 내 데이터베이스](../relational-databases/in-memory-database.md) 기능군의 일부인 새로운 기능 메모리 최적화 TempDB 메타데이터를 도입하여 해당 병목 상태를 효과적으로 제거하고 TempDB 리소스 사용량이 많은 워크로드를 위한 새로운 수준의 확장성을 구현합니다. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서 임시 테이블 메타데이터 관리에 필요한 시스템 테이블은 래치가 없는 비내구성 메모리 최적화 테이블로 이동될 수 있습니다. [메모리 최적화 TempDB 메타데이터](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)를 참조하세요.|
| 데이터베이스 스냅샷에 대한 메모리 내 OLTP 지원 | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 메모리 최적화된 파일 그룹을 포함하는 데이터베이스의 [데이터베이스 스냅샷](../relational-databases/databases/database-snapshots-sql-server.md)을 만들 수 있습니다. |
| &nbsp; | &nbsp; |

### <a name="intelligent-performance"></a>지능형 성능

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|인덱스에 높은 동시성 삽입에 대한 처리량을 향상시키는 데 도움이 되는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 내의 최적화를 켭니다. 이 옵션은 ID 열, 시퀀스 또는 날짜/시간 열과 같은 순차 키가 있는 인덱스에서 일반적으로 볼 수 있는 마지막 페이지 삽입 경합에 취약한 인덱스를 대상으로 합니다. 자세한 내용은 [INDEX 만들기](../t-sql/statements/create-index-transact-sql.md#sequential-keys)를 참조하세요.|
|빠른 전달 및 정적 커서 강제 적용 | 쿼리 저장소 계획에서 빠른 전달 및 정적 커서에 대한 지원을 강제 적용합니다. [계획에서 빠른 전달 및 정적 커서에 대한 강제 적용 지원](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23)을 참조하세요.|
|리소스 거버넌스| `CREATE WORKLOAD GROUP` 및 `ALTER WORKLOAD GROUP`의 `REQUEST_MAX_MEMORY_GRANT_PERCENT` 옵션에 대해 구성 가능한 값이 정수에서 부동 소수점 수 데이터 유형으로 변경되어 메모리 제한의 더 세분화된 제어가 가능합니다. [ALTER WORKLOAD GROUP](../t-sql/statements/alter-workload-group-transact-sql.md) 및 [CREATE WORKLOAD GROUP](../t-sql/statements/create-workload-group-transact-sql.md)을 참조하세요.|
|워크로드에 대한 다시 컴파일 감소| 여러 범위에서 임시 테이블을 사용하는 기능이 개선되었습니다. [워크로드에 대한 다시 컴파일 감소](../relational-databases/tables/tables.md#ctp23)를 참조하세요. |
|간접 검사점 확장성 |[향상된 간접 검사점 확장성](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23)을 참조하세요.|
|동시 PFS 업데이트|[PFS 페이지](https://techcommunity.microsoft.com/t5/SQL-Server/Under-the-covers-GAM-SGAM-and-PFS-pages/ba-p/383125)는 SQL Server가 개체 공간을 할당할 때 여유 공간을 찾는 데 사용하는 데이터베이스 파일 내의 특수 페이지입니다. PFS 페이지에서 페이지 래치 경합은 일반적으로 [`tempdb`](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d)와 관련이 있지만 동시 개체 할당 스레드가 많은 경우 사용자 데이터베이스에서도 발생할 수 있습니다. 이 개선 사항은 PFS 업데이트로 동시성을 관리하는 방식을 변경하여 단독 래치가 아닌 공유 래치에서 업데이트할 수 있도록 합니다. 이 동작은 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]부터 모든 데이터베이스(`tempdb` 포함)에서 기본적으로 설정되어 있습니다.|
| &nbsp; | &nbsp; |

### <a name="monitoring"></a>모니터링

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | `sys.dm_os_wait_stats` 동적 관리 뷰의 새 대기 유형입니다. 동기 통계 새로 고침 작업에 소요된 누적된 인스턴스 수준 시간을 보여 줍니다. [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)를 참조하세요.|
|쿼리 저장소에 대한 캡처 정책 사용자 지정|사용하도록 설정된 경우 특정 서버의 데이터 컬렉션을 정밀 조정하기 위해 새로운 쿼리 저장소 캡처 정책 설정 아래에서 추가 쿼리 저장소 구성을 사용할 수 있습니다. 자세한 내용은 [ALTER DATABASE SET 옵션](../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.|
|`LIGHTWEIGHT_QUERY_PROFILING`|새 데이터베이스 범위 지정 구성입니다. [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp)을 참조하세요. |
|`sys.dm_exec_requests` 열 `command` | `SELECT`가 쿼리 실행을 계속하기 전에 동기 통계 업데이트 작업이 완료되도록 기다리고 있는 경우 `SELECT (STATMAN)`을 표시합니다. [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)을 참조하세요.|
|`sys.dm_exec_query_plan_stats` |새 DMF는 대부분의 쿼리에 대해 마지막으로 알려진 실제 실행 계획과 동일한 것을 반환합니다. [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)를 참조하세요.|
|`LAST_QUERY_PLAN_STATS` | `sys.dm_exec_query_plan_stats`를 사용하도록 설정하는 새 데이터베이스 범위 지정 구성입니다. [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 참조하세요.|
|`query_post_execution_plan_profile` | 확장 이벤트는 표준 프로파일링을 사용하는 `query_post_execution_showplan`과 달리 경량 프로파일링을 기반으로한 실제 계획과 동등한 것을 수집합니다. [쿼리 프로파일링 인프라](../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요.|
|`sys.dm_db_page_info(database_id, file_id, page_id, mode)` | New DMF는 데이터베이스의 페이지에 대한 정보를 반환합니다. [sys.dm_db_page_info (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)를 참조하세요.|
| &nbsp; | &nbsp; |

## <a name="developer-experience"></a>개발자 환경

### <a name="graph"></a>그래프

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|에지 제약 조건 계단식 삭제 동작 |그래프 데이터베이스의 에지 제약 조건에 대한 계단식 삭제 작업을 정의합니다. [Edge 제약 조건](../relational-databases/tables/graph-edge-constraints.md)을 참조하세요. |
|새 그래프 함수 - `SHORTEST_PATH` | `MATCH`의 `SHORTEST_PATH`를 사용하여 그래프에서 노드 2개 사이의 최단 경로를 찾거나 임의의 길이 횡단을 수행합니다.|
|파티션 테이블 및 인덱스| 분할 테이블 및 인덱스의 데이터는 그래프 데이터베이스에서 두 개 이상의 파일 그룹으로 분할될 수 있는 단위로 나뉩니다. |
|그래프 일치 쿼리에서 파생된 테이블 또는 뷰 별칭 사용 |[그래프 일치 쿼리](../t-sql/queries/match-sql-graph.md)를 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="unicode-support"></a>유니코드 지원

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|UTF-8 문자 인코딩 지원 |가져오기 및 내보내기 인코딩에는 UTF-8 문자를 지원하고, 문자열 데이터의 경우 데이터베이스 수준 또는 열 수준 데이터 정렬로 지원합니다. 이는 글로벌 규모로 확장되는 애플리케이션을 지원합니다. 글로벌 다국어 데이터베이스 애플리케이션 및 서비스를 제공하는 요구 사항은 고객 수요 및 특정 시장 규정을 충족하는 데 매우 중요합니다. [데이터 정렬 및 유니코드 지원](../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.<br/><br/> [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 릴리스 후보를 사용하면 Polybase 외부 테이블 및 Always Encrypted(Enclaves를 사용하지 않을 경우)에 대한 UTF-8 지원이 가능합니다.|
| &nbsp; | &nbsp; |

### <a name="language-extensions"></a>언어 확장

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|새 Java 언어 SDK | SQL Server에서 실행할 수 있는 Java 프로그램의 개발을 간소화합니다. [SQL Server에 대한 Java용 Microsoft 확장성 SDK](../language-extensions/how-to/extensibility-sdk-java-sql-server.md)를 참조하세요. |
|Java 언어 SDK는 오픈 소스임 |[Microsoft SQL Server용 Java에 대한 Microsoft 확장성 SDK](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server)는 현재 오픈 소스로 [GitHub에서 제공합니다](https://github.com/microsoft/sql-server-language-extensions).|
|Java 데이터 형식 지원|[Java 데이터 형식](../language-extensions/how-to/java-to-sql-data-types.md)을 참조하세요.|
|새 기본 Java 런타임 | 이제 SQL Server에는 제품 전체의 Java 지원을 위한 Azul System Zulu Embedded가 포함되어 있습니다. 자세한 내용은 [SQL Server 2019에서 체험할 수 있는 Java 사용 가능](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/)을 참조하세요. |
|SQL Server 언어 확장| 확장성 프레임워크를 사용하여 외부 코드를 실행합니다. [SQL Server 언어 확장](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)을 참조하세요.
|외부 언어 등록|새로운 DDL `CREATE EXTERNAL LANGUAGE`는 SQL Server에서 Java와 같은 외부 언어를 등록합니다. [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md)를 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="spatial"></a>공간

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
| 새 SRID(spatial reference identifier) |[오스트레일리아 GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020)은 글로벌 위치 시스템과 더욱 긴밀하게 정렬된 더 강력하고 정확한 데이터를 제공합니다. 새 SRID는 다음과 같습니다.<br/><br/> - 지리적 2D의 경우 7843<br/> - 지리적 3D의 경우 7844 <br/><br/>[sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) 보기에는 새 SRID의 정의가 포함되어 있습니다. |
| &nbsp; | &nbsp; |

### <a name="error-messages"></a>오류 메시지

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|자세한 정보 잘림 경고 | 잘림 오류 메시지는 기본적으로 테이블 및 열 이름과 잘린 값을 포함합니다. [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation)를 참조하세요.|
| &nbsp; | &nbsp; |

## <a name="mission-critical-security"></a>중요 업무용 보안

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|보안 Enclave를 사용한 Always Encrypted|서버 쪽 보안 Enclave 내에서 일반 텍스트 데이터에 대한 계산을 사용하도록 설정하여 현재 위치의 암호화 및 다양한 계산을 사용하여 Always Encrypted 시에 확장합니다. 내부 암호화는 데이터베이스에서 데이터 이동을 방지하므로 암호화 작업(열 암호화, 열 회전 암호화 키 등)의 성능 및 안정성을 개선합니다. 다양한 계산(패턴 일치 및 비교 연산)이 지원되면 중요한 데이터 보호를 요구하는 한편 Transact-SQL 쿼리에서 풍부한 기능을 필요로 하는 광범위한 시나리오와 애플리케이션에서 Always Encrypted를 사용할 수 있게 됩니다. [보안 Enclave를 사용한 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.|
|SQL Server 구성 관리자의 인증서 관리|[인증서 관리(SQL Server 구성 관리자)](../database-engine/configure-windows/manage-certificates.md)를 참조하세요.|
| &nbsp; | &nbsp; |

## <a name="high-availability"></a>고가용성

### <a name="availability-groups"></a>가용성 그룹

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|최대 5개의 동기 복제본|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 동기 복제본의 최대 수가 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 3개에서 5개로 증가되었습니다. 그룹 내에서 자동 장애 조치가 수행되도록 이 그룹을 5개 복제본으로 구성할 수 있습니다. 여기에는 하나의 주 복제본 및 4개의 동기 보조 복제본이 있습니다.|
|보조-주 복제본 연결 리디렉션| 이 기능은 연결 문자열에 지정된 대상 서버에 관계없이 클라이언트 애플리케이션 연결이 주 복제본으로 전송되도록 합니다. 자세한 내용은 [보조-주 복제본 읽기/쓰기 연결 리디렉션(Always On 가용성 그룹)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)을 참조하세요.|
| &nbsp; | &nbsp; |

### <a name="recovery"></a>복구

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|가속 데이터베이스 복구 | 데이터베이스별로 가속 데이터베이스 복구를 사용하도록 설정합니다. [가속 데이터베이스 복구](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr)를 참조하세요.|
| &nbsp; | &nbsp; |

### <a name="resumable-operations"></a>다시 시작 가능한 작업

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|온라인 클러스터형 columnstore 인덱스 빌드 및 다시 빌드 | [온라인으로 인덱스 작업 수행](../relational-databases/indexes/perform-index-operations-online.md)을 참조하세요. |
|다시 시작 가능한 온라인 rowstore 인덱스 빌드 | [온라인으로 인덱스 작업 수행](../relational-databases/indexes/perform-index-operations-online.md)을 참조하세요. |
|TDE(투명한 데이터 암호화)의 초기 검색 일시 중단 및 다시 시작|[TDE(투명한 데이터 암호화) 검색 - 일시 중단 및 다시 시작](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)을 참조하세요.|
| &nbsp; | &nbsp; |

## <a name="setup"></a>설치 프로그램 

|새로운 기능 또는 업데이트 | 세부 정보 | 
|:---|:---| 
|새 메모리 설정 옵션 | 설치 중에 *최소 서버 메모리(MB)* 및 *최대 서버 메모리(MB)* 서버 구성을 설정합니다. 자세한 내용은 [데이터베이스 엔진 구성 - 메모리 페이지](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#memory)와 [명령 프롬프트에서 SQL Server 설치](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install)의 `USESQLRECOMMENDEDMEMORYLIMITS`, `SQLMINMEMORY` 및 `SQLMAXMEMORY` 매개 변수를 참조하세요. 제안된 값은 [서버 메모리 구성 옵션](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually)의 메모리 구성 지침에 따라 정렬됩니다.| 
|새 병렬 처리 설정 옵션 | 설치 중에 *최대 병렬 처리 수준* 서버 구성을 설정합니다. 자세한 내용은 [데이터베이스 엔진 구성 - MaxDOP 페이지](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#maxdop)와 [ SQL Server 설치](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install)의 `SQLMAXDOP` 매개 변수를 참조하세요. 기본값은 [최대 병렬 처리 수준 서버 구성 옵션 구성](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)의 최대 병렬 처리 수준 지침에 따라 정렬됩니다.| 
| &nbsp; | &nbsp; |

## <a name="platform-choice"></a>플랫폼 선택

### <a id="sql-server-on-linux"></a>Linux

| 새로운 기능 또는 업데이트 | 세부 정보 |
|:-----|:-----|
|새 컨테이너 레지스트리|[Docker에서 SQL Server 컨테이너 시작](../linux/quickstart-install-connect-docker.md) |
|복제 지원 |[Linux의 SQL Server 복제 개체](../linux/sql-server-linux-replication.md)
|MSDTC(Microsoft Distributed Transaction Coordinator) 지원 |[Linux에서 MSDTC를 구성하는 방법](../linux/sql-server-linux-configure-msdtc.md) |
|타사 AD 공급자에 대한 OpenLDAP 지원 |[자습서: Linux에서 SQL Server와 Active Directory 인증 사용](../linux/sql-server-linux-active-directory-authentication.md) |
|Linux의 Machine Learning |[Linux에서 Machine Learning 구성](../linux/sql-server-linux-setup-machine-learning.md) |
|TempDB 개선 사항 | 기본적으로 SQL Server on Linux를 새로 설치하면 논리적 코어 수(최대 8개 데이터 파일 포함)에 따라 여러 TempDB 데이터 파일이 생성됩니다. 이 위치에서 부 버전 또는 주 버전 업그레이드에는 적용되지 않습니다. 각 TempDB 파일은 자동 증가 속도가 64MB인 8MB입니다. 이 동작은 Windows의 기본 SQL Server 설치와 유사합니다. |
| Linux의 PolyBase. | Hadoop이 아닌 커넥터에 대한 Linux에 [PolyBase를 설치](../relational-databases/polybase/polybase-linux-setup.md)합니다.<br/><br/>[PolyBase 형식 매핑](../relational-databases/polybase/polybase-type-mapping.md). |
| CDC(변경 데이터 캡처) 지원 | CDC(변경 데이터 캡처)는 이제 SQL Server 2019용 Linux에서 지원됩니다. |
| &nbsp; | &nbsp; |

### <a name="containers"></a>SSIS 로그 구성

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
| Microsoft Container Registry | 이제 [Microsoft Container Registry](https://www.ntweekly.com/2019/09/23/microsoft-container-registry-to-replace-docker-hub-for-new-images/)가 Docker Hub 대신 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 비롯한 새 공식적인 Microsoft 컨테이너 이미지를 제공합니다. |
| 루트가 아닌 컨테이너 | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 기본적으로 [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] 프로세스를 루트가 아닌 사용자로 시작하여 더 안전한 컨테이너를 만들 수 있습니다. 자세한 내용은 [루트가 아닌 사용자 권한으로 SQL Server 컨테이너 빌드 및 실행](../linux/sql-server-linux-configure-docker.md#buildnonrootcontainer)을 참조하세요. |
| &nbsp; | &nbsp; |

## <a id="ml"></a> SQL Server Machine Learning Services

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|파티션 기반 모델링|`sp_execute_external_script`에 추가된 새 매개 변수를 사용하여 데이터 파티션별로 외부 스크립트를 처리합니다. 이 기능은 하나의 큰 모델 대신, 많은 작은 모델(데이터 파티션당 하나의 모델)을 학습하도록 지원합니다. [파티션 기반 모델 만들기](../advanced-analytics/tutorials/r-tutorial-create-models-per-partition.md)를 참조하세요.|
|Windows Server 장애 조치(Failover) 클러스터| Windows Server 장애 조치(Failover) 클러스터에서 Machine Learning 서비스의 고가용성을 구성합니다.|
| &nbsp; | &nbsp; |

## [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]

| 새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|Azure SQL Database 관리형 인스턴스 데이터베이스를 지원합니다.| 관리형 인스턴스에서 [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]를 호스팅합니다. [[!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] 설치 및 구성](../master-data-services/master-data-services-installation-and-configuration.md#SetUpWeb)을 참조하세요.|
|새 HTML 컨트롤| HTML 컨트롤은 이전의 모든 Silverlight 구성 요소를 대체합니다. Silverlight 종속성이 제거되었습니다.|
| &nbsp; | &nbsp; |

## <a name="sql-server-analysis-services"></a>SQL Server Analysis Services

| 새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|쿼리 인터리빙| [쿼리 인터리빙](https://docs.microsoft.com/analysis-services/tabular-models/query-interleaving)을 참조하세요. |
|계산 그룹을 포함하는 테이블 형식 모델에 대한 MDX 쿼리 지원 | [계산 그룹](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)을 참조하세요. |
|테이블 형식 모델의 계산 그룹| [테이블 형식 모델의 계산 그룹](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|계산 그룹을 포함하는 테이블 형식 모델에 대한 MDX 쿼리 지원 | [계산 그룹](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)을 참조하세요. |
|계산 그룹을 사용하여 측정값 서식을 동적으로 지정합니다. |이 기능을 사용하면 [계산 그룹](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)을 포함하는 측정값에 대한 형식 문자열을 조건부로 변경할 수 있습니다. 예를 들어 통화 변환을 통해 서로 다른 외국 통화 형식을 사용하여 측정값을 표시할 수 있습니다.|
|테이블 형식 모델의 다 대 다 관계|[테이블 형식 모델의 다 대 다 관계](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|리소스 거버넌스에 대한 속성 설정|[리소스 거버넌스에 대한 속성 설정](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
| Power BI 캐시 새로 고침에 대한 거버넌스 설정.  | Power BI 서비스는 라이브 연결 보고서의 초기 로드에 대한 대시보드 타일 데이터 및 보고서 데이터를 캐시하여 많은 수의 캐시 쿼리가 SSAS로 전송되도록 하며, 극단적인 경우 서버에 과부하를 발생하기도 합니다. 이 릴리스에는 **ClientCacheRefreshPolicy** 속성이 도입되었습니다. 이 속성을 사용하여 서버 수준에서 이 동작을 재정의할 수 있습니다. 자세히 알아보려면 [일반 속성](https://docs.microsoft.com/analysis-services/server-properties/general-properties)을 참조하세요. |
| 온라인 연결  | 이 기능은 테이블 형식 모델을 온라인 작업으로 연결하는 기능을 제공합니다. 온라인 연결 기능은 온-프레미스 쿼리 스케일 아웃 환경에서 읽기 전용 복제본을 동기화하는 데 사용할 수 있습니다. 자세히 알아보려면 [온라인 연결](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32)을 참조하세요. |
| &nbsp; | &nbsp; |

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

지원에서 제외된 특정 기능은 [릴리스 정보](sql-server-ver15-release-notes.md)를 참조하세요.

또한 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2에서 추가되었거나 개선된 기능은 다음과 같습니다.

## <a name="see-also"></a>관련 항목:

- [`SqlServer` PowerShell 모듈](https://www.powershellgallery.com/packages/Sqlserver)
- [SQL Server PowerShell 설명서](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>다음 단계

- [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 릴리스 정보](sql-server-ver15-release-notes.md).

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: 기술 백서](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />2018년 9월에 게시되었습니다. Windows, Linux 및 Docker 컨테이너용 Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0에 적용됩니다.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
