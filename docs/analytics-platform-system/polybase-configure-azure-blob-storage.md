---
title: PolyBase를 사용 하 여 Azure Blob storage에서 외부 데이터에 액세스
description: 외부 Hadoop에 연결 하도록 병렬 데이터 웨어하우스에서 PolyBase를 구성 하는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ea61ea7e6983f9601783957eee6776f36eccfb4
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400722"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>Azure Blob storage에서 외부 데이터에 액세스 하도록 PolyBase 구성

이 문서에서는 SQL Server 인스턴스에서 PolyBase를 사용 하 여 Azure Blob storage의 외부 데이터를 쿼리 하는 방법을 설명 합니다.

> [!NOTE]
> APS는 현재 표준 범용 v1 LRS (로컬 중복) Azure Blob 저장소만 지원 합니다.

## <a name="prerequisites"></a>사전 요구 사항

 - 구독의 Azure Blob storage입니다.
 - Azure Blob 저장소에서 만든 컨테이너입니다.

### <a name="configure-azure-blob-storage-connectivity"></a>Azure Blob storage 연결 구성

먼저 Azure Blob storage를 사용 하도록 AP를 구성 합니다.

1. ' Hadoop 연결 '이 Azure Blob 저장소 공급자로 설정 된 [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 실행 합니다. 공급자의 값을 찾으려면 [PolyBase 연결 구성](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)을 참조하세요.

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure Blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. [어플라이언스 Configuration Manager](launch-the-configuration-manager.md)의 서비스 상태 페이지를 사용 하 여 APS 영역을 다시 시작 합니다.
  
## <a name="configure-an-external-table"></a>외부 테이블 구성

Azure Blob 저장소에서 데이터를 쿼리하려면 Transact-sql 쿼리에 사용할 외부 테이블을 정의 해야 합니다. 다음 단계에서는 외부 테이블을 구성하는 방법을 설명합니다.

1. 데이터베이스에 마스터 키를 만듭니다. 자격 증명 암호를 암호화 해야 합니다.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

1. Azure Blob 저장소에 대 한 데이터베이스 범위 자격 증명을 만듭니다.

   ```sql
   -- IDENTITY: any string (this is not used for authentication to Azure storage).  
   -- SECRET: your Azure storage account key.  
   CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
   WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';
   ```

1. [외부 데이터 원본 만들기](../t-sql/statements/create-external-data-source-transact-sql.md)를 사용 하 여 외부 데이터 원본을 만듭니다.

   ```sql
   -- LOCATION:  Azure account storage account name and blob container name.  
   -- CREDENTIAL: The database scoped credential created above.  
   CREATE EXTERNAL DATA SOURCE AzureStorage with (  
         TYPE = HADOOP,
         LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
         CREDENTIAL = AzureStorageCredential  
   );  
   ```

1. [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md)을 사용하여 외부 파일 형식을 만듭니다.

   ```sql
   -- FORMAT TYPE: Type of format in Azure Blob storage (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   -- In this example, the files are pipe (|) delimited
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

1. [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md)을 사용하여 Azure Storage에 저장된 데이터를 가리키는 외부 테이블을 만듭니다. 이 예제에서 외부 데이터는 차량 센서 데이터를 포함합니다.

   ```sql
   -- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
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

1. 외부 테이블에 대한 통계를 만듭니다.

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>PolyBase 쿼리

세 가지 함수가 PolyBase에 적합합니다.  
  
- 외부 테이블에 대 한 임시 쿼리  
- 데이터 가져오기  
- 데이터 내보내기  

다음 쿼리는 가상 차량 센서 데이터를 포함하는 예제를 제공합니다.

### <a name="ad-hoc-queries"></a>임시 쿼리  

다음 임시 쿼리는 Azure Blob storage의 데이터와 관계형을 조인 합니다. 35입니다 보다 빠르게 구동 되는 고객을 선택 하 고, SQL Server에 저장 된 구조화 된 고객 데이터를 Azure Blob storage에 저장 된 자동차 센서 데이터로 조인 합니다.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
```  

### <a name="importing-data"></a>데이터 가져오기  

다음 쿼리는 외부 데이터를 APS로 가져옵니다. 이 예제에서는 fast driver에 대 한 데이터를 AP로 가져와서 심층 분석을 수행 합니다. 성능 향상을 위해 AP의 Columnstore 기술을 활용 합니다.  

```sql
CREATE TABLE Fast_Customers
WITH
(CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH (CustomerKey))
AS
SELECT DISTINCT
      Insured_Customers.CustomerKey, Insured_Customers.FirstName, Insured_Customers.LastName,   
      Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
from Insured_Customers INNER JOIN   
(  
      SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
```  

### <a name="exporting-data"></a>데이터 내보내기  

다음 쿼리는 APS에서 Azure Blob 저장소로 데이터를 내보냅니다. 관계형 데이터를 쿼리할 수 있는 동안 Azure Blob storage에 보관 하는 데 사용할 수 있습니다.

```sql
-- Export data: Move old data to Azure Blob storage while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = AzureStorage,  
      FILE_FORMAT = TextFileFormat
)  
AS
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssdt"></a>SSDT에서 PolyBase 개체 보기  

SQL Server Data Tools에서 외부 테이블은 별도의 폴더 **외부 테이블**에 표시 됩니다. 외부 데이터 원본 및 외부 파일 형식은 **외부 리소스**의 하위 폴더에 있습니다.  
  
![SSDT의 PolyBase 개체](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>다음 단계

PolyBase에 대한 자세한 내용은 [PolyBase란?](../relational-databases/polybase/polybase-guide.md)을 참조하세요. 

