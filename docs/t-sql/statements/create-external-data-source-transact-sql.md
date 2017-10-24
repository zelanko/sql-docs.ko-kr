---
title: "외부 데이터 원본 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
ms.assetid: 75d8a220-0f4d-4d91-8ba4-9d852b945509
caps.latest.revision: 58
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c2a0a43aefe59bc11f16445b5ee0c781179a33fa
ms.openlocfilehash: 477d2f682da2c91ba8e4bfd42186c4b1b9735f85
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="create-external-data-source-transact-sql"></a>외부 데이터 원본 (Transact SQL) 만들기
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  PolyBase, 탄력적 데이터베이스 쿼리 또는 Azure Blob 저장소에 대 한 외부 데이터 소스를 만듭니다. 시나리오에 따라 구문을 크게 다릅니다. 탄력적 데이터베이스 쿼리에 대 한 만든 PolyBase에 대 한 데이터 소스를 사용할 수 없습니다.  마찬가지로, PolyBase 등에 대해 만든 탄력적 데이터베이스 쿼리에 대 한 데이터 소스를 사용할 수 없습니다. 
  
> [!NOTE]  
>  PolyBase는 SQL Server 2016, Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 에서만 지원 됩니다. 탄력적 데이터베이스 쿼리 또는 나중에 Azure SQL 데이터베이스 v 12에만 사용할 수 있습니다.  
  
 PolyBase 시나리오에 대 한 외부 데이터 원본이 Hadoop 파일 시스템 (HDFS), Azure 저장소 blob 컨테이너 또는 Azure 데이터 레이크 저장소. 자세한 내용은 [PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md)을 참조하세요.  
  
 탄력적 데이터베이스 쿼리 시나리오에 대 한 외부 원본은 (Azure SQL 데이터베이스)에 shard map 관리자 또는 (Azure SQL 데이터베이스)에 원격 데이터베이스입니다.  사용 하 여 [sp_execute_remote &#40; Azure SQL 데이터베이스 &#41; ](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md) 외부 데이터 원본을 만든 후 합니다. 자세한 내용은 참조 [탄력적 데이터베이스 쿼리](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)합니다.  

  Azure Blob 저장소 외부 데이터 원본은 지원 `BULK INSERT` 및 `OPENROWSET` 구문과는 PolyBase에 대 한 Azure Blob 저장소와 다릅니다.
    
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
 *data_source_name* 데이터 원본에 대 한 사용자 정의 이름을 지정 합니다. 이름에 SQL Server, Azure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스 데이터베이스 내에서 고유 해야 합니다. 이름 서버에 병렬 데이터 웨어하우스 내에서 고유 해야 합니다.
  
 형식 = [HADOOP | SHARD_MAP_MANAGER | RDBMS | BLOB_STORAGE]  
 데이터 소스 유형을 지정합니다. HADOOP에 사용할 외부 데이터 소스는 Hadoop 또는 Azure 저장소 blob Hadoop에 대 한 합니다. Azure SQL 데이터베이스에서 분할에 대 한 탄력적 데이터베이스 쿼리에 대 한 외부 데이터 원본을 만들 때 SHARD_MAP_MANAGER를 사용 합니다. 외부 데이터 원본과 RDBMS를 사용 하 여 Azure SQL 데이터베이스 탄력적 데이터베이스 쿼리를 사용 하 여 데이터베이스 간 쿼리.  사용 하 여 대량 작업을 수행할 때 BLOB_STORAGE를 사용 하 여 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 또는 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 와 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]합니다.
  
위치 = \<location_path > **HADOOP**    
HADOOP는 표시기 URI (Uniform Resource) Hadoop 클러스터에 대 한을 지정합니다.  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI: 컴퓨터 이름 또는 Namenode Hadoop 클러스터의 IP 주소입니다.  
포트: Namenode IPC 포트입니다. 이 Hadoop에 fs.default.name 구성 매개 변수에 의해 표시 됩니다. 값을 지정 하지 않으면 8020 기본적으로 사용 됩니다.  
예:`LOCATION = 'hdfs://10.10.10.10:8020'`

