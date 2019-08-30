---
title: Kubernetes의 데이터 지속성
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터에서 데이터 지속성이 작동하는 방식을 알아봅니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7a12afd88f0eb83de7d5c5bd4a3735e71e037138
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155348"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Kubernetes의 SQL Server 빅 데이터 클러스터를 사용한 데이터 지속성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[영구적 볼륨](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)은 Kubernetes의 스토리지에 대한 플러그 인 모델을 제공합니다. 스토리지 제공 방법은 사용 방법과 별도로 추상화됩니다. 따라서 고유한 고가용성 스토리지를 가져와 SQL Server 빅 데이터 클러스터에 연결할 수 있습니다. 이 기능을 통해 필요한 스토리지 유형, 가용성 및 성능을 완벽하게 제어할 수 있습니다. Kubernetes는 Azure 디스크/파일, NFS, 로컬 스토리지 등을 비롯한 다양한 종류의 스토리지 솔루션을 지원합니다.

## <a name="configure-persistent-volumes"></a>영구적 볼륨 구성

SQL Server 빅 데이터 클러스터는 [스토리지 클래스](https://kubernetes.io/docs/concepts/storage/storage-classes/)를 통해 이러한 영구적 볼륨을 사용합니다. 스토리지 종류에 따라 다양한 스토리지 클래스를 만들고 빅 데이터 클러스터 배포 시 지정할 수 있습니다. 풀 수준에서 각 용도에 사용할 스토리지 클래스와 영구적 볼륨 클레임 크기를 구성할 수 있습니다. SQL Server 빅 데이터 클러스터는 영구적 볼륨이 필요한 각 구성 요소에 대해 [영구적 볼륨 클레임](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)을 지정된 스토리지 클래스 이름으로 만듭니다. 그런 다음, Pod에 해당하는 영구적 볼륨을 탑재합니다. 

## <a name="configure-big-data-cluster-storage-settings"></a>빅 데이터 클러스터 스토리지 설정 구성

다른 사용자 지정과 마찬가지로, 배포 시 각 풀과 제어 평면에 맞게 클러스터 구성 파일의 스토리지 설정을 지정할 수 있습니다. 풀 사양에 스토리지 구성 설정이 없으면 제어 평면 스토리지 설정이 사용됩니다. 다음은 사양에 포함할 수 있는 스토리지 구성 섹션의 샘플입니다.

```json
    "storage": 
    {
      "data": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
    }
```

빅 데이터 클러스터 배포는 영구적 스토리지를 사용하여 다양한 구성 요소의 데이터, 메타데이터 및 로그를 저장합니다. 배포 과정에서 생성되는 영구적 볼륨 클레임의 크기를 사용자 지정할 수 있습니다. 모범 사례에 따라 ‘유지’ [회수 정책](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)으로 스토리지 클래스를 사용하는 것이 좋습니다.

> [!NOTE]
> CTP 3.2에서는 배포 후에 스토리지 구성 설정을 수정할 수 없습니다. 또한 전체 클러스터에 대한 `ReadWriteOnce` 액세스 모드만 지원됩니다.

> [!WARNING]
> 테스트 환경에서는 영구적 스토리지 없이 실행할 수 있지만 클러스터 작동이 중단될 수 있습니다. Pod를 다시 시작하면 클러스터 메타데이터 및/또는 사용자 데이터가 영구적으로 손실됩니다. 이 구성으로 실행하지 않는 것이 좋습니다. 

[스토리지 구성](#config-samples) 섹션에서는 SQL Server 빅 데이터 클러스터 배포의 스토리지 설정을 구성하는 방법에 대한 추가 예제를 제공합니다.

## <a name="aks-storage-classes"></a>AKS 스토리지 클래스

AKS에는 [두 가지 기본 제공 스토리지 클래스](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv)인 **default** 및 **managed-premium**과 동적 프로비저닝 프로그램이 포함되어 있습니다. 두 클래스 중 하나를 지정하거나, 영구적 스토리지를 사용하는 빅 데이터 클러스터를 배포하기 위해 고유한 스토리지 클래스를 만들 수 있습니다. 기본적으로 aks *aks-dev-test*의 기본 제공 클러스터 구성 파일에는 **default** 스토리지 클래스를 사용하는 영구적 스토리지 구성이 있습니다.

> [!WARNING]
> 기본 제공 스토리지 클래스인 **default** 및 **managed-premium**을 사용하여 만든 영구적 볼륨에는 ‘삭제’ 회수 정책이 지정됩니다. 따라서 SQL Server 빅 데이터 클러스터를 삭제할 때 영구적 볼륨 클레임이 삭제된 다음, 영구적 볼륨도 삭제됩니다. [이](https://docs.microsoft.com/azure/aks/concepts-storage#storage-classes) 문서에 표시된 대로 ‘유지’ 회수 정책으로 **azure-disk** 프로비저닝 프로그램을 사용하여 사용자 지정 스토리지 클래스를 만들 수 있습니다.


## <a name="minikube-storage-class"></a>minikube 스토리지 클래스

minikube에는 **standard**라는 기본 제공 스토리지 클래스와 동적 프로비저닝 프로그램이 포함되어 있습니다. minikube *minikube-dev-test*의 기본 제공 구성 파일에는 제어 평면 사양의 스토리지 구성 설정이 있습니다. 모든 풀 사양에 동일한 설정이 적용됩니다. 이 파일의 복사본을 사용자 지정하고 minikube의 빅 데이터 클러스터 배포에 사용할 수도 있습니다. 사용자 지정 파일을 수동으로 편집하고 실행하려는 워크로드에 맞게 특정 풀의 영구적 볼륨 클레임 크기를 변경할 수 있습니다. 또는 *azdata* 명령을 사용하여 편집하는 방법의 예제를 보려면 [스토리지 구성](#config-samples) 섹션을 참조하세요.

## <a name="kubeadm-storage-classes"></a>kubeadm 스토리지 클래스

kubeadm에는 기본 제공 스토리지 클래스가 없습니다. 로컬 스토리지 또는 원하는 프로비저닝 프로그램(예: [Rook](https://github.com/rook/rook))을 사용하여 고유한 스토리지 클래스와 영구적 볼륨을 만들어야 합니다. 이 경우 **className**을 구성한 스토리지 클래스로 설정합니다. 

> [!NOTE]
>  *kubeadm kubeadm-dev-test*의 기본 제공 배포 구성 파일에는 데이터 및 로그 스토리지에 대해 지정된 스토리지 클래스 이름이 없습니다. 배포 전에 구성 파일을 사용자 지정하고 className의 값을 설정해야 합니다. 설정하지 않으면 배포 전 유효성 검사에 실패합니다. 또한 배포에는 스토리지 클래스의 현재 상태를 확인하는 유효성 검사 단계가 있지만 필요한 영구적 볼륨을 검사하는 단계는 없습니다. 클러스터 규모에 따라 충분한 볼륨을 만들어야 합니다. CTP 3.1에서는 기본 클러스터 크기에 대해 최소 23개의 볼륨을 만들어야 합니다. 로컬 프로비저닝 프로그램을 사용하여 영구적 볼륨을 만드는 방법의 예제는 [여기](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)를 참조하세요.


## <a name="customize-storage-configurations-for-each-pool"></a>각 풀의 스토리지 구성 사용자 지정

사용자 지정을 수행하는 경우 항상, 사용하려는 기본 제공 구성 파일의 복사본을 먼저 만들어야 합니다. 예를 들어 다음 명령은 `custom`이라는 하위 디렉터리에 *aks-dev-test* 배포 구성 파일의 복사본을 만듭니다.

```bash
azdata bdc config init --source aks-dev-test --target custom
```

이렇게 하면 파일을 수동으로 편집 하거나 **azdata bdc config** 명령을 사용 하 여 사용자 지정할 수 있는 두 개의 파일, 즉, 두 파일을 만듭니다. jsonpath 및 jsonpatch 라이브러리의 조합을 사용하여 구성 파일을 편집하는 방법을 제공할 수 있습니다.


### <a id="config-samples"></a> 스토리지 클래스 이름 및/또는 클레임 크기 구성

기본적으로 클러스터에 프로비저닝된 각 Pod에 대해 프로비저닝되는 영구적 볼륨 클레임 크기는 10GB입니다. 클러스터를 배포하기 전에 사용자 지정 구성 파일에서 실행 중인 워크로드에 맞게 이 값을 업데이트할 수 있습니다.

다음 예제에서는 **control.jsaon**의 영구적 볼륨 클레임 크기를 32Gi로 업데이트합니다. 풀 수준에서 재정의하지 않을 경우, 이 설정은 모든 풀에 적용됩니다.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

다음 예제에서는 **control.json** 파일의 스토리지 클래스를 수정하는 방법을 보여 줍니다.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

또 다른 옵션은 스토리지 풀의 스토리지 클래스를 변경하는 다음 예제와 같이 json 패치를 사용하거나 사용자 지정 구성 파일을 수동으로 편집하는 것입니다. 다음 콘텐츠를 사용하여 *patch.json* 파일을 만듭니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.resources.storage-0.spec",
      "value": {
        "type":"Storage",
        "replicas":2,
        "storage":{
            "data":{
                    "size": "100Gi",
                    "className": "myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    },
            "logs":{
                    "size":"32Gi",
                    "className":"myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    }
                }
            }
        }
    ]
}
```

패치 파일을 적용합니다. **azdata bdc config patch** 명령을 사용하여 JSON 패치 파일의 변경 내용을 적용합니다. 다음 예제에서는 patch.json 파일을 대상 배포 구성 파일 custom.json에 적용합니다.

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>다음 단계

Kubernetes 볼륨에 대한 전체 설명서는 [볼륨에 대한 Kubernetes 설명서](https://kubernetes.io/docs/concepts/storage/volumes/)를 참조하세요.

SQL Server 빅 데이터 클러스터를 배포하는 방법에 대한 자세한 내용은 [Kubernetes에 SQL Server 빅 데이터 클러스터를 배포하는 방법](deployment-guidance.md)을 참조하세요.

