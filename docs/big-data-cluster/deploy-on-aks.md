---
title: Azure Kubernetes Service를 구성 합니다.
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기) 배포에 대 한 Azure Kubernetes Service (AKS)를 구성 하는 방법에 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/10/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d39f62345a539094c585b196c9b6030b673f8e89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958483"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-big-data-cluster-deployments"></a>SQL Server 빅 데이터 클러스터 배포에 대 한 Azure Kubernetes Service 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 배포에 대 한 Azure Kubernetes Service (AKS)를 구성 하는 방법을 설명 합니다.

AKS를 사용 하면 간단 하 게 생성, 구성 및 컨테이너 화 된 응용 프로그램을 실행 하는 Kubernetes 클러스터를 사용 하 여 미리 구성 된 가상 머신의 클러스터를 관리 합니다. 이 통해 배포 하 고 Microsoft Azure에서 컨테이너 기반 응용 프로그램 관리의 커뮤니티 전문 지식의 점점 본문을 하거나 기존 기술을 사용할 수 있습니다.

이 문서에서는 Azure CLI를 사용 하 여 AKS에서 Kubernetes를 배포 하는 단계를 설명 합니다. Azure 구독이 없으면 시작 하기 전에 무료 계정을 만듭니다.

> [!TIP] 
> AKS와 SQL Server 빅 데이터 클러스터를 배포 하는 샘플 python 스크립트를 참조 하세요. [빠른 시작: 빅 데이터 클러스터 Azure Kubernetes Service (AKS)에서 SQL Server 배포](quickstart-big-data-cluster-deploy.md)합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 도구 배포](deploy-big-data-tools.md):
   - **Kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **Azure CLI**

- Kubernetes 서버용 1.10 최소 버전입니다. AKS를 사용 해야 `--kubernetes-version` 기본값과 다른 버전을 지정 하려면 매개 변수입니다.

- AKS에서 기본 시나리오를 확인 하는 동안 최적의 환경을 사용 합니다.
   - 모든 노드에서 8 개의 Vcpu
   - 32GB의 메모리가 VM 당
   - 모든 노드에서 24 또는 더 연결 된 디스크

   > [!TIP]
   > Vm에 대 한 여러 크기 옵션을 제공 하는 azure 인프라를 참조 하십시오 [여기](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) 배포 하려는 지역에 대 한 선택 항목에 대 한 합니다.

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Azure 리소스 그룹은 Azure 리소스가 배포 및 관리 되는 논리적 그룹입니다. 다음 단계를 Azure에 로그인 하 고 AKS 클러스터에 대 한 리소스 그룹을 만듭니다.

1. 명령 프롬프트에서 다음 명령을 실행 하 고 지시에 따라 Azure 구독에 로그인 합니다.

    ```azurecli
    az login
    ```

1. 여러 구독이 있는 경우 다음 명령을 실행 하 여 구독의 모든를 볼 수 있습니다.

   ```azurecli
   az account list
   ```

1. 다른 구독으로 변경 하려는 경우이 명령을 실행할 수 있습니다.

   ```azurecli
   az account set --subscription <subscription id>
   ```

1. 사용 하 여 리소스 그룹을 만들어야 합니다 **az 그룹 만들기** 명령입니다. 다음 예제에서는 명명 된 리소스 그룹을 만듭니다 `sqlbdcgroup` 에 `westus2` 위치 합니다.

   ```azurecli
   az group create --name sqlbdcgroup --location westus2
   ```

## <a name="verify-available-kubernetes-versions"></a>사용 가능한 Kubernetes 버전 확인

Kubernetes의 사용 가능한 최신 버전을 사용 합니다. 사용 가능한 최신 버전의 클러스터 배포 하는 위치에 따라 달라 집니다. 다음 명령은 특정 위치에 사용 가능한 Kubernetes 버전을 반환합니다.

이 명령은 실행 하기 전에 스크립트를 업데이트 합니다. 대체 `<Azure data center>` 클러스터의 위치입니다.

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

클러스터에서 사용 가능한 최신 버전을 선택 합니다. 버전 번호를 기록 합니다. 다음 단계에서이 사용 합니다.

## <a name="create-a-kubernetes-cluster"></a>Kubernetes 클러스터 만들기

1. 사용 하 여 AKS에서 Kubernetes 클러스터 만들기는 [az aks 만들기](https://docs.microsoft.com/cli/azure/aks) 명령입니다. 다음 예제에서는 라는 Kubernetes 클러스터를 만듭니다 *kubcluster* 크기의 Linux 에이전트 노드 하나를 사용 하 여 **Standard_L8s**합니다.

   스크립트를 실행 하기 전에 대체 `<version number>` 이전 단계에서 확인 된 버전 번호를 사용 하 여 합니다.

   이전 섹션에서 사용한 동일한 리소스 그룹에서 AKS 클러스터를 만든 있는지 확인 합니다.

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

   늘리거나 변경 하 여 Kubernetes 에이전트 노드 수를 줄일 수는 `--node-count <n>` 여기서 `<n>` 사용 하려는 에이전트 노드 수입니다. 여기에 AKS에서 내부적으로 관리 되는 마스터 Kubernetes 노드를 포함 되지 않습니다. 앞의 예제만 평가 목적에 대 한 단일 노드를 사용합니다.

   몇 분 후 명령이 완료 되 고 클러스터에 대 한 JSON 형식 정보를 반환 합니다.

   > [!TIP]
   > 오류가 발생 하면 AKS 클러스터를 만들기, 참조를 [문제 해결 섹션](#troubleshoot) 이 문서의.

1. 나중에 사용할 이전 명령의 JSON 출력을 저장 합니다.

## <a name="connect-to-the-cluster"></a>클러스터에 연결

1. Kubernetes 클러스터에 연결 하도록 kubectl을 구성 하려면 다음을 실행 합니다 [az aks 자격 증명 가져오기](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) 명령입니다. 이 단계는 자격 증명을 다운로드 하 고 kubectl CLI 사용을 구성 합니다.

   ```azurecli
   az aks get-credentials --resource-group=sqlbdcgroup --name kubcluster
   ```

1. 클러스터에 대 한 연결을 확인 하려면 사용 합니다 [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) 클러스터 노드의 목록을 반환 하는 명령입니다.  아래 예제에서는 출력을 보여 줍니다. 1 개 마스터 및 3 개의 에이전트 노드가 있는 경우.

   ```bash
   kubectl get nodes
   ```

## <a id="troubleshoot"></a> 문제 해결

이전 명령을 사용 하 여 Azure Kubernetes 서비스를 만드는 데 문제가 있으면 다음 해결 방법을 시도 합니다.

- 설치 해야 합니다 [최신 Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)합니다.
- 동일한 단계를 다른 리소스 그룹 및 클러스터 이름을 사용 하 여 시도 합니다.

## <a name="next-steps"></a>다음 단계

이 문서의 단계는 AKS에서 Kubernetes 클러스터를 구성합니다. AKS Kubernetes 클러스터에서 SQL Server 2019 빅 데이터 클러스터를 배포 하려면 다음 단계가입니다. 빅 데이터 클러스터를 배포 하는 방법에 대 한 자세한 내용은 다음 문서를 참조 하세요.

[Kubernetes에서 SQL Server 빅 데이터 클러스터를 배포 하는 방법](deployment-guidance.md)
