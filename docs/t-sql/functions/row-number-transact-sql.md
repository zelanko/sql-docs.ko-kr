---
title: ROW_NUMBER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROW_NUMBER
- ROW_NUMBER_TSQL
- ROW_NUMBER()_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ROW_NUMBER function
- row numbers [SQL Server]
- sequential row numbers [SQL Server]
ms.assetid: 82fa9016-77db-4b42-b4c8-df6095b81906
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 6ddb3472f19ce2fda8bc368cd07f7ea602d74a02
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="rownumber-transact-sql"></a>ROW_NUMBER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  숫자 결과의 출력을 설정합니다. 보다 구체적으로, 각 파티션의 첫 번째 행에 대 한 1부터 시작 하는 결과 집합의 파티션 내의 행 일련 번호를 반환 합니다. 
  
`ROW_NUMBER`및 `RANK` 비슷합니다. `ROW_NUMBER`숫자의 모든 행을 순서 대로 (예: 1, 2, 3, 4, 5). `RANK`동률 (예: 1, 2, 2, 4, 5)에 대 한 숫자 값을 제공합니다.   
  
> [!NOTE]
> `ROW_NUMBER`쿼리를 실행할 때 임시 값 계산 됩니다. 참조 테이블의 숫자를 유지 하기 위해 [IDENTITY 속성](../../t-sql/statements/create-table-transact-sql-identity-property.md) 및 [시퀀스](../../t-sql/statements/create-sequence-transact-sql.md)합니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
  
## <a name="syntax"></a>구문  
  
```  
ROW_NUMBER ( )   
    OVER ( [ PARTITION BY value_expression , ... [ n ] ] order_by_clause )  
```  
  
