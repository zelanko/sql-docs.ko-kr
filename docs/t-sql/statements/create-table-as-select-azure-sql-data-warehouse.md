---
title: CREATE TABLE AS SELECT(Azure SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 10/07/2016
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d1e08f88-64ef-4001-8a66-372249df2533
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 511be25daa32daa1a8d80707043280171f76edbc
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53980219"
---
# <a name="create-table-as-select-azure-sql-data-warehouse"></a>CREATE TABLE AS SELECT(Azure SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

CREATE TABLE AS SELECT(CTAS)는 사용할 수 있는 매우 중요한 T-SQL 기능 중 하나이며 SELECT 문의 출력을 기반으로 새 테이블을 만드는 완전히 병렬화된 작업입니다. CTAS는 테이블의 복사본을 만드는 가장 간단하고 빠른 방법입니다.   
 
 예를 들어 CTAS를 사용하여 다음을 수행할 수 있습니다.  
  
-   서로 다른 해시 배포 열로 테이블을 다시 만듭니다.
-   테이블을 복제본으로 다시 만듭니다.   
-   테이블의 몇몇 열에 대해서만 columnstore 인덱스를 만듭니다.  
-   외부 데이터를 쿼리하거나 가져옵니다.  

> [!NOTE]  
> CTAS는 테이블을 만드는 기능에 추가되므로 이 토픽에서는 CREATE TABLE 토픽을 반복하지 않으려고 합니다. 그 대신, CTAS와 CREATE TABLE 문의 차이점을 설명합니다. CREATE TABLE 세부 정보는 [CREATE TABLE(Azure SQL Data Warehouse)](https://msdn.microsoft.com/library/mt203953/) 문을 참조하세요. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
<a name="syntax-bk"></a>

## <a name="syntax"></a>구문   

```  
CREATE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    [ ( column_name [ ,...n ] ) ]  
    WITH ( 
      <distribution_option> -- required
      [ , <table_option> [ ,...n ] ]    
    )  
    AS <select_statement>   
[;]  

<distribution_option> ::=
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN 
      | DISTRIBUTION = REPLICATE
    }   

<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) --default is ASC 
    }  
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] --default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) ) 
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT select_criteria  

```  

<a name="arguments-bk"></a>
  
## <a name="arguments"></a>인수  
자세한 내용은 CREATE TABLE의 [인수 섹션](https://msdn.microsoft.com/library/mt203953/#Arguments)을 참조하세요.  

<a name="column-options-bk"></a>

### <a name="column-options"></a>열 옵션
`column_name` [ ,...`n` ]   
 열 이름은 CREATE TABLE에서 설명한 [열 옵션](https://msdn.microsoft.com/library/mt203953/#ColumnOptions)을 허용하지 않습니다.  그 대신, 새 테이블에 대해 하나 이상의 열 이름으로 이루어진 선택적 목록을 제공할 수 있습니다. 새 테이블의 열은 지정하는 이름을 사용합니다. 열 이름을 지정하는 경우 열 목록의 열 수가 선택 결과의 열 수와 일치해야 합니다. 열 이름을 지정하지 않으면 새 대상 테이블은 SELECT 문 결과의 열 이름을 사용합니다. 
  
 데이터 형식, 데이터 정렬 또는 NULL 허용 여부 등의 다른 열 옵션을 지정할 수 없습니다. 이러한 각각의 특성은 `SELECT` 문의 결과에서 파생됩니다. 그러나 SELECT 문을 사용하여 특성을 변경할 수 있습니다. 예제는 [CTAS를 사용하여 열 특성 변경](#ctas-change-column-attributes-bk)을 참조하세요.   

<a name="table-distribution-options-bk"></a>

### <a name="table-distribution-options"></a>테이블 분포 옵션

`DISTRIBUTION` = `HASH`(*distribution_column_name*) | ROUND_ROBIN | REPLICATE      
CTAS 문은 분포 옵션을 요구하며 기본값을 갖지 않습니다. 이 점이 기본값을 갖는 CREATE TABLE과 다릅니다. 

세부 정보 및 최선의 분포 열을 선택하는 방법을 이해하려면 CREATE TABLE의 [테이블 분포 옵션](https://msdn.microsoft.com/library/mt203953/#TableDistributionOptions) 섹션을 참조하세요. 

<a name="table-partition-options-bk"></a>

### <a name="table-partition-options"></a>테이블 파티션 옵션
CTAS 문은 원본 테이블이 분할되었더라도 기본적으로 분할되지 않은 테이블을 만듭니다. CTAS 문으로 분할된 테이블을 만들려면 파티션 옵션을 지정해야 합니다. 

자세한 내용은 CREATE TABLE의 [테이블 파티션 옵션](https://msdn.microsoft.com/library/mt203953/#TablePartitionOptions)을 참조하세요.

<a name="select-options-bk"></a>

### <a name="select-options"></a>옵션 선택
SELECT 문은 CTAS와 CREATE TABLE 간의 기본적인 차이점입니다.  

 `WITH` *common_table_expression*  
 CTE(공통 테이블 식)라고도 하는 임시로 이름이 지정된 결과 집합을 지정합니다. 자세한 내용은 [WITH common_table_expression&#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)을 참조하세요.  
  
 `SELECT` *select_criteria*  
 새 테이블을 SELECT 문의 결과로 채웁니다. *select_criteria*는새 테이블에 복사할 데이터를 결정하는 SELECT 문의 본문입니다. SELECT 문에 대한 자세한 내용은 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)을 참조하세요.  
  
<a name="permissions-bk"></a>  
  
## <a name="permissions"></a>Permissions  
CTAS를 사용하려면 *select_criteria*에 참조된 임의의 개체에 대한 `SELECT` 권한이 필요합니다.

테이블을 만들기 위한 권한은 CREATE TABLE의 [권한](https://msdn.microsoft.com/library/mt203953/#Permissions)을 참조하세요. 
  
<a name="general-remarks-bk"></a>
  
## <a name="general-remarks"></a>일반적인 주의 사항
자세한 내용은 CREATE TABLE의 [일반적인 참고사항](https://msdn.microsoft.com/library/mt203953/#GeneralRemarks)을 참조하세요.

<a name="limitations-bk"></a>

## <a name="limitations-and-restrictions"></a>제한 사항  
Azure SQL Data Warehouse는 아직 자동 만들기 또는 자동 업데이트 통계를 지원하지 않습니다.  최상의 쿼리 성능을 얻으려면 CTAS를 실행한 후, 그리고 데이터에 중요한 변경이 일어난 후 모든 테이블의 모든 열에 대한 통계를 작성해야 합니다. 자세한 내용은 [CREATE STATISTICS(Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.

[SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md)은 CTAS에 아무런 영향도 주지 않습니다. 비슷한 동작을 얻으려면 [TOP&#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)를 사용합니다.  
 
자세한 내용은 CREATE TABLE의 [제한 사항](https://msdn.microsoft.com/library/mt203953/#LimitationsRestrictions)을 참조하세요.

<a name="locking-behavior-bk"></a>
  
## <a name="locking-behavior"></a>잠금 동작  
 자세한 내용은 CREATE TABLE의 [잠금 동작](https://msdn.microsoft.com/library/mt203953/#LockingBehavior)을 참조하세요.
 
<a name="performance-bk"></a>
 
 ## <a name="performance"></a>성능 

해시 분포 테이블의 경우 조인 및 집계의 성능을 향상시키기 위해 CTAS를 사용하여 서로 다른 분포 열을 선택할 수 있습니다. 서로 다른 분포 열의 선택을 원하지 않는 경우, 같은 분포 열을 지정하면 행이 다시 배포되는 것을 방지할 수 있으므로 최상의 CTAS 성능을 얻습니다. 

CTAS를 사용하여 테이블을 만드는데 성능이 중요하지 않은 경우 분포 열에 대해 결정을 내릴 필요가 없도록 `ROUND_ROBIN`을 지정할 수 있습니다.

이후 쿼리에서 데이터 이동을 방지하려면 `REPLICATE`를 지정할 수 있지만 각 Compute 노드에 대해 전체 테이블 복사본을 로드하기 위해 저장소가 증가합니다.  


<a name="examples-copy-table-bk"></a>

## <a name="examples-for-copying-a-table"></a>테이블을 복사하는 예제

<a name="ctas-copy-table-bk"></a>

### <a name="a-use-ctas-to-copy-a-table"></a>1. CTAS를 사용하여 테이블 복사 
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse

`CTAS`의 매우 일반적인 사용 중 하나는 아마도 DDL(데이터 정의 언어)을 변경할 수 있도록 테이블의 복사본을 만드는 작업일 것입니다. 예를 들어 원래 테이블을 `ROUND_ROBIN`으로 만들었는데 이제 이 테이블을 열에 배포된 테이블로 만들려고 하는 경우 `CTAS`를 사용하여 분포 열을 변경합니다. 또한 `CTAS`를 사용하여 분할, 인덱싱 또는 열 형식을 변경할 수도 있습니다.

`CREATE TABLE`에서 분포 열을 지정하지 않았으므로 배포된 `ROUND_ROBIN`의 기본 배포 유형을 사용하여 이 테이블을 만들었다고 생각해 보겠습니다.

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

이제 클러스터형 columnstore 테이블의 성능을 이용할 수 있도록 클러스터형 columnstore 인덱스로 이 테이블의 새 복사본을 만들려고 합니다. 또한 이 열에 대한 조인을 예상하고 ProductKey에 대한 조인 중에 데이터 이동을 방지하려고 하므로 ProductKey에 대해 이 테이블을 배포하려고 합니다. 마지막으로 이전 파티션을 삭제하여 이전 데이터를 빨리 삭제할 수 있도록 OrderDateKey에 대한 파티션을 추가하려고 합니다. 다음은 이전 테이블을 새 테이블에 복사하는 CTAS 문입니다.

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

끝으로 새 테이블에서 바꿀 테이블 이름을 변경한 다음, 이전 테이블을 삭제할 수 있습니다.

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

<a name="examples-column-bk"></a>

## <a name="examples-for-column-options"></a>열 옵션에 대한 예제

<a name="ctas-change-column-attributes-bk"></a>

### <a name="b-use-ctas-to-change-column-attributes"></a>2. CTAS를 사용하여 열 특성 변경 
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse

이 예제에서는 CTAS를 사용하여 DimCustomer2 테이블의 여러 열에 대해 데이터 형식, NULL 허용 여부 및 데이터 정렬을 변경합니다.  
  
```  
-- Original table 
CREATE TABLE [dbo].[DimCustomer2] (  
    [CustomerKey] int NOT NULL,  
    [GeographyKey] int NULL,  
    [CustomerAlternateKey] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL  
)  
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([CustomerKey]));  
  
-- CTAS example to change data types, nullability, and column collations  
CREATE TABLE test  
WITH (HEAP, DISTRIBUTION = ROUND_ROBIN)  
AS  
SELECT  
    CustomerKey AS CustomerKeyNoChange,  
    CustomerKey*1 AS CustomerKeyChangeNullable,  
    CAST(CustomerKey AS DECIMAL(10,2)) AS CustomerKeyChangeDataTypeNullable,  
    ISNULL(CAST(CustomerKey AS DECIMAL(10,2)),0) AS CustomerKeyChangeDataTypeNotNullable,  
    GeographyKey AS GeographyKeyNoChange,  
    ISNULL(GeographyKey,0) AS GeographyKeyChangeNotNullable,  
    CustomerAlternateKey AS CustomerAlternateKeyNoChange,  
    CASE WHEN CustomerAlternateKey = CustomerAlternateKey 
        THEN CustomerAlternateKey END AS CustomerAlternateKeyNullable,  
    CustomerAlternateKey COLLATE Latin1_General_CS_AS_KS_WS AS CustomerAlternateKeyChangeCollation  
FROM [dbo].[DimCustomer2]  
  
-- Resulting table 
CREATE TABLE [dbo].[test] (
    [CustomerKeyNoChange] int NOT NULL, 
    [CustomerKeyChangeNullable] int NULL, 
    [CustomerKeyChangeDataTypeNullable] decimal(10, 2) NULL, 
    [CustomerKeyChangeDataTypeNotNullable] decimal(10, 2) NOT NULL, 
    [GeographyKeyNoChange] int NULL, 
    [GeographyKeyChangeNotNullable] int NOT NULL, 
    [CustomerAlternateKeyNoChange] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL, 
    [CustomerAlternateKeyNullable] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NULL, 
    [CustomerAlternateKeyChangeCollation] nvarchar(15) COLLATE Latin1_General_CS_AS_KS_WS NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN);
```
 
마지막 단계로 [RENAME &#40;Transact-SQL&#41;](../../t-sql/statements/rename-transact-sql.md)을 사용하여 테이블을 전환할 수 있습니다. 이렇게 하면 DimCustomer2가 새 테이블이 됩니다.

```
RENAME OBJECT DimCustomer2 TO DimCustomer2_old;
RENAME OBJECT test TO DimCustomer2;

DROP TABLE DimCustomer2_old;
```

<a name="examples-table-distribution-bk"></a>

## <a name="examples-for-table-distribution"></a>테이블 배포 예제

<a name="ctas-change-distribution-method-bk"></a>

### <a name="c-use-ctas-to-change-the-distribution-method-for-a-table"></a>3. CTAS를 사용하여 테이블에 대한 배포 방법 변경
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse

이 간단한 예제에서는 테이블에 대한 배포 방법을 변경하는 방법을 보여줍니다. 이 작업을 수행하는 방법의 원리를 보여주기 위해 해시 배포 테이블을 라운드 로빈으로 변경한 다음, 라운드 로빈 테이블을 다시 해시 배포로 변경해 보겠습니다. 마지막 테이블은 원본 테이블과 일치합니다. 

대부분의 경우 해시 테이블을 라운드 로빈 테이블로 변경할 필요가 없을 것입니다. 오히려 라운드 로빈 테이블을 해시 배포 테이블로 변경해야 할 경우가 더 많습니다. 예를 들어 조인 성능을 개선하기 위해 처음에 새 테이블을 라운드 로빈으로 로드한 다음, 나중에 해당 테이블을 해시 배포 테이블로 변경할 수 있습니다.

이 예에서는 AdventureWorksDW 예제 데이터베이스를 사용합니다. SQL Data Warehouse 버전을 로드하는 방법은 [SQL Data Warehouse에 샘플 데이터 로드](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-sample-databases/)를 참조하세요.
 
```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a round-robin table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];

```  
다음으로 이 테이블을 다시 해시 배포 테이블로 변경합니다.

```
-- You just made DimSalesTerritory a round-robin table.
-- Change it back to the original hash-distributed table. 
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH(SalesTerritoryKey) 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
<a name="ctas-change-to-replicated-bk"></a>

### <a name="d-use-ctas-to-convert-a-table-to-a-replicated-table"></a>D. CTAS를 사용하여 테이블을 복제된 테이블로 변환  
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse 

이 예제는 라운드 로빈 또는 해시 배포 테이블을 복제된 테이블로 변환하는 경우에 적용됩니다. 이 특정 예제에서는 이전의 배포 유형 변경 방법을 선택하고 한 단계를 더 실행합니다.  DimSalesTerritory는 하나의 차원이고 더 작은 테이블일 가능성이 있으므로 다른 테이블에 조인할 때 데이터 이동을 방지하기 위해 테이블을 복제본으로 다시 만드는 방법을 선택할 수 있습니다. 

```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a replicated table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
### <a name="e-use-ctas-to-create-a-table-with-fewer-columns"></a>E. CTAS를 사용하여 열 수가 적은 테이블 만들기
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse 

다음 예제에서는 `myTable (c, ln)`이라는 라운드 로빈 배포 테이블을 만듭니다. 새 테이블은 열을 두 개만 포함하며 SELECT 문에 열 이름으로 열 별칭을 사용합니다.  
  
```  
CREATE TABLE myTable  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT CustomerKey AS c, LastName AS ln  
    FROM dimCustomer;  
  
```  

<a name="examples-query-hints-bk"></a>

## <a name="examples-for-query-hints"></a>쿼리 힌트 예제

<a name="ctas-query-hint-bk"></a>

### <a name="f-use-a-query-hint-with-create-table-as-select-ctas"></a>F. CREATE TABLE AS SELECT(CTAS)와 함께 쿼리 힌트 사용  
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse
  
이 쿼리는 CTAS 문에 쿼리 조인 힌트를 사용하는 기본 구문을 보여줍니다. 쿼리가 제출된 후 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는 각 개별 배포에 대한 쿼리 계획을 생성할 때 해시 조인 방법을 적용합니다. 해시 조인 쿼리 힌트에 대한 자세한 내용은 [OPTION 절 &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)을 참조하세요.  
  
```  
CREATE TABLE dbo.FactInternetSalesNew  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN   
  )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  

<a name="examples-external-tables"></a>

## <a name="examples-for-external-tables"></a>외부 테이블 예제

<a name="ctas-azure-blob-storage-bk"></a>

### <a name="g-use-ctas-to-import-data-from-azure-blob-storage"></a>G. CTAS를 사용하여 Azure Blob Storage에서 데이터 가져오기  
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse  

외부 테이블에서 데이터를 가져오려면 CREATE TABLE AS SELECT를 사용하여 외부 테이블에서 선택합니다. 외부 테이블에서 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]로 가져올 데이터를 선택하는 구문은 일반 테이블에서 데이터를 선택하는 구문과 같습니다.  
  
 다음 예제에서는 Azure Blob Storage 계정의 데이터에 대한 외부 테이블을 정의합니다. 그런 다음, CREATE TABLE AS SELECT를 사용하여 외부 테이블에서 선택합니다. 그러면 Azure Blob Storage의 텍스트로 분리된 파일의 데이터를 가져와서 새 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 테이블에 저장합니다.  
  
```  
--Use your own processes to create the text-delimited files on Azure blob storage.  
--Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION='/logs/clickstream/2015/',  
    DATA_SOURCE = MyAzureStorage,  
    FILE_FORMAT = TextFileFormat)  
;  
  
--Use CREATE TABLE AS SELECT to import the Azure blob storage data into a new   
--SQL Data Warehouse table called ClickStreamData  
CREATE TABLE ClickStreamData   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;  
```  

<a name="ctas-import-Hadoop-bk"></a>
  
### <a name="h-use-ctas-to-import-hadoop-data-from-an-external-table"></a>H. CTAS를 사용하여 외부 테이블에서 Hadoop 데이터 가져오기  
적용 대상: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
외부 테이블에서 데이터를 가져오려면 CREATE TABLE AS SELECT를 사용하여 외부 테이블에서 선택합니다. 외부 테이블에서 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]로 가져올 데이터를 선택하는 구문은 일반 테이블에서 데이터를 선택하는 구문과 같습니다.  
  
 다음 예제에서는 Hadoop 클러스터에 외부 테이블을 정의합니다. 그런 다음, CREATE TABLE AS SELECT를 사용하여 외부 테이블에서 선택합니다. 이렇게 해서 Hadoop의 텍스트로 분리된 파일의 데이터를 가져와서 새 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 테이블에 저장합니다.  
  
```  
-- Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION = 'hdfs://MyHadoop:5000/tpch1GB/employee.tbl',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|')  
)  
;  
  
-- Use your own processes to create the Hadoop text-delimited files 
-- on the Hadoop Cluster.  
  
-- Use CREATE TABLE AS SELECT to import the Hadoop data into a new 
-- table called ClickStreamPDW  
CREATE TABLE ClickStreamPDW   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;   
```  
 
<a name="examples-workarounds-bk"></a>
 
## <a name="examples-using-ctas-to-replace-sql-server-code"></a>CTAS를 사용하여 SQL Server 코드를 바꾸는 예제

CTAS를 사용하여 몇몇 지원되지 않는 기능을 해결합니다. 기존 코드를 CTAS 사용이 가능하도록 다시 작성하면 데이터 웨어하우스에 대해 코드를 실행할 수 있을 뿐만 아니라 대개 성능도 향상됩니다. 이러한 성능 향상은 완전히 병렬화된 디자인의 결과입니다. 

> [!NOTE]
> "CTAS를 먼저" 생각해 보십시오. `CTAS`를 사용하여 문제를 해결할 수 있다고 생각한다면 결과적으로 더 많은 데이터를 기록하더라도 그 방법이 최선의 방법입니다.
>

<a name="ctas-replace-select-into-bk"></a>

### <a name="i-use-ctas-instead-of-selectinto"></a>9. SELECT..INTO 대신에 CTAS 사용  
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse

SQL Server 코드는 일반적으로 SELECT..INTO를 사용하여 테이블을 SELECT 문의 결과로 채웁니다. 다음은 SQL Server SELECT..INTO 문의 예입니다.

```sql
SELECT *
INTO    #tmp_fct
FROM    [dbo].[FactInternetSales]
```

이 구문은 Azure SQL Data Warehouse 및 병렬 데이터 웨어하우스에서 지원되지 않습니다. 이 예제에서는 이전의 SELECT..INTO 문을 CTAS 문으로 다시 작성하는 방법을 보여줍니다. CTAS 구문에서 설명한 임의의 DISTRIBUTION 옵션을 선택할 수 있습니다. 이 예제에서는 ROUND_ROBIN 배포 방법을 사용합니다.

```sql
CREATE TABLE #tmp_fct
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<a name="ctas-replace-implicit-joins-bk"></a>

### <a name="j-use-ctas-and-implicit-joins-to-replace-ansi-joins-in-the-from-clause-of-an-update-statement"></a>J. CTAS 및 암시적 조인을 사용하여 `UPDATE` 문의 `FROM` 절에서 ANSI 조인 바꾸기  
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse  

ANSI 조인 구문을 사용하여 UPDATE 또는 DELETE를 수행하여 두 개 이상의 테이블을 함께 조인하는 복잡한 업데이트 작업이 있을 수 있습니다.

이 테이블을 업데이트해야 했다고 가정해 보십시오.

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(   [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,   [CalendarYear]                  SMALLINT        NOT NULL
,   [TotalSalesAmount]              MONEY           NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

원래 쿼리는 다음과 유사했을 것입니다.

```sql
UPDATE  acs
SET     [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT  [EnglishProductCategoryName]
        ,       [CalendarYear]
        ,       SUM([SalesAmount])              AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]       AS s
        JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
        JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
        WHERE   [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,       [CalendarYear]
        ) AS fis
ON  [acs].[EnglishProductCategoryName]  = [fis].[EnglishProductCategoryName]
AND [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

SQL Data Warehouse는 `UPDATE` 문의 `FROM` 절에서 ANSI 조인을 지원하지 않으므로 이 SQL Server 코드는 조금 변경해야 사용할 수 있습니다.

`CTAS`와 암시적 조인의 조합을 사용하여 이 코드를 대체할 수 있습니다.

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT  ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,       ISNULL(CAST([CalendarYear] AS SMALLINT),0)                      AS [CalendarYear]
,       ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                     AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]       AS s
JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
WHERE   [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,       [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

<a name="ctas-replace-ansi-joins-bk"></a>

### <a name="k-use-ctas-to-specify-which-data-to-keep-instead-of-using-ansi-joins-in-the-from-clause-of-a-delete-statement"></a>11. DELETE 문의 FROM 절에 ANSI 조인을 사용하는 대신에 CTAS를 사용하여 보관할 데이터 지정  
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse  

`CTAS`를 사용하는 것이 데이터를 삭제하기 위한 최선의 방법일 때가 있습니다. 단순히 데이터를 삭제하는 것이 아니라 보관할 데이터를 선택합니다. SQL Data Warehouse는 `DELETE` 문의 `FROM` 절에 ANSI 조인을 지원하지 않으므로 이 방법은 ANSI 조인 구문을 사용하는 `DELETE` 문에 특히 유용합니다.

변환된 DELETE 문의 예를 아래에 제공합니다.

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

<a name="ctas-simplify-merge-bk"></a>

### <a name="l-use-ctas-to-simplify-merge-statements"></a>12. CTAS를 사용하여 MERGE 문 단순화  
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse  

`CTAS`을 사용하여 MERGE 문을 적어도 부분적으로 대체할 수 있습니다. `INSERT`과 `UPDATE`를 단일 명령문으로 통합할 수 있습니다. 삭제된 레코드는 두 번째 문에서 닫혀야 합니다.

`UPSERT`의 예를 아래에 제공합니다.

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimProduct_upsert]  TO [DimProduct];

```

<a name="ctas-data-type-and-nullability-bk"></a>

### <a name="m-explicitly-state-data-type-and-nullability-of-output"></a>13. 출력의 데이터 형식 및 NULL 허용 여부를 명시적으로 서술  
적용 대상: Azure SQL Data Warehouse 및 병렬 Data Warehouse  

SQL Server 코드를 SQL Data Warehouse로 마이그레이션하는 경우 이 형식의 코딩 패턴을 발견할 것입니다.

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

직관적으로 이 코드를 CTAS로 마이그레이션하는 것이 옳을 것 같다는 생각이 들 것입니다. 그러나 여기에는 숨겨진 문제가 있습니다.

다음 코드는 동일한 결과를 산출하지 않습니다.

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

참고로 "결과" 열은 식의 데이터 형식 및 NULL 허용 여부 값을 이월합니다. 이로 인해 주의하지 않으면 값이 미묘하게 분산될 수 있습니다.

다음을 예제로 실행해 보십시오.

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

결과에 저장된 값이 다릅니다. 결과 열에 보관된 값이 다른 식에 사용되면 오류가 훨씬 더 심각해집니다.

![CREATE TABLE AS SELECT 결과](../../t-sql/statements/media/create-table-as-select-results.png)

이것은 데이터 마이그레이션의 경우 특히 중요합니다. 두 번째 쿼리는 틀림없이 더 정확하지만 문제가 있습니다. 데이터가 원본 시스템과 다르며 마이그레이션에서 무결성 문제가 발생합니다. 이는 "오답"이 실제로는 정답인, 드문 경우 중 하나입니다!

두 결과 간에 차이가 나타나는 이유는 암시적 형 변환 때문입니다. 첫 번째 예제에서 테이블은 열 정의를 정의합니다. 행이 삽입되면 암시적 형 변환이 일어납니다. 두 번째 예제에서는 식이 열의 데이터 형식을 정의하기 때문에 암시적 형 변환이 없습니다. 또한 두 번째 예제의 열은 NULL을 허용하는 열로 정의된 데 비해 첫 번째 예제는 허용하지 않는다는 데 주의하십시오. 첫 번째 예제에서 테이블이 만들어질 때 열의 NULL 허용 여부를 명시적으로 정의했습니다. 두 번째 예제에서는 NULL 여부가 식에 따라서만 결정되기 때문에 기본적으로 이로 인해 NULL 정의가 있는 셈입니다.  

이 문제를 해결하려면 `CTAS` 문의 `SELECT` 부분에서 형식 변환과 NULL 허용 여부를 명시적으로 설정해야 합니다. CREATE TABLE 부분에서는 이 속성을 설정할 수 없습니다.

아래 예제는 이 코드를 올바르게 수정하는 방법을 보여줍니다.

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

다음에 유의하세요.
- CAST 또는 CONVERT가 사용되었을 수 있음
- ISNULL을 사용하여 NULL 허용 여부를 COALESCE로 강제 설정
- ISNULL은 맨 바깥쪽의 함수
- ISNULL의 두 번째 부분은 상수(즉, 0)

> [!NOTE]
> NULL 허용 여부를 올바르게 설정하려면 `COALESCE`를 사용하지 말고 `ISNULL`을 사용해야 합니다. `COALESCE`는 결정적 함수가 아니므로 식의 결과는 언제나 NULL을 허용합니다. `ISNULL`은 그와 다르며 결정적입니다. 그러므로 `ISNULL` 함수의 두 번째 부분이 상수 또는 리터럴이면 결과 값은 NOT NULL입니다.

이 팁은 계산의 데이터 무결성을 확보하는 데에만 유용한 것이 아니라 테이블 파티션 전환에도 중요합니다. 이 테이블을 자신의 사실로 정의했다고 가정해 보겠습니다.

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

단, 값 필드는 원본 데이터의 일부가 아닌 계산된 식입니다.

분할된 데이터 세트를 만들려면 다음을 수행하는 것이 좋습니다.

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

쿼리는 아주 잘 실행될 것입니다. 문제는 파티션 전환의 수행을 시도할 때 나타납니다. 즉, 테이블 정의가 일치하지 않는 것입니다. 테이블 정의를 일치시키려면 CTAS를 수정해야 합니다.

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

따라서 형식 일관성과 CTAS에 대한 NULL 허용 여부 속성을 유지하는 것이 좋은 엔지니어링 구현 방식임을 알 수 있습니다. 계산에서 무결성을 유지하고 파티션 전환도 가능하도록 하는 것이 좋습니다.
 
## <a name="see-also"></a>참고 항목  
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [DROP EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-table-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER EXTERNAL TABLE &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ae1b23c-67f6-41d0-b614-7a8de914d145)  
  
  


