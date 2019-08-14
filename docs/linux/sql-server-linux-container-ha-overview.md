---
title: SQL Server 컨테이너의 고가용성
description: 이 문서에서는 SQL Server 컨테이너의 고가용성을 소개합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: aa54849c16ea9dfb821404b553b1e9183b61d66a
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077485"
---
# <a name="high-availability-for-sql-server-containers"></a>SQL Server 컨테이너의 고가용성

Kubernetes에서 기본적으로 SQL Server 인스턴스를 만들고 관리합니다.

[Kubernetes](https://kubernetes.io/)에서 관리하는 docker 컨테이너에 SQL Server를 배포합니다. Kubernetes에서 클러스터 노드가 실패하는 경우 SQL Server 인스턴스가 포함된 컨테이너가 자동으로 복구될 수 있습니다. 보다 강력한 가용성을 위해 Kubernetes 클러스터에서 컨테이너의 SQL Server 인스턴스를 사용하여 SQL Server Always On 가용성 그룹을 구성합니다. 이 문서에서는 두 가지 솔루션을 비교합니다.

## <a name="compare-sql-server-versions-on-kubernetes"></a>Kubernetes의 SQL Server 버전 비교

SQL Server 2017은 Kubernetes에서 배포할 수 있는 Docker 이미지를 제공합니다. Kubernetes PVC(영구적 볼륨 클레임)를 사용하여 이미지를 구성할 수 있습니다. Kubernetes는 컨테이너의 SQL Server 프로세스를 모니터링합니다. 프로세스, Pod, 컨테이너 또는 노드가 실패하는 경우 Kubernetes는 자동으로 다른 인스턴스를 부트스트랩하고 스토리지에 다시 연결합니다.

SQL Server 2019(미리 보기)에는 Kubernetes StatefulSet가 포함된 더 강력한 아키텍처가 도입되었습니다. Kubernetes는 SQL Server Always On 가용성 그룹에 참여하는 컨테이너 이미지의 SQL Server 인스턴스를 오케스트레이션합니다. 이 패턴은 향상된 상태 모니터링, 더 빠른 복구, 오프로드 백업 및 읽기 확장을 제공합니다.  

## <a name="container-with-sql-server-instance-on-kubernetes"></a>Kubernetes의 SQL Server 인스턴스가 포함된 컨테이너

Kubernetes 1.6 이상에서는 [*스토리지 클래스*](https://kubernetes.io/docs/concepts/storage/storage-classes/), [*영구적 볼륨 클레임*](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims) 및 [*Azure 디스크 볼륨 유형*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)을 지원합니다. 

이 구성에서 Kubernetes는 컨테이너 오케스트레이터의 역할을 수행합니다. 

![Kubernetes SQL Server 클러스터의 다이어그램](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

위 다이어그램에서 `mssql-server`는 [*Pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod/)의 SQL Server 인스턴스(컨테이너)입니다. [복제본 세트](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)는 노드 실패 후에 Pod가 자동으로 복구되도록 합니다. 애플리케이션이 서비스에 연결됩니다. 이 경우 서비스는 `mssql-server` 실패 후에도 동일하게 유지되는 IP 주소를 호스트하는 부하 분산 장치를 나타냅니다.

Kubernetes는 클러스터의 리소스를 오케스트레이션합니다. SQL Server 인스턴스 컨테이너를 호스트하는 노드가 실패하면 SQL Server 인스턴스가 포함된 새 컨테이너를 부트스트랩하고 동일한 영구적 스토리지에 연결합니다.

SQL Server 2017 이상에서는 Kubernetes의 컨테이너를 지원합니다.

Kubernetes에서 컨테이너를 만들려면 [Kubernetes에 SQL Server 컨테이너 배포](tutorial-sql-server-containers-kubernetes.md)를 참조하세요.

## <a name="a-sql-server-always-on-availability-group-on-sql-server-containers-in-kubernetes"></a>Kubernetes의 SQL Server 컨테이너에 대한 SQL Server Always On 가용성 그룹

SQL Server 2019는 Kubernetes의 컨테이너에 대한 가용성 그룹을 지원합니다. 가용성 그룹에 대해 SQL Server [Kubernetes 연산자](https://coreos.com/blog/introducing-operators.html)를 Kubernetes 클러스터에 배포합니다. 이 연산자는 클러스터에서 SQL Server 인스턴스와 가용성 그룹을 패키지, 배포 및 관리하는 데 유용합니다.

![Kubernetes 컨테이너의 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

위의 그림에서 4개 노드 kubernetes 클러스터는 세 개의 복제본이 있는 가용성 그룹의 호스트입니다. 이 솔루션은 다음 구성 요소를 포함합니다.

* Kubernetes [*배포*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/). 이 배포에는 연산자와 구성 맵이 포함됩니다. 이 배포는 가용성 그룹의 SQL Server 인스턴스를 배포하는 데 필요한 컨테이너 이미지, 소프트웨어 및 지침을 설명합니다.

* 각각 [*StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)를 호스트하는 3개의 노드. StatefulSet는 Pod를 포함합니다. 각 Pod에는 다음이 포함됩니다.
  * SQL Server 인스턴스를 하나 실행하는 SQL Server 컨테이너
  * 가용성 그룹을 관리하는 감독자 `mcr.microsoft.com/mssql/ha`

* 가용성 그룹과 관련된 2개의 [*ConfigMap*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) ConfigMap은 다음에 대한 정보를 제공합니다.
  * 연산자의 배포
  * 가용성 그룹입니다.

 * SQL Server의 각 인스턴스에 대한 영구적 볼륨은 데이터 및 로그 파일용 스토리지를 제공합니다.

또한 클러스터는 암호, 인증서, 키 및 기타 중요한 정보에 대한 [‘비밀’](https://kubernetes.io/docs/concepts/configuration/secret/)을 저장합니다. 

## <a name="compare-sql-server-high-availability-on-containers-with-and-without-the-availability-group"></a>가용성 그룹이 포함된 컨테이너와 포함되지 않은 컨테이너에 대한 SQL Server 고가용성 비교

다음 표에서는 Kubernetes에서 가용성 그룹이 포함된 컨테이너와 포함되지 않은 컨테이너의 SQL Server 고가용성 기능을 비교합니다.

| |가용성 그룹 포함 | 독립 실행형 컨테이너 인스턴스<br/> 가용성 그룹 없음
|:------|:------|:------
|노드 실패에서 자동으로 복구 | 예 | 예
|Pod 실패에서 자동으로 복구 | 예 | 예
|더 빠른 장애 조치(failover) |예 |
|SQL Server 인스턴스 실패에서 자동으로 복구 | 예 | 
|데이터베이스 상태 검사 실패에서 자동으로 복구 | 예 | 
|읽기 전용 복제본 제공 | 예 |
|보조 복제본 백업 | 예 | 
|StatefulSet로 실행 | 예 | 

한 가지 주요 차이점은 컨테이너에서 단일 SQL Server 인스턴스를 사용하는 것보다 가용성 그룹을 사용하는 것이 복구(또는 장애 조치(failover)) 시간이 더 빠릅니다. SQL Server 가용성 그룹이 클러스터에서 다른 노드의 보조 복제본을 유지하기 때문에 이 기능이 향상됩니다. 장애 조치(failover) 시 보조 복제본이 선택되고 주 복제본으로 수준이 올라갑니다. 서비스에 연결된 애플리케이션은 새로운 주 복제본으로 리디렉션됩니다.

가용성 그룹이 없으면 Kubernetes가 장애 조치(failover)를 탐지할 때 컨테이너를 만들고 스토리지에 연결해야 합니다. 그러면 서비스에 연결된 애플리케이션이 다시 연결됩니다. 정확한 장애 조치(failover) 시간은 장애 조치(failover)의 위치 및 탐지 방법에 따라 달라집니다. 

일반적으로 가용성 그룹의 장애 조치(failover) 시간은 초 단위로 측정되는 반면, 단일 인스턴스가 컨테이너를 복구하는 장애 조치(failover) 시간은 최대 10분일 수 있습니다.

## <a name="next-steps"></a>다음 단계

AKS(Azure Kubernetes Service)에 SQL Server 컨테이너를 배포하려면 다음 예제를 참조하세요.

* [Docker 컨테이너에 SQL Server 배포](sql-server-linux-configure-docker.md)
* [Kubernetes에 SQL Server 컨테이너 배포](tutorial-sql-server-containers-kubernetes.md)
* [SQL Server 컨테이너의 Always On 가용성 그룹](sql-server-ag-kubernetes.md)

