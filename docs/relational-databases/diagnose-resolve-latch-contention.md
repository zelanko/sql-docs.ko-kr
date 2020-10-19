---
title: '백서: 래치 경합 진단 및 해결'
description: 이 문서에서는 SQL Server의 래치 경합을 진단하고 해결하는 방법을 자세히 살펴봅니다. 이 문서는 원래 Microsoft SQLCAT 팀이 게시한 것입니다.
ms.date: 09/30/2020
ms.prod: sql
ms.reviewer: jroth
ms.technology: performance
ms.topic: how-to
author: bluefooted
ms.author: pamela
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c1cbf760c16d6de88906d03f511315ae6caec335
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91811885"
---
# <a name="diagnose-and-resolve-latch-contention-on-sql-server"></a>SQL Server에서 래치 경합 진단 및 해결

이 가이드에서는 높은 동시성 시스템에서 특정 워크로드와 함께 SQL Server 애플리케이션을 실행할 때 관찰된 래치 경합 이슈를 식별하고 해결하는 방법을 설명합니다.

서버의 CPU 코어 수가 계속 증가함에 따라 관련된 동시성 증가로 인해 데이터베이스 엔진 내에서 직렬 방식으로 액세스해야 하는 데이터 구조에 경합 지점이 생길 수 있습니다. 높은 처리량/높은 동시성 트랜잭션 처리(OLTP) 워크로드의 경우 특히 가능성이 높습니다. 이 문제에 접근하는 다양한 도구, 기술, 방법이 있으며 애플리케이션을 디자인할 때 이런 문제를 방지하기 위해 사용할 수 있는 방법도 많습니다. 이 문서에서는 스핀 잠금을 사용하여 데이터 구조에 대한 액세스를 직렬화하는 데이터 구조의 특정 경합 유형에 대해 설명합니다.

> [!NOTE]
> 이 콘텐츠는 높은 동시성 시스템에서 SQL Server 애플리케이션의 페이지 래치 경합과 관련된 이슈를 확인하고 해결하는 프로세스를 기준으로 Microsoft SQLCAT(SQL Server 고객 자문 팀) 팀이 작성한 것입니다. 여기서 설명하는 권장 사항과 모범 사례는 실제 OLTP 시스템을 개발하고 배포하면서 겪은 실제 경험을 기반으로 합니다.

## <a name="what-is-sql-server-latch-contention"></a>SQL Server 래치 경합이란 무엇인가요?

래치는 인덱스, 데이터 페이지, 내부 구조(예: B-트리의 비-리프 페이지)를 비롯한 메모리 내 구조의 일관성을 보장하기 위해 SQL Server 엔진에서 사용하는 간단한 동기화 기본 형식입니다. SQL Server는 버퍼 래치를 사용하여 버퍼 풀의 페이지를 보호하고, I/O 래치를 사용하여 버퍼 풀에 아직 로드되지 않은 페이지를 보호합니다. SQL Server 버퍼 풀의 페이지에서 데이터를 쓰거나 읽을 때마다 작업자 스레드는 먼저 페이지에 대한 버퍼 래치를 획득해야 합니다. 배타적 래치(PAGELATCH_EX) 및 공유 래치(PAGELATCH_SH)를 비롯한 다양한 버퍼 래치 유형을 사용하여 버퍼 풀의 페이지에 액세스할 수 있습니다. SQL Server가 아직 버퍼 풀에 없는 페이지에 액세스하려고 하면 페이지를 버퍼 풀로 로드하기 위해 비동기 I/O가 게시됩니다. SQL Server가 I/O 하위 시스템의 응답을 기다려야 하는 경우 요청 유형에 따라 배타적(PAGEIOLATCH_EX) 또는 공유(PAGEIOLATCH_SH) I/O 래치에서 기다립니다. 이렇게 하면 다른 작업자 스레드가 호환되지 않는 래치를 사용하는 버퍼 풀에 동일한 페이지를 로드할 수 없도록 차단됩니다. 래치는 버퍼 풀 페이지 이외의 다른 내부 메모리 구조에 대한 액세스를 보호하는 데에도 사용되며, 해당 래치를 비-버퍼 래치라고 합니다.

페이지 래치 경합이 다중 CPU 시스템에서 발생하는 가장 일반적인 시나리오이므로, 이 문서의 대부분은 해당 시나리오에 중점을 둡니다.

래치 경합은 여러 스레드가 동일한 메모리 내 구조에 대해 호환되지 않는 래치를 동시에 획득하려고 할 때 발생합니다. 래치는 내부 제어 메커니즘이므로 SQL 엔진이 사용할 시기를 자동으로 결정합니다. 래치 동작은 결정적이므로 스키마 디자인을 비롯한 애플리케이션 결정이 동작에 영향을 줄 수 있습니다. 이 문서에서는 다음 정보를 제공합니다.

* SQL Server에서 래치를 사용하는 방식에 대한 배경 정보 
* 래치 경합을 조사하는 데 사용되는 도구 
* 관찰된 경합 양이 문제가 되는지 확인하는 방법

몇 가지 일반적인 시나리오와 경합을 완화하기 위해 해당 시나리오를 처리하는 최상의 방법을 알아보겠습니다.

## <a name="how-does-sql-server-use-latches"></a>SQL Server는 래치를 어떻게 사용하나요?

SQL Server의 각 페이지는 8KB이며 여러 행을 저장할 수 있습니다. 동시성 및 성능 향상을 위해 버퍼 래치는 논리 트랜잭션 기간 동안 유지되는 잠금과 달리 페이지에 대한 실제 작업 기간 동안만 유지됩니다.

래치는 SQL 엔진 내부에 있으며 메모리 일관성을 제공하는 데 사용되는 반면, 잠금은 SQL Server에서 논리 트랜잭션 일관성을 제공하는 데 사용됩니다. 다음 표에서는 잠금과 래치를 비교해서 설명합니다.

| 구조체 | 목적     | 제어  | 성능 비용 | 노출  |
|---|---|---|---|---|
| **래치** | 메모리 내 구조의 일관성을 보장합니다. | SQL Server 엔진만 제어할 수 있습니다.  | 성능 비용이 낮습니다. 최대 동시성을 허용하고 최대 성능을 제공하기 위해 래치는 논리 트랜잭션 기간 동안 유지되는 잠금과 달리 메모리 내 구조에 대한 실제 작업 기간 동안만 유지됩니다. | [sys.dm_os_wait_stats(Transact-SQL)](./system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) - PAGELATCH, PAGEIOLATCH, LATCH 대기 유형에 대한 정보를 제공합니다(LATCH_EX, LATCH_SH는 모든 비-버퍼 래치 대기를 그룹화하는 데 사용됨).<br/>[sys.dm_os_latch_stats(Transact-SQL)](./system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md) – 비-버퍼 래치 대기에 대한 자세한 정보를 제공합니다.<br/>[sys.dm_os_latch_stats(Transact-SQL)](./system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md) - 이 DMV는 래치 관련 성능 이슈를 해결하는 데 유용한 각 인덱스에 대해 집계된 대기를 제공합니다. |
| **잠금**  | 트랜잭션 일관성을 보장합니다.  | 사용자가 제어할 수 있습니다. | 잠금은 트랜잭션 기간 동안 유지해야 하므로 래치에 비해 성능 비용이 높습니다. | [sys.dm_tran_locks(Transact-SQL)](./system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)<br/>[sys.dm_exec_sessions(Transact-SQL)](./system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)|

## <a name="sql-server-latch-modes-and-compatibility"></a>SQL Server 래치 모드 및 호환성

일부 래치 경합은 SQL Server 엔진 작업의 정상적인 부분으로 예상되어야 합니다. 높은 동시성 시스템에서 서로 다른 호환성의 여러 래치 요청이 동시에 발생하는 것은 피할 수 없습니다. SQL Server는 처리 중인 래치 요청이 완료될 때까지 호환되지 않는 래치 요청은 큐에서 대기하도록 요구하여 래치 호환성을 적용합니다.

래치는 액세스 수준과 관련된 5가지 모드 중 하나로 획득됩니다. SQL Server 래치 모드를 다음과 같이 요약할 수 있습니다.

* **KP** - 유지 래치이며, 참조된 구조를 제거할 수 없도록 합니다. 스레드가 버퍼 구조를 확인하려고 할 때 사용됩니다. KP 래치는 제거(DT) 래치를 제외한 모든 래치와 호환되므로 “경량”으로 간주됩니다. 즉, KP 래치를 사용할 때 성능에 미치는 영향이 최소화됨을 의미합니다. KP 래치는 DT 래치와 호환되지 않으므로 다른 스레드가 참조된 구조를 제거할 수 없도록 차단합니다. 예를 들어 KP 래치는 참조된 구조가 지연 기록기 프로세스를 통해 제거되지 않도록 차단합니다. SQL Server 버퍼 페이지 관리와 함께 지연 기록기 프로세스를 사용하는 방법에 대한 자세한 내용은 [페이지 쓰기](./writing-pages.md)를 참조하세요.

* **SH** - 공유 래치이며, 페이지 구조를 읽는 데 필요합니다. 
* **UP** - 업데이트 래치이며, SH(공유 래치) 및 KP와 호환되지만 다른 래치와는 호환되지 않으므로 EX 래치가 참조된 구조에 쓸 수 없도록 차단합니다. 
* **EX** - 배타적 래치이며, 다른 스레드가 참조된 구조에서 쓰거나 읽을 수 없도록 차단합니다. 한 가지 사용 예로, 조각난 페이지 보호를 위해 페이지 내용을 수정하는 경우가 여기에 해당합니다. 
* **DT** - 제거 래치이며, 참조된 구조의 내용을 제거하기 전에 획득해야 합니다. 예를 들어 지연 기록기 프로세스는 다른 스레드가 사용할 수 있도록 사용 가능한 버퍼 목록에 추가하기 전에 클린 페이지를 확보하기 위해 DT 래치를 획득해야 합니다.

래치 모드의 호환성 수준은 각기 다릅니다. 예를 들어 공유 래치(SH)는 업데이트(UP) 또는 유지(KP) 래치와 호환되지만 제거 래치(DT)와는 호환되지 않습니다. 래치가 호환되기만 하면, 동일한 구조에 대해 여러 래치를 동시에 획득할 수 있습니다. 스레드가 호환되지 않는 모드의 래치를 획득하려고 하면 리소스를 사용할 수 있다는 신호를 기다리는 큐에 배치됩니다. SOS_Task 유형의 스핀 잠금은 큐에 대한 직렬화된 액세스를 적용하여 대기 큐를 보호하는 데 사용됩니다. 큐에 항목을 추가하려면 이 스핀 잠금을 획득해야 합니다. SOS_Task 스핀 잠금은 호환되지 않는 래치가 해제될 때 큐의 스레드에 신호를 보내 대기 중인 스레드가 호환되는 래치를 획득하여 작업을 계속할 수 있도록 합니다. 대기 큐는 래치 요청이 해제될 때 FIFO(선입 선출) 방식으로 처리됩니다. 래치는 이 FIFO 시스템을 따라 공정성을 보장하고 스레드 고갈을 방지합니다.

