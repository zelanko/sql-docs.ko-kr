---
title: GROUPING_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GROUPING_ID_TSQL
- GROUPING_ID
dev_langs:
- TSQL
helpviewer_keywords:
- GROUP BY clause, GROUPING_ID
- GROUPING_ID function
ms.assetid: c1050658-b19f-42ee-9a05-ecd6a73b896c
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: cbfbed6239d48cf01e65411250b163797d13333c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65943074"
---
# <a name="groupingid-transact-sql"></a>GROUPING_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  그룹 수준을 계산하는 함수입니다. GROUP BY 절이 지정된 경우 GROUPING_ID는 SELECT \<select> 목록, HAVING 및 ORDER BY 절에만 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GROUPING_ID ( <column_expression>[ ,...n ] )  
```  
  
## <a name="arguments"></a>인수  
 \<column_expression>  
 [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) 절의 *column_expression*입니다.  
  
## <a name="return-type"></a>반환 형식  
 **ssNoversion**  
  
## <a name="remarks"></a>Remarks  
 GROUPING_ID \<column_expression>은 GROUP BY 목록의 식과 정확하게 일치해야 합니다. 예를 들어 DATEPART(yyyy, \<*column name*>)를 기준으로 그룹화하는 경우에는 GROUPING_ID(DATEPART(yyyy, \<*column name*>))를 사용하고, \<*column name*>를 기준으로 그룹화하는 경우에는 GROUPING_ID(\<*column name*>)를 사용하세요.  
  
## <a name="comparing-groupingid--to-grouping-"></a>GROUPING_ID ()와 GROUPING () 비교  
 GROUPING_ID (\<column_expression> [ **,** ...*n* ])는 각 출력 행의 열 목록에 있는 각 열에 대해 반환되는 동등 함수인 GROUPING (\<column_expression>)을 0과 1로 구성된 문자열로 입력합니다. GROUPING_ID는 문자열을 밑이 2인 숫자로 해석하고 그에 해당하는 정수를 반환합니다. 예를 들어 다음 문을 살펴보세요: `SELECT a, b, c, SUM(d),``GROUPING_ID(a,b,c)``FROM T GROUP BY <group by list>`. 다음 표에서는 GROUPING_ID () 입력 및 출력 값을 보여 줍니다.  
  
|집계된 열|GROUPING_ID (a, b, c) 입력 = GROUPING(a) + GROUPING(b) + GROUPING(c)|GROUPING_ID () 출력|  
|------------------------|---------------------------------------------------------------------------------------|------------------------------|  
|`a`|`100`|`4`|  
|`b`|`010`|`2`|  
|`c`|`001`|`1`|  
|`ab`|`110`|`6`|  
|`ac`|`101`|`5`|  
|`bc`|`011`|`3`|  
|`abc`|`111`|`7`|  
  
## <a name="technical-definition-of-groupingid-"></a>GROUPING_ID ()의 기술적 정의  
 각 GROUPING_ID 인수는 GROUP BY 목록의 요소여야 합니다. GROUPING_ID ()는 최하위 N 비트가 lit인 **integer** 비트맵을 반환합니다. lit **bit**는 해당 인수가 지정된 출력 행에 대해 그룹화 열이 아님을 나타냅니다. 최하위 **bit**는 인수 N에 해당하고 N-1번째 최하위 **bit**는 인수 1에 해당합니다.<sup></sup>  
  
## <a name="groupingid--equivalents"></a>GROUPING_ID ()와 동일한 기능의 함수  
 단일 그룹화 쿼리의 경우 GROUPING (\<column_expression>)은 GROUPING_ID (\<column_expression>)와 같으며 둘 다 0을 반환합니다.  
  
 예를 들어 다음 두 개의 문은 동일합니다.  
  
 문 A:  
  
```  
SELECT GROUPING_ID(A,B)  
FROM T   
GROUP BY CUBE(A,B)   
```  
  
 문 B:  
  
```  
SELECT 3 FROM T GROUP BY ()  
UNION ALL  
SELECT 1 FROM T GROUP BY A  
UNION ALL  
SELECT 2 FROM T GROUP BY B  
UNION ALL  
SELECT 0 FROM T GROUP BY A,B  
```  
  
## <a name="examples"></a>예  
  
### <a name="a-using-groupingid-to-identify-grouping-levels"></a>1\. GROUPING_ID를 사용하여 그룹화 수준 식별  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Name`과 `Title`, `Name,` 및 Company Total별 직원 수를 반환합니다. `GROUPING_ID()`는 `Title` 열의 각 행에 대해 집계 수준을 식별하는 값을 생성합니다.  
  
