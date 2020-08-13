---
title: Kubernetes RBAC
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 빅 데이터 클러스터가 Kubernetes로 RBAC를 사용하는 방법을 설명합니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d2e3f379402f16f32020f9cd34103919f13a30c
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552978"
---
# <a name="kubernetes-rbac-model--impact-on-users-managing-bdc"></a>Kubernetes RBAC 모델 및 BDC를 관리하는 사용자에게 미치는 영향

다음 섹션에서는 빅 데이터 클러스터를 관리하는 사용자에게 필요한 권한에 대해 설명합니다.

> [!NOTE]
> Kubernetes RBAC 모델에 대한 추가 리소스는 [Using RBAC Authorization - Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)(RBAC 인증 사용 - Kubernetes) 및 [Using RBAC to define and apply permissions - OpenShift](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html)(RBAC를 사용하여 권한 정의 및 적용 - OpenShift)를 참조하세요.

## <a name="role-required-for-deployment"></a>배포에 필요한 역할

BDC는 서비스 계정(예: `sa-mssql-controller` 또는 `master`)을 사용하여 클러스터 Pod, 서비스, 고가용성, 모니터링 등의 프로비저닝을 오케스트레이션합니다. BDC 배포가 시작되면 (예: `azdata bdc create`) `azdata`가 다음 작업을 수행합니다.

1. 제공된 네임스페이스가 존재하는지 확인합니다.
2. 존재하지 않는 경우 네임스페이스를 만들고 `MSSQL_CLUSTER` 레이블을 적용합니다.
3. `sa-mssql-controller` 서비스 계정을 만듭니다.
4. 네임스페이스 또는 프로젝트에 대한 모든 권한을 가지되 클러스터 수준 권한은 없는 `<namespaced>-admin` 역할을 만듭니다.
5. 역할에 대해 해당 서비스 계정의 역할 할당을 만듭니다.

위 단계가 완료되면 컨트롤 플레인 Pod이 프로비저닝되고 서비스 계정이 빅 데이터 클러스터의 나머지 부분을 배포합니다.  

결과적으로 배포하는 사용자에게는 다음과 같은 권한이 있어야 합니다.

- 클러스터에 있는 네임스페이스를 나열합니다(1).
- 레이블을 사용하여 새 네임스페이스 또는 기존 네임스페이스를 패치합니다(2).
- 서비스 계정 `sa-mssql-controller`, `<namespaced>-admin` 역할 및 역할 바인딩을 만듭니다(3~5).

기본 `admin` 역할에는 이러한 권한이 없으므로 빅 데이터 클러스터를 배포하는 사용자에게는 최소한 네임스페이스 수준 관리자 권한이 있어야 합니다.

## <a name="cluster-role-required-for-pods-and-nodes-metrics-collection"></a>Pod 및 노드 메트릭 수집에 필요한 클러스터 역할

SQL Server 2019 CU5부터, Telegraf에는 Pod 및 노드 메트릭을 수집하기 위해 클러스터 전체 역할 권한이 있는 서비스 계정이 필요합니다. 배포(또는 기존 배포의 업그레이드) 중에 필요한 서비스 계정 및 클러스터 역할을 만들려고 시도합니다. 단, 클러스터를 배포하거나 업그레이드를 수행하는 사용자에게 충분한 권한이 없는 경우에도 배포 또는 업그레이드는 경고와 함께 계속 진행되고 성공합니다. 이 경우 Pod 및 노드 메트릭이 수집되지 않습니다. 클러스터를 배포하는 사용자는 클러스터 관리자에게 배포 또는 업그레이드 전 또는 후에 역할 및 서비스 계정을 만들도록 요청해야 합니다. 이렇게 만든 역할 및 서비스 계정은 BDC가 사용합니다. 

다음은 필요한 아티팩트를 만드는 방법을 보여 주는 스크립트입니다.

```console
export CLUSTER_NAME=mssql-cluster
kubectl create -f - <<EOF
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
rules:
- apiGroups:
  - '*'
  resources:
  - pods
  - nodes/stats
  verbs:
  - get
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: ${CLUSTER_NAME}:crb-mssql-metricsdc-reader
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
subjects:
- kind: ServiceAccount
  name: sa-mssql-metricsdc-reader
  namespace: ${CLUSTER_NAME}
EOF
```

서비스 계정, 클러스터 역할 및 클러스터 역할 바인딩은 BDC 배포 전 또는 후에 만들 수 있습니다. Kubernetes는 Telegraf 서비스 계정의 권한을 자동으로 업데이트합니다. 이것이 Pod 배포로 생성된 경우 Pod 및 노드 메트릭이 수집되기 전까지 몇 분 정도 지연 시간이 발생합니다.

> [!NOTE]
> SQL Server 2019 CU5부터 Pod 및 노드 메트릭의 수집을 제어하는 두 가지 기능 스위치가 도입되었습니다. 기본적으로 이 매개 변수는 기본값이 재정의되는 OpenShift를 제외하고 모든 환경 대상에서 true로 설정됩니다. 

이러한 설정은 `control.json` 배포 구성 파일의 보안 섹션에서 사용자 지정할 수 있습니다.

```json
  "security": {
    …
    "allowNodeMetricsCollection": false,
    "allowPodMetricsCollection": false
  }
```

이러한 설정이 `false`로 설정된 경우 BDC 배포 워크플로는 서비스 계정, 클러스터 역할 및 Telegraf에 대한 바인딩을 만들려고 시도하지 않습니다.
