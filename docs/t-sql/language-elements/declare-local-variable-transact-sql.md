---
title: DECLARE @local_variable(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECLARE
- DECLARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table-valued parameters
- variables [SQL Server], declaring
- DECLARE statement
- declaring variables
ms.assetid: d1635ebb-f751-4de1-8bbc-cae161f90821
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 01de83dc56a14fca265bd73b5d5df357f869a50a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47609249"
---
# <a name="declare-localvariable-transact-sql"></a>DECLARE @local_variable(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  DECLARE 문을 사용하여 일괄 처리나 프로시저의 본문에 변수를 선언하고 SET 또는 SELECT 문을 사용하여 값을 할당합니다. 이 문을 사용하여 커서 변수를 선언하고 다른 커서 관련 문과 함께 사용할 수 있습니다. 선언의 일부로 값을 지정하지 않으면 선언 후 모든 변수가 NULL로 초기화됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DECLARE   
{   
    { @local_variable [AS] data_type  [ = value ] }  
  | { @cursor_variable_name CURSOR }  
} [,...n]   
| { @table_variable_name [AS] <table_type_definition> }   
  
<table_type_definition> ::=   
     TABLE ( { <column_definition> | <table_constraint> } [ ,...n] )   
  
<column_definition> ::=   
     column_name { scalar_data_type | AS computed_column_expression }  
     [ COLLATE collation_name ]   
     [ [ DEFAULT constant_expression ] | IDENTITY [ (seed ,increment ) ] ]   
     [ ROWGUIDCOL ]   
     [ <column_constraint> ]   
  
<column_constraint> ::=   
     { [ NULL | NOT NULL ]   
     | [ PRIMARY KEY | UNIQUE ]   
     | CHECK ( logical_expression )   
     | WITH ( <index_option > )  
     }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n] )   
     | CHECK ( search_condition )   
     }   
  
<index_option> ::=  
See CREATE TABLE for index option syntax.  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DECLARE   
{{ @local_variable [AS] data_type } [ =value [ COLLATE <collation_name> ] ] } [,...n]  
  
