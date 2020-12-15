---
title: 하위 쿼리(SQL Server) | Microsoft Docs
description: SELECT, INSERT, UPDATE, DELETE 문이나 다른 하위 쿼리 내부에 중첩된 쿼리인 SQL Server의 하위 쿼리에 대해 알아봅니다.
ms.custom: ''
ms.date: 02/18/2018
ms.prod: sql
ms.technology: performance
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Subquery
- Subqueries
- subqueries [SQL Server], fundamentals
- subqueries [SQL Server], correlated
- subqueries [SQL Server], types
ms.assetid: bfc97432-c14c-4768-9dc5-a9c512f6b2bd
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f44ccb5de715b302f7b4db0b80fa4f3e5633021
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97406834"
---
# <a name="subqueries-sql-server"></a>하위 쿼리(SQL Server)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
 
하위 쿼리는 `SELECT`, `INSERT`, `UPDATE` 또는 `DELETE` 문이나 다른 하위 쿼리 내부에 중첩된 쿼리입니다. 하위 쿼리는 식이 허용되는 모든 위치에서 사용할 수 있습니다. 다음 예에서 하위 쿼리는 SELECT 문에서 MaxUnitPrice라는 열 식으로 사용됩니다.

```sql
USE AdventureWorks2016;
GO
SELECT Ord.SalesOrderID, Ord.OrderDate,
    (SELECT MAX(OrdDet.UnitPrice)
     FROM Sales.SalesOrderDetail AS OrdDet
     WHERE Ord.SalesOrderID = OrdDet.SalesOrderID) AS MaxUnitPrice
FROM Sales.SalesOrderHeader AS Ord;
GO
```

## <a name="subquery-fundamentals"></a><a name="fundamentals"></a> 하위 쿼리 기본 사항
하위 쿼리는 내부 쿼리 또는 내부 선택이라고도 하며 하위 쿼리가 포함된 문을 외부 쿼리 또는 외부 선택이라고 합니다.   

하위 쿼리가 포함된 대부분의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 조인으로 나타낼 수 있습니다. 다른 문제는 하위 쿼리에만 해당됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 하위 쿼리가 포함된 문과 하위 쿼리가 포함되지 않았으나 이와 의미상으로 동일한 문 사이에는 성능상의 차이가 없습니다. 하지만 존재 테스트를 해야 할 경우 조인을 사용하면 성능이 향상될 수 있습니다. 그렇지 않으면 중복 값을 제거하기 위해 각 외부 쿼리 결과에 대해 중첩 쿼리를 처리해야 합니다. 이런 경우 조인을 사용하면 결과를 더 쉽게 얻을 수 있습니다. 다음 예는 동일한 결과 집합을 반환하는 하위 쿼리 `SELECT`와 조인 `SELECT`를 보여 줍니다.

```sql
USE AdventureWorks2016;
GO

/* SELECT statement built using a subquery. */
SELECT Name
FROM Production.Product
WHERE ListPrice =
    (SELECT ListPrice
     FROM Production.Product
     WHERE Name = 'Chainring Bolts' );
GO

/* SELECT statement built using a join that returns
   the same result set. */
SELECT Prd1. Name
FROM Production.Product AS Prd1
     JOIN Production.Product AS Prd2
       ON (Prd1.ListPrice = Prd2.ListPrice)
WHERE Prd2. Name = 'Chainring Bolts';
GO
```

외부 SELECT 문에 중첩된 하위 쿼리는 다음과 같은 구성 요소를 갖습니다.    
-   일반적인 SELECT 목록 구성 요소가 포함된 일반 `SELECT` 쿼리   
-   하나 이상의 테이블이나 뷰 이름이 포함된 일반 `FROM` 절   
-   `WHERE` 절(옵션)   
-   `GROUP BY` 절(옵션)   
-   `HAVING` 절(옵션)   

하위 쿼리의 SELECT 쿼리는 항상 괄호로 묶습니다. 또한 `COMPUTE` 또는 `FOR BROWSE` 절은 포함할 수 없으며 TOP 절이 지정된 경우 `ORDER BY` 절만 포함할 수 있습니다.   

하위 쿼리는 외부 `SELECT`, `INSERT`, `UPDATE` 또는 `DELETE` 문의 `WHERE` 또는 `HAVING` 절이나 다른 하위 쿼리 내부에 중첩될 수 있습니다. 최대 32개 수준까지 중첩이 가능하지만 이 값은 사용 가능한 메모리 및 쿼리에 있는 다른 식의 복잡성에 따라 달라지며 개별 쿼리에서 32개 수준까지 중첩을 지원하지 않을 수도 있습니다. 하위 쿼리는 단일 값을 반환할 경우 식을 사용할 수 있는 모든 위치에 나타날 수 있습니다.   

