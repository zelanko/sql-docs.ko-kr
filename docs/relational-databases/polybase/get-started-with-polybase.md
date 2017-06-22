---
title: "PolyBase 시작하기 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 5/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- PolyBase
- PolyBase, getting started
- Hadoop import
- Hadoop export
- Azure blob storage import
- Azure blob storage export
- Hadoop import, PolyBase getting started
- Hadoop export, Polybase getting started
ms.assetid: c71ddc50-b4c7-416c-9789-264671bd9ecb
caps.latest.revision: 78
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 3fc2a681f001906cf9e819084679db097bca62c7
ms.openlocfilehash: 59bf4021617603f0720c23ca192f4ddb65aa6834
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="get-started-with-polybase"></a>PolyBase 시작하기
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 SQL Server 인스턴스에 PolyBase를 실행 하는 방법에 대 한 기본 사항입니다.
  
 아래 단계를 실행하면 다음이 수행됩니다.  
  
-   서버에 PolyBase 설치 및 실행 가능  
  
-   PolyBase 개체를 만드는 문 예제  
  
-   SQL Server Management Studio(SSMS)에서 PolyBase 개체 관리 방법 이해  
  
-   PolyBase 개체를 사용하는 쿼리 예제  
  
## <a name="prerequisites"></a>필수 구성 요소  
 인스턴스 [SQL Server (64 비트)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) 다음:  
  
-   Microsoft .NET Framework 4.5  
  
