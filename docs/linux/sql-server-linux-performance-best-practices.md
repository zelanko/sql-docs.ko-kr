---
title: SQL Server on Linux의 성능 모범 사례
description: 이 문서에서는 SQL Server on Linux를 실행하기 위한 성능 모범 사례 및 지침을 제공합니다.
author: tejasaks
ms.author: tejasaks
ms.reviewer: vanto
ms.date: 12/11/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 89b8a7c087fb87ed911be640126ec81021b045a7
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97323516"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>SQL Server on Linux의 성능 모범 사례 및 구성 지침

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 SQL Server on Linux에 연결하는 데이터베이스 애플리케이션의 성능을 최대화하기 위한 모범 사례 및 권장 사항을 제공합니다. 이 권장 사항은 Linux 플랫폼에서 실행하는 경우에 해당됩니다. 인덱스 디자인과 같은 일반적인 SQL Server 권장 사항은 모두 그대로 적용됩니다.

다음 지침에는 SQL Server 및 Linux OS(운영 체제)를 구성하기 위한 권장 사항이 포함되어 있습니다.

## <a name="linux-os-configuration"></a>Linux OS 구성

SQL Server 설치의 성능을 최대화하려면 다음 Linux OS 구성 설정을 사용하는 것이 좋습니다.

### <a name="storage-configuration-recommendation"></a>스토리지 구성 권장 사항

#### <a name="use-storage-subsystem-with-appropriate-iops-throughput-and-redundancy"></a>IOPS, 처리량, 중복도가 적절한 스토리지 하위 시스템 사용

데이터, 트랜잭션 로그 및 기타 관련 파일(예: 메모리 내 OLTP에 대한 검사점 파일)을 호스팅하는 스토리지 하위 시스템은 평균 워크로드와 최대 워크로드를 모두 정상적으로 관리할 수 있어야 합니다. 일반적으로 온-프레미스 환경에서 스토리지 공급업체는 여러 디스크에서 스트라이프하는 적절한 하드웨어 RAID 구성을 지원하여 적절한 IOPS, 처리량, 중복도를 보장합니다. 그러나 스토리지 공급업체와 다양한 아키텍처를 사용하는 스토리지 제품마다 다를 수 있습니다.

Azure Virtual Machine에 배포된 SQL Server on Linux의 경우 소프트웨어 RAID를 사용하여 적절한 IOPS 및 처리량 요구 사항이 충족되도록 하는 것이 좋습니다. Azure 가상 머신에서 SQL Server를 구성하는 경우 유사한 스토리지 고려 사항에 대해서는 다음 문서를 참조하세요. [SQL Server VM에 대한 스토리지 구성](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/storage-configuration)

다음은 Azure Virtual Machine의 Linux에서 소프트웨어 RAID를 만드는 방법에 대한 예제입니다. 예제는 아래와 같이 제공되지만 데이터, 트랜잭션 로그, tempdb IO 요구 사항에 따라 볼륨에 필요한 처리량 및 IOPS에 적절한 수의 데이터 디스크를 사용해야 합니다. 이 예제에서는 8개의 데이터 디스크가 Azure 가상 머신에 연결되었습니다. 4개는 호스트 데이터 파일에 연결되고, 2개는 트랜잭션 로그용으로, 2개는 tempdb 워크로드용으로 연결되었습니다.

```bash
# To locate the devices (for example /dev/sdc) for RAID creation, use the lsblk command
# For Data volume, using 4 devices, in RAID 5 configuration with 8KB stripes
mdadm --create --verbose /dev/md0 --level=raid5 --chunk=8K --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf

# For Log volume, using 2 devices in RAID 10 configuration with 64KB stripes
mdadm --create --verbose /dev/md1 --level=raid10 --chunk=64K --raid-devices=2 /dev/sdg /dev/sdh

# For tempdb volume, using 2 devices in RAID 0 configuration with 64KB stripes
mdadm --create --verbose /dev/md2 --level=raid0 --chunk=64K --raid-devices=2 /dev/sdi /dev/sdj
```

