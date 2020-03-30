---
title: PMEM(영구 메모리) 구성
description: 이 문서에서는 Linux에서 PMEM을 구성하기 위한 연습을 제공합니다.
ms.custom: seo-lt-2019
author: briancarrig
ms.author: brcarrig
ms.date: 10/31/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 5d98b728a1966861532a30a4b5dd92824d25f1d5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76831966"
---
# <a name="configure-persistent-memory-pmem-for-sql-server-on-linux"></a>SQL Server on Linux의 PMEM(영구적 메모리) 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 아티클에서는 [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] on Linux에 대해 PMEM(영구 메모리)을 구성하는 방법을 설명합니다.

## <a name="overview"></a>개요

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)]에는 영구 메모리를 사용하는 많은 메모리 내 기능이 있습니다. 이 문서에서는 SQL Server on Linux에 대해 영구 메모리를 구성하는 데 필요한 단계를 설명합니다.

> [!NOTE]
> ‘인식’이라는 용어는 영구 메모리 인식 파일 시스템의 작업 개념을 전달하기 위해 도입되었습니다.  메모리 매핑(`mmap()`)을 사용하면 간편하게 사용자 공간 애플리케이션에서 파일 시스템에 직접 액세스할 수 있습니다. 파일에 대한 메모리 매핑이 생성된 경우, 애플리케이션에서 I/O 스택을 완전히 무시하고 로드/저장 명령을 실행할 수 있습니다. 호스트 확장 애플리케이션 관점에서 “인식” 파일 액세스 방법으로 간주하며, SQLPAL이 Windows 또는 Linux OS와 상호 작용할 수 있도록 하는 블랙박스 코드입니다.

## <a name="create-namespaces-for-pmem-devices"></a>PMEM 디바이스에 대한 네임스페이스 만들기

### <a name="configure-the-devices"></a>디바이스 구성

Linux에서 `ndctl` 유틸리티를 사용합니다.

- `ndctl`을 설치하여 PMEM 디바이스를 구성합니다. [여기](https://docs.pmem.io/getting-started-guide/installing-ndctl)에서 찾을 수 있습니다.
- `ndctl`을 사용하여 네임스페이스를 만듭니다. 네임스페이스는 PMEM NVDIMM 간에 인터리브되며, 디바이스의 메모리 영역에 대한 여러 유형의 사용자 공간 액세스를 제공할 수 있습니다. `fsdax`는 SQL Server에 적합한 기본 모드입니다.

```bash 
ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=dev
```

여기서는 `fsdax` 모드를 선택했으며 시스템 메모리를 사용하여 페이지별 메타데이터를 저장합니다. `--map=dev`를 사용하는 것이 좋습니다. 이렇게 하면 메타데이터가 네임스페이스에 직접 저장됩니다. `--map=mem`을 사용하여 메타데이터를 메모리에 저장하는 기능은 현재 실험적인 것으로 간주됩니다.

`ndctl`을 사용하여 네임스페이스를 확인합니다. 
  
샘플 출력은 다음과 같습니다.

```bash
# ndctl list -N
{
  "dev":"namespace0.0",
  "mode":"fsdax",
  "map":"dev",
  "size":4294967296,
  "sector_size":512,
  "blockdev":"pmem0",
  "numa_node":0
}
```

### <a name="create-and-mount-pmem-device"></a>PMEM 디바이스 만들기 및 탑재

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

## <a name="technical-considerations"></a>기술 고려 사항

- 위에서 설명한 대로 XFS/EXT4에 대한 2MB 블록 할당
- 블록 할당과 `mmap` 간의 불일치로 인해 4KB로 자동 대체
- 파일 크기는 2MB의 배수여야 함(모듈로 2MB)
- THP(투명한 대용량 페이지) 해제 안 함(대부분의 배포에 기본적으로 사용하도록 설정되어 있음)

디바이스가 `ndctl`을 통해 구성되고 생성 및 탑재되고 나면, 디바이스에 데이터베이스 파일을 배치하거나 새 데이터베이스를 만들 수 있습니다.

PMEM 디바이스는 O_DIRECT(직접 I/O)로부터 안전하므로 강제 플러시 메커니즘을 해제하려면 추적 플래그 3979를 사용하도록 설정하는 것이 좋습니다. 자세한 내용은 [FUA 지원](https://support.microsoft.com/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux)을 참조하세요. 강제 단위 액세스 내부 요소는 [FUA 내부 요소](https://blogs.msdn.microsoft.com/bobsql/2018/12/18/sql-server-on-linux-forced-unit-access-fua-internals/)에서 설명합니다.

## <a name="next-steps"></a>다음 단계

SQL Server on Linux에 대한 자세한 내용은 [SQL Server on Linux](sql-server-linux-overview.md)를 참조하세요.
SQL Server on Linux의 성능 모범 사례는 [성능 모범 사례](sql-server-linux-performance-best-practices.md)를 참조하세요.
