---
title: SQL Server on Linux의 성능 모범 사례
description: 이 문서에서는 SQL Server on Linux를 실행하기 위한 성능 모범 사례 및 지침을 제공합니다.
author: rgward
ms.author: bobward
ms.reviewer: vanto
ms.date: 09/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 543488eada46a088f3c634ce2326c7e2db2a97a5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68105438"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>SQL Server on Linux의 성능 모범 사례 및 구성 지침

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 SQL Server on Linux에 연결하는 데이터베이스 애플리케이션의 성능을 최대화하기 위한 모범 사례 및 권장 사항을 제공합니다. 이 권장 사항은 Linux 플랫폼에서 실행하는 경우에 해당됩니다. 인덱스 디자인과 같은 일반적인 SQL Server 권장 사항은 모두 그대로 적용됩니다.

다음 지침에는 SQL Server 및 Linux 운영 체제를 구성하기 위한 권장 사항이 포함되어 있습니다.

## <a name="sql-server-configuration"></a>SQL Server 구성

애플리케이션 성능을 최대화하려면 SQL Server on Linux를 설치한 후에 다음 구성 작업을 수행하는 것이 좋습니다.

### <a name="best-practices"></a>모범 사례

- **노드 및/또는 CPU에 대해 PROCESS AFFINITY 사용**

   `ALTER SERVER CONFIGURATION`을 사용하여 Linux 운영 체제에서 SQL Server(일반적으로 모든 NODE 및 CPU에 사용됨)에 사용되는 모든 `PROCESS AFFINITY`NUMANODE**및/또는 CPU에 대해**를 설정하는 것이 좋습니다. 프로세서 선호도는 효율적인 Linux 및 SQL 예약 동작을 유지 관리하는 데 도움이 됩니다. **NUMANODE** 옵션을 사용하는 것이 가장 간단한 방법입니다. 컴퓨터에 NUMA 노드가 하나뿐인 경우에도 **PROCESS AFFINITY**를 사용해야 합니다.  [PROCESS AFFINITY](../t-sql/statements/alter-server-configuration-transact-sql.md)를 설정하는 방법에 대한 자세한 내용은 **ALTER SERVER CONFIGURATION** 설명서를 참조하세요.

- **여러 tempdb 데이터 파일 구성**

   SQL Server on Linux 설치는 여러 tempdb 파일을 구성하는 옵션을 제공하지 않으므로 설치 후에 여러 tempdb 데이터 파일을 만드는 것이 좋습니다. 자세한 내용은 [SQL Server tempdb 데이터베이스에서 할당 경합을 줄이기 위한 권장 사항](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d) 문서의 지침을 참조하세요.

### <a name="advanced-configuration"></a>고급 구성

다음 권장 사항은 SQL Server on Linux 설치 후에 수행할 수 있는 선택적 구성 설정입니다. 이러한 선택 사항은 Linux 운영 체제의 워크로드 및 구성 요구 사항에 따라 다릅니다.

