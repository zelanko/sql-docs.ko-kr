---
title: 쿼리 저장소에 대한 모범 사례 | Microsoft Docs
description: '워크로드에 SQL Server 쿼리 저장소를 사용하는 모범 사례(예: 최신 SQL Server Management Studio 및 Query Performance Insight 사용)에 대해 알아봅니다.'
ms.custom: ''
ms.date: 09/02/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, best practices
ms.assetid: 5b13b5ac-1e4c-45e7-bda7-ebebe2784551
author: pmasl
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c19088caa9942d3eafaf6ccf8c6195851f05c27f
ms.sourcegitcommit: f7c9e562d6048f89d203d71685ba86f127d8d241
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2020
ms.locfileid: "90042826"
---
# <a name="best-practices-with-query-store"></a>쿼리 저장소에 대한 모범 사례

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

이 문서에서는 워크로드에 SQL Server 쿼리 저장소를 사용하는 모범 사례에 대해 설명합니다.

## <a name="use-the-latest-ssmanstudiofull"></a><a name="SSMS"></a> 최신 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 사용

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에는 쿼리 저장소를 구성하고 수집된 워크로드 데이터를 사용하도록 설계된 사용자 인터페이스 집합이 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 최신 버전은 [여기](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)에서 다운로드하세요.

문제 해결 시나리오에서 쿼리 저장소를 사용하는 방법에 대한 간략한 설명은 [쿼리 저장소 @Azure 블로그](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)를 참조하세요.

