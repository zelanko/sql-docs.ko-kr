---
title: 모니터 및 문제 해결하기
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 모니터링 하 고 문제를 해결 하기 위한 유용한 명령을 제공 합니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 272249b7bd6c22895b7d10e7fbce4a20cb647a49
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419474"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>빅 데이터 클러스터 SQL Server 모니터링 및 문제 해결

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 모니터링 하 고 문제를 해결 하는 데 사용할 수 있는 몇 가지 유용한 Kubernetes 명령을 설명 합니다. 빅 데이터 클러스터에 있는 pod 또는 다른 Kubernetes 아티팩트에 대 한 자세한 정보를 보는 방법을 보여 줍니다. 이 문서에서는 SQL Server 빅 데이터 클러스터 서비스 중 하나를 실행 하는 컨테이너에서 파일을 복사 하는 등의 일반적인 작업에 대해서도 설명 합니다.

> [!TIP]
> Windows (cmd 또는 PS) 또는 Linux (bash) 클라이언트 컴퓨터에서 다음 **kubectl** 명령을 실행 합니다. 클러스터의 이전 인증과 실행할 클러스터 컨텍스트를 요구 합니다. 예를 들어 이전에 만든 AKS 클러스터의 경우를 실행 `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` 하 여 Kubernetes 클러스터 구성 파일을 다운로드 하 고 클러스터 컨텍스트를 설정할 수 있습니다.

## <a name="get-status-of-pods"></a>Pod의 상태를 가져옵니다.

`kubectl get pods` 명령을 사용 하 여 클러스터에서 모든 네임 스페이스 또는 빅 데이터 클러스터 네임 스페이스에 대 한 pod 상태를 가져올 수 있습니다. 다음 섹션에서는 두 가지 모두의 예를 보여 줍니다.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Kubernetes 클러스터에 있는 모든 pod의 상태를 표시 합니다.

다음 명령을 실행 하 여 pod 및 해당 상태를 가져옵니다. 여기에는 빅 데이터 클러스터 pod를 만든 SQL Server 네임 스페이스의 일부인 pod 포함 됩니다.

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터에 있는 모든 pod의 상태를 표시 합니다.

`-n` 매개 변수를 사용 하 여 특정 네임 스페이스를 지정 합니다. SQL Server 빅 데이터 클러스터 pod는 배포 구성 파일에 지정 된 클러스터 이름을 기반으로 클러스터 부트스트랩 시간에 생성 된 새 네임 스페이스에 생성 됩니다. 기본 이름인 `mssql-cluster`가 여기에 사용 됩니다.

```bash
kubectl get pods -n mssql-cluster
```

실행 중인 빅 데이터 클러스터에 대 한 다음 목록과 유사한 출력이 표시 됩니다.

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
> 배포 하는 동안 **상태가** **ContainerCreating** 인 pod 계속 됩니다. 어떤 이유로 든 배포가 중단 되 면 문제가 발생할 수 있는 위치를 파악할 수 있습니다. 또한 **준비** 열을 확인 합니다. 이를 통해 pod에서 시작 된 컨테이너의 수를 알 수 있습니다. 배포는 구성 및 네트워크에 따라 30 분 이상 걸릴 수 있습니다. 이 시간의 대부분은 다른 구성 요소에 대 한 컨테이너 이미지를 다운로드 하는 데 소요 됩니다.

## <a name="get-pod-details"></a>Pod 정보 가져오기

다음 명령을 실행 하 여 JSON 형식 출력의 특정 pod에 대 한 자세한 설명을 가져옵니다. 여기에는 pod가 배치 되는 현재 Kubernetes 노드, pod 내에서 실행 중인 컨테이너 및 컨테이너를 부트스트랩 하는 데 사용 되는 이미지와 같은 세부 정보가 포함 됩니다. 또한 pod와 연결 된 레이블, 상태 및 지속형 볼륨 클레임 등의 기타 세부 정보를 보여 줍니다.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

다음 예에서는 라는 `master-0` `mssql-cluster`빅 데이터 클러스터의 pod에 대 한 세부 정보를 보여 줍니다.

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

