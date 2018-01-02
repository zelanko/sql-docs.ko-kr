---
title: "PolyBase 쿼리 | Microsoft 문서"
ms.custom: 
ms.date: 12/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
keywords: PolyBase
helpviewer_keywords:
- PolyBase, import and export
- Hadoop, import with PolyBase
- Hadoop, export with PolyBase
- Azure blob storage, import with PolyBase
- Azure blob storage, export with PolyBase
ms.assetid: 2c5aa2bd-af7d-4f57-9a28-9673c2a4c07e
caps.latest.revision: "18"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bad7cdb475aa1b9416e7a0463485293e0035de8d
ms.sourcegitcommit: 05e2814fac4d308196b84f1f0fbac6755e8ef876
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="polybase-queries"></a>PolyBase Queries
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 문서에서는 SQL Server 2016의 [PolyBase 가이드](../../relational-databases/polybase/polybase-guide.md) 기능을 사용하는 쿼리의 예제를 제공합니다. 이러한 예제를 사용하기 전에 PolyBase를 설정하는 데 필요한 T-SQL 문을 파악해야 합니다( [PolyBase T-SQL 개체](../../relational-databases/polybase/polybase-t-sql-objects.md)참조).
  
## <a name="queries"></a>쿼리  
 외부 테이블에 대해 Transact-SQL 문을 실행하거나 BI 도구를 사용하여 외부 테이블을 쿼리합니다.
  
## <a name="select-from-external-table"></a>SELECT from external table  
 정의된 외부 테이블의 데이터를 반환하는 간단한 쿼리입니다.  
  
```tsql  
SELECT TOP 10 * FROM [dbo].[SensorData];   
```
  
 조건자를 포함하는 간단한 쿼리입니다.

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65;
```

## <a name="join-external-tables-with-local-tables"></a>JOIN external tables with local tables

```
SELECT InsuranceCustomers.FirstName,   
                           InsuranceCustomers.LastName,   
                           SensorData.Speed  
FROM InsuranceCustomers INNER JOIN SensorData    
ON InsuranceCustomers.CustomerKey = SensorData.CustomerKey   
WHERE SensorData.Speed > 65   
ORDER BY SensorData.Speed DESC  
  
```  
  
## <a name="pushdown-computation-to-hadoop"></a>Hadoop에 대한 푸시다운 계산

여기에 푸시다운 변형이 표시됩니다.

### <a name="pushdown-for-selecting-a-subset-of-rows"></a>행의 하위 집합을 선택하기 위한 푸시다운

조건자 푸시다운을 사용하여 외부 테이블에서 행 하위 집합을 선택하는 쿼리의 성능을 향상시킬 수 있습니다.

이 예에서 SQL Server 2016은 Hadoop에서 `customer.account_balance < 200000` 조건자와 일치하는 행을 검색하는 맵 감소 작업을 시작합니다. 테이블의 모든 행을 검색하지 않고 쿼리가 성공적으로 완료될 수 있으므로 조건자 조건에 맞는 행만 SQL Server에 복사됩니다. 이렇게 하면 잔액 < 200000인 고객 수가 계정 잔액 >= 200000인 고객 수에 비해 작은 경우 상당한 시간이 절약되며 필요한 임시 저장소 공간이 줄어듭니다.

```
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="pushdown-for-selecting-a-subset-of-columns"></a>열의 하위 집합을 선택하기 위한 푸시다운

조건자 푸시다운을 사용하여 외부 테이블에서 열 하위 집합을 선택하는 쿼리의 성능을 향상시킬 수 있습니다.

이 쿼리에서 SQL Server는 맵 감소 작업을 시작하여 customer.name과 customer.zip_code라는 두 열의 데이터만 SQL Server PDW에 복사되도록 Hadoop 구분된 텍스트 파일을 전처리합니다.

```
SELECT customer.name, customer.zip_code FROM customer WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>기본 식과 연산자에 대한 푸시다운

SQL Server는 조건자 푸시다운에 대해 다음과 같은 기본 식과 연산자를 허용합니다.

+ 숫자, 날짜 및 시간 값에 대한 이진 비교 연산자(\<, >, =, !=, <>, >=, <=)

+ 산술 연산자(+, -, *, /, %)

+ 논리 연산자(AND, OR)

+ 단항 연산자(NOT, IS NULL, IS NOT NULL)

BETWEEN, NOT, IN 및 LIKE 연산자를 푸시다운할 수도 있습니다. 실제 동작은 쿼리 최적화 프로그램에서 기본 관계형 연산자를 사용하는 일련의 문으로 다시 작성하는 방법에 따라 달라집니다.

이 예제의 쿼리에는 Hadoop에 푸시다운할 수 있는 여러 조건자가 있습니다. SQL Server는 Hadoop에 맵 감소 작업을 푸시하여 `customer.account_balance <= 200000` 조건자를 수행할 수 있습니다. `BETWEEN 92656 and 92677` 식도 Hadoop에 푸시할 수 있는 이진 및 논리 연산으로 구성됩니다. `customer.account_balance and customer.zipcode`의 논리적 **AND**는 최종 식입니다.

이 조건자를 결합하면 맵 감소 작업에서 모든 WHERE 절을 수행할 수 있습니다. SELECT 조건에 맞는 데이터만 SQL Server PDW에 다시 복사됩니다.

```
SELECT * FROM customer WHERE customer.account_balance <= 200000 AND customer.zipcode BETWEEN 92656 AND 92677
```

### <a name="force-pushdown"></a>강제 푸시다운

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

### <a name="disable-pushdown"></a>푸시다운 사용 안 함

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
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

먼저, ‘PolyBase 내보내기 허용’의 `sp_configure` 값을 1로 설정하여 내보내기 기능을 사용하도록 설정합니다. 그런 다음 대상 디렉터리를 가리키는 외부 테이블을 만듭니다. 그런 다음 INSERT INTO를 사용하여 로컬 SQL Server 테이블에서 외부 데이터 원본으로 데이터를 내보냅니다. 

INSERT INTO 문은 대상 디렉터리가 없을 경우 새로 만듭니다. SELECT 문의 결과는 지정된 파일 형식으로 생성되어 지정한 위치로 내보내집니다. 외부 파일의 이름은 *QueryID_date_time_ID.format*입니다. 여기서 *ID* 는 증분 식별자이고 *형식* 은 내보낸된 데이터 형식입니다. 예를 들어 1개의 파일 이름이 QID776_20160130_182739_0.orc일 수 있습니다.

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
INSERT INTO dbo.FastCustomer2009  
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
