---
title: SQL Server on Linux의 PMEM(영구적 메모리) 구성
description: 이 문서에서는 Linux에서 PMEM을 구성하기 위한 연습을 제공합니다.
ms.custom: seo-lt-2019
author: briancarrig
ms.author: brcarrig
ms.reviewer: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 0b5f86dac62c371a9e4dda607cbd9ec7533a187a
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558618"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>SQL Server on Linux에 대해 PMEM(영구적 메모리)를 구성하는 방법

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 SQL Server on Linux에 대해 PMEM(영구적 메모리)를 구성하는 방법을 설명합니다. Linux에 대한 PMEM 지원은 SQL Server 2019에서 도입되었습니다.

## <a name="overview"></a>개요

SQL Server 2016에는 비휘발성 DIMM에 대한 지원 및 [Tail of the Log Caching on NVDIMM]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/)(NVDIMM의 비상 로그 캐싱)이라는 최적화가 도입되었습니다. 이 최적화는 로그 버퍼를 영구적 스토리지로 강화하는 데 필요한 작업의 수를 줄입니다. 이 최적화는 DAX 모드의 영구적 메모리 디바이스에 대한 Windows Server 직접 액세스를 이용합니다.

SQL Server 2019는 PMEM(영구적 메모리) 디바이스 지원을 Linux로 확장하여 PMEM에 배치된 데이터 및 트랜잭션 로그 파일의 전체 향상 기능을 제공합니다. 향상 기능은 효율적인 사용자 공간 `memcpy()` 작업을 사용하여 스토리지 디바이스에 액세스하는 방법을 나타냅니다. SQL Server는 파일 시스템 및 스토리지 스택을 통과하지 않고 Linux에서 DAX 지원을 활용하여 데이터를 디바이스에 직접 배치하여 대기 시간을 줄입니다.

## <a name="enable-enlightenment-of-database-files"></a>데이터베이스 파일의 향상 기능 사용
SQL Server on Linux에서 데이터베이스 파일의 향상 기능을 사용하도록 설정하려면 다음 단계를 수행합니다.

1. 디바이스를 구성합니다.

  Linux에서 `ndctl` 유틸리티를 사용합니다.

  - `ndctl`을 설치하여 PMEM 디바이스를 구성합니다. [여기](https://docs.pmem.io/getting-started-guide/installing-ndctl)에서 찾을 수 있습니다.
  - [ndctl]을 사용하여 네임스페이스를 만듭니다.

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=mem
  ```

  >[!NOTE]
  >59 이전의 `ndctl` 버전을 사용하는 경우에는 `--mode=memory`를 사용합니다.

  `ndctl`을 사용하여 네임스페이스를 확인합니다. 샘플 출력은 다음과 같습니다.

```bash
ndctl list
[
  {
    "dev":"namespace0.0",
    "mode":"memory",
    "size":1099511627776,
    "blockdev":"pmem0",
    "numa_node":0
  }
]
```

  - PMEM 디바이스 만들기 및 탑재

    예: XFS 사용

    ```bash
    mkfs.xfs -f /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    xfs_io -c "extsize 2m" /mnt/dax
    ```

    예: EXT4 사용

    ```bash
    mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    ```

  디바이스가 ndctl을 통해 구성되고, 형식이 지정되고, 탑재된 후 디바이스에 데이터베이스 파일을 배치할 수 있습니다. 새 데이터베이스를 만들 수도 있습니다. 

1. PMEM 디바이스는 O_DIRECT에 안전하므로 추적 플래그 3979를 사용하도록 설정하면 강제 플러시 메커니즘이 사용되지 않습니다. 이 추적 플래그는 시작 추적 플래그이므로, mssql-conf 유틸리티를 사용하여 사용하도록 설정해야 합니다. 이는 서버 수준 구성 변경이며 데이터 무결성을 보장하기 위해 강제 플러시 메커니즘이 필요한 O_DIRECT 비규격 디바이스가 있는 경우 이 추적 플래그를 사용하면 안 됩니다. 자세한 내용은 https://support.microsoft.com/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux 을 참조하십시오.

1. SQL Server를 다시 시작하십시오.

## <a name="next-steps"></a>다음 단계

SQL Server on Linux에 대한 자세한 내용은 [SQL Server on Linux](sql-server-linux-overview.md)를 참조하세요.
