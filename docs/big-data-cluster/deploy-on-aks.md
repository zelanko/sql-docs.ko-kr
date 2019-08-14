---
title: Azure Container Service 구성
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터(미리 보기) 배포에 대해 AKS(Azure Kubernetes Service)를 구성하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/10/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1ba5b4b06d31f391733603ce146a7d05e05aebaf
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68470810"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-big-data-cluster-deployments"></a>SQL Server 빅 데이터 클러스터 배포에 대해 Azure Kubernetes Service 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 2019 빅 데이터 클러스터(미리 보기) 배포에 대해 AKS(Azure Kubernetes Service)를 구성하는 방법을 설명합니다.

AKS를 사용하면 Kubernetes 클러스터로 미리 구성된 가상 머신 클러스터를 간편하게 만들고 구성 및 관리하여 컨테이너화된 애플리케이션을 실행할 수 있습니다. 따라서 기존 기술을 사용하거나 계속 확장되는 대규모 커뮤니티 전문 지식을 활용하여 Microsoft Azure에 컨테이너 기반 애플리케이션을 배포하고 관리할 수 있습니다.

이 문서에서는 Azure CLI를 사용하여 AKS에 Kubernetes를 배포하는 단계를 설명합니다. Azure 구독이 없는 경우 시작하기 전에 체험 계정을 만듭니다.

> [!TIP]
> AKS 및 빅 데이터 클러스터의 배포를 한 단계로 스크립팅할 수도 있습니다. 자세한 내용은 [python 스크립트](quickstart-big-data-cluster-deploy.md) 또는 Azure Data Studio [Notebook](deploy-notebooks.md)의 작업 방법을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 도구 배포](deploy-big-data-tools.md):
   - **Kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **Azure CLI**

- Kubernetes 서버 버전 1.10 이상. AKS의 경우 `--kubernetes-version` 매개 변수를 사용하여 기본값과 다른 버전을 지정해야 합니다.

- AKS에서 기본 시나리오의 유효성을 검사하는 환경을 최적화하려면 다음을 사용합니다.
   - 모든 노드에서 vCPU 8개
   - VM당 32GB 메모리
   - 모든 노드에서 24개 이상의 연결된 디스크

   > [!TIP]
   > Azure 인프라는 VM에 대한 여러 가지 크기 옵션을 제공합니다. 배포하려는 지역에서 선택할 수 있는 옵션은 [여기](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)를 참조하세요.

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Azure 리소스 그룹은 Azure 리소스가 배포되고 관리되는 논리 그룹입니다. 다음 단계에서는 Azure에 로그인하고 AKS 클러스터의 리소스 그룹을 만듭니다.

1. 명령 프롬프트에서 다음 명령을 실행하고 프롬프트에 따라 해당 Azure 구독에 로그인합니다.

    ```azurecli
    az login
    ```

1. 구독이 여러 개인 경우 다음 명령을 실행하여 모든 구독을 볼 수 있습니다.

   ```azurecli
   az account list
   ```

1. 다른 구독으로 변경하려면 다음 명령을 실행할 수 있습니다.

   ```azurecli
   az account set --subscription <subscription id>
   ```

1. **az group create** 명령을 사용하여 리소스 그룹을 만듭니다. 다음 예제에서는 `westus2` 위치에 `sqlbdcgroup`이라는 리소스 그룹을 만듭니다.

   ```azurecli
   az group create --name sqlbdcgroup --location westus2
   ```

## <a name="verify-available-kubernetes-versions"></a>사용 가능한 Kubernetes 버전 확인

사용 가능한 최신 버전의 Kubernetes를 사용합니다. 사용 가능한 최신 버전은 클러스터를 배포하는 위치에 따라 다릅니다. 다음 명령은 특정 위치에서 사용할 수 있는 Kubernetes 버전을 반환합니다.

