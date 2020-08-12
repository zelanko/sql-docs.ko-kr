---
title: 배포되는 리소스
titleSuffix: SQL Server Big Data Clusters
description: 일반적으로 SQL Server 빅 데이터 클러스터에 배포되는 Pod에 대한 설명입니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 03/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ad3cc263ea81b9e3bda5cb34ea27cfabba1ae716
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730715"
---
# <a name="resources-deployed-with-big-data-cluster"></a>빅 데이터 클러스터를 사용하여 배포되는 리소스

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 SQL Server 빅 데이터 클러스터가 배포하는 리소스에 대해 설명합니다.

빅 데이터 클러스터는 배포 프로필을 기준으로 Pod를 배포합니다. 자세한 내용은 [기본 구성](deployment-guidance.md#configfile)을 참조하세요. 

이 문서에서는 `aks-dev-test-ha` 프로필을 사용하여 배포되는 Pod에 대해 설명하고 Spark 풀을 포함합니다. Kubernetes를 쿼리하여 클러스터에 배포된 Pod를 확인합니다. 다음 예제에서는 특정 네임스페이스의 Pod 목록을 반환합니다.

```bash
kubectl get pods -n <namespace>
```

`<namespace>`를 빅 데이터 클러스터의 이름으로 바꿉니다. 

자세한 내용은 [Kubernetes에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md#configfile)을 참조하세요.

다음 다이어그램은 빅 데이터 클러스터에 배포되는 구성 요소를 보여 줍니다.

:::image type="content" source="media/big-data-cluster-overview/architecture-diagram-overview.png" alt-text="big-data-cluster-diagram":::

아키텍처에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]란?](big-data-cluster-overview.md)을 참조하세요.

## <a name="deployed-pods"></a>배포되는 Pod

다음 표에는 빅 데이터 클러스터에 배포되는 Pod가 나와 있습니다.

