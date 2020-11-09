---
title: AD 모드 배포 중단 - 비정상 `sparkhead` Pod
titleSuffix: SQL Server Big Data Cluster
description: 비정상 `sparkhead` Pod가 있는 Active Directory 도메인에서 SQL Server 빅 데이터 클러스터의 응답하지 않는 배포 문제를 해결합니다.
author: macarv-ms
ms.author: macarv
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e23d45f9083e8acf1f8e889cda845b36eef087ee
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364505"
---
# <a name="ad-mode-deployment-hangs---unhealthy-sparkhead-pods"></a>AD 모드 배포 중단 - 비정상 `sparkhead` Pod

AD(Active Directory) 모드에서 배포가 중지됩니다. 증상을 검사하여 클러스터 노드의 다른 네트워크에 도메인 컨트롤러의 역방향 조회 영역 항목이 없는 것이 원인인지 확인합니다.

## <a name="symptom"></a>증상

AD 모드로 BDC 배포를 시작했지만 배포가 중단되어 더 이상 진행되지 않습니다.

다음 예제에서는 bash 셸에서의 배포 결과를 보여 줍니다.

```output
Starting cluster deployment.
Waiting for cluster controller to start.
Waiting for cluster controller to start.
Waiting for cluster controller to start.
Waiting for cluster controller to start.
Waiting for cluster controller to start.
Cluster controller endpoint is available at bdc-control.corpnet.contoso.com:30080, 10.166.6.77:30080.
Waiting for control plane to be ready after 5 minutes.
Cluster control plane is ready.
Cluster is not ready after 15 minutes. Check controller logs for more details.
Data pool is ready.
Storage pool is ready.
Compute pool is ready.
Master pool is ready.
Cluster is not ready after 30 minutes. Check controller logs for more details.
...
...
```

현재 배포된 Pod를 확인합니다.

```bash
kubectl get pods -n mssql-cluster
```

결과를 통해 모든 Pod가 배포되었지만 배포에서 성공을 보고하지 않음을 알 수 있습니다.

```output
NAME              READY   STATUS    RESTARTS   AGE 
appproxy-c7f2l    2/2     Running   0          3d13h 
compute-0-0       3/3     Running   0          3d13h 
control-88dgt     3/3     Running   0          3d13h 
controldb-0       2/2     Running   0          3d13h 
controlwd-zzkxz   1/1     Running   0          3d13h 
data-0-0          3/3     Running   0          3d13h 
data-0-1          3/3     Running   0          3d13h 
dns-xkdhh         2/2     Running   0          3d13h 
gateway-0         2/2     Running   0          3d13h 
logsdb-0          1/1     Running   0          3d13h 
logsui-qz8qq      1/1     Running   0          3d13h 
master-0          4/4     Running   0          3d13h 
master-1          4/4     Running   0          3d13h 
master-2          4/4     Running   0          3d13h 
metricsdb-0       1/1     Running   0          3d13h 
metricsdc-xezf7   1/1     Running   0          3d13h 
metricsdc-qdjkh   1/1     Running   0          3d13h 
metricsui-mr34w   1/1     Running   0          3d13h 
mgmtproxy-kz5gg   2/2     Running   0          3d13h 
nmnode-0-0        2/2     Running   1          3d13h 
nmnode-0-1        2/2     Running   0          3d13h 
operator-42ffv    1/1     Running   0          3d13h 
sparkhead-0       4/4     Running   0          3d13h 
sparkhead-1       4/4     Running   0          3d13h 
storage-0-0       4/4     Running   0          3d13h 
storage-0-1       4/4     Running   0          3d13h 
storage-0-2       4/4     Running   0          3d13h 
zookeeper-0       2/2     Running   0          3d13h 
zookeeper-1       2/2     Running   0          3d13h 
zookeeper-2       2/2     Running   0          3d13h 
```

HDFS 및 Spark 서비스의 상태를 검사합니다. `sparkhead` Pod 오류를 찾습니다.

## <a name="check-the-hdfs-and-spark-services"></a>HDFS 및 Spark 서비스 확인 

ADS(Azure Data Studio)에서 컨트롤러에 연결한 후 빅 데이터 클러스터 대시보드를 확인합니다. HDFS 및 Spark 서비스 둘 다에 비정상 `sparkhead` Pod가 있는지 확인합니다.

![HDFS Spark 서비스의 비정상 ‘sparkhead’ Pod](./media/troubleshoot-ad-hung-deployment-unhealthy-sparkhead-pods/hdfs_spark_unhealthy_sparkhead_pods.png)

