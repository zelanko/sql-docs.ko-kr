---
title: "SQL Server 구성(R Services) | Microsoft 문서"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 93c3dcf6dc4a64d116b8a660aaafa1d7a9092531
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="sql-server-configuration-for-use-with-r"></a>R로 사용 하기 위한 SQL Server 구성

이 문서는 두 번째 두 사례 연구를 기반으로 하는 R 서비스에 대 한 성능 최적화를 설명 하는 일련의 합니다.  이 문서에서는 SQL Server R Services를 실행 하는 데 사용 되는 컴퓨터의 하드웨어 및 네트워크 구성에 대 한 지침을 제공 합니다. 또한 SQL Server 인스턴스, 데이터베이스 또는 솔루션에 사용 되는 테이블을 구성 하는 방법에 대 한 정보를 포함 합니다. 하드웨어 및 데이터베이스 최적화 사이의 선에 흐리게 하는 SQL Server의 NUMA의 사용을 하기 때문에 세 번째 섹션에서는 CPU affinitization 및 리소스 관리를 자세히 설명 합니다.

> [!TIP]
> SQL Server을 처음 접하는 경우 좋습니다 SQL Server 성능 튜닝 가이드도 검토: [모니터 및 성능에 대 한 조정](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance)합니다.

## <a name="hardware-optimization"></a>하드웨어 최적화

서버 컴퓨터의 최적화는 외부 스크립트를 실행 하는 리소스 있는지 확인 하기 위한 것이 중요 합니다. 리소스가 제한 된 경우 이러한 현상이 나타날 수 있습니다.

- 작업이 실행을 지연 또는 다른 데이터베이스 작업의 우선 순위를 취소 합니다.
- 오류 "할당량이 초과 되었습니다" 바꾸지 R 스크립트를 완료 하지 않고 종료 합니다.
- 불완전 한 결과 대 한 잘리지 R 메모리에 로드 한 데이터

### <a name="memory"></a>메모리

컴퓨터에서 사용 가능한 메모리 양은 고급 분석 알고리즘의 성능에 큰 영향을 미칠 수 있습니다. 메모리가 부족 하 여 SQL 계산 컨텍스트를 사용 하는 경우 병렬 처리 수준을 영향을 줄 수 있습니다. 처리할 수 있는 청크 크기 및 지원할 수 있는 동시 세션 수에도 영향을 미칠 수 있습니다.

32GB의 최소값을 사용 하는 것이 좋습니다. 32GB 보다 많이 사용할 수 있는 경우에 성능 향상을 위해 모든 읽기 작업에 더 많은 행을 사용 하도록 SQL 데이터 원본을 구성할 수 있습니다.

인스턴스에서 사용 하는 메모리를 관리할 수 있습니다. 기본적으로 SQL Server 우선 순위를 가지도록 외부 스크립트 프로세스를 통해 메모리 할당 합니다. R Services의 기본 설치에서 사용 가능한 메모리의 20%만 오른쪽에 할당

일반적으로 아닌 데이터 과학 작업에 충분 하지만 원하지도 않을 SQL server의 메모리 고갈 합니다. 실험 하 고 데이터베이스 엔진, 관련된 서비스 및 가장 적합 한 구성 경우 달라 지는 이해를 바탕으로 외부 스크립트 간의 메모리 할당을 미세 조정 해야 합니다.

Resume 일치 하는 모델에 대 한 외부 스크립트 사용 된 많은 했 고 다른 데이터베이스 엔진 서비스 실행 따라서 외부 스크립트에 할당 된 리소스는 스크립트 성능에 대 한 최상의 구성을 이전의 70%로 증가 되었습니다.

### <a name="power-options"></a>전원 옵션

Windows 운영 체제에서의 **고성능** 전원 옵션을 사용 해야 합니다. 서로 다른 전원 설정을 사용 하 여 SQL Server를 사용 하는 경우 성능이 저하 되거나 일치 하지 않는 발생 합니다.

### <a name="disk-io"></a>디스크 IO

학습 및 R 서비스를 사용 하 여 작업은 본질적으로 IO 예측 바인딩되지 않습니다 되며 데이터베이스에 저장 되어 있는 디스크의 속도에 따라 다릅니다. SSD (반도체 드라이브)와 같은 고속 드라이브 도움이 될 수 있습니다.

