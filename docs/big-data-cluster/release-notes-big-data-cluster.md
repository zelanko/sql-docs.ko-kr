---
title: 릴리스 정보
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대 한 최신 업데이트 및 알려진 문제에 대해 설명 합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c0dd96d4a3227fda76921764429b4566e3e5dd28
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419306"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>SQL Server의 빅 데이터 클러스터에 대 한 릴리스 정보

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에는 빅 데이터 클러스터 SQL Server 최신 릴리스에 대 한 업데이트 및 알려진 문제가 나와 있습니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp32"></a>CTP 3.2 (7 월)

다음 섹션에서는 SQL Server 2019 CTP 3.2의 빅 데이터 클러스터에 대 한 새로운 기능 및 알려진 문제에 대해 설명 합니다.

|새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
|공개 미리 보기 |CTP 3.2 이전에는 SQL Server 빅 데이터 클러스터를 등록 하 여 초기에 등록 하는 데 사용할 수 있었습니다. 이 릴리스를 통해 모든 사용자는 빅 데이터 클러스터 SQL Server 기능을 경험할 수 있습니다. <br/><br/> [SQL Server 빅 데이터 클러스터 시작을](deploy-get-started.md)참조 하세요.|
|`azdata` |CTP 3.2 소개 `azdata` -클러스터 관리자가 REST api를 통해 빅 데이터 클러스터를 부트스트랩 하 고 관리할 수 있도록 하는 Python으로 작성 된 명령줄 유틸리티입니다. `azdata`가 `mssqlctl`를 대체합니다. [ 설치`azdata` ](deploy-install-azdata.md)를 참조 하세요. |
|PolyBase |이제 외부 테이블 열 이름이 SQL Server, Oracle, Teradata, MongoDB 및 ODBC 데이터 원본을 쿼리 하는 데 사용 됩니다. |
|HDFS 계층화 새로 고침 |원격 데이터의 최신 스냅숏에 대 한 기존 탑재를 새로 고칠 수 있도록 HDFS 계층화를 위한 새로 고침 기능 소개 [HDFS 계층화](hdfs-tiering.md) 를 참조 하세요. |
|노트북 기반 문제 해결 |CTP 3.2에는 SQL Server 빅 데이터 클러스터의 구성 요소에 대 한 [배포](deploy-notebooks.md) 및 [검색, 진단 및 문제 해결](manage-notebooks.md) 에 도움이 되는 jupyter 노트북이 도입 되었습니다. |
| &nbsp; | &nbsp; |

## <a id="ctp31"></a>CTP 3.1 (6 월)

다음 섹션에서는 SQL Server 2019 CTP 3.1의 빅 데이터 클러스터에 대 한 새로운 기능 및 알려진 문제에 대해 설명 합니다.