오류가 발생 한 경우 pod의 최근 이벤트에 오류가 가끔 표시 될 수 있습니다.

## <a name="get-pod-logs"></a>Pod 로그 가져오기

Pod에서 실행 되는 컨테이너에 대 한 로그를 검색할 수 있습니다. 다음 명령은 pod `master-0` 에서 실행 중인 모든 컨테이너의 로그를 검색 하 고 파일 이름 `master-0-pod-logs.txt`으로 출력 합니다.

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a>서비스 상태 가져오기

다음 명령을 실행 하 여 빅 데이터 클러스터 서비스에 대 한 세부 정보를 가져옵니다. 이러한 세부 정보에는 각 서비스 및 포트와 연결 된 형식 및 Ip가 포함 됩니다. SQL Server 빅 데이터 클러스터 서비스는 배포 구성 파일에 지정 된 클러스터 이름을 기반으로 클러스터 부트스트랩 시간에 생성 된 새 네임 스페이스에 만들어집니다.

```bash
kubectl get svc -n <namespace_name>
```

다음 예에서는 라는 `mssql-cluster`빅 데이터 클러스터의 서비스에 대 한 상태를 보여 줍니다.

```bash
kubectl get svc -n mssql-cluster
```

다음 서비스는 빅 데이터 클러스터에 대 한 외부 연결을 지원 합니다.

| 서비스 | 설명 |
|---|---|
| **master-svc-external** | 마스터 인스턴스에 대 한 액세스를 제공 합니다.<br/>(**외부 IP, 31433** 및 **SA** 사용자) |
| **controller-svc-external** | 는 클러스터를 관리 하는 도구 및 클라이언트를 지원 합니다. |
| **gateway-svc-external** | HDFS/Spark 게이트웨이에 대 한 액세스를 제공 합니다.<br/>(**외부 IP** 및 **루트** 사용자) |
| **appproxy-svc-external** | 응용 프로그램 배포 시나리오를 지원 합니다. |

