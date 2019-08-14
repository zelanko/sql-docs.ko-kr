---
title: Kubernetes의 SQL Server Always On 가용성 그룹 관리
description: 이 문서에서는 Kubernetes의 SQL Server Always On 가용성 그룹을 관리하는 방법을 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 893e502c35ae33ce6ff87efd88049db97a40f875
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952548"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>Kubernetes의 SQL Server Always On 가용성 그룹 관리

Kubernetes의 Always On 가용성 그룹을 관리하려면 매니페스트를 만들어 클러스터에 적용합니다. 매니페스트는 `.yaml` 파일입니다.  

이 문서의 예제는 모든 Kubernetes 클러스터에 적용됩니다. 이 예제의 시나리오는 Azure Kubernetes Service의 클러스터에 적용됩니다.

[Kubernetes 클러스터에 SQL Server Always On 가용성 그룹 배포](sql-server-linux-kubernetes-deploy.md)에서 전체 배포 예제를 참조하세요.

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>장애 조치(failover) - Kubernetes의 SQL Server 가용성 그룹

주 복제본을 가용성 그룹의 다른 노드로 장애 조치(failover)하거나 이동하려면 다음 단계를 완료합니다.

1. 매니페스트 파일에서 작업을 정의합니다.

  [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) github 리포지토리의 [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml)에서 장애 조치(failover) 작업을 설명합니다.

  매니페스트 파일을 관리 터미널에 복사합니다.

  해당 환경에 맞게 파일을 업데이트합니다.

  - `<containerName>`을 예상 가용성 그룹 대상의 Pod 이름(예: mssql2-0)으로 바꿉니다.
  - 가용성 그룹이 `ag1` 네임스페이스에 없는 경우 `ag1`을 네임스페이스로 바꿉니다.

  이 파일은 `manual-failover`라는 장애 조치(failover) 작업을 정의합니다.

1. 작업을 배포하려면 `kubectl apply`를 사용합니다. 다음 스크립트는 작업을 배포합니다.

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  작업이 배포된 후 Kubernetes는 SQL Server 운영자를 사용하여 다음 작업을 수행합니다.
  
  - 주 복제본을 보조 복제본으로 수준 내리기
  
  - 지정된 복제본을 주 복제본으로 수준 올리기
  
  매니페스트 파일을 적용하면 Kubernetes에서 작업을 실행합니다. 작업을 통해 감독자는 새 리더를 선택하고 주 복제본을 리더의 SQL Server 인스턴스로 이동합니다.

1. 작업이 완료되었는지 확인합니다.
  
  Kubernetes에서 작업을 실행한 후에 로그를 검토할 수 있습니다.
  
  다음 예제에서는 `manual-failover`라는 작업의 상태를 반환합니다.

  ```azurecli
  kubectl describe jobs/manual-failover --namespace ag1
  ```

1. 수동 장애 조치(failover) 작업을 삭제합니다. 

  >[!IMPORTANT]
  >다른 수동 장애 조치(failover)를 실행하기 전에 작업을 수동으로 삭제해야 합니다.
  > 
  >Kubernetes의 작업 개체는 완료된 후에도 그대로 유지되므로 해당 상태를 볼 수 있습니다. 상태를 확인한 후에는 이전 작업을 수동으로 삭제해야 합니다. 작업을 삭제하면 Kubernetes 로그도 삭제됩니다. 작업을 삭제하지 않으면, 작업 이름과 Pod 선택기를 변경하지 않을 경우 이후 장애 조치(failover) 작업이 실패합니다. 자세한 내용은 [작업 - 완료될 때까지 실행](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)을 참조하세요.

  다음 명령은 작업을 삭제합니다.

  ```azurecli
  kubectl delete jobs manual-failover --namespace ag1
  ```

## <a name="rotate-credentials"></a>자격 증명 회전

자격 증명을 회전하여 SQL Server `sa` 계정과 SQL Server [서비스 마스터 키](../relational-databases/security/encryption/service-master-key.md)의 암호를 재설정합니다. 

이 작업을 완료하려면 Kubernetes 클러스터에서 새 비밀을 만든 다음, 자격 증명을 회전하는 작업을 만듭니다.

자격 증명을 회전하기 전에 암호와 마스터 키의 새 비밀을 만듭니다.

다음 스크립트는 `new-sql-secrets`라는 비밀을 만듭니다. 스크립트를 실행하기 전에 `sapassword` 및 `masterkeypassword`에서 `<>`를 복잡한 암호로 바꿉니다. 각 값에 대해 서로 다른 암호를 사용합니다.

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

마스터 키 또는 `sa` 암호가 필요한 모든 SQL Server 인스턴스에 대해 다음 단계를 완료합니다.

1. 관리 터미널에 [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml)을 복사합니다.

  [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/) github 리포지토리의 [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml)은 이 작업의 매니페스트 예입니다.

  이 매니페스트를 적용하기 전에 해당 환경에 맞게 매니페스트를 업데이트합니다. 필요에 따라 다음 설정을 검토하고 변경합니다.

  - 네임스페이스를 확인합니다. 필요한 경우 업데이트합니다. 매니페스트의 다음 예제는 `ag1`이라는 네임스페이스에 적용됩니다.

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - SQL Server 인스턴스의 이름을 확인합니다. 필요한 경우 업데이트합니다. 매니페스트 사양의 다음 예제는 `mssql1`이라는 SQL Server 인스턴스에 적용됩니다.

    ```yaml
    env:
      - name: MSSQL_K8S_SQL_SERVER_NAME
        value: mssql1
    ```

  업데이트된 매니페스트 파일을 워크스테이션에 저장합니다.

1. `kubectl`을 사용하여 작업을 배포합니다.

  ```azurecli
  kubectl apply -f rotate-creds.yaml --namespace ag1
  ```

  Kubernetes는 가용성 그룹에 있는 한 SQL Server 인스턴스의 마스터 키와 `sa` 암호를 업데이트합니다.

1. 작업이 완료되었는지 확인합니다. 다음 명령을 실행합니다. 작업이 완료되었는지 확인하려면 다음 명령을 실행합니다. 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  작업이 성공하면 한 SQL Server 인스턴스의 마스터 키와 `sa` 암호가 업데이트됩니다.


1. 작업을 다시 실행하기 전에 작업을 삭제합니다. 각 작업 이름은 고유해야 합니다.

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

모든 SQL Server 인스턴스에 대해 동일한 `sa` 암호를 설정하려면 각 SQL Server 인스턴스에서 위 단계를 반복합니다.

## <a name="next-steps"></a>다음 단계

[AKS(Azure Kubernetes Service)를 사용하여 Kubernetes 대시보드에 액세스](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Kubernetes 클러스터의 SQL Server 가용성 그룹](sql-server-ag-kubernetes.md)