-   Oracle Java SE RunTime Environment(JRE) 버전 7.51 이상(64 비트) (두 [JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) 또는 [Server JRE](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) 작동). [Java SE 다운로드](http://www.oracle.com/technetwork/java/javase/downloads/index.html)로 이동합니다. JRE가 없으면 설치 관리자가 실패합니다.   
  
-   최소 메모리: 4GB  
  
-   최소 하드 디스크 공간: 2GB    
-   TCP/IP 연결을 사용할 수 있어야 합니다. [서버 네트워크 프로토콜 설정 또는 해제](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)를 참조하세요.  
  
 
 외부 데이터 원본은 다음 개체 중 하나입니다.  
  
-   Hadoop 클러스터. 지원되는 버전은 [PolyBase 구성](#supported)을 참조하세요.  

-   Azure Blob 저장소

> [!NOTE]
>   Hadoop에 대해 계산 푸시 다운 기능을 사용하려면 대상 Hadoop 클러스터에 HDFS의 핵심 구성 요소가 있고 Jobhistory 서버에서 Yarn/MapReduce가 사용하도록 설정되어 있는지 확인해야 합니다. PolyBase는 MapReduce를 통해 푸시다운 쿼리를 제출하고 JobHistory 서버에서 상태를 가져옵니다. 두 구성 요소 없이 쿼리가 실패 합니다. 

## <a name="install-polybase"></a>PolyBase 설치  
 PolyBase를 설치 하지 않은 경우 참조 [PolyBase 설치](../../relational-databases/polybase/polybase-installation.md)합니다.  
  
### <a name="how-to-confirm-installation"></a>설치 확인 방법  
 설치가 끝난 후 PolyBase가 제대로 설치되었는지 확인하려면 다음 명령을 실행합니다. PolyBase가 설치된 경우 1을 반환합니다. 그렇지 않으면 0이 반환됩니다.  
  
```tsql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
##  <a name="supported"></a> Configure PolyBase  
 를 설치한 후 사용자의 Hadoop 버전을 사용 하도록 SQL Server 또는 Azure Blob 저장소를 구성 해야 합니다. PolyBase는 두 명의 Hadoop 공급자 인 Hortonworks Data Platform (HDP) 및 CDH Cloudera Distributed Hadoop ()를 지원합니다.  지원되는 외부 데이터 원본은 다음과 같습니다.  
  
-   Linux/Windows Server에서 Hortonworks HDP 1.3  
  
-   Linux에서 Hortonworks HDP 2.1-2.6

-   Windows Server에서 Hortonworks HDP 2.1 - 2.3  
  
-   Linux에서 Cloudera CDH 4.3  
  
-   Cloudera CDH 5.1 – 5.5, linux 5.9 5.11  
  
-   Azure BLOB 저장소  
  
>  [!NOTE]
> Azure Data Lake Store 연결은 Azure SQL Data Warehouse에서만 지원됩니다.
  
### <a name="external-data-source-configuration"></a>외부 데이터 원본 구성  
  
1.  [sp_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 'hadoop connectivity'를 실행하고 적절한 값을 설정합니다. 기본적으로 hadoop 연결은 7로 설정됩니다. 값을 찾으려면 [PolyBase Connectivity Configuration&#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)을 참조하세요.  
      ```tsql  
    -- Values map to various external data sources.  
    -- Example: value 7 stands for Azure blob storage and Hortonworks HDP 2.3 on Linux.  
    sp_configure @configname = 'hadoop connectivity', @configvalue = 7;   
    GO   
  
    RECONFIGURE   
    GO   
    ```  
  
2.  **services.msc**를 사용하여 SQL Server를 다시 시작해야 합니다. SQL Server를 다시 시작하면 다음 서비스도 다시 시작됩니다.  
  
    -   SQL Server PolyBase 데이터 이동 서비스  
  
    -   SQL Server PolyBase 엔진  
  
 ![services.msc에서 PolyBase 서비스 중지 및 시작](../../relational-databases/polybase/media/polybase-stop-start.png "stop and start PolyBase services in services.msc")  
  
### <a name="pushdown-configuration"></a>푸시다운 구성  
 쿼리 성능을 향상시키려면 Hadoop 클러스터에 대한 푸시다운 계산을 사용하도록 설정합니다.  
  
1.  SQL Server 설치 경로에서 **yarn-site.xml** 파일을 찾습니다. 일반적인 경로는 다음과 같습니다.  
  
    ```  
  
    C:Program FilesMicrosoft SQL ServerMSSQL13.MSSQLSERVERMSSQLBinnPolybaseHadoopconf  
  
    ```  
  
2.  Hadoop 컴퓨터의 Hadoop 구성 디렉터리에서 동일한 파일을 찾습니다. 이 파일에서 구성 키 yarn.application.classpath의 값을 찾아서 복사합니다.  
  
3.  SQL Server 컴퓨터의 **yarn.site.xml 파일** 에서 **yarn.application.classpath** 속성을 찾은 다음 Hadoop 컴퓨터의 값을 value 요소에 붙여넣습니다.  
  
4. 모든 CDH 5.X 버전에서 mapreduce.application.classpath 구성 매개 변수를 yarn.site.xml 파일의 끝이나 mapred-site.xml 파일에 추가해야 합니다. HortonWorks는 yarn.application.classpath 구성 내에 이러한 구성을 포함하고 있습니다. 예제는 [PolyBase 구성](../../relational-databases/polybase/polybase-configuration.md)을 참조하세요.

 
## <a name="scale-out-polybase"></a>PolyBase 확장  
 PolyBase 그룹 기능을 사용하면 SQL Server 인스턴스 클러스터를 만들어 외부 데이터 원본에서 쿼리 성능을 향상하기 위해 스케일 아웃 방식으로 대규모 데이터를 처리할 수 있습니다.  
  
1.  여러 시스템에 PolyBase와 함께 SQL Server를 설치합니다.  
  
2.  헤드 노드로 하나의 SQL Server를 선택합니다.  
  
3.  [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)을 실행하여 다른 인스턴스를 계산 노드로 추가합니다.  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
4.  계산 노드에서 PolyBase 데이터 이동 서비스를 다시 시작합니다.  
  
 자세한 내용은 [PolyBase 확장 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md)을 참조하세요.  
  
## <a name="create-t-sql-objects"></a>T-SQL 개체 만들기  
 외부 데이터 원본, Hadoop 또는 Azure 저장소에 따라 개체를 만듭니다.  
  
### <a name="hadoop"></a>Hadoop  
  
```sql  
-- 1: Create a database scoped credential.  
-- Create a master key on the database. This is required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- 2: Create a database scoped credential  for Kerberos-secured Hadoop clusters.  
-- IDENTITY: the Kerberos user name.  
-- SECRET: the Kerberos password  
  
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1   
WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
  
-- 3:  Create an external data source.  
-- LOCATION (Required) : Hadoop Name Node IP address and port.  
-- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
-- CREDENTIAL (Optional):  the database scoped credential, created above.  
  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
        TYPE = HADOOP,   
        LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',   
        RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',   
        CREDENTIAL = HadoopUser1        
);  
  
-- 4: Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).    
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
-- 5:  Create an external table pointing to data stored in Hadoop.  
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
  
-- 6:  Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
### <a name="azure-blob-storage"></a>Azure BLOB 저장소  
  
