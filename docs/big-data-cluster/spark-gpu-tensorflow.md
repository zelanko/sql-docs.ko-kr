---
title: GPU 지원 및 TensorFlow
titleSuffix: SQL Server big data clusters
description: GPU 지원이 포함 된 빅 데이터 클러스터를 배포 하 고 Azure 데이터 Studio 노트북에서 TensorFlow를 사용 합니다.
author: inchiosa
ms.author: marinch
ms.reviewer: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2d31736ee4dd68857e3afce678b6dd806701a82b
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774947"
---
# <a name="deploy-a-big-data-cluster-with-gpu-support-and-run-tensorflow"></a>GPU 지원이 포함 된 빅 데이터 클러스터를 배포 및 TensorFlow를 실행 합니다.

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서 Kubernetes AKS (Azure Service) 계산 집약적 워크 로드에 대 한 GPU 사용 노드 풀을 지 원하는 빅 데이터 클러스터를 배포 하는 방법에 설명 합니다. 그런 다음 GPU에 대 한 TensorFlow 사용 하 여 이미지 분류를 수행 하는 Azure Data Studio에서 예제 notebook을 실행 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [빅 데이터 도구도](deploy-big-data-tools.md):
  - **mssqlctl**
  - **kubectl**
  - **Azure Data Studio**
  - **SQL Server 2019 확장**
  - **Azure CLI**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="create-an-aks-cluster"></a>AKS 클러스터 만들기

다음 단계를 지 원하는 Gpu AKS 클러스터를 만드는 Azure CLI를 사용 합니다.

1. 명령 프롬프트에서 다음 명령을 실행 하 고 지시에 따라 Azure 구독에 로그인 합니다.

    ```azurecli
    az login
    ```

1. 사용 하 여 리소스 그룹을 만들어야 합니다 **az 그룹 만들기** 명령입니다. 다음 예제에서는 명명 된 리소스 그룹을 만듭니다 `sqlbigdatagroupgpu` 에 `eastus` 위치 합니다.

   ```azurecli
   az group create --name sqlbigdatagroupgpu --location eastus
   ```

