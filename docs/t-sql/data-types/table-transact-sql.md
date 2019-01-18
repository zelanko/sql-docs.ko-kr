---
title: 테이블(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table data type [SQL Server]
- table variables [SQL Server]
ms.assetid: 1ef0b60e-a64c-4e97-847b-67930e3973ef
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0f61e3417e44fad0ce25796e5e888bcfc2781206
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204282"
---
# <a name="table-transact-sql"></a>table(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

나중에 처리하기 위해 결과 집합을 저장하는 데 사용할 수 있는 특별한 데이터 형식입니다. **테이블**은 주로 테이블 반환 함수의 결과 집합으로 반환되는 행 집합을 임시로 저장하는 데 사용됩니다. **테이블**은 주로 테이블 반환 함수의 결과 집합으로 반환되는 행 집합을 임시로 저장하는 데 사용됩니다. **테이블** 변수는 함수, 저장 프로시저 및 일괄 처리에 사용할 수 있습니다. **테이블** 유형의 변수를 선언하려면 [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)를 사용합니다.
  

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
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
구문에 대한 자세한 내용은 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md), [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md) 및 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)을 참조하세요.
  
*collation_definition*  
[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 로캘 및 비교 스타일, Windows 로캘 및 이진 표기법 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬로 구성된 열의 데이터 정렬입니다. *collation_definition*을 지정하지 않으면 현재 데이터베이스의 데이터 정렬이 해당 열에 상속됩니다. 또는 CLR(공용 언어 런타임) 사용자 정의 형식으로 열을 정의할 경우 사용자 정의 형식의 데이터 정렬이 해당 열에 상속됩니다.
  
## <a name="remarks"></a>Remarks  
다음 예에서와 같이 일괄 처리의 FROM 절에서 이름으로 **테이블** 변수를 참조할 수 있습니다.
  
```sql
SELECT Employee_ID, Department_ID FROM @MyTableVar;  
```  
  
FROM 절 밖에서는 다음 예에서와 같이 별칭을 사용하여 **테이블** 변수를 참조해야 합니다.
  
```sql
SELECT EmployeeID, DepartmentID   
FROM @MyTableVar m  
JOIN Employee on (m.EmployeeID =Employee.EmployeeID AND  
   m.DepartmentID = Employee.DepartmentID);  
```  
  
**테이블** 변수는 변경되지 않는 쿼리 계획이 있는 소규모 쿼리의 경우와 다시 컴파일 기능이 중요한 경우에 다음과 같은 이점을 제공합니다.
-   **테이블** 변수는 지역 변수처럼 작동하며 잘 정의된 범위를 가집니다. 범위는 변수가 선언된 함수, 저장 프로시저 또는 일괄 처리입니다.  
     범위 내에서 일반 테이블처럼 **테이블** 변수를 사용할 수 있으며 SELECT, INSERT, UPDATE 및 DELETE 문에서 테이블 또는 테이블 식이 사용되는 어디에나 적용할 수 있습니다. 그러나 다음 명령문에서는 **테이블**을 사용할 수 없습니다.  
  
```sql
SELECT select_list INTO table_variable;
```
  
**테이블** 변수는 자신이 정의된 함수, 저장 프로시저 및 일괄 처리가 끝나면 자동으로 정리됩니다.
  
-   저장 프로시저에 **테이블** 변수를 사용하면 성능에 영향을 주는 비용 기반 선택 사항이 없는 경우 임시 테이블을 사용할 때보다 저장 프로시저를 다시 컴파일하는 횟수가 줄어듭니다.  
-   **테이블** 변수와 관련된 트랜잭션은 **테이블** 변수가 업데이트되는 동안만 지속됩니다. 따라서 **테이블** 변수를 사용하면 리소스의 잠금과 로깅에 대한 요구가 줄어듭니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항
**테이블** 변수에는 배포 통계가 없으며 이 변수는 다시 컴파일을 트리거하지 않습니다. 따라서 대부분의 경우 최적화 프로그램은 테이블 변수에 행이 없다는 가정하에 쿼리 계획을 빌드합니다. 이러한 이유로, 많은 수의 행(100개 이상)을 예상하는 경우 테이블 변수를 사용할 때 주의해야 합니다. 이러한 경우 임시 테이블이 좋은 해결책일 수 있습니다. 또는 테이블 변수를 다른 테이블에 조인하는 쿼리의 경우 RECOMPILE 힌트를 사용하세요. 그러면 최적화 프로그램이 테이블 변수에 올바른 카디널리티를 사용합니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 최적화 프로그램의 비용 기반 추론 모델에서는 **테이블** 변수가 지원되지 않습니다. 따라서 효율적인 쿼리 계획을 얻기 위해 비용 기반 선택이 필요한 경우에는 이 변수를 사용하면 안 됩니다. 비용 기반 선택이 필요한 경우에는 임시 테이블이 적절합니다. 여기에는 일반적으로 조인, 병렬 처리 결정 및 인덱스 선택 사항 선택을 사용하는 쿼리가 포함됩니다.
  
**테이블** 변수를 수정하는 쿼리는 병렬 쿼리 실행 계획을 생성하지 않습니다. 매우 큰 **테이블** 변수나 복잡한 쿼리의 **테이블** 변수를 수정하면 성능에 영향을 줄 수 있습니다. 이런 상황에서는 임시 테이블을 대신 사용해 보세요. 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요. 수정하지 않고 **테이블** 변수를 읽는 쿼리는 병렬 처리할 수 있습니다.
  
명시적으로 **테이블** 변수에 대한 인덱스를 만들 수 없으며 **테이블** 변수에 대한 통계는 유지되지 않습니다. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터, 테이블 정의와 함께 특정 인덱스 유형을 인라인으로 만들 수 있는 새 구문이 도입되었습니다.  이 새 구문을 사용하여 테이블 정의의 일부로 **테이블** 변수의 인덱스를 만들 수 있습니다. 경우에 따라 전체 인덱스 지원과 통계를 제공하는 임시 테이블을 대신 사용하여 성능을 향상할 수도 있습니다. 임시 테이블 및 인라인 인덱스 만들기에 대한 자세한 내용은 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.

**테이블** 형식 선언 내의 CHECK 제약 조건, DEFAULT 값 및 계산 열은 사용자 정의 함수를 호출할 수 없습니다.
  
**테이블** 변수 간의 할당 작업은 지원되지 않습니다.
  
**테이블** 변수는 제한된 범위를 가지며 영구 데이터베이스의 일부가 아니므로 트랜잭션 롤백의 영향을 받지 않습니다.
  
테이블 변수는 생성 후 변경할 수 없습니다.

## <a name="table-variable-deferred-compilation"></a>테이블 변수 지연 컴파일
**테이블 변수 지연 컴파일**은 테이블 변수를 참조하는 쿼리의 플랜 품질 및 전체 성능을 개선합니다. 최적화 및 초기 플랜 컴파일 중에 이 기능은 실제 테이블 변수 행 수를 기반으로 하는 카디널리티 예측을 전파합니다. 이 정확한 행 수 정보는 다운스트림 플랜 작업을 최적화하는 데 사용됩니다.

> [!NOTE]
> 테이블 변수 지연 컴파일은 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 및 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]의 공개 미리 보기 기능입니다.

