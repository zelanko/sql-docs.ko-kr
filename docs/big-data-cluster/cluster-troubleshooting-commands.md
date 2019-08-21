---
title: 모니터 및 문제 해결하기
titleSuffix: SQL Server big data clusters
description: 이 문서에서는의 모니터링 및 문제 해결 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]을 위한 유용한 명령을 제공 합니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 36203552e9070d80179fa88df0a7d1951b09664a
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653029"
---
# <a name="monitoring-and-troubleshoot-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>모니터링 및 문제 해결[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는를 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]모니터링 하 고 문제를 해결 하는 데 사용할 수 있는 몇 가지 유용한 Kubernetes 명령을 설명 합니다. 빅 데이터 클러스터에 있는 Pod 또는 다른 Kubernetes 아티팩트에 대한 자세한 정보를 보는 방법을 보여 줍니다. 이 문서에서는 SQL Server 빅 데이터 클러스터 서비스 중 하나를 실행하는 컨테이너에(서) 파일 복사 등의 일반적인 작업에 대해서도 설명합니다.

> [!TIP]
> Windows(cmd 또는 PS) 또는 Linux(bash) 클라이언트 머신에서 다음 **kubectl** 명령을 실행합니다. 명령이 제대로 실행되려면 클러스터 내의 이전 인증과 명령을 실행할 클러스터 컨텍스트가 필요합니다. 예를 들어 이전에 만든 AKS 클러스터의 경우 `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>`을 실행하여 Kubernetes 클러스터 구성 파일을 다운로드하고 클러스터 컨텍스트를 설정할 수 있습니다.

## <a name="get-status-of-pods"></a>Pod 상태 가져오기

`kubectl get pods` 명령을 사용하여 클러스터에서 모든 네임스페이스 또는 빅 데이터 클러스터 네임스페이스의 Pod 상태를 가져올 수 있습니다. 다음 섹션에서는 두 가지 예제를 모두 보여 줍니다.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Kubernetes 클러스터의 모든 Pod 상태 표시

다음 명령을 실행하여 SQL Server 빅 데이터 클러스터 Pod가 생성된 네임스페이스의 Pod를 포함하여 모든 Pod와 해당 상태를 가져옵니다.

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터의 모든 Pod 상태 표시

`-n` 매개 변수를 사용하여 특정 네임스페이스를 지정합니다. SQL Server 빅 데이터 클러스터 Pod는 배포 구성 파일에 지정된 클러스터 이름을 기준으로 클러스터 부트스트랩 시 생성된 새 네임스페이스에 생성됩니다. 여기서는 기본 이름인 `mssql-cluster`를 사용합니다.

```bash
kubectl get pods -n mssql-cluster
```

실행 중인 빅 데이터 클러스터에 대한 출력이 다음 목록과 같이 표시됩니다.

```output
PS C:\> kubectl get pods -n mssql-cluster
NAME              READY   STATUS    RESTARTS   AGE
appproxy-f2qqt    2/2     Running   0          110m
compute-0-0       3/3     Running   0          110m
control-zlncl     4/4     Running   0          118m
data-0-0          3/3     Running   0          110m
data-0-1          3/3     Running   0          110m
gateway-0         2/2     Running   0          109m
logsdb-0          1/1     Running   0          112m
logsui-jtdnv      1/1     Running   0          112m
master-0          7/7     Running   0          110m
metricsdb-0       1/1     Running   0          112m
metricsdc-shv2f   1/1     Running   0          112m
metricsui-9bcj7   1/1     Running   0          112m
mgmtproxy-x6gcs   2/2     Running   0          112m
nmnode-0-0        1/1     Running   0          110m
storage-0-0       7/7     Running   0          110m
storage-0-1       7/7     Running   0          110m
```

