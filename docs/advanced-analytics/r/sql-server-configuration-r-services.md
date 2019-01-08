---
title: SQL Server 구성 (R Services)-SQL Server Machine Learning 서비스
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 63ba1878317427b4274d894ae1b0c4237601f141
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645282"
---
# <a name="sql-server-configuration-for-use-with-r"></a>R 사용에 대 한 SQL Server 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 두 가지 사용 사례에 따라 R Services에 대 한 성능 최적화를 설명 하는 시리즈의 두 번째입니다.  이 문서에서는 SQL Server R Services를 실행 하는 데 사용 되는 컴퓨터의 하드웨어 및 네트워크 구성에 대 한 지침을 제공 합니다. 또한 SQL Server 인스턴스, 데이터베이스 또는 솔루션에서 사용 되는 테이블을 구성 하는 방법에 대 한 정보를 포함 합니다. 하드웨어 및 데이터베이스 최적화 사이 있는 줄을 흐리게 하는 SQL Server의 NUMA 사용, 때문에 세 번째 섹션에는 CPU affinitization 및 리소스 거 버 넌 스를 자세히 설명 합니다.

> [!TIP]
> SQL Server를 처음 접하는 경우 SQL Server 성능 튜닝 가이드 검토 하는 것이 좋습니다. [모니터링 및 성능 튜닝](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance)합니다.

## <a name="hardware-optimization"></a>하드웨어 최적화

서버 컴퓨터의 최적화가 외부 스크립트를 실행할 리소스가 있는지 확인 하기 위한 중요 합니다. 리소스 제한 된 경우 이러한 현상이 발생할 수 있습니다.

- 작업 실행 지연 또는 다른 데이터베이스 작업과 우선 순위를 취소 합니다.
- 완료 하지 않고 종료 되어 R 스크립트 오류 "할당량이 초과 됨"
- 데이터가 잘리는 경우 불완전 한 결과 대 한 R 메모리로 로드

### <a name="memory"></a>메모리

컴퓨터에서 사용 가능한 메모리 양은 고급 분석 알고리즘의 성능에 큰 영향을 미칠 수 있습니다. 메모리가 부족 하 여 SQL 계산 컨텍스트를 사용 하는 경우 병렬 처리 수준이 달라질 수 있습니다. 처리할 수 있는 청크 크기 및 지원할 수 있는 동시 세션 수에도 영향을 미칠 수 있습니다.

32GB의 최소값을 사용 하는 것이 좋습니다. 32GB 이상 사용할 수 있는 경우에 성능 향상을 위해 모든 읽기 작업에서 더 많은 행을 사용 하도록 SQL 데이터 원본을 구성할 수 있습니다.

인스턴스에서 사용 하는 메모리를 관리할 수도 있습니다. 기본적으로 SQL Server 우선 순위를 가지도록 외부 스크립트 프로세스를 통해 메모리를 할당 하는 경우. R Services의 기본 설치에서 사용 가능한 메모리의 20%만 할당할 R.

일반적으로이 없는 데이터 과학 작업에 충분 하지만 원하지도 않을 것 SQL server 메모리 고갈. 실험 하 고 데이터베이스 엔진, 관련된 서비스 및 최적의 구성을 사례별로 달라 지는 이해를 사용 하 여 외부 스크립트 간의 메모리 할당을 미세 조정 해야 합니다.

Resume-일치 하는 모델에 대 한 외부 스크립트 사용 된 많은 및 다른 데이터베이스 엔진 서비스를 실행 했습니다. 따라서 외부 스크립트에 할당 된 리소스는 스크립트 성능에 대 한 최상의 구성 된 70%로 증가 되었습니다.

### <a name="power-options"></a>전원 옵션

Windows 운영 체제에는 **고성능** 전원 옵션을 사용 해야 합니다. SQL Server를 사용 하는 경우 성능이 저하 되거나 일관 되지 않은 결과 서로 다른 전원 설정을 사용 합니다.

### <a name="disk-io"></a>디스크 IO

학습 및 R Services를 사용 하 여 작업은 기본적으로 IO 예측 바인딩된 및 데이터베이스에 저장 된 디스크의 속도에 따라 달라 집니다. SSD (반도체 드라이브) 등의 더 빠른 드라이브가 도움이 될 수 있습니다.

