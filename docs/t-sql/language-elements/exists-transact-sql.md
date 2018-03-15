---
title: EXISTS(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
- EXISTS_TSQL
- EXISTS
dev_langs:
- TSQL
helpviewer_keywords:
- existence testing [SQL Server]
- testing existence
- EXISTS keyword
- subqueries [SQL Server], EXISTS keyword
- queries [SQL Server], comparing
- comparing queries
- NOT EXISTS keyword
- row existence testing [SQL Server]
ms.assetid: b6510a65-ac38-4296-a3d5-640db0c27631
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 40abe8ec35a89a51ecfb3d2100ffb47a40c58f23
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="exists-transact-sql"></a>EXISTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  하위 쿼리를 지정하여 행의 존재 여부를 테스트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
EXISTS ( subquery )  
```  
  
## <a name="arguments"></a>인수  
 *subquery*  
 제한된 SELECT 문입니다. INTO 키워드는 허용되지 않습니다. 자세한 내용은 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)에서 하위 쿼리에 대한 내용을 참조하세요.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="result-values"></a>결과 값  
 하위 쿼리에 행이 있으면 TRUE를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-null-in-a-subquery-to-still-return-a-result-set"></a>1. 하위 쿼리에서 NULL을 사용하여 결과 집합 계속 반환  
 다음 예에서는 하위 쿼리에 `NULL`을 지정하여 결과 집합을 반환하고 `EXISTS`를 사용하여 TRUE로 계속 평가됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name   
FROM HumanResources.Department   
WHERE EXISTS (SELECT NULL)  
ORDER BY Name ASC ;  
```  
  
### <a name="b-comparing-queries-by-using-exists-and-in"></a>2. EXISTS 및 IN을 사용하여 쿼리 비교  
 다음 예에서는 기능이 동일한 두 쿼리를 비교합니다. 첫 번째 쿼리에서는 `EXISTS`를 사용하고 두 번째 쿼리에서는 `IN`을 사용합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.FirstName, a.LastName  
FROM Person.Person AS a  
WHERE EXISTS  
(SELECT *   
    FROM HumanResources.Employee AS b  
    WHERE a.BusinessEntityID = b.BusinessEntityID  
    AND a.LastName = 'Johnson');  
GO  
```  
  
 다음 쿼리에서는 `IN`을 사용합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.FirstName, a.LastName  
FROM Person.Person AS a  
WHERE a.LastName IN  
(SELECT a.LastName  
    FROM HumanResources.Employee AS b  
    WHERE a.BusinessEntityID = b.BusinessEntityID  
    AND a.LastName = 'Johnson');  
GO  
```  
  
 각 쿼리의 결과 집합은 다음과 같습니다.  
  
 ```
FirstName                                          LastName
-------------------------------------------------- ----------
Barry                                              Johnson
David                                              Johnson
Willis                                             Johnson
  
(3 row(s) affected)
 ```  
  
### <a name="c-comparing-queries-by-using-exists-and--any"></a>3. EXISTS 및 = ANY를 사용하여 쿼리 비교  
 다음 예에서는 공급업체와 이름이 동일한 상점을 찾는 두 개의 쿼리를 보여 줍니다. 첫 번째 쿼리에서는 `EXISTS`를 사용하고 두 번째 쿼리에서는 `=``ANY`를 사용합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT s.Name  
FROM Sales.Store AS s   
WHERE EXISTS  
(SELECT *  
    FROM Purchasing.Vendor AS v  
    WHERE s.Name = v.Name) ;  
GO  
```  
  
 다음 쿼리에서는 `= ANY`을 사용합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT s.Name  
FROM Sales.Store AS s   
WHERE s.Name = ANY  
(SELECT v.Name  
    FROM Purchasing.Vendor AS v ) ;  
GO  
```  
  
### <a name="d-comparing-queries-by-using-exists-and-in"></a>4. EXISTS 및 IN을 사용하여 쿼리 비교  
 다음 예에서는 `P`로 시작되는 부서의 직원을 찾는 쿼리를 보여 줍니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p   
JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID   
WHERE EXISTS  
(SELECT *  
    FROM HumanResources.Department AS d  
    JOIN HumanResources.EmployeeDepartmentHistory AS edh  
       ON d.DepartmentID = edh.DepartmentID  
    WHERE e.BusinessEntityID = edh.BusinessEntityID  
    AND d.Name LIKE 'P%');  
GO  
```  
  
 다음 쿼리에서는 `IN`을 사용합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID   
JOIN HumanResources.EmployeeDepartmentHistory AS edh  
   ON e.BusinessEntityID = edh.BusinessEntityID   
WHERE edh.DepartmentID IN  
(SELECT DepartmentID  
   FROM HumanResources.Department  
   WHERE Name LIKE 'P%');  
GO  
```  
  
### <a name="e-using-not-exists"></a>5. NOT EXISTS 사용  
 NOT EXISTS는 EXISTS와 반대됩니다. 하위 쿼리에서 반환되는 행이 없는 경우에는 NOT EXISTS의 WHERE 절 조건이 충족됩니다. 다음 예에서는 이름이 `P`로 시작되는 부서에 속하지 않는 직원을 찾습니다.  
  
```  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p   
JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID   
WHERE NOT EXISTS  
(SELECT *  
   FROM HumanResources.Department AS d  
   JOIN HumanResources.EmployeeDepartmentHistory AS edh  
      ON d.DepartmentID = edh.DepartmentID  
   WHERE e.BusinessEntityID = edh.BusinessEntityID  
   AND d.Name LIKE 'P%')  
ORDER BY LastName, FirstName  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FirstName                      LastName                       Title
------------------------------ ------------------------------ ------------
Syed                           Abbas                          Pacific Sales Manager
Hazem                          Abolrous                       Quality Assurance Manager
Humberto                       Acevedo                        Application Specialist
Pilar                          Ackerman                       Shipping & Receiving Superviso
François                       Ajenstat                       Database Administrator
Amy                            Alberts                        European Sales Manager
Sean                           Alexander                      Quality Assurance Technician
Pamela                         Ansman-Wolfe                   Sales Representative
Zainal                         Arifin                         Document Control Manager
David                          Barber                         Assistant to CFO
Paula                          Barreto de Mattos              Human Resources Manager
Shai                           Bassli                         Facilities Manager
Wanida                         Benshoof                       Marketing Assistant
Karen                          Berg                           Application Specialist
Karen                          Berge                          Document Control Assistant
Andreas                        Berglund                       Quality Assurance Technician
Matthias                       Berndt                         Shipping & Receiving Clerk
Jo                             Berry                          Janitor
Jimmy                          Bischoff                       Stocker
Michael                        Blythe                         Sales Representative
David                          Bradley                        Marketing Manager
Kevin                          Brown                          Marketing Assistant
David                          Campbell                       Sales Representative
Jason                          Carlson                        Information Services Manager
Fernando                       Caro                           Sales Representative
Sean                           Chai                           Document Control Assistant
Sootha                         Charncherngkha                 Quality Assurance Technician
Hao                            Chen                           HR Administrative Assistant
Kevin                          Chrisulis                      Network Administrator
Pat                            Coleman                        Janitor
Stephanie                      Conroy                         Network Manager
Debra                          Core                           Application Specialist
Ovidiu                         Crãcium                        Sr. Tool Designer
Grant                          Culbertson                     HR Administrative Assistant
Mary                           Dempsey                        Marketing Assistant
Thierry                        D'Hers                         Tool Designer
Terri                          Duffy                          VP Engineering
Susan                          Eaton                          Stocker
Terry                          Eminhizer                      Marketing Specialist
Gail                           Erickson                       Design Engineer
Janice                         Galvin                         Tool Designer
Mary                           Gibson                         Marketing Specialist
Jossef                         Goldberg                       Design Engineer
Sariya                         Harnpadoungsataya              Marketing Specialist
Mark                           Harrington                     Quality Assurance Technician
Magnus                         Hedlund                        Facilities Assistant
Shu                            Ito                            Sales Representative
Stephen                        Jiang                          North American Sales Manager
Willis                         Johnson                        Recruiter
Brannon                        Jones                          Finance Manager
Tengiz                         Kharatishvili                  Control Specialist
Christian                      Kleinerman                     Maintenance Supervisor
Vamsi                          Kuppa                          Shipping & Receiving Clerk
David                          Liu                            Accounts Manager
Vidur                          Luthra                         Recruiter
Stuart                         Macrae                         Janitor
Diane                          Margheim                       Research & Development Enginee
Mindy                          Martin                         Benefits Specialist
Gigi                           Matthew                        Research & Development Enginee
Tete                           Mensa-Annan                    Sales Representative
Ramesh                         Meyyappan                      Application Specialist
Dylan                          Miller                         Research & Development Manager
Linda                          Mitchell                       Sales Representative
Barbara                        Moreland                       Accountant
Laura                          Norman                         Chief Financial Officer
Chris                          Norred                         Control Specialist
Jae                            Pak                            Sales Representative
Wanda                          Parks                          Janitor
Deborah                        Poe                            Accounts Receivable Specialist
Kim                            Ralls                          Stocker
Tsvi                           Reiter                         Sales Representative
Sharon                         Salavaria                      Design Engineer
Ken                            Sanchez                        Chief Executive Officer
José                           Saraiva                        Sales Representative
Mike                           Seamans                        Accountant
Ashvini                        Sharma                         Network Administrator
Janet                          Sheperdigian                   Accounts Payable Specialist
Candy                          Spoon                          Accounts Receivable Specialist
Michael                        Sullivan                       Sr. Design Engineer
Dragan                         Tomic                          Accounts Payable Specialist
Lynn                           Tsoflias                       Sales Representative
Rachel                         Valdez                         Sales Representative
Garrett                        Vargar                         Sales Representative
Ranjit                         Varkey Chudukatil              Sales Representative
Bryan                          Walton                         Accounts Receivable Specialist
Jian Shuo                      Wang                           Engineering Manager
Brian                          Welcker                        VP Sales
Jill                           Williams                       Marketing Specialist
Dan                            Wilson                         Database Administrator
John                           Wood                           Marketing Specialist
Peng                           Wu                             Quality Assurance Supervisor
  
(91 row(s) affected)
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-using-exists"></a>6. EXISTS 사용  
 다음 예제에서는 `ProspectiveBuyer` 테이블의 행이 `DimCustomer` 테이블의 행과 일치하는지 여부를 식별합니다. 쿼리는 두 테이블의 `LastName` 및 `BirthDate` 값이 모두 일치하는 경우에만 행을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.LastName, a.BirthDate  
FROM DimCustomer AS a  
WHERE EXISTS  
(SELECT *   
    FROM dbo.ProspectiveBuyer AS b  
    WHERE (a.LastName = b.LastName) AND (a.BirthDate = b.BirthDate));  
```  
  
### <a name="g-using-not-exists"></a>7. NOT EXISTS 사용  
 NOT EXISTS는 EXISTS와 반대됩니다. 하위 쿼리에서 반환되는 행이 없는 경우에는 NOT EXISTS의 WHERE 절 조건이 충족됩니다. 다음 예제에서는 `LastName` 및 `BirthDate`가 `ProspectiveBuyers` 테이블의 모든 항목에 일치하지 않는 행을 `DimCustomer` 테이블에서 찾습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.LastName, a.BirthDate  
FROM DimCustomer AS a  
WHERE NOT EXISTS  
(SELECT *   
    FROM dbo.ProspectiveBuyer AS b  
    WHERE (a.LastName = b.LastName) AND (a.BirthDate = b.BirthDate));  
```  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


