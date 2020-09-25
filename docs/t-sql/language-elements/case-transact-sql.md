---
title: CASE(Transact-SQL)
description: CASE 식의 Transact-SQL 참조입니다. CASE는 조건 목록을 평가하여 특정 결과를 반환합니다.
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: be188a87a06a91467a16862ea0a0d572e4f71b93
ms.sourcegitcommit: 8f062015c2a033f5a0d805ee4adabbe15e7c8f94
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91227413"
---
# <a name="case-transact-sql"></a>CASE(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

조건 목록을 평가하고 가능한 여러 결과 식 중 하나를 반환합니다.  
  
 CASE 식에는 두 가지 형식이 있습니다.  
  
-   단순 CASE 식은 특정 식을 일련의 단순 식과 비교하여 결과를 결정합니다.  
  
-   검색된 CASE 식은 일련의 부울 식을 평가하여 결과를 결정합니다.  
  
 두 가지 형식 모두 선택 사항인 ELSE 인수를 지원합니다.  
  
 CASE는 유효한 식이 허용되는 모든 문 및 절에 사용할 수 있습니다. 예를 들어 SELECT, UPDATE, DELETE 및 SET과 같은 문과 select_list, IN, WHERE, ORDER BY 및 HAVING과 같은 절에 CASE를 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
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
  
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
CASE  
     WHEN when_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수  
 *input_expression*  
 단순 CASE 형식을 사용할 때 평가되는 식입니다. *input_expression*은 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
 WHEN *when_expression*  
 단순 CASE 형식을 사용할 때 *input_expression*과 비교되는 단순 식입니다. *when_expression*은 유효한 식입니다. *input_expression* 및 각 *when_expression*의 데이터 형식은 동일하거나 암시적으로 변환되어야 합니다.  
  
 THEN *result_expression*  
 *input_expression*과 *when_expression*이 같다는 것이 TRUE로 평가되거나 *Boolean_expression*이 TRUE로 평가될 때 반환되는 식입니다. *result_expression*은 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
 ELSE *else_result_expression*  
 TRUE로 평가된 비교 연산이 없을 때 반환되는 식입니다. 이 인수가 생략되고 TRUE로 평가된 비교 연산이 없는 경우 CASE는 NULL을 반환합니다. *else_result_expression*은 유효한 식입니다. *else_result_expression* 및 임의의 *result_expression*의 데이터 형식은 동일하거나 암시적으로 변환되어야 합니다.  
  
 WHEN *Boolean_expression*  
 검색된 CASE 형식을 사용할 때 평가되는 부울 식입니다. *Boolean_expression*는 유효한 부울 식입니다.  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 *result_expressions* 및 선택적 *else_result_expression*의 형식 집합에서 우선 순위가 가장 높은 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
### <a name="return-values"></a>반환 값  
 **단순 CASE 식:**  
  
 단순 CASE 식은 첫 번째 식이 각 WHEN 절의 식과 같은지 비교하는 방식으로 작동합니다. 이러한 식이 같으면 THEN 절의 식이 반환됩니다.  
  
-   동등성만 검사합니다.  
  
-   지정된 순서대로 각 WHEN 절에 대해 input_expression = when_expression을 평가합니다.  
  
-   TRUE로 평가되는 첫 번째 *input_expression* = *when_expression*의 *result_expression*을 반환합니다.  
  
-   *input_expression* = *when_expression*이 TRUE로 평가되지 않은 경우, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 ELSE 절이 지정되어 있으면 *else_result_expression*을 반환하고, ELSE 절이 지정되어 있지 않으면 NULL 값을 반환합니다.  
  
 **검색된 CASE 식:**  
  
-   지정된 순서대로 각 WHEN 절에 대해 *Boolean_expression*을 평가합니다.  
  
-   TRUE로 평가되는 첫 번째 *Boolean_expression*의 *result_expression*을 반환합니다.  
  
