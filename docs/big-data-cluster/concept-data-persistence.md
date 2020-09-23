---
title: Kubernetes의 데이터 지속성
titleSuffix: SQL Server big data clusters
description: Kubernetes에서 영구 볼륨이 스토리지에 대한 플러그 인 모델을 제공하는 방법을 알아봅니다. 또한 SQL Server 2019 빅 데이터 클러스터에서 데이터 지속성이 작동하는 방식도 알아봅니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 970b049ec7933af9fab1d213d7441f101e01f7c1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88765692"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-in-kubernetes"></a>Kubernetes에서 SQL Server 빅 데이터 클러스터를 사용한 데이터 지속성

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

[영구적 볼륨](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)은 Kubernetes의 스토리지에 대한 플러그 인 모델을 제공합니다. 이 모델에서 스토리지를 제공하는 방법은 사용 방식으로부터 추상화됩니다. 따라서 고유한 고가용성 스토리지를 가져와 SQL Server 빅 데이터 클러스터에 연결할 수 있습니다. 이를 통해 필요한 스토리지 유형, 가용성 및 성능을 완벽하게 제어할 수 있습니다. Kubernetes는 Azure 디스크 및 파일, NFS(네트워크 파일 시스템) 및 로컬 저장소를 비롯한 [다양한 종류의 스토리지 솔루션](https://kubernetes.io/docs/concepts/storage/storage-classes/#provisioner)을 지원합니다.

## <a name="configure-persistent-volumes"></a>영구적 볼륨 구성

SQL Server 빅 데이터 클러스터는 [스토리지 클래스](https://kubernetes.io/docs/concepts/storage/storage-classes/)를 통해 이러한 영구적 볼륨을 사용합니다. 스토리지 종류에 따라 다양한 스토리지 클래스를 만들고 빅 데이터 클러스터를 배포할 때 지정할 수 있습니다. 풀 수준에서 특정 용도로 사용할 스토리지 클래스와 영구적 볼륨 클레임 크기를 구성할 수 있습니다. SQL Server 빅 데이터 클러스터는 영구적 볼륨이 필요한 각 구성 요소에 대해 지정된 스토리지 클래스 이름을 사용하여 [영구적 볼륨 클레임](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)을 만듭니다. 그런 다음, Pod에 해당하는 영구적 볼륨(또는 볼륨)을 탑재합니다. 

빅 데이터 클러스터의 스토리지 구성을 계획할 때 다음과 같은 중요한 사항을 고려해야 합니다.

- 빅 데이터 클러스터를 성공적으로 배포하려면 사용 가능한 영구적 볼륨을 필요한 만큼 확보해야 합니다. AKS(Azure Kubernetes Service) 클러스터에 배포하는 경우 기본 제공 스토리지 클래스(`default` 또는 `managed-premium`)를 사용하는 경우 이 클래스는 영구적 볼륨에 대한 동적 프로비저닝을 지원합니다. 따라서 영구적 볼륨을 미리 만들 필요가 없지만 AKS 클러스터에서 사용할 수 있는 작업자 노드가 배포에 필요한 영구적 볼륨 수 만큼의 디스크를 연결할 수 있는지 확인해야 합니다. 작업자 노드에 지정된 [VM 크기](/azure/virtual-machines/linux/sizes)에 따라 각 노드에서 특정 개수의 디스크를 연결할 수 있습니다. 기본 크기 클러스터(고가용성 없음)의 경우 최소 24개의 디스크가 필요합니다. 고가용성을 설정하거나 풀을 확장하는 경우 확장하는 리소스에 관계 없이 각 추가 복제본당 두 개 이상의 영구적 볼륨이 있어야 합니다.

- 구성에서 제공하려는 스토리지 클래스의 스토리지 프로비저닝 프로그램이 동적 프로비저닝을 지원하지 않는 경우 영구적 볼륨을 미리 만들어야 합니다. 예를 들어 `local-storage` 프로비저닝 프로그램은 동적 프로비저닝을 지원하지 않습니다. `kubeadm`을 사용하여 배포된 Kubernetes 클러스터에서 진행하는 방법에 대한 지침은 이 [샘플 스크립트](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)를 참조하세요.

- 빅 데이터 클러스터를 배포할 때 클러스터의 모든 구성 요소에서 동일한 스토리지 클래스를 사용하도록 구성할 수 있습니다. 하지만 프로덕션 배포의 모범 사례에 따라, 다양한 구성 요소에는 크기 또는 처리량의 측면에서 다양한 워크로드를 수용할 수 있는 다양한 스토리지 구성이 필요합니다. 각 SQL Server 마스터 인스턴스, 데이터 세트 및 스토리지 풀의 컨트롤러에 지정된 기본 스토리지 구성을 덮어쓸 수 있습니다. 이 문서에서는 이 작업을 수행하는 방법을 보여 줍니다.

- 스토리지 풀 크기 조정 요구 사항을 계산할 때는 HDFS가 어떤 복제 계수로 구성되었는지를 고려해야 합니다.  복제 계수는 클러스터 배포 구성 파일에서 배포 시점에 구성할 수 있습니다. 개발-테스트 프로필(`aks-dev-test` 또는 `kubeadm-dev-test`)의 기본값은 2이고, 프로덕션 배포용으로 권장되는 프로필(`kubeadm-prod`)의 기본값은 3입니다. 가장 좋은 방법은 빅 데이터 클러스터의 프로덕션 배포를 3 이상의 HDFS용 복제 계수로 구성하는 것입니다. 복제 계수의 값은 스토리지 풀에 있는 인스턴스의 개수에 영향을 줍니다. 따라서 적어도 복제 계수의 값보다 크거나 같은 스토리지 풀 인스턴스를 배포해야 합니다. 이에 더해, HDFS에서 복제 계수 값의 배수만큼 복제되는 데이터를 고려하여 스토리지의 크기를 정해야 합니다. HDFS에서의 데이터 복제에 대한 자세한 내용은 [여기](https://hadoop.apache.org/docs/r3.2.1/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Data_Replication)에서 확인할 수 있습니다. 

- SQL Server 2019 CU1 릴리스부터는 배포 후에 스토리지 구성 설정을 수정할 수 없습니다. 이 제약 조건 때문에 각 인스턴스에 대한 영구적 볼륨 클레임의 크기를 수정할 수도 없고 배포 후 크기 조정 작업도 수행할 수 없습니다. 따라서 빅 데이터 클러스터를 배포하기 전에 스토리지 레이아웃을 계획하는 것이 중요합니다.

- Kubernetes에 컨테이너화된 애플리케이션으로 배포하고 상태 저장 세트 및 영구적 스토리지와 같은 기능을 사용하여 Kubernetes는 상태 문제가 발생하면 Pod를 다시 시작하여 동일한 영구적 스토리지에 연결합니다. 그러나 노드 오류가 발생하여 Pod를 다른 노드에서 다시 시작해야 하는 경우에는 스토리지가 실패한 노드에 로컬이면 서비스를 사용할 수 없게 될 위험이 증가합니다. 이 위험을 완화하려면 추가 중복성을 구성하고 [고가용성 기능](deployment-high-availability.md)을 사용하도록 설정하거나 원격 중복 스토리지를 사용해야 합니다. 다음은 빅 데이터 클러스터의 다양한 구성 요소에 대한 스토리지 옵션의 개요입니다.

| 리소스 | 데이터의 스토리지 유형 | 로그의 스토리지 유형 |  참고 |
|---|---|---|--|
| SQL Server 마스터 인스턴스 | 로컬(복제본>=3) 또는 원격 중복 스토리지(복제본=1) | 로컬 스토리지 | Pod가 노드에 유지되는 상태 저장 세트 기반 구현은 다시 시작 및 일시적인 오류로 인해 데이터가 손상되지 않도록 보장합니다. |
| 풀 컴퓨팅 | 로컬 스토리지 | 로컬 스토리지 | 사용자 데이터가 저장되지 않았습니다. |
| 데이터 풀 | 로컬/원격 중복 스토리지 | 로컬 스토리지 | 다른 데이터 원본에서 데이터 풀을 다시 빌드할 수 없는 경우 원격 중복 스토리지를 사용합니다.  |
| 스토리지 풀(HDFS) | 로컬/원격 중복 스토리지 | 로컬 스토리지 | HDFS 복제가 사용됩니다. |
| Spark 풀 | 로컬 스토리지 | 로컬 스토리지 | 사용자 데이터가 저장되지 않았습니다. |
| 컨트롤(controldb, metricsdb, logsdb)| 원격 중복 스토리지 | 로컬 스토리지 | 빅 데이터 클러스터 메타데이터에 스토리지 수준 중복성을 사용하는 것이 중요합니다. |

> [!IMPORTANT]
> 컨트롤 관련 구성 요소가 원격 중복 스토리지 디바이스에 있는지 확인합니다. `controldb-0` Pod는 클러스터 서비스 상태, 다양한 설정 및 기타 관련 정보와 관련된 모든 메타데이터를 저장하는 데이터베이스를 사용하여 SQL Server 인스턴스를 호스팅합니다. 이 인스턴스를 사용할 수 없게 되면 클러스터의 다른 종속 서비스에서 상태 문제가 발생합니다.

## <a name="configure-big-data-cluster-storage-settings"></a>빅 데이터 클러스터 스토리지 설정 구성

다른 사용자 지정과 같이, 배포 시 `bdc.json` 구성 파일의 각 풀과 `control.json` 파일의 컨트롤 서비스에 맞게 클러스터 구성 파일의 스토리지 설정을 지정할 수 있습니다. 풀 사양에 스토리지 구성 설정이 없는 경우 SQL Server 마스터(`master` 리소스), HDFS(`storage-0` 리소스), 데이터 풀을 비롯한 다른 모든 구성 요소에 컨트롤 스토리지 설정이 사용됩니다. 다음 코드 샘플은 사양에 포함할 수 있는 스토리지 구성 섹션을 나타냅니다.

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

빅 데이터 클러스터 배포는 영구적 스토리지를 사용하여 다양한 구성 요소의 데이터, 메타데이터 및 로그를 저장합니다. 배포 과정에서 생성되는 영구적 볼륨 클레임의 크기를 사용자 지정할 수 있습니다. 모범 사례에 따라 *유지* [회수 정책](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)으로 스토리지 클래스를 사용하는 것이 좋습니다.

> [!WARNING]
> 테스트 환경에서는 영구적 스토리지 없이 실행할 수 있지만 클러스터 작동이 중단될 수 있습니다. Pod가 다시 시작하면 클러스터 메타데이터 및/또는 사용자 데이터가 영구적으로 손실됩니다. 이 구성으로는 실행하지 않는 것이 좋습니다.

[스토리지 구성](#config-samples) 섹션에서는 SQL Server 빅 데이터 클러스터 배포의 스토리지 설정을 구성하는 방법에 대한 추가 예제를 제공합니다.

## <a name="aks-storage-classes"></a>AKS 스토리지 클래스

AKS는 [두 가지 기본 제공 스토리지 클래스](/azure/aks/azure-disks-dynamic-pv/)인 `default` 및 `managed-premium`과 해당 동적 프로비저닝 프로그램이 함께 제공됩니다. 두 클래스 중 하나를 지정하거나 고유한 스토리지 클래스를 만들어 영구적 스토리지를 사용하는 빅 데이터 클러스터를 배포할 수 있습니다. 기본적으로 AKS(`aks-dev-test`)의 기본 제공 클러스터 구성 파일에는 `default` 스토리지 클래스를 사용하는 영구적 스토리지 구성이 있습니다.

> [!WARNING]
> 기본 제공 스토리지 클래스인 `default` 및 `managed-premium`을 사용하여 만든 영구적 볼륨에는 *삭제* 회수 정책이 있습니다. 따라서 빅 데이터 클러스터 SQL Server를 삭제하는 경우 영구적 볼륨과 마찬가지로 영구적 볼륨 클레임이 삭제됩니다. [스토리지 개념](/azure/aks/concepts-storage/#storage-classes)에 설명된 대로 `Retain` 회수 정책으로 `azure-disk` 프로비저닝 프로그램을 사용하여 사용자 지정 스토리지 클래스를 만들 수 있습니다.

## <a name="storage-classes-for-kubeadm-clusters"></a>`kubeadm` 클러스터의 스토리지 클래스 

`kubeadm`을 사용하여 배포된 Kubernetes 클러스터에는 기본 제공 스토리지 클래스가 없습니다. 로컬 스토리지 또는 [선호하는 프로비저닝 프로그램](https://kubernetes.io/docs/concepts/storage/storage-classes/#provisioner)을 사용하여 고유한 스토리지 클래스와 영구적 볼륨을 만들어야 합니다. 이 경우 `className`을 구성한 스토리지 클래스로 설정합니다.

> [!IMPORTANT]
>  kubeadm의 기본 제공 배포 구성 파일(`kubeadm-dev-test` 및 `kubeadm-prod`)에는 데이터 및 로그 스토리지에 대해 지정된 스토리지 클래스 이름이 없습니다. 배포하기 전에 구성 파일을 사용자 지정하고 `className`에 대한 값을 설정해야 합니다. 그렇지 않으면 배포 전 유효성 검사가 실패합니다. 또한 배포에는 스토리지 클래스의 현재 상태를 확인하는 유효성 검사 단계가 있지만 필요한 영구적 볼륨을 검사하는 단계는 없습니다. 클러스터 규모에 따라 충분한 볼륨을 만들어야 합니다. 기본 최소 클러스터 크기(기본 규모, 고가용성 없음)의 경우 최소 24개의 영구적 볼륨을 만들어야 합니다. 로컬 프로비저닝 프로그램을 사용하여 영구적 볼륨을 만드는 방법에 대한 예제는 [Kubeadm을 사용하여 Kubernetes 클러스터 만들기](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)를 참조하세요.

## <a name="customize-storage-configurations-for-each-pool"></a>각 풀의 스토리지 구성 사용자 지정

사용자 지정을 수행하는 경우 항상, 사용하려는 기본 제공 구성 파일의 복사본을 먼저 만들어야 합니다. 예를 들어 다음 명령은 하위 디렉터리 `custom`에 `aks-dev-test` 배포 구성 파일의 복사본을 만듭니다.

```bash
azdata bdc config init --source aks-dev-test --target custom
```

이 프로세스에서 두 개의 파일, 즉 `bdc.json` 및 `control.json`이 만들어집니다. 이들 파일은 수동으로 편집하거나 `azdata bdc config` 명령을 사용하여 사용자 지정할 수 있습니다. jsonpath 및 jsonpatch 라이브러리의 조합을 사용하여 구성 파일을 편집하는 방법을 제공할 수 있습니다.


### <a name="configure-storage-class-name-andor-claims-size"></a><a id="config-samples"></a> 스토리지 클래스 이름 및/또는 클레임 크기 구성

기본적으로 클러스터에 프로비저닝된 각 Pod에 대해 프로비저닝되는 영구적 볼륨 클레임 크기는 10GB입니다. 클러스터를 배포하기 전에 사용자 지정 구성 파일에서 실행 중인 워크로드에 맞게 이 값을 업데이트할 수 있습니다.

다음 예제에서는 `control.json`에서 영구적 볼륨 클레임의 크기가 32GB로 업데이트됩니다. 풀 수준에서 재정의하지 않을 경우, 이 설정은 모든 풀에 적용됩니다.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

다음 예제에서는 `control.json` 파일의 스토리지 클래스를 수정하는 방법을 보여 줍니다.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

또한 다음 예제와 같이 사용자 지정 구성 파일을 수동으로 편집하거나 스토리지 풀의 스토리지 클래스를 변경하는 json 패치를 사용할 수도 있습니다.

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

패치 파일을 적용합니다. `azdata bdc config patch` 명령을 사용하여 .json 패치 파일의 변경 내용을 적용합니다. 다음 예제에서는 `patch.json` 파일을 대상 배포 구성 파일 `custom.json`에 적용합니다.

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>다음 단계

- Kubernetes 볼륨에 대한 전체 설명은 [볼륨에 대한 Kubernetes 설명서](https://kubernetes.io/docs/concepts/storage/volumes/)를 참조하세요.

- SQL Server 빅 데이터 클러스터를 배포하는 방법에 대한 자세한 내용은 [Kubernetes에 SQL Server 빅 데이터 클러스터를 배포하는 방법](deployment-guidance.md)을 참조하세요.