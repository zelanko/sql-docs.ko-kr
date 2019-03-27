---
title: 릴리스 정보
titleSuffix: SQL Server 2019 big data clusters
description: 이 문서에서는 최신 업데이트 및 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대 한 알려진된 문제를 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 2adf081f68ec0941b287102f515da2cabbfbbe18
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494185"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>SQL Server에서 빅 데이터 클러스터에 대 한 릴리스 정보

이 문서에서는 업데이트를 나열 및 빅 데이터 클러스터 SQL Server의 최신 릴리스에 대 한 문제 인지 알고 있어야 합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp24"></a> CTP 2.4 (3 월)

다음 섹션에서는 새로운 기능 및 SQL Server 2019 CTP 2.4에서 빅 데이터 클러스터에 대해 알려진된 문제를 설명합니다.

### <a name="whats-new"></a>What's New

| 새 기능/업데이트 | 설명 |
|:---|:---|
| GPU에 대 한 지침 딥 러닝 Spark에서 TensorFlow를 사용 하 여 실행에 대 한 지원. | [GPU 지원이 포함 된 빅 데이터 클러스터를 배포 및 TensorFlow를 실행 합니다.](spark-gpu-tensorflow.md) |
| **SqlDataPool** 하 고 **SqlStoragePool** 데이터 원본에 더 이상 기본적으로 만들어집니다. | 필요에 따라 수동으로 이러한를 만듭니다. 참조 된 [알려진 문제](#externaltablesctp24)합니다. |
| Spark 2.4로 Spark 런타임 업그레이드 | |

### <a name="known-issues"></a>알려진 문제

다음 섹션의 알려진된 문제 및 제한 사항이이 릴리스를 사용 하 여 설명합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서 빅 데이터 데이터 클러스터를 업그레이드 하는 것은 지원 되지 않습니다.

   > [!IMPORTANT]
   > 데이터를 백업 하 고 다음 기존 빅 데이터 클러스터를 삭제 해야 합니다 (이전 버전의를 사용 하 여 **mssqlctl**) 최신 릴리스를 배포 하기 전에 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-guidance.md#upgrade)합니다.

- AKS를 배포한 후 배포에서 다음 두 경고 이벤트를 볼 수 있습니다. 이러한 이벤트는 알려진 문제, 있지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포를 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패 하면 연결된 된 네임 스페이스 제거 되지 않습니다. 이 클러스터에서 분리 된 네임 스페이스를 발생할 수 있습니다. 동일한 이름 사용 하 여 클러스터를 배포 하기 전에 네임 스페이스를 수동으로 삭제 됩니다.

#### <a name="kubeadm-deployments"></a>kubeadm 배포

Kubeadm를 사용 하 여 여러 컴퓨터에서 Kubernetes를 배포 하려면 클러스터 관리 포털에 빅 데이터 클러스터에 연결 하는 데 필요한 끝점을 올바르게 표시 되지 않습니다. 이 문제가 발생 하는 경우 서비스 끝점 IP 주소를 검색 하려면 다음 해결을 사용 합니다.

- 클러스터 내에서 연결 하는 경우 끝점에 연결 하려는 서비스 IP에 대 한 Kubernetes를 쿼리 합니다. 다음 예를 들어 **kubectl** 명령은 마스터 SQL Server 인스턴스의 IP 주소를 표시 합니다.

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 클러스터 외부에서 연결 하는 경우 다음 단계를 사용 하 여 연결 하려면:

   1. SQL Server 마스터 인스턴스를 실행 중인 노드의 IP 주소를 가져옵니다: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`합니다.

   1. 이 IP 주소를 사용 하는 SQL Server 마스터 인스턴스에 연결 합니다.

   1. 쿼리는 **cluster_endpoint_table** 다른 외부 끝점에 대 한 master 데이터베이스에 있습니다.

      연결 제한 시간 실패 하면이 경우 각 노드의 방화벽을 사용 합니다. 이 경우 Kubernetes 클러스터 관리자에 게 문의 하 고 외부적으로 노출 되는 노드 IP에 대 한 요청 해야 합니다. 노드 수 있습니다. 그런 다음 클러스터에서 실행 되는 다양 한 서비스에 연결 하는 IP 및 해당 포트를 사용할 수 있습니다. 예를 들어, 관리자를 실행 하 여이 IP를 찾을 수 있습니다.

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="externaltablesctp24"></a> 외부 테이블

- 빅 데이터 클러스터 배포에서는 더 이상 합니다 **SqlDataPool** 하 고 **SqlStoragePool** 외부 데이터 원본입니다. 이러한 데이터 원본은 데이터 풀 및 저장소 풀 데이터 가상화를 지원 하도록 수동으로 만들 수 있습니다.

   ```sql
   -- Create data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');

   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
     CREATE EXTERNAL DATA SOURCE SqlStoragePool
     WITH (LOCATION = 'sqlhdfs://service-mssql-controller:8080');
   ```

- 지원 되지 않는 열 형식에는 테이블에 대 한 데이터 풀 외부 테이블을 만들 가능성이 있습니다. 외부 테이블을 쿼리 하는 경우 메시지가 다음과 비슷합니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 오류가 발생할 수 있습니다는 동시에 기본 파일은 HDFS에 복사 되는 경우.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에는 외부 테이블을 만들면 Azure Data Studio virtualization 마법사는 외부 테이블 정의에서 이러한 열 VARCHAR로 해석 합니다. 외부 테이블 DDL에에서 실패를 하면 합니다. 하거나 NVARCHAR2 유형을 사용 하 여 또는 EXTERNAL TABLE 문을 수동으로 만들고, 마법사를 사용 하는 대신 NVARCHAR를 지정 하는 Oracle 스키마를 수정 합니다.

#### <a name="application-deployment"></a>응용 프로그램 배포

- R, Python 또는 MLeap 응용 프로그램에서 RESTful API를 호출할 때 호출에에서 시간 초과 5 분입니다.

#### <a name="spark-and-notebooks"></a>Spark 및 notebook

- POD IP 주소는 Pod 다시 시작으로 Kubernetes 환경에서 변경 될 수 있습니다. 마스터 pod를 다시 시작 되는 시나리오에서 Spark 세션을 사용 하 여 못할 `NoRoteToHostException`합니다. 이 새 IP를 사용 하 여 새로 고쳐지는 가져오기 하지 JVM 캐시 주소입니다.

- Windows에 이미 설치 된 Jupyter 및 별도 Python을 있다면 Spark 노트북 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북을 클릭할 경우에 **텍스트 추가** 명령, 텍스트 셀이 편집 모드 보다는 미리 보기 모드에서 추가 됩니다. 편집 모드에 있고 셀을 편집 하 여 전환한 다음 미리 보기 아이콘을 클릭할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- 미리 HDFS의 파일을 마우스 오른쪽 단추로 클릭 하는 경우 다음 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재는 Azure Data Studio에서 30 MB 보다 큰 파일을 미리 볼 수 없습니다.

- 구성 변경 내용은 hdfs-site.xml 변경 내용을 포함 하는 HDFS에 지원 되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 (예: 코드 덤프 파일)의 일부 환경의 및 검색할 수입니다. 배포 후 마스터 인스턴스에서 SA_PASSWORD 다시 설정 해야 합니다. 이 변경은 버그 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)합니다.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp23"></a> CTP 2.3 (2 월)

다음 섹션에서는 새로운 기능 및 SQL Server 2019 CTP 2.3에서 빅 데이터 클러스터에 대해 알려진된 문제를 설명합니다.

### <a name="new-features"></a>새로운 기능

| 새로운 기능 | 설명 |
| :---------- | :------ |
| IntelliJ에서 빅 데이터 클러스터에서 Spark 작업을 제출 합니다. | [IntelliJ에서 SQL Server 빅 데이터 클러스터에서 Spark 작업 제출](spark-submit-job-intellij-tool-plugin.md) |
| 응용 프로그램 배포 및 클러스터 관리에 대 한 일반 CLI입니다. | [SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 앱을 배포 하는 방법](big-data-cluster-create-apps.md) |
| VS Code 확장 빅 데이터 클러스터에 응용 프로그램을 배포 합니다. | [VS Code를 사용 하 여 SQL Server 빅 데이터 클러스터에 응용 프로그램을 배포 하는 방법](app-deployment-extension.md) |
| 변경 된 **mssqlctl** 명령 사용법을 도구입니다. | 자세한 내용은 참조는 [알려진 mssqlctl 문제](#mssqlctlctp23)합니다. |
| 빅 데이터 클러스터에 사용 하 여 Sparklyr | [SQL Server 2019 빅 데이터 클러스터에 사용 하 여 Sparklyr](sparklyr-from-RStudio.md) |
| 외부 HDFS 호환 저장소를 사용 하 여 빅 데이터 클러스터에 탑재 **HDFS 계층화**합니다. | 참조 [HDFS 계층화](hdfs-tiering.md)합니다. |
| 마스터 SQL Server 인스턴스 및 HDFS/Spark 게이트웨이에 대 한 새로운 통합 된 연결 환경입니다. | 참조 [SQL Server 마스터 인스턴스와 HDFS/Spark 게이트웨이](connect-to-big-data-cluster.md)합니다. |
| 사용 하 여 클러스터를 삭제 **mssqlctl 클러스터 삭제** 이제 빅 데이터 클러스터에 포함 된 네임 스페이스에 있는 개체만 삭제 합니다. | 네임 스페이스 삭제 되지 않습니다. 그러나 이전 릴리스에서이 명령은 전체 네임 스페이스를 삭제 하지 못했습니다. |
| _보안_ 끝점 이름이 변경 되었으며 통합 합니다. | **서비스-보안-lb** 하 고 **서비스-보안-nodeport** 로 통합 되었습니다 합니다 **끝점 보안** 끝점입니다. |
| _프록시_ 끝점 이름이 변경 되었으며 통합 합니다. | **서비스-프록시-lb** 하 고 **nodeport-프록시 서비스-** 로 통합 되었습니다 합니다 **끝점 서비스 프록시** 끝점. |
| _컨트롤러_ 끝점 이름이 변경 되었으며 통합 합니다. | **서비스 mssql-컨트롤러 lb** 하 고 **서비스 mssql-컨트롤러 nodeport** 로 통합 되었습니다 합니다 **끝점-컨트롤러** 끝점. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

다음 섹션의 알려진된 문제 및 제한 사항이이 릴리스를 사용 하 여 설명합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서 빅 데이터 데이터 클러스터를 업그레이드 하는 것은 지원 되지 않습니다.

   > [!IMPORTANT]
   > 데이터를 백업 하 고 다음 기존 빅 데이터 클러스터를 삭제 해야 합니다 (이전 버전의를 사용 하 여 **mssqlctl**) 최신 릴리스를 배포 하기 전에 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-guidance.md#upgrade)합니다.

- 합니다 **ACCEPT_EULA** EULA에 동의 하려면 "예"는 "yes" 또는 환경 변수 여야 합니다. 이전 릴리스에서 "y" 및 "Y" 사용할 수 있지만 및 배포가 실패 하면 더 이상 허용 됩니다.

- 합니다 **CLUSTER_PLATFORM** 환경 변수 없는 기본 이전 릴리스와 동일 합니다.

- AKS를 배포한 후 배포에서 다음 두 경고 이벤트를 볼 수 있습니다. 이러한 이벤트는 알려진 문제, 있지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포를 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패 하면 연결된 된 네임 스페이스 제거 되지 않습니다. 이 클러스터에서 분리 된 네임 스페이스를 발생할 수 있습니다. 동일한 이름 사용 하 여 클러스터를 배포 하기 전에 네임 스페이스를 수동으로 삭제 됩니다.

#### <a name="kubeadm-deployments"></a>kubeadm 배포

Kubeadm를 사용 하 여 여러 컴퓨터에서 Kubernetes를 배포 하려면 클러스터 관리 포털에 빅 데이터 클러스터에 연결 하는 데 필요한 끝점을 올바르게 표시 되지 않습니다. 이 문제가 발생 하는 경우 서비스 끝점 IP 주소를 검색 하려면 다음 해결을 사용 합니다.

- 클러스터 내에서 연결 하는 경우 끝점에 연결 하려는 서비스 IP에 대 한 Kubernetes를 쿼리 합니다. 다음 예를 들어 **kubectl** 명령은 마스터 SQL Server 인스턴스의 IP 주소를 표시 합니다.

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 클러스터 외부에서 연결 하는 경우 다음 단계를 사용 하 여 연결 하려면:

   1. SQL Server 마스터 인스턴스를 실행 중인 노드의 IP 주소를 가져옵니다: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`합니다.

   1. 이 IP 주소를 사용 하는 SQL Server 마스터 인스턴스에 연결 합니다.

   1. 쿼리는 **cluster_endpoint_table** 다른 외부 끝점에 대 한 master 데이터베이스에 있습니다.

      연결 제한 시간 실패 하면이 경우 각 노드의 방화벽을 사용 합니다. 이 경우 Kubernetes 클러스터 관리자에 게 문의 하 고 외부적으로 노출 되는 노드 IP에 대 한 요청 해야 합니다. 노드 수 있습니다. 그런 다음 클러스터에서 실행 되는 다양 한 서비스에 연결 하는 IP 및 해당 포트를 사용할 수 있습니다. 예를 들어, 관리자를 실행 하 여이 IP를 찾을 수 있습니다.

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="mssqlctlctp23"></a> mssqlctl

- 합니다 **mssqlctl** 도구 동사-명사 명령의 순서 명사-동사 순서를 변경 합니다. 예를 들어 `mssqlctl create cluster` 이제 `mssqlctl cluster create`합니다.

- 합니다 `--name` 매개 변수는 이제 사용 하 여 클러스터를 만들 때 필요한 `mssqlctl cluster create`합니다.

   ```bash
   mssqlctl cluster create --name <cluster_name>
   ```

- 빅 데이터 클러스터의 최신 버전으로 업그레이드 하는 방법에 대 한 중요 한 정보에 대 한 및 **mssqlctl**를 참조 하십시오 [새 릴리스로 업그레이드](deployment-guidance.md#upgrade)합니다.

#### <a name="external-tables"></a>외부 테이블

- 지원 되지 않는 열 형식에는 테이블에 대 한 데이터 풀 외부 테이블을 만들 가능성이 있습니다. 외부 테이블을 쿼리 하는 경우 메시지가 다음과 비슷합니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 오류가 발생할 수 있습니다는 동시에 기본 파일은 HDFS에 복사 되는 경우.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에는 외부 테이블을 만들면 Azure Data Studio virtualization 마법사는 외부 테이블 정의에서 이러한 열 VARCHAR로 해석 합니다. 외부 테이블 DDL에에서 실패를 하면 합니다. 하거나 NVARCHAR2 유형을 사용 하 여 또는 EXTERNAL TABLE 문을 수동으로 만들고, 마법사를 사용 하는 대신 NVARCHAR를 지정 하는 Oracle 스키마를 수정 합니다.

#### <a name="application-deployment"></a>응용 프로그램 배포

- R, Python 또는 MLeap 응용 프로그램에서 RESTful API를 호출할 때 호출에에서 시간 초과 5 분입니다.

#### <a name="spark-and-notebooks"></a>Spark 및 notebook

- POD IP 주소는 Pod 다시 시작으로 Kubernetes 환경에서 변경 될 수 있습니다. 마스터 pod를 다시 시작 되는 시나리오에서 Spark 세션을 사용 하 여 못할 `NoRoteToHostException`합니다. 이 새 IP를 사용 하 여 새로 고쳐지는 가져오기 하지 JVM 캐시 주소입니다.

- Windows에 이미 설치 된 Jupyter 및 별도 Python을 있다면 Spark 노트북 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북을 클릭할 경우에 **텍스트 추가** 명령, 텍스트 셀이 편집 모드 보다는 미리 보기 모드에서 추가 됩니다. 편집 모드에 있고 셀을 편집 하 여 전환한 다음 미리 보기 아이콘을 클릭할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- 미리 HDFS의 파일을 마우스 오른쪽 단추로 클릭 하는 경우 다음 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재는 Azure Data Studio에서 30 MB 보다 큰 파일을 미리 볼 수 없습니다.

- 구성 변경 내용은 hdfs-site.xml 변경 내용을 포함 하는 HDFS에 지원 되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 (예: 코드 덤프 파일)의 일부 환경의 및 검색할 수입니다. 배포 후 마스터 인스턴스에서 SA_PASSWORD 다시 설정 해야 합니다. 이 변경은 버그 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)합니다.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp22"></a> CTP 2.2 (2018 년 12 월)

다음 섹션에서는 새로운 기능 및 SQL Server 2019 CTP 2.2에서 빅 데이터 클러스터에 대해 알려진된 문제를 설명합니다.

### <a name="new-features"></a>새로운 기능

- 사용 하 여 클러스터 관리 포털에 액세스할 `/portal` (**https://\<ip 주소\>: 30777/포털**).
- 마스터 풀 서비스 이름을 변경할 `service-master-pool-lb` 하 고 `service-master-pool-nodeport` 에 `endpoint-master-pool`입니다.
- 새 버전의 **mssqlctl** 이미지를 업데이트 합니다.
- 기타 버그 수정 및 개선 합니다.

### <a name="known-issues"></a>알려진 문제

다음 섹션의 알려진된 문제 및 제한 사항이이 릴리스를 사용 하 여 설명합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서 빅 데이터 데이터 클러스터를 업그레이드 하는 것은 지원 되지 않습니다. 백업 하 고 최신 릴리스를 배포 하기 전에 모든 기존 빅 데이터 클러스터를 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-guidance.md#upgrade)합니다.

- AKS를 배포한 후 배포에서 다음 두 경고 이벤트를 볼 수 있습니다. 이러한 이벤트는 알려진 문제, 있지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포를 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패 하면 연결된 된 네임 스페이스 제거 되지 않습니다. 이 클러스터에서 분리 된 네임 스페이스를 발생할 수 있습니다. 동일한 이름 사용 하 여 클러스터를 배포 하기 전에 네임 스페이스를 수동으로 삭제 됩니다.

#### <a name="cluster-administration-portal"></a>클러스터 관리 포털

클러스터 관리 포털에서 마스터 SQL Server 인스턴스에 대 한 끝점을 표시 하지 않습니다. 마스터 인스턴스에 대 한 IP 주소 및 포트를 찾으려면 다음 사용 **kubectl** 명령:

```
kubectl get svc endpoint-master-pool -n <your-cluster-name>
```

#### <a name="external-tables"></a>외부 테이블

- 지원 되지 않는 열 형식에는 테이블에 대 한 데이터 풀 외부 테이블을 만들 가능성이 있습니다. 외부 테이블을 쿼리 하는 경우 메시지가 다음과 비슷합니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 오류가 발생할 수 있습니다는 동시에 기본 파일은 HDFS에 복사 되는 경우.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 및 notebook

- POD IP 주소는 Pod 다시 시작으로 Kubernetes 환경에서 변경 될 수 있습니다. 마스터 pod를 다시 시작 되는 시나리오에서 Spark 세션을 사용 하 여 못할 `NoRoteToHostException`합니다. 이 새 IP를 사용 하 여 새로 고쳐지는 가져오기 하지 JVM 캐시 주소입니다.

- Windows에 이미 설치 된 Jupyter 및 별도 Python을 있다면 Spark 노트북 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북을 클릭할 경우에 **텍스트 추가** 명령, 텍스트 셀이 편집 모드 보다는 미리 보기 모드에서 추가 됩니다. 편집 모드에 있고 셀을 편집 하 여 전환한 다음 미리 보기 아이콘을 클릭할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- 미리 HDFS의 파일을 마우스 오른쪽 단추로 클릭 하는 경우 다음 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재는 Azure Data Studio에서 30 MB 보다 큰 파일을 미리 볼 수 없습니다.

- 구성 변경 내용은 hdfs-site.xml 변경 내용을 포함 하는 HDFS에 지원 되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 (예: 코드 덤프 파일)의 일부 환경의 및 검색할 수입니다. 배포 후 마스터 인스턴스에서 SA_PASSWORD 다시 설정 해야 합니다. 이 변경은 버그 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)합니다.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp21"></a> CTP 2.1 (2018 년 11 월)

다음 섹션에서는 새로운 기능 및 SQL Server 2019 CTP 2.1에서 빅 데이터 클러스터에 대해 알려진된 문제를 설명합니다.

### <a name="new-features"></a>새로운 기능

- [R 및 Python 앱을 배포](big-data-cluster-create-apps.md) 빅 데이터 클러스터에 있습니다.
- 새 버전의 **mssqlctl** 이미지를 업데이트 합니다. 
- 기타 버그 수정 및 개선 합니다.

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 CTP 2.1에서 SQL Server 빅 데이터 클러스터에 대해 알려진된 문제를 제공합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서 빅 데이터 데이터 클러스터를 업그레이드 하는 것은 지원 되지 않습니다. 백업 하 고 최신 릴리스를 배포 하기 전에 모든 기존 빅 데이터 클러스터를 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-guidance.md#upgrade)합니다.

- AKS를 배포한 후 배포에서 다음 두 경고 이벤트를 볼 수 있습니다. 이러한 이벤트는 알려진 문제, 있지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포를 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패 하면 연결된 된 네임 스페이스 제거 되지 않습니다. 이 클러스터에서 분리 된 네임 스페이스를 발생할 수 있습니다. 동일한 이름 사용 하 여 클러스터를 배포 하기 전에 네임 스페이스를 수동으로 삭제 됩니다.

#### <a name="admin-portal"></a>관리 포털

- 경우 있습니다 [msqlctl ctp 명령을 사용 하 여 앱 만들기](big-data-cluster-create-apps.md) 빅 데이터 클러스터에 클러스터 관리 포털을 보여 줍니다 pod 관리자 부분의 컨트롤러 섹션에서 "알 수 없음"으로 응용 프로그램이 배포 된 SQL Server에 배포 합니다.

#### <a name="external-tables"></a>외부 테이블

- 지원 되지 않는 열 형식에는 테이블에 대 한 데이터 풀 외부 테이블을 만들 가능성이 있습니다. 외부 테이블을 쿼리 하는 경우 메시지가 다음과 비슷합니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 오류가 발생할 수 있습니다는 동시에 기본 파일은 HDFS에 복사 되는 경우.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 및 notebook

- POD IP 주소는 Pod 다시 시작으로 Kubernetes 환경에서 변경 될 수 있습니다. 마스터 pod를 다시 시작 되는 시나리오에서 Spark 세션을 사용 하 여 못할 `NoRoteToHostException`합니다. 이 새 IP를 사용 하 여 새로 고쳐지는 가져오기 하지 JVM 캐시 주소입니다.

- Windows에 이미 설치 된 Jupyter 및 별도 Python을 있다면 Spark 노트북 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북을 클릭할 경우에 **텍스트 추가** 명령, 텍스트 셀이 편집 모드 보다는 미리 보기 모드에서 추가 됩니다. 편집 모드에 있고 셀을 편집 하 여 전환한 다음 미리 보기 아이콘을 클릭할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- 미리 HDFS의 파일을 마우스 오른쪽 단추로 클릭 하는 경우 다음 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재는 Azure Data Studio에서 30 MB 보다 큰 파일을 미리 볼 수 없습니다.

- 구성 변경 내용은 hdfs-site.xml 변경 내용을 포함 하는 HDFS에 지원 되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 (예: 코드 덤프 파일)의 일부 환경의 및 검색할 수입니다. 배포 후 마스터 인스턴스에서 SA_PASSWORD 다시 설정 해야 합니다. 이 변경은 버그 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)합니다.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp20"></a> CTP 2.0 (2018 년 10 월)

