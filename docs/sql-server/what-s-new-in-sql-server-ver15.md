---
title: SQL Server 2019의 새로운 기능 | Microsoft Docs
ms.date: 03/27/2019
ms.prod: sql-server-2019
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4e2e29a3b473ca94ff203e99c9e4a76c803d69fc
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774608"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 새로운 기능

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 이전 릴리스를 토대로 하여 SQL Server로 구축되었으며 개발 언어, 데이터 형식, 온-프레미스 또는 클라우드, 운영 체제를 선택할 수 있는 플랫폼으로 개선되었습니다. 이 문서에서는[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 새로운 기능을 요약하고 있습니다. 첫 번째 섹션에는 최신 미리 보기 릴리스에 추가된 기능을 식별합니다. 이 문서의 다른 섹션에서는 이 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에 대해 지금까지 릴리스된 모든 기능에 대한 세부 정보를 제공합니다.

자세한 내용 및 알려진 문제에 대해서는 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 릴리스 정보](sql-server-ver15-release-notes.md)를 참조하세요.

**체험하기[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]**

- [![평가 센터에서 다운로드](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101)에서 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 다운로드하여 Windows에 설치](https://go.microsoft.com/fwlink/?LinkID=862101)합니다.
- [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md), [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 및 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)용 Linux에 설치
- [도커에서 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 실행합니다](../linux/quickstart-install-connect-docker.md).

**[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 통해 최상의 환경에 맞는 [최신 도구](#tools)를 사용해 보세요.**

## <a name="ctp-24"></a>CTP 2.4

CTP(Community Technology Preview) 2.4는 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 최신 공개 릴리스입니다. 이 릴리스에는 버그를 수정하고, 보안을 개선하고, 성능을 최적화하는 이전 CTP 릴리스의 개선 사항이 포함됩니다. 또한 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.4에서 추가되었거나 향상된 기능은 다음과 같습니다.

- [빅 데이터 클러스터](#bigdatacluster)
  - Spark에서 TensorFlow를 사용하여 딥 러닝을 실행하기 위한 GPU 지원 지침.
  - Spark 런타임을 Spark 런타임 2.4로 업그레이드합니다.
  - `INSERT INTO SELECT`가 데이터 풀을 지원합니다.
  - 외부 테이블 쿼리에 대한 `FORCE SCALEOUTEXECUTION` 및 `DISABLE SCALEOUTEXECUTION` 옵션 절.

- [데이터베이스 엔진](#databaseengine)
  - 잘림 오류 메시지는 기본적으로 테이블 및 열 이름과 잘린 값을 포함합니다. [잘림](#truncation)을 참조하세요.
  - 새 DMF `sys.dm_exec_query_plan_stats`는 대부분의 쿼리에 대해 마지막으로 알려진 실제 실행 계획과 동일한 것을 반환합니다.
  - TDE(Transparent Data Encryption) 검색 - 일시 중단 및 다시 시작.

- [SQL Server Analysis Services](#ssas)
  - 테이블 형식 모델의 다 대 다 관계.
  - 리소스 거버넌스에 대한 속성 설정.

다음 섹션에서는 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)의 이전 릴리스에 도입된 새로운 기능에 대해 설명합니다.

## <a id="bigdatacluster"></a>빅 데이터 클러스터

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] [빅 데이터 클러스터](../big-data-cluster/big-data-cluster-overview.md)는 다음을 비롯한 새로운 시나리오를 지원합니다.

- [Spark에서 TensorFlow를 사용하여 딥 러닝을 실행하기 위한 GPU 지원](../big-data-cluster/spark-gpu-tensorflow.md). (CTP 2.4)
- Spark 런타임을 Spark 런타임 2.4로 업그레이드합니다. (CTP 2.4)
- `INSERT INTO SELECT`가 데이터 풀을 지원합니다.
- 외부 테이블 쿼리에 대한 `FORCE SCALEOUTEXECUTION` 및 `DISABLE SCALEOUTEXECUTION` 옵션 절.
- [IntelliJ의 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 빅 데이터 클러스터에 Spark 작업을 제출합니다](../big-data-cluster/spark-submit-job-intellij-tool-plugin.md). (CTP 2.3)
- R 및 Python을 통한 기계 학습 모델 운영, SSIS(SQL Server Integration Services) 작업 실행 등 다양한 데이터 관련 앱에 대한 [애플리케이션 배포 및 관리 환경](../big-data-cluster/big-data-cluster-create-apps.md). (CTP 2.3)
- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 빅 데이터 클러스터에서 Sparklyr 사용](../big-data-cluster/sparklyr-from-RStudio.md). (CTP 2.3)
- [HDFS 계층화](../big-data-cluster/hdfs-tiering.md)를 통해 빅 데이터 클러스터에 외장 HDFS 호환 스토리지를 탑재합니다. (CTP 2.3)
- 빅 데이터 클러스터에 대해 Azure Data Studio의 SparkR 사용 (CTP 2.2)
- [Python 및 R 앱 배포](../big-data-cluster/big-data-cluster-create-apps.md) (CTP 2.2)
- Kubernetes에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 Spark Linux 컨테이너를 사용하여 빅 데이터 클러스터를 배포합니다. (CTP 2.0)
- HDFS에서 빅 데이터에 액세스합니다. (CTP 2.0)
- Spark를 사용하여 고급 분석 및 기계 학습을 실행합니다. (CTP 2.0)
- Spark 스트리밍을 사용하여 SQL 데이터 풀에 데이터를 스트리밍합니다. (CTP 2.0)
- [**Azure Data Studio**](../sql-operations-studio/what-is.md)에서 노트 환경을 제공하는 쿼리 책 실행 (CTP 2.0)
 
[!INCLUDE [Big data clusters preview](../includes/big-data-cluster-preview-note.md)]

## <a id="databaseengine"></a> 데이터베이스 엔진

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 다음과 같은 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 새로운 기능을 도입하거나 향상된 기능을 제공합니다.

### <a name="new-querypostexecutionplanprofile-extended-event-ctp-24"></a>새 query_post_execution_plan_profile 확장 이벤트(CTP 2.4)

새 `query_post_execution_plan_profile` 확장 이벤트는 표준 프로파일링을 사용하는 `query_post_execution_showplan`과 달리 경량 프로파일링에 기반한 실제 계획과 동등한 것을 수집합니다. 자세한 내용은 [쿼리 프로파일링 인프라](../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요.

#### <a name="example-1---extended-event-session-using-standard-profiling"></a>예제 1 - 표준 프로파일링을 사용한 확장 이벤트 세션

```sql
CREATE EVENT SESSION [QueryPlanOld] ON SERVER 
ADD EVENT sqlserver.query_post_execution_showplan(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename = N'C:\Temp\QueryPlanStd.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

#### <a name="example-2---extended-event-session-using-lightweight-profiling"></a>예제 2 - 경량 프로파일링을 사용한 확장 이벤트 세션

```sql
CREATE EVENT SESSION [QueryPlanLWP] ON SERVER 
ADD EVENT sqlserver.query_post_execution_plan_profile(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename=N'C:\Temp\QueryPlanLWP.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

### <a name="new-dmf-sysdmexecqueryplanstats-ctp-24"></a>새 DMF sys.dm_exec_query_plan_stats(CTP 2.4) 

새 DMF `sys.dm_exec_query_plan_stats`는 경량 프로파일링을 기반으로 대부분의 쿼리에 대해 마지막으로 알려진 실제 실행 계획과 동일한 것을 반환합니다. 자세한 내용은 [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md) 및 [프로파일링 인프라 쿼리](../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요. 다음 스크립트를 예제로 참조하세요.

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

이는 옵트인 기능이며 [추적 플래그](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451을 사용하도록 설정해야 합니다.

### <a name="transparent-data-encryption-tde-scan---suspend-and-resume-ctp-24"></a>TDE(Transparent Data Encryption) 검색 - 일시 중단 및 다시 시작(CTP 2.4)

데이터베이스에서 [TDE(Transparent Data Encryption)](../relational-databases/security/encryption/transparent-data-encryption.md)를 사용하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 데이터 파일에서 버퍼 풀로 각 페이지를 읽은 다음, 암호화된 페이지를 다시 작성하는 암호화 검사를 수행해야 합니다. 사용자에게 암호화 검사에 대한 추가 제어 권한을 제공하기 위해 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 TDE 검사(일시 중단 및 다시 시작 구문)를 도입하여 시스템의 워크로드가 많거나 업무상 중요한 시간 동안 검색을 일시 중지한 다음, 나중에 검사를 다시 시작하도록 합니다.

TDE 암호화 검사를 일시 중지하려면 다음 구문을 사용합니다.

```sql
ALTER DATABASE <db_name> SET ENCRYPTION SUSPEND;
```

마찬가지로, 다음 구문은 TDE 암호화 검사를 다시 시작합니다.

```sql
ALTER DATABASE <db_name> SET ENCRYPTION RESUME;
```

암호화 검사의 현재 상태를 표시하기 위해 `sys.dm_database_encryption_keys` 동적 관리 뷰에 `encryption_scan_state`가 추가되었습니다. 마지막 암호화 검사 상태 변경 날짜와 시간을 포함하는 `encryption_scan_modify_date`라는 새 열도 있습니다. 또한 암호화 검사가 일시 중단된 상태에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 다시 시작하면 일시 중지된 기존 검사가 있음을 나타내는 메시지가 시작 시 오류 로그에 기록됩니다.

### <a name="accelerated-database-recovery-ctp-23"></a>가속 데이터베이스 복구(CTP 2.3)

[가속 데이터베이스 복구](/azure/sql-database/sql-database-accelerated-database-recovery/)는 특히 장기 실행 트랜잭션이 있는 경우 SQL Server 데이터베이스 엔진 복구 프로세스를 다시 설계하여 데이터베이스 가용성을 크게 향상시킵니다. [데이터베이스 복구](../relational-databases/logs/the-transaction-log-sql-server.md?#recovery-of-all-incomplete-transactions-when--is-started)는 SQL Server에서 각 데이터베이스에 대해 트랜잭션 측면에서 일관되거나 깨끗한 상태에서 시작하는 데 사용하는 프로세스입니다. 가속 데이터베이스 복구를 사용하도록 설정된 데이터베이스는 장애 조치 또는 정리되지 않은 다른 종료 후에 복구를 훨씬 더 빨리 수행합니다. CTP 2.3부터 다음 구문을 사용하여 데이터베이스별로 가속 데이터베이스 복구를 사용하도록 설정할 수 있습니다.

```sql
ALTER DATABASE <db_name> SET ACCELERATED_DATABASE_RECOVERY = {ON | OFF}
```

> [!NOTE]
> [공개 미리 보기 도중 요청에 따라 이 기능이 기본적으로 설정되어 있는](/azure/sql-database/sql-database-accelerated-database-recovery#to-enable-adr-during-this-preview-period) Azure SQL DB에서는 이 구문을 이용할 필요가 없습니다. 사용하도록 설정한 후 기능이 기본적으로 사용하도록 설정됩니다.

대규모 트랜잭션이 발생할 수 있는 중요한 데이터베이스가 있는 경우 미리 보기 동안에 이 기능을 실험해 보세요. 그리고 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 팀 ](<https://aka.ms/sqlfeedback>)에 피드백도 제공해 주세요.

### <a name="query-store-plan-forcing-support-for-fast-forward-and-static-cursors-ctp-23"></a>쿼리 저장소 계획에서 빠른 전달 및 정적 커서에 대한 강제 적용 지원(CTP 2.3)

쿼리 저장소는 이제 빠른 전달과 정적 T-SQL 및 API 커서에 대한 쿼리 실행 계획을 강제로 적용하는 기능을 지원합니다. 강제 적용은 이제 `sp_query_store_force_plan` 또는 SQL Server Management Studio 쿼리 저장소 보고서를 통해 지원됩니다.

### <a name="reduced-recompilations-for-workloads-using-temporary-tables-across-multiple-scopes-ctp-23"></a>여러 범위에서 임시 테이블을 사용하여 워크로드에 대한 재컴파일 감소(CTP 2.3)

이 기능을 사용하기 전에 DML(데이터 조작 언어) 문(`SELECT`, `INSERT`, `UPDATE`, `DELETE`)을 사용하여 임시 테이블을 참조할 때 임시 테이블이 외부 범위 일괄 처리에서 만들어지면 DML 문이 실행될 때마다 다시 컴파일됩니다. 이 향상된 기능을 사용하면 SQL Server에서 불필요한 재컴파일을 방지하기 위해 다음과 같은 간단한 검사를 추가로 수행합니다.

- 컴파일 시간에 임시 테이블을 만드는 데 사용되는 외부 범위 모듈이 연속 실행에 사용되는 것과 동일한지 확인합니다. 
- 초기 컴파일에서 변경된 DDL(데이터 정의 언어)을 추적하고 이를 연속 실행에 대한 DDL 작업과 비교합니다. 

결과적으로 불필요한 재컴파일 및 CPU 오버헤드가 감소합니다.

### <a name="improved-indirect-checkpoint-scalability-ctp-23"></a>향상된 간접 검사점 확장성(CTP 2.3)

이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 tempdb와 같이 많은 수의 더티 페이지를 생성하는 데이터베이스가 있는 경우 사용자에게 생성되지 않은 스케줄러 오류가 발생할 수 있습니다. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 간접 검사점에 대해 향상된 확장성을 도입하여 UPDATE/INSERT 워크로드가 많은 데이터베이스에서 이러한 오류를 방지할 수 있습니다.

### <a name="utf-8-support-ctp-23"></a>UTF-8 지원(CTP 2.3)

가져오기 또는 내보내기 인코딩이나 텍스트 데이터의 데이터베이스 수준 또는 열 수준 데이터 정렬로 널리 사용되는 UTF-8 문자 인코딩이 완전히 지원됩니다. UTF-8은 `CHAR` 및 `VARCHAR` 데이터 형식에서 허용되며, `UTF8` 접미사를 사용하여 개체의 데이터 정렬을 만들거나 이 접미사를 갖는 데이터 정렬로 변경하여 설정합니다. 

예를 들어 `LATIN1_GENERAL_100_CI_AS_SC`에서 `LATIN1_GENERAL_100_CI_AS_SC_UTF8`로 변경합니다. UTF-8은 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에 제공된 보충 문자를 지원하는 Windows 데이터 정렬에서만 사용할 수 있습니다. `NCHAR` 및 `NVARCHAR`는 UTF-16 인코딩만 허용하며 변경되지 않고 유지됩니다.

이 기능은 사용 중인 문자 집합에 따라 스토리지 비용을 크게 절감하는 효과를 제공할 수 있습니다. 예를 들어 UTF-8 사용 데이터 정렬을 통해 ASCII(Latin) 문자열이 있는 기존 열 데이터 유형을 `NCHAR(10)`에서 `CHAR(10)`으로 변경하면 스토리지 요구 사항이 50% 감소합니다. 이러한 감소는 `NCHAR(10)`에는 스토리지로 20바이트가 필요하지만 `CHAR(10)`에는 동일한 유니코드 문자열에 대해 10바이트만 필요하기 때문입니다.

자세한 내용은 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.

**CTP 2.1** [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]설정 중 UTF-8 데이터 정렬을 기본값으로 선택하도록 지원을 추가했습니다.

**CTP 2.2** SQL Server 복제에서 UTF-8 문자 인코딩을 사용하도록 지원을 추가했습니다.

**CTP 2.3** BIN2 데이터 정렬(UTF8_BIN2)로 UTF-8 문자 인코딩을 사용하도록 지원을 추가했습니다.

### <a name="scalar-udf-inlining-ctp-21"></a>스칼라 UDF 인라인 처리(CTP 2.1)

스칼라 UDF 인라인 처리는 자동으로 스칼라 UDF(사용자 정의 함수)를 관계식으로 변환하고 호출 SQL 쿼리에 포함하여 스칼라 UDF를 활용하는 작업의 성능을 향상합니다. 스칼라 UDF 인라인 처리는 UDF 내에서 작업의 비용 기반 최적화를 용이하게 하고 비효율적이고 반복적인 직렬 실행 계획 대신 효율적인 집합 지향 병렬 계획을 가능하게 합니다. 이 기능은 데이터베이스 호환성 수준 150에서 기본적으로 사용하도록 설정됩니다.

자세한 내용은 [스칼라 UDF 인라인 처리](../relational-databases/user-defined-functions/scalar-udf-inlining.md)를 참조하세요.

### <a name="a-nametruncation-truncation-error-message-improved-to-include-table-and-column-names-and-truncated-value-ctp-21"></a><a name="truncation" />테이블 및 열 이름과 잘린 값을 포함하도록 잘림 오류 메시지 개선(CTP 2.1)

오류 메시지 ID 8152 `String or binary data would be truncated`는 데이터 이동 작업을 개발 및 유지 관리하는 많은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개발자와 관리자에게 익숙합니다. 이 오류는 다른 스키마를 사용하여 원본과 대상 사이에 데이터를 전송하는 동안 원본 데이터가 너무 커서 대상 데이터 형식에 맞지 않을 때 발생합니다. 이 오류 메시지는 문제를 해결하는 데 시간이 오래 걸릴 수 있습니다. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 이 시나리오에 대해 보다 구체적인 새 오류 메시지(2628)를 제공합니다.  

`String or binary data would be truncated in table '%.*ls', column '%.*ls'. Truncated value: '%.*ls'.`

새 오류 메시지 2628은 데이터 잘림 문제에 대한 자세한 컨텍스트를 제공하여 문제 해결 프로세스를 간소화합니다. 

**CTP 2.1 및 CTP 2.2** 이는 옵트인 오류 메시지이며 [추적 플래그](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460을 사용하도록 설정해야 합니다.

**CTP 2.4** 오류 메시지 2628이 기본 잘림 메시지가 되고 데이터베이스 호환성 수준 150에서 오류 메시지 8152를 대체합니다. 데이터베이스 호환성 수준이 150일 때 오류 메시지 2628과 8152 사이에서 전환하기 위해 새 데이터베이스 범위 구성 `VERBOSE_TRUNCATION_WARNINGS`가 도입되었습니다. 자세한 내용은 [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 참조하세요.
데이터베이스 호환성 수준 140 이하의 경우 오류 메시지 2628은 [추적 플래그](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460을 사용하도록 설정해야 하는 옵트인 오류 메지시로 남아 있습니다.

### <a name="improved-diagnostic-data-for-stats-blocking-ctp-21"></a>통계 차단에 대한 진단 데이터 개선(CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 동기 통계 업데이트 작업을 대기하는 장기 실행 쿼리를 위한 향상된 진단 데이터를 제공합니다. `SELECT`가 쿼리 실행을 계속하기 전에 동기 통계 업데이트 작업이 완료되도록 기다리고 있는 경우 동적 관리 뷰 `sys.dm_exec_requests` 열 `command`에서는 `SELECT (STATMAN)`가 나타납니다. 또한 새로운 대기 유형 `WAIT_ON_SYNC_STATISTICS_REFRESH`가 `sys.dm_os_wait_stats` 동적 관리 뷰에 표시됩니다. 동기 통계 새로 고침 작업에 소요된 누적된 인스턴스 수준 시간을 보여 줍니다.

### <a name="hybrid-buffer-pool-ctp-21"></a>하이브리드 버퍼 풀(CTP 2.1)

하이브리드 버퍼 풀은 SQL Server 데이터베이스 엔진의 새로운 기능입니다. 영구 메모리(PMEM) 디바이스의 데이터베이스 파일에 있는 데이터베이스 페이지를 필요 시 곧바로 액세스합니다. PMEM 디바이스는 데이터 액세스 시 대기 시간이 매우 짧기 때문에 엔진은 버퍼 풀의 "클린 페이지" 영역에 데이터 복사본을 만들지 않고 간단히 PMEM에서 직접 페이지에 액세스할 수 있습니다. 향상 기능의 경우처럼 메모리 매핑된 I/O를 사용하여 액세스가 이루어집니다. 따라서 DRAM에 페이지를 복사하지 않고 운영 체제의 I/O 스택에서 영구 스토리지의 페이지에 액세스하지 않으므로 성능상의 이점을 제공합니다. 이 기능은 Windows의 SQL Server와 Linux의 SQL Server에서 모두 사용할 수 있습니다.

자세한 내용은 [하이브리드 버퍼 풀](../database-engine/configure-windows/hybrid-buffer-pool.md)을 참조하세요.

### <a name="static-data-masking-ctp-21"></a>정적 데이터 마스킹(CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 정적 데이터 마스킹을 제공합니다. SQL Server 데이터베이스의 복사본에서 중요한 데이터를 삭제하는 정적 마스킹 데이터를 사용할 수 있습니다. 모든 중요한 정보가 프로덕션 외의 사용자와 복사본을 공유할 수 있는 방식으로 변경된 경우 정적 데이터 마스킹을 사용하면 정화된 데이터베이스 복사본을 만들 수 있습니다. 정적 데이터 마스킹은 개발, 테스트, 분석 및 비즈니스 보고, 규정 준수, 문제 해결 및 특정 데이터를 다른 환경에 복사할 수 없는 기타 시나리오에 사용할 수 있습니다.

정적 데이터 마스킹은 열 수준에서 작동합니다. 마스크할 열을 선택하고 선택한 각 열에 대해 마스킹 함수를 지정합니다. 정적 데이터 마스킹이 데이터베이스를 복사한 후 지정한 마스킹 함수를 열에 적용합니다.

#### <a name="static-data-masking-vs-dynamic-data-masking"></a>정적 데이터 마스킹 및 동적 데이터 마스킹

데이터 마스킹은 중요한 정보를 숨기기 위해 데이터베이스에 마스크를 적용하고 새 데이터나 삭제된 데이터로 대체하는 프로세스입니다. Microsoft는 정적 데이터 마스킹 및 동적 데이터 마스킹의 두 가지 마스킹 옵션을 제공합니다. 동적 데이터 마스킹은 [!INCLUDE[ssSQL16](../includes/sssql16-md.md)]에서 제공되었습니다. 다음 표에서는 이러한 두 솔루션을 비교합니다.

|정적 데이터 마스킹 |동적 데이터 마스킹|
|:----|:----|
|데이터베이스 복사본에서 발생 <br/><br/>원본 데이터를 검색할 수 없음<br/><br/>마스크는 스토리지 수준에서 발생<br/><br/>모든 사용자가 동일한 마스크된 데이터에 액세스할 수 있음<br/><br/>지속적인 팀 전체 액세스를 위해 설계|원본 데이터베이스에서 발생<br/><br/>원본 데이터가 그대로 유지됨<br/><br/>마스크는 쿼리 시 즉석에서 발생<br/><br/>마스크는 사용자 권한에 따라 다름 <br/><br/>정확한 시간에 사용자 특정 액세스를 위해 설계|

### <a name="database-compatibility-level-ctp-20"></a>데이터베이스 호환성 수준(CTP 2.0)

데이터베이스 **COMPATIBILITY_LEVEL 150**이 추가되었습니다. 특정 사용자 데이터베이스를 사용하려면 다음을 실행합니다.

   ```sql
   ALTER DATABASE database_name SET COMPATIBILITY_LEVEL =  150;
   ```

### <a name="resumable-online-index-create-ctp-20"></a>다시 시작 가능한 온라인 인덱스 만들기(CTP 2.0)

**다시 시작 가능한 온라인 인덱스 만들기**를 사용하면 인덱스 만들기 작업을 일시 중지한 후 처음부터 다시 시작하지 않고, 작업이 일시 중지되었거나 실패한 지점부터 다시 시작할 수 있습니다.

다시 시작 가능한 온라인 인덱스 만들기는 다음 시나리오를 지원합니다.
- 인덱스 만들기 실패 후[예: 데이터베이스 장애 조치(Failover) 이후 또는 디스크 공간이 부족해진 이후] 인덱스 만들기 작업을 다시 시작합니다.
- 진행 중인 인덱스 만들기 작업을 일시 중지하여 필요할 때 시스템 리소스를 일시적으로 사용 가능하게 만들고 나중에 이 작업을 다시 시작합니다.
- 많은 로그 공간과 장기 실행 트랜잭션을 사용하여 다른 유지 관리 작업을 차단하거나 로그 잘림을 허용하지 않으면서 큰 인덱스를 만듭니다.

인덱스 만들기가 실패하는 경우 이 기능을 사용하지 않고 온라인 인덱스 만들기 작업을 다시 실행해야 하며 작업을 처음부터 다시 시작해야 합니다.

이 릴리스에서는 다시 시작 가능한 기능을 확장하여 사용 가능한 [다시 시작 가능한 온라인 인덱스 다시 작성](http://azure.microsoft.com/blog/modernize-index-maintenance-with-resumable-online-index-rebuild/)에 이 기능을 추가합니다.

또한 [온라인 및 다시 시작 가능한 DDL 작업의 데이터베이스 범위 기본 설정](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 사용하여 이 기능을 특정 데이터베이스의 기본값으로 설정할 수 있습니다.

자세한 내용은 [다시 시작 가능한 온라인 인덱스 만들기](../t-sql/statements/create-index-transact-sql.md#resumable-indexes)를 참조하세요.

### <a name="build-and-rebuild-clustered-columnstore-indexes-online-ctp-20"></a>온라인으로 클러스터형 columnstore 인덱스 작성 및 다시 작성(CTP 2.0)

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

### <a name="always-encrypted-with-secure-enclaves-ctp-20"></a>보안 Enclave를 사용한 Always Encrypted(CTP 2.0)

바로 암호화 및 리치 계산으로 Always Encrypted를 확장합니다. 확장은 서버 쪽의 보안 Enclave 내에서 일반 텍스트 데이터에 대해 계산을 사용하도록 설정하여 제공됩니다.

암호화 작업에는 열 암호화 및 열 암호화 키 순환이 포함됩니다. 이제 이러한 작업은 [!INCLUDE[tsql](../includes/tsql-md.md)]를 사용하여 실행할 수 있으며 데이터를 데이터베이스 밖으로 이동할 필요가 없습니다. 보안 Enclave는 다음과 같은 요구 사항을 갖는 보다 광범위한 시나리오에 Always Encrypted를 제공합니다.  

- 데이터베이스 관리자, 시스템 관리자, 클라우드 운영자 또는 맬웨어를 포함하여 높은 권한을 갖지만 아직 허가되지 않은 사용자로부터 중요한 데이터를 보호해야 합니다.
- 데이터베이스 시스템 내에서 보호된 데이터에 대한 리치 계산을 지원해야 합니다.

자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.

> [!NOTE]
> 보안 Enclave를 사용한 Always Encrypted는 Windows OS에서만 사용할 수 있습니다.

### <a name="intelligent-query-processing-ctp-20"></a>지능형 쿼리 처리(CTP 2.0)

- **행 모드 메모리 부여 피드백**은 일괄 처리 및 행 모드 연산자의 메모리 부여 크기를 둘 다 조정하여 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]에 도입된 메모리 부여 피드백 기능을 확장합니다. 과도한 메모리 부여 조건의 경우 부여된 메모리가 실제로 사용된 메모리 크기의 두 배를 초과하면 메모리 부여 피드백이 메모리 부여를 다시 계산합니다. 그런 이후에는 연속 실행에 더 적은 메모리가 요구됩니다. 크기가 부족한 메모리 부여의 경우 디스크로 분산이 발생하며 메모리 부여 피드백이 메모리 부여 다시 계산을 트리거합니다. 그런 이후에는 연속 실행에 더 많은 메모리가 요구됩니다. 이 기능은 데이터베이스 호환성 수준 150에서 기본적으로 사용하도록 설정됩니다.

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
      - 그렇지 않더라도 애플리케이션이 columnstore 인덱스에서 아직 지원되지 않는 기능에 의존하기 때문에 실현 가능하지 않습니다.

- **테이블 변수 지연 컴파일**은 테이블 변수를 참조하는 쿼리의 플랜 품질 및 전체 성능을 개선합니다. 최적화 및 초기 컴파일 중에 이 기능은 실제 테이블 변수 행 수를 기반으로 하는 카디널리티 예측을 전파합니다. 이 정확한 행 수 정보는 다운스트림 계획 작업을 최적화하는 데 사용됩니다. 이 기능은 데이터베이스 호환성 수준 150에서 기본적으로 사용하도록 설정됩니다.

지능형 쿼리 처리 기능을 사용하려면 데이터베이스 `COMPATIBILITY_LEVEL = 150`을 설정합니다.

### <a id="programmability"></a> Java 언어 프로그래밍 기능 확장(CTP 2.0)

- **Java 언어 확장(미리 보기)**: Java 언어 확장을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 Java 코드를 실행합니다. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서 이 확장은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 'Machine Learning Services(데이터베이스 내)' 기능을 추가할 때 설치됩니다.

### <a id="sqlgraph"></a> SQL 그래프 기능(CTP 2.3)

- **그래프 일치 쿼리에서 파생 테이블 또는 보기 별칭 사용(CTP 2.1)** [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 미리 보기의 그래프 쿼리는 `MATCH` 구문에서 보기 및 파생 테이블 별칭을 사용할 수 있도록 지원합니다. 이러한 별칭을 `MATCH`에서 사용하려면 `UNION ALL` 연산자를 사용하여 노드 집합 또는 에지 테이블 집합에 대해 뷰 및 파생 테이블을 만들어야 합니다. 노드 또는 에지 테이블에는 필터가 있거나 없을 수 있습니다. `MATCH` 쿼리에서 파생 테이블과 뷰 별칭을 사용하는 기능은 그래프의 두 개 이상의 엔터티 간에 다른 유형의 엔터티 또는 다른 유형의 연결을 쿼리하려는 시나리오에서 매우 유용할 수 있습니다.

- **`MERGE` DML의 일치 지원(CTP 2.0)** 을 통해 그래프 관계를 별도의 `INSERT`, `UPDATE` 또는 `DELETE` 문이 아닌 단일 문에 지정할 수 있습니다. `MERGE` 문에 `MATCH` 조건자를 사용하여 노드 또는 에지 테이블의 현재 그래프 데이터를 새 데이터와 병합합니다. 이 기능을 통해 에지 테이블의 `UPSERT` 시나리오가 지원됩니다. 이제 단일 병합 문을 사용하여 두 노드 간에 새 에지를 삽입하거나 기존 에지를 업데이트할 수 있습니다.

- **Edge 제약 조건(CTP 2.0)** 은 SQL 그래프의 에지 테이블을 위해 도입되었습니다. 에지 테이블은 임의 노드를 데이터베이스의 다른 노드에 연결할 수 있습니다. 에지 제약 조건의 도입으로, 이제 이러한 동작을 어느 정도 제한할 수 있습니다. 새 `CONNECTION` 제약 조건을 사용하여 지정된 에지 테이블이 스키마에서 연결하도록 허용되는 노드 유형을 지정할 수 있습니다. 

  **(CTP 2.3)** 이 기능을 더 확장하면 에지 제약 조건에서 계단식 삭제 작업을 정의할 수 있습니다. 사용자가 특정 에지가 연결되는 노드를 삭제할 때 데이터베이스 엔진에서 수행하는 작업을 정의할 수 있습니다.

### <a name="database-scoped-default-setting-for-online-and-resumable-ddl-operations-ctp-20"></a>온라인 및 다시 시작 가능한 DDL 작업에 대한 데이터베이스 범위 기본 설정(CTP 2.0)

- **온라인 및 다시 시작 가능한 DDL 작업에 대한 데이터베이스 범위 기본 설정**을 사용하여 인덱스 만들기 또는 다시 작성과 같은 개별 인덱스 DDL 문에 대해 이러한 옵션을 정의하지 않고, 데이터베이스 수준에서 `ONLINE` 및 `RESUMABLE` 인덱스 작업에 대한 기본 동작 설정 지정할 수 있습니다.

- `ELEVATE_ONLINE` 및 `ELEVATE_RESUMABLE` 데이터베이스 범위 구성 옵션을 사용하여 이러한 기본값을 설정합니다. 두 옵션 모두 엔진이 지원되는 작업의 권한을 자동으로 온라인 또는 다시 시작이 가능 인덱스 실행으로 상승시키도록 합니다. 이러한 옵션을 사용하여 다음 동작을 사용하도록 설정할 수 있습니다.

  - `FAIL_UNSUPPORTED` 옵션을 사용하면 온라인 또는 다시 시작 가능한 모든 인덱스 작업을 허용하고 온라인 또는 다시 시작 가능 방식이 지원되지 않는 인덱스 작업을 실패하도록 할 수 있습니다.
  - `WHEN_SUPPPORTED` 옵션을 사용하면 온라인 또는 다시 시작 가능한 지원되는 작업을 허용하고 지원되지 않는 인덱스 작업을 오프라인 또는 다시 시작 불가능 방식으로 실행할 수 있습니다.
  - `OFF` 옵션을 사용하면 DDL 문에 명시적으로 지정되지 않는 한, 모든 인덱스 작업을 오프라인 및 다시 시작 불가능 방식으로 실행하는 현재 동작이 허용됩니다.

기본 설정을 재정의하려면 인덱스 만들기 및 다시 작성 명령에 `ONLINE` 또는 `RESUMABLE` 가능 옵션을 포함합니다. 

이 기능이 없으면 인덱스 만들기 및 다시 작성과 같은 인덱스 DDL 문에서 온라인 및 다시 시작 가능 옵션을 직접 지정해야 합니다.

인덱스 다시 시작 가능 작업에 대한 자세한 내용은 [다시 시작 가능한 온라인 인덱스 만들기](https://azure.microsoft.com/blog/resumable-online-index-create-is-in-public-preview-for-azure-sql-db/)를 참조하세요.

### <a id="ha"></a>Always On 가용성 그룹 - 추가 동기 복제본(CTP 2.0)

- **최대 5개의 동기 복제본**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 동기 복제본의 최대 수가 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 3개에서 5개로 증가되었습니다. 그룹 내에서 자동 장애 조치가 수행되도록 이 그룹을 5개 복제본으로 구성할 수 있습니다. 여기에는 하나의 주 복제본 및 4개의 동기 보조 복제본이 있습니다.

- **보조-주 복제본 연결 리디렉션**: 이 기능은 연결 문자열에 지정된 대상 서버에 관계없이 클라이언트 애플리케이션 연결이 주 복제본으로 전송되도록 합니다. 이 기능에서는 수신기 없는 연결 리디렉션이 허용됩니다. 다음과 같은 경우 보조-주 복제본 연결 리디렉션을 사용합니다.

  - 클러스터 기술이 수신기 기능을 제공하지 않습니다.
  - 리디렉션이 복잡한 다중 서브넷 구성을 사용하고 있습니다.
  - 클러스터 유형이 `NONE`인 읽기 스케일 아웃 또는 재해 복구 시나리오입니다.

자세한 내용은 [보조-주 복제본 읽기/쓰기 연결 리디렉션(Always On 가용성 그룹)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)을 참조하세요.

### <a name="data-discovery-and-classification-ctp-20"></a>데이터 검색 및 분류(CTP 2.0)

데이터 검색 및 분류는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기본적으로 제공된 고급 기능을 제공합니다. 가장 중요한 데이터를 분류하고 레이블을 지정하면 다음과 같은 이점을 얻을 수 있습니다.
- 데이터 프라이버시 표준 및 규정 준수 요구 사항을 충족할 수 있습니다.
- 중요한 데이터에 대한 비정상적인 액세스 모니터링(감사) 및 경고 등의 보안 시나리오를 지원합니다.
- 엔터프라이즈에서 중요한 데이터가 있는 위치를 보다 쉽게 파악하여 관리자가 데이터베이스를 보호하기 위한 적절한 단계를 수행할 수 있습니다.

자세한 내용은 [SQL 데이터 검색 및 분류](../relational-databases/security/sql-data-discovery-and-classification.md)를 참조하세요.

또한 [감사](../relational-databases/security/auditing/sql-server-audit-database-engine.md) 기능도 감사 로그에 `data_sensitivity_information`라는 새 필드를 포함하도록 개선되었습니다. 이 필드는 쿼리가 반환한 실제 데이터의 민감도 분류(레이블)를 기록합니다. 자세한 내용과 예제를 보려면 [민감도 분류 추가](../t-sql/statements/add-sensitivity-classification-transact-sql.md)를 참조하세요.

>[!NOTE]
>감사를 사용하도록 설정하는 방법은 변경되지 않았습니다. 감사 레코드에는 `data_sensitivity_information`라는 새 필드가 있습니다. 이 필드는 쿼리가 반환한 실제 데이터의 민감도 분류(레이블)를 기록합니다. [중요한 데이터에 대한 액세스 감사](/azure/sql-database/sql-database-data-discovery-and-classification/#subheading-3)를 참조하세요.

### <a name="expanded-support-for-persistent-memory-devices-ctp-20"></a>영구 메모리 디바이스에 대한 확장 지원(CTP 2.0)

이제 영구 메모리 디바이스에 배치되는 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 파일은 *지원* 모드로 작동될 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 효율적인 memcpy 작업을 사용하여 운영 체제 스토리지 스택을 우회하고 장치에 직접 액세스합니다. 이 모드는 이러한 디바이스에 대해 낮은 대기 시간의 입/출력을 허용하므로 성능을 향상시킵니다.
    - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 파일의 예에는 다음이 포함됩니다.
        - 데이터베이스 파일
        - 트랜잭션 로그 파일
        - 메모리 내 OLTP 검사점 파일
    - 영구 메모리를 스토리지 클래스 메모리라고도 합니다.
    - Microsoft 이외의 일부 웹 사이트에서는 경우에 따라 영구 메모리를 비공식적으로 *pmem*이라고도 합니다.

> [!NOTE]
> 이 미리 보기 릴리스에는 영구 메모리 디바이스의 파일을 Linux에서만 사용할 수 있습니다. Windows의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]부터 영구 메모리 디바이스를 지원합니다.

### <a name="support-for-columnstore-statistics-in-dbcc-clonedatabase-ctp-20"></a>DBCC CLONEDATABASE에서 Columnstore 통계 지원(CTP 2.0)

`DBCC CLONEDATABASE`는 데이터를 복사하지 않고 쿼리 성능 문제를 해결하는 데 필요한 모든 요소가 포함된 데이터베이스의 스키마 전용 복사본을 만듭니다. 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 이 명령은 columnstore 인덱스 쿼리 문제를 정확히 해결하는 데 필요한 통계를 복사하지 않으므로 수동 단계를 통해 이 정보를 캡처해야 했습니다. 이제 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서 `DBCC CLONEDATABASE`는 columnstore 인덱스에 대한 통계 Blob을 자동으로 캡처하므로 수동 단계가 필요하지 않습니다.

### <a name="new-options-added-to-spestimatedatacompressionsavings-ctp-20"></a>sp_estimate_data_compression_savings에 새로 추가된 옵션(CTP 2.0)

`sp_estimate_data_compression_savings`는 요청된 개체의 현재 크기를 반환하고 요청된 압축 상태에 대한 개체 크기를 예상합니다. 현재 이 프로시저는 `NONE`, `ROW` 및 `PAGE`의 세 가지 옵션을 지원합니다. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 `COLUMNSTORE` 및 `COLUMNSTORE_ARCHIVE`라는 두 가지 새 옵션을 제공합니다. 이러한 새 옵션을 사용하면 표준 또는 보관 columnstore 압축을 사용하여 테이블에서 columnstore 인덱스를 만들 경우의 예상되는 공간 절약을 추정할 수 있습니다.

### <a id="ml"></a> SQL Server Machine Learning Services 장애 조치(Failover) 클러스터 및 파티션 기반 모델링(CTP 2.0)

- **파티션 기반 모델링**: `sp_execute_external_script`에 추가된 새 매개 변수를 사용하여 데이터 파티션별로 외부 스크립트를 처리합니다. 이 기능은 하나의 큰 모델 대신, 많은 작은 모델(데이터 파티션당 하나의 모델)을 학습하도록 지원합니다.

- **Windows Server 장애 조치(Failover) 클러스터**: Windows Server 장애 조치(Failover) 클러스터에서 Machine Learning 서비스의 고가용성을 구성합니다.

자세한 내용은 [SQL Server Machine Learning Services의 새로운 기능](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)을 참조하세요.

### <a name="lightweight-query-profiling-infrastructure-enabled-by-default-ctp-20"></a>간단한 쿼리 프로파일링 인프라가 기본적으로 사용 가능(CTP 2.0)

LWP(간단한 쿼리 프로파일링 인프라)는 표준 프로파일링 매커니즘보다 더 효율적으로 쿼리 성능 데이터를 제공합니다. 간단한 프로파일링은 이제 기본적으로 사용되도록 설정됩니다. 이 기능은 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1에 도입되었습니다. 간단한 프로파일링은 표준 쿼리 프로파일링 메커니즘의 최대 75% CPU 오버헤드와 비교할 때 2% CPU 오버헤드가 예상되는 쿼리 실행 통계 수집 메커니즘을 제공합니다. 이전 버전에서 이 기능은 기본적으로 해제되었습니다. 데이터베이스 관리자는 [추적 플래그 7412](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 사용하여 이 기능을 사용하도록 설정할 수 있습니다. 

간단한 프로파일링에 대한 자세한 내용은 [쿼리 프로파일링 인프라](../relational-databases/performance/query-profiling-infrastructure.md)를 참조하세요.

**CTP 2.3** 새 데이터베이스 범위 구성 `LIGHTWEIGHT_QUERY_PROFILING`은 경량 쿼리 프로파일링 인프라를 활성화 또는 비활성화하기 위해 도입되었습니다.

### <a id="polybase"></a>새 PolyBase 커넥터

- **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata 및 MongoDB**용 새 커넥터: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata 및 MongoDB용 외부 데이터에 대한 새 커넥터를 도입했습니다.

### <a name="new-sysdmdbpageinfo-system-function-returns-page-information-ctp-20"></a>페이지 정보를 반환하는 새 sys.dm_db_page_info 시스템 함수(CTP 2.0)

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

- **Kubernetes를 사용하는 Docker 컨테이너의 Always On 가용성 그룹(CTP 2.2)**: Kubernetes는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컨테이너를 오케스트레이션하여 SQL Server Always On 가용성 그룹이 있는 일련의 고가용성 데이터베이스를 제공할 수 있습니다. Kubernetes 연산자는 **mssql-server 컨테이너** 및 상태 모니터가 있는 컨테이너를 포함하는 StatefulSet을 배포합니다.

- **새 컨테이너 레지스트리(CTP 2.1)**: 이제 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]뿐만 아니라 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]에 대한 모든 컨테이너 이미지가 Microsoft Container Registry에 있습니다. Microsoft Container Registry는 Microsoft 제품 컨테이너의 배포를 위한 공식 컨테이너 레지스트리입니다. 이제 인증된 RHEL 기반 이미지도 게시됩니다.

  - Microsoft Container Registry: `mcr.microsoft.com/mssql/server:vNext-CTP2.0`
  - 인증된 RHEL 기반 컨테이너 이미지: `mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0`

- **복제 지원(CTP 2.0)**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 Linux에서 SQL Server 복제를 지원합니다. SQL 에이전트를 사용하는 Linux 가상 머신은 게시자, 배포자 또는 구독자일 수 있습니다. 

  다음 유형의 게시를 만듭니다.
  - 트랜잭션
  - 스냅숏
  - 병합

  복제 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 구성하거나 [복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)를 만듭니다.

- **MSDTC(Microsoft Distributed Transaction Coordinator) 지원(CTP 2.0)**: Linux의 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 MSDTC를 지원합니다. 자세한 내용은 [Linux에서 MSDTC를 구성하는 방법](../linux/sql-server-linux-configure-msdtc.md)을 참조하세요.

- **타사 AD 공급 기업에 대한 OpenLDAP 지원(CTP 2.0)**: Linux의 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 타사 공급 기업이 Active Directory에 가입할 수 있도록 하는 OpenLDAP를 지원합니다.

- **Linux의 Machine Learning(CTP 2.0)**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Machine Learning Services(데이터베이스 내)는 이제 Linux에서 지원됩니다. 지원에는 `sp_execute_external_script` 저장 프로시저가 포함됩니다. Machine Learning Services를 Linux에 설치하는 방법에 대한 지침은 [Linux에 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Machine Learning Services R 및 Python 지원 설치](../linux/sql-server-linux-setup-machine-learning.md)를 참조하세요.

## <a id="mds"></a> Master Data Services 

- **Silverlight 컨트롤을 HTML로 대체(CTP 2.0)**: MDS(Master Data Services) 포털은 더 이상 Silverlight를 사용하지 않습니다. 이전의 모든 Silverlight 구성 요소가 HTML 컨트롤로 바뀌었습니다.

## <a id="security"></a>보안

- **SQL Server 구성 관리자의 인증서 관리(CTP 2.0)**: SSL/TLS 인증서는 SQL Server 인스턴스에 대한 액세스를 보호하기 위해 널리 사용됩니다. 이제 인증서 관리는 SQL Server 구성 관리자에 통합되어 다음과 같은 일반적인 작업을 간소화합니다.

  - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 설치된 인증서 보기 및 유효성 검사 
  - 만료가 가까워지는 인증서 보기
  - (주 복제본을 보유하는 노드에서) Always On 가용성 그룹에 참여하는 컴퓨터에 인증서를 배포합니다.
  - (활성 노드에서) 장애 조치(Failover) 클러스터 인스턴스에 참여하는 컴퓨터에 인증서를 배포합니다.

  > [!NOTE]
  > 사용자는 모든 클러스터 노드에서 관리자 권한이 있어야 합니다.

## <a id="tools"></a>도구

- [**Azure Data Studio**](../azure-data-studio/what-is.md): 이전에 미리 보기 이름 SQL Operations Studio로 릴리스되었던 Azure Data Studio는 데이터 개발 및 관리 측면에서 가장 일반적인 작업을 수행하기 위한 경량의 최신 오픈 소스, 플랫폼 간 데스크톱 도구입니다. Azure Data Studio 및 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 미리 보기 확장](../azure-data-studio/sql-server-2019-extension.md)을 사용하면 Windows, macOS 및 Linux에서 온-프레미스 및 클라우드의 SQL Server에 연결할 수 있습니다. Azure Data Studio를 사용하여 다음을 수행할 수 있습니다.

  - 이제 AAD를 지원합니다. (CTP 2.3)
  - Notebook 보기 UI가 Azure Data Studio 코어로 이동되었습니다. (CTP 2.3)
  - 외부 데이터 원본을 HDFS(Hadoop 분산 파일 시스템)에서 SQL Server 빅 데이터 클러스터로 만드는 마법사가 새로 추가되었습니다. (CTP 2.3)
  - Notebook 뷰어 UI가 향상되었습니다. (CTP 2.3)
  - 새 Notebook API가 추가되었습니다. (CTP 2.3)
  - Python 패키지 업데이트를 지원하는 "Notebook 종속성 재설치" 명령이 추가되었습니다. (CTP 2.3)
  - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 빅 데이터 클러스터를 연결하고 관리합니다. (CTP 2.1)
  - 대단히 빠른 Intellisense, 코드 조각 및 소스 제어 통합으로 최신 개발 환경에서 쿼리를 편집 및 실행합니다. (CTP 2.0) 
  - 결과 집합을 차트로 만드는 기본 제공 차트 기능으로 데이터를 빠르게 시각화합니다. (CTP 2.0)
  - 사용자 지정 가능한 위젯을 사용하여 서버 및 데이터베이스에 대한 사용자 지정 대시보드를 만듭니다. (CTP 2.0)  
  - 기본 제공 터미널을 사용하여 보다 광범위한 환경을 쉽게 관리합니다. (CTP 2.0)
  - Jupyter를 기반으로 하는 통합 노트 환경에서 데이터를 분석합니다. (CTP 2.0)
  - 사용자 지정 테마 및 확장을 사용하여 환경을 개선합니다.(CTP 2.0)
  - 또한 기본 제공 구독 및 리소스 브라우저를 사용하여 Azure 리소스를 탐색합니다. (CTP 2.0)
  - SQL Server 빅 데이터 클러스터를 사용하는 시나리오를 지원합니다. (CTP 2.0)
  
  > [!TIP]
  > Azure Data Studio의 향상된 최신 기능은 [Azure Data Studio 릴리스 정보](../azure-data-studio/release-notes-azure-data-studio.md)를 참조하세요.

- [**SSMS(SQL Server Management Studio) 18.0(미리 보기)**](../ssms/sql-server-management-studio-ssms.md): [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 지원합니다.

  - SSMS에서 Azure Data Studio를 시작합니다. (CTP 2.3)
  - 보안 Enclave를 사용한 Always Encrypted 지원 (CTP 2.0)
  - 보다 작아진 다운로드 크기 (CTP 2.0)
  - Visual Studio 2017 격리 셸을 기준으로 하는 새로운 방식 (CTP 2.0)
  - 전체 목록을 보려면 [SSMS 변경 로그](../ssms/release-notes-ssms.md)를 참조하세요. (CTP 2.0)

- [**SQL Server PowerShell 모듈**](http://www.powershellgallery.com/packages/SqlServer/21.1.18080): SqlServer PowerShell 모듈을 사용하면 SQL Server 개발자, 관리자 및 BI 전문가가 데이터베이스 배포 및 서버 관리를 자동화할 수 있습니다.

  - SMO v150을 지원하려면 21.0에서 21.1로 업그레이드합니다.
  - AS/IS/RS 그룹을 표시하도록 SQL Server 공급자(SQLRegistration)가 업데이트되었습니다.
  - SQL Server 2014를 대상으로 할 때 발생하는 `New-SqlAvailabilityGroup` cmdlet 문제가 해결되었습니다.
  - `Set-SqlAvailabilityReplica` 및 `New-SqlAvailabilityReplica`에 `–LoadBalancedReadOnlyRoutingList` 매개 변수가 추가되었습니다.
  - Azure Analysis Services에 대한 `Login-AzureAsAccount`에서 캐시된 로그인 토큰을 사용하도록 `AnalysisService` cmdlet이 업데이트되었습니다.

## <a id="ssas"></a>SSAS([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services) 

### <a name="many-to-many-relationships-in-tabular-models-ctp-24"></a>테이블 형식 모델의 다 대 다 관계(CTP 2.4)

이 기능은 두 열이 모두 고유하지 않은 테이블 간의 다 대 다 관계를 허용합니다. 차원의 키 열보다 높은 세분성의 차원 및 팩트 테이블 간에 관계를 정의할 수 있습니다. 이렇게 하면 결과 모델에는 논리적으로 그룹화된 열이 있는 테이블 수가 더 적기 때문에 차원 테이블을 정규화하지 않아도 되고 사용자 환경을 개선할 수 있습니다. 이 CTP 2.4 릴리스의 경우 다 대 다 관계는 엔진 전용 기능입니다. 

다 대 다 관계에는 현재 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.3 이상에서만 지원되는 1470 호환성 수준의 모델이 필요합니다. 이 CTP 2.4 릴리스의 경우 TOM(테이블 형식 개체 모델) API, TMSL( 테이블 형식 모델 스크립팅 언어) 및 오픈 소스 테이블 형식 편집기 도구를 사용하여 다 대 다 관계를 만들 수 있습니다. SSDT(SQL Server Data Tools) 지원은 설명서와 함께 이후 릴리스에 포함됩니다. 이 CTP 및 다른 CTP 기능 릴리스에 대한 추가 정보는 Analysis Services 블로그에서 제공됩니다.

### <a name="memory-settings-for-resource-governance-ctp-24"></a>리소스 거버넌스에 대한 메모리 설정(CTP 2.4)

여기에 설명된 메모리 설정은 이미 Azure Analysis Services에서 사용할 수 있습니다. CTP 2.4부터는 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Analysis Services에서도 지원됩니다. 

- **Memory\QueryMemoryLimit** - 이 메모리 속성은 모델에 제출된 DAX 쿼리에서 생성된 메모리 스풀을 제한하는 데 사용할 수 있습니다. 
- **DbpropMsmdRequestMemoryLimit** - 이 XMLA 속성은 연결용 Memory\QueryMemoryLimit 서버 속성 값을 재정의하는 데 사용할 수 있습니다.
- **OLAP\Query\RowsetSerializationLimit** - 이 서버 속성은 행 집합에서 반환되는 행 수를 제한하여 광범위한 데이터 내보내기 사용으로부터 서버 리소스를 보호합니다. 이 속성은 DAX 쿼리 및 MDX 쿼리 둘 다에 적용됩니다.

이러한 속성은 최신 버전의 SSMS(SQL Server Management Studio)를 사용하여 설정할 수 있습니다. 이 기능에 대한 추가 정보는 Analysis Services 블로그에서 제공됩니다.

### <a name="calculation-groups-in-tabular-models-ctp-23"></a>테이블 형식 모델의 계산 그룹(CTP 2.3) 

계산 그룹은 동일한 계산(예: 시간 인텔리전스)을 사용하여 측정값이 확산될 수 있는 복잡한 모델의 일반적인 문제를 해결합니다. 계산 그룹은 보고하는 클라이언트에 단일 열이 있는 테이블로 표시됩니다. 열의 각 값은 모든 측정값에 적용할 수 있는 재사용 가능한 계산 또는 계산 항목을 나타냅니다.  

계산 그룹에는 임의 개수의 계산 항목이 포함될 수 있습니다. 각 계산 항목은 DAX 식으로 정의됩니다. 계산 그룹을 사용하기 위해 다음 세 개의 DAX 함수가 새로 도입되었습니다. 

- `SELECTEDMEASURE()` - 현재 컨텍스트에 있는 측정값에 대한 참조를 반환합니다.  

- `SELECTEDMEASURENAME()` - 현재 컨텍스트에 있는 측정값의 이름이 포함된 문자열을 반환합니다.  

- `ISSELECTEDMEASURE(M1, M2, …)` - 현재 컨텍스트에 있는 측정값이 인수로 지정된 측정값 중 하나인지 여부를 나타내는 부울을 반환합니다.

새로운 DAX 함수 외에도 다음 두 개의 동적 관리 뷰가 새로 도입되었습니다.

- `TMSCHEMA_CALCULATION_GROUPS`  
- `TMSCHEMA_CALCULATION_ITEMS`  

#### <a name="limitations-in-this-release"></a>이 릴리스의 제한 사항:

- `ALLSELECTED DAX` 함수는 아직 지원되지 않습니다.
- 계산 그룹 테이블에 정의된 행 수준 보안은 아직 지원되지 않습니다.
- 계산 그룹 테이블에 정의된 개체 수준 보안은 아직 지원되지 않습니다.
- 계산 항목을 참조하는 DetailsRows 식은 아직 지원되지 않습니다.
- MDX는 아직 지원되지 않습니다.

#### <a name="known-issues-in-this-release"></a>이 릴리스의 알려진 문제:

- 모델에 계산 그룹이 있으면 측정 값이 변형 데이터 유형을 반환할 수 있으므로 계산된 열과 측정값을 참조하는 테이블에 대한 새로 고침 오류가 발생할 수 있습니다.

#### <a name="compatibility-level"></a>호환성 수준

계산 그룹에는 현재 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.3 이상에서만 지원되는 1470 호환성 수준의 모델이 필요합니다. 계산 그룹은 현재 TOM(테이블 형식 개체 모델) API, TMSL( 테이블 형식 모델 스크립팅 언어) 및 오픈 소스 테이블 형식 편집기 도구를 사용하여 만들 수 있습니다. SSDT(SQL Server Data Tools) 지원은 설명서와 함께 이후 릴리스에 포함됩니다. 이 CTP 및 다른 CTP 기능 릴리스에 대한 추가 정보는 Analysis Services 블로그에서 제공됩니다.

## <a name="other-services"></a>기타 서비스

CTP 2.4부터 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 다음 서비스의 새로운 기능을 도입하지 않습니다.

- SSIS([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)])
- SSRS([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)])

## <a name="next-steps"></a>다음 단계

- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 릴리스 정보](sql-server-ver15-release-notes.md).

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: 기술 백서](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />2018년 9월에 게시되었습니다. Windows, Linux 및 Docker 컨테이너용 Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0에 적용됩니다.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
