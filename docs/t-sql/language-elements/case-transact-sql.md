---
title: "대/소문자 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CASE_TSQL
- CASE
dev_langs:
- TSQL
helpviewer_keywords:
- CASE expression [Transact-SQL]
- simple CASE expression
- comparing expressions
- searched CASE expression
ms.assetid: 658039ec-8dc2-4251-bc82-30ea23708cee
caps.latest.revision: 59
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b366f7b6d57adbed5f028171617abb7516f3260b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="case-transact-sql"></a>CASE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  조건 목록을 평가하고 가능한 여러 결과 식 중 하나를 반환합니다.  
  
 CASE 식에는 두 가지 형식이 있습니다.  
  
-   단순 CASE 식은 특정 식을 일련의 단순 식과 비교하여 결과를 결정합니다.  
  
-   검색된 CASE 식은 일련의 부울 식을 평가하여 결과를 결정합니다.  
  
 두 가지 형식 모두 선택 사항인 ELSE 인수를 지원합니다.  
  
 CASE는 유효한 식이 허용되는 모든 문 및 절에 사용할 수 있습니다. 예를 들어 SELECT, UPDATE, DELETE 및 SET과 같은 문과 select_list, IN, WHERE, ORDER BY 및 HAVING과 같은 절에 CASE를 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
Simple CASE expression:   
CASE input_expression   
     WHEN when_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END   
Searched CASE expression:  
CASE  
     WHEN Boolean_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CASE  
     WHEN when_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END  
```  
  
## <a name="arguments"></a>인수  
 *input_expression*  
 단순 CASE 형식을 사용할 때 평가되는 식입니다. *input_expression* 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)합니다.  
  
 때 *when_expression*  
 에 단순 식 *input_expression* 단순 CASE 형식을 사용할 때를 비교 합니다. *when_expression* 유효한 식입니다. 데이터 형식이 *input_expression* 및 각 *when_expression* 동일 하거나 암시적으로 변환 되어야 합니다.  
  
 그런 다음 *result_expression*  
 이 식을 반환 *input_expression* equals *when_expression* TRUE로 평가 또는 *Boolean_expression* TRUE로 평가 합니다. *결과 식을* 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)합니다.  
  
 ELSE *else_result_expression*  
 TRUE로 평가된 비교 연산이 없을 때 반환되는 식입니다. 이 인수가 생략되고 TRUE로 평가된 비교 연산이 없는 경우 CASE는 NULL을 반환합니다. *else_result_expression* 유효한 식입니다. 데이터 형식이 *else_result_expression* 임의의 *result_expression* 동일 하거나 암시적으로 변환 되어야 합니다.  
  
 때 *Boolean_expression*  
 검색된 CASE 형식을 사용할 때 평가되는 부울 식입니다. *Boolean_expression* 은 유효한 부울 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 형식 집합에서 우선 순위가 가장 높은 형식을 반환 *result_expressions* 과 선택적 요소인 *else_result_expression*합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
### <a name="return-values"></a>반환 값  
 **단순 CASE 식:**  
  
 단순 CASE 식은 첫 번째 식이 각 WHEN 절의 식과 같은지 비교하는 방식으로 작동합니다. 이러한 식이 같으면 THEN 절의 식이 반환됩니다.  
  
-   동등성만 검사합니다.  
  
-   평가 input_expression 지정한 순서 대로 각 WHEN 절에 대 한 when_expression = 합니다.  
  
-   반환 된 *result_expression* 첫 번째 *input_expression* = *when_expression* TRUE로 계산 되는 합니다.  
  
-   없는 경우 *input_expression* = *when_expression* TRUE로 평가 된 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 반환는 *else_result_expression* ELSE 절이 지정 된, 또는 ELSE 절 없이 지정 된 경우 NULL 값입니다.  
  
 **검색 된 CASE 식:**  
  
-   계산 되 면, 지정 된 순서로 *Boolean_expression* 각 WHEN 절에 대 한 합니다.  
  
-   반환 *result_expression* 첫 번째 *Boolean_expression* TRUE로 계산 되는 합니다.  
  
-   없는 경우 *Boolean_expression* TRUE로 평가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 반환는 *else_result_expression* 는 ELSE 절이 지정 하는 경우 또는 ELSE 절 없이 지정 된 경우 NULL 값입니다.  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CASE 식의 중첩을 10개 수준까지만 허용합니다.  
  
 Transact-SQL 문, 문 블록, 사용자 정의 함수 및 저장 프로시저의 실행 흐름을 제어하는 데 CASE 식을 사용할 수는 없습니다. 흐름 제어 메서드의 목록을 참조 하십시오. [흐름 제어 언어 &#40; Transact SQL &#41; ](~/t-sql/language-elements/control-of-flow.md).  
  
 CASE 문은 해당 조건을 순서대로 평가하고 충족되는 첫 번째 조건에서 중지합니다. CASE 문이 식 결과를 입력으로 받기 전에 식이 계산되는 경우도 있습니다. 이러한 식을 계산하는 동안 오류가 발생할 수 있습니다. CASE 문의 WHEN 인수에 나타나는 집계 식이 먼저 계산된 다음 CASE 문에 제공됩니다. 예를 들어, 다음 쿼리는 MAX 집계 값을 생성할 때 0으로 나누기 오류를 생성합니다. 이는 CASE 식을 계산하기 전에 발생합니다.  
  
```tsql  
WITH Data (value) AS   
(   
SELECT 0   
UNION ALL   
SELECT 1   
)   
SELECT   
   CASE   
      WHEN MIN(value) <= 0 THEN 0   
      WHEN MAX(1/value) >= 100 THEN 1   
   END   