## <a name="use-query-performance-insight-in-azure-sql-database"></a><a name="Insight"></a> Azure SQL Database에서 Query Performance Insight 사용

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 쿼리 저장소를 실행하는 경우 [Query Performance Insight](https://docs.microsoft.com/azure/sql-database/sql-database-query-performance)를 사용하여 시간에 따른 리소스 사용을 분석할 수 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 및 [Azure Data Studio](../../azure-data-studio/what-is.md)를 사용하여 CPU, 메모리, I/O 등 모든 쿼리의 자세한 리소스 사용 정보를 가져올 수 있으며 Query Performance Insight를 사용하면 이와 같은 쿼리가 데이터베이스의 전반적인 DTU 사용에 미치는 영향을 빠르고 효율적으로 확인할 수 있습니다. 자세한 내용은 [Azure SQL 데이터베이스 Query Performance Insight](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/)를 참조하세요.

이 섹션에서는 쿼리 저장소 및 종속 기능의 안정적인 운영을 보장하도록 설계된 최적의 구성 기본값을 설명합니다. 기본 구성은 지속적인 데이터 수집을 위해 최적화됩니다(예: OFF/READ_ONLY 상태에 소요되는 시간 최소화). 사용 가능한 모든 쿼리 저장소 옵션에 대한 자세한 내용은 [ALTER DATABASE SET 옵션(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md#query-store)을 참조하세요.

| 구성 | Description | 기본값 | 주석 |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |쿼리 저장소가 사용자 데이터베이스 내부에서 사용하는 데이터 공간에 대한 제한을 지정합니다. |100 |새 데이터베이스에 적용 |
| INTERVAL_LENGTH_MINUTES |쿼리 계획에 대해 수집된 런타임 통계가 집계되고 지속되는 기간의 규모를 정의합니다. 모든 활성 쿼리 계획은 이 구성을 통해 정의된 기간에 대해 최대 하나의 행을 갖습니다. |60 |새 데이터베이스에 적용 |
| STALE_QUERY_THRESHOLD_DAYS |지속되는 런타임 통계 및 비활성 쿼리의 보존 기간을 제어하는 시간 기반 정리 정책 |30 |새 데이터베이스 및 이전 기본값을 포함하는 데이터베이스에 적용(367) |
| SIZE_BASED_CLEANUP_MODE |쿼리 저장소 데이터 크기가 한도에 접근할 때, 자동 데이터 정리를 수행할지를 지정합니다. |AUTO |모든 데이터베이스에 적용 |
| QUERY_CAPTURE_MODE |모든 쿼리를 추적할지 또는 쿼리의 하위 집합만 추적할지를 지정합니다. |AUTO |모든 데이터베이스에 적용 |
| FLUSH_INTERVAL_SECONDS |캡처한 런타임 통계를 디스크에 플러시하기 전에 메모리에 유지하는 최대 기간을 지정합니다. |900 |새 데이터베이스에 적용 |
| | | | |

> [!IMPORTANT]
> 이러한 기본값은 모든 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 쿼리 저장소 활성화 마지막 단계에서 자동으로 적용됩니다. 사용하도록 설정된 후 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 기본 워크로드 또는 쿼리 저장소의 안정적인 운영에 부정적인 영향을 미치지 않는 한 고객이 설정한 구성 값을 변경하지 않습니다.

> [!NOTE]  
> 쿼리 저장소는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 단일 데이터베이스 및 탄력적 풀에서 사용하지 않도록 설정할 수 없습니다. `ALTER DATABASE [database] SET QUERY_STORE = OFF`를 실행하면 경고 `'QUERY_STORE=OFF' is not supported in this version of SQL Server.`가 반환됩니다. 

사용자 지정 설정을 유지하려는 경우에는, [쿼리 저장소 옵션을 사용하여 ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md#query-store) 를 사용하여 이전 상태로 구성을 되돌립니다. 최적의 구성 매개 변수를 선택하는 방법을 알아보려면 [쿼리 저장소 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md)를 확인하세요.

## <a name="use-query-store-with-elastic-pool-databases"></a>탄력적 풀 데이터베이스에서 쿼리 저장소 사용

더 세부적으로 패키지된 풀에서는 모든 데이터베이스에서 쿼리 저장소를 사용할 수 있습니다. 탄력적 풀의 많은 데이터베이스에 대해 쿼리 저장소를 사용하도록 설정한 경우에 발생할 수 있었던 과도한 리소스 사용과 관련된 모든 문제가 해결되었습니다.

## <a name="keep-query-store-adjusted-to-your-workload"></a><a name="Configure"></a> 쿼리 저장소를 작업에 맞게 조정된 상태로 유지

작업 및 성능 문제 해결 요구 사항을 기반으로 쿼리 저장소를 구성합니다.
시작할 때는 기본 매개 변수를 사용하는 것이 좋지만, 시간이 흐름에 따라 쿼리 저장소가 동작하는 방식을 모니터링하여 구성을 적절하게 조정해야 합니다.

 ![쿼리 저장소 속성](../../relational-databases/performance/media/query-store-properties.png "query-store-properties")

 매개 변수 값 설정을 위해 따라야 할 지침은 아래와 같습니다.

**최대 크기(MB)** : 데이터베이스 내부에서 쿼리 저장소가 사용하는 데이터 공간의 한도를 지정합니다. 쿼리 저장소의 작업 모드에 직접적으로 영향을 주는 가장 중요한 설정입니다.

쿼리 저장소에서 쿼리, 실행 계획 및 통계를 수집하는 동안 이 한도에 도달할 때까지 데이터베이스에서 해당 크기가 증가합니다. 한도에 도달하면 쿼리 저장소는 작업 모드를 자동으로 읽기 전용으로 변경하고 새 데이터 수집을 중지합니다. 즉 성능 분석은 더 이상 정확하지 않게 됩니다.

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]의 기본값은 100MB입니다. 워크로드에서 서로 다른 쿼리와 계획을 많이 생성하거나 쿼리 기록을 장기간 유지하려는 경우 이 크기가 충분하지 않을 수도 있습니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 기본값은 1GB입니다. 현재 공간 사용량을 계속 추적하고, **최대 크기(MB)** 값을 늘려 쿼리 저장소가 읽기 전용 모드로 전환되지 않도록 합니다.

> [!IMPORTANT]
> **최대 크기(MB)** 한도는 엄격하게 적용되지 않습니다. 쿼리 저장소가 디스크에 데이터를 쓰는 경우에만 스토리지 크기가 확인됩니다. 이 간격은 **데이터 플러시 간격(분)** 옵션으로 설정됩니다. 쿼리 저장소가 스토리지 크기 검사 간에 최대 크기 한도를 위반할 경우 읽기 전용 모드로 전환됩니다. **크기 기반 정리 모드**를 사용하도록 설정하면, 최대 크기 한도를 적용하는 정리 메커니즘도 트리거됩니다.

[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하거나 다음 스크립트를 실행하여 쿼리 저장소 크기에 대한 최신 정보를 확인합니다.

```sql
USE [QueryStoreDB];
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
 max_storage_size_mb, readonly_reason
FROM sys.database_query_store_options;
```

다음 스크립트는 **최대 크기(MB)** 에 새 값을 설정합니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);
```

 **데이터 플러시 간격(분)** : 수집된 런타임 통계를 디스크에 유지하는 빈도를 정의합니다. GUI(그래픽 사용자 인터페이스)에서는 분 단위로 표시되지만 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서는 초 단위로 표시됩니다. 기본값은 900초이며 그래픽 사용자 인터페이스에서는 15분입니다. 워크로드에서 서로 다른 쿼리와 계획을 대량으로 생성하지 않거나 데이터베이스가 종료되기까지 데이터를 더 오래 유지해도 되는 경우 값을 늘리는 것이 좋습니다.

> [!NOTE]
> 추적 플래그 7745를 사용하면 장애 조치(failover) 또는 종료 명령 시 쿼리 저장소 데이터를 디스크에 쓸 수 없습니다. 자세한 내용은 [중요 업무용 서버에서 추적 플래그 사용](#Recovery) 섹션을 참조하세요.

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 **데이터 플러시 간격**에 다른 값을 설정할 수 있습니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS = 900);
```

**통계 수집 간격**: 수집되는 런타임 통계의 세분성 수준(분)을 정의합니다. 기본값은 60분입니다. 문제를 검색하고 완화하는 시간을 줄이거나 높은 수준의 세분성이 필요한 경우 값을 줄이는 것이 좋습니다. 하지만 이 값은 쿼리 저장소 데이터 크기에 직접 영향을 미칠 수 있음을 염두에 둬야 합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 **통계 수집 간격**에 다른 값을 설정할 수 있습니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 60);
```

**부실 쿼리 임계값(일)** : 지속형 런타임 통계와 비활성 쿼리의 보존 기간(일)을 제어하는 시간 기반 정리 정책입니다. 기본적으로 쿼리 저장소는 30일 동안 데이터를 유지하도록 구성되어 있으므로, 이 시간이 해당 시나리오에서 불필요하게 길 수도 있습니다.

사용하지 않을 기록 데이터는 유지하지 않는 것이 좋습니다. 이렇게 하면 읽기 전용 상태로 변경되는 횟수가 줄어듭니다. 쿼리 저장소 데이터 크기와 문제를 검색하여 완화하는 시간도 더 예측 가능해집니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 또는 다음 스크립트를 사용하여 시간 기반 정리 정책을 구성합니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 90));
```

**크기 기반 정리 모드**: 쿼리 저장소 데이터 크기가 한도에 도달할 때 자동 데이터 정리를 수행할지 여부를 지정합니다. 크기 기반 정리를 활성화하여 쿼리 저장소가 항상 읽기/쓰기 모드로 실행되고 최신 데이터를 수집하도록 합니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);
```

**쿼리 저장소 캡처 모드**: 쿼리 저장소에 대한 쿼리 캡처 정책을 지정합니다.

- **모두**: 쿼리를 모두 캡처합니다. 이 옵션은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]의 기본값입니다.
- **Auto**: 빈번하지 않은 쿼리와 컴파일 및 실행 기간이 짧은 쿼리는 무시됩니다. 실행 횟수, 컴파일 및 런타임 기간의 임계값은 내부적으로 결정됩니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 이 옵션이 기본 옵션입니다.
- **없음**: 쿼리 저장소에서 새 쿼리 캡처가 중지됩니다.
- **Custom**: 추가 컨트롤 및 데이터 수집 정책을 미세 조정하는 기능을 허용합니다. 새 사용자 지정 설정은 내부 캡처 정책 시간 임계값 내에서 수행되는 작업을 정의합니다. 이 시간 경계 내에서 구성 가능한 조건이 평가되고, true인 조건이 있으면 쿼리 저장소에서 쿼리를 캡처할 수 있습니다.

> [!IMPORTANT]
> 쿼리 저장소 캡처 모드를 **All**, **Auto** 또는 **Custom**으로 설정하면 커서, 저장 프로시저 내부 쿼리 및 네이티브 컴파일된 쿼리가 항상 캡처됩니다. 네이티브 컴파일된 쿼리를 캡처하려면 [sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md)를 사용하여 쿼리별 통계 수집을 사용하도록 설정합니다.

 다음 스크립트는 QUERY_CAPTURE_MODE를 AUTO로 설정합니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);
```

### <a name="examples"></a>예제

다음 예제에서는 QUERY_CAPTURE_MODE를 AUTO로 설정하고 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 다른 권장 옵션을 설정합니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60
    );
