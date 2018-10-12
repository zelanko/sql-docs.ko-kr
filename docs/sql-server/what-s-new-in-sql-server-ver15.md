---
title: SQL Server 2019의 새로운 기능 | Microsoft Docs
ms.custom: ''
ms.date: 09/26/2018
ms.prod: sql-server-2018
ms.reviewer: ''
ms.technology:
- server-general
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 68a872164528bec49b0342f603107fb86e31fe50
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678271"
---
# <a name="whats-new-in-sql-server-2019"></a>SQL Server 2019의 새로운 기능

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)]는 이전 릴리스를 토대로 구축되었으며 개발 언어, 데이터 형식, 온-프레미스 또는 클라우드, 운영 체제를 선택할 수 있는 플랫폼으로 개선되었습니다. 이 문서에서는 SQL Server 2019의 새로운 기능을 요약해서 설명합니다. 자세한 내용 및 알려진 문제에 대해서는 [SQL Server 2019 릴리스 정보](sql-server-ver15-release-notes.md)를 참조하세요.

**SQL Server 2019를 사용해 보세요.**
- [![평가 센터에서 다운로드](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=862101) [SQL Server 2019를 다운로드하여 Windows에 설치](http://go.microsoft.com/fwlink/?LinkID=862101)
- [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md), [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 및 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)용 Linux에 설치
- [Docker의 SQL Server 2019에서 실행](../linux/quickstart-install-connect-docker.md)

## <a name="ctp-20"></a>CTP 2.0 

CTP(Community Technology Preview) 2.0은 [!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)]의 첫 번째 공개 릴리스입니다. [!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)] CTP 2.0용으로 추가되었거나 개선된 기능은 다음과 같습니다.