Hadoop으로 Azure blob 저장소에 대 한 Azure blob 저장소에 연결 하기 위한 URI를 지정 합니다.  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb [s]: Azure blob 저장소에 대 한 프로토콜을 지정 합니다. [S]는 선택 사항이 며; 보안 SSL 연결을 지정 합니다. SQL Server에서 보낸 데이터는 SSL 프로토콜을 통해 안전 하 게 암호화 됩니다. 'Wasb' 대신 ' wasbs'를 사용 하는 것이 좋습니다. Note 위치가 wasb [s] 대신 [s] asv를 사용할 수 있습니다. Asv [s] 구문을 사용 되지 않으며 이후 릴리스에서 제거 됩니다.  
컨테이너: Azure blob 저장소 컨테이너의 이름을 지정 합니다. 도메인의 저장소 계정의 루트 컨테이너를 지정 하려면 컨테이너 이름 대신 도메인 이름을 사용 합니다. 루트 컨테이너는 읽기 전용 컨테이너에 데이터를 다시 쓸 수 없습니다.  
account_name: Azure 저장소 계정과의 정규화 된 도메인 이름 (FQDN)입니다.  
예:`LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

Azure 데이터 레이크 저장소에 대 한 위치는 Azure 데이터 레이크 저장소에 연결 하기 위한 URI를 지정 합니다.



**SHARD_MAP_MANAGER**   
 SHARD_MAP_MANAGER, Azure SQL 데이터베이스 또는 Azure 가상 컴퓨터에 SQL Server 데이터베이스에서 분할 맵 관리자를 호스트 하는 논리 서버 이름을 지정 합니다.
 
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

단계별 자습서를 참조 하십시오. [탄력적 쿼리 (수평 분할) 분할에 대 한 시작](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)합니다.
  
**RDBMS**   
RDBMS에 대 한 Azure SQL 데이터베이스에 원격 데이터베이스의 논리 서버 이름을 지정합니다.  

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
  
RDBMS에 대 한 단계별 자습서를 참조 하십시오. [데이터베이스 간 쿼리 (수직 분할) 시작](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/)합니다.  

**BLOB_STORAGE**   
대량 작업에 `LOCATION` 유효 해야 Azure Blob 저장소 및 컨테이너의 URL입니다. 에 두지 마십시오  **/** , 파일 이름, 또는 공유 액세스 서명 매개 변수 끝에 `LOCATION` URL입니다.   
사용 하 여을 사용 하는 자격 증명을 만들어야 `SHARED ACCESS SIGNATURE` id로 합니다. 공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요. Blob 저장소에 액세스 하는 예제를 F 예제를 보려면 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)합니다. 

  
 RESOURCE_MANAGER_LOCATION = '*ResourceManager_URI*[:*포트*]'  
 Hadoop 리소스 관리자 위치를 지정합니다. 을 지정 하면 쿼리 최적화 프로그램은 미리 MapReduce와 Hadoop의 계산 기능을 사용 하 여 PolyBase 쿼리를 위해 데이터를 처리 하는 비용 기반 결정에 가능 합니다. 조건자 푸시 다운이 수 Hadoop과 SQL을 간에 전송 되는 데이터 양이 크게 줄일를 호출한 따라서 쿼리 성능을 향상 시킵니다.  
  
 지정 하지 않으면 PolyBase 쿼리에서 Hadoop에 계산을 푸시할 비활성화 됩니다.  
 
포트가 지정 되지 않은 경우 기본값 'hadoop c 구성에 대 한 현재 설정을 사용 하 여 결정 됩니다.

|Hadoop 연결|리소스 관리자 기본 포트|
|-------------------|-----------------------------|
|1.|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

Hadoop 배포와 각 연결 값에서 지 원하는 버전의 전체 목록은 참조 하십시오. [PolyBase 연결 구성 (Transact SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)합니다.
  
> [!IMPORTANT]  
>  RESOURCE_MANAGER_LOCATION 값은 문자열로 외부 데이터 원본을 만들 때 유효성이 검사 되지 않습니다. 잘못 된 값 입력 위치에 액세스할 때 이후 지연 될 수 있습니다.  
  
 Hadoop 예제:  
  
-   Hortonworks HDP 2.0, 2.1, 2.2입니다. Windows에서 2.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   Hortonworks HDP 1.3 Windows에서:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Hortonworks HDP 2.0, 2.1, 2.2, 2.3 Linux에서:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8050'  
    ```  
  
