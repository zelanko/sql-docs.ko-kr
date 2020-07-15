---
title: NTILE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NTILE_TSQL
- NTILE
dev_langs:
- TSQL
helpviewer_keywords:
- distributing rows
- groups [SQL Server], row distribution
- row distribution [SQL Server]
- NTILE function
ms.assetid: 1c364511-d72a-4789-8efa-3cf2a1f6b791
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 66841ba6ac7e278cc2353a126675cbb2cc57c48f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86010853"
---
# <a name="ntile-transact-sql"></a>NTILE(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  정렬된 파티션의 행을 지정된 수의 그룹으로 분산시킵니다. 그룹에는 1부터 시작하는 번호가 매겨집니다. NTILE은 각 행에서 해당 행이 속한 그룹 번호를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
NTILE (integer_expression) OVER ( [ <partition_by_clause> ] < order_by_clause > )  
```  
  
## <a name="arguments"></a>인수  
 *integer_expression*  
 각 파티션을 분할해야 하는 그룹 수를 지정하는 양의 정수 식입니다. *integer_expression*은 **int** 또는 **bigint** 형식일 수 있습니다.  
  
 \<partition_by_clause>  
 [FROM](../../t-sql/queries/from-transact-sql.md) 절이 생성한 결과 집합을 함수가 적용되는 파티션으로 나눕니다. PARTITION BY 구문은 [OVER 절&#40;Transact-SQL& #41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.  
  
 \<order_by_clause>  
 파티션의 각 행에 NTILE 값이 할당되는 순서를 결정합니다. 순위 함수에 \<order_by_clause>가 사용된 경우 정수는 열을 나타낼 수 없습니다.  
  
## <a name="return-types"></a>반환 형식  
 **bigint**  
  
## <a name="remarks"></a>설명  
 파티션의 행 수를 *integer_expression*으로 나눌 수 없는 경우 멤버 수 하나의 차이가 있는 두 가지 크기의 그룹이 생성됩니다. OVER 절이 지정한 순서에서 큰 그룹이 작은 그룹 앞에 옵니다. 예를 들어 행의 총 수가 53개이고 그룹 수가 5개이면 처음 3개 그룹은 11개의 행을 포함하고 나머지 두 개 그룹은 10개의 행을 포함합니다. 반면에 행의 총 수를 그룹 수로 나눌 수 있으면 각 그룹에 행이 똑같이 분산됩니다. 예를 들어 행의 총 수가 50개이고 그룹이 5개 있으면 각 그룹이 10개의 행을 포함합니다.  
  
 NTILE은 비결정적입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
  
### <a name="a-dividing-rows-into-groups"></a>A. 행을 그룹으로 나누기  
 다음 예에서는 연간 누계 매출을 기준으로 행을 네 개의 직원 그룹으로 나눕니다. 총 행 수를 그룹 수로 나눌 수 없으므로 처음 두 그룹에는 네 개의 행이 포함되고 나머지 그룹에는 각각 세 개의 행이 포함됩니다.  
  
```  
USE AdventureWorks2012;   
GO  
SELECT p.FirstName, p.LastName  
    ,NTILE(4) OVER(ORDER BY SalesYTD DESC) AS Quartile  
    ,CONVERT(NVARCHAR(20),s.SalesYTD,1) AS SalesYTD  
    , a.PostalCode  
FROM Sales.SalesPerson AS s   
INNER JOIN Person.Person AS p   
    ON s.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.Address AS a   
    ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
FirstName      LastName              Quartile  SalesYTD       PostalCode  
-------------  --------------------- --------- -------------- ----------  
Linda          Mitchell              1         4,251,368.55   98027  
Jae            Pak                   1         4,116,871.23   98055  
Michael        Blythe                1         3,763,178.18   98027  
Jillian        Carson                1         3,189,418.37   98027  
Ranjit         Varkey Chudukatil     2         3,121,616.32   98055  
José           Saraiva               2         2,604,540.72   98055  
Shu            Ito                   2         2,458,535.62   98055  
Tsvi           Reiter                2         2,315,185.61   98027  
Rachel         Valdez                3         1,827,066.71   98055  
Tete           Mensa-Annan           3         1,576,562.20   98055  
David          Campbell              3         1,573,012.94   98055  
Garrett        Vargas                4         1,453,719.47   98027  
Lynn           Tsoflias              4         1,421,810.92   98055  
Pamela         Ansman-Wolfe          4         1,352,577.13   98027  

