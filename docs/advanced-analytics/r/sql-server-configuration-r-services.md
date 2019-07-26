---
title: SQL Server 구성(R Services)
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 88d9a5098752b0c5f0935b400c400c2ae2ff97af
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469919"
---
# <a name="sql-server-configuration-for-use-with-r"></a>R과 함께 사용 하기 위한 SQL Server 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서는 두 사례 연구를 기반으로 R 서비스에 대 한 성능 최적화를 설명 하는 시리즈의 두 번째입니다.  이 문서에서는 SQL Server R Services를 실행 하는 데 사용 되는 컴퓨터의 하드웨어 및 네트워크 구성에 대 한 지침을 제공 합니다. 또한 솔루션에서 사용 되는 SQL Server 인스턴스, 데이터베이스 또는 테이블을 구성 하는 방법에 대 한 정보도 포함 되어 있습니다. SQL Server에서 NUMA를 사용 하면 하드웨어와 데이터베이스 최적화 사이의 줄을 흐리게 하므로 세 번째 섹션에서는 CPU affinitization 및 리소스 관리에 대해 자세히 설명 합니다.

> [!TIP]
> SQL Server를 처음 접하는 경우 SQL Server 성능 조정 가이드도 검토 하는 것이 좋습니다. [성능을 모니터링 하 고 조정](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance)합니다.

## <a name="hardware-optimization"></a>하드웨어 최적화

서버 컴퓨터의 최적화는 외부 스크립트를 실행 하는 데 필요한 리소스가 있는지 확인 하는 데 중요 합니다. 리소스가 제한 되 면 다음과 같은 증상이 표시 될 수 있습니다.

- 작업 실행이 지연 되거나 취소 되어 다른 데이터베이스 작업의 우선 순위를 지정 합니다.
- "할당량을 초과 했습니다." 오류가 발생 하 여 R 스크립트가 완료 되지 않고 종료 됩니다.
- 불완전 한 결과에 대해 R 메모리로 로드 된 데이터가 잘렸습니다.

### <a name="memory"></a>메모리

컴퓨터에서 사용 가능한 메모리 양은 고급 분석 알고리즘의 성능에 큰 영향을 미칠 수 있습니다. 메모리가 부족 하면 SQL 계산 컨텍스트를 사용할 때 병렬 처리 수준에 영향을 줄 수 있습니다. 처리할 수 있는 청크 크기 및 지원할 수 있는 동시 세션 수에도 영향을 미칠 수 있습니다.

최소 32 GB를 권장 합니다. 사용 가능한 데이터가 32 GB 보다 많은 경우 모든 읽기 작업에서 더 많은 행을 사용 하 여 성능을 향상 시 키도 록 SQL 데이터 원본을 구성할 수 있습니다.

인스턴스에서 사용 하는 메모리를 관리할 수도 있습니다. 기본적으로 SQL Server는 메모리가 할당 될 때 외부 스크립트 프로세스 보다 우선 순위가 지정 됩니다. R Services의 기본 설치에서는 사용 가능한 메모리의 20%만 R에 할당 됩니다.

일반적으로이 작업은 데이터 과학 작업에는 부족 하지만 SQL server의 메모리를 결핍 하 고 싶지 않습니다. 최적 구성은 대/소문자에 따라 대/소문자를 변경 한다는 점을 이해 하 고 데이터베이스 엔진, 관련 서비스 및 외부 스크립트 간의 메모리 할당을 실험 하 고 미세 조정 해야 합니다.

다시 시작 일치 모델의 경우 외부 스크립트 사용이 과도 하 게 실행 되었으며 다른 데이터베이스 엔진 서비스가 실행 되 고 있지 않습니다. 따라서 외부 스크립트에 할당 된 리소스가 70%로 증가 되었습니다 .이는 스크립트 성능에 가장 적합 한 구성입니다.

### <a name="power-options"></a>전원 옵션

Windows 운영 체제에서는 **고성능** 전원 옵션을 사용 해야 합니다. 다른 전원 설정을 사용 하면 SQL Server를 사용 하는 경우 성능이 저하 되거나 일관 되지 않습니다.

### <a name="disk-io"></a>디스크 IO

R Services를 사용 하는 학습 및 예측 작업은 기본적으로 IO 바인딩되어 있으며 데이터베이스가 저장 된 디스크의 속도에 따라 달라 집니다. SSD (반도체 드라이브)와 같은 더 빠른 드라이브가 도움이 될 수 있습니다.

