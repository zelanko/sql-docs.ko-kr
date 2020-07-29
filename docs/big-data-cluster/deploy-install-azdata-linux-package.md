---
title: Linux에서 설치 관리자를 사용하여 azdata 설치
titleSuffix: SQL Server big data clusters
description: 설치 관리자(Linux)를 사용하여 SQL Server 빅 데이터 클러스터를 설치 및 관리하기 위한 azdata 도구를 설치하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 304515dcd288978c0d85ab992312eb2444430bfc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773641"
---
# <a name="install-azdata-with-apt"></a>apt를 사용하여 `azdata` 설치

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 Linux에서 SQL Server 2019 빅 데이터 클러스터용 `azdata`를 설치하는 방법을 설명합니다. 패키지 관리자가 출시되기 전에는 `azdata`를 설치하려면 `pip`가 필요했습니다.

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-azdata-for-linux"></a><a id="linux"></a>Linux용 `azdata` 설치

`azdata` 설치 패키지는 `apt`를 사용하여 Ubuntu에 사용할 수 있습니다.

### <a name="install-azdata-with-apt-ubuntu"></a><a id="azdata-apt"></a>apt를 사용하여 `azdata` 설치(Ubuntu)

>[!NOTE]
>`azdata` 패키지는 시스템 Python을 사용하지 않고 자체 Python 인터프리터를 설치합니다.

1. 설치 프로세스에 필요한 패키지를 가져옵니다.

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
    ```

2. 서명 키를 다운로드하여 설치합니다.

    ```bash
    curl -sL https://packages.microsoft.com/keys/microsoft.asc |
    gpg --dearmor |
    sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
    ```

3. `azdata` 리포지토리 정보를 추가합니다.

   Ubuntu 16.04 클라이언트 실행의 경우:
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
    ```

   Ubuntu 18.04 클라이언트 실행의 경우:
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
    ```

4. 리포지토리 정보를 업데이트하고 `azdata`를 설치합니다.

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. 설치를 확인합니다.

    ```bash
    azdata --version
    ```

### <a name="update"></a>업데이트

`azdata`만 업그레이드합니다.

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>제거

1. apt-get remove를 사용하여 제거합니다.

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. `azdata` 리포지토리 정보를 제거합니다.

    >[!NOTE]
    >나중에 `azdata`를 설치하려는 경우 이 단계를 수행할 필요가 없습니다.

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. 서명 키를 제거합니다.

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. Azdata CLI와 함께 설치된 불필요한 종속성을 제거합니다.

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