|새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
|공개 미리 보기 |CTP 3.2 이전에는 SQL Server 빅 데이터 클러스터를 등록 하 여 초기에 등록 하는 데 사용할 수 있었습니다. 이 릴리스를 통해 모든 사용자는 빅 데이터 클러스터 SQL Server 기능을 경험할 수 있습니다. <br/><br/> [SQL Server 빅 데이터 클러스터 시작을](deploy-get-started.md)참조 하세요.|
|노트북 기반 문제 해결.|CTP 3.2은 SQL Server 빅 데이터 클러스터의 구성 요소에 대 한 [배포](deploy-notebooks.md), [검색, 진단 및 문제 해결](manage-notebooks.md) 을 지원 하기 위해 jupyter 노트북을 소개 합니다. |
|`azdata` |CTP 3.2 소개 `azdata` -클러스터 관리자가 REST api를 통해 빅 데이터 클러스터를 부트스트랩 하 고 관리할 수 있도록 하는 Python으로 작성 된 명령줄 유틸리티입니다. `azdata`가 `mssqlctl`를 대체합니다. [ 설치`azdata` ](deploy-install-azdata.md)를 참조 하세요. |
|HDFS 계층화 새로 고침 |원격 데이터의 최신 스냅숏에 대 한 기존 탑재를 새로 고칠 수 있도록 HDFS 계층화를 위한 새로 고침 기능 소개 [HDFS 계층화](hdfs-tiering.md) 를 참조 하세요. |
| &nbsp; | &nbsp; |

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| `mssqlctl` 명령 변경 내용 | `mssqlctl cluster` 명령이 `mssqlctl bdc`로 변경되었습니다. 자세한 내용은 [`mssqlctl`참조](reference-azdata.md)를 참조하세요. |
| 새 `mssqlctl` 상태 명령 및 클러스터 관리 포털의 제거 | 이 릴리스에서는 클러스터 관리 포털이 제거 되었습니다. 새 상태 명령이 기존 모니터링 명령을 보완 `mssqlctl` 하는에 추가 되었습니다. |
| Spark 컴퓨팅 풀 | 추가 노드를 생성하여 스토리지를 확장하지 않고도 Spark 컴퓨팅 성능을 향상시킬 수 있습니다. 또한 Spark에 사용되지 않는 스토리지 풀 노드를 시작할 수도 있습니다. Spark와 스토리지는 분리됩니다. 자세한 내용은 [spark없이 스토리지 구성](deployment-custom-configuration.md#sparkstorage)을 참조하세요. |
| MSSQL Spark 커넥터 | 데이터 풀 외부 테이블에 대한 읽기/쓰기를 지원합니다. 이전 릴리스에서는 MASTER 인스턴스 테이블에만 읽기/쓰기를 지원했습니다. 자세한 내용은 [MSSQL Spark 커넥터를 사용하여 Spark에서 SQL Server에 읽고 쓰는 방법](spark-mssql-connector.md)을 참조하세요. |
| MLeap를 사용하여 기계 학습 | [Spark에서 MLeap 기계 학습 모델을 교육하고 Java 언어 확장을 사용하여 SQL Server에서 평가합니다](spark-create-machine-learning-model.md). |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는이 릴리스의 알려진 문제 및 제한 사항에 대해 설명 합니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭 하 여 미리 볼 경우 다음과 같은 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재 Azure Data Studio에서 30mb 보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- Hdfs-site.xml에 대 한 변경 내용을 포함 하는 HDFS에 대 한 구성 변경은 지원 되지 않습니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서는 빅 데이터 데이터 클러스터를 업그레이드할 수 없습니다.

   > [!IMPORTANT]
   > 최신 릴리스를 배포 하기 전에 데이터를 백업 하 고 기존 빅 데이터 클러스터 (이전 버전의 **azdata**사용)를 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조 하세요.

- AKS에 배포한 후 배포에서 다음과 같은 두 가지 경고 이벤트가 표시 될 수 있습니다. 이러한 이벤트는 모두 알려진 문제 이지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포 하는 것을 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포가 실패 하면 연결 된 네임 스페이스는 제거 되지 않습니다. 이로 인해 클러스터에 분리 된 네임 스페이스가 생성 될 수 있습니다. 해결 방법은 이름이 같은 클러스터를 배포 하기 전에 수동으로 네임 스페이스를 삭제 하는 것입니다.

#### <a name="external-tables"></a>외부 테이블

- 빅 데이터 클러스터 배포는 더 이상 **SqlDataPool** 및 **sqlstoragepool** 외부 데이터 원본을 생성 하지 않습니다. 데이터 풀 및 저장소 풀에 대 한 데이터 가상화를 지원 하기 위해 이러한 데이터 원본을 수동으로 만들 수 있습니다.

   > [!NOTE]
   > 이러한 외부 데이터 원본을 만들기 위한 URI는 CTPs 간에 다릅니다. 아래 Transact-sql 명령을 참조 하 여 만드는 방법을 확인 하세요. 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 지원 되지 않는 열 유형이 있는 테이블에 대 한 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리 하는 경우 다음과 유사한 메시지가 표시 됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 기본 파일이 HDFS로 동시에 복사 되는 경우 오류가 발생할 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에 외부 테이블을 만드는 경우 Azure Data Studio 가상화 마법사는 외부 테이블 정의에서 이러한 열을 VARCHAR로 해석 합니다. 이렇게 하면 외부 테이블 DDL에서 오류가 발생 합니다. NVARCHAR2 유형을 사용 하도록 Oracle 스키마를 수정 하거나, 마법사를 사용 하는 대신 수동으로 외부 테이블 문을 만들고 NVARCHAR를 지정 하십시오.

#### <a name="application-deployment"></a>응용 프로그램 개발

- RESTful API에서 R, Python 또는 MLeap 응용 프로그램을 호출 하면 5 분 내에 호출이 시간 초과 됩니다.

#### <a name="spark-and-notebooks"></a>Spark 및 노트북

- POD IP 주소는 Pod가 다시 시작 될 때 Kubernetes 환경에서 변경 될 수 있습니다. 마스터-pod가 다시 시작 되는 시나리오에서 Spark 세션은로 `NoRoteToHostException`실패할 수 있습니다. 이는 새 IP 주소를 사용 하 여 새로 고쳐지지 않는 JVM 캐시로 인해 발생 합니다.

- Jupyter가 이미 설치 되어 있고 Windows에 별도의 Python이 있는 경우 Spark 노트북이 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북에서 **텍스트 추가** 명령을 클릭 하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가 됩니다. 미리 보기 아이콘을 클릭 하 여 편집 모드로 전환 하 고 셀을 편집할 수 있습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부 이며 검색 가능 합니다 (예: 코드 덤프 파일). 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정 해야 합니다. 이는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경 하는 방법에 대 한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조 하세요.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

#### <a name="kibana-logs-dashboards"></a>Kibana logs 대시보드

- Aris CTP 3.0 및 3.1 사이에서 Kibana 버전은 6.3.1에서 7.0.1로 업그레이드 되었습니다.  그러면 Edge 브라우저가 Kibana와 호환 되지 않습니다. Edge에서 Kibana 대시보드의 현재 버전을 로드할 때 사용자에 게 빈 페이지가 표시 됩니다. Kibana.rs에 대해 지원 되는 브라우저는 [여기]( https://www.elastic.co/support/matrix#matrix_browse) 를 참조 하세요. 


## <a id="ctp30"></a>CTP 3.0 (5 월)

다음 섹션에서는 SQL Server 2019 CTP 3.0의 빅 데이터 클러스터에 대 한 새로운 기능 및 알려진 문제에 대해 설명 합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| **mssqlctl** 업데이트 | 여러 **mssqlctl** [명령 및 매개 변수가 업데이트되었습니다](reference-azdata.md). 예를 들어 **mssqlctl login** 명령은 이제 컨트롤러 사용자 이름 및 엔드포인트를 대상으로 하도록 업데이트되었습니다. |
| 스트리지 향상 | 로그 및 데이터에 대해 서로 다른 스토리지 구성을 지원합니다. 또한 빅 데이터 클러스터에 대한 영구적 볼륨 클레임 수가 감소했습니다. |
| 여러 컴퓨팅 풀 인스턴스 | 여러 컴퓨팅 풀 인스턴스를 지원합니다. |
| 새 풀 동작 및 기능 | 컴퓨팅 풀은 이제 **ROUND_ROBIN** 배포에서만 스토리지 풀 및 데이터 풀 작업에 대해 기본적으로 사용됩니다. 데이터 풀은 새로운 **REPLICATED** 배포 형식을 사용할 수 있습니다. 즉, 모든 데이터 풀 인스턴스에 동일한 데이터가 존재할 수 있습니다. |
| 외부 테이블 개선 | HADOOP 데이터 원본 형식의 외부 테이블은 이제 최대 1 MB 크기의 행 읽기를 지원합니다. 외부 테이블(ODBC, 스토리지 풀, 데이터 풀)은 이제 SQL Server 테이블만큼 폭이 넓은 행을 지원합니다. |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는이 릴리스의 알려진 문제 및 제한 사항에 대해 설명 합니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 새 폴더를 만들려고 하면 Azure Data Studio에서 오류를 반환 합니다. 이 기능을 사용 하도록 설정 하려면 Azure Data Studio의 참가자 빌드를 설치 합니다.
  
   - [Windows 사용자 설치 관리자- **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Windows 시스템 설치 관리자- **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [Windows ZIP- **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [macOS ZIP- **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [Linux TAR. RELEASE.TAR.GZ- **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭 하 여 미리 볼 경우 다음과 같은 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재 Azure Data Studio에서 30mb 보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- Hdfs-site.xml에 대 한 변경 내용을 포함 하는 HDFS에 대 한 구성 변경은 지원 되지 않습니다.

#### <a name="deployment"></a>배포

- GPU를 사용 하는 빅 데이터 클러스터에 대 한 이전 배포 절차는 CTP 3.0에서 지원 되지 않습니다. 대체 배포 절차를 조사 하 고 있습니다. 지금은 혼동을 피하기 위해 "GPU 지원을 사용 하 여 빅 데이터 클러스터 배포 및 TensorFlow 실행" 문서가 일시적으로 게시 취소 되었습니다.

- 이전 릴리스에서는 빅 데이터 데이터 클러스터를 업그레이드할 수 없습니다.

   > [!IMPORTANT]
   > 최신 릴리스를 배포 하기 전에 데이터를 백업 하 고 기존 빅 데이터 클러스터 (이전 버전의 **azdata**사용)를 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조 하세요.

- AKS에 배포한 후 배포에서 다음과 같은 두 가지 경고 이벤트가 표시 될 수 있습니다. 이러한 이벤트는 모두 알려진 문제 이지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포 하는 것을 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포가 실패 하면 연결 된 네임 스페이스는 제거 되지 않습니다. 이로 인해 클러스터에 분리 된 네임 스페이스가 생성 될 수 있습니다. 해결 방법은 이름이 같은 클러스터를 배포 하기 전에 수동으로 네임 스페이스를 삭제 하는 것입니다.

#### <a name="external-tables"></a>외부 테이블

- 빅 데이터 클러스터 배포는 더 이상 **SqlDataPool** 및 **sqlstoragepool** 외부 데이터 원본을 생성 하지 않습니다. 데이터 풀 및 저장소 풀에 대 한 데이터 가상화를 지원 하기 위해 이러한 데이터 원본을 수동으로 만들 수 있습니다.

   > [!NOTE]
   > 이러한 외부 데이터 원본을 만들기 위한 URI는 CTPs 간에 다릅니다. 아래 Transact-sql 명령을 참조 하 여 만드는 방법을 확인 하세요. 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 지원 되지 않는 열 유형이 있는 테이블에 대 한 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리 하는 경우 다음과 유사한 메시지가 표시 됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 기본 파일이 HDFS로 동시에 복사 되는 경우 오류가 발생할 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에 외부 테이블을 만드는 경우 Azure Data Studio 가상화 마법사는 외부 테이블 정의에서 이러한 열을 VARCHAR로 해석 합니다. 이렇게 하면 외부 테이블 DDL에서 오류가 발생 합니다. NVARCHAR2 유형을 사용 하도록 Oracle 스키마를 수정 하거나, 마법사를 사용 하는 대신 수동으로 외부 테이블 문을 만들고 NVARCHAR를 지정 하십시오.

#### <a name="application-deployment"></a>응용 프로그램 개발

- RESTful API에서 R, Python 또는 MLeap 응용 프로그램을 호출 하면 5 분 내에 호출이 시간 초과 됩니다.

#### <a name="spark-and-notebooks"></a>Spark 및 노트북

- POD IP 주소는 Pod가 다시 시작 될 때 Kubernetes 환경에서 변경 될 수 있습니다. 마스터-pod가 다시 시작 되는 시나리오에서 Spark 세션은로 `NoRoteToHostException`실패할 수 있습니다. 이는 새 IP 주소를 사용 하 여 새로 고쳐지지 않는 JVM 캐시로 인해 발생 합니다.

- Jupyter가 이미 설치 되어 있고 Windows에 별도의 Python이 있는 경우 Spark 노트북이 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북에서 **텍스트 추가** 명령을 클릭 하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가 됩니다. 미리 보기 아이콘을 클릭 하 여 편집 모드로 전환 하 고 셀을 편집할 수 있습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부 이며 검색 가능 합니다 (예: 코드 덤프 파일). 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정 해야 합니다. 이는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경 하는 방법에 대 한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조 하세요.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp25"></a>CTP 2.5 (4 월)

다음 섹션에서는 SQL Server 2019 CTP 2.5의 빅 데이터 클러스터에 대 한 새로운 기능 및 알려진 문제에 대해 설명 합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| 배포 프로필 | 환경 변수 대신 빅 데이터 클러스터 배포를 위해 기본 및 사용자 지정된 [배포 구성 JSON 파일](deployment-guidance.md#configfile)을 사용합니다. |
| 프롬프트된 배포 | `azdata cluster create`는 이제 기본 배포에 필요한 설정을 묻는 메시지를 표시합니다. |
| 서비스 엔드포인트 및 pod 이름 변경 | 다음 외부 끝점에서 이름이 변경 되었습니다.<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| **azdata** 향상 | **Azdata** 를 사용 하 여 [외부 끝점을 나열](deployment-guidance.md#endpoints) 하 고  `--version` 매개 변수를 사용 하 여 azdata 버전을 확인 합니다. |
| 오프라인 설치 | 오프 라인 빅 데이터 클러스터 배포에 대 한 지침입니다. |
| HDFS 계층화 개선 사항 | S3 계층화, 탑재 캐싱 및 ADLS Gen2에 대 한 OAuth 지원. |
| 새 `mssql` Spark-SQL Server 커넥터 | |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는이 릴리스의 알려진 문제 및 제한 사항에 대해 설명 합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서는 빅 데이터 데이터 클러스터를 업그레이드할 수 없습니다.

   > [!IMPORTANT]
   > 최신 릴리스를 배포 하기 전에 데이터를 백업 하 고 기존 빅 데이터 클러스터 (이전 버전의 **azdata**사용)를 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조 하세요.

- AKS에 배포한 후 배포에서 다음과 같은 두 가지 경고 이벤트가 표시 될 수 있습니다. 이러한 이벤트는 모두 알려진 문제 이지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포 하는 것을 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포가 실패 하면 연결 된 네임 스페이스는 제거 되지 않습니다. 이로 인해 클러스터에 분리 된 네임 스페이스가 생성 될 수 있습니다. 해결 방법은 이름이 같은 클러스터를 배포 하기 전에 수동으로 네임 스페이스를 삭제 하는 것입니다.

#### <a name="external-tables"></a>외부 테이블

- 빅 데이터 클러스터 배포는 더 이상 **SqlDataPool** 및 **sqlstoragepool** 외부 데이터 원본을 생성 하지 않습니다. 데이터 풀 및 저장소 풀에 대 한 데이터 가상화를 지원 하기 위해 이러한 데이터 원본을 수동으로 만들 수 있습니다.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- 지원 되지 않는 열 유형이 있는 테이블에 대 한 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리 하는 경우 다음과 유사한 메시지가 표시 됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 기본 파일이 HDFS로 동시에 복사 되는 경우 오류가 발생할 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에 외부 테이블을 만드는 경우 Azure Data Studio 가상화 마법사는 외부 테이블 정의에서 이러한 열을 VARCHAR로 해석 합니다. 이렇게 하면 외부 테이블 DDL에서 오류가 발생 합니다. NVARCHAR2 유형을 사용 하도록 Oracle 스키마를 수정 하거나, 마법사를 사용 하는 대신 수동으로 외부 테이블 문을 만들고 NVARCHAR를 지정 하십시오.

#### <a name="application-deployment"></a>응용 프로그램 개발

- RESTful API에서 R, Python 또는 MLeap 응용 프로그램을 호출 하면 5 분 내에 호출이 시간 초과 됩니다.

#### <a name="spark-and-notebooks"></a>Spark 및 노트북

- POD IP 주소는 Pod가 다시 시작 될 때 Kubernetes 환경에서 변경 될 수 있습니다. 마스터-pod가 다시 시작 되는 시나리오에서 Spark 세션은로 `NoRoteToHostException`실패할 수 있습니다. 이는 새 IP 주소를 사용 하 여 새로 고쳐지지 않는 JVM 캐시로 인해 발생 합니다.

- Jupyter가 이미 설치 되어 있고 Windows에 별도의 Python이 있는 경우 Spark 노트북이 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북에서 **텍스트 추가** 명령을 클릭 하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가 됩니다. 미리 보기 아이콘을 클릭 하 여 편집 모드로 전환 하 고 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭 하 여 미리 볼 경우 다음과 같은 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재 Azure Data Studio에서 30mb 보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- Hdfs-site.xml에 대 한 변경 내용을 포함 하는 HDFS에 대 한 구성 변경은 지원 되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부 이며 검색 가능 합니다 (예: 코드 덤프 파일). 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정 해야 합니다. 이는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경 하는 방법에 대 한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조 하세요.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp24"></a>CTP 2.4 (3 월)

다음 섹션에서는 SQL Server 2019 CTP 2.4의 빅 데이터 클러스터에 대 한 새로운 기능 및 알려진 문제에 대해 설명 합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| Spark에서 TensorFlow를 사용하여 딥 러닝을 실행하기 위한 GPU 지원 지침. | [GPU 지원이 포함된 빅 데이터 클러스터를 배포하고 TensorFlow를 실행](spark-gpu-tensorflow.md)합니다. |
| **SqlDataPool** 및 **SqlStoragePool** 데이터 원본은 더 이상 기본적으로 생성되지 않습니다. | 필요에 따라 수동으로 만듭니다. [알려진 문제](#externaltablesctp24)를 참조하세요. |
| `INSERT INTO SELECT`가 데이터 풀을 지원합니다. | 예제를 보려면 [ 자습서: Transact-SQL을 사용하여 SQL Server 데이터 풀에 데이터 수집](tutorial-data-pool-ingest-sql.md)을 참조하세요. |
| `FORCE SCALEOUTEXECUTION` 및 `DISABLE SCALEOUTEXECUTION` 옵션. | 외부 테이블에 대 한 쿼리에 compute 풀 사용을 강제로 또는 사용 하지 않도록 설정 합니다. `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)` )을 입력합니다. |
| AKS 배포 권장 사항을 업데이트합니다. | AKS에서 빅 데이터 클러스터를 평가할 때 이제 **Standard_L8s** 크기의 단일 노드를 사용하는 것이 좋습니다. |
| Spark 런타임을 Spark 런타임 2.4로 업그레이드합니다. | |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는이 릴리스의 알려진 문제 및 제한 사항에 대해 설명 합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서는 빅 데이터 데이터 클러스터를 업그레이드할 수 없습니다.

   > [!IMPORTANT]
   > 최신 릴리스를 배포 하기 전에 데이터를 백업 하 고 기존 빅 데이터 클러스터 (이전 버전의 **azdata**사용)를 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조 하세요.

- AKS에 배포한 후 배포에서 다음과 같은 두 가지 경고 이벤트가 표시 될 수 있습니다. 이러한 이벤트는 모두 알려진 문제 이지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포 하는 것을 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포가 실패 하면 연결 된 네임 스페이스는 제거 되지 않습니다. 이로 인해 클러스터에 분리 된 네임 스페이스가 생성 될 수 있습니다. 해결 방법은 이름이 같은 클러스터를 배포 하기 전에 수동으로 네임 스페이스를 삭제 하는 것입니다.

#### <a name="kubeadm-deployments"></a>kubeadm 배포

Kubeadm를 사용 하 여 여러 컴퓨터에 Kubernetes을 배포 하는 경우 클러스터 관리 포털에 빅 데이터 클러스터에 연결 하는 데 필요한 끝점이 올바르게 표시 되지 않습니다. 이 문제가 발생 하는 경우 다음 해결 방법을 사용 하 여 서비스 끝점 IP 주소를 검색 합니다.

- 클러스터 내에서 연결 하는 경우 연결 하려는 끝점의 서비스 IP에 대 한 Kubernetes를 쿼리 합니다. 예를 들어 다음 **kubectl** 명령은 SQL Server 마스터 인스턴스의 IP 주소를 표시 합니다.

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 클러스터 외부에서 연결 하는 경우 다음 단계를 사용 하 여 연결 합니다.

   1. SQL Server 마스터 인스턴스 `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`를 실행 하는 노드의 IP 주소를 가져옵니다.

   1. 이 IP 주소를 사용 하 여 SQL Server 마스터 인스턴스에 연결 합니다.

   1. Master 데이터베이스의 **cluster_endpoint_table** 에서 다른 외부 끝점을 쿼리 합니다.

      연결 시간 제한으로 인해 실패 하는 경우 해당 노드가 방화벽이 사용 될 수 있습니다. 이 경우 Kubernetes 클러스터 관리자에 게 문의 하 여 외부에 노출 되는 노드 IP를 요청 해야 합니다. 모든 노드일 수 있습니다. 그런 다음 해당 IP와 해당 포트를 사용 하 여 클러스터에서 실행 되는 다양 한 서비스에 연결할 수 있습니다. 예를 들어 관리자는 다음을 실행 하 여이 IP를 찾을 수 있습니다.

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>클러스터 삭제 실패

**Azdata**를 사용 하 여 클러스터를 삭제 하려고 하면 다음 오류와 함께 실패 합니다.

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

새 Python Kubernetes client (버전 9.0.0)가 현재 **azdata**를 중단 하는 네임 스페이스 삭제 API를 변경 했습니다. 이는 최신 Kubernetes python 클라이언트가 설치 된 경우에만 발생 합니다. **Kubectl** (`kubectl delete ns <ClusterName>`)를 사용 하 여 클러스터를 직접 삭제 하거나를 사용 하 여 `sudo pip install kubernetes==8.0.1`이전 버전을 설치할 수 있으므로이 문제를 해결할 수 있습니다.

#### <a id="externaltablesctp24"></a>외부 테이블

- 빅 데이터 클러스터 배포는 더 이상 **SqlDataPool** 및 **sqlstoragepool** 외부 데이터 원본을 생성 하지 않습니다. 데이터 풀 및 저장소 풀에 대 한 데이터 가상화를 지원 하기 위해 이러한 데이터 원본을 수동으로 만들 수 있습니다.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- 지원 되지 않는 열 유형이 있는 테이블에 대 한 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리 하는 경우 다음과 유사한 메시지가 표시 됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 기본 파일이 HDFS로 동시에 복사 되는 경우 오류가 발생할 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에 외부 테이블을 만드는 경우 Azure Data Studio 가상화 마법사는 외부 테이블 정의에서 이러한 열을 VARCHAR로 해석 합니다. 이렇게 하면 외부 테이블 DDL에서 오류가 발생 합니다. NVARCHAR2 유형을 사용 하도록 Oracle 스키마를 수정 하거나, 마법사를 사용 하는 대신 수동으로 외부 테이블 문을 만들고 NVARCHAR를 지정 하십시오.

#### <a name="application-deployment"></a>응용 프로그램 개발

- RESTful API에서 R, Python 또는 MLeap 응용 프로그램을 호출 하면 5 분 내에 호출이 시간 초과 됩니다.

#### <a name="spark-and-notebooks"></a>Spark 및 노트북

- POD IP 주소는 Pod가 다시 시작 될 때 Kubernetes 환경에서 변경 될 수 있습니다. 마스터-pod가 다시 시작 되는 시나리오에서 Spark 세션은로 `NoRoteToHostException`실패할 수 있습니다. 이는 새 IP 주소를 사용 하 여 새로 고쳐지지 않는 JVM 캐시로 인해 발생 합니다.

- Jupyter가 이미 설치 되어 있고 Windows에 별도의 Python이 있는 경우 Spark 노트북이 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북에서 **텍스트 추가** 명령을 클릭 하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가 됩니다. 미리 보기 아이콘을 클릭 하 여 편집 모드로 전환 하 고 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭 하 여 미리 볼 경우 다음과 같은 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재 Azure Data Studio에서 30mb 보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- Hdfs-site.xml에 대 한 변경 내용을 포함 하는 HDFS에 대 한 구성 변경은 지원 되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부 이며 검색 가능 합니다 (예: 코드 덤프 파일). 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정 해야 합니다. 이는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경 하는 방법에 대 한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조 하세요.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp23"></a>CTP 2.3 (2 월)

다음 섹션에서는 SQL Server 2019 CTP 2.3의 빅 데이터 클러스터에 대 한 새로운 기능 및 알려진 문제에 대해 설명 합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
| :---------- | :------ |
| IntelliJ의 빅 데이터 클러스터에 Spark 작업을 제출합니다. | [IntelliJ의 SQL Server 빅 데이터 클러스터에 Spark 작업 제출](spark-submit-job-intellij-tool-plugin.md) |
| 애플리케이션 배포 및 클러스터 관리를 위한 일반 CLI. | [SQL Server 2019 빅 데이터 클러스터에 앱을 배포하는 방법(미리 보기)](big-data-cluster-create-apps.md) |
| 애플리케이션을 빅 데이터 클러스터에 배포하기 위한 VS Code 확장. | [VS Code를 사용하여 SQL Server 빅 데이터 클러스터에 애플리케이션을 배포하는 방법](app-deployment-extension.md) |
| **Azdata** 도구 명령 사용에 대 한 변경 내용입니다. | 자세한 내용은 [azdata에 대 한 알려진 문제](#azdatactp23)를 참조 하세요. |
| 빅 데이터 클러스터에서 Sparklyr 사용 | [SQL Server 2019 빅 데이터 클러스터에서 Sparklyr 사용](sparklyr-from-RStudio.md) |
| **HDFS 계층화**를 통해 빅 데이터 클러스터에 외장 HDFS 호환 스토리지를 탑재합니다. | [HDFS 계층화](hdfs-tiering.md)를 참조하세요 |
| SQL Server 마스터 인스턴스 및 HDFS/Spark 게이트웨이에 대한 새로운 통합 연결 환경. | [SQL Server 마스터 인스턴스 및 HDFS/Spark 게이트웨이](connect-to-big-data-cluster.md)를 참조하세요. |
| 이제 **azdata cluster delete** 를 사용 하 여 클러스터를 삭제 하면 빅 데이터 클러스터에 포함 된 네임 스페이스의 개체만 삭제 됩니다. | 네임스페이스는 삭제되지 않습니다. 그러나 이전 릴리스에서 이 명령은 전체 네임스페이스를 삭제했습니다. |
| _보안_ 엔드포인트 이름이 변경되고 통합되었습니다. | **service-security-lb** 및 **service-security-nodeport**가 **endpoint-security** 엔드포인트에 통합되었습니다. |
| _프록시_ 엔드포인트 이름이 변경되고 통합되었습니다. | **service-proxy-lb** 및 **service-proxy-nodeport**가 **endpoint-service-proxy** 엔드포인트에 통합되었습니다. |
| _컨트롤러_ 엔드포인트 이름이 변경되고 통합되었습니다. | **service-mssql-controller-lb** 및 **service-mssql-controller-nodeport**가 **endpoint-controller** 엔드포인트에 통합되었습니다. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는이 릴리스의 알려진 문제 및 제한 사항에 대해 설명 합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서는 빅 데이터 데이터 클러스터를 업그레이드할 수 없습니다.

   > [!IMPORTANT]
   > 최신 릴리스를 배포 하기 전에 데이터를 백업 하 고 기존 빅 데이터 클러스터 (이전 버전의 **azdata**사용)를 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조 하세요.

- EULA에 동의 하려면 **ACCEPT_EULA** 환경 변수가 "yes" 또는 "yes" 여야 합니다. 이전 릴리스에서는 "y"와 "Y"를 사용할 수 있지만 더 이상 허용 되지 않으며 배포에 실패 합니다.

- **CLUSTER_PLATFORM** 환경 변수의 기본값은 이전 릴리스와 동일 하지 않습니다.

- AKS에 배포한 후 배포에서 다음과 같은 두 가지 경고 이벤트가 표시 될 수 있습니다. 이러한 이벤트는 모두 알려진 문제 이지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포 하는 것을 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포가 실패 하면 연결 된 네임 스페이스는 제거 되지 않습니다. 이로 인해 클러스터에 분리 된 네임 스페이스가 생성 될 수 있습니다. 해결 방법은 이름이 같은 클러스터를 배포 하기 전에 수동으로 네임 스페이스를 삭제 하는 것입니다.

#### <a name="kubeadm-deployments"></a>kubeadm 배포

Kubeadm를 사용 하 여 여러 컴퓨터에 Kubernetes을 배포 하는 경우 클러스터 관리 포털에 빅 데이터 클러스터에 연결 하는 데 필요한 끝점이 올바르게 표시 되지 않습니다. 이 문제가 발생 하는 경우 다음 해결 방법을 사용 하 여 서비스 끝점 IP 주소를 검색 합니다.

- 클러스터 내에서 연결 하는 경우 연결 하려는 끝점의 서비스 IP에 대 한 Kubernetes를 쿼리 합니다. 예를 들어 다음 **kubectl** 명령은 SQL Server 마스터 인스턴스의 IP 주소를 표시 합니다.

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 클러스터 외부에서 연결 하는 경우 다음 단계를 사용 하 여 연결 합니다.

   1. SQL Server 마스터 인스턴스 `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`를 실행 하는 노드의 IP 주소를 가져옵니다.

   1. 이 IP 주소를 사용 하 여 SQL Server 마스터 인스턴스에 연결 합니다.

   1. Master 데이터베이스의 **cluster_endpoint_table** 에서 다른 외부 끝점을 쿼리 합니다.

      연결 시간 제한으로 인해 실패 하는 경우 해당 노드가 방화벽이 사용 될 수 있습니다. 이 경우 Kubernetes 클러스터 관리자에 게 문의 하 여 외부에 노출 되는 노드 IP를 요청 해야 합니다. 모든 노드일 수 있습니다. 그런 다음 해당 IP와 해당 포트를 사용 하 여 클러스터에서 실행 되는 다양 한 서비스에 연결할 수 있습니다. 예를 들어 관리자는 다음을 실행 하 여이 IP를 찾을 수 있습니다.

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="azdatactp23"></a>azdata

- **Azdata** 도구가 동사-명사 명령 순서에서 명사-동사 순서로 변경 되었습니다. 예 `azdata create cluster` 를 들어는 이제 `azdata cluster create`입니다.

- 이제를 사용 하 `azdata cluster create`여 클러스터를 만들 때 매개변수가필요합니다.`--name`

   ```bash
   azdata cluster create --name <cluster_name>
   ```

- 최신 버전의 빅 데이터 클러스터 및 **azdata**로 업그레이드 하는 방법에 대 한 중요 정보는 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조 하세요.

#### <a name="external-tables"></a>외부 테이블

- 지원 되지 않는 열 유형이 있는 테이블에 대 한 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리 하는 경우 다음과 유사한 메시지가 표시 됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 기본 파일이 HDFS로 동시에 복사 되는 경우 오류가 발생할 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에 외부 테이블을 만드는 경우 Azure Data Studio 가상화 마법사는 외부 테이블 정의에서 이러한 열을 VARCHAR로 해석 합니다. 이렇게 하면 외부 테이블 DDL에서 오류가 발생 합니다. NVARCHAR2 유형을 사용 하도록 Oracle 스키마를 수정 하거나, 마법사를 사용 하는 대신 수동으로 외부 테이블 문을 만들고 NVARCHAR를 지정 하십시오.

#### <a name="application-deployment"></a>응용 프로그램 개발

- RESTful API에서 R, Python 또는 MLeap 응용 프로그램을 호출 하면 5 분 내에 호출이 시간 초과 됩니다.

#### <a name="spark-and-notebooks"></a>Spark 및 노트북

- POD IP 주소는 Pod가 다시 시작 될 때 Kubernetes 환경에서 변경 될 수 있습니다. 마스터-pod가 다시 시작 되는 시나리오에서 Spark 세션은로 `NoRoteToHostException`실패할 수 있습니다. 이는 새 IP 주소를 사용 하 여 새로 고쳐지지 않는 JVM 캐시로 인해 발생 합니다.

- Jupyter가 이미 설치 되어 있고 Windows에 별도의 Python이 있는 경우 Spark 노트북이 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북에서 **텍스트 추가** 명령을 클릭 하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가 됩니다. 미리 보기 아이콘을 클릭 하 여 편집 모드로 전환 하 고 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭 하 여 미리 볼 경우 다음과 같은 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재 Azure Data Studio에서 30mb 보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- Hdfs-site.xml에 대 한 변경 내용을 포함 하는 HDFS에 대 한 구성 변경은 지원 되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부 이며 검색 가능 합니다 (예: 코드 덤프 파일). 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정 해야 합니다. 이는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경 하는 방법에 대 한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조 하세요.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp22"></a>CTP 2.2 (12 월 2018)

다음 섹션에서는 SQL Server 2019 CTP 2.2의 빅 데이터 클러스터에 대 한 새로운 기능 및 알려진 문제에 대해 설명 합니다.

### <a name="new-features"></a>새로운 기능

- ( `/portal` **Https://:30777\</Portal)를 사용 하 여 클러스터 관리 포털에 액세스 합니다.\>**
- 마스터 풀 서비스 이름이 및 `service-master-pool-lb` `service-master-pool-nodeport` 에서로 `endpoint-master-pool`변경 되었습니다.
- 새 버전의 **azdata** 및 업데이트 된 이미지입니다.
- 기타 버그 수정 및 개선 사항.

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는이 릴리스의 알려진 문제 및 제한 사항에 대해 설명 합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서는 빅 데이터 데이터 클러스터를 업그레이드할 수 없습니다. 최신 릴리스를 배포 하기 전에 기존 빅 데이터 클러스터를 백업 하 고 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조 하세요.

- AKS에 배포한 후 배포에서 다음과 같은 두 가지 경고 이벤트가 표시 될 수 있습니다. 이러한 이벤트는 모두 알려진 문제 이지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포 하는 것을 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포가 실패 하면 연결 된 네임 스페이스는 제거 되지 않습니다. 이로 인해 클러스터에 분리 된 네임 스페이스가 생성 될 수 있습니다. 해결 방법은 이름이 같은 클러스터를 배포 하기 전에 수동으로 네임 스페이스를 삭제 하는 것입니다.

#### <a name="cluster-administration-portal"></a>클러스터 관리 포털

클러스터 관리 포털에 SQL Server 마스터 인스턴스의 끝점이 표시 되지 않습니다. 마스터 인스턴스에 대 한 IP 주소 및 포트를 찾으려면 다음 **kubectl** 명령을 사용 합니다.

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

#### <a name="external-tables"></a>외부 테이블

- 지원 되지 않는 열 유형이 있는 테이블에 대 한 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리 하는 경우 다음과 유사한 메시지가 표시 됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 기본 파일이 HDFS로 동시에 복사 되는 경우 오류가 발생할 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 및 노트북

- POD IP 주소는 Pod가 다시 시작 될 때 Kubernetes 환경에서 변경 될 수 있습니다. 마스터-pod가 다시 시작 되는 시나리오에서 Spark 세션은로 `NoRoteToHostException`실패할 수 있습니다. 이는 새 IP 주소를 사용 하 여 새로 고쳐지지 않는 JVM 캐시로 인해 발생 합니다.

- Jupyter가 이미 설치 되어 있고 Windows에 별도의 Python이 있는 경우 Spark 노트북이 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북에서 **텍스트 추가** 명령을 클릭 하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가 됩니다. 미리 보기 아이콘을 클릭 하 여 편집 모드로 전환 하 고 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭 하 여 미리 볼 경우 다음과 같은 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재 Azure Data Studio에서 30mb 보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- Hdfs-site.xml에 대 한 변경 내용을 포함 하는 HDFS에 대 한 구성 변경은 지원 되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부 이며 검색 가능 합니다 (예: 코드 덤프 파일). 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정 해야 합니다. 이는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경 하는 방법에 대 한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조 하세요.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp21"></a>CTP 2.1 (11 월 2018)

다음 섹션에서는 SQL Server 2019 CTP 2.1의 빅 데이터 클러스터에 대 한 새로운 기능 및 알려진 문제에 대해 설명 합니다.

### <a name="new-features"></a>새로운 기능

- 빅 데이터 클러스터에 [Python 및 R 앱을 배포](big-data-cluster-create-apps.md) 합니다.
- 새 버전의 **azdata** 및 업데이트 된 이미지입니다. 
- 기타 버그 수정 및 개선 사항.

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 CTP 2.1의 빅 데이터 클러스터 SQL Server에 대 한 알려진 문제를 제공 합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서는 빅 데이터 데이터 클러스터를 업그레이드할 수 없습니다. 최신 릴리스를 배포 하기 전에 기존 빅 데이터 클러스터를 백업 하 고 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조 하세요.

- AKS에 배포한 후 배포에서 다음과 같은 두 가지 경고 이벤트가 표시 될 수 있습니다. 이러한 이벤트는 모두 알려진 문제 이지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포 하는 것을 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포가 실패 하면 연결 된 네임 스페이스는 제거 되지 않습니다. 이로 인해 클러스터에 분리 된 네임 스페이스가 생성 될 수 있습니다. 해결 방법은 이름이 같은 클러스터를 배포 하기 전에 수동으로 네임 스페이스를 삭제 하는 것입니다.

#### <a name="admin-portal"></a>관리 포털

- [Msqlctl-ctp 명령을 사용 하 여 앱을 만들고](big-data-cluster-create-apps.md) SQL Server 빅 데이터 클러스터에 배포 하는 경우 클러스터 관리 포털에는 응용 프로그램이 관리 부분의 컨트롤러 섹션에서 "알 수 없음"으로 배포 된 pod 표시 됩니다.

#### <a name="external-tables"></a>외부 테이블

- 지원 되지 않는 열 유형이 있는 테이블에 대 한 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리 하는 경우 다음과 유사한 메시지가 표시 됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 기본 파일이 HDFS로 동시에 복사 되는 경우 오류가 발생할 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 및 노트북

- POD IP 주소는 Pod가 다시 시작 될 때 Kubernetes 환경에서 변경 될 수 있습니다. 마스터-pod가 다시 시작 되는 시나리오에서 Spark 세션은로 `NoRoteToHostException`실패할 수 있습니다. 이는 새 IP 주소를 사용 하 여 새로 고쳐지지 않는 JVM 캐시로 인해 발생 합니다.

- Jupyter가 이미 설치 되어 있고 Windows에 별도의 Python이 있는 경우 Spark 노트북이 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북에서 **텍스트 추가** 명령을 클릭 하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가 됩니다. 미리 보기 아이콘을 클릭 하 여 편집 모드로 전환 하 고 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭 하 여 미리 볼 경우 다음과 같은 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재 Azure Data Studio에서 30mb 보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- Hdfs-site.xml에 대 한 변경 내용을 포함 하는 HDFS에 대 한 구성 변경은 지원 되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부 이며 검색 가능 합니다 (예: 코드 덤프 파일). 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정 해야 합니다. 이는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경 하는 방법에 대 한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조 하세요.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp20"></a>CTP 2.0 (10 월 2018 일)

다음 섹션에서는 SQL Server 2019 CTP 2.0의 빅 데이터 클러스터에 대 한 새로운 기능 및 알려진 문제에 대해 설명 합니다.

### <a name="new-features"></a>새로운 기능

- Azdata 관리 도구를 사용 하는 간단한 배포 환경
- Azure Data Studio의 기본 노트북 환경
- SQL Server의 저장소 인스턴스를 통해 HDFS 파일을 쿼리 합니다.
- Master를 통해 SQL Server, Oracle, MongoDB 및 HDFS를 통한 데이터 가상화
- Azure Data Studio의 SQL Server 및 Oracle 용 데이터 가상화 마법사
- 마스터의 ML 서비스
- 모니터링 및 문제 해결에 사용할 수 있는 클러스터 관리 포털
- Azure Data Studio에서 Spark 작업 제출 
- 클러스터 관리 포털의 Spark UI
- 저장소 클래스에 볼륨 탑재
- Master에서 데이터 풀 쿼리
- SSMS에서 분산 쿼리 계획 표시
- Azdata 관리 도구용 Pip 패키지
- 컨트롤러 서비스를 통한 기본 제공 배포 엔진

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 CTP 2.0의 빅 데이터 클러스터 SQL Server에 대 한 알려진 문제를 제공 합니다.

#### <a name="deployment"></a>배포

- AKS (Azure Kubernetes Service)를 사용 하는 경우 권장 되는 버전의 Kubernetes는 1.10. * 이며,이는 디스크 크기 조정을 지원 하지 않습니다. 배포 시 저장소 크기를 적절 하 게 조정 해야 합니다. 저장소 크기를 조정 하는 방법에 대 한 자세한 내용은 [데이터 지 속성](concept-data-persistence.md) 문서를 참조 하세요. Vm에 배포 된 Kubernetes의 경우 권장 되는 버전은 1.11입니다.

- AKS에 배포한 후 배포에서 다음과 같은 두 가지 경고 이벤트가 표시 될 수 있습니다. 이러한 이벤트는 모두 알려진 문제 이지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포 하는 것을 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포가 실패 하면 연결 된 네임 스페이스는 제거 되지 않습니다. 이로 인해 클러스터에 분리 된 네임 스페이스가 생성 될 수 있습니다. 해결 방법은 이름이 같은 클러스터를 배포 하기 전에 수동으로 네임 스페이스를 삭제 하는 것입니다.

#### <a name="external-tables"></a>외부 테이블

- 지원 되지 않는 열 유형이 있는 테이블에 대 한 데이터 풀 외부 테이블을 만들 수 있습니다. 외부 테이블을 쿼리 하는 경우 다음과 유사한 메시지가 표시 됩니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 기본 파일이 HDFS로 동시에 복사 되는 경우 오류가 발생할 수 있습니다.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 및 노트북

- POD IP 주소는 Pod가 다시 시작 될 때 Kubernetes 환경에서 변경 될 수 있습니다. 마스터-pod가 다시 시작 되는 시나리오에서 Spark 세션은로 `NoRoteToHostException`실패할 수 있습니다. 이는 새 IP 주소를 사용 하 여 새로 고쳐지지 않는 JVM 캐시로 인해 발생 합니다.

- Jupyter가 이미 설치 되어 있고 Windows에 별도의 Python이 있는 경우 Spark 노트북이 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북에서 **텍스트 추가** 명령을 클릭 하면 텍스트 셀이 편집 모드가 아닌 미리 보기 모드로 추가 됩니다. 미리 보기 아이콘을 클릭 하 여 편집 모드로 전환 하 고 셀을 편집할 수 있습니다.

#### <a name="hdfs"></a>HDFS

- HDFS에서 파일을 마우스 오른쪽 단추로 클릭 하 여 미리 볼 경우 다음과 같은 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재 Azure Data Studio에서 30mb 보다 큰 파일을 미리 볼 수 있는 방법은 없습니다.

- Hdfs-site.xml에 대 한 변경 내용을 포함 하는 HDFS에 대 한 구성 변경은 지원 되지 않습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 환경의 일부 이며 검색 가능 합니다 (예: 코드 덤프 파일). 배포 후에 마스터 인스턴스에서 SA_PASSWORD를 다시 설정 해야 합니다. 이는 버그가 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD를 변경 하는 방법에 대 한 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조 하세요.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 SQL Server 하는 방법에 대 한 자세한 내용은 [SQL Server 2019 빅 데이터 클러스터 란?](big-data-cluster-overview.md)을 참조 하세요.
