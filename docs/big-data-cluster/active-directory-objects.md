---
title: Active Directory 개체
titleSuffix: SQL Server Big Data Cluster
description: Active Directory 도메인에서 SQL Server 빅 데이터 클러스터를 배포하는 방법을 알아봅니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e4f8736beeac2e92d25092c60c3fe7e60127ea94
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942745"
---
# <a name="auto-generated-active-directory-objects"></a>자동 생성된 Active Directory 개체

이 문서에서는 BDC(빅 데이터 클러스터) 배포 중에 SQL Server가 만드는 AD(Active Directory) 계정 및 그룹에 대해 설명합니다.

## <a name="accounts--groups"></a>계정 및 그룹

사용자 계정 및 그룹은 클러스터 배포 중에 제공된 [OU(조직 구성 단위)](/windows-server/identity/ad-ds/plan/reviewing-ou-design-concepts) 안에서 생성됩니다.

각 계정은 BDC의 서비스를 나타냅니다. 계정은 각 서비스에 필요한 SPN(서비스 사용자 이름)을 소유합니다. [setspn](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spn-setspn-syntax.aspx) 명령을 사용하여 각 계정이 소유하는 SPN을 나열할 수 있습니다.

배포에서 자동으로 계정 및 그룹 이름을 생성합니다. SQL Server 2019 CU5부터, 계정 또는 그룹 이름 접두사는 배포 네임스페이스 이름(BDC 클러스터 이름)입니다. 이 문서의 항목에 대해 클러스터 이름이 `bdc`인 경우, `<prefix>`를 `bdc`로 바꿔서 계정을 식별하세요.

아래에서 Pod 접미사 (-x)는 변수 Pod ID를 나타냅니다. 아래 이름에는 배포 중에 사용자가 제공하는 변수 접두사가 포함되어 있지 않습니다.

클래식 계정 이름은 SQL Server 2019 CU5 이전 버전을 사용하는 배포와 보안 구성에서 “useSubdomain” 옵션이 false로 설정된 배포에 적용됩니다.