테이블 변수 지연 컴파일을 사용하면 테이블 변수를 참조하는 문 컴파일은 문이 실제로 처음 실행될 때까지 지연됩니다. 이 지연 컴파일 동작은 임시 테이블의 동작과 동일하고, 이 변경으로 인해 원래 1행 추측 대신에 실제 카디널리티가 사용됩니다. 

테이블 변수 지연 컴파일의 공개 미리 보기를 사용하도록 설정하려면 쿼리를 실행할 때 연결된 데이터베이스의 데이터베이스 호환성 수준 150을 사용하도록 설정합니다.

테이블 변수 지연 컴파일은 테이블 변수의 다른 특성을 변경하지 **않습니다**. 예를 들어,이 기능은 테이블 변수에 열 통계를 추가하지 않습니다.

테이블 변수 지연 컴파일은 **다시 컴파일 빈도를 늘리지 않습니다**.  대신 초기 컴파일이 발생하는 위치를 이동합니다. 결과 캐시된 플랜은 초기 지연 컴파일 테이블 변수 행 개수를 기반으로 생성됩니다. 플랜이 제거되거나 다시 컴파일될 때까지 캐시된 플랜은 연속 쿼리에서 다시 사용됩니다. 

초기 플랜 컴파일에 사용되는 테이블 변수 행 개수가 고정된 행 개수 추측과 상당히 다른 일반적인 값을 나타내는 경우, 다운스트림 작업에 도움이 됩니다.  테이블 변수 행 개수가 실행 간에 크게 달라지는 경우, 이 기능으로 성능이 향상되지 않을 수 있습니다.

