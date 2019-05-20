---
title: IntelliSense에서 지원되는 Transact-SQL 구문 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- Transact-SQL IntelliSense
- IntelliSense [SQL Server], Transact-SQL syntax
ms.assetid: 194e8f4f-fd7e-4f32-a169-f23531128004
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 40a73c7b741ec4ac5ce624bce3f0a36fe573eda2
ms.sourcegitcommit: c29150492383f48ef484fa02a483cde1cbc68aca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65821601"
---
# <a name="transact-sql-syntax-supported-by-intellisense"></a>IntelliSense에서 지원되는 Transact-SQL 구문
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  이 항목에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 의 IntelliSense에서 지원하는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]문 및 구문 요소에 대해 설명합니다.  
  
## <a name="statements-supported-by-intellisense"></a>IntelliSense에서 지원하는 문  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 IntelliSense는 가장 일반적으로 사용되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문만 지원합니다. 일부 일반적인 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 조건으로 인해 IntelliSense가 제대로 작동하지 않을 수 있습니다. 자세한 내용은 [IntelliSense 문제 해결&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/troubleshooting-intellisense.md)을 참조하세요.  
  
> [!NOTE]  
>  암호화된 저장 프로시저 또는 사용자 정의 함수와 같이 암호화된 데이터베이스 개체에 대해 IntelliSense를 사용할 수 없습니다. 확장 저장 프로시저 및 CLR 통합 사용자 정의 유형의 매개 변수에 대해 매개 변수 도움말 및 요약 정보를 사용할 수 없습니다.  
  
### <a name="select-statement"></a>SELECT 문  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서는 SELECT 문의 다음 구문 요소에 대한 IntelliSense 지원을 제공합니다.  
  
|||  
|-|-|  
|SELECT|WHERE|  
|FROM|ORDER BY|  
|HAVING|UNION|  
|FOR|GROUP BY|  
|맨 위로 이동|OPTION (hint)|  
  
### <a name="additional-transact-sql-statements-that-are-supported"></a>지원되는 추가 Transact-SQL 문  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서는 다음 표에 표시된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 대한 IntelliSense 지원도 제공합니다.  
  
|Transact-SQL 문|지원되는 구문|예외|  
|-----------------------------|----------------------|----------------|  
|[INSERT](../../t-sql/statements/insert-transact-sql.md)|*execute_statement* 절을 제외한 모든 구문|없음|  
|[UPDATE](../../t-sql/queries/update-transact-sql.md)|모든 구문|없음|  
|[DELETE](../../t-sql/statements/delete-transact-sql.md)|모든 구문|없음|  
|[DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)|모든 구문|없음|  
|[SET @local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md)|모든 구문|없음|  
|[EXECUTE](../../t-sql/language-elements/execute-transact-sql.md)|사용자 정의 저장 프로시저, 시스템 저장 프로시저, 사용자 정의 함수 및 시스템 함수 실행|없음|  
|[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)|모든 구문|없음|  
|[CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)|모든 구문|없음|  
|[CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)|모든 구문|EXTERNAL NAME 절에 대한 IntelliSense 지원은 없습니다.<br /><br /> AS 절에서 IntelliSense는 이 항목에 나열된 문과 구문만 지원합니다.|  
|[ALTER PROCEDURE](../../t-sql/statements/alter-procedure-transact-sql.md)|모든 구문|EXTERNAL NAME 절에 대한 IntelliSense 지원은 없습니다.<br /><br /> AS 절에서 IntelliSense는 이 항목에 나열된 문과 구문만 지원합니다.|  
|[USE](../../t-sql/language-elements/use-transact-sql.md)|모든 구문|없음|  
  
## <a name="intellisense-in-supported-statements"></a>지원되는 문의 IntelliSense  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기의 IntelliSense는 지원되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 중 하나에서 사용되는 경우 다음 구문 요소를 지원합니다.  
  
-   APPLY를 비롯한 모든 조인 유형  
  
-   PIVOT 및 UNPIVOT  
  
-   다음 데이터베이스 개체에 대한 참조  
  
    -   데이터베이스 및 스키마  
  
    -   테이블, 뷰, 테이블 반환 함수 및 테이블 식  
  
    -   열  
  
    -   프로시저 및 프로시저 매개 변수  
  
    -   스칼라 함수 및 스칼라 식  
  
    -   지역 변수  
  
    -   CTE(공통 테이블 식)  
  
-   스크립트나 일괄 처리에 있는 CREATE 또는 ALTER 문에서만 참조되지만 스크립트나 일괄 처리를 아직 실행하지 않았기 때문에 데이터베이스에 없는 데이터베이스 개체. 이러한 개체는 다음과 같습니다.  
  
    -   스크립트나 일괄 처리에 있는 CREATE TABLE 또는 CREATE PROCEDURE 문에서 지정한 테이블 및 프로시저  
  
    -   스크립트나 일괄 처리에 있는 ALTER TABLE 또는 ALTER PROCEDURE 문에서 지정한 테이블 및 프로시저에 대한 변경 내용  
  
    > [!NOTE]  
    >  CREATE VIEW 문을 실행할 때까지 CREATE VIEW 문의 열에 대해 IntelliSense를 사용할 수 없습니다.  
  
 앞에서 나열된 요소가 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 사용되는 경우에는 IntelliSense가 제공되지 않습니다. 예를 들어 SELECT 문에서 사용되는 열 이름에 대해서는 IntelliSense가 지원되지만 CREATE FUNCTION 문에서 사용되는 열에 대해서는 IntelliSense가 지원되지 않습니다.  
  
## <a name="examples"></a>예  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트나 일괄 처리 내에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기의 IntelliSense는 이 항목에 나열된 문과 구문만 지원합니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드 예제에서는 IntelliSense에서 지원하는 문 및 구문을 보여 줍니다. 예를 들어 다음 일괄 처리에서 IntelliSense는 `SELECT` 가 `SELECT` 문에 포함되어 있지 않고 자체적으로 코딩된 경우 `CREATE FUNCTION` 문에 대해 사용할 수 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE Name LIKE N'Road-250%' and Color = N'Red';  
GO  
CREATE FUNCTION Production.ufn_Red250 ()  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT Name  
    FROM AdventureWorks2012.Production.Product  
    WHERE Name LIKE N'Road-250%'  
      AND Color = N'Red'  
);GO  
```  
  
 이 기능은 CREATE PROCEDURE 또는 ALTER PROCEDURE 문의 AS 절에 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 집합에도 적용됩니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트나 일괄 처리 내에서 IntelliSense는 CREATE 또는 ALTER 문에서 지정했지만 문을 실행하지 않았기 때문에 데이터베이스에 없는 개체를 지원합니다. 예를 들어 쿼리 편집기에 다음과 같은 코드를 입력할 수 있습니다.  
  
```  
USE MyTestDB;  
GO  
CREATE TABLE MyTable  
    (PrimaryKeyCol   INT PRIMARY KEY,  
    FirstNameCol      NVARCHAR(50),  
   LastNameCol       NVARCHAR(50));  
GO  
SELECT   
```  
  
 `SELECT`를 입력하면 스크립트를 실행하지 않아 **이**에 아직 없더라도 IntelliSense는 SELECT 목록에 **PrimaryKeyCol**, **FirstNameCol** 및 `MyTable` LastNameCol `MyTestDB`을 사용 가능한 요소로 나열합니다.  
  
  
