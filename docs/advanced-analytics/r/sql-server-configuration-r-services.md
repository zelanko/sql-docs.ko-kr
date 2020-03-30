---
title: R 사용을 위한 구성
description: 이 문서에서는 SQL Server R Services 실행을 위해 사용되는 컴퓨터의 하드웨어 및 네트워크 구성에 대한 지침을 제공합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7d18661fadb12167fd0a443758cced1188401750
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727337"
---
# <a name="sql-server-configuration-for-use-with-r"></a>R 사용을 위한 SQL Server 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서는 두 가지 사례 연구를 기준으로 R 서비스를 위한 성능 최적화를 기술하는 시리즈의 두 번째 문서입니다.  이 문서에서는 SQL Server R Services 실행을 위해 사용되는 컴퓨터의 하드웨어 및 네트워크 구성에 대한 지침을 제공합니다. 또한 솔루션에 사용되는 SQL Server 인스턴스, 데이터베이스 또는 테이블을 구성하기 위한 방법에 대한 정보도 포함되어 있습니다. SQL Server에서 NUMA를 사용하면 하드웨어 및 데이터베이스 최적화 간의 경계가 흐려지기 때문에 세 번째 섹션에서는 CPU affinitization 및 리소스 거버넌스에 대해 자세히 설명합니다.