-   Linux에서 Hortonworks HDP 1.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Linux에서 Cloudera 4.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8021'  
    ```  
  
-   Linux에서 Cloudera 5.1 5.11:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 자격 증명 = *credential_name*  
 외부 데이터 원본에 대 한 인증에 대 한 데이터베이스 범위 자격 증명을 지정 합니다. 예를 들어 참조 [3. Azure blob 저장소 외부 데이터 원본 만들기](../../t-sql/statements/create-external-data-source-transact-sql.md#credential)합니다. 자격 증명을 만들려면 참조 [CREATE CREDENTIAL (TRANSACT-SQL)](../../t-sql/statements/create-credential-transact-sql.md)합니다. 자격 증명이 익명 액세스를 허용 하는 공용 데이터 집합에 대 한 필요 하지 않음을 참고 합니다. 
  
 DATABASE_NAME = *'QueryDatabaseName'*  
 (RDBMS)에 대 한 원격 데이터베이스 또는 (SHARD_MAP_MANAGER)에 대 한 분할 맵 관리자로 기능 하는 데이터베이스의 이름입니다.  
  
 SHARD_MAP_NAME = *'ShardMapName'*  
 에 대 한 SHARD_MAP_MANAGER에만 해당 합니다. 분할 맵은의 이름입니다. 분할 맵 만들기에 대 한 자세한 내용은 참조 [탄력적 데이터베이스 쿼리 시작](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)  
  
## <a name="polybase-specific-notes"></a>PolyBase 관련 참고 사항  
지원 되는 외부 데이터 원본의 목록은 전체 참조 [PolyBase 연결 구성 (Transact SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)합니다.

 PolyBase를 사용 하려면 이러한 세 가지 개체를 만들려면:  
  
-   외부 데이터 원본입니다.  
  
-   외부 파일 형식 및  
  
-   외부 데이터 원본 및 외부 파일 형식을 참조 하는 외부 테이블입니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스 SQL DW "," SQL Server "," APS 2016 "및" SQL DB에 대 한 CONTROL 권한이 필요합니다.

> [!IMPORTANT]  
>  PDW의 이전 버전에서는 외부 데이터 원본 필수 ALTER ANY EXTERNAL DATA SOURCE 권한을 만듭니다.
  
  
## <a name="error-handling"></a>오류 처리  
 외부 Hadoop 데이터 원본 정의 RESOURCE_MANAGER_LOCATION 것에 대해 일치 하지 않는 경우 런타임 오류가 발생 합니다. 즉, 동일한 Hadoop 클러스터 및 하나에 대 한 아닌와 다른 리소스 관리자 위치를 제공 하는 다음을 참조 하는 두 개의 외부 데이터 소스를 지정할 수 없습니다.  
  
 SQL 엔진에서 외부 데이터 원본 개체를 만들 때 외부 데이터 원본의 존재 여부를 확인 하지 않습니다. 데이터 원본이 존재 하지 않는 경우 쿼리를 실행 하는 동안 오류가 발생 합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
PolyBase, 외부 데이터 원본은 SQL Server 및 SQL 데이터 웨어하우스 데이터베이스 범위입니다. 서버 범위에 있기 병렬 데이터 웨어하우스 합니다.
  
PolyBase에 대 한 RESOURCE_MANAGER_LOCATION 또는 JOB_TRACKER_LOCATION 정의 될 때 쿼리 최적화 프로그램은 고려 지도 시작 하 여 각 쿼리 줄일 외부 Hadoop 원본과 푸시 다운 계산에서 작업을 최적화 합니다. 이것은 완전히 비용 기반 결정 합니다.  

을 보장 하기 위해 Hadoop NameNode 장애 조치 발생 시 성공적인 PolyBase 쿼리 Hadoop 클러스터의 NameNode에 대 한 가상 IP 주소를 사용 하는 것이 좋습니다. Hadoop NameNode에 대 한 가상 IP 주소를 사용 하지 않는 경우 Hadoop NameNode 장애 조치 시 해야 합니다 외부 데이터 원본 변경 개체 새 위치를 가리키도록 합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 동일한 Hadoop 클러스터 위치에 정의 된 모든 데이터 원본 RESOURCE_MANAGER_LOCATION 또는 JOB_TRACKER_LOCATION 동일한 설정을 사용 해야 합니다. 불일치가 있으면 런타임 오류가 발생 합니다.  
  
 Hadoop 클러스터 이름으로 설정 되어 외부 데이터 원본 클러스터 위치에 대 한 IP 주소를 사용 하는 경우 PolyBase에 데이터 소스를 사용할 때 클러스터 이름을 확인할 수 해야 합니다. 이름을 해결 하려면 DNS 전달자를 사용 하도록 설정 해야 합니다.  
  
## <a name="locking"></a>잠금  
 외부 데이터 원본 개체에 대 한 공유 잠금을 사용합니다.  
  
##  <a name="examples"></a>예: SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>1. 참조 Hadoop에 외부 데이터 원본 만들기  
Hortonworks 또는 Cloudera Hadoop 클러스터를 참조 하는 외부 데이터 원본을 만들려면 컴퓨터 이름이 나 IP 주소는 Hadoop Namenode 및 포트를 지정 합니다.  
  
```tsql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>2. 푸시 다운을 사용 하도록 설정 참조 Hadoop에 외부 데이터 원본 만들기  
Polybase에 대 한 Hadoop에 푸시 다운 계산을 사용 하도록 설정 하려면 RESOURCE_MANAGER_LOCATION 옵션을 지정 합니다. 활성화 되 면 PolyBase 비용 기반 결정을 사용 하 여 Hadoop으로 쿼리 계산을 푸시할 또는 모든 데이터가 SQL Server의 쿼리 처리를 설정할지 여부를 결정 합니다.
  