다음 섹션에서는 새로운 기능 및 SQL Server 2019 CTP 2.0에서 빅 데이터 클러스터에 대해 알려진된 문제를 설명합니다.

### <a name="new-features"></a>새로운 기능

- Mssqlctl 관리 도구를 사용 하 여 간단한 배포 환경
- Azure Data Studio에서 네이티브 전자 필기장 환경
- 쿼리 저장소 SQL Server 인스턴스를 통해 HDFS 파일
- 마스터 SQL Server, Oracle, MongoDB, HDFS를 통해 데이터 가상화
- SQL Server 및 Azure Data Studio에서 Oracle 데이터 가상화 마법사
- 마스터 ML 서비스
- 모니터링 및 문제 해결에 사용할 수 있는 클러스터 관리 포털
- Azure Data Studio에서 Spark 작업 제출 
- 클러스터 관리 포털에서 Spark UI
- 저장소 클래스에 탑재 된 볼륨
- 마스터에서 데이터 풀에 대 한 쿼리
- SSMS에서 분산된 쿼리 계획을 보여 줍니다.
- Mssqlctl 관리 도구에 대 한 pip 패키지
- 컨트롤러 서비스를 통해 기본 제공 배포 엔진

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 CTP 2.0에서 SQL Server 빅 데이터 클러스터에 대해 알려진된 문제를 제공합니다.

