---
title: Kubernetes의 데이터 지 속성
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터에서 데이터 지 속성이 작동 하는 방식에 대해 알아봅니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9142836032acc5e302c947e1619d17b07faff683
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419464"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Kubernetes의 SQL Server 빅 데이터 클러스터를 사용 하는 데이터 지 속성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[영구적 볼륨](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) 은 Kubernetes의 저장소에 대 한 플러그 인 모델을 제공 합니다. 저장소를 제공 하는 방법은 사용 방법에서 추상화 됩니다. 따라서 사용자 고유의 항상 사용 가능한 저장소를 가져와서 SQL Server 빅 데이터 클러스터에 연결할 수 있습니다. 이를 통해 필요한 저장소, 가용성 및 성능 유형을 완벽 하 게 제어할 수 있습니다. Kubernetes는 Azure 디스크/파일, NFS, 로컬 저장소 등을 비롯 한 다양 한 종류의 저장소 솔루션을 지원 합니다.

## <a name="configure-persistent-volumes"></a>영구적 볼륨 구성

SQL Server 빅 데이터 클러스터가 이러한 영구 볼륨을 소비 하는 방식은 [저장소 클래스](https://kubernetes.io/docs/concepts/storage/storage-classes/)를 사용 하는 것입니다. 저장소 종류에 따라 다양 한 저장소 클래스를 만들고 빅 데이터 클러스터 배포 시간에 지정할 수 있습니다. 풀 수준의 용도에 사용할 저장소 클래스와 영구 볼륨 클레임 크기를 구성할 수 있습니다. SQL Server 빅 데이터 클러스터는 영구 볼륨을 필요로 하는 각 구성 요소에 대해 지정 된 저장소 클래스 이름을 사용 하 여 [영구 볼륨 클레임](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) 을 만듭니다. 그런 다음 pod에 해당 하는 영구 볼륨을 탑재 합니다. 

## <a name="configure-big-data-cluster-storage-settings"></a>빅 데이터 클러스터 저장소 설정 구성

다른 사용자 지정과 마찬가지로 배포 시 각 풀 및 제어 평면에 대 한 클러스터 구성 파일에서 저장소 설정을 지정할 수 있습니다. 풀 사양에 저장소 구성 설정이 없는 경우 제어 평면 저장소 설정이 사용 됩니다. 다음은 사양에 포함할 수 있는 저장소 구성 섹션의 샘플입니다.

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

빅 데이터 클러스터의 배포는 영구 저장소를 사용 하 여 다양 한 구성 요소에 대 한 데이터, 메타 데이터 및 로그를 저장 합니다. 배포의 일부로 생성 된 영구적 볼륨 클레임의 크기를 사용자 지정할 수 있습니다. 모범 사례에 따라 [회수 정책](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy) *유지* 와 함께 저장소 클래스를 사용 하는 것이 좋습니다.

> [!NOTE]
> CTP 3.2에서는 배포 후 저장소 구성 설정을 수정할 수 없습니다. 또한 전체 클러스터에 대 한 액세스모드만지원됩니다.`ReadWriteOnce`

> [!WARNING]
> 영구 저장소 없이 실행은 테스트 환경에서 작동할 수 있지만 작동 하지 않는 클러스터가 될 수 있습니다. Pod가 다시 시작 되 면 클러스터 메타 데이터 및/또는 사용자 데이터가 영구적으로 손실 됩니다. 이 구성에서는를 실행 하지 않는 것이 좋습니다. 

[저장소 구성](#config-samples) 섹션에서는 SQL Server 빅 데이터 클러스터 배포에 대 한 저장소 설정을 구성 하는 방법에 대 한 추가 예제를 제공 합니다.

## <a name="aks-storage-classes"></a>AKS 저장소 클래스

AKS에는 [두 가지 기본 제공 저장소 클래스](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **기본** 및 **관리 되는 premium** 과 함께 동적 provisioner 함께 제공 됩니다. 이러한 방법 중 하나를 지정 하거나 영구 저장소를 사용 하는 빅 데이터 클러스터를 배포 하기 위한 고유한 저장소 클래스를 만들 수 있습니다. 기본적으로 aks *aks* 에 대 한 기본 제공 클러스터 구성 파일은 **기본** 저장소 클래스를 사용 하는 영구 저장소 구성과 함께 제공 됩니다.

> [!WARNING]
> **기본** 제공 저장소 클래스를 사용 하 여 만든 영구 볼륨 및 **관리 되는 프리미엄** 에는 *삭제*의 회수 정책이 있습니다. 따라서 빅 데이터 클러스터 SQL Server를 삭제 하는 시점에서 영구적 볼륨 클레임이 삭제 되 고 영구적 볼륨도 삭제 됩니다. [이](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes) 문서에 표시 된 대로 회수 정책 *유지* 와 함께 **azure-disk** privioner를 사용 하 여 사용자 지정 저장소 클래스를 만들 수 있습니다.


## <a name="minikube-storage-class"></a>Minikube 저장소 클래스

Minikube에는 **standard** 라는 기본 제공 저장소 클래스와 함께 dynamic provisioner가 제공 됩니다. Minikube *minikube* 의 기본 제공 구성 파일에는 제어 평면 사양의 저장소 구성 설정이 있습니다. 동일한 설정이 모든 풀 사양에 적용 됩니다. 이 파일의 복사본을 사용자 지정 하 고 minikube의 빅 데이터 클러스터 배포에 사용할 수도 있습니다. 사용자 지정 파일을 수동으로 편집 하 고 실행 하려는 작업에 맞게 특정 풀의 영구적 볼륨 클레임 크기를 변경할 수 있습니다. 또는 *azdata* 명령을 사용 하 여 편집 하는 방법에 대 한 예제는 [저장소 구성](#config-samples) 섹션을 참조 하세요.

## <a name="kubeadm-storage-classes"></a>Kubeadm 저장소 클래스

Kubeadm에는 기본 제공 저장소 클래스가 제공 되지 않습니다. 로컬 저장소 또는 기본 provisioner (예: [Rook](https://github.com/rook/rook))를 사용 하 여 고유한 저장소 클래스 및 영구 볼륨을 만들어야 합니다. 이 경우 **className** 을 구성 된 저장소 클래스로 설정 합니다. 

> [!NOTE]
>  *Kubeadm kubeadm* 에 대 한 기본 제공 배포 구성 파일에는 데이터 및 로그 저장소에 대해 지정 된 저장소 클래스 이름이 없습니다. 배포 하기 전에 구성 파일을 사용자 지정 하 고 클래스 이름에 대 한 값을 설정 해야 합니다. 그렇지 않으면 배포 전 유효성 검사가 실패 합니다. 배포에는 저장소 클래스의 존재 여부를 확인 하는 유효성 검사 단계도 있지만 필요한 영구적 볼륨은 없습니다. 클러스터의 크기에 따라 충분 한 볼륨을 만들어야 합니다. CTP 3.1에서 기본 클러스터 크기에 대해 최소 23 개의 볼륨을 만들어야 합니다. 로컬 provisioner를 사용 하 여 영구 볼륨을 만드는 방법에 대 한 예제는 [다음과](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) 같습니다.


## <a name="customize-storage-configurations-for-each-pool"></a>각 풀에 대 한 저장소 구성 사용자 지정

모든 사용자 지정에 대해 먼저 사용 하려는 기본 제공 구성 파일의 복사본을 만들어야 합니다. 예를 들어 다음 명령은 라는 `custom`하위 디렉터리에 *aks* 배포 구성 파일의 복사본을 만듭니다.

```bash
azdata bdc config init --source aks-dev-test --target custom
```

이렇게 하면 파일을 수동으로 편집 하거나 **azdata bdc config** 명령을 사용 하 여 사용자 지정할 수 있는 두 개의 파일 인 **cluster.exe 및** **컨트롤** 을 만듭니다. Jsonpath 및 jsonpatch 라이브러리의 조합을 사용 하 여 구성 파일을 편집 하는 방법을 제공할 수 있습니다.


### <a id="config-samples"></a>저장소 클래스 이름 및/또는 클레임 크기 구성

기본적으로 클러스터에 프로 비전 된 각 pod에 대해 프로 비전 된 영구적 볼륨 클레임의 크기는 10gb입니다. 클러스터를 배포 하기 전에 사용자 지정 구성 파일에서 실행 중인 작업을 수용할 수 있도록이 값을 업데이트할 수 있습니다.

다음 예제에서는 영구 볼륨 클레임 크기의 크기를 컨트롤의 32Gi로 업데이트 합니다 **. jsaon**. 풀 수준에서 재정의 되지 않은 경우이 설정은 모든 풀에 적용 됩니다.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

다음 예제에서는 **컨트롤의 json** 파일에 대 한 저장소 클래스를 수정 하는 방법을 보여 줍니다.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

또 다른 옵션은 저장소 풀의 저장소 클래스를 변경 하는 다음 예제와 같이 사용자 지정 구성 파일을 수동으로 편집 하거나 json 패치를 사용 하는 것입니다. 다음 콘텐츠를 사용 하 여 *패치. json* 파일을 만듭니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage"
      "value": {
          "type":"Storage",
          "replicas":2,
          "data": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
      }
  ]
}
```

패치 파일을 적용 합니다. **Azdata bdc 구성 패치** 명령을 사용 하 여 JSON 패치 파일의 변경 내용을 적용 합니다. 다음 예제에서는 사용자 지정. json 파일을 대상 배포 구성 파일에 적용 합니다.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>다음 단계

Kubernetes의 볼륨에 대 한 전체 설명서는 [볼륨에 대 한 Kubernetes 설명서](https://kubernetes.io/docs/concepts/storage/volumes/)를 참조 하세요.

SQL Server 빅 데이터 클러스터를 배포 하는 방법에 대 한 자세한 내용은 [Kubernetes에서 빅 데이터 클러스터 SQL Server 배포 하는 방법](deployment-guidance.md)을 참조 하세요.