(14 row(s) affected)  
```  
  
### <a name="b-dividing-the-result-set-by-using-partition-by"></a>B. PARTITION BY를 사용하여 결과 집합 나누기  
 다음 예에서는 예 1의 코드에 `PARTITION BY` 인수를 추가합니다. 행은 먼저 `PostalCode`로 분할된 다음 각 `PostalCode` 내에 4개 그룹으로 나누어집니다. 또한 이 예에서는 변수 `@NTILE_Var`을 선언하고 이 변수를 사용하여 *integer_expression* 매개 변수의 값을 지정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @NTILE_Var int = 4;  
  
SELECT p.FirstName, p.LastName  
    ,NTILE(@NTILE_Var) OVER(PARTITION BY PostalCode ORDER BY SalesYTD DESC) AS Quartile  
    ,CONVERT(NVARCHAR(20),s.SalesYTD,1) AS SalesYTD  
    ,a.PostalCode  
FROM Sales.SalesPerson AS s   
INNER JOIN Person.Person AS p   
    ON s.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.Address AS a   
    ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
FirstName    LastName             Quartile SalesYTD      PostalCode  
------------ -------------------- -------- ------------  ----------  
Linda        Mitchell             1        4,251,368.55  98027  
Michael      Blythe               1        3,763,178.18  98027  
Jillian      Carson               2        3,189,418.37  98027  
Tsvi         Reiter               2        2,315,185.61  98027  
Garrett      Vargas               3        1,453,719.47  98027  
Pamela       Ansman-Wolfe         4        1,352,577.13  98027  
Jae          Pak                  1        4,116,871.23  98055  
Ranjit       Varkey Chudukatil    1        3,121,616.32  98055  
José         Saraiva              2        2,604,540.72  98055  
Shu          Ito                  2        2,458,535.62  98055  
Rachel       Valdez               3        1,827,066.71  98055  
Tete         Mensa-Annan          3        1,576,562.20  98055  
David        Campbell             4        1,573,012.94  98055  
Lynn         Tsoflias             4        1,421,810.92  98055  
  
(14 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-dividing-rows-into-groups"></a>C. 행을 그룹으로 나누기  
 다음 예에서는 NTILE 함수를 사용하여 2003년에 할당된 판매 할당량을 기반으로 영업 담당자 집합을 4개의 그룹으로 나눕니다. 행의 총 수를 그룹 수로 나눌 수 없으므로 첫 번째 그룹에는 5개의 행이 있고 나머지 그룹에는 각각 4개의 행이 있습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT e.LastName, NTILE(4) OVER(ORDER BY SUM(SalesAmountQuota) DESC) AS Quartile,  
       CONVERT (VARCHAR(13), SUM(SalesAmountQuota), 1) AS SalesQuota  
FROM dbo.DimEmployee AS e   
INNER JOIN dbo.FactSalesQuota AS sq   
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE sq.CalendarYear = 2003  
    AND SalesTerritoryKey IS NOT NULL AND SalesAmountQuota <> 0  
GROUP BY e.LastName  
ORDER BY Quartile, e.LastName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName          Quartile SalesYTD  
----------------- -------- ------------`  
Blythe            1        4,716,000.00  
Carson            1        4,350,000.00  
Mitchell          1        4,682,000.00  
Pak               1        5,142,000.00  
Varkey Chudukatil 1        2,940,000.00  
Ito               2        2,644,000.00  
Saraiva           2        2,293,000.00  
Vargas            2        1,617,000.00  
Ansman-Wolfe      3        1,183,000.00  
Campbell          3        1,438,000.00  
Mensa-Annan       3        1,481,000.00  
Valdez            3        1,294,000.00  
Abbas             4          172,000.00  
Albert            4          651,000.00  
Jiang             4          544,000.00  
Tsoflias          4          867,000.00
```  
  
### <a name="d-dividing-the-result-set-by-using-partition-by"></a>D. PARTITION BY를 사용하여 결과 집합 나누기  
 다음 예에서는 예 1의 코드에 PARTITION BY 인수를 추가합니다. 행은 먼저 `SalesTerritoryCountry`로 분할된 다음, 각 `SalesTerritoryCountry` 내에서 두 그룹으로 나뉩니다. OVER 절의 ORDER BY는 NTILE을 정렬하고, SELECT 문의 ORDER BY는 결과 집합을 정렬합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT e.LastName, NTILE(2) OVER(PARTITION BY e.SalesTerritoryKey ORDER BY SUM(SalesAmountQuota) DESC) AS Quartile,  
       CONVERT (VARCHAR(13), SUM(SalesAmountQuota), 1) AS SalesQuota  
   ,st.SalesTerritoryCountry  
FROM dbo.DimEmployee AS e   
INNER JOIN dbo.FactSalesQuota AS sq   
    ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st  
    ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE sq.CalendarYear = 2003  
GROUP BY e.LastName,e.SalesTerritoryKey,st.SalesTerritoryCountry  
ORDER BY st.SalesTerritoryCountry, Quartile;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName          Quartile SalesYTD       SalesTerritoryCountry  
----------------- -------- -------------- ------------------  
Tsoflias          1         867,000.00     Australia  
Saraiva           1        2,293,000.00    Canada  
Varkey Chudukatil 1        2,940,000.00    France  
Valdez            1        1,294,000.00    Germany  
Alberts           1          651,000.00    NA  
Jiang             1          544,000.00    NA  
Pak               1        5,142,000.00    United Kingdom  
Mensa-Annan       1        1,481,000.00    United States  
Campbell          1        1,438,000.00    United States  
Reiter            1        2,768,000.00    United States  
Blythe            1        4,716,000.00    United States  
Carson            1        4,350,000.00     United States  
Mitchell          1        4,682,000.00     United States  
Vargas            2        1,617,000.00     Canada  
Abbas             2          172,000.00     NA  
Ito               2        2,644,000.00     United States  
Ansman-Wolfe      2        1,183,000.00     United States
```  
  
## <a name="see-also"></a>참고 항목  
 [RANK&#40;Transact-SQL&#41;](../../t-sql/functions/rank-transact-sql.md)   
 [DENSE_RANK&#40;Transact-SQL&#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [ROW_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/row-number-transact-sql.md)   
 [순위 함수&#40;Transact-SQL&#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  