래치 모드 호환성은 다음 표에 나와 있습니다(**Y**는 호환성을 나타내고, **N**은 비호환성을 나타냄).

|래치 모드 |**KP**  |**SH** |**UP**  |**EX**  |**DT**|
|--------|--------|-------|--------|--------|--------|
|**KP**  |Y       |Y      |Y       |Y       |N|
|**SH**  |Y       |Y      |Y       |N       |N|
|**UP**  |Y       |Y      |N       |N       |N|
|**EX**  |Y       |N      |N       |N       |N|
|**DT**  |N       |N      |N       |N       |N|

## <a name="sql-server-superlatches-and-sublatches"></a>SQL Server 슈퍼 래치 및 하위 래치

NUMA 기반의 다중 소켓/다중 코어 시스템이 증가하면서 SQL Server 2005에는 32개 이상의 논리 프로세서가 있는 시스템에만 적용되는 슈퍼 래치(하위 래치라고도 함)가 도입되었습니다. 슈퍼 래치는 높은 동시성 OLTP 워크로드의 특정 사용 패턴에 대해 SQL 엔진의 효율성을 높입니다. 예를 들어 특정 페이지에 읽기 전용 공유(SH) 액세스는 많지만 쓰기는 거의 없는 패턴이 있는 경우입니다. 해당 액세스 패턴이 있는 페이지의 예로 B-트리(즉, 인덱스) 루트 페이지가 있습니다. SQL 엔진은 B-트리의 임의 수준에서 페이지 분할이 발생할 경우 공유 래치가 루트 페이지에 유지되도록 요구합니다. 삽입이 많은 높은 동시성 OLTP 워크로드에서는 처리량에 따라 페이지 분할 수가 크게 증가하므로 성능이 저하될 수 있습니다. 슈퍼 래치를 사용하면 동시에 실행되는 여러 작업자 스레드에 SH 래치가 필요한 공유 페이지에 대한 액세스 성능을 높일 수 있습니다. 성능 향상을 위해 SQL Server 엔진은 해당 페이지의 래치를 슈퍼 래치로 동적으로 승격합니다. 슈퍼 래치는 CPU 코어별로 파티션당 하나의 하위 래치를 사용하는 하위 래치 구조 배열로 단일 래치를 분할합니다. 여기서 주 래치는 프록시 리디렉터가 되고 읽기 전용 래치에는 전역 상태 동기화가 필요하지 않습니다. 이렇게 하면 항상 특정 CPU에 할당되는 작업자는 로컬 스케줄러에 할당된 공유(SH) 하위 래치만 획득하면 됩니다.

공유 슈퍼 래치와 같은 호환되는 래치를 획득하면 전역 상태 동기화 요구 사항이 제거됨으로써 로컬 NUMA 메모리만 액세스하여 성능이 훨씬 향상되기 때문에 분할되지 않은 공유 래치보다 리소스가 더 적게 사용되고 핫 페이지에 대한 액세스의 스케일링이 향상됩니다. 반대로, 배타적(EX) 슈퍼 래치를 획득하면 SQL에서 모든 하위 래치에 신호를 보내야 하므로 EX 일반 래치보다 비용이 더 많이 듭니다. 슈퍼 래치가 EX 액세스가 많은 패턴을 사용하는 것으로 관찰될 경우 SQL 엔진은 버퍼 풀에서 페이지가 삭제된 후 슈퍼 래치를 강등할 수 있습니다. 다음 다이어그램에서는 일반 래치와 분할된 슈퍼 래치를 보여 줍니다.

![SQL Server 슈퍼 래치](./media/diagnose-resolve-latch-contention/image4.png)

성능 모니터의 **SQL Server:Latches** 개체 및 연결된 카운터를 사용하여 슈퍼 래치 수, 초당 슈퍼 래치 승격 수, 초당 슈퍼 래치 강등 수 등의 슈퍼 래치 정보를 수집할 수 있습니다. **SQL Server:Latches** 개체 및 연결된 카운터에 대한 자세한 내용은 [SQL Server, Latches 개체](./performance-monitor/sql-server-latches-object.md)를 참조하세요.

## <a name="latch-wait-types"></a>래치 대기 유형

누적 대기 정보는 SQL Server에서 추적되며, *sys.dm_os_wait_stats* DMV(동적 관리 뷰)를 사용하여 액세스할 수 있습니다. SQL Server는 *sys.dm_os_wait_stats* DMV에서 해당 “wait_type”으로 정의된 세 가지 래치 대기 유형을 사용합니다.

* **버퍼(BUF) 래치:** 사용자 개체 인덱스 및 데이터 페이지의 일관성을 보장하는 데 사용됩니다. SQL Server가 시스템 개체에 사용하는 데이터 페이지에 대한 액세스를 보호하는 데에도 사용됩니다. 예를 들어 버퍼 래치는 할당을 관리하는 페이지를 보호합니다. 여기에는 PFS(페이지 여유 공간), GAM(전역 할당 맵), SGAM(공유 전역 할당 맵), IAM(인덱스 할당 맵) 페이지가 포함됩니다. 버퍼 래치는 *sys.dm_os_wait_stats*에서 *wait_type* **PAGELATCH\_\*** 로 보고됩니다.

* **비-버퍼(Non-BUF) 래치:** 버퍼 풀 페이지가 아닌 다른 모든 메모리 내 구조의 일관성을 보장하는 데 사용됩니다. 비-버퍼 래치 대기는 *wait_type* **LATCH\_\*** 로 보고됩니다.

* **IO 래치:** I/O 작업을 사용하여 버퍼 풀에 구조를 로드해야 하는 경우 버퍼 래치로 보호된 동일한 구조의 일관성을 보장하는 버퍼 래치의 하위 집합입니다. IO 래치는 다른 스레드가 호환되지 않는 래치를 사용하는 버퍼 풀에 동일한 페이지를 로드할 수 없도록 차단합니다. *wait_type* **PAGEIOLATCH\_\*** 와 연결됩니다.

   > [!NOTE]
   > 표시되는 PAGEIOLATCH 대기가 상당히 높으면 SQL Server가 I/O 하위 시스템에서 대기하고 있음을 의미합니다. 어느 정도의 PAGEIOLATCH 대기는 예상되고 정상적인 동작이지만 평균 PAGEIOLATCH 대기 시간이 지속적으로 10ms(밀리초)를 초과할 경우 I/O 하위 시스템이 압력을 받고 있는 이유를 조사해야 합니다.

*sys.dm_os_wait_stats* DMV에서 비-버퍼 래치를 발견할 경우 *sys.dm_os_latch_waits*를 검사하여 비-버퍼 래치에 대한 누적 대기 정보의 자세한 분석을 확인해야 합니다. 모든 버퍼 래치 대기는 BUFFER 래치 클래스로 분류되고, 나머지 대기는 비-버퍼 래치를 분류하는 데 사용됩니다.

## <a name="symptoms-and-causes-of-sql-server-latch-contention"></a>SQL Server 래치 경합의 증상 및 원인

사용량이 많은 높은 동시성 시스템에서는 자주 액세스하고 SQL Server의 래치 및 다른 제어 메커니즘으로 보호된 구조에서 활성 경합이 나타나는 것이 일반적입니다. 페이지에 대한 래치 획득과 관련된 경합 및 대기 시간으로 인해 리소스(CPU) 사용률이 감소하여 처리량이 저하되는 경우 문제가 있는 것으로 간주됩니다.

### <a name="example-of-latch-contention"></a>래치 경합 예제

다음 다이어그램에서 파란색 선은 초당 트랜잭션 수로 측정된 SQL Server의 처리량을 나타내고, 검은색 선은 평균 페이지 래치 대기 시간을 나타냅니다. 이 예제에서 각 트랜잭션은 bigint 데이터 형식의 IDENTITY 열을 채우는 경우와 같이 순차적으로 증가하는 선행 값을 사용하여 클러스터형 인덱스에 INSERT를 수행합니다. CPU 수를 32개로 늘리면 전반적인 처리량은 감소했고, 페이지 래치 대기 시간은 검은색 선으로 알 수 있듯이 약 48밀리초로 증가한 것이 명확해집니다. 처리량과 페이지 래치 대기 시간 간의 반비례 관계는 쉽게 진단할 수 있는 일반적인 시나리오입니다.

![동시성이 증가하면 처리량은 감소함](./media/diagnose-resolve-latch-contention/image5.png)

### <a name="performance-when-latch-contention-is-resolved"></a>래치 경합이 해결된 경우의 성능

다음 다이어그램에 표시된 것처럼 SQL Server는 더 이상 페이지 래치 대기로 병목 상태를 겪지 않으며 처리량이 초당 트랜잭션 수로 측정 시 300% 증가합니다. 해당 작업은 이 문서의 뒷부분에서 설명하는 **계산 열을 통한 해시 분할 사용** 기술로 수행되었습니다. 이 성능 향상은 코어 수가 많고 동시성 수준이 높은 시스템으로 전달됩니다.

![해시 분할을 통해 실현된 처리량 향상](./media/diagnose-resolve-latch-contention/image6.png)

## <a name="factors-affecting-latch-contention"></a>래치 경합에 영향을 주는 요소

OLTP 환경의 성능을 방해하는 래치 경합은 일반적으로 다음 요소 중 하나 이상과 관련된 높은 동시성으로 인해 발생합니다.