> [!NOTE]
> 배포 중에는 **STATUS**가 **ContainerCreating**인 Pod도 표시됩니다. 어떤 이유로든 배포가 중단되면 이 목록을 통해 문제가 발생한 위치를 파악할 수 있습니다. **READY** 열도 확인합니다. 이 열을 통해 Pod에서 시작된 컨테이너 수를 파악할 수 있습니다. 구성 및 네트워크에 따라 배포를 완료하는 데 30분 이상 걸릴 수 있습니다. 이 시간의 대부분은 다양한 구성 요소의 컨테이너 이미지를 다운로드하는 데 사용됩니다.

## <a name="get-pod-details"></a>Pod 정보 가져오기

다음 명령을 실행하여 특정 Pod에 대한 자세한 설명을 JSON 형식 출력으로 가져옵니다. 여기에는 Pod가 배치된 현재 Kubernetes 노드, Pod 내에서 실행 중인 컨테이너, 컨테이너를 부트스트랩하는 데 사용된 이미지 등의 세부 정보가 포함됩니다. 레이블, 상태, Pod와 연결된 영구적 볼륨 클레임 등의 기타 세부 정보도 표시됩니다.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

다음 예제에서는 `mssql-cluster`라는 빅 데이터 클러스터의 `master-0` Pod에 대한 세부 정보를 표시합니다.

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

오류가 발생한 경우 Pod의 최근 이벤트에 오류가 표시되는 경우도 있습니다.

## <a name="get-pod-logs"></a>Pod 로그 가져오기

