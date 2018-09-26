---
title: SQL Server Always On 가용성 그룹에서 Kubernetes 클러스터 배포
description: 이 문서는 SQL Server Kubernetes Always On 가용성 그룹 연산자 글로벌 요구 사항에 대 한 매개 변수를 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4d24cd2ab59e1a7959f5a8ac1c929ff2e5e8e54a
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049603"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-kubernetes-cluster"></a>SQL Server Always On 가용성 그룹에서 Kubernetes 클러스터 배포

## <a name="requirements"></a>요구 사항

- Kubernetes 클러스터
- Kubernetes 버전 1.11.0 이상이
- 4 개 이상의 노드
- [kubectl](http://kubernetes.io/docs/tasks/tools/install-kubectl/)합니다.

  >[!NOTE]
  >모든 유형의 Kubernetes 클러스터를 사용할 수 있습니다. Azure Kubernetes Service (AKS)에서 Kubernetes 클러스터를 만들려면, 참조 [AKS 클러스터 만들기](http://docs.microsoft.com/azure/aks/create-cluster.md)합니다.
  > 다음 스크립트는 Azure에서 4 개 노드 Kubernetes 클러스터를 만듭니다.
  >```azure-cli
  az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version 1.11.1
  >```

## <a name="steps"></a>단계

1. 저장소 구성

  Azure와 같은 클라우드 환경에서 구성할 [영구적 볼륨](http://kubernetes.io/docs/concepts/storage/persistent-volumes/) SQL Server의 각 인스턴스에 대 한 합니다.

  Azure에서 영구적 볼륨을 만들려면 참조 `pv.yaml` 하 고 `pvc.yaml` 에 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/templates)합니다.

  다음 명령을 실행 하는 저장소를 만들려면:

  ```azurecli
  kubectl apply -f <pv.yaml>
  ```

1. SA 암호 및 마스터 키에 대 한 Kubernetes 비밀을 만듭니다.

  다음 예제에서는 두 개의 암호를 만듭니다. `sapassword` SA 암호는 및 `masterkeypassword` 마스터 키입니다. 대신 스크립트를 실행 하기 전에 `<MyC0mp13xP@55w04d!>` 각 비밀에 대 한 다른 복잡 한 암호를 사용 하 여 합니다.

   ```azurecli
   kubectl create secret generic sql-secrets --from-literal='sapassword=<MyC0mp13xP@55w04d!>' --from-literal='masterkeypassword=<MyC0mp13xP@55w04d!>'
   ```

1. 구성 하 고 SQL Server 연산자 매니페스트를 배포 합니다.

  SQL Server 연산자 복사 `operator.yaml` 에서 파일 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)합니다.

  `operator.yaml` 파일은 Kubernetes 연산자에 대 한 배포 manifiest 합니다.

  매니페스트를 구성 하려면 업데이트 된 `operator.yaml` 사용자 환경에 대 한 파일입니다.

  매니페스트는 Kubernetes 클러스터에 적용 됩니다.

  ```azurecli
  kubectl apply -f operator.yaml
  ```

1. SQL Server 사용자 지정 리소스를 배포 합니다.

  SQL Server 매니페스트를 복사 `sqlserver.yaml` 에서 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)합니다.

  매니페스트는 Kubernetes 클러스터에 적용 됩니다.

  ```azurecli
  kubectl apply -f sqlserver.yaml
  ```

SQL Server 매니페스트를 배포한 후 연산자 컨테이너의 pod로 SQL Server의 인스턴스를 배포 합니다.

스크립트를 완료 한 후 저장소, SQL Server 인스턴스, 부하 분산 장치 서비스는 Kubernetes 연산자가 만들어집니다. 사용 하 여 배포를 모니터링할 수 있습니다 [Kubernetes 대시보드](http://docs.microsoft.com/azure/aks/kubernetes-dashboard)합니다.

Kubernetes를 만든 후 SQL Server 컨테이너 데이터베이스를 가용성 그룹에 추가 하려면 다음 단계를 완료:

1. [연결](sql-server-linux-kubernetes-connect.md) 클러스터의 SQL Server 인스턴스에 있습니다.

1. 데이터베이스를 만듭니다.

1. 전체 로그 체인을 시작 하려면 데이터베이스 백업을 수행 합니다.

1. 가용성 그룹에 데이터베이스를 추가 합니다.

가용성 그룹 자동 시드로 하므로 SQL Server가 보조 복제본을 만드는 자동으로 만들어집니다.

## <a name="next-steps"></a>다음 단계

[Kubernetes 클러스터에서 SQL Server 가용성 그룹에 연결](sql-server-linux-kubernetes-connect.md)

[Kubernetes 클러스터에서 SQL Server 가용성 그룹 관리](sql-server-linux-kubernetes-manage.md)

[Kubernetes 클러스터에서 SQL Server 가용성 그룹](sql-server-ag-kubernetes.md)