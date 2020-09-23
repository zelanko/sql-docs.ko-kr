---
title: Kubernetes RBAC
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 빅 데이터 클러스터가 Kubernetes로 RBAC를 사용하는 방법을 설명합니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 79ea97a0824d7213f0758d75f8b552372bba51c2
ms.sourcegitcommit: a4ee6957708089f7d0dda15668804e325b8a240c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879048"
---
# <a name="kubernetes-rbac-model--impact-on-users-and-service-accounts-managing-bdc"></a>Kubernetes RBAC 모델과 BDC를 관리하는 사용자 및 서비스 계정에 대한 영향

이 문서에서는 빅 데이터 클러스터를 관리하는 사용자의 권한 요구 사항과 빅 데이터 클러스터 내부로부터 기본 서비스 계정 및 Kubernetes 액세스에 관한 의미 체계를 설명합니다.

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

다음은 필요한 아티팩트를 만드는 방법을 보여 주는 단계입니다.

1. 아래 내용이 포함된 *metrics-role.yaml* 파일을 만듭니다. *<clusterName>* 자리 표시자를 빅 데이터 클러스터의 이름으로 바꿔야 합니다.

   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRole
   metadata:
     name: <clusterName>:cr-mssql-metricsdc-reader
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
     name: <clusterName>:crb-mssql-metricsdc-reader
   roleRef:
     apiGroup: rbac.authorization.k8s.io
     kind: ClusterRole
     name: <clusterName>:cr-mssql-metricsdc-reader
   subjects:
   - kind: ServiceAccount
     name: sa-mssql-metricsdc-reader
     namespace: <clusterName>
   ```

2. 클러스터 역할과 클러스터 역할 바인딩을 만듭니다.

   ```bash
   kubectl create -f metrics-role.yaml
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

## <a name="default-service-account-usage-from-within-a-bdc-pod"></a>BDC Pod 내부로부터 기본 서비스 계정 사용

보안 모델을 강화하기 위해 SQL Server 2019 CU5에서는 BDC Pod 내 기본 Kubernetes 서비스 계정에 대한 자격 증명을 기본적으로 탑재하지 않도록 설정했습니다. 이는 CU5 이상 버전의 새 배포와 업그레이드된 배포 모두에 적용됩니다.
Pod 내부의 자격 증명 토큰을 사용하여 Kubernetes API 서버에 액세스할 수 있으며 권한 수준은 Kubernetes 권한 부여 정책 설정에 따라 달라집니다. 이전 CU5 동작으로 되돌려야 하는 특정 사용 사례가 있는 경우 CU6에서는 배포 시에만 자동 탑재를 켤 수 있도록 새 기능 스위치를 도입했습니다. 이렇게 하려면 control.json 구성 배포 파일을 사용하고 *automountServiceAccountToken*을 *true*로 설정합니다. `azdata` CLI를 사용하여 다음 명령을 실행해 *control.json* 사용자 지정 구성 파일에서 이 설정을 업데이트합니다. 

``` bash
azdata bdc config replace -c custom-bdc/control.json -j "$.security.automountServiceAccountToken=true"
```
