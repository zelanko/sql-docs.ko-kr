---
title: SQL Server용 Apache Spark 커넥터
description: SQL Server용 Apache Spark 커넥터를 사용하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rajmera3
ms.author: raajmera
ms.reviewer: mikeray
ms.openlocfilehash: 059ecfb25389de1be0f8636a868e81e621e57bac
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867234"
---
# <a name="apache-spark-connector-sql-server--azure-sql"></a>Apache Spark 커넥터: SQL Server 및 Azure SQL

SQL Server 및 Azure SQL용 Apache Spark 커넥터는 빅 데이터 분석에서 트랜잭션 데이터를 사용할 수 있도록 하는 고성능 커넥터이며 임시 쿼리 또는 보고를 위해 결과를 유지합니다. 이 커넥터를 사용하면 온-프레미스 또는 클라우드의 모든 SQL 데이터베이스를 Spark 작업에 대한 입력 데이터 원본 또는 출력 데이터 싱크로 사용할 수 있습니다.

이 라이브러리에는 SQL Server 및 Azure SQL용 Apache Spark 커넥터의 소스 코드가 포함되어 있습니다.

[Apache Spark](https://spark.apache.org/)는 대규모 데이터를 처리하기 위한 통합 분석 엔진입니다.

Maven 좌표(`com.microsoft.azure:spark-mssql-connector:1.0.0`)를 통해 커넥터를 프로젝트로 가져올 수 있습니다. 원본에서 커넥터를 빌드하거나, GitHub의 릴리스 섹션에서 jar을 다운로드할 수도 있습니다. 이 커넥터에 대한 최신 정보는 [SQL Spark 커넥터 GitHub 리포지토리](https://github.com/microsoft/sql-spark-connector)를 참조하세요.

## <a name="supported-features"></a>지원되는 기능

* 모든 Spark 바인딩(Scala, Python, R) 지원
* 기본 인증 및 AD(Active Directory) 키 탭 지원
* 다시 정렬된 `dataframe` 쓰기 지원
* SQL Server 빅 데이터 클러스터에서 SQL Server 단일 인스턴스 및 데이터 풀에 쓰기 지원
* SQL Server 단일 인스턴스에 대한 안정적인 커넥터 지원

| 구성 요소                            | 지원되는 버전              |
|--------------------------------------|---------------------------------|
| Apache Spark                         | 2.4.5(Spark 3.0은 지원되지 않음) |
| Scala                                | 2.11                            |
| SQL Server용 Microsoft JDBC Driver | 8.2                             |
| Microsoft SQL Server                 | SQL Server 2008 이상        |
| Azure SQL Databases                  | 지원됨                       |

> [!NOTE]
> Azure Synapse Analytics(Azure SQL DW) 사용은 이 커넥터에서 테스트되지 않았습니다. 작동할 수 있지만 의도하지 않은 결과가 발생할 수도 있습니다.

### <a name="supported-options"></a>지원되는 옵션
SQL Server 및 Azure SQL용 Apache Spark 커넥터는 여기에 정의된 옵션을 지원합니다. [SQL DataSource JDBC](https://spark.apache.org/docs/latest/sql-data-sources-jdbc.html)

다음 옵션도 지원됩니다.

| 옵션 | 기본값 | 설명 |
| --------- | ------------------ | ------------------------------------------ |
| `reliabilityLevel` | `BEST_EFFORT` | `BEST_EFFORT` 또는 `NO_DUPLICATES` `NO_DUPLICATES`는 실행기 다시 시작 시나리오에서 안정적인 삽입을 구현합니다. |
| `dataPoolDataSource` | `none` | `none`은 값이 설정되지 않았으며 커넥터가 SQL Server 단일 인스턴스에 써야 함을 나타냅니다. 빅 데이터 클러스터의 데이터 풀 테이블에 쓰려면 이 값을 데이터 원본 이름으로 설정합니다.|
| `isolationLevel` | `READ_COMMITTED` | 격리 수준을 지정합니다. |
| `tableLock` | `false` | 쓰기 성능을 향상시키기 위해 `TABLOCK`을 사용하여 삽입 옵션을 구현합니다. |
| `schemaCheckEnabled` | `true` | false로 설정하면 엄격한 데이터 프레임 및 SQL 테이블 스키마 검사가 사용되지 않습니다. |

다른 [대량 복사 옵션](../jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)은 `dataframe` 옵션으로 설정될 수 있으며 쓰기 시 `bulkcopy` API에 전달됩니다.

## <a name="performance-comparison"></a>성능 비교

SQL Server 및 Azure SQL용 Apache Spark 커넥터는 SQL Server 쓰기 속도가 일반 JDBC 커넥터보다 최대 15배 빠릅니다. 성능 특성은 유형, 데이터 볼륨, 사용하는 옵션에 따라 달라지며 실행마다 차이를 보일 수 있습니다. 다음 성능 결과는 spark `dataframe`에 약 144만 개 행이 있는 SQL 테이블을 덮어쓰는 데 걸리는 시간입니다. Spark `dataframe`은 [spark TPCDS 벤치마크](https://github.com/databricks/spark-sql-perf)를 사용하여 생성된 `store_sales` HDFS 테이블을 읽어 생성됩니다. `store_sales`를 `dataframe`으로 읽는 시간은 제외됩니다. 결과는 세 번의 실행에 대한 평균입니다.

| 연결선 유형 | 옵션 | 설명 |  쓰기 시간 |
| --------- | ------------------ | -------------------------------------| ---------- |
| `JDBCConnector` | 기본값 | 기본 옵션을 사용한 일반 JDBC 커넥터 |  1,385초 |
| `sql-spark-connector` | `BEST_EFFORT` | 기본 옵션을 사용한 최상의 노력 `sql-spark-connector` |580초 |
| `sql-spark-connector` | `NO_DUPLICATES ` | 안정적인 `sql-spark-connector` | 709초 |
| `sql-spark-connector` | `BEST_EFFORT` + tabLock=true | 테이블 잠금이 설정된 최상의 노력 `sql-spark-connector` | 72초 |
| `sql-spark-connector` | `NO_DUPLICATES ` + tabLock=true| 테이블 잠금이 설정된 안정적 `sql-spark-connector`| 198초 |

Config

- Spark config: num_executors = 20, executor_memory = '1664 m', executor_cores = 2
- Data Gen config: scale_factor=50, partitioned_tables=true
- 행이 143,997,590개인 데이터 파일 `store_sales`

환경

- [SQL Server 빅 데이터 클러스터](../../big-data-cluster/release-notes-big-data-cluster.md) CU5
- `master` + 6개 노드
- 각 노드는 5세대 서버, 512GB RAM, 노드당 4TB NVM, NIC 10GB

## <a name="commonly-faced-issues"></a>일반적으로 발생하는 문제

### `java.lang.NoClassDefFoundError: com/microsoft/aad/adal4j/AuthenticationException`

이 문제는 Hadoop 환경에서 이전 버전의 mssql 드라이버(현재 이 커넥터에 포함됨)를 사용하는 경우 발생합니다. 이전 Azure SQL 커넥터를 사용하고 해당 클러스터에 드라이버를 수동으로 설치하여 Azure Active Directory 호환성을 제공한 경우 해당 드라이버를 제거해야 합니다.

문제를 해결하는 단계:

1. 일반 Hadoop 환경을 사용하는 경우 mssql jar: `rm $HADOOP_HOME/share/hadoop/yarn/lib/mssql-jdbc-6.2.1.jre7.jar`을 확인하고 제거합니다. Databricks를 사용하는 경우 전역 또는 클러스터 init 스크립트를 추가하여 `/databricks/jars` 폴더에서 이전 버전의 mssql 드라이버를 제거하거나 기존 스크립트에 다음 줄을 추가합니다. `rm /databricks/jars/*mssql*`
2. `adal4j` 및 `mssql` 패키지를 추가합니다. 예를 들어 Maven을 사용할 수 있지만 어떤 방법이든 작동합니다. 

   > [!CAUTION]
   > 이러한 방식으로 SQL spark 커넥터를 설치하지 마십시오.

1. 연결 구성에 드라이버 클래스를 추가합니다. 예를 들어:

   ```csharp
   connectionProperties = {
     `Driver`: `com.microsoft.sqlserver.jdbc.SQLServerDriver`
   }`
   ```

자세한 내용 및 설명은 [https://github.com/microsoft/sql-spark-connector/issues/26](https://github.com/microsoft/sql-spark-connector/issues/26#issuecomment-672006339)에 대한 해결 방법을 참조하세요.

## <a name="get-started"></a>시작

SQL Server 및 Azure SQL용 Apache Spark 커넥터는 Spark DataSourceV1 API 및 SQL Server Bulk API를 기반으로 하며 기본 제공 JDBC Spark-SQL 커넥터와 동일한 인터페이스를 사용합니다. 이러한 통합을 통해 단순히 `com.microsoft.sqlserver.jdbc.spark`로 형식 매개 변수를 업데이트하여 커넥터를 쉽게 통합하고 기존 Spark 작업을 마이그레이션할 수 있습니다.

프로젝트에 커넥터를 포함하려면 이 리포지토리를 다운로드하고 SBT를 사용하여 jar을 빌드합니다.

## <a name="write-to-a-new-sql-table"></a>새 SQL 테이블에 쓰기

> [!WARNING]
> `overwrite` 모드에서는 데이터베이스에 이미 테이블이 있는 경우 기본적으로 먼저 테이블을 삭제합니다. 예기치 않은 데이터 손실을 방지하려면 이 옵션을 신중하게 사용해야 합니다.

`overwrite` 모드를 사용할 때 `truncate` 옵션을 사용하지 않을 경우 테이블을 다시 만들면서 인덱스가 손실됩니다. 예를 들어 columnstore 테이블이 이제 힙이 됩니다. 기존 인덱싱을 유지하려면 `truncate` 옵션을 true로 지정해야 합니다. 예들 들어 `.option("truncate","true")`입니다.

```python
server_name = "jdbc:sqlserver://{SERVER_ADDR}"
database_name = "database_name"
url = server_name + ";" + "databaseName=" + database_name + ";"

table_name = "table_name"
username = "username"
password = "password123!#" # Please specify password here

try:
  df.write \
    .format("com.microsoft.sqlserver.jdbc.spark") \
    .mode("overwrite") \
    .option("url", url) \
    .option("dbtable", table_name) \
    .option("user", username) \
    .option("password", password) \
    .save()
except ValueError as error :
    print("Connector write failed", error)
```

### <a name="append-to-sql-table"></a>SQL 테이블에 추가

```python
try:
  df.write \
    .format("com.microsoft.sqlserver.jdbc.spark") \
    .mode("append") \
    .option("url", url) \
    .option("dbtable", table_name) \
    .option("user", username) \
    .option("password", password) \
    .save()
except ValueError as error :
    print("Connector write failed", error)
```

## <a name="specify-the-isolation-level"></a>격리 수준 지정

기본적으로 이 커넥터는 데이터베이스에 대량 삽입을 수행할 때 `READ_COMMITTED` 격리 수준을 사용합니다. 격리 수준을 재정의하려면 아래와 같이 `mssqlIsolationLevel` 옵션을 사용합니다.

```python
    .option("mssqlIsolationLevel", "READ_UNCOMMITTED") \
```

## <a name="read-from-sql-table"></a>SQL 테이블에서 읽기

```python
jdbcDF = spark.read \
        .format("com.microsoft.sqlserver.jdbc.spark") \
        .option("url", url) \
        .option("dbtable", table_name) \
        .option("user", username) \
        .option("password", password).load()
```

## <a name="azure-active-directory-authentication"></a>Azure Active Directory 인증

### <a name="python-example-with-service-principal"></a>서비스 주체를 사용하는 Python 예제

```python
context = adal.AuthenticationContext(authority)
token = context.acquire_token_with_client_credentials(resource_app_id_url, service_principal_id, service_principal_secret)
access_token = token["accessToken"]

jdbc_db = spark.read \
        .format("com.microsoft.sqlserver.jdbc.spark") \
        .option("url", url) \
        .option("dbtable", table_name) \
        .option("accessToken", access_token) \
        .option("encrypt", "true") \
        .option("hostNameInCertificate", "*.database.windows.net") \
        .load()
```

### <a name="python-example-with-active-directory-password"></a>Active Directory 암호를 사용하는 Python 예제

```python
jdbc_df = spark.read \
        .format("com.microsoft.sqlserver.jdbc.spark") \
        .option("url", url) \
        .option("dbtable", table_name) \
        .option("authentication", "ActiveDirectoryPassword") \
        .option("user", user_name) \
        .option("password", password) \
        .option("encrypt", "true") \
        .option("hostNameInCertificate", "*.database.windows.net") \
        .load()
```

Active Directory를 사용하여 인증하려면 필요한 종속성을 설치해야 합니다.

**Scala**의 경우 `_com.microsoft.aad.adal4j_` 아티팩트를 설치해야 합니다.

**Python**의 경우 `_adal_` 라이브러리 설치해야 합니다.  이 라이브러리는 PIP를 통해 사용할 수 있습니다.

예제는 [샘플 Notebook](https://github.com/microsoft/sql-spark-connector/tree/master/samples)을 참조하세요.

## <a name="support"></a>지원

Azure SQL 및 SQL Server용 Apache Spark 커넥터는 오픈 소스 프로젝트입니다. 이 커넥터에는 Microsoft 지원이 제공되지 않습니다. 커넥터에 대한 문제 또는 질문이 있는 경우 이 프로젝트 리포지토리에서 문제를 게시하세요. 커넥터 커뮤니티는 활발하게 제출을 모니터링하고 있습니다.

## <a name="next-steps"></a>다음 단계

[SQL Spark 커넥터 GitHub 리포지토리](https://github.com/microsoft/sql-spark-connector)를 참조하세요.

격리 수준에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL(Transact-SQL)](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.