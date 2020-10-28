---
title: zypper를 사용하여 Azure Data CLI(azdata) 설치
titleSuffix: ''
description: zypper를 사용하여 Azure Data CLI(azdata) 도구를 설치하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d43a1f9c65aa17fae3d262a51f45105b5f583cdd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257516"
---
# <a name="install-azure-data-cli-azdata-with-zypper"></a>zypper를 사용하여 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] 설치

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

`zypper`을 사용한 Linux 배포판의 경우, `azdata-cli`에 대한 패키지가 있습니다. CLI 패키지는 `zypper`을 사용하는 다음의 Linux 버전에서 테스트되었습니다.

- openSUSE 42.2(leap) 이상
- SLES 12 SP 2 이상

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-zypper"></a>zypper를 사용하여 설치

>[!IMPORTANT]
>`azdata-cli`의 RPM 패키지는 python3 패키지에 따라 달라집니다. 시스템에서 이 패키지는 *Python 3.6.x* 요구 사항 이전의 Python 버전일 수 있습니다. 이로 인해 문제가 발생하는 경우, 대체 python3 패키지를 찾거나 [`pip`](../install/deploy-install-azdata-pip.md)를 사용하는 수동 설치 지침을 따릅니다.

1. `azdata-cli` 설치에 필요한 종속성을 설치합니다.

   ```bash
   sudo zypper install -y curl
   ```

1. Microsoft 리포지토리 키를 가져옵니다.

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. 로컬 리포지토리 정보를 만듭니다.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo
   ```

1. `azdata-cli`설치

   ```bash
   sudo zypper install --from packages-microsoft-com-mssql-server-2019 -y azdata-cli
   ```

## <a name="verify-install"></a>설치 확인

```bash
azdata
azdata --version
```

## <a name="update"></a>업데이트

`zypper update` 명령을 사용하여 `azdata-cli`를 업데이트합니다.

```bash
sudo zypper refresh
sudo zypper update azdata-cli
```

## <a name="uninstall"></a>제거

시스템에서 패키지를 제거합니다.

```bash
sudo zypper removerepo azdata-cli
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]란?](../../big-data-cluster/big-data-cluster-overview.md)을 참조하세요.

[Azure Arc 지원 데이터 서비스](/azure/azure-arc/data/)와 함께 azdata 사용