Pod에서 실행되는 컨테이너의 로그를 검색할 수 있습니다. 다음 명령은 `master-0`이라는 Pod에서 실행되는 모든 컨테이너의 로그를 검색하고 파일 이름 `master-0-pod-logs.txt`로 출력합니다.

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluster > master-0-pod-logs.txt
```

## <a id="services"></a> 서비스 상태 가져오기

다음 명령을 실행하여 빅 데이터 클러스터 서비스의 세부 정보를 가져옵니다. 이러한 세부 정보에는 각 서비스 및 포트와 연결된 유형 및 ID가 포함됩니다. SQL Server 빅 데이터 클러스터 서비스는 배포 구성 파일에 지정된 클러스터 이름을 기준으로 클러스터 부트스트랩 시 생성된 새 네임스페이스에 생성됩니다.

```bash
kubectl get svc -n <namespace_name>
```

다음 예제에서는 `mssql-cluster`라는 빅 데이터 클러스터의 서비스 상태를 표시합니다.

```bash
kubectl get svc -n mssql-cluster
```

다음 서비스는 빅 데이터 클러스터에 대한 외부 연결을 지원합니다.

| 서비스 | 설명 |
|---|---|
| **master-svc-external** | 마스터 인스턴스에 대한 액세스를 제공합니다.<br/>(**EXTERNAL-IP,31433** 및 **SA** 사용자) |
| **controller-svc-external** | 클러스터를 관리하는 도구 및 클라이언트를 지원합니다. |
| **gateway-svc-external** | HDFS/Spark 게이트웨이에 대한 액세스를 제공합니다.<br/>(**EXTERNAL-IP** 및 **root** 사용자) |
| **appproxy-svc-external** | 애플리케이션 배포 시나리오를 지원합니다. |

> [!TIP]
> 이 방법으로 **kubectl**을 사용하여 서비스를 볼 수 있지만, `azdata bdc endpoint list` 명령을 사용하여 해당 엔드포인트를 볼 수도 있습니다. 자세한 내용은 [빅 데이터 클러스터 엔드포인트 가져오기](deployment-guidance.md#endpoints)를 참조하세요.

## <a name="get-service-details"></a>서비스 정보 가져오기

다음 명령을 실행하여 서비스에 대한 자세한 설명을 JSON 형식 출력으로 가져옵니다. 여기에는 레이블, 선택기, IP, 외부 IP(서비스가 LoadBalancer 유형인 경우), 포트 등의 세부 정보가 포함됩니다.

```bash
kubectl describe service <service_name> -n <namespace_name>
```

다음 예제에서는 **master-svc-external** 서비스의 세부 정보를 검색합니다.

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a id="copy"></a> 파일 복사

컨테이너에서 로컬 머신으로 파일을 복사해야 하는 경우 다음 구문으로 `kubectl cp` 명령을 사용합니다.

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

마찬가지로, `kubectl cp`를 사용하여 로컬 머신에서 특정 컨테이너로 파일을 복사할 수 있습니다.

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a> 컨테이너에서 파일 복사

다음 예제에서는 컨테이너에서 로컬 머신(이 예제에서 로컬 머신은 Linux 클라이언트임)의 `~/temp/sqlserverlogs` 경로로 SQL Server 로그 파일을 복사합니다.

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> 컨테이너에 파일 복사

다음 예제에서는 로컬 머신에서 `master-0` Pod의 SQL Server 마스터 인스턴스 컨테이너(`mssql-server`)로 **AdventureWorks2016CTP3** 파일을 복사합니다. 파일은 컨테이너의 `/tmp` 디렉터리에 복사됩니다. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a> Pod 강제 삭제
 
Pod를 강제로 삭제하는 것은 권장되지 않습니다. 그러나 가용성, 복원력 또는 데이터 지속성을 테스트하기 위해 `kubectl delete pods` 명령을 통해 Pod를 삭제하여 Pod 오류를 시뮬레이트할 수 있습니다.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

다음 예제에서는 스토리지 풀 Pod `storage-0-0`을 삭제합니다.

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a> Pod IP 가져오기
 
문제 해결을 위해 Pod가 현재 실행되고 있는 노드의 IP를 가져와야 할 수도 있습니다. IP 주소를 가져오려면 다음 구문으로 `kubectl get pods` 명령을 사용합니다.

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

다음 예제에서는 `master-0` Pod가 실행되는 노드의 IP 주소를 가져옵니다.

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="kubernetes-dashboard"></a>Kubernetes 대시보드

클러스터에 대한 추가 정보를 보기 위해 Kubernetes 대시보드를 시작할 수 있습니다. 다음 섹션에서는 kubeadm을 사용하여 부트스트랩된 Kubernetes 및 AKS의 Kubernetes에 대한 대시보드를 시작하는 방법을 설명합니다.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>클러스터가 AKS에서 실행되는 경우 대시보드 시작

Kubernetes 대시보드를 시작하려면 다음 명령을 실행합니다.

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> 다음 오류가 표시되는 경우 ‘포트 8001에서 수신 대기할 수 없습니다. 다음 오류가 발생하여 모든 수신기를 만들지 못했습니다. 수신기를 만들 수 없습니다. 오류 listen tcp4 127.0.0.1:8001: >bind: 각 소켓 주소(프로토콜/네트워크 주소/포트)는 한 가지 사용만 허용됩니다. 수신기를 만들 수 없습니다. 오류 listen tcp6: address [[::1]]:8001: missing port in >address error: 요청된 포트에서 수신 대기할 수 없습니다. [{8001 9090}]’, 다른 창에서 해당 대시보드를 이미 시작하지 않았는지 확인합니다.*

브라우저에서 대시보드를 시작하면 AKS 클러스터에서 RBAC가 기본적으로 사용하도록 설정되고 대시보드에서 사용되는 서비스 계정에 모든 리소스에 액세스할 수 있는 권한이 없기 때문에 사용 권한 경고가 표시될 수 있습니다. 예를 들어 ‘Pod를 사용할 수 없습니다. 사용자 “system:serviceaccount:kube-system:kubernetes-dashboard”는 “default” 네임 스페이스의 Pod를 나열할 수 없습니다.’가 표시됩니다.* 다음 명령을 실행하여 `kubernetes-dashboard`에 필요한 사용 권한을 부여하고 대시보드를 다시 시작합니다.

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Kubernetes 클러스터가 kubeadm을 사용하여 부트스트랩된 경우 대시보드 시작

Kubernetes 클러스터에 대시보드를 배포하고 구성하는 방법에 대한 자세한 내용은 [Kubernetes 설명서](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)를 참조하세요. Kubernetes 대시보드를 시작하려면 다음 명령을 실행합니다.

```bash
kubectl proxy
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [항목 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](big-data-cluster-overview.md)을 참조 하세요.
