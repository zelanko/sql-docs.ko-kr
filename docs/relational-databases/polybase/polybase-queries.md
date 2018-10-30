---
title: PolyBase 쿼리 시나리오 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
keywords:
- PolyBase
helpviewer_keywords:
- PolyBase, import and export
- Hadoop, import with PolyBase
- Hadoop, export with PolyBase
- Azure blob storage, import with PolyBase
- Azure blob storage, export with PolyBase
ms.assetid: 2c5aa2bd-af7d-4f57-9a28-9673c2a4c07e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fb91a4603fa55fa967c51e25d24fcd33bc211218
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50099994"
---
# <a name="polybase-query-scenarios"></a>PolyBase 쿼리 시나리오

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 아티클에서는 SQL Server(2016부터)의 [PolyBase](../../relational-databases/polybase/polybase-guide.md) 기능을 사용하는 쿼리의 예제를 제공합니다. 이러한 예제를 사용하기 전에 먼저 PolyBase를 설치 및 구성해야 합니다. 자세한 내용은 [PolyBase 개요](polybase-guide.md)를 참조하세요.
  
외부 테이블에 대해 Transact-SQL 문을 실행하거나 BI 도구를 사용하여 외부 테이블을 쿼리합니다.
  
## <a name="select-from-external-table"></a>SELECT from external table  

정의된 외부 테이블의 데이터를 반환하는 간단한 쿼리입니다.  

```sql  
SELECT TOP 10 * FROM [dbo].[SensorData];   
```

조건자를 포함하는 간단한 쿼리입니다.

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65;
```

## <a name="join-external-tables-with-local-tables"></a>JOIN external tables with local tables

```sql
SELECT InsuranceCustomers.FirstName,   
   InsuranceCustomers.LastName,   
   SensorData.Speed  
FROM InsuranceCustomers INNER JOIN SensorData    
ON InsuranceCustomers.CustomerKey = SensorData.CustomerKey   
WHERE SensorData.Speed > 65   
ORDER BY SensorData.Speed DESC  
  
```  

## <a name="import-data"></a>데이터 가져오기

Hadoop 또는 Azure Storage의 데이터를 영구적으로 저장하기 위해 SQL Server로 가져옵니다. SELECT INTO를 사용하여 외부 테이블이 참조하는 데이터를 SQL Server에 영구적으로 저장하기 위해 가져옵니다. 먼저 대략적인 관계형 테이블을 만든 다음 두 번째 단계에서 테이블 위에 columnstore 인덱스를 만듭니다.

```sql
-- PolyBase scenario - import external data into SQL Server
-- Import data for fast drivers into SQL Server to do more in-depth analysis
-- Leverage columnstore technology
  
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

## <a name="export-data"></a>데이터 내보내기

SQL Server에서 Hadoop 또는 Azure Storage로 데이터를 내보냅니다. 

먼저, ‘PolyBase 내보내기 허용’의 `sp_configure` 값을 1로 설정하여 내보내기 기능을 사용하도록 설정합니다. 그런 다음 대상 디렉터리를 가리키는 외부 테이블을 만듭니다. 대상 디렉터리가 아직 없는 경우 CREATE EXTERNAL TABLE 문은 대상 디렉터리를 만듭니다. 그런 다음, INSERT INTO를 사용하여 로컬 SQL Server 테이블에서 외부 데이터 원본으로 데이터를 내보냅니다. 

SELECT 문의 결과는 지정된 파일 형식의 지정된 위치로 내보내집니다. 외부 파일의 이름은 *QueryID_date_time_ID.format*입니다. 여기서 *ID* 는 증분 식별자이고 *형식* 은 내보낸된 데이터 형식입니다. 예를 들어 1개의 파일 이름이 QID776_20160130_182739_0.orc일 수 있습니다.

> [!NOTE]
> PolyBase를 통해 데이터를 Hadoop 또는 Azure Blob Storage로 내보낼 때 CREATE EXTERNAL TABLE 명령에서 정의된 열 이름(메타데이터)이 아닌 데이터만 내보내집니다.

```sql  
-- PolyBase scenario  - export data from SQL Server to Hadoop
-- Create an external table
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
INSERT INTO dbo.FastCustomers2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```

## <a name="new-catalog-views"></a>새 카탈로그 뷰

아래의 새 카탈로그 뷰는 외부 리소스를 표시합니다.

```sql
SELECT * FROM sys.external_data_sources;   
SELECT * FROM sys.external_file_formats;  
SELECT * FROM sys.external_tables;  
```

 다음을 사용하여 테이블이 외부 테이블인지를 확인: `is_external`  

```sql  
SELECT name, type, is_external FROM sys.tables WHERE name='myTableName'   
```  

## <a name="next-steps"></a>다음 단계  

문제 해결에 대한 자세한 내용은 [PolyBase 문제 해결](../../relational-databases/polybase/polybase-troubleshooting.md)을 참조하세요.