테이블이 하위 쿼리에만 나타나고 외부 쿼리에는 나타나지 않으면 해당 테이블의 열은 결과(외부 쿼리의 SELECT 목록)에 포함될 수 없습니다.   

하위 쿼리가 포함된 문은 다음 중 한 가지 형식을 취합니다.   
-   WHERE 식 \[NOT] IN(하위 쿼리)
-   WHERE 식 comparison_operator \[ANY | ALL](하위 쿼리)
-   WHERE \[NOT] EXISTS(하위 쿼리)   

일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 하위 쿼리는 독립적인 쿼리처럼 평가될 수 있습니다. 개념적으로 하위 쿼리 결과는 외부 쿼리로 대체됩니다. 물론 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 하위 쿼리가 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 반드시 이렇게 처리되는 것은 아닙니다.    

하위 쿼리에는 다음과 같은 세 가지 기본 유형이 있습니다. 
-   `ANY` 또는 `ALL`에 의해 수정된 비교 연산자나 `IN`으로 시작하는 목록에서 실행
-   수정되지 않은 비교 연산자로 시작하고 단일 값을 반환
-   `EXISTS`로 시작하는 존재 테스트

## <a name="subquery-rules"></a><a name="rules"></a> 하위 쿼리 규칙
하위 쿼리에는 다음과 같은 제한 사항이 있습니다. 
-   비교 연산자로 시작하는 하위 쿼리의 선택 목록에는 식이나 열 이름이 한 개만 포함될 수 있습니다(`EXISTS` 및 `IN`이 `SELECT *`나 목록에서 실행될 경우는 제외).   
-   외부 쿼리의 `WHERE` 절에 열 이름이 포함되면 하위 쿼리 선택 목록의 열과 조인이 호환 가능해야 합니다.   
-   **ntext**, **text** 및 **image** 데이터 형식은 하위 쿼리의 선택 목록에 사용할 수 없습니다.   
-   단일 값을 반환해야 하므로 수정되지 않은 비교 연산자로 시작하는 하위 쿼리(ANY 또는 ALL 키워드가 나오지 않음)에는 `GROUP BY` 및 `HAVING` 절이 포함될 수 없습니다.   
-   GROUP BY가 포함된 하위 쿼리에는 `DISTINCT` 키워드를 사용할 수 없습니다.
-   `COMPUTE` 및 `INTO` 절은 지정할 수 없습니다.   
-   `ORDER BY`은 `TOP`을 함께 지정해야만 지정할 수 있습니다.   
-   하위 쿼리를 사용하여 만든 뷰는 업데이트할 수 없습니다.   
-   `EXISTS`로 시작하는 하위 쿼리의 선택 목록은 규칙에 따라 단일 열 이름 대신 별표(\*)로 구성됩니다. `EXISTS`로 시작하는 하위 쿼리는 존재 테스트를 만들며 데이터 대신 TRUE 또는 FALSE를 반환하므로 `EXISTS`로 시작하는 하위 쿼리에 대한 규칙은 표준 선택 목록의 규칙과 동일합니다.   

## <a name="qualifying-column-names-in-subqueries"></a><a name="qualifying"></a> 하위 쿼리의 열 이름 한정
다음 예제에서는 외부 쿼리의 `WHERE` 절에 있는 *BusinessEntityID* 열이 외부 쿼리의 `FROM` 절에 있는 테이블 이름(*Sales.Store*)으로 암시적으로 한정됩니다. 하위 쿼리의 SELECT 목록에서 *CustomerID* 에 대한 참조는 하위 쿼리의 `FROM` 절, 즉 *Sales.Customer* 테이블로 한정됩니다.

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Sales.Store
WHERE BusinessEntityID NOT IN
    (SELECT CustomerID
     FROM Sales.Customer
     WHERE TerritoryID = 5);
GO
```

일반적으로 문의 열 이름은 같은 수준의 `FROM` 절에서 참조하는 테이블로 암시적으로 한정됩니다. 하위 쿼리의 `FROM` 절에서 참조하는 테이블에 없는 열은 외부 쿼리의 `FROM` 절에서 참조하는 테이블로 암시적으로 한정됩니다.   

다음은 이러한 암시적 한정이 지정된 쿼리입니다.

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Sales.Store
WHERE Sales.Store.BusinessEntityID NOT IN
    (SELECT Sales.Customer.CustomerID
     FROM Sales.Customer
     WHERE TerritoryID = 5);
GO
```