#### <a name="deployment"></a>배포

- Azure Kubernetes Service (AKS)를 사용 하는 경우 권장 되는 Kubernetes 버전이 1.10. *, 디스크 크기 조정 지원 하지 않는 합니다. 그에 따라 저장소 크기 해야 배포 시. 저장소 크기를 조정 하는 방법에 대 한 자세한 내용은 참조는 [데이터 지 속성](concept-data-persistence.md) 문서. Vm에 배포 된 kubernetes의 경우 권장 되는 버전 1.11입니다.

- AKS를 배포한 후 배포에서 다음 두 경고 이벤트를 볼 수 있습니다. 이러한 이벤트는 알려진 문제, 있지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포를 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패 하면 연결된 된 네임 스페이스 제거 되지 않습니다. 이 클러스터에서 분리 된 네임 스페이스를 발생할 수 있습니다. 동일한 이름 사용 하 여 클러스터를 배포 하기 전에 네임 스페이스를 수동으로 삭제 됩니다.

#### <a name="external-tables"></a>외부 테이블

- 지원 되지 않는 열 형식에는 테이블에 대 한 데이터 풀 외부 테이블을 만들 가능성이 있습니다. 외부 테이블을 쿼리 하는 경우 메시지가 다음과 비슷합니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 오류가 발생할 수 있습니다는 동시에 기본 파일은 HDFS에 복사 되는 경우.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 및 notebook

