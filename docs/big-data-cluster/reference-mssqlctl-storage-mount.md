---
title: mssqlctl 저장소 탑재 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 저장소 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3ad8a97bac1f708dcf01612368c76d584fa39f5c
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860294"
---
# <a name="mssqlctl-storage-mount"></a>mssqlctl 스토리지 탑재

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **저장소 탑재** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a id="commands"></a> 명령

|||
|---|---|
| [create](#create) | HDFS에서 원격 저장소의 탑재를 만듭니다. |
| [delete](#delete) | HDFS의 원격 저장소의 탑재를 삭제 합니다. |
| [상태](#status) | Mount(s)의 상태입니다. |

## <a id="create"></a> mssqlctl 저장소 탑재 만들기

HDFS에서 원격 저장소의 탑재를 만듭니다.

```
mssqlctl storage mount create
   --local-path
   --remote-uri
   [--credential-file]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--local-path** | 탑재 되도록에 있는 HDFS 경로 (탑재 대상)를 만듭니다. 필수 사항입니다. |
| **--remote-uri** | 탑재 된 (탑재의 원본)에 있는 원격 저장소의 URI입니다. 필수 사항입니다. |
| **--credential-file** | 원격 저장소에 액세스 하는 자격 증명을 포함 하는 파일입니다. 자격 증명 키로 지정할 필요가 = 값 쌍 하나의 키를 사용 하 여 = 줄 값입니다. 키 또는 값에서 모든 equals를 이스케이프 해야 합니다. 기본적으로 자격 증명이 필요 합니다. 필요한 키를 탑재 하는 원격 저장소의 유형 및 사용 권한 부여의 형식에 따라 달라 집니다. |

### <a name="examples"></a>예

HDFS 경로에서 ADLS Gen 2 계정의 "adlsv2example" 컨테이너 "데이터"를 탑재 하려면 `/mounts/adlsv2/data` 공유 키를 사용 하 여:

```
mssqlctl storage mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/ --local-path /mounts/adlsv2/data --credentials credential_file
```

탑재할 원격 HDFS 클러스터 (`hdfs://namenode1:8080/`)에서 로컬 HDFS 경로 `/mounts/hdfs/`:

```
mssqlctl storage mount create --remote-uri hdfs://namenode1:8080/ --local-path /mounts/hdfs/
```

## <a id="delete"></a> mssqlctl 저장소 탑재 삭제

HDFS의 원격 저장소의 탑재를 삭제 합니다.

```
mssqlctl storage mount delete
   --local-path
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--local-path** | 삭제 된 해당 탑재 하는 HDFS 경로입니다. 필수 사항입니다. |

### <a name="examples"></a>예

Gen 2 ADLS 저장소 계정에 대 한 /mounts/adlsv2/data에서 생성 하는 탑재를 삭제 합니다.

```
mssqlctl storage mount delete --local-path /mounts/adlsv2/data
```

## <a id="status"></a> mssqlctl 저장소 탑재 상태

Mount(s)의 상태입니다.

```
mssqlctl storage mount status
   --local-path
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--mount-path** | 탑재 경로입니다. 필수 사항입니다. |

### <a name="examples"></a>예

경로로 탑재 상태 가져오기

```
mssqlctl storage mount status --mount-path /mounts/hdfs
```

모든 탑재의 상태를 가져옵니다.

```
mssqlctl storage mount status
```

## <a name="next-steps"></a>다음 단계

다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다. 설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.