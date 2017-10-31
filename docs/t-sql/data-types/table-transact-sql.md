---
title: "테이블 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table data type [SQL Server]
- table variables [SQL Server]
ms.assetid: 1ef0b60e-a64c-4e97-847b-67930e3973ef
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b22ecfa04f949af77df974abc3359b7bc5144a82
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="table-transact-sql"></a>table(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

나중에 처리하기 위해 결과 집합을 저장하는 데 사용할 수 있는 특별한 데이터 형식입니다. **테이블** 는 주로 테이블 반환 함수의 결과 집합으로 반환 되는 행 집합의 임시 저장에 사용 합니다. 함수 및 변수 형식으로 선언할 수 있습니다 **테이블**합니다. **테이블** 함수, 저장된 프로시저 및 일괄 처리에서 변수를 사용할 수 있습니다. 형식의 변수를 선언 하려면 **테이블**를 사용 하 여 [DECLARE @local_variable ](../../t-sql/language-elements/declare-local-variable-transact-sql.md)합니다.
  

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
table_type_definition ::=   
    TABLE ( { <column_definition> | <table_constraint> } [ ,...n ] )   
  
<column_definition> ::=   
    column_name scalar_data_type   
    [ COLLATE <collation_definition> ]   
    [ [ DEFAULT constant_expression ] | IDENTITY [ ( seed , increment ) ] ]   
    [ ROWGUIDCOL ]   
    [ column_constraint ] [ ...n ]   
  
 <column_constraint> ::=   
    { [ NULL | NOT NULL ]   
    | [ PRIMARY KEY | UNIQUE ]   
    | CHECK ( logical_expression )   
    }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n ] )  
     | CHECK ( logical_expression )   
     }   
```  
  
## <a name="arguments"></a>인수  
*table_type_definition*  
CREATE TABLE에서 테이블을 정의하는 데 사용되는 정보의 같은 하위 집합입니다. 테이블 선언에는 열 정의, 이름, 데이터 형식 및 제약 조건 등이 포함되며 허용되는 제약 조건 유형은 PRIMARY KEY, UNIQUE KEY 및 NULL뿐입니다.  
구문에 대 한 자세한 내용은 참조 [CREATE table&#40; Transact SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md), [함수 &#40; 만들기 Transact SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md), 및 [DECLARE @local_variable &#40; Transact SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  
*collation_definition*  
구성 된 열의 데이터 정렬을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 로캘 및 비교 스타일, Windows 로캘 및 이진 표기법 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬입니다. 경우 *collation_definition* 를 지정 하지 않으면 해당 열에는 현재 데이터베이스의 데이터 정렬을 상속 합니다. 또는 CLR(공용 언어 런타임) 사용자 정의 형식으로 열을 정의할 경우 사용자 정의 형식의 데이터 정렬이 해당 열에 상속됩니다.
  
## <a name="remarks"></a>주의  
**테이블** 다음 예제와 같이 이름, 일괄 처리의 FROM 절에 변수를 참조할 수 있습니다.
  
```sql
SELECT Employee_ID, Department_ID FROM @MyTableVar;  
```  
  
FROM 절 밖 **테이블** 다음 예제와 같이 별칭을 사용 하 여 변수를 참조 해야 합니다.
  
```sql
SELECT EmployeeID, DepartmentID   
FROM @MyTableVar m  
JOIN Employee on (m.EmployeeID =Employee.EmployeeID AND  
   m.DepartmentID = Employee.DepartmentID);  