| 계정 또는 그룹 이름|자세한 정보|
|----|---|
|`<prefix>-ctrl`|[컨트롤러 서비스 계정](#controller-service-account)|
|`<prefix>-ngxm`|[모니터링 서비스 프록시 서비스 계정](#monitoring-service-proxy-service-account)|
|`<prefix>-ldap`|[LDAP 조회 사용자](#ldap-lookup-user)|
|`<prefix>-sqc0-x/<prefix>-sqc0`|[컴퓨팅 풀 SQL Server 사용자](#compute-pool-sql-server-user)|
|`<prefix>-dmc0-x`|[컴퓨팅 풀 데이터 웨어하우스 DMS 사용자](#compute-pool-data-warehouse-dms-user)|
|`<prefix>-dec0-x`|[컴퓨팅 풀 데이터 웨어하우스 엔진 사용자](#compute-pool-data-warehouse-engine-user)|
|`<prefix>-sqd0`|[데이터 풀 SQL Server 사용자](#data-pool-sql-server-user)|
|`<prefix>-sqs0`|[스토리지 풀 SQL Server 사용자](#storage-pool-sql-server-user)|
|`<prefix>-ynt0-x`|[스토리지 풀 Yarn 노드 관리자 서비스 사용자](#storage-pool-yarn-node-manager-service-user)|
|`<prefix>-htt0`|[스토리지 풀 HTTP 서비스 사용자](#storage-pool-http-service-user)|
|`<prefix>-hdt0`|[스토리지 풀 HDFS 데이터 노드 서비스 사용자](#storage-pool-hdfs-datanode-service-user)|
|`<prefix>-hdnn`|[HDFS 이름 노드 서비스 사용자](#hdfs-name-node-service-user)|
|`<prefix>-htnn`|[HDFS 이름 노드 HTTP 서비스 사용자](#hdfs-name-node-http-service-user)|
|`<prefix>-kmnn-x`|[이름 노드 KMS 서비스 사용자](#name-node-kms-service-user)|
|`<prefix>-jnzk-x`|[Zookeeper JournalNode 서비스 사용자](#zookeeper-journalnode-service-users)|
|`<prefix>-htzk`|[Zookeeper HTTP 서비스 사용자](#zookeeper-http-service-user)|
|`<prefix>-yrsh-x`|[Sparkhead Yarn 리소스 관리자 서비스 사용자](#sparkhead-yarn-resource-manager-service-user)|
|`<prefix>-htsh`|[Sparkhead HTTP 사용자](#sparkhead-http-user)|
|`<prefix>-shsh-x`|[Sparkhead Spark 기록 서비스 사용자](#sparkhead-spark-history-service-user)|
|`<prefix>-lvsh-x`|[Sparkhead Livy 서비스 사용자](#sparkhead-livy-service-user)|
|`<prefix>-hvsh-x`|[Sparkhead Hive 서비스 사용자](#sparkhead-hive-service-user)|
|`<prefix>-yns0-x`|[Spark 풀 Yarn 노드 관리자 서비스 사용자](#spark-pool-yarn-node-manager-service-user)|
|`<prefix>-hts0`|[Spark 풀 Yarn 노드 관리자 HTTP 사용자](#spark-pool-yarn-node-manager-http-user)|
|`<prefix>-knox-x`|[Knox 게이트웨이 사용자](#knox-gateway-user)|
|`<prefix>-htgw`|[Knox 게이트웨이 HTTP 사용자](#knox-gateway-http-user)|
|`<prefix>-apst`|[앱 설정 사용자](#app-setup-user)|
|`<prefix>-dmsvc`|[데이터 웨어하우스 DMS 서비스 그룹](#data-warehouse-dms-service-group)|
|`<prefix>-desvc`|[데이터 웨어하우스 엔진 서비스 그룹](#data-warehouse-engine-service-group)|

다음 섹션에서는 각 계정에 대한 자세한 정보를 제공합니다. 그룹에 대한 자세한 내용을 보려면 [그룹](#groups)으로 건너뛰세요.

## <a name="controller-management--ldap-related-accounts"></a>컨트롤러, 관리 및 LDAP 관련 계정

### <a name="controller-service-account"></a>컨트롤러 서비스 계정

|Object|계정 이름|
|---|---|
|확장 집합 이름|`control`|
|Pod 이름|`control-x`|
|컨테이너 이름|`controller`|
|서비스 이름|`controller`|
|계정 이름(접두사 제외)| `ctrl`|
|계정(네임스페이스 접두사 포함)|`<prefix>-ctrl`|
|클래식 계정 이름|`ctrl-controller`|

### <a name="monitoring-service-proxy-service-account"></a>모니터링 서비스 프록시 서비스 계정

|Object|계정 이름|
|---|---|
|확장 집합 이름|`mgmtproxy`|
|Pod 이름|`mgmtproxy-x`|
|컨테이너 이름|`service-proxy`|
|서비스 이름|`nginx`|
|계정(접두사 제외)| `ngxm`|
|계정(네임스페이스 접두사 포함)|`<prefix>-ngxm`|
|클래식 계정 이름|`nginx-mgmtproxy`|

### <a name="ldap-lookup-user"></a>LDAP 조회 사용자

grafana 및 hadoop 서비스에서 LDAP를 통해 사용자를 조회하는 데 사용됩니다.

|Object|계정 이름|
|---|---|
|확장 집합 이름|`metricsui`|
|Pod 이름|`metricsui-x`|
|컨테이너 이름|`grafana`|
|서비스 이름|`grafana`|
|계정 이름(접두사 제외)| `ldap`|
|계정 이름(네임스페이스 접두사 포함)|`<prefix>-ldap`|
|클래식 계정 이름|`ldap-user`|

## <a name="master-pool-accounts"></a>마스터 풀 계정

### <a name="master-pool-sql-server-user"></a>마스터 풀 SQL Server 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`master`|
|Pod 이름|`master-x`|
|컨테이너 이름|`mssql-server`|
|서비스 이름|`mssql`|
|계정 이름(접두사 제외)| `sqmp-x/sqmp`|
|계정 이름(네임스페이스 접두사 포함)|`<prefix>-sqmp-x/<prefix>-sqmp`|
|클래식 계정 이름|`mssql-master-x`|

### <a name="master-pool-data-warehouse-dms-user"></a>마스터 풀 데이터 웨어하우스 DMS 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`master`|
|Pod 이름|`master-x`|
|컨테이너 이름|`mssql-server`|
|서비스 이름|`dwdms`|
|계정(접두사 제외)| `dmmp-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-dmmp-x`|
|클래식 계정 이름|`dwdms-master-x`|

### <a name="master-pool-data-warehouse-engine-user"></a>마스터 풀 데이터 웨어하우스 엔진 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`master`|
|Pod 이름|`master-x`|
|컨테이너 이름|`mssql-server`|
|서비스 이름|`dweng`|
|계정(접두사 제외)| `demp`|
|계정(네임스페이스 접두사 포함)|`<prefix>-demp-x`|
|클래식 계정 이름|`dweng-master-x`|

## <a name="compute-pool-accounts"></a>컴퓨팅 풀 계정

### <a name="compute-pool-sql-server-user"></a>컴퓨팅 풀 SQL Server 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`compute-0`|
|Pod 이름|`compute-0-x`|
|컨테이너 이름|`mssql-server`|
|서비스 이름|`mssql`|
|계정(접두사 제외)| `sqc0-x/sqlc0`|
|계정(네임스페이스 접두사 포함)|`<prefix>-sqc0-x/<prefix>-sqc0`|
|클래식 계정 이름|`mssql-compute-0-x`|

### <a name="compute-pool-data-warehouse-dms-user"></a>컴퓨팅 풀 데이터 웨어하우스 DMS 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`compute-0`|
|Pod 이름|`compute-0-x`|
|컨테이너 이름|`mssql-server`|
|서비스 이름|`dwdms`|
|계정(접두사 제외)| `dmc0-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-dmc0-x`|
|클래식 계정 이름|`dwdms-compute-0-x`|

### <a name="compute-pool-data-warehouse-engine-user"></a>컴퓨팅 풀 데이터 웨어하우스 엔진 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`compute-0`|
|Pod 이름|`compute-0-x`|
|컨테이너 이름|`mssql-server`|
|서비스 이름|`dweng`|
|계정(접두사 제외)| `dec0-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-dec0-x`|
|클래식 계정 이름|`dweng-compute-0-x`|

## <a name="data-pool-accounts"></a>데이터 풀 계정

### <a name="data-pool-sql-server-user"></a>데이터 풀 SQL Server 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`data-0`|
|Pod 이름|`data-0-x`|
|컨테이너 이름|`mssql-server`|
|서비스 이름|`mssql`|
|계정(접두사 제외)| `sqd0`|
|계정(네임스페이스 접두사 포함)|`<prefix>-sqd0`|
|클래식 계정 이름|`mssql-data-0`|

## <a name="storage-pool-accounts"></a>스토리지 풀 계정

### <a name="storage-pool-sql-server-user"></a>스토리지 풀 SQL Server 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`storage-0`|
|Pod 이름|`storage-0-x`|
|컨테이너 이름|`mssql-server`|
|서비스 이름|`mssql`|
|계정(접두사 제외)| `sqs0`|
|계정(네임스페이스 접두사 포함)|`<prefix>-sqs0`|
|클래식 계정 이름|`mssql-storage-0`|

### <a name="storage-pool-yarn-node-manager-service-user"></a>스토리지 풀 Yarn 노드 관리자 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`storage-0`|
|Pod 이름|`storage-0-x`|
|컨테이너 이름|`hadoop`|
|서비스 이름|`Yarn Node Manager`|
|계정(접두사 제외)| `ynt0-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-ynt0-x`|
|클래식 계정 이름|`yarnnm-storage-0-x`|

### <a name="storage-pool-http-service-user"></a>스토리지 풀 HTTP 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`storage-0`|
|Pod 이름|`storage-0-x`|
|컨테이너 이름|`hadoop`|
|서비스 이름|`HDFS Datanode`|
|계정(접두사 제외)| `hdt0`|
|계정(네임스페이스 접두사 포함)|`<prefix>-hdt0`|
|클래식 계정 이름|`http-storage-0`|

### <a name="storage-pool-hdfs-datanode-service-user"></a>스토리지 풀 HDFS 데이터 노드 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`storage-0`|
|Pod 이름|`storage-0-x`|
|컨테이너 이름|`hadoop`|
|서비스 이름|`HDFS Datanode`|
|계정(접두사 제외)| `hdt0`|
|계정(네임스페이스 접두사 포함)|`<prefix>-hdt0`|
|클래식 계정 이름|`hdfsdn-storage-0`|

## <a name="hdfs-accounts"></a>HDFS 계정

### <a name="hdfs-name-node-service-user"></a>HDFS 이름 노드 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`nmnode-0`|
|Pod 이름|`nmnode-0-x`|
|컨테이너 이름|`hadoop`|
|서비스 이름|`HDFS Namenode`|
|계정(접두사 제외)| `hdnn`|
|계정(네임스페이스 접두사 포함)|`<prefix>-hdnn`|
|클래식 계정 이름|`hdfsnn-nmnode`|

### <a name="hdfs-name-node-http-service-user"></a>HDFS 이름 노드 HTTP 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`nmnode-0`|
|Pod 이름|`nmnode-0-x`|
|컨테이너 이름|`hadoop`|
|서비스 이름|`HDFS Namenode`|
|계정(접두사 제외)| `htnn`|
|계정(네임스페이스 접두사 포함)|`<prefix>-htnn`|
|클래식 계정 이름|`http-nmnode`|

## <a name="kms-accounts"></a>KMS 계정

### <a name="name-node-kms-service-user"></a>이름 노드 KMS 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`nmnode-0`|
|Pod 이름|`nmnode-0-x`|
|컨테이너 이름|`hadoop`|
|서비스 이름|`KMS`|
|계정(접두사 제외)| `kmnn-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-kmnn-x`|
|클래식 계정 이름|`kms-nmnode-x`|

## <a name="zookeeper-accounts"></a>Zookeeper 계정

### <a name="zookeeper-journalnode-service-users"></a>Zookeeper JournalNode 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`zookeeper`|
|Pod 이름|`zookeeper-x`|
|컨테이너 이름|`zookeeper`|
|서비스 이름|`Journal node`|
|계정(접두사 제외)| `jnzk-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-jnzk-x`|
|클래식 계정 이름|`jn-zookeeper-x`|

### <a name="zookeeper-http-service-user"></a>Zookeeper HTTP 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`zookeeper`|
|Pod 이름|`zookeeper-x`|
|컨테이너 이름|`zookeeper`|
|서비스 이름|`Zookeeper`|
|계정(접두사 제외)| `htzk`|
|계정(네임스페이스 접두사 포함)|`<prefix>-htzk`|
|클래식 계정 이름|`http-zookeeper`|

## <a name="spark-related-accounts"></a>Spark 관련 계정

### <a name="sparkhead-yarn-resource-manager-service-user"></a>Sparkhead Yarn 리소스 관리자 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`sparkhead`|
|Pod 이름|`sparkhead-x`|
|컨테이너 이름|`hadoop-yarn-jobhistory`|
|서비스 이름|`Yarn Resource Manager`|
|계정(접두사 제외)| `yrsh-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-yrsh-x`|
|클래식 계정 이름|`yarnrm-sparkhead-x`|

### <a name="sparkhead-http-user"></a>Sparkhead HTTP 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`sparkhead`|
|Pod 이름|`sparkhead-x`|
|컨테이너 이름|`*`|
|서비스 이름|`*`|
|계정(접두사 제외)| `htsh`|
|계정(네임스페이스 접두사 포함)|`<prefix>-htsh`|
|클래식 계정 이름|`http-sparkhead`|

### <a name="sparkhead-spark-history-service-user"></a>Sparkhead Spark 기록 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`sparkhead`|
|Pod 이름|`sparkhead-x`|
|컨테이너 이름|`hadoop-livy-sparkhistory`|
|서비스 이름|`Spark History Server`|
|계정(접두사 제외)| `shsh-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-shsh-x`|
|클래식 계정 이름|`sph-sparkhead-x`|

### <a name="sparkhead-livy-service-user"></a>Sparkhead Livy 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`sparkhead`|
|Pod 이름|`sparkhead-x`|
|컨테이너 이름|`hadoop-livy-sparkhistory`|
|서비스 이름|`Livy`|
|계정(접두사 제외)| `lvsh-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-lvsh-x`|
|클래식 계정 이름|`livy-sparkhead-x`|

### <a name="sparkhead-hive-service-user"></a>Sparkhead Hive 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`sparkhead`|
|Pod 이름|`sparkhead-x`|
|컨테이너 이름|`hadoop-hivemetastore`|
|서비스 이름|`Hive Metastore`|
|계정(접두사 제외)| `hvsh-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-hvsh-x`|
|클래식 계정 이름|`hive-sparkhead-x`|

### <a name="spark-pool-yarn-node-manager-service-user"></a>Spark 풀 Yarn 노드 관리자 서비스 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`spark-0`|
|Pod 이름|`spark-0-x`|
|컨테이너 이름|`hadoop`|
|서비스 이름|`Yarn Node Manager`|
|계정(접두사 제외)| `yns0-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-yns0-x`|
|클래식 계정 이름|`yarnnm-spark-0-x`|

### <a name="spark-pool-yarn-node-manager-http-user"></a>Spark 풀 Yarn 노드 관리자 HTTP 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`spark-0`|
|Pod 이름|`spark-0-x`|
|컨테이너 이름|`hadoop`|
|서비스 이름|`Yarn Node Manager`|
|계정(접두사 제외)| `hts0`|
|계정(네임스페이스 접두사 포함)|`<prefix>-hts0`|
|클래식 계정 이름|`http-spark-0`|

## <a name="knox-accounts"></a>Knox 계정

### <a name="knox-gateway-user"></a>Knox 게이트웨이 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`gateway`|
|Pod 이름|`gateway-x`|
|컨테이너 이름|`knox`|
|서비스 이름|`Knox`|
|계정(접두사 제외)| `knox-x`|
|계정(네임스페이스 접두사 포함)|`<prefix>-knox-x`|
|클래식 계정 이름|`knox-gateway-x`|

### <a name="knox-gateway-http-user"></a>Knox 게이트웨이 HTTP 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`gateway`|
|Pod 이름|`gateway-x`|
|컨테이너 이름|`knox`|
|서비스 이름|`Knox`|
|계정(접두사 제외)| `htgw`|
|계정(네임스페이스 접두사 포함)|`<prefix>-htgw`|
|클래식 계정 이름|`http-gateway`|

## <a name="app-accounts"></a>앱 계정

### <a name="app-setup-user"></a>앱 설정 사용자

|Object|계정 이름|
|---|---|
|확장 집합 이름|`appproxy`|
|Pod 이름|`appproxy-x`|
|컨테이너 이름|`App Service Proxy`|
|서비스 이름|`nginx`|
|계정(접두사 제외)| `apst`|
|계정(네임스페이스 접두사 포함)|`<prefix>-apst`|
|클래식 계정 이름|`app-setup`|

## <a name="groups"></a>그룹

다음 그룹은 사용자가 제공한 OU에서 생성됩니다. 그룹의 멤버는 위에서 해당 서비스에 대해 만들어진 사용자입니다.

### <a name="data-warehouse-dms-service-group"></a>데이터 웨어하우스 DMS 서비스 그룹

|Object|그룹 이름|
|---|---|
|확장 집합 이름|`master/compute-0`|
|Pod 이름|`master-x/compute-0-x`|
|컨테이너 이름|`mssql-server`|
|서비스 이름|`dwdms`|
|그룹(접두사 제외)| `dmsvc`|
|계정(네임스페이스 접두사 포함)|`<prefix>-dmsvc`|
|클래식 계정 이름|`dwdms-service`|

### <a name="data-warehouse-engine-service-group"></a>데이터 웨어하우스 엔진 서비스 그룹

|Object|그룹 이름|
|---|---|
|확장 집합 이름|`master/compute-0`|
|Pod 이름|`master-x/compute-0-x`|
|컨테이너 이름|`mssql-server`|
|서비스 이름|`dweng`|
|그룹(접두사 제외)| `desvc`|
|계정(네임스페이스 접두사 포함)|`<prefix>-desvc`|
|클래식 계정 이름|`desvc`|

## <a name="next-steps"></a>다음 단계

[Active Directory 모드에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](deploy-active-directory.md)

[동일한 Active Directory 도메인에 여러 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](active-directory-deployment-background.md)
