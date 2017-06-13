---
title: "스레드 및 태스크 아키텍처 가이드 | Microsoft 문서"
ms.custom: 
ms.date: 10/26/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guide, thread and task architecture
- thread and task architecture guide
ms.assetid: 925b42e0-c5ea-4829-8ece-a53c6cddad3b
caps.latest.revision: 3
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 93be3a22ee517f90e65b8c8ba6dcaa8d90ed8515
ms.openlocfilehash: 3b835536b4f510021f0d966e3214cf1ec5f71f5c
ms.contentlocale: ko-kr
ms.lasthandoff: 06/07/2017

---
# <a name="thread-and-task-architecture-guide"></a>스레드 및 태스크 아키텍처 가이드
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

스레드는 응용 프로그램 논리를 여러 동시 실행 경로로 분리할 수 있게 하는 운영 체제 기능입니다. 이 기능은 여러 태스크를 동시에 수행할 수 있는 복잡한 응용 프로그램에 유용합니다. 

운영 체제는 응용 프로그램 인스턴스를 실행할 때 인스턴스를 관리하는 프로세스라는 단위를 만듭니다. 프로세스에는 실행 스레드가 하나씩 있습니다. 실행 스레드는 응용 프로그램 코드가 수행하는 일련의 프로그래밍 명령입니다. 예를 들어 차례로 수행되는 단일 명령 집합을 포함하는 단순한 응용 프로그램에는 응용 프로그램에 하나의 실행 경로 또는 스레드만 있습니다. 좀 더 복잡한 응용 프로그램은 차례로 진행되지 않고 동시에 수행될 수 있는 여러 태스크를 포함할 수 있습니다. 이 경우 응용 프로그램은 각 태스크에 대해 별도의 프로세스를 시작해야 합니다. 그러나 프로세스를 시작하는 데는 많은 리소스가 필요합니다. 따라서 응용 프로그램은 프로세스를 시작하는 대신 별도의 스레드를 시작할 수 있습니다. 이렇게 하면 리소스 사용량이 상대적으로 줄어듭니다. 또한 각 스레드는 프로세스와 관련된 다른 스레드와 독립적으로 실행되도록 예약할 수 있습니다.

스레드는 복잡한 응용 프로그램이 단일 CPU가 있는 컴퓨터에서도 CPU를 더 효율적으로 사용할 수 있게 합니다. 하나의 CPU가 있으면 한 번에 한 스레드만 실행할 수 있습니다. 한 스레드가 디스크 읽기 또는 쓰기와 같이 CPU를 사용하지 않는 장기 실행 작업을 실행하는 경우 첫 번째 작업이 완료될 때까지 다른 스레드를 실행할 수 있습니다. 다른 스레드가 작업이 끝날 때까지 기다리는 동안 스레드를 실행할 수 있으면 응용 프로그램이 CPU의 사용을 최대화할 수 있습니다. 이와 같은 이점은 특히 데이터베이스 서버와 같은 여러 사용자가 사용하는 디스크 입출력 집중형 응용 프로그램에서 잘 나타납니다. 여러 마이크로프로세서 또는 CPU가 있는 컴퓨터는 CPU당 하나의 스레드를 실행할 수 있으므로 동시에 여러 스레드를 실행할 수 있습니다. 예를 들어 CPU가 8개 있는 컴퓨터에서는 동시에 8개의 스레드를 실행할 수 있습니다.

## <a name="sql-server-batch-or-task-scheduling"></a>SQL Server 일괄 처리 또는 태스크 일정 예약

### <a name="allocating-threads-to-a-cpu"></a>CPU에 스레드 할당

기본적으로 SQL Server 인스턴스마다 각 스레드를 시작합니다. affinity를 사용하는 경우에는 운영 체제에서 각 스레드를 특정 CPU에 할당합니다. 운영 체제에서는 여러 SQL Server 인스턴스의 스레드를 부하에 따라 컴퓨터의 마이크로프로세서 또는 CPU에 균일하게 분산합니다. 사용량이 많은 CPU에서 다른 CPU로 스레드를 이동하는 경우도 있습니다. 반대로 SQL Server 데이터베이스 엔진은 스레드를 CPU에 균일하게 분산하는 스케줄러에 작업자 스레드를 할당합니다.

