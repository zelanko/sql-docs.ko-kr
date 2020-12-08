---
title: '백서: 스핀 잠금 경합 진단 및 해결'
description: 이 문서에서는 SQL Server의 스핀 잠금 경합을 진단하고 해결하는 방법을 자세히 살펴봅니다. 이 문서는 원래 Microsoft SQLCAT 팀이 게시한 것입니다.
ms.date: 09/30/2020
ms.prod: sql
ms.reviewer: wiassaf
ms.technology: performance
ms.topic: how-to
author: bluefooted
ms.author: pamela
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6ecce46a04943d36dc6d821d6a3457b056f00356
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506317"
---
# <a name="diagnose-and-resolve-spinlock-contention-on-sql-server"></a>SQL Server에서 스핀 잠금 경합 진단 및 해결

이 문서에서는 높은 동시성 시스템에서 SQL Server 애플리케이션의 스핀 잠금 경합 관련 이슈를 식별하고 해결하는 방법에 대한 자세한 정보를 제공합니다.

> [!NOTE]
> 여기서 설명하는 권장 사항과 모범 사례는 실제 OLTP 시스템을 개발하고 배포하면서 겪은 실제 경험을 기반으로 합니다. 원래 Microsoft SQLCAT(SQL Server 고객 자문 팀) 팀이 게시한 것입니다.

## <a name="background"></a>배경

이전에는 상용 Windows Server 컴퓨터에서 한두 개의 마이크로프로세서/CPU 칩만 활용했으며 CPU가 단일 프로세서 또는 “코어”로만 설계되었습니다. 주로 트랜지스터 집적도의 발전을 통해 가능해진 더 빠른 CPU를 사용하면서 컴퓨터 처리 용량이 증가했습니다. 1971년에 첫 번째 범용 단일 칩 CPU가 개발된 이후 트랜지스터 집적도, 즉 통합 회로에 배치할 수 있는 트랜지스터 수는 “무어의 법칙”에 따라 지속적으로 2년마다 두 배로 증가했습니다. 최근 몇 년간 여러 개의 CPU가 포함된 컴퓨터를 구축함으로써 더 빠른 CPU로 컴퓨터 처리 용량을 늘이는 기존 방식이 확대되었습니다. 이 문서를 작성할 당시 Intel Nehalem CPU 아키텍처는 CPU당 최대 8개의 코어를 수용하므로, 8소켓 시스템에서 사용할 경우 하이퍼 스레딩 기술을 통해 두 배인 128개의 논리 프로세서로 늘릴 수 있습니다. x86 호환 컴퓨터의 논리 프로세서 수가 증가함에 따라 논리 프로세서가 리소스를 경합하므로 동시성 관련 이슈가 증가합니다. 이 가이드에서는 높은 동시성 시스템에서 일부 워크로드와 함께 SQL Server 애플리케이션을 실행할 때 관찰되는 특정 리소스 경합 이슈를 식별하고 해결하는 방법을 설명합니다.

이 섹션에서는 SQLCAT 팀이 스핀 잠금 경합 이슈를 진단하고 해결하면서 얻은 교훈을 분석합니다. 스핀 잠금 경합은 대규모 시스템의 실제 고객 워크로드에서 관찰되는 동시성 이슈 유형 중 하나입니다.

## <a name="symptoms-and-causes-of-spinlock-contention"></a>스핀 잠금 경합 증상 및 원인

이 섹션에서는 SQL Server의 OLTP 애플리케이션 성능에 부정적인 영향을 주는 ‘스핀 잠금 경합’ 관련 이슈를 진단하는 방법을 설명합니다. 스핀 잠금 진단 및 문제 해결은 고급 주제로 간주되어야 하며, 디버깅 도구 및 Windows 내부 요소에 대한 지식이 필요합니다.

스핀 잠금은 데이터 구조에 대한 액세스를 보호하는 데 사용되는 간단한 동기화 기본 형식입니다. 스핀 잠금은 SQL Server에 고유하지 않습니다. 지정된 데이터 구조에 짧은 시간 동안만 액세스하면 되는 경우 운영 체제에서 스핀 잠금을 사용합니다. 스핀 잠금을 획득하려는 스레드가 액세스 권한을 얻을 수 없는 경우 즉시 일시 중단되는 대신, 루프로 실행되어 리소스를 사용할 수 있는지 주기적으로 확인합니다. 일정 기간이 지나면 스핀 잠금에서 대기 중인 스레드가 리소스를 획득하기 전에 일시 중단됩니다. 일시 중단되면 동일한 CPU에서 실행되는 다른 스레드를 실행할 수 있습니다. 이 동작을 백오프라고 하며, 이 문서의 뒷부분에서 자세히 설명합니다.

SQL Server는 스핀 잠금을 활용하여 몇 가지 내부 데이터 구조에 대한 액세스를 보호합니다. 스핀 잠금은 래치와 유사한 방식으로 특정 데이터 구조에 대한 액세스를 직렬화하기 위해 엔진 내에서 사용됩니다. 래치와 스핀 잠금의 주요 차이점은 스핀 잠금의 경우 일정 기간 동안 스핀(루프 실행)하여 데이터 구조의 가용성을 확인하는 반면, 래치로 보호된 구조에 액세스하려는 스레드는 리소스를 사용할 수 없는 경우 즉시 일시 중단된다는 팩트입니다. 일시 중단하는 경우 CPU에서 스레드 컨텍스트를 전환하여 다른 스레드를 실행할 수 있게 해야 합니다. 비교적 비용이 많이 드는 작업으로, 짧은 기간 동안 보유하는 리소스의 경우 스레드를 루프로 실행하여 리소스의 가용성을 주기적으로 확인할 수 있게 하는 것이 전반적으로 더 효율적입니다.

## <a name="symptoms"></a>증상