```  
  
## <a name="arguments"></a>인수  
@*local_variable*  
 변수의 이름입니다. 변수 이름은 @ 기호로 시작해야 합니다. 지역 변수 이름은 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다.  
  
*data_type*  
 시스템 제공 데이터 형식, CLR(공용 언어 런타임) 사용자 정의 테이블 형식 또는 별칭 데이터 형식입니다. 변수는 **text**, **ntext** 또는 **image** 데이터 형식일 수 없습니다.  
  
 시스템 데이터 형식에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요. CLR 사용자 정의 형식에 대한 자세한 내용은 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)을 참조하세요.  
  
 =*value*  
 인라인으로 변수에 값을 할당합니다. 값은 상수 또는 식일 수 있지만 변수 선언 형식과 일치하거나 해당 형식으로 암시적으로 변환할 수 있어야 합니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
@*cursor_variable_name*  
 커서 변수의 이름입니다. 커서 변수 이름은 @ 기호로 시작해야 하며 식별자 규칙을 따라야 합니다.  
  
CURSOR  
 변수가 로컬 커서 변수가 되도록 지정합니다.  
  
@*table_variable_name*  
 **table** 형식의 변수 이름입니다. 변수 이름은 at 기호(@)로 시작해야 하며 식별자 규칙을 따라야 합니다.  
  
<table_type_definition>  
**table** 데이터 형식을 정의합니다. 테이블 선언에는 열 정의, 이름, 데이터 형식 및 제약 조건 등이 포함되며 PRIMARY KEY, UNIQUE, NULL 및 CHECK만 제약 조건 유형으로 사용할 수 있습니다. 규칙 또는 기본 정의가 형식에 바인딩되어 있는 경우 별칭 데이터 형식을 열 스칼라 데이터 형식으로 사용할 수 없습니다.
  
\<table_type_definition>은 CREATE TABLE에 있는 테이블을 정의하는 정보의 하위 집합입니다. 여러 요소와 주요 정의가 여기에 포함됩니다. 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.  
  
 *n*  
 여러 변수를 지정하여 값을 할당할 수 있음을 나타내는 자리 표시자입니다. **table** 변수를 선언할 때는 **table** 변수가 DECLARE 문으로 선언되는 유일한 변수여야 합니다.  
  
 *column_name*  
 테이블에 있는 열의 이름입니다.  
  
 *scalar_data_type*  
 열에 스칼라 데이터 형식을 지정합니다.  
  
 *computed_column_expression*  
 계산 열의 값을 정의하는 식입니다. 동일한 테이블의 다른 열을 사용하는 식에서 계산됩니다. 예를 들어 계산 열은 **cost** AS **price \* qty** 정의를 가질 수 있습니다. 식은 계산되지 않은 열 이름, 상수, 기본 제공 함수, 변수 또는 이러한 요소를 하나 이상의 연산자로 연결한 조합이 될 수 있습니다. 식은 하위 쿼리 또는 사용자 정의 함수가 될 수 없습니다. 식은 CLR 사용자 정의 데이터 형식을 참조할 수 없습니다.  
  
 [ COLLATE *collation_name*]  
 열에 대한 데이터 정렬을 지정합니다. *collation_name*은 Windows 데이터 정렬 이름이나 SQL 데이터 정렬 이름이 될 수 있으며, **char**, **varchar**, **text**, **nchar**, **nvarchar** 및 **ntext** 데이터 형식의 열에만 적용할 수 있습니다. 지정하지 않은 경우 열이 사용자 정의 데이터 형식이면 사용자 정의 데이터 형식의 데이터 정렬에 열이 할당되고 그렇지 않은 경우에는 현재 데이터베이스의 데이터 정렬에 할당됩니다.  
  
 Windows 및 SQL 데이터 정렬 이름에 대한 자세한 내용은 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)를 참조하세요.  
  
 DEFAULT  
 삽입 중에 값이 명시적으로 지정되지 않은 경우에 열에 대해 제공되는 값을 지정합니다. DEFAULT 정의는 **timestamp**로 정의되거나 IDENTITY 속성이 있는 열을 제외한 모든 열에 적용할 수 있습니다. DEFAULT 정의는 테이블이 삭제될 때 제거됩니다. 문자열 같은 상수 값, SYSTEM_USER() 같은 시스템 함수 또는 NULL을 기본값으로 사용할 수 있습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환성을 유지하기 위해 DEFAULT에 제약 조건 이름을 할당할 수 있습니다.  
  
 *constant_expression*  
 열의 기본값으로 사용되는 상수, NULL 또는 시스템 함수입니다.  
  
 IDENTITY  
 새 열이 ID 열임을 나타냅니다. 테이블에 새 행이 추가되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 열에 사용할 고유한 증가값을 제공합니다. ID 열은 일반적으로 PRIMARY KEY 제약 조건과 함께 사용되어 테이블의 고유한 행 식별자 역할을 합니다. IDENTITY 속성은 **tinyint**, **smallint**, **int**, **decimal(p,0)** 또는 **numeric(p,0)** 열에 할당할 수 있습니다. ID 열은 테이블당 하나만 만들 수 있습니다. ID 열에는 바인딩된 기본값 및 DEFAULT 제약 조건을 사용할 수 없습니다. 초기값과 증가값을 모두 지정하거나 모두 지정하지 않아야 합니다. 둘 다 지정하지 않은 경우에는 기본값 (1,1)이 사용됩니다.  
  
 *seed*  
 테이블에 로드되는 첫 번째 행에 사용하는 값입니다.  
  
 *increment*  
 이전에 로드된 행의 ID 값에 추가되는 증가값입니다.  
  
 ROWGUIDCOL  
 새 열이 행 전역 고유 식별자 열임을 나타냅니다. 테이블당 한 개의 **uniqueidentifier** 열만 ROWGUIDCOL 열로 지정할 수 있으며 ROWGUIDCOL 속성은 **uniqueidentifier** 열에만 할당할 수 있습니다.  
  
 NULL | NOT NULL  
 변수에 null이 허용되는지 여부를 나타냅니다. 기본값은 NULL입니다.  
  
 PRIMARY KEY  
 고유한 인덱스를 통해 지정된 열 또는 여러 열에 엔터티 무결성을 제공하는 제약 조건입니다. PRIMARY KEY 제약 조건은 각 테이블마다 하나만 만들 수 있습니다.  
  
 UNIQUE  
 고유한 인덱스를 통해 지정된 열 또는 여러 열에 엔터티 무결성을 제공하는 제약 조건입니다. 하나의 테이블이 여러 개의 UNIQUE 제약 조건을 가질 수 있습니다.  
  
 CHECK  
 열에 입력 가능한 값을 제한하여 도메인 무결성을 적용하는 제약 조건입니다.  
  
 *logical_expression*  
 TRUE 또는 FALSE를 반환하는 논리 식입니다.  
  
## <a name="remarks"></a>Remarks  
 일괄 처리나 프로시저에서 변수는 종종 WHILE, LOOP 또는 IF...ELSE 블록의 카운터로 사용됩니다.  
  
 변수는 식에서만 사용할 수 있으며 개체 이름이나 키워드 대신 사용할 수 없습니다. 동적 SQL 문을 생성하려면 EXECUTE를 사용합니다.  
  
 지역 변수의 범위는 변수가 선언된 일괄 처리입니다.  
 
 테이블 변수가 반드시 메모리 상주하지는 않습니다. 메모리가 부족하면 테이블 변수에 속한 페이지를 tempdb로 푸시 아웃 할 수 있습니다.
  
 현재 커서가 할당된 커서 변수는 다음 문의 원본으로 참조될 수 있습니다.  
  
-   CLOSE 문  
  
-   DEALLOCATE 문  
  
-   FETCH 문  
  
-   OPEN 문  
  
-   지정된 DELETE 문 또는 UPDATE 문  
  
-   SET CURSOR 변수 문(오른쪽에 있음)  
  
 위의 모든 문에서 참조되는 커서 변수가 존재하지만 현재 할당된 커서가 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류가 발생합니다. 또한 참조되는 커서 변수가 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 선언되지 않은 다른 형식의 변수에 동일한 오류가 발생합니다.  
  
 커서 변수는 다음과 같습니다.  
  
-   커서 형식이나 다른 커서 변수의 대상이 될 수 있습니다. 자세한 내용은 [SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)을 참조하세요.  
  
-   커서 변수에 현재 할당된 커서가 없으면 EXECUTE 문에서 출력 커서 매개 변수의 대상으로 참조될 수 있습니다.  
  
-   커서에 대한 포인터로 간주됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-declare"></a>1. DECLARE 사용  
 다음 예에서는 `@find`라는 지역 변수를 사용하여 성이 `Man`으로 시작하는 모든 연락처 정보를 검색합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @find varchar(30);   
/* Also allowed:   
DECLARE @find varchar(30) = 'Man%';   
*/  
SET @find = 'Man%';   
SELECT p.LastName, p.FirstName, ph.PhoneNumber  
FROM Person.Person AS p   
JOIN Person.PersonPhone AS ph ON p.BusinessEntityID = ph.BusinessEntityID  
WHERE LastName LIKE @find;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName            FirstName               Phone
------------------- ----------------------- -------------------------
Manchepalli         Ajay                    1 (11) 500 555-0174
Manek               Parul                   1 (11) 500 555-0146
Manzanares          Tomas                   1 (11) 500 555-0178
  
(3 row(s) affected)
```  
  