디스크 IO는 디스크에 액세스하는 다른 애플리케이션의 영향도 받습니다(예: 다른 클라이언트에 의한 데이터베이스 읽기 작업). 디스크 IO 성능은 사용 중인 파일 시스템에 대한 설정의 영향을 받을 수도 있습니다(예: 파일 시스템에서 사용되는 블록 크기).

여러 드라이브를 사용할 수 있는 경우 데이터베이스 엔진에 대 한 요청이 데이터베이스에 저장 된 데이터에 대 한 요청과 동일한 디스크에 도달 하지 않도록 SQL Server와 다른 드라이브에 데이터베이스를 저장 합니다.

교육 중에 여러 반복을 사용하는 RevoScaleR analytic 함수를 실행 중인 경우 디스크 IO가 성능에 큰 영향을 미칠 수도 있습니다. 예를 들어 `rxLogit`, `rxDTree`, `rxDForest` 및`rxBTrees` 는 모두 여러 반복을 사용 합니다. 데이터 원본이 SQL Server 되는 경우 이러한 알고리즘은 데이터를 캡처하기 위해 최적화 된 임시 파일을 사용 합니다. 이러한 파일은 세션이 완료된 후 자동으로 정리됩니다. 읽기/쓰기 작업을 위한 고성능 디스크가 있으면 이러한 알고리즘에 대해 전반적으로 경과 된 시간을 크게 향상 시킬 수 있습니다.

> [!NOTE]
> 초기 버전의 R Services에는 Windows 운영 체제에서 파일 이름 지원이 8.3 필요 합니다. 이 제한은 서비스 팩 1 이후에 리프트 되었습니다. 그러나 cmd.exe를 사용 하 여 드라이브가 8.3 파일 이름을 지원 하는지 확인 하거나 지원 하지 않는 경우 지원을 사용 하도록 설정할 수 있습니다.

### <a name="paging-file"></a>페이징 파일

Windows 운영 체제에서는 페이징 파일을 사용하여 크래시 덤프를 관리하고 가상 메모리 페이지를 저장합니다. 과도한 페이징이 발견되면 컴퓨터에서 실제 메모리를 늘리는 것이 좋습니다. 실제 메모리를 추가해도 페이징은 제거되지 않지만 페이징의 필요성이 감소합니다.

페이지 파일이 저장된 디스크의 속도가 성능에 영향을 미칠 수도 있습니다. 페이지 파일을 SSD에 저장하거나 여러 SSD에 걸쳐 여러 페이지 파일을 사용하면 성능이 향상될 수 있습니다.