FROM Data ;  
```  
  
 집계 식이 아닌 스칼라 식(스칼라를 반환하는 상호 관련되지 않은 하위 쿼리)의 경우 WHEN 조건의 평가 순서만 사용해야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-a-select-statement-with-a-simple-case-expression"></a>1. SELECT 문에 단순 CASE 식 사용  
 `SELECT` 문 내에서 단순 `CASE` 식은 동등성만 검사하고 다른 비교 작업은 수행할 수 없습니다. 다음 예에서는 `CASE` 식을 사용하여 제품 라인 범주 표시를 이해하기 쉽게 변경합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductNumber, Category =  
      CASE ProductLine  
         WHEN 'R' THEN 'Road'  
         WHEN 'M' THEN 'Mountain'  
         WHEN 'T' THEN 'Touring'  
         WHEN 'S' THEN 'Other sale items'  
         ELSE 'Not for sale'  
      END,  
   Name  
FROM Production.Product  
ORDER BY ProductNumber;  
GO  
  
```  
  
### <a name="b-using-a-select-statement-with-a-searched-case-expression"></a>2. SELECT 문에 검색된 CASE 식 사용  
 `SELECT` 문 내에서 검색된 `CASE` 식은 비교 값에 따라 결과 집합의 값이 바뀌도록 합니다. 다음 예에서는 제품의 가격 범위에 따라 가격을 텍스트 설명으로 표시합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductNumber, Name, "Price Range" =   
      CASE   
         WHEN ListPrice =  0 THEN 'Mfg item - not for resale'  
         WHEN ListPrice < 50 THEN 'Under $50'  
         WHEN ListPrice >= 50 and ListPrice < 250 THEN 'Under $250'  
         WHEN ListPrice >= 250 and ListPrice < 1000 THEN 'Under $1000'  
         ELSE 'Over $1000'  
      END  
FROM Production.Product  
ORDER BY ProductNumber ;  
GO  
  