## <a name="arguments"></a>인수  
 PARTITION BY *value_expression*  
 생성 한 결과 집합을 나눕니다는 [FROM](../../t-sql/queries/from-transact-sql.md) 절에 ROW_NUMBER 함수가 적용 되는 파티션으로 합니다. *value_expression* 결과 집합을 분할 하는 열을 지정 합니다. 경우 `PARTITION BY` 을 지정 하지 않으면 함수는 쿼리 결과 집합을 단일 그룹의 모든 행을 처리 합니다. 자세한 내용은 참조 [OVER 절 &#40; Transact SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 *order_by_clause*  
 `ORDER BY` 절 결정 행 할당 된 고유한 시퀀스 `ROW_NUMBER` 지정 된 파티션 내에서. 필수 항목입니다. 자세한 내용은 참조 [OVER 절 &#40; Transact SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>반환 형식  
 **bigint**  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 보장이 없습니다 행을 반환 하는 쿼리를 사용 하 여 `ROW_NUMBER()` 를 정렬할 똑같이 실행 될 때마다 다음 조건이 true가 아니면 합니다.  
  
1.  분할된 열 값이 고유합니다.  
  
2.  값은 `ORDER BY` 열은 고유 합니다.  
  
3.  파티션 열 값의 조합이 및 `ORDER BY` 열은 고유 합니다.  
  
 `ROW_NUMBER()`비결 정적입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-examples"></a>1. 간단한 예 

다음 쿼리에서 알파벳 순서로 4 개의 시스템 테이블을 반환합니다.

```sql
SELECT 
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5
ORDER BY name ASC;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|NAME    |recovery_model_desc |  
|-----------  |------------ |  
|master |SIMPLE |
|model |FULL |
|msdb |SIMPLE |
|tempdb |SIMPLE |

각 행 앞에 행 번호 열을 추가 하려면 지정 된 열을 추가 `ROW_NUMBER` 함수,이 경우 이름은 `Row#`합니다. `ORDER BY`절을`OVER` 절로 이동해야합니다.

```sql
SELECT 
  ROW_NUMBER() OVER(ORDER BY name ASC) AS Row#,
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|행 번호 |NAME    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |master |SIMPLE |
|2 |model |FULL |
|3 |msdb |SIMPLE |
|4 |tempdb |SIMPLE |

추가 `PARTITION BY` 절에는 `recovery_model_desc` 열 번호 매기기 때 다시 시작 됩니다는 `recovery_model_desc` 값이 변경 합니다. 
 
```sql
SELECT 
  ROW_NUMBER() OVER(PARTITION BY recovery_model_desc ORDER BY name ASC) 
    AS Row#,
  name, recovery_model_desc
FROM sys.databases WHERE database_id < 5;
```  

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|행 번호 |NAME    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |model |FULL |
|1 |master |SIMPLE |
|2 |msdb |SIMPLE |
|3 |tempdb |SIMPLE |


### <a name="b-returning-the-row-number-for-salespeople"></a>2. 영업 사원의 행 번호 반환  
 다음 예에서는 연간 누계 판매 실적에 따라 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]의 영업 사원에 대한 행 번호를 계산합니다.  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT ROW_NUMBER() OVER(ORDER BY SalesYTD DESC) AS Row,   
    FirstName, LastName, ROUND(SalesYTD,2,1) AS "Sales YTD"   
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Row FirstName    LastName               SalesYTD  
--- -----------  ---------------------- -----------------  
1   Linda        Mitchell               4251368.54  
2   Jae          Pak                    4116871.22  
3   Michael      Blythe                 3763178.17  
4   Jillian      Carson                 3189418.36  
5   Ranjit       Varkey Chudukatil      3121616.32  
6   José         Saraiva                2604540.71  
7   Shu          Ito                    2458535.61  
8   Tsvi         Reiter                 2315185.61  
9   Rachel       Valdez                 1827066.71  
10  Tete         Mensa-Annan            1576562.19  
11  David        Campbell               1573012.93  
12  Garrett      Vargas                 1453719.46  
13  Lynn         Tsoflias               1421810.92  
14  Pamela       Ansman-Wolfe           1352577.13  
```  
  
### <a name="c-returning-a-subset-of-rows"></a>3. 행의 하위 집합 반환  
 다음 예에서는 `SalesOrderHeader` 테이블에서 `OrderDate`를 기준으로 모든 행의 행 번호를 계산한 후 `50`에서 `60`까지의 행만 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
WITH OrderedOrders AS  
(  
    SELECT SalesOrderID, OrderDate,  
    ROW_NUMBER() OVER (ORDER BY OrderDate) AS RowNumber  
    FROM Sales.SalesOrderHeader   
)   
SELECT SalesOrderID, OrderDate, RowNumber    
FROM OrderedOrders   
WHERE RowNumber BETWEEN 50 AND 60;  
```  
  
### <a name="d-using-rownumber-with-partition"></a>4. PARTITION에 ROW_NUMBER() 사용  
 다음 예에서는 `PARTITION BY` 인수를 사용하여 `TerritoryName` 열을 기준으로 쿼리 결과 집합을 분할합니다. `ORDER BY` 절에 지정된 `OVER` 절은 각 파티션의 행을 `SalesYTD` 열을 기준으로 정렬합니다. `ORDER BY` 문의 `SELECT` 절은 전체 쿼리 결과 집합을 `TerritoryName`을 기준으로 정렬합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FirstName, LastName, TerritoryName, ROUND(SalesYTD,2,1) AS SalesYTD,  
ROW_NUMBER() OVER(PARTITION BY TerritoryName ORDER BY SalesYTD DESC) 
  AS Row  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0  
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
FirstName  LastName             TerritoryName        SalesYTD      Row  
---------  -------------------- ------------------   ------------  ---  
Lynn       Tsoflias             Australia            1421810.92    1  
José       Saraiva              Canada               2604540.71    1  
Garrett    Vargas               Canada               1453719.46    2  
Jillian    Carson               Central              3189418.36    1  
Ranjit     Varkey Chudukatil    France               3121616.32    1  
Rachel     Valdez               Germany              1827066.71    1  
Michael    Blythe               Northeast            3763178.17    1  
Tete       Mensa-Annan          Northwest            1576562.19    1  
David      Campbell             Northwest            1573012.93    2  
Pamela     Ansman-Wolfe         Northwest            1352577.13    3  
Tsvi       Reiter               Southeast            2315185.61    1  
Linda      Mitchell             Southwest            4251368.54    1  
Shu        Ito                  Southwest            2458535.61    2  
Jae        Pak                  United Kingdom       4116871.22    1  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-returning-the-row-number-for-salespeople"></a>5. 영업 사원의 행 번호 반환  
 다음 예제에서는 반환 된 `ROW_NUMBER` 영업 담당자의 판매 할당량에 따라에 대 한 합니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(ORDER BY SUM(SalesAmountQuota) DESC) 
    AS RowNumber,  
    FirstName, LastName,   
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName;  
```  
  
 다음은 결과 집합의 일부입니다.  

```  

RowNumber  FirstName  LastName            SalesQuota  
---------  ---------  ------------------  -------------  
1          Jillian    Carson              12,198,000.00  
2          Linda      Mitchell            11,786,000.00  
3          Michael    Blythe              11,162,000.00  
4          Jae        Pak                 10,514,000.00  
```

### <a name="f-using-rownumber-with-partition"></a>6. PARTITION에 ROW_NUMBER() 사용  
 다음 예에서는 `ROW_NUMBER` 인수에 `PARTITION BY` 함수를 사용하는 방법을 보여 줍니다. 이 인해는 `ROW_NUMBER` 함수 각 파티션에 있는 행 번호입니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(PARTITION BY SalesTerritoryKey 
        ORDER BY SUM(SalesAmountQuota) DESC) AS RowNumber,  
    LastName, SalesTerritoryKey AS Territory,  
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName, SalesTerritoryKey;  
```  
  
 다음은 결과 집합의 일부입니다.  
 
```  
 
RowNumber  LastName            Territory  SalesQuota  
---------  ------------------  ---------  -------------  
1          Campbell            1           4,025,000.00  
2          Ansman-Wolfe        1           3,551,000.00  
3          Mensa-Annan         1           2,275,000.00  
1          Blythe              2          11,162,000.00  
1          Carson              3          12,198,000.00  
1          Mitchell            4          11,786,000.00  
2          Ito                 4           7,804,000.00  
```
  
## <a name="see-also"></a>관련 항목:  
 [순위 &#40; Transact SQL &#41;](../../t-sql/functions/rank-transact-sql.md)   
 [DENSE_RANK &#40; Transact SQL &#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [NTILE &#40; Transact SQL &#41;](../../t-sql/functions/ntile-transact-sql.md)  
  
  


