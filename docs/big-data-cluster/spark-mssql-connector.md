---
title: SQL Server 및 Azure SQL용 Apache Spark 커넥터 사용
titleSuffix: SQL Server big data clusters
description: SQL Server 및 Azure SQL용 Apache Spark 커넥터를 사용하여 SQL Server를 읽고 쓰는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: 454d5fadaa88d645e9d1c2feec2c9d87c2af29c9
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645504"
---
# <a name="use-the-apache-spark-connector-for-sql-server-and-azure-sql"></a>SQL Server 및 Azure SQL용 Apache Spark 커넥터 사용

[SQL Server 및 Azure SQL용 Apache Spark 커넥터](https://github.com/microsoft/sql-spark-connector)는 빅 데이터 분석에서 트랜잭션 데이터를 사용할 수 있도록 하는 고성능 커넥터이며 임시 쿼리 또는 보고를 위해 결과를 유지합니다. 이 커넥터를 사용하면 온-프레미스 또는 클라우드의 모든 SQL 데이터베이스를 Spark 작업에 대한 입력 데이터 원본 또는 출력 데이터 싱크로 사용할 수 있습니다. 이 커넥터는 SQL Server 대량 쓰기 API를 사용합니다. 사용자는 모든 대량 쓰기 매개 변수를 선택적 매개 변수로 전달할 수 있으며, 커넥터는 이 매개 변수를 그대로 기본 API에 전달합니다. 대량 쓰기 작업에 대한 자세한 내용은 [JDBC 드라이버에서 대량 복사 사용]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)을 참조하세요.

커넥터는 SQL Server 빅 데이터 클러스터에 기본적으로 포함되어 있습니다.

[오픈 소스 리포지토리](https://github.com/microsoft/sql-spark-connector)에 커넥터에 대해 자세히 알아보세요. 예제는 [샘플](https://github.com/microsoft/sql-spark-connector/tree/master/samples)을 참조하세요.

## <a name="write-to-a-new-sql-table"></a>새 SQL 테이블에 쓰기

>[!CAUTION]
> `overwrite` 모드에서는 데이터베이스에 이미 테이블이 있는 경우 기본적으로 커넥터가 먼저 테이블을 삭제합니다. 예기치 않은 데이터 손실을 방지하려면 이 옵션을 신중하게 사용해야 합니다.
> 
> `overwrite` 모드를 사용할 때 `truncate` 옵션을 사용하지 않을 경우 테이블을 다시 만들면서 인덱스가 손실됩니다. 예를 들어 columnstore 테이블은 힙이 됩니다. 기존 인덱싱을 유지하려면 `truncate` 옵션을 `true`로 지정해야 합니다. 예: `.option("truncate",true)`

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

## <a name="append-to-sql-table"></a>SQL 테이블에 추가
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

기본적으로 이 커넥터는 데이터베이스에 대량 삽입을 수행할 때 READ_COMMITTED 격리 수준을 사용합니다. 이를 다른 격리 수준으로 재정의하려는 경우 아래와 같이 `mssqlIsolationLevel` 옵션을 사용합니다.
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

## <a name="non-active-directory-mode"></a>비 Active Directory 모드

비 Active Directory 모드 보안에서는 각 사용자에게 사용자 이름과 암호가 있으며, 읽기 및/또는 쓰기를 수행하려면 커넥터를 인스턴스화할 때 사용자 이름과 암호를 매개 변수로 제공해야 합니다.

비 Active Directory 모드의 커넥터 인스턴스화 예제는 다음과 같습니다. 스크립트를 실행하기 전에 `?`를 계정의 값으로 바꿉니다.

```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark" 

url = "jdbc:sqlserver://master-p-svc;databaseName=?;"
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("user", ?) \ 
   .option("password",?) 
writer.save() 
```

## <a name="active-directory-mode"></a>Active Directory 모드

Active Directory 모드 보안에서는 사용자가 keytab 파일을 생성한 후, 커넥터를 인스턴스화할 때 `principal` 및 `keytab`을 매개 변수로 제공해야 합니다.

이 모드에서 드라이버는 keytab 파일을 해당 실행기 컨테이너에 로드합니다. 실행기는 보안 주체 이름과 keytab을 사용하여 읽기/쓰기용 JDBC 커넥터를 만드는 데 사용되는 토큰을 생성합니다.

Active Directory 모드의 커넥터 인스턴스화 예제는 다음과 같습니다. 스크립트를 실행하기 전에 `?`를 계정의 값으로 바꿉니다.

```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark"

url = "jdbc:sqlserver://master-p-svc;databaseName=?;integratedSecurity=true;authenticationScheme=JavaKerberos;" 
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("principal", ?) \ 
   .option("keytab", ?)   

writer.save() 
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)을 참조하세요.

SQL Server 빅 데이터 클러스터에 대한 피드백이나 기능 권장 사항이 있으면 [SQL Server 빅 데이터 클러스터 피드백에 의견을 남겨 주세요](https://aka.ms/sql-server-bdc-feedback).
