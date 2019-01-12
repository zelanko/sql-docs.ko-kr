---
title: 빅 데이터 도구 설치
titleSuffix: SQL Server 2019 big data clusters
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기)와 함께 사용 되는 도구를 설치 하는 방법에 알아봅니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/13/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 54ea67e8b85d4e9a1a8cdbe4b40cf1bb9c3f1062
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241604"
---
# <a name="install-sql-server-2019-big-data-tools"></a>SQL Server 2019 빅 데이터 도구 설치

이 문서에서는 관리를 만들기 위해 설치 해야 하는 클라이언트 도구를 설명 하 고 SQL Server 2019를 사용 하 여 빅 데이터 클러스터 (미리 보기).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>빅 데이터 클러스터 도구

다음 표에서 일반적인 빅 데이터 클러스터 도구 및 설치 하는 방법을 나열 합니다.

| 도구 | 필수 | Description | 설치 |
|---|---|---|---|
| **mssqlctl** | 사용자 계정 컨트롤 | 설치 하 고 빅 데이터 클러스터를 관리 하기 위한 명령줄 도구입니다. | [설치](deploy-install-mssqlctl.md) |
| **kubectl**<sup>1</sup> | 사용자 계정 컨트롤 | 기본 Kuberentes 클러스터를 모니터링 하기 위한 명령줄 도구 ([자세한 내용은](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio** | 사용자 계정 컨트롤 | SQL Server를 쿼리 하기 위한 플랫폼 간 그래픽 도구 ([자세한 내용은](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15)). | [설치](../azure-data-studio/download.md) |
| **SQL Server 2019 확장** | 사용자 계정 컨트롤 | 빅 데이터 클러스터에 연결을 지 원하는 Azure 데이터 Studio에 대 한 확장입니다. 또한 데이터 가상화 마법사를 제공합니다. | [설치](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | AKS에 대 한 | Azure 서비스를 관리 하는 것에 대 한 최신 명령줄 인터페이스입니다. AKS 빅 데이터 클러스터 배포 사용 ([자세한 내용은](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [설치](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | 선택 사항 | SQL Server 쿼리를 위한 최신 명령줄 인터페이스 ([자세한 내용은](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | 일부 스크립트 | SQL Server를 쿼리 하기 위한 레거시 명령줄 도구 ([자세한 내용은](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | 일부 스크립트 | Url 사용 하 여 데이터를 전송 하기 위한 명령줄 도구입니다. | [Windows](https://curl.haxx.se/windows/) \| Linux: curl 패키지 설치 |

<sup>1</sup> kubectl 버전 1.10 이상을 사용 해야 합니다. 또한 kubectl 버전이 더하기 또는 빼기 Kubernetes 클러스터의 한 부 버전 이어야 합니다. Kubectl 클라이언트에 특정 버전을 설치 하려는 경우 참조 [curl을 통해 이진 kubectl 설치](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (Windows 10에서 사용 하 여 cmd.exe와 Windows PowerShell이 아닌 curl을 실행).

<sup>2</sup> Azure CLI 버전 2.0.4 사용 해야 이상. 실행 `az --version` 필요한 경우 버전을 찾으려고 합니다.

<sup>3</sup> Windows 10에서 실행 하는 경우 **curl** cmd 프롬프트에서 실행 하는 경우 경로에 이미 있습니다. Windows의 다른 버전을 다운로드 **curl** 링크를 사용 하 여 경로에 놓습니다.

## <a name="which-tools-are-required"></a>어떤 도구가 필요 한가요?

앞의 표에 모든 빅 데이터 클러스터와 함께 사용 되는 일반적인 도구를 제공 합니다. 도구에 필요한 시나리오에 따라 달라 집니다. 하지만 일반적으로 다음과 같은 도구는 관리, 연결 및 쿼리 하는 클러스터에 대 한 가장 중요 합니다.

- **mssqlctl**
- **Kubectl**
- **Azure Data Studio**
- **SQL Server 2019 확장**

나머지 도구는 특정 시나리오 에서만 필요 합니다. **Azure CLI** AKS 배포와 관련 된 Azure 서비스 관리에 사용할 수 있습니다. **mssql cli** 는 클러스터의 마스터 SQL Server 인스턴스에 연결 하 고 명령줄에서 쿼리를 실행할 수 있는 선택 사항 이지만 유용한 도구입니다. 및 **sqlcmd** 하 고 **curl** GitHub 스크립트를 사용 하 여 샘플 데이터를 설치 하려는 경우이 필요 합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.
