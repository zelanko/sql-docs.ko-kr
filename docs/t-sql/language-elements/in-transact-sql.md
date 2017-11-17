---
title: "(Transact SQL)에서 | Microsoft Docs"
ms.custom: 
ms.date: 08/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70b186107966791e29ccb76ea9c310724b76e3b6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="in-transact-sql"></a>IN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정된 값과 일치하는 값이 하위 쿼리 또는 목록 내에 있는지 확인합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
test_expression [ NOT ] IN   
    ( subquery | expression [ ,...n ]  
    )   
```  
  
## <a name="arguments"></a>인수  
 *test_expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)합니다.  
  
 *하위 쿼리*  
 하나의 열로 구성된 결과 집합을 갖는 하위 쿼리입니다. 이 열에 동일한 데이터 형식으로 되어 있어야 *test_expression*합니다.  
  
 *식*[ **,**... *n* ]  
 일치 여부를 검사할 식의 목록입니다. 모든 식은 같은 형식 이어야 합니다 *test_expression*합니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="result-value"></a>결과 값  
 경우의 값 *test_expression* 반환한 모든 값과 같은 *하위 쿼리* 과 일치 하는 또는 *식* 쉼표로 구분 된 목록에서 결과 값은 TRUE입니다. 그렇지 않으면 결과 값은 FALSE입니다.  
  
 NOT IN을 사용 하 여 부정는 *하위 쿼리* 값 또는 *식*합니다.  
  
> [!CAUTION]  
>  Null 값을 반환한 *하위 쿼리* 또는 *식* 비교할는 *test_expression* IN을 사용 하거나에 없는 UNKNOWN을 반환 합니다. IN 또는 NOT IN과 함께 Null 값을 사용하면 예기치 않은 결과가 발생할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 IN 절에는 괄호 안에 매우 많은 수의 값 (수천 개 쉼표로 구분 된 값의)을 명시적으로 포함 리소스가 소비 되 고 오류 8623 또는 8632가 반환 됩니다. 이 문제를 해결 하려면 테이블에서 목록의 항목을 저장 하 고 IN 절 내에서 SELECT 하위 쿼리를 사용 합니다.  
  
 오류 8623:  
  
 `The query processor ran out of internal resources and could not produce a query plan. This is a rare event and only expected for extremely complex queries or queries that reference a very large number of tables or partitions. Please simplify the query. If you believe you have received this message in error, contact Customer Support Services for more information.`  
  
 오류 8632:  
  
 `Internal error: An expression services limit has been reached. Please look for potentially complex expressions in your query, and try to simplify them.`  
  
## <a name="examples"></a>예  
  
### <a name="a-comparing-or-and-in"></a>1. OR와 IN 비교  
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
  
### <a name="b-using-in-with-a-subquery"></a>2. 하위 쿼리와 함께 IN 사용  
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
  
### <a name="c-using-not-in-with-a-subquery"></a>3. 하위 쿼리와 함께 NOT IN 사용  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-in-and-not-in"></a>4. 및에 없는 사용 하 여  
 다음 예제에서 모든 항목을 찾은 `FactInternetSales` 일치 하는 테이블 `SalesReasonKey` 값에 `DimSalesReason` 테이블입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
IN (SELECT SalesReasonKey FROM DimSalesReason);   
```  
  
 다음 예제에서 모든 항목을 찾은 `FactInternetSalesReason` 일치 하지 않는 테이블 `SalesReasonKey` 값에 `DimSalesReason` 테이블입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
NOT IN (SELECT SalesReasonKey FROM DimSalesReason);  
```  
  
### <a name="e-using-in-with-an-expression-list"></a>5. 식 목록을 사용 하 여 사용 하 여  
 다음 예제에서는의 영업 사원에 대 한 모든 Id를 찾습니다는 `DimEmployee` 는 첫 번째 직원 이름 중 하나에 대 한 테이블 `Mike` 또는 `Michael`합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM DimEmployee  
WHERE FirstName IN ('Mike', 'Michael');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [대/소문자 &#40; Transact SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [모든 &#40; Transact SQL &#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [일부 &#124; 모든 &#40; Transact SQL &#41;](../../t-sql/language-elements/some-any-transact-sql.md)  
  
  