디스크 IO는 디스크에 액세스하는 다른 애플리케이션의 영향도 받습니다(예: 다른 클라이언트에 의한 데이터베이스 읽기 작업). 디스크 IO 성능은 사용 중인 파일 시스템에 대한 설정의 영향을 받을 수도 있습니다(예: 파일 시스템에서 사용되는 블록 크기).

여러 드라이브를 사용할 수 있는 경우 SQL Server 데이터베이스 엔진에 대 한 요청 하므로 다른 드라이브에 있는 데이터베이스와 동일한 디스크 도달 하지 하는 저장소 데이터베이스에 저장 된 데이터에 대 한 요청 합니다.

교육 중에 여러 반복을 사용하는 RevoScaleR analytic 함수를 실행 중인 경우 디스크 IO가 성능에 큰 영향을 미칠 수도 있습니다. 예를 들어 `rxLogit`, `rxDTree`를 `rxDForest`, 및 `rxBTrees` 모두 여러 반복을 사용 합니다. 데이터 원본 SQL Server 인 경우 이러한 알고리즘 데이터를 캡처하기 위해 최적화 된 임시 파일을 사용 합니다. 이러한 파일은 세션이 완료된 후 자동으로 정리됩니다. 읽기/쓰기 작업용 고성능 디스크 이러한 알고리즘에 대 한 전체 경과 시간이 크게 향상 시킬 수 있습니다.

> [!NOTE]
> R Services의 이전 버전 Windows 운영 체제에서 8.3 파일 이름 지원이 필요합니다. 이 제한 사항은 서비스 팩 1 후 변경 되었습니다. 그러나 드라이브를 8.3 파일 이름을 지원 하는지 여부를 확인 하거나 지원을 사용 하도록 설정 하지 않는 경우 fsutil.exe를 사용할 수 있습니다.

### <a name="paging-file"></a>페이징 파일

Windows 운영 체제에서는 페이징 파일을 사용하여 크래시 덤프를 관리하고 가상 메모리 페이지를 저장합니다. 과도한 페이징이 발견되면 컴퓨터에서 실제 메모리를 늘리는 것이 좋습니다. 실제 메모리를 추가해도 페이징은 제거되지 않지만 페이징의 필요성이 감소합니다.

페이지 파일이 저장된 디스크의 속도가 성능에 영향을 미칠 수도 있습니다. 페이지 파일을 SSD에 저장하거나 여러 SSD에 걸쳐 여러 페이지 파일을 사용하면 성능이 향상될 수 있습니다.

