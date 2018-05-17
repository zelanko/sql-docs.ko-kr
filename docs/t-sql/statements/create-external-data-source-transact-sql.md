---
title: CREATE EXTERNAL DATA SOURCE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9da6613c69319197da22b9b4cee74e8ef0b289d6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="create-external-data-source-transact-sql"></a>CREATE EXTERNAL DATA SOURCE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  PolyBase 또는 Elastic Database 쿼리에 대한 외부 데이터 원본을 만듭니다. 시나리오에 따라 구문은 크게 다릅니다. PolyBase용으로 만든 외부 데이터 원본은 Elastic Database 쿼리에 사용할 수 없습니다.  마찬가지로 Elastic Database 쿼리용으로 만든 외부 데이터 원본은 PolyBase 등에 사용할 수 없습니다. 
  
> [!NOTE]  
>  PolyBase는 SQL Server 2016(또는 그 이상), Azure SQL Data Warehouse 및 병렬 데이터 웨어하우스에서만 지원됩니다. Elastic Database 쿼리는 Azure SQL Database v12 이상에서만 지원됩니다.  
  
 PolyBase 시나리오의 경우 외부 데이터 원본은 Azure Storage blob 컨테이너인 HDFS(Hadoop 파일 시스템) 또는 Azure Data Lake Store입니다. 자세한 내용은 [PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md)을 참조하세요.  
  
 Elastic Database 쿼리 시나리오의 경우 외부 원본은 분할된 데이터베이스 맵 관리자(Azure SQL Database의) 또는 원격 데이터베이스(Azure SQL Database의)입니다.  외부 데이터 원본을 만든 후 [sp_execute_remote &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md)를 사용합니다. 자세한 내용은 참조 [Elastic Database 쿼리](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)를 참조하세요.  

  Azure Blob Storage 외부 데이터 원본은 
`BULK INSERT` 및 `OPENROWSET` 구문을 지원하며, Azure Blob Storage for PolyBase와는 다릅니다.
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- PolyBase only:  Hadoop cluster as data source   
-- (on SQL Server 2016)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,
        LOCATION = 'hdfs://NameNode_URI[:port]'  
        [, RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI[:port]' ]  
        [, CREDENTIAL = credential_name ]
    )
[;]  
  
-- PolyBase only: Azure Storage Blob as data source   
-- (on SQL Server 2016 and Azure SQL Data Warehouse)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,  
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
[;]

-- PolyBase only: Azure Data Lake Store
-- (on Azure SQL Data Warehouse)
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalake.net',
    CREDENTIAL = AzureStorageCredential
);

-- PolyBase only: Hadoop cluster as data source
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP, 
        LOCATION = 'hdfs://NameNode_URI[:port]'
        [, JOB_TRACKER_LOCATION = 'JobTracker_URI[:port]' ]
    )
[;]

-- PolyBase only: Azure Storage Blob as data source 
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP,
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
    )
[;]
  
-- Elastic Database query only: a shard map manager as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = SHARD_MAP_MANAGER,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '\<ElasticDatabase_ShardMapManagerDb'>,  
        CREDENTIAL = <ElasticDBQueryCred>,  
        SHARD_MAP_NAME = '<ShardMapName>'  
    )  
[;]  
  
-- Elastic Database query only: a remote database on Azure SQL Database as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = RDBMS,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '<Remote_Database_Name>',  
        CREDENTIAL = <SQL_Credential>  
    )  
[;]  

-- Bulk operations only: Azure Storage Blob as data source   
-- (on SQL Server 2017 or later, and Azure SQL Database).
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'https://storage_account_name.blob.core.windows.net/container_name'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>인수  
 *data_source_name*은 데이터 원본에 대한 사용자 정의 이름을 지정합니다. 이름은 SQL Server, Azure SQL Database 및 Azure SQL Data Warehouse 내에서 고유해야 합니다. 또한 이름은 병렬 데이터 웨어하우스의 서버 내에서 고유해야 합니다.
  
 TYPE = [ HADOOP | SHARD_MAP_MANAGER | RDBMS | BLOB_STORAGE]  
 데이터 원본 유형을 지정합니다. 외부 데이터 원본이 Hadoop 또는 Azure Storage Blob for Hadoop인 경우 HADOOP 을 사용합니다. Azure SQL Database에서 분할하기 위해 Elastic Database 쿼리에 대한 외부 데이터 원본을 만드는 경우 SHARD_MAP_MANAGER를 사용합니다. Azure SQL Database에 대한 Elastic Database 쿼리를 사용하는 데이터베이스 간 쿼리의 경우 외부 데이터 원본과 함께 RDBMS를 사용합니다.  [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]와 함께 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 또는 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)을 사용하여 대량 작업을 수행하는 경우 BLOB_STORAGE를 사용합니다.
  