```  
SELECT D.Name  
    ,CASE   
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 0 THEN E.JobTitle  
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 1 THEN N'Total: ' + D.Name   
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 3 THEN N'Company Total:'  
        ELSE N'Unknown'  
    END AS N'Job Title'  
    ,COUNT(E.BusinessEntityID) AS N'Employee Count'  
FROM HumanResources.Employee E  
    INNER JOIN HumanResources.EmployeeDepartmentHistory DH  
        ON E.BusinessEntityID = DH.BusinessEntityID  
    INNER JOIN HumanResources.Department D  
        ON D.DepartmentID = DH.DepartmentID       
WHERE DH.EndDate IS NULL  
    AND D.DepartmentID IN (12,14)  
GROUP BY ROLLUP(D.Name, E.JobTitle);  
```  
  
### <a name="b-using-groupingid-to-filter-a-result-set"></a>2\. GROUPING_ID를 사용하여 결과 집합 필터링  
  
#### <a name="simple-example"></a>간단한 예  
 다음 예제에서 title별 직원 수를 갖는 행만 반환하려면 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `HAVING GROUPING_ID(D.Name, E.JobTitle); = 0`에서 주석 문자를 제거하세요. department별 직원 수를 갖는 행만 반환하려면 `HAVING GROUPING_ID(D.Name, E.JobTitle) = 1;`에서 주석 문자를 제거하세요.  
  
```  
SELECT D.Name  
    ,E.JobTitle  
    ,GROUPING_ID(D.Name, E.JobTitle) AS 'Grouping Level'  
    ,COUNT(E.BusinessEntityID) AS N'Employee Count'  
FROM HumanResources.Employee AS E  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS DH  
        ON E.BusinessEntityID = DH.BusinessEntityID  
    INNER JOIN HumanResources.Department AS D  
        ON D.DepartmentID = DH.DepartmentID       
WHERE DH.EndDate IS NULL  
    AND D.DepartmentID IN (12,14)  
GROUP BY ROLLUP(D.Name, E.JobTitle)  
--HAVING GROUPING_ID(D.Name, E.JobTitle) = 0; --All titles  
--HAVING GROUPING_ID(D.Name, E.JobTitle) = 1; --Group by Name;  
```  
  
 다음은 필터링되지 않은 결과 집합입니다.  
  
|속성|Title|Grouping Level|Employee Count|속성|  
|----------|-----------|--------------------|--------------------|----------|  
|문서 제어|Control Specialist|0|2|문서 제어|  
|문서 제어|Document Control Assistant|0|2|문서 제어|  
|문서 제어|Document Control Manager|0|1|문서 제어|  
|문서 제어|NULL|1|5|문서 제어|  
|시설 및 유지 관리|Facilities Administrative Assistant|0|1|시설 및 유지 관리|  
|시설 및 유지 관리|Facilities Manager|0|1|시설 및 유지 관리|  
|시설 및 유지 관리|Janitor|0|4|시설 및 유지 관리|  
|시설 및 유지 관리|Maintenance Supervisor|0|1|시설 및 유지 관리|  
|시설 및 유지 관리|NULL|1|7|시설 및 유지 관리|  
|NULL|NULL|3|12|NULL|  
  
#### <a name="complex-example"></a>복잡한 예  
 다음 예제에서는 여러 개의 그룹화 수준을 그룹화 수준별로 포함하는 결과 집합을 필터링하는 데 `GROUPING_ID()`를 사용합니다. 그룹화 수준을 기준으로 뷰를 필터링하는 매개 변수를 전달하여 뷰를 호출하는 저장 프로시저와 여러 그룹화 수준을 포함하는 뷰를 만드는 데 비슷한 코드를 사용할 수 있습니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```  
DECLARE @Grouping nvarchar(50);  
DECLARE @GroupingLevel smallint;  
SET @Grouping = N'CountryRegionCode Total';  
  
SELECT @GroupingLevel = (  
    CASE @Grouping  
        WHEN N'Grand Total'             THEN 15  
        WHEN N'SalesPerson Total'       THEN 14  
        WHEN N'Store Total'             THEN 13  
        WHEN N'Store SalesPerson Total' THEN 12  
        WHEN N'CountryRegionCode Total' THEN 11  
        WHEN N'Group Total'             THEN 7  
        ELSE N'Unknown'  
    END);  
  
SELECT   
    T.[Group]  
    ,T.CountryRegionCode  
    ,S.Name AS N'Store'  
    ,(SELECT P.FirstName + ' ' + P.LastName   
        FROM Person.Person AS P   
        WHERE P.BusinessEntityID = H.SalesPersonID)  
        AS N'Sales Person'  
    ,SUM(TotalDue)AS N'TotalSold'  
    ,CAST(GROUPING(T.[Group])AS char(1)) +   
        CAST(GROUPING(T.CountryRegionCode)AS char(1)) +   
        CAST(GROUPING(S.Name)AS char(1)) +   
        CAST(GROUPING(H.SalesPersonID)AS char(1))   
        AS N'GROUPING base-2'  
    ,GROUPING_ID((T.[Group])  
        ,(T.CountryRegionCode),(S.Name),(H.SalesPersonID)  
        ) AS N'GROUPING_ID'  
    ,CASE   
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 15 THEN N'Grand Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 14 THEN N'SalesPerson Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 13 THEN N'Store Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 12 THEN N'Store SalesPerson Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 11 THEN N'CountryRegionCode Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) =  7 THEN N'Group Total'  
        ELSE N'Error'  
        END AS N'Level'  
FROM Sales.Customer AS C  
    INNER JOIN Sales.Store AS S  
        ON C.StoreID  = S.BusinessEntityID   
    INNER JOIN Sales.SalesTerritory AS T  
        ON C.TerritoryID  = T.TerritoryID   
    INNER JOIN Sales.SalesOrderHeader AS H  
        ON C.CustomerID = H.CustomerID  
GROUP BY GROUPING SETS ((S.Name,H.SalesPersonID)  
    ,(H.SalesPersonID),(S.Name)  
    ,(T.[Group]),(T.CountryRegionCode),()  
    )  
HAVING GROUPING_ID(  
    (T.[Group]),(T.CountryRegionCode),(S.Name),(H.SalesPersonID)  
    ) = @GroupingLevel  
ORDER BY   
    GROUPING_ID(S.Name,H.SalesPersonID),GROUPING_ID((T.[Group])  
    ,(T.CountryRegionCode)  
    ,(S.Name)  
    ,(H.SalesPersonID))ASC;  
```  
  