affinity mask 옵션은 [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md)를 사용하여 설정합니다. affinity mask를 설정하지 않으면 SQL Server 인스턴스가 제외되지 않은 스케줄러에 균등하게 작업자 스레드를 할당합니다.

### <a name="using-the-lightweight-pooling-option"></a>lightweight pooling 옵션 사용

스레드 컨텍스트 전환과 관련된 오버헤드는 별로 크지 않습니다. lightweight pooling 옵션을 0으로 설정할 때나 1로 설정할 때 대부분의 SQL Server 인스턴스에는 성능상의 차이가 전혀 없습니다. [lightweight pooling](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md) 을 사용할 경우 성능이 향상될 수 있는 SQL Server 인스턴스는 다음 특성을 가진 컴퓨터에서 실행되는 인스턴스뿐입니다.    
* 대형 다중 CPU 서버입니다.
* 모든 CPU가 거의 최대 용량에서 실행됩니다.
* 높은 수준의 컨텍스트 전환이 있습니다.

이러한 시스템의 경우 lightweight pooling 값을 1로 설정하면 성능이 조금 향상됩니다.

일상 작업을 예약하는 데에는 파이버 모드를 사용하지 않는 것이 좋습니다. 파이버 모드를 사용하면 컨텍스트 전환을 활용하지 못해 성능이 저하될 수 있으며 SQL Server의 일부 구성 요소가 파이버 모드에서 제대로 작동하지 않을 수 있습니다. 자세한 내용은 lightweight pooling을 참조하세요.

## <a name="thread-and-fiber-execution"></a>스레드 및 파이버 실행

Microsoft Windows에서는 1부터 31까지의 숫자 우선 순위 시스템을 사용하여 스레드 실행 일정을 예약합니다. 0은 운영 체제용으로 예약됩니다. 여러 스레드가 실행을 위해 대기하고 있을 때 Windows에서는 우선 순위가 가장 높은 스레드를 디스패치합니다.

기본적으로 각 SQL Server 인스턴스의 우선 순위는 보통 우선 순위인 7입니다. 이 기본값은 다른 응용 프로그램에 나쁜 영향을 주지 않고 SQL Server 스레드가 충분한 CPU 리소스를 얻을 수 있는 우선 순위를 제공합니다. 

[priority boost](../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) 구성 옵션을 사용하면 SQL Server 인스턴스 스레드의 우선 순위를 13으로 높일 수 있습니다. 13으로 높일 수 있습니다. 이 설정은 대부분의 다른 응용 프로그램보다 높은 우선 순위를 SQL Server 스레드에 제공합니다. 따라서 SQL Server 스레드는 일반적으로 실행할 준비가 될 때마다 디스패치되고 다른 응용 프로그램의 스레드에 의해 미리 점유되지 않습니다. 이는 서버가 SQL Server 인스턴스만 실행하고 다른 응용 프로그램은 실행하지 않을 때 성능을 향상시킬 수 있습니다. 그러나 메모리 집중형 작업이 SQL Server에서 발생할 경우 대개는 다른 응용 프로그램이 SQL Server 스레드를 미리 점유할 만큼 충분히 높은 우선 순위를 갖고 있지 않습니다. 

컴퓨터에서 SQL Server의 여러 인스턴스를 실행하고 일부 인스턴스에 대해서만 priority boost 옵션이 설정되어 있는 경우 보통 우선 순위에서 실행되는 인스턴스의 성능에 나쁜 영향을 줄 수 있습니다. 또한 priority boost가 설정되어 있으면 서버의 다른 응용 프로그램 및 구성 요소의 성능도 저하될 수 있습니다. 따라서 엄격하게 제어되는 환경에서만 이 설정을 사용해야 합니다.