LOCATION = \<location_path> **HADOOP**    
HADOOP의 경우 Hadoop 클러스터에 대해 URI(Uniform Resource Indicator)를 지정합니다.  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI: Hadoop 클러스터 Namenode의 컴퓨터 이름 또는 IP 주소입니다.  
포트: Namenode IPC 포트이며 Hadoop의 fs.default.name 구성 매개 변수에 의해 표시됩니다. 값을 지정하지 않으면 기본적으로 8020이 사용됩니다.  
예: `LOCATION = 'hdfs://10.10.10.10:8020'`

Hadoop을 포함한 Azure Blob Storage의 경우 Azure Blob Storage에 연결하기 위한 URI를 지정합니다.  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb [s]: Azure Blob Storage에 대한 프로토콜을 지정합니다. [s]는 선택 사항이며 보안 SSL 연결을 지정합니다. SQL Server에서 보낸 데이터는 SSL 프로토콜을 통해 안전하게 암호화됩니다. 'wasb' 대신 'wasbs'를 사용할 것을 적극 권장합니다. 참고로 위치에 wasb[s] 대신에 asv[s]를 사용할 수 있습니다. asv[s] 구문은 더 이상 사용되지 않으며 후속 릴리스에서 제거될 예정입니다.  
container: Azure Blob Storage 컨테이너의 이름을 지정합니다. 도메인의 저장소 계정의 루트 컨테이너를 지정하려면 컨테이너 이름 대신에 도메인 이름을 사용합니다. 루트 컨테이너는 읽기 전용이므로 데이터를 컨테이너에 다시 쓸 수 없습니다.  
account_name: Azure Storage 계정의 정규화된 도메인 이름(FQDN)입니다.  
예: `LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

Azure Data Lake Store의 경우 위치는 Azure Data Lake Store에 연결하기 위한 URI를 지정합니다.



**SHARD_MAP_MANAGER**   
 SHARD_MAP_MANAGER의 경우 Azure 가상 머신의 Azure SQL Database 또는 SQL Server Database에서 분할된 데이터베이스 맵 관리자를 호스팅하는 논리 서버 이름을 지정합니다.
 
 ```
 CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
  (TYPE = SHARD_MAP_MANAGER,
  LOCATION = '<server_name>.database.windows.net',
  DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
  CREDENTIAL = ElasticDBQueryCred,
  SHARD_MAP_NAME = 'CustomerIDShardMap'
) ;
```

단계별 자습서는 [분할을 위한 탄력적 쿼리 시작(수평 분할)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)을 참조하세요.
  
**RDBMS**   
RDBMS의 경우 Azure SQL Database에 있는 원격 데이터베이스의 논리 서버 이름을 지정합니다.  

```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';  
  
CREATE DATABASE SCOPED CREDENTIAL SQL_Credential    
WITH IDENTITY = '<username>',  
SECRET = '<password>';  
  
CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH   
    (TYPE = RDBMS,   
    LOCATION = '<server_name>.database.windows.net',   
    DATABASE_NAME = 'Customers',   
    CREDENTIAL = SQL_Credential   
) ;   
```  
  
RDBMS에 대한 단계별 자습서는 [데이터베이스 간 쿼리 시작(수직 분할)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/)을 참조하세요.  

**BLOB_STORAGE**   
대량 작업의 경우에만 `LOCATION`은 Azure Blob Storage 및 컨테이너에 유효한 URL이어야 합니다. `LOCATION` URL 끝에 **/**, 파일 이름 또는 공유 액세스 서명 매개 변수를 두지 마십시오.   
사용되는 자격 증명은 `SHARED ACCESS SIGNATURE`을 ID로 사용하여 만들어져야 합니다. 공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요. Blob 저장소에 액세스하는 예는 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)의 예제 F를 참조하세요. 

  
 RESOURCE_MANAGER_LOCATION = '*ResourceManager_URI*[:*port*]'  
 Hadoop 리소스 관리자 위치를 지정합니다. 지정된 경우 쿼리 최적화 프로그램은 MapReduce와 함께 Hadoop의 계산 기능을 사용하여 PolyBase 쿼리의 데이터를 사전 처리하기 위해 비용 기반 결정을 내릴 수 있습니다. 조건자 푸시 다운이라는 이 기능은 Hadoop과 SQL 간에 전송되는 데이터 양을 크게 줄여 쿼리 성능을 향상시킬 수 있습니다.  
  
 이 기능을 지정하지 않으면 Hadoop에 대한 푸시 계산은 PolyBase 쿼리에 대해 비활성화됩니다.  
 
포트를 지정하지 않을 경우 기본값은 ‘hadoop 연결’ 구성에 대한 현재 설정을 사용하여 결정됩니다.

|Hadoop 연결|기본 Resource Manager 포트|
|-------------------|-----------------------------|
|1|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

각 연결에서 지원되는 Hadoop 배포 및 버전의 전체 목록은 [PolyBase 연결 구성(Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)을 참조하세요.
  
> [!IMPORTANT]  
>  RESOURCE_MANAGER_LOCATION 값은 문자열이며 외부 데이터 원본을 만드는 경우 유효성이 검사되지 않습니다. 잘못된 값을 입력하면 이후 위치에 액세스할 때 지연이 발생할 수 있습니다.  
  
 Hadoop 예제:  
  
-   Hortonworks HDP 2.0, 2.1, 2.2. Windows용 2.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   Windows용 Hortonworks HDP 1.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Linux용 Hortonworks HDP 2.0, 2.1, 2.2, 2.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8050'  
    ```  
  