```

다음 예제에서는 QUERY_CAPTURE_MODE를 AUTO로 설정하고, 대기 통계를 포함하도록 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]에서 다른 권장 옵션을 설정합니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON
    );
```

다음 예제에서는 QUERY_CAPTURE_MODE를 AUTO로 설정하고, [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서 다른 권장 옵션을 설정하며, ‘필요에 따라’ 새로운 기본 AUTO 캡처 모드 대신 CUSTOM 캡처 정책을 기본값으로 설정합니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
      QUERY_CAPTURE_MODE = CUSTOM,
      QUERY_CAPTURE_POLICY = (
        STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS,
        EXECUTION_COUNT = 30,
        TOTAL_COMPILE_CPU_TIME_MS = 1000,
        TOTAL_EXECUTION_CPU_TIME_MS = 100
      )
    );
```

## <a name="start-with-query-performance-troubleshooting"></a>쿼리 성능 문제 해결 시작

다음 다이어그램에 표시된 대로 쿼리 저장소의 워크플로 문제는 간단히 해결됩니다.

![쿼리 저장소 문제 해결](../../relational-databases/performance/media/query-store-troubleshooting.png "query-store-troubleshooting")

이전 섹션에서 설명한 대로 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 통해 쿼리 저장소를 사용하도록 설정하거나, 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.

```sql
ALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON;
```

쿼리 저장소에서 워크로드를 정확하게 나타내는 데이터 세트를 수집할 때까지 약간의 시간이 걸립니다. 매우 복잡한 작업의 경우라도 일반적으로 하루면 충분합니다. 그러나 기능을 사용하도록 설정한 후 즉시 데이터 검색을 시작하고 주의가 필요한 쿼리를 확인할 수 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 개체 탐색기에서 데이터베이스 노드 아래의 쿼리 저장소 하위 폴더로 이동하여 특정 시나리오에 대한 문제 해결 뷰를 엽니다.

[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 쿼리 저장소 보기는 실행 메트릭 집합을 사용하여 동작하며 각 메트릭은 다음 통계 함수 중 하나로 표현됩니다.

|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전|실행 메트릭|통계 함수|
|----------------------|----------------------|------------------------|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|CPU 시간, 기간, 실행 횟수, 논리적 읽기, 논리적 쓰기, 메모리 사용, 물리적 읽기, CLR 시간, DOP(병렬 처리 수준) 및 행 개수|평균, 최대값, 최소값, 표준 편차, 합계|
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|CPU 시간, 기간, 실행 횟수, 논리적 읽기, 논리적 쓰기, 메모리 사용, 물리적 읽기, CLR 시간, 병렬 처리 수준, 행 개수, 로그 메모리, TempDB 메모리 및 대기 시간|평균, 최대값, 최소값, 표준 편차, 합계|

다음 그림은 쿼리 저장소 보기를 찾는 방법을 보여 줍니다.

![쿼리 저장소 보기](../../relational-databases/performance/media/objectexplorerquerystore_sql17.png "쿼리 저장소 보기")

다음 표에서는 각 쿼리 저장소 보기를 사용하는 시기를 설명합니다.

|SQL Server Management Studio 뷰|시나리오|
|---------------|--------------|
|**재발된 쿼리**|최근에 실행 메트릭이 재발(예: 악화로 변경)된 쿼리를 정확히 파악합니다. <br />이 뷰를 사용하여 애플리케이션에서 관찰된 성능 문제와 수정하거나 개선해야 할 실제 쿼리를 상호 연결할 수 있습니다.|
|**전체 리소스 사용**|실행 메트릭 중 하나에 대한 데이터베이스의 전체 리소스 사용을 분석합니다.<br />리소스 패턴(낮 작업 vs. 밤 작업)을 식별하고 데이터베이스에 대한 전체 사용을 최적화하려면 이 보기를 사용합니다.|
|**리소스를 가장 많이 사용하는 쿼리**|관심 있는 메트릭 실행을 선택하고 제공된 시간 간격 동안 가장 값이 높은 쿼리를 확인합니다. <br />이 뷰를 사용하여 데이터베이스 리소스 사용에 가장 큰 영향을 미치는 가장 관련된 쿼리에 집중할 수 있습니다.|
|**강제 계획이 포함된 쿼리**|쿼리 저장소를 사용하여 이전 강제 계획을 나열합니다. <br />모든 현재 강제 계획에 빠르게 액세스하려면 이 보기를 사용합니다.|
|**고변형 쿼리**|원하는 시간 간격의 기간, CPU 시간, IO 및 메모리 사용량과 같은 사용 가능한 차원과 관련하여 실행 변형이 높은 쿼리를 분석합니다.<br />이 뷰를 사용하여 애플리케이션 전체의 사용자 환경에 영향을 미칠 수 있는, 성능 변형이 높은 쿼리를 확인할 수 있습니다.|
|**쿼리 대기 통계**|데이터베이스에서 가장 많이 사용되는 대기 범주는 무엇이고 선택한 대기 범주에 가장 많은 영향을 주는 쿼리는 무엇인지 분석합니다.<br />이 뷰를 사용하여 대기 통계를 분석하고, 애플리케이션의 사용자 환경에 영향을 줄 수 있는 쿼리를 확인할 수 있습니다.<br /><br />적용 대상: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18.0 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터|
|**추적된 쿼리**|가장 중요한 쿼리 실행을 실시간으로 추적합니다. 일반적으로 강제 계획을 사용하는 쿼리가 있고 해당 쿼리 성능이 안정적인지 확인하려고 할 경우 이 보기를 사용합니다.|

> [!TIP]
> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용하여 리소스를 가장 많이 사용하는 쿼리를 확인하고, 선택한 계획을 변경하여 재발된 쿼리를 수정하는 방법은 [쿼리 저장소 @Azure 블로그](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)를 참조하세요.

최적이 아닌 성능의 쿼리를 확인한 경우 수행할 작업은 문제의 성격에 따라 다릅니다.

- 쿼리가 여러 계획으로 실행되었으며 마지막 계획이 이전 계획보다 훨씬 악화된 경우 계획 강제 적용 메커니즘을 사용하여 강제 적용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 최적화 프로그램에서 계획을 적용하려고 합니다. 계획을 적용하는 데 실패하면 XEvent가 발생하고, 최적화 프로그램이 일반적인 방법으로 최적화하도록 지시됩니다.

  ![쿼리 저장소 계획 강제 적용](../../relational-databases/performance/media/query-store-force-plan.png "query-store-force-plan")

  > [!NOTE]
  > 위의 그림에서 쿼리 계획에 따라 셰이프가 다를 수 있으며, 가능한 각 셰이프 상태의 의미는 다음과 같습니다.<br />
  >
  > |셰이프|의미|
  > |-------------------|-------------|
  > |Circle|쿼리 완료됨(기본 실행이 완료됨)|
  > |Square|취소됨(클라이언트 시작으로 실행이 중단됨)|
  > |Triangle|실패(예외로 실행이 중단됨)|
  >
  > 또한 셰이프 크기는 지정된 시간 간격 내의 쿼리 실행 횟수를 나타냅니다. 실행 횟수가 많을수록 크기가 증가합니다.

- 쿼리에 최적 실행을 위한 인덱스가 없다는 결론을 내릴 수도 있습니다. 이 정보는 쿼리 실행 계획 내에 표시됩니다. 누락된 인덱스를 만들고 쿼리 저장소를 사용하여 쿼리 성능을 확인합니다.

   ![쿼리 저장소 계획 표시](../../relational-databases/performance/media/query-store-show-plan.png "query-store-show-plan")

작업을 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 실행하는 경우 인덱스 권장 사항을 자동으로 받을 수 있도록 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 인덱스 관리자에 등록합니다.

- 실행 계획의 실제 행 수와 예상 행 수 간에 차이가 큰 경우 통계 재컴파일을 적용할 수 있는 경우도 있습니다.
- 문제가 되는 쿼리를 다시 생성합니다. 예를 들어 쿼리 매개 변수화를 활용하거나 보다 최적 논리를 구현하도록 다시 생성합니다.

## <a name="verify-that-query-store-collects-query-data-continuously"></a><a name="Verify"></a> 쿼리 저장소에서 쿼리 데이터를 계속 수집하는지 확인

쿼리 저장소에서 작업 모드를 자동으로 변경할 수 있습니다. 쿼리 저장소의 상태를 정기적으로 모니터링하여 쿼리 저장소가 작동 중인지 확인하고, 예방 가능한 원인으로 인해 오류가 발생하지 않도록 조치를 취합니다. 다음 쿼리를 실행하여 작업 모드를 결정하고 가장 관련성이 높은 매개 변수를 확인합니다.

```sql
USE [QueryStoreDB];
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
    max_storage_size_mb, readonly_reason, interval_length_minutes,
    stale_query_threshold_days, size_based_cleanup_mode_desc,
    query_capture_mode_desc