사용량이 많은, 높은 동시성 시스템에서는 스핀 잠금으로 보호되고 자주 액세스하는 구조에 활성 경합이 나타나는 것이 일반적입니다. 이 사용은 경합으로 인해 상당한 CPU 오버헤드가 발생하는 경우에만 문제가 됩니다. 스핀 잠금 통계는 SQL Server 내에서 *sys.dm_os_spinlock_stats* DMV(동적 관리 뷰)를 통해 노출됩니다. 예를 들어 이 쿼리는 다음 출력을 생성합니다.

> [!NOTE]
> DMV에서 반환되는 정보를 해석하는 방법에 대한 자세한 내용은 이 문서의 뒷부분에서 설명합니다.

```sql
select * from sys.dm_os_spinlock_stats
order by spins desc
```

![sys.dm_os_spinlock_stats output](./media/diagnose-resolve-spinlock-contention/image4.png)

이 쿼리를 통해 노출되는 통계는 다음과 같습니다.

| 열 | 설명 |
|---|---|
| **충돌 횟수** | 이 값은 스핀 잠금으로 보호된 리소스에 대한 스레드 액세스가 차단될 때마다 증가합니다. |
| **스핀 횟수** | 이 값은 스핀 잠금을 사용할 수 있게 될 때까지 기다리는 동안 스레드가 루프를 실행할 때마다 증가합니다. 스레드가 리소스를 얻으려고 시도하는 동안 수행하는 작업량의 측정값입니다. |
| **Spins_per_collision** | 충돌당 스핀 비율입니다. |
| **일시 중지 시간** | 백오프 이벤트와 관련이 있지만 이 문서에 설명된 기술과는 관련이 없습니다. |
| **백오프 횟수** | 보유한 리소스에 액세스하려는 “스핀” 스레드가 동일한 CPU에서 다른 스레드의 실행을 허용해야 하는 경우에 발생합니다. |

이 논의의 목적에 특히 중요한 통계는 시스템 부하가 높은 특정 기간 내에 발생하는 충돌 횟수, 스핀 횟수, 백오프 이벤트 수입니다. 스레드가 스핀 잠금으로 보호된 리소스에 액세스하려고 하면 충돌이 발생합니다. 충돌이 발생하면 충돌 횟수가 증가하고, 스레드가 루프로 스핀을 시작하여 리소스를 사용할 수 있는지 주기적으로 확인합니다. 스레드가 스핀(루프)할 때마다 스핀 횟수가 증가합니다.

충돌당 스핀 횟수는 스레드가 스핀 잠금을 보유하는 동안 발생한 스핀량의 측정값으로, 스레드가 스핀 잠금을 보유하는 동안 발생한 스핀 횟수를 알려줍니다. 예를 들어 충돌당 스핀 횟수가 적고 충돌 횟수가 많으면 스핀 잠금에서 발생하는 스핀량이 적고 경합하는 스레드 수가 많은 것입니다. 스핀량이 많으면 스핀 잠금 코드에서 스핀하는 데 걸린 시간이 상대적으로 길었음을 의미합니다. 즉, 코드가 해시 버킷의 많은 항목을 처리하고 있습니다. 경합이 증가할수록(따라서 충돌 횟수가 증가할수록) 스핀 횟수도 늘어납니다.

백오프도 스핀과 유사한 방식으로 생각할 수 있습니다. 과도한 CPU 낭비를 방지하기 위해 스핀 잠금은 보유한 리소스에 액세스할 수 있을 때까지 무기한 스핀을 계속하지 않도록 설계되어 있습니다. 스핀 잠금은 CPU 리소스를 과도하게 사용하지 않기 위해 백오프하거나 스핀을 중단하고 “일시 중지”합니다. 스핀 잠금은 대상 리소스의 소유권 획득 여부에 관계없이 백오프합니다. 이 작업은 CPU에서 다른 스레드를 예약하여 생산성을 높이기 위한 것입니다. 엔진의 기본 동작은 백오프를 수행하기 전에 먼저 일정한 시간 간격 동안 스핀하는 것입니다. 스핀 잠금을 획득하려면 캐시 동시성 상태를 유지 관리해야 하며, 이 작업은 스핀의 CPU 비용에 비해 많은 CPU를 사용합니다. 따라서 스핀 잠금을 획득하려는 시도는 드물게 사용되며, 스레드가 스핀할 때마다 수행되지는 않습니다. SQL Server에서 특정 스핀 잠금 유형(예: LOCK_HASH)은 스핀 잠금을 획득하려는 시도 간격을 특정 한도까지 높여 향상되었으며, 이로 인해 CPU 성능에 미치는 영향도 감소하는 경우가 많습니다.

다음 다이어그램에서는 스핀 잠금 알고리즘의 개념을 보여 줍니다.

![스핀 잠금 알고리즘의 개념 보기](./media/diagnose-resolve-spinlock-contention/image5.png)

## <a name="typical-scenarios"></a>일반적인 시나리오

스핀 잠금 경합은 데이터베이스 디자인 결정과 관련이 없을 수도 있는 여러 가지 이유로 발생할 수 있습니다. 스핀 잠금이 내부 데이터 구조에 대한 액세스를 제어하기 때문에 스핀 잠금 경합은 스키마 디자인 선택 및 데이터 액세스 패턴의 직접적인 영향을 받는 버퍼 래치 경합과 동일한 방식으로 발생하지 않습니다.

스핀 잠금 경합과 관련된 주요 증상은 높은 스핀 횟수와 동일한 스핀 잠금을 획득하려는 많은 스레드 수로 인한 높은 CPU 사용량입니다. 일반적으로 CPU 코어 수가 24개 이상인 시스템에서 관찰되었으며, CPU 코어 수가 32개 이상인 시스템에서 가장 많이 관찰되었습니다. 앞서 언급했듯이 상당한 부하가 있는 높은 동시성 OLTP 시스템에서 일정 수준의 스핀 잠금 경합은 정상적이며, 오랜 시간 동안 실행된 시스템의 *sys.dm_os_spinlock_stats* DMV에서는 10억/조 단위의 많은 스핀 횟수가 보고되는 경우도 많습니다. 따라서 지정된 스핀 잠금 유형에 대해 높은 스핀 횟수가 관찰된다고 해서 워크로드 성능에 부정적인 영향을 미친다고 확신할 수는 없습니다.

