---
title: yum을 사용하여 azdata 설치
titleSuffix: ''
description: yum을 사용하여 azdata 도구를 설치하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: eae81ccee65899335b161b3a32fbb260d0a8517a
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914895"
---
# <a name="install-azdata-with-yum"></a>yum을 사용하여 `azdata` 설치

`yum`을 사용한 Linux 배포판의 경우, `azdata-cli`에 대한 패키지가 있습니다. CLI 패키지는 `yum`을 사용하는 다음의 Linux 버전에서 테스트되었습니다.

- RHEL 7, RHEL 8


[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-yum"></a>yum을 사용하여 설치

>[!IMPORTANT]
> `azdata-cli`의 RPM 패키지는 python3 패키지에 따라 달라집니다. 시스템에서 이 패키지는 *Python 3.6.x* 요구 사항 이전의 Python 버전일 수 있습니다. 이로 인해 문제가 발생하는 경우, 대체 python3 패키지를 찾거나 [`pip`](../install/deploy-install-azdata-pip.md)를 사용하는 수동 설치 지침을 따릅니다.

1. Microsoft 리포지토리 키 가져오기

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. 로컬 리포지토리 정보 만들기

   RHEL 7 클라이언트의 경우 다음을 실행합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```
  
   RHEL 8 클라이언트의 경우 다음을 실행합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/prod.repo
   ```

1. `yum install` 명령을 사용하여 설치

   ```bash
   sudo yum install azdata-cli
   ```

## <a name="verify-install"></a>설치 확인

```
azdata
azdata --version
```

## <a name="update"></a>업데이트

`yum update` 명령을 사용하여 `azdata-cli`를 업데이트합니다.

```bash
sudo yum update azdata-cli
```

## <a name="uninstall"></a>제거

1. 시스템에서 패키지를 제거합니다.

   ```bash
   sudo yum remove azdata-cli
   ```

1. `azdata-cli`를 다시 설치하지 않으려면 리포지토리 정보를 제거합니다.

   ```bash
   sudo rm /etc/yum.repos.d/azdata-cli.repo
   ```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]란?](../../big-data-cluster/big-data-cluster-overview.md)을 참조하세요.

[Azure Arc 지원 데이터 서비스](/azure/azure-arc/data/)와 함께 azdata 사용
