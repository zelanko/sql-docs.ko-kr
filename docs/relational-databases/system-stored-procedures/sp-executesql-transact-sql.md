---
title: sp_executesql (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_executesql
- sp_executesql_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_executesql
- dynamic SQL
ms.assetid: a8d68d72-0f4d-4ecb-ae86-1235b962f646
caps.latest.revision: 64
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 38c0cd9d348e78a10be4917172c149750da8a657
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083795"
---
# <a name="spexecutesql-transact-sql"></a>sp_executesql(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  여러 번 사용할 수 있거나 동적으로 빌드된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이나 일괄 처리를 실행합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리는 포함 매개 변수를 포함할 수 있습니다.  
  
> [!IMPORTANT]  
>  런타임 컴파일된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 악의적인 공격에 응용 프로그램을 노출시킬 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_executesql [ @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [ OUT | OUTPUT ][ ,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>인수  
 [ \@stmt =] *문*  
 포함 하는 유니코드 문자열을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리 합니다. \@stmt은 유니코드 상수 또는 유니코드 변수 여야 합니다. + 연산자로 두 문자열을 연결한 식처럼 더 복잡한 유니코드 식은 사용할 수 없습니다. 문자 상수도 사용할 수 없습니다. 유니코드 상수를 지정 하면이 접두사로 추가 해야 합니다는 **N**합니다. 예를 들어 유니코드 상수 **N'sp_who '** 유효 하지만 문자 상수 **'sp_who'** 아닙니다. 문자열의 크기는 사용 가능한 데이터베이스 서버 메모리의 용량에 따라서만 제한됩니다. 64 비트 서버의 문자열의 크기는 최대 크기인 2GB로 제한 됩니다 **nvarchar (max)** 합니다.  
  
> [!NOTE]  
>  \@stmt 매개 변수는 변수 이름과 동일한 형식의 예를 들어를 포함할 수 있습니다. `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 에 포함 된 각 매개 변수에 \@stmt는 둘 다에 해당 하는 항목이 있어야 합니다 \@params 매개 변수 정의 목록과 매개 변수 값 목록입니다.  
  
 [ \@params =] N'\@*parameter_name * * data_type* [,... *n* ] '  
 에 포함 된 모든 매개 변수의 정의 포함 하는 하나의 문자열 \@stmt 합니다. 문자열은 유니코드 상수 또는 유니코드 변수여야 합니다. 각 매개 변수의 정의는 매개 변수 이름과 데이터 형식으로 구성됩니다. *n* 추가 매개 변수 정의 나타내는 자리 표시자입니다. 에 지정 된 모든 매개 변수에 \@stmtmust 정의 \@매개 변수입니다. 경우는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리 \@stmt 매개 변수는 \@params가 필요 하지 않습니다. 이 매개 변수의 기본값은 NULL입니다.  
  
 [ \@param1 =] '*value1*'  
 매개 변수 문자열에 정의된 첫 번째 매개 변수의 값입니다. 값은 유니코드 상수 또는 유니코드 변수가 될 수 있습니다. 에 포함 된 모든 매개 변수에 제공 되는 매개 변수 값이 있어야 \@stmt 합니다. 값이 필요한 경우는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리 \@stmt에 매개 변수가 없습니다.  
  
 [ OUT | OUTPUT ]  
 매개 변수가 출력 매개 변수임을 나타냅니다. **텍스트**하십시오 **ntext**, 및 **이미지** 프로시저 공용 언어 런타임 (CLR) 프로시저가 아닐 경우 출력 매개 변수로 매개 변수를 사용할 수 있습니다. 프로시저가 CLR 프로시저가 아닐 경우 OUTPUT 키워드를 사용하는 출력 매개 변수가 커서 자리 표시자일 수 있습니다.  
  
 *n*  
 추가 매개 변수의 값에 대한 자리 표시자입니다. 값은 상수 또는 변수만 가능합니다. 함수 또는 연산자를 사용하여 작성한 식처럼 더 복잡한 식은 값으로 사용할 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 값(실패)  
  
## <a name="result-sets"></a>결과 집합  
 작성된 모든 SQL 문에서 SQL 문자열로 결과 집합을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 이 항목 앞부분에서의 "구문" 섹션에 설명 된 대로 sp_executesql 매개 변수를 특정 순서로 입력 되어야 합니다. 매개 변수 순서가 잘못되면 오류 메시지가 나타납니다.  
  
 sp_executesql은 일괄 처리, 이름의 범위 및 데이터베이스 컨텍스트 면에서 EXECUTE와 동작이 동일합니다. 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리는 sp_executesql \@stmt 매개 변수는 sp_executesql 문이 실행 될 때까지 컴파일되지 않습니다. 내용을 \@stmt는 컴파일되고 sp_executesql 이라는 일괄 처리의 실행 계획과 별도로 실행 계획으로 실행 합니다. sp_executesql 일괄 처리는 sp_executesql을 호출하는 일괄 처리에서 선언된 변수를 참조할 수 없습니다. sp_executesql 일괄 처리의 로컬 커서 또는 변수는 sp_executesql을 호출하는 일괄 처리에 노출되지 않습니다. 데이터베이스 컨텍스트의 변경 내용은 sp_executesql 문이 종료될 때까지만 지속됩니다.  
  
 문에 대한 매개 변수 값의 변경 내용이 변형뿐인 경우 저장 프로시저 대신 sp_executesql을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 여러 번 실행할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 자체는 달라지지 않고 매개 변수 값만 달라지므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 처음 실행할 때 생성되는 실행 계획을 다시 사용합니다.  
  
> [!NOTE]  
>  문의 문자열에 정규화된 개체 이름을 사용하여 성능을 향상시킬 수 있습니다.  
  
 다음 예와 같이 sp_executesql은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문자열과 별도로 매개 변수 값 설정을 지원합니다.  
  
```  
DECLARE @IntVariable int;  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
  
/* Build the SQL string one time.*/  
SET @SQLString =  
     N'SELECT BusinessEntityID, NationalIDNumber, JobTitle, LoginID  
       FROM AdventureWorks2012.HumanResources.Employee   
       WHERE BusinessEntityID = @BusinessEntityID';  
SET @ParmDefinition = N'@BusinessEntityID tinyint';  
/* Execute the string with the first parameter value. */  
SET @IntVariable = 197;  
EXECUTE sp_executesql @SQLString, @ParmDefinition,  
                      @BusinessEntityID = @IntVariable;  
/* Execute the same string with the second parameter value. */  
SET @IntVariable = 109;  
EXECUTE sp_executesql @SQLString, @ParmDefinition,  
                      @BusinessEntityID = @IntVariable;  
```  
  
 출력 매개 변수는 sp_executesql에도 사용할 수 있습니다. 다음 예에서는 `AdventureWorks2012.HumanResources.Employee` 테이블에서 직함을 검색하여 출력 매개 변수 `@max_title`에 반환합니다.  
  
```  
DECLARE @IntVariable int;  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
DECLARE @max_title varchar(30);  
  
SET @IntVariable = 197;  
SET @SQLString = N'SELECT @max_titleOUT = max(JobTitle)   
   FROM AdventureWorks2012.HumanResources.Employee  
   WHERE BusinessEntityID = @level';  
SET @ParmDefinition = N'@level tinyint, @max_titleOUT varchar(30) OUTPUT';  
  
EXECUTE sp_executesql @SQLString, @ParmDefinition, @level = @IntVariable, @max_titleOUT=@max_title OUTPUT;  
SELECT @max_title;  
```  
  
 sp_executesql에서 매개 변수를 대체할 수 있으면 EXECUTE 문을 사용하여 문자열을 실행할 때 다음과 같은 이점이 있습니다.  
  
-   sp_executesql 문자열에 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 실제 텍스트는 모든 실행에서 동일하기 때문에 쿼리 최적화 프로그램이 두 번째 실행의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 첫 번째 실행에서 생성된 실행 계획을 일치시킬 수 있습니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 두 번째 문을 컴파일할 필요가 없습니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문자열이 한 번만 작성됩니다.  
  
-   정수 매개 변수는 해당 네이티브 형식으로 지정됩니다. 유니코드로 캐스팅할 필요가 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-executing-a-simple-select-statement"></a>1. 단순 SELECT 문 실행  
 다음은 `SELECT`이라는 포함 매개 변수를 포함한 단순 `@level` 문을 만들고 실행하는 예입니다.  
  
```  
EXECUTE sp_executesql   
          N'SELECT * FROM AdventureWorks2012.HumanResources.Employee   
          WHERE BusinessEntityID = @level',  
          N'@level tinyint',  
          @level = 109;  
```  
  
### <a name="b-executing-a-dynamically-built-string"></a>2. 동적으로 작성된 문자열 실행  
 다음 예에서는 `sp_executesql`을 사용하여 동적으로 작성된 문자열 실행을 보여 줍니다. 예로 사용된 저장 프로시저는 1년 간의 판매 데이터를 분할하기 위해 사용하는 일련의 테이블에 데이터를 삽입하는 데 사용됩니다. 해당 연도의 각 달마다 다음과 같은 형식의 테이블이 하나씩 있습니다.  
  
```  
CREATE TABLE May1998Sales  
    (OrderID int PRIMARY KEY,  
    CustomerID int NOT NULL,  
    OrderDate  datetime NULL  
        CHECK (DATEPART(yy, OrderDate) = 1998),  
    OrderMonth int  
        CHECK (OrderMonth = 5),  
    DeliveryDate datetime  NULL,  
        CHECK (DATEPART(mm, OrderDate) = OrderMonth)  
    )  
```  
  
 이 예제 저장 프로시저는 동적으로 `INSERT` 문을 작성하고 실행하여 새 주문을 알맞은 테이블에 삽입합니다. 이 예에서는 주문 날짜를 사용하여 데이터를 포함해야 하는 테이블의 이름을 작성한 다음 `INSERT` 문에 통합합니다.  
  
> [!NOTE]  
>  다음은 sp_executesql의 간단한 예입니다. 이 예에는 오류 검사가 포함되지 않으며 여러 테이블에서 주문 번호가 중복되지 않도록 하는 등의 비즈니스 규칙 확인이 포함되지 않습니다.  
  
```  
CREATE PROCEDURE InsertSales @PrmOrderID INT, @PrmCustomerID INT,  
                 @PrmOrderDate DATETIME, @PrmDeliveryDate DATETIME  
AS  
DECLARE @InsertString NVARCHAR(500)  
DECLARE @OrderMonth INT  
  
-- Build the INSERT statement.  
SET @InsertString = 'INSERT INTO ' +  
       /* Build the name of the table. */  
       SUBSTRING( DATENAME(mm, @PrmOrderDate), 1, 3) +  
       CAST(DATEPART(yy, @PrmOrderDate) AS CHAR(4) ) +  
       'Sales' +  
       /* Build a VALUES clause. */  
       ' VALUES (@InsOrderID, @InsCustID, @InsOrdDate,' +  
       ' @InsOrdMonth, @InsDelDate)'  
  
/* Set the value to use for the order month because  
   functions are not allowed in the sp_executesql parameter  
   list. */  
SET @OrderMonth = DATEPART(mm, @PrmOrderDate)  
  
EXEC sp_executesql @InsertString,  
     N'@InsOrderID INT, @InsCustID INT, @InsOrdDate DATETIME,  
       @InsOrdMonth INT, @InsDelDate DATETIME',  
     @PrmOrderID, @PrmCustomerID, @PrmOrderDate,  
     @OrderMonth, @PrmDeliveryDate  
  
GO  
```  
  
 이 프로시저에서는 EXECUTE를 사용하는 것보다 sp_executesql을 사용하여 문자열을 실행하는 것이 효과적입니다. sp_executesql을 사용하는 경우 월별 테이블마다 하나씩 12개 버전의 INSERT 문자열만 작성됩니다. EXECUTE를 사용하면 매개 변수 값이 다르므로 각 INSERT 문자열이 고유합니다. 두 방법 모두 같은 수의 일괄 처리를 생성하지만 sp_executesql에 의해 생성된 INSERT 문자열이 서로 비슷하기 때문에 쿼리 최적화 프로그램이 실행 계획을 다시 사용하기 쉽습니다.  
  
### <a name="c-using-the-output-parameter"></a>3. OUTPUT 매개 변수 사용  
 다음 예제에서는 `OUTPUT` 매개 변수에서 생성 된 결과 집합을 저장 합니다 `SELECT` 문에서 `@SQLString` 매개 변수입니다. 두 개의 `SELECT` 문이 실행 됩니다의 값을 사용 하 여 `OUTPUT` 매개 변수입니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
DECLARE @SalesOrderNumber nvarchar(25);  
DECLARE @IntVariable int;  
SET @SQLString = N'SELECT @SalesOrderOUT = MAX(SalesOrderNumber)  
    FROM Sales.SalesOrderHeader  
    WHERE CustomerID = @CustomerID';  
SET @ParmDefinition = N'@CustomerID int,  
    @SalesOrderOUT nvarchar(25) OUTPUT';  
SET @IntVariable = 22276;  
EXECUTE sp_executesql  
    @SQLString  
    ,@ParmDefinition  
    ,@CustomerID = @IntVariable  
    ,@SalesOrderOUT = @SalesOrderNumber OUTPUT;  
-- This SELECT statement returns the value of the OUTPUT parameter.  
SELECT @SalesOrderNumber;  
-- This SELECT statement uses the value of the OUTPUT parameter in  
-- the WHERE clause.  
SELECT OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderNumber = @SalesOrderNumber;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-executing-a-simple-select-statement"></a>4. 단순 SELECT 문 실행  
 다음은 `SELECT`이라는 포함 매개 변수를 포함한 단순 `@level` 문을 만들고 실행하는 예입니다.  
  
```  
-- Uses AdventureWorks  
  
EXECUTE sp_executesql   
          N'SELECT * FROM AdventureWorksPDW2012.dbo.DimEmployee   
          WHERE EmployeeKey = @level',  
          N'@level tinyint',  
          @level = 109;  
```  
  
 추가 예제를 보려면 [sp_executesql (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms188001.aspx)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
