---
title: 매개 변수 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- user-defined functions [SQL Server], parameters
ms.assetid: c1f9bd93-3271-4098-a23b-7bd7a19ab65b
author: pmasl
ms.author: pelopes
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a30db8e163fcae15ac74af4d447a958182a88f5e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47599813"
---
# <a name="parameters"></a>매개 변수
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
매개 변수는 저장 프로시저나 함수를 호출하는 도구 또는 응용 프로그램, 함수 및 저장 프로시저 간에 데이터를 교환하는 데 사용됩니다. 

*  입력 매개 변수를 사용하면 호출자가 저장 프로시저나 함수에 데이터 값을 전달할 수 있습니다.
*  출력 매개 변수를 사용하면 저장 프로시저가 저장 프로시저나 함수에 데이터 값이나 커서 변수를 다시 전달할 수 있습니다. 사용자 정의 함수는 출력 매개 변수를 지정할 수 없습니다.
*  모든 저장 프로시저는 호출자에게 정수 반환 코드를 반환합니다. 저장 프로시저가 반환 코드에 대해 값을 명시적으로 설정하지 않는 경우 반환 코드는 0입니다.

다음 저장 프로시저는 입력 매개 변수, 출력 매개 변수 및 반환 코드의 사용 방식을 보여 줍니다.
```
-- Create a procedure that takes one input parameter and returns one output parameter and a return code.
CREATE PROCEDURE SampleProcedure @EmployeeIDParm INT,
         @MaxTotal INT OUTPUT
AS
-- Declare and initialize a variable to hold @@ERROR.
DECLARE @ErrorSave INT
SET @ErrorSave = 0

-- Do a SELECT using the input parameter.
SELECT FirstName, LastName, JobTitle
FROM HumanResources.vEmployee
WHERE EmployeeID = @EmployeeIDParm

-- Save any nonzero @@ERROR value.
IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Set a value in the output parameter.
SELECT @MaxTotal = MAX(TotalDue)
FROM Sales.SalesOrderHeader;

IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Returns 0 if neither SELECT statement had an error; otherwise, returns the last error.
RETURN @ErrorSave
GO
```

저장 프로시저나 함수가 실행되면 입력 매개 변수는 값을 상수로 설정하거나 변수의 값을 사용할 수 있습니다. 출력 매개 변수와 반환 코드는 값을 변수로 반환해야 합니다. 매개 변수와 반환 코드는 Transact-SQL 변수나 응용 프로그램 변수와 데이터 값을 교환할 수 있습니다.

일괄 처리 또는 스크립트에서 저장 프로시저를 호출하면 매개 변수와 반환 코드 값은 동일한 일괄 처리에 정의된 Transact-SQL 변수를 사용할 수 있습니다. 다음 예는 이전에 생성된 프로시저를 실행하는 일괄 처리입니다. 입력 매개 변수는 상수로 지정되고 출력 매개 변수와 반환 코드는 해당 값을 Transact-SQL 변수에 넣습니다.
```
-- Declare the variables for the return code and output parameter.
DECLARE @ReturnCode INT
DECLARE @MaxTotalVariable INT

-- Execute the stored procedure and specify which variables
-- are to receive the output parameter and return code values.
EXEC @ReturnCode = SampleProcedure @EmployeeIDParm = 19,
   @MaxTotal = @MaxTotalVariable OUTPUT

-- Show the values returned.
PRINT ' '
PRINT 'Return code = ' + CAST(@ReturnCode AS CHAR(10))
PRINT 'Maximum Quantity = ' + CAST(@MaxTotalVariable AS CHAR(10))
GO
```

응용 프로그램은 프로그램 변수에 바인딩된 매개 변수 표식을 사용하여 응용 프로그램 변수, 매개 변수 및 반환 코드 간에 데이터를 교환할 수 있습니다.

## <a name="see-also"></a>참고 항목
[CREATE PROCEDURE(Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable(Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [CREATE FUNCTION(Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)   
 [매개 변수 및 실행 계획 재사용 섹션](../../relational-databases/query-processing-architecture-guide.md)   
 [변수(Transact-SQL)](../../t-sql/language-elements/variables-transact-sql.md)