다음 증상 중 몇 가지가 결합되면 스핀 잠금 경합을 나타낼 수 있습니다.

* 특정 스핀 잠금 유형에 대해 높은 스핀 횟수와 백오프 횟수가 관찰됩니다.

* 시스템의 CPU 사용률이 높거나 CPU 사용량이 급증합니다. 과도한 CPU 사용 시나리오에서는 SOS_SCHEDULER_YEILD의 신호 대기 수가 높습니다(DMV *sys.dm_os_wait_stats* 를 통해 보고됨).

* 시스템의 동시성이 높습니다.

* CPU 사용량과 스핀 횟수가 처리량에 비해 과도하게 증가합니다.

   > [!IMPORTANT]
   > 위 조건이 각각 true인 경우에도 높은 CPU 사용량의 근본 원인은 다른 곳에 있을 수 있습니다. 실제로 대부분의 경우 스핀 잠금 경합 이외의 이유로 CPU가 증가합니다. CPU 사용량 증가의 몇 가지 일반적인 원인은 다음과 같습니다.

* 기본 데이터가 증가하여 시간에 따라 비용이 늘어나는 쿼리로 인해 메모리 상주 데이터의 논리적 읽기를 추가로 수행해야 합니다.

* 쿼리 계획의 변경 결과로 실행이 최적이 아닙니다.

위 조건이 모두 true이면 가능한 스핀 잠금 경합 이슈를 추가로 조사합니다.

쉽게 진단할 수 있는 일반적인 현상 중 하나는 처리량과 CPU 사용량 간의 상당한 차이입니다. 많은 OLTP 워크로드는 (처리량/시스템의 사용자 수)와 CPU 사용량 간에 관계가 있습니다. CPU 사용량과 처리량 간의 상당한 차이와 함께 높은 스핀 횟수가 관찰되면 CPU 오버헤드를 유발하는 스핀 잠금 경합을 나타낼 수 있습니다. 여기서 유의해야 할 중요한 사항은 특정 쿼리의 비용이 시간에 따라 증가하는 경우에도 일반적으로 시스템에서 이 유형의 차이가 나타난다는 것입니다. 예를 들어 시간에 따라 논리적 읽기를 추가로 수행하는 데이터 세트에 대해 실행되는 쿼리도 비슷한 증상을 유발할 수 있습니다.

이 유형의 문제를 해결할 때는 높은 CPU의 더 일반적인 다른 원인을 제외하는 것이 중요합니다.

## <a name="example"></a>예제

다음 예제에서는 트랜잭션에서 초당 측정된 CPU 사용량과 처리량 간에 거의 선형 관계가 있습니다. 여기서는 워크로드가 증가함에 따라 오버헤드가 발생하기 때문에 약간의 차이가 나타나는 것이 정상적입니다. 여기서 볼 수 있듯이 이 차이는 상당히 커집니다. 또한 CPU 사용량이 100%에 도달하면 처리량이 급락합니다.

![성능 모니터의 CPU 하락](./media/diagnose-resolve-spinlock-contention/image7.png)

3분 간격으로 스핀 횟수를 측정하면 스핀 횟수 증가가 선형보다 더 가파른 것을 확인할 수 있으며, 스핀 잠금 경합이 문제가 될 수 있음을 나타냅니다.

![3분 간격의 스핀 횟수 차트](./media/diagnose-resolve-spinlock-contention/image8.png)

앞서 언급했듯이 스핀 잠금은 상당한 부하가 있는 높은 동시성 시스템에서 가장 일반적으로 나타납니다.

해당 이슈가 발생하기 쉬운 몇 가지 시나리오는 다음과 같습니다.

