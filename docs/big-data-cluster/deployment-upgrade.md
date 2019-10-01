---
title: 새 릴리스로 업그레이드
titleSuffix: SQL Server big data clusters
description: '@No__t-0 (미리 보기)을 새 릴리스로 업그레이드 하는 방법에 대해 알아봅니다.'
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bb1bf33c9ccb342e6afc4d22d67463791c0d67b6
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688271"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>@No__t 업그레이드 하는 방법-0

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 빅 데이터 클러스터를 새 릴리스로 업그레이드하는 방법을 설명합니다. 이 문서의 단계는 특히 미리 보기 릴리스 간에 업그레이드하는 방법에 적용됩니다.

## <a name="backup-and-delete-the-old-cluster"></a>이전 클러스터 백업 및 삭제

현재, 빅 데이터 클러스터를 새 릴리스로 업그레이드하는 방법은 클러스터를 수동으로 제거하고 다시 만드는 것뿐입니다. 각 릴리스에는 이전 버전과 호환 되지 않는 `azdata`의 고유한 버전이 있습니다. 또한 이전 클러스터가 새 노드에 이미지를 다운로드해야 했다면 최신 이미지가 클러스터의 이전 이미지와 호환되지 않을 수도 있습니다. 최신 릴리스로 업그레이드하려면 다음 단계를 사용합니다.

1. 이전 클러스터를 삭제하기 전에 SQL Server 마스터 인스턴스와 HDFS의 데이터를 백업합니다. SQL Server 마스터 인스턴스의 경우 [SQL Server 백업 및 복원](data-ingestion-restore-database.md)을 사용할 수 있습니다. HDFS의 경우 [`curl`을 사용 하 여 데이터를 복사할 수](data-ingestion-curl.md)있습니다.

1. `azdata delete cluster` 명령을 사용하여 이전 클러스터를 삭제합니다.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 클러스터와 일치 하는 `azdata` 버전을 사용 합니다. 최신 버전의 `azdata` 인 이전 클러스터를 삭제 하지 마십시오.

   > [!Note]
   > @No__t-0 명령을 실행 하면 네임 스페이스 내에 생성 된 모든 개체가 삭제 될 빅 데이터 클러스터 이름으로 식별 되지만 네임 스페이스 자체는 생성 되지 않습니다. 네임 스페이스는 비어 있고 내에 다른 응용 프로그램이 생성 되지 않은 한 후속 배포에 다시 사용할 수 있습니다.

1. CTP 3.2 이전에 `azdata`이-1 @no__t 호출 되었습니다. @No__t-0 또는 `azdata`의 이전 릴리스가 설치 된 경우 최신 버전의 `azdata`를 설치 하기 전에 먼저를 제거 하는 것이 중요 합니다.

   CTP 2.3 이상에서는 다음 명령을 실행합니다. 명령에서 `ctp3.1`을 제거할 `mssqlctl`의 버전으로 바꿉니다. CTP 3.1 이전 버전의 경우 버전 번호 앞에 대시를 추가합니다(예: `ctp-2.5`).

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. @No__t-0의 최신 버전을 설치 합니다. 다음 명령은 릴리스 후보의 `azdata`을 설치 합니다.

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 각 릴리스에 대해 `azdata`에 대 한 경로가 변경 됩니다. 이전에 `azdata` 또는 `mssqlctl`을 설치한 경우에도 새 클러스터를 만들기 전에 최신 경로에서 다시 설치 해야 합니다.

## <a id="azdataversion"></a> azdata 버전 확인

새 빅 데이터 클러스터를 배포 하기 전에 `--version` 매개 변수와 함께 `azdata`의 최신 버전을 사용 하 고 있는지 확인 합니다.

```bash
azdata --version
```

## <a name="install-the-new-release"></a>새 릴리스 설치

이전 빅 데이터 클러스터를 제거 하 고 최신 `azdata`을 설치한 후에는 현재 배포 지침을 사용 하 여 새 빅 데이터 클러스터를 배포 합니다. 자세한 내용은 [Kubernetes에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]을 배포 하는 방법](deployment-guidance.md)을 참조 하세요. 그런 다음, 필요한 데이터베이스 또는 파일을 모두 복원합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)을 참조 하세요.