디스크 IO는 디스크에 액세스하는 다른 응용 프로그램의 영향도 받습니다(예: 다른 클라이언트에 의한 데이터베이스 읽기 작업). 디스크 IO 성능은 사용 중인 파일 시스템에 대한 설정의 영향을 받을 수도 있습니다(예: 파일 시스템에서 사용되는 블록 크기).

여러 드라이브를 사용할 수 있으면 하도록 데이터베이스 엔진에 대 한 요청 하는 SQL Server와 다른 드라이브에서 데이터베이스와 동일한 디스크에 도달 하지는 저장소를 데이터베이스에 저장 된 데이터에 대 한 요청입니다.

교육 중에 여러 반복을 사용하는 RevoScaleR analytic 함수를 실행 중인 경우 디스크 IO가 성능에 큰 영향을 미칠 수도 있습니다. 예를 들어 `rxLogit`, `rxDTree`, `rxDForest`, 및 `rxBTrees` 모두 여러 반복을 사용 합니다. 데이터 원본이 SQL Server 인 경우 이러한 알고리즘 데이터를 캡처하기 위해 최적화 된 임시 파일을 사용 합니다. 이러한 파일은 세션이 완료된 후 자동으로 정리됩니다. 읽기/쓰기 작업에 대 한 고성능 디스크 것 이러한 알고리즘에 대 한 전반적인 경과 시간을 크게 향상 시킬 수 있습니다.

> [!NOTE]
> R Services의 초기 버전 Windows 운영 체제에서 8.3 파일 이름 지원이 필요합니다. 이 제한 사항은 서비스 팩 1 이후 변경 되었습니다. 그러나 드라이브 8.3 파일을 지원 하는지 여부를 결정 하거나 그렇지 않은 경우 지원을 사용 하도록 fsutil.exe을 사용할 수 있습니다.

### <a name="paging-file"></a>페이징 파일

Windows 운영 체제에서는 페이징 파일을 사용하여 크래시 덤프를 관리하고 가상 메모리 페이지를 저장합니다. 과도한 페이징이 발견되면 컴퓨터에서 실제 메모리를 늘리는 것이 좋습니다. 실제 메모리를 추가해도 페이징은 제거되지 않지만 페이징의 필요성이 감소합니다.

페이지 파일이 저장된 디스크의 속도가 성능에 영향을 미칠 수도 있습니다. 페이지 파일을 SSD에 저장하거나 여러 SSD에 걸쳐 여러 페이지 파일을 사용하면 성능이 향상될 수 있습니다.

