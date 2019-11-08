---
title: 새 릴리스로 업그레이드
titleSuffix: SQL Server big data clusters
description: '[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)](미리 보기)를 새 릴리스로 업그레이드하는 방법을 알아봅니다.'
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 90bfaaa1a8cb6fd42081d8afa5feff13f9aec37c
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531956"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 업그레이드하는 방법

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 빅 데이터 클러스터를 새 릴리스로 업그레이드하는 방법을 설명합니다. 이 문서의 단계는 미리 보기 릴리스에서 SQL Server 2019 서비스 업데이트 릴리스로 업그레이드하는 방법을 설명합니다.

## <a name="backup-and-delete-the-old-cluster"></a>이전 클러스터 백업 및 삭제

현재 빅 데이터 클러스터의 현재 위치 업그레이드 방법은 없으며, 빅 데이터 클러스터를 새 릴리스로 업그레이드하는 방법은 클러스터를 수동으로 제거하고 다시 만드는 것뿐입니다. 각 릴리스에는 이전 버전과 호환되지 않는 고유한 `azdata` 버전이 있습니다. 또한 이전 클러스터가 새 노드에 컨테이너 이미지를 다운로드해야 했다면 최신 이미지가 클러스터의 이전 이미지와 호환되지 않을 수도 있습니다. 새 이미지는 컨테이너 설정의 배포 구성 파일에서 `latest` 이미지 태그를 사용하는 경우에만 끌어올 수 있습니다. 기본적으로 각 릴리스에는 SQL Server 릴리스 버전에 해당하는 특정 이미지 태그가 있습니다. 최신 릴리스로 업그레이드하려면 다음 단계를 사용합니다.

1. 이전 클러스터를 삭제하기 전에 SQL Server 마스터 인스턴스와 HDFS의 데이터를 백업합니다. SQL Server 마스터 인스턴스의 경우 [SQL Server 백업 및 복원](data-ingestion-restore-database.md)을 사용할 수 있습니다. HDFS의 경우 [`curl`을 사용하여 데이터를 복사](data-ingestion-curl.md)할 수 있습니다.

1. `azdata delete cluster` 명령을 사용하여 이전 클러스터를 삭제합니다.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 해당 클러스터와 일치하는 `azdata`버전을 사용합니다. 최신 버전의 `azdata`를 사용하여 이전 클러스터를 삭제하면 안 됩니다.

   > [!Note]
   > `azdata bdc delete` 명령을 실행하면 해당 빅 데이터 클러스터를 사용하여 식별된 네임스페이스 안에 생성된 모든 개체가 삭제되지만 네임스페이스 자체는 삭제되지 않습니다. 네임스페이스는 비어 있고 그 안에 생성된 다른 애플리케이션이 없는 한 후속 배포에서 재사용할 수 있습니다.

1. `azdata`의 기존 버전을 제거합니다.

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. `azdata`의 최신 버전을 설치합니다. 다음 명령은 최신 릴리스의 `azdata`를 설치합니다.

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 각 릴리스에 관해, `azdata`의 `n-1` 버전 경로가 변경됩니다. 이전에 `azdata`를 설치했더라도 새 클러스터를 만들기 전에 최신 경로에서 다시 설치해야 합니다.

## <a id="azdataversion"></a> azdata 버전 확인

새로운 빅 데이터 클러스터를 배포하기 전에 `--version` 매개 변수를 통해 최신 버전의 `azdata`를 사용하고 있는지 확인합니다.

```bash
azdata --version
```

## <a name="install-the-new-release"></a>새 릴리스 설치

이전 빅 데이터 클러스터를 제거하고 최신 `azdata`를 설치한 후에는 현재 배포 지침을 사용하여 새로운 빅 데이터 클러스터를 배포합니다. 자세한 내용은 [Kubernetes에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)을 참조하세요. 그런 다음, 필요한 데이터베이스 또는 파일을 모두 복원합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]란?](big-data-cluster-overview.md)을 참조하세요.
