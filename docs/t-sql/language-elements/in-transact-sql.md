---
title: IN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IN_TSQL
- IN
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], matching
- NOT IN keyword
- 8623 (Database Engine error)
- matching values in subquery or list [SQL Server]
- IN keyword
- 8632 (Database Engine error)
ms.assetid: 4419de73-96b1-4dfe-8500-f4507915db04
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 99d179218e52801da593eaba6ef9ff5c7dde5ee0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68075058"
---
# <a name="in-transact-sql"></a>IN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정된 값과 일치하는 값이 하위 쿼리 또는 목록 내에 있는지 확인합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
test_expression [ NOT ] IN   
    ( subquery | expression [ ,...n ]  
    )   
```  
  
## <a name="arguments"></a>인수  
 *test_expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
 *subquery*  
 하나의 열로 구성된 결과 집합을 갖는 하위 쿼리입니다. 이 열은 *test_expression*과 데이터 형식이 같아야 합니다.  
  
 *expression*[ **,** ... *n* ]  
 일치 여부를 검사할 식의 목록입니다. 모든 식은 *test_expression*과 형식이 같아야 합니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="result-value"></a>결과 값  
 *test_expression*의 값이 *subquery*에서 반환된 값과 일치하거나 쉼표로 구분된 목록의 *식*과 일치하는 경우 결과 값은 TRUE입니다. 그렇지 않으면 결과 값은 FALSE입니다.  
  
 NOT IN을 사용하면 *하위 쿼리* 값 또는 *식*을 부정합니다.  
  
> [!CAUTION]  
>  IN 또는 NOT IN을 사용한 *test_expression*과 비교하여 *subquery* 또는 *expression*에서 반환되는 Null 값은 UNKNOWN을 반환합니다. IN 또는 NOT IN과 함께 Null 값을 사용하면 예기치 않은 결과가 발생할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 IN 절에서 괄호 안에 너무 많은 값(콤마로 구분된 수천 개의 값)을 명시적으로 포함하면 리소스가 소비되고 오류 8623 또는 8632가 반환됩니다. 이 문제를 해결하려면 IN 목록의 항목을 테이블에 저장하고, IN 절 내에서 SELECT 하위 쿼리를 사용합니다.  
  
 오류 8623:  
  
 `The query processor ran out of internal resources and could not produce a query plan. This is a rare event and only expected for extremely complex queries or queries that reference a very large number of tables or partitions. Please simplify the query. If you believe you have received this message in error, contact Customer Support Services for more information.`  
  
 오류 8632:  
  
 `Internal error: An expression services limit has been reached. Please look for potentially complex expressions in your query, and try to simplify them.`  
  
## <a name="examples"></a>예  
  
### <a name="a-comparing-or-and-in"></a>A. OR와 IN 비교  
 다음 예에서는 디자인 엔지니어, 툴 엔지니어 또는 마케팅 지원 담당 직원들의 이름 목록을 선택합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle = 'Design Engineer'   
   OR e.JobTitle = 'Tool Designer'   
   OR e.JobTitle = 'Marketing Assistant';  
GO  
```  
  
 IN을 사용해도 동일한 결과를 얻을 수 있습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle IN ('Design Engineer', 'Tool Designer', 'Marketing Assistant');  
GO  
```  
  
 두 쿼리의 결과 집합은 다음과 같습니다.  
  
```  
FirstName   LastName      Title  
---------   ---------   ---------------------  
Sharon      Salavaria   Design Engineer                                     
Gail        Erickson    Design Engineer                                     
Jossef      Goldberg    Design Engineer                                     
Janice      Galvin      Tool Designer                                       
Thierry     D'Hers      Tool Designer                                       
Wanida      Benshoof    Marketing Assistant                                 
Kevin       Brown       Marketing Assistant                                 
Mary        Dempsey     Marketing Assistant                                 
  
(8 row(s) affected)  
```  
  
### <a name="b-using-in-with-a-subquery"></a>B. 하위 쿼리와 함께 IN 사용  
 다음 예에서는 `SalesPerson` 테이블에서 연간 판매 할당량이 $250,000 이상인 모든 직원들의 ID를 찾은 다음 `Employee` 테이블에서 `EmployeeID`가 `SELECT` 하위 쿼리의 결과와 일치하는 모든 직원들의 이름을 선택합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
FirstName   LastName                                             
---------   --------   
Tsvi         Reiter                                              
Michael      Blythe                                              
Tete         Mensa-Annan                                         
  
(3 row(s) affected)  
```  
  
### <a name="c-using-not-in-with-a-subquery"></a>C. 하위 쿼리와 함께 NOT IN 사용  
 다음 예에서는 할당량이 $250,000 이하인 영업 사원을 찾습니다. `NOT IN`은 값 목록의 항목과 일치하지 않는 영업 사원을 찾습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID NOT IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-in-and-not-in"></a>D. IN 및 NOT IN 사용  
 다음 예제에서는 `DimSalesReason` 테이블의 `SalesReasonKey` 값에 일치하는 모든 항목을 `FactInternetSales` 테이블에서 찾습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
IN (SELECT SalesReasonKey FROM DimSalesReason);   
```  
  
 다음 예제에서는 `DimSalesReason` 테이블의 `SalesReasonKey` 값에 일치하지 않는 모든 항목을 `FactInternetSalesReason` 테이블에서 찾습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
NOT IN (SELECT SalesReasonKey FROM DimSalesReason);  
```  
  
### <a name="e-using-in-with-an-expression-list"></a>E. 식 목록과 함께 IN 사용  
 다음 예제에서는 이름이 `Mike` 또는 `Michael`인 직원을 위한 `DimEmployee` 테이블에서 영업 사원의 모든 ID를 찾습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM DimEmployee  
WHERE FirstName IN ('Mike', 'Michael');  
```  
  
## <a name="see-also"></a>참고 항목  
 [CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [SOME &#124; ANY&#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)  
  
  



