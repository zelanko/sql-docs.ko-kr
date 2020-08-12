---
title: SQL Server 빅 데이터 클러스터의 성능 모범 사례
description: 이 문서에서는 Kubernetes에서 SQL Server 빅 데이터 클러스터를 실행하기 위한 성능 모범 사례 및 지침을 제공합니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: abb5a73f472ccefa53517c54a3d403af82d0beb2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85906241"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터의 성능 모범 사례 및 구성 지침

[!INCLUDE [sqlserver2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 빅 데이터 클러스터 내에서 실행되는 서비스를 대상으로 하는 애플리케이션의 성능을 최대화하기 위한 모범 사례 및 권장 사항을 제공합니다.

다음 지침에서는 BDC를 배포할 Kubernetes 작업자 노드를 호스팅하는 Linux 운영 체제를 구성하기 위한 권장 사항을 중점적으로 설명합니다. 빅 데이터 클러스터를 배포하기 전에 튜닝 프로필을 구성하는 것이 가장 좋습니다. 제안된 튜닝 프로필에 포함된 설정은 Microsoft와 Intel에서 수행하는 사례 연구 중에 유효성이 검사되었습니다. 연구의 결과는 다운로드할 수 있도록 이 [백서](https://aka.ms/sql-bdc-spark-perf/)에 게시되어 있습니다.

> [!TIP]
> SQL Server on Linux 관련 특정 구성은 [SQL Server on Linux의 성능 모범 사례 및 구성 지침](../linux/sql-server-linux-performance-best-practices.md)을 참조하세요. 또한 SQL Server 데이터베이스용 인덱스 디자인과 같은 다른 모범 사례도 여전히 적용됩니다.

## <a name="proposed-linux-settings-using-a-tuned-mssql-bdc-profile"></a>튜닝된 `mssql-bdc` 프로필을 사용하는 권장 Linux 설정

아래 내용을 사용하여 **tuned.conf** 구성 프로필을 만듭니다.

```bash
[main]
summary=Optimize for Microsoft SQL Server Big Data Clusters TPC-DS performance
include=throughput-performance
 
[sysctl]
#network tunings
net.ipv4.conf.default.rp_filter=1
net.ipv4.tcp_timestamps=0
net.ipv4.tcp_sack = 1
net.core.netdev_max_backlog = 25000
net.core.rmem_max = 2147483647
net.core.wmem_max = 2147483647
net.core.rmem_default = 33554431
net.core.wmem_default = 33554432
net.core.optmem_max = 33554432
net.ipv4.tcp_rmem =8192 33554432 2147483647
net.ipv4.tcp_wmem =8192 33554432 2147483647
net.ipv4.tcp_low_latency=1
net.ipv4.tcp_adv_win_scale=1
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv4.conf.all.arp_filter=1
net.ipv4.tcp_retries2=5
net.ipv6.conf.lo.disable_ipv6 = 1
net.core.somaxconn = 65535
 
#memory cache settings
vm.swappiness=1
vm.overcommit_memory=0
vm.dirty_background_ratio=1
 
#kernel NUMA
kernel.numa_balancing=0

#filesystem
fs.aio-max-nr=1048576
 
[vm]
#should be revisited for SQL large pages use in master/data/compute pods
transparent_hugepages=never
```

## <a name="install-tuned-utility-on-all-the-kubernetes-worker-nodes"></a>모든 Kubernetes 작업자 노드에 **tuned** 유틸리티 설치

**tuned**를 설치하려면 다음을 실행합니다.

```bash
apt-get -y install tuned
```

## <a name="apply-tuning-settings-to-all-kubernetes-worker-nodes"></a>모든 Kubernetes 작업자 노드에 튜닝 설정 적용

각 대상 작업자 노드에 위에서 만든 **tuned.conf** 파일을 복사합니다.

```bash
cd /usr/lib/tuned
scp -r <sourcePath> ./mssql-bdc
```

튜닝된 프로필인 이 **mssql-bdc**를 사용하도록 설정하려면 모든 Kubernetes 작업자 노드에서 `/usr/lib/tuned/mssql-bdc` 폴더 아래에 있는 **tuned.conf** 파일에 이러한 정의를 저장하고 다음을 사용하여 프로필을 사용하도록 설정합니다.

```bash
chmod +x /usr/lib/tuned/mssql-bdc/tuned.conf
tuned-adm profile mssql-bdc
```

프로필이 사용하도록 설정되었는지 다음 명령을 사용하여 확인합니다.

```bash
tuned-adm active
```

또는

```bash
tuned-adm list
```

프로필이 동적으로 변경되는 경우 새 변경 내용이 적용되려면 영향을 받는 모든 작업자 노드에서 **tuned**를 다시 시작해야 합니다.

```bash
systemctl restart tuned
```
 
**tuned** 서비스의 로그는 */var/log/tuned/tuned.log*에서 찾을 수 있습니다.

필요에 따라 Kubernetes 클러스터의 한 노드에서 튜닝 프로필을 구성하고 아래 스크립트를 사용하여 튜닝 프로필을 나머지 노드에 복사한 후 구성할 수 있습니다.

```bash
#!/bin/bash -e
# This script takes a list of servers (IPs like `cat ~administrator/workerhosts)) as input
# and update these servers with the local version of mssql-bdc tuned.conf.
 
is_root() {
    local is_root_set=0
    if [ "$EUID" -ne 0 ]; then
        echo "Please run as root"
    else
        is_root_set=1
    fi
    return "${is_root_set}"
}
 
# function main
if is_root -eq 0; then
    exit 0
fi
 
while [ $# -gt 0 ]
do
    # sometimes, people add non-breaking space characters to their *host* files.
    WORKER_IP=$(echo "$1" | sed -e 's/\xC2\xA0//g')
    echo -e "updating mssql-bdc tuned on \e[42m${WORKER_IP}\e[0m"
    # the following commands assume tuned was not set up and active...
    # TODO: add the tuned install and status checks
    ssh "${WORKER_IP}" mkdir -p /usr/lib/tuned/mssql-bdc
    scp ~administrator/tuned.conf "${WORKER_IP}":/usr/lib/tuned/mssql-bdc/tuned.conf
    ssh "${WORKER_IP}" tuned-adm profile mssql-bdc
    ssh "${WORKER_IP}" systemctl restart tuned
    ssh "${WORKER_IP}" tuned-adm active
    shift
done

```

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대한 참조 아키텍처를 포함하여 자세한 리소스는 다음을 참조하세요.

* [사례 연구: SQL Workloads running on Apache Spark in MS SQL Server 2019 Big Data Cluster](https://aka.ms/sql-bdc-spark-perf/)

* [HPE Reference Architecture for delivering insight across all your data with Microsoft SQL Server 2019 Big Data Clusters](https://h20195.www2.hpe.com/V2/GetDocument.aspx?docname=a50001963enw)

* [Dell EMC PowerStore: Microsoft SQL Server 2019 Big Data Clusters](https://www.dellemc.com/resources/en-us/asset/white-papers/products/storage/h18231-dell-emc-powerstore-sql-server-big-data-clusters.pdf)

* [Microsoft SQL Server 2019 Big Data Clusters: A Big Data Solution Using Dell EMC Infrastructure](https://infohub.delltechnologies.com/t/microsoft-sql-server-2019-big-data-clusters-a-big-data-solution-using-dell-emc-infrastructure/)

* [Microsoft SQL Server 2019 Big Data Clusters on Cisco UCS Reference Architecture](https://www.cisco.com/c/en/us/solutions/collateral/data-center-virtualization/unified-computing/sql-server-on-big-data-cluster-on-ucs.html)