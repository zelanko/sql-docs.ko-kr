---
title: Kubernetes에 데이터 지 속성
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터에서 데이터 지 속성의 작동 방식에 대해 알아봅니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 24c90bfb8c99178e8ffa7822fba4bea709c536e1
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800720"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Kubernetes에서 SQL Server 빅 데이터 클러스터를 사용 하 여 데이터 지 속성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[영구적 볼륨](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) 저장소 Kubernetes에 대 한 플러그 인 모델을 제공 합니다. 저장소를 제공 하는 방법을 사용 되는 방법에서 추상화 됩니다. 따라서 고유한 항상 사용 가능한 저장소를 가져올 수 있으며 SQL Server 빅 데이터 클러스터에 연결할 수 있습니다. 저장소, 가용성 및 성능이 필요한 유형의 전체 제어할 수 있습니다. Kubernetes는 다양 한 Azure 디스크/파일, NFS, 로컬 저장소 등을 포함 한 저장소 솔루션을 지원 합니다.

## <a name="configure-persistent-volumes"></a>영구적 볼륨 구성

SQL Server 빅 데이터 클러스터를 이러한 영구 볼륨을 사용 하는 방법은 사용 하 여 것 [저장소 클래스](https://kubernetes.io/docs/concepts/storage/storage-classes/)합니다. 다른 종류의 저장소에 대 한 다양 한 저장소 클래스를 만들고 빅 데이터 클러스터 배포 시에 지정할 수 있습니다. 저장소 클래스 및 풀 수준에서 어떤 용도로 사용 하 여 영구적 볼륨 클레임 크기를 구성할 수 있습니다. SQL Server 빅 데이터 클러스터를 만듭니다 [영구적 볼륨 클레임](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) 영구적 볼륨에 필요한 각 구성 요소에 대해 지정 된 저장소 클래스 이름입니다. 그런 다음 pod에 해당 영구 볼륨을 탑재합니다. 

## <a name="configure-big-data-cluster-storage-settings"></a>빅 데이터 클러스터 저장소 설정 구성

비슷하게 기타 사용자 지정 설정을 지정할 수 있습니다 저장소 클러스터 구성 파일에서 각 풀 및 제어 평면에 대 한 배포 시. 풀 사양에 저장소 구성 설정은 없습니다, 제어 평면 저장소 설정이 사용 됩니다. 다음은 사양에 포함할 수 있는 저장소 구성 섹션의 샘플입니다.

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

빅 데이터 클러스터의 배포는 데이터, 메타 데이터 및 다양 한 구성 요소에 대 한 로그를 저장할 영구 저장소를 사용 합니다. 배포의 일부로 만들어진 영구적 볼륨 클레임의 크기를 사용자 지정할 수 있습니다. 저장소 클래스를 사용 하도록 권장 모범 사례로 *보존* [회수 정책](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)합니다.

> [!NOTE]
> CTP 3.0에서는 저장소 배포 후 구성 설정을 수정할 수 없습니다. 또한만 `ReadWriteOnce` 전체 클러스터에 대 한 액세스 모드가 지원 됩니다.

> [!WARNING]
> 영구 저장소 없이 실행 된 테스트 환경에서 작업할 수 있지만 작동 하지 않는 클러스터 될 수 있습니다. Pod 다시 시작 하면 시 클러스터 메타 데이터 및/또는 사용자 데이터가 손실 됩니다 영구적으로 합니다. 이 구성에서 실행 하지 않는 것이 좋습니다. 

[저장소 구성](#config-samples) 섹션에서는 SQL Server 빅 데이터 클러스터 배포에 대 한 저장소 설정을 구성 하는 방법에 더 많은 예제를 제공 합니다.

## <a name="aks-storage-classes"></a>AKS 저장소 클래스

AKS가 함께 [두 개의 기본 제공 저장소 클래스](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **기본** 하 고 **관리 되는 프리미엄** 에 동적 프로 비 저 너와 함께 합니다. 그 중 하나를 지정할 수도 있고 사용 하도록 설정 하는 영구 저장소를 사용 하 여 빅 데이터 클러스터를 배포 하는 것에 대 한 사용자 고유의 저장소 클래스를 만들 수 있습니다. 기본적으로 기본 제공 aks 클러스터 구성 파일에 *aks-dev-test.json* 사용 하는 영구 저장소 구성에 수반 **기본** 저장소 클래스입니다.

> [!WARNING]
> 기본 제공 저장소 클래스를 사용 하 여 만든 영구적 볼륨 **기본** 하 고 **관리 되는 premium** 재요청 정책이 *삭제*합니다. 시 있습니다 SQL Server 빅 데이터 클러스터를 삭제 하므로 영구적 볼륨 클레임도 삭제 하 고 다음 영구 볼륨을 가져옵니다. 사용 하 여 사용자 지정 저장소 클래스를 만들 수 있습니다 **azure 디스크** 사용 하 여 privioner를 *보존* 에 표시 된 대로 정책을 회수 [이](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes) 문서.


## <a name="minikube-storage-class"></a>Minikube 저장소 클래스

Minikube 라는 기본 제공 저장소 클래스를 함께 **표준** 는 대 한 동적 프로 비 저 너와 함께 합니다. Minikube에 대 한 기본 제공된 구성 파일 *minikube-dev-test.json* 제어 평면 사양에서 저장소 구성 설정을 포함 합니다. 동일한 설정은 모든 풀 사양에 적용 됩니다. 또한이 파일의 복사본을 사용자 지정 하 고 minikube의 빅 데이터 클러스터 배포에 사용할 수 있습니다. 수동으로 사용자 지정 파일을 편집 하 고 실행 하려는 워크 로드를 수용 하기 위해 특정 풀에 대 한 영구적 볼륨 클레임의 크기를 변경할 수 있습니다. 또는 참조 하세요 [저장소 구성](#config-samples) 수행 하는 방법에 대 한 예제 섹션을 사용 하 여 편집 *mssqlctl* 명령입니다.

## <a name="kubeadm-storage-classes"></a>Kubeadm 저장소 클래스

기본 제공 저장소 클래스를 사용 하 여 Kubeadm 제공 되지 않습니다. 사용자 고유의 저장소 클래스와 같은 로컬 저장소 또는 기본 프로 비 저 너 프로그램을 사용 하 여 영구 볼륨을 만들어야 [루크](https://github.com/rook/rook)합니다. 설정한 경우에 **className** 구성한 저장소 클래스입니다. 

> [!NOTE]
>  기본 제공에 대 한 배포 구성 파일에서 *kubeadm kubeadm-dev-test.json* 데이터 및 로그 저장소에 대해 지정 된 저장소 클래스 이름이 없습니다. 배포 하기 전에 구성 파일을 사용자 지정 하 고 className 그렇지 않은 경우 배포 전 유효성 검사 실패에 대 한 값을 설정 해야 합니다. 배포에 필요한 영구적 볼륨 아니라 저장소 클래스의 존재 여부를 확인 하는 유효성 검사 단계가 있습니다. 클러스터의 규모에 따라 충분 한 볼륨을 만들 수 있어야 합니다. CTP 3.0에서는 기본 클러스터 크기에 대 한 만들어야 이상 23 볼륨. [여기](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) 은 로컬 프로 비 저 너를 사용 하 여 영구 볼륨을 만드는 방법의 예입니다.


## <a name="customize-storage-configurations-for-each-pool"></a>각 풀에 대 한 저장소 구성을 사용자 지정

모든 사용자 지정의 경우 먼저 만들어야 기본 제공의 복사본을 사용 하려면 구성 파일에 있습니다. 예를 들어 다음 명령은의 복사본을 만듭니다는 *aks-dev-test.json* 현재 디렉터리에 배포 구성 파일:

```bash
mssqlctl cluster config init --src aks-dev-test.json --target custom.json
```

그런 다음 사용자 지정할 수 있습니다 구성 파일을 수동으로 편집 하 여 하나 또는 사용할 수 있습니다 *mssqlctl 클러스터 구성 섹션 집합* 명령입니다. 이 집합 명령은 jsonpath 및 jsonpatch 라이브러리의 조합을 사용 하 여 구성 파일을 편집 하는 방법을 제공 합니다.

### <a name="configure-size"></a>크기를 구성 합니다.

기본적으로 각 클러스터에 프로 비전 된 pod에 대 한 프로 비전 된 영구적 볼륨 클레임의 크기는 10GB입니다. 클러스터를 배포 하기 전에 사용자 지정 구성 파일에서 실행 중인 워크 로드를 수용 하기 위해이 값을 업데이트할 수 있습니다.

다음 예제에서는 100 Gi 저장소 풀에 저장 된 데이터에 대 한 영구적 볼륨 클레임의 크기를 업데이트 합니다. 이 명령을 실행 하기 전에 저장소 섹션 저장소 풀에 대 한 구성 파일에 존재 해야 note:

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.size=100Gi"
```

다음 예제에서는 32 Gi에 모든 풀에 대 한 영구적 볼륨 클레임의 크기를 업데이트합니다.

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.storage.data.size=32Gi"
```

### <a id="config-samples"></a> 저장소 클래스를 구성 합니다.

다음 예제에는 제어 평면에 대 한 저장소 클래스를 수정 하는 방법을 보여 줍니다.

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.storage.data.className=<yourStorageClassName>"
```

사용자 지정 구성 파일을 수동으로 편집 하거나 저장소 풀에 대 한 저장소 클래스를 변경 하는 다음 예와 같은 jsonpatch를 사용 하는 방법도 있습니다. 만들기는 *patch.json* 이 콘텐츠로 파일:

```json
{
  "patch": [
    {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage",
      "value": {
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

패치 파일을 적용 합니다. 사용 하 여 *mssqlctl 클러스터 구성 섹션 집합* JSON 패치 파일에 변경 내용을 적용 하려면 명령입니다. 다음 예제에서는 대상 배포 구성 파일 custom.json patch.json 파일을 적용 합니다.

```bash
mssqlctl cluster config section set -c custom.json -p ./patch.json
```

## <a name="next-steps"></a>다음 단계

Kubernetes에서 볼륨에 대 한 전체 설명서를 참조 하세요. 합니다 [볼륨에 대 한 Kubernetes 설명서](https://kubernetes.io/docs/concepts/storage/volumes/)합니다.

SQL Server 빅 데이터 클러스터를 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [빅 데이터에서 kubernetes 클러스터는 SQL Server를 배포 하는 방법을](deployment-guidance.md)합니다.