### <a name="c-using-groupingid--with-rollup-and-cube-to-identify-grouping-levels"></a>C. GROUPING_ID ()를 ROLLUP 및 CUBE와 함께 사용하여 그룹화 수준 식별  
 다음 예제에서의 코드는 `GROUPING()`을 사용하여 `Bit Vector(base-2)` 열을 계산하는 방법을 보여 줍니다. `GROUPING_ID()`는 해당 `Integer Equivalent` 열을 계산하는 데 사용됩니다. `GROUPING_ID()` 함수의 열 순서는 `GROUPING()` 함수로 연결되는 열의 순서와 반대입니다.  
  
 이 예제에서 `GROUPING_ID()`는 `Grouping Level` 열의 각 행에 대해 그룹화 수준을 식별하는 값을 생성합니다. 그룹화 수준이 1로 시작되는 연속된 정수 목록(0, 1, 2,...*n*)이 아닌 경우도 있습니다.  
  
> [!NOTE]  
>  GROUPING 및 GROUPING_ID를 HAVING 절에 사용하여 결과 집합을 필터링할 수 있습니다.  
  
#### <a name="rollup-example"></a>ROLLUP 예  
 다음 CUBE 예에서는 모든 그룹화 수준이 표시되지만 이 예제에서는 일부 그룹화 수준만 표시됩니다. `ROLLUP` 목록의 열 순서가 변경될 경우 `Grouping Level` 열의 수준 값도 변경해야 합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,DATEPART(mm,OrderDate) AS N'Month'  
    ,DATEPART(dd,OrderDate) AS N'Day'  
    ,SUM(TotalDue) AS N'Total Due'  
    ,CAST(GROUPING(DATEPART(dd,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(mm,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(yyyy,OrderDate))AS char(1))   
     AS N'Bit Vector(base-2)'  
    ,GROUPING_ID(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))   
        AS N'Integer Equivalent'  
    ,CASE  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 0 THEN N'Year Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 1 THEN N'Year Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 2 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 3 THEN N'Year'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 4 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 5 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 6 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 7 THEN N'Grand Total'  
    ELSE N'Error'  
    END AS N'Grouping Level'  
FROM Sales.SalesOrderHeader  
WHERE DATEPART(yyyy,OrderDate) IN(N'2007',N'2008')  
    AND DATEPART(mm,OrderDate) IN(1,2)  
    AND DATEPART(dd,OrderDate) IN(1,2)  
GROUP BY ROLLUP(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))  
ORDER BY GROUPING_ID(DATEPART(mm,OrderDate)  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(dd,OrderDate)  
    )  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate);  
