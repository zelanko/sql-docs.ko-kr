---
title: OpenShift에 배포
titleSuffix: SQL Server Big Data Cluster
description: OpenShift에서 SQL Server 빅 데이터 클러스터를 업그레이드하는 방법을 알아봅니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 91c491facec15ea50ee93641ff9482b20e5bbf1a
ms.sourcegitcommit: f2bdebed3efa55a2b7e64de9d6d9d9b1c85f479e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/24/2020
ms.locfileid: "96123984"
---
# <a name="deploy-big-data-clusters-2019-on-openshift-on-premises-and-azure-red-hat-openshift"></a>OpenShift 온-프레미스 및 Azure Red Hat OpenShift에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 OpenShift 환경, 온-프레미스 또는 ARO(Azure Red Hat OpenShift)에 SQL Server BDC(빅 데이터 클러스터)를 배포하는 방법을 설명합니다.

> [!TIP]
> ARO를 사용하고 그런 다음 이 플랫폼에 배포된 BDC를 사용하여 샘플 환경을 부트스트랩하는 빠른 방법이 필요한 경우 [여기](quickstart-big-data-cluster-deploy-aro.md)에서 제공되는 Python 스크립트를 사용하면 됩니다.


SQL Server 2019 CU5부터 OpenShift에서 SQL Server 빅 데이터 클러스터에 대한 지원이 도입되었습니다. 온-프레미스 OpenShift 또는 ARO(Azure Red Hat OpenShift)에 빅 데이터 클러스터를 배포할 수 있습니다. 배포하려면 OpenShift 클러스터 버전 4.3 이상이 필요합니다. 배포 워크플로는 여타 Kubernetes 기반 플랫폼([kubeadm](deploy-with-kubeadm.md) 및 [AKS](deploy-on-aks.md))과 비슷하나, 몇 가지 차이점이 있습니다. 차이점은 주로 애플리케이션을 루트가 아닌 사용자로 실행하는 것과 BDC가 배포된 네임스페이스에 사용되는 보안 컨텍스트와 관련되어 있습니다.

OpenShift 클러스터를 온-프레미스에 배포하는 방법은 [Red Hat OpenShift 설명서](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-installation-and-upgrade)를 참조하세요. ARO 배포는 [Azure Red Hat OpenShift](/azure/openshift/intro-openshift)를 참조하세요.

이 문서에서는 OpenShift 플랫폼에 해당하는 배포 단계를 설명하고, 대상 환경에 액세스하기 위한 옵션과 빅 데이터 클러스터를 배포하는 데 사용하는 네임스페이스를 안내합니다.

## <a name="pre-requisites"></a>필수 구성 요소

> [!IMPORTANT]
> 아래의 필수 구성 요소는 클러스터 수준 개체를 만들기 위한 충분한 권한이 있는 OpenShift 클러스터 관리자(cluster-admin 클러스터 역할)가 수행해야 합니다. OpenShift의 클러스터 역할에 대한 자세한 내용은 [RBAC를 사용하여 권한 정의 및 적용](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html)을 참조하세요.