테이블 이름을 명시적으로 지정해도 되며 언제든지 명시적 한정으로 테이블 이름에 대한 암시적 한정을 무시할 수 있습니다.   

> [!IMPORTANT]
> 하위 쿼리에서 참조하는 열이 하위 쿼리의 `FROM` 절에서 참조하는 테이블에는 없지만 외부 쿼리의 `FROM` 절에서 참조하는 테이블에는 있는 경우 쿼리가 오류 없이 실행됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 외부 쿼리의 테이블 이름으로 하위 쿼리의 열을 암시적으로 한정합니다.   

## <a name="multiple-levels-of-nesting"></a><a name="nesting"></a> 다중 중첩 수준
하위 쿼리에는 하나 이상의 하위 쿼리가 포함될 수 있습니다. 또한 문에 원하는 수만큼 하위 쿼리를 중첩시킬 수 있습니다.   

다음 쿼리는 영업 사원이기도 한 직원의 이름을 찾습니다.   

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person
WHERE BusinessEntityID IN
    (SELECT BusinessEntityID
     FROM HumanResources.Employee
     WHERE BusinessEntityID IN
        (SELECT BusinessEntityID
         FROM Sales.SalesPerson)
    );
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
LastName                                           FirstName
-------------------------------------------------- -----------------------
Jiang                                              Stephen
Abbas                                              Syed
Alberts                                            Amy
Ansman-Wolfe                                       Pamela
Campbell                                           David
Carson                                             Jillian
Ito                                                Shu
Mitchell                                           Linda
Reiter                                             Tsvi
Saraiva                                            Jos
Vargas                                             Garrett
Varkey Chudukatil                                  Ranjit
Valdez                                             Rachel
Tsoflias                                           Lynn
Pak                                                Jae
Blythe                                             Michael
Mensa-Annan                                        Tete

(17 row(s) affected)
```

가장 안쪽의 쿼리는 영업 사원 ID를 반환합니다. 이 쿼리보다 한 수준 위의 쿼리는 이러한 영업 사원 ID로 평가하여 직원의 연락처 ID 번호를 반환합니다. 마지막으로 외부 쿼리가 연락처 ID를 사용하여 직원 이름을 찾습니다.   

위의 쿼리를 조인으로 표시할 수도 있습니다.

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person c
INNER JOIN HumanResources.Employee e
ON c.BusinessEntityID = e.BusinessEntityID
JOIN Sales.SalesPerson s 
ON e.BusinessEntityID = s.BusinessEntityID;
GO
```

## <a name="correlated-subqueries"></a><a name="correlated"></a> 상관 하위 쿼리
대부분의 쿼리는 하위 쿼리를 한 번 실행하고 그 결과 값을 외부 쿼리의 `WHERE` 절에 대체함으로써 평가됩니다. 상관 하위 쿼리(반복 하위 쿼리라고도 함)가 포함된 쿼리에서 하위 쿼리는 외부 쿼리에 따라 값이 달라집니다. 즉, 하위 쿼리는 외부 쿼리에서 선택될 수 있는 각 행에 대해 한 번씩 반복적으로 실행됩니다.
다음 쿼리는 *SalesPerson* 테이블에서 보너스가 5000이고 *Employee* 및 *SalesPerson* 테이블에서 직원 ID 번호가 일치하는 각 직원의 성과 이름을 찾습니다.

```sql
USE AdventureWorks2016;
GO
SELECT DISTINCT c.LastName, c.FirstName, e.BusinessEntityID 
FROM Person.Person AS c JOIN HumanResources.Employee AS e
ON e.BusinessEntityID = c.BusinessEntityID 
WHERE 5000.00 IN
    (SELECT Bonus
    FROM Sales.SalesPerson sp
    WHERE e.BusinessEntityID = sp.BusinessEntityID) ;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
LastName FirstName BusinessEntityID
-------------------------- ---------- ------------
Ansman-Wolfe Pamela 280
Saraiva José 282

(2 row(s) affected)
```

이 문의 이전 하위 쿼리는 외부 쿼리와 독립적으로 평가할 수 없습니다. 하위 쿼리에는 *Employee.BusinessEntityID* 값이 필요하지만 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 *Employee* 의 다른 행을 검사할 때마다 바뀝니다.   
위의 쿼리는 다음과 같은 방법으로 평가됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 내부 쿼리에 각 행의 값을 대체함으로써 결과에 포함될 Employee 테이블의 각 행을 평가합니다.
예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 먼저 `Syed Abbas`에 대한 행을 검사하는 경우 *Employee.BusinessEntityID* 변수의 값이 285가 되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 값을 내부 쿼리에 대체합니다.