- POD IP 주소는 Pod 다시 시작으로 Kubernetes 환경에서 변경 될 수 있습니다. 마스터 pod를 다시 시작 되는 시나리오에서 Spark 세션을 사용 하 여 못할 `NoRoteToHostException`합니다. 이 새 IP를 사용 하 여 새로 고쳐지는 가져오기 하지 JVM 캐시 주소입니다.

- Windows에 이미 설치 된 Jupyter 및 별도 Python을 있다면 Spark 노트북 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북을 클릭할 경우에 **텍스트 추가** 명령, 텍스트 셀이 편집 모드 보다는 미리 보기 모드에서 추가 됩니다. 편집 모드에 있고 셀을 편집 하 여 전환한 다음 미리 보기 아이콘을 클릭할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- 미리 HDFS의 파일을 마우스 오른쪽 단추로 클릭 하는 경우 다음 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재는 Azure Data Studio에서 30 MB 보다 큰 파일을 미리 볼 수 없습니다.

- 구성 변경 내용은 hdfs-site.xml 변경 내용을 포함 하는 HDFS에 지원 되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 (예: 코드 덤프 파일)의 일부 환경의 및 검색할 수입니다. 배포 후 마스터 인스턴스에서 SA_PASSWORD 다시 설정 해야 합니다. 이 변경은 버그 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)합니다.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.