```  
  
 다음은 결과 집합의 일부입니다.  
  
|Year|Month|Day|Total Due|Bit Vector (base-2)|Integer Equivalent|Grouping Level|  
|----------|-----------|---------|---------------|----------------------------|------------------------|--------------------|  
|2007|1|1|1497452.6066|000|0|Year Month Day|  
|2007|1|2|21772.3494|000|0|Year Month Day|  
|2007|2|1|2705653.5913|000|0|Year Month Day|  
|2007|2|2|21684.4068|000|0|Year Month Day|  
|2008|1|1|1908122.0967|000|0|Year Month Day|  
|2008|1|2|46458.0691|000|0|Year Month Day|  
|2008|2|1|3108771.9729|000|0|Year Month Day|  
|2008|2|2|54598.5488|000|0|Year Month Day|  
|2007|1|NULL|1519224.956|100|1|Year Month|  
|2007|2|NULL|2727337.9981|100|1|Year Month|  
|2008|1|NULL|1954580.1658|100|1|Year Month|  
|2008|2|NULL|3163370.5217|100|1|Year Month|  
|2007|NULL|NULL|4246562.9541|110|3|Year|  
|2008|NULL|NULL|5117950.6875|110|3|Year|  
|NULL|NULL|NULL|9364513.6416|111|7|총합계|  
  
#### <a name="cube-example"></a>CUBE 예  
 이 예제에서 `GROUPING_ID()` 함수는 `Grouping Level` 열의 각 행에 대해 그룹화 수준을 식별하는 값을 생성합니다.  
  
 앞 예제에 나온 `ROLLUP`과 달리 `CUBE`는 모든 그룹화 수준을 출력합니다. `CUBE` 목록의 열 순서가 변경될 경우 `Grouping Level` 열의 수준 값도 변경해야 합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,DATEPART(mm,OrderDate) AS N'Month'  
    ,DATEPART(dd,OrderDate) AS N'Day'  
    ,SUM(TotalDue) AS N'Total Due'  
    ,CAST(GROUPING(DATEPART(dd,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(mm,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(yyyy,OrderDate))AS char(1))   
        AS N'Bit Vector(base-2)'  
    ,GROUPING_ID(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))   
        AS N'Integer Equivalent'  
    ,CASE  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 0 THEN N'Year Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 1 THEN N'Year Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 2 THEN N'Year Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 3 THEN N'Year'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 4 THEN N'Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 5 THEN N'Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 6 THEN N'Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 7 THEN N'Grand Total'  
    ELSE N'Error'  
    END AS N'Grouping Level'  
FROM Sales.SalesOrderHeader  
WHERE DATEPART(yyyy,OrderDate) IN(N'2007',N'2008')  
    AND DATEPART(mm,OrderDate) IN(1,2)  
    AND DATEPART(dd,OrderDate) IN(1,2)  
GROUP BY CUBE(DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate))  
ORDER BY GROUPING_ID(DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate)  
    )  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate);  
```  
  
 다음은 결과 집합의 일부입니다.  
  
|Year|Month|Day|Total Due|Bit Vector (base-2)|Integer Equivalent|Grouping Level|  
|----------|-----------|---------|---------------|----------------------------|------------------------|--------------------|  
|2007|1|1|1497452.6066|000|0|Year Month Day|  
|2007|1|2|21772.3494|000|0|Year Month Day|  
|2007|2|1|2705653.5913|000|0|Year Month Day|  
|2007|2|2|21684.4068|000|0|Year Month Day|  
|2008|1|1|1908122.0967|000|0|Year Month Day|  
|2008|1|2|46458.0691|000|0|Year Month Day|  
|2008|2|1|3108771.9729|000|0|Year Month Day|  
|2008|2|2|54598.5488|000|0|Year Month Day|  
|2007|1|NULL|1519224.956|100|1|Year Month|  
|2007|2|NULL|2727337.9981|100|1|Year Month|  
|2008|1|NULL|1954580.1658|100|1|Year Month|  
|2008|2|NULL|3163370.5217|100|1|Year Month|  
|2007|NULL|1|4203106.1979|010|2|Year Day|  
|2007|NULL|2|43456.7562|010|2|Year Day|  
|2008|NULL|1|5016894.0696|010|2|Year Day|  
|2008|NULL|2|101056.6179|010|2|Year Day|  
|2007|NULL|NULL|4246562.9541|110|3|Year|  
|2008|NULL|NULL|5117950.6875|110|3|Year|  
|NULL|1|1|3405574.7033|001|4|Month Day|  
|NULL|1|2|68230.4185|001|4|Month Day|  
|NULL|2|1|5814425.5642|001|4|Month Day|  
|NULL|2|2|76282.9556|001|4|Month Day|  
|NULL|1|NULL|3473805.1218|101|5|Month|  
|NULL|2|NULL|5890708.5198|101|5|Month|  
|NULL|NULL|1|9220000.2675|011|6|Day|  
|NULL|NULL|2|144513.3741|011|6|Day|  
|NULL|NULL|NULL|9364513.6416|111|7|총합계|  
  
## <a name="see-also"></a>참고 항목  
 [GROUPING&#40;Transact-SQL&#41;](../../t-sql/functions/grouping-transact-sql.md)   
 [GROUP BY&#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
