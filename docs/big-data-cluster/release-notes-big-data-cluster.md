---
title: 릴리스 정보
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 최신 업데이트 및 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대 한 알려진된 문제를 설명 합니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 389a521d256becb431b23ec073cadcde7c116952
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67681551"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>SQL Server에서 빅 데이터 클러스터에 대 한 릴리스 정보

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 업데이트를 나열 및 빅 데이터 클러스터 SQL Server의 최신 릴리스에 대 한 문제 인지 알고 있어야 합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp31"></a> CTP 3.1 (월)

다음 섹션에서는 새로운 기능 및 SQL Server 2019 CTP 3.1에서 빅 데이터 클러스터에 대해 알려진된 문제를 설명합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| `mssqlctl` 명령 변경 내용 | `mssqlctl cluster` 명령이 `mssqlctl bdc`로 변경되었습니다. 자세한 내용은 [`mssqlctl`참조](reference-mssqlctl.md)를 참조하세요. |
| 새 `mssqlctl` 상태 명령 및 클러스터 관리 포털을 제거 합니다. | 클러스터 관리 포털에는이 릴리스에서 제거 됩니다. 새 상태 명령에 추가 된 `mssqlctl` 해당 보수 기존 명령을 모니터링 합니다. |
| Spark 컴퓨팅 풀 | 추가 노드를 생성하여 스토리지를 확장하지 않고도 Spark 컴퓨팅 성능을 향상시킬 수 있습니다. 또한 Spark에 사용되지 않는 스토리지 풀 노드를 시작할 수도 있습니다. Spark와 스토리지는 분리됩니다. 자세한 내용은 [spark없이 스토리지 구성](deployment-custom-configuration.md#sparkstorage)을 참조하세요. |
| MSSQL Spark 커넥터 | 데이터 풀 외부 테이블에 대한 읽기/쓰기를 지원합니다. 이전 릴리스에서는 MASTER 인스턴스 테이블에만 읽기/쓰기를 지원했습니다. 자세한 내용은 [MSSQL Spark 커넥터를 사용하여 Spark에서 SQL Server에 읽고 쓰는 방법](spark-mssql-connector.md)을 참조하세요. |
| MLeap를 사용하여 기계 학습 | [Spark에서 MLeap 기계 학습 모델을 교육하고 Java 언어 확장을 사용하여 SQL Server에서 평가합니다](spark-create-machine-learning-model.md). |

### <a name="known-issues"></a>알려진 문제

다음 섹션의 알려진된 문제 및 제한 사항이이 릴리스를 사용 하 여 설명합니다.

#### <a name="hdfs"></a>HDFS

- 미리 HDFS의 파일을 마우스 오른쪽 단추로 클릭 하는 경우 다음 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재는 Azure Data Studio에서 30 MB 보다 큰 파일을 미리 볼 수 없습니다.

- 구성 변경 내용은 hdfs-site.xml 변경 내용을 포함 하는 HDFS에 지원 되지 않습니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서 빅 데이터 데이터 클러스터를 업그레이드 하는 것은 지원 되지 않습니다.

   > [!IMPORTANT]
   > 데이터를 백업 하 고 다음 기존 빅 데이터 클러스터를 삭제 해야 합니다 (이전 버전의를 사용 하 여 **mssqlctl**) 최신 릴리스를 배포 하기 전에 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)합니다.

- AKS를 배포한 후 배포에서 다음 두 경고 이벤트를 볼 수 있습니다. 이러한 이벤트는 알려진 문제, 있지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포를 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패 하면 연결된 된 네임 스페이스 제거 되지 않습니다. 이 클러스터에서 분리 된 네임 스페이스를 발생할 수 있습니다. 동일한 이름 사용 하 여 클러스터를 배포 하기 전에 네임 스페이스를 수동으로 삭제 됩니다.

#### <a name="external-tables"></a>외부 테이블

