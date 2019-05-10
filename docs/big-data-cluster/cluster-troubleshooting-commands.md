---
title: 모니터 및 문제 해결하기
titleSuffix: SQL Server big data clusters
description: 이 문서에는 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 문제 해결 및 모니터링에 대 한 유용한 명령을 제공 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 51e6f11460e7a7c1f650b68624cc09d7cea76399
ms.sourcegitcommit: 6193aa9b4967302424270d67c27dbc601ca6849a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877659"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>모니터링 및 SQL Server 빅 데이터 클러스터 문제 해결

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 모니터링 하 고 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 문제 해결에 사용할 수 있는 몇 가지 유용한 Kubernetes 명령을 설명 합니다. Pod의 빅 데이터 클러스터에 있는 다른 Kubernetes 아티팩트 자세한 세부 정보를 확인 하는 방법을 보여 줍니다. SQL Server 빅 데이터 클러스터 서비스 중 하나를 실행 하는 컨테이너에서 파일을 복사 하는 등의 일반적인 작업에이 대해서도 설명 합니다.

> [!TIP]
> 다음을 실행 합니다 **kubectl** (cmd 또는 PS) Windows 또는 Linux (bash) 클라이언트 컴퓨터에서 명령을 합니다. 클러스터에 대해 실행할 클러스터 컨텍스트를 이전 인증을 필요로 합니다. 예를 들어, 이전에 만든된 AKS 클러스터를 실행할 수 있습니다 `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` 를 Kubernetes 클러스터 구성 파일을 다운로드 하 여 클러스터 컨텍스트를 설정 합니다.

## <a name="get-status-of-pods"></a>Pod의 상태를 가져옵니다.

사용할 수는 `kubectl get pods` 모든 네임 스페이스 또는 빅 데이터 클러스터 네임 스페이스에 대 한 클러스터의 pod의 상태를 가져오려면 명령입니다. 다음 섹션의 예제를 보여 줍니다.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Kubernetes 클러스터의 모든 pod의 상태를 보여 줍니다.

빅 데이터 클러스터 pod에 생성 되는 SQL Server를 모든 pod 및 네임 스페이스의 일부인 pod를 포함 하 여 해당 상태를 가져오려면 다음 명령을 실행 합니다.

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터의 모든 pod의 상태를 보여 줍니다.

사용 된 `-n` 매개 변수를 특정 네임 스페이스를 지정 합니다. 참고 SQL Server 빅 데이터 클러스터 pod는 배포 구성 파일에 지정 된 클러스터 이름을 기반으로 하는 클러스터 부트스트랩 시에 만들어진 새 네임 스페이스에 생성 됩니다. 기본 이름을 `mssql-cluster`, 여기에 사용 됩니다.

```bash
kubectl get pods -n mssql-cluster
```

실행 빅 데이터 클러스터에 대 한 다음 목록과 유사한 출력이 표시 됩니다.

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
> 배포 하는 동안 사용 하 여 포드를 **상태** 의 **ContainerCreating** 여전히 발생 됩니다. 배포에 어떤 이유로 중지 되는 경우이 수 알 수 있습니다 위치 문제일 수 있습니다. 살펴볼 수도 합니다 **준비** 열입니다. 그러면 pod에 얼마나 많은 컨테이너가 시작 합니다. Note는 배포 구성 및 네트워크에 따라 30 분 이상 걸릴 수 있습니다. 다양 한 구성 요소에 대 한 컨테이너 이미지를 다운로드 하는 데 소요 된이 시간의 대부분입니다.

## <a name="get-pod-details"></a>Pod 세부 정보 가져오기

JSON 출력 형식에서에서 특정 pod에 대 한 자세한 설명을 가져오려면 다음 명령을 실행 합니다. Pod는 pod 및 컨테이너를 부트스트랩 하는 데 사용 된 이미지 내에서 실행 중인 컨테이너에 배치 되는 현재 Kubernetes 노드 같은 세부 정보를 포함 합니다. 또한 레이블, 상태 등의 다른 세부 정보를 표시 하 고 pod와 연관 된 볼륨 클레임을 유지 합니다.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

다음 예제에 대 한 세부 정보를 표시 합니다 `master-0` 빅 데이터 클러스터의 pod `mssql-cluster`:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

오류가 발생 한 경우 때로는 pod에 대 한 최근 이벤트에서 오류를 볼 수 있습니다.

## <a name="get-pod-logs"></a>Pod 로그 가져오기

