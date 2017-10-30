---
title: "Linux에서 SQL Server에 대 한 성능 모범 사례 | Microsoft Docs"
description: "이 항목에서는 SQL Server 2017 Linux에서 실행 하기 위한 성능 모범 사례 및 지침 제공."
author: rgward
ms.author: bobward
manager: jhubbard
ms.date: 09/14/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 18d40800ee74783b0ce3df4d9d4e0458fbb72ebb
ms.contentlocale: ko-kr
ms.lasthandoff: 10/02/2017

---

# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-2017-on-linux"></a>성능에 대 한 유용한 정보 및 SQL Server 2017 linux에 대 한 구성 지침

이 항목에서는 모범 사례 및 Linux에서 SQL Server에 연결 하는 데이터베이스 응용 프로그램에 대 한 성능을 최대화 하기 위해 권장 사항을 제공 합니다. 이러한 권장 사항은 Linux 플랫폼에서 실행 됩니다. 모든 표준 SQL Server 권장 사항, 같은 인덱스 디자인 계속 적용 됩니다.

다음 지침에는 SQL Server와 Linux 운영 체제를 구성 하기 위한 권장 사항을 포함 합니다.

## <a name="sql-server-configuration"></a>SQL Server 구성

Linux 응용 프로그램에 대 한 최상의 성능을 얻으려면 SQL Server를 설치한 후 다음 구성 작업을 수행 하는 것이 좋습니다.

### <a name="best-practices"></a>최선의 구현 방법

- **노드 및/또는 Cpu에 대 한 프로세스 선호도 사용 하 여**

   사용 하는 것이 좋습니다. `ALTER SERVER CONFIGURATION` 설정 하려면 `PROCESS AFFINITY` 모든는 **NUMANODEs** Cpu 사용 하는 SQL Server (이 일반적으로 모든 노드 및 Cpu에 대 한)에 대 한 Linux 운영 체제에서 및/또는 합니다. 프로세서 선호도 효율적인 Linux와 SQL 예약 동작을 유지 하는 데 도움이 됩니다. 사용 하 여 **NUMANODE** 옵션은 가장 간단한 방법입니다. 주의 기울여야 **프로세스 선호도** 컴퓨터에 NUMA 노드 중 하나만 있는 경우에 합니다.  참조는 [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) 설정 하는 방법에 대 한 자세한 내용은 설명서 **프로세스 선호도**합니다.

- **Tempdb 데이터 파일이 여러 개를 구성 합니다.**

   Linux 설치에 SQL Server tempdb 파일이 여러 개를 구성 하는 옵션을 제공 하지 않으므로, 설치 후 여러 tempdb 데이터 파일을 만드는 고려 하는 것이 좋습니다. 자세한 내용은 문서에서 지침을 참조 하세요. [권장 사항은 SQL Server tempdb 데이터베이스의 할당 경합을 줄이려면](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d)합니다.

### <a name="advanced-configuration"></a>고급 구성

다음 권장 사항을 선택적 구성 하는 설정이 Linux에서 SQL Server 설치 후에 수행 하도록 선택할 수 있습니다. 이러한 선택 작업와 Linux 운영 체제의 구성 요구 사항을 기반으로 합니다.

- **Mssql conf와 메모리 제한을 설정합니다**

   Linux 운영 체제에 대 한 사용 가능한 실제 메모리가 충분 한지 확인을 위해 SQL Server 프로세스는 기본적으로 실제 RAM의 80%를 사용 합니다. 20% 수 있습니다는 많은 양의 실제 RAM 일부 시스템에 대 한 많은 수 있습니다. 예를 들어 ram 1TB 시스템에서는에서 기본 설정으로 인해 약 200 g B ram 사용 하지 않는 합니다. 이 경우 더 큰 값으로 메모리 제한을 구성 하는 것이 좋습니다. 설명서를 참조는 **mssql conf** 도구 및 [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) 메모리 (MB 단위)에 SQL Server에 표시를 제어 하는 설정입니다.

   이 설정을 변경할 때이 값을 너무 높게 설정 하지 않도록 주의 수입니다. 충분 한 메모리를 생략 하지 않는 Linux 운영 체제 및 기타 Linux 응용 프로그램에 문제가 발생할 수 있습니다.

## <a name="linux-os-configuration"></a>Linux 운영 체제 구성

