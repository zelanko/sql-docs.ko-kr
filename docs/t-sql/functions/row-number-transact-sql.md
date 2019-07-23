---
title: ROW_NUMBER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e73d13927ff4618f0c0ea0b7246df0d722340a1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095377"
---
# <a name="rownumber-transact-sql"></a>ROW_NUMBER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

결과 집합의 출력 번호를 지정합니다. 보다 구체적으로는, 결과 집합 파티션 내의 행 일련 번호를 반환합니다. 각 파티션의 첫 번째 행은 1로 시작합니다. 
  
`ROW_NUMBER`와 `RANK`는 유사합니다. `ROW_NUMBER`는 모든 행의 번호를 순차적으로 지정합니다(예: 1, 2, 3, 4, 5). `RANK`는 순위 동률(예: 1, 2, 2, 4, 5)에 대해 동일한 숫자 값을 제공합니다.   
  
> [!NOTE]
> `ROW_NUMBER`는 쿼리를 실행할 때 계산되는 임시 값입니다. 테이블의 숫자를 유지하려면 [IDENTITY 속성](../../t-sql/statements/create-table-transact-sql-identity-property.md) 및 [SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md)를 참조하세요. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
  
## <a name="syntax"></a>구문  
  
```  
ROW_NUMBER ( )   
    OVER ( [ PARTITION BY value_expression , ... [ n ] ] order_by_clause )  
```  
  
## <a name="arguments"></a>인수  
 PARTITION BY *value_expression*  
 [FROM](../../t-sql/queries/from-transact-sql.md) 절이 생성한 결과 집합을 ROW_NUMBER 함수가 적용되는 파티션으로 나눕니다. *value_expression*은 결과 집합을 분할하는 데 사용하는 열을 지정합니다. `PARTITION BY`를 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.  
  
 *order_by_clause*  
 `ORDER BY` 절은 지정된 파티션 내에서 행에 고유 `ROW_NUMBER`가 할당되는 순서를 결정합니다. 필수 항목입니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.  
  
## <a name="return-types"></a>반환 형식  
 **bigint**  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 다음 조건이 충족되지 않으면 `ROW_NUMBER()`를 사용하여 쿼리에서 반환하는 행이 각 실행마다 정확히 동일하게 정렬된다는 보장이 없습니다.  
  
1.  분할된 열 값이 고유합니다.  
  
2.  `ORDER BY` 열 값이 고유합니다.  
  
3.  파티션 열 및 `ORDER BY` 열 값의 조합이 고유합니다.  
  
 `ROW_NUMBER()`는 비결정적입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-examples"></a>1\. 간단한 예제 

다음 쿼리는 알파벳 순서로 4개의 시스템 테이블을 반환합니다.

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

각 행 앞에 행 번호 열을 추가하려면 `ROW_NUMBER` 함수(이 경우 `Row#`)가 포함된 열을 추가합니다. `ORDER BY` 절을 `OVER` 절까지 이동해야 합니다.

```sql
SELECT 
  ROW_NUMBER() OVER(ORDER BY name ASC) AS Row#,
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|Row# |NAME    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |master |SIMPLE |
|2 |model |FULL |
|3 |msdb |SIMPLE |
|4 |tempdb |SIMPLE |

`recovery_model_desc` 열에 `PARTITION BY` 절을 추가하면 `recovery_model_desc` 값이 변경될 때 번호 매기기가 다시 시작됩니다. 
 
```sql
SELECT 
  ROW_NUMBER() OVER(PARTITION BY recovery_model_desc ORDER BY name ASC) 
    AS Row#,
  name, recovery_model_desc
FROM sys.databases WHERE database_id < 5;
```  

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|Row# |NAME    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |model |FULL |
|1 |master |SIMPLE |
|2 |msdb |SIMPLE |
|3 |tempdb |SIMPLE |


### <a name="b-returning-the-row-number-for-salespeople"></a>2\. 영업 사원의 행 번호 반환  
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
  
### <a name="c-returning-a-subset-of-rows"></a>C. 행의 하위 집합 반환  
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
  
### <a name="d-using-rownumber-with-partition"></a>D. PARTITION에 ROW_NUMBER() 사용  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-returning-the-row-number-for-salespeople"></a>E. 영업 사원의 행 번호 반환  
 다음 예는 담당자의 판매 할당량을 기반으로 영업 담당자의 `ROW_NUMBER`를 반환합니다.  
  
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

### <a name="f-using-rownumber-with-partition"></a>F. PARTITION에 ROW_NUMBER() 사용  
 다음 예에서는 `ROW_NUMBER` 인수에 `PARTITION BY` 함수를 사용하는 방법을 보여 줍니다. 이로 인해 `ROW_NUMBER` 함수가 각 파티션의 행에 번호를 매기게 됩니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [RANK&#40;Transact-SQL&#41;](../../t-sql/functions/rank-transact-sql.md)   
 [DENSE_RANK&#40;Transact-SQL&#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [NTILE&#40;Transact-SQL&#41;](../../t-sql/functions/ntile-transact-sql.md)  
  
  