#### <a name="file-system-configuration-recommendation"></a>파일 시스템 구성 권장 사항

SQL Server는 데이터베이스, 트랜잭션 로그 및 추가 파일(예: SQL Server의 메모리 내 OLTP에 대한 검사점 파일)을 호스트하는 EXT4 및 XFS 파일 시스템을 모두 지원합니다. SQL Server 데이터 및 트랜잭션 로그 파일을 호스팅하는 데는 XFS 파일 시스템을 사용하는 것이 좋습니다.

```bash
# Formatting the volume with XFS filesystem
mkfs.xfs /dev/md0 -f -L datavolume
mkfs.xfs /dev/md1 -f -L logvolume
mkfs.xfs /dev/md2 -f -L tempdb
```

> [!NOTE]
> XFS 볼륨을 만들고 포맷할 때 대/소문자를 구분하지 않도록 XFS 파일 시스템을 구성할 수 있습니다. Linux 에코시스템에서 자주 사용되는 구성은 아니지만 호환성을 위해 사용할 수는 있습니다.
>
> 예제: mkfs.xfs /dev/md0 -f -n version=ci -L datavolume
>
> 이 예제에서 `-n version=ci` 매개 변수는 대/소문자를 구분하지 않도록 XFS 파일 시스템을 구성하는 데 사용됩니다.

##### <a name="persistent-memory-filesystem-recommendation"></a>영구 메모리 파일 시스템 권장 사항