- **mssql-conf를 사용하여 메모리 한도 설정**

   Linux 운영 체제가 충분한 실제 메모리를 사용할 수 있도록 하기 위해 SQL Server 프로세스는 기본적으로 물리적 RAM의 80%만 사용합니다. 물리적 RAM 양이 많은 일부 시스템의 경우 20%도 상당한 크기일 수 있습니다. 예를 들어 RAM이 1TB인 시스템에서 기본 설정을 사용할 경우 약 200GB RAM이 사용되지 않는 상태로 유지됩니다. 이런 상황에서는 메모리 한도를 더 큰 값으로 구성하는 것이 좋습니다. SQL Server에 표시되는 메모리(MB 단위)를 제어하는 **memory.memorylimitmb** 설정과 [mssql-conf](sql-server-linux-configure-mssql-conf.md#memorylimit) 도구는 설명서를 참조하세요.

   이 설정을 변경하는 경우 값을 너무 높게 설정하지 않도록 주의합니다. 충분한 메모리를 유지하지 않으면 Linux 운영 체제와 기타 Linux 애플리케이션에서 문제가 발생할 수 있습니다.

## <a name="linux-os-configuration"></a>Linux OS 구성

SQL Server 설치의 성능을 최대화하려면 다음 Linux 운영 체제 구성 설정을 사용하는 것이 좋습니다.

### <a name="kernel-settings-for-high-performance"></a>고성능을 위한 커널 설정
이 설정은 SQL Server 설치의 고성능 및 처리량과 관련해서 권장되는 Linux 운영 체제 설정입니다. 이 설정을 구성하는 프로세스는 해당 Linux 운영 체제 설명서를 참조하세요.



> [!Note]
> RHEL(Red Hat Enterprise Linux) 사용자의 경우 처리량-성능 프로필에서 이러한 설정을 자동으로 구성합니다(C-States 제외).

다음 표에서는 CPU 설정 권장 사항을 제공합니다.

| 설정 | 값 | 자세한 정보 |
|---|---|---|
| CPU frequency governor | 성능 | **cpupower** 명령을 참조하세요. |
| ENERGY_PERF_BIAS | 성능 | **x86_energy_perf_policy** 명령을 참조하세요. |
| min_perf_pct | 100 | intel p-state는 해당 설명서를 참조하세요. |
| C-States | C1 only | C-States가 C1 only로 설정되었는지 확인하는 방법은 해당 Linux 또는 시스템 설명서를 참조하세요. |

다음 표에서는 디스크 설정 권장 사항을 제공합니다.

| 설정 | 값 | 자세한 정보 |
|---|---|---|
| disk readahead | 4096 | **blockdev** 명령을 참조하세요. |
| sysctl settings | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness = 10 | **sysctl** 명령을 참조하세요. |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>다중 노드 NUMA 시스템의 커널 설정 auto numa balancing

다중 노드 **NUMA** 시스템에서 SQL Server를 설치하는 경우 다음과 같은 **kernel.numa_balancing** 커널 설정이 기본적으로 사용하도록 설정됩니다. SQL Server가 **NUMA** 시스템에서 최대한 효율적으로 작동할 수 있게 하려면 다중 노드 NUMA 시스템에서 auto numa balancing을 사용하지 않도록 설정합니다.

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>가상 주소 공간의 커널 설정

**vm.max_map_count**의 기본 설정(65536)이 SQL Server 설치에 충분히 높지 않을 수 있습니다. 이 값(상한)을 256K로 변경합니다.

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>SQL Server 데이터 및 로그 파일에 대해 파일 시스템의 마지막으로 액세스한 날짜/시간 사용 안 함

SQL Server 데이터와 로그 파일을 저장하는 데 사용되는 모든 파일 시스템에서 **noatime** 특성을 사용합니다. 이 특성을 설정하는 방법은 해당 Linux 설명서를 참조하세요.

### <a name="leave-transparent-huge-pages-thp-enabled"></a>THP(Transparent Huge Pages)를 사용 상태로 유지

대부분의 Linux 설치에서는 이 옵션이 기본적으로 설정되어 있어야 합니다. 가장 일관된 성능을 유지하려면 이 구성 옵션을 사용 상태로 유지하는 것이 좋습니다.

### <a name="swapfile"></a>swapfile

메모리 부족 문제를 방지하려면 올바르게 구성된 swapfile이 있어야 합니다. swapfile을 만들고 올바른 크기를 지정하는 방법은 해당 Linux 설명서를 참조하세요.

### <a name="virtual-machines-and-dynamic-memory"></a>Virtual Machines 및 동적 메모리

가상 머신에서 SQL Server on Linux를 실행하는 경우 가상 머신에 대해 예약된 메모리 크기를 수정하는 옵션을 선택해야 합니다. Hyper-V 동적 메모리와 같은 기능을 사용하지 않도록 합니다.

## <a name="next-steps"></a>다음 단계

성능을 향상하는 SQL Server 기능에 대한 자세한 내용은 [성능 기능 시작](sql-server-linux-performance-get-started.md)을 참조하세요.

SQL Server on Linux에 대한 자세한 내용은 [SQL Server on Linux 개요](sql-server-linux-overview.md)를 참조하세요.