> [!TIP]
> 이는 **kubectl**를 사용 하 여 서비스를 볼 수 있는 방법 이지만 명령을 사용 `azdata bdc endpoint list` 하 여 이러한 끝점을 볼 수도 있습니다. 자세한 내용은 [빅 데이터 클러스터 끝점 가져오기](deployment-guidance.md#endpoints)를 참조 하세요.

## <a name="get-service-details"></a>서비스 세부 정보 가져오기

JSON 형식 출력에서 서비스에 대 한 자세한 설명을 보려면이 명령을 실행 합니다. 레이블, 선택기, IP, 외부 IP (서비스가 LoadBalancer 유형인 경우), 포트 등의 세부 정보가 포함 됩니다.

```bash
kubectl describe service <service_name> -n <namespace_name>
```

다음 예제에서는 **마스터-외부** 서비스에 대 한 세부 정보를 검색 합니다.

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>컨테이너에서 명령 실행

기존 도구나 인프라에서 실제로 컨테이너의 컨텍스트에 있지 않고 특정 작업을 수행할 수 없는 경우 명령을 사용 하 여 `kubectl exec` 컨테이너에 로그인 할 수 있습니다. 예를 들어 특정 파일이 있는지 확인 하거나 컨테이너에서 서비스를 다시 시작 해야 할 수 있습니다. 

`kubectl exec` 명령을 사용 하려면 다음 구문을 사용 합니다.

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

다음 두 섹션에서는 특정 컨테이너에서 명령을 실행 하는 두 가지 예를 제공 합니다.

### <a id="restartsql"></a>특정 컨테이너에 로그인 하 고 SQL Server 프로세스 다시 시작

다음 예제에서는 `mssql-server` `master-0` pod의 컨테이너에서 SQL Server 프로세스를 다시 시작 하는 방법을 보여 줍니다.

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a>특정 컨테이너에 로그인 하 고 컨테이너에서 서비스를 다시 시작 합니다.
 
다음 예에서는 **supervisord**에서 관리 하는 모든 서비스를 다시 시작 하는 방법을 보여 줍니다. 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a>파일 복사

컨테이너에서 로컬 컴퓨터로 파일을 복사 해야 하는 경우 다음 구문을 사용 하 `kubectl cp` 여 명령을 사용 합니다.

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

마찬가지로를 사용 `kubectl cp` 하 여 로컬 컴퓨터에서 특정 컨테이너로 파일을 복사할 수 있습니다.

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a>컨테이너에서 파일 복사

다음 예에서는 컨테이너의 SQL Server 로그 파일을 로컬 컴퓨터의 `~/temp/sqlserverlogs` 경로에 복사 합니다 (이 예제에서는 로컬 컴퓨터가 Linux 클라이언트입니다).

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a>컨테이너에 파일 복사

다음 예제에서는 **AdventureWorks2016CTP3** 파일을 로컬 컴퓨터에서`mssql-server` `master-0` pod의 SQL Server 마스터 인스턴스 컨테이너 ()로 복사 합니다. 파일은 컨테이너의 `/tmp` 디렉터리에 복사 됩니다. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a>Pod 강제 삭제
 
Pod를 강제로 삭제 하는 것은 권장 되지 않습니다. 그러나 가용성, 복원 력 또는 데이터 지 속성을 테스트 하기 위해 pod를 삭제 하 여 `kubectl delete pods` 명령으로 pod 오류를 시뮬레이션할 수 있습니다.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

다음 예제에서는 저장소 풀 pod를 `storage-0-0`삭제 합니다.

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a>Pod IP 가져오기
 
문제 해결을 위해 pod가 현재 실행 되 고 있는 노드의 IP를 가져와야 할 수 있습니다. IP 주소를 가져오려면 다음 구문과 함께 `kubectl get pods` 명령을 사용 합니다.

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

다음 예제에서는 `master-0` pod가 실행 되 고 있는 노드의 IP 주소를 가져옵니다.

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="kubernetes-dashboard"></a>Kubernetes 대시보드

클러스터에 대 한 추가 정보는 Kubernetes 대시보드를 시작할 수 있습니다. 다음 섹션에서는 kubeadm를 사용 하 여 AKS 및 Kubernetes 부트스트랩에 대해 대시보드를 시작 하는 방법을 설명 합니다.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>클러스터가 AKS에서 실행 되는 경우 대시보드 시작

Kubernetes 대시보드 실행을 시작 하려면:

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> 다음 오류가 발생 하는 경우: *8001 포트에서 수신 대기할 수 없습니다. 모든 수신기를 만들지 못했습니다. 다음 오류가 발생 했습니다. 수신기를 만들 수 없습니다. 오류 수신 tcp4 127.0.0.1:8001: > 바인드: 일반적으로 각 소켓 주소 (프로토콜/네트워크 주소/포트)의 사용은 하나만 허용 됩니다. 수신기를 만들 수 없습니다. 오류 수신 tcp6: 주소 [[:: 1]]: 8001: 누락 된 포트 > 주소 오류: 요청 된 포트 [{8001 9090}]* 에서 수신할 수 없습니다. 다른 창에서 대시보드를 아직 시작 하지 않았는지 확인 하세요.

브라우저에서 대시보드를 시작 하면 AKS 클러스터에서 RBAC가 기본적으로 사용 하도록 설정 되어 있고 대시보드에 사용 되는 서비스 계정에 모든 리소스에 액세스할 수 있는 충분 한 권한이 없는 경우 (예:  *pod는 사용할 수 없습니다. 사용자 "system: serviceaccount: kube: kubernetes"는 네임 스페이스 "default"* 에서 pod를 나열할 수 없습니다. 다음 명령을 실행 하 여에 `kubernetes-dashboard`필요한 권한을 부여 하 고 대시보드를 다시 시작 합니다.

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Kubernetes 클러스터가 kubeadm를 사용 하 여 부트스트랩 될 때 대시보드 시작

Kubernetes 클러스터에서 대시보드를 배포 및 구성 하는 방법에 대 한 자세한 지침은 [Kubernetes 설명서](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)를 참조 하세요. Kubernetes 대시보드를 시작 하려면 다음 명령을 실행 합니다.

```bash
kubectl proxy
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [SQL Server 빅 데이터 클러스터 란?](big-data-cluster-overview.md)을 참조 하세요.
