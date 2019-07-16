---
title: Linux를 실행 하는 컨테이너에 대 한 always On 가용성 그룹
titleSuffix: SQL Server
description: 이 문서에서는 SQL Server 컨테이너에서 가용성 그룹을 소개합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3910c74be803b7fc63c8bf560fc637387e06ee15
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910476"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>SQL Server 컨테이너에 대 한 always On 가용성 그룹

SQL Server 2019 Kubernetes 클러스터에서 컨테이너에 대 한 가용성 그룹을 지원합니다. 가용성 그룹에 대 한 SQL Server를 배포 [Kubernetes 연산자](https://coreos.com/blog/introducing-operators.html) Kubernetes 클러스터에 있습니다. 연산자에는 패키지를 배포 하 고 클러스터에서 가용성 그룹을 관리할 수 있습니다.

![Kubernetes 컨테이너에서 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

위의 이미지에서 4 개 노드 kubernetes 클러스터 세 개의 복제본을 사용 하 여 가용성 그룹을 호스팅합니다. 다음 구성 요소를 포함 하는 솔루션:

* Kubernetes [ *배포*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)합니다. 배포 구성 맵과 연산자를 포함합니다. 이러한 컨테이너 이미지, 소프트웨어 및 가용성 그룹에 대 한 SQL Server 인스턴스를 배포 하는 데 필요한 지침을 제공 합니다.

* 세 개의 노드를 호스팅하는 [ *StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)합니다. StatefulSet의 포함 된 [ *pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)합니다. 각 pod에는 다음이 포함 됩니다.
  * SQL Server 인스턴스를 실행 하는 SQL Server 컨테이너입니다.
  * 가용성 그룹 에이전트입니다. 

* 두 개의 [ *ConfigMaps* ](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) 가용성 그룹과 관련 됩니다. ConfigMaps에 대 한 정보를 제공합니다.
  * 연산자에 대 한 배포 합니다.
  * 가용성 그룹입니다.

 * [*영구적 볼륨* ](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) 조각 저장소입니다. A *영구적 볼륨 클레임* (PVC)는 사용자가 저장소에 대 한 요청입니다. 각 컨테이너는 데이터 및 로그 저장소에 대 한 PVC를 사용 하 여 관련 됩니다. Azure Kubernetes Service (AKS), 있습니다 [영구적 볼륨 클레임을 만드는](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) 에 자동으로 저장소를 프로 비전 된 저장소 클래스를 기반으로 합니다.


또한 클러스터 저장 [ *비밀* ](https://kubernetes.io/docs/concepts/configuration/secret/) 암호, 인증서, 키 및 기타 중요 한 정보에 대 한 합니다.

## <a name="deploy-the-availability-group-in-kubernetes"></a>Kubernetes에서 가용성 그룹 배포

Kubernetes에서 가용성 그룹을 배포 합니다.

1. Kubernetes 클러스터 만들기

   가용성 그룹에 대 한 마스터에 대 한 SQL Server와 노드 노드가 3 개 이상 만듭니다.

1. 연산자를 배포 합니다.

1. 저장소 구성

1. StatefulSet 배포

   연산자는 StatefulSet를 배포 하는 지침에 대 한 수신 대기 합니다. 자동으로 세 개의 별도 노드에서 SQL Server의 인스턴스를 만듭니다 하 고 외부 클러스터 관리자를 사용 하 여 가용성 그룹을 구성 합니다.

1. 데이터베이스를 만들고 가용성 그룹에 연결

자세한 단계를 참조 하세요 [SQL Server 컨테이너에 대 한 Always On 가용성 그룹](sql-server-ag-kubernetes.md)합니다.

## <a name="sql-server-kubernetes-operator"></a>SQL Server Kubernetes 연산자

연산자를 배포한 후 사용자 지정 SQL Server 리소스를 등록 합니다. 이 리소스를 배포 하는 연산자를 사용 합니다.  각 리소스의 SQL Server 인스턴스에 해당 하며, 및와 같은 특정 속성을 포함 `sapassword` 고 `monitoring policy`입니다. 리소스 구문 분석 하 고 Kubernetes StatefulSet를 배포 하는 연산자입니다.

StatfulSet 포함 되어 있습니다.

* mssql server 컨테이너

* mssql-ha-supervisor container

연산자, HA 감독자 및 SQL Server에 대 한 코드를 호출 하는 Docker 이미지에 패키지 됩니다 `mcr.microsoft.com/mssql/ha`합니다. 이 이미지는 다음 이진 파일이 포함 되어 있습니다.

* `mssql-operator`

    이 프로세스는 별도 Kubernetes 배포로 배포 됩니다. 등록 된 [Kubernetes 사용자 지정 리소스](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) 호출 `SqlServer` (sqlservers.mssql.microsoft.com). 그런 다음 이러한 리소스를 만들거나 Kubernetes 클러스터에서 업데이트에 대 한 수신 대기 합니다. 이러한 모든 이벤트에 대 한 생성 또는 업데이트 해당 인스턴스에 대 한 Kubernetes 리소스 (예를 들어 StatefulSet, 또는 `mssql-server-k8s-init-sql` 작업).

* `mssql-server-k8s-health-agent`

    이 웹 서버 역할 Kubernetes [선거의 프로브](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) SQL Server 인스턴스의 상태를 확인 합니다. 호출 하 여 로컬 SQL Server 인스턴스의 상태를 모니터링 `sp_server_diagnostics` 및 프로그램 모니터링 정책 사용 하 여 결과 비교 합니다.

* `mssql-ha-supervisor`

   Ag 인증서와 끝점을 유지 관리합니다. 

* `mssql-server-k8s-ag-agent`
  
    이 프로세스는 단일 SQL Server 인스턴스에서 AG 복제본의 상태를 모니터링 하 고 장애 조치를 수행 합니다.

    리더 선택도 유지 됩니다.

* `mssql-server-k8s-init-sql`
  
    이 Kubernetes [작업](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/) SQL Server 인스턴스에 필요한 상태 구성을 적용 합니다. Sql Server 리소스를 만들거나 업데이트할 때마다 작업 연산자에서 생성 됩니다. 사용자 지정 리소스에 해당 하는 대상 SQL Server 인스턴스의 리소스에 설명 된 원하는 구성이 있는지 확인 합니다.

    예를 들어, 필요한 경우 다음 설정 중 필요한 설정을 완료 합니다.
  * SA 암호를 업데이트 합니다.
  * 에이전트에 대 한 SQL 로그인을 만듭니다.
  * DBM 끝점이 만들어집니다.

* `mssql-server-k8s-rotate-creds`
  
    이 Kubernetes 작업 자격 증명 회전 작업을 구현 합니다. SA 암호, 에이전트 SQL 로그인 암호, DBM 인증서에 대 한 업데이트를 요청 하려면이 작업을 만듭니다. SA 암호 작업 매개 변수로 지정 됩니다. 나머지는 자동으로 생성 합니다.

* `mssql-server-k8s-failover`

   수동 장애 조치 워크플로 구현 하는 Kubernetes 작업.

### <a name="notes"></a>참고

AG 구성에 관계 없이 연산자 HA 감독자 항상 배포 됩니다. SqlServer 리소스는 다른 AG를 나열 하지 않습니다, 경우 연산자는이 컨테이너를 배포 계속 합니다.

연산자 이미지에 대 한 버전이 SQL Server 이미지에 대 한 버전과 동일 합니다.

## <a name="next-steps"></a>다음 단계

> [Kubernetes에서 SQL Server 컨테이너](tutorial-sql-server-containers-kubernetes.md)