페이지 파일의 크기를 조정 하는 방법에 대 한 자세한 내용은 [Windows의 64 비트 버전에 적절 한 페이지 파일 크기를 확인 하는 방법](https://support.microsoft.com/kb/2860880)을 참조 하세요.

## <a name="optimizations-at-instance-or-database-level"></a>인스턴스 또는 데이터베이스 수준에서 최적화

SQL Server 인스턴스의 최적화는 외부 스크립트를 효율적으로 실행 하기 위한 핵심입니다.

> [!NOTE]
> 최적의 설정은 데이터의 크기와 형식, 모델의 점수를 매기는 데 사용 하는 열 수, 모델을 학습 하는 데 사용 하는 열 수에 따라 달라 집니다.
> 
> 최종 문서에서 특정 최적화 결과를 검토할 수 있습니다. [성능 튜닝-사례 연구 결과](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> 샘플 스크립트는 별도의 [GitHub 리포지토리](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)를 참조 하세요.

### <a name="table-compression"></a>테이블 압축

IO 성능은 종종 압축 또는 칼럼 형식 데이터 저장소를 사용 하 여 향상 시킬 수 있습니다. 일반적으로 데이터는 테이블 내의 여러 열에서 반복 되므로 columnstore를 사용 하면 데이터를 압축할 때 이러한 반복이 수행 됩니다.

테이블에 많은 삽입 내용이 있는 경우 columnstore가 효율적이 지 않을 수 있지만 데이터가 정적 이거나 자주 변경 되지 않는 경우에는이 옵션을 선택 하는 것이 좋습니다. 열 형식 저장소가 적절하지 않은 경우 행 우선 테이블에서 압축을 사용하면 IO 성능이 향상될 수 있습니다.

자세한 내용은 다음 문서를 참조하세요.

+ [데이터 압축](../../relational-databases/data-compression/data-compression.md)

+ [테이블 또는 인덱스에 압축 사용](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Columnstore 인덱스 가이드](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블

오늘날, 메모리는 더 이상 최신 컴퓨터에 문제가 되지 않습니다. 하드웨어 사양은 계속 개선 되 면 적절 한 값으로 RAM을 얻는 것은 비교적 쉽습니다. 그러나 동시에 데이터는 이전 보다 더 빠르게 생성 되며 데이터는 짧은 대기 시간으로 처리 되어야 합니다.

메모리 액세스에 최적화 된 테이블은 고급 컴퓨터에서 사용할 수 있는 큰 메모리를 활용 하 여 빅 데이터의 문제를 처리할 수 있는 솔루션 하나를 나타냅니다. 메모리 액세스에 최적화 된 테이블은 메모리에 상주 하므로 메모리에서 데이터를 읽고 쓸 수 있습니다. 내구성의 경우 테이블의 두 번째 복사본은 디스크에서 유지 관리 되 고 데이터는 데이터베이스 복구 중에만 디스크에서 읽습니다.

테이블에서 읽기 및 쓰기를 자주 수행 해야 하는 경우 메모리 최적화 테이블은 높은 확장성 및 짧은 대기 시간으로 지원할 수 있습니다.  다시 시작 일치 시나리오에서는 메모리 최적화 테이블을 사용 하 여 데이터베이스에서 모든 이력서 기능을 읽은 후 주 메모리에 저장 하 여 새 작업을 시작할 수 있었습니다. 이로 인해 디스크 IO가 크게 줄어듭니다.

여러 동시 일괄 처리에서 데이터베이스에 대 한 예측을 다시 작성 하는 프로세스에서 메모리 최적화 테이블을 사용 하 여 추가 성능을 향상 시킬 수 있습니다. SQL Server에서 메모리 최적화 테이블을 사용 하면 테이블 읽기 및 쓰기에 짧은 대기 시간이 사용 됩니다.

개발 중에도 원활한 환경을 제공 합니다. 지속형 메모리 최적화 테이블은 데이터베이스를 만들 때 생성 됩니다. 따라서 개발은 데이터 저장 위치에 관계 없이 동일한 워크플로를 사용 했습니다.

### <a name="processor"></a>프로세서

SQL Server은 컴퓨터에서 사용 가능한 코어를 사용 하 여 작업을 병렬로 수행할 수 있습니다. 더 많은 코어가 제공 되므로 성능이 향상 됩니다. 코어 수를 늘릴 경우 IO 바인딩 작업에 도움이 되지 않을 수 있지만 CPU 바인딩 알고리즘은 많은 코어를 사용 하는 더 빠른 Cpu를 활용 합니다.

서버는 일반적으로 여러 사용자가 동시에 사용 하므로 데이터베이스 관리자는 최고 워크 로드 계산을 지 원하는 데 필요한 이상적인 코어 수를 결정 해야 합니다.

### <a name="resource-governance"></a>리소스 관리

Resource Governor를 지 원하는 버전에서 리소스 풀을 사용 하 여 특정 워크 로드에 몇 개의 Cpu를 할당 하도록 지정할 수 있습니다. 특정 작업에 할당 된 메모리 양을 관리할 수도 있습니다.

SQL Server의 리소스 관리를 통해 SQL Server 및 R에서 사용 되는 다양 한 리소스에 대 한 모니터링 및 제어를 중앙 집중화할 수 있습니다. 예를 들어 데이터베이스 엔진에 대 한 사용 가능한 메모리의 절반을 할당 하 여 코어 서비스가 일시적으로 과도 한 워크 로드에도 불구 하 고 항상 실행 되도록 할 수 있습니다.

외부 스크립트의 메모리 소비량에 대 한 기본값은 SQL Server 자체에 사용할 수 있는 총 메모리의 20%로 제한 됩니다. 이 제한은 데이터베이스 서버를 사용 하는 모든 태스크가 장기 실행 R 작업의 심각한 영향을 받지 않도록 기본적으로 적용 됩니다. 하지만 이 제한은 데이터베이스 관리자가 변경할 수 있습니다. 대부분의 경우 20% 제한은 심각한 기계 학습 워크 로드를 지원 하기에 적합 하지 않습니다.

지원 되는 구성 옵션은 **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT**및 **MAX_PROCESSES**입니다. 현재 설정을 보려면 다음 문을 사용 합니다.`SELECT * FROM sys.resource_governor_external_resource_pools`

-  서버가 주로 R Services에 사용 되는 경우 MAX_CPU_PERCENT를 40% 또는 60%로 늘리는 것이 유용할 수 있습니다.

-  여러 R 세션이 동시에 동일한 서버를 사용 해야 하는 경우 세 가지 설정을 모두 늘려야 합니다.

할당 된 리소스 값을 변경 하려면 T-sql 문을 사용 합니다.

+ 이 문은 메모리 사용량을 40%로 설정 합니다.`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 이 문은 세 가지 구성 가능한 값을 모두 설정 합니다.`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 메모리, CPU 또는 최대 프로세스 설정을 변경한 다음 설정을 즉시 적용 하려면 다음 문을 실행 합니다.`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>소프트 NUMA, 하드웨어 NUMA 및 CPU 선호도

SQL Server를 계산 컨텍스트로 사용 하는 경우 NUMA 및 프로세서 선호도와 관련 된 설정을 조정 하 여 성능을 향상 시킬 수 있습니다. 

_하드웨어 NUMA_ 를 사용 하는 시스템에는 작은 프로세서 집합을 처리 하는 시스템 버스가 둘 이상 있습니다. 각 CPU는 일관 된 방식으로 다른 그룹과 연결 된 메모리에 액세스할 수 있습니다. 각 그룹을 NUMA 노드라고 합니다. 하드웨어 NUMA가 있는 경우 NUMA 대신 인터리브 메모리를 사용하도록 구성할 수 있습니다. 이 경우 Windows 및 SQL Server는이를 NUMA로 인식 하지 않습니다. 

다음 쿼리를 실행 하 여 SQL Server 하는 데 사용할 수 있는 메모리 노드 수를 확인할 수 있습니다.

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

쿼리가 단일 메모리 노드 (노드 0)를 반환 하는 경우 하드웨어 NUMA가 없거나 하드웨어가 인터리브 (비-NUMA)로 구성 되어 있습니다. Cpu가 4 개 이하인 경우 또는 하나 이상의 노드에 하나의 CPU만 있는 경우에도 하드웨어 NUMA가 무시 SQL Server.

컴퓨터에 프로세서가 여러 개 있지만 하드웨어 NUMA가 없는 경우 [소프트 numa](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) 를 사용 하 여 cpu를 더 작은 그룹으로 분할할 수도 있습니다.  SQL Server 2016 및 SQL Server 2017에서 SQL Server 서비스를 시작할 때 소프트 NUMA 기능이 자동으로 설정 됩니다.

소프트 NUMA를 사용 하도록 설정 하면 SQL Server 자동으로 노드를 관리 합니다. 그러나 특정 워크 로드에 대해 최적화 하려면 _소프트 선호도_ 를 사용 하지 않도록 설정 하 고 소프트 NUMA 노드에 대해 CPU 선호도를 수동으로 구성할 수 있습니다. 이렇게 하면 특히 리소스 관리를 지 원하는 SQL Server 버전을 사용 하는 경우 해당 노드에 할당 되는 워크 로드를 더 효과적으로 제어할 수 있습니다. CPU 선호도를 지정 하 고 Cpu 그룹을 사용 하 여 리소스 풀을 정렬 하면 대기 시간을 줄이고 관련 프로세스가 동일한 NUMA 노드 내에서 수행 되도록 할 수 있습니다.

R 워크 로드를 지원 하기 위해 소프트 NUMA 및 CPU 선호도를 구성 하는 전체 프로세스는 다음과 같습니다.

1. 소프트 NUMA를 사용 하도록 설정 합니다 (사용 가능한 경우).
2. 프로세서 선호도 정의
3. [Resource Governor](../r/resource-governance-for-r-services.md) 를 사용 하 여 외부 프로세스에 대 한 리소스 풀 만들기
4. 특정 선호도 그룹에 [작업 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md) 할당

샘플 코드를 비롯 한 자세한 내용은이 자습서를 참조 하세요. [SQL 최적화 팁과 요령 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**기타 리소스:**

+ [SQL Server의 소프트 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    소프트 NUMA 노드를 Cpu에 매핑하는 방법

## <a name="task-specific-optimizations"></a>작업 관련 최적화

이 섹션에서는 특정 기계 학습 작업을 최적화 하기 위해 이러한 사례 연구 및 다른 테스트에서 채택한 방법을 요약 합니다. 일반적인 작업으로는 모델 학습, 기능 추출 및 기능 엔지니어링, 점수 매기기를 위한 다양 한 시나리오 (단일 행, 작은 일괄 처리 및 대량 배치)가 있습니다.

### <a name="feature-engineering"></a>기능 엔지니어링

R을 사용 하는 한 가지 어려움은 일반적으로 단일 CPU에서 처리 된다는 점입니다. 이는 많은 작업, 특히 기능 엔지니어링에 대 한 주요 성능 병목 현상입니다. 다시 시작 일치 솔루션에서 기능 엔지니어링 작업 만으로는 원래 100 기능과 결합 되어야 하는 2500 제품 간 기능을 만들었습니다. 단일 CPU에서 모든 작업을 수행 하는 경우이 작업은 상당한 시간이 소요 됩니다.

기능 엔지니어링의 성능을 향상 시키는 방법에는 여러 가지가 있습니다. 모델링 프로세스 내에서 R 코드를 최적화 하 고 기능 추출을 유지 하거나 기능 엔지니어링 프로세스를 SQL로 이동할 수 있습니다.

- R 사용. 함수를 정의한 다음 학습 중에 [Rxtransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) 에 인수로 전달 합니다. 모델에서 병렬 처리를 지 원하는 경우 여러 Cpu를 사용 하 여 기능 엔지니어링 작업을 처리할 수 있습니다. 이 접근 방식을 사용 하 여 데이터 과학 팀은 점수 매기기 시간 측면에서 16% 성능 향상을 관찰 했습니다. 그러나이 방법에는 병렬 계획을 사용 하 여 실행할 수 있는 쿼리 및 병렬화를 지 원하는 모델이 필요 합니다.

- SQL 계산 컨텍스트를 사용 하 여 R을 사용 합니다. 개별 일괄 처리를 실행 하는 데 사용할 수 있는 격리 된 리소스를 포함 하는 다중 프로세서 환경에서는 각 일괄 처리에 사용 되는 SQL 쿼리를 분리 하 여 테이블에서 데이터를 추출 하 고 동일한 작업 그룹에서 데이터를 제한 하 여 효율성을 높일 수 있습니다. 일괄 처리를 격리 하는 데 사용 되는 방법에는 분할이 포함 되며 PowerShell을 사용 하 여 별도 쿼리를 병렬로 실행 합니다.

- 임시 병렬 실행: SQL Server 계산 컨텍스트에서는 SQL database 엔진을 사용 하 여 가능한 경우 병렬 실행을 적용 하 고, 해당 옵션이 더 효율적으로 검색 될 수 있습니다.

- 별도의 기능화 프로세스에서 T-sql을 사용 합니다. SQL을 사용한 기능 데이터 Precomputing 일반적으로 더 빠릅니다.

### <a name="prediction-scoring-in-parallel"></a>예측 (점수 매기기) 병렬

SQL Server의 이점 중 하나는 대량의 행을 병렬로 처리할 수 있다는 것입니다. 이러한 이점이 있으므로 점수 매기기로 표시 됩니다. 일반적으로 모델은 점수 매기기를 위해 모든 데이터에 액세스할 필요가 없으므로 입력 데이터를 분할 하 고 각 작업 그룹에서 하나의 작업을 처리할 수 있습니다.

또한 입력 데이터를 단일 쿼리로 보내고 SQL Server 다음 쿼리를 분석할 수 있습니다. 입력 데이터에 대해 병렬 쿼리 계획을 만들 수 있는 경우에는 노드에 할당 된 데이터를 자동으로 분할 하 고 필요한 조인과 집계도 병렬로 수행 합니다.

점수 매기기에 사용 하기 위해 저장 프로시저를 정의 하는 방법에 대 한 자세한 내용은 [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) 의 샘플 프로젝트를 참조 하 고 "step5_score_for_matching" 파일을 찾습니다. 또한이 샘플 스크립트는 쿼리 시작 및 종료 시간을 추적 하 고 성능을 평가할 수 있도록 시간을 SQL 콘솔에 기록 합니다.

### <a name="concurrent-scoring-using-resource-groups"></a>리소스 그룹을 사용 하 여 동시 점수 매기기

점수 매기기 문제를 강화 하려면 수백만 개의 항목이 여러 일괄 처리로 분할 되는 맵 감소 방식을 채택 하는 것이 좋습니다. 그러면 여러 점수 매기기 작업이 동시에 실행 됩니다. 이 프레임 워크에서는 여러 CPU 집합에서 일괄 처리를 처리 하 고 결과를 수집 하 여 데이터베이스에 다시 기록 합니다.

다시 시작 일치 시나리오에서 사용 되는 방법입니다. 그러나 SQL Server의 리소스 관리는이 방법을 구현 하는 데 필수적입니다. 외부 스크립트 작업에 대 한 작업 그룹을 설정 하 여 R 점수 매기기 작업을 다른 프로세서 그룹으로 라우팅하고 더 빠른 처리량을 달성할 수 있습니다.

리소스 관리는 서버에서 사용 가능한 리소스 (CPU 및 메모리)를 할당 하 여 워크 로드 경쟁을 최소화 하는 데도 도움이 됩니다. R 작업의 여러 유형을 구분하기 위해 분류 자 기능을 설정할 수 있습니다. 예를 들어, 재교육 작업은 우선 순위가 낮은 반면, 응용 프로그램에서 호출 된 점수는 항상 우선 순위로 결정할 수 있습니다. 이 리소스 격리는 잠재적으로 실행 시간을 개선 하 고 보다 예측 가능한 성능을 제공할 수 있습니다.

### <a name="concurrent-scoring-using-powershell"></a>PowerShell을 사용 하 여 동시 점수 매기기

데이터를 직접 분할 하기로 결정 한 경우 PowerShell 스크립트를 사용 하 여 여러 동시 점수 매기기 작업을 실행할 수 있습니다. 이렇게 하려면 SqlCmd cmdlet을 사용 하 고 점수 매기기 작업을 병렬로 시작 합니다.

다시 시작 일치 시나리오에서 동시성은 다음과 같이 설계 되었습니다.

- 20 개의 프로세서가 각각 5 개의 Cpu로 나뉘어 있습니다. 각 Cpu 그룹은 동일한 NUMA 노드에 있습니다.

- 최대 동시 일괄 처리 수가 8 개로 설정 되었습니다.

- 각 작업 그룹은 두 개의 점수 매기기 작업을 처리 해야 합니다. 한 작업에서 데이터 읽기를 완료 하 고 점수 매기기를 시작 하는 즉시 다른 태스크는 데이터베이스에서 데이터 읽기를 시작할 수 있습니다.

이 시나리오에 대 한 PowerShell 스크립트를 보려면 [Github 프로젝트](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)에서 파일 실험. p s 1을 엽니다.

### <a name="storing-models-for-prediction"></a>예측을 위한 모델 저장

학습 및 평가를 완료 하 고 최상의 모델을 선택한 경우 예측에 사용할 수 있도록 데이터베이스에 모델을 저장 하는 것이 좋습니다. SQL Server machine learning은 R과 데이터베이스 간에 이동할 때 특수 serialization 알고리즘을 사용 하 여 모델을 저장 하 고 로드 하므로 예측을 위해 데이터베이스에서 미리 계산 된 모델을 로드 하는 것이 효율적입니다.

> [!TIP]
> SQL Server 2017에서 PREDICT 함수를 사용 하 여 R이 서버에 설치 되어 있지 않은 경우에도 점수 매기기를 수행할 수 있습니다. RevoScaleR 패키지에서 제한 된 모델 유형이 지원 됩니다.

그러나 사용 하는 알고리즘에 따라 일부 모델은 매우 클 수 있으며, 특히 규모가 많은 데이터 집합에서 학습 하는 경우에는 매우 클 수 있습니다. 예를 들어 **lm** 또는 **글 m** 과 같은 알고리즘은 규칙과 함께 많은 요약 데이터를 생성 합니다. Varbinary 열에 저장할 수 있는 모델 크기에 제한이 있기 때문에 프로덕션을 위해 데이터베이스에 모델을 저장 하기 전에 모델에서 불필요 한 아티팩트를 제거 하는 것이 좋습니다.

## <a name="articles-in-this-series"></a>이 시리즈의 문서

[R에 대 한 성능 조정-소개](../r/sql-server-r-services-performance-tuning.md)

[R SQL Server 구성에 대 한 성능 조정](../r/sql-server-configuration-r-services.md)

[R의 성능 튜닝-R 코드 및 데이터 최적화](../r/r-and-data-optimization-r-services.md)

[성능 튜닝-사례 연구 결과](../r/performance-case-study-r-services.md)