```sql
USE AdventureWorks2016;
GO
SELECT Bonus
FROM Sales.SalesPerson
WHERE BusinessEntityID = 285;
GO
```

`Syed Abbas`는 영업 사원이 아니기 때문에 보너스를 받지 않으므로 결과 값은 0이 되어 외부 쿼리는 다음으로 평가됩니다.

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person AS c JOIN HumanResources.Employee AS e
ON e.BusinessEntityID = c.BusinessEntityID 
WHERE 5000 IN (0.00);
GO
```

이 문의 결과는 false이므로 `Syed Abbas`에 대한 행은 결과에 포함되지 않습니다. `Pamela Ansman-Wolfe`에 대한 행에 같은 프로시저를 실행합니다. 그러면 이 행이 결과에 포함됩니다.     

상관 하위 쿼리는 외부 쿼리의 테이블에 있는 열을 테이블 반환 함수의 인수로 참조함으로써 `FROM` 절에 테이블 반환 함수를 포함할 수 있습니다. 이 경우 외부 쿼리의 각 행에 대해 테이블 반환 함수가 하위 쿼리에 따라 평가됩니다.    
  
## <a name="subquery-types"></a><a name="types"></a> 하위 쿼리 유형
하위 쿼리는 다음과 같이 여러 위치에서 지정할 수 있습니다. 
-   별칭과 함께 사용. 자세한 내용은 [별칭이 있는 하위 쿼리](#aliases)를 참조하세요.
-   `IN` 또는 `NOT IN` 있음. 자세한 내용은 [IN이 있는 하위 쿼리](#in) 및 [NOT IN이 있는 하위 쿼리](#notin)를 참조하세요.
-   `UPDATE`, `DELETE` 및 `INSERT` 문에서. 자세한 내용은 [UPDATE, DELETE 및 INSERT 문의 하위 쿼리](#upsert)를 참조하세요.
-   비교 연산자와 함께 사용. 자세한 내용은 [압축 연산자가 있는 하위 쿼리](#comparison)를 참조하세요.
-   `ANY`, `SOME`, 또는 `ALL` 있음. 자세한 내용은 [ANY, SOME 또는 ALL에 의해 수정된 비교 연산자](#comparison_modified)를 참조하세요.
-   `EXISTS` 또는 `NOT EXISTS` 있음. 자세한 내용은 [EXISTS가 있는 하위 쿼리](#exists) 및 [NOT EXISTS가 있는 하위 쿼리](#notexists)를 참조하세요.
-   식 대신 사용. 자세한 내용은 [식 대신 하위 쿼리 사용](#expression)을 참조하세요.

### <a name="subqueries-with-aliases"></a><a name="aliases"></a> 별칭이 있는 하위 쿼리
하위 쿼리와 외부 쿼리가 동일한 테이블을 참조(테이블을 자기 자신에게 조인)하는 문을 대부분 자체 조인이라고 합니다. 예를 들어 다음과 같은 하위 쿼리를 사용하여 특정 주에 있는 직원의 주소를 찾을 수 있습니다.   

```sql
USE AdventureWorks2016;
GO
SELECT StateProvinceID, AddressID
FROM Person.Address
WHERE AddressID IN
    (SELECT AddressID
     FROM Person.Address
     WHERE StateProvinceID = 39);
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
StateProvinceID AddressID
----------- -----------
39 942
39 955
39 972
39 22660

(4 row(s) affected)
```   

또는 자체 조인을 사용할 수도 있습니다.   

```sql
USE AdventureWorks2016;
GO
SELECT e1.StateProvinceID, e1.AddressID
FROM Person.Address AS e1
INNER JOIN Person.Address AS e2
ON e1.AddressID = e2.AddressID
AND e2.StateProvinceID = 39;
GO
```

자기 자신에게 조인된 테이블은 두 개의 다른 역할을 하므로 테이블 별칭이 필요합니다. 내부 쿼리와 외부 쿼리에서 동일한 테이블을 참조하는 중첩 쿼리에서도 별칭을 사용할 수 있습니다.    

```sql
USE AdventureWorks2016;
GO
SELECT e1.StateProvinceID, e1.AddressID
FROM Person.Address AS e1
WHERE e1.AddressID IN
    (SELECT e2.AddressID
     FROM Person.Address AS e2
     WHERE e2.StateProvinceID = 39);