```  
  
### <a name="c-using-case-in-an-order-by-clause"></a>3. ORDER BY 절에 CASE 사용  
 다음 예에서는 ORDER BY 절에 CASE 식을 사용하여 지정된 열 값에 따라 행의 정렬 순서를 결정합니다. 첫 번째 예에서는 `SalariedFlag` 테이블의 `HumanResources.Employee` 열의 값이 계산됩니다. `SalariedFlag`가 1로 설정된 직원은 `BusinessEntityID` 순서에 따라 내림차순으로 반환됩니다. `SalariedFlag`가 0으로 설정된 직원은 `BusinessEntityID` 순서에 따라 오름차순으로 반환됩니다. 두 번째 예에서 결과 집합은 `TerritoryName` 열이 'United States'와 동일하면 `CountryRegionName` 열을 기준으로 정렬되고 그 외 다른 행에는 `CountryRegionName` 열을 기준으로 정렬됩니다.  
  
```  
SELECT BusinessEntityID, SalariedFlag  
FROM HumanResources.Employee  
ORDER BY CASE SalariedFlag WHEN 1 THEN BusinessEntityID END DESC  
        ,CASE WHEN SalariedFlag = 0 THEN BusinessEntityID END;  
GO  
  
```  
  
```  
SELECT BusinessEntityID, LastName, TerritoryName, CountryRegionName  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL  
ORDER BY CASE CountryRegionName WHEN 'United States' THEN TerritoryName  
         ELSE CountryRegionName END;  
  
```  
  
### <a name="d-using-case-in-an-update-statement"></a>4. UPDATE 문에 CASE 사용  
 다음 예에서는 UPDATE 문에 CASE 식을 사용하여 `VacationHours`가 0으로 설정된 직원의 열 `SalariedFlag`에 설정된 값을 확인합니다. `VacationHours`에서 10시간을 뺀 결과 음수 값이 되면 `VacationHours`가 40시간 증가되고, 그렇지 않으면 `VacationHours`가 20시간 증가됩니다. OUTPUT 절은 휴가의 이전 값과 이후 값을 표시하는 데 사용됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN ((VacationHours - 10.00) < 0) THEN VacationHours + 40  
         ELSE (VacationHours + 20.00)  
       END  
    )  
OUTPUT Deleted.BusinessEntityID, Deleted.VacationHours AS BeforeValue,   
       Inserted.VacationHours AS AfterValue  
WHERE SalariedFlag = 0;  
  
```  
  
### <a name="e-using-case-in-a-set-statement"></a>5. SET 문에 CASE 사용  
 다음 예에서는 테이블 반환 함수 `dbo.GetContactInfo`에서 SET 문에 CASE 식을 사용합니다. 에 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 사용자에 게 관련 된 모든 데이터에 저장 되는 `Person.Person` 테이블입니다. 예를 들어 직원, 공급 업체 담당자 또는 고객의 사람이 있을 수 있습니다. 함수 반환의 성과 이름은 주어진 `BusinessEntityID` 및 해당 사용자에 대 한 연락처 유형. 열에 대해 표시할 값을 결정 하는 SET 문에 CASE 식을 `ContactType` 의 존재 여부에 따라는 `BusinessEntityID` 열에는 `Employee`, `Vendor`, 또는 `Customer` 테이블입니다.  
  
```  
  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.GetContactInformation(@BusinessEntityID int)  
    RETURNS @retContactInformation TABLE   
(  
BusinessEntityID int NOT NULL,  
FirstName nvarchar(50) NULL,  
LastName nvarchar(50) NULL,  
ContactType nvarchar(50) NULL,  
    PRIMARY KEY CLUSTERED (BusinessEntityID ASC)  
)   
AS   
-- Returns the first name, last name and contact type for the specified contact.  
BEGIN  
    DECLARE   
        @FirstName nvarchar(50),   
        @LastName nvarchar(50),   
        @ContactType nvarchar(50);  
  
    -- Get common contact information  
    SELECT   
        @BusinessEntityID = BusinessEntityID,   
@FirstName = FirstName,   
        @LastName = LastName  
    FROM Person.Person   
    WHERE BusinessEntityID = @BusinessEntityID;  
  
    SET @ContactType =   
        CASE   
            -- Check for employee  
            WHEN EXISTS(SELECT * FROM HumanResources.Employee AS e   
                WHERE e.BusinessEntityID = @BusinessEntityID)   
                THEN 'Employee'  
  
            -- Check for vendor  
            WHEN EXISTS(SELECT * FROM Person.BusinessEntityContact AS bec  
                WHERE bec.BusinessEntityID = @BusinessEntityID)   
                THEN 'Vendor'  
  
            -- Check for store  
            WHEN EXISTS(SELECT * FROM Purchasing.Vendor AS v            
                WHERE v.BusinessEntityID = @BusinessEntityID)   
                THEN 'Store Contact'  
  
            -- Check for individual consumer  
            WHEN EXISTS(SELECT * FROM Sales.Customer AS c   
                WHERE c.PersonID = @BusinessEntityID)   
                THEN 'Consumer'  
        END;  
  
    -- Return the information to the caller  
    IF @BusinessEntityID IS NOT NULL   
    BEGIN  
        INSERT @retContactInformation  
        SELECT @BusinessEntityID, @FirstName, @LastName, @ContactType;  
    END;  
  
    RETURN;  
END;  
GO  
  
SELECT BusinessEntityID, FirstName, LastName, ContactType  
FROM dbo.GetContactInformation(2200);  
GO  
SELECT BusinessEntityID, FirstName, LastName, ContactType  
FROM dbo.GetContactInformation(5);  
  
```  
  
