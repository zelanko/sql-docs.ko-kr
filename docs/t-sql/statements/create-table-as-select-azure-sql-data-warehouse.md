---
title: "TABLE AS SELECT (Azure SQL 데이터 웨어하우스) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 10/07/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d1e08f88-64ef-4001-8a66-372249df2533
caps.latest.revision: 40
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2f95f9bc6975593f2536848e2bb3a2b346eca538
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-as-select-azure-sql-data-warehouse"></a>TABLE AS SELECT (Azure SQL 데이터 웨어하우스) 만들기
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

만들 테이블 AS 선택 (CTAS에는) 사용할 수 있는 가장 중요 한 T-SQL 기능 중 하나입니다. SELECT 문의 출력에 따라 새 테이블을 만드는 완벽 하 게 병렬화 된 연산입니다. CTAS에는 테이블의 복사본을 만드는 가장 간단 하 고 가장 빠른 방법입니다.   
 
 예를 들어 CTAS에는를 사용 합니다.  
  
-   다른 해시 배포 열이 있는 테이블을 다시 만듭니다.
-   복제 테이블을 다시 만듭니다.   
-   Columnstore 인덱스는 테이블의 열 중 일부만를 만듭니다.  
-   쿼리 또는 외부 데이터 가져오기 있습니다.  