* 개체 이름을 정규화하지 못해 발생하는 이름 확인 문제. 자세한 내용은 [컴파일 잠금으로 인한 SQL Server 차단 설명](https://support.microsoft.com/help/263889/how-to-troubleshoot-blocking-caused-by-compile-locks)을 참조하세요. 해당 특정 이슈는 이 문서에서 자세히 설명합니다.

* 동일한 잠금에 자주 액세스하는 워크로드에 대한 잠금 관리자의 잠금 해시 버킷 경합(예: 자주 읽는 행의 공유 잠금). 이 유형의 경합은 LOCK_HASH 유형의 스핀 잠금으로 표시됩니다. 한 가지 특정 경우에 이 문제가 테스트 환경에서 잘못 모델링된 액세스 패턴의 결과로 발생하는 것을 발견했습니다. 이 환경에서는 잘못 구성된 테스트 매개 변수 때문에 필요한 개수보다 많은 스레드가 정확히 동일한 행을 지속적으로 액세스했습니다.

* MSDTC 트랜잭션 코디네이터 간에 대기 시간이 높은 경우 DTC 트랜잭션의 높은 비율. 이 특정 문제는 SQLCAT 블로그 항목 [DTC 관련 대기 해결 및 DTC 스케일링 성능 튜닝](https://techcommunity.microsoft.com/t5/datacat/resolving-dtc-related-waits-and-tuning-scalability-of-dtc/ba-p/305054)에서 자세히 설명합니다.

## <a name="diagnosing-spinlock-contention"></a>spinlock 경합 진단

이 섹션에서는 SQL Server 스핀 잠금 경합을 진단하는 방법을 설명합니다. 스핀 잠금 경합을 진단하는 데 사용되는 기본 도구는 다음과 같습니다.

| 도구 | 기능 |
|---|---|
| **성능 모니터링** | 높은 CPU 조건 또는 처리량과 CPU 사용량 간의 큰 차이를 찾습니다. |
| **sys.dm_os_spinlock stats DMV** | 지정한 기간에서 높은 스핀 횟수 및 백오프 이벤트 수를 찾습니다. |
| **SQL Server 확장 이벤트** | 높은 스핀 횟수가 발생하는 스핀 잠금의 호출 스택을 추적하는 데 사용됩니다. |
| **메모리 덤프** | 경우에 따라 SQL Server 프로세스 및 Windows 디버깅 도구의 메모리 덤프가 있습니다. 일반적으로 이 수준의 분석은 Microsoft SQL Server 지원 팀이 참여하는 경우에 수행됩니다. |

SQL Server 스핀 잠금 경합을 진단하는 일반적인 기술 프로세스는 다음과 같습니다.

1. **1단계**: 스핀 잠금과 관련된 경합이 있는지 확인합니다.

2. **2단계**: *sys.dm\_ os_spinlock_stats* 의 통계를 캡처하여 가장 많은 경합이 발생하는 스핀 잠금 유형을 찾습니다.

3. **3단계**: sqlservr.exe(sqlservr.pdb)의 디버그 기호를 가져와 SQL Server 인스턴스의 SQL Server 서비스 .exe 파일(sqlservr.exe)과 동일한 디렉터리에 기호를 저장합니다.\ 백오프 이벤트의 호출 스택을 확인하려면 실행하는 특정 SQL Server 버전의 기호가 있어야 합니다. SQL Server 기호는 Microsoft 기호 서버에서 다운로드할 수 있습니다. Microsoft 기호 서버에서 기호를 다운로드하는 방법에 대한 자세한 내용은 [기호를 사용하여 디버깅](https://docs.microsoft.com/windows/win32/dxtecharts/debugging-with-symbols)을 참조하세요.

4. **4단계**: SQL Server 확장 이벤트를 사용하여 관심 있는 스핀 잠금 유형의 백오프 이벤트를 추적합니다.

확장 이벤트를 통해 \"백오프\" 이벤트를 추적하고 적극적으로 스핀 잠금을 획득하려고 시도한 작업의 호출 스택을 캡처할 수 있습니다. 호출 스택을 분석하면 특정 스핀 잠금 경합에 참여하고 있는 작업 유형을 확인할 수 있습니다.

## <a name="diagnostic-walkthrough"></a>진단 연습

다음 연습에서는 도구와 기술을 사용하여 실제 시나리오에서 스핀 잠금 경합 문제를 진단하는 방법을 보여 줍니다. 이 연습은 고객 참여를 기반으로 하며 1TB 메모리가 있는 8소켓, 물리적 64코어 서버에서 약 6,500명의 동시 사용자를 시뮬레이트하는 벤치마크 테스트를 실행합니다.

### <a name="symptoms"></a>증상

CPU 사용률을 거의 100%까지 푸시하는 주기적 CPU 급증이 관찰되었습니다. 처리량과 CPU 사용량 간의 차이가 문제로 이어지는 것이 관찰되었습니다. CPU 급증이 발생할 즈음에는 CPU 사용량이 많은 시간 동안 특정 간격으로 높은 스핀 횟수가 발생하는 패턴이 설정되었습니다.

이 극단적인 경우에는 과도한 경합으로 인해 스핀 잠금 호위(convoy) 조건이 생성되었습니다. 호위(convoy)는 스레드가 더 이상 워크로드를 처리하지 못하고 잠금에 액세스하려는 시도에 모든 처리 리소스를 사용하는 경우에 발생합니다. 성능 모니터 로그는 트랜잭션 로그 처리량과 CPU 사용량 간의 이 차이와 궁극적으로 CPU 사용률의 급증을 보여 줍니다.

![성능 모니터의 CPU 급증](./media/diagnose-resolve-spinlock-contention/image9.png)

*sys.dm_os_spinlock_stats* 를 쿼리하여 SOS_CACHESTORE에 상당한 경합이 있음을 확인한 후 확장 이벤트 스크립트를 사용하여 관심 있는 스핀 잠금 유형의 백오프 이벤트 수를 측정했습니다.

| 이름 | 충돌 횟수 | 스핀 횟수 | 충돌당 스핀 횟수 | 백오프 횟수 |
|---|---|---|---|---|
| **SOS_CACHESTORE** |       14,752,117 |   942,869,471,526 |   63,914 |                67,900,620 |
| **SOS_SUSPEND_QUEUE** |   69,267,367 |   473,760,338,765 |   6,840  |                2,167,281 |
| **LOCK_HASH** |           5,765,761 |    260,885,816,584 |   45,247 |                3,739,208 |
| **MUTEX** |               2,802,773 |    9,767,503,682 |     3,485  |                350,997 |
| **SOS_SCHEDULER** |       1,207,007 |    3,692,845,572 |     3,060  |                109,746 |

스핀 횟수의 영향을 수량화하는 가장 간단한 방법은 스핀 횟수가 가장 많은 스핀 잠금 유형에 대해 동일한 1분 간격 동안 *sys.dm_os_spinlock_stats* 에서 노출된 백오프 이벤트 수를 확인하는 것입니다. 이 방법은 스레드가 스핀 잠금을 획득하려고 기다리는 동안 스핀 한도에 도달하는 경우를 나타내므로 상당한 경합을 감지하는 데 가장 적합합니다. 다음 스크립트는 확장 이벤트를 활용하여 관련 백오프 이벤트를 측정하고 경합이 있는 특정 코드 경로를 식별하는 고급 기술을 보여 줍니다.

SQL Server의 확장 이벤트에 대한 자세한 내용은 [SQL Server 확장 이벤트 소개](./extended-events/extended-events.md)를 참조하세요.

**스크립트**

```sql
/*
This Scriptis provided "AS IS" with no warranties, and confers no rights.

This script will monitor for backoff events over a given period of time and
capture the code paths (callstacks) for those.

--Find the spinlock types
select map_value, map_key, name from sys.dm_xe_map_values
where name = 'spinlock_types'
order by map_value asc

--Example: Get the type value for any given spinlock type
select map_value, map_key, name from sys.dm_xe_map_values
where map_value IN ('SOS_CACHESTORE', 'LOCK_HASH', 'MUTEX')

Examples:
61LOCK_HASH
144 SOS_CACHESTORE
08MUTEX

*/

--create the even session that will capture the callstacks to a bucketizer
--more information is available in this reference: http://msdn.microsoft.com/en-us/library/bb630354.aspx
create event session spin_lock_backoff on server
      add event sqlos.spinlock_backoff (action (package0.callstack)
where 
type = 61--LOCK_HASH
or type = 144--SOS_CACHESTORE
or type = 8--MUTEX
)
      add target package0.asynchronous_bucketizer (
            set filtering_event_name='sqlos.spinlock_backoff',
            source_type=1, source='package0.callstack')
      with (MAX_MEMORY=50MB, MEMORY_PARTITION_MODE = PER_NODE)

--Ensure the session was created
select * from sys.dm_xe_sessions
where name = 'spin_lock_backoff'

--Run this section to measure the contention 
alter event session spin_lock_backoff on server state=start

--wait to measure the number of backoffs over a 1 minute period
waitfor delay '00:01:00'

--To view the data
--1. Ensure the sqlservr.pdb is in the same directory as the sqlservr.exe
--2. Enable this trace flag to turn on symbol resolution 
DBCC traceon (3656, -1)

--Get the callstacks from the bucketize target
select event_session_address, target_name, execution_count, cast (target_data as XML)
from sys.dm_xe_session_targets xst
inner join sys.dm_xe_sessions xs on (xst.event_session_address = xs.address)
where xs.name = 'spin_lock_backoff'

--clean up the session 
alter event session spin_lock_backoff on server state=stop
drop event session spin_lock_backoff on server
```

출력을 분석하면 SOS_CACHESTORE 스핀과 관련된 가장 일반적인 코드 경로의 호출 스택을 확인할 수 있습니다. 반환된 호출 스택의 일관성을 검사하기 위해 CPU 사용률이 높은 시간 동안 스크립트를 여러 번 실행했습니다. 슬롯 버킷 수가 가장 높은 호출 스택이 두 출력에서 공통적으로 나타나는 것을 확인합니다(35,668 및 8,506). 해당 호출 스택의 “슬롯 수”는 다음으로 가장 높은 항목보다 두 자릿수가 더 큽니다. 이 조건은 관심 있는 코드 경로를 나타냅니다.

> [!NOTE]
> 이전 스크립트에서 반환된 호출 스택을 확인하는 것이 일반적입니다. 스크립트를 1분간 실행했을 때, 슬롯 수가 1000보다 큰 스택 및 슬롯 수가 10,000보다 큰 스택에서 문제가 발생할 가능성이 큰 것으로 관찰되었습니다.

> [!NOTE]
> 다음 출력의 서식은 읽기 쉽도록 정리되었습니다.

**출력 1**

```xml
<BucketizerTarget truncated="0" buckets="256">
<Slot count="35668" trunc="0">
  <value>
      XeSosPkg::spinlock_backoff::Publish 
      SpinlockBase::Sleep 
      SpinlockBase::Backoff 
      Spinlock<144,1,0>::SpinToAcquireOptimistic 
      SOS_CacheStore::GetUserData 
      OpenSystemTableRowset 
      CMEDScanBase::Rowset 
      CMEDScan::StartSearch 
      CMEDCatalogOwner::GetOwnerAliasIdFromSid 
      CMEDCatalogOwner::LookupPrimaryIdInCatalog CMEDCacheEntryFactory::GetProxiedCacheEntryByAltKey
      CMEDCatalogOwner::GetProxyOwnerBySID
      CMEDProxyDatabase::GetOwnerBySID
      ISECTmpEntryStore::Get 
      ISECTmpEntryStore::Get
      NTGroupInfo::`vector deleting destructor'
  </value> 
</Slot>
<Slot count="752" trunc="0">
  <value>
      XeSosPkg::spinlock_backoff::Publish 
      SpinlockBase::Sleep 
      SpinlockBase::Backoff 
      Spinlock<144,1,0>::SpinToAcquireOptimistic 
      SOS_CacheStore::GetUserData 
      OpenSystemTableRowset
      CMEDScanBase::Rowset 
      CMEDScan::StartSearch
      CMEDCatalogOwner::GetOwnerAliasIdFromSid CMEDCatalogOwner::LookupPrimaryIdInCatalog CMEDCacheEntryFactory::GetProxiedCacheEntryByAltKey             CMEDCatalogOwner::GetProxyOwnerBySID 
      CMEDProxyDatabase::GetOwnerBySID 
      ISECTmpEntryStore::Get
      ISECTmpEntryStore::Get 
      ISECTmpEntryStore::Get
  </value>
  </Slot>
```

**출력 2**

```xml
<BucketizerTarget truncated="0" buckets="256">
<Slot count="8506" trunc="0">
  <value>
      XeSosPkg::spinlock_backoff::Publish 
      SpinlockBase::Sleep+c7 [ @ 0+0x0 SpinlockBase::Backoff Spinlock<144,1,0>::SpinToAcquireOptimistic
      SOS_CacheStore::GetUserData 
      OpenSystemTableRowset 
      CMEDScanBase::Rowset 
      CMEDScan::StartSearch
      CMEDCatalogOwner::GetOwnerAliasIdFromSid CMEDCatalogOwner::LookupPrimaryIdInCatalog CMEDCacheEntryFactory::GetProxiedCacheEntryByAltKey CMEDCatalogOwner::GetProxyOwnerBySID 
      CMEDProxyDatabase::GetOwnerBySID 
      ISECTmpEntryStore::Get
      ISECTmpEntryStore::Get
      NTGroupInfo::`vector deleting destructor'
</value> 
 </Slot>
<Slot count="190" trunc="0">
  <value>
      XeSosPkg::spinlock_backoff::Publish 
      SpinlockBase::Sleep
       SpinlockBase::Backoff 
      Spinlock<144,1,0>::SpinToAcquireOptimistic 
      SOS_CacheStore::GetUserData 
      OpenSystemTableRowset 
      CMEDScanBase::Rowset 
      CMEDScan::StartSearch 
      CMEDCatalogOwner::GetOwnerAliasIdFromSid CMEDCatalogOwner::LookupPrimaryIdInCatalog CMEDCacheEntryFactory::GetProxiedCacheEntryByAltKey CMEDCatalogOwner::GetProxyOwnerBySID 
      CMEDProxyDatabase::GetOwnerBySID 
      ISECTmpEntryStore::Get 
      ISECTmpEntryStore::Get
      ISECTmpEntryStore::Get
   </value> 
 </Slot>
```

이전 예제에서 가장 흥미로운 스택은 슬롯 수가 가장 높은(35,668 및 8,506) 스택으로, 실제로 슬롯 수가 1000보다 큽니다.

이제 “이 정보로 무엇을 할 수 있나요?”라고 질문할 수 있습니다. 일반적으로 호출 스택 정보를 사용하려면 SQL Server 엔진을 자세히 알아야 하므로, 이 시점에서 문제 해결 프로세스는 애매한 영역으로 넘어갑니다. 이 특정 사례에서 호출 스택을 살펴보면 (**CMEDCatalogOwner::GetProxyOwnerBySID & CMEDProxyDatabase::GetOwnerBySID** 스택 프레임을 통해) 이슈가 발생한 코드 경로가 보안 및 메타데이터 조회와 관련이 있음을 확인할 수 있습니다.

이 정보만으로 문제를 해결하기는 어렵지만, 이슈를 자세히 파악하기 위해 추가 문제 해결을 집중할 영역에 대한 몇 가지 아이디어를 제공합니다.

해당 이슈는 보안 관련 검사를 수행하는 코드 경로와 관련된 것 같으므로 데이터베이스에 연결하는 애플리케이션 사용자에게 sysadmin 권한을 부여하는 테스트를 실행하기로 결정했습니다. 프로덕션 환경에서는 권장되지 않지만, 테스트 환경에서 이 기술은 유용한 문제 해결 단계인 것으로 입증되었습니다. 상승된 권한(sysadmin)으로 세션을 실행했을 때 경합과 관련된 CPU 급증이 사라졌습니다.

## <a name="options-and-workarounds"></a>옵션 및 해결 방법

스핀 잠금 경합 문제 해결은 확실히 사소한 작업이 아닐 수 있습니다. “한 가지 일반적인 최상의 방법”은 없습니다. 성능 문제를 해결하는 첫 번째 단계는 근본 원인을 확인하는 것입니다. 이 문서에 설명된 기술과 도구를 사용하는 것은 스핀 잠금 관련 경합 지점을 파악하는 데 필요한 분석의 첫 번째 단계입니다.

최신 SQL Server 버전이 개발됨에 따라 높은 동시성 시스템에 최적화된 코드를 구현함으로써 엔진의 스케일링 성능이 계속 향상되고 있습니다. SQL Server는 높은 동시성 시스템을 위한 많은 최적화를 도입했으며, 그 중 하나가 가장 일반적인 경합 지점에 대한 지수 백오프입니다. 엔진 내의 모든 스핀 잠금에 지수 백오프 알고리즘을 활용하여 구체적으로 이 특정 영역을 향상하는 특정 개선 사항이 SQL Server 2012부터 도입되었습니다.

뛰어난 성능과 스케일링이 필요한 고급 애플리케이션을 디자인하는 경우 SQL Server 내에서 필요한 코드 경로를 가능한 한 짧게 유지하는 방법을 고려합니다. 코드 경로가 짧을수록 데이터베이스 엔진에서 수행하는 작업이 감소하므로 자연스럽게 경합 지점이 방지됩니다. 대부분의 모범 사례에는 엔진에 요구되는 작업량이 감소하는 부작용이 있으므로 워크로드 성능이 최적화됩니다.

이 문서의 앞부분에 있는 몇 가지 모범 사례를 예로 들어 살펴보겠습니다.

* **정규화된 이름:** 모든 개체의 이름을 정규화하면 SQL Server에서 이름 확인에 필요한 코드 경로를 실행하지 않아도 됩니다. 저장 프로시저 호출에 정규화된 이름을 활용하지 않을 때 발생하는 SOS_CACHESTORE 스핀 잠금 유형에서도 경합 지점이 관찰되었습니다. 해당 이름을 정규화하지 않으면 SQL Server에서 사용자의 기본 스키마를 조회해야 하므로 SQL을 실행하는 데 필요한 코드 경로가 더 길어집니다.

* **매개 변수가 있는 쿼리:** 또 다른 예는 매개 변수가 있는 쿼리와 저장 프로시저 호출을 활용하여 실행 계획을 생성하는 데 필요한 작업을 줄이는 것입니다. 이 경우에도 실행할 코드 경로가 짧아집니다.

* **LOCK_HASH 경합:** 특정 잠금 구조 또는 해시 버킷 충돌에서 경합을 피할 수 없는 경우도 있습니다. SQL Server 엔진이 대다수 잠금 구조를 분할하지만, 잠금을 획득한 결과로 동일한 해시 버킷에 액세스하게 되는 경우도 있습니다. 예를 들어 애플리케이션에서 여러 스레드가 동시에 동일한 행에 액세스합니다(즉, 참조 데이터). 이 유형의 문제는 데이터베이스 스키마 내에서 해당 참조 데이터를 스케일 아웃하거나 가능한 경우 NOLOCK 힌트를 활용하는 기술로 접근할 수 있습니다.

SQL Server 워크로드를 튜닝할 때 첫 번째 방어선은 항상 표준 튜닝 방법(예: 인덱싱, 쿼리 최적화, I/O 최적화 등)입니다. 그러나 표준 튜닝 외에도 작업 수행에 필요한 코드 양을 줄이는 방법을 따르는 것이 중요합니다. 모범 사례를 따르는 경우에도 사용량이 많은, 높은 동시성 시스템에서는 스핀 잠금 경합이 발생할 수 있습니다. 이 문서에 설명된 도구와 기술을 사용하여 해당 유형의 문제를 파악하거나 제외하고 적절한 Microsoft 리소스에게 도움을 요청해야 하는 경우를 확인할 수 있습니다.

이 기술이 해당 유형의 문제 해결에 유용한 방법과 SQL Server에서 사용 가능한 몇 가지 고급 성능 프로파일링 기술에 대한 인사이트를 제공하기를 바랍니다.

## <a name="appendix-automate-memory-dump-capture"></a>부록: 메모리 덤프 캡처 자동화

다음 확장 이벤트 스크립트는 스핀 잠금 경합이 심해질 경우 메모리 덤프 수집을 자동화하는 데 유용한 것으로 입증되었습니다. 문제를 완전히 진단하는 데 메모리 덤프가 필요하거나 Microsoft 지원 팀이 심층 분석을 위해 메모리 덤프를 요청하는 경우가 있습니다. SQL Server 2008에서는 bucketizer가 캡처하는 호출 스택의 프레임 수가 16개로 제한되므로 엔진 내에서 호출 스택의 입력 위치를 정확하게 확인하지 못할 수 있습니다. SQL Server 2012에서는 bucketizer가 캡처하는 호출 스택의 프레임 수를 32개로 늘려 기능을 개선했습니다.

다음 SQL 스크립트를 사용하면 스핀 잠금 경합 분석에 도움이 되도록 메모리 덤프 캡처 프로세스를 자동화할 수 있습니다.

```sql
/*
This script is provided "AS IS" with no warranties, and confers no rights.

Use:    This procedure will monitor for spinlocks with a high number of backoff events
        over a defined time period which would indicate that there is likely significant
        spin lock contention.
        
        Modify the variables noted below before running.


Requires:
        xp_cmdshell to be enabled
            sp_configure 'xp_cmd', 1
            go 
            reconfigure 
            go
        
*********************************************************************************************************/
use tempdb
go 
if object_id('sp_xevent_dump_on_backoffs') is not null
    drop proc sp_xevent_dump_on_backoffs
go 
create proc sp_xevent_dump_on_backoffs
(
    @sqldumper_path                       nvarchar(max)      = '"c:\Program Files\Microsoft SQL Server\100\Shared\SqlDumper.exe"'
    ,@dump_threshold                      int                = 500           --capture mini dump when the slot count for the top bucket exceeds this
    ,@total_delay_time_seconds            int                = 60            --poll for 60 seconds
    ,@PID                                 int                = 0
    ,@output_path                         nvarchar(max)      = 'c:\'
    ,@dump_captured_flag                  int = 0 OUTPUT
    
)
as
/* 
    --Find the spinlock types
    select map_value, map_key, name from sys.dm_xe_map_values
    where name = 'spinlock_types'
    order by map_value asc

    --Example: Get the type value for any given spinlock type
    select map_value, map_key, name from sys.dm_xe_map_values
    where map_value IN ('SOS_CACHESTORE', 'LOCK_HASH', 'MUTEX')
*/
if exists (select * from sys.dm_xe_session_targets xst
                inner join sys.dm_xe_sessions xs on (xst.event_session_address = xs.address)
                where xs.name = 'spinlock_backoff_with_dump')
    drop event session spinlock_backoff_with_dump on server

create event session spinlock_backoff_with_dump  on server
      add event sqlos.spinlock_backoff (action (package0.callstack)
            where
                type = 61                 --LOCK_HASH
                --or type = 144           --SOS_CACHESTORE
                --or type = 8             --MUTEX
                --or type = 53            --LOGCACHE_ACCESS
                --or type = 41            --LOGFLUSHQ
                --or type = 25            --SQL_MGR
                --or type = 39            --XDESMGR
                )
      add target package0.asynchronous_bucketizer (
            set filtering_event_name='sqlos.spinlock_backoff',
            source_type=1, source='package0.callstack')
      with (MAX_MEMORY=50MB, MEMORY_PARTITION_MODE = PER_NODE)

alter event session spinlock_backoff_with_dump  on server state=start


declare @instance_name            nvarchar(max) = @@SERVICENAME
declare @loop_count               int = 1
declare @xml_result               xml 
declare @slot_count               bigint 
declare @xp_cmdshell              nvarchar(max) = null

--start polling for the backoffs
print 'Polling for: ' + convert(varchar(32), @total_delay_time_seconds) + ' seconds'
while (@loop_count < CAST (@total_delay_time_seconds/1 as int))
begin 
    waitfor delay '00:00:01'

    --get the xml from the bucketizer for the session
    select @xml_result= CAST(target_data as xml)
    from sys.dm_xe_session_targets xst
        inner join sys.dm_xe_sessions xs on (xst.event_session_address = xs.address)
    where xs.name = 'spinlock_backoff_with_dump'
    
    --get the highest slot count from the bucketizer
    select @slot_count = @xml_result.value(N'(//Slot/@count)[1]', 'int')

    --if the slot count is higher than the threshold in the one minute period
    --dump the process and clean up session
    if (@slot_count > @dump_threshold)
    begin 
        print 'exec xp_cmdshell ''' + @sqldumper_path + ' ' + convert(nvarchar(max), @PID) + ' 0 0x800 0 c:\ '''
        select @xp_cmdshell = 'exec xp_cmdshell ''' + @sqldumper_path + ' ' + convert(nvarchar(max), @PID) + ' 0 0x800 0 ' + @output_path + ' '''
        exec sp_executesql @xp_cmdshell
        print 'loop count: ' + convert (varchar(128), @loop_count)
        print 'slot count: ' + convert (varchar(128), @slot_count)
        set @dump_captured_flag = 1
        break
    end 

    --otherwise loop 
    set @loop_count = @loop_count + 1

end

--see what was collected then clean up
DBCC traceon (3656, -1)
select event_session_address, target_name, execution_count, cast (target_data as XML)
from sys.dm_xe_session_targets xst
    inner join sys.dm_xe_sessions xs on (xst.event_session_address = xs.address)
where xs.name = 'spinlock_backoff_with_dump'

alter event session spinlock_backoff_with_dump  on server state=stop
drop event session spinlock_backoff_with_dump  on server
go

/* CAPTURE THE DUMPS 
******************************************************************/
--Example: This will run continuously until a dump is created. 
declare @sqldumper_path                nvarchar(max)        = '"c:\Program Files\Microsoft SQL Server\100\Shared\SqlDumper.exe"'
declare @dump_threshold                int                  = 300            --capture mini dump when the slot count for the top bucket exceeds this
declare @total_delay_time_seconds      int                  = 60             --poll for 60 seconds 
declare @PID                           int                  = 0
declare @flag                          tinyint              = 0
declare @dump_count                    tinyint              = 0
declare @max_dumps                     tinyint              = 3              --stop after collecting this many dumps
declare @output_path                   nvarchar(max)        = 'c:\'          --no spaces in the path please :)


--Get the process id for sql server 
declare @error_log table (LogDate datetime,
    ProcessInfo varchar(255),
    Text varchar(max)
    )
insert into @error_log
    exec ('xp_readerrorlog 0, 1, ''Server Process ID''')
select @PID = convert(int, (REPLACE(REPLACE(Text, 'Server Process ID is ', ''), '.', '')))
    from @error_log where Text like ('Server Process ID is%')
print 'SQL Server PID: ' + convert (varchar(6), @PID)

--Loop to monitor the spinlocks and capture dumps. while (@dump_count < @max_dumps)
begin 

    exec sp_xevent_dump_on_backoffs @sqldumper_path             = @sqldumper_path,
                                    @dump_threshold             = @dump_threshold,
                                    @total_delay_time_seconds   = @total_delay_time_seconds,
                                    @PID                        = @PID,
                                    @output_path                = @output_path,
                                    @dump_captured_flag         = @flag OUTPUT
    if (@flag > 0) 
        set @dump_count=@dump_count + 1
    print 'Dump Count: ' + convert(varchar(2), @dump_count)
    waitfor delay '00:00:02'

end
```

## <a name="appendix-capture-spinlock-statistics-over-time"></a>부록: 시간별 스핀 잠금 통계 캡처

다음 스크립트를 사용하여 특정 기간의 스핀 잠금 통계를 확인할 수 있습니다. 스크립트를 실행할 때마다 현재 값과 수집된 이전 값 사이의 델타가 반환됩니다.

```sql
/* Snapshot the current spinlock stats and store so that this can be compared over a time period
   Return the statistics between this point in time and the last collection point in time.

   **This data is maintained in tempdb so the connection must persist between each execution**
   **alternatively this could be modified to use a persisted table in tempdb. if that
   is changed code should be included to clean up the table at some point.**
*/

use tempdb
go

declare @current_snap_time    datetime
declare @previous_snap_time   datetime

set @current_snap_time = GETDATE()

if not exists(select name from tempdb.sys.sysobjects where name like '#_spin_waits%')
    create table #_spin_waits
    (
        lock_name    varchar(128)
        ,collisions  bigint
        ,spins       bigint
        ,sleep_time  bigint
        ,backoffs    bigint
        ,snap_time   datetime
    )

--capture the current stats
insert into #_spin_waits
    (
        lock_name
        ,collisions
        ,spins
        ,sleep_time
        ,backoffs
        ,snap_time
        )
        select  name
                ,collisions
                ,spins
                ,sleep_time
                ,backoffs
                ,@current_snap_time
        from sys.dm_os_spinlock_stats

select top 1 @previous_snap_time = snap_time from #_spin_waits
                where snap_time < (select max(snap_time) from #_spin_waits)
                order by snap_time desc

--get delta in the spin locks stats   
select top 10
        spins_current.lock_name
        , (spins_current.collisions - spins_previous.collisions) as collisions
        , (spins_current.spins - spins_previous.spins) as spins
        , (spins_current.sleep_time - spins_previous.sleep_time) as sleep_time
        , (spins_current.backoffs - spins_previous.backoffs) as backoffs
        , spins_previous.snap_time as [start_time]
        , spins_current.snap_time as [end_time]
        , DATEDIFF(ss, @previous_snap_time, @current_snap_time) as [seconds_in_sample]
    from #_spin_waits spins_current
    inner join (
        select * from #_spin_waits
          where snap_time = @previous_snap_time
        ) spins_previous on (spins_previous.lock_name = spins_current.lock_name)
    where
        spins_current.snap_time = @current_snap_time
        and spins_previous.snap_time = @previous_snap_time
        and spins_current.spins > 0
    order by (spins_current.spins - spins_previous.spins) desc

--clean up table
delete from #_spin_waits
where snap_time = @previous_snap_time
```

## <a name="next-steps"></a>다음 단계

성능 모니터링 도구에 대한 자세한 내용은 [성능 모니터링 및 튜닝 도구](./performance/performance-monitoring-and-tuning-tools.md)를 참조하세요.