### <a name="f-using-case-in-a-having-clause"></a>6. HAVING 절에 CASE 사용  
 다음 예에서는 HAVING 절에 CASE 식을 사용하여 SELECT 문에서 반환하는 행을 제한합니다. 각 직함에 대 한 최대 시간당 급여를 반환 하는 명령문의 `HumanResources.Employee` 테이블입니다. HAVING 절은 직함을 최대 급여가 40달러가 넘는 남자 직원의 직함 또는 최대 급여가 42달러가 넘는 여자 직원의 직함으로 제한합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT JobTitle, MAX(ph1.Rate)AS MaximumRate  
FROM HumanResources.Employee AS e  
JOIN HumanResources.EmployeePayHistory AS ph1 ON e.BusinessEntityID = ph1.BusinessEntityID  
GROUP BY JobTitle  
HAVING (MAX(CASE WHEN Gender = 'M'   
        THEN ph1.Rate   
        ELSE NULL END) > 40.00  
     OR MAX(CASE WHEN Gender  = 'F'   
        THEN ph1.Rate    
        ELSE NULL END) > 42.00)  
ORDER BY MaximumRate DESC;  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="g-using-a-select-statement-with-a-case-expression"></a>7. SELECT 문에 CASE 식 사용  
 SELECT 문 내에서 CASE 식은 비교 값을 기반으로 결과 집합에서 바뀔 값을 허용 합니다. 다음 예제에서는 이해 하면 제품 라인 범주 표시를 변경 하는 CASE 식을 사용 합니다. 값이 존재 하지 않는 경우, 텍스트 "판매에 대해 ' 표시 됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT   ProductAlternateKey, Category =  
      CASE ProductLine  
         WHEN 'R' THEN 'Road'  
         WHEN 'M' THEN 'Mountain'  
         WHEN 'T' THEN 'Touring'  
         WHEN 'S' THEN 'Other sale items'  
         ELSE 'Not for sale'  
      END,  
   EnglishProductName  
FROM dbo.DimProduct  
ORDER BY ProductKey;  
```  
  
### <a name="h-using-case-in-an-update-statement"></a>8. UPDATE 문에 CASE 사용  
 다음 예에서는 UPDATE 문에 CASE 식을 사용하여 `VacationHours`가 0으로 설정된 직원의 열 `SalariedFlag`에 설정된 값을 확인합니다. `VacationHours`에서 10시간을 뺀 결과 음수 값이 되면 `VacationHours`가 40시간 증가되고, 그렇지 않으면 `VacationHours`가 20시간 증가됩니다.  
  
```  
-- Uses AdventureWorks   
  
UPDATE dbo.DimEmployee  
SET VacationHours =   
    ( CASE  
         WHEN ((VacationHours - 10.00) < 0) THEN VacationHours + 40  
         ELSE (VacationHours + 20.00)   
       END  
    )   
WHERE SalariedFlag = 0;  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [COALESCE &#40; Transact SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)   
 [IIF &#40; Transact SQL &#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)   
 [선택 &#40; Transact SQL &#41;](../../t-sql/functions/logical-functions-choose-transact-sql.md)  
  
  




