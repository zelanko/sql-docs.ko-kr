---
title: 새 릴리스로 업그레이드
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 빅 데이터 클러스터를 새 릴리스로 업그레이드하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2f8ca3e42221387470ee4fc4cbd6873b526bc8b7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77256877"
---
# <a name="how-to-upgrade-big-data-clusters-2019"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 업그레이드하는 방법

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

업그레이드 경로는 SQL Server 빅 데이터 클러스터(BDC)의 현재 버전에 따라 달라집니다. GDR(일반 배포 릴리스), CU(누적 업데이트) 또는 QFE(빠른 수정) 업데이트 등의 지원되는 릴리스에서 업그레이드하려면 현재 위치에서 업그레이드할 수 있습니다. CTP(고객 기술 미리 보기) 또는 릴리스 후보 버전의 BDC에서는 현재 위치 업그레이드가 지원되지 않습니다. 클러스터를 제거하고 다시 만들어야 합니다. 다음 섹션은 각 시나리오의 단계를 설명합니다.

- [지원되는 릴리스에서 업그레이드](#upgrade-from-supported-release)
- [CTP 또는 릴리스 후보에서 BDC 배포 업데이트](#update-a-bdc-deployment-from-ctp-or-release-candidate)

>[!NOTE]
>빅 데이터 클러스터의 지원되는 첫 번째 릴리스는 SQL Server 2019 GDR1입니다.

## <a name="upgrade-release-notes"></a>업그레이드 릴리스 정보

계속하기 전에 [알려진 문제에 대한 업그레이드 릴리스 정보](release-notes-big-data-cluster.md#known-issues)를 확인하세요.

## <a name="upgrade-from-supported-release"></a>지원되는 릴리스에서 업그레이드

이 섹션에서는 지원되는 릴리스(SQL Server 2019 GDR1)에서 지원되는 최신 릴리스로 SQL Server BDC를 업그레이드하는 방법에 대해 설명합니다.

1. SQL Server 마스터 인스턴스를 백업합니다.
2. HDFS를 백업합니다.

   ```
   azdata bdc hdfs cp --from-path <path> --to-path <path>
   ```
   
   다음은 그 예입니다. 

   ```
   azdata bdc hdfs cp --from-path hdfs://user/hive/warehouse/%%D --to-path ./%%D
   ```

3. `azdata`를 업데이트합니다.

   `azdata` 설치를 위한 지침을 따릅니다. 
   - [Windows Installer](deploy-install-azdata-installer.md)
   - [apt를 사용하는 Linux](deploy-install-azdata-linux-package.md)
   - [yum을 사용하는 Linux](deploy-install-azdata-yum.md)
   - [zypper를 사용하는 Linux](deploy-install-azdata-zypper.md)

   >[!NOTE]
   >`azdata`가 `pip`와 함께 설치된 경우 Windows 설치 프로그램 또는 Linux 패키지 관리자를 사용하여 설치하기 전에 수동으로 제거해야 합니다.

1. 빅 데이터 클러스터를 업데이트합니다.

   ```
   azdata bdc upgrade -n <clusterName> -t <imageTag> -r <containerRegistry>/<containerRepository>
   ```

   예를 들어 다음 스크립트는 `2019-CU1-ubuntu-16.04` 이미지 태그를 사용합니다.

   ```
   azdata bdc upgrade -n bdc -t 2019-CU1-ubuntu-16.04 -r mcr.microsoft.com/mssql/bdc
   ```

>[!NOTE]
>최신 이미지 태그는 [SQL Server 2019 빅 데이터 클러스터 릴리스 정보](release-notes-big-data-cluster.md)에서 확인할 수 있습니다.

>[!IMPORTANT]
>프라이빗 리포지토리를 사용하여 BDC를 배포하거나 업그레이드하기 위해 이미지를 미리 가져오는 경우 현재 빌드 이미지와 대상 빌드 이미지가 프라이빗 리포지토리에 있는지 확인합니다. 이렇게 하면 필요한 경우 성공적으로 롤백할 수 있습니다. 또한 원래 배포 이후 프라이빗 리포지토리의 자격 증명을 변경한 경우 해당 환경 변수 DOCKER_PASSWORD 및 DOCKER_USERNAME을 업데이트합니다. 현재 및 대상 빌드에 다른 프라이빗 리포지토리를 사용하여 업그레이드할 수 없습니다.

### <a name="increase-the-timeout-for-the-upgrade"></a>업그레이드 시간 제한 늘리기

특정 구성 요소가 할당된 시간 내에 업그레이드 되지 않으면 시간 초과가 발생할 수 있습니다. 다음 코드는 오류가 어떻게 표시되는지 보여 줍니다.

   ```
   >azdata.EXE bdc upgrade --name <mssql-cluster>
   Upgrading cluster to version 15.0.4003

   NOTE: Cluster upgrade can take a significant amount of time depending on
   configuration, network speed, and the number of nodes in the cluster.

   Upgrading Control Plane.
   Control plane upgrade failed. Failed to upgrade controller.
   ```

업그레이드에 대한 시간 제한을 늘리려면 **--controller-timeout** 및 **--component-timeout** 매개 변수를 사용하여 업그레이드를 실행할 때 더 높은 값을 지정합니다. 이 옵션은 SQL Server 2019 CU2 릴리스부터 사용할 수 있습니다. 다음은 그 예입니다.

   ```bash
   azdata bdc upgrade -t 2019-CU2-ubuntu-16.04 --controller-timeout=40 --component-timeout=40 --stability-threshold=3
   ```
**--controller-timeout**은 컨트롤러 또는 컨트롤러 db의 업그레이드가 완료될 때까지 대기할 시간(분)을 지정합니다.
**--component-timeout**은 업그레이드의 각 후속 단계를 완료해야 하는 기간을 지정합니다.

SQL Server 2019 CU2 릴리스 전에 업그레이드에 대한 시간 제한을 늘리려면 업그레이드 구성 맵을 편집합니다. 업그레이드 구성 맵을 편집하려면 다음을 수행합니다.

다음 명령 실행:

   ```bash
   kubectl edit configmap controller-upgrade-configmap
   ```

다음 필드를 편집합니다.

   **controllerUpgradeTimeoutInMinutes** 컨트롤러 또는 컨트롤러 db의 업그레이드가 완료될 때까지 대기할 시간(분)을 지정합니다. 기본값은 5입니다. 20 이상으로 업데이트합니다.
   **totalUpgradeTimeoutInMinutes**: 컨트롤러와 컨트롤러 db 모두가 업그레이드를 완료하는 데 걸리는 시간을 합한 값을 지정합니다(컨트롤러 + 컨트롤러 db 업그레이드). 기본값은 10입니다. 40 이상으로 업데이트합니다.
   **componentUpgradeTimeoutInMinutes**: 업그레이드의 각 후속 단계를 완료해야 하는 기간을 지정합니다. 기본값은 30입니다. 45로 업데이트합니다.

저장한 후 종료합니다.

## <a name="update-a-bdc-deployment-from-ctp-or-release-candidate"></a>CTP 또는 릴리스 후보에서 BDC 배포 업데이트

CTP 또는 SQL Server 빅 데이터 클러스터의 릴리스 후보 빌드에서는 현재 위치 업그레이드가 지원되지 않습니다. 다음 섹션에서는 클러스터를 수동으로 제거하고 다시 만드는 방법을 설명합니다.

### <a name="backup-and-delete-the-old-cluster"></a>이전 클러스터 백업 및 삭제

SQL Server 2019 GDR1 릴리스 이전에 배포된 빅 데이터 클러스터에 대한 현재 위치 업그레이드는 없습니다. 새 릴리스로 업그레이드하는 방법은 클러스터를 수동으로 제거하고 다시 만드는 것뿐입니다. 각 릴리스에는 이전 버전과 호환되지 않는 고유한 `azdata` 버전이 있습니다. 또한 다른 이전 버전으로 배포된 클러스터에서 최신 컨테이너 이미지를 다운로드하면 최신 이미지가 클러스터의 이전 이미지와 호환되지 않을 수 있습니다. 새 이미지는 컨테이너 설정의 배포 구성 파일에서 `latest` 이미지 태그를 사용하는 경우에 끌어올 수 있습니다. 기본적으로 각 릴리스에는 SQL Server 릴리스 버전에 해당하는 특정 이미지 태그가 있습니다. 최신 릴리스로 업그레이드하려면 다음 단계를 사용합니다.

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

### <a name="verify-the-azdata-version"></a><a id="azdataversion"></a> azdata 버전 확인

새로운 빅 데이터 클러스터를 배포하기 전에 `--version` 매개 변수를 통해 최신 버전의 `azdata`를 사용하고 있는지 확인합니다.

```bash
azdata --version
```

### <a name="install-the-new-release"></a>새 릴리스 설치

이전 빅 데이터 클러스터를 제거하고 최신 `azdata`를 설치한 후에는 현재 배포 지침을 사용하여 새로운 빅 데이터 클러스터를 배포합니다. 자세한 내용은 [Kubernetes에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)을 참조하세요. 그런 다음, 필요한 데이터베이스 또는 파일을 모두 복원합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]란?](big-data-cluster-overview.md)을 참조하세요.