Pod에서 실행 중인 컨테이너에 대 한 로그를 검색할 수 있습니다. 다음 명령은 명명 된 pod에서 실행 중인 모든 컨테이너에 대 한 로그 검색 `master-0` 파일 이름으로 출력 `master-0-pod-logs.txt`:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a> 서비스의 상태를 가져옵니다.

빅 데이터 클러스터 서비스에 대 한 세부 정보를 가져오려면 다음 명령을 실행 합니다. 해당 서비스 및 포트와 연결 된 Ip 및 이러한 세부 정보에 해당 형식이 포함 됩니다. 참고 SQL Server 빅 데이터 클러스터 서비스는 배포 구성 파일에 지정 된 클러스터 이름을 기반으로 하는 클러스터 부트스트랩 시에 만들어진 새 네임 스페이스에 생성 됩니다.

```bash
kubectl get svc -n <namespace_name>
```

다음 예제에서는 빅 데이터 클러스터에서 서비스에 대 한 상태를 보여 줍니다. `mssql-cluster`:

```bash
kubectl get svc -n mssql-cluster
```

다음 서비스는 빅 데이터 클러스터에 대 한 외부 연결을 지원합니다.

| 서비스 | Description |
|---|---|
| **master-svc-external** | 마스터 인스턴스에 대 한 액세스를 제공합니다.<br/>(**EXTERNAL-IP 31433** 하며 **SA** 사용자) |
| **controller-svc-external** | 도구 및 클러스터를 관리 하는 클라이언트를 지원 합니다. |
| **mgmtproxy-svc-external** | 에 대 한 액세스를 제공 합니다 [클러스터 관리 포털](cluster-admin-portal.md)합니다.<br/>(https://**EXTERNAL-IP**: 30777/포털) |
| **gateway-svc-external** | HDFS/Spark gateway에 대 한 액세스를 제공합니다.<br/>(**EXTERNAL-IP** 하며 **루트** 사용자) |
| **appproxy-svc-external** | 응용 프로그램 배포 시나리오를 지원 합니다. |

> [!TIP]
> 이 사용 하 여 서비스를 표시 하는 방법 **kubectl**를 사용 하 여도 가능 하지만 `mssqlctl cluster endpoints list` 이러한 끝점을 보려면 명령입니다. 자세한 내용은 [빅 데이터 클러스터 끝점 가져오기](deployment-guidance.md#endpoints)합니다.

## <a name="get-service-details"></a>서비스 세부 정보 가져오기

JSON 출력 형식에에서는 서비스에 대 한 자세한 설명을 가져오기 위해이 명령을 실행 합니다. 세부 정보가 포함 됩니다 것 같은 레이블, 선택기 IP, 외부 IP (서비스 LoadBalancer 형식인 경우), 포트, 등입니다.

```bash
kubectl describe service <service_name> -n <namespace_name>
```

다음 예제에 대 한 세부 정보를 검색 합니다 **마스터 svc 외부** 서비스:

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>컨테이너에서 명령 실행된

기존 도구 또는 인프라 없이 실제로 컨테이너의 컨텍스트에서 특정 작업을 수행할 수 있습니다 설정 되지 않으면, 로그인 할 수 있습니다 사용 하 여 컨테이너 `kubectl exec` 명령입니다. 예를 들어, 특정 파일이 있는 경우 또는 컨테이너의 서비스를 다시 시작 해야 할 수 있습니다를 확인 해야 합니다. 

사용 하는 `kubectl exec` 명령에 다음 구문을 사용 합니다.

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

다음 두 섹션에서는 특정 컨테이너에서 명령을 실행 하는 두 가지 예제를 제공 합니다.

### <a id="restartsql"></a> 특정 컨테이너에 로그인 하 고 SQL Server 프로세스를 다시 시작

다음 예제에서는 SQL Server 프로세스를 다시 시작 하는 방법을 보여 줍니다 합니다 `mssql-server` 컨테이너에는 `master-0` pod:

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a> 특정 컨테이너에 로그인 하 고 컨테이너에 서비스를 다시 시작
 
다음 예제에서 관리 하는 모든 서비스를 다시 시작 하는 방법을 보여 줍니다 **supervisord를 사용**: 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a> 파일 복사

사용 하 여 로컬 컴퓨터에 컨테이너에서 파일을 복사 해야 할 경우 `kubectl cp` 다음 구문을 사용 하 여 명령:

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

마찬가지로, 사용할 수 있습니다 `kubectl cp` 특정 컨테이너에 로컬 컴퓨터에서 파일을 복사 합니다.

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a> 컨테이너에서 파일을 복사 합니다.

다음 예제에서는 컨테이너에서 SQL Server 로그 파일을 복사 합니다 `~/temp/sqlserverlogs` 이 예에서는 로컬 컴퓨터는 Linux 클라이언트 컴퓨터의 로컬 경로:

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> 컨테이너에 파일을 복사 합니다.

다음 예제에서는 복사 합니다 **AdventureWorks2016CTP3.bak** SQL Server 마스터 인스턴스 컨테이너에 로컬 컴퓨터에서 파일 (`mssql-server`)에 `master-0` pod입니다. 파일에 복사 됩니다는 `/tmp` 컨테이너의 디렉터리입니다. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a> Pod 강제 삭제
 
Pod 강제로 삭제 하는 권장 되지 않습니다. 가용성, 복원 력 또는 데이터 지 속성 테스트를 사용 하 여 pod 실패를 시뮬레이션 하는 pod를 삭제할 수 있습니다 하지만 `kubectl delete pods` 명령입니다.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

다음 예제에서는 저장소 풀 pod를 삭제 `storage-0-0`:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a> Pod IP 가져오기
 
문제 해결을 위해 pod에서 현재 실행 중인 노드의 IP 가져오기 해야 합니다. IP 주소를 확인 하려면 사용 된 `kubectl get pods` 다음 구문을 사용 하 여 명령:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

다음 예제에서는 노드의 IP 주소를 가져옵니다는 `master-0` pod에서 실행 되 고:

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="cluster-administration-portal"></a>클러스터 관리 포털

사용 된 [클러스터 관리 포털](cluster-admin-portal.md) 빅 데이터 클러스터의 상태를 모니터링할 수 있습니다. 예를 들어, 배포 하는 동안 사용할 수는 **배포** 탭 합니다. 기다릴 필요가 합니다 **mgmtproxy svc 외부** 서비스를 배포의 시작 부분에 사용할 수 없게 되므로이 포털에 액세스 하기 전에 시작 합니다.

## <a name="kubernetes-dashboard"></a>Kubernetes 대시보드

클러스터에 대 한 추가 정보에 대 한 Kubernetes 대시보드를 시작할 수 있습니다. 다음 섹션에서는 AKS에서 Kubernetes에 대 한 및 부트스트랩 kubeadm를 사용 하 여 kubernetes 대시보드를 시작 하는 방법에 설명 합니다.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>AKS에서 클러스터가 실행 되는 경우 대시보드 시작

실행 하 여 Kubernetes 대시보드를 시작 합니다.

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> 다음 오류가 발생 하면: *포트 8001에서 수신 대기할 수 없습니다. 모든 수신기는 다음 오류와 함께 만들지 못했습니다. 수신기를 만들 수 없습니다. 오류가 수신 tcp4 127.0.0.1:8001: > 바인딩: 각 소켓 주소 (프로토콜/네트워크 주소/포트) 하나만 사용은 일반적으로 허용 됩니다. 수신기를 만들 수 없습니다. 오류 tcp6 수신: 주소 [[:: 1]]: 8001: 포트에서 누락 > 오류를 해결 합니다. 요청 된 포트에서 수신 대기할 없습니다: [{8001 9090}]*, 사용자가 시작 하지 대시보드에 이미 다른 창에서 있는지 확인 합니다.

브라우저에서 대시보드를 시작, AKS 클러스터에서 기본적으로 사용 되는 RBAC로 인해 권한 경고가 표시 될 수 있습니다 및 대시보드에 사용 되는 서비스 계정에 모든 리소스에 액세스할 수 있는 권한이 없는 경우 (예를 들어  *pod는 사용할 수 없음: 사용자 "시스템: serviceaccount:kube-시스템: kubernetes-대시보드" "default" 네임 스페이스의 pod를 나열할 수 없습니다.*). 에 필요한 권한을 부여 하려면 다음 명령을 실행 `kubernetes-dashboard`, 고 대시보드를 다시 시작 합니다.

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Kubeadm를 사용 하 여 Kubernetes 클러스터 부트스트랩 되 면 대시보드 시작

에 대 한 자세한 지침 배포, Kubernetes 클러스터에 대시보드를 구성할를 참조 하는 방법 [Kubernetes 설명서](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)합니다. Kubernetes 대시보드를 시작 하려면이 명령을 실행 합니다.

```bash
kubectl proxy
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 참조 하십시오 [SQL Server 빅 데이터 클러스터 이란](big-data-cluster-overview.md)합니다.
