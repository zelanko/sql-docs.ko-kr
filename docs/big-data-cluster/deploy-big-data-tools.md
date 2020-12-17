---
title: 빅 데이터 도구 설치
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터와 함께 사용되는 도구를 설치하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e6571c92f68412a464b96964be4b02d22a106a0b
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489703"
---
# <a name="install-sql-server-2019-big-data-tools"></a>SQL Server 2019 빅 데이터 도구 설치

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]를 만들고 관리 및 사용하기 위해 설치해야 하는 클라이언트 도구를 설명합니다. 다음 섹션에서는 도구 목록 및 설치 지침 링크를 제공합니다. 빅 데이터 클러스터를 배포하기 전에 Windows 또는 Linux에서 필수로 표시된 도구를 구성합니다.

## <a name="big-data-cluster-tools"></a>빅 데이터 클러스터 도구

다음 표에는 일반적인 빅 데이터 클러스터 도구와 도구 설치 방법이 나와 있습니다.

| 도구 | 필수 | Description | 설치 |
|---|---|---|---|
| `python` | 예 | python은 동적 의미 체계를 사용하는 해석된 개체 지향 고급 프로그래밍 언어입니다. SQL Server 빅 데이터 클러스터의 대부분은 python을 사용합니다. | [python 설치](#python).|
| [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] | 예 | 빅 데이터 클러스터를 설치하고 관리하기 위한 명령줄 도구입니다. | [설치](../azdata/install/deploy-install-azdata.md) |
| `kubectl`<sup>1</sup> | 예 | 기본 Kubernetes 클러스터를 모니터링하기 위한 명령줄 도구입니다([자세한 정보](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-using-native-package-management) |
| **Azure Data Studio** | 예 | SQL Server를 쿼리하기 위한 플랫폼 간 그래픽 도구입니다. | [설치](../azure-data-studio/download-azure-data-studio.md) |
| **데이터 가상화 확장** | 예 | 데이터 가상화 마법사를 제공하는 Azure Data Studio용 확장입니다. | [설치](../azure-data-studio/extensions/data-virtualization-extension.md) |
| **Azure CLI**<sup>2</sup> | AKS의 경우 | Azure 서비스를 관리하기 위한 최신 명령줄 인터페이스입니다. AKS 빅 데이터 클러스터 배포와 함께 사용됩니다([자세한 정보](/cli/azure/)). | [설치](/cli/azure/install-azure-cli) |
| **mssql-cli** | 옵션 | SQL Server를 쿼리하기 위한 최신 명령줄 인터페이스입니다([자세한 정보](../tools/mssql-cli.md)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | 일부 스크립트의 경우 | SQL Server를 쿼리하기 위한 레거시 명령줄 도구입니다([자세한 정보](../tools/sqlcmd-utility.md)). SQLCMD 패키지를 설치하기 전에 Microsoft ODBC Driver 11 for SQL Server를 설치해야 할 수 있습니다. | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| `curl` <sup>3</sup> | 일부 스크립트의 경우 | URL을 사용하여 데이터를 전송하기 위한 명령줄 도구입니다. | [Windows](https://curl.haxx.se/windows/) \| Linux: curl 패키지 설치 |
| `oc` | Red Hat OpenShift 및 Azure Redhat OpenShift 배포에 필요합니다. |`oc`는 OpenShift CLI(명령줄 인터페이스)입니다. | [CLI 설치](https://docs.openshift.com/container-platform/4.4/cli_reference/openshift_cli/getting-started-cli.html#installing-the-cli)

<sup>1</sup>`kubectl` 버전 1.13 이상을 사용해야 합니다. 또한 `kubectl` 버전은 Kubernetes 클러스터의 바로 이전 또는 이후 부 버전이어야 합니다. `kubectl` 클라이언트에서 특정 버전을 설치하려는 경우 [Install `kubectl` binary via curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)(curl을 통해 kubectl 이진 설치)를 참조하세요(Windows 10에서는 Windows PowerShell이 아닌 cmd.exe를 사용하여 curl 실행).

> [!TIP]
> AKS(Azure Kubernetes Service)에서 이전에 배포한 클러스터와 함께 `kubectl`을 사용하려면 다음 Azure CLI 명령을 사용하여 클러스터 컨텍스트를 설정해야 합니다.
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> Azure CLI 버전 2.0.4 이상을 사용해야 합니다. 필요한 경우 `az --version`을 실행하여 버전을 찾습니다.

<sup>3</sup> Windows 10에서 실행하는 경우에는 cmd 프롬프트에서 실행할 때 `curl`이 PATH에 이미 있습니다. 다른 Windows 버전에서는 링크를 사용하여 `curl`을 다운로드한 다음, PATH에 저장합니다.

## <a name="which-tools-are-required"></a>필수 도구

위의 표에서는 빅 데이터 클러스터에서 사용되는 일반적인 도구를 모두 제공합니다. 필수 도구는 시나리오에 따라 다릅니다. 그러나 일반적으로 클러스터를 관리, 연결 및 쿼리하는 데 가장 중요한 도구는 다음과 같습니다.

- [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]
- `kubectl`
- **Azure Data Studio**
- **데이터 가상화 확장**

나머지 도구는 특정 시나리오에서만 필요합니다. **Azure CLI** 는 AKS 배포와 관련된 Azure 서비스를 관리하는 데 사용할 수 있습니다. **mssql-cli** 는 선택 사항이지만, 클러스터의 SQL Server 마스터 인스턴스에 연결하고 명령줄에서 쿼리를 실행할 수 있도록 하는 유용한 도구입니다. 또한 GitHub 스크립트를 사용하여 샘플 데이터를 설치하려는 경우 **sqlcmd** 및 `curl`이 필요합니다.

### <a name="install-python-offline"></a><a id="python"></a> python 오프라인 설치

1. 인터넷에 액세스할 수 있는 머신에서 Python을 포함하는 다음 압축 파일 중 하나를 다운로드합니다.

   | 운영 체제 | 다운로드 |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 압축 파일을 대상 머신에 복사하고 선택한 폴더로 추출합니다.

1. 해당 폴더에서 `installLocalPythonPackages.bat`를 실행하고 동일한 폴더의 전체 경로를 매개 변수로 전달합니다(Windows에만 해당).

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="download-and-install-azure-data-studio"></a>Azure Data Studio 다운로드 및 설치

Azure Data Studio는 특히 SQL Server 빅 데이터 클러스터를 위한 기능을 제공합니다.

[최신 Azure Data Studio를 가져옵니다](../azure-data-studio/download-azure-data-studio.md).

최신 릴리스에 대한 자세한 내용은 [릴리스 정보](./release-notes-big-data-cluster.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

도구를 구성한 후에는 클라우드 또는 온-프레미스의 Kubernetes에 SQL Server 2019 빅 데이터 클러스터를 배포합니다. 자세한 내용은 다음 배포 문서를 참조하세요.

- [빠른 시작: AKS(Azure Kubernetes Service)에 SQL Server 빅 데이터 클러스터 배포](quickstart-big-data-cluster-deploy.md)
- [Kubernetes에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.