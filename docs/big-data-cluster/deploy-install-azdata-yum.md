---
title: yum을 사용하여 azdata 설치
titleSuffix: SQL Server big data clusters
description: yum을 사용하여 빅 데이터 클러스터를 설치하고 관리할 수 있는 azdata 도구 설치 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cf6e061b0ca4fca7c843575a87038a801ab8f758
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75728554"
---
# <a name="install-azdata-with-yum"></a>yum을 사용하여 `azdata` 설치

`yum`을 사용한 Linux 배포판의 경우, `azdata-cli`에 대한 패키지가 있습니다. CLI 패키지는 `yum`을 사용하는 다음의 Linux 버전에서 테스트되었습니다.

- RHEL 7, RHEL 8


[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-yum"></a>yum을 사용하여 설치

>[!IMPORTANT]
> `azdata-cli`의 RPM 패키지는 python3 패키지에 따라 달라집니다. 시스템에서 이 패키지는 *Python 3.6.x* 요구 사항 이전의 Python 버전일 수 있습니다. 이로 인해 문제가 발생하는 경우, 대체 python3 패키지를 찾거나 [`pip`](deploy-install-azdata-pip.md)를 사용하는 수동 설치 지침을 따릅니다.

1. Microsoft 리포지토리 키 가져오기

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. 로컬 리포지토리 정보 만들기

   RHEL 7 클라이언트의 경우 다음을 실행합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```
  
   RHEL 8 클라이언트의 경우 다음을 실행합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo
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

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