로그를 추출한 후 다음 로그를 찾습니다.

`\mssql-cluster\control-<identifier>\controller\control-<identifier>-controller-stdout.log`.

> [!TIP]
> 로그를 수집하는 방법은 여러 가지가 있습니다. [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]를 사용하여 로그를 복사하는 대신 Azure Data Studio에서 노트북을 사용할 수 있습니다.
> Azure Data Studio에서 Kubernetes 클러스터에 연결하고 적절한 문제 해결 노트북을 실행합니다. 노트북의 예는 다음과 같습니다.
>
> - TSG027 - 클러스터 배포 관찰
> - TSG061 - BDC 네임스페이스의 Pod에 대한 모든 컨테이너 로그의 끝부분 가져오기
> - TSG001 - `azdata copy-logs` 실행
>
  
## <a name="inspect-the-logs"></a>로그를 검사합니다.

로그를 찾습니다. 다음 예제에서는 컨트롤러 배포 로그를 가리킵니다.

`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-YYYYMMDD-HHMMSS\<namespace>\control-<identifier>\controller\control-<identifier>-controller-stdout.log`

```output
StatefulSet sparkhead is not healthy: 
{{Pod sparkhead-0 is unhealthy: 
{Container hadoop-yarn-jobhistory is unhealthy: 
{Found error properties: 
{Property: jobhistoryserver.readiness, Details: 'Health module returned error state. error: Head https://sparkhead-0.corpnet.contoso.com:19888/ws/v1/history: dial tcp 10.244.2.33:19888: connect: connection refused'}}} 
{Container hadoop-livy-sparkhistory is unhealthy: 
{Found error properties: 
{Property: sparkhistory.readiness, Details: 'Health module returned error state. error: Head https://sparkhead-0.corpnet.contoso.com:18480: dial tcp 10.244.2.33:18480: connect: connection refused'}}}, 
{Container hadoop-hivemetastore is unhealthy: 
{Found error properties: 
{Property: hivemetastorehttp.readiness, Details: 'Health module returned error state. error: Post https://sparkhead-0.corpnet.contoso.com:9084/api/hms: dial tcp 10.244.2.33:9084: connect: connection refused'}}}}}, 
  
{{Pod sparkhead-1 is unhealthy: 
{Container hadoop-yarn-jobhistory is unhealthy: 
{Found error properties: 
{Property: jobhistoryserver.readiness, Details: 'Health module returned error state. error: Head https://sparkhead-1.corpnet.contoso.com:19888/ws/v1/history: dial tcp 10.244.1.24:19888: connect: connection refused'}}}, 
{Container hadoop-livy-sparkhistory is unhealthy: 
{Found error properties: 
{Property: sparkhistory.readiness, Details: 'Health module returned error state. error: Head https://sparkhead-1.corpnet.contoso.com:18480: dial tcp 10.244.1.24:18480: connect: connection refused'}}}, 
{Container hadoop-hivemetastore is unhealthy: 
{Found error properties: 
{Property: hivemetastorehttp.readiness, Details: 'Health module returned error state. error: Post https://sparkhead-1.corpnet.contoso.com:9084/api/hms: dial tcp 10.244.1.24:9084: connect: connection refused'}}}}} 
```

컨테이너 로그에 주의하여 `sparkhead` Pod를 검사합니다. 이 예제에서는 `sparkhead-0`을 살펴봅니다.