- [빅 데이터 클러스터](#bigdatacluster)
  - Kubernetes에서 SQL 및 Spark Linux 컨테이너를 사용하여 빅 데이터 클러스터 배포
  - HDFS에서 빅 데이터에 액세스
  - Spark에서 고급 분석 및 Machine Learning 실행
  - Spark Streaming을 사용하여 SQL 데이터 풀에 데이터 스트리밍
  - Azure Data Studio를 사용하여 노트 환경을 제공하는 쿼리 책 실행

- [데이터베이스 엔진](#databaseengine)
  - UTF-8 지원
  - 다시 시작 가능한 온라인 인덱스 만들기를 통해 중단 후에 인덱스 만들기를 다시 시작할 수 있음
  - 클러스터형 columnstore 온라인 인덱스 작성 및 다시 작성
  - 보안 Enclave를 사용한 Always Encrypted
  - 지능형 쿼리 처리
  - Java 언어 프로그래밍 기능 확장
  - SQL 그래프 기능
  - 온라인 및 다시 시작 가능한 DDL 작업에 대한 데이터베이스 범위 구성 설정
  - Always On 가용성 그룹 - 보조 복제본 연결 리디렉션
  - 데이터 검색 및 분류 - SQL Server에 기본적으로 제공
  - 영구 메모리 장치에 대한 확장 지원
  - `DBCC CLONEDATABASE`에서 Columnstore 통계 지원
  - `sp_estimate_data_compression_savings`에 새로 추가된 옵션
  - SQL Server Machine Learning Services 장애 조치(Failover) 클러스터
  - 간단한 쿼리 프로파일링 인프라가 기본적으로 사용 가능
  - 새 Polybase 커넥터
  - 페이지 정보를 반환하는 새 `sys.dm_db_page_info` 시스템 함수

- [Linux의 SQL Server](#sqllinux)
  - 복제 지원
  - MSDTC(Microsoft Distributed Transaction Coordinator) 지원
  - Kubernetes를 사용하는 Docker 컨테이너의 Always On 가용성 그룹
  - 타사 AD 공급자에 대한 OpenLDAP 지원
  - Linux의 Machine Learning
  - 새 컨테이너 레지스트리
  - 새 RHEL 기반 컨테이너 이미지
  - 메모리 부족 알림

- [MDS(Master Data Services)](#mds)
  - Silverlight 컨트롤이 대체됨

- [보안](#security)
  - SQL Server 구성 관리자의 인증서 관리

- [도구](#tools)
  - SSMS(SQL Server Management Studio) 18.0(미리 보기)
  - Azure Data Studio

이러한 기능에 대한 자세한 내용을 보려면 계속 읽어보세요.

## <a id="bigdatacluster"></a>빅 데이터 클러스터

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] [빅 데이터 클러스터](../big-data-cluster/big-data-cluster-overview.md)는 다음을 비롯한 새로운 시나리오를 지원합니다.

- Kubernetes에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 Spark Linux 컨테이너를 사용하여 빅 데이터 클러스터 배포
- HDFS에서 빅 데이터에 액세스
- Spark에서 고급 분석 및 Machine Learning 실행
- Spark Streaming을 사용하여 SQL 데이터 풀에 데이터 스트리밍
- [**Azure Data Studio**](../sql-operations-studio/what-is.md)에서 노트 환경을 제공하는 쿼리 책 실행
  
[!INCLUDE [Big Data Clusters preview](../includes/big-data-cluster-preview-note.md)]

## <a id="databaseengine"></a> 데이터베이스 엔진

CTP 2.0에서는 다음과 같은 [!INCLUDE[ssdeNoVersion](../includes/ssdenoversion_md.md)]의 새로운 기능을 도입하거나 향상된 기능을 제공합니다.

### <a name="database-compatibility-level"></a>데이터베이스 호환성 수준

데이터베이스 **COMPATIBILITY_LEVEL 150**이 추가되었습니다. 특정 사용자 데이터베이스를 사용하려면 다음을 실행합니다.

   ```sql
   ALTER DATABASE database_name SET COMPATIBILITY_LEVEL =  150;
   ```

### <a name="utf-8-support"></a>UTF-8 지원

가져오기 또는 내보내기 인코딩이나 텍스트 데이터의 데이터베이스 수준 또는 열 수준 데이터 정렬로 널리 사용되는 UTF-8 문자 인코딩이 완전히 지원됩니다. UTF-8은 `CHAR` 및 `VARCHAR` 데이터 형식에서 허용되며, `UTF8` 접미사를 사용하여 개체의 데이터 정렬을 만들거나 이 접미사를 갖는 데이터 정렬로 변경하여 설정합니다. 

예를 들어 `LATIN1_GENERAL_100_CI_AS_SC`에서 `LATIN1_GENERAL_100_CI_AS_SC_UTF8`로 변경합니다. UTF-8은 SQL Server 2012에 도입된 보충 문자를 지원하는 Windows 데이터 정렬에서만 사용할 수 있습니다. `NCHAR` 및 `NVARCHAR`는 UTF-16 인코딩만 허용하며 변경되지 않고 유지됩니다.

이 기능은 사용 중인 문자 집합에 따라 저장소 비용을 크게 절감하는 효과를 제공할 수 있습니다. 예를 들어, ASCII 문자열을 포함하는 기존 열 데이터 형식을 UTF-8 사용 데이터 정렬을 통해 `NCHAR(10)`에서 `CHAR(10)`으로 변경하면 저장소 요구 수준이 거의 50%로 감소합니다. 이러한 감소는 `NCHAR(10)`에는 저장소로 22바이트가 필요하지만 `CHAR(10)`에는 동일한 유니코드 문자열에 대해 12바이트만 필요하기 때문입니다.

### <a name="resumable-online-index-create"></a>다시 시작 가능한 온라인 인덱스 만들기

- **다시 시작 가능한 온라인 인덱스 만들기**를 사용하면 인덱스 만들기 작업을 일시 중지한 후 처음부터 다시 시작하지 않고, 작업이 일시 중지되었거나 실패한 지점부터 다시 시작할 수 있습니다.

  다시 시작 가능한 온라인 인덱스 만들기는 다음 시나리오를 지원합니다.
  - 인덱스 만들기 실패 후[예: 데이터베이스 장애 조치(Failover) 이후 또는 디스크 공간이 부족해진 이후] 인덱스 만들기 작업을 다시 시작합니다.
  - 진행 중인 인덱스 만들기 작업을 일시 중지하여 필요할 때 시스템 리소스를 일시적으로 사용 가능하게 만들고 나중에 이 작업을 다시 시작합니다.
  - 많은 로그 공간과 장기 실행 트랜잭션을 사용하여 다른 유지 관리 작업을 차단하거나 로그 잘림을 허용하지 않으면서 큰 인덱스를 만듭니다.

  인덱스 만들기가 실패하는 경우 이 기능을 사용하지 않고 온라인 인덱스 만들기 작업을 다시 실행해야 하며 작업을 처음부터 다시 시작해야 합니다.

이 릴리스에서는 다시 시작 가능한 기능을 확장하여 사용 가능한 [다시 시작 가능한 온라인 인덱스 다시 작성](http://azure.microsoft.com/blog/modernize-index-maintenance-with-resumable-online-index-rebuild/)에 이 기능을 추가합니다.

또한 [온라인 및 다시 시작 가능한 DDL 작업의 데이터베이스 범위 기본 설정](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 사용하여 이 기능을 특정 데이터베이스의 기본값으로 설정할 수 있습니다.

자세한 내용은 [다시 시작 가능한 온라인 인덱스 만들기](../t-sql/statements/create-index-transact-sql.md#resumable-indexes)를 참조하세요.

### <a name="build-and-rebuild-clustered-columnstore-indexes-online"></a>온라인으로 클러스터형 columnstore 인덱스 작성 및 다시 작성

행 저장소 테이블을 columnstore 형식으로 변환합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 CCI(클러스터형 columnstore 인덱스) 만들기가 오프라인 프로세스였으므로 CCI를 만드는 동안 모든 변경을 중지해야 했습니다. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 및 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]를 사용하여 온라인으로 CCI를 만들거나 다시 만들 수 있습니다. 워크로드는 차단되지 않으며 기본 데이터에 대해 수행한 모든 변경 내용이 대상 columnstore 테이블에 투명하게 추가됩니다. 사용할 수 있는 새 [!INCLUDE[tsql](../includes/tsql-md.md)] 문 예제는 다음과 같습니다.

  ```sql
  CREATE CLUSTERED COLUMNSTORE INDEX cci
    ON <tableName>
    WITH (ONLINE = ON);
  ```

  ```sql
  ALTER INDEX cci
    ON <tableName>
    REBUILD WITH (ONLINE = ON);
  ```

### <a name="always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted

바로 암호화 및 리치 계산으로 Always Encrypted를 확장합니다. 확장은 서버 쪽의 보안 Enclave 내에서 일반 텍스트 데이터에 대해 계산을 사용하도록 설정하여 제공됩니다.

암호화 작업에는 열 암호화 및 열 암호화 키 순환이 포함됩니다. 이제 이러한 작업은 [!INCLUDE[tsql](../includes/tsql-md.md)]를 사용하여 실행할 수 있으며 데이터를 데이터베이스 밖으로 이동할 필요가 없습니다. 보안 Enclave는 다음과 같은 요구 사항을 갖는 보다 광범위한 시나리오에 Always Encrypted를 제공합니다.  

- 데이터베이스 관리자, 시스템 관리자, 클라우드 운영자 또는 맬웨어를 포함하여 높은 권한을 갖지만 아직 허가되지 않은 사용자로부터 중요한 데이터를 보호해야 합니다.
- 데이터베이스 시스템 내에서 보호된 데이터에 대한 리치 계산을 지원해야 합니다.

자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.

> [!NOTE]
> 보안 Enclave를 사용한 Always Encrypted는 Windows OS에서만 사용할 수 있습니다.

### <a name="intelligent-query-processing"></a>지능형 쿼리 처리

- **행 모드 메모리 부여 피드백**은 일괄 처리 및 행 모드 연산자의 메모리 부여 크기를 둘 다 조정하여 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]에 도입된 메모리 부여 피드백 기능을 확장합니다.  과도한 메모리 부여 조건의 경우 부여된 메모리가 실제로 사용된 메모리 크기의 두 배를 초과하면 메모리 부여 피드백이 메모리 부여를 다시 계산합니다. 그런 이후에는 연속 실행에 더 적은 메모리가 요구됩니다. 크기가 부족한 메모리 부여의 경우 디스크로 분산이 발생하며 메모리 부여 피드백이 메모리 부여 다시 계산을 트리거합니다. 그런 이후에는 연속 실행에 더 많은 메모리가 요구됩니다. 이 기능은 데이터베이스 호환성 수준 150에서 기본적으로 사용하도록 설정됩니다.

- **Approximate COUNT DISTINCT**는 그룹에 있는 고유한 null이 아닌 값의 대략적인 개수를 반환합니다. 이 함수는 빅 데이터 시나리오에서 사용하도록 디자인되었습니다. 이 함수는 다음 조건이 모두 true인 쿼리에서 최적화됩니다.
   - 수백만 개 이상의 행이 있는 데이터 집합에 액세스합니다.
   - 많은 수의 고유 값이 포함된 열을 집계합니다.
   - 응답성이 절대 정밀도보다 더 중요합니다.
      - `APPROX_COUNT_DISTINCT`는 일반적으로 정확한 응답의 2% 내에 있는 결과를 반환합니다.
      - 또한 대략적인 응답의 경우 정확한 응답에 필요한 시간보다 짧은 시간 내에 반환됩니다.

- **Rowstore의 일괄 처리 모드**에서는 더 이상 columnstore 인덱스가 쿼리를 일괄 처리 모드에서 처리할 필요가 없습니다. 일괄 처리 모드에서는 쿼리 연산자가 한 번에 행 1개가 아닌 행 집합에 작동할 수 있습니다. 이 기능은 데이터베이스 호환성 수준 150에서 기본적으로 사용하도록 설정됩니다. 일괄 처리 모드를 사용할 경우 다음 조건이 모두 true이면 rowstore 테이블에 액세스하는 쿼리의 속도가 빨라집니다.
   - 쿼리가 조인 또는 집계 연산자와 같은 분석 연산자를 사용합니다.
   - 쿼리에 100,000개 이상의 행에 사용됩니다.
   - 쿼리가 입/출력 데이터가 아니라 CPU에 따라 좌우됩니다.
   - Columnstore 인덱스의 생성 및 사용할 경우 다음과 같은 단점 중 하나가 발생할 수 있습니다.
      - 쿼리에 너무 많은 오버헤드가 추가됩니다.
      - 그렇지 않더라도 응용 프로그램이 columnstore 인덱스에서 아직 지원되지 않는 기능에 의존하기 때문에 실현 가능하지 않습니다.

- **테이블 변수 지연 컴파일**은 테이블 변수를 참조하는 쿼리의 플랜 품질 및 전체 성능을 개선합니다. 최적화 및 초기 컴파일 중에 이 기능은 실제 테이블 변수 행 수를 기반으로 하는 카디널리티 예측을 전파합니다.  이 정확한 행 수 정보는 다운스트림 계획 작업을 최적화하는 데 사용됩니다. 이 기능은 데이터베이스 호환성 수준 150에서 기본적으로 사용하도록 설정됩니다.

지능형 쿼리 처리 기능을 사용하려면 데이터베이스 `COMPATIBILITY_LEVEL = 150`을 설정합니다.

### <a id="programmability"></a> Java 언어 프로그래밍 기능 확장

- **Java 언어 확장(미리 보기)**: Java 언어 확장을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 Java 코드를 실행합니다. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서 이 확장은 SQL Server 인스턴스에 'Machine Learning Services(데이터베이스 내)' 기능을 추가할 때 설치됩니다.

### <a id="sqlgraph"></a> SQL 그래프 기능

- **`MERGE` DML**의 일치 지원을 통해 그래프 관계를 별도의 `INSERT`, `UPDATE` 또는 `DELETE` 문이 아닌 단일 문에 지정할 수 있습니다. `MERGE` 문에 `MATCH` 조건자를 사용하여 노드 또는 에지 테이블의 현재 그래프 데이터를 새 데이터와 병합합니다. 이 기능을 통해 에지 테이블의 `UPSERT` 시나리오가 지원됩니다. 이제 단일 병합 문을 사용하여 두 노드 간에 새 에지를 삽입하거나 기존 에지를 업데이트할 수 있습니다.

- **에지 제약 조건**은 SQL 그래프의 에지 테이블을 위해 도입되었습니다. 에지 테이블은 임의 노드를 데이터베이스의 다른 노드에 연결할 수 있습니다. 에지 제약 조건의 도입으로, 이제 이러한 동작을 어느 정도 제한할 수 있습니다. 새 `CONNECTION` 제약 조건을 사용하여 지정된 에지 테이블이 스키마에서 연결하도록 허용되는 노드 유형을 지정할 수 있습니다.

### <a name="database-scoped-default-setting-for-online-and-resumable-ddl-operations"></a>온라인 및 다시 시작 가능한 DDL 작업에 대한 데이터베이스 범위 기본 설정 

- **온라인 및 다시 시작 가능한 DDL 작업에 대한 데이터베이스 범위 기본 설정**을 사용하여 인덱스 만들기 또는 다시 작성과 같은 개별 인덱스 DDL 문에 대해 이러한 옵션을 정의하지 않고, 데이터베이스 수준에서 `ONLINE` 및 `RESUMABLE` 인덱스 작업에 대한 기본 동작 설정 지정할 수 있습니다.

- `ELEVATE_ONLINE` 및 `ELEVATE_RESUMABLE` 데이터베이스 범위 구성 옵션을 사용하여 이러한 기본값을 설정합니다. 두 옵션 모두 엔진이 지원되는 작업의 권한을 자동으로 온라인 또는 다시 시작이 가능 인덱스 실행으로 상승시키도록 합니다. 이러한 옵션을 사용하여 다음 동작을 사용하도록 설정할 수 있습니다.

  - `FAIL_UNSUPPORTED` 옵션을 사용하면 온라인 또는 다시 시작 가능한 모든 인덱스 작업을 허용하고 온라인 또는 다시 시작 가능 방식이 지원되지 않는 인덱스 작업을 실패하도록 할 수 있습니다.
  - `WHEN_SUPPPORTED` 옵션을 사용하면 온라인 또는 다시 시작 가능한 지원되는 작업을 허용하고 지원되지 않는 인덱스 작업을 오프라인 또는 다시 시작 불가능 방식으로 실행할 수 있습니다.
  - `OFF` 옵션을 사용하면 DDL 문에 명시적으로 지정되지 않는 한, 모든 인덱스 작업을 오프라인 및 다시 시작 불가능 방식으로 실행하는 현재 동작이 허용됩니다.

기본 설정을 재정의하려면 인덱스 만들기 및 다시 작성 명령에 온라인 또는 다시 시작 가능 옵션을 포함합니다.  

이 기능을 사용하지 않을 경우 인덱스 만들기 및 다시 작성과 같은 인덱스 DDL 문에서 직접 온라인 및 다시 시작 가능 옵션을 지정해야 합니다.

추가 정보: 인덱스 다시 시작 가능 작업에 대한 자세한 내용은 [다시 시작 가능한 온라인 인덱스 만들기](http://azure.microsoft.com/blog/resumable-online-index-create-is-in-public-preview-for-azure-sql-db/)를 참조하세요.

### <a id="ha"></a>Always On 가용성 그룹 - 추가 동기 복제본 

- **최대 5개의 동기 복제본**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 최대 동기 복제본의 수가 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 3개에서 5개로 증가되었습니다. 그룹 내에서 자동 장애 조치(Failover)가 수행되도록 이러한 5개 복제본으로 이루어진 그룹을 구성할 수 있습니다. 이러한 그룹은 주 복제본 1개와 동기 보조 복제본 4개로 구성됩니다.

- **보조-주 복제본 연결 리디렉션**: 이 기능은 연결 문자열에 지정된 대상 서버에 관계없이, 클라이언트 응용 프로그램 연결이 주 복제본으로 전송되도록 합니다. 이 기능에서는 수신기 없는 연결 리디렉션이 허용됩니다. 다음과 같은 경우 보조-주 복제본 연결 리디렉션을 사용합니다.

  - 클러스터 기술이 수신기 기능을 제공하지 않습니다.
  - 리디렉션이 복잡한 다중 서브넷 구성을 사용하고 있습니다.
  - 클러스터 유형이 `NONE`인 읽기 스케일 아웃 또는 재해 복구 시나리오입니다.

자세한 내용은 [보조-주 복제본 읽기/쓰기 연결 리디렉션(Always On 가용성 그룹)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)을 참조하세요.

### <a name="data-discovery-and-classification"></a>데이터 검색 및 분류

데이터 검색 및 분류는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기본적으로 제공된 고급 기능을 제공합니다. 가장 중요한 데이터를 분류하고 레이블을 지정하면 다음과 같은 이점을 얻을 수 있습니다.
- 데이터 프라이버시 표준 및 규정 준수 요구 사항을 충족할 수 있습니다.
- 중요한 데이터에 대한 비정상적인 액세스 모니터링(감사) 및 경고 등의 보안 시나리오를 지원합니다.
- 엔터프라이즈에서 중요한 데이터가 있는 위치를 보다 쉽게 파악하여 관리자가 데이터베이스를 보호하기 위한 적절한 단계를 수행할 수 있습니다.

자세한 내용은 [SQL 데이터 검색 및 분류](../relational-databases/security/sql-data-discovery-and-classification.md)를 참조하세요.

또한 [감사](../relational-databases/security/auditing/sql-server-audit-database-engine.md) 기능도 감사 로그에 `data_sensitivity_information`라는 새 필드를 포함하도록 개선되었습니다. 이 필드는 쿼리가 반환한 실제 데이터의 민감도 분류(레이블)를 기록합니다. 자세한 내용과 예제를 보려면 [민감도 분류 추가](../t-sql/statements/add-sensitivity-classification-transact-sql.md)를 참조하세요.

>[!NOTE]
>감사를 사용하도록 설정하는 방법은 변경되지 않았습니다. 감사 레코드에는 `data_sensitivity_information`라는 새 필드가 있습니다. 이 필드는 쿼리가 반환한 실제 데이터의 민감도 분류(레이블)를 기록합니다. [중요한 데이터에 대한 액세스 감사](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-data-discovery-and-classification#subheading-3)를 참조하세요.

### <a name="expanded-support-for-persistent-memory-devices"></a>영구 메모리 장치에 대한 확장 지원

이제 영구 메모리 장치에 배치되는 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 파일은 *지원* 모드로 작동될 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 효율적인 memcpy 작업을 사용하여 운영 체제 저장소 스택을 우회하고 장치에 직접 액세스합니다. 이 모드는 이러한 장치에 대해 낮은 대기 시간의 입/출력을 허용하므로 성능을 향상시킵니다.
    - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 파일의 예에는 다음이 포함됩니다.
        - 데이터베이스 파일
        - 트랜잭션 로그 파일
        - 메모리 내 OLTP 검사점 파일
    - 영구 메모리를 저장소 클래스 메모리라고도 합니다.
    - Microsoft 이외의 일부 웹 사이트에서는 경우에 따라 영구 메모리를 비공식적으로 *pmem*이라고도 합니다.

> [!NOTE]
> 이 미리 보기 릴리스에는 영구 메모리 장치의 파일을 Linux에서만 사용할 수 있습니다. Windows의 SQL Server는 SQL Server 2016부터 영구 메모리 장치를 지원합니다.

### <a name="support-for-columnstore-statistics-in-dbcc-clonedatabase"></a>DBCC CLONEDATABASE에서 Columnstore 통계 지원

`DBCC CLONEDATABASE`는 데이터를 복사하지 않고 쿼리 성능 문제를 해결하는 데 필요한 모든 요소가 포함된 데이터베이스의 스키마 전용 복사본을 만듭니다.  이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 이 명령은 columnstore 인덱스 쿼리 문제를 정확히 해결하는 데 필요한 통계를 복사하지 않으므로 수동 단계를 통해 이 정보를 캡처해야 했습니다. 이제 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서 DBCC CLONEDATABASE는 columnstore 인덱스에 대한 통계 Blob을 자동으로 캡처하므로 수동 단계가 필요하지 않습니다.

### <a name="new-options-added-to-spestimatedatacompressionsavings"></a>sp_estimate_data_compression_savings에 새로 추가된 옵션

`sp_estimate_data_compression_savings`는 요청된 개체의 현재 크기를 반환하고 요청된 압축 상태에 대한 개체 크기를 예상합니다.  현재 이 프로시저는 `NONE`, `ROW` 및 `PAGE`의 세 가지 옵션을 지원합니다. SQL Server 2019는 두 가지 새 옵션인 `COLUMNSTORE` 및 `COLUMNSTORE_ARCHIVE`를 도입했습니다. 이러한 새 옵션을 사용하면 표준 또는 보관 columnstore 압축을 사용하여 테이블에서 columnstore 인덱스를 만들 경우의 예상되는 공간 절약을 추정할 수 있습니다.

### <a id="ml"></a> SQL Server Machine Learning Services 장애 조치(Failover) 클러스터 및 파티션 기반 모델링

- **파티션 기반 모델링**: `sp_execute_external_script`에 추가된 새 매개 변수를 사용하여 데이터 파티션별로 외부 스크립트를 처리합니다. 이 기능은 하나의 큰 모델 대신, 많은 작은 모델(데이터 파티션당 하나의 모델)을 학습하도록 지원합니다.

- **Windows Server 장애 조치(Failover) 클러스터**: Windows Server 장애 조치(Failover) 클러스터에서 Machine Learning 서비스의 고가용성을 구성합니다.

자세한 내용은 [SQL Server Machine Learning Services의 새로운 기능](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)을 참조하세요.

### <a name="lightweight-query-profiling-infrastructure-enabled-by-default"></a>간단한 쿼리 프로파일링 인프라가 기본적으로 사용 가능

LWP(간단한 쿼리 프로파일링 인프라)는 표준 프로파일링 기술보다 좀 더 효율적으로 쿼리 성능 데이터를 제공합니다. 간단한 프로파일링은 이제 기본적으로 사용되도록 설정됩니다. 이 기능은 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1에 도입되었습니다. 간단한 프로파일링은 표준 쿼리 프로파일링 메커니즘의 최대 75% CPU 오버헤드와 비교할 때 2% CPU 오버헤드가 예상되는 쿼리 실행 통계 수집 메커니즘을 제공합니다. 이전 버전에서 이 기능은 기본적으로 해제되었습니다. 데이터베이스 관리자는 [추적 플래그 7412](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 사용하여 이 기능을 사용하도록 설정할 수 있습니다. 

간단한 프로파일링에 대한 자세한 내용은 [Developers Choice: Query progress – anytime, anywhere](http://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)(개발자 선택 사항: 쿼리 진행률 - 시간, 장소에 제한 없음)를 참조하세요.

### <a id="polybase"></a>새 Polybase 커넥터

- **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata 및 MongoDB**용 새 커넥터: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata 및 MongoDB용 외부 데이터에 대한 새 커넥터를 도입했습니다.

### <a name="new-sysdmdbpageinfo-system-function-returns-page-information"></a>페이지 정보를 반환하는 새 sys.dm_db_page_info 시스템 함수

`sys.dm_db_page_info(database_id, file_id, page_id, mode)`는 데이터베이스의 페이지에 대한 정보를 반환합니다. 이 함수는 `object_id`, `index_id` 및 `partition_id`를 포함하여 페이지의 헤더 정보를 포함하는 행을 반환합니다. 이 함수를 사용하면 대부분의 경우에서 `DBCC PAGE`를 사용할 필요가 없습니다.  

페이지 관련 대기 문제를 보다 용이하게 해결하기 위해 page_resource라는 새 열도 `sys.dm_exec_requests` 및 `sys.sysprocesses`에 추가되었습니다. 이 새 열을 사용하면 또 다른 새 시스템 함수인 `sys.fn_PageResCracker`를 사용하여 `sys.dm_db_page_info`를 이러한 뷰에 조인할 수 있습니다. 다음 스크립트를 예제로 참조하세요.

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d 
  CROSS APPLY sys.fn_PageResCracker(d.page_resource) AS r
  CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id,'DETAILED')
    AS page_info;
```

## <a id="sqllinux"></a> Linux의 SQL Server

- **복제 지원**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 Linux에서 SQL Server 복제를 지원합니다. SQL 에이전트를 사용하는 Linux 가상 머신은 게시자, 배포자 또는 구독자일 수 있습니다. 

  다음 유형의 게시를 만듭니다.
  - 트랜잭션
  - 스냅숏
  - 병합

  복제 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 구성하거나 [복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)를 만듭니다.

- **MSDTC(Microsoft Distributed Transaction Coordinator) 지원**: Linux의 SQL Server 2019는 MSDTC(Microsoft Distributed Transaction Coordinator)를 지원합니다. 자세한 내용은 [Linux에서 MSDTC를 구성하는 방법](../linux/sql-server-linux-configure-msdtc.md)을 참조하세요.

- **Kubernetes를 사용하는 Docker 컨테이너의 Always On 가용성 그룹**: Kubernetes는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컨테이너를 오케스트레이션하여 SQL Server Always On 가용성 그룹이 있는 고가용성 데이터베이스 집합을 제공할 수 있습니다. Kubernetes 연산자는 **mssql-server 컨테이너** 및 상태 모니터가 있는 컨테이너를 포함하는 StatefulSet을 배포합니다.

- **타사 AD 공급자에 대한 OpenLDAP 지원**: Linux의 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 타사 공급자가 Active Directory에 가입할 수 있도록 하는 OpenLDAP를 지원합니다.

- **Linux의 Machine Learning**: 이제 Linux에서 SQL Server 2019 Machine Learning Services(데이터베이스 내)가 지원됩니다. 지원에는 `sp_execute_external_script` 저장 프로시저가 포함됩니다. Linux에서 Machine Learning Services를 설치하는 방법에 대한 지침은 [Linux에서 SQL Server 2019 Machine Learning Services R 및 Python 지원 설치](../linux/sql-server-linux-setup-machine-learning.md)를 참조하세요.

- **새 컨테이너 레지스트리**: 이제 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 뿐만 아니라 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]에 대한 모든 컨테이너 이미지가 Microsoft Container Registry에 있습니다. Microsoft Container Registry는 Microsoft 제품 컨테이너의 배포를 위한 공식 컨테이너 레지스트리입니다. 이제 인증된 RHEL 기반 이미지도 게시됩니다.

  - Microsoft Container Registry: `mcr.microsoft.com/mssql/server:vNext-CTP2.0`
  - 인증된 RHEL 기반 컨테이너 이미지: `mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0`

## <a id="mds"></a> MDS(Master Data Services)

- **HTML로 Silverlight 컨트롤이 대체됨**: MDS(Master Data Services) 포털은 더 이상 Silverlight에 의존하지 않습니다. 이전의 모든 Silverlight 구성 요소가 HTML 컨트롤로 바뀌었습니다.

## <a id="security"></a>보안

- **SQL Server 구성 관리자의 인증서 관리**: SSL/TLS 인증서는 SQL Server 인스턴스 액세스를 보호하기 위해 널리 사용됩니다. 이제 인증서 관리는 SQL Server 구성 관리자에 통합되어 다음과 같은 일반적인 작업을 간소화합니다.

  - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 설치된 인증서 보기 및 유효성 검사 
  - 만료가 가까워지는 인증서 보기
  - (주 복제본을 보유하는 노드에서) Always On 가용성 그룹에 참여하는 컴퓨터에 인증서를 배포합니다.
  - (활성 노드에서) 장애 조치(Failover) 클러스터 인스턴스에 참여하는 컴퓨터에 인증서를 배포합니다.

  > [!NOTE]
  > 사용자는 모든 클러스터 노드에서 관리자 권한이 있어야 합니다.

## <a id="tools"></a>도구

- [**Azure Data Studio**](../azure-data-studio/what-is.md): 이전에 미리 보기 이름 SQL Operations Studio로 릴리스되었던 Azure Data Studio는 데이터 개발 및 관리 측면에서 가장 일반적인 작업을 수행하기 위한 경량의 최신 오픈 소스, 플랫폼 간 데스크톱 도구입니다. Azure Data Studio를 사용하여 Windows, macOS 및 Linux에서 온-프레미스 및 클라우드의 SQL Server에 연결할 수 있습니다. Azure Data Studio를 사용하여 다음을 수행할 수 있습니다.

  - 대단히 빠른 Intellisense, 코드 조각 및 소스 제어 통합으로 최신 개발 환경에서 쿼리를 편집 및 실행합니다.  
  - 결과 집합을 차트로 만드는 기본 제공 차트 기능으로 데이터를 빠르게 시각화합니다.  
  - 사용자 지정 가능한 위젯을 사용하여 서버 및 데이터베이스에 대한 사용자 지정 대시보드를 만듭니다.  
  - 기본 제공 터미널을 사용하여 보다 광범위한 환경을 쉽게 관리합니다.  
  - Jupyter를 기반으로 하는 통합 노트 환경에서 데이터를 분석합니다.  
  - 사용자 지정 테마 및 확장을 사용하여 환경을 개선합니다.  
  - 또한 기본 제공 구독 및 리소스 브라우저를 사용하여 Azure 리소스를 탐색합니다.
  - SQL Server 빅 데이터 클러스터를 사용하는 시나리오를 지원합니다.


- [**SSMS(SQL Server Management Studio) 18.0(미리 보기)**](../ssms/sql-server-management-studio-ssms.md)

  - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 지원
  - 보안 Enclave를 사용한 Always Encrypted 지원
  - 보다 작아진 다운로드 크기
  - Visual Studio 2017 격리 셸을 기준으로 하는 새로운 방식
  - 전체 목록을 보려면 [SSMS 변경 로그](../ssms/sql-server-management-studio-changelog-ssms.md)를 참조하세요.

## <a name="other-services"></a>기타 서비스

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0은 다음 서비스의 새 기능을 제공하지 않습니다.

- SSAS([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services)
- SSIS([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)])
- SSRS([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)])

## <a name="next-steps"></a>다음 단계

- [SQL Server 2019 릴리스 정보](sql-server-ver15-release-notes.md)

- [Microsoft SQL Server 2019: 기술 백서](https://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />2018년 9월에 게시되었습니다. Windows, Linux 및 Docker 컨테이너용 Microsoft SQL Server 2019 CTP 2.0에 적용됩니다.


[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