- 빅 데이터 클러스터 배포에서는 더 이상 합니다 **SqlDataPool** 하 고 **SqlStoragePool** 외부 데이터 원본입니다. 이러한 데이터 원본은 데이터 풀 및 저장소 풀 데이터 가상화를 지원 하도록 수동으로 만들 수 있습니다.

   > [!NOTE]
   > 이러한 외부 데이터 원본 만들기에 대 한 URI가 Ctp에 따라 다릅니다. 만드는 방법은 다음 TRANSACT-SQL 명령을 참조 하세요 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 지원 되지 않는 열 형식에는 테이블에 대 한 데이터 풀 외부 테이블을 만들 가능성이 있습니다. 외부 테이블을 쿼리 하는 경우 메시지가 다음과 비슷합니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 오류가 발생할 수 있습니다는 동시에 기본 파일은 HDFS에 복사 되는 경우.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에는 외부 테이블을 만들면 Azure Data Studio virtualization 마법사는 외부 테이블 정의에서 이러한 열 VARCHAR로 해석 합니다. 외부 테이블 DDL에에서 실패를 하면 합니다. 하거나 NVARCHAR2 유형을 사용 하 여 또는 EXTERNAL TABLE 문을 수동으로 만들고, 마법사를 사용 하는 대신 NVARCHAR를 지정 하는 Oracle 스키마를 수정 합니다.

#### <a name="application-deployment"></a>응용 프로그램 개발

- R, Python 또는 MLeap 응용 프로그램에서 RESTful API를 호출할 때 호출에에서 시간 초과 5 분입니다.

#### <a name="spark-and-notebooks"></a>Spark 및 notebook

- POD IP 주소는 Pod 다시 시작으로 Kubernetes 환경에서 변경 될 수 있습니다. 마스터 pod를 다시 시작 되는 시나리오에서 Spark 세션을 사용 하 여 못할 `NoRoteToHostException`합니다. 이 새 IP를 사용 하 여 새로 고쳐지는 가져오기 하지 JVM 캐시 주소입니다.

- Windows에 이미 설치 된 Jupyter 및 별도 Python을 있다면 Spark 노트북 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북을 클릭할 경우에 **텍스트 추가** 명령, 텍스트 셀이 편집 모드 보다는 미리 보기 모드에서 추가 됩니다. 편집 모드에 있고 셀을 편집 하 여 전환한 다음 미리 보기 아이콘을 클릭할 수 있습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 (예: 코드 덤프 파일)의 일부 환경의 및 검색할 수입니다. 배포 후 마스터 인스턴스에서 SA_PASSWORD 다시 설정 해야 합니다. 이 변경은 버그 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)합니다.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp30"></a> CTP 3.0 (월)

다음 섹션에서는 새로운 기능 및 SQL Server 2019 CTP 3.0에서 빅 데이터 클러스터에 대해 알려진된 문제를 설명합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| **mssqlctl** 업데이트 | 여러 **mssqlctl** [명령 및 매개 변수가 업데이트되었습니다](../big-data-cluster/reference-mssqlctl.md). 예를 들어 **mssqlctl login** 명령은 이제 컨트롤러 사용자 이름 및 엔드포인트를 대상으로 하도록 업데이트되었습니다. |
| 스트리지 향상 | 로그 및 데이터에 대해 서로 다른 스토리지 구성을 지원합니다. 또한 빅 데이터 클러스터에 대한 영구적 볼륨 클레임 수가 감소했습니다. |
| 여러 컴퓨팅 풀 인스턴스 | 여러 컴퓨팅 풀 인스턴스를 지원합니다. |
| 새 풀 동작 및 기능 | 컴퓨팅 풀은 이제 **ROUND_ROBIN** 배포에서만 스토리지 풀 및 데이터 풀 작업에 대해 기본적으로 사용됩니다. 데이터 풀 이제 새 사용할 수 있습니다 **복제 된** 데이터 풀 인스턴스를 모두에 동일한 데이터가 있는지 즉 분포 유형입니다. |
| 외부 테이블 개선 | HADOOP 데이터 원본 형식의 외부 테이블은 이제 최대 1 MB 크기의 행 읽기를 지원합니다. 외부 테이블(ODBC, 스토리지 풀, 데이터 풀)은 이제 SQL Server 테이블만큼 폭이 넓은 행을 지원합니다. |