명령을 실행하기 전에 스크립트를 업데이트합니다. `<Azure data center>`를 해당 클러스터의 위치로 바꿉니다.

   **bash**

   ```bash
   az aks get-versions \
   --location <Azure data center> \
   --query orchestrators \
   --o table
   ```

   **PowerShell**

   ```powershell
   az aks get-versions `
   --location <Azure data center> `
   --query orchestrators `
   --o table
   ```

해당 클러스터에 사용할 수 있는 최신 버전을 선택합니다. 버전 번호를 적어 둡니다. 이 버전 번호는 다음 단계에서 사용합니다.

## <a name="create-a-kubernetes-cluster"></a>Kubernetes 클러스터 만들기

1. [az aks create](https://docs.microsoft.com/cli/azure/aks) 명령을 사용하여 AKS에서 Kubernetes 클러스터를 만듭니다. 다음 예제에서는 크기가 **Standard_L8s**인 Linux 에이전트 노드 1개를 사용하여 *kubcluster*라는 Kubernetes 클러스터를 만듭니다.

   스크립트를 실행하기 전에 `<version number>`를 이전 단계에서 확인한 버전 번호로 바꿉니다.

   이전 섹션에서 사용한 것과 동일한 리소스 그룹에 AKS 클러스터를 만들어야 합니다.

   **bash:**

   ```bash
   az aks create --name kubcluster \
   --resource-group sqlbdcgroup \
   --generate-ssh-keys \
   --node-vm-size Standard_L8s \
   --node-count 1 \
   --kubernetes-version <version number>
   ```

   **PowerShell:**

   ```powershell
   az aks create --name kubcluster `
   --resource-group sqlbdcgroup `
   --generate-ssh-keys `
   --node-vm-size Standard_L8s `
   --node-count 1 `
   --kubernetes-version <version number>
   ```

   `--node-count <n>`를 변경하여 Kubernetes 에이전트 노드 수를 늘리거나 줄일 수 있습니다. 여기서 `<n>`은 사용하려는 에이전트 노드 수입니다. AKS에서 백그라운드로 관리하는 마스터 Kubernetes 노드는 여기에 포함되지 않습니다. 위 예제에서는 평가 목적으로 단일 노드만 사용합니다.

   몇 분 후에 명령이 완료되고 클러스터에 대한 JSON 형식의 정보가 반환됩니다.

   > [!TIP]
   > AKS에서 클러스터를 만드는 중 오류가 발생하는 경우 이 문서의 [문제 해결 섹션](#troubleshoot)을 참조하세요.

1. 나중에 사용하기 위해 위 명령의 JSON 출력을 저장합니다.

## <a name="connect-to-the-cluster"></a>클러스터에 연결

1. Kubernetes 클러스터에 연결하도록 kubectl을 구성하려면 [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) 명령을 실행합니다. 이 단계에서는 자격 증명을 다운로드하고 해당 자격 증명을 사용하도록 kubectl CLI를 구성합니다.

   ```azurecli
   az aks get-credentials --resource-group=sqlbdcgroup --name kubcluster
   ```

1. 클러스터에 대한 연결을 확인하려면 [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) 명령을 사용하여 클러스터 노드 목록을 반환합니다.  아래 예제에서는 마스터 1개와 에이전트 노드 3개가 있는 경우의 출력을 보여 줍니다.

   ```bash
   kubectl get nodes
   ```

## <a id="troubleshoot"></a> 문제 해결

위 명령을 사용하여 Azure Kubernetes Service를 만드는 데 문제가 있는 경우 다음 해결 방법을 사용해 보세요.

- [최신 Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)를 설치했는지 확인합니다.
- 다른 리소스 그룹 및 클러스터 이름을 사용하여 동일한 단계를 시도합니다.

## <a name="next-steps"></a>다음 단계

이 문서의 단계에서는 AKS에서 Kubernetes 클러스터를 구성했습니다. 다음 단계는 AKS Kubernetes 클러스터에 SQL Server 2019 빅 데이터 클러스터를 배포하는 것입니다. 빅 데이터 클러스터를 배포하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

[Kubernetes에 SQL Server 빅 데이터 클러스터를 배포하는 방법](deployment-guidance.md)
