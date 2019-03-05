---
title: 테이블 값 생성자(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- inserting multiple rows
- row value expression
- row constructor [SQL Server]
- table value constructor [SQL Server]
ms.assetid: e57cd31d-140e-422f-8178-2761c27b9deb
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 03ae3b2808fbca63c92ee689218c6e76cb0c0ffd
ms.sourcegitcommit: 670082cb47f7d3d82e987b549b6f8e3a8968b5db
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57334480"
---
# <a name="table-value-constructor-transact-sql"></a>테이블 값 생성자(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  테이블에 생성할 행 값 식의 집합을 지정합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 테이블 값 생성자를 사용하면 단일 DML  문에 여러 데이터 행을 지정할 수 있습니다. INSERT 문의 VALUES 절, MERGE 문의 USING \<source table> 절 및 FROM 절의 파생 테이블 정의에 테이블 값 생성자를 지정할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
VALUES ( <row value expression list> ) [ ,...n ]   
  
<row value expression list> ::=  
    {<row value expression> } [ ,...n ]  
  
<row value expression> ::=  
    { DEFAULT | NULL | expression }  
```  
  
## <a name="arguments"></a>인수  
 VALUES  
 행 값 식 목록을 나타냅니다. 각 목록은 괄호로 묶고 쉼표로 구분해야 합니다.  
  
 각 목록에는 같은 수의 값을 지정해야 하고 이러한 값의 순서는 테이블의 열 순서와 같아야 합니다. 테이블의 각 열에 대해 값을 지정하거나,  들어오는 각 값을 위한 열을 열 목록에서 명시적으로 지정해야 합니다.  
  
 DEFAULT  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 열에 대해 정의된 기본값을 삽입하도록 설정합니다. 열에 대한 기본값이 없고 열에 Null  값을 사용할 수 있는 경우에는 NULL이 삽입됩니다. ID  열에는 DEFAULT를 사용할 수 없습니다. 테이블 값 생성자에 지정되는 경우 INSERT  문에만 DEFAULT를 사용할 수 있습니다.  
  
 *expression*  
 상수,  변수 또는 식입니다. 식은 EXECUTE  문을 포함할 수 없습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 테이블 값 생성자는 다음 두 가지 방법 중 하나로 사용할 수 있습니다. 즉, INSERT ... VALUES 문의 VALUES 목록에서 직접 사용하거나, 파생 테이블이 허용되는 모든 위치에서 파생 테이블로 사용합니다. 행 수가 최대값을 초과하면 오류 10738이 반환됩니다. 제한에서 허용하는 것보다 많은 행을 삽입하려면 다음 방법 중 하나를 사용합니다.  
  
-   다중 INSERT  문 만들기  
  
-   파생 테이블 사용  
  
-   **bcp** 유틸리티 또는 BULK INSERT 문을 사용하여 데이터를 대량 가져오기  
  
 단일 스칼라 값만 행 값 식으로 사용할 수 있습니다. 여러 열을 포함하는 하위 쿼리는 행 값 식으로 사용할 수 없습니다. 예를 들어 다음 코드에서는 세 번째 행 값 식 목록에 여러 열을 포함하는 하위 쿼리가 있으므로 구문 오류가 발생합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.MyProducts (Name varchar(50), ListPrice money);  
GO  
-- This statement fails because the third values list contains multiple columns in the subquery.  
INSERT INTO dbo.MyProducts (Name, ListPrice)  
VALUES ('Helmet', 25.50),  
       ('Wheel', 30.00),  
       (SELECT Name, ListPrice FROM Production.Product WHERE ProductID = 720);  
GO  
  
```  
  
 하지만 하위 쿼리에서 각 열이 개별적으로 지정되도록 문을 다시 작성할 수 있습니다. 다음 예에서는 세 개의 행을 `MyProducts` 테이블에 삽입합니다.  
  
```  
INSERT INTO dbo.MyProducts (Name, ListPrice)  
VALUES ('Helmet', 25.50),  
       ('Wheel', 30.00),  
       ((SELECT Name FROM Production.Product WHERE ProductID = 720),  
        (SELECT ListPrice FROM Production.Product WHERE ProductID = 720));  
GO  
  
```  
  
## <a name="data-types"></a>데이터 형식  
 다중 행 INSERT  문에 지정되는 값은 UNION  ALL  구문의 데이터 형식 변환 속성에 따릅니다. 그 결과 일치하지 않는 형식은 [우선 순위](../../t-sql/data-types/data-type-precedence-transact-sql.md)가 높은 형식으로 암시적으로 변환됩니다. 이때 변환이 암시적으로 지원되지 않으면 오류가 반환됩니다. 예를 들어 다음 명령문은 **char** 형식의 열에 정수 값과 문자 값을 하나씩 삽입합니다.  
  
```  
CREATE TABLE dbo.t (a int, b char);  
GO  
INSERT INTO dbo.t VALUES (1,'a'), (2, 1);  
GO  
```  
  
 데이터 형식 우선 순위에 따르면 정수가 문자보다 우선 순위가 높은 형식이므로 INSERT  문이 실행되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 'a'를 정수로 변환하려고 합니다. 이 변환은 실패하고 오류가 반환됩니다. 이 오류는 값을 명시적으로 적절하게 변환하면 피할 수 있습니다. 예를 들어 위의 문을 다음과 같이 작성할 수 있습니다.  
  
```  
INSERT INTO dbo.t VALUES (1,'a'), (2, CONVERT(CHAR,1));  
```  
  
## <a name="examples"></a>예  
  
### <a name="a-inserting-multiple-rows-of-data"></a>1. 여러 데이터 행 삽입  
 다음 예에서는 `dbo.Departments` 테이블을 만든 다음 테이블 값 생성자를 사용하여 이 테이블에 5개의 행을 삽입합니다. 모든 열에 대한 값이 제공되어 있고 값이 테이블 내의 열과 같은 순서로 나열되어 있기 때문에 열 목록에 열 이름을 지정할 필요가 없습니다.  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT2', N'Square Feet ', '20080923'), (N'Y', N'Yards', '20080923'), (N'Y3', N'Cubic Yards', '20080923');  
GO  
  
```  
  
### <a name="b-inserting-multiple-rows-with-default-and-null-values"></a>2. DEFAULT 및 NULL 값을 사용하여 여러 행 삽입  
 다음 예에서는 테이블 값 생성자를 사용하여 테이블에 행을 삽입할 때 DEFAULT  및 NULL을 지정하는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE Sales.MySalesReason(  
SalesReasonID int IDENTITY(1,1) NOT NULL,  
Name dbo.Name NULL ,  
ReasonType dbo.Name NOT NULL DEFAULT 'Not Applicable' );  
GO  
INSERT INTO Sales.MySalesReason   
VALUES ('Recommendation','Other'), ('Advertisement', DEFAULT), (NULL, 'Promotion');  
  
SELECT * FROM Sales.MySalesReason;  
  
```  
  
### <a name="c-specifying-multiple-values-as-a-derived-table-in-a-from-clause"></a>C. FROM 절에 여러 값을 파생 테이블로 지정  
 다음 예에서는 테이블 값 생성자를 사용하여 SELECT 문의 FROM 절에 여러 값을 지정합니다.  
  
```  
SELECT a, b FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);  
GO  
-- Used in an inner join to specify values to return.  
SELECT ProductID, a.Name, Color  
FROM Production.Product AS a  
INNER JOIN (VALUES ('Blade'), ('Crown Race'), ('AWC Logo Cap')) AS b(Name)   
ON a.Name = b.Name;  
  
```  
  
### <a name="d-specifying-multiple-values-as-a-derived-source-table-in-a-merge-statement"></a>D. MERGE 문에 여러 값을 파생 원본 테이블로 지정  
 다음 예에서는 MERGE를 사용하여 행을 업데이트하거나 삽입하는 방식으로 `SalesReason` 테이블을 수정합니다. 원본 테이블의 `NewName` 값이 대상 테이블 `Name`의 `SalesReason` 열에 있는 값과 일치하는 경우 대상 테이블에서 `ReasonType` 열이 업데이트됩니다. `NewName` 값이 일치하지 않으면 원본 행이 대상 테이블에 삽입됩니다. 원본 테이블은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 테이블 값 생성자를 사용하여 원본 테이블의 여러 행을 지정하는 파생 테이블입니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), ('Internet', 'Promotion'))  
       AS Source (NewName, NewReasonType)  
ON Target.Name = Source.NewName  
WHEN MATCHED THEN  
UPDATE SET ReasonType = Source.NewReasonType  
WHEN NOT MATCHED BY TARGET THEN  
INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)  
OUTPUT $action INTO @SummaryOfChanges;  
  
-- Query the results of the table variable.  
SELECT Change, COUNT(*) AS CountPerChange  
FROM @SummaryOfChanges  
GROUP BY Change;  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [MERGE&#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  