페이지 파일 크기 조정에 대 한 내용은 참조 하세요 [64 비트 버전의 Windows에 대 한 적절 한 페이지 파일 크기를 확인 하는 방법을](https://support.microsoft.com/kb/2860880)합니다.

## <a name="optimizations-at-instance-or-database-level"></a>인스턴스 또는 데이터베이스 수준에서 최적화

SQL Server 인스턴스의 최적화에 효율적으로 실행 한 외부 스크립트의 키입니다.

> [!NOTE]
> 가장 적합 한 설정 크기 및 유형의 데이터에 점수 매기기 모델 학습에 사용 하는 열의 수에 따라 다릅니다.
> 
> 마지막 기사에서는 특정 최적화 결과 검토할 수 있습니다. [성능 튜닝-사례 연구 결과](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> 샘플 스크립트는 별도 참조 하세요 [GitHub 리포지토리](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)합니다.

### <a name="table-compression"></a>테이블 압축

IO 성능은 압축 또는 칼럼 형식 데이터 저장소를 사용 하 여 종종 개선할 수 있습니다. 일반적으로 데이터 이므로 columnstore를 사용 하 여 이러한 반복의 데이터를 압축할 때 종종 테이블 내의 여러 열에서 반복 됩니다.

Columnstore는 테이블에 대 한 다양 한 삽입 경우 효율적이 아닐 이지만 적합 한 데이터는 정적 이거나 자주 변경 하는 경우. 열 형식 저장소가 적절하지 않은 경우 행 우선 테이블에서 압축을 사용하면 IO 성능이 향상될 수 있습니다.

자세한 내용은 다음 문서를 참조하세요.

+ [데이터 압축](../../relational-databases/data-compression/data-compression.md)

+ [테이블 또는 인덱스에서 압축 사용](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Columnstore 인덱스 가이드](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블

오늘날에 메모리가 더 이상 최신 컴퓨터에 대 한 문제입니다. 하드웨어 사양 개선 하기 위해 계속, 적절 한 값에서 RAM을 가져오려는 비교적 쉽습니다. 그러나 이와 동시에 데이터를 그 어느 때 보다 신속 하 게 생성 되는 및 짧은 대기 시간으로 데이터를 처리할 수 있어야 합니다.

메모리 최적화 테이블의 빅 데이터 문제를 해결 하는 고급 컴퓨터의 사용 가능한 많은 메모리를 활용할 수에 하나의 솔루션을 나타냅니다. 메모리 최적화 테이블에서 데이터는 읽고 메모리에 기록 되도록에 주로 메모리에 상주 합니다. 내구성에 대 한 테이블의 두 번째 복사본은 디스크에서 유지 관리 및 데이터를만 데이터베이스를 복구 하는 동안 디스크에서 읽으면 됩니다.

을 읽고 테이블에 쓰기 작업을 자주 할 경우 높은 확장성과 짧은 대기 시간을 사용 하 여 메모리 최적화 테이블 도움이 됩니다.  Resume-일치 하는 시나리오에서 사용 하 여 메모리 최적화 테이블의를 사용 하면 데이터베이스에서 모든 다시 시작 기능을 읽고 새 채용와 일치 하도록 주 메모리에 저장할 수 있었습니다. 이 디스크 IO 상당히 줄어듭니다.

추가 성능 향상에서 여러 동시 일괄 처리 다시 데이터베이스에 예측을 작성 하는 동안 메모리 최적화 테이블을 사용 하 여 얻은 결과입니다. 테이블 읽기 및 쓰기에 짧은 대기 시간을 사용 하는 SQL Server에서 메모리 최적화 테이블의를 사용 합니다.

개발 하는 동안 환경을 원활 하 게도 했습니다. 메모리 최적화 내구성이 있는 테이블 데이터베이스에서 생성 된 동시에 생성 되었습니다. 따라서 개발에서 데이터를 저장 하는 위치에 관계 없이 동일한 워크플로 사용 합니다.

### <a name="processor"></a>프로세서

SQL Server 컴퓨터에서 사용 가능한 코어를 사용 하 여 병렬로 작업을 수행할 수 있습니다. 사용할 수 있는 코어 수가 많을 수록 성능이 합니다. IO 바인딩 작업에 대 한 코어 수를 늘리면 도움이 되지 않을 수 있습니다 하는 동안 CPU 코어 수를 사용 하 여 더 빠른 cpu에서 알고리즘 혜택을 바인딩됩니다.

서버는 일반적으로 여러 사용자가 동시에 사용 하기 때문에 데이터베이스 관리자는 최대 작업 계산을 지 원하는 데 필요한 코어의 이상적인 개수를 결정 해야 합니다.

### <a name="resource-governance"></a>리소스 거 버 넌 스

Resource Governor를 지 원하는 버전에서 특정 워크 로드가 특정 개수의 Cpu 할당 된 지정 하려면 리소스 풀을 사용할 수 있습니다. 또한 특정 워크 로드에 할당 된 메모리의 양을 관리할 수 있습니다.

SQL Server의 리소스 거 버 넌 스를 사용 하면 SQL Server에 R에서 사용 되는 다양 한 리소스의 모니터링 및 제어를 중앙 집중화 예를 들어, 데이터베이스 엔진의 경우 해당 코어 서비스 일시적인 많은 워크 로드에 관계 없이 항상 실행할 수 있도록 절반 사용 가능한 메모리를 할당할 수 있습니다.

외부 스크립트의 메모리 사용에 대 한 기본 값 자체 SQL Server에 대 한 사용 가능한 총 메모리의 20%로 제한 됩니다. 이 제한은 데이터베이스 서버에 의존 하는 모든 작업은 심각한 영향을 받지 않도록 장기 실행 R 작업이 되도록 기본적으로 적용 됩니다. 하지만 이 제한은 데이터베이스 관리자가 변경할 수 있습니다. 대부분의 경우에서 20%도 심각한 기계 학습 워크 로드를 지원 하도록 적합 하지 않습니다.

지원 되는 구성 옵션은 **MAX_CPU_PERCENT**를 **MAX_MEMORY_PERCENT**, 및 **MAX_PROCESSES**합니다. 현재 설정을 보려면이 문을 사용 합니다. `SELECT * FROM sys.resource_governor_external_resource_pools`

-  R Services에 대 한 서버를 사용 하는 것이 주로, 경우 MAX_CPU_PERCENT를 40% 또는 60% 향상 하는 데 도움이 수 있습니다.

-  많은 R 세션이 동시에 동일한 서버를 사용 해야 합니다, 세 가지 설정이 모두 늘려야 합니다.

할당 된 리소스 값을 변경 하려면 T-SQL 문을 사용 합니다.

+ 이 문은 40%로 메모리 사용량을 설정합니다. `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 이 문은 모든 세 가지 구성 가능한 값을 설정합니다. `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 메모리, CPU 또는 최대 프로세스 설정을 변경한 후에 즉시 설정을 적용 하려면 경우에이 문을 실행 합니다. `ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>소프트 NUMA, NUMA 하드웨어 및 CPU 선호도

SQL Server 계산 컨텍스트를 사용 하는 경우에 따라 NUMA 및 프로세서 선호도 관련 된 설정을 조정 하 여 더 나은 성능을 얻을 수 있습니다. 

시스템과 _하드웨어 NUMA_ 둘 이상의 시스템 버스, 사용 되는 작은 프로세서 집합에 있어야 합니다. 각 CPU는 일관 된 방식으로 다른 그룹과 연결 된 메모리를 액세스할 수 있습니다. 각 그룹을 NUMA 노드라고 합니다. 하드웨어 NUMA가 있는 경우 NUMA 대신 인터리브 메모리를 사용하도록 구성할 수 있습니다. 이 경우 Windows 및 SQL Server는 하지 NUMA로 인식 합니다. 

SQL Server에 사용 가능한 메모리 노드의 번호를 찾으려면 다음 쿼리를 실행할 수 있습니다.

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

쿼리에서 하나의 메모리 노드 (노드 0)을 반환 하는 경우 하드웨어 NUMA가 없는 또는 하드웨어가 인터리브 (비-NUMA)로 구성 됩니다. SQL Server에도 하드웨어 NUMA 무시 때 있는 4 개 이하의 Cpu가 하나 이상의 노드 CPU가 하나뿐인 경우입니다.

컴퓨터에 프로세서가 여러 개 있지만 하드웨어 NUMA가 없는, 하는 경우 사용할 수도 있습니다 [SOFT-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) 에 Cpu를 더 작은 그룹으로 세분화 합니다.  SQL Server 2016 및 SQL Server 2017에서 SQL Server 서비스를 시작 합니다. 소프트 NUMA 기능을 자동으로 활성화 됩니다.

SQL Server를; 노드를 자동으로 관리 소프트 NUMA를 사용 하는 경우 그러나 특정 워크 로드를 최적화 하려면 비활성화할 수 있습니다 _소프트 선호도_ 및 소프트 NUMA 노드에 대 한 CPU 선호도 수동으로 구성 합니다. 이 수 강력 하 게 제어는 워크 로드는 노드에 할당 된 리소스 거 버 넌 스를 지 원하는 SQL Server 버전을 사용 하는 경우에 특히 합니다. CPU 선호도 지정 하 고 cpu 그룹과 리소스 풀에 맞게 조정 하 여 대기 시간을 줄일 수 있으며 관련된 프로세스는 동일한 NUMA 노드 내에서 수행 되었는지 확인 합니다.

소프트 NUMA 및 R 워크 로드를 지원 하기 위해 CPU 선호도 구성 하기 위한 전체 프로세스는 다음과 같습니다.

1. 사용 가능한 경우 소프트 NUMA를 사용 하도록 설정
2. 프로세서 선호도 정의 합니다.
3. 사용 하 여 외부 프로세스에 대 한 리소스 풀을 만들 [리소스 관리자](../r/resource-governance-for-r-services.md)
4. 할당 된 [워크 로드 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md) 특정 선호도 그룹

세부 정보, 샘플 코드를 포함 하 여이 자습서를 참조 하세요. [SQL 최적화 팁과 트릭 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**기타 리소스:**

+ [SQL Server에서 소프트 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Cpu를 소프트 NUMA 노드를 매핑하는 방법

+ [자동 SOFT-NUMA: 빠른 (Bob Ward) 실행](https://blogs.msdn.microsoft.com/bobsql/2016/06/03/sql-2016-it-just-runs-faster-automatic-soft-numa/)

   기록에 설명 합니다. 최신 다중 코어 서버에서 성능 구현 세부 정보 뿐만 아니라 합니다.

## <a name="task-specific-optimizations"></a>태스크 별 최적화

이 섹션에는 이러한 사례 연구에 특정 한 기계 학습 워크 로드를 최적화 하기 위한 다른 테스트를 채택 하는 방법을 요약 합니다. 모델 학습, 기능 추출 및 기능 엔지니어링 및 점수 매기기에 대 한 다양 한 시나리오를 포함 하는 일반적인 작업: 단일 행, 작은 일괄 처리 및 큰 일괄 처리 합니다.

### <a name="feature-engineering"></a>기능 엔지니어링

R 사용 하 여 고충 단일 CPU에 일반적으로 처리 되지 않는 경우 이 많은 작업에 대 한 주요 성능 병목 현상이 특히 기능 엔지니어링 합니다. 다시 시작-일치 하는 솔루션을 단독으로 기능 엔지니어링 작업 원래 100 기능과 결합 된 2,500 제품 간 기능을 만들었습니다. 모든 단일 CPU에서 수행 된 경우이 작업 시간이 많이 걸립니다.

여러 가지 방법으로 기능 엔지니어링의 성능을 향상 시킬 수 있습니다. R 코드를 최적화 하 고 모델링 프로세스 내에서 기능 추출 유지 하거나 기능 엔지니어링 프로세스를 SQL로 이동 합니다.

- R 함수를 정의 하 고 인수로 전달한 [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) 학습 중입니다. 모델에서 병렬 처리를 지 원하는 경우 기능 엔지니어링 작업을 여러 Cpu를 사용 하 여 처리할 수 있습니다. 데이터 과학 팀이이 방법을 사용 하면 시간을 점수 매기기를 기준으로 16% 성능 향상을 관찰 합니다. 그러나이 방법은 병렬 처리 및 병렬 계획을 사용 하 여 실행할 수 있는 쿼리를 지 원하는 모델을 해야 합니다.

- SQL 사용 하 여 R을 사용 하는 컨텍스트를 계산 합니다. 별도의 일괄 처리 실행에 사용할 수 있는 격리 된 리소스를 사용 하 여 다중 프로세서 환경에서 각 일괄 처리에 대 한 테이블에서 데이터를 추출 하 고 동일한 작업 그룹에 있는 데이터를 제한 하는 데 사용 하는 SQL 쿼리를 격리 하 여 효율성을 얻을 수 있습니다. 일괄 처리를 격리 하는 데 사용 하는 방법 및 분할 등이 병렬로 별도 쿼리를 실행 하려면 PowerShell 사용 하 여.

- 임시 병렬 실행: SQL Server 계산 컨텍스트에서 적용 가능한 경우 병렬 실행 하 고 해당 옵션을 더 효율적으로 발견 되 면 SQL 데이터베이스 엔진에서 사용할 수 있습니다.

- 별도 기능화 (featurization) 프로세스에서 T-SQL을 사용 합니다. SQL을 사용 하 여 데이터 기능 향상이 일반적으로 더 빠릅니다.

### <a name="prediction-scoring-in-parallel"></a>예측 (점수 매기기) 병렬로

SQL Server의 이점 중 하나는 대량의 동시에 행을 처리 하는 기능입니다. Nowhere이 활용 하므로 것으로 표시 되어 점수 매기기입니다. 일반적으로 모델 않아도 모든 데이터에 대 한 액세스 점수 매기기를 위해 하나 이상의 태스크를 처리 하는 각 작업 그룹을 사용 하 여 입력된 데이터를 분할할 수 있게 됩니다.

단일 쿼리로 입력된 데이터를 보낼 수도 있습니다 및 SQL Server에서 쿼리를 분석 합니다. 입력된 데이터에 대 한 병렬 쿼리 계획을 만들 수 있는 경우 자동으로 노드를 할당 하는 데이터를 분할 하 고 병렬로 필요한 조인 및 집계를 수행 합니다.

점수 매기기에 사용 하기 위해 저장된 프로시저를 정의 하는 방법의 세부 정보에 관심이에서 샘플 프로젝트를 참조 하세요. [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) "step5_score_for_matching.sql" 파일을 찾습니다. 예제는 성능을 평가할 수 있도록 추적 쿼리 시작 및 종료 시간, 쓰기 SQL 콘솔에 스크립트.

### <a name="concurrent-scoring-using-resource-groups"></a>리소스 그룹을 사용 하 여 동시 점수 매기기

점수 매기기 문제를 강화 하려면 여러 일괄 처리로 나뉘고는 수백만 개의 항목이 있는 맵 감소 접근 방식을 채택 하는 것이 좋습니다. 그런 다음 여러 점수 매기기 작업을 동시에 실행 됩니다. 일괄 처리에이 프레임 워크에서 다른 CPU 집합 처리 및 결과 수집 되 고 데이터베이스에 다시 기록 합니다.

이 다시 시작-일치 하는 시나리오;에서 사용 하는 방법 그러나 SQL Server의 리소스 거 버 넌 스가 접근이 방식을 구현 하는 데 필수적입니다. 외부 스크립트 작업에 대 한 작업 그룹을 설정 하 여 R 다른 프로세서 그룹에 점수 매기기 작업을 라우팅할 수 있으며 더 빠른 처리량을 달성할 수 있습니다.

리소스 거 버 넌 스를 할당할 수 있습니다 (CPU 및 메모리) 워크 로드 경쟁을 최소화 하는 서버의 사용 가능한 리소스를 나눕니다. R 작업의 여러 유형을 구분하기 위해 분류 자 기능을 설정할 수 있습니다. 예를 들어, 재교육 작업은 우선 순위가 낮은 반면, 응용 프로그램에서 호출 된 점수는 항상 우선 순위로 결정할 수 있습니다. 잠재적으로이 리소스 격리 실행 시간을 개선 하 고 예측 가능성이 더욱 뛰어난 성능을 제공할 수 있습니다.

### <a name="concurrent-scoring-using-powershell"></a>PowerShell을 사용 하 여 동시 점수 매기기

직접 데이터를 분할 하려는 경우에 여러 동시 점수 매기기 작업을 실행할 PowerShell 스크립트를 사용할 수 있습니다. 이렇게 하려면 Invoke-sqlcmd cmdlet을 사용 하 고 점수 매기기 작업을 병렬로 시작 합니다.

Resume-일치 하는 경우 동시성 같이 설계 되었습니다.

- 20 프로세서의 cpu가 5 개 각 4 개 그룹으로 나뉩니다. Cpu의 각 그룹은 동일한 NUMA 노드에 있습니다.

- 동시 일괄 처리의 최대 수는 8 개로 설정 되었습니다.

- 각 작업 그룹에는 두 가지 점수 매기기 작업 처리 해야 합니다. 한 작업이 끝나면 데이터 및 점수 매기기 시작 읽기는 즉시 데이터베이스에서 데이터를 읽는 다른 작업이 시작할 수 있습니다.

이 시나리오에 대 한 PowerShell 스크립트를 보려면에서 파일 experiment.ps1 엽니다는 [Github 프로젝트](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)합니다.

### <a name="storing-models-for-prediction"></a>예측 모델을 저장합니다.

학습 및 평가 완료 최상의 모델을 선택한 경우에 예측에 사용할 수 있도록 모델 데이터베이스에 저장 하는 것이 좋습니다. SQL Server machine learning에서 특별 한 serialization 알고리즘을 사용 하 여 저장 하 고 R과 데이터베이스 간에 이동 하는 경우 모델을 로드 하기 때문에 예측을 위해 데이터베이스에서 미리 계산 된 모델을 로드 하는 것이 효율적,입니다.

> [!TIP]
> SQL Server 2017의 R 서버에 설치 되어 있지 않더라도 점수 매기기를 수행 하 여 PREDICT 함수를 사용할 수 있습니다. 제한 된 모델 형식 RevoScaleR 패키지에서 지원 됩니다.

그러나 사용 하는 알고리즘에 따라 일부 모델 상당히 클 수 있습니다, 특히 큰 데이터 집합에서 학습 하는 경우. 예를 들어 같은 알고리즘 **lm** 또는 **glm** 많은 규칙과 함께 요약 데이터를 생성 합니다. Varbinary 열에 저장할 수 있는 모델의 크기에 제한이 있기 때문에 프로덕션 데이터베이스에서 모델을 저장 하기 전에 모델에서 불필요 한 아티팩트를 제거 하는 것이 좋습니다.

## <a name="articles-in-this-series"></a>이 시리즈의 기사

[성능 튜닝-R에 대 한 소개](../r/sql-server-r-services-performance-tuning.md)

[R-SQL Server 구성에 대 한 성능 조정](../r/sql-server-configuration-r-services.md)

[R-R의 성능 튜닝 코드 및 데이터 최적화](../r/r-and-data-optimization-r-services.md)

[성능 튜닝-사례 연구 결과](../r/performance-case-study-r-services.md)
