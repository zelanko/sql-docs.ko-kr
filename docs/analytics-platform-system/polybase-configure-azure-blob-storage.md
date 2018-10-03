---
title: Azure Blob storage에서 외부 데이터에 액세스 하는 PolyBase 구성 | Microsoft Docs
description: 외부 Hadoop 연결할 Parallel Data Warehouse에서 PolyBase를 구성 하는 방법을 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 09bac30e30a6549dd572b8594e5efeec6473ef2a
ms.sourcegitcommit: 5afec8b4b73ce1727e4e5cf875d1e1ce9df50eab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47450367"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>Azure Blob storage에서 외부 데이터에 액세스 하는 PolyBase를 구성 합니다.

문서는 Azure Blob storage에서 외부 데이터를 쿼리 하는 SQL Server 인스턴스에서 PolyBase를 사용 하는 방법을 설명 합니다.

> [!NOTE]
> AP는 현재 지원 표준 범용 v1 로컬 중복 (LRS) Azure Blob storage.

## <a name="prerequisites"></a>사전 요구 사항

 - 구독에서 azure Blob 저장소입니다.
 - Azure Blob storage에서 만든 컨테이너입니다.

### <a name="configure-azure-blob-storage-connectivity"></a>Azure Blob 저장소 연결 구성

먼저, Azure Blob storage를 사용 하는 AP를 구성 합니다.

1. 실행할 [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 'hadoop 연결' Azure Blob 저장소 공급자를 설정 합니다. 값 공급자에 대 한 참조 하세요 [PolyBase 연결 구성](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)합니다.

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure Blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. AP 지역에서 서비스 상태 페이지를 사용 하 여 다시 시작 [구성 관리자 어플라이언스](launch-the-configuration-manager.md)합니다.
  
## <a name="configure-an-external-table"></a>외부 테이블을 구성 합니다.

Azure Blob storage의 데이터를 쿼리하려면 Transact SQL 쿼리에 사용 하는 외부 테이블을 정의 해야 합니다. 다음 단계를 외부 테이블을 구성 하는 방법에 설명 합니다.

1. 데이터베이스 마스터 키를 만듭니다. 자격 증명 비밀을 암호화 해야 합니다.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

1. Azure Blob storage에 대 한 데이터베이스 범위 자격 증명을 만듭니다.

   ```sql
   -- IDENTITY: any string (this is not used for authentication to Azure storage).  
   -- SECRET: your Azure storage account key.  
   CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
   WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';
   ```

1. 사용 하 여 외부 데이터 원본 만들기 [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md)...

   ```sql
   -- LOCATION:  Azure account storage account name and blob container name.  
   -- CREDENTIAL: The database scoped credential created above.  
   CREATE EXTERNAL DATA SOURCE AzureStorage with (  
         TYPE = HADOOP,
         LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
         CREDENTIAL = AzureStorageCredential  
   );  
   ```

1. 사용 하 여 외부 파일 형식 만들기 [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md)합니다.

   ```sql
   -- FORMAT TYPE: Type of format in Azure Blob storage (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   -- In this example, the files are pipe (|) delimited
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

1. 사용 하 여 Azure storage에 저장 된 데이터를 가리키는 외부 테이블을 만듭니다 [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md)합니다. 이 예제에서는 외부 데이터는 차량 센서 데이터를 포함합니다.

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

1. 외부 테이블에서 통계를 만듭니다.

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>PolyBase 쿼리

세 가지 함수가 PolyBase에 적합합니다.  
  
- 외부 테이블에 대 한 임시 쿼리 합니다.  
- 데이터를 가져오는 중입니다.  
- 데이터를 내보내는 중입니다.  

다음 쿼리는 가상의 차량 센서 데이터를 사용 하 여 예제를 제공합니다.

### <a name="ad-hoc-queries"></a>임시 쿼리  

Azure Blob 저장소의 다음 임시 쿼리 관계형 데이터와 조인합니다. 35 속도로, Azure Blob storage에 저장 된 차량 센서 데이터를 사용 하 여 SQL Server에 저장 된 구조화 된 고객 데이터를 조인 보다 더 빠르게 드라이브 고객을 선택 합니다.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
```  

### <a name="importing-data"></a>데이터 가져오기  

다음 쿼리는 AP에 외부 데이터를 가져옵니다. 이 예제에서는 자세한 심층 분석을 위해 AP에 빠른 드라이버에 대 한 데이터를 가져옵니다. 성능 향상을 위해 AP의 Columnstore 기술을 활용 합니다.  

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

다음 쿼리 AP에서 Azure Blob storage로 데이터를 내보냅니다. Azure Blob으로 관계형 데이터를 보관할 수 동안 저장소를 쿼리할 수 있습니다.

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

## <a name="view-polybase-objects-in-ssdt"></a>SSDT에서 PolyBase 개체를 보려면  

SQL Server Data Tools, 외부 테이블을 별도 폴더에 표시 됩니다 **외부 테이블**합니다. 외부 데이터 원본 및 외부 파일 형식은 **외부 리소스**의 하위 폴더에 있습니다.  
  
![SSDT에서 PolyBase 개체](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>다음 단계

다음 문서에서 PolyBase를 모니터링 및 사용 방법 살펴보기

[PolyBase 사용 하 여 형식 매핑을](../relational-databases/polybase/polybase-type-mapping.md)합니다.  