| 요인 | 세부 정보 |
|---|---|
| **SQL Server에서 사용되는 논리 CPU 수가 많음**  | 래치 경합은 모든 다중 코어 시스템에서 발생할 수 있습니다. SQLCAT 환경에서 허용 수준 이상으로 애플리케이션 성능에 영향을 주는 과도한 래치 경합은 일반적으로 16개 이상의 CPU 코어가 있는 시스템에서 관찰되었으며, 추가 코어를 사용할 수 있게 되면 늘어날 수 있습니다. |
| **스키마 디자인 및 액세스 패턴** | B-트리 깊이, 클러스터형 및 비클러스터형 인덱스 디자인, 페이지당 행 크기 및 밀도, 액세스 패턴(읽기/쓰기/삭제 작업)은 과도한 페이지 래치 경합에 기여할 수 있는 요소입니다. |
| **애플리케이션 수준의 높은 동시성** | 과도한 페이지 래치 경합은 일반적으로 애플리케이션 계층의 높은 동시 요청 수준과 함께 발생합니다. 특정 프로그래밍 방법으로 인해 특정 페이지에 대한 요청 수가 증가할 수도 있습니다. |
| **SQL Server 데이터베이스에서 사용되는 논리 파일의 레이아웃** | 논리 파일 레이아웃은 PFS(페이지 여유 공간), GAM(전역 할당 맵), SGAM(공유 전역 할당 맵), IAM(인덱스 할당 맵) 페이지 등의 할당 구조로 인한 페이지 래치 경합 수준에 영향을 줄 수 있습니다. 자세한 내용은 [TempDB 모니터링 및 문제 해결: 할당 병목 상태](https://techcommunity.microsoft.com/t5/sql-server/tempdb-monitoring-and-troubleshooting-allocation-bottleneck/ba-p/383516)를 참조하세요. |
| **I/O 하위 시스템 성능** | PAGEIOLATCH 대기가 상당히 높으면 SQL Server가 I/O 하위 시스템에서 대기하고 있음을 나타납니다. |

## <a name="diagnosing-sql-server-latch-contention"></a>SQL Server 래치 경합 진단

이 섹션에서는 SQL Server 래치 경합을 진단하여 환경에 문제가 되는지 확인하는 데 필요한 정보를 제공합니다.

### <a name="tools-and-methods-for-diagnosing-latch-contention"></a>래치 경합 진단 도구 및 방법

래치 경합을 진단하는 데 사용되는 기본 도구는 다음과 같습니다.

* 성능 모니터 - SQL Server 내의 CPU 사용률과 대기 시간을 모니터링하고 CPU 사용률과 래치 대기 시간 간에 관계가 있는지 여부를 설정합니다.

* SQL Server DMV - 이슈의 원인이 되는 특정 래치 유형과 영향을 받는 리소스를 확인하는 데 사용할 수 있습니다.

* Windows 디버깅 도구를 사용하여 SQL Server 프로세스의 메모리 덤프를 가져와 분석해야 하는 경우도 있습니다.

> [!NOTE]
> 이 수준의 고급 문제 해결은 일반적으로 비-버퍼 래치 경합 문제를 해결하는 경우에만 필요합니다. 해당 유형의 고급 문제 해결에는 Microsoft 기술 지원 서비스를 활용하는 것이 좋습니다.

래치 경합을 진단하는 기술 프로세스는 다음 단계로 요약할 수 있습니다.

1. 래치와 관련된 경합이 있는지 확인합니다.

2. [부록: SQL Server 래치 경합 스크립트](#appendix-sql-server-latch-contention-scripts)에 제공된 DMV 뷰를 사용하여 래치 유형 및 영향을 받는 리소스를 확인합니다.

3. [다양한 테이블 패턴의 래치 경합 처리](#handling-latch-contention-for-different-table-patterns)에 설명된 기술 중 하나를 사용하여 경합을 완화합니다.

### <a name="indicators-of-latch-contention"></a>래치 경합 지표

앞서 언급한 대로 래치 경합은 페이지 래치 획득과 관련된 경합 및 대기 시간으로 인해 CPU 리소스를 사용할 수 있는 경우에도 처리량이 증가하지 않는 경우에만 문제가 됩니다. 허용되는 경합 수준을 확인하려면 성능 및 처리량 요구 사항과 사용 가능한 I/O 및 CPU 리소스를 함께 고려하는 전체적인 접근 방식이 필요합니다. 이 섹션에서는 래치 경합이 워크로드에 미치는 영향을 확인하는 과정을 다음과 같이 안내합니다.

1. 대표 테스트 중에 전반적인 대기 시간을 측정합니다.

2. 순서대로 순위를 지정합니다.

3. 래치와 관련된 대기 시간의 비율을 확인합니다.

누적 대기 정보는 *sys.dm_os_wait_stats* DMV에서 확인할 수 있습니다. 가장 일반적인 유형의 래치 경합은 버퍼 래치 경합이며, *wait_type* **PAGELATCH\_\*** 인 래치의 대기 시간이 증가하는 것으로 관찰되었습니다. 비-버퍼 래치는 **LATCH\*** 대기 유형 아래에 그룹화되어 있습니다. 다음 다이어그램과 같이 먼저 *sys.dm_os_wait_stats* DMV에서 누적 시스템 대기를 살펴보고 버퍼 또는 비-버퍼 래치로 인한 전반적인 대기 시간의 비율을 확인해야 합니다. 비-버퍼 래치를 발견한 경우 *sys.dm_os_latch_stats* DMV도 검사해야 합니다.

다음 다이어그램에서는 *sys.dm_os_wait_stats* 및 *sys.dm_os_latch_stats* DMV에서 반환된 정보 간의 관계를 설명합니다.

![래치 대기](./media/diagnose-resolve-latch-contention/image7.png)

*sys.dm_os_wait_stats* DMV에 대한 자세한 내용은 SQL Server 도움말에서 [sys.dm_os_wait_stats(Transact-SQL)](./system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)를 참조하세요.

*sys.dm_os_latch_stats* DMV에 대한 자세한 내용은 SQL Server 도움말에서 [sys.dm_os_latch_stats(Transact-SQL)](./system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)를 참조하세요.

다음 래치 대기 시간 측정값은 과도한 래치 경합이 애플리케이션 성능에 영향을 주는 것을 나타내는 지표입니다.

* **평균 페이지 래치 대기 시간이 처리량과 함께 지속적으로 증가함**: 평균 페이지 래치 대기 시간이 처리량과 함께 지속적으로 증가하고 평균 버퍼 래치 대기 시간도 예상 디스크 응답 시간 이상으로 증가하는 경우 *sys.dm_os_waiting_tasks* DMV에서 현재 대기 중인 작업을 검사해야 합니다. 평균만 분리해서 분석할 경우 잘못된 결과가 도출될 수 있으므로 워크로드 특성을 파악하기 위해 가능하면 시스템을 라이브 상태로 살펴보는 것이 중요합니다. 특히 페이지에서 PAGELATCH_EX 및/또는 PAGELATCH_SH 요청의 대기가 높은지 여부를 확인합니다. 처리량과 함께 증가하는 평균 페이지 래치 대기 시간을 진단하려면 다음 단계를 수행합니다.

   * [세션 ID를 기준으로 정렬된 sys.dm_os_waiting_tasks 쿼리](#waiting-tasks-script1) 또는 [일정 기간의 대기 계산](#calculate-waits-over-a-time-period) 샘플 스크립트를 사용하여 현재 대기 중인 작업을 확인하고 평균 래치 대기 시간을 측정합니다. 
   * [버퍼 설명자를 쿼리하여 래치 경합을 유발하는 개체 확인](#query-buffer-descriptors) 샘플 스크립트를 사용하여 경합이 발생하는 인덱스 및 기본 테이블을 확인합니다. 
   * **MSSQL%InstanceName%\\대기 통계\\페이지 래치 대기\\평균 대기 시간** 성능 모니터 카운터를 사용하거나 *sys.dm_os_wait_stats* DMV를 실행하여 평균 페이지 래치 대기 시간을 측정합니다.

   > [!NOTE]
   > *sys.dm_os_wait_stats*에서 *wt_:type*으로 반환된 특정 대기 유형의 평균 대기 시간을 계산하려면 *wait_time_ms*로 반환된 총 대기 시간을 *waiting_tasks_count*로 반환된 대기 중인 작업 수로 나눕니다.

* **최대 부하 시간 동안 래치 대기 유형에서 소요된 총 대기 시간의 백분율**: 애플리케이션 부하에 따라 전반적인 대기 시간의 백분율인 평균 래치 대기 시간이 증가하는 경우 래치 경합이 성능에 영향을 줄 수 있으므로 조사해야 합니다.

   [SQLServer:Wait Statistics 개체](./performance-monitor/sql-server-wait-statistics-object.md) 성능 카운터를 사용하여 페이지 래치 대기와 비페이지 래치 대기를 측정합니다. 그런 다음, 성능 카운터의 값을 CPU, I/O, 메모리, 네트워크 처리량과 연결된 성능 카운터와 비교합니다. 예를 들어 트랜잭션/초 및 일괄 처리 요청/초는 리소스 사용률을 나타내는 두 가지 유용한 측정값입니다.

   > [!NOTE]
   > *sys.dm_os_wait_stats* DMV는 SQL Server 인스턴스가 마지막으로 시작되었거나 누적 대기 통계가 DBCC SQLPERF를 사용하여 다시 설정된 이후의 대기 시간을 측정하기 때문에 각 대기 유형의 상대 대기 시간은 이 DMV에 포함되지 않습니다. 각 대기 유형의 상대 대기 시간을 계산하려면 최대 부하 시간 이전과 최대 부하 시간 이후에 *sys.dm_os_wait_stats*의 스냅샷을 만들고 차이를 계산합니다. [일정 기간의 대기 계산](#calculate-waits-over-a-time-period) 샘플 스크립트를 이 용도로 사용할 수 있습니다.

   **비프로덕션 환경**에서만 다음 명령을 사용하여 *sys.dm_os_wait_stats* DMV를 지웁니다.
   
   ```sql
   dbcc SQLPERF ('sys.dm_os_wait_stats', 'CLEAR')
   ```
   유사한 명령을 실행하여 *sys.dm_os_latch_stats* DMV를 지울 수 있습니다.
   
   ```sql
   dbcc SQLPERF ('sys.dm_os_latch_stats', 'CLEAR')
   ```

* **애플리케이션 부하가 증가하고 SQL Server에서 사용할 수 있는 CPU 수가 증가함에 따라 처리량이 증가하지 않을 뿐 아니라 감소하는 경우도 있음**: 이 경우에 대해서는 [래치 경합 예제](#example-of-latch-contention)에서 설명했습니다.

* **애플리케이션 워크로드가 증가함에 따라 CPU 사용률이 증가하지 않음**: 애플리케이션 처리량 기반의 동시성이 증가함에 따라 시스템의 CPU 사용률이 증가하지 않는 경우 SQL Server가 어딘가에서 대기하고 있음을 나타내는 지표이며 래치 경합의 증상입니다.

근본 원인을 분석합니다. 위 조건이 각각 true인 경우에도 성능 이슈의 근본 원인은 다른 곳에 있을 수 있습니다. 실제로 대부분의 경우 최적화되지 않은 CPU 사용률은 잠금을 통한 차단, I/O 관련 대기 또는 네트워크 관련 이슈와 같은 다른 유형의 대기로 인해 발생합니다. 경험상, 심층 분석을 진행하기 전에 전반적인 대기 시간의 최대 비율을 나타내는 리소스 대기를 해결하는 것이 항상 가장 좋습니다.

## <a name="analyzing-current-wait-buffer-latches"></a>현재 대기 버퍼 래치 분석

버퍼 래치 경합은 *sys.dm_os_wait_stats* DMV에 표시된 것처럼 *wait_type*이 **PAGELATCH\_\*** 또는 **PAGEIOLATCH\_\*** 인 래치의 대기 시간 증가로 나타납니다. 시스템을 실시간으로 확인하려면 시스템에서 다음 쿼리를 실행하여 *sys.dm_os_wait_stats*, *sys.dm_exec_sessions*, *sys.dm_exec_requests* DMV에 참가합니다. 결과를 사용하여 서버에서 실행되는 세션의 현재 대기 유형을 확인할 수 있습니다.

```sql
SELECT wt.session_id, wt.wait_type
, er.last_wait_type AS last_wait_type
, wt.wait_duration_ms
, wt.blocking_session_id, wt.blocking_exec_context_id, resource_description
FROM sys.dm_os_waiting_tasks wt
JOIN sys.dm_exec_sessions es ON wt.session_id = es.session_id
JOIN sys.dm_exec_requests er ON wt.session_id = er.session_id
WHERE es.is_user_process = 1
AND wt.wait_type <> 'SLEEP_TASK'
ORDER BY wt.wait_duration_ms desc
```

![실행 중인 세션의 대기 유형](./media/diagnose-resolve-latch-contention/image8.png)

이 쿼리를 통해 노출되는 통계는 다음과 같습니다.

| 통계 | Description |
|---|---|
| **Session_id** | 태스크와 연결된 세션의 ID입니다. |
| **Wait_type** | SQL Server가 엔진에서 기록한 대기 유형으로, 현재 요청이 실행되지 않도록 차단합니다. |
| **Last_wait_type** | 이 요청이 이전에 차단된 경우 이 열은 마지막 대기의 유형을 반환합니다. Null을 허용하지 않습니다. |
| **Wait_duration_ms** | SQL Server 인스턴스가 시작된 이후 또는 누적 대기 통계가 다시 설정된 이후 이 대기 유형에서 대기하는 데 소요된 총 대기 시간(밀리초)입니다. |
| **Blocking_session_id** | 요청을 차단하고 있는 세션의 ID입니다. |
| **Blocking_exec_context_id** | 태스크와 연결된 실행 컨텍스트의 ID입니다. |
| **Resource_description** | resource_description 열에는 대기 중인 정확한 페이지가 `<database_id>:<file_id>:<page_id>` 형식으로 나열됩니다. |

다음 쿼리는 모든 비-버퍼 래치에 대한 정보를 반환합니다.

```sql
select * from sys.dm_os_latch_stats where latch_class <> 'BUFFER' order by wait_time_ms desc
```

![쿼리 출력](./media/diagnose-resolve-latch-contention/image9.png)

이 쿼리를 통해 노출되는 통계는 다음과 같습니다.

| 통계 | Description |
|---|---|
| **Latch_class** | SQL Server가 엔진에서 기록한 래치 유형으로, 현재 요청이 실행되지 않도록 차단합니다. |
| **Waiting_requests_count** | SQL Server가 다시 시작된 이후 이 클래스 래치의 대기 수입니다. 이 카운터는 래치 대기가 시작될 때 증가합니다. |
| **Wait_time_ms** | 이 래치 유형에서 대기하는 데 소요된 총 대기 시간(밀리초)입니다. |
| **Max_wait_time_ms** | 요청이 이 래치 유형에서 대기하는 데 소요한 최대 시간(밀리초)입니다. |

> [!NOTE]
> 이 DMV에서 반환되는 값은 마지막으로 서버를 다시 시작했거나 DMV를 다시 설정한 이후 누적된 값입니다. 즉, 오랜 시간 동안 실행된 시스템에서 *Max_wait_time_ms*와 같은 일부 통계는 거의 유용하지 않습니다. 다음 명령을 사용하여 이 DMV의 대기 통계를 다시 설정할 수 있습니다.
>
> ```sql
> DBCC SQLPERF ('sys.dm_os_latch_stats', CLEAR)
> ```

## <a name="sql-server-latch-contention-scenarios"></a>SQL Server 래치 경합 시나리오

다음 시나리오는 과도한 래치 경합을 유발하는 것으로 관찰되었습니다.

### <a name="last-pagetrailing-page-insert-contention"></a>마지막 페이지/후행 페이지 삽입 경합

일반적인 OLTP 방법은 ID 또는 날짜 열에 클러스터형 인덱스를 만드는 것입니다. 이렇게 하면 인덱스의 올바른 실제 구성을 유지 관리하는 데 도움이 되므로 인덱스에서 읽기 및 쓰기 성능을 훨씬 향상할 수 있습니다. 그러나 이 스키마 디자인에서는 실수로 래치 경합이 발생할 수 있습니다. 해당 이슈는 작은 행이 있는 큰 테이블, 오름차순 정수 또는 날짜/시간 키와 같이 순차적으로 증가하는 선행 키 열을 포함하는 인덱스에 삽입 등에서 가장 일반적으로 나타납니다. 이 시나리오에서 애플리케이션은 보관 작업을 제외하고 업데이트 또는 삭제 작업을 거의 수행하지 않습니다.

다음 예제에서 스레드 1과 스레드 2는 모두 299페이지에 저장되는 레코드를 삽입하려고 합니다. 논리적 잠금 관점에서는 행 수준 잠금이 사용되고 동일한 페이지의 두 레코드에 배타적 잠금을 동시에 유지할 수 있으므로 문제가 없습니다. 그러나 실제 메모리의 무결성을 보장하기 위해 한 번에 하나의 스레드만 배타적 래치를 획득할 수 있으므로 메모리의 업데이트 손실을 방지하기 위해 페이지에 대한 액세스가 직렬화됩니다. 이 예제에서는 스레드 1이 배타적 래치를 획득하고, 스레드 2는 대기 통계에 해당 리소스에 대한 PAGELATCH_EX 대기를 등록합니다. 이 대기는 *sys.dm_os_waiting_tasks* DMV에 *wait_type* 값으로 표시됩니다.

![마지막 행의 배타적 페이지 래치](./media/diagnose-resolve-latch-contention/image10.png)

이 충돌은 다음 다이어그램과 같이 B-트리의 맨 오른쪽 가장자리에서 발생하므로 일반적으로 “마지막 페이지 삽입” 경합이라고 합니다.

![마지막 페이지 삽입 경합](./media/diagnose-resolve-latch-contention/image11.png)

이 유형의 래치 경합은 다음과 같이 설명할 수 있습니다. 인덱스에 새 행을 삽입하면 SQL Server는 다음 알고리즘을 사용하여 수정을 실행합니다.

1. B-트리를 트래버스하여 새 레코드를 보관할 올바른 페이지를 찾습니다.

2. 페이지에 대한 PAGELATCH_EX 래치를 획득하여 다른 사용자가 페이지를 수정할 수 없도록 차단하고 모든 비-리프 페이지에 대한 공유 래치(PAGELATCH_SH)를 획득합니다.

   > [!NOTE]
   > 경우에 따라 SQL 엔진은 비-리프 B-트리 페이지에 대한 EX 래치도 획득해야 합니다. 예를 들어 페이지 분할이 발생하는 경우 직접 영향을 받는 모든 페이지에 대한 배타적 래치(PAGELATCH_EX)가 필요합니다.

3. 행이 수정된 로그 항목을 기록합니다.

4. 페이지에 행을 추가하고 페이지를 더티로 표시합니다.

5. 모든 페이지에 대한 래치를 해제합니다.

테이블 인덱스가 순차적으로 증가하는 키를 기반으로 하는 경우 페이지가 가득 찰 때까지 새 삽입은 동일한 페이지의 B-트리 끝에 추가됩니다. 이로 인해 높은 동시성 시나리오에서는 B-트리의 맨 오른쪽 가장자리와 클러스터형 인덱스 및 비클러스터형 인덱스에서 경합이 발생할 수 있습니다. 이 경합 유형의 영향을 받는 테이블은 주로 INSERT를 허용하며, 일반적으로 문제가 되는 인덱스 페이지는 비교적 밀도가 높습니다.(예를 들어 행 오버헤드를 포함하여 행 크기 \~165바이트는 페이지당 \~49행과 같습니다.) 삽입이 많은 이 예제에서는 PAGELATCH_EX/PAGELATCH_SH 대기가 발생할 것으로 예상되며, 일반적으로 관찰됩니다. 페이지 래치 대기와 트리 페이지 래치 대기를 비교해서 검사하려면 *sys.dm_db_index_operational_stats* DMV를 사용합니다.

다음 표에는 이 유형의 래치 경합과 함께 관찰된 주요 요소가 요약되어 있습니다.

| 요인 | 일반적인 관찰 |
|---|---|
| **SQL Server에서 사용 중인 논리 CPU** | 이 유형의 래치 경합은 주로 16개 이상의 CPU 코어 시스템에서 발생하며, 32개 이상의 CPU 코어 시스템에서 가장 일반적으로 나타납니다. |
| **스키마 디자인 및 액세스 패턴** | 트랜잭션 데이터 테이블의 인덱스에서 순차적으로 증가하는 ID 값을 선행 열로 사용합니다.<br/><br/>인덱스에는 증가하는 기본 키가 있으며, 높은 삽입 비율이 포함됩니다.<br/><br/>인덱스에 순차적으로 증가하는 열 값이 하나 이상 있습니다.<br/><br/>일반적으로 페이지당 많은 행이 있는 작은 행 크기입니다. |
| **관찰된 대기 유형** | 대기 기간을 기준으로 정렬된 sys.dm_os_waiting_tasks 쿼리에서 반환된 sys.dm_os_waiting_tasks DMV에서 동일한 resource_description과 연결된 배타적(EX) 또는 공유(SH) 래치 대기를 사용하여 동일한 리소스를 경합하는 많은 스레드를 관찰합니다. |
| **고려할 디자인 요소** | 삽입이 항상 B-트리 전체에 균일하게 분산되도록 할 수 있는 경우 비순차적 인덱스 완화 전략에 설명된 대로 인덱스 열의 순서를 변경하는 것이 좋습니다.<br/><br/>해시 파티션 완화 전략을 사용할 경우 슬라이딩 윈도우 보관과 같은 다른 모든 용도로 분할을 사용할 수 없게 됩니다.<br/><br/>해시 파티션 완화 전략을 사용하면 애플리케이션에서 사용되는 SELECT 쿼리에 대해 파티션 제거 문제가 발생할 수 있습니다. |

### <a name="latch-contention-on-small-tables-with-a-non-clustered-index-and-random-inserts-queue-table"></a>비클러스터형 인덱스 및 임의 삽입이 있는 작은 테이블에 대한 래치 경합(큐 테이블)

이 시나리오는 일반적으로 SQL 테이블이 임시 큐로 사용되는 경우(예: 비동기 메시징 시스템)에 나타납니다.

이 시나리오에서는 다음 조건에서 배타적(EX) 및 공유(SH) 래치 경합이 발생할 수 있습니다.

* 높은 동시성에서 삽입, 선택, 업데이트 또는 삭제 작업이 수행됩니다.
* 행 크기가 비교적 작습니다(덴스 페이지 생성).
* 테이블의 행 수가 비교적 적어 인덱스 깊이가 2 또는 3으로 정의된 단순 B-트리가 생성됩니다.

> [!NOTE]
> DML(데이터 조작 언어) 빈도와 시스템 동시성이 충분히 높으면 깊이가 이보다 큰 B-트리의 경우에도 이 유형의 액세스 패턴에서 경합이 발생할 수 있습니다. 시스템에서 16개 이상의 CPU 코어를 사용할 수 있는 경우 동시성이 증가함에 따라 래치 경합 수준도 높아질 수 있습니다.

비순차적 열이 클러스터형 인덱스의 선행 키인 경우와 같이 B-트리에서 액세스가 무작위로 수행되는 경우에도 래치 경합이 발생할 수 있습니다. 다음 스크린샷은 이 유형의 래치 경합이 발생하는 시스템에서 만든 것입니다. 이 예제에서는 작은 행 크기와 비교적 단순한 B-트리로 인한 페이지 밀도 때문에 경합이 발생합니다. 동시성이 증가함에 따라, GUID가 인덱스의 선행 열이기 때문에 B-트리에서 삽입이 무작위로 수행되는 경우에도 페이지에 대한 래치 경합이 발생합니다.

다음 스크린샷에서는 버퍼 데이터 페이지 및 PFS(페이지 여유 공간) 페이지에서 대기가 발생합니다. PFS 페이지 래치 경합에 대한 자세한 내용은 SQLSkills에서 다음 타사 블로그 게시물을 참조하세요. [벤치마킹: SSD의 여러 데이터 파일](https://www.sqlskills.com/blogs/paul/benchmarking-multiple-data-files-on-ssds-plus-the-latest-fusion-io-driver/). 데이터 파일 수가 증가한 경우에도 버퍼 데이터 페이지에서 래치 경합이 많이 발생했습니다.

![대기 형식](./media/diagnose-resolve-latch-contention/image12.png)

다음 표에는 이 유형의 래치 경합과 함께 관찰된 주요 요소가 요약되어 있습니다.

| 요인 | 일반적인 관찰 |
|---|---|
| **SQL Server에서 사용 중인 논리 CPU** | 래치 경합은 주로 16개 이상의 CPU 코어가 있는 컴퓨터에서 발생합니다.
| **스키마 디자인 및 액세스 패턴** | 작은 테이블에 대한 삽입/선택/업데이트/삭제 액세스 패턴의 높은 비율<br/><br/>단순 B-트리(인덱스 깊이가 2 또는 3임)<br/><br/>작은 행 크기(페이지당 많은 레코드)
| **동시성 수준** | 래치 경합은 애플리케이션 계층의 동시 요청 수준이 높은 경우에만 발생합니다.
| **관찰된 대기 유형** | 루트 분할로 인해 버퍼(PAGELATCH_EX 및 PAGELATCH_SH) 및 비-버퍼 래치 ACCESS_METHODS_HOBT_VIRTUAL_ROOT에서 대기를 관찰합니다. 또한 PFS 페이지에서 PAGELATCH_UP 대기를 관찰합니다. 비-버퍼 래치 대기에 대한 자세한 내용은 SQL Server 도움말에서 [sys.dm_os_latch_stats(Transact-SQL)](./system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)를 참조하세요.

인덱스에 단순 B-트리와 무작위 삽입을 함께 사용할 경우 B-트리에서 페이지 분할이 발생하기 쉽습니다. 페이지 분할을 수행하려면 SQL Server가 모든 수준에서 공유(SH) 래치를 획득한 다음, 페이지 분할에 관련된 B-트리 페이지에 대한 배타적(EX) 래치를 획득해야 합니다. 동시성이 높고 데이터가 지속적으로 삽입 및 삭제되는 경우에도 B-트리 루트 분할이 발생할 수 있습니다. 예제에서는 다른 삽입이 B-트리에 대한 비-버퍼 래치가 획득될 때까지 기다려야 할 수 있습니다. 이 사항은 *sys.dm_os_latch_stats* DMV에서 관찰된 ACCESS_METHODS_HBOT_VIRTUAL_ROOT 래치 유형의 대기 수가 많은 것에서 확인할 수 있습니다.

다음 스크립트를 수정하여 영향을 받는 테이블 인덱스의 B-트리 깊이를 확인할 수 있습니다.

```sql
select o.name as [table],
   i.name as [index],
   indexProperty(object_id(o.name), i.name, 'indexDepth')
   + indexProperty(object_id(o.name), i.name, 'isClustered') as depth, --clustered index depth reported doesn't count leaf level
   i.[rows] as [rows],
   i.origFillFactor as [fillFactor],
   case (indexProperty(object_id(o.name), i.name, 'isClustered'))
      when 1 then 'clustered'
      when 0 then 'nonclustered'
      else 'statistic'
   end as type
from sysIndexes i
join sysObjects o on o.id = i.id
where o.type = 'u'
   and indexProperty(object_id(o.name), i.name, 'isHypothetical') = 0 --filter out hypothetical indexes
   and indexProperty(object_id(o.name), i.name, 'isStatistics') = 0 --filter out statistics
order by o.name
```

### <a name="latch-contention-on-page-free-space-pfs-pages"></a>PFS(페이지 여유 공간) 페이지의 래치 경합

PFS는 Page Free Space의 약어로, SQL Server는 각 데이터베이스 파일의 모든 8088페이지(PageID = 1부터 시작)에 대해 PFS 1페이지를 할당합니다. PFS 페이지의 각 바이트는 페이지의 여유 공간 크기, 페이지가 할당되었는지 여부, 페이지에 고스트 레코드가 저장되는지 여부를 비롯한 정보를 기록합니다. PFS 페이지에는 삽입 또는 업데이트 작업에 새 페이지가 필요할 때 할당할 수 있는 페이지에 대한 정보가 포함됩니다. 페이지를 할당 또는 할당 취소하는 경우를 포함하여 다양한 시나리오에서 PFS 페이지를 업데이트해야 합니다. PFS 페이지를 보호하려면 업데이트(UP) 래치를 사용해야 하므로, 파일 그룹의 데이터 파일 수가 비교적 적고 CPU 코어 수가 많은 경우 PFS 페이지에서 래치 경합이 발생할 수 있습니다. 이 문제를 해결하는 간단한 방법은 파일 그룹당 파일 수를 늘리는 것입니다.

> [!WARNING]
> 파일 그룹당 파일 수를 늘리면 메모리를 디스크에 분산하는 많은 대규모 정렬 작업을 포함하는 부하와 같은 특정 부하의 성능이 저하될 수 있습니다.

tempdb의 PFS 또는 SGAM 페이지에 대해 많은 PAGELATCH_UP 대기가 관찰되는 경우 다음 단계를 완료하여 이 병목 상태를 제거합니다.

1. tempdb 데이터 파일 수가 서버의 프로세서 코어 수와 같도록 tempdb에 데이터 파일을 추가합니다.

2. SQL Server 추적 플래그 1118을 사용하도록 설정합니다.

시스템 페이지의 경합으로 인한 할당 병목 상태에 대한 자세한 내용은 [할당 병목 상태란?](https://techcommunity.microsoft.com/t5/sql-server/what-is-allocation-bottleneck/ba-p/383513) 블로그 게시물을 참조하세요.

### <a name="table-valued-functions-and-latch-contention-on-tempdb"></a>tempdb의 테이블 반환 함수 및 래치 경합

할당 경합 외에도 쿼리 내에서 TVF를 많이 사용하는 경우와 같이 tempdb에서 래치 경합을 유발할 수 있는 다른 요소가 있습니다.

## <a name="handling-latch-contention-for-different-table-patterns"></a>다양한 테이블 패턴의 래치 경합 처리

다음 섹션에서는 과도한 래치 경합과 관련된 성능 이슈를 해결하는 데 사용할 수 있는 기술에 대해 설명합니다.

### <a name="use-a-non-sequential-leading-index-key"></a>비순차적 선행 인덱스 키 사용

래치 경합을 처리하는 한 가지 방법은 순차적 인덱스 키를 순차적이지 않은 키로 바꿔 인덱스 범위에서 삽입을 균등하게 분산하는 것입니다.

일반적으로 워크로드를 비례 분산하는 선행 열을 인덱스에 사용하면 됩니다. 다음 몇 가지 옵션이 있습니다.

#### <a name="option-use-a-column-within-the-table-to-distribute-values-across-the-index-key-range"></a>옵션: 테이블 내의 열을 사용하여 인덱스 키 범위에 값 분산

키 범위에 삽입을 분산하는 데 사용할 수 있는 자연 값에 대해 워크로드를 평가합니다. 예를 들어 ATM 뱅킹 시나리오를 고려해 보세요. 이 경우에는 한 고객이 한 번에 하나의 ATM만 사용할 수 있기 때문에 인출 트랜잭션 테이블에 삽입을 분산하는 데 ATM_ID가 적합할 수 있습니다. 마찬가지로, POS(Point of Sale) 시스템에서는 Checkout_ID 또는 스토어 ID가 키 범위에 삽입을 분산하는 데 사용할 수 있는 자연 값이 됩니다. 이 기술을 사용하려면 선행 키 열이 식별된 열의 값이거나, 고유성을 제공하기 위해 해당 값의 일부 해시가 하나 이상의 추가 열과 결합된 복합 인덱스 키를 만들어야 합니다. 고유 값이 너무 많아도 부적절한 물리적 구성이 생성되므로, 대부분의 경우 값 해시가 가장 효과적입니다. 예를 들어 POS(Point of Sale) 시스템에서는 CPU 코어 수에 맞게 조정되는 모듈로인 스토어 ID를 통해 해시를 만들 수 있습니다. 이 기술을 사용하면 생성되는 테이블 내의 범위 수가 비교적 적지만 래치 경합 방지를 위해 삽입을 분산하기에 충분합니다. 다음 이미지는 이 기술을 보여 줍니다.

![비순차적 인덱스를 적용한 후의 삽입](./media/diagnose-resolve-latch-contention/image14.png)

> [!IMPORTANT]
> 이 패턴은 기존의 인덱싱 모범 사례와 일치하지 않습니다. 이 기술은 B-트리에 삽입을 균일하게 분산하는 데 도움이 되지만 애플리케이션 수준에서 스키마를 변경해야 할 수도 있습니다. 또한 이 패턴은 클러스터형 인덱스를 활용하는 범위 검사가 필요한 쿼리의 성능에 부정적인 영향을 줄 수 있습니다. 워크로드 패턴을 분석하여 이 디자인 방법이 효과적인지 확인해야 합니다. 삽입 처리량 및 스케일링을 위해 어느 정도의 순차적 검사 성능 저하를 감수할 수 있는 경우에만 이 패턴을 구현해야 합니다.

이 패턴은 성능 랩 참여 과정에서 구현되었으며, 32개의 물리적 CPU 코어가 있는 시스템에서 래치 경합을 해결했습니다. 테이블을 사용하여 트랜잭션 종료 시 마감 잔액을 저장했으며, 각 비즈니스 트랜잭션은 테이블에 단일 삽입 작업을 수행했습니다.

**원래 테이블 정의**

원래 테이블 정의를 사용할 경우 클러스터형 인덱스 pk_table1에서 과도한 래치 경합이 발생하는 것으로 관찰되었습니다.

```sql
create table table1
(
       TransactionID bigint not null,
       UserID      int not null,
       SomeInt       int not null
)
go

alter table table1
       add constraint pk_table1
       primary key clustered (TransactionID, UserID)
go
```

> [!NOTE]
> 테이블 정의의 개체 이름이 원래 값에서 변경되었습니다.

**다시 정렬된 인덱스 정의**

사용자 ID를 기본 키의 선행 열로 사용하여 인덱스를 다시 정렬하면 삽입이 여러 페이지에 거의 무작위로 분산되었습니다. 모든 사용자가 동시에 온라인 상태는 아니기 때문에 최종 분산이 100% 무작위는 아니었지만, 과도한 래치 경합을 완화하기에 충분히 무작위로 분산되었습니다. 인덱스 정의를 다시 정렬할 때의 한 가지 주의 사항은 이 테이블에 대한 모든 select 쿼리를 수정하여 UserID와 TransactionID 둘 다를 같음 조건자로 사용해야 한다는 것입니다.

> [!IMPORTANT]
> 프로덕션 환경에서 실행하기 전에 테스트 환경에서 변경 내용을 철저하게 테스트해야 합니다.

```sql
create table table1
(
       TransactionID bigint not null,
       UserID      int not null,
       SomeInt       int not null
)
go

alter table table1
       add constraint pk_table1
       primary key clustered (UserID, TransactionID)
go
```

**기본 키의 선행 열로 해시 값 사용**

다음 테이블 정의를 사용하여 CPU 수에 맞게 조정되는 모듈로를 생성할 수 있습니다. 순차적으로 증가하는 TransactionID 값으로 HashValue를 생성하여 B-트리에 균일하게 분산되도록 합니다.

```sql
create table table1
(
       TransactionID bigint not null,
       UserID      int not null,
       SomeInt       int not null
)
go
-- Consider using bulk loading techniques to speed it up
ALTER TABLE table1
   ADD [HashValue] AS (CONVERT([tinyint], abs([TransactionID])%(32))) PERSISTED NOT NULL   
alter table table1
       add constraint pk_table1
       primary key clustered (HashValue, TransactionID, UserID)
go
```

#### <a name="option-use-a-guid-as-the-leading-key-column-of-the-index"></a>옵션: 인덱스의 선행 키 열로 GUID 사용

자연 구분 기호가 없는 경우 GUID 열을 인덱스의 선행 키 열로 사용하여 삽입이 균일하게 분산되도록 할 수 있습니다. GUID를 인덱스 키의 선행 열로 사용하는 방법을 선택하면 다른 기능에 분할을 사용할 수 있는 반면 페이지 분할 증가, 부적절한 물리적 구성, 낮은 페이지 밀도 등의 잠재적 단점이 나타날 수도 있습니다.

> [!NOTE]
> GUID를 인덱스의 선행 키 열로 사용하는 것은 논란의 여지가 많은 주제입니다. 이 방법의 장단점에 대한 자세한 논의는 이 문서에서 다루지 않습니다.

### <a name="use-hash-partitioning-with-a-computed-column"></a>계산 열을 통한 해시 분할 사용

SQL Server 내의 테이블 분할을 사용하여 과도한 래치 경합을 완화할 수 있습니다. 일반적인 방법은 분할된 테이블의 계산 열을 사용하여 해시 파티션 구성표를 만드는 것으로, 다음 단계를 수행하면 됩니다.

1. 새 파일 그룹을 만들거나 기존 파일 그룹을 사용하여 파티션을 보관합니다.

2. 새 파일 그룹을 사용하는 경우 LUN에서 개별 파일의 균형을 동일하게 유지하면서 최적 레이아웃을 사용합니다. 액세스 패턴에서 삽입 비율이 높은 경우 SQL Server 컴퓨터의 물리적 CPU 코어 수와 동일한 개수의 파일을 생성해야 합니다.

3. **CREATE PARTITION FUNCTION** 명령을 사용하여 테이블을 *X*개 파티션으로 분할합니다. 여기서 *X*는 SQL Server 컴퓨터의 물리적 CPU 코어 수입니다. (32개 이상 파티션)

   > [!NOTE]
   > CPU 코어 수와 파티션 수가 항상 1:1로 일치해야 하는 것은 아닙니다. 대부분의 경우 CPU 코어 수보다 작은 값이면 됩니다. 파티션 수가 많을수록 모든 파티션을 검색해야 하는 쿼리의 오버헤드가 증가할 수 있으므로, 이 경우에는 파티션 수가 더 적은 것이 도움이 됩니다. 실제 고객 워크로드를 사용하여 64개 및 128개 논리 CPU 시스템에서 수행한 SQLCAT 테스트에서는 32개 파티션만 있으면 과도한 래치 경합을 해결하고 스케일링 목표에 도달하기에 충분했습니다. 궁극적으로 이상적인 파티션 수는 테스트를 통해 결정해야 합니다. 

4. **CREATE PARTITION SCHEME** 명령을 사용합니다.

   * 파티션 함수를 파일 그룹에 바인딩합니다. 
   * tinyint 또는 smallint 형식의 해시 열을 테이블에 추가합니다. 
   * 적절한 해시 분포를 계산합니다. 예를 들어 모듈로 또는 binary_checksum과 함께 hashbytes를 사용합니다.

다음 샘플 스크립트를 구현 목적에 맞게 사용자 지정할 수 있습니다.

```sql
--Create the partition scheme and function, align this to the number of CPU cores 1:1 up to 32 core computer
-- so for below this is aligned to 16 core system
CREATE PARTITION FUNCTION [pf_hash16] (tinyint) AS RANGE LEFT FOR VALUES
   (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15)

CREATE PARTITION SCHEME [ps_hash16] AS PARTITION [pf_hash16] ALL TO ( [ALL_DATA] )
-- Add the computed column to the existing table (this is an OFFLINE operation)

-- Consider using bulk loading techniques to speed it up
ALTER TABLE [dbo].[latch_contention_table]
   ADD [HashValue] AS (CONVERT([tinyint], abs(binary_checksum([hash_col])%(16)),(0))) PERSISTED NOT NULL

--Create the index on the new partitioning scheme 
CREATE UNIQUE CLUSTERED INDEX [IX_Transaction_ID] 
ON [dbo].[latch_contention_table]([T_ID] ASC, [HashValue]) 
ON ps_hash16(HashValue)
```

이 스크립트를 사용하여 [마지막 페이지/후행 페이지 삽입 경합](#last-pagetrailing-page-insert-contention)으로 인한 문제가 발생한 테이블을 해시 분할할 수 있습니다. 이 기술은 테이블을 분할하고 해시 값 모듈러스 연산으로 여러 테이블 파티션에 삽입을 분산하여 마지막 페이지에서 다른 곳으로 경합을 이동합니다.

#### <a name="what-hash-partitioning-with-a-computed-column-does"></a>계산 열을 통한 해시 분할이 수행하는 작업

다음 다이어그램과 같이 이 기술은 해시 함수의 인덱스를 다시 작성하고 SQL Server 컴퓨터의 물리적 CPU 코어 수와 동일한 개수의 파티션을 만들어 마지막 페이지에서 다른 곳으로 경합을 이동합니다. 삽입은 여전히 논리 범위의 끝(순차적으로 증가하는 값)에 추가되지만, 해시 값 모듈러스 연산을 통해 삽입이 여러 B-트리에 분할되도록 하여 병목 상태를 완화합니다. 다음 다이어그램은 이 내용을 그림으로 표현한 것입니다.

![마지막 페이지 삽입의 페이지 래치 경합](./media/diagnose-resolve-latch-contention/image16.png)

![분할을 사용하여 해결된 페이지 래치 충돌](./media/diagnose-resolve-latch-contention/image17.png)

#### <a name="trade-offs-when-using-hash-partitioning"></a>해시 분할을 사용할 경우의 장단점

해시 분할은 삽입의 경합을 제거할 수 있지만, 이 기술의 사용 여부를 결정할 때 고려해야 하는 몇 가지 장단점이 있습니다.

* 대부분의 경우 조건자에 해시 파티션을 포함하고, 이 쿼리를 실행할 때 파티션 제거를 제공하지 않는 쿼리 계획을 생성하도록 select 쿼리를 수정해야 합니다. 다음 스크린샷은 해시 분할이 구현된 후에 파티션 제거가 없는 부적절한 계획을 보여 줍니다.

   ![파티션 제거가 없는 쿼리 계획](./media/diagnose-resolve-latch-contention/image18.png)

* 범위 기반 보고서와 같은 다른 특정 쿼리에서 파티션을 제거할 수 없게 합니다.

* 해시 분할된 테이블을 다른 테이블에 조인하는 경우 파티션을 제거하려면 두 번째 테이블을 동일한 키에서 해시 분할해야 하며, 해시 키가 조인 조건의 일부여야 합니다.

* 해시 분할은 슬라이딩 윈도우 보관, 파티션 전환 기능 등의 다른 관리 기능에 분할을 사용할 수 없도록 합니다.

해시 분할은 삽입의 경합을 완화하여 전반적인 시스템 처리량을 늘리기 때문에 과도한 래치 경합을 완화하는 효과적인 전략입니다. 몇 가지 장단점이 있으므로 일부 액세스 패턴에는 최적 솔루션이 아닐 수도 있습니다.

## <a name="summary-of-techniques-used-to-address-latch-contention"></a>래치 경합을 해결하는 데 사용되는 기술 요약

다음 두 섹션에는 과도한 래치 경합을 해결하는 데 사용할 수 있는 기술이 요약되어 있습니다.

### <a name="non-sequential-keyindex"></a>비순차적 키/인덱스

**장점:**

* 슬라이딩 윈도우 구성표를 사용한 데이터 보관, 파티션 전환 기능 등의 다른 분할 기능을 사용할 수 있습니다.

**단점:**

* 항상 삽입이 ‘충분히’ 균일하게 분산되도록 키/인덱스를 선택하기 어려울 수 있습니다.
* GUID를 선행 열로 사용하여 균일하게 분산되도록 할 수 있지만, 과도한 페이지 분할 작업이 발생할 수 있다는 것에 주의해야 합니다.
* B-트리에 무작위로 삽입하는 경우 페이지 분할 작업이 너무 많이 생성되어 비-리프 페이지에서 래치 경합이 발생할 수 있습니다.

### <a name="hash-partitioning-with-computed-column"></a>계산 열을 통한 해시 분할

**장점:**

* 삽입에 대해 투명하게 적용됩니다.

**단점:**

* 파티션 전환 옵션을 사용한 데이터 보관 등의 의도한 관리 기능에 분할을 사용할 수 없습니다.
* 개별 및 범위 기반 선택/업데이트를 포함하는 쿼리와 조인을 수행하는 쿼리에 대해 파티션 제거 이슈를 유발할 수 있습니다.
* 지속형 계산 열 추가는 오프라인 작업입니다.

> [!TIP]
> 추가 기술에 대해서는 [PAGELATCH_EX 대기 및 과도한 삽입](https://techcommunity.microsoft.com/t5/sql-server/pagelatch-ex-waits-and-heavy-inserts/ba-p/384289) 블로그 게시물을 참조하세요.

## <a name="walkthrough-diagnose-a-latch-contention"></a>연습: 래치 경합 진단

다음 연습에서는 [SQL Server 래치 진단](#diagnosing-sql-server-latch-contention) 및 [다양한 테이블 패턴의 래치 경합 처리](#handling-latch-contention-for-different-table-patterns)에 설명된 도구와 기술을 사용하여 실제 시나리오에서 문제를 해결하는 방법을 보여 줍니다. 이 시나리오에서는 256GB 메모리가 있는 8소켓, 32개 물리적 코어 시스템에서 실행되는 SQL Server 애플리케이션에 대해 트랜잭션을 수행하는 약 8,000개 스토어를 시뮬레이트한 POS(Point of Sale) 시스템의 부하 테스트를 수행하는 고객 참여에 대해 설명합니다.

다음 다이어그램은 POS(Point of Sale) 시스템을 테스트하는 데 사용되는 하드웨어를 자세히 설명합니다.

![POS(Point of Sale) 시스템 테스트 환경](./media/diagnose-resolve-latch-contention/image19.png)

### <a name="symptom-hot-latches"></a>증상: 핫 래치

이 예제에서는 PAGELATCH_EX의 대기가 높은 것으로 관찰되었습니다. 여기서 높음은 일반적으로 평균 1ms 초과로 정의됩니다. 예제에서는 지속적으로 대기가 20ms를 초과하는 것이 관찰되었습니다.

![핫 래치](./media/diagnose-resolve-latch-contention/image20.png)

래치 경합이 문제가 된다고 결정한 후 래치 경합을 유발하는 원인을 확인하려고 했습니다.

### <a name="isolating-the-object-causing-latch-contention"></a>래치 경합을 유발하는 개체 격리

다음 스크립트는 resource_description 열을 사용하여 PAGELATCH_EX 경합을 유발하는 인덱스를 격리합니다.

> [!NOTE]
> 이 스크립트에서 반환된 resource_description 열은 리소스 설명을 \<DatabaseID,FileID,PageID\> 형식으로 제공합니다. 여기서 DatabaseID와 연결된 데이터베이스 이름은 DB_NAME () 함수에 DatabaseID 값을 전달하여 확인할 수 있습니다.

```sql
SELECT wt.session_id, wt.wait_type, wt.wait_duration_ms           
, s.name AS schema_name           
, o.name AS object_name           
, i.name AS index_name           
FROM sys.dm_os_buffer_descriptors bd 
JOIN (           
  SELECT *
    --resource_description          
  , CHARINDEX(':', resource_description) AS file_index            
  , CHARINDEX(':', resource_description, CHARINDEX(':', resource_description)+1) AS page_index  
  , resource_description AS rd           
  FROM sys.dm_os_waiting_tasks wt           
  WHERE wait_type LIKE 'PAGELATCH%'                      
  ) AS wt           
    ON bd.database_id = SUBSTRING(wt.rd, 0, wt.file_index)           
    AND bd.file_id = SUBSTRING(wt.rd, wt.file_index+1, 1) --wt.page_index)           
    AND bd.page_id = SUBSTRING(wt.rd, wt.page_index+1, LEN(wt.rd))
JOIN sys.allocation_units au ON bd.allocation_unit_id = au.allocation_unit_id
JOIN sys.partitions p ON au.container_id = p.partition_id
JOIN sys.indexes i ON  p.index_id = i.index_id AND p.object_id = i.object_id
JOIN sys.objects o ON i.object_id = o.object_id 
JOIN sys.schemas s ON o.schema_id = s.schema_id
order by wt.wait_duration_ms desc
```

여기에 표시된 대로 LATCHTEST 테이블과 CIX_LATCHTEST 인덱스 이름에서 경합이 발생합니다. 워크로드를 익명화하기 위해 이름이 변경된 것을 확인합니다.

![LATCHTEST 경합](./media/diagnose-resolve-latch-contention/image21.png)

반복적으로 폴링하고 임시 테이블을 사용하여 구성 가능한 기간의 총 대기 시간을 확인하는 고급 스크립트에 대해서는 부록의 [버퍼 설명자를 쿼리하여 래치 경합을 유발하는 개체 확인](#query-buffer-descriptors)을 참조하세요.

### <a name="alternative-technique-to-isolate-the-object-causing-latch-contention"></a>래치 경합을 유발하는 개체를 격리하기 위한 대체 기술

*sys.dm_os_buffer_descriptors* 쿼리가 비실용적인 경우도 있습니다. 버퍼 풀에서 사용할 수 있는 시스템 메모리가 증가하면 이 DMV를 실행하는 데 필요한 시간도 늘어납니다. 256GB 시스템에서 이 DMV를 실행하려면 10분 이상 걸릴 수 있습니다. 사용 가능한 대체 기술은 다음과 같이 간략하게 소개할 수 있으며, 랩에서 실행한 다른 워크로드를 사용하여 설명합니다.

1. [대기 기간을 기준으로 정렬된 sys.dm_os_waiting_tasks 쿼리](#waiting-tasks-script2) 부록 스크립트를 사용하여 현재 대기 중인 작업을 쿼리합니다.

2. 여러 스레드가 동일한 페이지에서 경합할 때 발생하는 호위(convoy)가 관찰된 키 페이지를 확인합니다. 이 예제에서 삽입을 수행하는 스레드는 B-트리의 후행 페이지에서 경합하며, EX 래치를 획득할 수 있을 때까지 기다립니다. 이 사항은 첫 번째 쿼리의 resource_description을 통해 확인할 수 있습니다(예제에서는 8:1:111305).

3. DBCC PAGE를 통해 페이지에 대한 추가 정보를 표시하는 추적 플래그 3604를 다음 구문으로 사용하도록 설정합니다. resource_description을 통해 얻은 값으로 괄호 안의 값을 대체합니다.

   ```sql
   --enable trace flag 3604 to enable console output
   dbcc traceon (3604)

   --examine the details of the page
   dbcc page (8,1, 111305, -1)
   ```

4. DBCC 출력을 검사합니다. 연결된 메타데이터 ObjectID가 있어야 합니다(예제에서는 ‘78623323’).

   ![메타데이터 ObjectID](./media/diagnose-resolve-latch-contention/image22.png)

5. 이제 다음 명령을 실행하여 경합을 유발하는 개체의 이름을 확인할 수 있습니다. 예상대로 LATCHTEST입니다.
   
   > [!NOTE]
   > 올바른 데이터베이스 컨텍스트에 있는지 확인합니다. 그렇지 않으면 쿼리가 NULL을 반환합니다.

   ```sql
   --get object name
   select OBJECT_NAME (78623323)
   ```

   ![개체 이름](./media/diagnose-resolve-latch-contention/image23.png)

### <a name="summary-and-results"></a>요약 및 결과

위 기술을 사용하면, 압도적으로 가장 많은 개수의 삽입을 받은 테이블에서 순차적으로 증가하는 키 값을 통해 클러스터형 인덱스에 경합이 발생했음을 확인할 수 있었습니다. 날짜/시간, ID 또는 애플리케이션에서 생성된 transactionID와 같은 순차적으로 증가하는 키 값이 있는 인덱스에서는 이 유형의 경합이 자주 발생합니다.

해당 이슈를 해결하기 위해 [계산 열을 통한 해시 분할](#use-hash-partitioning-with-a-computed-column)을 사용했으며 690% 성능 향상이 관찰되었습니다. 다음 표에는 계산 열을 통한 해시 분할을 구현하기 전후의 애플리케이션 성능이 요약되어 있습니다. 래치 경합 병목 상태가 제거된 후 CPU 사용률이 처리량과 함께 예상대로 크게 증가합니다.

| 측정 | 해시 분할 이전 | 해시 분할 이후 |
|---|---|---|
| 비즈니스 트랜잭션/초 | 36 | 249 |
| 평균 페이지 래치 대기 시간 | 36밀리초 | 0.6밀리초 |
| 래치 대기/초 | 9,562 | 2,873 |
| SQL 프로세서 시간 | 24% | 78% |
| SQL 일괄 처리 요청/초 | 12,368 | 47,045 |

위의 표에서 볼 수 있듯이 과도한 페이지 래치 경합으로 인한 성능 이슈를 올바르게 확인하고 해결하면 전반적인 애플리케이션 성능에 긍정적인 영향을 줄 수 있습니다.

## <a name="appendix-alternate-technique"></a>부록: 대체 기술

과도한 페이지 래치 경합을 방지하는 한 가지 가능한 전략은 각 행에 CHAR 열을 패딩하여 각 행이 전체 페이지를 사용하도록 하는 것입니다. 이 전략은 전반적인 데이터 크기가 작고, 다음과 같은 요소가 결합되어 발생하는 EX 페이지 래치 경합을 처리해야 하는 경우에 사용할 수 있는 옵션입니다.

* 작은 행 크기 
* 단순 B-트리 
* 무작위 삽입, 선택, 업데이트, 삭제 작업의 비율이 높은 액세스 패턴 
* 임시 큐 테이블 등의 작은 테이블 

전체 페이지를 차지하도록 행을 패딩하여 SQL에서 추가 페이지를 할당하게 함으로써 삽입에 사용할 수 있는 페이지를 늘리고 EX 페이지 래치 경합을 줄입니다.

### <a name="padding-rows-to-ensure-each-row-occupies-a-full-page"></a>각 행이 전체 페이지를 차지하도록 행 패딩

다음과 유사한 스크립트를 사용하여 전체 페이지를 차지하도록 행을 패딩할 수 있습니다.

```sql
ALTER TABLE mytable ADD Padding CHAR(5000) NOT NULL DEFAULT ('X')
```

> [!NOTE]
> 페이지당 한 행을 강제 적용하는 가능한 가장 작은 char를 사용하여 패딩 값에 대한 추가 CPU 요구 사항과 행을 기록하는 데 필요한 추가 공간을 줄입니다. 고성능 시스템에서는 모든 1바이트가 중요합니다.

이 기술은 완전한 설명을 위해 포함되었을 뿐이며, 실제로 SQLCAT는 단일 성능 참여에서 10,000행이 포함된 작은 테이블에서만 해당 기술을 사용했습니다. 이 기술은 큰 테이블에 대한 SQL Server의 메모리 압력을 늘리고 비-리프 페이지에서 비-버퍼 래치 경합을 유발할 수 있기 때문에 기술의 응용이 제한됩니다. 추가 메모리 압력은 기술의 응용을 제한하는 중요한 요소가 될 수 있습니다. 최신 서버에서 사용할 수 있는 메모리 양을 감안할 때 OLTP 워크로드에 대한 작업 집합의 상당 부분은 일반적으로 메모리에 유지됩니다. 데이터 세트가 더 이상 메모리에 들어가지 않는 크기까지 증가하면 성능이 급락합니다. 따라서 이 기술은 작은 테이블에만 적용할 수 있는 옵션입니다. SQLCAT는 큰 테이블에 대한 마지막 페이지/후행 페이지 삽입 경합 등의 시나리오에 이 기술을 사용하지 않습니다.

> [!IMPORTANT]
> 이 전략을 사용할 경우 B-트리의 비-리프 수준에서 많은 페이지 분할이 발생할 수 있으므로 ACCESS_METHODS_HBOT_VIRTUAL_ROOT 래치 유형의 대기 수가 많을 수 있습니다. 이 경우에는 SQL Server가 모든 수준에서 공유(SH) 래치를 획득한 다음, 페이지 분할이 가능한 B-트리의 페이지에 대한 배타적(EX) 래치를 획득해야 합니다. 행을 패딩한 후 *sys.dm_os_latch_stats* DMV에서 ACCESS_METHODS_HBOT_VIRTUAL_ROOT 래치 유형의 대기 수가 많은지 확인합니다.

## <a name="appendix-sql-server-latch-contention-scripts"></a>부록: SQL Server 래치 경합 스크립트

이 섹션에는 래치 경합 이슈를 진단하고 해결하는 데 사용할 수 있는 스크립트가 포함되어 있습니다.

### <a name="query-sysdm_os_waiting_tasks-ordered-by-session-id"></a><a id="waiting-tasks-script1"></a> 세션 ID를 기준으로 정렬된 sys.dm_os_waiting_tasks 쿼리

다음 샘플 스크립트는 sys.dm_os_waiting_tasks를 쿼리하고 세션 ID를 기준으로 정렬된 래치 대기를 반환합니다.

```sql
-- WAITING TASKS ordered by session_id 
SELECT wt.session_id, wt.wait_type
, er.last_wait_type AS last_wait_type
, wt.wait_duration_ms
, wt.blocking_session_id, wt.blocking_exec_context_id,
resource_description
FROM sys.dm_os_waiting_tasks wt
JOIN sys.dm_exec_sessions es ON wt.session_id = es.session_id
JOIN sys.dm_exec_requests er ON wt.session_id = er.session_id
WHERE es.is_user_process = 1
AND wt.wait_type <> 'SLEEP_TASK'
ORDER BY session_id
```

### <a name="query-sysdm_os_waiting_tasks-ordered-by-wait-duration"></a><a id="waiting-tasks-script2"></a> 대기 기간을 기준으로 정렬된 sys.dm_os_waiting_tasks 쿼리

다음 샘플 스크립트는 sys.dm_os_waiting_tasks를 쿼리하고 대기 기간을 기준으로 정렬된 래치 대기를 반환합니다.

```sql
-- WAITING TASKS ordered by wait_duration_ms
SELECT wt.session_id, wt.wait_type
, er.last_wait_type AS last_wait_type
, wt.wait_duration_ms
, wt.blocking_session_id, wt.blocking_exec_context_id, resource_description
FROM sys.dm_os_waiting_tasks wt
JOIN sys.dm_exec_sessions es ON wt.session_id = es.session_id
JOIN sys.dm_exec_requests er ON wt.session_id = er.session_id
WHERE es.is_user_process = 1
AND wt.wait_type <> 'SLEEP_TASK'
ORDER BY wt.wait_duration_ms desc
```

### <a name="calculate-waits-over-a-time-period"></a>일정 기간 동안 대기 계산

다음 스크립트는 일정 기간 동안 래치 대기를 계산하고 반환합니다.

```sql
/* Snapshot the current wait stats and store so that this can be compared over a time period 
   Return the statistics between this point in time and the last collection point in time.
   
   **This data is maintained in tempdb so the connection must persist between each execution**
   **alternatively this could be modified to use a persisted table in tempdb.  if that
   is changed code should be included to clean up the table at some point.**
*/
use tempdb
go

declare @current_snap_time datetime
declare @previous_snap_time datetime

set @current_snap_time = GETDATE()

if not exists(select name from tempdb.sys.sysobjects where name like '#_wait_stats%')
   create table #_wait_stats
   (
      wait_type varchar(128)
      ,waiting_tasks_count bigint
      ,wait_time_ms bigint
      ,avg_wait_time_ms int
      ,max_wait_time_ms bigint
      ,signal_wait_time_ms bigint
      ,avg_signal_wait_time int
      ,snap_time datetime
   )

insert into #_wait_stats (
         wait_type
         ,waiting_tasks_count
         ,wait_time_ms
         ,max_wait_time_ms
         ,signal_wait_time_ms
         ,snap_time
      )
      select
         wait_type
         ,waiting_tasks_count
         ,wait_time_ms
         ,max_wait_time_ms
         ,signal_wait_time_ms
         ,getdate()
      from sys.dm_os_wait_stats

--get the previous collection point
select top 1 @previous_snap_time = snap_time from #_wait_stats 
         where snap_time < (select max(snap_time) from #_wait_stats)
         order by snap_time desc

--get delta in the wait stats  
select top 10
      s.wait_type
      , (e.waiting_tasks_count - s.waiting_tasks_count) as [waiting_tasks_count]
      , (e.wait_time_ms - s.wait_time_ms) as [wait_time_ms]
      , (e.wait_time_ms - s.wait_time_ms)/((e.waiting_tasks_count - s.waiting_tasks_count)) as [avg_wait_time_ms]
      , (e.max_wait_time_ms) as [max_wait_time_ms]
      , (e.signal_wait_time_ms - s.signal_wait_time_ms) as [signal_wait_time_ms]
      , (e.signal_wait_time_ms - s.signal_wait_time_ms)/((e.waiting_tasks_count - s.waiting_tasks_count)) as [avg_signal_time_ms]
      , s.snap_time as [start_time]
      , e.snap_time as [end_time]
      , DATEDIFF(ss, s.snap_time, e.snap_time) as [seconds_in_sample]
   from #_wait_stats e
   inner join (
      select * from #_wait_stats 
         where snap_time = @previous_snap_time 
      ) s on (s.wait_type = e.wait_type)
   where 
      e.snap_time = @current_snap_time 
      and s.snap_time = @previous_snap_time
      and e.wait_time_ms > 0 
      and (e.waiting_tasks_count - s.waiting_tasks_count) > 0 
      and e.wait_type NOT IN ('LAZYWRITER_SLEEP', 'SQLTRACE_BUFFER_FLUSH'
                              , 'SOS_SCHEDULER_YIELD','DBMIRRORING_CMD', 'BROKER_TASK_STOP'
                              , 'CLR_AUTO_EVENT', 'BROKER_RECEIVE_WAITFOR', 'WAITFOR'
                              , 'SLEEP_TASK', 'REQUEST_FOR_DEADLOCK_SEARCH', 'XE_TIMER_EVENT'
                              , 'FT_IFTS_SCHEDULER_IDLE_WAIT', 'BROKER_TO_FLUSH', 'XE_DISPATCHER_WAIT'
                              , 'SQLTRACE_INCREMENTAL_FLUSH_SLEEP')

order by (e.wait_time_ms - s.wait_time_ms) desc 

--clean up table
delete from #_wait_stats
where snap_time = @previous_snap_time
```

### <a name="query-buffer-descriptors-to-determine-objects-causing-latch-contention"></a><a id="query-buffer-descriptors"></a> 버퍼 설명자를 쿼리하여 래치 경합을 유발하는 개체 확인

다음 스크립트는 버퍼 설명자를 쿼리하여 가장 긴 래치 대기 시간과 연결된 개체를 확인합니다.

```sql
IF EXISTS (SELECT * FROM tempdb.sys.objects WHERE [name] like '#WaitResources%') DROP TABLE #WaitResources;
CREATE TABLE #WaitResources (session_id INT, wait_type NVARCHAR(1000), wait_duration_ms INT,
                             resource_description sysname NULL, db_name NVARCHAR(1000), schema_name NVARCHAR(1000),
                             object_name NVARCHAR(1000), index_name NVARCHAR(1000));
GO
declare @WaitDelay varchar(16), @Counter INT, @MaxCount INT, @Counter2 INT
SELECT @Counter = 0, @MaxCount = 600, @WaitDelay = '00:00:00.100'-- 600x.1=60 seconds

SET NOCOUNT ON;
WHILE @Counter < @MaxCount
BEGIN
   INSERT INTO #WaitResources(session_id, wait_type, wait_duration_ms, resource_description)--, db_name, schema_name, object_name, index_name)
   SELECT   wt.session_id,
            wt.wait_type,
            wt.wait_duration_ms,
            wt.resource_description
      FROM sys.dm_os_waiting_tasks wt
      WHERE wt.wait_type LIKE 'PAGELATCH%' AND wt.session_id <> @@SPID
--select * from sys.dm_os_buffer_descriptors
   SET @Counter = @Counter + 1;
   WAITFOR DELAY @WaitDelay;
END;

--select * from #WaitResources

   update #WaitResources 
      set db_name = DB_NAME(bd.database_id),
         schema_name = s.name,
         object_name = o.name,
         index_name = i.name
            FROM #WaitResources wt
      JOIN sys.dm_os_buffer_descriptors bd
         ON bd.database_id = SUBSTRING(wt.resource_description, 0, CHARINDEX(':', wt.resource_description))
            AND bd.file_id = SUBSTRING(wt.resource_description, CHARINDEX(':', wt.resource_description) + 1, CHARINDEX(':', wt.resource_description, CHARINDEX(':', wt.resource_description) +1 ) - CHARINDEX(':', wt.resource_description) - 1)
            AND bd.page_id = SUBSTRING(wt.resource_description, CHARINDEX(':', wt.resource_description, CHARINDEX(':', wt.resource_description) +1 ) + 1, LEN(wt.resource_description) + 1)
            --AND wt.file_index > 0 AND wt.page_index > 0
      JOIN sys.allocation_units au ON bd.allocation_unit_id = AU.allocation_unit_id
      JOIN sys.partitions p ON au.container_id = p.partition_id
      JOIN sys.indexes i ON p.index_id = i.index_id AND p.object_id = i.object_id
      JOIN sys.objects o ON i.object_id = o.object_id
      JOIN sys.schemas s ON o.schema_id = s.schema_id
select * from #WaitResources order by wait_duration_ms desc
GO

/*
--Other views of the same information
SELECT wait_type, db_name, schema_name, object_name, index_name, SUM(wait_duration_ms) [total_wait_duration_ms] FROM #WaitResources
GROUP BY wait_type, db_name, schema_name, object_name, index_name;
SELECT session_id, wait_type, db_name, schema_name, object_name, index_name, SUM(wait_duration_ms) [total_wait_duration_ms] FROM #WaitResources
GROUP BY session_id, wait_type, db_name, schema_name, object_name, index_name;
*/

--SELECT * FROM #WaitResources
--DROP TABLE #WaitResources;
```

### <a name="hash-partitioning-script"></a>해시 분할 스크립트

이 스크립트 사용은 [계산 열을 통한 해시 분할 사용](#use-hash-partitioning-with-a-computed-column)에서 설명하며, 구현 목적에 맞게 사용자 지정해야 합니다.

```sql
--Create the partition scheme and function, align this to the number of CPU cores 1:1 up to 32 core computer
-- so for below this is aligned to 16 core system
CREATE PARTITION FUNCTION [pf_hash16] (tinyint) AS RANGE LEFT FOR VALUES
   (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15)

CREATE PARTITION SCHEME [ps_hash16] AS PARTITION [pf_hash16] ALL TO ( [ALL_DATA] )
-- Add the computed column to the existing table (this is an OFFLINE operation)

-- Consider using bulk loading techniques to speed it up
ALTER TABLE [dbo].[latch_contention_table]
   ADD [HashValue] AS (CONVERT([tinyint], abs(binary_checksum([hash_col])%(16)),(0))) PERSISTED NOT NULL

--Create the index on the new partitioning scheme 
CREATE UNIQUE CLUSTERED INDEX [IX_Transaction_ID] 
ON [dbo].[latch_contention_table]([T_ID] ASC, [HashValue]) 
ON ps_hash16(HashValue)
```

## <a name="next-steps"></a>다음 단계

성능 모니터링 도구에 대한 자세한 내용은 [성능 모니터링 및 튜닝 도구](./performance/performance-monitoring-and-tuning-tools.md)를 참조하세요.