-   *Boolean_expression*이 TRUE로 평가되지 않은 경우, [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 ELSE 절이 지정되어 있으면 *else_result_expression*을 반환하고, ELSE 절이 지정되어 있지 않으면 NULL 값을 반환합니다.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CASE 식의 중첩을 10개 수준까지만 허용합니다.  
  
 Transact-SQL 문, 문 블록, 사용자 정의 함수 및 저장 프로시저의 실행 흐름을 제어하는 데 CASE 식을 사용할 수는 없습니다. 흐름 제어 메서드의 목록은 [흐름 제어 언어&#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)를 참조하세요.  
  
 CASE 식은 해당 조건을 순서대로 평가하고 충족되는 첫 번째 조건에서 중지합니다. CASE 식이 식의 결과를 입력으로 받기 전에 식이 계산되는 경우도 있습니다. 이러한 식을 계산하는 동안 오류가 발생할 수 있습니다. CASE 식의 WHEN 인수에 나타나는 집계 식이 먼저 계산된 다음, CASE 식에 제공됩니다. 예를 들어, 다음 쿼리는 MAX 집계 값을 생성할 때 0으로 나누기 오류를 생성합니다. 이는 CASE 식을 계산하기 전에 발생합니다.  
  
```sql  
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
  
### <a name="a-using-a-select-statement-with-a-simple-case-expression"></a>A. SELECT 문에 단순 CASE 식 사용  
 `SELECT` 문 내에서 단순 `CASE` 식은 동등성만 검사하고 다른 비교 작업은 수행할 수 없습니다. 다음 예에서는 `CASE` 식을 사용하여 제품 라인 범주 표시를 이해하기 쉽게 변경합니다.  
  
```sql  
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
  
### <a name="b-using-a-select-statement-with-a-searched-case-expression"></a>B. SELECT 문에 검색된 CASE 식 사용  
 `SELECT` 문 내에서 검색된 `CASE` 식은 비교 값에 따라 결과 집합의 값이 바뀌도록 합니다. 다음 예에서는 제품의 가격 범위에 따라 가격을 텍스트 설명으로 표시합니다.  
  
```sql  
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
  
### <a name="c-using-case-in-an-order-by-clause"></a>C. ORDER BY 절에 CASE 사용  
 다음 예에서는 ORDER BY 절에 CASE 식을 사용하여 지정된 열 값에 따라 행의 정렬 순서를 결정합니다. 첫 번째 예에서는 `SalariedFlag` 테이블의 `HumanResources.Employee` 열의 값이 계산됩니다. `SalariedFlag`가 1로 설정된 직원은 `BusinessEntityID` 순서에 따라 내림차순으로 반환됩니다. `SalariedFlag`가 0으로 설정된 직원은 `BusinessEntityID` 순서에 따라 오름차순으로 반환됩니다. 두 번째 예에서 결과 집합은 `TerritoryName` 열이 'United States'와 동일하면 `CountryRegionName` 열을 기준으로 정렬되고 그 외 다른 행에는 `CountryRegionName` 열을 기준으로 정렬됩니다.  
  
```sql  
SELECT BusinessEntityID, SalariedFlag  
FROM HumanResources.Employee  
ORDER BY CASE SalariedFlag WHEN 1 THEN BusinessEntityID END DESC  
        ,CASE WHEN SalariedFlag = 0 THEN BusinessEntityID END;  
GO    
```  
  
```sql  
SELECT BusinessEntityID, LastName, TerritoryName, CountryRegionName  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL  
ORDER BY CASE CountryRegionName WHEN 'United States' THEN TerritoryName  
         ELSE CountryRegionName END; 
```  
  
### <a name="d-using-case-in-an-update-statement"></a>D. UPDATE 문에 CASE 사용  
 다음 예에서는 UPDATE 문에 CASE 식을 사용하여 `VacationHours`가 0으로 설정된 직원의 열 `SalariedFlag`에 설정된 값을 확인합니다. `VacationHours`에서 10시간을 뺀 결과 음수 값이 되면 `VacationHours`가 40시간 증가되고, 그렇지 않으면 `VacationHours`가 20시간 증가됩니다. OUTPUT 절은 휴가의 이전 값과 이후 값을 표시하는 데 사용됩니다.  
  
```sql  
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
  
### <a name="e-using-case-in-a-set-statement"></a>E. SET 문에 CASE 사용  
 다음 예에서는 테이블 반환 함수 `dbo.GetContactInfo`에서 SET 문에 CASE 식을 사용합니다. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 사용자와 관련된 모든 데이터는 `Person.Person` 테이블에 저장됩니다. 예를 들어 사용자는 직원, 공급업체 담당자 또는 고객일 수 있습니다. 함수는 지정된 `BusinessEntityID`의 성과 이름 및 해당 사용자에 대한 연락처 유형을 반환합니다. SET 문의 CASE 식은 `Employee`, `Vendor` 또는 `Customer` 테이블에 `BusinessEntityID` 열이 있는지 여부에 따라 `ContactType` 열에 대해 표시할 값을 결정합니다.  
  
```sql   
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.GetContactInformation(@BusinessEntityID INT)  
    RETURNS @retContactInformation TABLE   
(  
BusinessEntityID INT NOT NULL,  
FirstName NVARCHAR(50) NULL,  
LastName NVARCHAR(50) NULL,  
ContactType NVARCHAR(50) NULL,  
    PRIMARY KEY CLUSTERED (BusinessEntityID ASC)  
)   
AS   
-- Returns the first name, last name and contact type for the specified contact.  
BEGIN  
    DECLARE   
        @FirstName NVARCHAR(50),   
        @LastName NVARCHAR(50),   
        @ContactType NVARCHAR(50);  
  
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
  
### <a name="f-using-case-in-a-having-clause"></a>F. HAVING 절에 CASE 사용  
 다음 예에서는 HAVING 절에 CASE 식을 사용하여 SELECT 문에서 반환하는 행을 제한합니다. 이 명령문은 `HumanResources.Employee` 테이블에서 각 직함에 대한 최대 시간당 급여를 반환합니다. HAVING 절은 직함을 최대 급여가 40달러가 넘는 남자 직원의 직함 또는 최대 급여가 42달러가 넘는 여자 직원의 직함으로 제한합니다.  
  
```sql  
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
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="g-using-a-select-statement-with-a-case-expression"></a>G. CASE 식이 포함된 SELECT 문 사용  
 SELECT 문 내에서 CASE 식을 사용하면 비교 값에 따라 결과 집합에서 값을 바꿀 수 있습니다. 다음 예제에서는 CASE 식을 사용하여 제품 라인 범주의 표시를 더 쉽게 이해할 수 있도록 변경합니다. 값이 없으면 "Not for sale"(판매하지 않음) 텍스트가 표시됩니다.  
  
```sql 
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
  
### <a name="h-using-case-in-an-update-statement"></a>H. UPDATE 문에 CASE 사용  
 다음 예에서는 UPDATE 문에 CASE 식을 사용하여 `VacationHours`가 0으로 설정된 직원의 열 `SalariedFlag`에 설정된 값을 확인합니다. `VacationHours`에서 10시간을 뺀 결과 음수 값이 되면 `VacationHours`가 40시간 증가되고, 그렇지 않으면 `VacationHours`가 20시간 증가됩니다.  
  
```sql  
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
  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [COALESCE&#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)   
 [IIF&#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)   
 [CHOOSE&#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-choose-transact-sql.md)  
  
  



