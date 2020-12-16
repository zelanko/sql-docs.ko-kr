---
description: 변수(Transact-SQL)
title: 변수(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f372ae86-a003-40af-92de-fa52e3eea13f
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8ae1facbb6e69dee6fe9e91ab5755e1d454fa679
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460936"
---
# <a name="variables-transact-sql"></a>변수(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Transact-SQL 지역 변수는 특정 유형의 단일 데이터 값을 보유할 수 있는 개체입니다. 일괄 처리 및 스크립트에 있는 변수는 일반적으로 다음과 같이 사용될 수 있습니다. 

* 루프가 수행되는 횟수를 세거나 제어하는 카운터로 사용됩니다.
* 흐름 제어 문에서 테스트되는 데이터 값을 보유할 수 있습니다.
* 저장 프로시저 반환 코드 또는 함수 반환 값으로 반환되는 데이터 값을 저장할 수 있습니다.

> [!NOTE]
> - 일부 Transact-SQL 시스템 함수의 이름은 두 개의 *at* 기호(\@\@)로 시작합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 \@\@함수가 전역 변수로 참조되지만 \@\@함수는 변수가 아니며 변수와 동일하게 동작하지 않습니다. \@\@함수는 시스템 함수이며 구문 사용법이 함수 규칙을 따릅니다.
> - 뷰에서 변수를 사용할 수 없습니다.
> - 변수의 변경 내용은 트랜잭션 롤백의 영향을 받지 않습니다.

다음 스크립트는 작은 테스트 테이블을 만들고 26개 행으로 채웁니다. 이 스크립트는 변수를 사용하여 다음 세 가지 작업을 수행합니다. 

* 루프가 실행되는 횟수를 제어하여 삽입되는 행 수를 제어합니다.
* 정수 열에 삽입되는 값을 제공합니다.
* 문자 열에 삽입되는 문자를 생성하는 식의 일부로 기능합니다.  

```sql
-- Create the table.
CREATE TABLE TestTable (cola INT, colb CHAR(3));
GO
SET NOCOUNT ON;
GO
-- Declare the variable to be used.
DECLARE @MyCounter INT;

-- Initialize the variable.
SET @MyCounter = 0;

-- Test the variable to see if the loop is finished.
WHILE (@MyCounter < 26)
BEGIN;
   -- Insert a row into the table.
   INSERT INTO TestTable VALUES
       -- Use the variable to provide the integer value
       -- for cola. Also use it to generate a unique letter
       -- for each row. Use the ASCII function to get the
       -- integer value of 'a'. Add @MyCounter. Use CHAR to
       -- convert the sum back to the character @MyCounter
       -- characters after 'a'.
       (@MyCounter,
        CHAR( ( @MyCounter + ASCII('a') ) )
       );
   -- Increment the variable to count this iteration
   -- of the loop.
   SET @MyCounter = @MyCounter + 1;
END;
GO
SET NOCOUNT OFF;
GO
-- View the data.
SELECT cola, colb
FROM TestTable;
GO
DROP TABLE TestTable;
GO
```

## <a name="declaring-a-transact-sql-variable"></a>Transact-SQL 변수 선언
DECLARE 문은 다음을 통해 Transact-SQL 변수를 초기화합니다. 
* 이름 할당. 이름에는 첫 문자로 \@을 하나 사용해야 합니다.
* 시스템 제공 또는 사용자 정의 데이터 형식 및 길이 할당. 숫자 변수에 대해 전체 자릿수 및 소수 자릿수도 할당됩니다. XML 형식의 변수에 대해서는 선택적 스키마 컬렉션이 할당될 수 있습니다.
* 값을 NULL로 설정

예를 들어 다음 **DECLARE** 문은 int 데이터 형식의 **\@mycounter** 라는 지역 변수를 만듭니다.  
```sql
DECLARE @MyCounter INT;
```
둘 이상의 지역 변수를 선언하려면 정의된 첫 지역 변수 다음에 쉼표를 사용한 후 다음 지역 변수의 이름 및 데이터 형식을 지정합니다.

예를 들어 다음 **DECLARE** 문은 **\@LastName**, **\@FirstName** 및 **\@StateProvince** 의 세 지역 변수를 만들고 각각 NULL로 초기화합니다.  
```sql
DECLARE @LastName NVARCHAR(30), @FirstName NVARCHAR(20), @StateProvince NCHAR(2);
```

변수 범위는 변수를 참조할 수 있는 Transact-SQL 문의 범위입니다. 변수 범위는 선언된 시점부터 이를 선언했던 일괄 처리 또는 저장 프로시저가 끝날 때까지 계속됩니다. 예를 들어 다음 스크립트는 변수가 하나의 일괄 처리에서 선언되고 또 다른 일괄 처리에서 참조되므로 구문 오류를 일으킵니다.  
```sql
USE AdventureWorks2014;
GO
DECLARE @MyVariable INT;
SET @MyVariable = 1;
-- Terminate the batch by using the GO keyword.
GO 
-- @MyVariable has gone out of scope and no longer exists.

-- This SELECT statement generates a syntax error because it is
-- no longer legal to reference @MyVariable.
SELECT BusinessEntityID, NationalIDNumber, JobTitle
FROM HumanResources.Employee
WHERE BusinessEntityID = @MyVariable;
```

변수에는 변수가 정의된 일괄 처리 또는 프로시저 내에서만 표시되는 로컬 범위가 있습니다. 다음 예에서 sp_executesql을 실행하기 위해 만든 중첩 범위에서는 더 높은 범위에서 선언된 변수에 액세스할 수 없으므로 오류가 반환됩니다.  

```sql
DECLARE @MyVariable INT;
SET @MyVariable = 1;
EXECUTE sp_executesql N'SELECT @MyVariable'; -- this produces an error
```

## <a name="setting-a-value-in-a-transact-sql-variable"></a>Transact-SQL 변수에서의 값 설정

변수가 처음으로 선언되면 그 값은 NULL로 설정됩니다. 변수에 값을 할당하려면 SET 문을 사용합니다. 이는 변수에 값을 할당하는 기본 설정 방법입니다. 변수에는 또한 SELECT 문의 선택 목록에서 참조되어 할당된 값이 있을 수 있습니다.

SET 문을 사용하여 변수에 값을 할당하려면 변수 이름과 변수에 할당할 값을 포함시킵니다. 이는 변수에 값을 할당하는 기본 설정 방법입니다. 예를 들어 다음 일괄 처리는 두 변수를 선언하고 값을 할당한 다음 `WHERE` 문의 `SELECT` 절에서 사용합니다.  

```sql
USE AdventureWorks2014;
GO
-- Declare two variables.
DECLARE @FirstNameVariable NVARCHAR(50),
   @PostalCodeVariable NVARCHAR(15);

-- Set their values.
SET @FirstNameVariable = N'Amy';
SET @PostalCodeVariable = N'BA5 3HX';

-- Use them in the WHERE clause of a SELECT statement.
SELECT LastName, FirstName, JobTitle, City, StateProvinceName, CountryRegionName
FROM HumanResources.vEmployee
WHERE FirstName = @FirstNameVariable
   OR PostalCode = @PostalCodeVariable;
GO
```

변수에는 또한 선택 목록에서 참조되어 할당된 값이 있을 수 있습니다. 변수가 선택 목록에서 참조되면 이 변수에 스칼라 값이 할당되거나 SELECT 문이 행을 하나만 반환해야 합니다. 예를 들면 다음과 같습니다.  

```sql
USE AdventureWorks2014;
GO
DECLARE @EmpIDVariable INT;

SELECT @EmpIDVariable = MAX(EmployeeID)
FROM HumanResources.Employee;
GO
```

> [!WARNING]
> SELECT 문 하나에 할당 절이 여러 개 있을 경우 SQL Server에서는 식의 계산 순서를 보장하지 않습니다. 할당 간에 참조가 있을 경우에만 그 결과가 표시됩니다.

SELECT 문에서 행을 두 개 이상 반환하고 변수가 스칼라가 아닌 식을 참조하면 변수는 결과 집합의 마지막 행에 있는 식에 대해 반환된 값으로 설정됩니다. 예를 들어 다음 일괄 처리에서 **\@EmpIDVariable** 은 반환된 마지막 행의 **BusinessEntityID** 값인 1로 설정됩니다.  

```sql
USE AdventureWorks2014;
GO
DECLARE @EmpIDVariable INT;

SELECT @EmpIDVariable = BusinessEntityID
FROM HumanResources.Employee
ORDER BY BusinessEntityID DESC;

SELECT @EmpIDVariable;
GO
```

## <a name="see-also"></a>참고 항목  
 [Declare@local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
 [SET @local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
 [SELECT @local_variable](../../t-sql/language-elements/select-local-variable-transact-sql.md)  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
  
  