GO
```

명시적 별칭은 하위 쿼리에서 *Person.Address* 에 대한 참조가 외부 쿼리에서의 참조와 동일하지 않음을 분명하게 해 줍니다.   

### <a name="subqueries-with-in"></a><a name="in"></a> IN이 있는 하위 쿼리
`IN`(또는 `NOT IN`)으로 시작하는 하위 쿼리의 결과는 값이 0 이상인 목록입니다. 하위 쿼리에서 결과를 반환하면 외부 쿼리에서 이 값을 사용합니다.    
다음 쿼리는 Adventure Works Cycles에서 만드는 모든 탈 것 제품의 이름을 검색합니다.     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]     

```
Name
----------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```

이 문은 두 단계로 나누어서 계산됩니다. 먼저 내부 쿼리는 이름이 'Wheel'(17)인 하위 범주 ID를 반환합니다. 두 번째는 이 값이 Product에서 하위 범주의 ID에 해당하는 제품 이름을 검색하는 외부 쿼리로 대체됩니다.     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN ('17');
GO
```

이 경우 하위 쿼리 대신 조인을 사용하면 결과에 둘 이상의 테이블에 포함된 열을 보여 줄 수 있다는 점이 다릅니다. 예를 들어 결과에 제품 하위 범주의 이름을 포함하려면 조인 버전을 사용해야 합니다.    

```sql
USE AdventureWorks2016;
GO
SELECT p.Name, s.Name
FROM Production.Product p
INNER JOIN Production.ProductSubcategory s
ON p.ProductSubcategoryID = s.ProductSubcategoryID
AND s.Name = 'Wheels';
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]    

```
Name
LL Mountain Front Wheel Wheels
ML Mountain Front Wheel Wheels
HL Mountain Front Wheel Wheels
LL Road Front Wheel Wheels
ML Road Front Wheel Wheels
HL Road Front Wheel Wheels
Touring Front Wheel Wheels
LL Mountain Rear Wheel Wheels
ML Mountain Rear Wheel Wheels
HL Mountain Rear Wheel Wheels
LL Road Rear Wheel Wheels
ML Road Rear Wheel Wheels
HL Road Rear Wheel Wheels
Touring Rear Wheel Wheels

(14 row(s) affected)
```    

다음 쿼리는 20개 이상의 Adventure Works Cycles 제품을 주문하고 평균 배달 리드 타임이 16일 미만으로 신용도가 좋은 모든 공급업체의 이름을 검색합니다.    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Purchasing.Vendor
WHERE CreditRating = 1
AND BusinessEntityID IN
    (SELECT BusinessEntityID
     FROM Purchasing.ProductVendor
     WHERE MinOrderQty >= 20
     AND AverageLeadTime < 16);
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
Name
--------------------------------------------------
Compete Enterprises, Inc
International Trek Center
First National Sport Co.
Comfort Road Bicycles
Circuit Cycles
First Rate Bicycles
Jeff's Sporting Goods
Competition Bike Training Systems
Electronic Bike Repair & Supplies
Crowley Sport
Expert Bike Co
Team Athletic Co.
Compete, Inc.   

(13 row(s) affected)
```   

내부 쿼리를 계산하여 하위 쿼리 조건을 만족하는 공급업체의 ID를 반환한 후 외부 쿼리를 계산합니다. 내부 쿼리 및 외부 쿼리 모두에 있는 WHERE 절에 둘 이상의 조건을 포함할 수 있습니다.   

조인을 사용하면 동일한 쿼리를 다음과 같이 표시할 수 있습니다.

```sql
USE AdventureWorks2016;
GO
SELECT DISTINCT Name
FROM Purchasing.Vendor v
INNER JOIN Purchasing.ProductVendor p
ON v.BusinessEntityID = p.BusinessEntityID
WHERE CreditRating = 1
  AND MinOrderQty >= 20
  AND AverageLeadTime < 16;
GO
```

조인은 항상 하위 쿼리로 표시할 수 있지만 하위 쿼리를 항상 조인으로 표시할 수는 없습니다. 그 이유는 조인이 대칭적이기 때문입니다. 즉, 어떤 순서로 테이블 A를 테이블 B에 조인해도 같은 결과를 얻습니다. 그러나 하위 쿼리가 있는 경우는 이에 해당되지 않습니다.    