다음과 같은 Linux 운영 체제 구성 설정을 사용 하 여 SQL Server 설치에 대 한 최상의 성능을 경험할 수 하는 것이 좋습니다.

### <a name="kernel-settings-for-high-performance"></a>고성능에 대 한 커널 설정

이들은 권장 Linux 운영 체제 설정 높은 관련 된 성능 및 SQL Server 설치에 대 한 처리량입니다. 이러한 설정을 구성 하는 프로세스에 대 한 Linux 운영 체제 설명서를 참조 하십시오.



> [!Note]
> Red Hat Enterprise Linux (RHEL) 사용자에 대 한 성능 처리량 프로필에는 자동으로 (상태를 제외한 C-) 이러한 설정을 구성 합니다.

다음 표에서 CPU 설정에 대 한 권장 사항을 제공합니다.

| 설정 | 값 | 자세한 정보 |
|---|---|---|
| CPU 주기 관리자 | 성능 | 참조는 **cpupower** 명령 |
| ENERGY_PERF_BIAS | 성능 | 참조는 **x86_energy_perf_policy** 명령 |
| min_perf_pct | 100 | 인텔 p-상태에서 설명서를 참조 하십시오. |
| C 상태 | C 1에만 | C 상태 C1로만 설정 되었는지 확인 하는 방법에 Linux 또는 시스템 설명서를 참조 하십시오. |

다음 표에서 디스크 설정에 대 한 권장 사항을 제공합니다.

| 설정 | 값 | 자세한 정보 |
|---|---|---|
| 미리 읽기가 디스크 | 4096 | 참조는 **blockdev** 명령 |
| sysctl 설정 | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns 15000000 =<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness=10 | 참조는 **sysctl** 명령 |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>다중 노드 NUMA 시스템에 대 한 분산 커널 설정 자동 numa

다중 노드에 SQL Server를 설치 하는 경우 **NUMA** 시스템, 다음 **kernel.numa_balancing** 커널 설정이 기본적으로 사용 됩니다. SQL server에 최대 효율을에서 작동 하도록 하는 **NUMA** 시스템, 사용 안 함 자동 numa는 다중 노드 NUMA 시스템에 분산:

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>가상 주소 공간에 대 한 커널 설정

기본 설정은 **vm.max_map_count** (65536은)는 SQL Server 설치 수 있을 정도로 충분히 높은 수 없습니다. 256 K입니다 (즉, 상한값)이이 값을 변경 합니다.

```bash
sysctl -w vm.max_map_count 262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>마지막으로 액세스 한 날짜/시간에서 파일 시스템에 SQL Server 데이터 및 로그 파일에 대 한 사용 안 함

사용 하 여는 **noatime** SQL Server 데이터를 저장 하 고 로그 파일에 사용 되는 모든 파일 시스템을 사용 하 여 특성입니다. 이 특성을 설정 하는 방법에 Linux 설명서를 참조 하십시오.

### <a name="leave-transparent-huge-pages-thp-enabled"></a>투명 한 거 대 한 페이지 (THP) 사용 하도록 설정 그대로 둡니다.

대부분의 Linux 설치 기본적으로의이 옵션을 해야 합니다. 이 구성 옵션을 사용 하도록 설정 하려면 가장 일관 된 성능 경험에 대 한 것이 좋습니다.

### <a name="swapfile"></a>스왑 파일

모든 메모리가 부족 한 문제를 방지 하기 위해는 올바르게 구성 된 스왑 파일 확인 합니다. 만들고 제대로 스왑 파일 크기를 하는 방법에 대 한 Linux 설명서를 참조 하십시오.

### <a name="virtual-machines-and-dynamic-memory"></a>가상 컴퓨터와 동적 메모리

Linux에서 SQL Server를 실행 하는 가상 컴퓨터에는, 경우에 가상 컴퓨터에 대 한 예약 된 메모리의 양을 해결할 수 있는 옵션을 선택 확인 합니다. Hyper-v 동적 메모리와 같은 기능을 사용 하지 마십시오.

## <a name="next-steps"></a>다음 단계

성능을 향상 시키는 SQL Server 기능에 대 한 자세한 참조 [성능 기능을 시작](sql-server-linux-performance-get-started.md)합니다.

Linux에서 SQL Server에 대 한 자세한 내용은 참조 [linux 개요 SQL Server의](sql-server-linux-overview.md)합니다.