## <a name="hot-add-cpu"></a>Hot Add CPU

Hot add CPU는 실행 중인 시스템에 CPU를 동적으로 추가할 수 있는 기능입니다. CPU는 새 하드웨어를 추가하여 물리적으로 추가하거나, 온라인으로 하드웨어를 분할하여 논리적으로 추가하거나, 가상화 계층을 통해 가상으로 추가할 수 있습니다. SQL Server 2008부터 SQL Server는 hot add CPU를 지원합니다.

hot add CPU 요구 사항  
* hot add CPU를 지원하는 하드웨어
* 64비트 버전의 Windows Server 2008 Datacenter 또는 Itanium 기반 시스템 운영 체제용 Windows Server 2008 Enterprise Edition
* SQL Server Enterprise
* SQL Server는 소프트 NUMA를 사용하도록 구성할 수 없음. 소프트 NUMA에 대한 자세한 내용은 [Soft-NUMA(SQL Server)](../database-engine/configure-windows/soft-numa-sql-server.md)를 참조하세요.

SQL Server는 CPU가 추가된 후에 CPU 사용을 자동으로 시작하지 않습니다. 따라서 SQL Server에서 다른 용도로 추가되었을 수 있는 CPU를 사용하지 않도록 방지할 수 있습니다. CPU를 추가한 후 [RECONFIGURE](../t-sql/language-elements/reconfigure-transact-sql.md) 문을 실행하면 SQL Server에서 새로운 CPU를 사용할 수 있는 리소스로 인식하게 됩니다.

> [!NOTE]
> [affinity64 mask](../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) 가 구성된 경우 새로운 CPU를 사용하도록 affinity64 mask를 수정해야 합니다.
 

## <a name="best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus"></a>CPU 개수가 64개를 초과하는 컴퓨터에서 SQL Server를 실행하기 위한 최선의 방법

### <a name="assigning-hardware-threads-with-cpus"></a>CPU와 함께 하드웨어 스레드 할당

특정 스레드에 프로세서를 바인딩하는 데 선호도 마스크 및 affinity64 마스크 서버 구성 옵션을 사용하지 마세요. 이러한 옵션은 CPU가 최대 64개일 때만 사용할 수 있습니다. 대신 [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) 의 SET PROCESS AFFINITY 옵션을 사용하세요.

### <a name="managing-the-transaction-log-file-size"></a>트랜잭션 로그 파일 크기 관리

트랜잭션 로그 파일의 크기를 늘리려면 자동 증가에 의존하지 마십시오. 트랜잭션 로그를 늘리는 작업은 직렬 프로세스로 수행되어야 합니다. 로그를 확장하면 로그 확장이 끝날 때까지 트랜잭션 쓰기 작업이 수행되지 않을 수 있습니다. 대신 환경의 일반적인 작업량을 지원할 수 있는 값으로 파일 크기를 설정하여 로그 파일에 충분한 공간을 미리 할당합니다.

### <a name="setting-max-degree-of-parallelism-for-index-operations"></a>인덱스 작업을 위한 최대 병렬 처리 수준 설정

CPU가 여러 개인 컴퓨터에서 데이터베이스의 복구 모델을 임시로 대량 로그 또는 단순 복구 모델로 설정하여 인덱스 만들기 또는 다시 작성과 같은 인덱스 작업의 성능을 향상시킬 수 있습니다. 이러한 인덱스 작업으로 인해 상당한 로그 작업이 수행될 수 있으며 로그 경합으로 인해 SQL Server에서 선택하는 최상의 DOP(병렬 처리 수준)에 영향이 있을 수 있습니다.

또한 조정 하는 것이 좋습니다는 **최대 병렬 처리 수준 (MAXDOP)** 이러한 작업에 대 한 서버 구성 옵션입니다. 다음 지침은 내부 테스트를 기반으로 하며 일반적인 권장 사항입니다. 몇 가지 MAXDOP 설정을 사용해 보고 사용 환경에 최적인 설정을 확인해야 합니다.