```  
  
**테이블** 변수 쿼리 계획이 변경 되지 않는 한 경우 다시 컴파일 기능이 중요 널리 사용 되 고 있는 소규모 쿼리의 대 한 다음과 같은 이점을 제공 합니다.
-   A **테이블** 변수 지역 변수 처럼 동작 합니다. 잘 정의된 범위를 가집니다. 범위는 변수가 선언된 함수, 저장 프로시저 또는 일괄 처리입니다.  
     해당 범위 내에서 한 **테이블** 일반 테이블 처럼 변수를 사용할 수 있습니다. SELECT, INSERT, UPDATE 및 DELETE 문에서 테이블 또는 테이블 식이 사용되는 어디에나 적용할 수 있습니다. 그러나 **테이블** 다음 문에서 사용할 수 없습니다.  
  
```sql
SELECT select_list INTO table_variable;
```
  
**테이블** 함수, 저장된 프로시저 또는 정의 된 일괄 처리의 끝에 변수는 자동으로 정리 합니다.
  
-   **테이블** 저장된 프로시저에서 사용 되는 변수는 저장된 프로시저의 다시 컴파일이 성능에 영향을 주는 비용 기반 선택 없는 경우 임시 테이블을 사용할 때 보다 적게 발생 합니다.  
-   관련 된 트랜잭션은 **테이블** 변수에 대 한 업데이트 기간에만 마지막는 **테이블** 변수입니다. 따라서 **테이블** 변수 잠금 및 로깅 리소스 덜 필요 합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항
**테이블** 변수 배포 통계, 재컴파일 트리거하지 것입니다. 따라서 대부분의 경우 최적화 프로그램은 테이블 변수에 행이 없다는 가정하에 쿼리 계획을 빌드합니다. 이러한 이유로, 많은 수의 행(100개 이상)을 예상하는 경우 테이블 변수를 사용할 때 주의해야 합니다. 이러한 경우 임시 테이블이 좋은 해결책일 수 있습니다. 또는 테이블 변수를 다른 테이블을 조인 하는 쿼리의 경우 하는 최적화 프로그램이 테이블 변수에 올바른 카디널리티를 사용 하 게 RECOMPILE 힌트를 사용 합니다.
  
**테이블** 변수에서 지원 되지 않습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 최적화 프로그램의 비용 기반 추론 모델입니다. 따라서 효율적인 쿼리 계획을 얻기 위해 비용 기반 선택이 필요한 경우에는 이 변수를 사용하면 안 됩니다. 비용 기반 선택이 필요한 경우에는 임시 테이블이 적절합니다. 여기에는 일반적으로 조인, 병렬 처리 결정 및 인덱스 선택 사항 선택을 사용하는 쿼리가 포함됩니다.
  
쿼리를 수정 하는 **테이블** 변수는 병렬 쿼리 실행 계획을 생성 하지 않습니다. 매우 큰 경우 성능 영향을 받을 수 **테이블** 변수 또는 **테이블** 복잡 한 쿼리의 변수는 수정 됩니다. 이런 상황에서는 임시 테이블을 대신 사용해 보세요. 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요. 읽는 쿼리는 **테이블** 수정 하지 않고도 변수 병렬 처리할 수 있습니다.
  
인덱스를 명시적으로 on으로 만들 수 없습니다 **테이블** 변수와 그 통계에 유지할지 **테이블** 변수입니다. 경우에 따라서는 인덱스와 통계를 지원하는 임시 테이블을 대신 사용하여 성능을 향상시킬 수도 있습니다. 임시 테이블에 대 한 자세한 내용은 참조 [CREATE table&#40; Transact SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).
  
CHECK 제약 조건, 기본값 및 계산된 열에는 **테이블** 형식 선언에서 사용자 정의 함수를 호출할 수 없습니다.
  
간의 할당 작업 **테이블** 변수는 지원 되지 않습니다.
  
때문에 **테이블** 변수는 범위가 제한 및 영구 데이터베이스의 일부가 아닌, 트랜잭션 롤백의 영향을 받지 않습니다.
  
테이블 변수는 생성 후 변경할 수 없습니다.
  
## <a name="examples"></a>예  
  
### <a name="a-declaring-a-variable-of-type-table"></a>1. 테이블 형식의 변수 선언  
다음 예에서는 UPDATE 문의 OUTPUT 절에서 지정된 값을 저장하는 `table` 변수를 만듭니다. 각각 `SELECT`의 값과 `@MyTableVar` 테이블의 업데이트 작업 결과를 반환하는 두 개의 `Employee` 문이 이어집니다. 결과 `INSERTED.ModifiedDate` 열 값에서 다는 `ModifiedDate` 열에는 `Employee` 테이블입니다. 그 이유는 `AFTER UPDATE` 값을 현재 날짜로 업데이트하는 `ModifiedDate` 트리거가 `Employee` 테이블에 정의되어 있기 때문입니다. 그러나 `OUTPUT`에서 반환된 열은 트리거가 실행되기 전의 데이터를 반영합니다. 자세한 내용은 참조 [OUTPUT 절 &#40; Transact SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).
  
```sql
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
  
### <a name="b-creating-an-inline-table-valued-function"></a>2. 인라인 테이블 반환 함수 만들기  
다음 예에서는 인라인 테이블 반환 함수를 반환합니다. 세 개의 열을 반환 `ProductID`, `Name` 및로 대리점 별 연도-날짜까지 총 집계 `YTD Total` 저장소에 판매 된 각 제품에 대 한 합니다.
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```  
  
함수를 호출하려면 이 쿼리를 실행하세요.
  
```sql
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
## <a name="see-also"></a>참고 항목
[COLLATE &#40; Transact SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
[사용자 정의 함수](../../relational-databases/user-defined-functions/user-defined-functions.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[테이블 반환 매개 변수 사용 &#40; 데이터베이스 엔진 &#41;를 사용 하 여](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
[쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)
  
  