> [!TIP]
> SQL Server에 익숙치 않으면 SQL Server 성능 튜닝 가이드도 살펴보는 것이 좋습니다. [성능 모니터링 및 튜닝](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>하드웨어 최적화

서버 컴퓨터 최적화는 외부 스크립트 실행을 위한 리소스를 확보하는 데 있어서 중요한 영향을 줍니다. 리소스가 제한된 경우 다음과 같은 증상이 나타날 수 있습니다.

- 다른 데이터베이스 작업을 우선 처리하기 위해 작업 실행이 지연되거나 취소됩니다.
- "할당량 초과" 오류가 발생하여 R 스크립트가 완료되지 않고 종료됩니다.
- 데이터가 R 메모리에 잘린 상태로 로드되어 결과가 불완전합니다.

### <a name="memory"></a>메모리

컴퓨터에서 사용 가능한 메모리 양은 고급 분석 알고리즘의 성능에 큰 영향을 미칠 수 있습니다. 메모리가 부족하면 SQL 컴퓨팅 컨텍스트를 사용할 경우 병렬 처리 정도에 영향을 미칠 수 있습니다. 처리할 수 있는 청크 크기 및 지원할 수 있는 동시 세션 수에도 영향을 미칠 수 있습니다.

최소 32GB가 권장됩니다. 32GB 이상 사용할 수 있는 경우 모든 읽기 작업에서 더 많은 행을 사용하여 성능을 향상하도록 SQL 데이터 원본을 구성할 수 있습니다.

또한 인스턴스에 사용되는 메모리도 관리할 수 있습니다. 기본적으로 SQL Server는 메모리가 할당될 때 다른 외부 스크립트 프로세스보다 우선 적용됩니다. R Services의 기본 설치에서는 사용 가능한 메모리 중 20%만 R에 할당됩니다.

일반적으로 데이터 과학 작업에는 이것만으로 충분하지 않지만 SQL Server의 메모리까지 부족해서는 안 됩니다. 최적 구성은 사례에 따라 달라진다는 이해와 함께 데이터베이스 엔진, 관련 서비스 및 외부 스크립트 사이에 메모리 할당을 실험하고 미세 조정해야 합니다.

다시 시작 일치 모델의 경우 외부 스크립트 사용이 심하고, 실행되는 다른 데이터베이스 엔진 서비스가 없습니다. 따라서 외부 스크립트에 할당되는 리소스가 스크립트 성능의 최적 구성인 70%로 증가했습니다.

### <a name="power-options"></a>전원 옵션

Windows 운영 체제에서는 **고성능** 전원 옵션을 사용해야 합니다. 다른 전원 설정을 사용하면 SQL Server를 사용할 경우 성능이 저하되거나 일관되지 않을 수 있습니다.

### <a name="disk-io"></a>디스크 IO

R Services를 사용한 학습 및 예측 작업은 기본적으로 IO에 바인딩되고 데이터베이스가 저장된 디스크의 속도에 따라 달라집니다. SSD(Solid State Drives)와 같은 더 빠른 드라이브가 도움이 될 수 있습니다.

디스크 IO는 디스크에 액세스하는 다른 애플리케이션의 영향도 받습니다(예: 다른 클라이언트에 의한 데이터베이스 읽기 작업). 디스크 IO 성능은 사용 중인 파일 시스템에 대한 설정의 영향을 받을 수도 있습니다(예: 파일 시스템에서 사용되는 블록 크기).

여러 드라이브를 사용할 수 있으면 데이터베이스 엔진에 대한 요청이 데이터베이스에 저장된 데이터에 대한 요청과 같은 디스크에 대해 실행되지 않도록 데이터베이스를 SQL Server와는 다른 드라이브에 저장하세요.

교육 중에 여러 반복을 사용하는 RevoScaleR analytic 함수를 실행 중인 경우 디스크 IO가 성능에 큰 영향을 미칠 수도 있습니다. 예를 들어 `rxLogit`, `rxDTree`, `rxDForest` 및 `rxBTrees`는 모두 여러 반복을 사용합니다. 데이터 원본이 SQL Server이면 이러한 알고리즘에는 데이터 캡처에 최적화된 임시 파일이 사용됩니다. 이러한 파일은 세션이 완료된 후 자동으로 정리됩니다. 읽기/쓰기 작업용 고성능 디스크가 있는 경우 이러한 알고리즘에 대한 전체 경과 시간이 크게 향상될 수 있습니다.

> [!NOTE]
> 이전 버전의 R Services는 Windows 운영 체제의 8.3 파일 이름 지원이 필요했습니다. 이러한 제한은 서비스 팩 1 이후에 사라졌습니다. 하지만 fsutil.exe를 사용하여 드라이브가 8.3 파일 이름을 지원하는지 확인하거나 지원하지 않는 경우 지원을 사용하도록 설정할 수 있습니다.

### <a name="paging-file"></a>페이징 파일

Windows 운영 체제에서는 페이징 파일을 사용하여 크래시 덤프를 관리하고 가상 메모리 페이지를 저장합니다. 과도한 페이징이 발견되면 컴퓨터에서 실제 메모리를 늘리는 것이 좋습니다. 실제 메모리를 추가해도 페이징은 제거되지 않지만 페이징의 필요성이 감소합니다.

페이지 파일이 저장된 디스크의 속도가 성능에 영향을 미칠 수도 있습니다. 페이지 파일을 SSD에 저장하거나 여러 SSD에 걸쳐 여러 페이지 파일을 사용하면 성능이 향상될 수 있습니다.

페이지 파일 크기 조정에 대한 자세한 내용은 [Windows 64비트 버전에 적절한 페이지 파일 크기를 결정하는 방법](https://support.microsoft.com/kb/2860880)을 참조하세요.

## <a name="optimizations-at-instance-or-database-level"></a>인스턴스 또는 데이터베이스 수준의 최적화

SQL Server 인스턴스 최적화는 효율적인 외부 스크립트 실행을 위한 핵심입니다.

> [!NOTE]
> 최적 설정은 모델 채점 또는 학습을 위해 사용되는 열 수 및 데이터 크기와 유형에 따라 달라집니다.
> 
> 특정 최적화의 결과는 최종 문서에서 검토할 수 있습니다. [성능 조정 - 사례 연구 결과](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> 샘플 스크립트는 개별 [GitHub 리포지토리](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)를 참조하세요.

### <a name="table-compression"></a>테이블 압축

IO 성능은 종종 압축 또는 칼럼 형식 데이터 저장소를 사용하여 향상될 수 있습니다. 일반적으로 데이터는 테이블 내의 여러 열에서 반복되므로 columnstore를 사용하면 데이터를 압축할 때 이러한 반복이 도움이 됩니다.

columnstore는 테이블에 대한 삽입이 많을 경우 비효율적일 수 있지만 데이터가 정적이거나 자주 변경되지 않는 경우에는 좋은 선택입니다. 열 형식 저장소가 적절하지 않은 경우 행 우선 테이블에서 압축을 사용하면 IO 성능이 향상될 수 있습니다.

자세한 내용은 다음 문서를 참조하세요.

+ [데이터 압축](../../relational-databases/data-compression/data-compression.md)

+ [테이블 또는 인덱스에 압축 사용](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Columnstore 인덱스 가이드](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>메모리 최적화 테이블

요즘의 현대식 컴퓨터에서는 메모리가 더 이상 문제가 되지 않습니다. 하드웨어 사양이 계속 발전되고 있기 때문에 비교적 쉽게 적절한 가격으로 RAM을 갖출 수 있습니다. 하지만 동시에 데이터도 이전보다 훨씬 빠르게 생성되며, 데이터를 처리할 때의 대기 시간이 짧아야 합니다.

메모리 최적화 테이블은 빅 데이터 문제 해결을 위해 고급 컴퓨터에서 제공되는 대용량 메모리를 활용한다는 점에서 한 가지 해결책을 제시합니다. 메모리 최적화 테이블은 주로 메모리에 상주하기 때문에 데이터가 메모리에서 읽고 쓰여집니다. 내구성을 위해 테이블의 두 번째 복사본이 디스크에 유지 관리되고, 데이터베이스 복구 중에만 디스크에서 데이터가 읽혀집니다.

테이블에서 데이터를 자주 읽고 써야 할 경우에는 확장성이 높고 대기 시간이 낮은 메모리 최적화 테이블이 도움이 될 수 있습니다.  다시 시작 일치 시나리오에서는 새로운 작업 개설과 일치하도록 메모리 최적화 테이블을 사용하여 데이터베이스에서 모든 다시 시작 기능을 읽고 이를 주로 메모리에 저장할 수 있었습니다. 그 결과 디스크 IO가 크게 줄어 들었습니다.

또한 여러 동시 일괄 처리에서 데이터베이스로 다시 예측을 기록하는 프로세스에서 메모리 최적화 테이블을 사용하여 추가적인 성능 이점도 얻을 수 있었습니다. SQL Server에서 메모리 최적화 테이블을 사용하여 테이블 읽기 및 쓰기에서의 대기 시간이 낮아졌습니다.

이러한 환경은 개발 중에도 원활하게 작동했습니다. 지속형 메모리 최적화 테이블은 데이터베이스가 생성될 때와 동일한 시간에 생성되었습니다. 따라서 데이터가 저장된 위치에 관계없이 동일한 워크플로가 개발에 사용되었습니다.

### <a name="processor"></a>프로세서

SQL Server는 컴퓨터에서 사용 가능한 코어를 사용하여 태스크를 병렬로 수행합니다. 사용 가능한 코어가 많을 수록 성능이 향상됩니다. 코어 수를 늘려도 IO 바인딩 작업에는 도움이 되지 않을 수 있지만 CPU 바인딩 알고리즘에는 코어가 많은 더 빠른 CPU가 도움이 됩니다.

서버는 일반적으로 여러 사용자에 의해 동시에 사용되므로 데이터베이스 관리자는 최대 작업 계산을 지원하는 데 필요한 최적의 코어 수를 결정해야 합니다.

### <a name="resource-governance"></a>리소스 거버넌스

Resource Governor를 지원하는 버전에서는 리소스 풀을 사용하여 특정 워크로드에 할당되는 CPU 수를 지정할 수 있습니다. 또한 특정 워크로드에 할당되는 메모리 양도 관리할 수 있습니다.

SQL Server에서 리소스 거버넌스는 SQL Server 및 R에서 사용되는 여러 리소스에 대한 모니터링 및 제어를 중앙화할 수 있게 해줍니다. 예를 들어 워크로드가 일시적으로 커지더라도 코어 서비스는 계속 실행될 수 있도록 데이터베이스 엔진에 사용 가능한 메모리의 절반을 할당할 수 있습니다.

외부 스크립트의 메모리 소비를 위한 기본값은 SQL Server 자체에 사용 가능한 총 메모리 양의 20%로 제한됩니다. 데이터베이스 서버에 의존하는 모든 작업이 장기 실행 R 작업에 의해 심각한 영향을 받지 않도록 보장하기 위해 기본적으로 이러한 제한이 적용됩니다. 하지만 이 제한은 데이터베이스 관리자가 변경할 수 있습니다. 많은 경우에 심각한 Machine Learning 워크로드를 지원하기 위해서는 이러한 20% 제한이 적절하지 않습니다.

지원되는 구성 옵션은 **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT** 및 **MAX_PROCESSES**입니다. 현재 설정을 보려면 다음 명령문을 사용하십시오. `SELECT * FROM sys.resource_governor_external_resource_pools`

-  서버가 기본적으로 R Services에 사용될 경우 MAX_CPU_PERCENT를 40% 또는 60%로 늘리는 것이 좋습니다.

-  많은 R 세션이 동시에 동일한 서버를 사용해야 하는 경우 세 가지 설정을 모두 늘려야 합니다.

할당된 리소스 값을 변경하려면 T-SQL 문을 사용합니다.

+ 이 명령문은 메모리 사용량을 40%로 설정합니다. `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 이 명령문은 세 가지 구성 가능한 값을 모두 설정합니다. `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 메모리, CPU 또는 최대 프로세스 설정을 변경한 후 설정을 즉시 적용하려면 다음 명령문을 실행합니다. `ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Soft-NUMA, 하드웨어 NUMA 및 CPU 선호도

SQL Server를 컴퓨팅 컨텍스트로 사용할 때는 경우에 따라 NUMA 및 프로세서 선호도와 관련된 설정을 튜닝하여 성능을 향상시킬 수 있습니다. 

_하드웨어 NUMA_가 포함된 시스템에는 각각 소규모 프로세서 집합으로 작동하는 2개 이상의 시스템 버스가 있습니다. 각 CPU는 일관된 방법으로 다른 그룹과 연결된 메모리에 액세스할 수 있습니다. 각 그룹을 NUMA 노드라고 합니다. 하드웨어 NUMA가 있는 경우 NUMA 대신 인터리브 메모리를 사용하도록 구성할 수 있습니다. 따라서 이 경우 Windows와 SQL Server는 이를 NUMA로 인식하지 않습니다. 

다음 쿼리를 사용하여 SQL Server에서 사용 가능한 메모리 노드 수를 찾을 수 있습니다.

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

쿼리에서 하나의 메모리 노드(노드 0)만 반환되면 하드웨어 NUMA가 없거나 해당 하드웨어가 인터리브(비-NUMA)로 구성되어 있는 것입니다. SQL Server는 또한 CPU가 4개 이하이거나 하나 이상의 노드에 CPU가 하나만 포함된 경우 하드웨어 NUMA를 무시합니다.

컴퓨터에 여러 프로세서가 있지만 하드웨어 NUMA가 없다면 [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)를 사용하여 CPU를 더 작은 그룹으로 분할할 수도 있습니다.  SQL Server 2016 및 SQL Server 2017 모두, SQL Server 서비스를 시작할 때 Soft-NUMA 기능이 자동으로 사용 설정됩니다.

Soft-NUMA가 사용 설정되면 SQL Server가 노드를 자동으로 관리하지만, 특정 워크로드를 최적화하기 위해 _소프트 선호도_를 사용하지 않도록 설정하고 Soft NUMA 노드에 대해 CPU 선호도를 수동으로 구성할 수 있습니다. 이렇게 하면 특히 리소스 거버넌스를 지원하는 SQL Server 버전을 사용할 경우 할당할 워크로드 및 노드를 더 세부적으로 제어할 수 있습니다. CPU 선호도를 지정하고 리소스 풀을 CPU 그룹에 맞게 정렬하면, 대기 시간을 줄이고, 동일한 NUMA 노드 내에서 관련 프로세스가 수행되도록 보장할 수 있습니다.

R 워크로드를 지원하도록 Soft-NUMA 및 CPU 선호도를 구성하는 전체 프로세스는 다음과 같습니다.

1. Soft-NUMA 사용 설정(가능한 경우)
2. 프로세서 선호도 정의
3. [Resource Governor](../r/resource-governance-for-r-services.md)를 사용하여 외부 프로세스를 위한 리소스 풀 만들기
4. 특정 선호도 그룹에 [워크로드 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md) 할당

샘플 코드를 포함한 자세한 내용은 다음 자습서를 참조하세요. [SQL 최적화 팁과 힌트(Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**기타 리소스:**

+ [SQL Server의 Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    CPU에 Soft-NUMA 노드 매핑 방법

## <a name="task-specific-optimizations"></a>작업 관련 최적화

이 섹션에서는 특정 Machine Learning 워크로드를 최적화하기 위해 이 사용 사례들 및 기타 테스트에서 채택된 방법들을 요약해서 보여줍니다. 일반적인 워크로드에는 모델 학습, 기능 추출, 기능 엔지니어링 및 단일 행, 소규모 일괄 처리 및 대규모 일괄 처리 등 채점을 위한 여러 시나리오가 포함됩니다.

### <a name="feature-engineering"></a>기능 엔지니어링

R에서 한 가지 문제는 일반적으로 단일 CPU에서 처리된다는 것입니다. 이 문제는 특히 기능 엔지니어링과 같은 여러 작업들에서 중요한 성능 병목 지점으로 나타납니다. 다시 시작 일치 솔루션에서는 기능 엔지니어링 작업 단독으로 원래 있던 100개의 기능들과 결합되어야 하는 2,500개의 제품 간 기능이 생성되었습니다. 이러한 작업은 모든 것이 단일 CPU로 수행되었을 때 상당한 시간이 소요될 것입니다.

기능 엔지니어링의 성능을 향상시키는 방법은 여러 가지가 있습니다. R 코드를 최적화하고 기능 추출을 모델링 프로세스 내에 유지하거나, 기능 엔지니어링 프로세스를 SQL로 이동할 수 있습니다.

- R 사용. 함수를 정의한 후 이를 학습 중 [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform)에 대한 인수로 전달합니다. 모델에서 병렬 처리가 지원될 경우에는 여러 CPU를 사용해서 기능 엔지니어링 작업을 처리할 수 있습니다. 이 방법을 통해 데이터 과학 팀은 채점 시간 측면에서 16% 성능 향상을 관찰했습니다. 하지만 이 방법을 위해서는 병렬화를 지원하는 모델과 병렬 계획을 사용해서 실행될 수 있는 쿼리가 필요합니다.

- SQL 컴퓨팅 컨텍스트에서 R 사용. 개별 일괄 처리 실행을 위해 격리된 리소스가 제공되는 다중 프로세서 환경에서는 테이블에서 데이터를 추출하고 동일한 워크로드 그룹으로 데이터를 제한하기 위해 각 일괄 처리에 사용되는 SQL 쿼리를 격리하여 효율성을 더 높일 수 있습니다. 일괄 처리를 격리시키기 위해 사용되는 방법에는 분할 방법과 개별 쿼리를 병렬로 실행하기 위한 PowerShell 사용 방법이 포함됩니다.

- 임시 병렬 실행: SQL Server 컴퓨팅 컨텍스트에서는 SQL 데이터베이스 엔진을 사용하여 병렬 실행을 강화할 수 있습니다(이 방식을 사용할 수 있고 다른 방법보다 효율적으로 확인된 경우).

- 개별 기능화 프로세스에서 T-SQL 사용. SQL을 사용하여 기능 데이터를 미리 계산하는 것이 일반적으로 더 빠릅니다.

### <a name="prediction-scoring-in-parallel"></a>병렬 예측(채점)

SQL Server의 이점 중 하나는 매우 많은 양의 행을 병렬로 처리할 수 있다는 것입니다. 이 기능은 특히 채점 측면에서 가장 강력한 이점입니다. 일반적으로 모델은 채점을 위해 모든 데이터에 액세스할 필요가 없기 때문에, 입력 데이터를 분할하고 각 워크로드 그룹이 하나의 작업을 처리하도록 할 수 있습니다.

또한 입력 데이터를 단일 쿼리로 보내면 SQL Server가 쿼리를 분석합니다. 입력 데이터에 대해 병렬 쿼리 계획을 만들 수 있으면 노드에 할당되는 데이터를 자동으로 분할하고 필요한 조인 및 집계를 병렬로 수행합니다.

채점에 사용하기 위한 저장 프로시저를 정의하는 방법에 대해 자세히 알고 싶으면 [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR)에서 샘플 프로젝트를 참조하고 "step5_score_for_matching.sql" 파일을 검색하십시오. 샘플 스크립트는 또한 성능을 평가할 수 있도록 쿼리 시작 및 종료 시간을 추적하고 이 시간을 SQL 콘솔에 기록합니다.

### <a name="concurrent-scoring-using-resource-groups"></a>리소스 그룹을 사용한 동시 채점

채점 문제를 확대하기 위한 좋은 방법은 수백만 개의 항목이 여러 일괄 처리로 분할되는 맵 감소 방식을 채택하는 것입니다. 그런 후 여러 채점 작업이 동시에 실행됩니다. 이 프레임워크에서 일괄 처리는 여러 CPU 집합에서 처리되고 결과가 수집되어 데이터베이스에 다시 기록됩니다.

이 방법은 다시 시작 일치 시나리오에 사용된 방법이지만, 이 방법을 구현하기 위해서는 SQL Server에서의 리소스 거버넌스가 필수적입니다. 외부 스크립트 작업을 위한 워크로드 그룹을 설정하여 R 채점 작업을 다른 프로세서 그룹으로 라우팅하고 더 빠른 처리 결과를 얻을 수 있습니다.

리소스 거버넌스는 워크로드 경합을 최소화하기 위해 서버에서 사용 가능한 리소스(CPU 및 메모리)를 분할하여 할당하는 데에도 도움을 줄 수 있습니다. 여러 R 작업 유형을 구분하기 위한 분류자 기능을 설정할 수 있습니다. 예를 들어 애플리케이션에서 호출된 채점이 항상 우선 적용되고 재학습 작업이 낮은 우선 순위를 갖도록 결정할 수 있습니다. 이러한 리소스 격리는 잠재적으로 실행 시간을 향상시킬 수 있으며, 보다 예측 가능한 성능을 제공할 수 있습니다.

### <a name="concurrent-scoring-using-powershell"></a>PowerShell을 사용한 동시 채점

데이터를 직접 분할하기로 결정한 경우에는 PowerShell 스크립트를 사용하여 여러 동시 채점 작업을 실행할 수 있습니다. 이를 위해서는 Invoke-SqlCmd cmdlet을 사용하고 채점 작업을 병렬로 시작합니다.

다시 시작 일치 시나리오에서 동시성은 다음과 같이 설계되었습니다.

- 20개의 프로세서가 각각 5개의 CPU 그룹으로 분할되어 있습니다. 각 CPU 그룹은 동일한 NUMA 노드에 배치되어 있습니다.

- 동시 일괄 처리의 최대 개수는 8개로 설정되었습니다.

- 각 작업 그룹은 두 개의 채점 작업을 처리해야 합니다. 한 작업의 데이터 읽기가 완료되고, 채점이 시작되는 즉시, 다른 작업이 데이터베이스에서 데이터 읽기를 시작할 수 있습니다.

이 시나리오의 PowerShell 스크립트를 보려면 [Github 프로젝트](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)에서 experiment.ps1 파일을 엽니다.

### <a name="storing-models-for-prediction"></a>예측을 위한 모델 저장

학습 및 평가가 완료되고 최적 모델이 선택되었으면 예측에 사용할 수 있도록 데이터베이스에 모델을 저장하는 것이 좋습니다. SQL Server Machine Learning은 R과 데이터베이스 사이에 이동할 때 특별한 serialization알고리즘을 사용하여 모델을 저장하고 로드하기 때문에 예측을 위해 데이터베이스에서 사전 계산된 모델을 로드하는 것이 효율적입니다.

> [!TIP]
> SQL Server 2017에서는 R이 서버에 설치되지 않았더라도 PREDICT 함수를 사용하여 채점을 수행할 수 있습니다. 제한된 모델 유형이 RevoScaleR 패키지로부터 지원됩니다.

하지만 사용되는 알고리즘에 따라 일부 모델은 특히 대규모 데이터 세트로 학습할 때 상당히 커질 수 있습니다. 예를 들어 **lm** 또는 **glm**과 같은 알고리즘은 규칙들과 함께 많은 요약 데이터를 생성합니다. varbinary 열에 저장할 수 있는 모델 크기에 제한이 있기 때문에 프로덕션용 데이터베이스에 모델을 저장하기 전에 모델에서 불필요한 아티팩트를 제거하는 것이 좋습니다.

## <a name="articles-in-this-series"></a>이 시리즈의 문서

[R의 성능 튜닝 - 소개](../r/sql-server-r-services-performance-tuning.md)

[R의 성능 조정 - SQL Server 구성](../r/sql-server-configuration-r-services.md)

[R의 성능 조정 - R 코드 및 데이터 최적화](../r/r-and-data-optimization-r-services.md)

[성능 조정 - 사례 연구 결과](../r/performance-case-study-r-services.md)