```tsql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> 3. Kerberos 보안 Hadoop 참조 하려면 외부 데이터 원본 만들기  
Kerberos 보안 Hadoop 클러스터 인지를 확인 하려면 Hadoop 코어 site.xml hadoop.security.authentication 속성의 값을 확인 합니다. Kerberos 보안 Hadoop 클러스터를 참조 하려면 Kerberos 사용자 이름 및 암호를 포함 하는 데이터베이스 범위 자격 증명을 지정 해야 합니다. 데이터베이스 범위 자격 증명 암호를 암호화 하는 데이터베이스 마스터 키 사용 됩니다. 
  
```tsql  
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

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>4. Azure blob 저장소를 참조 하는 외부 데이터 원본 만들기
Azure blob 저장소 컨테이너를 참조 하는 외부 데이터 원본을 만들려면 Azure blob 저장소 URI 및 Azure 저장소 계정 키가 포함 된 데이터베이스 범위 자격 증명을 지정 합니다.

이 예제에서는 외부 데이터 원본은 dailylogs myaccount 라는 Azure 저장소 계정에서 호출 하는 Azure blob 저장소 컨테이너를입니다. 데이터 전송만;에 외부 데이터 소스는 Azure 저장소 및 조건자 푸시 다운을 지원 하지 않습니다.

이 예제에는 Azure 저장소 인증에 대 한 데이터베이스 범위 자격 증명을 만드는 방법을 보여 줍니다. 데이터베이스 자격 증명 암호에 Azure 저장소 계정 키를 지정 합니다. 모든 문자열에 데이터베이스 범위 자격 증명 id, Azure 저장소 인증에 사용 되지 않습니다 지정 합니다. 그런 다음 자격 증명을 외부 데이터 원본을 만드는 문을에 사용 됩니다.

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = HADOOP, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>예: Azure SQL 데이터베이스

### <a name="e-create-a-shard-map-manager-external-data-source"></a>5. Shard map manager 외부 데이터 원본 만들기
SHARD_MAP_MANAGER 참조 하려면 외부 데이터 소스를 만들려면 Azure SQL 데이터베이스 또는 Azure 가상 컴퓨터에 SQL Server 데이터베이스에서 분할 맵 관리자를 호스트 하는 논리 서버 이름을 지정 합니다.

```tsql
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
RDBMS가 참조 하는 외부 데이터 원본을 만들려면 Azure SQL 데이터베이스에 원격 데이터베이스의 논리 서버 이름을 지정 합니다.

```tsql
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

## <a name="examples-azure-sql-data-warehouse"></a>예: Azure SQL 데이터 웨어하우스

### <a name="g-create-external-data-source-to-reference-azure-blob-storage"></a>7. Azure blob 저장소를 참조 하는 외부 데이터 원본 만들기
Azure blob 저장소 컨테이너를 참조 하는 외부 데이터 원본을 만들려면 Azure blob 저장소 URI 및 Azure 저장소 계정 키가 포함 된 데이터베이스 범위 자격 증명을 지정 합니다.