### <a name="known-issues"></a>알려진 문제

다음 섹션의 알려진된 문제 및 제한 사항이이 릴리스를 사용 하 여 설명합니다.

#### <a name="hdfs"></a>HDFS

- Azure Data Studio HDFS에서 새 폴더를 만들려고 할 때 오류를 반환 합니다. 이 기능을 사용 하도록 설정 하려면 Azure Data Studio의 참가자 빌드를 설치 합니다.
  
   - [Windows 사용자 관리자- **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Windows 시스템 관리자- **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [Windows ZIP- **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [macOS-ZIP **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [TAR Linux입니다. -GZ **참가자 빌드**](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- 미리 HDFS의 파일을 마우스 오른쪽 단추로 클릭 하는 경우 다음 오류가 표시 될 수 있습니다.

   `Error previewing file: File exceeds max size of 30MB`

   현재는 Azure Data Studio에서 30 MB 보다 큰 파일을 미리 볼 수 없습니다.

- 구성 변경 내용은 hdfs-site.xml 변경 내용을 포함 하는 HDFS에 지원 되지 않습니다.

#### <a name="deployment"></a>배포

- CTP 3.0에서 GPU 사용 하는 빅 데이터 클러스터에 대 한 이전 배포 절차를 사용 하는 것이 없습니다. 대체 배포 프로시저를 조사 중입니다. 지금은 "배포는 빅 데이터 GPU 지원이 포함 된 클러스터 및 TensorFlow 실행" 문서 혼동을 피하기 위해 일시적으로 게시 된가 합니다.

- 이전 릴리스에서 빅 데이터 데이터 클러스터를 업그레이드 하는 것은 지원 되지 않습니다.

   > [!IMPORTANT]
   > 데이터를 백업 하 고 다음 기존 빅 데이터 클러스터를 삭제 해야 합니다 (이전 버전의를 사용 하 여 **mssqlctl**) 최신 릴리스를 배포 하기 전에 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)합니다.

- AKS를 배포한 후 배포에서 다음 두 경고 이벤트를 볼 수 있습니다. 이러한 이벤트는 알려진 문제, 있지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포를 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패 하면 연결된 된 네임 스페이스 제거 되지 않습니다. 이 클러스터에서 분리 된 네임 스페이스를 발생할 수 있습니다. 동일한 이름 사용 하 여 클러스터를 배포 하기 전에 네임 스페이스를 수동으로 삭제 됩니다.

#### <a name="external-tables"></a>외부 테이블

- 빅 데이터 클러스터 배포에서는 더 이상 합니다 **SqlDataPool** 하 고 **SqlStoragePool** 외부 데이터 원본입니다. 이러한 데이터 원본은 데이터 풀 및 저장소 풀 데이터 가상화를 지원 하도록 수동으로 만들 수 있습니다.

   > [!NOTE]
   > 이러한 외부 데이터 원본 만들기에 대 한 URI가 Ctp에 따라 다릅니다. 만드는 방법은 다음 TRANSACT-SQL 명령을 참조 하세요 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 지원 되지 않는 열 형식에는 테이블에 대 한 데이터 풀 외부 테이블을 만들 가능성이 있습니다. 외부 테이블을 쿼리 하는 경우 메시지가 다음과 비슷합니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 오류가 발생할 수 있습니다는 동시에 기본 파일은 HDFS에 복사 되는 경우.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에는 외부 테이블을 만들면 Azure Data Studio virtualization 마법사는 외부 테이블 정의에서 이러한 열 VARCHAR로 해석 합니다. 외부 테이블 DDL에에서 실패를 하면 합니다. 하거나 NVARCHAR2 유형을 사용 하 여 또는 EXTERNAL TABLE 문을 수동으로 만들고, 마법사를 사용 하는 대신 NVARCHAR를 지정 하는 Oracle 스키마를 수정 합니다.

#### <a name="application-deployment"></a>응용 프로그램 개발

- R, Python 또는 MLeap 응용 프로그램에서 RESTful API를 호출할 때 호출에에서 시간 초과 5 분입니다.

#### <a name="spark-and-notebooks"></a>Spark 및 notebook

- POD IP 주소는 Pod 다시 시작으로 Kubernetes 환경에서 변경 될 수 있습니다. 마스터 pod를 다시 시작 되는 시나리오에서 Spark 세션을 사용 하 여 못할 `NoRoteToHostException`합니다. 이 새 IP를 사용 하 여 새로 고쳐지는 가져오기 하지 JVM 캐시 주소입니다.

- Windows에 이미 설치 된 Jupyter 및 별도 Python을 있다면 Spark 노트북 실패할 수 있습니다. 이 문제를 해결 하려면 Jupyter를 최신 버전으로 업그레이드 합니다.

- 노트북을 클릭할 경우에 **텍스트 추가** 명령, 텍스트 셀이 편집 모드 보다는 미리 보기 모드에서 추가 됩니다. 편집 모드에 있고 셀을 편집 하 여 전환한 다음 미리 보기 아이콘을 클릭할 수 있습니다.

#### <a name="security"></a>보안

- SA_PASSWORD는 (예: 코드 덤프 파일)의 일부 환경의 및 검색할 수입니다. 배포 후 마스터 인스턴스에서 SA_PASSWORD 다시 설정 해야 합니다. 이 변경은 버그 아니라 보안 단계입니다. Linux 컨테이너에서 SA_PASSWORD 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)합니다.

- AKS 로그는 빅 데이터 클러스터 배포에 대 한 SA 암호를 포함할 수 있습니다.

## <a id="ctp25"></a> CTP 2.5 (월)

다음 섹션에서는 새로운 기능 및 SQL Server 2019 CTP 2.5에서 빅 데이터 클러스터에 대해 알려진된 문제를 설명합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| 배포 프로필 | 환경 변수 대신 빅 데이터 클러스터 배포를 위해 기본 및 사용자 지정된 [배포 구성 JSON 파일](deployment-guidance.md#configfile)을 사용합니다. |
| 프롬프트된 배포 | `mssqlctl cluster create`는 이제 기본 배포에 필요한 설정을 묻는 메시지를 표시합니다. |
| 서비스 엔드포인트 및 pod 이름 변경 | 다음 외부 끝점 이름이 변경 되었습니다.<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| **mssqlctl** 개선 사항 | **mssqlctl**를 사용하여 [외부 엔드포인트를 나열](deployment-guidance.md#endpoints)하고 **mssqlctl**의 버전을 `--version` 매개 변수로 확인합니다. |
| 오프라인 설치 | 오프 라인 빅 데이터 클러스터 배포에 대 한 지침입니다. |
| HDFS 계층화 개선 사항 | S3 계층, 탑재 캐싱 및 OAuth Gen2 ADLS에 대 한 지원. |
| 새 `mssql` Spark-SQL Server 커넥터 | |

### <a name="known-issues"></a>알려진 문제

다음 섹션의 알려진된 문제 및 제한 사항이이 릴리스를 사용 하 여 설명합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서 빅 데이터 데이터 클러스터를 업그레이드 하는 것은 지원 되지 않습니다.

   > [!IMPORTANT]
   > 데이터를 백업 하 고 다음 기존 빅 데이터 클러스터를 삭제 해야 합니다 (이전 버전의를 사용 하 여 **mssqlctl**) 최신 릴리스를 배포 하기 전에 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)합니다.

- AKS를 배포한 후 배포에서 다음 두 경고 이벤트를 볼 수 있습니다. 이러한 이벤트는 알려진 문제, 있지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포를 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패 하면 연결된 된 네임 스페이스 제거 되지 않습니다. 이 클러스터에서 분리 된 네임 스페이스를 발생할 수 있습니다. 동일한 이름 사용 하 여 클러스터를 배포 하기 전에 네임 스페이스를 수동으로 삭제 됩니다.

#### <a name="external-tables"></a>외부 테이블

- 빅 데이터 클러스터 배포에서는 더 이상 합니다 **SqlDataPool** 하 고 **SqlStoragePool** 외부 데이터 원본입니다. 이러한 데이터 원본은 데이터 풀 및 저장소 풀 데이터 가상화를 지원 하도록 수동으로 만들 수 있습니다.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- 지원 되지 않는 열 형식에는 테이블에 대 한 데이터 풀 외부 테이블을 만들 가능성이 있습니다. 외부 테이블을 쿼리 하는 경우 메시지가 다음과 비슷합니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 오류가 발생할 수 있습니다는 동시에 기본 파일은 HDFS에 복사 되는 경우.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에는 외부 테이블을 만들면 Azure Data Studio virtualization 마법사는 외부 테이블 정의에서 이러한 열 VARCHAR로 해석 합니다. 외부 테이블 DDL에에서 실패를 하면 합니다. 하거나 NVARCHAR2 유형을 사용 하 여 또는 EXTERNAL TABLE 문을 수동으로 만들고, 마법사를 사용 하는 대신 NVARCHAR를 지정 하는 Oracle 스키마를 수정 합니다.

#### <a name="application-deployment"></a>응용 프로그램 개발

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

## <a id="ctp24"></a> CTP 2.4 (3 월)

다음 섹션에서는 새로운 기능 및 SQL Server 2019 CTP 2.4에서 빅 데이터 클러스터에 대해 알려진된 문제를 설명합니다.

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
|:---|:---|
| Spark에서 TensorFlow를 사용하여 딥 러닝을 실행하기 위한 GPU 지원 지침. | [GPU 지원이 포함된 빅 데이터 클러스터를 배포하고 TensorFlow를 실행](spark-gpu-tensorflow.md)합니다. |
| **SqlDataPool** 및 **SqlStoragePool** 데이터 원본은 더 이상 기본적으로 생성되지 않습니다. | 필요에 따라 수동으로 만듭니다. [알려진 문제](#externaltablesctp24)를 참조하세요. |
| `INSERT INTO SELECT`가 데이터 풀을 지원합니다. | 예제를 보려면 [ 자습서: Transact-SQL을 사용하여 SQL Server 데이터 풀에 데이터 수집](tutorial-data-pool-ingest-sql.md)을 참조하세요. |
| `FORCE SCALEOUTEXECUTION` 및 `DISABLE SCALEOUTEXECUTION` 옵션. | 강제로 또는 외부 테이블에서 쿼리 계산 풀을 사용 하는 사용 하지 않도록 설정 합니다. `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)` )을 입력합니다. |
| AKS 배포 권장 사항을 업데이트합니다. | AKS에서 빅 데이터 클러스터를 평가할 때 이제 **Standard_L8s** 크기의 단일 노드를 사용하는 것이 좋습니다. |
| Spark 런타임을 Spark 런타임 2.4로 업그레이드합니다. | |

### <a name="known-issues"></a>알려진 문제

다음 섹션의 알려진된 문제 및 제한 사항이이 릴리스를 사용 하 여 설명합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서 빅 데이터 데이터 클러스터를 업그레이드 하는 것은 지원 되지 않습니다.

   > [!IMPORTANT]
   > 데이터를 백업 하 고 다음 기존 빅 데이터 클러스터를 삭제 해야 합니다 (이전 버전의를 사용 하 여 **mssqlctl**) 최신 릴리스를 배포 하기 전에 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)합니다.

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

#### <a name="delete-cluster-fails"></a>클러스터 실패를 삭제 합니다.

사용 하 여 클러스터를 삭제 하려고 할 때 **mssqlctl**, 다음 오류로 인해 실패 합니다.

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

새 Python Kubernetes 클라이언트 (버전 9.0.0) 변경 삭제 네임 스페이스는 API를 현재 중단 **mssqlctl**합니다. 이 새로운 Kubernetes python 클라이언트가 설치 되어 있는 경우에 발생 합니다. 직접 사용 하 여 클러스터를 삭제 하 여이 문제를 해결할 수 있습니다 **kubectl** (`kubectl delete ns <ClusterName>`)를 사용 하 여 이전 버전을 설치할 수 있습니다 또는 `sudo pip install kubernetes==8.0.1`합니다.

#### <a id="externaltablesctp24"></a> 외부 테이블

- 빅 데이터 클러스터 배포에서는 더 이상 합니다 **SqlDataPool** 하 고 **SqlStoragePool** 외부 데이터 원본입니다. 이러한 데이터 원본은 데이터 풀 및 저장소 풀 데이터 가상화를 지원 하도록 수동으로 만들 수 있습니다.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- 지원 되지 않는 열 형식에는 테이블에 대 한 데이터 풀 외부 테이블을 만들 가능성이 있습니다. 외부 테이블을 쿼리 하는 경우 메시지가 다음과 비슷합니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 오류가 발생할 수 있습니다는 동시에 기본 파일은 HDFS에 복사 되는 경우.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에는 외부 테이블을 만들면 Azure Data Studio virtualization 마법사는 외부 테이블 정의에서 이러한 열 VARCHAR로 해석 합니다. 외부 테이블 DDL에에서 실패를 하면 합니다. 하거나 NVARCHAR2 유형을 사용 하 여 또는 EXTERNAL TABLE 문을 수동으로 만들고, 마법사를 사용 하는 대신 NVARCHAR를 지정 하는 Oracle 스키마를 수정 합니다.

#### <a name="application-deployment"></a>응용 프로그램 개발

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

### <a name="whats-new"></a>What's New

| 새로운 기능 또는 업데이트 | 설명 |
| :---------- | :------ |
| IntelliJ의 빅 데이터 클러스터에 Spark 작업을 제출합니다. | [IntelliJ의 SQL Server 빅 데이터 클러스터에 Spark 작업 제출](spark-submit-job-intellij-tool-plugin.md) |
| 애플리케이션 배포 및 클러스터 관리를 위한 일반 CLI. | [SQL Server 2019 빅 데이터 클러스터에 앱을 배포하는 방법(미리 보기)](big-data-cluster-create-apps.md) |
| 애플리케이션을 빅 데이터 클러스터에 배포하기 위한 VS Code 확장. | [VS Code를 사용하여 SQL Server 빅 데이터 클러스터에 애플리케이션을 배포하는 방법](app-deployment-extension.md) |
| **mssqlctl** 도구 명령 사용법이 변경되었습니다. | 자세한 내용은 [mssqlctl의 알려진 문제](#mssqlctlctp23)를 참조하세요. |
| 빅 데이터 클러스터에 사용 하 여 Sparklyr | [SQL Server 2019 빅 데이터 클러스터에서 Sparklyr 사용](sparklyr-from-RStudio.md) |
| **HDFS 계층화**를 통해 빅 데이터 클러스터에 외장 HDFS 호환 스토리지를 탑재합니다. | [HDFS 계층화](hdfs-tiering.md)를 참조하세요 |
| SQL Server 마스터 인스턴스 및 HDFS/Spark 게이트웨이에 대한 새로운 통합 연결 환경. | [SQL Server 마스터 인스턴스 및 HDFS/Spark 게이트웨이](connect-to-big-data-cluster.md)를 참조하세요. |
| **mssqlctl 클러스터 삭제**를 통해 클러스터를 삭제하면 이제 빅 데이터 클러스터의 일부인 네임스페이스의 개체만 삭제됩니다. | 네임스페이스는 삭제되지 않습니다. 그러나 이전 릴리스에서 이 명령은 전체 네임스페이스를 삭제했습니다. |
| _보안_ 엔드포인트 이름이 변경되고 통합되었습니다. | **service-security-lb** 및 **service-security-nodeport**가 **endpoint-security** 엔드포인트에 통합되었습니다. |
| _프록시_ 엔드포인트 이름이 변경되고 통합되었습니다. | **service-proxy-lb** 및 **service-proxy-nodeport**가 **endpoint-service-proxy** 엔드포인트에 통합되었습니다. |
| _컨트롤러_ 엔드포인트 이름이 변경되고 통합되었습니다. | **service-mssql-controller-lb** 및 **service-mssql-controller-nodeport**가 **endpoint-controller** 엔드포인트에 통합되었습니다. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

다음 섹션의 알려진된 문제 및 제한 사항이이 릴리스를 사용 하 여 설명합니다.

#### <a name="deployment"></a>배포

- 이전 릴리스에서 빅 데이터 데이터 클러스터를 업그레이드 하는 것은 지원 되지 않습니다.

   > [!IMPORTANT]
   > 데이터를 백업 하 고 다음 기존 빅 데이터 클러스터를 삭제 해야 합니다 (이전 버전의를 사용 하 여 **mssqlctl**) 최신 릴리스를 배포 하기 전에 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)합니다.

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

- 빅 데이터 클러스터의 최신 버전으로 업그레이드 하는 방법에 대 한 중요 한 정보에 대 한 및 **mssqlctl**를 참조 하십시오 [새 릴리스로 업그레이드](deployment-upgrade.md)합니다.

#### <a name="external-tables"></a>외부 테이블

- 지원 되지 않는 열 형식에는 테이블에 대 한 데이터 풀 외부 테이블을 만들 가능성이 있습니다. 외부 테이블을 쿼리 하는 경우 메시지가 다음과 비슷합니다.

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 저장소 풀 외부 테이블을 쿼리 하는 경우 오류가 발생할 수 있습니다는 동시에 기본 파일은 HDFS에 복사 되는 경우.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 문자 데이터 형식을 사용 하는 Oracle에는 외부 테이블을 만들면 Azure Data Studio virtualization 마법사는 외부 테이블 정의에서 이러한 열 VARCHAR로 해석 합니다. 외부 테이블 DDL에에서 실패를 하면 합니다. 하거나 NVARCHAR2 유형을 사용 하 여 또는 EXTERNAL TABLE 문을 수동으로 만들고, 마법사를 사용 하는 대신 NVARCHAR를 지정 하는 Oracle 스키마를 수정 합니다.

#### <a name="application-deployment"></a>응용 프로그램 개발

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

- 이전 릴리스에서 빅 데이터 데이터 클러스터를 업그레이드 하는 것은 지원 되지 않습니다. 백업 하 고 최신 릴리스를 배포 하기 전에 모든 기존 빅 데이터 클러스터를 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)합니다.

- AKS를 배포한 후 배포에서 다음 두 경고 이벤트를 볼 수 있습니다. 이러한 이벤트는 알려진 문제, 있지만 AKS에서 빅 데이터 클러스터를 성공적으로 배포를 방지 하지 않습니다.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 빅 데이터 클러스터 배포에 실패 하면 연결된 된 네임 스페이스 제거 되지 않습니다. 이 클러스터에서 분리 된 네임 스페이스를 발생할 수 있습니다. 동일한 이름 사용 하 여 클러스터를 배포 하기 전에 네임 스페이스를 수동으로 삭제 됩니다.

#### <a name="cluster-administration-portal"></a>클러스터 관리 포털

클러스터 관리 포털에서 마스터 SQL Server 인스턴스에 대 한 끝점을 표시 하지 않습니다. 마스터 인스턴스에 대 한 IP 주소 및 포트를 찾으려면 다음 사용 **kubectl** 명령:

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
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

- 이전 릴리스에서 빅 데이터 데이터 클러스터를 업그레이드 하는 것은 지원 되지 않습니다. 백업 하 고 최신 릴리스를 배포 하기 전에 모든 기존 빅 데이터 클러스터를 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)합니다.

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