```output
sparkhead-0\hadoop-hivemetastore\supervisor\log\hivemetastorehttp-stderr---supervisor-pZ1gdb 
  
YYYY-MM-DD HH:MM:SS.ms INFO retry.RetryInvocationHandler: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.ipc.StandbyException): Operation category READ is not supported in state standby. Visit https://s.apache.org/sbnn-error 
at org.apache.hadoop.hdfs.server.namenode.ha.StandbyState.checkOperation(StandbyState.java:98) 
at org.apache.hadoop.hdfs.server.namenode.NameNode$NameNodeHAContext.checkOperation(NameNode.java:1998) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkOperation(FSNamesystem.java:1502) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getFileInfo(FSNamesystem.java:3227) 
at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.getFileInfo(NameNodeRpcServer.java:1158) 
at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.getFileInfo(ClientNamenodeProtocolServerSideTranslatorPB.java:983) 
at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java) 
at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:527) 
at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:1036) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:978) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:906) 
at java.security.AccessController.doPrivileged(Native Method) 
at javax.security.auth.Subject.doAs(Subject.java:422) 
at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1729) 
at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2876) 
, while invoking ClientNamenodeProtocolTranslatorPB.getFileInfo over nmnode-0-0.corpnet.contoso.com/10.244.2.36:9000 after 8 failover attempts. Trying to failover after sleeping for 13518ms. 
  
sparkhead-0\hadoop-yarn-jobhistory\supervisor\log\jobhistoryserver-stderr---supervisor-GvebR8 
  
YYYY-MM-DD HH:MM:SS.ms INFO retry.RetryInvocationHandler: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.ipc.StandbyException): Operation category READ is not supported in state standby. Visit https://s.apache.org/sbnn-error 
at org.apache.hadoop.hdfs.server.namenode.ha.StandbyState.checkOperation(StandbyState.java:98) 
at org.apache.hadoop.hdfs.server.namenode.NameNode$NameNodeHAContext.checkOperation(NameNode.java:1998) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkOperation(FSNamesystem.java:1502) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getFileInfo(FSNamesystem.java:3227) 
at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.getFileInfo(NameNodeRpcServer.java:1158) 
at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.getFileInfo(ClientNamenodeProtocolServerSideTranslatorPB.java:983) 
at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java) 
at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:527) 
at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:1036) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:978) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:906) 
at java.security.AccessController.doPrivileged(Native Method) 
at javax.security.auth.Subject.doAs(Subject.java:422) 
at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1729) 
at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2876) 
, while invoking ClientNamenodeProtocolTranslatorPB.getFileInfo over nmnode-0-1.corpnet.contoso.com/10.244.1.30:9000 after 5 failover attempts. Trying to failover after sleeping for 11416ms. 
  
sparkhead-0\hadoop-livy-sparkhistory\supervisor\log\livy-stderr---supervisor-XiHB1w 
  
YYYY-MM-DD HH:MM:SS.ms INFO retry.RetryInvocationHandler: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.ipc.StandbyException): Operation category READ is not supported in state standby. Visit https://s.apache.org/sbnn-error 
at org.apache.hadoop.hdfs.server.namenode.ha.StandbyState.checkOperation(StandbyState.java:98) 
at org.apache.hadoop.hdfs.server.namenode.NameNode$NameNodeHAContext.checkOperation(NameNode.java:1998) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkOperation(FSNamesystem.java:1502) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getFileInfo(FSNamesystem.java:3227) 
at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.getFileInfo(NameNodeRpcServer.java:1158) 
at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.getFileInfo(ClientNamenodeProtocolServerSideTranslatorPB.java:983) 
at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java) 
at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:527) 
at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:1036) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:978) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:906) 
at java.security.AccessController.doPrivileged(Native Method) 
at javax.security.auth.Subject.doAs(Subject.java:422) 
at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1729) 
at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2876) 
, while invoking ClientNamenodeProtocolTranslatorPB.getFileInfo over nmnode-0-1.corpnet.contoso.com/10.244.1.30:9000 after 1 failover attempts. Trying to failover after sleeping for 1401ms. 
```

## <a name="cause"></a>원인

Kubernetes 네트워크에 대한 DC의 DNS 서버에 도메인 컨트롤러의 역방향 조회 영역 항목이 없습니다. 이 예제에서 누락된 항목은 `cni0 10.244`입니다. `sparkhead` Pod 컨테이너는 IP 주소 10.244.1.30:9000을 사용하여 nnnode-0-1에 도달하려고 하는데 DNS에서 주소를 확인할 수 없었습니다.

:::image type="content" source="media/troubleshoot-ad-hung-deployment-unhealthy-sparkhead-pods/missing_reverse_lookup_zone_entry_for_domain_controller.png" alt-text="도메인 컨트롤러의 누락된 역방향 조회 영역 항목":::

## <a name="resolution"></a>해결 방법

로그에 참조된 영역의 누락된 역방향 DNS 항목(PTR 레코드)을 추가합니다. 이 예제에서는 244.10을 추가했습니다.

:::image type="content" source="media/troubleshoot-ad-hung-deployment-unhealthy-sparkhead-pods/missing_reverse_lookup_zone_entry_for_domain_controller_add.png" alt-text="도메인 컨트롤러의 누락된 역방향 조회 영역 항목 추가":::

> [!NOTE]
> 클러스터 노드의 다른 모든 네트워크에 대한 DNS 서버에 도메인 컨트롤러 자체의 역방향 DNS 항목(PTR 레코드)이 등록되어 있는지 확인합니다.

## <a name="next-steps"></a>다음 단계

[도메인 컨트롤러의 역방향 DNS 항목(PTR 레코드)을 확인](deploy-active-directory.md#verify-reverse-dns-entry-for-domain-controller)합니다.