* 전체 복구 모델의 경우 max degree of parallelism 옵션 값은 8 이하로 설정해야 합니다.   
* 대량 로그 모델 또는 단순 복구 모델의 경우에는 max degree of parallelism 옵션 값을 8보다 크게 설정하는 것이 좋습니다.   
* NUMA가 구성된 서버에서는 최대 병렬 처리 수준이 각 NUMA 노드에 할당된 CPU 수를 초과하면 안 됩니다. 이는 쿼리가 1개의 NUMA 노드에서 로컬 메모리를 사용할 가능성이 높고 이 경우 메모리 액세스 시간을 개선할 수 있기 때문입니다.  
* 에 대 한 MAXDOP 값 논리 프로세서 보다는 실제 프로세서의 수를 초과 하지 않아야, 하이퍼 스레딩 가진 서버에 사용 하도록 설정 되었고 2009 년에 제조 또는 (하이퍼 스레딩 기능 향상 되었습니다) 전에 이전 버전입니다.

Max degree of parallelism 옵션에 대 한 자세한 내용은 참조 [max degree of parallelism 서버 구성 옵션 구성](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)합니다.

### <a name="setting-the-maximum-number-of-worker-threads"></a>최대 작업자 스레드 수 설정

최대 작업자 스레드 수는 항상 최대 병렬 처리 수준에 대한 설정보다 높게 설정합니다. 작업자 스레드 수는 항상 서버에 있는 CPU 수의 7배 이상의 값으로 설정해야 합니다. 자세한 내용은 [Configure the max worker threads Option](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)(최대 작업자 스레드 수 옵션 구성)을 참조하세요.

### <a name="using-sql-trace-and-sql-server-profiler"></a>SQL 추적 및 SQL Server Profiler 사용

 프로덕션 환경에서는 SQL 추적과 SQL Server Profiler를 사용하지 않는 것이 좋습니다. CPU 수가 늘어날수록 이러한 도구의 실행으로 인한 오버헤드도 늘어납니다. 프로덕션 환경에서 SQL 추적을 사용해야 하는 경우 추적 이벤트의 수를 최소로 제한합니다. 부하를 고려하여 주의 깊게 각 추적 이벤트를 프로파일링 및 테스트해야 하며 성능에 많은 영향을 주는 이벤트를 조합해서 사용하지 마십시오.

### <a name="setting-the-number-of-tempdb-data-files"></a>tempdb 데이터 파일 수 설정

일반적으로 tempdb 데이터 파일 수는 CPU 수와 일치해야 합니다. 하지만 tempdb에 대한 동시성 요구를 신중하게 고려하면 데이터베이스 관리 작업을 줄일 수 있습니다. 예를 들어 시스템에 64개의 CPU가 있고 일반적으로 32개의 쿼리에서만 tempdb를 사용하는 경우 tempdb 파일의 수를 64개로 늘려도 성능이 개선되지 않습니다.

### <a name="sql-server-components-that-can-use-more-than-64-cpus"></a>64개를 초과하는 CPU를 사용할 수 있는 SQL Server 구성 요소

다음 표에서는 SQL Server 구성 요소를 나열하고 이들 구성 요소가 64개를 초과하는 CPU를 사용할 수 있는지를 보여 줍니다.

|프로세스 이름   |실행 프로그램 |64개를 초과하는 CPU 사용 |  
|----------|----------|----------|  
|SQL Server 데이터베이스 엔진 |Sqlserver.exe  |예 |  
|Reporting Services |Rs.exe |아니오 |  
|Analysis Services  |As.exe |아니오 |  
|Integration Services   |Is.exe |아니오 |  
|Service Broker |Sb.exe |아니오 |  
|전체 텍스트 검색   |Fts.exe    |아니오 |  
|SQL Server 에이전트   |Sqlagent.exe   |아니오 |  
|SQL Server Management Studio   |Ssms.exe   |아니오 |  
|SQL Server 설치   |Setup.exe  |아니오 |  