-   Linux용 Hortonworks HDP 1.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Linux용 Cloudera 4.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8021'  
    ```  
  
-   Linux용 Cloudera 5.1 - 5.11:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 CREDENTIAL = *credential_name*  
 외부 데이터 원본에 대해 인증하기 위한 데이터베이스 범위 자격 증명을 지정합니다. 예를 들어 [C. Azure Blob Storage 외부 데이터 원본 만들기](../../t-sql/statements/create-external-data-source-transact-sql.md#credential)를 참조하세요. 자격 증명을 만드는 방법은 [CREATE CREDENTIAL(Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md)을 참조하세요. 참고로 CREDENTIAL은 익명 액세스를 허용하는 공용 데이터 집합의 경우 필요하지 않습니다. 
  
 DATABASE_NAME = *'QueryDatabaseName'*  
 분할된 데이터베이스 맵 관리자(SHARD_MAP_MANAGER의 경우) 또는 원격 데이터베이스(RDBMS의 경우)로 작동하는 데이터베이스의 이름입니다.  
  
 SHARD_MAP_NAME = *'ShardMapName'*  
 SHARD_MAP_MANAGER의 경우만. 분할된 데이터베이스 맵의 이름입니다. 분할된 데이터베이스 맵 만들기에 대한 자세한 내용은 [Elastic Database 쿼리 시작](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/) 참조  
  
## <a name="polybase-specific-notes"></a>PolyBase 관련 메모  
지원되는 외부 데이터 원본의 전체 목록은 [PolyBase 연결 구성(Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)을 참조하세요.

 PolyBase를 사용하려면 다음 세 개체를 만들어야 합니다.  
  
-   외부 데이터 원본.  
  
-   외부 파일 형식, 그리고  
  
-   외부 데이터 원본과 외부 파일 형식을 참조하는 외부 테이블.  
  
## <a name="permissions"></a>사용 권한  
 SQL DW, SQL Server, APS 2016 및 SQL DB의 데이터베이스에 대한 CONTROL 권한이 필요합니다.

> [!IMPORTANT]  
>  PDW의 이전 릴리스에서는 외부 데이터 원본을 만들려면 ALTER ANY EXTERNAL DATA SOURCE 권한이 필요했습니다.
  
  
## <a name="error-handling"></a>오류 처리  
 런타임 오류는 외부 Hadoop 데이터 원본이 정의된 RESOURCE_MANAGER_LOCATION에 관하여 일관성이 없는 경우 발생합니다. 즉, 같은 Hadoop 클러스터를 참조하는 외부 데이터 원본 두 개를 지정한 다음, 하나에는 리소스 관리자 위치를 제공하고 다른 하나에는 제공하지 않는 식으로 할 수 없습니다.  
  
 SQL 엔진은 외부 데이터 원본 개체를 만들 때 해당 외부 데이터 원본이 존재하는지 확인하지 않습니다. 쿼리를 실행하는 동안 데이터 원본이 존재하지 않으면 오류가 발생합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
PolyBase의 경우 외부 데이터 원본은 SQL Server 및 SQL Data Warehouse에 범위가 지정된 데이터베이스입니다. 이는 병렬 데이터 웨어하우스에 범위 지정된 서버입니다.
  
PolyBase의 경우 RESOURCE_MANAGER_LOCATION 또는 JOB_TRACKER_LOCATION을 정의하면 쿼리 최적화 프로그램은 외부 Hadoop 원본에 대해 맵 감소 작업을 시작하고 계산을 푸시 다운하여 각 쿼리의 최적화를 고려합니다. 이것은 전적으로 비용 기반의 결정입니다.  

Hadoop NameNode 장애 조치(Failover) 시 성공적인 PolyBase를 보장하려면 Hadoop 클러스터의 NameNode에 가상 IP 주소 사용을 고려하세요. Hadoop NameNode에 가상 IP 주소를 사용하지 않으면 Hadoop NameNode 장애 조치 시 ALTER EXTERNAL DATA SOURCE 개체가 새 위치를 가리키게 해야 합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 같은 Hadoop 클러스터 위치에 정의된 모든 데이터 원본은 RESOURCE_MANAGER_LOCATION 또는 JOB_TRACKER_LOCATION에 대해 같은 설정을 사용해야 합니다. 일관되지 않은 부분이 있으면 런타임 오류가 발생합니다.  
  
 Hadoop 클러스터가 이름을 사용하여 설정되었는데 외부 데이터 원본이 클러스터 위치에 대해 IP 주소를 사용하는 경우, PolyBase는 데이터 원본이 사용될 때 클러스터 이름을 여전히 확인할 수 있어야 합니다. 이름을 확인하려면 DNS 전달자를 활성화해야 합니다.  
  
## <a name="locking"></a>잠금  
 EXTERNAL DATA SOURCE 개체에 대해 공유 잠금을 적용합니다.  
  
##  <a name="examples"></a> 예제: SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>1. Hadoop를 참조하는 외부 데이터 원본 만들기  
Hortonworks 또는 Cloudera Hadoop 클러스터를 참조하는 외부 데이터 원본을 만들려면 컴퓨터 이름 또는 Hadoop Namenode 및 포트의 IP 주소를 지정합니다.  
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>2. 푸시 다운이 활성화된 상태에서 Hadoop를 참조하는 외부 데이터 원본 만들기  
RESOURCE_MANAGER_LOCATION 옵션을 지정하여 PolyBase 쿼리에 대한 Hadoop 계산 푸시 다운을 활성화합니다. 활성화되면 PolyBase는 비용 기반 결정을 사용하여 Hadoop에 대해 쿼리 계산을 푸시해야 하는지 아니면 SQL Server를 처리하기 위해 모든 데이터를 이동해야 하는지 결정합니다.
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> 3. Kerberos 보안 Hadoop를 참조하는 외부 데이터 원본 만들기  
Hadoop 클러스터가 Kerberos 보안 방식인지 확인하려면 Hadoop core-site.xml에서 hadoop.security.authentication 속성의 값을 확인합니다. Kerberos 보안 Hadoop 클러스터를 확인하려면 Kerberos 사용자 이름과 암호를 포함한 데이터베이스 범위 자격 증명을 지정해야 합니다. 데이터베이스 범위 자격 증명 비밀을 암호화하는 데에는 데이터베이스 마스터 키가 사용됩니다. 
  
```sql  
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1 
WITH IDENTITY = '<hadoop_user_name>', 
SECRET = '<hadoop_password>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (
    TYPE = HADOOP, 
    LOCATION = 'hdfs://10.10.10.10:8050', 
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050', 
    CREDENTIAL = HadoopUser1
);
```

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>4. Azure Blob Storage를 참조하는 외부 데이터 원본 만들기
Azure Blob Storage 컨테이너를 참조하는 외부 데이터 원본을 만들려면 Azure Blob Storage URI 및 Azure Storage 계정 키를 포함한 데이터베이스 범위 자격 증명을 지정합니다.

이 예제에서 외부 데이터 원본은 myaccount라는 Azure Storage 계정 아래의 dailylogs라는 Azure Blob Storage 컨테이너입니다. Azure Storage 외부 데이터 원본은 데이터 전송만을 위한 것이며 조건자 푸시 다운을 지원하지 않습니다.

이 예제에서는 Azure Storage에 대한 인증을 위해 데이터베이스 범위 자격 증명을 만드는 방법을 보여 줍니다. 데이터베이스 자격 증명 비밀에 Azure Storage 계정 키를 지정합니다. 데이터베이스 범위 자격 증명 ID의 문자열을 지정하며, 이 문자열은 Azure Storage에 대한 인증을 위해 사용되지 않습니다. 그런 다음, 외부 데이터 원본을 만드는 문에 자격 증명이 사용됩니다.

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = BLOB_STORAGE, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>예제: Azure SQL Database

### <a name="e-create-a-shard-map-manager-external-data-source"></a>5. 분할된 데이터베이스 맵 관리자 외부 데이터 원본 만들기
SHARD_MAP_MANAGER를 참조하는 외부 데이터 원본을 만들려면 Azure 가상 머신의 Azure SQL Database 또는 SQL Server Database에서 분할된 데이터베이스 맵 관리자를 호스팅하는 논리 서버 이름을 지정합니다.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = SHARD_MAP_MANAGER,
    LOCATION = '<server_name>.database.windows.net',
    DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
    CREDENTIAL = ElasticDBQueryCred,
    SHARD_MAP_NAME = 'CustomerIDShardMap'
);
```

