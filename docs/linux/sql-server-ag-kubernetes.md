---
title: Linux를 실행하는 컨테이너의 Always On 가용성 그룹
titleSuffix: SQL Server
description: 이 문서에서는 SQL Server 컨테이너의 가용성 그룹을 소개합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3910c74be803b7fc63c8bf560fc637387e06ee15
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67910476"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>SQL Server 컨테이너의 Always On 가용성 그룹

SQL Server 2019는 Kubernetes 클러스터의 컨테이너에 대한 가용성 그룹을 지원합니다. 가용성 그룹에 대해 SQL Server [Kubernetes 연산자](https://coreos.com/blog/introducing-operators.html)를 Kubernetes 클러스터에 배포합니다. 이 연산자는 클러스터에서 가용성 그룹을 패키지, 배포 및 관리하는 데 유용합니다.

![Kubernetes 컨테이너의 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

위의 그림에서 4개 노드 kubernetes 클러스터는 세 개의 복제본이 있는 가용성 그룹의 호스트입니다. 이 솔루션은 다음 구성 요소를 포함합니다.

* Kubernetes [*배포*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/). 이 배포에는 연산자와 구성 맵이 포함됩니다. 이 배포는 가용성 그룹의 SQL Server 인스턴스를 배포하는 데 필요한 컨테이너 이미지, 소프트웨어 및 지침을 제공합니다.

* 각각 [*StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)을 호스트하는 3개의 노드. StatefulSet은 [*pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)를 포함합니다. 각 pod에는 다음이 포함됩니다.
  * SQL Server 인스턴스를 하나 실행하는 SQL Server 컨테이너
  * 가용성 그룹 에이전트 

* 가용성 그룹과 관련된 2개의 [*ConfigMap*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/). ConfigMap은 다음에 대한 정보를 제공합니다.
  * 연산자의 배포
  * 가용성 그룹입니다.

 * [*영구적 볼륨*](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)은 스토리지의 일부입니다. PVC(*영구적 볼륨 클레임*)는 사용자의 스토리지 요청입니다. 각 컨테이너는 데이터 및 로그 스토리지에 대한 PVC와 관련됩니다. AKS(Azure Kubernetes Service)에서는 스토리지 클래스를 기준으로 스토리지를 자동으로 프로비저닝하기 위한 [영구적 볼륨 클레임을 만듭니다](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv).


또한 클러스터는 암호, 인증서, 키 및 기타 중요한 정보에 대한 [*비밀*](https://kubernetes.io/docs/concepts/configuration/secret/)을 저장합니다.

## <a name="deploy-the-availability-group-in-kubernetes"></a>Kubernetes에서 가용성 그룹 배포

Kubernetes에서 가용성 그룹을 배포하려면

1. Kubernetes 클러스터를 만듭니다.

   가용성 그룹의 경우, SQL Server용 노드 3개 이상과 마스터용 노드 1개 이상을 만듭니다.

1. 연산자를 배포합니다.

1. 스토리지를 구성합니다.

1. StatefulSet을 배포합니다.

   연산자는 StatefulSet을 배포하기 위한 지침을 수신합니다. 별도의 3개 노드에서 SQL Server 인스턴스를 자동으로 만들고 외부 클러스터 관리자를 사용하여 가용성 그룹을 구성합니다.

1. 데이터베이스를 만든 후 가용성 그룹에 연결합니다.

자세한 단계는 [SQL Server 컨테이너의 Always On 가용성 그룹](sql-server-ag-kubernetes.md)을 참조하세요.

## <a name="sql-server-kubernetes-operator"></a>SQL Server Kubernetes 연산자

이 연산자를 배포하면 사용자 지정 SQL Server 리소스를 등록합니다. 연산자를 사용하여 이 리소스를 배포합니다.  각 리소스는 SQL Server 인스턴스에 해당하고, `sapassword` 및 `monitoring policy`와 같은 특정 속성을 포함합니다. 연산자는 리소스를 구문 분석하고 Kubernetes StatefulSet을 배포합니다.

StatfulSet에는 다음이 포함됩니다.

* mssql-server 컨테이너

* mssql-ha-supervisor 컨테이너

연산자, HA 감독자 및 SQL Server에 대한 코드는 `mcr.microsoft.com/mssql/ha`라는 Docker 이미지에 패키지됩니다. 이 이미지에는 다음 이진 파일이 포함됩니다.

* `mssql-operator`

    이 프로세스는 별도의 Kubernetes 배포로 배포됩니다. `SqlServer`(sqlservers.mssql.microsoft.com)라는 [Kubernetes 사용자 지정 리소스](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)를 등록합니다. 그런 후 Kubernetes 클러스터에서 만들어지거나 업데이트되는 이러한 리소스를 수신 대기합니다. 이러한 모든 이벤트에 대해, 해당 인스턴스의 Kubernetes 리소스(예: StatefulSet 또는 `mssql-server-k8s-init-sql` 작업)를 만들거나 업데이트합니다.

* `mssql-server-k8s-health-agent`

    이 웹 서버는 Kubernetes [liveness 프로브](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)를 제공하여 SQL Server 인스턴스의 상태를 확인하도록 합니다. `sp_server_diagnostics`를 호출하고 결과를 모니터 정책과 비교하여 로컬 SQL Server 인스턴스의 상태를 모니터링합니다.

* `mssql-ha-supervisor`

   AG 인증서 및 엔드포인트를 유지 관리합니다. 

* `mssql-server-k8s-ag-agent`
  
    이 프로세스는 단일 SQL Server 인스턴스에서 AG 복제본의 상태를 모니터링하고 장애 조치(failover)를 수행합니다.

    리더 선택도 유지 관리합니다.

* `mssql-server-k8s-init-sql`
  
    이 Kubernetes [작업](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)은 SQL Server 인스턴스에 필요한 상태 구성을 적용합니다. 이 작업은 SqlServer 리소스가 만들어지거나 업데이트될 때마다 연산자가 만듭니다. 사용자 지정 리소스에 해당하는 대상 SQL Server 인스턴스에 리소스에 설명된 필요한 구성이 있는지 확인합니다.

    예를 들어 다음 설정 중 하나 이상이 필요한 경우 완료합니다.
  * SA 암호를 업데이트합니다.
  * 에이전트에 대한 SQL 로그인을 만듭니다.
  * DBM 엔드포인트를 만듭니다.

* `mssql-server-k8s-rotate-creds`
  
    이 Kubernetes 작업은 자격 증명 회전 작업을 구현합니다. SA 암호, 에이전트 SQL 로그인 암호, DBM 인증서 등의 업데이트를 요청하려면 이 작업을 만듭니다. SA 암호는 작업 매개 변수로 지정됩니다. 다른 항목은 자동으로 생성됩니다.

* `mssql-server-k8s-failover`

   수동 장애 조치(failover) 워크플로를 구현하는 Kubernetes 작업입니다.

### <a name="notes"></a>참고

AG 구성에 관계없이 연산자는 항상 HA 감독자를 배포합니다. SqlServer 리소스가 AG를 나열하지 않는 경우에도 연산자는 이 컨테이너를 계속 배포합니다.

연산자 이미지의 버전은 SQL Server 이미지의 버전과 동일합니다.

## <a name="next-steps"></a>다음 단계

> [Kubernetes의 SQL Server 컨테이너](tutorial-sql-server-containers-kubernetes.md)