### <a name="subqueries-with-not-in"></a><a name="notin"></a> NOT IN이 있는 하위 쿼리
NOT IN 키워드로 시작하는 하위 쿼리도 0개 이상의 값 목록을 반환합니다.   
다음은 완성된 자전거가 아닌 제품의 이름을 찾는 쿼리입니다.   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID NOT IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Mountain Bikes' 
        OR Name = 'Road Bikes'
        OR Name = 'Touring Bikes');
GO
```

이 문은 조인으로 변환할 수 없습니다. 이와 유사한 같지 않음 조인은 의미가 다릅니다. 즉 이 조인은 완성된 자전거 이외의 하위 범주에 있는 제품 이름을 찾습니다.      

### <a name="subqueries-in-update-delete-and-insert-statements"></a><a name="upsert"></a> UPDATE, DELETE 및 INSERT 문의 하위 쿼리
`UPDATE`, `DELETE`, `INSERT` 및 `SELECT` DML(데이터 조작 언어) 문에 하위 쿼리가 중첩될 수 있습니다.    

다음 예에서는 *Production.Product* 테이블의 *ListPrice* 열 값을 두 배로 만듭니다. `WHERE` 절의 하위 쿼리는 *Product* 테이블에서 업데이트되는 행을 *BusinessEntity* 1540이 제공하는 행으로만 제한하여 *Purchasing.ProductVendor* 테이블을 참조합니다.

```sql
USE AdventureWorks2016;
GO 
UPDATE Production.Product
SET ListPrice = ListPrice * 2
WHERE ProductID IN
    (SELECT ProductID 
     FROM Purchasing.ProductVendor
     WHERE BusinessEntityID = 1540);
GO
```

다음은 조인을 사용하여 동일한 기능을 수행하는 `UPDATE` 문입니다.

```sql
USE AdventureWorks2016;
GO 
UPDATE Production.Product
SET ListPrice = ListPrice * 2
FROM Production.Product AS p
INNER JOIN Purchasing.ProductVendor AS pv
    ON p.ProductID = pv.ProductID AND BusinessEntityID = 1540;
GO   
```

### <a name="subqueries-with-comparison-operators"></a><a name="comparison"></a> 비교 연산자가 있는 하위 쿼리
하위 쿼리는 다음 비교 연산자 중 하나로 시작할 수 있습니다. (=, < >, >, > =, <, ! >, ! < 또는 < =).   

수정되지 않은 비교 연산자(뒤에 `ANY` 또는 `ALL`이 나오지 않는 비교 연산자)로 시작하는 하위 쿼리는 `IN`으로 시작하는 하위 쿼리처럼 값 목록이 아닌 단일 값을 반환해야 합니다. 이러한 하위 쿼리가 둘 이상의 값을 반환하면 SQL Server는 오류 메시지를 표시합니다.    

수정되지 않은 비교 연산자로 시작하는 하위 쿼리를 사용하려면 하위 쿼리가 정확히 하나의 값만 반환한다는 것을 알 수 있도록 데이터와 문제의 특성을 충분히 이해해야 합니다.     

예를 들어 각 영업 사원이 하나의 판매 지역만 담당한다고 가정하고 `Linda Mitchell`이라는 사원이 담당하는 지역에 있는 고객을 찾을 경우 간단하게 '=' 비교 연산자로 시작하는 하위 쿼리로 문을 작성할 수 있습니다.    

```sql
USE AdventureWorks2016;
GO
SELECT CustomerID
FROM Sales.Customer
WHERE TerritoryID =
    (SELECT TerritoryID
     FROM Sales.SalesPerson
     WHERE BusinessEntityID = 276);
GO
```

그러나 `Linda Mitchell`이 두 개 이상의 판매 지역을 담당할 경우 오류 메시지가 나타납니다. 이런 경우 '=' 비교 연산자 대신 `IN` 구문(또는 =ANY)을 사용할 수 있습니다.    

수정되지 않은 비교 연산자로 시작하는 하위 쿼리는 단일 값을 반환하므로 집계 함수가 포함되는 경우가 많습니다. 예를 들어 다음 문은 제품 가격이 평균 가격보다 비싼 모든 제품의 이름을 찾습니다.     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >
    (SELECT AVG (ListPrice)
     FROM Production.Product);
GO
```     

수정되지 않은 비교 연산자로 시작하는 하위 쿼리는 단일 값을 반환해야 하므로 `GROUP BY` 또는 `HAVING` 절이 단일 값을 반환하지 않으면 하위 쿼리에 GROUP BY나 HAVING 절을 포함할 수 없습니다. 예를 들어 다음 쿼리에서는 하위 범주 14에 있는 가격이 가장 저렴한 제품보다 가격이 높은 제품을 찾습니다.     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >
    (SELECT MIN (ListPrice)
     FROM Production.Product
     GROUP BY ProductSubcategoryID
     HAVING ProductSubcategoryID = 14);