### <a name="f-create-an-rdbms-external-data-source"></a>6. RDBMS 외부 데이터 원본 만들기
RDBMS를 참조하는 외부 데이터 원본을 만들려면 Azure SQL Database에 있는 원격 데이터베이스의 논리 서버 이름을 지정합니다.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL SQL_Credential  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = RDBMS, 
    LOCATION = '<server_name>.database.windows.net', 
    DATABASE_NAME = 'Customers', 
    CREDENTIAL = SQL_Credential 
);
```

## <a name="examples-azure-sql-data-warehouse"></a>예제: Azure SQL Data Warehouse

### <a name="g-create-external-data-source-to-reference-azure-data-lake-store"></a>7. Azure Data Lake Store를 참조하는 외부 데이터 원본 만들기
Azure Data Lake Store 연결은 ADLS URI 및 Azure Acitve directory 응용 프로그램의 서비스 원칙을 기반으로 합니다. 이 응용 프로그램을 만들기 위한 문서는 [Active Directory를 사용하여 Data Lake 저장소 인증](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)에서 찾을 수 있습니다.

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = '<ADLS URI>'
)
```



## <a name="examples-parallel-data-warehouse"></a>예제: 병렬 데이터 웨어하우스

### <a name="h-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>8. 푸시 다운이 활성화된 상태에서 Hadoop를 참조하는 외부 데이터 원본 만들기
JOB_TRACKER_LOCATION 옵션을 지정하여 PolyBase 쿼리에 대한 Hadoop 계산 푸시 다운을 활성화합니다. 활성화되면 PolyBase는 비용 기반 결정을 사용하여 Hadoop에 대해 쿼리 계산을 푸시해야 하는지 아니면 SQL Server를 처리하기 위해 모든 데이터를 이동해야 하는지 결정합니다. 

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="i-create-external-data-source-to-reference-azure-blob-storage"></a>9. Azure Blob Storage를 참조하는 외부 데이터 원본 만들기
Azure Blob Storage 컨테이너를 참조하는 외부 데이터 원본을 만들려면 Azure Blob Storage를 외부 데이터 소스 위치(LOCATION)로 지정합니다. 인증을 위해 Azure Storage 계정 키를 PDW core-site.xml 파일에 추가합니다.

이 예제에서 외부 데이터 원본은 myaccount라는 Azure Storage 계정 아래의 dailylogs라는 Azure Blob Storage 컨테이너입니다. Azure Storage 외부 데이터 원본은 데이터 전송만을 위한 것이며 조건자 푸시 다운을 지원하지 않습니다.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>예제: 대량 작업   
### <a name="j-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>10. Azure Blob Storage에서 데이터를 검색하는 대량 작업을 위한 외부 데이터 원본을 만듭니다.   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]을 참조하세요.   
[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 또는 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)을 사용하여 대량 작업에 대한 다음 데이터 원본을 만듭니다. 사용되는 자격 증명은 `SHARED ACCESS SIGNATURE`을 ID로 사용하여 만들어져야 합니다. 공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요.   
```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
사용 중인 이 예제를 보려면 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)를 참조하세요.
  
## <a name="see-also"></a>참고 항목
[ALTER EXTERNAL DATA SOURCE(Transact-SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
[CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[sys.external_data_sources(Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  

