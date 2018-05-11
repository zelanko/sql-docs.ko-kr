---
title: PolyBase T-SQL 개체 | Microsoft 문서
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: polybase
ms.reviewer: ''
ms.suite: sql
ms.technology: database
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- PolyBase, fundamentals
- PolyBase, SQL statements
- PolyBase, SQL objects
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f8b9f0199664f1c348dfa140270ce51ebc5afeb7
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="polybase-t-sql-objects"></a>PolyBase T-SQL 개체
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  PolyBase를 사용하려면 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다.  
  
 [CREATE DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
  
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)  
 
> [!NOTE]
>  SQL Server 2016의 PolyBase는 Windows 사용자만 지원합니다. SQL 사용자를 사용하여 PolyBase 외부 테이블을 쿼리하려고 하면 쿼리에 실패합니다.

## <a name="prerequisites"></a>사전 요구 사항  
 PolyBase를 구성합니다. [PolyBase configuration](../../relational-databases/polybase/polybase-configuration.md)을 참조하세요.  
  
## <a name="create-external-tables-for-hadoop"></a>Hadoop에 대한 외부 테이블 만들기
적용 대상: SQL Server(2016부터), 병렬 데이터 웨어하우스
  
 **1. 데이터베이스 범위 자격 증명 만들기**  
  
 이 단계는 Kerberos 보안 Hadoop 클러스터에만 필요합니다.  
  
```sql  
-- Create a master key on the database.  
-- Required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- Create a database scoped credential  for Kerberos-secured Hadoop clusters.  
-- IDENTITY: the Kerberos user name.  
-- SECRET: the Kerberos password  
  
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1   
WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
  
```  
  
 **2. 외부 데이터 원본 만들기**  
  
```sql  
-- Create an external data source.  
-- LOCATION (Required) : Hadoop Name Node IP address and port.  
-- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
-- CREDENTIAL (Optional):  the database scoped credential, created above.  
  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
        TYPE = HADOOP,   
        LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',   
        RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',   
        CREDENTIAL = HadoopUser1      
);  
  
```  
  
 **3. 외부 파일 형식 만들기**  
  
```sql  
-- Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).  
  
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
```  
  
 **4. 외부 테이블 만들기**  
  
```sql  
-- Create an external table pointing to data stored in Hadoop.  
-- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
  
CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
        [SensorKey] int NOT NULL,   
        [CustomerKey] int NOT NULL,   
        [GeographyKey] int NULL,   
        [Speed] float NOT NULL,   
        [YearMeasured] int NOT NULL  
)  
WITH (LOCATION='/Demo/',   
        DATA_SOURCE = MyHadoopCluster,  
        FILE_FORMAT = TextFileFormat  
);  
  
```  
  
 **5. 통계 만들기**  
  
```sql  
-- Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
## <a name="create-external-tables-for-azure-blob-storage"></a>Azure blob 저장소에 대한 외부 테이블 만들기  
적용 대상: SQL Server(2016부터), Azure SQL Data Warehouse, 병렬 데이터 웨어하우스

 **1. 데이터베이스 범위 자격 증명 만들기**  
  
```sql  
-- Create a master key on the database.  
-- Required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- Create a database scoped credential  for Azure blob storage.  
-- IDENTITY: any string (this is not used for authentication to Azure storage).  
-- SECRET: your Azure storage account key.  
  
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential   
WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';  
  
```  
  
 **2. 외부 데이터 원본 만들기**  
  
```sql  
-- Create an external data source.  
-- LOCATION:  Azure account storage account name and blob container name.  
-- CREDENTIAL: The database scoped credential created above.  
  
CREATE EXTERNAL DATA SOURCE AzureStorage with (  
        TYPE = HADOOP,   
        LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
        CREDENTIAL = AzureStorageCredential  
);  
  
```  
  
 **3. 외부 파일 형식 만들기**  
  
```sql  
-- Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).  
  
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
```  
  
 **4. 외부 테이블 만들기**  
  
```sql  
-- Create an external table pointing to data stored in Azure storage.  
-- LOCATION: path to a file or directory that contains the data (relative to the blob container).  
-- To point to all files under the blob container, use LOCATION='/'   
  
CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
        [SensorKey] int NOT NULL,   
        [CustomerKey] int NOT NULL,   
        [GeographyKey] int NULL,   
        [Speed] float NOT NULL,   
        [YearMeasured] int NOT NULL  
)  
WITH (LOCATION='/Demo/',   
        DATA_SOURCE = AzureStorage,  
        FILE_FORMAT = TextFileFormat  
);  
  
```  
  
 **5. 통계 만들기**  
  
```sql  
-- Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
 
## <a name="create-external-tables-for-azure-data-lake-store"></a>Azure Data Lake Store의 외부 테이블 만들기
적용 대상: Azure SQL Data Warehouse

자세한 내용은 [Azure Data Lake Store를 사용하여 로드](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store)를 참조하세요.
 
 **1. 데이터베이스 범위 자격 증명 만들기**   

```sql
-- Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;

-- Create a database scoped credential
-- IDENTITY: Pass the client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>'
    ,SECRET = '<key>'
;
```  
  
 **2. 외부 데이터 원본 만들기**  
  
```sql  
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Store.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalake.net,
    CREDENTIAL = AzureStorageCredential
);
```  
  
 **3. 외부 파일 형식 만들기**  
  
```sql  
-- FIELD_TERMINATOR: Marks the end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies the field terminator for data of type string in the text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE
                    )
);
```  
  
 **4. 외부 테이블 만들기**  
  
```sql  
-- LOCATION: Folder under the ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object to use.
-- FILE_FORMAT: Specifies which File Format Object to use
-- REJECT_TYPE: Specifies how you want to deal with rejected rows. Either Value or percentage of the total
-- REJECT_VALUE: Sets the Reject value based on the reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```  
  
 **5. 통계 만들기**  
  
```sql     
CREATE STATISTICS StatsForProduct on DimProduct_external(ProductKey)  
```  

## <a name="next-steps"></a>다음 단계  
 쿼리의 예제를 보려면 [PolyBase 쿼리](../../relational-databases/polybase/polybase-queries.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [PolyBase 시작하기](../../relational-databases/polybase/get-started-with-polybase.md)   
 [PolyBase 가이드](../../relational-databases/polybase/polybase-guide.md)  
  
  
