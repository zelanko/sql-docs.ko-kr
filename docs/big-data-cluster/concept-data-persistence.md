---
title: Kubernetes에 데이터 지 속성
titleSuffix: SQL Server 2019 big data clusters
description: SQL Server 2019 빅 데이터 클러스터에서 데이터 지 속성의 작동 방식에 대해 알아봅니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 75cf78e7c73ad61e5e28ed6f0707639899d8ec19
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207672"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Kubernetes에서 SQL Server 빅 데이터 클러스터를 사용 하 여 데이터 지 속성

[영구적 볼륨](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) 저장소 저장소가 제공 됩니다 하는 방법에 Kubernetes에 사용 되는 방법에서 추출 된 완료 된에 대 한 플러그 인 모델을 제공 합니다. 따라서 고유한 항상 사용 가능한 저장소를 가져올 수 있으며 SQL Server 빅 데이터 클러스터에 연결할 수 있습니다. 저장소, 가용성 및 성능이 필요한 유형의 전체 제어할 수 있습니다. Kubernetes는 다양 한 Azure 디스크/파일, NFS, 로컬 저장소 등을 포함 한 저장소 솔루션을 지원 합니다.

## <a name="configure-persistent-volumes"></a>영구적 볼륨 구성

SQL Server 빅 데이터 클러스터 이러한 영구 볼륨을 사용 하는 방법은 사용 하 여 것 [저장소 클래스](https://kubernetes.io/docs/concepts/storage/storage-classes/)합니다. 다른 종류의 저장소에 대 한 다양 한 저장소 클래스를 만들고 빅 데이터 클러스터 배포 시에 지정할 수 있습니다. (풀) 어떤 용도로 사용 하는 저장소 클래스를 구성할 수 있습니다. SQL Server 빅 데이터 클러스터를 만듭니다 [영구적 볼륨 클레임](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) 영구적 볼륨에 필요한 각 pod에 대 한 지정 된 저장소 클래스 이름입니다. 그런 다음 pod에 해당 영구 볼륨을 탑재합니다.

> [!NOTE]
> CTP 2.2에만 한 `ReadWriteOnce` 전체 클러스터에 대 한 액세스 모드가 지원 됩니다.

## <a name="deployment-settings"></a>배포 설정

배포 하는 동안 영구 저장소를 사용 하려면 구성 합니다 **USE_PERSISTENT_VOLUME** 하 고 **STORAGE_CLASS_NAME** 실행 하기 전에 환경 변수 `mssqlctl create cluster` 명령입니다. **USE_PERSISTENT_VOLUME** 로 설정 된 `true` 기본적으로 합니다. 기본값을 무시 하 고 설정할 수 있습니다 `false` 및 SQL Server 빅 데이터 클러스터 emptyDir 탑재를 사용 하는 예제의 경우. 

> [!WARNING]
> 영구 저장소 없이 실행 된 테스트 환경에서 작업할 수 있지만 작동 하지 않는 클러스터 될 수 있습니다. Pod 다시 시작 하면 시 클러스터 메타 데이터 및/또는 사용자 데이터가 손실 됩니다 영구적으로 합니다.

도 제공 해야 플래그를 true로 설정 하면 **STORAGE_CLASS_NAME** 배포 시 매개 변수로 합니다.

## <a name="aks-storage-classes"></a>AKS 저장소 클래스

AKS가 함께 [두 개의 기본 제공 저장소 클래스](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **기본** 하 고 **관리 되는 프리미엄** 에 동적 프로 비 저 너와 함께 합니다. 그 중 하나를 지정할 수도 있고 사용 하도록 설정 하는 영구 저장소를 사용 하 여 빅 데이터 클러스터를 배포 하는 것에 대 한 사용자 고유의 저장소 클래스를 만들 수 있습니다.

## <a name="minikube-storage-class"></a>Minikube 저장소 클래스

Minikube 라는 기본 제공 저장소 클래스를 함께 **표준** 는 대 한 동적 프로 비 저 너와 함께 합니다. 경우 minikube를에 유의 `USE_PERSISTENT_VOLUME=true` (기본값)를 재정의 해야에 대 한 기본값을 **STORAGE_CLASS_NAME** 환경 변수 기본값 다르기 때문입니다. 값을 설정 합니다 `standard`: 

Windows에서 다음 명령을 사용 합니다.

```cmd
SET STORAGE_CLASS_NAME=standard
```

Linux에서 다음 명령을 사용 합니다.

```cmd
export STORAGE_CLASS_NAME=standard
```

Minikube에서 영구적 볼륨을 사용 하 여 설정 하 여 무시할 수 또는 `USE_PERSISTENT_VOLUME=false`합니다.

## <a name="kubeadm"></a>Kubeadm

기본 제공 저장소 클래스를 사용 하 여 Kubeadm 제공 되지 않습니다. 사용자 고유의 영구적 볼륨 및 저장소 클래스와 같은 로컬 저장소 또는 기본 프로 비 저 너 프로그램을 사용 하 여 만들 수 있습니다 [루크](https://github.com/rook/rook)합니다. 설정한 경우에 **STORAGE_CLASS_NAME** 구성한 저장소 클래스입니다. 설정할 수 있습니다 `USE_PERSISTENT_VOLUME=false` 테스트 환경에서의 이전 경고를 확인 하지만 합니다 **배포 설정** 이 문서의 섹션입니다.  

## <a name="on-premises-cluster"></a>온-프레미스 클러스터

설정 해야 하므로, 온-프레미스 클러스터 물론 모든 기본 제공 저장소 클래스를 사용 하 여 제공 되지 않습니다 [영구적 볼륨](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)/[프로 비 저 너를](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/) 미리 사용 하 여 해당 SQL Server 빅 데이터 클러스터 배포 시 저장소 클래스입니다.

## <a name="customize-storage-size-for-each-pool"></a>각 풀에 대 한 저장소 크기를 사용자 지정
기본적으로 각 클러스터에 프로 비전 된 pod에 대 한 프로 비전 된 영구적 볼륨의 크기는 6GB 됩니다. 이 환경 변수를 설정 하 여 구성할 수는 `STORAGE_SIZE` 다른 값으로. 예를 들어, 아래 10GB로 실행 하기 전에 값을 설정 하는 명령을 실행할 수 있습니다는 `mssqlctl create cluster command`합니다.

```bash
export STORAGE_SIZE=10Gi
```

이러한 저장소 클래스 이름 및 클러스터의 다른 풀에 대 한 영구적 볼륨 크기에는 영구 저장소 설정에 대 한 다른 구성 수도 있습니다. 예를 들어, 클러스터를 배포 하기 전에 환경 변수 아래 설정으로 더 많은 용량을 다른 저장소 클래스를 사용 하 여 저장소 풀에 배포 된 영구적 볼륨을 구성할 수 있습니다.

```bash
export STORAGE_POOL_USE_PERSISTENT_VOLUME=true
export STORAGE_POOL_STORAGE_CLASS_NAME=managed-premium
export STORAGE_POOL_STORAGE_SIZE=100Gi
```

SQL Server 빅 데이터 클러스터에 대 한 영구 저장소를 설정 하기 위해 환경 변수를 관련 된 포괄적인 목록은 다음과 같습니다.

| 환경 변수 | 기본값 | Description |
|---|---|---|
| **USE_PERSISTENT_VOLUME** | true | `true` Kubernetes 영구적 볼륨을 사용 하려면 pod 저장소에 대 한 클레임입니다. `false` pod 저장소에 대 한 임시 호스트 저장소를 사용 하 합니다. |
| **STORAGE_CLASS_NAME** | 기본 | 하는 경우 `USE_PERSISTENT_VOLUME` 는 `true` 사용할 Kubernetes 저장소 클래스의 이름을 나타냅니다. |
| **STORAGE_SIZE** | 6 gi | 하는 경우 `USE_PERSISTENT_VOLUME` 는 `true`,이 각 pod에 대 한 영구적 볼륨 크기를 나타냅니다. |
| **DATA_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` Kubernetes 영구적 볼륨을 사용 하는 데이터 풀에서 pod에 대 한 클레임입니다. `false` 데이터 풀 pod에 대 한 임시 호스트 저장소를 사용 합니다. |
| **DATA_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | 데이터 풀 pod와 연결 된 영구적 볼륨에 사용할 Kubernetes 저장소 클래스의 이름을 나타냅니다.|
| **DATA_POOL_STORAGE_SIZE** | STORAGE_SIZE |데이터 풀의 각 pod에 대 한 영구적 볼륨 크기를 나타냅니다. |
| **STORAGE_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` Kubernetes 영구적 볼륨을 사용 하는 저장소 풀의 pod에 대 한 클레임입니다. `false` 저장소 풀 pod에 대 한 임시 호스트 저장소를 사용 합니다.|
| **STORAGE_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | TIndicates 저장소 풀 pod를 사용 하 여 연결 된 영구적 볼륨에 사용할 Kubernetes 저장소 클래스의 이름입니다. |
| **STORAGE_POOL_STORAGE_SIZE** | STORAGE_SIZE | 저장소 풀의 각 pod에 대 한 영구적 볼륨 크기를 나타냅니다. |

## <a name="next-steps"></a>다음 단계

Kubernetes에서 볼륨에 대 한 전체 설명서를 참조 하세요. 합니다 [볼륨에 대 한 Kubernetes 설명서](https://kubernetes.io/docs/concepts/storage/volumes/)합니다.

SQL Server 빅 데이터 클러스터를 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [빅 데이터에서 kubernetes 클러스터는 SQL Server를 배포 하는 방법을](deployment-guidance.md)합니다.