영구 메모리 디바이스의 파일 시스템 구성을 위한 기본 파일 시스템의 블록 할당은 2MB여야 합니다. 이 항목에 대한 자세한 내용은 [기술 고려 사항](sql-server-linux-configure-pmem.md#technical-considerations)을 검토하세요.

#### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>SQL Server 데이터 및 로그 파일에 대해 파일 시스템의 마지막으로 액세스한 날짜/시간 사용 안 함

시스템에 연결된 드라이브가 다시 부팅 후 자동으로 다시 탑재되도록 하려면 `/etc/fstab` 파일에 추가해야 합니다. 또한 `/etc/fstab`에서 UUID(Universally Unique Identifier)를 사용하여 디바이스 이름(예: `/dev/sdc1`)만이 아니라 드라이브를 나타내는 것이 좋습니다.

SQL Server 데이터와 로그 파일을 저장하는 데 사용되는 모든 파일 시스템에서 **noatime** 특성을 사용하는 것이 좋습니다. 이 특성을 설정하는 방법은 해당 Linux 설명서를 참조하세요. Azure 가상 머신에 탑재된 볼륨에 대해 **noatime** 옵션을 사용하도록 설정하는 방법에 대한 예제는 다음과 같습니다.

**_/etc/fstab_* _의 탑재 지점 항목

```bash
UUID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" /data1 xfs,rw,attr2,noatime 0 0
```

위의 예제에서 UUID는 _*_blkid_*_ 명령을 사용하여 찾을 수 있는 디바이스를 나타냅니다.

#### <a name="sql-server-and-forced-unit-access-fua-io-subsystem-capability"></a>SQL Server 및 FUA(Forced Unit Access) I/O 하위 시스템 기능

특정 버전의 지원되는 Linux 배포에서는 FUA I/O 하위 시스템 기능을 지원하여 데이터 내구성을 제공합니다. SQL Server는 FUA 기능을 사용하여 SQL Server 워크로드에 대해 매우 효율적이고 안정적인 I/O를 제공합니다. Linux 배포의 FUA 지원과 SQL Server에 미치는 영향에 대한 자세한 내용은 [SQL Server On Linux: Forced Unit Access (FUA) Internals](https://bobsql.com/sql-server-on-linux-forced-unit-access-fua-internals/)(SQL Server On Linux: FUA(Forced Unit Access) 내부) 블로그를 참조하세요.

SUSE Linux Enterprise Server 12 SP5 및 Red Hat Enterprise Linux 8.0 이상은 I/O 하위 시스템에서 FUA 기능을 지원합니다. SQL Server 2017 CU6 이상이나 SQL Server 2019를 사용하고 있는 경우 SQL Server에서 FUA를 사용하여 성능이 뛰어나고 효율적인 I/O를 구현하려면 다음 구성을 사용해야 합니다.

다음 조건이 충족되는 경우 아래에 나열된 권장 구성을 사용합니다.

- SQL Server 2017 CU6 이상 또는 SQL Server 2019 사용
- FUA 기능을 지원하는 Linux 배포 및 버전(Red Hat Enterprise Linux 8.0 이상 또는 SUSE Linux Enterprise Server 12 SP5) 사용
- FUA 기능을 지원하고 이 기능용으로 구성된 스토리지 하위 시스템 및/또는 하드웨어

권장 구성:

1. 추적 플래그 3979를 시작 매개 변수로 사용
2. _ *mssql-conf**를 사용하여 `control.writethrough = 1` 및 `control.alternatewritethrough = 0` 구성

위의 조건을 충족하지 않는 거의 모든 다른 구성에서 권장되는 구성은 다음과 같습니다.

1. 추적 플래그 3982를 시작 매개 변수로 사용(Linux 에코시스템의 SQL Server인 경우 기본값)하여 추적 플래그 3979가 시작 매개 변수로 사용되지 않도록 함
2. **mssql-conf** 를 사용하여 `control.writethrough = 1` 및 `control.alternatewritethrough = 1` 구성

### <a name="kernel-and-cpu-settings-for-high-performance"></a>고성능을 위한 커널 및 CPU 설정

다음 섹션에서는 SQL Server 설치의 고성능 및 처리량과 관련하여 권장되는 Linux OS 설정에 대해 설명합니다. 이 설정을 구성하는 프로세스는 Linux OS 설명서를 참조하세요. 설명된 대로 [**_Tuned_* _](https://tuned-project.org)를 사용하면 아래에 설명된 많은 CPU 및 커널을 구성하는 데 도움이 됩니다.

#### <a name="using-__tuned__-to-configure-kernel-settings"></a>_*_Tuned_*_ 를 사용하여 Kernel 설정 구성

RHEL(Red Hat Enterprise Linux) 사용자의 경우 [Tuned](https://tuned-project.org) 처리량-성능 프로필에서 일부 커널 및 CPU 설정을 자동으로 구성합니다(C-States 제외). RHEL 8.0부터 _ *mssql**이라는 _*_Tuned_*_ 프로필은 Red Hat과 공동으로 개발되었으며 SQL Server 워크로드에 대해 더욱 정교한 Linux 성능 관련 조정을 제공합니다. 이 프로필은 RHEL 처리량-성능 프로필을 포함하므로 Microsoft는 이 프로필 없이 다른 Linux 배포판 및 RHEL 릴리스와 함께 검토를 위해 다음의 정의를 제공합니다.

SUSE Linux Enterprise Server 12 SP5, Ubuntu 18.04 및 Red Hat Enterprise Linux 7.x에서는 **_Tuned_ *_ 패키지를 수동으로 설치할 수 있습니다. 아래에 설명된 대로 _* mssql** 프로필을 만들고 구성하는 데 사용할 수 있습니다.

##### <a name="proposed-linux-settings-using-a-tuned-mssql-profile"></a>Tuned mssql 프로필을 사용하는 권장 Linux 설정

```bash
#
# A Tuned configuration for SQL Server on Linux
#

[main]
summary=Optimize for Microsoft SQL Server
include=throughput-performance

[cpu]
force_latency=5

[sysctl]
vm.swappiness = 1
vm.dirty_background_ratio = 3
vm.dirty_ratio = 80
vm.dirty_expire_centisecs = 500
vm.dirty_writeback_centisecs = 100
vm.transparent_hugepages=always
# For multi-instance SQL deployments, use
# vm.transparent_hugepages=madvise
vm.max_map_count=1600000
net.core.rmem_default = 262144
net.core.rmem_max = 4194304
net.core.wmem_default = 262144
net.core.wmem_max = 1048576
kernel.numa_balancing=0
kernel.sched_latency_ns = 60000000
kernel.sched_migration_cost_ns = 500000
kernel.sched_min_granularity_ns = 15000000
kernel.sched_wakeup_granularity_ns = 2000000
```

이 Tuned 프로필을 사용하려면 `/usr/lib/tuned/mssql` 폴더 아래의 **tuned.conf** 파일에 이러한 정의를 저장하고 다음 명령을 사용하여 프로필을 사용하도록 설정합니다.

```bash
chmod +x /usr/lib/tuned/mssql/tuned.conf
tuned-adm profile mssql
```

다음 명령을 사용하여 사용하도록 설정되었는지 확인합니다.

```bash
tuned-adm active
```

또는

```bash
tuned-adm list
```

#### <a name="cpu-settings-recommendation"></a>CPU 설정 권장 사항

다음 표에서는 CPU 설정 권장 사항을 제공합니다.

| 설정 | 값 | 자세한 정보 |
|---|---|---|
| CPU frequency governor | 성능 | **cpupower** 명령을 참조하세요. |
| ENERGY_PERF_BIAS | 성능 | **x86_energy_perf_policy** 명령을 참조하세요. |
| min_perf_pct | 100 | intel p-state는 해당 설명서를 참조하세요. |
| C-States | C1 only | C-States가 C1 only로 설정되었는지 확인하는 방법은 해당 Linux 또는 시스템 설명서를 참조하세요. |

앞에서 설명한 대로 **_Tuned_ *_를 사용하면 _* mssql** 프로필의 기반으로 사용되는 처리량-성능 프로필로 인해 CPU frequency governor, ENERGY_PERF_BIAS 및 min_perf_pct 설정이 적절하게 자동으로 구성됩니다. C-States 매개 변수는 Linux 또는 시스템 배포자가 제공한 설명서에 따라 수동으로 구성해야 합니다.

#### <a name="disk-settings-recommendations"></a>디스크 설정 권장 사항

다음 표에서는 디스크 설정 권장 사항을 제공합니다.

| 설정 | 값 | 자세한 정보 |
|---|---|---|
| 디스크 `readahead` | 4096 | `blockdev` 명령을 참조하세요. |
| sysctl settings | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness = 1 | **sysctl** 명령을 참조하세요. |

**설명:**

- **vm.swappiness**: 이 매개 변수는 SQL Server 프로세스 메모리 페이지를 교체하도록 커널을 제한하여 런타임 메모리 교체에 지정된 상대적 가중치를 제어합니다.

- **vm.dirty_\** _: SQL Server 파일 쓰기 액세스가 캐시되지 않아 데이터 무결성 요구 사항을 충족합니다. 이러한 매개 변수는 효율적인 비동기 쓰기 성능을 허용하며, 플러시를 제한하면서 충분히 큰 캐싱을 허용하여 Linux 캐싱 쓰기의 스토리지 IO 영향을 낮춥니다.

- _*kernel.sched_\**_: 이러한 매개 변수 값은 Linux 커널의 CFS(the Completely Fair Scheduling) 알고리즘 조정에 대한 현재 권장 사항을 나타내며, 프로세스 간 선점 및 스레드 다시 시작과 관련된 네트워크 처리량 및 스토리지 IO 호출을 개선합니다.

_*mssql** **_Tuned_*_ 프로필을 사용하여 _*vm.swappiness**, **vm.dirty_\* *_ 및 _* kernel.sched_\**_ 설정을 구성합니다. `blockdev` 명령을 사용하는 디스크 `readahead` 구성은 디바이스 단위이며 수동으로 수행해야 합니다.

#### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>다중 노드 NUMA 시스템의 커널 설정 auto numa balancing

다중 노드 _ *NUMA** 시스템에 SQL Server를 설치하면 다음 **kernel.numa_balancing** 커널 설정이 기본적으로 사용하도록 설정됩니다. SQL Server가 **NUMA** 시스템에서 최대한 효율적으로 작동할 수 있게 하려면 다중 노드 NUMA 시스템에서 auto numa balancing을 사용하지 않도록 설정합니다.

```bash
sysctl -w kernel.numa_balancing=0
```

**mssql** **_Tuned_ *_ 프로필을 사용하여 _* kernel.numa_balancing** 옵션을 구성합니다.

#### <a name="kernel-settings-for-virtual-address-space"></a>가상 주소 공간의 커널 설정

**vm.max_map_count** 의 기본 설정(65536)이 SQL Server 설치에 충분히 높지 않을 수 있습니다. 이런 이유로, SQL Server 배포의 경우 **vm.max_map_count** 값을 262144 이상으로 변경합니다. 커널 매개 변수의 추가 조정에 대해서는 [Tuned mssql 프로필을 사용하는 권장 Linux 설정](#proposed-linux-settings-using-a-tuned-mssql-profile) 섹션을 참조하세요. vm.max_map_count의 최댓값은 2147483647입니다.

```bash
sysctl -w vm.max_map_count=1600000
```

**mssql** **_Tuned_ *_ 프로필을 사용하여 _* vm.max_map_count** 옵션을 구성합니다.

#### <a name="leave-transparent-huge-pages-thp-enabled"></a>THP(Transparent Huge Pages)를 사용 상태로 유지

대부분의 Linux 설치에서는 이 옵션이 기본적으로 설정되어 있어야 합니다. 가장 일관된 성능을 유지하려면 이 구성 옵션을 사용 상태로 유지하는 것이 좋습니다. 그러나 예를 들어 여러 인스턴스와 함께 SQL Server를 배포하거나 서버에서 메모리 요구 사항이 높은 애플리케이션과 함께 SQL Server를 실행해야 하므로 메모리 페이징 활동이 많은 경우 다음 명령을 실행한 후 애플리케이션 성능을 테스트하는 것이 좋습니다.

```bash
echo madvise > /sys/kernel/mm/transparent_hugepage/enabled
```

또는 다음 줄을 사용하여 **mssql** **_Tuned_* _ 프로필을 수정합니다.

```bash
vm.transparent_hugepages=madvise
```

수정 후 _ *mssql** 프로필을 활성화합니다.

```bash
tuned-adm off
tuned-adm profile mssql
```

**mssql** **_Tuned_ *_ 프로필을 사용하여 _* transparent_hugepage** 옵션을 구성합니다.

#### <a name="additional-advanced-kernelos-configuration"></a>추가 고급 커널/OS 구성

1. 최상의 스토리지 IO 성능을 위해 블록 디바이스에 Linux 다중 큐 일정을 사용하는 것이 좋습니다. 이렇게 하면 고속 SSD(반도체 드라이브) 및 다중 코어 시스템에서 블록 계층 성능이 제대로 스케일링됩니다. Linux 배포에서 기본적으로 사용하도록 설정되어 있는 경우 설명서를 확인하세요. 사용 중인 Linux 배포의 설명서에 추가 지침이 있을 수 있지만 대부분의 경우 **scsi_mod.use_blk_mq=y** 로 커널을 부팅하여 사용하도록 설정합니다. 이는 업스트림 Linux 커널과 일치합니다.

1. 다중 경로 IO는 SQL Server 배포에 자주 사용되므로 **dm_mod.use_blk_mq=y** 커널 부팅 옵션을 사용하도록 설정하여 `blk-mq` 인프라를 사용하도록 DM(디바이스 매퍼) 다중 경로 대상도 구성해야 합니다. 기본값은 `n`(사용 안 함)입니다. 기본 SCSI 디바이스에서 `blk-mq`를 사용하는 경우 이 설정은 DM 계층의 잠금 오버헤드를 줄입니다. 구성 방법에 대한 추가 지침은 사용 중인 Linux 배포의 설명서를 참조하세요.

#### <a name="configure-swapfile"></a>스왑 파일 구성

메모리 부족 문제를 방지하려면 올바르게 구성된 swapfile이 있어야 합니다. swapfile을 만들고 올바른 크기를 지정하는 방법은 해당 Linux 설명서를 참조하세요.

#### <a name="virtual-machines-and-dynamic-memory"></a>Virtual Machines 및 동적 메모리

가상 머신에서 SQL Server on Linux를 실행하는 경우 가상 머신에 대해 예약된 메모리 크기를 수정하는 옵션을 선택해야 합니다. Hyper-V 동적 메모리와 같은 기능을 사용하지 않도록 합니다.

## <a name="sql-server-configuration"></a>SQL Server 구성

애플리케이션 성능을 최대화하려면 SQL Server on Linux를 설치한 후에 다음 구성 작업을 수행하는 것이 좋습니다.

### <a name="best-practices"></a>모범 사례

- **노드 및/또는 CPU에 대해 PROCESS AFFINITY 사용**

   Linux OS의 SQL Server에 사용하는 모든 **NUMANODE** 및/또는 CPU(일반적으로 모든 NODE 및 CPU)에 대해 `ALTER SERVER CONFIGURATION`을 사용하여 `PROCESS AFFINITY`를 설정하는 것이 좋습니다. 프로세서 선호도는 효율적인 Linux 및 SQL 예약 동작을 유지 관리하는 데 도움이 됩니다. **NUMANODE** 옵션을 사용하는 것이 가장 간단한 방법입니다. 컴퓨터에 NUMA 노드가 하나뿐인 경우에도 **PROCESS AFFINITY** 를 사용합니다. **PROCESS AFFINITY** 를 설정하는 방법에 대한 자세한 내용은 [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) 문서를 참조하세요.

- **여러 tempdb 데이터 파일 구성**

   SQL Server on Linux 설치는 여러 tempdb 파일을 구성하는 옵션을 제공하지 않으므로 설치 후에 여러 tempdb 데이터 파일을 만드는 것이 좋습니다. 자세한 내용은 [SQL Server tempdb 데이터베이스에서 할당 경합을 줄이기 위한 권장 사항](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d) 문서의 지침을 참조하세요.

### <a name="advanced-configuration"></a>고급 구성

다음 권장 사항은 SQL Server on Linux 설치 후에 수행할 수 있는 선택적 구성 설정입니다. 이러한 선택 사항은 Linux OS의 워크로드 및 구성 요구 사항에 따라 다릅니다.

- **mssql-conf를 사용하여 메모리 한도 설정**

   Linux OS에서 충분한 실제 메모리를 사용할 수 있도록 하기 위해 SQL Server 프로세스는 기본적으로 실제 RAM의 80%만 사용합니다. 실제 RAM이 큰 일부 시스템에서는 20%도 상당한 크기일 수 있습니다. 예를 들어 RAM이 1TB인 시스템에서 기본 설정을 사용할 경우 약 200GB RAM이 사용되지 않는 상태로 유지됩니다. 이런 상황에서는 메모리 한도를 더 큰 값으로 구성하는 것이 좋습니다. SQL Server에 표시되는 메모리(MB 단위)를 제어하는 **memory.memorylimitmb** 설정과 [mssql-conf](sql-server-linux-configure-mssql-conf.md#memorylimit) 도구는 설명서를 참조하세요.

   이 설정을 변경하는 경우 값을 너무 높게 설정하지 않도록 주의합니다. 충분한 메모리를 유지하지 않으면 Linux OS와 기타 Linux 애플리케이션에서 문제가 발생할 수 있습니다.

## <a name="next-steps"></a>다음 단계

성능을 향상하는 SQL Server 기능에 대한 자세한 내용은 [성능 기능 시작](sql-server-linux-performance-get-started.md)을 참조하세요.

SQL Server on Linux에 대한 자세한 내용은 [SQL Server on Linux 개요](sql-server-linux-overview.md)를 참조하세요.
