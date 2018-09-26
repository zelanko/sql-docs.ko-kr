---
title: SQL Server 컨테이너에 대 한 고가용성
description: 이 문서에서는 SQL Server 컨테이너에 대 한 고가용성을 소개합니다.
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
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 13c48bf8b5edefbfd86855197128abfd5674067e
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715163"
---
# <a name="high-availability-for-sql-server-containers"></a>SQL Server 컨테이너에 대 한 고가용성

Kubernetes에서 기본적으로 SQL Server 인스턴스를 만들고 설정 합니다.

SQL Server에서 관리 하는 docker 컨테이너 배포 [Kubernetes](https://kubernetes.io/)합니다. Kubernetes 클러스터 노드가 실패 하는 경우에 자동으로 SQL Server 인스턴스를 사용 하 여 컨테이너를 복구할 수 있습니다. 더 강력한 가용성에 대 한 Kubernetes 클러스터에 컨테이너의 SQL Server 인스턴스를 사용 하 여 SQL Server Always On 가용성 그룹을 구성 합니다. 이 문서에서는 두 가지 솔루션을 비교 합니다.

## <a name="compare-sql-server-versions-on-kubernetes"></a>Kubernetes의 SQL Server 버전 비교

SQL Server 2017 Kubernetes에 배포할 수 있는 Docker 이미지를 제공 합니다. PVC ()는 Kubernetes 영구적 볼륨 클레임을 사용 하 여 이미지를 구성할 수 있습니다. Kubernetes는 컨테이너에서 SQL Server 프로세스를 모니터링합니다. 프로세스, pod, 컨테이너 또는 노드 실패, Kubernetes는 자동으로 다른 인스턴스를 부트스트랩 하 고 저장소에 다시 연결 합니다.

SQL Server 2019 Kubernetes StatefulSet를 사용 하 여 더 강력한 archicture를 소개합니다. 따라서 Kubernetes에서를 컨테이너 이미지를 SQL Server Always On 가용성 그룹에 참여할 수 있는 SQL Server의 인스턴스를 오케스트레이션 할 수 있습니다. 이렇게 향상 된 상태 모니터링, 빠른 복구를 제공, 백업을 오프 로드 하 고 읽기 크기 조정.  

## <a name="container-with-sql-server-instance-on-kubernetes"></a>Kubernetes 인스턴스에서 SQL Server를 사용 하 여 컨테이너

Kubernetes 버전 1.6 이상에 대 한 지원 [ *저장소 클래스*](http://kubernetes.io/docs/concepts/storage/storage-classes/)에 [ *영구적 볼륨 클레임*](http://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims), 및 [  *Azure 디스크 볼륨 유형을*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)합니다. 

이 구성에서는 Kubernetes 컨테이너 오 케 스트레이 터의 역할을 재생합니다. 

![Kubernetes SQL Server 클러스터의 다이어그램](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

위의 다이어그램에서 `mssql-server` SQL Server 인스턴스 (컨테이너)에 [ *pod*](http://kubernetes.io/docs/concepts/workloads/pods/pod/)합니다. A [복제본 세트](http://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) pod가 노드 실패 후 자동으로 복구 하 고 있는지 확인 합니다. 응용 프로그램 서비스에 연결 합니다. 이 경우 서비스를 나타내는 실패 후에 동일 하 게 유지 하는 IP 주소를 호스트 하는 부하 분산 장치는 `mssql-server`합니다.

Kubernetes는 클러스터의 리소스를 조정합니다. Pod 또는 컨테이너에서 SQL Server 인스턴스를 호스트 하는 노드 실패 하면는 오 케 스트레이 터 SQL Server 인스턴스와 동일한 포드를에서 컨테이너를 부트스트랩 하 고 같은 영구 저장소에 연결 합니다.

SQL Server 2017 및 이후 Kubernetes에서 컨테이너를 지원 합니다.

Kubernetes에서 컨테이너를 만들려고 참조 [Kubernetes에서 SQL Server 컨테이너를 배포 합니다.](tutorial-sql-server-containers-kubernetes.md)

## <a name="a-sql-server-always-on-availability-group-on-sql-server-containers-in-kubernetes"></a>Kubernetes에서 SQL Server 컨테이너에서 SQL Server Always On 가용성 그룹

SQL Server 2019 Kubernetes에서 컨테이너에 대 한 가용성 그룹을 지원합니다. 가용성 그룹에 대 한 SQL Server를 배포 [Kubernetes 연산자](http://coreos.com/blog/introducing-operators.html) Kubernetes 클러스터에 있습니다. 연산자에는 패키지를 배포 하 고 SQL Server 인스턴스 및 클러스터에서 가용성 그룹을 관리할 수 있습니다.

![Kubernetes 컨테이너에서 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

위의 이미지에서 4 개 노드 kubernetes 클러스터를 세 개의 복제본을 사용 하 여 가용성 그룹을 호스팅합니다. 다음 구성 요소를 포함 하는 솔루션:

* Kubernetes [ *배포*](http://kubernetes.io/docs/concepts/workloads/controllers/deployment/)합니다. 배포 구성 맵과 연산자를 포함합니다. 이러한 컨테이너 이미지, 소프트웨어 및 가용성 그룹에 대 한 SQL Server 인스턴스를 배포 하는 데 필요한 지침을 제공 합니다.

* 세 개의 노드를 호스팅하는 [ *StatefulSet*](http://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)합니다. StatefulSet의 pod를 포함합니다. 각 pod에는 다음이 포함 됩니다.
  * SQL Server 인스턴스를 실행 하는 SQL Server 컨테이너입니다.
  * 감독자 `mcr.microsoft.com/mssql/ha` 가용성 그룹을 관리할 수 있습니다.

* 두 개의 [ *ConfigMaps* ](http://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) 가용성 그룹과 관련 됩니다. ConfigMaps에 대 한 정보를 제공합니다.
  * 연산자에 대 한 배포 합니다.
  * 가용성 그룹입니다.

 * SQL Server의 각 인스턴스에 대 한 영구 볼륨의 데이터 및 로그 파일에 대 한 저장소를 제공합니다.

또한 클러스터 저장 [ *비밀* ](http://kubernetes.io/docs/concepts/configuration/secret/) 암호, 인증서, 키 및 기타 중요 한 정보에 대 한 합니다.

## <a name="compare-sql-server-high-availabiltiy-on-containers-with-and-without-the-availability-group"></a>SQL Server 가용성 그룹 없이 컨테이너를에서 높은 가용성을 비교 합니다.

다음 테이블 compairs 가용성 그룹을 하지 않고, Kubernetes에서 컨테이너에서 SQL Server 고가용성 기능:

| |가용성 그룹을 사용 하 여 | 독립 실행형 컨테이너 인스턴스<br/> 가용성 그룹 없음
|:------|:------|:------
|노드 실패에서 자동으로 복구 | 사용자 계정 컨트롤 | 사용자 계정 컨트롤
|자동으로 pod 오류 로부터 복구 | 사용자 계정 컨트롤 | 사용자 계정 컨트롤
|보다 빠르게 장애 조치할 |사용자 계정 컨트롤 |
|자동으로 SQL Server 인스턴스 오류 복구 | 사용자 계정 컨트롤 | 
|데이터베이스 상태 확인 실패에서 자동으로 복구 | 사용자 계정 컨트롤 | 
|읽기 전용 복제본을 제공 합니다. | 사용자 계정 컨트롤 |
|보조 복제본에 백업 | 사용자 계정 컨트롤 | 
|StatefulSet으로 실행 | 사용자 계정 컨트롤 | 

하나 주요 차이점은 복구 (또는 장애 조치)에 컨테이너에서 SQL Server의 단일 인스턴스를 사용 하 여 가용성 그룹이 보다 빠릅니다. SQL Server 가용성 그룹 클러스터의 다른 노드에서 가용성 그룹 데이터베이스의 보조 복제본을 유지 하는 때문입니다. 장애 조치를 보조 복제본 선택 되 고 기본으로 승격 합니다. 서비스에 연결 하는 응용 프로그램은 새로운 주 복제본으로 리디렉션됩니다. 

가용성 그룹을 Kubernetes에서 장애 조치를 감지 하면 컨테이너를 만들고, 저장소에 연결 해야 하지 않고 서비스에 연결 하는 응용 프로그램 다시 연결 합니다. 정확 하 게 장애 조치 시간을 장애 조치가 및 감지 된 방법에 따라 달라 집니다. 

일반적으로 컨테이너를 복구 하려면 단일 인스턴스에 대 한 장애 조치에 최대 10 분 동안 가용성 그룹에 대 한 장애 조치 시간을 초 단위로 측정 됩니다.

## <a name="next-steps"></a>다음 단계

Azure Kubernetes Service (AKS)에서 SQL Server 컨테이너를 배포 하려면 다음이 자습서 중 하나를 수행 합니다.

* [Docker 컨테이너에서 SQL Server 배포](sql-server-linux-configure-docker.md)
* [Kubernetes에서 SQL Server 컨테이너를 배포 합니다.](tutorial-sql-server-containers-kubernetes.md)
* [SQL Server Always On 가용성 그룹을 Kubernetes 배포](tutorial-sql-server-ag-kubernetes.md)

