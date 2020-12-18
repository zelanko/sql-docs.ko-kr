---
description: CREATE EXTERNAL DATA SOURCE(Transact-SQL)
title: CREATE EXTERNAL DATA SOURCE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/26/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL DATA SOURCE
- CREATE_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, data source
- PolyBase, create data source
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e85d783f9e06c5b0a7ede983f6ab4d1079ef2a5e
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489423"
---
# <a name="create-external-data-source-transact-sql"></a>CREATE EXTERNAL DATA SOURCE(Transact-SQL)

SQL Server, SQL Database, Azure Synapse Analytics 또는 Analytics Platform System(병렬 데이터 웨어하우스 또는 PDW)을 사용하여 쿼리용 외부 데이터 원본을 만듭니다.

이 아티클에서는 원하는 SQL 제품에 대한 구문, 인수, 설명, 사용 권한 및 예제를 제공합니다.

구문 표기 규칙에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)을 참조하십시오.

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](create-external-data-source-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />분석](create-external-data-source-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](create-external-data-source-transact-sql.md?view=aps-pdw-2016-au7)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-sql-server"></a>개요: SQL Server

PolyBase 쿼리에 대한 외부 데이터 원본을 만듭니다. 외부 데이터 원본은 연결을 설정하고 다음과 같은 기본 사용 사례를 지원하는 데 사용됩니다.

- [PolyBase][intro_pb]를 사용하여 데이터 가상화 및 데이터 로드
- `BULK INSERT` 또는 `OPENROWSET`를 사용한 대량 로드 작업

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]로 시작

## <a name="syntax"></a>구문

```syntaxsql
CREATE EXTERNAL DATA SOURCE <data_source_name>
WITH
  ( [ LOCATION = '<prefix>://<path>[:<port>]' ]
    [ [ , ] CONNECTION_OPTIONS = '<name_value_pairs>']
    [ [ , ] CREDENTIAL = <credential_name> ]
    [ [ , ] PUSHDOWN = { ON | OFF } ]
    [ [ , ] TYPE = { HADOOP | BLOB_STORAGE } ]
    [ [ , ] RESOURCE_MANAGER_LOCATION = '<resource_manager>[:<port>]' )
[ ; ]
```

## <a name="arguments"></a>인수

### <a name="data_source_name"></a>data_source_name

데이터 원본에 대한 사용자 정의 이름을 지정합니다. 이름은 반드시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터베이스 내에서 고유해야 합니다.

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

외부 데이터 원본에 대한 연결 프로토콜 및 경로를 제공합니다.

| 외부 데이터 원본    | 위치 접두사 | 위치 경로                                         | 제품 / 서비스별로 지원되는 위치 |
| ----------------------- | --------------- | ----------------------------------------------------- | ---------------------------------------- |
| Cloudera 또는 Hortonworks | `hdfs`          | `<Namenode>[:port]`                                   | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]로 시작                       |
| Azure Storage 계정(V2) | `wasb[s]`       | `<container>@<storage_account>.blob.core.windows.net` | [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 시작         계층 구조 네임스페이스는 지원되지 **않음** |
| [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]              | `sqlserver`     | `<server_name>[\<instance_name>][:port]`              | [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]로 시작                       |
| Oracle                  | `oracle`        | `<server_name>[:port]`                                | [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]로 시작                       |
| Teradata                | `teradata`      | `<server_name>[:port]`                                | [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]로 시작                       |
| MongoDB 또는 CosmosDB     | `mongodb`       | `<server_name>[:port]`                                | [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]로 시작                       |
| ODBC                    | `odbc`          | `<server_name>[:port]`                                | [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]로 시작-Windows만        |
| 대량 작업         | `https`         | `<storage_account>.blob.core.windows.net/<container>` | [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]로 시작                        |
| 에지 허브         | `edgehub`         | 해당 사항 없음 | EdgeHub는 항상 [Azure SQL Edge](/azure/azure-sql-edge/overview/) 인스턴스에 대해 로컬입니다. 따라서 경로 또는 포트 값을 지정할 필요가 없습니다. Azure SQL Edge에서만 사용할 수 있습니다.                      |
| Kafka        | `kafka`         | `<Kafka IP Address>[:port]` | Azure SQL Edge에서만 사용할 수 있습니다.                      |

위치 경로:

- `<`Namenode`>` = Hadoop 클러스터에 있는 `Namenode`의 머신 이름, 이름서비스 URI 또는 IP 주소입니다. PolyBase는 Hadoop 클러스터에서 사용하는 모든 DNS 이름을 확인해야 합니다. <!-- For highly available Hadoop configurations, provide the Nameservice ID as the `LOCATION`. -->
- `port` = 외부 데이터 원본이 수신 대기 중인 포트입니다. Hadoop에서는 `fs.defaultFS` 구성 매개 변수를 사용하여 포트를 찾을 수 있습니다. 기본값은 8020입니다.
- `<container>` = 데이터를 보관하는 스토리지 계정의 컨테이너입니다. 루트 컨테이너는 읽기 전용이므로 데이터를 컨테이너에 다시 쓸 수 없습니다.
- `<storage_account>` = Azure 리소스의 스토리지 계정 이름입니다.
- `<server_name>` = 호스트 이름입니다.
- `<instance_name>` = SQL Server 명명된 인스턴스의 이름입니다. 대상 인스턴스에서 SQL Server Browser Service가 실행 중인 경우에 사용됩니다.

위치 설정 시 추가 참고 사항 및 지침:

- [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 개체가 생성될 때 외부 데이터 원본이 존재하는지 확인하지 않습니다. 유효성을 검사하려면 외부 데이터 원본을 사용하여 외부 테이블을 만듭니다.
- 일관된 쿼리 의미 체계를 보장하기 위해 Hadoop을 쿼리할 때 모든 테이블에 대해 동일한 외부 데이터 원본을 사용합니다.
- `sqlserver` 위치 접두사를 사용하여 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]를 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 또는 Azure Synapse Analytics에 연결할 수 있습니다.
- `ODBC`를 통해 연결할 때 `Driver={<Name of Driver>}`를 지정합니다.
- `wasbs`는 선택 사항이지만, 데이터가 보안 TLS/SSL 연결을 사용하여 전송되므로 Azure Storage 계정에 액세스하는 데 권장됩니다.
- `abfs` 또는 `abfss` API는 Azure Storage 계정에 액세스할 때 지원되지 않습니다.
- Azure Storage 계정(V2)의 계층 구조 네임스페이스 옵션은 지원되지 않습니다. 이 옵션이 **비활성화** 되어 있는지 확인하세요.
- Hadoop `Namenode` 장애 조치(failover) 중에 PolyBase 쿼리를 성공적으로 수행하려면 Hadoop 클러스터의 `Namenode`에 대한 가상 IP 주소 사용을 고려하세요. 그렇지 않은 경우 [ALTER EXTERNAL DATA SOURCE][alter_eds] 명령을 실행하여 새 위치를 가리킵니다.

### <a name="connection_options--key_value_pair"></a>CONNECTION_OPTIONS = *key_value_pair*

`ODBC`를 외부 데이터 원본에 연결할 때 추가 옵션을 지정합니다. 여러 연결 옵션을 사용하려면 세미콜론으로 구분합니다.


최소한 드라이버 이름이 필요하지만, 설정하면 유용하고 문제 해결에 도움이 되는 `APP='<your_application_name>'`, `ApplicationIntent= ReadOnly|ReadWrite` 등의 다른 옵션도 있습니다.

허용된 [CONNECTION_OPTIONS][connection_options]의 목록은 `ODBC` 제품 설명서를 참조하세요.

### <a name="pushdown--on--off"></a>PUSHDOWN = *ON | OFF*

외부 데이터 원본에 푸시 다운할 수 있는지 여부를 알려줍니다. 기본적으로 설정되어 있습니다.

`PUSHDOWN`은 외부 데이터 원본 수준에서 SQL Server, Oracle, Teradata, MongoDB 또는 ODBC에 연결할 때 지원됩니다.

쿼리 수준에서 푸시 다운을 활성화 또는 비활성화는 [힌트][hint_pb]를 통해 구현됩니다.

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

외부 데이터 원본에 대해 인증하기 위한 데이터베이스 범위 자격 증명을 지정합니다.

자격 증명 생성 시 추가 참고 사항 및 지침:

- `CREDENTIAL`은 데이터 보안이 설정된 경우에만 필요합니다. 익명 액세스를 허용하는 데이터 세트에는 `CREDENTIAL`이 필요하지 않습니다.
- `TYPE` = `BLOB_STORAGE`인 경우 `SHARED ACCESS SIGNATURE`를 ID로 사용하여 자격 증명을 만들어야 합니다. 또한 SAS 토큰은 다음과 같이 구성되어야 합니다.
  - 비밀로 구성된 경우 앞에 오는 `?` 제외
  - 로드해야 하는 파일에 대해 적어도 읽기 권한이 있어야 합니다(예: `srt=o&sp=r`).
  - 유효한 만료 기간을 사용합니다(모든 날짜는 UTC 시간임).

`SHARED ACCESS SIGNATURE` 및 `TYPE` = `BLOB_STORAGE`에서 `CREDENTIAL`을 사용하는 예제는 [대량 작업을 실행하고 Azure Storage에서 SQL Database로 데이터를 검색하기 위한 외부 데이터 원본 만들기](#i-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-storage)를 참조하세요.

데이터베이스 범위 지정 자격 증명을 만들려면 [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)][create_dsc]을 참조하세요.

### <a name="type---hadoop--blob_storage-"></a>TYPE = *[ HADOOP | BLOB_STORAGE ]*

구성 중인 외부 데이터 원본의 유형을 지정합니다. 이 매개 변수가 항상 필요한 것은 아닙니다.

- 외부 데이터 원본이 Cloudera, Hortonworks 또는 Azure Storage 계정이면 HADOOP을 사용합니다.
- [BULK INSERT][bulk_insert]를 사용하거나 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]에서 [OPENROWSET][openrowset]를 사용하여 Azure Storage 계정에서 대량 작업을 실행하는 경우 BLOB_STORAGE를 사용합니다.