참조 페이지 파일 크기 조정에 대 한 내용은 [64 비트 버전의 Windows에 대 한 적절 한 페이지 파일 크기를 결정 하는 방법을](https://support.microsoft.com/kb/2860880)합니다.

## <a name="optimizations-at-instance-or-database-level"></a>인스턴스 또는 데이터베이스 수준에서 최적화

SQL Server 인스턴스의 최적화에 효율적으로 실행 한 외부 스크립트의 키입니다.

> [!NOTE]
> 가장 적합 한 설정 크기 및 형식의 데이터를 모델 학습 또는 점수 매기기에 대 한 사용 하는 열의 수에 따라 다릅니다.
> 
> 마지막 문서에 특정 최적화의 결과 검토할 수 있습니다: [성능 튜닝-사례 연구 결과](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> 예제 스크립트는 별도 참조 하십시오. [GitHub 리포지토리](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)합니다.

### <a name="table-compression"></a>테이블 압축

IO 성능은 압축 또는 칼럼 형식 데이터 저장소를 사용 하 여 자주 향상 될 수 있습니다. 일반적으로 여러 열은 테이블 내에서 데이터 반복 종종 되므로 columnstore를 사용 하 여 활용 이러한 반복 데이터를 압축할 때.

Columnstore는 테이블에 대 한 다양 한 삽입 경우 효율적인 수 있지만 데이터는 정적 또는 자주 변경 되지 않는 경우이 좋은 대안입니다. 열 형식 저장소가 적절하지 않은 경우 행 우선 테이블에서 압축을 사용하면 IO 성능이 향상될 수 있습니다.

자세한 내용은 다음 문서를 참조하세요.

+ [데이터 압축](../../relational-databases/data-compression/data-compression.md)

+ [테이블이 나 인덱스에 압축 사용](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Columnstore 인덱스 가이드](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블

오늘날에 메모리는 더 이상 최신 컴퓨터에 대 한 문제입니다. 하드웨어 사양 지속적으로 개선 때 상대적으로 쉽지만 RAM 값이 적절 합니다. 그러나 같은 시간에 데이터를 그 어느 때 보다 빠르게 생산 되는 및 짧은 대기 시간으로 데이터를 처리 해야 합니다.

빅 데이터의 문제를 해결할 수 있는 고급 컴퓨터에서 사용할 수 있는 대규모 메모리를 활용 된다는 점에서 메모리 액세스에 최적화 된 테이블에서 하나의 솔루션을 나타냅니다. 메모리 액세스에 최적화 된 테이블에서 데이터는 읽고 메모리에 기록 되도록에 주로 메모리에 상주 합니다. 내구성의 경우 테이블의 보조 복사본이 디스크에서 유지 관리 됩니다 및 데이터 데이터베이스를 복구 하는 동안 디스크에서 읽기만 합니다.

읽고 테이블에 쓰기 작업을 자주 해야 할 경우 메모리 액세스에 최적화 된 테이블 높은 확장성 및 짧은 대기 시간 도움이 됩니다.  Resume 일치 하는 경우에는 메모리 액세스에 최적화 된 테이블 사용을 사용 하면 데이터베이스에서 다시 시작 하는 모든 기능을 읽고 새 작업 시작에 맞게 주 메모리에 저장할 수 있었습니다. 이 디스크 IO 상당히 줄어듭니다.

여러 동시 일괄 처리를 다시 데이터베이스에 예측을 작성할 즈음 메모리 액세스에 최적화 된 테이블을 사용 하 여 추가 성능 향상이 이루어질 되었습니다. 테이블 읽기 및 쓰기에 짧은 대기 시간을 사용 하는 SQL Server에서 메모리 액세스에 최적화 된 테이블의 사용 합니다.

환경을 개발 하는 동안 원활한 이기도 합니다. 해당 데이터베이스가 생성 하는 동시에 메모리 액세스에 최적화 된 내구성이 있는 테이블을 만들었습니다. 따라서 개발에서 데이터를 저장 하는 위치에 관계 없이 동일한 워크플로 사용 합니다.

### <a name="processor"></a>프로세서

SQL Server; 컴퓨터에서 사용 가능한 코어를 사용 하 여 병렬에서 작업을 수행할 수 있습니다. 를 사용할 수 있는 더 많은 코어 성능이 좋아집니다. 바인딩된 IO 작업에 대 한 코어의 수를 늘리면 도움이 되지 않을 수 있습니다 하는 동안 CPU에서 많은 코어와 더 빠른 Cpu 알고리즘 혜택을 바인딩됩니다.

서버는 일반적으로 사용 되는 여러 사용자가 동시에, 때문에 데이터베이스 관리자 이상적인 최대 작업 계산을 지원 해야 하는 코어 수를 결정 해야 합니다.

### <a name="resource-governance"></a>리소스 관리

리소스 관리자 지원 버전에서 특정 작업 부하 Cpu 일부 수를 할당 된 지정 하려면 리소스 풀을 사용할 수 있습니다. 또한 특정 작업에 할당 된 메모리의 양을 관리할 수 있습니다.

SQL Server에서 리소스 관리를 사용 하면 중앙 집중화 하 고 오른쪽 및 SQL Server에서 사용 하는 다양 한 리소스의 모니터링 및 제어 예를 들어 데이터베이스 엔진이 해당 핵심 서비스 일시적인 무거운 작업 부하에 관계 없이 항상 실행할 수 있는지 확인 하기 위한 사용 가능한 메모리를 절반을 할당할 수 있습니다.

외부 스크립트를 통해 메모리 사용에 대 한 기본 값 자체 SQL Server에 사용할 수 있는 총 메모리의 20%로 제한 됩니다. 데이터베이스 서버를 사용 하는 모든 작업은 심각 하 게 장기 실행 R 작업에 저하 되지 않도록 기본적으로이 제한이 적용 됩니다. 하지만 이 제한은 데이터베이스 관리자가 변경할 수 있습니다. 대부분의 경우에서 20% 제한이 심각한 시스템 작업 부하를 학습을 지원 하도록 적합 하지 않습니다.

지원 되는 구성 옵션은 **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT**, 및 **MAX_PROCESSES**합니다. 현재 설정을 보려면이 문을 사용 합니다.`SELECT * FROM sys.resource_governor_external_resource_pools`

-  R 서비스에 대 한 서버는 주로 40% 또는 60%까지 MAX_CPU_PERCENT 증가할 것이 도움이 수도 있습니다.

-  R 세션의 수를 사용 해야 경우 같은 서버 동시에 세 가지 설정이 모두 증가 되어야 합니다.

할당 된 리소스 값을 변경 하려면 T-SQL 문을 사용 합니다.

+ 이 문은 40%로 메모리 사용을 설정합니다.`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 이 문은 세 가지 구성 가능 값을 설정합니다.`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 메모리, CPU, 또는 최대 프로세스 설정을 변경 하 고 즉시 설정을 적용 하려면이 문을 실행 합니다.`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>소프트 NUMA, NUMA, 하드웨어 및 CPU 선호도

SQL Server 계산 컨텍스트를 사용할 때와 관련 된 NUMA 및 프로세서 선호도 설정을 튜닝 하 여 성능 향상을 얻는 경우도 있습니다. 

시스템과 _하드웨어 NUMA_ 둘 이상의 시스템 버스가 작은 프로세서 집합에 있어야 합니다. 각 CPU는 일관 된 방법으로 다른 그룹과 연결 된 메모리에 액세스할 수 있습니다. 각 그룹을 NUMA 노드라고 합니다. 하드웨어 NUMA가 있는 경우 NUMA 대신 인터리브 메모리를 사용하도록 구성할 수 있습니다. 이 경우 Windows 및 SQL Server는 하지 NUMA로 인식 합니다. 

SQL Server에 사용 가능한 메모리 노드의 번호를 찾으려면 다음 쿼리를 실행할 수 있습니다.

```SQL
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

쿼리에서 하나의 메모리 노드 (노드 0)을 반환 하는 경우 하드웨어 NUMA가 없는 또는 하드웨어가 인터리브 (비-NUMA)로 구성 됩니다. SQL Server에서는 하드웨어 NUMA 무시 때 없어 4 개 이하의 Cpu 노드가 하나 이상 CPU가 하나뿐인 경우입니다.

컴퓨터에 프로세서가 여러 개 있지만 하드웨어 NUMA가 없습니다를 사용할 수도 있습니다 [소프트 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) 더 작은 그룹으로 Cpu를 세분화 하 합니다.  SQL Server 2016 및 SQL Server 2017에서는 SQL Server 서비스를 시작 하는 소프트 NUMA 기능 자동으로 활성화 됩니다.

SQL Server를; 노드를 자동으로 관리 소프트 NUMA를 사용 하는 경우 그러나 특정 작업을 최적화 하려면 비활성화할 수 있습니다 _소프트 선호도_ 소프트 NUMA 노드에 대 한 CPU 선호도 수동으로 구성 하 고 있습니다. 이 수 자세히 제어할 수 있는 노드에 할당 된 작업 부하는 리소스 관리를 지 원하는 SQL Server 버전을 사용 하는 경우에 특히 합니다. CPU 선호도 지정 하 고 cpu 그룹으로 리소스 풀을 맞춤, 대기 시간을 줄일 수 있으며 관련된 프로세스 동일한 NUMA 노드 내에서 수행 되도록 수 있습니다.

소프트 NUMA 및 R 작업을 지원 하기 위해 CPU 선호도 구성 하기 위한 전체 프로세스는 다음과 같습니다.

1. 사용 가능한 경우 소프트 NUMA를 사용 하도록 설정
2. 프로세서 선호도 정의 합니다.
3. 사용 하 여 외부 프로세스에 대 한 리소스 풀을 만들 [리소스 관리자](../r/resource-governance-for-r-services.md)
4. 할당 된 [작업 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md) 특정 선호도 그룹에

자세한 내용은, 샘플 코드를 포함 하 여이 자습서를 참조 하십시오.: [SQL 최적화 팁과 요령 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**다른 리소스:**

+ [SQL Server에서 소프트 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Cpu에 소프트 NUMA 노드를 매핑하는 방법

+ [자동 SOFT-NUMA: 더 빠른 (Bob 워드) 실행](https://blogs.msdn.microsoft.com/bobsql/2016/06/03/sql-2016-it-just-runs-faster-automatic-soft-numa/)

   기록에 설명 최신 다중 코어 서버에서 성능 구현 세부 정보 뿐만 아니라 합니다.

## <a name="task-specific-optimizations"></a>태스크 별 최적화

이 섹션에는 작업 부하를 학습 하는 특정 컴퓨터를 최적화 하기 위한 다른 테스트와 이러한 사례 연구에 채택 하는 방법을 요약 합니다. 일반적인 작업에는 모델을 학습, 기능 추출 및 기능 엔지니어링 및 점수 매기기에 대 한 다양 한 시나리오: 단일 행, 작은 일괄 처리 및 큰 일괄 처리 합니다.

### <a name="feature-engineering"></a>기능 엔지니어링

R 사용 하는 하나 불만 지점이 단일 CPU에서 처리 된 일반적으로입니다. 이 많은 작업에 대 한 주요 성능 병목 현상 특히 엔지니어링 기능입니다. Resume 일치 하는 솔루션을 단독 기능 엔지니어링 작업을 다시 원래 100 기능과 함께 사용 하는 2500 제품 간 기능을 만들었습니다. 이 태스크는 단일 CPU에 수행 된 모든 경우 상당한 시간이 걸립니다.

여러 가지 방법으로 기능 엔지니어링의 성능을 향상 시킬 수 있습니다. R 코드를 최적화 하 고 기능 추출 모델링 프로세스 내부에 유지 하거나 기능 엔지니어링 프로세스 SQL로 이동 합니다.

- 오른쪽을 사용 하 여 함수를 정의 하 고 다음에 대 한 인수로 전달 [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) 학습 중입니다. 모델 병렬 처리를 지 원하는 경우에 cpu를 여러 개를 사용 하 여 기능 엔지니어링 작업을 처리할 수 있습니다. 데이터 과학 팀이이 방법을 사용 하면 시간 점수 매기기를 기준으로 16% 성능 향상을 관찰 합니다. 그러나이 방법은 병렬화 및 병렬 계획을 사용 하 여 실행할 수 있는 쿼리를 지 원하는 모델을 해야 합니다.

- R을 사용 하는 SQL 계산 컨텍스트. 격리 된 리소스를 별도의 일괄 처리 실행에 사용할 수 있는 경우 하나의 다중 프로세서 환경, 테이블에서 데이터를 추출 하 고 동일한 작업 그룹에 있는 데이터를 제한 하려면 각 일괄 처리에 사용 되는 SQL 쿼리를 격리 하 여 효율성 향상을 얻을 수 있습니다. 일괄 처리를 격리 하는 데 사용 하는 방법 및 분할 등이의 PowerShell을 사용 하 여 병렬로 별도 쿼리를 실행 하 합니다.

- 임시 병렬 실행: SQL Server 계산 컨텍스트에서 병렬 실행 가능 하면 그리고 해당 옵션을 더 효율적으로 발견 되 면 적용 하려면 SQL 데이터베이스 엔진에 의존할 수 있습니다.

- T-SQL을 사용 하 여 별도 기능 생성 프로세스에서 합니다. SQL을 사용 하 여 기능 데이터 향상이 일반적으로 더 빠릅니다.

### <a name="prediction-scoring-in-parallel"></a>예측 병렬로 (점수)

SQL Server의 이점 중 하나는 많은 양의 행 병렬에서 처리 기능을 합니다. 곳은 이러한 이점은 하므로 것으로 표시 되어 점수 매기기입니다. 일반적으로 모델 않아도 모든 데이터에 대 한 액세스 상태 평가 대 한 하나 이상의 태스크를 처리 하는 각 작업 그룹으로 입력된 데이터를 분할할 수 있게 됩니다.

단일 쿼리로 입력된 데이터를 보낼 수도 있습니다 하 고 SQL Server 쿼리를 분석 합니다. 입력된 데이터에 대 한 병렬 쿼리 계획을 만들 수 있으면 자동으로 노드에 할당 된 데이터를 분할 하 고도 병렬로 필요한 조인 및 집계를 수행 합니다.

점수 계산에 사용 하기 위해 저장된 프로시저를 정의 하는 방법에 대 한 세부 정보에 관심이에 샘플 프로젝트를 참조 하십시오. [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) "step5_score_for_matching.sql" 파일을 찾습니다. 샘플 스크립트를 추적 쿼리 시작 및 종료 시간 및 시간 SQL 콘솔에 쓰기 성능을 평가할 수 있도록 합니다.

### <a name="concurrent-scoring-using-resource-groups"></a>리소스 그룹을 사용 하 여 동시 점수 매기기

점수 매기기 문제를 크기를 조정 하려면 여러 일괄 처리로 많은 항목이 나뉩니다 맵 감소 접근 방식을 사용 하는 것이 좋습니다. 그런 다음 여러 점수 매기기 작업이 동시에 실행 됩니다. 이 프레임 워크는 일괄 처리는 다양 한 CPU 집합에서 처리 및 결과 수집 되 고 데이터베이스에 다시 기록 됩니다.

이; resume 일치 하는 시나리오에서 사용 하는 방법 그러나 SQL Server에서 리소스 관리를이 접근 방식을 구현 해야 합니다. 외부 스크립트 작업에 대 한 작업 그룹을 설정 하 여 서로 다른 프로세서 그룹에 작업 점수 매기기 R 라우팅하고 더 빠른 처리량을 달성 합니다.

리소스 관리를 할당할 수 있습니다 (CPU 및 메모리)의 경쟁을 작업 부하를 최소화 하기 위해 서버에서 사용 가능한 리소스를 나눕니다. R 작업의 여러 유형을 구분하기 위해 분류 자 기능을 설정할 수 있습니다. 예를 들어, 재교육 작업은 우선 순위가 낮은 반면, 응용 프로그램에서 호출 된 점수는 항상 우선 순위로 결정할 수 있습니다. 잠재적으로 이러한 리소스 격리 실행 시간을 향상 되 고 예측 가능성이 더욱 뛰어난 성능을 제공할 수 있습니다.

### <a name="concurrent-scoring-using-powershell"></a>PowerShell을 사용 하 여 동시 점수 매기기

직접 데이터를 분할 하는 경우에 여러 동시 점수 매기기 작업을 실행할 PowerShell 스크립트를 사용할 수 있습니다. 이 위해 Invoke-sqlcmd cmdlet을 사용 하 고 동시에 점수 매기기 작업을 시작 합니다.

Resume 일치 하는 시나리오에서 동시성 다음과 같이 설계 되었습니다.

- 20 프로세서 5 개 cpu 4 개 그룹으로 나뉩니다. Cpu의 각 그룹은 동일한 NUMA 노드에 있습니다.

- 동시 일괄 처리의 최대 수는 8 개로 설정 되었습니다.

- 각 작업 그룹에는 두 점수 매기기 작업 처리 해야 합니다. 하나 이상의 태스크 완료 읽는 데이터와 점수 매기기 시작 되는 즉시 다른 작업 데이터베이스에서 데이터를 읽는 시작할 수 있습니다.

이 시나리오에 대 한 PowerShell 스크립트 확인 하려면 파일 experiment.ps1에서 열고는 [Github 프로젝트](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)합니다.

### <a name="storing-models-for-prediction"></a>예측에 대 한 모델을 저장

학습 및 평가 완료 되 고 있습니다 최상의 모델을 선택한 경우에 예측에 사용할 수 있도록 모델은 데이터베이스에 저장 하는 것이 좋습니다. SQL Server 기계 학습에서 특별 한 serialization 알고리즘을 사용 하 여 저장 하 고 R과 데이터베이스 사이 이동할 때 모델을 로드할 때문에 예측에 대 한 데이터베이스에서 미리 계산 된 모델을 로드 하는 것이 효율적,입니다.

> [!TIP]
> SQL Server 2017 년 R 서버에 설치 되지 않은 하는 경우에 점수 매기기를 수행 하려면 예측 함수를 사용할 수 있습니다. 제한 된 모델 유형과 RevoScaleR 패키지에서 지원 됩니다.

그러나 사용 하는 알고리즘에 따라 일부 모델에는 매우 클 수 있습니다, 특히 큰 데이터 집합에 대해 학습 하는 경우. 예를 들어와 같은 알고리즘 **lm** 또는 **glm** 많은 규칙과 함께 요약 데이터를 생성 합니다. Varbinary 열에 저장할 수 있는 모델의 크기에 제한이 있기 때문에 모델을 프로덕션에 대 한 데이터베이스에 저장 하기 전에 모델에서 불필요 한 아티팩트를 제거 하는 것이 좋습니다.

## <a name="articles-in-this-series"></a>이 시리즈의 기사

[성능-R에 대 한 튜닝 소개](../r/sql-server-r-services-performance-tuning.md)

[R-SQL Server 구성에 대 한 성능 조정](../r/sql-server-configuration-r-services.md)

[R-R에 대 한 성능 조정 코드 및 데이터 최적화](../r/r-and-data-optimization-r-services.md)

[성능 튜닝-사례 연구 결과](../r/performance-case-study-r-services.md)
