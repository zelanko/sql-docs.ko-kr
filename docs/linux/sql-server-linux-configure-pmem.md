---
title: Linux의 SQL Server에 대 한 영구 메모리 (PMEM)를 구성 하는 방법 | Microsoft Docs
description: 이 문서에서는 PMEM linux 구성에 대 한 연습을 제공 합니다.
author: DBArgenis
ms.author: argenisf
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 07f068a24c60fe82c299387fe859f07296f21df8
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269437"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>Linux의 SQL Server에 대 한 영구 메모리 (PMEM)를 구성 하는 방법

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux의 SQL Server에 대 한 영구 메모리 (PMEM)를 구성 하는 방법을 설명 합니다. Linux에서 PMEM 지원 SQL Server 2019 미리 보기에서 도입 되었습니다.

## <a name="overview"></a>개요

SQL Server 2016에서는 비휘발성 Dimm에 대 한 지원 및 최적화 라는 [NVDIMM의 비상 로그 캐싱의]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/)합니다. 이러한 최적화는 영구 저장소에 로그 버퍼를 강화 하는 데 필요한 작업 수가 줄어듭니다. 이 Windows Server 영구 메모리 모드에서 장치에 DAX에 직접 액세스를 활용합니다.

SQL Server 2019 미리 보기를 확장 영구 메모리에 대 한 지원 (PMEM) Linux 장치 PMEM에 배치 하는 데이터 및 트랜잭션 로그 파일의 전체 계몽을 제공 합니다. 계몽 메서드를 참조 하는 효율적인 사용자 공간을 사용 하 여 저장소 장치에 대 한 액세스 `memcpy()` 작업 합니다. 파일 시스템 및 저장소 스택을 통해 이동, 대신 SQL Server에 직접 장치에 데이터를 배치 하는 대기 시간을 줄이고 Linux에서 DAX 지원을 활용 하 합니다.

## <a name="enable-enlightenment-of-database-files"></a>계몽 데이터베이스 파일을 사용 하도록 설정
계몽 Linux에서 SQL Server의 데이터베이스 파일을 사용 하도록 설정 하려면 다음 단계를 수행 합니다.

1. 장치를 구성 합니다.

  Linux에서 사용 된 `ndctl` 유틸리티입니다.

  - 설치 `ndctl` PMEM 장치를 구성 합니다. 찾을 수 있습니다 [여기](https://docs.pmem.io/getting-started-guide/installing-ndctl)합니다.
  - 네임 스페이스를 만들려면 [ndctl]를 사용 합니다.

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* -–map=mem
  ```

  >[!NOTE]
  >사용 중인 경우 `ndctl` 59를 사용 하 여 보다 낮은 버전 `--mode=memory`합니다.

  사용 하 여 `ndctl` 네임 스페이스를 확인 합니다. 샘플 출력 다음과 같습니다.

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

  - 만들고 PMEM 장치를 탑재 합니다.

    예를 들어 XFS로

    ```bash
    mkfs.xfs -f /dev/pmem0
    mount –o dax,noatime /dev/pmem0 /mnt/dax
    xfs_io -c "extsize 2m" /mnt/dax
    ```

    예를 들어 EXT4

    ```bash
    mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
    mount –o dax,noatime /dev/pmem0 /mnt/dax
    ```

  장치 ndctl를 사용 하 여 구성, 포맷 되어 탑재를 후에 데이터베이스 파일을 배치할 수 있습니다. 새 데이터베이스를 만들 수도 있습니다. 

1. SQL Server 데이터베이스 파일 계몽 3979 추적 플래그를 사용 하 여 사용 합니다. 이 추적 플래그 추적 플래그가 시작 이며 따라서 mssql conf 유틸리티를 사용 하는 데 사용할 수 있어야 합니다.

1. SQL Server를 다시 시작하십시오.

## <a name="next-steps"></a>다음 단계

Linux의 SQL Server에 대 한 자세한 내용은 참조 하세요. [Linux의 SQL Server](sql-server-linux-overview.md)합니다.