> [!IMPORTANT]
> 기타 외부 데이터 원본을 사용하는 경우 `TYPE`을 설정하지 마세요.

`TYPE` = `HADOOP`을 사용하여 Azure Storage 계정에서 데이터를 로드하는 예제는 [wasb://인터페이스를 사용하여 Azure Storage의 데이터에 액세스하는 외부 데이터 원본 만들기](#e-create-external-data-source-to-access-data-in-azure-storage-using-the-wasb-interface)를 참조하세요. <!--[Create external data source to reference Azure Storage](#e-create-external-data-source-to-reference-azure-storage).-->

### <a name="resource_manager_location--resourcemanager_uriport"></a>RESOURCE_MANAGER_LOCATION = *'ResourceManager_URI[:port]'*

Hortonworks 또는 Cloudera에 연결할 때 이 선택적 값을 구성합니다.

`RESOURCE_MANAGER_LOCATION`이 정의되면 쿼리 최적화 프로그램은 성능 향상을 위해 비용 기반 결정을 내립니다. MapReduce 작업을 사용하여 Hadoop으로 계산을 푸시 다운할 수 있습니다. `RESOURCE_MANAGER_LOCATION`을 지정하면 Hadoop과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간에 전송되는 데이터 양을 크게 줄여 쿼리 성능을 향상할 수 있습니다.

리소스 관리자를 지정하지 않은 경우 Hadoop에 대한 푸시 컴퓨팅은 PolyBase 쿼리에 대해 비활성화됩니다.

포트를 지정하지 않을 경우 기본값은 'hadoop 연결' 구성에 대한 현재 설정을 사용하여 선택됩니다.

| Hadoop 연결 | 기본 Resource Manager 포트 |
| ------------------- | ----------------------------- |
| 1                   | 50300                         |
| 2                   | 50300                         |
| 3                   | 8021                          |
| 4                   | 8032                          |
| 5                   | 8050                          |
| 6                   | 8032                          |
| 7                   | 8050                          |

지원되는 Hadoop 버전의 전체 목록은 [PolyBase 연결 구성(Transact-SQL)][connectivity_pb]을 참조하세요.

> [!IMPORTANT]  
> 외부 데이터 원본을 만들 때 RESOURCE_MANAGER_LOCATION 값의 유효성이 검사되지 않습니다. 잘못된 값을 입력하면 제공된 값을 확인할 수 없으므로 푸시 다운을 시도할 때마다 실행 시 쿼리 오류가 발생할 수 있습니다.

[푸시 다운이 활성화된 Hadoop을 참조하는 외부 데이터 원본 만들기](#c-create-external-data-source-to-reference-hadoop-with-push-down-enabled)는 구체적인 예제와 추가 지침을 제공합니다.

## <a name="permissions"></a>사용 권한

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터베이스에 대한 `CONTROL` 권한이 필요합니다.

## <a name="locking"></a>잠금

`EXTERNAL DATA SOURCE` 개체에 대한 공유 잠금을 수행합니다.

## <a name="security"></a>보안

PolyBase는 대부분의 외부 데이터 원본에 대해 프록시 기반 인증을 지원합니다. 데이터베이스 범위 자격 증명을 생성하여 프록시 계정을 만듭니다.

SQL Server 빅 데이터 클러스터의 스토리지 또는 데이터 풀에 연결하면 사용자의 자격 증명이 백 엔드 시스템을 통해 전달됩니다. 통과 인증을 사용하도록 설정하려면 데이터 풀 자체의 로그인을 만듭니다.

현재 `HADOOP` 유형의 SAS 토큰이 지원되지 않습니다. 스토리지 계정 액세스 키에서만 지원됩니다. `HADOOP` 유형 및 SAS 자격 증명으로 외부 데이터 원본을 만들려고 하면 다음 오류로 인해 실패합니다.

`Msg 105019, Level 16, State 1 - EXTERNAL TABLE access failed due to internal error: 'Java exception raised on call to HdfsBridge_Connect. Java exception message: Parameters provided to connect to the Azure storage account are not valid.: Error [Parameters provided to connect to the Azure storage account are not valid.] occurred while accessing external file.'`

## <a name="examples-starting-with-sssql15"></a>예제([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]로 시작)

> [!IMPORTANT]
> PolyBase를 설치하고 사용하도록 설정하는 방법에 대한 자세한 내용은 [Windows에 PolyBase 설치](../../relational-databases/polybase/polybase-installation.md)를 참조하세요.

### <a name="a-create-external-data-source-in-sql-server-2019-to-reference-oracle"></a>A. Oracle을 참조하는 SQL Server 2019에서 외부 데이터 원본 만들기

Oracle을 참조하는 외부 데이터 원본을 만들려면 데이터베이스 범위 자격 증명이 있는지 확인합니다. 이 데이터 원본에 대한 계산 푸시 다운을 활성화하거나 비활성화할 수도 있습니다.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '!MyC0mpl3xP@ssw0rd!' ;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL OracleProxyAccount
WITH
     IDENTITY = 'oracle_username',
     SECRET = 'oracle_password' ;

CREATE EXTERNAL DATA SOURCE MyOracleServer
WITH
  ( LOCATION = 'oracle://145.145.145.145:1521',
    CREDENTIAL = OracleProxyAccount,
    PUSHDOWN = ON
  ) ;
```

MongoDB와 같은 다른 데이터 원본에 대한 추가 예제는 [MongoDB에서 외부 데이터에 액세스하도록 PolyBase 구성][mongodb_pb]을 참조하세요.

### <a name="b-create-external-data-source-to-reference-hadoop"></a>B. Hadoop를 참조하는 외부 데이터 원본 만들기

Hortonworks 또는 Cloudera Hadoop 클러스터를 참조하는 외부 데이터 원본을 만들려면 머신 이름 또는 Hadoop `Namenode` 및 포트의 IP 주소를 지정합니다. <!-- Provide the Nameservice ID as the `LOCATION` for highly available configurations. -->

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
  ( LOCATION = 'hdfs://10.10.10.10:8050' ,
    TYPE = HADOOP
  ) ;
```

### <a name="c-create-external-data-source-to-reference-hadoop-with-push-down-enabled"></a>C. 푸시 다운이 활성화된 상태에서 Hadoop를 참조하는 외부 데이터 원본 만들기

`RESOURCE_MANAGER_LOCATION` 옵션을 지정하여 PolyBase 쿼리에 대한 Hadoop 계산 푸시 다운을 활성화합니다. 활성화되면 PolyBase는 쿼리 계산을 Hadoop에 푸시해야 하는지 여부를 결정하기 위해 비용 기반 결정을 내립니다.

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
  ( LOCATION = 'hdfs://10.10.10.10:8020' ,
    TYPE = HADOOP ,
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
  ) ;
```

### <a name="d-create-external-data-source-to-reference-kerberos-secured-hadoop"></a>D. Kerberos 보안 Hadoop를 참조하는 외부 데이터 원본 만들기

Hadoop 클러스터가 Kerberos 보안 방식인지 확인하려면 Hadoop core-site.xml에서 hadoop.security.authentication 속성의 값을 확인합니다. Kerberos 보안 Hadoop 클러스터를 확인하려면 Kerberos 사용자 이름과 암호를 포함한 데이터베이스 범위 자격 증명을 지정해야 합니다. 데이터베이스 범위 자격 증명 비밀을 암호화하는 데에는 데이터베이스 마스터 키가 사용됩니다.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo' ;

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
WITH
     IDENTITY = '<hadoop_user_name>',
     SECRET = '<hadoop_password>' ;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
  ( LOCATION = 'hdfs://10.10.10.10:8050' ,
    CREDENTIAL = HadoopUser1 ,
    TYPE = HADOOP ,
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
  );
```

### <a name="e-create-external-data-source-to-access-data-in-azure-storage-using-the-wasb-interface"></a>E. wasb://인터페이스를 사용하여 Azure Storage의 데이터에 액세스하는 외부 데이터 원본 만들기
이 예제에서 외부 데이터 원본은 `logs`라는 Azure V2 Storage 계정입니다. 컨테이너는 `daily`입니다. Azure Storage 외부 데이터 원본은 데이터 전송 전용입니다. 조건자 푸시 다운을 지원하지 않습니다. 계층 구조 네임스페이스는 `wasb://` 인터페이스를 통해 데이터에 액세스하는 경우 지원되지 않습니다.

이 예제에서는 Azure V2 Storage 계정에 대한 인증을 위해 데이터베이스 범위 자격 증명을 만드는 방법을 보여 줍니다. 데이터베이스 자격 증명 비밀에 Azure Storage 계정 키를 지정합니다. Azure Storage에 대한 인증 중에는 사용되지 않으므로 데이터베이스 범위 지정 자격 증명 ID에 문자열을 지정할 수 있습니다.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo' ;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
  IDENTITY = '<my_account>' ,
  SECRET = '<azure_storage_account_key>' ;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage
WITH
  ( LOCATION = 'wasbs://daily@logs.blob.core.windows.net/' ,
    CREDENTIAL = AzureStorageCredential ,
    TYPE = HADOOP
  ) ;
```

### <a name="f-create-external-data-source-to-reference-a-sql-server-named-instance-via-polybase-connectivity-sql-server-2019"></a>F. Polybase 연결을 통해 SQL Server 명명된 인스턴스를 참조하는 외부 데이터 원본 만들기([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)])

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 명명된 인스턴스를 참조하는 외부 데이터 원본을 만들려면 CONNECTION_OPTIONS를 사용하여 인스턴스 이름을 지정하면 됩니다. 아래 예제에서 `WINSQL2019`는 호스트 이름이고 `SQL2019`는 인스턴스 이름입니다.

```sql
CREATE EXTERNAL DATA SOURCE SQLServerInstance2
WITH (
  LOCATION = 'sqlserver://WINSQL2019' ,
  CONNECTION_OPTIONS = 'Server=%s\SQL2019' ,
  CREDENTIAL = SQLServerCredentials
) ;
```

또는 포트를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있습니다.

```sql
CREATE EXTERNAL DATA SOURCE SQLServerInstance2
WITH (
  LOCATION = 'sqlserver://WINSQL2019:58137' ,
  CREDENTIAL = SQLServerCredentials
) ;
```

### <a name="g-create-external-data-source-to-reference-kafka"></a>G. Kafka를 참조하는 외부 데이터 원본 만들기

이 예제에서 외부 데이터 원본은 IP 주소가 xxx.xxx.xxx.xxx이고 포트 1900에서 수신 대기하는 Kafak 서버입니다. Kafka 외부 데이터 원본은 데이터 스트리밍 전용이며 조건자 푸시다운을 지원하지 않습니다.

```sql
-- Create an External Data Source for Kafka
CREATE EXTERNAL DATA SOURCE MyKafkaServer WITH (
    LOCATION = 'kafka://xxx.xxx.xxx.xxx:1900'
)
go
```

### <a name="h-create-external-data-source-to-reference-edgehub"></a>H. EdgeHub를 참조하는 외부 데이터 원본 만들기

이 예제에서 외부 데이터 원본은 Azure SQL Edge와 동일한 에지 디바이스에서 실행되는 EdgeHub입니다. EdgeHub 외부 데이터 원본은 데이터 스트리밍 전용이며 조건자 푸시다운을 지원하지 않습니다.

```sql
-- Create an External Data Source for Kafka
CREATE EXTERNAL DATA SOURCE MyEdgeHub WITH (
    LOCATION = 'edgehub://'
)
go
```

## <a name="examples-bulk-operations"></a>예제: 대량 작업

> [!IMPORTANT]
> 대량 작업을 위해 외부 데이터 원본을 구성할 때 `LOCATION` URL 끝에 추적 **/** , 파일 이름 또는 공유 액세스 서명 매개 변수를 추가하지 마세요.

### <a name="i-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-storage"></a>9\. Azure Storage에서 데이터를 검색하는 대량 작업을 위한 외부 데이터 원본 만들기

**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
[BULK INSERT][bulk_insert] 또는 [OPENROWSET][openrowset]을 사용하여 대량 작업에 대한 다음 데이터 원본을 만듭니다. 자격 증명은 `SHARED ACCESS SIGNATURE`를 ID로 설정해야 하며 SAS 토큰에서 앞에 `?`가 없어야 하며, 적어도 로드할 파일에 대한 읽기 권한이 있어야 하고(예: `srt=o&sp=r`) 만료 기간이 유효해야 합니다(모든 날짜는 UTC 시간임). 공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용][sas_token]을 참조하세요.

```sql
CREATE DATABASE SCOPED CREDENTIAL AccessAzureInvoices
WITH
  IDENTITY = 'SHARED ACCESS SIGNATURE',
  -- Remove ? from the beginning of the SAS token
  SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************' ;

CREATE EXTERNAL DATA SOURCE MyAzureInvoices
WITH
  ( LOCATION = 'https://newinvoices.blob.core.windows.net/week3' ,
    CREDENTIAL = AccessAzureInvoices ,
    TYPE = BLOB_STORAGE
  ) ;
```

이 예제를 사용하는 방법에 대한 자세한 내용은 [BULK INSERT][bulk_insert_example] 예제를 참조하세요.

## <a name="see-also"></a>참고 항목

- [ALTER EXTERNAL DATA SOURCE(Transact-SQL)][alter_eds]
- [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)][create_dsc]
- [CREATE EXTERNAL FILE FORMAT(Transact-SQL)][create_eff]
- [CREATE EXTERNAL TABLE(Transact-SQL)][create_etb]
- [sys.external_data_sources(Transact-SQL)][cat_eds]
- [SAS(공유 액세스 서명) 사용][sas_token]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: ./bulk-insert-transact-sql.md
[bulk_insert_example]: ./bulk-insert-transact-sql.md#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: ../functions/openrowset-transact-sql.md

[create_dsc]: ./create-database-scoped-credential-transact-sql.md
[create_eff]: ./create-external-file-format-transact-sql.md
[create_etb]: ./create-external-table-transact-sql.md
[create_etb_as_sel]: ./create-external-table-as-select-transact-sql.md?view=azure-sqldw-latest
[create_tbl_as_sel]: ./create-table-as-select-azure-sql-data-warehouse.md?view=azure-sqldw-latest

[alter_eds]: ./alter-external-data-source-transact-sql.md

[cat_eds]: ../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md
<!-- PolyBase docs -->
[intro_pb]: ../../relational-databases/polybase/polybase-guide.md
[mongodb_pb]: ../../relational-databases/polybase/polybase-configure-mongodb.md
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: ../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md
[hint_pb]: ../../relational-databases/polybase/polybase-pushdown-computation.md#force-pushdown

<!-- Azure Docs -->
[sas_token]: /azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
::: moniker range="=azuresqldb-current"

:::row:::
    :::column:::
        [SQL Server](create-external-data-source-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        **_\* SQL Database \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Azure Synapse<br />분석](create-external-data-source-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](create-external-data-source-transact-sql.md?view=aps-pdw-2016-au7)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-azure-sql-database"></a>개요: Azure SQL Database

탄력적 쿼리에 대한 외부 데이터 원본을 만듭니다. 외부 데이터 원본은 연결을 설정하고 다음과 같은 기본 사용 사례를 지원하는 데 사용됩니다.

- `BULK INSERT` 또는 `OPENROWSET`를 사용한 대량 로드 작업
- [탄력적 쿼리][remote_eq]로 SQL Database를 사용하여 원격 SQL Database 또는 Azure Synapse 인스턴스 쿼리
- [탄력적 쿼리][sharded_eq]를 사용하여 분할된 Azure SQL Database 쿼리

## <a name="syntax"></a>구문

```syntaxsql
CREATE EXTERNAL DATA SOURCE <data_source_name>
WITH
  ( [ LOCATION = '<prefix>://<path>[:<port>]' ]
    [ [ , ] CREDENTIAL = <credential_name> ]
    [ [ , ] TYPE = { BLOB_STORAGE | RDBMS | SHARD_MAP_MANAGER } ]
    [ [ , ] DATABASE_NAME = '<database_name>' ]
    [ [ , ] SHARD_MAP_NAME = '<shard_map_manager>' ] )
[ ; ]
```

## <a name="arguments"></a>인수

### <a name="data_source_name"></a>data_source_name

데이터 원본에 대한 사용자 정의 이름을 지정합니다. 이름은 SQL 데이터베이스의 데이터베이스 내에서 고유해야 합니다.

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

외부 데이터 원본에 대한 연결 프로토콜 및 경로를 제공합니다.

| 외부 데이터 원본   | 위치 접두사 | 위치 경로                                         |
| ---------------------- | --------------- | ----------------------------------------------------- |
| 대량 작업        | `https`         | `<storage_account>.blob.core.windows.net/<container>` |
| 탄력적 쿼리(분할)  | 필요하지 않음    | `<shard_map_server_name>.database.windows.net`        |
| 탄력적 쿼리(원격) | 필요하지 않음    | `<remote_server_name>.database.windows.net`           |

위치 경로:

- `<shard_map_server_name>` = 분할된 맵 관리자를 호스팅하는 Azure의 논리 서버 이름입니다. `DATABASE_NAME` 인수는 분할된 맵을 호스트하는 데 사용되는 데이터베이스를 제공하고 `SHARD_MAP_NAME`은 분할된 맵 자체에 사용됩니다.
- `<remote_server_name>` = 탄력적 쿼리에 대한 대상 논리 서버 이름입니다. 데이터베이스 이름은 `DATABASE_NAME` 인수를 사용하여 지정됩니다.

위치 설정 시 추가 참고 사항 및 지침:

- [!INCLUDE[ssde_md](../../includes/ssde_md.md)]에서는 개체가 생성될 때 외부 데이터 원본이 존재하는지 확인하지 않습니다. 유효성을 검사하려면 외부 데이터 원본을 사용하여 외부 테이블을 만듭니다.

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

외부 데이터 원본에 대해 인증하기 위한 데이터베이스 범위 자격 증명을 지정합니다.

자격 증명 생성 시 추가 참고 사항 및 지침:

- Azure Storage에서 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]로 데이터를 로드하려면 SAS 토큰(공유 액세스 서명)을 사용합니다.
- `CREDENTIAL`은 데이터 보안이 설정된 경우에만 필요합니다. 익명 액세스를 허용하는 데이터 세트에는 `CREDENTIAL`이 필요하지 않습니다.
- `TYPE` = `BLOB_STORAGE`가 ID로 `SHARED ACCESS SIGNATURE`를 사용하여 자격 증명을 만들어야 하는 경우 또한 SAS 토큰은 다음과 같이 구성되어야 합니다.
  - 비밀로 구성된 경우 앞에 오는 `?` 제외
  - 로드해야 하는 파일에 대해 적어도 읽기 권한이 있어야 합니다(예: `srt=o&sp=r`).
  - 유효한 만료 기간을 사용합니다(모든 날짜는 UTC 시간임).

`SHARED ACCESS SIGNATURE` 및 `TYPE` = `BLOB_STORAGE`에서 `CREDENTIAL`을 사용하는 예제는 [대량 작업을 실행하고 Azure Storage에서 SQL Database로 데이터를 검색하기 위한 외부 데이터 원본 만들기](#c-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-storage)를 참조하세요.

데이터베이스 범위 지정 자격 증명을 만들려면 [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)][create_dsc]을 참조하세요.

### <a name="type---blob_storage--rdbms--shard_map_manager"></a>TYPE = *[ BLOB_STORAGE | RDBMS | SHARD_MAP_MANAGER]*

구성 중인 외부 데이터 원본의 유형을 지정합니다. 이 매개 변수가 항상 필요한 것은 아닙니다.

- SQL Database에서 탄력적 쿼리를 통해 데이터베이스 간 쿼리에 `RDBMS`를 사용합니다.
- 분할된 SQL Database에 연결할 때 외부 데이터 원본을 만드는 경우 `SHARD_MAP_MANAGER`를 사용합니다.
- [BULK INSERT][bulk_insert] 또는 [OPENROWSET][openrowset]를 통해 대량 작업을 실행하는 경우 `BLOB_STORAGE`를 사용합니다.

> [!IMPORTANT]
> 기타 외부 데이터 원본을 사용하는 경우 `TYPE`을 설정하지 마세요.

### <a name="database_name--database_name"></a>DATABASE_NAME = *database_name*

`TYPE`이 `RDBMS` 또는 `SHARD_MAP_MANAGER`로 설정된 경우 이 인수를 구성합니다.

| TYPE              | DATABASE_NAME의 값                                       |
| ----------------- | ------------------------------------------------------------ |
| RDBMS             | `LOCATION`을 사용하여 제공된 서버의 원격 데이터베이스 이름 |
| SHARD_MAP_MANAGER | 분할된 맵 관리자로 작동하는 데이터베이스의 이름      |

`TYPE` = `RDBMS`인 외부 데이터 원본을 만드는 방법을 보여 주는 예제는 [RDBMS 외부 데이터 원본 만들기](#b-create-an-rdbms-external-data-source)를 참조하세요.

### <a name="shard_map_name--shard_map_name"></a>SHARD_MAP_NAME = *shard_map_name*

`TYPE` 인수가 `SHARD_MAP_MANAGER`로 설정된 경우에만 분할된 맵의 이름을 설정하는 데 사용됩니다.

`TYPE` = `SHARD_MAP_MANAGER`인 외부 데이터 원본을 만드는 방법을 보여 주는 예제는 [분할된 데이터베이스 맵 관리자 외부 데이터 원본 만들기](#a-create-a-shard-map-manager-external-data-source)를 참조하세요.

## <a name="permissions"></a>사용 권한

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 데이터베이스에 대한 `CONTROL` 권한이 필요합니다.

## <a name="locking"></a>잠금

`EXTERNAL DATA SOURCE` 개체에 대한 공유 잠금을 수행합니다.

## <a name="examples"></a>예제:

### <a name="a-create-a-shard-map-manager-external-data-source"></a>A. 분할된 맵 관리자 외부 데이터 원본 만들기

SHARD_MAP_MANAGER를 참조하는 외부 데이터 원본을 만들려면 가상 머신의 SQL Database 또는 SQL Server 데이터베이스에서 분할된 맵 관리자를 호스트하는 SQL Database 서버 이름을 지정합니다.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>' ;

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
WITH
  IDENTITY = '<username>',
  SECRET = '<password>' ;

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc
WITH
  ( TYPE = SHARD_MAP_MANAGER ,
    LOCATION = '<server_name>.database.windows.net' ,
    DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb' ,
    CREDENTIAL = ElasticDBQueryCred ,
    SHARD_MAP_NAME = 'CustomerIDShardMap'
  ) ;
```

단계별 자습서는 [분할을 위한 탄력적 쿼리 시작(수평 분할)][sharded_eq_tutorial]을 참조하세요.

### <a name="b-create-an-rdbms-external-data-source"></a>B. RDBMS 외부 데이터 원본 만들기

RDBMS를 참조하는 외부 데이터 원본을 만들려면 SQL Database에 있는 원격 데이터베이스의 SQL Database 서버 이름을 지정합니다.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>' ;

CREATE DATABASE SCOPED CREDENTIAL SQL_Credential
WITH
  IDENTITY = '<username>' ,
  SECRET = '<password>' ;

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc
WITH
  ( TYPE = RDBMS ,
    LOCATION = '<server_name>.database.windows.net' ,
    DATABASE_NAME = 'Customers' ,
    CREDENTIAL = SQL_Credential
  ) ;
```

RDBMS에 대한 단계별 자습서는 [데이터베이스 간 쿼리 시작(수직 분할)][remote_eq_tutorial]을 참조하세요.

## <a name="examples-bulk-operations"></a>예제: 대량 작업

> [!IMPORTANT]
> 대량 작업을 위해 외부 데이터 원본을 구성할 때 `LOCATION` URL 끝에 추적 **/** , 파일 이름 또는 공유 액세스 서명 매개 변수를 추가하지 마세요.

### <a name="c-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-storage"></a>C. Azure Storage에서 데이터를 검색하는 대량 작업을 위한 외부 데이터 원본 만들기

[BULK INSERT][bulk_insert] 또는 [OPENROWSET][openrowset]을 사용하여 대량 작업에 대한 다음 데이터 원본을 만듭니다. 자격 증명은 `SHARED ACCESS SIGNATURE`를 ID로 설정해야 하며 SAS 토큰에서 앞에 `?`가 없어야 하며, 적어도 로드할 파일에 대한 읽기 권한이 있어야 하고(예: `srt=o&sp=r`) 만료 기간이 유효해야 합니다(모든 날짜는 UTC 시간임). 공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용][sas_token]을 참조하세요.

```sql
CREATE DATABASE SCOPED CREDENTIAL AccessAzureInvoices
WITH
  IDENTITY = 'SHARED ACCESS SIGNATURE',
  -- Remove ? from the beginning of the SAS token
  SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************' ;

CREATE EXTERNAL DATA SOURCE MyAzureInvoices
WITH
  ( LOCATION = 'https://newinvoices.blob.core.windows.net/week3' ,
    CREDENTIAL = AccessAzureInvoices ,
    TYPE = BLOB_STORAGE
  ) ;
```

사용 중인 이 예제를 보려면 [BULK INSERT][bulk_insert_example]를 참조하세요.

## <a name="see-also"></a>참고 항목

- [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)][create_dsc]
- [CREATE EXTERNAL TABLE(Transact-SQL)][create_etb]
- [sys.external_data_sources(Transact-SQL)][cat_eds]
- [SAS(공유 액세스 서명) 사용][sas_token]
- [탄력적 쿼리 소개][intro_eq]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: ./bulk-insert-transact-sql.md
[bulk_insert_example]: ./bulk-insert-transact-sql.md#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: ../functions/openrowset-transact-sql.md
[create_dsc]: ./create-database-scoped-credential-transact-sql.md
[create_etb]: https://docs.microsoft.com/sql/t-sql/statements/create-external-data-source
[alter_eds]: ./alter-external-data-source-transact-sql.md
[cat_eds]: ../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md
<!-- PolyBase docs -->
[intro_pb]: ../../relational-databases/polybase/polybase-guide.md
[mongodb_pb]: ../../relational-databases/polybase/polybase-configure-mongodb.md
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: ../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md
[hint_pb]: ../../relational-databases/polybase/polybase-pushdown-computation.md#force-pushdown
<!-- Elastic Query Docs -->
[intro_eq]: /azure/azure-sql/database/elastic-query-overview
[remote_eq]: /azure/azure-sql/database/elastic-query-getting-started-vertical
[remote_eq_tutorial]: /azure/azure-sql/database/elastic-query-getting-started-vertical
[sharded_eq]: /azure/azure-sql/database/elastic-query-getting-started
[sharded_eq_tutorial]: /azure/azure-sql/database/elastic-query-getting-started

<!-- Azure Docs -->
[azure_ad]: /azure/data-lake-store/data-lake-store-authenticate-using-active-directory
[sas_token]: /azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
::: moniker range="=azure-sqldw-latest"

:::row:::
    :::column:::
        [SQL Server](create-external-data-source-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](create-external-data-source-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />분석 \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](create-external-data-source-transact-sql.md?view=aps-pdw-2016-au7)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-azure-synapse-analytics"></a>개요: Azure Synapse Analytics

PolyBase에 대한 외부 데이터 원본을 만듭니다. 외부 데이터 원본은 연결을 설정하고 다음과 같은 기본 사용 사례를 지원하는 데 사용됩니다. [PolyBase][intro_pb]를 사용하여 데이터 가상화 및 데이터 로드

> [!IMPORTANT]  
> [탄력적 쿼리][remote_eq]로 Azure SQL Database를 사용하여 SQL Analytics 리소스를 쿼리하는 외부 데이터 원본을 만들려면 [SQL Database](create-external-data-source-transact-sql.md?view=azuresqldb-current)를 참조하세요.

## <a name="syntax"></a>구문

### [[!INCLUDE[sss-dedicated-pool-md.md](../../includes/sss-dedicated-pool-md.md)]](#tab/dedicated)
```syntaxsql
CREATE EXTERNAL DATA SOURCE <data_source_name>
WITH
  ( [ LOCATION = '<prefix>://<path>[:<port>]' ]
    [ [ , ] CREDENTIAL = <credential_name> ]
    [ [ , ] TYPE = HADOOP ]
[ ; ]
```
### [[!INCLUDE[sssod-md.md](../../includes/sssod-md.md)]](#tab/serverless)
```syntaxsql
CREATE EXTERNAL DATA SOURCE <data_source_name>  
WITH
(    LOCATION = '<prefix>://<path>[:<port>]'
) 
[;]
```
---

## <a name="arguments"></a>인수

### <a name="data_source_name"></a>data_source_name

데이터 원본에 대한 사용자 정의 이름을 지정합니다. 이름은 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 내에서 고유해야 합니다.

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

외부 데이터 원본에 대한 연결 프로토콜 및 경로를 제공합니다.

| 외부 데이터 원본        | 위치 접두사 | 위치 경로                                         |
| --------------------------- | --------------- | ----------------------------------------------------- |
| Azure Data Lake Store Gen 1 | `adl`           | `<storage_account>.azuredatalake.net`                 |
| Azure Data Lake Store Gen 2 | `abfs[s]`       | `<container>@<storage_account>.dfs.core.windows.net`  |
| Azure V2 Storage 계정    | `wasb[s]`       | `<container>@<storage_account>.blob.core.windows.net` |

위치 경로:

- `<container>` = 데이터를 보관하는 스토리지 계정의 컨테이너입니다. 루트 컨테이너는 읽기 전용이므로 데이터를 컨테이너에 다시 쓸 수 없습니다.
- `<storage_account>` = Azure 리소스의 스토리지 계정 이름입니다.

위치 설정 시 추가 참고 사항 및 지침:

- Azure Data Lake Storage Gen 2를 프로비저닝할 때 기본 옵션은 `enable secure SSL connections`를 사용하는 것입니다. 이 기능을 사용하도록 설정한 경우 보안 TLS/SSL 연결을 선택할 때 `abfss`를 사용해야 합니다. `abfss`는 보안되지 않은 TLS/ 연결에서도 작동합니다.
- Azure Synapse는 개체가 생성될 때 외부 데이터 원본이 존재하는지 확인하지 않습니다. . 유효성을 검사하려면 외부 데이터 원본을 사용하여 외부 테이블을 만듭니다.
- 일관된 쿼리 의미 체계를 보장하기 위해 Hadoop을 쿼리할 때 모든 테이블에 대해 동일한 외부 데이터 원본을 사용합니다.
- `wasbs`는 데이터가 보안 TLS 연결을 사용하여 전송되므로 권장됩니다.
- 계층 구조 네임스페이스는 wasb:// 인터페이스를 사용하여 PolyBase를 통해 데이터에 액세스하는 경우 Azure V2 Storage 계정에서 지원되지 않습니다.

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

외부 데이터 원본에 대해 인증하기 위한 데이터베이스 범위 자격 증명을 지정합니다.

자격 증명 생성 시 추가 참고 사항 및 지침:

- Azure Storage 또는 ADLS(Azure Data Lake Store) Gen 2에서 Azure Synapse Analytics로 데이터를 로드하려면 Azure Storage 키를 사용합니다.
- `CREDENTIAL`은 데이터 보안이 설정된 경우에만 필요합니다. 익명 액세스를 허용하는 데이터 세트에는 `CREDENTIAL`이 필요하지 않습니다.

데이터베이스 범위 지정 자격 증명을 만들려면 [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)][create_dsc]을 참조하세요.

### <a name="type--hadoop"></a>TYPE = *HADOOP*

구성 중인 외부 데이터 원본의 유형을 지정합니다. 이 매개 변수가 항상 필요한 것은 아닙니다.

- 외부 데이터 원본이 Azure Storage, ADLS Gen 1 또는 ADLS Gen 2인 경우 HADOOP을 사용합니다.

`TYPE` = `HADOOP`을 사용하여 Azure Storage에서 데이터를 로드하는 방법에 대한 예제를 보려면 [서비스 주체를 사용하여 Azure Data Lake Store Gen 1 또는 2를 참조하는 외부 데이터 원본 만들기](#b-create-external-data-source-to-reference-azure-data-lake-store-gen-1-or-2-using-a-service-principal)를 참조하세요.

## <a name="permissions"></a>사용 권한

데이터베이스에 대한 `CONTROL` 권한이 필요합니다.

## <a name="locking"></a>잠금

`EXTERNAL DATA SOURCE` 개체에 대한 공유 잠금을 수행합니다.

## <a name="security"></a>보안

PolyBase는 대부분의 외부 데이터 원본에 대해 프록시 기반 인증을 지원합니다. 데이터베이스 범위 자격 증명을 생성하여 프록시 계정을 만듭니다.

SQL Server 빅 데이터 클러스터의 스토리지 또는 데이터 풀에 연결하면 사용자의 자격 증명이 백 엔드 시스템을 통해 전달됩니다. 통과 인증을 사용하도록 설정하려면 데이터 풀 자체의 로그인을 만듭니다.

현재 `HADOOP` 유형의 SAS 토큰이 지원되지 않습니다. 스토리지 계정 액세스 키에서만 지원됩니다. `HADOOP` 유형 및 SAS 자격 증명으로 외부 데이터 원본을 만들려고 하면 다음 오류로 인해 실패합니다.

`Msg 105019, Level 16, State 1 - EXTERNAL TABLE access failed due to internal error: 'Java exception raised on call to HdfsBridge_Connect. Java exception message: Parameters provided to connect to the Azure storage account are not valid.: Error [Parameters provided to connect to the Azure storage account are not valid.] occurred while accessing external file.'`

## <a name="examples"></a>예제:

### <a name="a-create-external-data-source-to-access-data-in-azure-storage-using-the-wasb-interface"></a>A. wasb://인터페이스를 사용하여 Azure Storage의 데이터에 액세스하는 외부 데이터 원본 만들기
이 예제에서 외부 데이터 원본은 `logs`라는 Azure V2 Storage 계정입니다. 컨테이너는 `daily`입니다. Azure Storage 외부 데이터 원본은 데이터 전송 전용입니다. 조건자 푸시 다운을 지원하지 않습니다. 계층 구조 네임스페이스는 `wasb://` 인터페이스를 통해 데이터에 액세스하는 경우 지원되지 않습니다.

이 예제에서는 Azure Storage에 대한 인증을 위해 데이터베이스 범위 자격 증명을 만드는 방법을 보여 줍니다. 데이터베이스 자격 증명 비밀에 Azure Storage 계정 키를 지정합니다. Azure 스토리지에 대한 인증 중에는 사용되지 않으므로 데이터베이스 범위 지정 자격 증명 ID에 문자열을 지정할 수 있습니다.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo' ;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
  IDENTITY = '<my_account>',
  SECRET = '<azure_storage_account_key>' ;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage
WITH
  ( LOCATION = 'wasbs://daily@logs.blob.core.windows.net/' ,
    CREDENTIAL = AzureStorageCredential ,
    TYPE = HADOOP
  ) ;
```

### <a name="b-create-external-data-source-to-reference-azure-data-lake-store-gen-1-or-2-using-a-service-principal"></a>B. Azure Data Lake Store Gen 1 또는 2를 참조하거나 서비스 주체를 사용하여 외부 데이터 소스를 생성합니다.

Azure Data Lake Store 연결은 ADLS URI 및 Azure Active Directory 애플리케이션의 서비스 주체를 기반으로 할 수 있습니다. 이 애플리케이션을 만들기 위한 설명서는 [Active Directory를 사용한 Data Lake Store 인증][azure_ad]에서 찾을 수 있습니다.

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>' ;

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLS_credential
WITH
  -- IDENTITY = '<clientID>@<OAuth2.0TokenEndPoint>' ,
  IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token' ,
  -- SECRET = '<KEY>'
  SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI=' 
;

-- For Gen 1 - Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Storage.
-- LOCATION: Provide Data Lake Storage Gen 1 account name and URI
-- CREDENTIAL: Provide the credential created in the previous step
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH
  ( LOCATION = 'adl://newyorktaxidataset.azuredatalakestore.net' ,
    CREDENTIAL = ADLS_credential ,
    TYPE = HADOOP
  ) ;

-- For Gen 2 - Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Storage.
-- LOCATION: Provide Data Lake Storage Gen 2 account name and URI
-- CREDENTIAL: Provide the credential created in the previous step
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH
  -- Please note the abfss endpoint when your account has secure transfer enabled
  ( LOCATION = 'abfss://data@newyorktaxidataset.dfs.core.windows.net' , 
    CREDENTIAL = ADLS_credential ,
    TYPE = HADOOP
  ) ;
```

### <a name="c-create-external-data-source-to-reference-azure-data-lake-store-gen-2-using-the-storage-account-key"></a>C. Azure Data Lake Store Gen 2를 참조하거나 스토리지 계정 키를 사용하여 외부 데이터 소스를 생성합니다.

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>' ;

CREATE DATABASE SCOPED CREDENTIAL ADLS_credential
WITH
-- IDENTITY = '<storage_account_name>' ,
  IDENTITY = 'newyorktaxidata' ,
-- SECRET = '<storage_account_key>'
  SECRET = 'yz5N4+bxSb89McdiysJAzo+9hgEHcJRJuXbF/uC3mhbezES/oe00vXnZEl14U0lN3vxrFKsphKov16C0w6aiTQ=='
;

-- Note this example uses a Gen 2 secured endpoint (abfss)
CREATE EXTERNAL DATA SOURCE <data_source_name>
WITH
  ( LOCATION = 'abfss://2013@newyorktaxidataset.dfs.core.windows.net' ,
    CREDENTIAL = ADLS_credential ,
    TYPE = HADOOP
  ) ;
```

### <a name="d-create-external-data-source-to-reference-polybase-connectivity-to-azure-data-lake-store-gen-2-using-abfs"></a>D. abfs://를 사용하여 Azure Data Lake Store Gen 2에 대한 Polybase 연결을 참조하는 외부 데이터 원본 만들기

[관리 ID](/azure/active-directory/managed-identities-azure-resources/overview
) 메커니즘으로 Azure Data Lake Store Gen2 계정에 연결할 경우 SECRET을 지정할 필요가 없습니다.

```sql
-- If you do not have a Master Key on your DW you will need to create one
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>' ;

--Create database scoped credential with **IDENTITY = 'Managed Service Identity'**

CREATE DATABASE SCOPED CREDENTIAL msi_cred 
WITH IDENTITY = 'Managed Service Identity' ;

--Create external data source with abfss:// scheme for connecting to your Azure Data Lake Store Gen2 account

CREATE EXTERNAL DATA SOURCE ext_datasource_with_abfss 
WITH 
  ( TYPE = HADOOP , 
    LOCATION = 'abfss://myfile@mystorageaccount.dfs.core.windows.net' , 
    CREDENTIAL = msi_cred
  ) ;
```

## <a name="see-also"></a>참고 항목

- [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)][create_dsc]
- [CREATE EXTERNAL FILE FORMAT(Transact-SQL)][create_eff]
- [CREATE EXTERNAL TABLE(Transact-SQL)][create_etb]
- [CREATE EXTERNAL TABLE AS SELECT(Azure Synapse Analytics)][create_etb_as_sel]
- [CREATE TABLE AS SELECT(Azure Synapse Analytics)][create_tbl_as_sel]
- [sys.external_data_sources(Transact-SQL)][cat_eds]
- [SAS(공유 액세스 서명) 사용][sas_token]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: ./bulk-insert-transact-sql.md
[bulk_insert_example]: ./bulk-insert-transact-sql.md#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: ../functions/openrowset-transact-sql.md

[create_dsc]: ./create-database-scoped-credential-transact-sql.md
[create_eff]: ./create-external-file-format-transact-sql.md
[create_etb]: https://docs.microsoft.com/sql/t-sql/statements/create-external-data-source
[create_etb_as_sel]: ./create-external-table-as-select-transact-sql.md?view=azure-sqldw-latest
[create_tbl_as_sel]: ./create-table-as-select-azure-sql-data-warehouse.md?view=azure-sqldw-latest

[alter_eds]: ./alter-external-data-source-transact-sql.md

[cat_eds]: ../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md
<!-- PolyBase docs -->
[intro_pb]: ../../relational-databases/polybase/polybase-guide.md
[mongodb_pb]: ../../relational-databases/polybase/polybase-configure-mongodb.md
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: ../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md
[hint_pb]: ../../relational-databases/polybase/polybase-pushdown-computation.md#force-pushdown
<!-- Elastic Query Docs -->
[intro_eq]: /azure/azure-sql/database/elastic-query-overview
[remote_eq]: /azure/azure-sql/database/elastic-query-getting-started-vertical
[remote_eq_tutorial]: /azure/azure-sql/database/elastic-query-getting-started-vertical
[sharded_eq]: /azure/azure-sql/database/elastic-query-getting-started
[sharded_eq_tutorial]: /azure/azure-sql/database/elastic-query-getting-started

<!-- Azure Docs -->
[azure_ad]: /azure/data-lake-store/data-lake-store-authenticate-using-active-directory
[sas_token]: /azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
::: moniker range=">=aps-pdw-2016"

:::row:::
    :::column:::
        [SQL Server](create-external-data-source-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](create-external-data-source-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />분석](create-external-data-source-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        **_\* Analytics<br />Platform System(PDW) \*_** &nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="overview-analytics-platform-system"></a>개요: 분석 플랫폼 시스템

PolyBase 쿼리에 대한 외부 데이터 원본을 만듭니다. 외부 데이터 원본은 연결을 설정하고 다음과 같은 사용 사례를 지원하는 데 사용됩니다. [PolyBase][intro_pb]를 사용하여 데이터 가상화 및 데이터 로드

## <a name="syntax"></a>구문

```syntaxsql
CREATE EXTERNAL DATA SOURCE <data_source_name>
WITH
  ( [ LOCATION = '<prefix>://<path>[:<port>]' ]
    [ [ , ] CREDENTIAL = <credential_name> ]
    [ [ , ] TYPE = HADOOP ]
    [ [ , ] RESOURCE_MANAGER_LOCATION = '<resource_manager>[:<port>]' )
[ ; ]
```

## <a name="arguments"></a>인수

### <a name="data_source_name"></a>data_source_name

데이터 원본에 대한 사용자 정의 이름을 지정합니다. 이름은 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]의 서버 내에서 고유해야 합니다.

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

외부 데이터 원본에 대한 연결 프로토콜 및 경로를 제공합니다.

| 외부 데이터 원본    | 위치 접두사 | 위치 경로                                         |
| ----------------------- | --------------- | ----------------------------------------------------- |
| Cloudera 또는 Hortonworks | `hdfs`          | `<Namenode>[:port]`                                   |
| Azure Storage 계정   | `wasb[s]`       | `<container>@<storage_account>.blob.core.windows.net` |

위치 경로:

- `<Namenode>` = Hadoop 클러스터에 있는 `Namenode`의 머신 이름, 이름 서비스 URI 또는 IP 주소입니다. PolyBase는 Hadoop 클러스터에서 사용하는 모든 DNS 이름을 확인해야 합니다. <!-- For highly available Hadoop configurations, provide the Nameservice ID as the `LOCATION`. -->
- `port` = 외부 데이터 원본이 수신 대기 중인 포트입니다. Hadoop에서는 `fs.defaultFS` 구성 매개 변수를 사용하여 포트를 찾을 수 있습니다. 기본값은 8020입니다.
- `<container>` = 데이터를 보관하는 스토리지 계정의 컨테이너입니다. 루트 컨테이너는 읽기 전용이므로 데이터를 컨테이너에 다시 쓸 수 없습니다.
- `<storage_account>` = Azure 리소스의 스토리지 계정 이름입니다.

위치 설정 시 추가 참고 사항 및 지침:

- PDW 엔진은 개체가 생성될 때 외부 데이터 원본이 존재하는지 확인하지 않습니다. 유효성을 검사하려면 외부 데이터 원본을 사용하여 외부 테이블을 만듭니다.
- 일관된 쿼리 의미 체계를 보장하기 위해 Hadoop을 쿼리할 때 모든 테이블에 대해 동일한 외부 데이터 원본을 사용합니다.
- `wasbs`는 데이터가 보안 TLS 연결을 사용하여 전송되므로 권장됩니다.
- 계층 구조 네임스페이스는 wasb://를 통해 Azure Storage 계정에서 사용하는 경우 지원되지 않습니다.
- Hadoop `Namenode` 장애 조치(failover) 중에 PolyBase 쿼리를 성공적으로 수행하려면 Hadoop 클러스터의 `Namenode`에 대한 가상 IP 주소 사용을 고려하세요. 그렇지 않은 경우 [ALTER EXTERNAL DATA SOURCE][alter_eds] 명령을 실행하여 새 위치를 가리킵니다.

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

외부 데이터 원본에 대해 인증하기 위한 데이터베이스 범위 자격 증명을 지정합니다.

자격 증명 생성 시 추가 참고 사항 및 지침:

- Azure Storage에서 Azure Synapse 또는 PDW로 데이터를 로드하려면 Azure Storage 키를 사용합니다.
- `CREDENTIAL`은 데이터 보안이 설정된 경우에만 필요합니다. 익명 액세스를 허용하는 데이터 세트에는 `CREDENTIAL`이 필요하지 않습니다.

### <a name="type---hadoop-"></a>TYPE = *[ HADOOP ]*

구성 중인 외부 데이터 원본의 유형을 지정합니다. 이 매개 변수가 항상 필요한 것은 아닙니다.

- 외부 데이터 원본이 Cloudera, Hortonworks 또는 Azure Storage이면 HADOOP을 사용합니다.

`TYPE` = `HADOOP`을 사용하여 Azure Storage에서 데이터를 로드하는 예제는 [Hadoop을 참조하는 외부 데이터 원본 만들기](#a-create-external-data-source-to-reference-hadoop)를 참조하세요.

### <a name="resource_manager_location--resourcemanager_uriport"></a>RESOURCE_MANAGER_LOCATION = *'ResourceManager_URI[:port]'*

Hortonworks 또는 Cloudera에 연결할 때 이 선택적 값을 구성합니다.

`RESOURCE_MANAGER_LOCATION`이 정의되면 쿼리 최적화 프로그램은 성능 향상을 위해 비용 기반 결정을 내립니다. MapReduce 작업을 사용하여 Hadoop으로 계산을 푸시 다운할 수 있습니다. `RESOURCE_MANAGER_LOCATION`을 지정하면 Hadoop과 SQL 간에 전송되는 데이터 양을 크게 줄여 쿼리 성능을 향상시킬 수 있습니다.

리소스 관리자를 지정하지 않은 경우 Hadoop에 대한 푸시 컴퓨팅은 PolyBase 쿼리에 대해 비활성화됩니다.

포트를 지정하지 않을 경우 기본값은 'hadoop 연결' 구성에 대한 현재 설정을 사용하여 선택됩니다.

| Hadoop 연결 | 기본 Resource Manager 포트 |
| ------------------- | ----------------------------- |
| 1                   | 50300                         |
| 2                   | 50300                         |
| 3                   | 8021                          |
| 4                   | 8032                          |
| 5                   | 8050                          |
| 6                   | 8032                          |
| 7                   | 8050                          |

지원되는 Hadoop 버전의 전체 목록은 [PolyBase 연결 구성(Transact-SQL)][connectivity_pb]을 참조하세요.

> [!IMPORTANT]
> 외부 데이터 원본을 만드는 경우에는 `RESOURCE_MANAGER_LOCATION` 값의 유효성이 검사되지 않습니다. 잘못된 값을 입력하면 제공된 값을 확인할 수 없으므로 푸시 다운을 시도할 때마다 실행 시 쿼리 오류가 발생할 수 있습니다.

[푸시 다운이 활성화된 Hadoop을 참조하는 외부 데이터 원본 만들기](#b-create-external-data-source-to-reference-hadoop-with-push-down-enabled)는 구체적인 예제와 추가 지침을 제공합니다.

## <a name="permissions"></a>사용 권한

[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]의 데이터베이스에 대한 `CONTROL` 권한이 필요합니다.

> [!NOTE]
> PDW의 이전 릴리스에서는 외부 데이터 원본을 만들려면 `ALTER ANY EXTERNAL DATA SOURCE` 권한이 필요했습니다.

## <a name="locking"></a>잠금

`EXTERNAL DATA SOURCE` 개체에 대한 공유 잠금을 수행합니다.

## <a name="security"></a>보안

PolyBase는 대부분의 외부 데이터 원본에 대해 프록시 기반 인증을 지원합니다. 데이터베이스 범위 자격 증명을 생성하여 프록시 계정을 만듭니다.

현재 `HADOOP` 유형의 SAS 토큰이 지원되지 않습니다. 스토리지 계정 액세스 키에서만 지원됩니다. `HADOOP` 유형 및 SAS 자격 증명으로 외부 데이터 원본을 만들려고 하면 다음 오류로 인해 실패합니다.

`Msg 105019, Level 16, State 1 - EXTERNAL TABLE access failed due to internal error: 'Java exception raised on call to HdfsBridge_Connect. Java exception message: Parameters provided to connect to the Azure storage account are not valid.: Error [Parameters provided to connect to the Azure storage account are not valid.] occurred while accessing external file.'`

## <a name="examples"></a>예제:

### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. Hadoop를 참조하는 외부 데이터 원본 만들기

Hortonworks 또는 Cloudera Hadoop 클러스터를 참조하는 외부 데이터 원본을 만들려면 머신 이름 또는 Hadoop `Namenode` 및 포트의 IP 주소를 지정합니다. <!-- Provide the Nameservice ID as the `LOCATION` for highly available configurations. -->

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
  ( LOCATION = 'hdfs://10.10.10.10:8050' ,
    TYPE = HADOOP
  ) ;
```

### <a name="b-create-external-data-source-to-reference-hadoop-with-push-down-enabled"></a>B. 푸시 다운이 활성화된 상태에서 Hadoop를 참조하는 외부 데이터 원본 만들기

`RESOURCE_MANAGER_LOCATION` 옵션을 지정하여 PolyBase 쿼리에 대한 Hadoop 계산 푸시 다운을 활성화합니다. 활성화되면 PolyBase는 쿼리 계산을 Hadoop에 푸시해야 하는지 여부를 결정하기 위해 비용 기반 결정을 내립니다.

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
  ( LOCATION = 'hdfs://10.10.10.10:8020'
    TYPE = HADOOP
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
) ;
```

### <a name="c-create-external-data-source-to-reference-kerberos-secured-hadoop"></a>C. Kerberos 보안 Hadoop를 참조하는 외부 데이터 원본 만들기

Hadoop 클러스터가 Kerberos 보안 방식인지 확인하려면 Hadoop core-site.xml에서 hadoop.security.authentication 속성의 값을 확인합니다. Kerberos 보안 Hadoop 클러스터를 확인하려면 Kerberos 사용자 이름과 암호를 포함한 데이터베이스 범위 자격 증명을 지정해야 합니다. 데이터베이스 범위 자격 증명 비밀을 암호화하는 데에는 데이터베이스 마스터 키가 사용됩니다.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo' ;

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
WITH
  IDENTITY = '<hadoop_user_name>' ,
  SECRET = '<hadoop_password>' ;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
  ( LOCATION = 'hdfs://10.10.10.10:8050' ,
    CREDENTIAL = HadoopUser1 ,
    TYPE = HADOOP ,
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
  ) ;
```

### <a name="d-create-external-data-source-to-access-data-in-azure-storage-using-the-wasb-interface"></a>D. wasb://인터페이스를 사용하여 Azure Storage의 데이터에 액세스하는 외부 데이터 원본 만들기

이 예제에서 외부 데이터 원본은 `logs`라는 Azure V2 Storage 계정입니다. 컨테이너는 `daily`입니다. Azure Storage 외부 데이터 원본은 데이터 전송 전용입니다. 조건자 푸시 다운을 지원하지 않습니다. 계층 구조 네임스페이스는 `wasb://` 인터페이스를 통해 데이터에 액세스하는 경우 지원되지 않습니다.

이 예제에서는 Azure Storage에 대한 인증을 위해 데이터베이스 범위 자격 증명을 만드는 방법을 보여 줍니다. 데이터베이스 자격 증명 비밀에 Azure Storage 계정 키를 지정합니다. Azure 스토리지에 대한 인증 중에는 사용되지 않으므로 데이터베이스 범위 지정 자격 증명 ID에 문자열을 지정할 수 있습니다.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo' ;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
  IDENTITY = '<my_account>' ,
  SECRET = '<azure_storage_account_key>' ;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage
WITH
  ( LOCATION = 'wasbs://daily@logs.blob.core.windows.net/'
    CREDENTIAL = AzureStorageCredential
    TYPE = HADOOP
  ) ;
```


## <a name="see-also"></a>참고 항목

- [CREATE DATABASE SCOPED CREDENTIAL(Transact-SQL)][create_dsc]
- [CREATE EXTERNAL FILE FORMAT(Transact-SQL)][create_eff]
- [CREATE EXTERNAL TABLE(Transact-SQL)][create_etb]
- [sys.external_data_sources(Transact-SQL)][cat_eds]
- [SAS(공유 액세스 서명) 사용][sas_token]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: ./bulk-insert-transact-sql.md
[bulk_insert_example]: ./bulk-insert-transact-sql.md#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: ../functions/openrowset-transact-sql.md

[create_dsc]: ./create-database-scoped-credential-transact-sql.md
[create_eff]: ./create-external-file-format-transact-sql.md
[create_etb]: https://docs.microsoft.com/sql/t-sql/statements/create-external-data-source
[create_etb_as_sel]: ./create-external-table-as-select-transact-sql.md?view=azure-sqldw-latest
[create_tbl_as_sel]: ./create-table-as-select-azure-sql-data-warehouse.md?view=azure-sqldw-latest

[alter_eds]: ./alter-external-data-source-transact-sql.md

[cat_eds]: ../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md
<!-- PolyBase docs -->
[intro_pb]: ../../relational-databases/polybase/polybase-guide.md
[mongodb_pb]: ../../relational-databases/polybase/polybase-configure-mongodb.md
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: ../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md
[hint_pb]: ../../relational-databases/polybase/polybase-pushdown-computation.md#force-pushdown
<!-- Elastic Query Docs -->
[intro_eq]: /azure/azure-sql/database/elastic-query-overview
[remote_eq]: /azure/azure-sql/database/elastic-query-getting-started-vertical
[remote_eq_tutorial]: /azure/azure-sql/database/elastic-query-getting-started-vertical
[sharded_eq]: /azure/azure-sql/database/elastic-query-getting-started
[sharded_eq_tutorial]: /azure/azure-sql/database/elastic-query-getting-started

<!-- Azure Docs -->
[azure_ad]: /azure/data-lake-store/data-lake-store-authenticate-using-active-directory
[sas_token]: /azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
