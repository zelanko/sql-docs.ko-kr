---
title: 릴리스 정보
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 (미리 보기)의 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 최신 업데이트 및 알려진 문제에 대해 설명 합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bcbc3537a6ba26dc907bf348c565939ff869ea43
ms.sourcegitcommit: da8bb7abd256b2bebee7852dc0164171eeff11be
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70988102"
---
# <a name="release-notes-for-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터의 릴리스 정보

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 최신 버전의 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대 한 업데이트 및 알려진 문제를 나열 합니다.

## <a id="rc"></a>릴리스 후보 (8 월)

다음 섹션에서는 SQL Server 2019 릴리스 후보에 있는 빅 데이터 클러스터의 새로운 기능 및 알려진 문제에 대해 설명 합니다.

### <a name="whats-new"></a>What's New

|새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
|Always On 가용성 그룹 SQL Server |SQL Server 빅 데이터 클러스터를 배포 하는 경우 다음을 제공 하는 가용성 그룹을 만들도록 배포를 구성할 수 있습니다.<br/><br/>-고가용성 <br/><br/>-읽기-축소 <br/><br/>-데이터 풀에 데이터를 삽입 하는 스케일 아웃<br/><br>[고가용성을 사용 하 여 배포를](../big-data-cluster/deployment-high-availability.md)참조 하세요. |
|`azdata` |[설치 관리자](./deploy-install-azdata-linux-package.md) 를 사용 하는 도구에 대 한 간단한 설치<br/><br/>[`azdata notebook`명령](./reference-azdata-notebook.md)<br/><br/>[`azdata bdc status`명령](./reference-azdata-bdc-status.md) |
|Azure Data Studio|[Azure Data Studio의 릴리스 후보 빌드를 다운로드](deploy-big-data-tools.md#download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc)합니다.<br/><br/>SQL Server 2019 가이드 Jupyter 책을 통해 전자 필기장 문제 해결을 추가 했습니다.<br/><br/>컨트롤러 로그인 환경이 추가 되었습니다.<br/><br/>서비스 끝점을 확인 하 고, 클러스터 상태를 보고, 노트북 문제 해결을 위한 컨트롤러 대시보드가 추가 되었습니다.<br/><br/>향상 된 노트북 셀 출력/편집 성능.|
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

* SQL Server 2019 빅 데이터 클러스터 릴리스 후보 새로 고침 빌드 번호 `15.0.1900.47`는입니다.

* "Kubeadm" 배포 프로필은 위의 빌드 번호를 사용 하는 SQL Server 2019 빅 데이터 클러스터 릴리스 후보에서 지원 되지 않습니다. 대신, Kubeadm 배포에 대해 "kubeadm" 프로필을 사용 합니다.

## <a id="ctp32"></a>CTP 3.2(7월)

다음 섹션에서는 SQL Server 2019 CTP 3.2 빅 데이터 클러스터의 새로운 기능 및 알려진 문제를 설명합니다.

### <a name="whats-new"></a>What's New

|새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
|퍼블릭 미리 보기 |CTP 3.2 이전에는 등록한 얼리어답터가 SQL Server 빅 데이터 클러스터를 사용할 수 있었습니다. 이번 릴리스에서는 누구나 빅 데이터 클러스터 SQL Server 기능을 경험할 수 있습니다. <br/><br/> [시작 하기를 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](deploy-get-started.md)참조 하세요.|
|`azdata` |CTP 3.2는 클러스터 관리자가 REST API를 통해 빅 데이터 클러스터를 부트스트랩하고 관리할 수 있도록 하는 Python으로 작성된 `azdata` 명령줄 유틸리티를 도입했습니다. `azdata`는 `mssqlctl`을 대신합니다. [`azdata` 설치](deploy-install-azdata.md)를 참조하세요. |
|PolyBase |이제 외부 테이블 열 이름이 SQL Server, Oracle, Teradata, MongoDB 및 ODBC 데이터 원본을 쿼리하는 데 사용됩니다. 이전 CTP 릴리스에서는 외부 데이터 원본의 열이 전적으로 서수 위치에 따라 바인딩되고 EXTERNAL TABLE 정의에 지정된 이름이 사용되지 않았습니다. |
|HDFS 계층화 새로 고침 |원격 데이터의 최신 스냅숏에 대해 기존 탑재를 새로 고칠 수 있도록 HDFS 계층화의 새로 고침 기능을 도입합니다. [HDFS 계층화](hdfs-tiering.md)를 참조하세요. |
|Notebook 기반 문제 해결 |CTP 3.2에서는 SQL Server 빅 데이터 클러스터 구성 요소의 [배포](deploy-notebooks.md)와 [검색, 진단 및 문제 해결](manage-notebooks.md)에 도움이 되는 Jupyter Notebook이 도입되었습니다. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 이 릴리스의 알려진 문제 및 제한 사항을 설명합니다.

#### <a name="polybase"></a>PolyBase

- 이 릴리스에서는 개수가 1000개를 초과할 경우 TOP 절의 푸시다운이 지원되지 않습니다. 이 경우 원격 데이터 원본의 모든 행을 읽습니다. (릴리스 후보에서 수정 됨)

- 이 릴리스에서는 외부 데이터 원본에 대한 공동 배치 조인의 푸시다운이 지원되지 않습니다. 예를 들어 ROUND_ROBIN 배포 유형의 데이터 풀 테이블 2개를 푸시다운하면 조인 작업을 수행하기 위해 SQL 마스터 인스턴스 또는 컴퓨팅 풀 인스턴스로 데이터를 가져옵니다.

#### <a name="compute-pool"></a>컴퓨팅 풀

- 빅 데이터 클러스터 배포는 인스턴스 1개가 포함된 컴퓨팅 풀만 지원합니다. (릴리스 후보에서 수정 됨)

#### <a name="storage-pool"></a>스토리지 풀

- 스토리지 풀의 parquet 파일을 쿼리할 때 특정 데이터 형식은 지원되지 않습니다.

- 연결된 형식이 없는 부모 열뿐만 아니라 MAP 및 LIST 부모 열도 쿼리할 수 없습니다. 오류가 반환됩니다.

- REPEATED 노드는 쿼리할 수 없으며 잘못된 결과가 반환될 수 있습니다.

## <a id="ctp31"></a> CTP 3.1(6월)

다음 섹션에서는 SQL Server 2019 CTP 3.1 빅 데이터 클러스터의 새로운 기능 및 알려진 문제를 설명합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| `mssqlctl` 명령 변경 내용 | `mssqlctl cluster` 명령이 `mssqlctl bdc`로 변경되었습니다. 자세한 내용은 [`mssqlctl`참조](reference-azdata.md)를 참조하세요. |
| 새로운 `mssqlctl` 상태 명령 및 클러스터 관리 포털 제거 | 이 릴리스에서는 클러스터 관리 포털이 제거 되었습니다. 기존의 모니터링 명령을 보완하는 새로운 상태 명령이 `mssqlctl`에 추가되었습니다. |
| Spark 컴퓨팅 풀 | 추가 노드를 생성하여 스토리지를 확장하지 않고도 Spark 컴퓨팅 성능을 향상시킬 수 있습니다. 또한 Spark에 사용되지 않는 스토리지 풀 노드를 시작할 수도 있습니다. Spark와 스토리지는 분리됩니다. 자세한 내용은 [spark없이 스토리지 구성](deployment-custom-configuration.md#sparkstorage)을 참조하세요. |
| MSSQL Spark 커넥터 | 데이터 풀 외부 테이블에 대한 읽기/쓰기를 지원합니다. 이전 릴리스에서는 MASTER 인스턴스 테이블에만 읽기/쓰기를 지원했습니다. 자세한 내용은 [MSSQL Spark 커넥터를 사용하여 Spark에서 SQL Server에 읽고 쓰는 방법](spark-mssql-connector.md)을 참조하세요. |
| MLeap를 사용하여 기계 학습 | [Spark에서 MLeap 기계 학습 모델을 교육하고 Java 언어 확장을 사용하여 SQL Server에서 평가합니다](spark-create-machine-learning-model.md). |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 이 릴리스의 알려진 문제 및 제한 사항을 설명합니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭하여 미리 보는 경우 다음과 같은 오류가 표시될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재, Azure Data Studio에서 30MB보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- hdfs-site.xml 변경을 포함하는 HDFS의 구성 변경은 지원되지 않습니다.

#### <a name="deployment"></a>배포

- 이전 릴리스의 빅 데이터 클러스터를 업그레이드할 수 없습니다.

   > [!IMPORTANT]
   > 최신 릴리스를 배포하기 전에 데이터를 백업하고 기존 빅 데이터 클러스터(이전 버전의 **azdata** 사용)를 삭제해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조하세요.

- AKS에 배포한 후 배포에서 다음 두 가지 경고 이벤트가 표시될 수 있습니다. 두 이벤트는 모두 알려진 문제이지만 무시하고 AKS에 빅 데이터 클러스터를 배포할 수 있습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패해도 연결된 네임스페이스는 제거되지 않습니다. 이로 인해 클러스터에 연결 없는 네임스페이스가 생성될 수 있습니다. 해결 방법은 동일한 이름의 클러스터를 배포하기 전에 수동으로 네임스페이스를 삭제하는 것입니다.

#### <a name="external-tables"></a>외부 테이블

- 빅 데이터 클러스터 배포는 더 이상 **SqlDataPool** 및 **SqlStoragePool** 외부 데이터 원본을 만들지 않습니다. 데이터 풀과 스토리지 풀로 데이터 가상화를 지원하기 위해 이 데이터 원본을 수동으로 만들 수 있습니다.

   > [!NOTE]
   > 이러한 외부 데이터 원본을 만들기 위한 URI는 CTP마다 다릅니다. 만드는 방법을 확인하려면 아래 Transact-SQL 명령을 참조하세요. 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 지원되지 않는 열 유형이 있는 테이블의 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리하면 다음과 유사한 메시지가 표시됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 스토리지 풀 외부 테이블을 쿼리하는 경우 기본 파일이 동시에 HDFS로 복사되고 있으면 오류가 표시될 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용하는 외부 테이블을 Oracle에 만드는 경우 Azure Data Studio 가상화 마법사는 외부 테이블 정의에서 해당 열을 VARCHAR로 해석합니다. 이로 인해 외부 테이블 DDL에서 오류가 발생합니다. NVARCHAR2 형식을 사용하도록 Oracle 스키마를 수정하거나, 마법사를 사용하는 대신 수동으로 EXTERNAL TABLE 문을 만들고 NVARCHAR를 지정합니다.

#### <a name="application-deployment"></a>애플리케이션 배포

- RESTful API에서 R, Python 또는 MLeap 애플리케이션을 호출하는 경우 5분 후에 호출이 시간 초과됩니다.

#### <a name="spark-and-notebooks"></a>Spark 및 Notebook

- Pod를 다시 시작하면 Kubernetes 환경에서 Pod IP 주소가 변경될 수 있습니다. master-Pod가 다시 시작되는 시나리오에서는 `NoRoteToHostException`이 발생하고 Spark 세션이 실패할 수 있습니다. 이 오류는 JVM 캐시가 새 IP 주소로 새로 고쳐지지 않기 때문에 발생합니다.

- Jupyter가 이미 설치되어 있고 Windows에 별도의 Python이 있는 경우 Spark Notebook이 실패할 수 있습니다. 이 문제를 해결하려면 Jupyter를 최신 버전으로 업그레이드합니다.

- Notebook에서 **텍스트 추가** 명령을 클릭하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가됩니다. 미리 보기 아이콘을 클릭하여 편집 모드로 전환한 다음, 셀을 편집할 수 있습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부이며 코드 덤프 파일 등에서 검색될 수 있습니다. 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정해야 합니다. 이 이슈는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경하는 방법에 대한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조하세요.

- AKS 로그에 빅 데이터 클러스터 배포의 SA 암호가 포함될 수 있습니다.

#### <a name="kibana-logs-dashboards"></a>Kibana 로그 대시보드

- Aris CTP 3.0과 3.1 사이에서 Kibana 버전이 6.3.1에서 7.0.1로 업그레이드되었습니다.  그러면 Microsoft Edge 브라우저가 Kibana와 호환 되지 않습니다. 사용자는 Microsoft Edge에서 Kibana 대시보드의 현재 버전을 로드할 때 빈 페이지를 표시 합니다. Kibana.rs에 대해 지원되는 브라우저를 보려면 [여기]( https://www.elastic.co/support/matrix#matrix_browse)를 참조하세요. 


## <a id="ctp30"></a> CTP 3.0(5월)

다음 섹션에서는 SQL Server 2019 CTP 3.0 빅 데이터 클러스터의 새로운 기능 및 알려진 문제를 설명합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| **mssqlctl** 업데이트 | 여러 **mssqlctl** [명령 및 매개 변수가 업데이트되었습니다](reference-azdata.md). 예를 들어 **mssqlctl login** 명령은 이제 컨트롤러 사용자 이름 및 엔드포인트를 대상으로 하도록 업데이트되었습니다. |
| 스트리지 향상 | 로그 및 데이터에 대해 서로 다른 스토리지 구성을 지원합니다. 또한 빅 데이터 클러스터에 대한 영구적 볼륨 클레임 수가 감소했습니다. |
| 여러 컴퓨팅 풀 인스턴스 | 여러 컴퓨팅 풀 인스턴스를 지원합니다. |
| 새 풀 동작 및 기능 | 컴퓨팅 풀은 이제 **ROUND_ROBIN** 배포에서만 스토리지 풀 및 데이터 풀 작업에 대해 기본적으로 사용됩니다. 데이터 풀은 새로운 **REPLICATED** 배포 형식을 사용할 수 있습니다. 즉, 모든 데이터 풀 인스턴스에 동일한 데이터가 존재할 수 있습니다. |
| 외부 테이블 개선 | HADOOP 데이터 원본 형식의 외부 테이블은 이제 최대 1 MB 크기의 행 읽기를 지원합니다. 외부 테이블(ODBC, 스토리지 풀, 데이터 풀)은 이제 SQL Server 테이블만큼 폭이 넓은 행을 지원합니다. |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 이 릴리스의 알려진 문제 및 제한 사항을 설명합니다.

#### <a name="hdfs"></a>HDFS

- HDFS에 새 폴더를 만들려고 하면 Azure Data Studio에서 오류가 반환됩니다. 이 기능을 사용하려면 Azure Data Studio 참가자 빌드를 설치합니다.
  
   - [Windows 사용자 설치 관리자 - **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Windows 시스템 설치 관리자 - **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [Windows ZIP - **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [macOS ZIP - **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [Linux TAR.GZ - **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭하여 미리 보는 경우 다음과 같은 오류가 표시될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재, Azure Data Studio에서 30MB보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- hdfs-site.xml 변경을 포함하는 HDFS의 구성 변경은 지원되지 않습니다.

#### <a name="deployment"></a>배포

- GPU 사용이 가능한 빅 데이터 클러스터의 이전 배포 절차는 CTP 3.0에서 지원되지 않습니다. 대체 배포 절차를 조사 중입니다. 당분간 “GPU 지원을 사용하여 빅 데이터 클러스터 배포 및 TensorFlow 실행” 문서는 혼동을 피하기 위해 일시적으로 게시가 취소되었습니다.

- 이전 릴리스의 빅 데이터 클러스터를 업그레이드할 수 없습니다.

   > [!IMPORTANT]
   > 최신 릴리스를 배포하기 전에 데이터를 백업하고 기존 빅 데이터 클러스터(이전 버전의 **azdata** 사용)를 삭제해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조하세요.

- AKS에 배포한 후 배포에서 다음 두 가지 경고 이벤트가 표시될 수 있습니다. 두 이벤트는 모두 알려진 문제이지만 무시하고 AKS에 빅 데이터 클러스터를 배포할 수 있습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패해도 연결된 네임스페이스는 제거되지 않습니다. 이로 인해 클러스터에 연결 없는 네임스페이스가 생성될 수 있습니다. 해결 방법은 동일한 이름의 클러스터를 배포하기 전에 수동으로 네임스페이스를 삭제하는 것입니다.

#### <a name="external-tables"></a>외부 테이블

- 빅 데이터 클러스터 배포는 더 이상 **SqlDataPool** 및 **SqlStoragePool** 외부 데이터 원본을 만들지 않습니다. 데이터 풀과 스토리지 풀로 데이터 가상화를 지원하기 위해 이 데이터 원본을 수동으로 만들 수 있습니다.

   > [!NOTE]
   > 이러한 외부 데이터 원본을 만들기 위한 URI는 CTP마다 다릅니다. 만드는 방법을 확인하려면 아래 Transact-SQL 명령을 참조하세요. 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 지원되지 않는 열 유형이 있는 테이블의 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리하면 다음과 유사한 메시지가 표시됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 스토리지 풀 외부 테이블을 쿼리하는 경우 기본 파일이 동시에 HDFS로 복사되고 있으면 오류가 표시될 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용하는 외부 테이블을 Oracle에 만드는 경우 Azure Data Studio 가상화 마법사는 외부 테이블 정의에서 해당 열을 VARCHAR로 해석합니다. 이로 인해 외부 테이블 DDL에서 오류가 발생합니다. NVARCHAR2 형식을 사용하도록 Oracle 스키마를 수정하거나, 마법사를 사용하는 대신 수동으로 EXTERNAL TABLE 문을 만들고 NVARCHAR를 지정합니다.

#### <a name="application-deployment"></a>애플리케이션 배포

- RESTful API에서 R, Python 또는 MLeap 애플리케이션을 호출하는 경우 5분 후에 호출이 시간 초과됩니다.

#### <a name="spark-and-notebooks"></a>Spark 및 Notebook

- Pod를 다시 시작하면 Kubernetes 환경에서 Pod IP 주소가 변경될 수 있습니다. master-Pod가 다시 시작되는 시나리오에서는 `NoRoteToHostException`이 발생하고 Spark 세션이 실패할 수 있습니다. 이 오류는 JVM 캐시가 새 IP 주소로 새로 고쳐지지 않기 때문에 발생합니다.

- Jupyter가 이미 설치되어 있고 Windows에 별도의 Python이 있는 경우 Spark Notebook이 실패할 수 있습니다. 이 문제를 해결하려면 Jupyter를 최신 버전으로 업그레이드합니다.

- Notebook에서 **텍스트 추가** 명령을 클릭하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가됩니다. 미리 보기 아이콘을 클릭하여 편집 모드로 전환한 다음, 셀을 편집할 수 있습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부이며 코드 덤프 파일 등에서 검색될 수 있습니다. 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정해야 합니다. 이 이슈는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경하는 방법에 대한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조하세요.

- AKS 로그에 빅 데이터 클러스터 배포의 SA 암호가 포함될 수 있습니다.

## <a id="ctp25"></a> CTP 2.5(4월)

다음 섹션에서는 SQL Server 2019 CTP 2.5 빅 데이터 클러스터의 새로운 기능 및 알려진 문제를 설명합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| 배포 프로필 | 환경 변수 대신 빅 데이터 클러스터 배포를 위해 기본 및 사용자 지정된 [배포 구성 JSON 파일](deployment-guidance.md#configfile)을 사용합니다. |
| 프롬프트된 배포 | `azdata cluster create`는 이제 기본 배포에 필요한 설정을 묻는 메시지를 표시합니다. |
| 서비스 엔드포인트 및 pod 이름 변경 | 다음 외부 엔드포인트의 이름이 변경되었습니다.<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| **azdata** 개선 사항 | **azdata**를 사용하여 [외부 엔드포인트를 나열](deployment-guidance.md#endpoints)하고 **azdata**의 버전을 `--version` 매개 변수로 확인합니다. |
| 오프라인 설치 | 오프라인 빅 데이터 클러스터 배포에 대한 지침 |
| HDFS 계층화 개선 사항 | S3 계층화, 탑재 캐싱, ADLS Gen2에 대한 OAuth 지원 |
| 새로운 `mssql` Spark-SQL Server 커넥터 | |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 이 릴리스의 알려진 문제 및 제한 사항을 설명합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스의 빅 데이터 클러스터를 업그레이드할 수 없습니다.

   > [!IMPORTANT]
   > 최신 릴리스를 배포하기 전에 데이터를 백업하고 기존 빅 데이터 클러스터(이전 버전의 **azdata** 사용)를 삭제해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조하세요.

- AKS에 배포한 후 배포에서 다음 두 가지 경고 이벤트가 표시될 수 있습니다. 두 이벤트는 모두 알려진 문제이지만 무시하고 AKS에 빅 데이터 클러스터를 배포할 수 있습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패해도 연결된 네임스페이스는 제거되지 않습니다. 이로 인해 클러스터에 연결 없는 네임스페이스가 생성될 수 있습니다. 해결 방법은 동일한 이름의 클러스터를 배포하기 전에 수동으로 네임스페이스를 삭제하는 것입니다.

#### <a name="external-tables"></a>외부 테이블

- 빅 데이터 클러스터 배포는 더 이상 **SqlDataPool** 및 **SqlStoragePool** 외부 데이터 원본을 만들지 않습니다. 데이터 풀과 스토리지 풀로 데이터 가상화를 지원하기 위해 이 데이터 원본을 수동으로 만들 수 있습니다.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- 지원되지 않는 열 유형이 있는 테이블의 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리하면 다음과 유사한 메시지가 표시됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 스토리지 풀 외부 테이블을 쿼리하는 경우 기본 파일이 동시에 HDFS로 복사되고 있으면 오류가 표시될 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용하는 외부 테이블을 Oracle에 만드는 경우 Azure Data Studio 가상화 마법사는 외부 테이블 정의에서 해당 열을 VARCHAR로 해석합니다. 이로 인해 외부 테이블 DDL에서 오류가 발생합니다. NVARCHAR2 형식을 사용하도록 Oracle 스키마를 수정하거나, 마법사를 사용하는 대신 수동으로 EXTERNAL TABLE 문을 만들고 NVARCHAR를 지정합니다.

#### <a name="application-deployment"></a>애플리케이션 배포

- RESTful API에서 R, Python 또는 MLeap 애플리케이션을 호출하는 경우 5분 후에 호출이 시간 초과됩니다.

#### <a name="spark-and-notebooks"></a>Spark 및 Notebook

- Pod를 다시 시작하면 Kubernetes 환경에서 Pod IP 주소가 변경될 수 있습니다. master-Pod가 다시 시작되는 시나리오에서는 `NoRoteToHostException`이 발생하고 Spark 세션이 실패할 수 있습니다. 이 오류는 JVM 캐시가 새 IP 주소로 새로 고쳐지지 않기 때문에 발생합니다.

- Jupyter가 이미 설치되어 있고 Windows에 별도의 Python이 있는 경우 Spark Notebook이 실패할 수 있습니다. 이 문제를 해결하려면 Jupyter를 최신 버전으로 업그레이드합니다.

- Notebook에서 **텍스트 추가** 명령을 클릭하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가됩니다. 미리 보기 아이콘을 클릭하여 편집 모드로 전환한 다음, 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭하여 미리 보는 경우 다음과 같은 오류가 표시될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재, Azure Data Studio에서 30MB보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- hdfs-site.xml 변경을 포함하는 HDFS의 구성 변경은 지원되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부이며 코드 덤프 파일 등에서 검색될 수 있습니다. 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정해야 합니다. 이 이슈는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경하는 방법에 대한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조하세요.

- AKS 로그에 빅 데이터 클러스터 배포의 SA 암호가 포함될 수 있습니다.

## <a id="ctp24"></a> CTP 2.4(3월)

다음 섹션에서는 SQL Server 2019 CTP 2.4 빅 데이터 클러스터의 새로운 기능 및 알려진 문제를 설명합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| Spark에서 TensorFlow를 사용하여 딥 러닝을 실행하기 위한 GPU 지원 지침. | [GPU 지원이 포함된 빅 데이터 클러스터를 배포하고 TensorFlow를 실행](spark-gpu-tensorflow.md)합니다. |
| **SqlDataPool** 및 **SqlStoragePool** 데이터 원본은 더 이상 기본적으로 생성되지 않습니다. | 필요에 따라 수동으로 만듭니다. [알려진 문제](#externaltablesctp24)를 참조하세요. |
| `INSERT INTO SELECT`가 데이터 풀을 지원합니다. | 예제를 보려면 [ 자습서: Transact-SQL을 사용하여 SQL Server 데이터 풀에 데이터 수집](tutorial-data-pool-ingest-sql.md)을 참조하세요. |
| `FORCE SCALEOUTEXECUTION` 및 `DISABLE SCALEOUTEXECUTION` 옵션. | 외부 테이블에 대한 쿼리에 컴퓨팅 풀을 강제로 사용하거나 사용하지 않도록 설정합니다. 예를 들어, `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)`을 입력합니다. |
| AKS 배포 권장 사항을 업데이트합니다. | AKS에서 빅 데이터 클러스터를 평가할 때 이제 **Standard_L8s** 크기의 단일 노드를 사용하는 것이 좋습니다. |
| Spark 런타임을 Spark 런타임 2.4로 업그레이드합니다. | |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 이 릴리스의 알려진 문제 및 제한 사항을 설명합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스의 빅 데이터 클러스터를 업그레이드할 수 없습니다.

   > [!IMPORTANT]
   > 최신 릴리스를 배포하기 전에 데이터를 백업하고 기존 빅 데이터 클러스터(이전 버전의 **azdata** 사용)를 삭제해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조하세요.

- AKS에 배포한 후 배포에서 다음 두 가지 경고 이벤트가 표시될 수 있습니다. 두 이벤트는 모두 알려진 문제이지만 무시하고 AKS에 빅 데이터 클러스터를 배포할 수 있습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패해도 연결된 네임스페이스는 제거되지 않습니다. 이로 인해 클러스터에 연결 없는 네임스페이스가 생성될 수 있습니다. 해결 방법은 동일한 이름의 클러스터를 배포하기 전에 수동으로 네임스페이스를 삭제하는 것입니다.

#### <a name="kubeadm-deployments"></a>kubeadm 배포

kubeadm을 사용하여 여러 머신에 Kubernetes를 배포하는 경우 빅 데이터 클러스터에 연결하는 데 필요한 엔드포인트가 클러스터 관리 포털에 올바르게 표시되지 않습니다. 이 문제가 발생하는 경우 다음 해결 방법을 사용하여 서비스 엔드포인트 IP 주소를 검색합니다.

- 클러스터 내에서 연결하는 경우 연결하려는 엔드포인트의 서비스 IP를 Kubernetes에서 쿼리합니다. 예를 들어 다음 **kubectl** 명령은 SQL Server 마스터 인스턴스의 IP 주소를 표시합니다.

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 클러스터 외부에서 연결하는 경우 다음 단계를 사용하여 연결합니다.

   1. SQL Server 마스터 인스턴스를 실행하는 노드의 IP 주소를 가져옵니다. `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`

   1. 이 IP 주소를 사용하여 SQL Server 마스터 인스턴스에 연결합니다.

   1. master 데이터베이스의 **cluster_endpoint_table**에서 다른 외부 엔드포인트를 쿼리합니다.

      연결 시간 초과로 인해 실패하는 경우 해당 노드에서 방화벽을 사용하는 것일 수 있습니다. 이 경우 Kubernetes 클러스터 관리자에게 외부에 공개된 노드 IP를 문의해야 합니다. 이 노드는 임의 노드일 수 있습니다. 그런 다음, 해당 IP와 포트를 사용하여 클러스터에서 실행되는 다양한 서비스에 연결할 수 있습니다. 예를 들어 관리자는 다음을 실행하여 이 IP를 찾을 수 있습니다.

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>클러스터 삭제 실패

**azdata**를 사용하여 클러스터를 삭제하려고 하면 다음 오류가 발생하고 실패합니다.

```
2019-03-26 20:38:11.0614 UTC | INFO | Deleting cluster ...
Error processing command: "TypeError"
delete_namespaced_service() takes 3 positional arguments but 4 were given
Makefile:61: recipe for target 'delete-cluster' failed
make[2]: *** [delete-cluster] Error 1
Makefile:223: recipe for target 'deploy-clean' failed
make[1]: *** [deploy-clean] Error 2
Makefile:203: recipe for target 'deploy-clean' failed
make: *** [deploy-clean] Error 2
```

새 Python Kubernetes 클라이언트(버전 9.0.0)에서 네임스페이스 삭제 API가 변경되었으며, 이로 인해 현재 **azdata**가 중단됩니다. 이 오류는 최신 Kubernetes python 클라이언트가 설치된 경우에만 발생합니다. **kubectl**(`kubectl delete ns <ClusterName>`)을 통해 클러스터를 직접 삭제하여 이 문제를 해결하거나, `sudo pip install kubernetes==8.0.1`을 사용하여 이전 버전을 설치할 수 있습니다.

#### <a id="externaltablesctp24"></a> 외부 테이블

- 빅 데이터 클러스터 배포는 더 이상 **SqlDataPool** 및 **SqlStoragePool** 외부 데이터 원본을 만들지 않습니다. 데이터 풀과 스토리지 풀로 데이터 가상화를 지원하기 위해 이 데이터 원본을 수동으로 만들 수 있습니다.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- 지원되지 않는 열 유형이 있는 테이블의 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리하면 다음과 유사한 메시지가 표시됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 스토리지 풀 외부 테이블을 쿼리하는 경우 기본 파일이 동시에 HDFS로 복사되고 있으면 오류가 표시될 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용하는 외부 테이블을 Oracle에 만드는 경우 Azure Data Studio 가상화 마법사는 외부 테이블 정의에서 해당 열을 VARCHAR로 해석합니다. 이로 인해 외부 테이블 DDL에서 오류가 발생합니다. NVARCHAR2 형식을 사용하도록 Oracle 스키마를 수정하거나, 마법사를 사용하는 대신 수동으로 EXTERNAL TABLE 문을 만들고 NVARCHAR를 지정합니다.

#### <a name="application-deployment"></a>애플리케이션 배포

- RESTful API에서 R, Python 또는 MLeap 애플리케이션을 호출하는 경우 5분 후에 호출이 시간 초과됩니다.

#### <a name="spark-and-notebooks"></a>Spark 및 Notebook

- Pod를 다시 시작하면 Kubernetes 환경에서 Pod IP 주소가 변경될 수 있습니다. master-Pod가 다시 시작되는 시나리오에서는 `NoRoteToHostException`이 발생하고 Spark 세션이 실패할 수 있습니다. 이 오류는 JVM 캐시가 새 IP 주소로 새로 고쳐지지 않기 때문에 발생합니다.

- Jupyter가 이미 설치되어 있고 Windows에 별도의 Python이 있는 경우 Spark Notebook이 실패할 수 있습니다. 이 문제를 해결하려면 Jupyter를 최신 버전으로 업그레이드합니다.

- Notebook에서 **텍스트 추가** 명령을 클릭하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가됩니다. 미리 보기 아이콘을 클릭하여 편집 모드로 전환한 다음, 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭하여 미리 보는 경우 다음과 같은 오류가 표시될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재, Azure Data Studio에서 30MB보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- hdfs-site.xml 변경을 포함하는 HDFS의 구성 변경은 지원되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부이며 코드 덤프 파일 등에서 검색될 수 있습니다. 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정해야 합니다. 이 이슈는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경하는 방법에 대한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조하세요.

- AKS 로그에 빅 데이터 클러스터 배포의 SA 암호가 포함될 수 있습니다.

## <a id="ctp23"></a> CTP 2.3(2월)

다음 섹션에서는 SQL Server 2019 CTP 2.3 빅 데이터 클러스터의 새로운 기능 및 알려진 문제를 설명합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
| :---------- | :------ |
| IntelliJ의 빅 데이터 클러스터에 Spark 작업을 제출합니다. | [IntelliJ의에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Spark 작업 제출](spark-submit-job-intellij-tool-plugin.md) |
| 애플리케이션 배포 및 클러스터 관리를 위한 일반 CLI. | [앱을 배포 하는 방법[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-create-apps.md) |
| 애플리케이션을 빅 데이터 클러스터에 배포하기 위한 VS Code 확장. | [VS Code를 사용 하 여 응용 프로그램을 배포 하는 방법[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](app-deployment-extension.md) |
| **azdata** 도구 명령 사용법 변경 | 자세한 내용은 [azdata의 알려진 문제](#azdatactp23)를 참조하세요. |
| 빅 데이터 클러스터에서 Sparklyr 사용 | [SQL Server 2019 빅 데이터 클러스터에서 Sparklyr 사용](sparklyr-from-RStudio.md) |
| **HDFS 계층화**를 통해 빅 데이터 클러스터에 외장 HDFS 호환 스토리지를 탑재합니다. | [HDFS 계층화](hdfs-tiering.md)를 참조하세요 |
| SQL Server 마스터 인스턴스 및 HDFS/Spark 게이트웨이에 대한 새로운 통합 연결 환경. | [SQL Server 마스터 인스턴스 및 HDFS/Spark 게이트웨이](connect-to-big-data-cluster.md)를 참조하세요. |
| 이제 **azdata 클러스터 삭제**를 통해 클러스터를 삭제할 경우 빅 데이터 클러스터에 속한 네임스페이스의 개체만 삭제됩니다. | 네임스페이스는 삭제되지 않습니다. 그러나 이전 릴리스에서 이 명령은 전체 네임스페이스를 삭제했습니다. |
| _보안_ 엔드포인트 이름이 변경되고 통합되었습니다. | **service-security-lb** 및 **service-security-nodeport**가 **endpoint-security** 엔드포인트에 통합되었습니다. |
| _프록시_ 엔드포인트 이름이 변경되고 통합되었습니다. | **service-proxy-lb** 및 **service-proxy-nodeport**가 **endpoint-service-proxy** 엔드포인트에 통합되었습니다. |
| _컨트롤러_ 엔드포인트 이름이 변경되고 통합되었습니다. | **service-mssql-controller-lb** 및 **service-mssql-controller-nodeport**가 **endpoint-controller** 엔드포인트에 통합되었습니다. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 이 릴리스의 알려진 문제 및 제한 사항을 설명합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스의 빅 데이터 클러스터를 업그레이드할 수 없습니다.

   > [!IMPORTANT]
   > 최신 릴리스를 배포하기 전에 데이터를 백업하고 기존 빅 데이터 클러스터(이전 버전의 **azdata** 사용)를 삭제해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조하세요.

- EULA에 동의하려면 **ACCEPT_EULA** 환경 변수가 “yes” 또는 “yes”여야 합니다. 이전 릴리스에서는 “y”와 “Y”를 사용할 수 있었지만 더 이상 허용되지 않으며 배포에 실패합니다.

- 이전 릴리스와 달리 **CLUSTER_PLATFORM** 환경 변수에 기본값이 없습니다.

- AKS에 배포한 후 배포에서 다음 두 가지 경고 이벤트가 표시될 수 있습니다. 두 이벤트는 모두 알려진 문제이지만 무시하고 AKS에 빅 데이터 클러스터를 배포할 수 있습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패해도 연결된 네임스페이스는 제거되지 않습니다. 이로 인해 클러스터에 연결 없는 네임스페이스가 생성될 수 있습니다. 해결 방법은 동일한 이름의 클러스터를 배포하기 전에 수동으로 네임스페이스를 삭제하는 것입니다.

#### <a name="kubeadm-deployments"></a>kubeadm 배포

kubeadm을 사용하여 여러 머신에 Kubernetes를 배포하는 경우 빅 데이터 클러스터에 연결하는 데 필요한 엔드포인트가 클러스터 관리 포털에 올바르게 표시되지 않습니다. 이 문제가 발생하는 경우 다음 해결 방법을 사용하여 서비스 엔드포인트 IP 주소를 검색합니다.

- 클러스터 내에서 연결하는 경우 연결하려는 엔드포인트의 서비스 IP를 Kubernetes에서 쿼리합니다. 예를 들어 다음 **kubectl** 명령은 SQL Server 마스터 인스턴스의 IP 주소를 표시합니다.

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 클러스터 외부에서 연결하는 경우 다음 단계를 사용하여 연결합니다.

   1. SQL Server 마스터 인스턴스를 실행하는 노드의 IP 주소를 가져옵니다. `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`

   1. 이 IP 주소를 사용하여 SQL Server 마스터 인스턴스에 연결합니다.

   1. master 데이터베이스의 **cluster_endpoint_table**에서 다른 외부 엔드포인트를 쿼리합니다.

      연결 시간 초과로 인해 실패하는 경우 해당 노드에서 방화벽을 사용하는 것일 수 있습니다. 이 경우 Kubernetes 클러스터 관리자에게 외부에 공개된 노드 IP를 문의해야 합니다. 이 노드는 임의 노드일 수 있습니다. 그런 다음, 해당 IP와 포트를 사용하여 클러스터에서 실행되는 다양한 서비스에 연결할 수 있습니다. 예를 들어 관리자는 다음을 실행하여 이 IP를 찾을 수 있습니다.

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="azdatactp23"></a> azdata

- **azdata** 도구가 동사-명사 명령 순서에서 명사-동사 순서로 변경되었습니다. 예를 들어 `azdata create cluster`가 이제 `azdata cluster create`입니다.

- 이제 `azdata cluster create`를 사용하여 클러스터를 만들 때 `--name` 매개 변수가 필요합니다.

   ```bash
   azdata cluster create --name <cluster_name>
   ```

- 최신 버전의 빅 데이터 클러스터 및 **azdata**로 업그레이드하는 방법에 대한 중요 정보는 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조하세요.

#### <a name="external-tables"></a>외부 테이블

- 지원되지 않는 열 유형이 있는 테이블의 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리하면 다음과 유사한 메시지가 표시됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 스토리지 풀 외부 테이블을 쿼리하는 경우 기본 파일이 동시에 HDFS로 복사되고 있으면 오류가 표시될 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용하는 외부 테이블을 Oracle에 만드는 경우 Azure Data Studio 가상화 마법사는 외부 테이블 정의에서 해당 열을 VARCHAR로 해석합니다. 이로 인해 외부 테이블 DDL에서 오류가 발생합니다. NVARCHAR2 형식을 사용하도록 Oracle 스키마를 수정하거나, 마법사를 사용하는 대신 수동으로 EXTERNAL TABLE 문을 만들고 NVARCHAR를 지정합니다.

#### <a name="application-deployment"></a>애플리케이션 배포

- RESTful API에서 R, Python 또는 MLeap 애플리케이션을 호출하는 경우 5분 후에 호출이 시간 초과됩니다.

#### <a name="spark-and-notebooks"></a>Spark 및 Notebook

- Pod를 다시 시작하면 Kubernetes 환경에서 Pod IP 주소가 변경될 수 있습니다. master-Pod가 다시 시작되는 시나리오에서는 `NoRoteToHostException`이 발생하고 Spark 세션이 실패할 수 있습니다. 이 오류는 JVM 캐시가 새 IP 주소로 새로 고쳐지지 않기 때문에 발생합니다.

- Jupyter가 이미 설치되어 있고 Windows에 별도의 Python이 있는 경우 Spark Notebook이 실패할 수 있습니다. 이 문제를 해결하려면 Jupyter를 최신 버전으로 업그레이드합니다.

- Notebook에서 **텍스트 추가** 명령을 클릭하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가됩니다. 미리 보기 아이콘을 클릭하여 편집 모드로 전환한 다음, 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭하여 미리 보는 경우 다음과 같은 오류가 표시될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재, Azure Data Studio에서 30MB보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- hdfs-site.xml 변경을 포함하는 HDFS의 구성 변경은 지원되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부이며 코드 덤프 파일 등에서 검색될 수 있습니다. 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정해야 합니다. 이 이슈는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경하는 방법에 대한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조하세요.

- AKS 로그에 빅 데이터 클러스터 배포의 SA 암호가 포함될 수 있습니다.

## <a id="ctp22"></a> CTP 2.2(2018년 12월)

다음 섹션에서는 SQL Server 2019 CTP 2.2 빅 데이터 클러스터의 새로운 기능 및 알려진 문제를 설명합니다.

### <a name="new-features"></a>새 기능

- `/portal`(**https://\<ip-address\>:30777/portal**)을 사용하여 액세스하는 클러스터 관리 포털
- 마스터 풀 서비스 이름이 `service-master-pool-lb` 및 `service-master-pool-nodeport`에서 `endpoint-master-pool`로 변경됨
- 새 버전의 **azdata** 및 업데이트된 이미지
- 기타 버그 수정 및 개선 사항

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 이 릴리스의 알려진 문제 및 제한 사항을 설명합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스의 빅 데이터 클러스터를 업그레이드할 수 없습니다. 최신 릴리스를 배포하기 전에 기존 빅 데이터 클러스터를 백업하고 삭제해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조하세요.

- AKS에 배포한 후 배포에서 다음 두 가지 경고 이벤트가 표시될 수 있습니다. 두 이벤트는 모두 알려진 문제이지만 무시하고 AKS에 빅 데이터 클러스터를 배포할 수 있습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패해도 연결된 네임스페이스는 제거되지 않습니다. 이로 인해 클러스터에 연결 없는 네임스페이스가 생성될 수 있습니다. 해결 방법은 동일한 이름의 클러스터를 배포하기 전에 수동으로 네임스페이스를 삭제하는 것입니다.

#### <a name="cluster-administration-portal"></a>클러스터 관리 포털

클러스터 관리 포털에는 SQL Server 마스터 인스턴스의 엔드포인트가 표시되지 않습니다. 마스터 인스턴스의 IP 주소와 포트를 찾으려면 다음 **kubectl** 명령을 사용합니다.

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

#### <a name="external-tables"></a>외부 테이블

- 지원되지 않는 열 유형이 있는 테이블의 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리하면 다음과 유사한 메시지가 표시됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 스토리지 풀 외부 테이블을 쿼리하는 경우 기본 파일이 동시에 HDFS로 복사되고 있으면 오류가 표시될 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 및 Notebook

- Pod를 다시 시작하면 Kubernetes 환경에서 Pod IP 주소가 변경될 수 있습니다. master-Pod가 다시 시작되는 시나리오에서는 `NoRoteToHostException`이 발생하고 Spark 세션이 실패할 수 있습니다. 이 오류는 JVM 캐시가 새 IP 주소로 새로 고쳐지지 않기 때문에 발생합니다.

- Jupyter가 이미 설치되어 있고 Windows에 별도의 Python이 있는 경우 Spark Notebook이 실패할 수 있습니다. 이 문제를 해결하려면 Jupyter를 최신 버전으로 업그레이드합니다.

- Notebook에서 **텍스트 추가** 명령을 클릭하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가됩니다. 미리 보기 아이콘을 클릭하여 편집 모드로 전환한 다음, 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭하여 미리 보는 경우 다음과 같은 오류가 표시될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재, Azure Data Studio에서 30MB보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- hdfs-site.xml 변경을 포함하는 HDFS의 구성 변경은 지원되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부이며 코드 덤프 파일 등에서 검색될 수 있습니다. 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정해야 합니다. 이 이슈는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경하는 방법에 대한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조하세요.

- AKS 로그에 빅 데이터 클러스터 배포의 SA 암호가 포함될 수 있습니다.

## <a id="ctp21"></a> CTP 2.1(2018년 11월)

다음 섹션에서는 SQL Server 2019 CTP 2.1 빅 데이터 클러스터의 새로운 기능 및 알려진 문제를 설명합니다.

### <a name="new-features"></a>새 기능

- 빅 데이터 클러스터에 [Python 및 R 앱 배포](big-data-cluster-create-apps.md)
- 새 버전의 **azdata** 및 업데이트된 이미지 
- 기타 버그 수정 및 개선 사항

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 CTP 2.1의에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 대 한 알려진 문제를 제공 합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스의 빅 데이터 클러스터를 업그레이드할 수 없습니다. 최신 릴리스를 배포하기 전에 기존 빅 데이터 클러스터를 백업하고 삭제해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조하세요.

- AKS에 배포한 후 배포에서 다음 두 가지 경고 이벤트가 표시될 수 있습니다. 두 이벤트는 모두 알려진 문제이지만 무시하고 AKS에 빅 데이터 클러스터를 배포할 수 있습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패해도 연결된 네임스페이스는 제거되지 않습니다. 이로 인해 클러스터에 연결 없는 네임스페이스가 생성될 수 있습니다. 해결 방법은 동일한 이름의 클러스터를 배포하기 전에 수동으로 네임스페이스를 삭제하는 것입니다.

#### <a name="admin-portal"></a>관리 포털

- [msqlctl-ctp 명령을 사용하여 앱을 만들고](big-data-cluster-create-apps.md) SQL Server 빅 데이터 클러스터에 배포하는 경우 클러스터 관리 포털에서 애플리케이션이 배포된 Pod가 관리 부분의 컨트롤러 섹션에 “알 수 없음”으로 표시됩니다.

#### <a name="external-tables"></a>외부 테이블

- 지원되지 않는 열 유형이 있는 테이블의 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리하면 다음과 유사한 메시지가 표시됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 스토리지 풀 외부 테이블을 쿼리하는 경우 기본 파일이 동시에 HDFS로 복사되고 있으면 오류가 표시될 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 및 Notebook

- Pod를 다시 시작하면 Kubernetes 환경에서 Pod IP 주소가 변경될 수 있습니다. master-Pod가 다시 시작되는 시나리오에서는 `NoRoteToHostException`이 발생하고 Spark 세션이 실패할 수 있습니다. 이 오류는 JVM 캐시가 새 IP 주소로 새로 고쳐지지 않기 때문에 발생합니다.

- Jupyter가 이미 설치되어 있고 Windows에 별도의 Python이 있는 경우 Spark Notebook이 실패할 수 있습니다. 이 문제를 해결하려면 Jupyter를 최신 버전으로 업그레이드합니다.

- Notebook에서 **텍스트 추가** 명령을 클릭하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가됩니다. 미리 보기 아이콘을 클릭하여 편집 모드로 전환한 다음, 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭하여 미리 보는 경우 다음과 같은 오류가 표시될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재, Azure Data Studio에서 30MB보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- hdfs-site.xml 변경을 포함하는 HDFS의 구성 변경은 지원되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부이며 코드 덤프 파일 등에서 검색될 수 있습니다. 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정해야 합니다. 이 이슈는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경하는 방법에 대한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조하세요.

- AKS 로그에 빅 데이터 클러스터 배포의 SA 암호가 포함될 수 있습니다.

## <a id="ctp20"></a> CTP 2.0(2018년 10월)

다음 섹션에서는 SQL Server 2019 CTP 2.0 빅 데이터 클러스터의 새로운 기능 및 알려진 문제를 설명합니다.

### <a name="new-features"></a>새 기능

- azdata 관리 도구를 사용하는 간단한 배포 환경
- Azure Data Studio의 기본 Notebook 환경
- SQL Server 스토리지 인스턴스를 통해 HDFS 파일 쿼리
- 마스터를 통해 SQL Server, Oracle, MongoDB 및 HDFS로 데이터 가상화
- Azure Data Studio의 SQL Server 및 Oracle용 데이터 가상화 마법사
- 마스터의 ML Services
- 모니터링 및 문제 해결에 사용할 수 있는 클러스터 관리 포털
- Azure Data Studio의 Spark 작업 제출 
- 클러스터 관리 포털의 Spark UI
- 스토리지 클래스에 볼륨 탑재
- 마스터에서 데이터 풀 쿼리
- SSMS의 분산 쿼리 실행 계획
- azdata 관리 도구용 Pip 패키지
- 컨트롤러 서비스를 통한 기본 제공 배포 엔진

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 CTP 2.0의에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 대 한 알려진 문제를 제공 합니다.

#### <a name="deployment"></a>배포

- AKS(Azure Kubernetes Service)를 사용하는 경우 Kubernetes의 권장 버전은 1.10.*입니다. 이 버전에서는 디스크 크기 조정이 지원되지 않습니다. 배포 시 스토리지 크기를 적절하게 지정해야 합니다. 스토리지 크기를 조정하는 방법에 대한 자세한 내용은 [데이터 지속성](concept-data-persistence.md) 문서를 참조하세요. VM에 배포되는 Kubernetes의 경우 권장 버전은 1.11입니다.

- AKS에 배포한 후 배포에서 다음 두 가지 경고 이벤트가 표시될 수 있습니다. 두 이벤트는 모두 알려진 문제이지만 무시하고 AKS에 빅 데이터 클러스터를 배포할 수 있습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패해도 연결된 네임스페이스는 제거되지 않습니다. 이로 인해 클러스터에 연결 없는 네임스페이스가 생성될 수 있습니다. 해결 방법은 동일한 이름의 클러스터를 배포하기 전에 수동으로 네임스페이스를 삭제하는 것입니다.

#### <a name="external-tables"></a>외부 테이블

- 지원되지 않는 열 유형이 있는 테이블의 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리하면 다음과 유사한 메시지가 표시됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 스토리지 풀 외부 테이블을 쿼리하는 경우 기본 파일이 동시에 HDFS로 복사되고 있으면 오류가 표시될 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 및 Notebook

- Pod를 다시 시작하면 Kubernetes 환경에서 Pod IP 주소가 변경될 수 있습니다. master-Pod가 다시 시작되는 시나리오에서는 `NoRoteToHostException`이 발생하고 Spark 세션이 실패할 수 있습니다. 이 오류는 JVM 캐시가 새 IP 주소로 새로 고쳐지지 않기 때문에 발생합니다.

- Jupyter가 이미 설치되어 있고 Windows에 별도의 Python이 있는 경우 Spark Notebook이 실패할 수 있습니다. 이 문제를 해결하려면 Jupyter를 최신 버전으로 업그레이드합니다.

- Notebook에서 **텍스트 추가** 명령을 클릭하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가됩니다. 미리 보기 아이콘을 클릭하여 편집 모드로 전환한 다음, 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭하여 미리 보는 경우 다음과 같은 오류가 표시될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재, Azure Data Studio에서 30MB보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- hdfs-site.xml 변경을 포함하는 HDFS의 구성 변경은 지원되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부이며 코드 덤프 파일 등에서 검색될 수 있습니다. 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정해야 합니다. 이 이슈는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경하는 방법에 대한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조하세요.

- AKS 로그에 빅 데이터 클러스터 배포의 SA 암호가 포함될 수 있습니다.

## <a name="next-steps"></a>다음 단계

에 대 한 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]자세한 내용은 [무엇 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]인가요?](big-data-cluster-overview.md)를 참조 하세요.