```sql  
--1: Create a master key on the database.  
-- Required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- Create a database scoped credential  for Azure blob storage.  
-- IDENTITY: any string (this is not used for authentication to Azure storage).  
-- SECRET: your Azure storage account key.  
  
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential   
WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';  
  
--2:  Create an external data source.  
-- LOCATION:  Azure account storage account name and blob container name.  
-- CREDENTIAL: The database scoped credential created above.  
  
CREATE EXTERNAL DATA SOURCE AzureStorage with (  
        TYPE = HADOOP,   
        LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
        CREDENTIAL = AzureStorageCredential  
);  
  
--3:  Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).  
  
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
--4: Create an external table.  
-- The external table points to data stored in Azure storage.  
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
  
--5: Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
## <a name="polybase-queries"></a>PolyBase 쿼리  
 세 가지 함수가 PolyBase에 적합합니다.  
  
-   외부 테이블에 대한 임시 쿼리입니다.  
  
-   데이터 가져오기  
  
-   데이터 내보내기  
  
### <a name="query-examples"></a>쿼리 예제  
  
-   임시 쿼리  
  
    ```tsql  
    -- PolyBase Scenario 1: Ad-Hoc Query joining relational with Hadoop data   
    -- Select customers who drive faster than 35 mph: joining structured customer data stored   
    -- in SQL Server with car sensor data stored in Hadoop.  
    SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,   
            Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
    FROM Insured_Customers, CarSensor_Data  
    WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35   
    ORDER BY CarSensor_Data.Speed DESC  
    OPTION (FORCE EXTERNALPUSHDOWN);    -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
    ```  
  
-   데이터 가져오기  
  
    ```tsql  
    -- PolyBase Scenario 2: Import external data into SQL Server.  
    -- Import data for fast drivers into SQL Server to do more in-depth analysis and  
    -- leverage Columnstore technology.  
  
    SELECT DISTINCT   
            Insured_Customers.FirstName, Insured_Customers.LastName,   
            Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
    INTO Fast_Customers from Insured_Customers INNER JOIN   
    (  
            SELECT * FROM CarSensor_Data where Speed > 35   
    ) AS SensorD  
    ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
    ORDER BY YearlyIncome  
  
    CREATE CLUSTERED COLUMNSTORE INDEX CCI_FastCustomers ON Fast_Customers;  
    ```  
  
-   데이터 내보내기  
  
    ```  
    -- PolyBase Scenario 3: Export data from SQL Server to Hadoop.  
  
    -- Enable INSERT into external table  
    sp_configure ‘allow polybase export’, 1;  
    reconfigure  
  
    -- Create an external table.   
    CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
            [FirstName] char(25) NOT NULL,   
            [LastName] char(25) NOT NULL,   
            [YearlyIncome] float NULL,   
            [MaritalStatus] char(1) NOT NULL  
    )  
    WITH (  
            LOCATION='/old_data/2009/customerdata',  
            DATA_SOURCE = HadoopHDP2,  
            FILE_FORMAT = TextFileFormat,  
            REJECT_TYPE = VALUE,  
            REJECT_VALUE = 0  
    );  
  
    -- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
    INSERT INTO dbo.FastCustomer2009  
    SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
    ON (T1.CustomerKey = T2.CustomerKey)  
    WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
    ```  
  
## <a name="managing-polybase-objects-in-ssms"></a>SSMS에서 PolyBase 개체 관리  
 SSMS에서 외부 테이블은 별도 폴더인 **외부 테이블**에 표시됩니다. 외부 데이터 원본 및 외부 파일 형식은 **외부 리소스**의 하위 폴더에 있습니다.  
  
 ![SSMS에서 PolyBase 개체](../../relational-databases/polybase/media/polybase-management.png "PolyBase objects in SSMS")  
  
## <a name="troubleshooting"></a>문제 해결  
 DMV를 사용하여 성능 및 쿼리 문제를 해결합니다. 자세한 내용은 [PolyBase 문제 해결](../../relational-databases/polybase/polybase-troubleshooting.md)을 참조하세요.  
  
 SQL Server 2016 RC1에서 RC2 또는 RC3으로 업그레이드한 후 쿼리가 실패할 수 있습니다. 자세한 내용 및 해결 방법은 [SQL Server 2016 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md) 를 참조하고 "PolyBase"를 검색하세요.  
  
## <a name="next-steps"></a>다음 단계  
 확장 기능을 이해하려면 [PolyBase 확장 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md)을 참조하세요.  PolyBase를 모니터링하려면 [PolyBase 문제 해결](../../relational-databases/polybase/polybase-troubleshooting.md)을 참조하세요. PolyBase 성능 문제를 해결하려면 [PolyBase troubleshooting with dynamic management views](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)을(를) 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [PolyBase 가이드](../../relational-databases/polybase/polybase-guide.md)   
 [PolyBase 확장 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md)   
 [PolyBase 저장 프로시저](http://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)   
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  

