---
title: 스레드 및 태스크 아키텍처 가이드 | Microsoft 문서
description: 태스크 예약, Hot Add CPU, CPU 64개 이상을 사용하는 컴퓨터에서의 모범 사례를 포함한 SQL Server에서의 스레드 및 태스크 아키텍처에 대해 알아봅니다.
ms.custom: ''
ms.date: 09/23/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- guide, thread and task architecture
- thread and task architecture guide
- task scheduling
- working threads
- Large Deficit First scheduling
- LDF scheduling
- scheduling, SQL Server
- tasks, SQL Server
- threads, SQL Server
- quantum, SQL Server
ms.assetid: 925b42e0-c5ea-4829-8ece-a53c6cddad3b
author: pmasl
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8b2e8810783bb3341f10b21c3068881558dfc611
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97403911"
---
# <a name="thread-and-task-architecture-guide"></a>스레드 및 태스크 아키텍처 가이드
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]

## <a name="operating-system-task-scheduling"></a>운영 체제 태스크 예약
스레드는 운영 체제에서 실행할 수 있는 가장 작은 처리 단위이며, 애플리케이션 로직을 여러 동시 실행 경로로 분리할 수 있습니다. 스레드는 여러 태스크를 동시에 수행할 수 있는 복잡한 애플리케이션에 유용합니다. 

운영 체제는 애플리케이션 인스턴스를 실행할 때 인스턴스를 관리하는 프로세스라는 단위를 만듭니다. 프로세스에는 실행 스레드가 하나씩 있습니다. 실행 스레드는 애플리케이션 코드가 수행하는 일련의 프로그래밍 명령입니다. 예를 들어 차례로 수행되는 단일 명령 집합을 포함하는 단순한 애플리케이션에는 명령 집합이 단일 **태스크** 로 처리되고, 애플리케이션에 하나의 실행 경로(또는 **스레드**)만 있습니다. 좀 더 복잡한 애플리케이션은 차례로 진행되지 않고 동시에 수행될 수 있는 여러 **태스크** 를 포함할 수 있습니다. 애플리케이션은 리소스를 많이 사용하는 작업인 각 태스크에 대해 별도의 프로세스를 시작하거나 리소스를 상대적으로 적게 사용하는 별도의 스레드를 시작하여 이를 수행할 수 있습니다. 또한 각 스레드는 프로세스와 관련된 다른 스레드와 독립적으로 실행되도록 예약할 수 있습니다.

스레드는 복잡한 애플리케이션이 단일 프로세서(CPU)가 있는 컴퓨터에서도 CPU를 더 효율적으로 사용할 수 있게 합니다. 하나의 CPU가 있으면 한 번에 한 스레드만 실행할 수 있습니다. 한 스레드가 디스크 읽기 또는 쓰기와 같이 CPU를 사용하지 않는 장기 실행 작업을 실행하는 경우 첫 번째 작업이 완료될 때까지 다른 스레드를 실행할 수 있습니다. 다른 스레드가 작업이 끝날 때까지 기다리는 동안 스레드를 실행할 수 있으면 애플리케이션이 CPU의 사용을 최대화할 수 있습니다. 이와 같은 이점은 특히 데이터베이스 서버와 같은 여러 사용자가 사용하는 디스크 입출력 집중형 애플리케이션에서 잘 나타납니다. 여러 CPU가 있는 컴퓨터는 CPU당 하나의 스레드를 실행할 수 있으므로 동시에 여러 스레드를 실행할 수 있습니다. 예를 들어 CPU가 8개 있는 컴퓨터에서는 동시에 8개의 스레드를 실행할 수 있습니다.