GO
```

### <a name="comparison-operators-modified-by-any-some-or-all"></a><a name="comparison_modified"></a> ANY, SOME 또는 ALL에 의해 수정된 비교 연산자
하위 쿼리를 시작하는 비교 연산자는 ALL 또는 ANY 키워드에 의해 수정될 수 있습니다. SOME은 `ANY`의 ISO 표준 동의어입니다.     

수정된 비교 연산자로 시작하는 하위 쿼리는 0개 이상의 값 목록을 반환하고 `GROUP BY` 또는 `HAVING` 절을 포함할 수 있습니다. 이러한 하위 쿼리는 `EXISTS`를 사용하여 다시 작성할 수 있습니다.     

> 비교 연산자를 예로 들면 `>ALL`은 모든 값보다 크다는 것을 의미합니다. 즉, 최대값보다 크다는 것을 나타냅니다. 예를 들어 `>ALL (1, 2, 3)`은 3보다 크다는 것을 의미합니다. `>ANY`는 적어도 하나의 값보다 큼 즉, 최소값보다 크다는 것을 의미합니다. 따라서 `>ANY (1, 2, 3)`은 1보다 큼을 의미합니다.
`>ALL`이 있는 하위 쿼리의 행이 외부 쿼리에 지정된 조건을 만족시키려면 하위 쿼리를 시작하는 열의 값이 하위 쿼리에서 반환되는 값 목록의 모든 값보다 커야 합니다.    

마찬가지로 `>ANY`가 있는 행이 외부 쿼리에 지정된 조건을 만족시키려면 하위 쿼리를 시작하는 열의 값이 하위 쿼리에서 반환되는 값 목록에서 하나 이상의 값보다 커야 합니다.    

다음은 ANY로 수정된 비교 연산자로 시작하는 하위 쿼리를 보여 주는 예입니다. 이 쿼리에서는 가격이 제품 하위 범주의 최대 가격보다 크거나 동일한 제품을 찾습니다.    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >= ANY
    (SELECT MAX (ListPrice)
     FROM Production.Product
     GROUP BY ProductSubcategoryID);
GO
```    

각각의 Product 하위 범주마다 내부 쿼리는 최대 가격을 찾습니다. 외부 쿼리는 이러한 값 모두를 찾고 Product 하위 범주의 최대 가격보다 크거나 동일한 개별 제품의 가격을 확인합니다. `ANY`를 `ALL`로 변경하면 가격이 내부 쿼리에서 반환된 모든 가격보다 크거나 동일한 제품만 반환됩니다.    

하위 쿼리에서 반환된 값이 없으면 전체 쿼리에도 반환 값이 없습니다.    

`=ANY` 연산자는 `IN`에 해당합니다. 예를 들어 `IN` 또는 `=ANY`를 사용하여 Adventure Works Cycles에서 만드는 모든 바퀴 제품의 이름을 찾을 수 있습니다.

```sql
--Using =ANY
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID =ANY
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO

--Using IN
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```

각 쿼리의 결과 집합은 다음과 같습니다.

```
Name
--------------------------------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```    

그러나 `<>ANY` 연산자는 `NOT IN`과 다릅니다. `<>ANY`는 not = a, not = b 또는 not = c를 의미합니다. `NOT IN`은 not = a, not = b 및 not = c를 의미합니다. `<>ALL`은 `NOT IN`과 동일합니다.     

예를 들어 다음 쿼리는 영업 직원이 담당하지 않는 지역에 있는 고객을 찾습니다.     

```sql
USE AdventureWorks2016;
GO
SELECT CustomerID
FROM Sales.Customer
WHERE TerritoryID <> ANY
    (SELECT TerritoryID
     FROM Sales.SalesPerson);
GO
```    

고객에게 할당된 모든 지역을 영업 직원이 담당하기 때문에 결과에는 영업 지역이 NULL인 고객을 제외한 모든 고객이 포함됩니다. 내부 쿼리가 영업 직원의 담당 영업 지역을 모두 찾은 후 외부 쿼리가 각 지역마다 해당 지역에 없는 고객을 찾습니다.    

이와 같은 이유로 이 쿼리에서 `NOT IN`을 사용하면 결과에 아무 고객도 포함되지 않습니다.      

