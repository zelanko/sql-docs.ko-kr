---
title: SQL Server 2019의 새로운 기능 | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2ded17c5baf35949b16c173236f94f8d0d3dd299
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028908"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 새로운 기능

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 이전 릴리스를 토대로 하여 SQL Server로 구축되었으며 개발 언어, 데이터 형식, 온-프레미스 또는 클라우드, 운영 체제를 선택할 수 있는 플랫폼으로 개선되었습니다.

이 문서에서는 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 새로운 기능 및 향상된 기능을 요약합니다.

자세한 내용 및 알려진 문제에 대해서는 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 릴리스 정보](sql-server-ver15-release-notes.md)를 참조하세요.

**[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 통해 최상의 환경에 맞는 [최신 도구](what-s-new-in-sql-server-ver15-prerelease.md#tools)를 사용해 보세요.**

## <a name="ctp-32-july-2019"></a>CTP 3.2 2019년 7월

CTP(Community Technology Preview) 3.2는 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 최신 퍼블릭 릴리스입니다. 이 릴리스에는 버그를 수정하고, 보안을 개선하고, 성능을 최적화하는 이전 CTP 릴리스의 개선 사항이 포함됩니다. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2 이전의 각 CTP 릴리스에서 도입되었거나 개선된 기능 목록은 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 알림 보관](what-s-new-in-sql-server-ver15-prerelease.md)을 참조하세요.

### <a name="new-in-big-data-clusters"></a>빅 데이터 클러스터의 새로운 기능

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|퍼블릭 미리 보기 |CTP 3.2 이전에는 등록한 얼리어답터가 SQL Server 빅 데이터 클러스터를 사용할 수 있었습니다. 이번 릴리스에서는 누구나 빅 데이터 클러스터 SQL Server 기능을 경험할 수 있습니다. <br/><br/> [SQL Server 빅 데이터 클러스터 시작](../big-data-cluster/deploy-get-started.md)을 참조하세요.|
|`azdata` |CTP 3.2는 클러스터 관리자가 REST API를 통해 빅 데이터 클러스터를 부트스트랩하고 관리할 수 있도록 하는 Python으로 작성된 `azdata` 명령줄 유틸리티를 도입했습니다. `azdata`는 `mssqlctl`을 대신합니다. [`azdata` 설치](../big-data-cluster/deploy-install-azdata.md)를 참조하세요. |
|PolyBase |이제 외부 테이블 열 이름이 SQL Server, Oracle, Teradata, MongoDB 및 ODBC 데이터 원본을 쿼리하는 데 사용됩니다. 이전 CTP 릴리스에서는 열이 대상의 서수를 기준으로 바인딩되었으며 외부 테이블 정의의 열 이름은 사용되지 않았습니다.|
|HDFS 계층화 새로 고침 |원격 데이터의 최신 스냅샷에 대해 기존 탑재를 새로 고칠 수 있도록 HDFS 계층화의 새로 고침 기능을 도입합니다. [HDFS 계층화](../big-data-cluster/hdfs-tiering.md)를 참조하세요. |
|Notebook 기반 문제 해결 |CTP 3.2에는 SQL Server 빅 데이터 클러스터 구성 요소의 [배포](../big-data-cluster/deploy-notebooks.md)와 [검색, 진단 및 문제 해결](../big-data-cluster/manage-notebooks.md)에 도움이 되는 Jupyter Notebook이 도입되었습니다. |
| &nbsp; | &nbsp; |

### <a name="new-in-analysis-services"></a>Analysis Services의 새로운 기능

| 새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---| 
| Power BI 캐시 새로 고침에 대한 거버넌스 설정.  | Power BI 서비스는 라이브 연결 보고서의 초기 로드에 대한 대시보드 타일 데이터 및 보고서 데이터를 캐시하여 많은 수의 캐시 쿼리가 SSAS로 전송되도록 하며, 극단적인 경우 서버에 과부하를 발생하기도 합니다. 이 릴리스에는 **ClientCacheRefreshPolicy** 속성이 도입되었습니다. 이 속성을 사용하여 서버 수준에서 이 동작을 재정의할 수 있습니다. 자세히 알아보려면 [일반 속성](https://docs.microsoft.com/analysis-services/server-properties/general-properties)을 참조하세요. |
| 온라인 연결  | 이 기능은 테이블 형식 모델을 온라인 작업으로 연결하는 기능을 제공합니다. 온라인 연결 기능은 온-프레미스 쿼리 스케일 아웃 환경에서 읽기 전용 복제본을 동기화하는 데 사용할 수 있습니다. 자세히 알아보려면 [온라인 연결](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="new-in-language-extensions"></a>언어 확장의 새로운 기능

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
| 새 기본 Java 런타임  | 이제 SQL Server에는 제품 전체의 Java 지원을 위한 Azul System의 Zulu Embedded가 포함되어 있습니다. 자세한 내용은 [SQL Server 2019에서 체험할 수 있는 Java 사용 가능](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/)을 참조하세요. |

### <a name="new-in-sql-server-on-linux"></a>Linux SQL Server의 새로운 기능

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
| CDC(변경 데이터 캡처) 지원 | CDC(변경 데이터 캡처)는 이제 SQL Server 2019용 Linux에서 지원됩니다. |

## <a name="includesql-server-2019includessssqlv15-mdmd-features-by-component"></a>구성 요소별 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 기능

다음 섹션에서는 이전 버전의 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서 개선된 기능과 새 구성 요소를 집중적으로 설명합니다.

## <a name="big-data-clusters"></a>빅 데이터 클러스터

| 새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
| 확장 가능한 빅 데이터 솔루션 | Kubernetes에서 실행되는 SQL Server, Spark 및 HDFS 컨테이너의 [확장 가능한 클러스터 배포](../big-data-cluster/deploy-get-started.md) <br/><br/> Transact-SQL 또는 Spark에서 빅 데이터 읽기, 쓰기 및 처리<br/><br/> 고용량 빅 데이터를 사용하여 가치 높은 관계형 데이터를 쉽게 조합 및 분석<br/><br/>외부 데이터 원본 쿼리<br/><br/>SQL Server에서 관리하는 HDFS에 빅 데이터 저장<br/><br/>클러스터를 통해 여러 외부 데이터 원본에서 데이터 쿼리<br/><br/> AI, 기계 학습 및 기타 분석 작업에 데이터 사용<br/><br/> 빅 데이터 클러스터에서 애플리케이션 배포 및 실행 <br/>|
| &nbsp; | &nbsp; |

자세한 내용은 [SQL Server 빅 데이터 클러스터란 무엇인가요?](../big-data-cluster/big-data-cluster-overview.md)를 참조하세요.

CTP([[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]) 알림 보관](what-s-new-in-sql-server-ver15-prerelease.md)에는 이 기능의 모든 이전 CTP 릴리스에 대해 발표되고 변경된 기능 목록이 포함되어 있습니다.

## <a name="database-engine"></a>데이터베이스 엔진

### <a name="security"></a>보안

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|인덱스 암호화된 열|임의 암호화 및 enclave- 키를 사용하여 암호화된 열에 인덱스를 생성하여 리치 쿼리(`LIKE` 및 비교 연산자 사용)의 성능을 향상시킵니다. [보안 Enclave를 사용한 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.
|TDE(투명한 데이터 암호화)의 초기 검색 일시 중단 및 다시 시작|[TDE(투명한 데이터 암호화) 검색 - 일시 중단 및 다시 시작](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)을 참조하세요.|
|SQL Server 구성 관리자의 인증서 관리|[인증서 관리(SQL Server 구성 관리자)](../database-engine/configure-windows/manage-certificates.md)를 참조하세요.
| &nbsp; | &nbsp; |


### <a name="graph"></a>그래프

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|에지 제약 조건 계단식 삭제 동작 |그래프 데이터베이스의 에지 제약 조건에 대한 계단식 삭제 작업을 정의합니다. [에지 제약 조건](../relational-databases/tables/graph-edge-constraints.md)을 참조하세요. |
|새 그래프 함수 - `SHORTEST_PATH` | `MATCH`의 `SHORTEST_PATH`를 사용하여 그래프에서 노드 2개 사이의 최단 경로를 찾거나 임의의 길이 횡단을 수행합니다.|
|파티션 테이블 및 인덱스| 분할 테이블 및 인덱스의 데이터는 그래프 데이터베이스에서 두 개 이상의 파일 그룹으로 분할될 수 있는 단위로 나뉩니다. |
|그래프 일치 쿼리에서 파생된 테이블 또는 뷰 별칭 사용 |[Graph 에지 제약 조건](../relational-databases/tables/graph-edge-constraints.md)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="indexes"></a>인덱스

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|인덱스에 높은 동시성 삽입에 대한 처리량을 향상시키는 데 도움이 되는 데이터베이스 엔진 내의 최적화를 켭니다. 이 옵션은 ID 열, 시퀀스 또는 날짜/시간 열과 같은 순차 키가 있는 인덱스에서 일반적으로 볼 수 있는 마지막 페이지 삽입 경합에 취약한 인덱스를 대상으로 합니다. 자세한 내용은 [INDEX 만들기](../t-sql/statements/create-index-transact-sql.md#sequential-keys)를 참조하세요.|
|온라인 클러스터형 columnstore 인덱스 작성 및 다시 작성 | [온라인으로 인덱스 작업 수행](../relational-databases/indexes/perform-index-operations-online.md)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="in-memory-databases"></a>메모리 내 데이터베이스

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|하이브리드 버퍼 풀에 대한 DDL 컨트롤 |[하이브리드 버퍼 풀](../database-engine/configure-windows/hybrid-buffer-pool.md)을 사용하여 영구 메모리(PMEM) 디바이스의 데이터베이스 파일에 있는 데이터베이스 페이지를 필요 시 곧바로 액세스합니다.|
|메모리 최적화 tempdb 메타데이터|[메모리 최적화 tempdb 메타데이터](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)를 참조하세요.|
| &nbsp; | &nbsp; |

### <a name="linked-servers"></a>연결된 서버

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|연결된 서버는 UTF-8 문자 인코딩을 지원합니다. |[데이터 정렬 및 유니코드 지원](../relational-databases/collations/collation-and-unicode-support.md) |
| &nbsp; | &nbsp; |

### <a name="polybase"></a>PolyBase

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|PolyBase |이제 외부 테이블 열 이름이 SQL Server, Oracle, Teradata, MongoDB 및 ODBC 데이터 원본을 쿼리하는 데 사용됩니다. |
| &nbsp; | &nbsp; |

### <a name="collation"></a>데이터 정렬

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|UTF-8 문자 인코딩 지원 |BIN2 데이터 정렬(`Latin1_General_100_BIN2_UTF8`)에 사용할 수 있습니다. [데이터 정렬 및 유니코드 지원](../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요. |
|설치하는 동안 UTF-8 데이터 정렬을 기본 데이터 정렬로 선택 | [데이터 정렬 및 유니코드 지원](../relational-databases/collations/collation-and-unicode-support.md#ctp23)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="server-settings"></a>서버 설정

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|설정 시 `MIN` 및 `MAX` 서버 메모리 값을 설정합니다. |설치하는 동안 서버 메모리 값을 설정할 수 있습니다. **권장** 옵션 [서버 메모리 서버 구성 옵션](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually)을 선택한 후 기본값, 계산된 권장 값을 사용하거나 사용자 고유의 값을 수동으로 지정합니다.|
|SQL Server 설치 프로그램이 MAXDOP 설정을 사용하도록 설정 |새 권장 사항은 설명된 지침을 따릅니다. [max degree of parallelism 서버 구성 옵션 구성](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)|
|하이브리드 버퍼 풀| SQL Server 데이터베이스 엔진의 새로운 기능으로, 영구 메모리(PMEM) 디바이스의 데이터베이스 파일에 있는 데이터베이스 페이지를 필요 시 곧바로 액세스합니다. [하이브리드 버퍼 풀](../database-engine/configure-windows/hybrid-buffer-pool.md)을 참조하세요.|
| &nbsp; | &nbsp; |

### <a name="performance-monitoring"></a>성능 모니터링

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|스칼라 UDF 인라인 처리 |자동으로 스칼라 UDF(사용자 정의 함수)를 관계식으로 변환하고 이를 호출 SQL 쿼리에 포함합니다. [스칼라 UDF 인라인 처리](../relational-databases/user-defined-functions/scalar-udf-inlining.md)를 참조하세요. |
| `sys.dm_exec_requests` 열 `command` | `SELECT`가 쿼리 실행을 계속하기 전에 동기 통계 업데이트 작업이 완료되도록 기다리고 있는 경우 `SELECT (STATMAN)`을 표시합니다. [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)를 참조하세요.|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | `sys.dm_os_wait_stats` 동적 관리 뷰의 새 대기 유형입니다. 동기 통계 새로 고침 작업에 소요된 누적된 인스턴스 수준 시간을 보여 줍니다. [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)를 참조하세요.|
|쿼리 저장소에 대한 캡처 정책 사용자 지정|사용하도록 설정된 경우 특정 서버의 데이터 컬렉션을 정밀 조정하기 위해 새로운 쿼리 저장소 캡처 정책 설정 아래에서 추가 쿼리 저장소 구성을 사용할 수 있습니다. 자세한 내용은 [ALTER DATABASE SET 옵션](../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.|
|`sys.dm_exec_query_plan_stats` |새 DMF는 대부분의 쿼리에 대해 마지막으로 알려진 실제 실행 계획과 동일한 것을 반환합니다. [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)를 참조하세요.|
|`LAST_QUERY_PLAN_STATS` | `sys.dm_exec_query_plan_stats`를 사용하도록 설정하는 새 데이터베이스 범위 지정 구성입니다. [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 참조하세요.|
|`LIGHTWEIGHT_QUERY_PROFILING`|새 데이터베이스 범위 지정 구성입니다. [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp)을 참조하세요. |
|`query_post_execution_plan_profile` | 확장 이벤트는 표준 프로파일링을 사용하는 `query_post_execution_showplan`과 달리 경량 프로파일링을 기반으로한 실제 계획과 동등한 것을 수집합니다. [쿼리 프로파일링 인프라](../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요.|
|행 모드 메모리 부여 피드백. |[행 모드 메모리 부여 피드백](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback) |
|테이블 변수 지연 컴파일.|[테이블 변수 지연 컴파일](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation) |
|대략 `COUNT DISTINCT`입니다.|[대략적인 쿼리 처리](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)|
|rowstore의 일괄 처리 모드.|[rowstore의 일괄 처리 모드](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore) |

### <a name="language-extensions"></a>언어 확장

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|새 Java 언어 SDK | SQL Server에서 실행할 수 있는 Java 프로그램의 개발을 간소화합니다. [SQL Server Machine Learning Services의 새로운 기능](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)을 참조하세요. |
|SQL Server 언어 확장 - [Java 언어 확장](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)|[Microsoft SQL Server용 Java에 대한 Microsoft 확장성 SDK](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server)는 현재 오픈 소스로 [GitHub에서 제공합니다](https://github.com/microsoft/sql-server-language-extensions).|
|외부 언어 등록|새로운 DDL `CREATE EXTERNAL LANGUAGE`는 SQL Server에서 Java와 같은 외부 언어를 등록합니다. [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md)를 참조하세요. |
|Java 데이터 형식 지원|[Java 데이터 형식](../language-extensions/how-to/java-to-sql-data-types.md)을 참조하세요.|

### <a name="spatial"></a>공간

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
| 새 SRID(spatial reference identifier) |[오스트레일리아 GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020)은 글로벌 위치 시스템과 더욱 긴밀하게 정렬된 더 강력하고 정확한 데이터를 제공합니다. 새 SRID는 다음과 같습니다.<br/><br/> - 7843 - 지리적 2D<br/> - 7844 - 지리적 3D <br/><br/>[sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) 보기에는 새 SRID의 정의가 포함되어 있습니다. |
| &nbsp; | &nbsp; |

### <a name="performance"></a>성능

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|가속 데이터베이스 복구 | 데이터베이스별로 가속 데이터베이스 복구를 사용하도록 설정합니다. [가속 데이터베이스 복구](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr)를 참조하세요.|
|빠른 전달 및 정적 커서 강제 적용 | 쿼리 저장소 계획에서 빠른 전달 및 정적 커서에 대한 지원을 강제 적용합니다. [계획에서 빠른 전달 및 정적 커서에 대한 강제 적용 지원](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23)을 참조하세요.|
|워크로드에 대한 다시 컴파일 감소| 여러 범위에서 임시 테이블을 사용하는 기능이 개선되었습니다. [워크로드에 대한 다시 컴파일 감소](../relational-databases/tables/tables.md#ctp23)를 참조하세요. |
|간접 검사점 확장성 |[향상된 간접 검사점 확장성](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23)을 참조하세요.|
| &nbsp; | &nbsp; |

### <a name="availability-groups"></a>가용성 그룹

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|최대 5개의 동기 복제본|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 동기 복제본의 최대 수가 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 3개에서 5개로 증가되었습니다. 그룹 내에서 자동 장애 조치가 수행되도록 이 그룹을 5개 복제본으로 구성할 수 있습니다. 여기에는 하나의 주 복제본 및 4개의 동기 보조 복제본이 있습니다.|
|보조-주 복제본 연결 리디렉션| 이 기능은 연결 문자열에 지정된 대상 서버에 관계없이 클라이언트 애플리케이션 연결이 주 복제본으로 전송되도록 합니다. 자세한 내용은 [보조-주 복제본 읽기/쓰기 연결 리디렉션(Always On 가용성 그룹)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)을 참조하세요.|
| &nbsp; | &nbsp; |

### <a name="error-messages"></a>오류 메시지

|새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|자세한 정보 잘림 경고 | 잘림 오류 메시지는 기본적으로 테이블 및 열 이름과 잘린 값을 포함합니다. [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation)를 참조하세요.|
| &nbsp; | &nbsp; |

## <a name="sql-server-on-linux"></a>SQL Server on Linux

| 새로운 기능 또는 업데이트 | 세부 정보 |
|:-----|:-----|
|새 컨테이너 레지스트리|[Docker에서 SQL Server 컨테이너 시작](../linux/quickstart-install-connect-docker.md) |
|Kubernetes를 사용하는 Docker 컨테이너의 Always On 가용성 그룹 |[컨테이너의 Always On 가용성 그룹](../linux/sql-server-ag-kubernetes.md) |
|복제 지원 |[Linux의 SQL Server 복제 개체](../linux/sql-server-linux-replication.md)
|MSDTC(Microsoft Distributed Transaction Coordinator) 지원 |[Linux에서 MSDTC를 구성하는 방법](../linux/sql-server-linux-configure-msdtc.md) |
|타사 AD 공급자에 대한 OpenLDAP 지원 |[자습서: Linux에서 SQL Server와 Active Directory 인증 사용](../linux/sql-server-linux-active-directory-authentication.md) |
|Linux의 Machine Learning |[Linux에서 Machine Learning 구성](../linux/sql-server-linux-setup-machine-learning.md) |
|Tempdb 개선 사항 | 기본적으로 Linux에 SQL Server를 새로 설치하면 논리적 코어 수(최대 8개 데이터 파일 포함)에 따라 여러 tempdb 데이터 파일이 생성됩니다. 이 위치에서 부 버전 또는 주 버전 업그레이드에는 적용되지 않습니다. 각 tempdb 파일은 자동 증가 속도가 64MB인 8MB입니다. 이 동작은 Windows의 기본 SQL Server 설치와 유사합니다. |
| Linux의 PolyBase. | Hadoop이 아닌 커넥터에 대한 Linux에 [PolyBase를 설치](../relational-databases/polybase/polybase-linux-setup.md)합니다.<br/><br/>[PolyBase 형식 매핑](../relational-databases/polybase/polybase-type-mapping.md). |
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

## <a name="analysis-services"></a>Analysis Services

| 새로운 기능 또는 업데이트 | 세부 정보 |
|:---|:---|
|테이블 형식 모델의 계산 그룹| [테이블 형식 모델의 계산 그룹](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|계산 그룹을 포함하는 테이블 형식 모델에 대한 MDX 쿼리 지원 | [계산 그룹](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)을 참조하세요. |
|계산 그룹을 사용하여 측정값 서식을 동적으로 지정합니다. |이 기능을 사용하면 [계산 그룹](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)을 포함하는 측정값에 대한 형식 문자열을 조건부로 변경할 수 있습니다. 예를 들어 통화 변환을 통해 서로 다른 외국 통화 형식을 사용하여 측정값을 표시할 수 있습니다.|
|테이블 형식 모델의 다 대 다 관계|[테이블 형식 모델의 다 대 다 관계](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|리소스 거버넌스에 대한 속성 설정|[리소스 거버넌스에 대한 속성 설정](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
| &nbsp; | &nbsp; |

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

지원에서 제외된 특정 기능은 [릴리스 정보](sql-server-ver15-release-notes.md)를 참조하세요.

또한 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2에서 추가되었거나 개선된 기능은 다음과 같습니다.

## <a name="see-also"></a>관련 항목:

- [`SqlServer` PowerShell 모듈](https://www.powershellgallery.com/packages/Sqlserver)
- [SQL Server PowerShell 설명서](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>다음 단계

- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 릴리스 정보](sql-server-ver15-release-notes.md).

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: 기술 백서](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />2018년 9월에 게시되었습니다. Windows, Linux 및 Docker 컨테이너용 Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0에 적용됩니다.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