이 예제에서는 외부 데이터 원본은 dailylogs myaccount 라는 Azure 저장소 계정에서 호출 하는 Azure blob 저장소 컨테이너를입니다. Azure 저장소 외부 데이터 원본의 데이터 전송만 되며 조건자 푸시 다운을 지원 하지 않습니다.

이 예제에는 Azure 저장소 인증에 대 한 데이터베이스 범위 자격 증명을 만드는 방법을 보여 줍니다. 데이터베이스 자격 증명 암호에 Azure 저장소 계정 키를 지정 합니다. 모든 문자열에 데이터베이스 범위 자격 증명 id, Azure 저장소 인증에 사용 되지 않습니다 지정 합니다. 그런 다음 자격 증명을 외부 데이터 원본을 만드는 문을에 사용 됩니다.

```tsql
-- Create a database master key if one does not already exist. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage 
WITH (
    TYPE = HADOOP, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```
### <a name="h-create-external-data-source-to-reference-azure-data-lake-store"></a>8. Azure 데이터 레이크 저장소 참조를 외부 데이터 원본 만들기
Azure 데이터 레이크 저장소 연결 ADLS URI 및 Azure 활성 디렉터리 응용 프로그램의 서비스 사용자 기반으로 합니다. 이 응용 프로그램 만들기에 대 한 설명서에서 찾을 수 있습니다[Active Directory를 사용 하 여 데이터 레이크 저장소 인증](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)합니다.

```tsql
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



## <a name="examples-parallel-data-warehouse"></a>예: 병렬 데이터 웨어하우스

### <a name="i-create-external-data-source-to-reference-hadoop"></a>9. 참조 Hadoop에 외부 데이터 원본 만들기
Hortonworks 또는 Cloudera Hadoop 클러스터를 참조 하는 외부 데이터 원본을 만들려면 컴퓨터 이름이 나 IP 주소는 Hadoop Namenode 및 포트를 지정 합니다.

```tsql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);
```

### <a name="j-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>10. 푸시 다운을 사용 하도록 설정 참조 Hadoop에 외부 데이터 원본 만들기
Polybase에 대 한 Hadoop에 푸시 다운 계산을 사용 하도록 설정 하려면 JOB_TRACKER_LOCATION 옵션을 지정 합니다. 활성화 되 면 PolyBase 비용 기반 결정을 사용 하 여 Hadoop으로 쿼리 계산을 푸시할 또는 모든 데이터가 SQL Server의 쿼리 처리를 설정할지 여부를 결정 합니다. 

```tsql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="k-create-external-data-source-to-reference-azure-blob-storage"></a>11. Azure blob 저장소를 참조 하는 외부 데이터 원본 만들기
외부 만들려면 데이터 소스 외부 데이터로 Azure blob 저장소 URI를 지정 Azure blob 저장소 컨테이너를 사용 하 여 참조를 원본 위치입니다. 인증을 위해 PDW site.xml 코어 파일을 Azure 저장소 계정 키를 추가 합니다.

이 예제에서는 외부 데이터 원본은 dailylogs myaccount 라는 Azure 저장소 계정에서 호출 하는 Azure blob 저장소 컨테이너를입니다. Azure 저장소 외부 데이터 원본의 데이터 전송만 되며 조건자 푸시 다운을 지원 하지 않습니다.

```tsql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>예: 대량 작업   
### <a name="l-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>12. Azure Blob 저장소에서 데이터를 검색 하는 대량 작업에 대 한 외부 데이터 원본을 만듭니다.   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]을 참조하세요.   
사용 하 여 대량 작업에 대 한 다음 데이터 소스를 사용 하 여 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 또는 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)합니다. 사용 하 여을 사용 하는 자격 증명을 만들어야 `SHARED ACCESS SIGNATURE` id로 합니다. 공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요.   
```tsql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
사용에서이 예제를 보려면 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)합니다.
  
## <a name="see-also"></a>관련 항목:
[ALTER 외부 데이터 원본 (Transact SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
[외부 TABLE AS SELECT &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[TABLE AS SELECT &#40; 만들기 Azure SQL 데이터 웨어하우스 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[sys.external_data_sources (Transact SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  


