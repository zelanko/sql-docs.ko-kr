---
title: apt를 사용하여 Azure Data CLI(azdata) 설치
description: apt를 사용하여 Azure Data CLI(azdata) 도구를 설치하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2f248978e09be4670d702805873a5ae6f4f7c9de
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257466"
---
# <a name="install-azure-data-cli-azdata-with-apt"></a>apt를 사용하여 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] 설치

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

`apt`을 사용한 Linux 배포판의 경우, `azdata-cli`에 대한 패키지가 있습니다. CLI 패키지는 `apt`을 사용하는 다음의 Linux 버전에서 테스트되었습니다.

- Ubuntu 16.04, Ubuntu 18.04

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-apt"></a>apt를 사용하여 설치

>[!IMPORTANT]
> `azdata-cli`의 RPM 패키지는 python3 패키지에 따라 달라집니다. 시스템에서 이 패키지는 *Python 3.6.x* 요구 사항 이전의 Python 버전일 수 있습니다. 이로 인해 문제가 발생하는 경우, 대체 python3 패키지를 찾거나 [`pip`](../install/deploy-install-azdata-pip.md)를 사용하는 수동 설치 지침을 따릅니다.

1. `azdata-cli` 설치에 필요한 종속성을 설치합니다.

   ```bash
   sudo apt-get update
   sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
   ```

2. Microsoft 리포지토리 키를 가져옵니다.

   ```bash
   curl -sL https://packages.microsoft.com/keys/microsoft.asc |
   gpg --dearmor |
   sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
   ```

3. 로컬 리포지토리 정보를 만듭니다.

   Ubuntu 16.04 클라이언트 실행의 경우:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
    ```

   Ubuntu 18.04 클라이언트 실행의 경우:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/prod.list)"
    ```

   Ubuntu 20.04 클라이언트 실행의 경우:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/20.04/prod.list)
    ```

4. `azdata-cli`설치

   ```bash
   sudo apt-get update
   sudo apt-get install -y azdata-cli
   ```

## <a name="verify-install"></a>설치 확인

```bash
azdata
azdata --version
```

## <a name="update"></a>업데이트

`apt-get update` 및 `apt-get install` 명령을 사용하여 `azdata-cli`를 업데이트합니다.

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

## <a name="uninstall"></a>제거

1. 시스템에서 패키지를 제거합니다.

   ```bash
   sudo apt-get remove -y azdata-cli
   ```

2. `azdata-cli`를 다시 설치하지 않으려면 리포지토리 정보를 제거합니다.

   ```bash
   sudo rm /etc/apt/sources.list.d/azdata-cli.list
   ```

3. 리포지토리 키를 제거합니다.

   ```bash
   sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
   ```

4. 종속성 제거는 더 이상 필요하지 않습니다.

   ```bash
   sudo apt autoremove
   ```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]란?](../../big-data-cluster/big-data-cluster-overview.md)을 참조하세요.

[Azure Arc 지원 데이터 서비스](/azure/azure-arc/data/)와 함께 azdata 사용