1. OpenShift의 `pidsLimit` 설정이 SQL Server 워크로드를 수용할 수 있도록 업데이트되었는지 확인합니다. OpenShift의 기본값은 워크로드와 같은 프로덕션용으로는 너무 낮습니다. 최소 `4096`으로 시작하지만 최적 값은 SQL Server의 `max worker threads` 설정과 OpenShift 호스트 노드의 CPU 프로세서 수에 따라 다릅니다. 
    - OpenShift 클러스터의 `pidsLimit`를 업데이트하는 방법을 확인하려면 [해당 지침]( https://github.com/openshift/machine-config-operator/blob/master/docs/ContainerRuntimeConfigDesign.md)을 참조하세요. `4.3.5` 전의 OpenShift 버전에는 업데이트된 값의 효력이 발생되지 않는 결함이 있었습니다. 반드시 OpenShift를 최신 버전으로 업그레이드하세요. 
    - 환경 및 계획된 SQL Server 워크로드에 따라 최적의 값을 계산하는 데 도움이 되도록, 아래의 추산 및 예를 참고하세요.

    |프로세서 수|기본 max worker threads|프로세서당 기본 작업자|최소 pidsLimit 값|
    |--------------------|--------------------------|-----------------------------|-----------------------|
    |          64        |           512            |             16              | 512 + (64 *16) = 1536 |
    |         128        |           512            |             32              | 512 + (128*32) = 4608 |

    > [!NOTE]
    > 다른 프로세스(예: 백업, CLR, Fulltext, SQLAgent) 또한 얼마간의 오버헤드를 더하므로 추산된 값에 버퍼를 더하세요.

1. 사용자 지정 SCC(보안 컨텍스트 제약) [`bdc-scc.yaml`](#bdc-sccyaml-file) 다운로드:

    ```console
    curl https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/openshift/bdc-scc.yaml -o bdc-scc.yaml
    ```

1. 클러스터에 SCC를 적용합니다.

    ```console
    oc apply -f bdc-scc.yaml
    ```

    > [!NOTE]
    > BDC의 사용자 지정 SCC는 추가 권한과 함께 OpenShift의 기본 제공 `nonroot` SCC에 기반합니다. OpenShift의 보안 컨텍스트 제약 조건에 대해 자세히 알아보려면 [보안 컨텍스트 제약 조건 관리](https://docs.openshift.com/container-platform/4.3/authentication/managing-security-context-constraints.html)를 참조하세요. 빅 데이터 클러스터를 사용하는 데 `nonroot` SCC 외에 추가로 어떤 권한이 필요한지 알아보려면 [여기](https://aka.ms/sql-bdc-openshift-security)에서 백서를 다운로드하세요.

3. 네임스페이스/프로젝트를 만듭니다.

   ```console
   oc new-project <namespaceName>
   ```

4. BDC가 배포된 네임스페이스 내에서 사용자의 서비스 계정에 사용자 지정 SCC를 할당합니다.

   ```console
   oc adm policy add-scc-to-group bdc-scc system:serviceaccounts:<namespaceName>
   ```

5. BDC를 배포하는 사용자에게 적절한 권한을 할당합니다. 다음 중 하나를 수행합니다. 

   - BDC를 배포하는 사용자에게 cluster-admin 역할이 있는 경우 [빅 데이터 클러스터 배포](#deploy-big-data-cluster)로 넘어가세요.

   - BDC를 배포하는 사용자가 네임스페이스 관리자인 경우 사용자에게 생성된 네임스페이스에 대한 cluster-admin 로컬 역할을 할당합니다. 이는 빅 데이터 클러스터를 배포 및 관리하는 사용자가 네임스페이스 수준 관리자 권한을 갖도록 하기 위한 선호되는 옵션입니다.

   ```console
   oc adm policy add-role-to-user cluster-admin <deployingUser> -n <namespaceName>
   ```

   그런 다음 빅 데이터 클러스터를 배포하는 사용자가 OpenShift 콘솔에 로그인해야 합니다.

   ```console
   oc login -u <deployingUser> -p <password>
   ```

## <a name="deploy-big-data-cluster"></a>빅 데이터 클러스터를 배포합니다.

1. 최신 [azdata](../azdata/install/deploy-install-azdata.md)를 설치합니다.

1. 대상 환경(OpenShift 온-프레미스 또는 ARO) 및 배포 시나리오에 따라 기본 제공 구성 파일 중 하나를 OpenShift에 대해 복제합니다. 기본 제공 구성 파일에서 OpenShift에 해당하는 설정은 아래의 ‘배포 구성 파일에서 OpenShift에 해당하는 설정’ 섹션을 참조하세요. 사용 가능한 구성 파일에 대한 자세한 내용은 [배포 지침](deployment-guidance.md)을 참조하세요.

   사용 가능한 모든 기본 제공 구성 파일을 나열합니다.

   ```console
   azdata bdc config list
   ```

   기본 제공 구성 파일 중 하나를 복제하려면 아래 명령을 실행합니다. 또는 선택적으로 대상 플랫폼/시나리오에 따라 프로필을 바꿀 수 있습니다.

   ```console
   azdata bdc config init --source openshift-dev-test --target custom-openshift
   ```

   ARO에 배치하려면 이 환경에 적합한 `serviceType` 및 `storageClass`에 대한 기본값을 포함하는 `aro-` 프로파일 중 하나로 시작하세요. 예를 들면 다음과 같습니다.

   ```console
   azdata bdc config init --source aro-dev-test --target custom-openshift
   ```

1. 구성 파일 control.json 및 bdc.json을 사용자 지정합니다. 다음은 다양한 사용 사례에 대해 지원되는 사용자 지정을 안내하는 몇 가지 추가 리소스입니다.

   - [스토리지](concept-data-persistence.md)
   - [AD 관련 설정](active-directory-deploy.md)
   - [기타 사용자 지정](deployment-custom-configuration.md)

   > [!NOTE]
   > BDC용 Azure Active Directory와의 통합은 지원되지 않으므로, ARO에 배포할 때는 이 인증 방법을 사용할 수 없습니다.

1. [환경 변수](deployment-guidance.md#env)를 설정합니다.

1. 빅 데이터 클러스터를 배포합니다.

   ```console
   azdata bdc create --config custom-openshift --accept-eula yes
   ```

1. 성공적으로 배포되면 로그인하여 외부 클러스터 엔드포인트를 나열할 수 있습니다.

   ```console
      azdata login -n mssql-cluster
      azdata bdc endpoint list
   ```

## <a name="openshift-specific-settings-in-the-deployment-configuration-files"></a>배포 구성 파일에서 OpenShift에 해당하는 설정

SQL Server 2019 CU5부터 Pod 및 노드 메트릭의 수집을 제어하는 두 가지 기능 스위치가 도입되었습니다. 이러한 매개 변수는 OpenShift에 대한 기본 제공 프로필에서 기본적으로 `false`로 설정됩니다. 모니터링 컨테이너에 [권한 있는 보안 컨텍스트](https://www.openshift.com/blog/managing-sccs-in-openshift)가 필요하기 때문입니다. 이로 인해 BDC가 배포된 네임스페이스의 보안 제약 조건이 일부 완화됩니다.

```json
    "security": {
      "allowNodeMetricsCollection": false,
      "allowPodMetricsCollection": false
}
```

ARO의 기본 스토리지 클래스 이름은 (기본 스토리지 클래스가 기본값인 경우의 AKS가 아닌) managed-premium입니다. 이는 `aro-dev-test` 및 `aro-dev-test-ha`에 대응되는 `control.json`에서 확인할 수 있습니다.

```json
    },
    "storage": {
      "data": {
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
      }
```

## <a name="bdc-sccyaml-file"></a>`bdc-scc.yaml` 파일:

이 배포에 대한 SCC 파일은 다음과 같습니다.

:::code language="yaml" source="../../sql-server-samples/samples/features/sql-big-data-cluster/deployment/openshift/bdc-scc.yaml":::

## <a name="next-steps"></a>다음 단계

[자습서: SQL Server 빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)