|속성  |영역|
|---------|---------|
|`control-<nnnn>`        |[제어](#control)|
|`controldb-<#>`         |[제어](#control)|
|`controlwd-<nnnn>`      |[제어](#control)|
|`logsdb-<#>`            |[제어](#control)|
|`logsui-<nnnn>`         |[제어](#control)|
|`metricsdb-<#>`         |[제어](#control)|
|`metricsdc-<nnnn>`      |[제어](#control)|
|`metricsui-<nnnn>`      |[제어](#control)|
|`mgmtproxy-<nnnn>`      |[제어](#control)|
|`zookeeper-<#>`         |[제어](#control)|
|`dns-<nnnn>`            |[제어](#control)|
|`master-<#n>`           |[마스터 인스턴스](#master-instance)|
|`operator-<nnnn>`       |[마스터 인스턴스](#master-instance)
|`compute-<#n>-<#m>`     |[컴퓨팅 풀](#compute-pool)|
|`data-<#>-<#>`          |[데이터 풀](#data-pool) |
|`storage-<#>-<#>`       |[스토리지 풀](#storage-pool)|
|`nmnode-<#>-<#>`        |[스토리지 풀](#storage-pool)|
|`sparkhead-<#>`         |[스토리지 풀](#storage-pool)|
|`appproxy-<#m>`         |[애플리케이션 풀](#application-pool)|
|`gateway-<#>`           |[게이트웨이 서비스](#gateway-service)|

모든 Pod가 모든 BDC 클러스터에 포함되는 것은 아닙니다. 고가용성 또는 Active Directory 통합이 있는 배포에는 특정 Pod가 포함됩니다. 

### <a name="high-availability-specific-pods"></a>고가용성 관련 Pod:

- `operator-<nnnn>`
- `zookeeper-<#>`

### <a name="active-directory-specific-pods"></a>Active Directory 관련 Pod:

- `dns-<nnnn>`

다음 섹션에서는 Pod에 대해 설명하고 각 Pod의 컨테이너를 나열합니다.

## <a name="control"></a>제어

제어 Pod는 제어 서비스를 제공합니다.

|Pod 이름 |개수| Kubernetes 컨트롤러 유형 | 컨테이너 |
|--------|----|------|--------|-------|
|`control-#`|1| ReplicaSet |- `controller`<br><br>- `security-support`<br><br>- `fluentbit`
|`controldb`|1| StatefulSet |- `mssql-server`<br><br>- `fluentbit`
|`controlwd`|1|  ReplicaSet |- `controlwatchdog`
|`logsdb-#` |1| StatefulSet |- `elasticsearch`
|`logsui`   |1| ReplicaSet |- `kibana`
|`metricsdb-#`|1| StatefulSet |- `influxdb`
|`metricsdc`|Kubernetes 노드당 1개 | DaemonSet |- `telegraf` |
|`metricsui-nnnn`|1| ReplicaSet |- `grafana` |
|`mgmtproxy-nnnn`|1| ReplicaSet |- `service-proxy`<br><br>- `fluentbit`|
|`dns-nnnn`|Active Directory 통합의 경우 0개 또는 1개| ReplicaSet |- `dns`<br><br>- `fluentbit`|

## <a name="master-instance"></a>마스터 인스턴스

`master-<#n>`은 SQL Server 마스터 인스턴스입니다.

- DDL을 통해 데이터 풀을 관리합니다.
- DML을 통해 데이터 풀의 데이터를 조작합니다.
- 분석 쿼리 실행을 데이터 풀로 오프로드합니다.

|Pod 이름 |개수| Kubernetes 컨트롤러 유형 | 컨테이너 |
|--------|----|------|--------|
|`master-<#n>`|고가용성의 경우 1개 이상| StatefulSet|- `mssql-server`<br><br>- `fluentbit`<br><br>- `collectd`<br><br>- `mssql-ha-supervisor` <sup>*</sup>|
|`operator`<sup>*</sup>| 고가용성의 경우 0개 또는 1개 | ReplicaSet |- `mssql-ha-operator`

<sup>*</sup> 고가용성 배포만 해당합니다. 운영자는 SQL Server 및 가용성 그룹 리소스에 대한 사용자 지정 리소스 정의를 구현하고 등록합니다. 운영자를 배포하면 Kubernetes 클러스터에 배포되는 SQL Server 리소스에 대한 알림 수신기로 등록됩니다. `mssql-ha-supervisor`는 가용성 그룹을 지원합니다.

각 `master` Pod에는 SQL Server 인스턴스 1개가 포함됩니다. 고가용성 배포에는 Pod 3개가 포함됩니다. 각 Pod에는 SQL Server Always On 가용성 그룹에 데이터베이스가 있는 SQL Server 인스턴스 1개가 포함됩니다.

워크로드에 따라 배포 시 추가 Pod를 포함합니다. 

## <a name="compute-pool"></a>풀 컴퓨팅

컴퓨팅 풀은 계산용 SQL Server 인스턴스를 제공합니다.

|Pod 이름 |개수| Kubernetes 컨트롤러 유형 | 컨테이너 |
|--------|----|------|--------|
|`compute-<#n>-<#m>`|1개 이상| StatefulSet |- `mssql-server`<br><br>- `fluentbit`<br><br>- `collectd`

- `#n`은 컴퓨팅 풀을 식별합니다.
- `#m`은 풀 내에서 인스턴스 ID를 식별합니다.

컴퓨팅 풀 SQL Server 인스턴스는 상태 비저장입니다. `tempdb` 스토리지만 있으면 됩니다.

워크로드에 따라 배포 시 추가 Pod를 포함합니다. 

## <a name="data-pool"></a>데이터 풀

데이터 풀은 스토리지 및 컴퓨팅용 SQL Server 인스턴스를 제공합니다.

|Pod 이름 |개수| Kubernetes 컨트롤러 유형 | 컨테이너 |
|--------|----|------|--------|-------|
|`data-<#n>-<#m>` | 0개 이상 | StatefulSet | -` mssql-server` <br><br>- `fluentbit`<br><br>- `collectd`|

- `#n`은 데이터 풀을 식별합니다.
- `#m`은 풀 내에서 인스턴스 ID를 식별합니다.

워크로드에 따라 배포 시 추가 Pod를 포함합니다.

## <a name="storage-pool"></a>스토리지 풀

스토리지 풀은 Spark를 통한 데이터 수집, HDFS의 스토리지, HDFS 및 SQL Server 엔드포인트를 통한 데이터 액세스를 제공합니다.

|Pod 이름 |개수| Kubernetes 컨트롤러 유형 | 컨테이너 |
|--------|----|------|--------|
|`storage-0-#`|1개 이상 워크로드에 따라 배포 시 추가 Pod를 포함합니다. | StatefulSet |- `hadoop`<br><br>- `mssql-server`<br><br>- `fluentbit`<br><br>
|`nmnode-0-#`|고가용성의 경우 1개 이상| StatefulSet |- `hadoop`<br><br>- `fluentbit`
|`sparkehead-#`|고가용성의 경우 1개 이상| StatefulSet |- `hadoop-yarn-jobhistory`<br><br>- `hadoop-livy-sparkhistory`<br><br>- `hadoop-hivemetastore`<br><br>-- `fluentbit`
|`zookeeper`|고가용성의 경우 0개 또는 3개 | StatefulSet |- `zookeeper`<br><br>- `fluentbit`

## <a name="application-pool"></a>애플리케이션 풀

애플리케이션 풀은 일부 테스트 구성 프로필에 포함되어 있습니다. 애플리케이션 풀은 빅 데이터 클러스터용 애플리케이션을 배포할 때 정의하는 애플리케이션 서비스 프록시를 호스트합니다. 

`appproxy`는 애플리케이션 풀 애플리케이션 앞에 배치되는 웹 API입니다. 사용자를 인증하고 요청을 애플리케이션으로 라우팅합니다.

|Pod 이름 | Kubernetes 컨트롤러 유형 | 컨테이너  |
|--------|----|------|
|`appproxy`| ReplicaSet |- `app-service-proxy`<br><br>- `fluentbit`

자세한 내용은 [빅 데이터 클러스터의 애플리케이션 배포란?](concept-application-deployment.md)을 참조하세요.

워크로드에 따라 배포 시 추가 Pod를 포함합니다. 

## <a name="gateway-service"></a>게이트웨이 서비스

게이트웨이 서비스는 Spark, HDFS, [Yarn](https://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html), Yarn UI 및 Spark UI에 대한 Knox 게이트웨이를 제공합니다.

|Pod 이름 | Kubernetes 컨트롤러 유형 | 컨테이너 |
|--------|-----|-----|
|`gateway-<#>`| StatefulSet |- `knox`<br><br>- `fluentbit`

게이트웨이는 하나만 지원됩니다.

## <a name="open-source-container-references"></a>오픈 소스 컨테이너 참조

일부 컨테이너는 오픈 소스 프로젝트에서 개발되었습니다. 사용되는 오픈 소스 컨테이너에 대한 자세한 내용은 다음을 참조하세요.

- [Elasticsearch](https://www.elastic.co/)
- [Kibana](https://www.elastic.co/kibana)
- [InfluxDB](https://www.influxdata.com)
- [Grafana](https://grafana.com/)
- [Fluent Bit](https://docs.fluentbit.io/manual/about/what-is-fluent-bit)
- [HDFS DataNode](concept-storage-pool.md)
- [HDFS NameNode](https://cwiki.apache.org/confluence/display/HADOOP2/NameNode) 
- [Spark](configure-spark-hdfs.md)
- [ZooKeeper](https://kubernetes.io/docs/tutorials/stateful-application/zookeeper/) 


## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)
- [워크샵: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
- [Kubernetes에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md#configfile)