## <a name="sql-server-task-scheduling"></a>SQL Server 태스크 예약
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 범위에서 **요청** 은 쿼리 또는 일괄 처리의 논리적 표현입니다. 요청은 검사점 또는 로그 기록기와 같은 시스템 스레드에 필요한 작업도 나타냅니다. 요청은 수명이 지속되는 동안 다양한 상태로 존재하고 요청을 실행하는 데 필요한 리소스를 사용할 수 없는 경우(예: [잠금](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md#locks) 또는 [래치](../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md#latches)) 대기를 누적시킬 수 있습니다. 요청 상태에 대한 자세한 내용은 [sys.dm_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)를 참조하세요.

**태스크** 는 요청을 수행하기 위해 완료해야 하는 작업 단위를 나타냅니다. 하나 이상의 태스크를 단일 요청에 할당할 수 있습니다. 
-  병렬 요청은 **부모 태스크**(또는 조정 태스크) 하나와 여러 **자식 태스크** 를 사용하여 순차적이 아니라 동시에 실행되는 여러 활성 태스크를 포함합니다. 병렬 요청에 대한 실행 계획에는 병렬로 실행되지 않는 연산자를 사용하는 계획의 일련 분기 영역이 포함되기도 합니다. 부모 태스크는 이러한 직렬 연산자를 실행하는 작업을 담당합니다.
-  직렬 요청은 실행 도중 특정 시점에서 하나의 활성 태스크만 포함합니다.     
태스크는 수명이 지속되는 동안 다양한 상태로 존재합니다. 태스크 상태에 대한 자세한 내용은 [sys.dm_os_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)를 참조하세요. 작업이 일시 중단됨 상태일 경우 작업을 실행하는 데 필요한 리소스가 사용 가능해질 때까지 기다리고 있는 것입니다. 대기 태스크에 대한 자세한 내용은 [sys.dm_os_waiting_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md)를 참조하세요.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **작업자 스레드**(작업자 또는 스레드라고도 함)는 운영 체제 스레드의 논리적 표현입니다. **직렬 요청** 을 실행하는 경우 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]는 활성 캐스트를 실행할 작업자를 생성합니다(1:1). [행 모드](../relational-databases/query-processing-architecture-guide.md#execution-modes)에서 **병렬 요청** 을 실행하는 경우 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 할당된 작업을 완료해야 하는 자식 작업자를(역시 1:1로) 조정하는 작업자인 **부모 스레드**(또는 조정 스레드)를 할당합니다. 부모 스레드에는 연결된 부모 태스크가 있습니다. 부모 스레드는 요청의 진입점이며 엔진이 쿼리를 구문 분석하기 전에도 존재합니다. 부모 스레드의 주요 책임은 다음과 같습니다. 
-  병렬 검색을 조정합니다.
-  자식 병렬 작업자를 시작합니다.
-  병렬 스레드에서 행을 수집하여 클라이언트로 보냅니다.
-  로컬 및 전역 집계를 수행합니다.    

> [!NOTE]
> 쿼리 계획에 직렬 및 병렬 분기가 있는 경우 병렬 작업 중 하나가 직렬 분기 실행을 담당합니다. 

각 태스크에 대해 생성되는 작업자 스레드 수는 다음에 따라 달라집니다.
-   요청이 쿼리 최적화 프로그램에 의해 결정된 대로 병렬 처리에 적합한지 여부.
-   현재 로드를 기반으로 하는 시스템에서 실제 사용 가능한 [DOP(병렬 처리 수준)](../relational-databases/query-processing-architecture-guide.md#DOP). 이는 MAXDOP(최대 병렬 처리 수준)에 대한 서버 구성을 기반으로 하는 예상 DOP와 다를 수 있습니다. 예를 들어 MAXDOP에 대한 서버 구성은 8이지만 런타임에 사용 가능한 DOP는 단지 2일 수 있습니다. 이것이 쿼리 성능에 영향을 미칩니다. 

> [!NOTE]
> **MAXDOP(최대 병렬 처리 수준)** 제한은 요청별이 아니라 태스크별로 설정됩니다. 즉 병렬 쿼리를 실행하는 동안 단일 요청은 MAXDOP 제한에 도달할 때까지 여러 태스크를 생성할 수 있으며 각 태스크는 작업자 하나를 사용합니다. MAXDOP에 대한 자세한 내용은 [최대 병렬 처리 수준 서버 구성 옵션 구성](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.

**스케줄러**(SOS 스케줄러라고도 함)는 태스크를 대신하여 작업을 수행하기 위해 처리 시간이 필요한 작업자 스레드를 관리합니다. 각 스케줄러는 개별 프로세서(CPU)에 매핑됩니다. 작업자가 스케줄러에서 활성 상태를 유지할 수 있는 시간을 OS 퀀텀이라고 하며 최대 4ms입니다. 퀀텀 시간이 만료된 후 작업자는 CPU 리소스에 액세스해야 하는 다른 작업자에게 시간을 양보하고 상태를 변경합니다. 이와 같이 CPU 리소스에 대한 액세스를 최대화하기 위한 작업자 간 협력을 **협조적 예약**(비선점형 예약)이라고 합니다. 작업자 상태 변경은 해당 작업자와 연결된 태스크, 그리고 해당 태스크와 연결된 요청에 전파됩니다. 작업자 상태에 대한 자세한 내용은 [sys.dm_os_workers](../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)를 참조하세요. 스케줄러에 대한 자세한 내용은 [sys.dm_os_schedulers ](../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)를 참조하세요. 

요약하면 **요청** 은 하나 이상의 **태스크** 를 생성하여 작업 단위를 실행합니다. 각 태스크는 태스크 완료를 담당하는 **작업자 스레드** 에 할당됩니다. 태스크 활성 실행을 위해 각 작업자 스레드는 예약되어야 합니다(**스케줄러** 에 배치되어야 합니다). 

> [!NOTE]
> 다음 시나리오를 고려하세요.   
> -  작업자 1은 메모리 내 기반 테이블에 대한 미리 읽기를 사용하는 읽기 쿼리처럼 오래 실행되는 작업입니다. 작업자 1은 필요한 데이터 페이지가 이미 버퍼 풀에 있기 때문에 I/O 작업을 기다릴 필요 없이 결과 생성 전에 전체 퀀텀을 사용할 수 있다는 것을 확인합니다.   
> -  작업자 2는 밀리초 미만의 더 짧은 작업을 수행하므로 전체 퀀텀이 고갈되기 전에 결과를 생성해야 합니다.     
>
> 이 시나리오 및 최대 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에서 작업자 1은 기본적으로 전체 퀀텀 시간을 늘려서 스케줄러를 독점할 수 있습니다.   
> [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]부터 협조적 일정 예약에 LDF(Large Deficit First) 일정이 포함됩니다. LDF 일정을 사용하면 퀀텀 사용 패턴이 모니터링되고 한 작업자 스레드가 스케줄러를 독점하지 않습니다. 동일한 시나리오에서 작업자 2는 작업자 1에게 더 많은 퀀텀이 허용되기 전에 반복 퀀텀을 사용할 수 있으므로, 작업자 1이 생소한 패턴의 스케줄러를 독점할 수 없습니다.

### <a name="scheduling-parallel-tasks"></a>병렬 작업 예약
MaxDOP 8로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 구성하고 CPU 선호도가 NUMA 노드 0 및 1에서 CPU 24개(스케줄러)를 대상으로 구성했다고 상상해 보세요. 스케줄러 0~11은 NUMA 노드 0에 속하며 스케줄러 12~23은 NUMA 노드 1에 속합니다. 애플리케이션은 [!INCLUDE[ssde_md](../includes/ssde_md.md)]에 다음 쿼리(요청)를 보냅니다.

```sql
SELECT h.SalesOrderID, h.OrderDate, h.DueDate, h.ShipDate
FROM Sales.SalesOrderHeaderBulk AS h 
INNER JOIN Sales.SalesOrderDetailBulk AS d ON h.SalesOrderID = d.SalesOrderID 
WHERE (h.OrderDate >= '2014-3-28 00:00:00');
```

> [!TIP]
> 예제 쿼리는 [AdventureWorks2016_EXT 예제 데이터베이스](../samples/adventureworks-install-configure.md) 데이터베이스를 사용하여 실행할 수 있습니다. `Sales.SalesOrderHeader` 및 `Sales.SalesOrderDetail` 테이블은 50번 확대되고 `Sales.SalesOrderHeaderBulk` 및 `Sales.SalesOrderDetailBulk`로 이름이 변경되었습니다.

실행 계획은 두 테이블 간의 [해시 조인](../relational-databases/performance/joins.md#hash)을 표시하며, 화살표 두 개가 있는 노란색 원을 보면 알 수 있듯이 각 연산자는 병렬로 실행됩니다. 각 Parallelism 연산자는 계획의 다른 분기입니다. 따라서 아래 실행 계획에는 분기 세 개가 존재합니다. 

![병렬 쿼리 계획](../relational-databases/media/schedule-parallel-query-plan.png)

> [!NOTE]
> 실행 계획을 나무라고 생각하면 **분기** 는 Exchange 반복기라고도 하는 Parallelism 연산자 하나 이상을 그룹화하는 계획 영역입니다. 계획 연산자에 대한 자세한 내용은 [실행 계획 논리 및 물리 연산자 참조](../relational-databases/showplan-logical-and-physical-operators-reference.md)를 확인하세요. 

실행 계획에는 분기 세 개가 있지만 이 실행 계획에서는 실행 중 다음 분기 두 개만 동시에 실행할 수 있습니다.
1.  `Sales.SalesOrderHeaderBulk`에서 ‘클러스터형 인덱스 스캔’이 사용되는 분기(조인의 빌드 입력)는 단독으로 실행됩니다.
2.  그런 다음, `Sales.SalesOrderDetailBulk`(조인의 프로브 입력)에서 ‘클러스터형 인덱스 스캔’을 사용하는 분기는 ‘비트맵’을 생성하고 현재 ‘해시 매치’가 실행 중인 분기와 동시에 실행됩니다.

실행 계획 XML에서는 작업자 스레드 16개가 예약되었고 NUMA 노드 0에서 사용했음을 확인할 수 있습니다.

```xml
<ThreadStat Branches="2" UsedThreads="16">
  <ThreadReservation NodeId="0" ReservedThreads="16" />
</ThreadStat>
```

스레드 예약을 사용하면 [!INCLUDE[ssde_md](../includes/ssde_md.md)]는 요청에 필요한 모든 태스크를 수행할 수 있을 만큼의 작업자 스레드를 확보할 수 있습니다. 스레드는 여러 NUMA 노드에 예약하거나 단일 NUMA 노드에 예약할 수 있습니다. 스레드 예약은 실행 시작 전 런타임 시에 수행되며 스케줄러 로드에 따라 달라집니다. 예약된 작업자 스레드 수는 일반적으로 **동시 스레드 * 런타임 DOP** 수식에서 파생되며 부모 작업자 스레드를 제외합니다. 각 분기는 MaxDOP와 동일한 작업자 스레드 수로 제한됩니다. 이 예제에서는 동시 분기 두 개가 있고 MaxDOP가 8로 설정되어 있으므로 **2 * 8 = 16** 개입니다.

참조를 위해 [활성 쿼리 통계](../relational-databases/performance/live-query-statistics.md)의 활성 실행 계획을 확인하면 분기 하나가 완료되고 분기 두 개가 동시에 실행 중임을 알 수 있습니다.

![활성 병렬 쿼리 계획](../relational-databases/media/schedule-parallel-query-live-plan.png)

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 작업자 스레드를 할당하여 활성 태스크를 실행합니다(1:1). 아래 예제와 같이 [sys.dm_os_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md) DMV를 쿼리하면 쿼리 실행 중에 이를 확인할 수 있습니다.

```sql
SELECT parent_task_address, task_address, 
       task_state, scheduler_id, worker_address
FROM sys.dm_os_tasks
WHERE session_id = <insert_session_id>
ORDER BY parent_task_address, scheduler_id;
```

> [!TIP]
> `parent_task_address` 열은 부모 태스크에 대해 언제나 NULL입니다. 

> [!TIP]
> 대단히 바쁜 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 예약된 스레드로 설정하는 제한을 초과하는 수의 활성 태스크가 표시될 수 있습니다. 이러한 태스크는 더 이상 사용하지 않는 분기에 속할 수 있으며 현재는 정리를 기다리는 임시 상태입니다. 

[!INCLUDE[ssResult](../includes/ssresult-md.md)] 현재 실행 중인 분기에 대한 활성 태스크 17개가 있습니다. 예약된 스레드에 해당하는 자식 태스크 16개와 부모 태스크(조정 태스크) 1개로 구성됩니다.

|parent_task_address|task_address|task_state|scheduler_id|worker_address|
|--------|--------|--------|--------|--------|
|NULL|**0x000001EF4758ACA8**|SUSPENDED|3|0x000001EFE6CB6160|
|0x000001EF4758ACA8|0x000001EFE43F3468|SUSPENDED|0|0x000001EF6DB70160|
|0x000001EF4758ACA8|0x000001EEB243A4E8|SUSPENDED|0|0x000001EF6DB7A160|
|0x000001EF4758ACA8|0x000001EC86251468|SUSPENDED|5|0x000001EEC05E8160|
|0x000001EF4758ACA8|0x000001EFE3023468|SUSPENDED|5|0x000001EF6B46A160|
|0x000001EF4758ACA8|0x000001EFE3AF1468|SUSPENDED|6|0x000001EF6BD38160|
|0x000001EF4758ACA8|0x000001EFE4AFCCA8|SUSPENDED|6|0x000001EF6ACB4160|
|0x000001EF4758ACA8|0x000001EFDE043848|SUSPENDED|7|0x000001EEA18C2160|
|0x000001EF4758ACA8|0x000001EF69038108|SUSPENDED|7|0x000001EF6AEBA160|
|0x000001EF4758ACA8|0x000001EFCFDD8CA8|SUSPENDED|8|0x000001EFCB6F0160|
|0x000001EF4758ACA8|0x000001EFCFDD88C8|SUSPENDED|8|0x000001EF6DC46160|
|0x000001EF4758ACA8|0x000001EFBCC54108|SUSPENDED|9|0x000001EFCB886160|
|0x000001EF4758ACA8|0x000001EC86279468|SUSPENDED|9|0x000001EF6DE08160|
|0x000001EF4758ACA8|0x000001EFDE901848|SUSPENDED|10|0x000001EFF56E0160|
|0x000001EF4758ACA8|0x000001EF6DB32108|SUSPENDED|10|0x000001EFCC3D0160|
|0x000001EF4758ACA8|0x000001EC8628D468|SUSPENDED|11|0x000001EFBFA4A160|
|0x000001EF4758ACA8|0x000001EFBD3A1C28|SUSPENDED|11|0x000001EF6BD72160|

16개의 각 자식 태스크에는 (`worker_address`에서처럼) 서로 다른 작업자 스레드가 할당되어 있지만 모든 작업자는 같은 8개 스케줄러 풀(0,5,6,7,8,9,10,11)에 할당되며 부모 태스크는 이 풀에 속하지 않는 스케줄러(3)에 할당됩니다.

> [!IMPORTANT]
> 지정된 분기에 대한 첫 번째 병렬 태스크 모음이 예약되면 [!INCLUDE[ssde_md](../includes/ssde_md.md)]에서는 다른 분기의 추가 태스크에 대해 같은 스케줄러 풀을 사용합니다. 따라서 전체 실행 계획의 모든 병렬 태스크에 대해 같은 스케줄러 모음을 사용하며 유일한 제한은 MaxDOP입니다.  
> [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 항상 작업 실행을 위해 동일한 NUMA 노드에서 스케줄러를 할당하도록 시도하고, 스케줄러를 사용할 수 있는 경우 순차적으로(라운드 로빈 방식) 할당합니다. 그러나 부모 태스크에 할당된 작업자 스레드는 다른 태스크와 다른 NUMA 노드에 배치할 수 있습니다.

작업자 스레드는 자신의 퀀텀 기간(4ms)에만 스케줄러에서 활성 상태를 유지하며 활성화될 수 있는 다른 태스크에 작업자 스레드가 할당될 수 있도록 퀀텀이 끝나면 스케줄러를 일시 중단해야 합니다. 작업자의 퀀텀이 만료되고 활성 상태가 끝나면 대응하는 태스크는 다시 RUNNING 상태가 되기 전까지 RUNNABLE 상태로 FIFO 큐에 배치됩니다. 태스크는 래치 또는 잠금처럼 현재 사용할 수 없는 리소스에 대한 액세스를 요구하지 않는다고 가정하며, 요구한다면 태스크는 이러한 리소스를 사용할 수 있을 때까지 RUNNABLE이 아닌 SUSPENDED 상태로 배치됩니다.  

> [!TIP] 
> 위에 표시된 DMV 출력에서는 모든 활성 태스크가 SUSPENDED 상태입니다. 대기 태스크에 대한 자세한 내용은 [dm_os_waiting_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md) DMV를 쿼리하여 확인할 수 있습니다. 

요약하자면, 병렬 요청은 여러 작업을 생성합니다. 각 작업은 단일 작업자 스레드에 할당되어야 합니다. 각 작업자 스레드는 단일 스케줄러에 할당되어야 합니다. 따라서 사용 중인 스케줄러 수는 분기당 병렬 작업 수를 초과할 수 없습니다. 이 수는 MaxDOP 구성 또는 쿼리 힌트에 의해 설정됩니다. 조정 스레드는 MaxDOP 제한에 영향을 주지 않습니다. 

### <a name="allocating-threads-to-a-cpu"></a>CPU에 스레드 할당
기본적으로 각각의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스는 각 스레드를 시작하며 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 스레드를 부하에 따라 컴퓨터의 프로세서(CPU)에 균일하게 분산합니다. affinity 프로세스가 운영 체제 수준에서 사용하도록 설정된 경우, 운영 체제에서 각 스레드를 특정 CPU에 할당합니다. 반대로 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 스레드를 CPU에 균일하게 분산하는 **스케줄러** 에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **작업자 스레드** 를 라운드 로빈 방식으로 할당합니다.
    
동일한 CPU 세트에 여러 애플리케이션이 액세스하는 등, 멀티태스킹을 수행하기 위해 운영 체제가 가끔 다른 CPU 간에 작업자 스레드를 이동하기도 합니다. 이는 운영 체제의 측면에서 볼 때는 효율적이지만 각 프로세서 캐시에 데이터를 반복적으로 다시 로드해야 하므로 시스템 부하가 큰 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 성능 저하를 초래할 수 있습니다. CPU를 특정 스레드에 할당하면 프로세서를 다시 로드할 필요가 없고 CPU 간에 스레드 마이그레이션이 감소되어 컨텍스트 전환이 줄게 되므로 성능이 향상될 수 있습니다. 스레드와 프로세서의 이러한 관계를 프로세서 선호도라고 합니다. affinity를 사용하는 경우에는 운영 체제에서 각 스레드를 특정 CPU에 할당합니다. 

[affinity mask](../database-engine/configure-windows/affinity-mask-server-configuration-option.md) 옵션은 [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md)을 사용하여 설정합니다. affinity mask를 설정하지 않으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스가 제외되지 않은 스케줄러에 균등하게 작업자 스레드를 할당합니다.

> [!CAUTION]
> 운영 체제에서 CPU 선호도를 구성하지 말고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서도 선호도 마스크를 구성하지 않습니다. 동일한 결과를 얻기 위해 이렇게 설정하는 경우도 있지만 구성이 일치하지 않는 경우 예상치 못한 결과가 나올 수 있습니다. 자세한 내용은 [affinity mask 옵션](../database-engine/configure-windows/affinity-mask-server-configuration-option.md)을 참조하세요.

스레드 풀링을 사용하면 많은 클라이언트가 서버에 연결되어 있을 때 성능이 최적화됩니다. 보통 각 쿼리 요청마다 별도의 운영 체제 스레드가 생성됩니다. 그러나 서버에 대한 연결 수가 수백 개인 경우 쿼리 요청별로 스레드를 하나씩 사용하면 시스템 리소스를 상당히 많이 소비하게 될 수 있습니다. [max worker threads](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) 옵션을 사용하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 작업자 스레드 풀을 만들어 많은 쿼리 요청을 처리할 수 있으므로 성능이 향상됩니다. 

### <a name="using-the-lightweight-pooling-option"></a>lightweight pooling 옵션 사용
스레드 컨텍스트 전환과 관련된 오버헤드는 별로 크지 않을 수 있습니다. lightweight pooling 옵션을 0으로 설정할 때나 1로 설정할 때 대부분의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에는 성능상의 차이가 전혀 없습니다. [lightweight pooling](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)을 사용할 경우 성능이 향상될 수 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스는 다음 특성을 가진 컴퓨터에서 실행되는 인스턴스뿐입니다.    
* 대형 다중 CPU 서버
* 모든 CPU가 거의 최대 용량에서 실행됩니다.
* 높은 수준의 컨텍스트 전환이 있습니다.

이러한 시스템의 경우 lightweight pooling 값을 1로 설정하면 성능이 조금 향상됩니다.

> [!IMPORTANT]
> 일상 작업을 예약하는 데에는 파이버 모드를 사용하지 않습니다. 파이버 모드를 사용하면 컨텍스트 전환을 활용하지 못해 성능이 저하될 수 있으며 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 일부 구성 요소가 파이버 모드에서 제대로 작동하지 않을 수 있습니다. 자세한 내용은 [lightweight pooling](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)을 참조하세요.

## <a name="thread-and-fiber-execution"></a>스레드 및 파이버 실행
Microsoft Windows에서는 1부터 31까지의 숫자 우선 순위 시스템을 사용하여 스레드 실행 일정을 예약합니다. 0은 운영 체제용으로 예약됩니다. 여러 스레드가 실행을 위해 대기하고 있을 때 Windows에서는 우선 순위가 가장 높은 스레드를 디스패치합니다.

기본적으로 각 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스의 우선 순위는 보통 우선 순위인 7입니다. 이 기본값은 다른 애플리케이션에 나쁜 영향을 주지 않고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스레드가 충분한 CPU 리소스를 얻을 수 있는 우선 순위를 제공합니다. 

> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../includes/ssnotedepfuturedontuse-md.md)]  

[priority boost](../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) 구성 옵션을 사용하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 스레드의 우선 순위를 높은 우선 순위인 13으로 높일 수 있습니다. 이 설정은 대부분의 다른 애플리케이션보다 높은 우선 순위를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스레드에 제공합니다. 따라서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스레드는 일반적으로 실행할 준비가 될 때마다 디스패치되고 다른 애플리케이션의 스레드에 의해 미리 점유되지 않습니다. 이는 서버가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스만 실행하고 다른 애플리케이션은 실행하지 않을 때 성능을 향상시킬 수 있습니다. 그러나 메모리 집중형 작업이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 발생할 경우 대개는 다른 애플리케이션이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스레드를 미리 점유할 만큼 충분히 높은 우선 순위를 갖고 있지 않습니다. 

컴퓨터에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 여러 인스턴스를 실행하고 일부 인스턴스에 대해서만 priority boost 옵션이 설정되어 있는 경우 보통 우선 순위에서 실행되는 인스턴스의 성능에 나쁜 영향을 줄 수 있습니다. 또한 priority boost가 설정되어 있으면 서버의 다른 애플리케이션 및 구성 요소의 성능도 저하될 수 있습니다. 따라서 엄격하게 제어되는 환경에서만 이 설정을 사용해야 합니다.


## <a name="hot-add-cpu"></a>Hot add CPU
Hot add CPU는 실행 중인 시스템에 CPU를 동적으로 추가할 수 있는 기능입니다. CPU는 새 하드웨어를 추가하여 물리적으로 추가하거나, 온라인으로 하드웨어를 분할하여 논리적으로 추가하거나, 가상화 계층을 통해 가상으로 추가할 수 있습니다. [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)]는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]부터 hot add CPU를 지원합니다.

hot add CPU 요구 사항  
* hot add CPU를 지원하는 하드웨어
* 64비트 버전의 Windows Server 2008 Datacenter 또는 Itanium 기반 시스템 운영 체제용 Windows Server 2008 Enterprise Edition
* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise
* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 소프트 NUMA를 사용하도록 구성할 수 없음. 소프트 NUMA에 대한 자세한 내용은 [Soft-NUMA(SQL Server)](../database-engine/configure-windows/soft-numa-sql-server.md)를 참조하세요.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 CPU가 추가된 후에 CPU 사용을 자동으로 시작하지 않습니다. 따라서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 다른 용도로 추가되었을 수 있는 CPU를 사용하지 않도록 방지할 수 있습니다. CPU를 추가한 후 [RECONFIGURE](../t-sql/language-elements/reconfigure-transact-sql.md) 문을 실행하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 새로운 CPU를 사용할 수 있는 리소스로 인식하게 됩니다.

> [!NOTE]
> [affinity64 mask](../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) 가 구성된 경우 새로운 CPU를 사용하도록 affinity64 mask를 수정해야 합니다.
 
## <a name="best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus"></a>CPU가 64개를 초과하는 컴퓨터에서 SQL Server를 실행하기 위한 최선의 방법

### <a name="assigning-hardware-threads-with-cpus"></a>CPU와 함께 하드웨어 스레드 할당
특정 스레드에 프로세서를 바인딩하는 데 선호도 마스크 및 affinity64 마스크 서버 구성 옵션을 사용하지 마세요. 이러한 옵션은 CPU가 최대 64개일 때만 사용할 수 있습니다. 대신 [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md)의 `SET PROCESS AFFINITY` 옵션을 사용하세요.

### <a name="managing-the-transaction-log-file-size"></a>트랜잭션 로그 파일 크기 관리
트랜잭션 로그 파일의 크기를 늘리려면 자동 증가에 의존하지 마십시오. 트랜잭션 로그를 늘리는 작업은 직렬 프로세스로 수행되어야 합니다. 로그를 확장하면 로그 확장이 끝날 때까지 트랜잭션 쓰기 작업이 수행되지 않을 수 있습니다. 대신 환경의 일반적인 작업량을 지원할 수 있는 값으로 파일 크기를 설정하여 로그 파일에 충분한 공간을 미리 할당합니다.

### <a name="setting-max-degree-of-parallelism-for-index-operations"></a>인덱스 작업을 위한 최대 병렬 처리 수준 설정
CPU가 여러 개인 컴퓨터에서 데이터베이스의 복구 모델을 임시로 대량 로그 또는 단순 복구 모델로 설정하여 인덱스 만들기 또는 다시 작성과 같은 인덱스 작업의 성능을 향상시킬 수 있습니다. 이러한 인덱스 작업으로 인해 상당한 로그 작업이 수행될 수 있으며 로그 경합으로 인해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 선택하는 최상의 DOP(병렬 처리 수준)에 영향이 있을 수 있습니다.

**MAXDOP(최대 병렬 처리 수준)** 서버 구성 옵션을 조정하는 것 외에도 [MAXDOP 옵션](../t-sql/statements/alter-index-transact-sql.md)을 사용하여 인덱스 작업에 대한 병렬 처리를 조정할 수 있습니다. 자세한 내용은 [병렬 인덱스 작업 구성](../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요. 최대 병렬 처리 수준 서버 구성 옵션을 조정하는 방법에 대한 자세한 내용 및 지침은 [최대 병렬 처리 수준 서버 구성 옵션 구성](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.

### <a name="setting-the-maximum-number-of-worker-threads"></a>최대 작업자 스레드 수 설정
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 시작 시 **최대 작업자 스레드** 서버 구성 옵션을 동적으로 구성합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 사용 가능한 CPU 수와 시스템 아키텍처를 사용하여 시작 시 문서화된 [수식](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md#Recommendations)을 사용하여 이 서버 구성을 확인합니다.

이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 SQL Server 전문가만이 변경해야 합니다. 성능 문제가 의심되는 경우 작업자 스레드 가용성 문제는 아닙니다. 원인은 작업자 스레드를 대기하게 하는 I/O 관련 문제일 가능성이 높습니다. 최대 작업자 스레드 설정이 변경하기 전에 성능 문제의 근본 원인을 찾는 것이 가장 좋습니다. 그러나 최대 작업자 스레드 수를 수동으로 설정해야 하는 경우 이 구성 값은 항상 시스템에 있는 CPU 수의 7배 이상의 값으로 설정해야 합니다. 자세한 내용은 [최대 작업자 스레드 수 구성](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)을 참조하세요.

### <a name="using-sql-trace-and-sql-server-profiler"></a>SQL 추적 및 SQL Server Profiler 사용
프로덕션 환경에서는 SQL 추적과 SQL Server Profiler를 사용하지 않는 것이 좋습니다. CPU 수가 늘어날수록 이러한 도구의 실행으로 인한 오버헤드도 늘어납니다. 프로덕션 환경에서 SQL 추적을 사용해야 하는 경우 추적 이벤트의 수를 최소로 제한합니다. 부하를 고려하여 주의 깊게 각 추적 이벤트를 프로파일링 및 테스트해야 하며 성능에 많은 영향을 주는 이벤트를 조합해서 사용하지 마십시오.

> [!IMPORTANT]
> SQL 추적 및 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]는 사용되지 않습니다. Microsoft SQL Server 추적 및 재생 개체를 포함하는 *Microsoft.SqlServer.Management.Trace* 네임스페이스도 더 이상 사용되지 않습니다. 
> [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)] 
> 확장 이벤트를 대신 사용하세요. [확장 이벤트](../relational-databases/extended-events/extended-events.md)에 대한 자세한 내용은 [빠른 시작: SQL Server의 확장 이벤트](../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md) 및 [SSMS XEvent Profiler](../relational-databases/extended-events/use-the-ssms-xe-profiler.md)를 참조하세요.

> [!NOTE]
> Analysis Services 워크로드에는 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]가 계속 사용되며 지원됩니다.

### <a name="setting-the-number-of-tempdb-data-files"></a>tempdb 데이터 파일 수 설정
파일의 수는 컴퓨터의 논리 프로세서 수에 따라 달라집니다. 일반적으로 논리 프로세서의 수가 8 이하인 경우 논리 프로세서와 같은 수의 데이터 파일을 사용합니다. 논리 프로세서의 수가 8보다 클 경우 8개의 데이터 파일을 사용합니다. 그런 다음에도 경합이 계속될 경우 경합이 허용 가능한 수준으로 감소할 때까지 데이터 파일의 수를 4의 배수로 늘리거나 작업/코드를 변경합니다. 또한 [SQL Server에서 tempdb 성능 최적화](../relational-databases/databases/tempdb-database.md#optimizing-tempdb-performance-in-sql-server)에 나와 있는 tempdb에 대한 다른 권장 사항도 염두에 두어야 합니다. 

하지만 tempdb에 대한 동시성 요구를 신중하게 고려하면 데이터베이스 관리 오버헤드를 줄일 수 있습니다. 예를 들어 시스템에 64개의 CPU가 있고 일반적으로 32개의 쿼리에서만 tempdb를 사용하는 경우 tempdb 파일의 수를 64개로 늘려도 성능이 개선되지 않습니다.

### <a name="sql-server-components-that-can-use-more-than-64-cpus"></a>64개를 초과하는 CPU를 사용할 수 있는 SQL Server 구성 요소
다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소를 나열하고 이들 구성 요소가 64개를 초과하는 CPU를 사용할 수 있는지를 보여 줍니다.

|프로세스 이름   |실행 프로그램 |64개를 초과하는 CPU 사용 |  
|----------|----------|----------|  
|SQL Server 데이터베이스 엔진 |Sqlserver.exe  |예 |  
|Reporting Services |Rs.exe |예 |  
|Analysis Services  |As.exe |예 |  
|Integration Services   |Is.exe |예 |  
|Service Broker |Sb.exe |예 |  
|전체 텍스트 검색   |Fts.exe    |예 |  
|SQL Server 에이전트   |Sqlagent.exe   |예 |  
|SQL Server Management Studio   |Ssms.exe   |예 |  
|SQL Server 설치   |Setup.exe  |예 |  
