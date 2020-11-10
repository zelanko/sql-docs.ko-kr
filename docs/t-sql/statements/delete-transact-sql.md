---
description: DELETE (Transact-SQL)
title: DELETE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/19/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DELETE
- DELETE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row removal [SQL Server]
- DELETE statement [SQL Server], about DELETE statement
- views [SQL Server], deleting rows
- removing rows
- tables [SQL Server], deleting rows
- DELETE statement [SQL Server]
- deleting rows
- row removal [SQL Server], DELETE statement
- deleting data
ms.assetid: ed6b2105-0f35-408f-ba51-e36ade7ad5b2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7e074f54cb4d31616abced2e0b555c068728ec6c
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384825"
---
# <a name="delete-transact-sql"></a>DELETE (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 테이블 또는 뷰에서 하나 이상의 행을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
[ WITH <common_table_expression> [ ,...n ] ]  
DELETE   
    [ TOP ( expression ) [ PERCENT ] ]   
    [ FROM ]   
    { { table_alias  
      | <object>   
      | rowset_function_limited   
      [ WITH ( table_hint_limited [ ...n ] ) ] }   
      | @table_variable  
    }  
    [ <OUTPUT Clause> ]  
    [ FROM table_source [ ,...n ] ]   
    [ WHERE { <search_condition>   
            | { [ CURRENT OF   
                   { { [ GLOBAL ] cursor_name }   
                       | cursor_variable_name   
                   }   
                ]  
              }  
            }   
    ]   
    [ OPTION ( <Query Hint> [ ,...n ] ) ]   
[; ]  
  
<object> ::=  
{   
    [ server_name.database_name.schema_name.   
      | database_name. [ schema_name ] .   
      | schema_name.  
    ]  
    table_or_view_name   
}  
```  
  
```syntaxsql
-- Syntax for Azure Synapse Analytics

[ WITH <common_table_expression> [ ,...n ] ] 
DELETE [database_name . [ schema ] . | schema. ] table_name  
FROM [database_name . [ schema ] . | schema. ] table_name 
JOIN {<join_table_source>}[ ,...n ]  
ON <join_condition>
[ WHERE <search_condition> ]   
[ OPTION ( <query_options> [ ,...n ]  ) ]  
[; ]  

<join_table_source> ::=   
{  
    [ database_name . [ schema_name ] . | schema_name . ] table_or_view_name [ AS ] table_or_view_alias 
    [ <tablesample_clause>]  
    | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]  
}  
```

```syntaxsql
-- Syntax for Parallel Data Warehouse  
  
DELETE 
    [ FROM [database_name . [ schema ] . | schema. ] table_name ]   
    [ WHERE <search_condition> ]   
    [ OPTION ( <query_options> [ ,...n ]  ) ]  
[; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 WITH \<common_table_expression>  
 DELETE 문 범위 내에 정의되고 공통 테이블 식이라고도 하는 명명된 임시 결과 집합을 지정합니다. 결과 집합은 SELECT 문에서 파생됩니다.  
  
 공통 테이블 식은 SELECT, INSERT, UPDATE 및 CREATE VIEW 문과 함께 사용될 수도 있습니다. 자세한 내용은 [WITH common_table_expression&#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)을 참조하세요.  
  
 TOP **(** _expression_ **)** [ PERCENT ]  
 삭제될 임의 행의 개수 또는 백분율(%)을 지정합니다. *expression* 은 행의 수 또는 비율일 수 있습니다. INSERT, UPDATE 또는 DELETE와 함께 사용된 TOP 식에서 참조된 행은 어떠한 순서로도 정렬되지 않습니다. 자세한 내용은 [TOP&#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)을 참조하세요.  
  
 FROM  
 DELETE 키워드와 대상 *table_or_view_name* 또한 *rowset_function_limited* 사이에서 선택적으로 사용할 수 있는 키워드입니다.  
  
 *table_alias*  
 행을 삭제할 테이블 또는 뷰를 나타내는 FROM *table_source* 절에 지정되는 별칭입니다.  
  
 *server_name*  
 **적용 대상** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 테이블이나 뷰가 위치한 서버의 이름입니다. 연결된 서버 이름 또는 [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) 함수를 서버 이름으로 사용합니다. *server_name* 이 지정되면 *database_name* 과 *schema_name* 이 필요합니다.  
  
 *database_name*  
 데이터베이스의 이름입니다.  
  
 *schema_name*  
 테이블이나 뷰가 속한 스키마의 이름입니다.  
  
 *table_or_view_name*  
 행을 제거할 테이블 또는 뷰의 이름입니다.  
  
 테이블 변수는 해당 범위 내에서 DELETE 문의 테이블 원본으로도 사용될 수 있습니다.  
  
 *table_or_view_name* 에서 참조되는 뷰는 업데이트가 가능해야 하며 해당 뷰 정의의 FROM 절에서 정확히 하나의 기본 테이블을 참조해야 합니다. 업데이트할 수 있는 뷰에 대한 자세한 내용은 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)를 참조하세요.  
  
 *rowset_function_limited*  
 **적용 대상** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 공급자 기능에 관련된 [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) 또는 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 함수입니다.  
  
 WITH **(** \<table_hint_limited> [... *n* ] **)**  
 대상 테이블에 허용되는 하나 이상의 테이블 힌트를 지정합니다. WITH 키워드와 괄호가 필요합니다. NOLOCK 및 READUNCOMMITTED는 허용되지 않습니다. 테이블 힌트에 대한 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
 \<OUTPUT_Clause>  
 삭제된 행 또는 삭제된 행 기반의 식을 DELETE 작업의 일부로 반환합니다. OUTPUT 절은 뷰나 원격 테이블을 대상으로 하는 모든 DML 문에서 지원되지 않습니다. 이 절의 인수 및 동작에 대한 자세한 내용은 [OUTPUT Clause &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)을 참조하세요.  
  
 FROM *table_source*  
 FROM 절을 추가로 지정합니다. DELETE에 대한 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 확장을 사용하여 \<table_source>의 데이터를 지정하고 첫 번째 FROM 절에 있는 테이블에서 해당 행을 삭제할 수 있습니다.  
  
 조인을 지정하는 이 확장을 WHERE 절에서 하위 쿼리 대신 사용하여 제거될 행을 식별할 수 있습니다.  
  
 자세한 내용은 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)을 참조하세요.  
  
 WHERE  
 삭제될 행의 개수를 제한하는 조건을 지정합니다. WHERE 절을 지정하지 않으면 DELETE는 테이블의 모든 행을 제거합니다.  
  
 WHERE 절에 지정된 내용에 따라 두 가지 형식의 삭제 작업이 있습니다.  
  
-   검색 결과 삭제는 삭제할 행을 한정하는 검색 조건을 지정합니다. 예를 들어,WHERE *column_name* = *값*.  
  
-   위치 지정 삭제는 커서를 지정하는 CURRENT OF 절을 사용합니다. 이 경우 커서의 현재 위치에서 삭제 작업이 발생합니다. 이것은 WHERE *search_condition* 절을 사용하여 삭제될 행을 한정하는 검색 결과 DELETE 문보다 정확한 방법입니다. 검색 결과 DELETE 문은 검색 조건이 한 행을 고유하게 식별하지 못할 경우 여러 행을 삭제할 수 있습니다.  
  
\<search_condition>  
 삭제될 행을 제한하는 조건을 지정합니다. 검색 조건에 포함시킬 수 있는 조건자의 개수에는 제한이 없습니다. 자세한 내용은 [검색 조건&#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)을 참조하세요.  
  
 CURRENT OF  
 지정한 커서의 현재 위치에서 DELETE가 수행되도록 지정합니다.  
  
 GLOBAL  
 *cursor_name* 이 전역 커서를 참조하도록 지정합니다.  
  
 *cursor_name*  
 인출이 수행되는 열린 커서의 이름입니다. 이름이 *cursor_name* 인 전역 커서와 로컬 커서가 모두 있는 경우 이 인수는 GLOBAL이 지정되면 전역 커서를 참조하고, 그렇지 않으면 로컬 커서를 참조합니다. 커서는 업데이트될 수 있어야 합니다.  
  
 *cursor_variable_name*  
 커서 변수의 이름입니다. 커서 변수는 업데이트를 허용하는 커서를 참조해야 합니다.  
  
 OPTION **(** \<query_hint> [ **,** ... *n* ] **)**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 최적화 프로그램 힌트를 사용하여 문을 처리하는 방법을 사용자 지정한다는 것을 나타내는 키워드입니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
## <a name="best-practices"></a>모범 사례  
 테이블의 모든 행을 삭제하려면 TRUNCATE TABLE을 사용합니다. TRUNCATE TABLE은 DELETE보다 더 빠르고 시스템 및 트랜잭션 로그 리소스를 더 적게 사용합니다. TRUNCATE TABLE은 테이블이 복제에 참여할 수 없는 등의 제한 사항이 있습니다. 자세한 내용은 [TRUNCATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/truncate-table-transact-sql.md)을 참조하세요.  
  
 @@ROWCOUNT 함수를 사용하여 클라이언트 애플리케이션에 삭제된 행의 수를 반환할 수 있습니다. 자세한 내용은 [@@ROWCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)을 참조하세요.  
  
## <a name="error-handling"></a>오류 처리  
 TRY…CATCH 구문에 명령문을 지정하여 DELETE 문에 대한 오류 처리를 구현할 수 있습니다.  
  
 DELETE 문이 트리거를 위반하거나 FOREIGN KEY 제약 조건이 있는 다른 테이블의 데이터에 의해 참조되는 행을 제거하려고 하면 DELETE 문은 실패할 수 있습니다. DELETE가 여러 행을 제거하는 경우 제거되는 행 중 하나가 트리거 또는 제약 조건을 위반하면 이 문이 취소되고 오류가 반환되며 행이 제거되지 않습니다.  
  
 식 계산 중 DELETE 문에서 산술 오류(오버플로, 0으로 나누기, 도메인 오류 등)가 발생하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 SET ARITHABORT가 ON으로 설정된 것처럼 이러한 오류를 처리합니다. 나머지 일괄 처리가 취소되고 오류 메시지가 반환됩니다.  
  
## <a name="interoperability"></a>상호 운용성  
 수정할 개체가 테이블 변수인 경우 사용자 정의 함수의 본문에 DELETE를 사용할 수 있습니다.  
  
 FILESTREAM 열이 있는 행을 삭제하면 해당 내부 파일 시스템 파일도 삭제됩니다. 기본 파일은 FILESTREAM 가비지 수집기를 통해 제거됩니다. 자세한 내용은 [Access FILESTREAM Data with Transact-SQL](../../relational-databases/blob/access-filestream-data-with-transact-sql.md)을 참조하세요.  
  
 INSTEAD OF 트리거가 정의된 뷰를 직접 또는 간접으로 참조하는 DELETE 문에 FROM 절을 지정할 수 없습니다. INSTEAD OF 트리거에 대한 자세한 내용은 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)를 참조하세요.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 TOP을 DELETE와 함께 사용할 경우 참조된 행은 어떠한 순서로도 정렬되지 않으며 ORDER BY 절을 이 문에서 직접 지정할 수 없습니다. TOP을 사용하여 시간 순서로 행을 삭제해야 하는 경우에는 하위 SELECT 문에서 ORDER BY 절을 지정하는 방식으로 TOP을 사용해야 합니다. 이 항목의 뒷부분에 나오는 예 섹션을 참조하세요.  
  
 TOP은 분할된 뷰에서 DELETE 문에 사용할 수 없습니다.  
  
## <a name="locking-behavior"></a>잠금 동작  
 기본적으로 DELETE 문은 항상, 수정하는 테이블 개체에 대해 IX(의도 배타) 잠금을 획득하고 해당 트랜잭션이 완료될 때까지 이 잠금을 보유합니다. IX(의도 배타) 잠금을 사용하면 다른 트랜잭션이 데이터를 수정할 수 없습니다. NOLOCK 힌트 또는 READ UNCOMMITED 격리 수준을 사용하여 읽기 작업만 가능합니다. 테이블 힌트를 지정해 다른 잠금 방법을 지정하여 DELETE 문의 기간에 이 기본 동작을 재정의할 수 있지만, 숙련된 개발자 및 데이터베이스 관리자가 최후의 수단으로만 힌트를 사용하시기 바랍니다. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
 힙에서 행을 삭제할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 작업에 대해 행 또는 페이지 잠금을 사용할 수 있습니다. 이 경우 삭제 작업에서 비운 페이지가 힙에 할당된 상태로 남아 있습니다. 빈 페이지의 할당이 취소되지 않으면 데이터베이스의 다른 개체가 해당 공간을 다시 사용할 수 없습니다.  
  
 힙에서 행을 삭제하고 페이지 할당을 취소하려면 다음 방법 중 하나를 사용하세요.  
  
-   DELETE 문에 TABLOCK 힌트를 지정합니다. TABLOCK 힌트를 사용하면 삭제 작업이 행 또는 페이지 잠금 대신 배타적 잠금을 수행하므로 페이지 할당을 취소할 수 있습니다. TABLOCK 힌트에 대한 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
-   테이블에서 모든 행을 삭제하려면 `TRUNCATE TABLE`을 사용합니다.  
  
-   행을 삭제하기 전에 힙에 클러스터형 인덱스를 만듭니다. 행이 삭제되고 나면 클러스터형 인덱스를 삭제할 수 있습니다. 이 방법은 앞의 두 방법보다 시간이 오래 걸리며 임시 리소스를 더 많이 사용합니다.  
  
> [!NOTE]  
>  `ALTER TABLE <table_name> REBUILD` 문을 사용하여 언제든지 힙에서 빈 페이지를 제거할 수 있습니다.  
  
## <a name="logging-behavior"></a>로깅 동작  
DELETE 문은 항상 전체 로깅됩니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 대상 테이블에 대한 `DELETE` 권한이 필요합니다. 문에 WHERE 절이 포함되어 있으면 `SELECT` 권한도 필요합니다.  
  
 DELETE 권한은 `sysadmin` 고정 서버 역할, `db_owner` 및 `db_datawriter` 고정 데이터베이스 역할, 테이블 소유자의 멤버에게 기본적으로 부여됩니다. `sysadmin`, `db_owner` 및 `db_securityadmin` 역할의 멤버와 테이블 소유자는 다른 사용자에게 권한을 이전할 수 있습니다.  
  
## <a name="examples"></a>예제  
  
|범주|중요한 구문 요소|  
|--------------|------------------------------|  
|[기본 구문](#BasicSyntax)|Delete|  
|[삭제되는 행 제한](#LimitRows)|WHERE • FROM • 커서 •|  
|[원격 테이블에서 행 삭제](#RemoteTables)|연결된 서버 • OPENQUERY 행 집합 함수 • OPENDATASOURCE 행 집합 함수|  
|[DELETE 문의 결과 캡처](#CaptureResults)|OUTPUT 절|  
  
###  <a name="basic-syntax"></a><a name="BasicSyntax"></a> 기본 구문  
 이 섹션의 예에서는 최소 필수 구문을 사용하여 DELETE 문의 기본 기능을 보여 줍니다.  
  
#### <a name="a-using-delete-with-no-where-clause"></a>A. WHERE 절 없이 DELETE 사용  
 다음 예에서는 삭제되는 행 수를 제한하는 WHERE 절을 사용하지 않았기 때문에 `SalesPersonQuotaHistory` 데이터베이스의 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 테이블에서 모든 행을 삭제합니다.  
  
```sql
DELETE FROM Sales.SalesPersonQuotaHistory;  
GO  
```  
  
###  <a name="limiting-the-rows-deleted"></a><a name="LimitRows"></a>삭제되는 행 제한  
 이 섹션의 예에서는 삭제되는 행 수를 제한하는 방법을 보여 줍니다.  
  
#### <a name="b-using-the-where-clause-to-delete-a-set-of-rows"></a>B. WHERE 절을 사용하여 행 집합 삭제  
 다음 예에서는 `StandardCost` 열의 값이 `1000.00`을 초과하는 모든 행을 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `ProductCostHistory`테이블에서 삭제합니다.  
  
```sql
DELETE FROM Production.ProductCostHistory  
WHERE StandardCost > 1000.00;  
GO  
```  
  
 다음 예서는 보다 복잡한 WHERE 절을 보여 줍니다. WHERE 절은 삭제할 행을 확인하기 위해 충족해야 하는 두 가지 조건을 정의합니다. `StandardCost` 열의 값은 `12.00` 에서 `14.00` 사이여야 하고, `SellEndDate` 열의 값은 Null이어야 합니다. 또한 이 예제에서는 **\@\@ROWCOUNT** 함수 값을 인쇄하여 삭제된 행 수를 반환합니다.  
  
```sql
DELETE Production.ProductCostHistory  
WHERE StandardCost BETWEEN 12.00 AND 14.00  
      AND EndDate IS NULL;  
PRINT 'Number of rows deleted is ' + CAST(@@ROWCOUNT as char(3));  
```  
  
#### <a name="c-using-a-cursor-to-determine-the-row-to-delete"></a>C. 커서를 사용하여 삭제할 행 확인  
 다음 예에서는 `complex_cursor`이라는 커서를 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `EmployeePayHistory` 테이블에서 단일 행을 삭제합니다. 삭제 작업은 현재 커서에서 인출된 한 행에만 영향을 줍니다.  
  
```sql
DECLARE complex_cursor CURSOR FOR  
    SELECT a.BusinessEntityID  
    FROM HumanResources.EmployeePayHistory AS a  
    WHERE RateChangeDate <>   
         (SELECT MAX(RateChangeDate)  
          FROM HumanResources.EmployeePayHistory AS b  
          WHERE a.BusinessEntityID = b.BusinessEntityID) ;  
OPEN complex_cursor;  
FETCH FROM complex_cursor;  
DELETE FROM HumanResources.EmployeePayHistory  
WHERE CURRENT OF complex_cursor;  
CLOSE complex_cursor;  
DEALLOCATE complex_cursor;  
GO  
```  
  
#### <a name="d-using-joins-and-subqueries-to-data-in-one-table-to-delete-rows-in-another-table"></a>D. 한 테이블의 데이터에 대한 조인 및 하위 쿼리를 사용하여 다른 테이블의 행 삭제  
 다음 예에서는 한 테이블의 데이터를 기반으로 다른 테이블의 행을 삭제하는 두 가지 방법을 보여 줍니다. 두 예에서 모두 `SalesPerson` 테이블에 저장된 연누계 매출에 기반하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `SalesPersonQuotaHistory` 테이블에서 행을 삭제합니다. 첫 번째 `DELETE` 문은 ISO 호환 하위 쿼리 솔루션을 보여 주고 두 번째 `DELETE` 문은 두 테이블을 조인하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] FROM 확장을 보여 줍니다.  
  
```sql
-- SQL-2003 Standard subquery  
  
DELETE FROM Sales.SalesPersonQuotaHistory   
WHERE BusinessEntityID IN   
    (SELECT BusinessEntityID   
     FROM Sales.SalesPerson   
     WHERE SalesYTD > 2500000.00);  
GO  
```  
  
```sql
-- Transact-SQL extension  
  
DELETE FROM Sales.SalesPersonQuotaHistory   
FROM Sales.SalesPersonQuotaHistory AS spqh  
INNER JOIN Sales.SalesPerson AS sp  
ON spqh.BusinessEntityID = sp.BusinessEntityID  
WHERE sp.SalesYTD > 2500000.00;  
GO  
```  
  
```sql
-- No need to mention target table more than once.  
  
DELETE spqh  
  FROM  
        Sales.SalesPersonQuotaHistory AS spqh  
    INNER JOIN Sales.SalesPerson AS sp  
        ON spqh.BusinessEntityID = sp.BusinessEntityID  
  WHERE  sp.SalesYTD > 2500000.00;  
```  
  
#### <a name="e-using-top-to-limit-the-number-of-rows-deleted"></a>E. TOP를 사용하여 삭제되는 행 수 제한  
 DELETE 문에 TOP( *n* ) 절을 사용하면 *n* 개의 행을 임의로 선택하여 삭제 작업이 수행됩니다. 다음 예에서는 `20` 데이터베이스의 `PurchaseOrderDetail` 테이블에서 기한이 2006년 7월 1일 이전인 행 중 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]개의 행을 임의로 선택하여 삭제합니다.  
  
```sql
DELETE TOP (20)   
FROM Purchasing.PurchaseOrderDetail  
WHERE DueDate < '20020701';  
GO  
```  
  
 TOP을 사용하여 시간 순서로 행을 삭제해야 하는 경우에는 하위 SELECT 문에서 ORDER BY를 지정하는 방식으로 TOP을 사용해야 합니다. 다음 쿼리는 `PurchaseOrderDetail` 테이블에서 기한이 가장 빠른 10개의 행을 삭제합니다. 10개의 행만 삭제하기 위해 하위 SELECT 문에서 지정한 열(`PurchaseOrderID`)은 테이블의 기본 키입니다. 하위 SELECT 문에 키가 아닌 열을 사용하면 지정한 열에 중복 값이 있을 경우 10개가 넘는 행이 삭제될 수 있습니다.  
  
```sql
DELETE FROM Purchasing.PurchaseOrderDetail  
WHERE PurchaseOrderDetailID IN  
   (SELECT TOP 10 PurchaseOrderDetailID   
    FROM Purchasing.PurchaseOrderDetail   
    ORDER BY DueDate ASC);  
GO  
```  
  
###  <a name="deleting-rows-from-a-remote-table"></a><a name="RemoteTables"></a> 원격 테이블에서 행 삭제  
 이 섹션의 예에서는 원격 테이블을 참조하는 [연결된 서버](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 또는 [행 집합 함수](../functions/opendatasource-transact-sql.md) 를 사용하여 원격 테이블에서 행을 삭제하는 방법을 보여 줍니다. 원격 테이블은 SQL Server의 다른 서버 또는 인스턴스에 있습니다.  
  
**적용 대상** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
#### <a name="f-deleting-data-from-a-remote-table-by-using-a-linked-server"></a>F. 연결된 서버를 사용하여 원격 테이블에서 데이터 삭제  
 다음 예에서는 원격 테이블에서 행을 삭제합니다. 먼저 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)를 사용하여 원격 데이터 원본에 대한 링크를 만듭니다. 그런 다음, 연결된 서버 이름 `MyLinkServer`가 *server.catalog.schema.object* 와 같이 네 부분으로 구성된 개체 이름의 일부로 지정됩니다.  
  
```sql
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' or 'server_name\instance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  
```  
  
```sql
-- Specify the remote data source using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
DELETE MyLinkServer.AdventureWorks2012.HumanResources.Department 
WHERE DepartmentID > 16;  
GO  
```  
  
#### <a name="g-deleting-data-from-a-remote-table-by-using-the-openquery-function"></a>G. OPENQUERY 함수를 사용하여 원격 테이블에서 데이터 삭제  
 다음 예에서는 [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) 행 집합 함수를 지정하여 원격 테이블에서 행을 삭제합니다. 이 예에서는 이전 예에서 만든 연결된 서버 이름이 사용됩니다.  
  
```sql
DELETE OPENQUERY (MyLinkServer, 'SELECT Name, GroupName 
FROM AdventureWorks2012.HumanResources.Department  
WHERE DepartmentID = 18');  
GO  
```  
  
#### <a name="h-deleting-data-from-a-remote-table-by-using-the-opendatasource-function"></a>H. OPENDATASOURCE 함수를 사용하여 원격 테이블에서 데이터 삭제  
 다음 예에서는 [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) 행 집합 함수를 지정하여 원격 테이블에서 행을 삭제합니다. *server_name* 또는 *server_name\instance_name* 형식을 사용하여 데이터 원본에 대해 유효한 서버 이름을 지정해야 합니다.  
  
```sql
DELETE FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source= <server_name>; Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department   
WHERE DepartmentID = 17;
```  
  
###  <a name="capturing-the-results-of-the-delete-statement"></a><a name="CaptureResults"></a> DELETE 문의 결과 캡처  
  
#### <a name="i-using-delete-with-the-output-clause"></a>9\. DELETE에 OUTPUT 절 사용  
 다음 예에서는 `DELETE` 문의 결과를 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 테이블 변수로 저장하는 방법을 보여 줍니다.  
  
```sql
DELETE Sales.ShoppingCartItem  
OUTPUT DELETED.*   
WHERE ShoppingCartID = 20621;  
  
--Verify the rows in the table matching the WHERE clause have been deleted.  
SELECT COUNT(*) AS [Rows in Table] 
FROM Sales.ShoppingCartItem 
WHERE ShoppingCartID = 20621;  
GO  
```  
  
#### <a name="j-using-output-with-from_table_name-in-a-delete-statement"></a>J. DELETE 문에 OUTPUT 및 <from_table_name> 사용  
 다음 예에서는 `DELETE` 문의 `FROM` 절에 정의된 검색 조건에 따라 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `ProductProductPhoto` 테이블에서 행을 삭제합니다. `OUTPUT` 절은 삭제될 테이블의 `DELETED.ProductID`, `DELETED.ProductPhotoID`열과 `Product` 테이블의 열을 반환합니다. 이것은 `FROM` 절에서 삭제할 행을 지정하는 데 사용됩니다.  
  
```sql
DECLARE @MyTableVar table (  
    ProductID int NOT NULL,   
    ProductName nvarchar(50)NOT NULL,  
    ProductModelID int NOT NULL,   
    PhotoID int NOT NULL);  
  
DELETE Production.ProductProductPhoto  
OUTPUT DELETED.ProductID,  
       p.Name,  
       p.ProductModelID,  
       DELETED.ProductPhotoID  
    INTO @MyTableVar  
FROM Production.ProductProductPhoto AS ph  
JOIN Production.Product as p   
    ON ph.ProductID = p.ProductID   
    WHERE p.ProductModelID BETWEEN 120 and 130;  
  
--Display the results of the table variable.  
SELECT ProductID, ProductName, ProductModelID, PhotoID   
FROM @MyTableVar  
ORDER BY ProductModelID;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="k-delete-all-rows-from-a-table"></a>11. 테이블에서 행을 삭제합니다.  
 다음 예에서는 삭제될 행 수를 제한하는 WHERE 절을 사용하지 않았기 때문에 `Table1` 테이블에서 모든 행을 삭제합니다.  
  
```sql
DELETE FROM Table1;  
```  
  
### <a name="l-delete-a-set-of-rows-from-a-table"></a>12. 테이블에서 행 집합을 DELETE합니다.

 다음 예에서는 `Table1` 테이블에서 `StandardCost` 열에 1000.00보다 큰 값을 가진 모든 행을 삭제합니다.  
  
```sql
DELETE FROM Table1  
WHERE StandardCost > 1000.00;  
```  
  
### <a name="m-using-label-with-a-delete-statement"></a>13. DELETE 문과 함께 LABEL 사용

 다음 예제에서는 DELETE 문과 함께 레이블을 사용합니다.  
  
```sql
DELETE FROM Table1  
OPTION ( LABEL = N'label1' );  
  
```  
  
### <a name="n-using-a-label-and-a-query-hint-with-the-delete-statement"></a>14. DELETE 문에 레이블 및 쿼리 힌트 사용

 이 쿼리는 DELETE 문에 쿼리 조인 힌트를 사용하는 기본 구문을 보여줍니다. 조인 힌트 및 OPTION 절을 사용하는 방법에 대한 자세한 내용은 [OPTION 절(Transact-SQL)](../queries/option-clause-transact-sql.md)을 참조하세요.
  
```sql
-- Uses AdventureWorks  
  
DELETE FROM dbo.FactInternetSales  
WHERE ProductKey IN (   
    SELECT T1.ProductKey FROM dbo.DimProduct T1   
    JOIN dbo.DimProductSubcategory T2  
    ON T1.ProductSubcategoryKey = T2.ProductSubcategoryKey  
    WHERE T2.EnglishProductSubcategoryName = 'Road Bikes' )  
OPTION ( LABEL = N'CustomJoin', HASH JOIN ) ;  
```  

### <a name="o-delete-using-a-where-clause"></a>15. WHERE 절을 사용하여 삭제

이 쿼리는 FROM 절을 사용하지 않고 WHERE 절을 사용하여 삭제하는 방법을 보여 줍니다.

```sql
DELETE tableA WHERE EXISTS (
SELECT TOP 1 1 FROM tableB tb WHERE tb.col1 = tableA.col1
)
```

### <a name="p-delete-based-on-the-result-of-joining-with-another-table"></a>16. 다른 테이블과의 조인 결과에 따라 삭제

이 예제에서는 다른 테이블과의 조인 결과에 따라 테이블에서 삭제하는 방법을 보여 줍니다.

```sql
CREATE TABLE dbo.Table1   
    (ColA int NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  

CREATE TABLE dbo.Table2   
    (ColA int PRIMARY KEY NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  
INSERT INTO dbo.Table1 VALUES(1, 10.0), (1, 20.0);  
INSERT INTO dbo.Table2 VALUES(1, 0.0);  
GO  

DELETE dbo.Table2   
FROM dbo.Table2   
    INNER JOIN dbo.Table1   
    ON (dbo.Table2.ColA = dbo.Table1.ColA)
    WHERE dboTable2.ColA = 1;  
```

## <a name="see-also"></a>참고 항목

 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [TRUNCATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WITH common_table_expression&#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)   
 [@@ROWCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)  
  