`<>ALL`에 해당하는 `NOT IN` 연산자를 사용해도 동일한 결과를 얻을 수 있습니다.   

### <a name="subqueries-with-exists"></a><a name="exists"></a> EXISTS로 시작하는 하위 쿼리
하위 쿼리가 `EXISTS` 키워드로 시작하면 존재 여부를 테스트할 수 있습니다. 외부 쿼리의 `WHERE` 절은 하위 쿼리에서 반환된 행이 있는지 여부를 테스트합니다. 하위 쿼리는 실제로 데이터를 생성하지 않고 TRUE 또는 FALSE 값을 반환합니다.   

EXISTS로 시작하는 하위 쿼리는 다음 구문을 사용합니다.   

`WHERE [NOT] EXISTS (subquery)`    

다음 쿼리는 Wheels 하위 범주에 있는 모든 제품의 이름을 검색합니다.    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE EXISTS
    (SELECT * 
     FROM Production.ProductSubcategory
     WHERE ProductSubcategoryID = 
            Production.Product.ProductSubcategoryID
        AND Name = 'Wheels');
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]    

```
Name
--------------------------------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```    

각 제품의 이름을 차례로 고려하여 위 쿼리의 결과를 확인합니다. 이 값을 통해 하위 쿼리에서 하나 이상의 행을 반환하는지, 즉 쿼리에서 존재 테스트의 결과가 TRUE인지 확인합니다.   

EXISTS로 시작하는 하위 쿼리는 다음과 같은 점에서 다른 하위 쿼리와 다릅니다. 
-   `EXISTS` 키워드 앞에는 열 이름, 상수, 다른 식이 올 수 없습니다.     
-   `EXISTS`로 시작하는 하위 쿼리의 SELECT 목록은 대부분 별표(*)로 구성됩니다. 하위 쿼리에 지정된 조건을 만족하는 행이 있는지 여부를 테스트하는 것이므로 열 이름은 나열하지 않아도 됩니다.    

대부분 하위 쿼리를 사용하지 않는 대체 구문이 없으므로 `EXISTS` 키워드는 중요합니다. EXISTS를 사용하여 만든 일부 쿼리는 다른 방식으로 표시할 수 없지만 IN을 사용하거나 `ANY` 또는 `ALL`에 의해 수정된 비교 연산자를 사용하여 유사한 결과를 얻을 수 있는 쿼리가 많습니다.     

예를 들어 앞의 쿼리는 IN을 사용하여 다음과 같이 표시할 수 있습니다.   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```   

### <a name="subqueries-with-not-exists"></a><a name="notexists"></a> NOT EXISTS가 있는 하위 쿼리
`NOT EXISTS`는 하위 쿼리에서 반환되는 행이 없을 때 이것이 사용되는 `WHERE` 절이 만족되는 경우를 제외하면 `EXISTS`와 비슷합니다.    

예를 들어 Wheels 하위 범주에 없는 제품 이름을 찾으려면 다음 코드를 사용합니다.   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE NOT EXISTS
    (SELECT * 
     FROM Production.ProductSubcategory
     WHERE ProductSubcategoryID = 
            Production.Product.ProductSubcategoryID
        AND Name = 'Wheels');
GO
```   

### <a name="subqueries-used-in-place-of-an-expression"></a><a name="expression"></a> 식 대신 하위 쿼리 사용
[!INCLUDE[tsql](../../includes/tsql-md.md)]에서 하위 쿼리는 `ORDER BY` 목록을 제외하고 `SELECT`, `UPDATE`, `INSERT` 및 `DELETE` 문에서 식 대신 사용할 수 있습니다.    

다음은 이러한 향상된 기능을 사용하는 방법을 보여 주는 예입니다. 다음 쿼리는 모든 산악용 자전거의 가격, 평균 가격 및 각 산악용 자전거의 가격과 평균 가격 간의 차이를 검색합니다.    

```sql
USE AdventureWorks2016;
GO
SELECT Name, ListPrice, 
(SELECT AVG(ListPrice) FROM Production.Product) AS Average, 
    ListPrice - (SELECT AVG(ListPrice) FROM Production.Product)
    AS Difference
FROM Production.Product
WHERE ProductSubcategoryID = 1;
GO
```   

## <a name="see-also"></a>참고 항목  
[IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)       
[EXISTS &#40;Transact-SQL&#41;](../../t-sql/language-elements/exists-transact-sql.md)     
[ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)     
[SOME | ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)     
[조인](../../relational-databases/performance/joins.md)    
[비교 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)       
  
