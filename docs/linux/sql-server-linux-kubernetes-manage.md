---
title: SQL Server Always On 가용성 그룹 관리 Kubernetes
description: 이 문서는 SQL Server Always On 가용성 그룹에서 Kubernetes 관리 하는 방법에 설명 합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ad4f310ce6c0e200d5e658b3d5814131000d0004
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518489"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>SQL Server 가용성 그룹 Kubernetes Always On 관리

Always On 가용성 그룹에서 kubernetes를 관리 하려면 매니페스트를 만들고 클러스터에 적용 합니다. 매니페스트는는 `.yaml` 파일입니다.  

이 문서의 예제에서는 모든 Kubernetes 클러스터에 적용 됩니다. 이 예제 시나리오는 Azure Kubernetes Service에서 클러스터에 대해 적용 됩니다.

전체 배포의 예제를 보려면 [는 SQL Server Always On 가용성 그룹에서 Kubernetes 클러스터 배포](sql-server-linux-kubernetes-deploy.md)합니다.

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>장애 조치-Kubernetes에서 SQL Server 가용성 그룹

장애 조치 또는 주 복제본을 가용성 그룹의 다른 노드로 이동 하려면 다음 단계를 수행 합니다.

1. 매니페스트 파일에서 작업을 정의 합니다.

  [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml) -에 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) github 리포지토리를 장애 조치 작업에 설명 합니다.

  터미널에 게 관리 하는 매니페스트 파일을 복사 합니다.

  사용자 환경에 대 한 파일을 업데이트 합니다.

  - 대체 `<containerName>` pod 이름 (예:: mssql2-0) 예상 되는 가용성 그룹 대상으로 합니다.
  - 가용성 그룹에 없는 경우는 `ag1` 네임 스페이스 대체 `ag1` 네임 스페이스를 사용 하 여 합니다.

  이 파일은 명명 된 장애 조치 작업을 정의 `manual-failover`합니다.

1. 작업을 배포 하려면 사용 하 여 `kubectl apply`입니다. 다음 스크립트는 작업을 배포합니다.

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  작업이 배포 되 면 kubernetes의 경우 SQL Server 연산자를 사용 하 여 다음 작업을 수행 합니다.
  
  - 주 복제본이 보조 복제본에서는 보조로 강등
  
  - 지정 된 복제본을 주 복제본을 승격합니다.
  
  Kubernetes 매니페스트 파일을 적용 한 후 작업을 실행 합니다. 작업은 감독자 새 리더를 선택할 수 있습니다 하 고 프로덕션에서는 리더의 SQL Server 인스턴스를 주 복제본을 이동 합니다.

1. 작업이 완료 되었는지 확인 합니다.
  
  Kubernetes 작업을 실행 한 후에 로그를 검토할 수 있습니다.
  
  다음 예제에서는 명명 된 작업의 상태를 반환 합니다. `manual-failover`합니다.

  ```azurecli
  kubectl describe jobs/manual-failover --namespace ag1
  ```

1. 수동 장애 조치 작업을 삭제 합니다. 

  >[!IMPORTANT]
  >수동 장애 조치를 실행 하기 전에 작업을 수동으로 삭제 해야 합니다.
  > 
  >Kubernetes에서 작업 개체는 해당 상태를 볼 수 있도록 완료 된 후 유지 됩니다. 해당 상태를 확인 한 후 이전 작업을 수동으로 삭제 해야 합니다. Kubernetes 로그 삭제 작업을 삭제 하면 됩니다. 작업을 삭제 하지 않으면, 작업 이름 및 pod 선택기를 변경 하지 않는 한 이후 장애 조치 작업이 실패 합니다. 자세한 내용은 [-작업 실행을 완료 하려면](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)합니다.

  다음 명령은 작업을 삭제 합니다.

  ```azurecli
  kubectl delete jobs manual-failover --namespace ag1
  ```

## <a name="rotate-credentials"></a>자격 증명 회전

SQL Server에 대 한 암호를 재설정 하려면 자격 증명 회전 `sa` 계정 및 SQL Server [서비스 마스터 키](../relational-databases/security/encryption/service-master-key.md)합니다. 

이 작업을 완료 하려면 Kubernetes 클러스터에서 새 암호 만들기를 다음 자격 증명 회전 하는 작업을 만듭니다.

자격 증명을 회전 하기 전에 암호 및 마스터 키에 대 한 새 암호를 확인 합니다.

다음 스크립트를 만들고 라는 비밀 `new-sql-secrets`합니다. 스크립트를 실행 하기 전에 교체 `<>` 에 대 한 복잡 한 암호를 사용 하 여 합니다 `sapassword` 하며 `masterkeypassword`합니다. 각 해당 값에 대해 다른 암호를 사용 합니다.

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

마스터 키가 필요 하는 SQL Server의 모든 인스턴스에 대해 다음 단계를 완료 하거나 `sa` 암호입니다.

1. 복사본 [ `rotate-creds.yaml` ](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) 터미널에 관리 합니다.

  [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) 에 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/) github 리포지토리는이 작업에 대 한 매니페스트 예입니다.

  이 매니페스트를 적용 하기 전에 사용자 환경에 대 한 매니페스트를 업데이트 합니다. 검토 하 고 필요에 따라 다음 설정을 변경 합니다.

  - 네임 스페이스를 확인 합니다. 필요한 경우 업데이트 합니다. 매니페스트에 다음 예제에서는 명명 된 네임 스페이스 적용할 `ag1`합니다.

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - SQL Server 인스턴스의 이름을 확인 합니다. 필요한 경우 업데이트 합니다. 다음 예제에서는 매니페스트 사양 라는 SQL Server 인스턴스를 적용할 `mssql1`합니다.

    ```yaml
    env:
      - name: MSSQL_K8S_SQL_SERVER_NAME
        value: mssql1
    ```

  사용자의 워크스테이션에 업데이트 된 매니페스트 파일을 저장 합니다.

1. 사용 하 여 `kubectl` 작업을 배포 합니다.

  ```azurecli
  kubectl apply -f rotate-creds.yaml --namespace ag1
  ```

  Kubernetes 마스터 키를 업데이트 하 고 `sa` 가용성 그룹에 SQL Server의 단일 인스턴스에 대 한 암호입니다.

1. 작업이 완료 되었는지 확인 합니다. 다음 명령을 실행합니다. 작업이 완료 되 고 있는지를 확인. 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  작업이 성공 하면 마스터 키 및 `sa` SQL Server의 한 인스턴스에서만 암호 업데이트 됩니다.


1. 작업을 다시 실행 하기 전에 작업을 삭제 합니다. 각 작업의 이름은 고유 해야 합니다.

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

동일 하 게 설정 하려면 `sa` SQL Server의 모든 인스턴스에 대 한 암호는 SQL Server의 각 인스턴스에 대해 위의 단계를 반복 합니다.

## <a name="next-steps"></a>다음 단계

[Azure Kubernetes Service (AKS)를 사용 하 여 Kubernetes 대시보드에 액세스](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Kubernetes 클러스터에서 SQL Server 가용성 그룹](sql-server-ag-kubernetes.md)
