---
title: 빅 데이터 도구 설치
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기)와 함께 사용 되는 도구를 설치 하는 방법에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 757209ff89fd40dcc737b65d3b19f2a7d4ef247b
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419458"
---
# <a name="install-sql-server-2019-big-data-tools"></a>SQL Server 2019 빅 데이터 도구 설치

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 만들고 관리 하 고 사용 하기 위해 설치 해야 하는 클라이언트 도구에 대해 설명 합니다. 다음 섹션에서는 도구 목록 및 설치 지침에 대 한 링크를 제공 합니다. 빅 데이터 클러스터를 배포 하기 전에 Windows 또는 Linux에서 필수로 표시 된 도구를 구성 합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>빅 데이터 클러스터 도구

다음 표에서는 일반적인 빅 데이터 클러스터 도구와 이러한 도구를 설치 하는 방법을 보여 줍니다.

| 도구 | 필수 | 설명 | 설치 |
|---|---|---|---|
| **python** | 예 | Python은 동적 의미 체계를 사용 하는 해석 된 개체 지향 상위 수준 프로그래밍 언어입니다. SQL Server에 대 한 빅 데이터 클러스터의 많은 부분은 python을 사용 합니다. | [Python 설치](#python)|
| **azdata** | 예 | 빅 데이터 클러스터를 설치 하 고 관리 하기 위한 명령줄 도구입니다. | [설치](deploy-install-azdata.md) |
| **kubectl**<sup>1</sup> | 예 | 기본 Kuberentes 클러스터 ([추가 정보](https://kubernetes.io/docs/tasks/tools/install-kubectl/))를 모니터링 하기 위한 명령줄 도구입니다. | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio (참가자)** | 예 | SQL Server 쿼리를 위한 플랫폼 간 그래픽 도구 ([추가 정보](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15)) | [설치](https://aka.ms/azdata-insiders) |
| **SQL Server 2019 확장** | 예 | 빅 데이터 클러스터에 대 한 연결을 지 원하는 Azure Data Studio의 확장입니다. 는 데이터 가상화 마법사도 제공 합니다. | [설치](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | AKS의 경우 | Azure 서비스를 관리 하기 위한 최신 명령줄 인터페이스입니다. AKS 빅 데이터 클러스터 배포와 함께 사용 됩니다 ([자세한 정보](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [설치](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Optional | SQL Server 쿼리를 위한 최신 명령줄 인터페이스 ([추가 정보](https://github.com/dbcli/mssql-cli/blob/master/README.rst)) | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | 일부 스크립트 | SQL Server 쿼리를 위한 레거시 명령줄 도구 ([추가 정보](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)) | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | 일부 스크립트 | Url을 사용 하 여 데이터를 전송 하기 위한 명령줄 도구입니다. | [Windows](https://curl.haxx.se/windows/) \| Linux: 말아 넘기기 패키지 설치 |

<sup>1</sup> kubectl 버전 1.10 이상을 사용 해야 합니다. 또한 kubectl의 버전은 Kubernetes 클러스터의 부 버전의 부 버전 이상 이어야 합니다. Kubectl client에 특정 버전을 설치 하려는 경우에는 [kubectl binary](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) 를 사용 하 여 설치 (windows 10에서는 windows PowerShell을 실행 하는 데 windows PowerShell이 아닌 cmd.exe 사용)를 참조 하세요. 

> [!TIP]
> AKS (Azure Kubernetes Service)에서 이전에 배포 된 클러스터와 함께 kubectl를 사용 하려면 다음 Azure CLI 명령을 사용 하 여 클러스터 컨텍스트를 설정 해야 합니다.
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> Azure CLI 버전 2.0.4 이상을 이상을 사용 해야 합니다. 필요한 `az --version` 경우를 실행 하 여 버전을 찾습니다.

<sup>3</sup> Windows 10에서 실행 중인 경우에는 cmd 프롬프트에서 실행 하는 경우에는 현재 경로에 **말아 넘기기** 를 실행 합니다. 다른 버전의 Windows에서는 링크를 사용 하 여 **말아 넘기기** 를 다운로드 하 고 경로에 저장 합니다.

## <a name="which-tools-are-required"></a>필요한 도구는 무엇입니까?

위의 표에서는 빅 데이터 클러스터에 사용 되는 모든 일반 도구를 제공 합니다. 필요한 도구는 시나리오에 따라 달라 집니다. 그러나 일반적으로 다음 도구는 클러스터를 관리, 연결 및 쿼리 하는 데 가장 중요 합니다.

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 확장**

나머지 도구는 특정 시나리오 에서만 필요 합니다. **Azure CLI** 는 AKS 배포와 관련 된 Azure 서비스를 관리 하는 데 사용할 수 있습니다. **mssql-cli** 는 클러스터의 SQL Server 마스터 인스턴스에 연결 하 고 명령줄에서 쿼리를 실행할 수 있도록 하는 선택적 이지만 유용한 도구입니다. 그리고 GitHub 스크립트를 사용 하 여 샘플 데이터를 설치 하려는 경우에는 **sqlcmd** 및 **말아** 가 필요 합니다.

### <a id="python"></a>Python 오프 라인 설치

1. 인터넷에 액세스 된 컴퓨터에서 Python을 포함 하는 다음 압축 파일 중 하나를 다운로드 합니다.

   | 운영 체제 | 다운로드 |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 압축 된 파일을 대상 컴퓨터에 복사 하 고 원하는 폴더에 압축을 풉니다.

1. Windows의 경우 해당 폴더 `installLocalPythonPackages.bat` 에서를 실행 하 고 전체 경로를 매개 변수와 동일한 폴더에 전달 합니다.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="next-steps"></a>다음 단계

도구를 구성한 후에는 클라우드 또는 온-프레미스에서 Kubernetes에 SQL Server 2019 빅 데이터 클러스터를 배포 합니다. 자세한 내용은 다음 배포 문서를 참조 하세요.

- [빠른 시작: AKS (Azure Kubernetes Service)에서 빅 데이터 클러스터 SQL Server 배포](quickstart-big-data-cluster-deploy.md)
- [Kubernetes에서 SQL Server 빅 데이터 클러스터를 배포 하는 방법](deployment-guidance.md)

빅 데이터 클러스터에 대 한 자세한 내용은 [SQL Server 2019 빅 데이터 클러스터 란?](big-data-cluster-overview.md)을 참조 하세요.