### <a name="disabling-table-variable-deferred-compilation-without-changing-the-compatibility-level"></a>호환성 수준을 변경하지 않고 테이블 변수 지연 컴파일 비활성화
데이터베이스 호환성 수준 150 이상을 유지하면서 데이터베이스 또는 명령문 범위에서 테이블 변수 지연 컴파일을 비활성화할 수 있습니다. 데이터베이스에서 발생하는 모든 쿼리 실행에 대한 테이블 변수 지연 컴파일을 비활성화하려면 해당 데이터베이스의 컨텍스트 내에서 다음을 실행합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DEFERRED_COMPILATION_TV = OFF;
```

데이터베이스에서 발생하는 모든 쿼리 실행에 대한 테이블 변수 지연 컴파일을 다시 활성화하려면 해당 데이터베이스의 컨텍스트 내에서 다음을 실행합니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DEFERRED_COMPILATION_TV = ON;
```

DISABLE_DEFERRED_COMPILATION_TV를 USE HINT 쿼리 힌트로 지정하여 특정 쿼리에 대한 테이블 변수 지연 컴파일을 비활성화할 수도 있습니다.  예를 들어 다음과 같이 사용할 수 있습니다.

```sql
DECLARE @LINEITEMS TABLE 
    (L_OrderKey INT NOT NULL,
     L_Quantity INT NOT NULL
    );

INSERT @LINEITEMS
SELECT L_OrderKey, L_Quantity
FROM dbo.lineitem
WHERE L_Quantity = 5;

SELECT  O_OrderKey,
    O_CustKey,
    O_OrderStatus,
    L_QUANTITY
FROM    
    ORDERS,
    @LINEITEMS
WHERE   O_ORDERKEY  =   L_ORDERKEY
    AND O_OrderStatus = 'O'
OPTION (USE HINT('DISABLE_DEFERRED_COMPILATION_TV'));
```

  
## <a name="examples"></a>예  
  
### <a name="a-declaring-a-variable-of-type-table"></a>1. 테이블 형식의 변수 선언  
다음 예에서는 UPDATE 문의 OUTPUT 절에서 지정된 값을 저장하는 `table` 변수를 만듭니다. 각각 `SELECT`의 값과 `@MyTableVar` 테이블의 업데이트 작업 결과를 반환하는 두 개의 `Employee` 문이 이어집니다. `INSERTED.ModifiedDate` 열의 결과 값은 `Employee` 테이블의 `ModifiedDate` 열 값과 다릅니다. 그 이유는 `AFTER UPDATE` 값을 현재 날짜로 업데이트하는 `ModifiedDate` 트리거가 `Employee` 테이블에 정의되어 있기 때문입니다. 그러나 `OUTPUT`에서 반환된 열은 트리거가 실행되기 전의 데이터를 반영합니다. 자세한 내용은 [OUTPUT Clause&#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)를 참조하세요.
  
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
다음 예에서는 인라인 테이블 반환 함수를 반환합니다. `ProductID` 열, `Name` 열, 그리고 대리점에 판매된 각 제품에 대한 대리점별 총 연간 매출의 집계를 `YTD Total` 열로 반환합니다.
  
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
  
## <a name="see-also"></a>관련 항목:
[COLLATE&#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
[사용자 정의 함수](../../relational-databases/user-defined-functions/user-defined-functions.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[테이블 반환 매개 변수 사용&#40;Database Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
[쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)