FROM sys.database_query_store_options;
```

`actual_state_desc` 및 `desired_state_desc` 간 차이는 작업 모드 변경이 자동으로 발생했음을 나타냅니다. 가장 일반적인 변경은 쿼리 저장소가 읽기 전용 모드로 자동 전환되는 경우입니다. 아주 드물긴 하지만, 내부 오류로 인해 쿼리 저장소가 오류 상태로 종료될 수도 있습니다.

실제 상태가 읽기 전용인 경우 **readonly_reason** 열을 사용하여 원인을 파악합니다. 일반적으로 크기 할당량 초과로 인해 쿼리 저장소가 읽기 전용 모드로 전환되었음을 알 수 있습니다. 이 경우 **readonly_reason**은 65536으로 설정됩니다. 다른 이유를 보려면 [sys.database_query_store_options&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)를 참조하세요.

다음 단계를 수행하여 쿼리 저장소를 읽기-쓰기 모드로 전환하고 데이터 수집을 활성화해 보세요.

- **ALTER DATABASE** 의 **MAX_STORAGE_SIZE_MB**옵션을 사용하여 최대 스토리지 크기를 늘립니다.
- 다음 문을 사용하여 쿼리 저장소 데이터를 정리합니다.

  ```sql
  ALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR;
  ```

명시적으로 작업 모드를 읽기/쓰기로 변경하는 다음 문을 실행하여 위 단계 중 하나 또는 모두를 적용할 수 있습니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);
```