1. 사용 하 여 AKS에서 Kubernetes 클러스터 만들기는 [az aks 만들기](https://docs.microsoft.com/cli/azure/aks) 명령입니다. 다음 예제에서는 라는 Kubernetes 클러스터를 만듭니다 `gpucluster` 에 `sqlbigdatagroupgpu` 리소스 그룹입니다.

   ```azurecli
   az aks create --name gpucluster --resource-group sqlbigdatagroupgpu --generate-ssh-keys --node-vm-size Standard_NC6s_v3 --node-count 3 --node-osdisk-size 50 --kubernetes-version 1.11.9 --location eastus
   ```

   > [!NOTE]
   > 이 클러스터에서 사용 하는 **Standard_NC6s_v3** [GPU에 최적화 된 가상 머신 크기](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-gpu), 단일 또는 여러 NVIDIA Gpu를 사용 하 여 사용할 수 있는 특수 한 가상 컴퓨터 중 하나입니다. 자세한 내용은 [계산 집약적인 워크 로드에 Azure Kubernetes Service (AKS)를 사용 하 여 Gpu](https://docs.microsoft.com/azure/aks/gpu-cluster)합니다.

1. Kubernetes 클러스터에 연결 하도록 kubectl을 구성 하려면 다음을 실행 합니다 [az aks 자격 증명 가져오기](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) 명령입니다.

   ```azurecli
   az aks get-credentials --overwrite-existing --resource-group=sqlbigdatagroupgpu --name gpucluster
   ```

## <a name="apply-yaml-manifest"></a>YAML 매니페스트를 적용 합니다.

1. 사용 하 여 **kubectl** 이라는 Kubernetes 네임 스페이스를 만드는 `gpu-resources`합니다.

   ```bash
   kubectl create namespace gpu-resources
   ```

1. 라는 파일에 다음 YAML 파일의 내용을 저장할 **nvidia 장치-플러그 인 ds.yaml**합니다. 실행 중인 컴퓨터에서 작업 디렉터리에 저장 **kubectl** 에서 합니다.

   업데이트 된 `image: nvidia/k8s-device-plugin:1.11` Kubernetes 버전과 일치 하도록 매니페스트를 아래로 반 방향입니다. 예를 들어, AKS 클러스터 버전 1.12 Kubernetes를 실행 하는 경우 태그를 업데이트 `image: nvidia/k8s-device-plugin:1.12`합니다.

   ```yaml
   apiVersion: extensions/v1beta1
   kind: DaemonSet
   metadata:
     labels:
       kubernetes.io/cluster-service: "true"
     name: nvidia-device-plugin
     namespace: gpu-resources
   spec:
     template:
       metadata:
         # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler
         # reserves resources for critical add-on pods so that they can be rescheduled after
         # a failure.  This annotation works in tandem with the toleration below.
         annotations:
           scheduler.alpha.kubernetes.io/critical-pod: ""
         labels:
           name: nvidia-device-plugin-ds
       spec:
         tolerations:
         # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode.
         # This, along with the annotation above marks this pod as a critical add-on.
         - key: CriticalAddonsOnly
           operator: Exists
         containers:
         - image: nvidia/k8s-device-plugin:1.11 # Update this tag to match your Kubernetes version
           name: nvidia-device-plugin-ctr
           securityContext:
             allowPrivilegeEscalation: false
             capabilities:
               drop: ["ALL"]
           volumeMounts:
             - name: device-plugin
               mountPath: /var/lib/kubelet/device-plugins
         volumes:
           - name: device-plugin
             hostPath:
               path: /var/lib/kubelet/device-plugins
         nodeSelector:
           beta.kubernetes.io/os: linux
           accelerator: nvidia
   ```

1. 지금 사용 하 여 kubectl apply DaemonSet를 만들려면 명령입니다. **nvidia 장치-플러그 인 ds.yaml** 명령을 실행할 때 작업 디렉터리에 있어야 합니다.

   ```bash
   kubectl apply -f nvidia-device-plugin-ds.yaml
   ```

## <a name="deploy-the-big-data-cluster"></a>빅 데이터 클러스터를 배포 합니다.

Gpu를 지 원하는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 배포 하려면 리포지토리 특정 docker 레지스트리를 배포 해야 합니다. 다음 환경 변수를 GPU 배포용 다릅니다.

| 환경 변수 | 값 |
|---|---|
| **DOCKER_REGISTRY** | `marinchcreus3.azurecr.io` |
| **DOCKER_REPOSITORY** | `ctp25-8-0-61-gpu` |
| **DOCKER_USERNAME** | `<your username, gpu-specific credentials provided by Microsoft>` |
| **DOCKER_PASSWORD** | `<your password, gpu-specific credentials provided by Microsoft>` |

사용 하 여 **mssqlctl** 클러스터, aks-dev-test.json 구성 선택 및 사용자 지정 메시지가 표시 되 면 위의 값 공급 배포할 수 있습니다.

```bash
mssqlctl cluster create
```

> [!TIP]
> 빅 데이터 클러스터의 기본 이름은 `mssql-cluster`합니다.

또한 사용자 지정 배포 구성 파일을 전달 하 여 추가 배포를 지정할 수 있습니다. 자세한 내용은 참조는 [배포 가이드](deployment-guidance.md#customconfig)합니다.

## <a name="run-the-tensorflow-example"></a>TensorFlow 예제 실행

다음 두 가지 예제 notebook에는 두 가지 이미지 분류 모델을 학습 GPU에 대 한 TensorFlow를 사용 하 여 Spark 클러스터의 단일 노드에서 보여 줍니다.

| Notebook 다운로드 | Description |
|---|---|
| [**tf-cuda8.ipynb**](https://aka.ms/AA4jdgd) | 8 CUDA, CUDNN, 6 및 1.4.0 TensorFlow를 사용합니다.  |
| [**tf-cuda9.ipynb**](https://aka.ms/AA4ixzr) | 9 CUDA, CUDNN 7 및 1.12.0 TensorFlow를 사용합니다. |

로컬 컴퓨터에 적절 한 전자 필기장 파일 열기 및 PySpark3 커널을 사용 하 여 Azure 데이터 스튜디오에서 실행 합니다. CUDA TensorFlow의 이전 버전 특별히 필요한 경우가 아니라면 CUDA 9/CUDNN 7/TensorFlow 1.12.0를 선택 합니다. 빅 데이터 클러스터를 사용 하 여 notebook을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법을](notebooks-guidance.md)합니다.

> [!NOTE]
> 시스템 위치에 소프트웨어를 설치 하 여 notebook을 참고 합니다. Notebook은 현재 CTP 2.5에서 루트 권한으로 실행 되기 때문에 이것이 가능 합니다.

NVIDIA GPU 라이브러리 및 TensorFlow gpu를 설치한 후 notebook에 사용할 수 있는 GPU 장치를 나열 합니다. 그런 다음 적합 하며 MNIST 데이터 집합을 사용 하 여 필기 숫자를 인식 하도록 TensorFlow 모델을 평가 합니다. 사용 가능한 디스크 공간을 확인 한 후 다운로드 하며에서 10 CIFAR 이미지 분류 예제를 실행 [ https://github.com/tensorflow/models.git ](https://github.com/tensorflow/models.git)합니다. 여러 Gpu 클러스터에서 CIFAR 10 예제를 실행 하 여 Azure에서 사용 가능한 GPU의 각 세대에서 제공 하는 속도 향상을 확인할 수 있습니다.

## <a name="clean-up-resources"></a>리소스 정리

빅 데이터 클러스터를 삭제 하려면 다음 명령을 사용 합니다.

```bash
mssqlctl cluster delete --name gpubigdatacluster
```

이전 명령에서 AKS 클러스터를 제거 하지 않습니다. AKS 클러스터와 연결 된 리소스를 삭제 하려면 다음 명령을 사용 합니다.

```azurecli
az group delete -n sqlbigdatagroupgpu
```

## <a name="next-steps"></a>다음 단계

SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.