### <a name="b-using-declare-with-two-variables"></a>2. 두 변수가 있는 DECLARE 사용  
 다음 예에서는 북미 영업 지역 소속이고 연간 $2,000,000 이상을 판매한 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 판매원을 검색합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SET NOCOUNT ON;  
GO  
DECLARE @Group nvarchar(50), @Sales money;  
SET @Group = N'North America';  
SET @Sales = 2000000;  
SET NOCOUNT OFF;  
SELECT FirstName, LastName, SalesYTD  
FROM Sales.vSalesPerson  
WHERE TerritoryGroup = @Group and SalesYTD >= @Sales;  
```  
  
### <a name="c-declaring-a-variable-of-type-table"></a>3. 테이블 형식의 변수 선언  
 다음 예에서는 UPDATE 문의 OUTPUT 절에서 지정된 값을 저장하는 `table` 변수를 만듭니다. 각각 `SELECT`의 값과 `@MyTableVar` 테이블의 업데이트 작업 결과를 반환하는 두 개의 `Employee` 문이 이어집니다. `INSERTED.ModifiedDate` 열의 결과 값은 `Employee` 테이블의 `ModifiedDate` 열 값과 다릅니다. 그 이유는 `AFTER UPDATE` 값을 현재 날짜로 업데이트하는 `ModifiedDate` 트리거가 `Employee` 테이블에 정의되어 있기 때문입니다. 그러나 `OUTPUT`에서 반환된 열은 트리거가 실행되기 전의 데이터를 반영합니다. 자세한 내용은 [OUTPUT Clause&#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)를 참조하세요.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25   
OUTPUT INSERTED.BusinessEntityID,  
       DELETED.VacationHours,  
       INSERTED.VacationHours,  
       INSERTED.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
--Note that ModifiedDate reflects the value generated by an  
--AFTER UPDATE trigger.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
### <a name="d-declaring-a-variable-of-user-defined-table-type"></a>4. 사용자 정의 테이블 형식의 변수 선언  
 다음 예에서는 `@LocationTVP`라고 하는 테이블 반환 매개 변수 또는 테이블 변수를 만듭니다. 이렇게 하려면 `LocationTableType`이라고 하는 해당 사용자 정의 테이블 형식이 필요합니다. 사용자 정의 테이블 형식을 만드는 방법은 [CREATE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)을 참조하세요. 테이블 반환 매개 변수에 관한 자세한 내용은 [Use Table-Valued Parameters&#40;Database Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)를 참조하세요.  
  
```  
DECLARE @LocationTVP   
AS LocationTableType;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-declare"></a>5. DECLARE 사용  
 다음 예에서는 `@find`라는 지역 변수를 사용하여 성이 `Walt`으로 시작하는 모든 연락처 정보를 검색합니다.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @find varchar(30);  
/* Also allowed:   
DECLARE @find varchar(30) = 'Man%';  
*/  
SET @find = 'Walt%';  
  
SELECT LastName, FirstName, Phone  
FROM DimEmployee   
WHERE LastName LIKE @find;  
```  
  
### <a name="f-using-declare-with-two-variables"></a>6. 두 변수가 있는 DECLARE 사용  
 다음 예는 `DimEmployee` 테이블에 있는 직원의 성과 이름을 지정하기 위해 변수를 검색하여 사용합니다.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @lastName varchar(30), @firstName varchar(30);  
  
SET @lastName = 'Walt%';  
SET @firstName = 'Bryan';  
  
SELECT LastName, FirstName, Phone  
FROM DimEmployee   
WHERE LastName LIKE @lastName AND FirstName LIKE @firstName;  
```  
  
## <a name="see-also"></a>참고 항목  
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)  
  
  