> [!NOTE]  
> CTAS에 추가 하는 테이블을 만드는 기능 때문에이 항목에 대해 CREATE TABLE 항목 시도 합니다. 대신, CTAS에는 및 CREATE TABLE 문 간의 차이점을 설명 합니다. CREATE TABLE 세부 정보를 참조 하십시오. [CREATE TABLE (Azure SQL 데이터 웨어하우스)](https://msdn.microsoft.com/library/mt203953/) 문. 
  
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
자세한 내용은 참조는 [인수 섹션](https://msdn.microsoft.com/library/mt203953/#Arguments) CREATE TABLE에 있습니다.  

<a name="column-options-bk"></a>

### <a name="column-options"></a>열 옵션
`column_name` [ ,...`n` ]   
 열 이름을 허용 하지 않습니다는 [열 옵션](https://msdn.microsoft.com/library/mt203953/#ColumnOptions) CREATE TABLE에서 설명 합니다.  대신, 새 테이블에 대 한 하나 이상의 열 이름의 선택 사항 목록을 제공할 수 있습니다. 새 테이블의 열은 지정한 이름을 사용 합니다. 열 이름을 지정할 때 열 목록에 있는 열의 수는 select 결과의 열 수가 일치 해야 합니다. 열 이름은 지정 하지 않으면, 새 대상 테이블 select 문 결과에서 열 이름을 사용 합니다. 
  
 데이터 형식, 데이터 정렬 또는 null 허용 여부 등의 다른 모든 열 옵션을 지정할 수 없습니다. 이러한 각 특성의 결과에서 파생 되는 `SELECT` 문. 그러나 특성을 변경 하려면 SELECT 문에 사용할 수 있습니다. 예를 들어 참조 [열 특성을 변경 하려면 CTAS에는 사용 하 여](#ctas-change-column-attributes-bk)합니다.   

<a name="table-distribution-options-bk"></a>

### <a name="table-distribution-options"></a>테이블의 배포 옵션

`DISTRIBUTION` = `HASH`( *distribution_column_name* ) | ROUND_ROBIN | 복제      
CTAS 문은 배포 옵션을 사용 해야 하며는 기본값이 없습니다. 이 CREATE TABLE에 기본값이 있는와 다릅니다. 

자세한 내용을 보고 최상의 배포 열을 선택 하는 방법을 이해 하 참조는 [표 배포 옵션](https://msdn.microsoft.com/library/mt203953/#TableDistributionOptions) CREATE TABLE의 섹션입니다. 

<a name="table-partition-options-bk"></a>

### <a name="table-partition-options"></a>테이블 파티션 옵션
CTAS 문은 원본 테이블이 분할 된 경우에 기본적으로 분할 되지 않은 테이블을 만듭니다. CTAS에는 문을 사용 하 여 분할된 된 테이블을 만들려면 파티션 옵션을 지정 해야 합니다. 

자세한 내용은 참조는 [테이블 파티션 옵션](https://msdn.microsoft.com/library/mt203953/#TablePartitionOptions) CREATE TABLE의 섹션입니다.

<a name="select-options-bk"></a>

### <a name="select-options"></a>옵션을 선택 합니다.
Select 문에 근본적인 차이점 CTAS과 CREATE TABLE입니다.  

 `WITH`*common_table_expression*  
 CTE(공통 테이블 식)라고도 하는 임시로 이름이 지정된 결과 집합을 지정합니다. 자세한 내용은 참조 [common_table_expression &AMP; #40; Transact SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 `SELECT`*select_criteria*  
 SELECT 문에서 결과 함께 새 테이블을 채웁니다. *select_criteria* 데이터를 새 테이블로 복사를 결정 하는 SELECT 문의 본문입니다. SELECT 문에 대 한 정보를 참조 하십시오. [select&#40; Transact SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
<a name="permissions-bk"></a>  
  
## <a name="permissions"></a>Permissions  
CTAS에는 필요 `SELECT` 권한에서 참조 되는 개체에 대해서는 *select_criteria*합니다.

참조 테이블을 만들 수 있는 권한이 [권한을](https://msdn.microsoft.com/library/mt203953/#Permissions) CREATE TABLE에 있습니다. 
  
<a name="general-remarks-bk"></a>
  
## <a name="general-remarks"></a>일반적인 주의 사항
자세한 내용은 참조 [일반적인 주의 사항](https://msdn.microsoft.com/library/mt203953/#GeneralRemarks) CREATE TABLE에 있습니다.

<a name="limitations-bk"></a>

## <a name="limitations-and-restrictions"></a>제한 사항  
Azure SQL 데이터 웨어하우스 지원 자동 만들기 또는 자동으로 통계를 업데이트 하지 않습니다.  쿼리에서 최상의 성능을 얻으려면 CTAS에 실행 한 후 전후에 상당한 변경 된 내용이 데이터의 모든 테이블의 모든 열에서 통계를 작성 해야 합니다. 자세한 내용은 [CREATE STATISTICS(Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.

[SET ROWCOUNT &#40; Transact SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) CTAS에는 아무 효과가 없습니다. 비슷한 동작이 얻기 위해 사용 하 여 [top&#40; Transact SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
 
자세한 내용은 참조 [제한 사항](https://msdn.microsoft.com/library/mt203953/#LimitationsRestrictions) CREATE TABLE에 있습니다.

<a name="locking-behavior-bk"></a>
  
## <a name="locking-behavior"></a>잠금 동작  
 자세한 내용은 참조 [잠금 동작](https://msdn.microsoft.com/library/mt203953/#LockingBehavior) CREATE TABLE에 있습니다.
 
<a name="performance-bk"></a>
 
 ## <a name="performance"></a>성능 

해시 distributed 테이블에 대 한 조인 및 집계에 대 한 성능을 향상 시키려면 다른 배포 열을 선택할 CTAS에는 사용할 수 있습니다. 다른 배포 열이 목표를 선택 하는 경우을 피해 야 행을 다시 배포 하므로 동일한 배포 열을 지정 하는 경우 최상의 CTAS에는 성능을 갖습니다. 

경우 CTAS에는 사용 하는 테이블을 만들 및 성능 영향을 주지 않습니다를 지정할 수 있습니다 `ROUND_ROBIN` 는 배포 열 결정 필요가 없도록 합니다.

이후의 쿼리에서에서 데이터 이동을 방지 하려면 지정할 수 있습니다 `REPLICATE` 증가 된 저장소에 각 계산 노드가 있는 테이블의 전체 복사본을 로드 하기 위한 비용입니다.  


<a name="examples-copy-table-bk"></a>

## <a name="examples-for-copying-a-table"></a>테이블을 복사 하면에 대 한 예제

<a name="ctas-copy-table-bk"></a>

### <a name="a-use-ctas-to-copy-a-table"></a>1. CTAS에는 사용 하 여 테이블을 복사 하려면 
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스

아마도 가장 일반적인 용도의 `CTAS` DDL을 변경할 수 있도록 테이블의 복사본을 만드는 것입니다. 예를 들어으로 테이블에 원래 만든 경우 `ROUND_ROBIN` 이제 원하는 열에 분산을 테이블로 변경 하 고 `CTAS` 은 어떻게 배포 열을 변경할 수 있습니다. `CTAS`분할 인덱싱 또는 열 유형을 변경 하려면 사용할 수도 있습니다.

기본 배포 유형을 사용 하 여이 테이블을 만든 경우를 가정해 `ROUND_ROBIN` 배포 열에 지정 된 이후 배포는 `CREATE TABLE`합니다.

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

지금 만들려는이 테이블의 새 복사본을 클러스터형된 columnstore 인덱스가 있는 클러스터형된 columnstore 테이블의 성능을 활용할 수 있도록 합니다. 또한이 열에서 조인을 지정 해야 하므로 ProductKey에이 테이블을 배포 하려면 하 고 ProductKey에 조인 하는 동안 데이터 이동을 방지 하려고 합니다. 마지막으로 추가 하려면 기존 파티션을 삭제 하 여 오래 된 데이터를 신속 하 게 삭제할 수 있도록 OrderDateKey에서 분할 합니다. 다음은 이전 테이블에 새 테이블로 복사는 CTAS에는 문이입니다.

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

마지막으로 새 테이블을 전환 하 고 다음 이전 테이블을 삭제 하기 위해 테이블 이름을 바꿀 수 있습니다.

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

<a name="examples-column-bk"></a>

## <a name="examples-for-column-options"></a>열 옵션에 대 한 예제

<a name="ctas-change-column-attributes-bk"></a>

### <a name="b-use-ctas-to-change-column-attributes"></a>2. CTAS에는 사용 하 여 열 특성을 변경 하려면 
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스

이 예제에서는 CTAS에는 사용 하 여 데이터 형식, null 허용 여부 및 DimCustomer2 테이블의 여러 열에 대 한 데이터 정렬을 변경 합니다.  
  
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
 
마지막 단계로 사용할 수 있습니다 [이름 바꾸기 &#40; Transact SQL &#41; ](../../t-sql/statements/rename-transact-sql.md) 테이블 이름을 전환할 수 있습니다. 따라서 DimCustomer2 새 테이블을 수 있습니다.

```
RENAME OBJECT DimCustomer2 TO DimCustomer2_old;
RENAME OBJECT test TO DimCustomer2;

DROP TABLE DimCustomer2_old;
```

<a name="examples-table-distribution-bk"></a>

## <a name="examples-for-table-distribution"></a>테이블 배포에 대 한 예제

<a name="ctas-change-distribution-method-bk"></a>

### <a name="c-use-ctas-to-change-the-distribution-method-for-a-table"></a>3. CTAS에는 사용 하 여 변경 테이블에 대 한 배포 방법
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스

이 간단한 예제는 테이블에 대 한 배포 방법을 변경 하는 방법을 보여 줍니다. 이 작업을 수행 하는 방법의 메커니즘을 표시 하려면이 클래스는 라운드 로빈 방식으로 해시 distributed 테이블 변경을 수정한 다음 distributed 해시에 다시 라운드 로빈 테이블입니다. 최종 테이블 원래 테이블을 찾습니다. 

대부분의 경우에서 라운드 로빈 테이블에는 해시 distributed 테이블을 변경할 필요가 없습니다. 더 자주 분산된 해시 테이블에 라운드 로빈 테이블을 변경 해야 할 수 있습니다. 예를 들어 처음 라운드 로빈 방식으로 새 테이블을 로드 한 다음 나중에 조인 성능을 향상 하기 위해 해시 distributed 테이블에 이동할 수 있습니다.

이 예제에서는 AdventureWorksDW 예제 데이터베이스를 사용 합니다. SQL 데이터 웨어하우스 버전을 로드 하려면 참조 [SQL 데이터 웨어하우스로 샘플 데이터를 로드 합니다.](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-sample-databases/)
 
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
다음으로, 해시 분산된 테이블으로 다시 변경 합니다.

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

### <a name="d-use-ctas-to-convert-a-table-to-a-replicated-table"></a>4. CTAS에는 사용 하 여 복제 된 테이블에 테이블을 변환 하려면  
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 

이 예에서는 복제 된 테이블에 라운드 로빈 또는 해시 distributed 테이블 변환에 적용 됩니다. 이 특정 예제에서는 이전 메서드는 배포 유형 한 단계 더 발전을 변경 합니다.  차원 및 가능성이 더 작은 테이블로 DimSalesTerritory 이므로 다른 테이블에 조인 하는 경우 데이터 이동을 방지 하도록 복제 테이블을 다시 만들 수도 있습니다. 

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
 
### <a name="e-use-ctas-to-create-a-table-with-fewer-columns"></a>5. 사용 하 여 테이블을 만들려면 적은 열이 있는 CTAS에는
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 

다음 예에서는 라는 라운드 로빈 분산된 테이블을 만들어 `myTable (c, ln)`합니다. 새 테이블에는 두 개의 열에만 합니다. SELECT 문에서 열 별칭은 열 이름에 대 한 사용합니다.  
  
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

## <a name="examples-for-query-hints"></a>쿼리 힌트에 대 한 예제

<a name="ctas-query-hint-bk"></a>

### <a name="f-use-a-query-hint-with-create-table-as-select-ctas"></a>6. CREATE TABLE AS와 쿼리 힌트를 사용 하 여 선택 (CTAS에)  
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스
  
이 쿼리에서 CTAS에는 문을 사용 하 여 쿼리 조인 힌트를 사용 하기 위한 기본 구문을 보여 줍니다. 쿼리를 전송할 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 각 개별 배포에 대 한 쿼리 계획을 생성할 때 해시 조인 전략을 적용 합니다. 해시 조인 쿼리 힌트에 대 한 자세한 내용은 참조 하십시오. [OPTION 절 &#40; Transact SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
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

## <a name="examples-for-external-tables"></a>외부 테이블에 대 한 예제

<a name="ctas-azure-blob-storage-bk"></a>

### <a name="g-use-ctas-to-import-data-from-azure-blob-storage"></a>7. CTAS에는 사용 하 여 Azure Blob 저장소에서 데이터를 가져오려면  
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스  

외부 테이블에서 데이터를 가져오려면을 사용 하 여 CREATE TABLE AS SELECT는 외부 테이블에서 선택 합니다. 에 외부 테이블에서 데이터를 선택 하는 구문은 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 일반 테이블에서 데이터를 선택 하는 구문은와 같습니다.  
  
 다음 예제에서는 Azure blob 저장소 계정에서 데이터에 외부 테이블을 정의합니다. 다음 사용 하 여 CREATE TABLE AS SELECT는 외부 테이블에서 선택 합니다. Azure blob 저장소 텍스트 구분 파일에서 데이터를 가져옵니다.이 새 데이터를 저장 합니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 테이블입니다.  
  
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
  
### <a name="h-use-ctas-to-import-hadoop-data-from-an-external-table"></a>8. CTAS에는 사용 하 여 외부 테이블에서 Hadoop 데이터를 가져오려면  
적용 대상:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
외부 테이블에서 데이터를 가져오려면을 사용 하 여 CREATE TABLE AS SELECT는 외부 테이블에서 선택 합니다. 에 외부 테이블에서 데이터를 선택 하는 구문은 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 일반 테이블에서 데이터를 선택 하는 구문은와 같습니다.  
  
 다음 예제에서는 Hadoop 클러스터에서 외부 테이블을 정의합니다. 다음 사용 하 여 CREATE TABLE AS SELECT는 외부 테이블에서 선택 합니다. 이 새 데이터를 저장 합니다 Hadoop 텍스트 구분 파일에서 데이터를 가져오는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 테이블입니다.  
  
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
 
## <a name="examples-using-ctas-to-replace-sql-server-code"></a>SQL Server 코드를 바꾸려면 CTAS에는 사용 하는 예제

CTAS에는 지원 되지 않는 일부 기능을 해결 하려면 사용 합니다. 데이터 웨어하우스에 대 한 코드를 실행할 수 있을 뿐 CTAS에는 사용 하도록 기존 코드를 다시 작성 해도 일반적으로 성능이 향상. 이것은 완벽 하 게 병렬화 된 디자인입니다. 

> [!NOTE]
> 고려 하십시오 "CTAS에는 첫 번째"입니다. 사용 하 여 문제를 해결할 수 있다고 생각 되 면 `CTAS` 다음 하는 일반적으로-접근 하는 가장 좋은 방법은 결과적으로 더 많은 데이터를 작성 하는 경우에 합니다.
>

<a name="ctas-replace-select-into-bk"></a>

### <a name="i-use-ctas-instead-of-selectinto"></a>9. CTAS에는 사용 하 여 선택 하는 대신... 에  
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스

일반적으로 SQL Server 코드를 사용합니다. INTO를 사용 하는 SELECT 문의 결과 테이블을 채웁니다. 이 SQL Server 선택의 예는... 문으로 합니다.

```sql
SELECT *
INTO    #tmp_fct
FROM    [dbo].[FactInternetSales]
```

이 구문은 SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 지원 되지 않습니다. 이 예제에서는 이전 SELECT를 다시 작성 하는 방법을 보여 줍니다. 문으로 CTAS에는 서술입니다. CTAS에는 구문에 설명 된 배포 옵션 중 하나를 선택할 수 있습니다. 이 예제에서는 ROUND_ROBIN 배포 방법을 사용 합니다.

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

### <a name="j-use-ctas-and-implicit-joins-to-replace-ansi-joins-in-the-from-clause-of-an-update-statement"></a>10. ANSI 조인에 대체를 CTAS 및 암시적 조인을 사용 하 여는 `FROM` 절은 `UPDATE` 문  
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스  

UPDATE 또는 DELETE를 수행 하려면 ANSI 조인 구문을 사용 하 여 함께 두 개 이상의 테이블을 조인 하는 복잡 한 업데이트가 있는 알 수 있습니다.

이 테이블을 업데이트 해야 했습니다 같이 가정해 봅니다.

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

원래 쿼리 다음과 같이 보지 못했을 수 있습니다.

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

ANSI 조인 SQL 데이터 웨어하우스를 지원 하지 않으므로 `FROM` 절은 `UPDATE` 문, 약간 변경 하지 않고이 SQL Server 코드를 통해 사용할 수 없습니다.

조합을 사용할 수 있습니다는 `CTAS` 및 암시적 조인을이 코드를 바꾸려면:

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

### <a name="k-use-ctas-to-specify-which-data-to-keep-instead-of-using-ansi-joins-in-the-from-clause-of-a-delete-statement"></a>11. CTAS에는 사용 하 여 DELETE 문의 FROM 절에 조인 ANSI를 사용 하는 대신 유지 하는 데이터를 지정 하려면  
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스  

데이터를 삭제 하는 최선의 방법을 사용 하는 경우에 따라 `CTAS`합니다. 단순히 데이터를 삭제 하는 대신 보관 하려는 데이터를 선택 합니다. 이 경우에 특히 유용 `DELETE` ansi 조인 구문을 SQL 데이터 웨어하우스 ANSI를 지원 하지 않으므로 조인에 사용 하는 문에 `FROM` 절은 `DELETE` 문.

변환 된 DELETE 문의 예는 아래 제공 됩니다.

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

### <a name="l-use-ctas-to-simplify-merge-statements"></a>12. CTAS에는 사용 하 여 merge 문의 단순화  
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스  

Merge 문에에서 대체할 수 있습니다, 적어도 파트를 사용 하 여 `CTAS`합니다. 통합을 수행할 수는 `INSERT` 및 `UPDATE` 단일 문으로 합니다. 삭제 된 데이터를 두 번째 문에 오프 닫을 수 있게 해야 합니다.

예로 `UPSERT` 는 아래에 나와 있습니다.

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
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

<a name="ctas-data-type-and-nullability-bk"></a>

### <a name="m-explicitly-state-data-type-and-nullability-of-output"></a>13. 데이터 형식 및 출력의 null 허용 여부가 명시적으로 지정  
적용 대상: Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스  

SQL 데이터 웨어하우스를 SQL Server 코드를 마이그레이션하는 경우이 유형의 코딩 방식 여러 실행을 알 수 있습니다.

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

Instinctively이 코드는 CTAS에 마이그레이션해야 하 고 올바른는 생각할 수 있습니다. 그러나 여기서는 숨겨진된 문제가 있습니다.

다음 코드는 동일한 결과 생성 하지 않습니다.

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

"Result" 열은 식의 데이터 형식 및 null 허용 여부 값 있는지 확인 합니다. 주의 하지 않은 경우 값에 미묘한 차이가 발생할 수 있습니다.

예를 들어 다음을 시도해 보십시오.

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

결과 대해 저장 된 값은 다릅니다. 결과 열에 보관 된 값이 다른 식에 사용 되는 오류 훨씬 더 중요 한 됩니다.

![CREATE TABLE AS SELECT 결과](../../t-sql/statements/media/create-table-as-select-results.png)

데이터 마이그레이션에 특히 유용합니다. 두 번째 쿼리는 풀링할 때 보다 정확 하 게 하는 경우에 문제가 있습니다. 데이터는 다른 원본 시스템에 비해와 마이그레이션에 대 한 무결성의 질문에 연결 하는 합니다. 드문 경우 지만 "잘못 된" 답이 적합 한 실제로 중 하나입니다.

암시적 형식 캐스팅 아래로 두 결과 간의이 차이 보면 이유가입니다. 첫 번째 예에서는 테이블 열 정의 정의합니다. 행이 삽입 될 때 암시적 형식 변환이 발생 합니다. 두 번째 예에서는 즉 암시적 형식 변환 작업 없이 식 열의 데이터 형식을 정의 하는 대로 있습니다. 반면 하지 않았으면 첫 번째 예에서는 null 허용 열으로 두 번째 예제에서 열에 정의 된를 확인할 수 있습니다. 첫 번째 예에서는 열의 null 허용에 테이블을 만들 때 명시적으로 정의 되었습니다. 두 번째 것만 두었습니다 식 및 기본적으로이 예제에서는 NULL 정의에 반환 됩니다.  

이러한 문제를 해결 하려면 명시적으로 설정 해야 형식 변환 및에서 null 허용 여부는 `SELECT` 부분의 `CTAS` 문. Create 테이블 부분에서 이러한 속성을 설정할 수 없습니다.

다음 예제에서는 코드를 수정 하는 방법을 보여 줍니다.

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

다음에 유의하세요.
- CAST 또는 CONVERT 사용 되었을 수 있습니다.
- COALESCE 하지 null 허용 여부를 ISNULL 사용
- ISNULL은 가장 바깥쪽 함수
- ISNULL의 두 번째 부분은 상수, 즉 0

> [!NOTE]
> Null 허용 여부에 따라 올바르게 설정 수에 대 한이 사용 하도록 중요 `ISNULL` 아닌 `COALESCE`합니다. `COALESCE`결정적 함수 아니며 따라서 식의 결과 항상 것이 null을 허용 합니다. `ISNULL`다릅니다. 그는 결정적입니다. 따라서 때의 두 번째 부분에서 `ISNULL` 상수 또는 리터럴 함수는 다음 결과 값이 됩니다 NOT NULL입니다.

이 팁 방금 유용 계산의 무결성을 보장 하지 않습니다. 테이블 파티션 전환을 위한 중요 한 이기도합니다. 정의 팩트로이 테이블이 있다고 가정해 봅니다.

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

그러나 값 필드에는 원본 데이터에 속하지 않습니다 계산 된 식입니다.

이 작업을 수행 하려면 분할 된 데이터 집합을 만들려면:

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

쿼리는 완벽 하 게 제대로 실행 됩니다. 이 문제는 파티션 전환을 수행 하려고 할 때 제공 됩니다. 테이블 정의와 일치 하지 않습니다. 일치는 CTAS에는 테이블 정의를 수정 해야 합니다.

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

형식 일관성 및 CTAS에는 null 허용 여부 속성을 유지 관리이 좋은 엔지니어링 좋습니다 따라서 볼 수 있습니다. 계산의 무결성을 유지 하는 데 도움이 하 고 갖는지도 확인 된 파티션 전환을 합니다.
 
## <a name="see-also"></a>관련 항목:  
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [외부 TABLE AS SELECT &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [테이블 &#40; 만들기 Azure SQL 데이터 웨어하우스 &#41; ](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) [DROP table&#40; Transact SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [외부 테이블 삭제 &#40; Transact SQL &#41;](../../t-sql/statements/drop-external-table-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [외부 테이블 &#40; 변경 Transact SQL &#41;](http://msdn.microsoft.com/library/4ae1b23c-67f6-41d0-b614-7a8de914d145)  
  
  