사전 조치를 위해 다음 단계를 수행합니다.

- 모범 사례를 적용하여 작동 모드의 자동 변동을 방지할 수 있습니다. 쿼리 저장소 크기가 항상 허용되는 최댓값 아래인지 확인하여 읽기 전용 모드로 전환될 가능성을 줄입니다. 크기가 한도에 도달할 때 쿼리 저장소에서 데이터를 자동으로 정리할 수 있도록 [쿼리 저장소 구성](#Configure) 섹션에 설명된 대로 크기 기반 정책을 활성화합니다.
- 가장 최근 데이터가 보존되었는지 확인하려면 오래된 정보를 정기적으로 제거하도록 시간 기반 정책을 구성합니다.
- 마지막으로 **쿼리 저장소 캡처 모드**를 **Auto**로 설정하는 것이 좋습니다. 이렇게 하면 주로 워크로드와 관련성이 낮은 쿼리가 필터링하여 제외됩니다.

### <a name="error-state"></a>ERROR 상태

쿼리 저장소를 복구하려면 명시적으로 읽기/쓰기 모드를 설정하고 실제 상태를 다시 확인합니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
    max_storage_size_mb, readonly_reason, interval_length_minutes,
    stale_query_threshold_days, size_based_cleanup_mode_desc,
    query_capture_mode_desc
FROM sys.database_query_store_options;
```

문제가 지속되면 손상된 쿼리 저장소 데이터가 디스크에 유지됨을 나타냅니다.

[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터, 영향을 받는 데이터베이스 내에서 **sp_query_store_consistency_check** 저장 프로시저를 실행하여 쿼리 저장소를 복구할 수 있습니다. 복구 작업을 시도하기 전에 쿼리 저장소를 사용하지 않도록 설정해야 합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 경우, 표시된 것처럼 쿼리 저장소에서 데이터를 지워야 합니다.

복구에 실패한 경우 읽기/쓰기 모드를 설정하기 전에 쿼리 저장소를 지워볼 수도 있습니다.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE CLEAR;
GO

ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
    max_storage_size_mb, readonly_reason, interval_length_minutes,
    stale_query_threshold_days, size_based_cleanup_mode_desc,
    query_capture_mode_desc
FROM sys.database_query_store_options;
```

## <a name="set-the-optimal-query-store-capture-mode"></a>최적 쿼리 저장소 캡처 모드 설정

쿼리 저장소에 가장 관련성이 높은 데이터를 보관합니다. 다음 표에서는 각 쿼리 저장소 캡처 모드의 일반적인 시나리오를 설명합니다.

|쿼리 저장소 캡처 모드|시나리오|
|------------------------|--------------|
|**모두**|모든 쿼리 셰이프 및 해당 실행 빈도와 기타 통계 관점에서 워크로드를 철저하게 분석합니다.<br /><br /> 작업에서 새 쿼리를 식별합니다.<br /><br /> 사용자나 자동 매개 변수화에 대한 기회를 식별하는 데 임시 쿼리를 사용하는지 검색합니다.<br /><br />참고: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 및[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]의 기본 캡처 모드입니다.|
|**자동**|관련성이 높고 실행 가능한 쿼리에 주목합니다. 예를 들어 정기적으로 실행되거나 리소스 사용이 상당히 많은 쿼리가 여기에 해당합니다.<br /><br />참고: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 이 모드가 기본 캡처 모드입니다.|
|**없음**|런타임 시 모니터링하고 다른 쿼리에서 발생할 수 있는 방해 요소를 제거할 쿼리 집합을 이미 캡처했습니다.<br /><br /> 이 모드는 환경 테스트 및 벤치마킹에 적합합니다.<br /><br /> 또한 애플리케이션 작업을 모니터링하도록 구성된 쿼리 저장소 구성을 제공하는 소프트웨어 공급업체에게도 적절합니다.<br /><br /> 이 모드는 주의해서 사용해야 합니다. 중요한 새 쿼리를 추적하고 최적화할 기회를 놓칠 수 있기 때문입니다. 필요한 특정 시나리오가 없으면 사용하지 마세요.|
|**Custom**|[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서는 `ALTER DATABASE SET QUERY_STORE` 명령 아래에 Custom 캡처 모드가 도입되었습니다. 사용하도록 설정하면, 특정 서버의 데이터 수집을 세부적으로 튜닝하기 위한 추가 쿼리 저장소 구성이 새 쿼리 저장소 캡처 정책 설정 아래에 제공됩니다.<br /><br />새 사용자 지정 설정은 내부 캡처 정책 시간 임계값 내에서 수행되는 작업을 정의합니다. 이 시간 경계 내에서 구성 가능한 조건이 평가되고, true인 조건이 있으면 쿼리 저장소에서 쿼리를 캡처할 수 있습니다. 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.|

> [!NOTE]
> 쿼리 저장소 캡처 모드를 **All**, **Auto** 또는 **Custom**으로 설정하면 커서, 저장 프로시저 내부 쿼리 및 네이티브 컴파일된 쿼리가 항상 캡처됩니다. 네이티브 컴파일된 쿼리를 캡처하려면 [sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md)를 사용하여 쿼리별 통계 수집을 사용하도록 설정합니다.

## <a name="keep-the-most-relevant-data-in-query-store"></a>쿼리 저장소에 가장 관련성이 높은 데이터 보관

관련된 데이터만 포함하도록 쿼리 저장소를 구성하면 쿼리 저장소가 지속적으로 실행되고, 기본 워크로드에 미치는 영향을 최소화하면서 뛰어난 문제 해결 경험을 제공합니다.
다음 표에서는 모범 사례를 제공합니다.

|모범 사례|설정|
|-------------------|-------------|
|보관된 기록 데이터를 제한합니다.|자동 정리를 활성화하도록 시간 기반 정책을 구성합니다.|
|관련 없는 쿼리를 필터링하여 제외합니다.|**쿼리 저장소 캡처 모드**를 **Auto**로 구성합니다.|
|최대 크기에 도달하면 관련성이 적은 쿼리를 삭제합니다.|크기 기반 정리 정책을 활성화합니다.|

## <a name="avoid-using-non-parameterized-queries"></a><a name="Parameterize"></a> 매개 변수화되지 않은 쿼리 사용 방지

필요하지 않은 경우 매개 변수가 없는 쿼리를 사용하지 않는 것이 좋습니다. 임시 분석의 경우를 예로 들 수 있습니다. 쿼리 최적화 프로그램에서 모든 고유 쿼리 텍스트에 대해 쿼리를 컴파일하도록 강제 적용하는 캐시된 계획은 재사용할 수 없습니다. 자세한 내용은 [강제 매개 변수화 사용 지침](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide)을 참조하세요.

또한 잠재적으로 서로 다른 쿼리 텍스트가 많고 결과적으로 셰이프가 비슷한 서로 다른 실행 계획이 많아져 쿼리 저장소가 갑자기 크기 할당량을 초과할 수도 있습니다. 따라서 워크로드 성능이 최적이 아닌 상태가 되고 쿼리 저장소가 읽기 전용 모드로 전환되거나 들어오는 쿼리 속도에 맞춰 데이터를 계속 삭제해야 할 수 있습니다.

다음 옵션을 살펴보세요.

- 해당하는 경우 쿼리를 매개 변수화합니다. 예를 들면 저장 프로시저 또는 sp_executesql 내부에 쿼리를 래핑합니다. 자세한 내용은 [매개 변수 및 실행 계획 재사용](../../relational-databases/query-processing-architecture-guide.md#PlanReuse)을 참조하세요.
- 워크로드에 서로 다른 쿼리 계획이 포함된 일회용 임시 일괄 처리가 많은 경우 [임시 작업을 위해 최적화](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) 옵션을 사용합니다.
  - 고유 query_hash 값 수를 sys.query_store_query의 총 항목 수와 비교합니다. 비율이 1에 가까우면 임시 워크로드에서 다른 쿼리를 생성합니다.
- 서로 다른 쿼리 계획 수가 많지 않으면 데이터베이스 또는 쿼리의 하위 집합에 대해 [강제 매개 변수화](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)를 적용합니다.
  - 선택한 쿼리에 대해서만 매개 변수화를 강제로 적용하려면 [계획 지침](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)을 사용합니다.
  - 워크로드에 서로 다른 쿼리 계획 수가 적으면 [매개 변수화 데이터베이스 옵션](../../relational-databases/databases/database-properties-options-page.md#miscellaneous)을 사용하여 강제 매개 변수화를 구성합니다. 예를 들어 고유 query_hash 수와 sys.query_store_query의 총 항목 수 비율이 1보다 훨씬 작은 경우가 여기에 해당합니다.
- QUERY_CAPTURE_MODE를 AUTO로 설정하여 리소스 사용이 작은 임시 쿼리를 자동으로 필터링하여 제외합니다.

## <a name="avoid-a-drop-and-create-pattern-for-containing-objects"></a><a name="Drop"></a> 포함하는 개체에 대해 DROP 및 CREATE 패턴 방지

쿼리 저장소는 포함하는 개체(예: 저장 프로시저, 함수 및 트리거)에 쿼리 항목을 연결합니다. 포함하는 개체를 다시 만드는 경우, 동일한 쿼리 텍스트에 대해 새 쿼리 항목이 생성됩니다. 이 때문에 시간에 따른 해당 쿼리의 성능 통계 추적과 계획 강제 적용 메커니즘을 사용할 수 없게 됩니다. 이러한 상황을 방지하려면 `ALTER <object>` 프로세스를 사용하여 가능할 때마다 포함하는 개체 정의를 변경합니다.

## <a name="check-the-status-of-forced-plans-regularly"></a><a name="CheckForced"></a> 강제 계획의 상태를 정기적으로 확인

강제 계획은 중요한 쿼리 성능을 수정하고 쿼리를 좀 더 예측 가능하게 하는 편리한 메커니즘입니다. 그러나 계획 힌트 및 계획 지침과 마찬가지로, 계획을 강제 적용한다고 쿼리가 이후 실행에 사용된다는 보장은 없습니다. 일반적으로 실행 계획에서 참조하는 개체가 변경되거나 삭제되는 방식으로 데이터베이스 스키마가 변경되면 계획 강제 적용이 실패하기 시작합니다. 이 경우 실제 강제 실패 이유가 [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)에 표시되는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 쿼리 재컴파일로 대체합니다. 다음 쿼리는 강제 계획에 대한 정보를 반환합니다.

```sql
USE [QueryStoreDB];
GO

SELECT p.plan_id, p.query_id, q.object_id as containing_object_id,
    force_failure_count, last_force_failure_reason_desc
FROM sys.query_store_plan AS p
JOIN sys.query_store_query AS q on p.query_id = q.query_id
WHERE is_forced_plan = 1;
```

전체 이유 목록은 [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)을 참조하세요. **query_store_plan_forcing_failed** XEvent를 사용하여 플랜 강제 오류를 추적하고 문제를 해결할 수 있습니다.

## <a name="avoid-renaming-databases-for-queries-with-forced-plans"></a><a name="Renaming"></a> 강제 계획이 포함된 쿼리의 경우 데이터베이스 이름 변경 방지

실행 계획에서는 `database.schema.object`와 같이 세 부분으로 이루어진 이름을 사용하여 개체를 참조합니다.

데이터베이스의 이름을 바꾸면 계획 강제 적용에 실패하여 모든 후속 쿼리 실행 시 다시 컴파일됩니다.

## <a name="using-query-store-in-mission-critical-servers"></a><a name="Recovery"></a> 중요 업무용 서버에서 쿼리 저장소 사용

전역 추적 플래그 7745 및 7752를 사용하여 쿼리 저장소를 통해 데이터베이스의 가용성을 개선할 수 있습니다. 자세한 내용은 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.

- 추적 플래그 7745는 쿼리 저장소에서 데이터를 디스크에 기록해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 종료할 수 있는 기본 동작을 방지합니다. 따라서 수집되었으나 아직 디스크에 유지되지 않은 쿼리 저장소 데이터가 `DATA_FLUSH_INTERVAL_SECONDS`로 정의된 기간까지 손실됩니다.
- 추적 플래그 7752는 쿼리 저장소의 비동기 로드를 사용하도록 설정합니다. 이 설정을 통해 쿼리 저장소가 완전히 복구되기 전에 데이터베이스가 온라인 상태로 전환되고 쿼리를 실행할 수 있습니다. 기본 동작은 쿼리 저장소의 비동기 로드 실행입니다. 이 기본 동작은 쿼리 저장소가 복구되기 전에 쿼리가 실행되지 않도록 방지할 뿐 아니라 데이터 수집에서 쿼리가 누락되지 않도록 방지합니다.

> [!NOTE]
> [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 이 동작은 엔진에서 제어되며, 7752 추적 플래그가 적용되지 않습니다.

> [!IMPORTANT]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 Just-In-Time 워크로드 인사이트를 위해 쿼리 저장소를 사용하는 경우, 최대한 빨리 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU2([KB 4340759](https://support.microsoft.com/help/4340759))의 성능 확장성 기능 향상을 설치하세요. 이러한 기능 향상이 없으면 데이터베이스의 작업량이 많을 때 스핀 잠금 경합이 발생할 수 있으며 서버 성능이 저하될 수 있습니다. 특히 `QUERY_STORE_ASYNC_PERSIST` 스핀 잠금 또는 `SPL_QUERY_STORE_STATS_COOKIE_CACHE` 스핀 잠금에 상당한 경합이 발생할 수 있습니다. 이러한 기능 향상이 적용되면 쿼리 저장소에서 더 이상 스핀 잠금 경합이 발생하지 않습니다.

> [!IMPORTANT]
> [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]에서 Just-In-Time 워크로드 인사이트를 위해 쿼리 저장소를 사용하는 경우, 최대한 빨리 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU22의 성능 확장성 기능 향상을 설치하세요. 이러한 기능 향상을 사용하지 않으면 데이터베이스의 사용량이 많은 경우에는 쿼리 저장소에서 많은 양의 메모리를 사용할 수 있으며 서버 성능이 저하될 수 있습니다. 이러한 기능 향상이 적용되면 쿼리 저장소의 다양한 구성 요소에서 사용할 수 있는 메모리 양에 대한 내부 제한을 적용하고 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]에 충분한 메모리가 반환될 때까지 자동으로 작업 모드를 읽기 전용으로 전환할 수 있습니다. 쿼리 저장소 내부 메모리 제한은 변경될 수 있으므로 문서화되지 않습니다.  

## <a name="see-also"></a>참고 항목

- [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)
- [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)
- [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)
- [메모리 내 OLTP와 쿼리 저장소 사용](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)
- [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)
