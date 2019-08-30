---
title: Linux에서 설치 관리자를 사용 하 여 azdata 설치
titleSuffix: SQL Server big data clusters
description: 설치 관리자 (Linux)로 설치 및 관리 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (미리 보기) 하기 위해 azdata 도구를 설치 하는 방법에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e11e4851294ac8ffd8efa66e2156dcd47bce3aa0
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160677"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>Linux `azdata` 에서 관리 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 하려면 설치

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 Linux에서 SQL Server `azdata` 2019 빅 데이터 클러스터 릴리스 후보에 대해을 설치 하는 방법을 설명 합니다. 이러한 패키지 관리자를 사용 하려면 `azdata` 필수 설치를 수행 해야 `pip`합니다.

패키지 관리자는 다양 한 운영 체제 및 배포를 위해 설계 되었습니다.

- Linux (Ubuntu)의 경우 [를 `azdata` 사용 `apt` 하 여 설치](#azdata-apt)

지금은 다른 운영 체제 또는 배포에 설치할 `azdata` 패키지 관리자가 없습니다. 이러한 플랫폼의 경우 [패키지 관리자 `azdata` 를 사용 하지 않고 설치](./deploy-install-azdata.md)를 참조 하세요.

## <a id="linux"></a>Linux `azdata` 용 설치

`azdata`설치 패키지는 Ubuntu에서 `apt`사용할 수 있습니다.

### <a id="azdata-apt"></a>Apt `azdata` 를 사용 하 여 설치 (Ubuntu)

>[!NOTE]
>패키지 `azdata` 는 시스템 python을 사용 하지 않고 자체 python 인터프리터를 설치 합니다.

1. 설치 프로세스에 필요한 패키지를 가져옵니다.

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. 서명 키를 다운로드 하 여 설치 합니다.

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add –
    ```

3. 리포지토리 정보 `azdata` 를 추가 합니다.

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
    ```

4. 리포지토리 정보 업데이트 및 설치 `azdata`:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. 설치 확인:

    ```bash
    azdata --version
    ```

### <a name="update"></a>업데이트

업그레이드 `azdata` 만 해당:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Uninstall

1. Apt를 사용 하 여 제거-제거:

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. 리포지토리 정보 `azdata` 를 제거 합니다.

    >[!NOTE]
    >향후 설치 `azdata` 를 계획 하는 경우에는이 단계가 필요 하지 않습니다.

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. 서명 키를 제거 합니다.

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. Azdata CLI를 사용 하 여 설치 된 불필요 한 종속성을 제거 합니다.

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)을 참조 하세요.
