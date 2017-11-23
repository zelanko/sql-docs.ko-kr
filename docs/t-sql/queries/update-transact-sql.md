---
title: "업데이트 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE_TSQL
- UPDATE
dev_langs: TSQL
helpviewer_keywords:
- DML [SQL Server], UPDATE statement
- data updates [SQL Server], UPDATE statement
- updating data [SQL Server]
- TOP clause, UPDATE
- OUTPUT clause
- large value data types
- data manipulation language [SQL Server], UPDATE statement
- user-defined types [SQL Server], modifying
- INSTEAD OF triggers
- modifying data [SQL Server], UPDATE statement
- data modifications [SQL Server], UPDATE statement
- large data, modifying
- .WRITE clause
- table modifications [SQL Server], UPDATE statement
- UDTs [SQL Server], modifying
- UPDATE statement [SQL Server], about UPDATE statement
- LOB data [SQL Server], modifying
- modifying LOB data
- UPDATE statement [SQL Server]
- FROM clause, UPDATE statement
- WHERE clause, UPDATE statement
ms.assetid: 40e63302-0c68-4593-af3e-6d190181fee7
caps.latest.revision: "91"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 671eb95a5c1772ec790886d923112d491bbd2a35
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="update-transact-sql"></a>UPDATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 테이블 또는 뷰의 기존 데이터를 변경합니다. 예제를 보려면 [예제](#UpdateExamples)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```tsql  
-- Syntax for SQL Server and Azure SQL Database  

[ WITH <common_table_expression> [...n] ]  
UPDATE   
    [ TOP ( expression ) [ PERCENT ] ]   
    { { table_alias | <object> | rowset_function_limited   
         [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
      }  
      | @table_variable      
    }  
    SET  
        { column_name = { expression | DEFAULT | NULL }  
          | { udt_column_name.{ { property_name = expression  
                                | field_name = expression }  
                                | method_name ( argument [ ,...n ] )  
                              }  
          }  
          | column_name { .WRITE ( expression , @Offset , @Length ) }  
          | @variable = expression  
          | @variable = column = expression  
          | column_name { += | -= | *= | /= | %= | &= | ^= | |= } expression  
          | @variable { += | -= | *= | /= | %= | &= | ^= | |= } expression  
          | @variable = column { += | -= | *= | /= | %= | &= | ^= | |= } expression  
        } [ ,...n ]   
  
    [ <OUTPUT Clause> ]  
    [ FROM{ <table_source> } [ ,...n ] ]   
    [ WHERE { <search_condition>   
            | { [ CURRENT OF   
                  { { [ GLOBAL ] cursor_name }   
                      | cursor_variable_name   
                  }   
                ]  
              }  
            }   
    ]   
    [ OPTION ( <query_hint> [ ,...n ] ) ]  
[ ; ]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
    | database_name .[ schema_name ] .   
    | schema_name .  
    ]  
    table_or_view_name}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

UPDATE [ database_name . [ schema_name ] . | schema_name . ] table_name   
SET { column_name = { expression | NULL } } [ ,...n ]  
[ FROM from_clause ]  
[ WHERE <search_condition> ]   
[ OPTION ( LABEL = label_name ) ]  
[;]  
```  
  
## <a name="arguments"></a>인수  
 와 \<common_table_expression >  
 UPDATE 문의 범위 내에서 정의된 임시 명명된 결과 집합 또는 뷰를 지정합니다. 이를 CTE(공통 테이블 식)라고 합니다. CTE 결과 집합은 단순 쿼리에서 파생되며 UPDATE 문에서 참조됩니다.  
  
 공통 테이블 식은 SELECT, INSERT, DELETE 및 CREATE VIEW 문에서도 사용됩니다. 자세한 내용은 참조 [common_table_expression &AMP;#40; Transact SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 TOP **(** *식***)** [%]  
 수 또는 업데이트 되는 행의 비율을 지정 합니다. *expression* 은 행의 수 또는 비율일 수 있습니다.  
  
 INSERT, UPDATE 또는 DELETE와 함께 사용된 TOP 식에서 참조된 행은 어떠한 순서로도 정렬되지 않습니다.  
  
 구분 하는 괄호가 *식* INSERT, UPDATE 및 DELETE 문에 TOP에 필요 합니다. 자세한 내용은 참조 [top&#40; Transact SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 *table_alias*  
 행을 업데이트할 테이블 또는 뷰를 나타내는 FROM 절에 지정되는 별칭입니다.  
  
 *server_name*  
 서버 이름입니다 (연결 된 서버 이름을 사용 하 여 또는 [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) 함수를 서버 이름으로)에 테이블이 나 뷰가 위치한 합니다. 경우 *server_name* 지정 된 *database_name* 및 *schema_name* 필요 합니다.  
  
 *database_name*  
 데이터베이스의 이름입니다.  
  
 *schema_name*  
 테이블이나 뷰가 속한 스키마의 이름입니다.  
  
 *table_or view_name*  
 행을 업데이트할 테이블 또는 뷰의 이름입니다. 참조 되는 뷰 *table_or_view_name* 업데이트할 수 있도록 하 고 보기의 FROM 절에서 정확히 한 개의 기본 테이블을 참조 해야 합니다. 업데이트할 수 있는 뷰에 대 한 자세한 내용은 참조 하세요. [CREATE view&#40; Transact SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 *rowset_function_limited*  
 이 [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) 또는 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 공급자 기능에 따라 함수입니다.  
  
 와 **(** \<Table_Hint_Limited > **)**  
 대상 테이블에 허용되는 하나 이상의 테이블 힌트를 지정합니다. WITH 키워드와 괄호가 필요합니다. NOLOCK 및 READUNCOMMITTED는 허용되지 않습니다. 테이블 힌트에 대 한 정보를 참조 하십시오. [테이블 힌트 &#40; Transact SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
 @*table_variable*  
 지정 된 [테이블](../../t-sql/data-types/table-transact-sql.md) 테이블 원본으로 변수입니다.  
  
 SET  
 업데이트할 열이나 변수 이름의 목록을 지정합니다.  
  
 *column_name*  
 변경할 데이터가 포함된 열입니다. *column_name* 에 존재 해야 *table_or view_name*합니다. ID 열은 업데이트할 수 없습니다.  
  
 *expression*  
 단일 값을 반환하는 변수, 리터럴 값, 식 또는 괄호로 묶인 하위 SELECT 문입니다. 반환한 값 *식* 의 기존 값을 대체 *column_name* 또는  *@variable* 합니다.  
  
> [!NOTE]  
>  유니코드 문자 데이터 형식을 참조할 때는 **nchar**, **nvarchar**, 및 **ntext**, 'expression' 대문자 접두사로 추가 해야 ' N '입니다. 'N'을 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 또는 열의 기본 데이터 정렬에 해당하는 코드 페이지로 문자열을 변환합니다. 이 코드 페이지에 없는 문자는 모두 손실됩니다.  
  
 DEFAULT  
 열에 정의한 기본값이 열의 기존 값을 대체하도록 지정합니다. 열에 기본값이 없고 NULL 값을 허용하도록 정의한 경우, 열을 NULL로 변경하는 데 사용할 수도 있습니다.  
  
 { **+=** | **-=** | **\*=** | **/=** | **%=** | **&=** | **^=** | **|=** }  
 복합 할당 연산자:  
 + = 더하기 및 할당  
 -= 빼기 및 할당  
 * = 곱하기 및 할당  
 / = 나누기 및 할당  
 % = 모듈로 및 할당  
 & = 비트 AND 및 할당  
 ^ = 비트 XOR 및 할당  
 | = 비트 OR 및 할당  
  
 *udt_column_name*  
 사용자 정의 형식의 열입니다.  
  
 *property_name* | *d _*  
 사용자 정의 형식의 공용 속성 또는 공용 데이터 멤버입니다.  
  
 *method_name* **(** *인수* [ **,**... *n*] **)**  
 비정적 공용 변경자 (mutator) 메서드가 *udt_column_name* 하는 하나 이상의 인수를 사용 하 고 사용 합니다.  
  
 **.** 쓰기 **(***식***,***@Offset***,** *@Length***)**  
 지정 하는 값의 섹션 *column_name* 수정 하는 것입니다. *식* 대체  *@Length*  에서 시작 하는 단위  *@Offset*  의 *column_name*합니다. 열만 **varchar (max)**, **nvarchar (max)**, 또는 **varbinary (max)** 이 절을 사용 하 여 지정할 수 있습니다. *column_name* NULL 일 수 없습니다 및 테이블 이름 또는 테이블 별칭으로 정규화 할 수 없습니다.  
  
 *식* 에 복사 하는 값은 *column_name*합니다. *식* 평가 되거나 암시적으로 캐스팅 될 수는 *column_name* 유형입니다. 경우 *식* NULL로 설정 되어  *@Length*  무시 됩니다에 값 *column_name* 잘렸습니다. 지정 된 위치에서  *@Offset* .  
  
 *@Offset*클래스의 값의 시작 지점 *column_name* 입니다 *식* 기록 됩니다. *@Offset*0부터 시작 하는 서 수 위치를 **bigint**, 및는 음수일 수 없습니다. 경우  *@Offset*  이 NULL 이면 업데이트 작업이 추가 *식* 기존 끝날 때 *column_name* 값 및  *@Length*  는 무시 됩니다. 경우 @Offset 의 길이 보다 크면는 *column_name* 값의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 오류를 반환 합니다. 경우  *@Offset*  플러스  *@Length*  까지 삭제가 이루어집니다 마지막 값의 문자, 열에 기본 값의 끝을 초과 합니다. 경우  *@Offset*  LEN 더하기 (*식*) 내부 보다 큰 크기를 선언 하면 오류가 발생 합니다.  
  
 *@Length*시작 하 여 열의의 섹션 길이  *@Offset* , 즉 교체 *식*합니다. *@Length***bigint** 하며 음수가 될 수 없습니다. 경우  *@Length*  이 NULL 이면 업데이트 작업에서 데이터를 모두 제거  *@Offset*  의 끝에는 *column_name* 값입니다.  
  
 자세한 내용은 설명 부분을 참조하세요.  
  
 **@***변수*  
 선언 된 변수에서 반환 된 값으로 설정 된 *식*합니다.  
  
 설정  **@**  *변수* = *열* = *식* 는 같은 변수를 설정 합니다. 열 값입니다. 집합에서이 점에서 차이가  **@**  *변수* = *열*, *열*  =  *식*, 변수 열의 업데이트 전 값을 설정 합니다.  
  
 \<OUTPUT_Clause >  
 UPDATE 작업의 일부로서 업데이트된 데이터 또는 이를 바탕으로 한 식을 반환합니다. OUTPUT 절은 원격 테이블 또는 뷰를 대상으로 하는 어떤 DML 문에서도 지원되지 않습니다. 자세한 내용은 참조 [OUTPUT 절 &#40; Transact SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
 \<b l e _ >  
 업데이트 작업의 기준이 될 테이블, 뷰 또는 파생된 테이블 원본을 지정합니다. 자세한 내용은 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)을 참조하세요.  
  
 업데이트되는 개체가 FROM 절의 개체와 같고 개체에 대한 참조가 FROM 절에 하나만 있는 경우, 개체 별칭은 지정될 수도 있고 지정되지 않을 수도 있습니다. 업데이트되는 개체가 FROM 절에서 두 번 이상 나타날 경우 개체에 대한 단 한 번의 참조로 테이블 별칭을 지정할 수는 없습니다. FROM 절의 개체에 대한 다른 모든 참조에는 개체 별칭이 포함되어야 합니다.  
  
 INSTEAD OF UPDATE 트리거가 있는 뷰는 FROM 절이 있는 UPDATE의 대상이 될 수 없습니다.  
  
> [!NOTE]  
>  FROM 절에서 OPENDATASOURCE, OPENQUERY 또는 OPENROWSET에 대한 모든 호출은 두 호출에 동일한 인수가 제공되는 경우에도 업데이트의 대상으로 사용되는 함수에 대한 호출과는 개별적이고 독립적으로 평가됩니다. 특히 이러한 호출 중 하나의 결과에 적용되는 필터 또는 조인 조건은 다른 호출의 결과에 영향을 미치지 않습니다.  
  
 WHERE  
 업데이트되는 열을 제한하는 조건을 지정합니다. 어떤 형식의 WHERE 절을 사용하는가에 따라 다음 두 가지 업데이트 형식이 있습니다.  
  
-   검색 결과 업데이트 - 삭제할 행을 제한하는 검색 조건을 지정합니다.  
  
-   현재 위치 업데이트 - 커서를 지정하는 CURRENT OF 절을 사용합니다. 이 경우 커서의 현재 위치에서 업데이트 작업이 이루어집니다.  
  
\<c h _ c >  
 업데이트할 행을 결정하는 조건을 지정합니다. 조인을 기반으로 하는 조건도 검색 조건으로 사용할 수 있습니다. 검색 조건에 포함시킬 수 있는 조건자의 개수에는 제한이 없습니다. 조건자와 검색 조건에 대 한 자세한 내용은 참조 [검색 조건 &#40; Transact SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
CURRENT OF  
 지정한 커서의 현재 위치에서 업데이트가 수행되도록 지정합니다.  
  
 WHERE CURRENT OF 절을 사용하여 현재 위치 업데이트를 수행하면 커서의 현재 위치에서 단일 행을 업데이트합니다. 이 WHERE를 사용 하는 검색 결과 업데이트 보다 정확한 수 \<c h _ c >는 업데이트할 행을 한 정하는 데 절. 검색 결과 업데이트는 검색 조건이 단일 행을 고유하게 식별하지 못할 경우 여러 행을 변경할 수 있습니다.  
  
GLOBAL  
 지정 하는 *cursor_name* 전역 커서를 참조 합니다.  
  
*cursor_name*  
 인출이 수행되는 열린 커서의 이름입니다. 전역 및 로컬 커서 이름의 경우 *cursor_name* 존재, GLOBAL이 고, 그렇지 않으면 지정 된 경우이 인수는 전역 커서를, 로컬 커서를 참조 합니다. 커서는 업데이트될 수 있어야 합니다.  
  
*cursor_variable_name*  
 커서 변수의 이름입니다. *cursor_variable_name* 업데이트를 허용 하는 커서를 참조 해야 합니다.  
  
옵션 **(** \<쿼리 힌트 > [ **,**... *n* ] **)**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 문을 처리하는 방식을 사용자 지정하기 위한 최적화 프로그램 힌트를 지정합니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 사용 된 @@ROWCOUNT 삽입 된 클라이언트 응용 프로그램에는 행의 수를 반환 하는 함수입니다. 자세한 내용은 참조 [@@ROWCOUNT &#40; Transact SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md).  
  
 UPDATE 문에서 변수 이름을 사용하면 영향을 받는 이전 값과 새로운 값을 표시할 수 있지만 이는 UPDATE 문이 단일 레코드에 영향을 줄 경우에만 사용할 수 있는 방법입니다. 경우 UPDATE 문은 각 레코드에 대 한 기존 패턴과 새 값을 반환 하려면 여러 레코드를 사용 하 여는 [OUTPUT 절](../../t-sql/queries/output-clause-transact-sql.md)합니다.  
  
 업데이트 작업의 기준을 제공하는 FROM 절을 지정할 때는 주의해야 합니다. 업데이트되는 각 열에 대해 하나의 값만 가능하도록 지정되지 않은 FROM 절이 문에 포함된 경우(즉, UPDATE 문이 비결정적인 경우) UPDATE 문의 결과가 정의되지 않습니다. 예를 들어 다음 스크립트의 UPDATE 문에서 `Table1`에 있는 두 행이 UPDATE 문의 FROM 절 조건을 충족하지만 `Table1`의 행을 업데이트하기 위해 `Table2.`의 어떤 행을 사용할 것인지는 정의되지 않았습니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.Table1', 'U') IS NOT NULL  
    DROP TABLE dbo.Table1;  
GO  
IF OBJECT_ID ('dbo.Table2', 'U') IS NOT NULL  
    DROP TABLE dbo.Table2;  
GO  
CREATE TABLE dbo.Table1   
    (ColA int NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  
CREATE TABLE dbo.Table2   
    (ColA int PRIMARY KEY NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  
INSERT INTO dbo.Table1 VALUES(1, 10.0), (1, 20.0);  
INSERT INTO dbo.Table2 VALUES(1, 0.0);  
GO  
UPDATE dbo.Table2   
SET dbo.Table2.ColB = dbo.Table2.ColB + dbo.Table1.ColB  
FROM dbo.Table2   
    INNER JOIN dbo.Table1   
    ON (dbo.Table2.ColA = dbo.Table1.ColA);  
GO  
SELECT ColA, ColB   
FROM dbo.Table2;  
```  
  
 FROM 및 WHERE CURRENT OF 절을 함께 사용할 때도 같은 문제가 발생합니다. 다음 예에서 `Table2` 테이블의 두 행은 `FROM` 문에 있는 `UPDATE` 절의 조건을 충족시킵니다. 하지만 `Table2`의 행을 업데이트하기 위해 `Table1`의 어떤 행을 사용할 것인지는 정의되지 않았습니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.Table1', 'U') IS NOT NULL  
    DROP TABLE dbo.Table1;  
GO  
IF OBJECT_ID ('dbo.Table2', 'U') IS NOT NULL  
    DROP TABLE dbo.Table2;  
GO  
CREATE TABLE dbo.Table1  
    (c1 int PRIMARY KEY NOT NULL, c2 int NOT NULL);  
GO  
CREATE TABLE dbo.Table2  
    (d1 int PRIMARY KEY NOT NULL, d2 int NOT NULL);  
GO  
INSERT INTO dbo.Table1 VALUES (1, 10);  
INSERT INTO dbo.Table2 VALUES (1, 20), (2, 30);  
GO  
DECLARE abc CURSOR LOCAL FOR  
    SELECT c1, c2   
    FROM dbo.Table1;  
OPEN abc;  
FETCH abc;  
UPDATE dbo.Table1   
SET c2 = c2 + d2   
FROM dbo.Table2   
WHERE CURRENT OF abc;  
GO  
SELECT c1, c2 FROM dbo.Table1;  
GO  
```  
  
## <a name="compatibility-support"></a>호환성 지원  
 UPDATE 또는 DELETE 문의 대상 테이블에 적용되는 FROM 절의 READUNCOMMITTED 및 NOLOCK 힌트 사용 지원은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서 제거될 예정입니다. 새 개발 작업에서는 이 컨텍스트에서 이러한 힌트를 사용하지 않도록 하고 현재 이 힌트를 사용하는 응용 프로그램은 수정하세요.  
  
## <a name="data-types"></a>데이터 형식  
 모든 **char** 및 **nchar** 열은 정의 된 길이를 오른쪽으로 채워집니다.  
  
 ANSI_PADDING이 OFF로 설정 하는 경우 모든 후행 공백이 삽입 된 데이터에서 제거 됩니다 **varchar** 및 **nvarchar** 열, 공백만 포함 하는 문자열은 예외입니다. 공백만 있는 문자열은 빈 문자열로 잘립니다. ANSI_PADDING이 ON으로 설정되면 후행 공백이 삽입됩니다. Microsoft SQL Server ODBC 드라이버와 SQL Server용 OLE DB 공급자는 각 연결에 대해 ANSI_PADDING ON을 자동 설정합니다. 이 설정은 ODBC 데이터 원본이나 연결 특성 또는 속성을 통해 구성할 수 있습니다. 자세한 내용은 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)을 참조하세요.  
  
### <a name="updating-text-ntext-and-image-columns"></a>text, ntext 및 image 열 업데이트  
 수정 된 **텍스트**, **ntext**, 또는 **이미지** 업데이트로 열 열 초기화 유효한 텍스트 포인터를 할당 하 고 하지 않는 한 하나 이상의 데이터 페이지가 할당는 열이 NULL로 업데이트 되 고 있습니다.  
  
 바꾸거나 수정 **텍스트**, **ntext**, 또는 **이미지** 데이터를 사용 하 여 [WRITETEXT](../../t-sql/queries/writetext-transact-sql.md) 또는 [UPDATETEXT](../../t-sql/queries/updatetext-transact-sql.md) UPDATE 문 대신 합니다.  
  
 UPDATE 문이 모두 클러스터링 키와 하나 이상의 업데이트 하는 동안 하나 이상의 행을 변경할 수 있는 경우 **텍스트**, **ntext**, 또는 **이미지** 열, 부분 업데이트 이러한 열 값의 전체 대체 값으로 실행 됩니다.  
  
> [!IMPORTANT]  
>  **ntext**, **텍스트**, 및 **이미지** 데이터 형식은 나중 버전의에서 제거 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 향후 개발 작업에서는 이 데이터 형식을 사용하지 않도록 하고 현재 이 데이터 형식을 사용하는 응용 프로그램은 수정하세요. 대신 [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)및 [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) 를 사용합니다.  
  
### <a name="updating-large-value-data-types"></a>큰 값 데이터 형식 업데이트  
 사용 하 여 **.** 쓰기 (*식***,**  *@Offset*  **,***@Length*) 절을 전체 또는 일부 업데이트를 수행 **varchar (max)**, **nvarchar (max)**, 및 **varbinary (max)** 데이터 형식입니다. 예를 들어의 부분 업데이트는 **varchar (max)** 열을 삭제 하거나 전체 업데이트는 삭제 하거나 열에서 모든 데이터를 수정 하는 반면 열의 처음 200 자만 수정할 수 있습니다. **.** 삽입 또는 새 데이터 추가 최소 로깅하도록 업데이트 데이터베이스 복구 모델이 대량 로그 또는 단순으로 설정 된 경우를 작성 합니다. 기존 값이 업데이트되면 최소 로깅이 사용되지 않습니다. 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)을(를) 참조하세요.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 UPDATE 문이 다음 중 한 가지 동작을 유발할 때 부분 업데이트를 전체 업데이트로 변환합니다.  
-   분할된 뷰 또는 테이블의 키 열을 변경합니다.  
-   하나 이상의 행을 변경하고 고유하지 않은 클러스터형 인덱스의 키를 상수가 아닌 값으로 업데이트합니다.  
  
사용할 수 없습니다는 **.** NULL 열을 업데이트 하거나 값을 설정 하려면 WRITE 절 *column_name* NULL로 합니다.  
  
*@Offset*및  *@Length*  에 대 한 바이트에 지정 된 **varbinary** 및 **varchar** 데이터 형식 및에 대 한 문자는 **nvarchar**데이터 형식입니다. 오프셋은 DBCS(더블바이트 문자 집합) 데이터 정렬에 맞게 적절히 계산됩니다.  
  
최상의 성능을 위해 8,040바이트의 배수인 청크 크기로 데이터를 삽입 또는 업데이트하는 것이 좋습니다.  
  
수정 된 열은 **.** 절에서에서 참조 된 열의 전체 값 OUTPUT 절 즉 쓰기는 이전 이미지 **삭제.** *column_name* 또는 이후 이미지가 **삽입.** *column_name*, 테이블 변수에서 지정된 된 열에 반환 됩니다. 다음에 나오는 R 예제를 참조 하십시오.  
  
동일한 기능을 얻기 위해 **.** 다른 문자 또는 이진 데이터 형식 쓰기, 사용 된 [항목 &#40; Transact SQL &#41; ](../../t-sql/functions/stuff-transact-sql.md).  
  
### <a name="updating-user-defined-type-columns"></a>사용자 정의 형식 열 업데이트  
 다음 중 한 가지 방법으로 사용자 정의 형식 열의 값을 업데이트할 수 있습니다.  
  
-   사용자 정의 형식에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식의 암시적 또는 명시적 변환이 지원되는 경우 해당 형식의 값을 제공합니다. 다음 예에서는 문자열에서 명시적 변환을 통해 사용자 정의 형식인 `Point` 열의 값을 업데이트하는 방법을 보여 줍니다.  
  
    ```sql  
    UPDATE Cities  
    SET Location = CONVERT(Point, '12.3:46.2')  
    WHERE Name = 'Anchorage';  
    ```  
  
-   변경자(mutator)로 표시된 사용자 정의 형식의 메서드를 호출하여 업데이트를 수행합니다. 다음 예에서는 `Point`라는 `SetXY` 유형의 변경자 메서드를 호출합니다. 해당 유형의 인스턴스 상태가 업데이트됩니다.  
  
    ```sql  
    UPDATE Cities  
    SET Location.SetXY(23.5, 23.5)  
    WHERE Name = 'Anchorage';  
    ```  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Null 값에서 변경자(mutator) 메서드를 호출하거나 변경자(mutator) 메서드에 의해 생성된 새 값이 Null이면 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 오류가 반환됩니다.  
  
-   등록된 속성 또는 사용자 정의 형식의 공용 데이터 멤버 값을 변경합니다. 값을 제공하는 식은 암시적으로 해당 속성 유형으로 변환할 수 있어야 합니다. 다음 예에서는 사용자 정의 형식 `X`의 `Point` 속성 값을 수정합니다.  
  
    ```sql  
    UPDATE Cities  
    SET Location.X = 23.5  
    WHERE Name = 'Anchorage';  
    ```  
  
     동일한 사용자 정의 형식 열의 다른 속성을 수정하려면 UPDATE 문을 실행하거나 해당 유형의 변경자(mutator) 메서드를 호출합니다.  
  
### <a name="updating-filestream-data"></a>FILESTREAM 데이터 업데이트  
 UPDATE 문을 통해 FILESTREAM 필드를 Null 값, 비어 있는 값 또는 상대적으로 짧은 인라인 데이터로 업데이트할 수 있습니다. 그러나 크기가 큰 데이터는 Win32 인터페이스를 사용하여 파일로 좀 더 효율적으로 스트리밍됩니다. FILESTREAM 필드를 업데이트할 때 파일 시스템의 기본 BLOB 데이터를 수정합니다. FILESTREAM 필드를 NULL로 설정하면 이 필드와 연결된 BLOB 데이터가 삭제됩니다. 사용할 수 없습니다. Write () FILESTREAM 데이터에 부분 업데이트를 수행 합니다. 자세한 내용은 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)을 참조하세요.  
  
## <a name="error-handling"></a>오류 처리  
 행에 대한 업데이트가 제약 조건이나 규칙을 위반할 경우, 열에 대한 NULL 설정을 위반할 경우 또는 새 값이 호환되지 않는 데이터 형식인 경우에는 문이 취소되고 오류가 반환되며 레코드가 업데이트되지 않습니다.  
  
 식을 평가할 때 UPDATE 문에 산술 오류(오버플로, 0으로 나누기 또는 도메인 오류)가 발생하면 업데이트가 실행되지 않으며 나머지 일괄 처리가 실행되지 않고 오류 메시지가 반환됩니다.  
  
 클러스터형 인덱스에 참여하는 열을 업데이트하여 클러스터형 인덱스와 행의 크기가 8,060바이트를 넘어서면 업데이트가 실패하고 오류 메시지가 반환됩니다.  
  
## <a name="interoperability"></a>상호 운용성  
 수정되고 있는 테이블이 테이블 변수인 경우에만 UPDATE 문이 사용자 정의 함수의 본문에 허용됩니다.  
  
 테이블에 대한 UPDATE 동작에 INSTEAD OF 트리거가 정의되면 UPDATE 문 대신 트리거가 실행됩니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 UPDATE 및 기타 데이터 수정 문에서 정의된 AFTER 트리거만 지원되었습니다. INSTEAD OF 트리거가 정의되어 있는 뷰를 직접 또는 간접적으로 참조하는 UPDATE 문에는 FROM 절을 지정할 수 없습니다. Instead of 트리거에 대 한 자세한 내용은 참조 하세요. [CREATE trigger&#40; Transact SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 INSTEAD OF 트리거가 정의되어 있는 뷰를 직접 또는 간접적으로 참조하는 UPDATE 문에는 FROM 절을 지정할 수 없습니다. Instead of 트리거에 대 한 자세한 내용은 참조 하세요. [CREATE trigger&#40; Transact SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 CTE(공통 테이블 식)가 UPDATE 문의 대상인 경우 문에서 CTE에 대한 모든 참조가 일치해야 합니다. 예를 들어 FROM 절에서 CTE에 별칭이 지정된 경우 CTE에 대한 다른 모든 참조에서 이 별칭을 사용해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 개체 ID를 사용하여 개체와 해당 별칭 간의 암시적 관계를 인식하는데, CTE는 개체 ID가 없기 때문에 CTE 참조가 분명해야 합니다. 이 관계가 없으면 쿼리 계획에서 예기치 않은 조인 동작과 의도하지 않은 쿼리 결과가 발생할 수 있습니다. 다음 예에서는 CTE가 업데이트 작업의 대상 개체일 때 CTE를 지정하는 올바른 방법과 잘못된 방법을 보여 줍니다.  
  
```sql  
USE tempdb;  
GO  
-- UPDATE statement with CTE references that are correctly matched.  
DECLARE @x TABLE (ID int, Value int);  
DECLARE @y TABLE (ID int, Value int);  
INSERT @x VALUES (1, 10), (2, 20);  
INSERT @y VALUES (1, 100),(2, 200);  
  
WITH cte AS (SELECT * FROM @x)  
UPDATE x -- cte is referenced by the alias.  
SET Value = y.Value  
FROM cte AS x  -- cte is assigned an alias.  
INNER JOIN @y AS y ON y.ID = x.ID;  
SELECT * FROM @x;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ID     Value  
 ------ -----  
 1      100  
 2      200  
 (2 row(s) affected)  
```  

UPDATE 문을 올바르게 일치 CTE 참조를 사용 합니다.  
```sql  
USE tempdb;  
GO  
DECLARE @x TABLE (ID int, Value int);  
DECLARE @y TABLE (ID int, Value int);  
INSERT @x VALUES (1, 10), (2, 20);  
INSERT @y VALUES (1, 100),(2, 200);  
  
WITH cte AS (SELECT * FROM @x)  
UPDATE cte   -- cte is not referenced by the alias.  
SET Value = y.Value  
FROM cte AS x  -- cte is assigned an alias.  
INNER JOIN @y AS y ON y.ID = x.ID;   
SELECT * FROM @x;   
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ID     Value  
------ -----  
1      100  
2      100  
(2 row(s) affected)  
```  

## <a name="locking-behavior"></a>잠금 동작  
 UPDATE 문은 항상 수정하는 테이블에 대해 배타적(X) 잠금을 획득하고 해당 트랜잭션이 완료될 때까지 이 잠금을 보유합니다. 배타적 잠금이 설정되면 다른 트랜잭션에서 데이터를 수정할 수 없습니다. 테이블 힌트를 지정해 다른 잠금 방법을 지정하여 UPDATE 문의 기간에 이 기본 동작을 재정의할 수 있지만, 숙련된 개발자 및 데이터베이스 관리자가 최후의 수단으로만 힌트를 사용하시기 바랍니다. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
## <a name="logging-behavior"></a>로깅 동작  
 UPDATE 문은 기록 됩니다. 그러나 한 부분을 사용 하 여 큰 값 데이터 형식 업데이트는 **.** 절은 최소한으로 기록에 작성 합니다. 자세한 내용은 "업데이트 큰 값 데이터 형식" 이전 단원의 "데이터 형식"을 참조 하십시오.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 대상 테이블에 대한 UPDATE 권한이 필요합니다. 되어 필요한 경우 또는 UPDATE 문의 WHERE 절을 포함 하는 경우 업데이트 되는 테이블에 대 한 SELECT 권한도 *식* 집합에 절에서 테이블의 열을 사용 합니다.  
  
 멤버에 게 권한은 기본적으로 업데이트는 **sysadmin** 고정 서버 역할의 **db_owner** 및 **db_datawriter** 고정 데이터베이스 역할 및 테이블 소유자입니다. 멤버는 **sysadmin**, **db_owner**, 및 **db_securityadmin** 역할 및 테이블 소유자 권한을 다른 사용자에 게 위임할 수 있습니다.  
  
##  <a name="UpdateExamples"></a> 예  
  
|범주|중요한 구문 요소|  
|--------------|------------------------------|  
|[기본 구문](#BasicSyntax)|UPDATE|  
|[업데이트 되는 행 제한](#LimitingValues)|WHERE • TOP • WITH 공통 테이블 식 • WHERE CURRENT OF|  
|[열 값 설정](#ColumnValues)|계산 값 • 복합 연산자 • 기본값 • 하위 쿼리|  
|[표준 테이블 이외의 대상 개체 지정](#TargetObjects)|뷰 • 테이블 변수 • 테이블 별칭|  
|[다른 테이블의 데이터를 기반으로 하는 데이터 업데이트](#OtherTables)|FROM|  
|[원격 테이블의 행 업데이트](#RemoteTables)|연결된 서버 • OPENQUERY • OPENDATASOURCE|  
|[큰 개체 데이터 형식 업데이트](#LOBValues)|. • OPENROWSET 작성|  
|[사용자 정의 형식 업데이트](#UDTs)|사용자 정의 형식|  
|[힌트를 사용 하 여 쿼리 최적화 프로그램의 기본 동작 재정의](#TableHints)|테이블 힌트 • 쿼리 힌트|  
|[UPDATE 문의 결과 캡처](#CaptureResults)|OUTPUT 절|  
|[다른 문에서 UPDATE 사용](#Other)|저장 프로시저 • TRY…CATCH|  
  
###  <a name="BasicSyntax"></a>기본 구문  
 이 섹션의 예에서는 최소 필수 구문을 사용하여 UPDATE 문의 기본 기능을 보여 줍니다.  
  
#### <a name="a-using-a-simple-update-statement"></a>1. 단순 UPDATE 문 사용  
 다음 예에서는 `Person.Address` 테이블의 모든 행에 대해 단일 열을 업데이트합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Person.Address  
SET ModifiedDate = GETDATE();  
```  
  
#### <a name="b-updating-multiple-columns"></a>2. 여러 열 업데이트  
 다음 예에서는 `Bonus` 테이블의 모든 행에 대해 `CommissionPct`, `SalesQuota` 및 `SalesPerson` 열의 값을 업데이트합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET Bonus = 6000, CommissionPct = .10, SalesQuota = NULL;  
GO  
```  
  
###  <a name="LimitingValues"></a>업데이트 되는 행 제한  
 이 섹션의 예에서는 UPDATE 문의 영향을 받는 행 수를 제한하는 데 사용할 수 있는 방법을 보여 줍니다.  
  
#### <a name="c-using-the-where-clause"></a>3. WHERE 절 사용  
 다음 예에서는 WHERE 절을 사용하여 업데이트할 행을 지정합니다. 이 문은 `Color` 테이블에서 `Production.Product` 열의 기존 값이 'Red'이고 `Color` 열의 값이 'Road-250'으로 시작하는 모든 행에 대해 `Name` 열의 값을 업데이트합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Product  
SET Color = N'Metallic Red'  
WHERE Name LIKE N'Road-250%' AND Color = N'Red';  
GO  
```  
  
#### <a name="d-using-the-top-clause"></a>4. TOP 절 사용  
 다음 예에서는 UPDATE 문에 TOP 절을 사용하여 수정되는 행 수를 제한합니다. Top (*n*) 절을 사용 하 여 업데이트, 업데이트 작업을 임의로 선택에서 수행 됩니다 '*n*' 개 행입니다. 다음 예에서는 `VacationHours` 테이블에 있는 임의의 10개 행의 `Employee` 열을 25% 업데이트합니다.  
  
```sql  
USE AdventureWorks2012;
GO
UPDATE TOP (10) HumanResources.Employee
SET VacationHours = VacationHours * 1.25 ;
GO  
```  
  
 TOP를 사용하여 의미 있는 연대순으로 업데이트를 적용해야 할 경우 하위 SELECT 문에서 TOP를 ORDER BY와 함께 사용해야 합니다. 다음 예에서는 채용일이 가장 빠른 직원 10명의 휴가 기간을 업데이트합니다.  
  
```sql  
UPDATE HumanResources.Employee  
SET VacationHours = VacationHours + 8  
FROM (SELECT TOP 10 BusinessEntityID FROM HumanResources.Employee  
     ORDER BY HireDate ASC) AS th  
WHERE HumanResources.Employee.BusinessEntityID = th.BusinessEntityID;  
GO  
```  
  
#### <a name="e-using-the-with-commontableexpression-clause"></a>5. WITH common_table_expression 절 사용  
 다음 예에서는 `PerAssemnblyQty`을 만드는 데 직접 또는 간접적으로 사용되는 모든 부분과 구성 요소의 `ProductAssemblyID 800` 값을 업데이트합니다. 공통 테이블 식은 `ProductAssemblyID 800`를 만드는 데 직접 사용되는 부분 및 해당 구성 요소를 만드는 데 사용되는 부분과 같은 식으로 이어지는 계층적 목록을 반환합니다. 이렇게 공통 테이블 식이 반환한 행만 수정됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
UPDATE Production.BillOfMaterials  
SET PerAssemblyQty = c.PerAssemblyQty * 2  
FROM Production.BillOfMaterials AS c  
JOIN Parts AS d ON c.ProductAssemblyID = d.AssemblyID  
WHERE d.ComponentLevel = 0;  
```  
  
#### <a name="f-using-the-where-current-of-clause"></a>6. WHERE CURRENT OF 절 사용  
 다음 예에서는 WHERE CURRENT OF 절을 사용하여 커서가 있는 행만 업데이트합니다. 커서가 조인을 기반으로 할 경우 UPDATE 문에 지정된 `table_name`만 수정되고 커서에 사용한 다른 테이블은 영향을 받지 않습니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE complex_cursor CURSOR FOR  
    SELECT a.BusinessEntityID  
    FROM HumanResources.EmployeePayHistory AS a  
    WHERE RateChangeDate <>   
         (SELECT MAX(RateChangeDate)  
          FROM HumanResources.EmployeePayHistory AS b  
          WHERE a.BusinessEntityID = b.BusinessEntityID) ;  
OPEN complex_cursor;  
FETCH FROM complex_cursor;  
UPDATE HumanResources.EmployeePayHistory  
SET PayFrequency = 2   
WHERE CURRENT OF complex_cursor;  
CLOSE complex_cursor;  
DEALLOCATE complex_cursor;  
GO  
```  
  
###  <a name="ColumnValues"></a>열 값 설정  
 이 섹션의 예에서는 계산 값, 하위 쿼리 및 DEFAULT 값을 사용하여 열을 업데이트하는 방법을 보여 줍니다.  
  
#### <a name="g-specifying-a-computed-value"></a>7. 계산 값 지정  
 다음 예에서는 UPDATE 문에 계산 값을 사용합니다. 이 예에서는 `ListPrice` 테이블의 모든 행에 대해 `Product` 열의 값을 두 배로 만듭니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
UPDATE Production.Product  
SET ListPrice = ListPrice * 2;  
GO  
```  
  
#### <a name="h-specifying-a-compound-operator"></a>8. 복합 연산자 지정  
 다음 예에서는 `@NewPrice` 변수를 사용하여 현재 가격을 가져오고 여기에 10을 더하여 모든 빨간색 자전거의 가격을 올립니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @NewPrice int = 10;  
UPDATE Production.Product  
SET ListPrice += @NewPrice  
WHERE Color = N'Red';  
GO  
```  
  
 다음 예에서는 += 복합 연산자를 사용하여 `' - tool malfunction'`가 10에서 12 사이인 행에 대해 `Name` 열의 기존 값에 `ScrapReasonID`을 추가합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.ScrapReason   
SET Name += ' - tool malfunction'  
WHERE ScrapReasonID BETWEEN 10 and 12;  
```  
  
#### <a name="i-specifying-a-subquery-in-the-set-clause"></a>9. SET 절에 하위 쿼리 지정  
 다음 예에서는 SET 절에 하위 쿼리를 사용하여 열을 업데이트하는 데 사용되는 값을 확인합니다. 이 하위 쿼리는 스칼라 값, 즉 각 행에 대해 단일 값을 반환해야 합니다. 이 예에서는 `SalesYTD` 테이블의 `SalesPerson` 열을 변경하여 `SalesOrderHeader` 테이블의 가장 최근 판매 기록을 반영합니다. 하위 쿼리는 `UPDATE` 문에서 각 영업 사원의 판매를 집계합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD +   
    (SELECT SUM(so.SubTotal)   
     FROM Sales.SalesOrderHeader AS so  
     WHERE so.OrderDate = (SELECT MAX(OrderDate)  
                           FROM Sales.SalesOrderHeader AS so2  
                           WHERE so2.SalesPersonID = so.SalesPersonID)  
     AND Sales.SalesPerson.BusinessEntityID = so.SalesPersonID  
     GROUP BY so.SalesPersonID);  
GO  
```  
  
#### <a name="j-updating-rows-using-default-values"></a>10. DEFAULT 값을 사용하여 행 업데이트  
 다음 예에서는 `CostRate` 값이 `CostRate`보다 큰 모든 행에 대해 `20.00` 열을 기본값(0.00)으로 설정합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Location  
SET CostRate = DEFAULT  
WHERE CostRate > 20.00;  
```  
  
###  <a name="TargetObjects"></a>표준 테이블 이외의 대상 개체 지정  
 이 섹션의 예에서는 뷰, 테이블 별칭 또는 테이블 변수를 지정하여 행을 업데이트하는 방법을 보여 줍니다.  
  
#### <a name="k-specifying-a-view-as-the-target-object"></a>11. 뷰를 대상 개체로 지정  
 다음 예에서는 뷰를 대상 개체로 지정하여 테이블의 행을 업데이트합니다. 뷰 정의에서는 여러 테이블을 참조하지만 UPDATE 문은 기본 테이블 중 하나의 열만 참조하므로 성공적으로 실행됩니다. 모든 테이블의 열을 지정하면 UPDATE 문이 실패합니다. 자세한 내용은 참조 [수정 데이터 뷰를 통해](../../relational-databases/views/modify-data-through-a-view.md)합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Person.vStateProvinceCountryRegion  
SET CountryRegionName = 'United States of America'  
WHERE CountryRegionName = 'United States';  
```  
  
#### <a name="l-specifying-a-table-alias-as-the-target-object"></a>12. 테이블 별칭을 대상 개체로 지정  
 다음 예에서는 `Production.ScrapReason` 테이블의 행을 업데이트합니다. FROM 절에서 `ScrapReason`에 할당된 테이블 별칭은 UPDATE 절에서 대상 개체로 지정됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE sr  
SET sr.Name += ' - tool malfunction'  
FROM Production.ScrapReason AS sr  
JOIN Production.WorkOrder AS wo   
     ON sr.ScrapReasonID = wo.ScrapReasonID  
     AND wo.ScrappedQty > 300;  
```  
  
#### <a name="m-specifying-a-table-variable-as-the-target-object"></a>13. 테이블 변수를 대상 개체로 지정  
 다음 예에서는 테이블 변수의 행을 업데이트합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create the table variable.  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    NewVacationHours int,  
    ModifiedDate datetime);  
  
-- Populate the table variable with employee ID values from HumanResources.Employee.  
INSERT INTO @MyTableVar (EmpID)  
    SELECT BusinessEntityID FROM HumanResources.Employee;  
  
-- Update columns in the table variable.  
UPDATE @MyTableVar  
SET NewVacationHours = e.VacationHours + 20,  
    ModifiedDate = GETDATE()  
FROM HumanResources.Employee AS e   
WHERE e.BusinessEntityID = EmpID;  
  
-- Display the results of the UPDATE statement.  
SELECT EmpID, NewVacationHours, ModifiedDate FROM @MyTableVar  
ORDER BY EmpID;  
GO  
```  
  
###  <a name="OtherTables"></a>다른 테이블의 데이터를 기반으로 하는 데이터 업데이트  
 이 섹션의 예에서는 한 테이블의 행을 다른 테이블의 정보에 따라 업데이트하는 방법을 보여 줍니다.  
  
#### <a name="n-using-the-update-statement-with-information-from-another-table"></a>14. 다른 테이블의 정보와 함께 UPDATE 문 사용  
 다음 예에서는 `SalesYTD` 테이블의 `SalesPerson` 열을 변경하여 `SalesOrderHeader` 테이블의 가장 최근 판매 기록을 반영합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD + SubTotal  
FROM Sales.SalesPerson AS sp  
JOIN Sales.SalesOrderHeader AS so  
    ON sp.BusinessEntityID = so.SalesPersonID  
    AND so.OrderDate = (SELECT MAX(OrderDate)  
                        FROM Sales.SalesOrderHeader  
                        WHERE SalesPersonID = sp.BusinessEntityID);  
GO  
```  
  
 앞의 예에서는 특정 날짜에 지정된 판매 직원에 대해 하나의 판매 정보만 기록되고 테이블이 최신 상태로 업데이트된 상태라고 가정합니다. 지정된 판매 직원에 대해 두 건 이상의 판매 정보를 같은 날 기록할 수 있는 경우 이 예는 제대로 실행되지 않습니다. 이 예제에서는 실행 되지만 각 오류 없이 `SalesYTD` 값이 해당 날짜에 판매 실적에 관계 없이 하나의 판매와 업데이트 합니다. 이는 하나의 UPDATE 문이 같은 행을 두 번 업데이트하지 않기 때문입니다.  
  
 지정된 판매 직원에 대해 하루에 두 번 이상의 판매가 발생할 수 있는 상황에서 각 판매 직원에 대한 모든 판매 정보는 다음 예와 같이 `UPDATE` 문 내에서 함께 집계되어야 합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD +   
    (SELECT SUM(so.SubTotal)   
     FROM Sales.SalesOrderHeader AS so  
     WHERE so.OrderDate = (SELECT MAX(OrderDate)  
                           FROM Sales.SalesOrderHeader AS so2  
                           WHERE so2.SalesPersonID = so.SalesPersonID)  
     AND Sales.SalesPerson.BusinessEntityID = so.SalesPersonID  
     GROUP BY so.SalesPersonID);  
GO  
```  
  
###  <a name="RemoteTables"></a>원격 테이블의 행 업데이트  
 이 섹션의 예를 사용 하 여 원격 대상 테이블의 행을 업데이트 하는 방법을 보여 주기는 [연결 된 서버](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 또는 [행 집합 함수](../../t-sql/functions/rowset-functions-transact-sql.md) 원격 테이블을 참조 합니다.  
  
#### <a name="o-updating-data-in-a-remote-table-by-using-a-linked-server"></a>15. 연결된 서버를 사용하여 원격 테이블의 데이터 업데이트  
 다음 예에서는 원격 서버의 테이블을 업데이트합니다. 사용 하 여 원격 데이터 원본에 대 한 링크 만들기 먼저 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)합니다. 그런 다음 연결된 서버 이름 `MyLinkServer`가 server.catalog.schema.object와 같이 네 부분으로 구성된 개체 이름의 일부로 지정됩니다. `@datasrc`에는 유효한 서버 이름을 지정해야 합니다.  
  
```sql  
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' or 'server_nameinstance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI10',   
    @datasrc = N'<server name>',  
    @catalog = N'AdventureWorks2012';  
GO  
USE AdventureWorks2012;  
GO  
-- Specify the remote data source using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
UPDATE MyLinkServer.AdventureWorks2012.HumanResources.Department  
SET GroupName = N'Public Relations'  
WHERE DepartmentID = 4;  
```  
  
#### <a name="p-updating-data-in-a-remote-table-by-using-the-openquery-function"></a>16. OPENQUERY 함수를 사용하여 원격 테이블의 데이터 업데이트  
 지정 하 여 원격 테이블의 행을 업데이트 하는 다음 예제는 [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) 행 집합 함수입니다. 이 예에서는 이전 예에서 만든 연결된 서버 이름이 사용됩니다.  
  
```sql  
UPDATE OPENQUERY (MyLinkServer, 'SELECT GroupName FROM HumanResources.Department WHERE DepartmentID = 4')   
SET GroupName = 'Sales and Marketing';  
```  
  
#### <a name="q-updating-data-in-a-remote-table-by-using-the-opendatasource-function"></a>17. OPENDATASOURCE 함수를 사용하여 원격 테이블의 데이터 업데이트  
 다음 예제에서는 지정 하 여 원격 테이블에 행을 삽입의 [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) 행 집합 함수입니다. 형식을 사용 하 여 데이터 원본에 대 한 올바른 서버 이름을 지정 *server_name* 또는 *server_name\instance_name*합니다. 임시 분산 쿼리에 맞게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 구성해야 할 수 있습니다. 자세한 내용은 참조 [임시 분산 쿼리 서버 구성 옵션](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md)합니다.  
  
```sql  
UPDATE OPENQUERY (MyLinkServer, 'SELECT GroupName FROM HumanResources.Department WHERE DepartmentID = 4')   
SET GroupName = 'Sales and Marketing';  
```  
  
###  <a name="LOBValues"></a>큰 개체 데이터 형식 업데이트  
 이 섹션의 예에서는 LOB(Large Object) 데이터 형식을 사용하여 정의된 열의 값을 업데이트하는 방법을 보여 줍니다.  
  
#### <a name="r-using-update-with-write-to-modify-data-in-an-nvarcharmax-column"></a>18. UPDATE를 .WRITE와 함께 사용하여 nvarchar(max) 열의 데이터 수정  
 다음 예제에서는 사용 하 여 여 합니다. 부분 값을 업데이트 하려면 WRITE 절 `DocumentSummary`, **nvarchar (max)** 열에는 `Production.Document` 테이블입니다. 대체 단어, 기존 데이터에서 대체할 단어의 시작 위치(오프셋) 및 대체할 문자 수(길이)를 지정하여 `components`를 `features`로 대체합니다. 또한이 예제에서는 OUTPUT 절을 반환 하는 이전 및 이후 이미지는 `DocumentSummary` 열을는 `@MyTableVar` 테이블 변수입니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    SummaryBefore nvarchar(max),  
    SummaryAfter nvarchar(max));  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
OUTPUT deleted.DocumentSummary,   
       inserted.DocumentSummary   
    INTO @MyTableVar  
WHERE Title = N'Front Reflector Bracket Installation';  
SELECT SummaryBefore, SummaryAfter   
FROM @MyTableVar;  
GO  
```  
  
#### <a name="s-using-update-with-write-to-add-and-remove-data-in-an-nvarcharmax-column"></a>S.는 UPDATE를 .WRITE와 함께 사용하여 nvarchar(max) 열의 데이터 추가 및 제거  
 다음 예에서는 추가 하 고 데이터를 제거는 **nvarchar (max)** NULL로 설정 된 현재 값이 있는 열입니다. 때문에 합니다. NULL 열을 수정 하려면 절을 사용할 수 없습니다, 열이 먼저 임시 데이터로 채워져 작성 합니다. 그런 다음 .WRITE 절을 사용하여 이 데이터를 올바른 데이터로 대체합니다. 다음 추가 예에서는 열 값의 끝에 데이터를 추가하고 열에서 데이터를 제거(잘라내기)하고 마지막으로 열에서 일부 데이터를 제거합니다. SELECT 문은 각각의 UPDATE 문에 의한 데이터 수정 내용을 표시합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Replacing NULL value with temporary data.  
UPDATE Production.Document  
SET DocumentSummary = N'Replacing NULL value'  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Replacing temporary data with the correct data. Setting @Length to NULL   
-- truncates all existing data from the @Offset position.  
UPDATE Production.Document  
SET DocumentSummary .WRITE(N'Carefully inspect and maintain the tires and crank arms.',0,NULL)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Appending additional data to the end of the column by setting   
-- @Offset to NULL.  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N' Appending data to the end of the column.', NULL, 0)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Removing all data from @Offset to the end of the existing value by   
-- setting expression to NULL.   
UPDATE Production.Document  
SET DocumentSummary .WRITE (NULL, 56, 0)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Removing partial data beginning at position 9 and ending at   
-- position 21.  
UPDATE Production.Document  
SET DocumentSummary .WRITE ('',9, 12)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
```  
  
#### <a name="t-using-update-with-openrowset-to-modify-a-varbinarymax-column"></a>20. UPDATE를 OPENROWSET와 함께 사용하여 varbinary(max) 열 수정  
 다음 예제에서는 대체에 저장 된 기존 이미지는 **varbinary (max)** 새 이미지가 포함 된 열입니다. [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 함수는 열에 이미지를 로드 하 고 BULK 옵션을 함께 사용 합니다. 이 예에서는 지정된 파일 경로에 `Tires.jpg`라는 이름의 파일이 존재하는 것으로 가정합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.ProductPhoto  
SET ThumbNailPhoto = (  
    SELECT *  
    FROM OPENROWSET(BULK 'c:Tires.jpg', SINGLE_BLOB) AS x )  
WHERE ProductPhotoID = 1;  
GO  
```  
  
#### <a name="u-using-update-to-modify-filestream-data"></a>21. UPDATE를 사용하여 FILESTREAM 데이터 수정  
 다음 예에서는 UPDATE 문을 사용하여 파일 시스템 파일의 데이터를 수정합니다. 많은 양의 데이터를 파일로 스트리밍하는 데는 이 방법을 사용하지 않는 것이 좋습니다. 적절한 Win32 인터페이스를 사용해야 합니다. 다음 예에서는 파일 레코드에 있는 임의의 텍스트를 `Xray 1`로 바꿉니다. 자세한 내용은 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)을 참조하세요.  
  
```sql  
UPDATE Archive.dbo.Records  
SET [Chart] = CAST('Xray 1' as varbinary(max))  
WHERE [SerialNumber] = 2;  
```  
  
###  <a name="UDTs"></a>사용자 정의 형식 업데이트  
 다음 예에서는 CLR UDT(사용자 정의 형식) 열의 값을 수정하는 세 가지 방법을 보여 줍니다. 사용자 정의 열에 대 한 자세한 내용은 참조 [clr 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)합니다.  
  
#### <a name="v-using-a-system-data-type"></a>22. 시스템 데이터 형식 사용  
 사용자 정의 형식에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식의 암시적 또는 명시적 변환이 지원되는 경우 해당 형식의 값을 제공하여 UDT를 업데이트할 수 있습니다. 다음 예에서는 문자열에서 명시적 변환을 통해 사용자 정의 형식인 `Point` 열의 값을 업데이트하는 방법을 보여 줍니다.  
  
```sql  
UPDATE dbo.Cities  
SET Location = CONVERT(Point, '12.3:46.2')  
WHERE Name = 'Anchorage';  
```  
  
#### <a name="w-invoking-a-method"></a>W. 메서드 호출  
 변경자(mutator)로 표시된 사용자 정의 형식의 메서드를 호출하여 업데이트를 수행하는 방법으로 UDT를 업데이트할 수 있습니다. 다음 예에서는 `Point`라는 `SetXY` 유형의 변경자 메서드를 호출합니다. 해당 유형의 인스턴스 상태가 업데이트됩니다.  
  
```sql  
UPDATE dbo.Cities  
SET Location.SetXY(23.5, 23.5)  
WHERE Name = 'Anchorage';  
```  
  
#### <a name="x-modifying-the-value-of-a-property-or-data-member"></a>X입니다. 속성 또는 데이터 멤버의 값 수정  
 등록된 속성 또는 사용자 정의 형식의 공용 데이터 멤버 값을 수정하여 UDT를 업데이트할 수 있습니다. 값을 제공하는 식은 암시적으로 해당 속성 유형으로 변환할 수 있어야 합니다. 다음 예에서는 사용자 정의 형식 `X`의 `Point` 속성 값을 수정합니다.  
  
```sql  
UPDATE dbo.Cities  
SET Location.X = 23.5  
WHERE Name = 'Anchorage';  
```  
  
###  <a name="TableHints"></a>힌트를 사용 하 여 쿼리 최적화 프로그램의 기본 동작 재정의  
 이 섹션의 예에서는 UPDATE 문을 처리할 때 쿼리 최적화 프로그램의 기본 동작을 임시로 재정의하기 위해 테이블 및 쿼리 힌트를 사용하는 방법을 보여 줍니다.  
  
> [!CAUTION]  
>  일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 쿼리에 대해 최상의 실행 계획을 선택하므로 숙련된 개발자 및 데이터베이스 관리자가 마지막 방법으로만 힌트를 사용하는 것이 좋습니다.  
  
#### <a name="y-specifying-a-table-hint"></a>Y입니다. 테이블 힌트 지정  
 다음 예에서는 지정 된 [테이블 힌트](../../t-sql/queries/hints-transact-sql-table.md) TABLOCK 합니다. 이 힌트는 `Production.Product` 테이블에 공유 잠금을 사용하고 UPDATE 문이 끝날 때까지 이 잠금을 유지하도록 지정합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Product  
WITH (TABLOCK)  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE 'BK-%';  
GO  
```  
  
#### <a name="z-specifying-a-query-hint"></a>Z 합니다. 쿼리 힌트 지정  
 다음 예에서는 지정 된 [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md) `OPTIMIZE FOR (@variable)` UPDATE 문의 합니다. 이 힌트는 쿼리가 컴파일되고 최적화될 때 쿼리 최적화 프로그램이 지역 변수에 대해 특정 값을 사용하도록 지시합니다. 해당 값은 쿼리 최적화 중에만 사용되고 쿼리 실행 중에는 사용되지 않습니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE Production.uspProductUpdate  
@Product nvarchar(25)  
AS  
SET NOCOUNT ON;  
UPDATE Production.Product  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE @Product  
OPTION (OPTIMIZE FOR (@Product = 'BK-%') );  
GO  
-- Execute the stored procedure   
EXEC Production.uspProductUpdate 'BK-%';  
```  
  
###  <a name="CaptureResults"></a>UPDATE 문의 결과 캡처  
 이 섹션의 예에 사용 하는 방법을 보여 줍니다는 [OUTPUT 절](../../t-sql/queries/output-clause-transact-sql.md) UPDATE 문에 의해 영향을 각 행의 정보 또는 식을 기반으로 돌아갑니다. 이러한 결과를 처리 응용 프로그램에 반환하여 확인 메시지, 보관 및 기타 응용 프로그램 요구 사항을 충족시키는 데 사용할 수 있습니다.  
  
#### <a name="aa-using-update-with-the-output-clause"></a>AA 합니다. OUTPUT 절과 함께 UPDATE 사용  
 다음 예에서는 `VacationHours` 테이블의 처음 10개 행에 대해 `Employee` 열을 25% 업데이트하고 `ModifiedDate` 열의 값을 현재 날짜로 설정합니다. `OUTPUT` 의 값을 반환 하는 절 `VacationHours` 적용 하기 전에 존재 하는 `UPDATE` 에서 문을 `deleted.VacationHours` 열과 업데이트 된 값에는 `inserted.VacationHours` 열을는 `@MyTableVar` 테이블 변수입니다.  
  
 각각 `SELECT`의 값과 `@MyTableVar` 테이블의 업데이트 작업 결과를 반환하는 두 개의 `Employee` 문이 이어집니다. OUTPUT 절을 사용 하 여 더 많은 예제를 참조 하십시오. [OUTPUT 절 &#40; Transact SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()   
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
###  <a name="Other"></a>다른 문에서 UPDATE 사용  
 이 섹션의 예에서는 다른 문에 UPDATE를 사용하는 방법을 보여 줍니다.  
  
#### <a name="ab-using-update-in-a-stored-procedure"></a>AB. 저장 프로시저에 UPDATE 사용  
 다음 예에서는 저장 프로시저에 UPDATE 문을 사용합니다. 이 프로시저에서는 `@NewHours`라는 입력 매개 변수 하나와 `@RowCount`라는 출력 매개 변수 하나를 사용합니다. `@NewHours` 매개 변수 값은 UPDATE 문이 열을 업데이트 사용 `VacationHours` 표에 `HumanResources.Employee`합니다. `@RowCount` 출력 매개 변수는 영향을 받는 행 수를 지역 변수에 반환하는 데 사용됩니다. SET 절에 사용된 CASE 식은 `VacationHours`에 대해 설정되는 값을 조건에 따라 결정합니다. 시간당 급여를 받는 직원(`SalariedFlag` = 0)의 경우 현재 시간 수에 `VacationHours`에 지정된 값을 더한 값으로 `@NewHours`가 설정되고, 그 외의 경우에는 `VacationHours`에 지정된 값으로 `@NewHours`가 설정됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE HumanResources.Update_VacationHours  
@NewHours smallint  
AS   
SET NOCOUNT ON;  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN SalariedFlag = 0 THEN VacationHours + @NewHours  
         ELSE @NewHours  
       END  
    )  
WHERE CurrentFlag = 1;  
GO  
  
EXEC HumanResources.Update_VacationHours 40;  
```  
  
#### <a name="ac-using-update-in-a-trycatch-block"></a>AC 합니다. TRY…CATCH 블록에 UPDATE 사용  
 다음 예제에서는 UPDATE 문을 사용 하 여 try... CATCH 블록 업데이트 작업 중 발생할 수 있는 실행 오류를 처리 합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
  
BEGIN TRY  
    -- Intentionally generate a constraint violation error.  
    UPDATE HumanResources.Department  
    SET Name = N'MyNewName'  
    WHERE DepartmentID BETWEEN 1 AND 2;  
END TRY  
BEGIN CATCH  
    SELECT   
         ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
  
    IF @@TRANCOUNT > 0  
        ROLLBACK TRANSACTION;  
END CATCH;  
  
IF @@TRANCOUNT > 0  
    COMMIT TRANSACTION;  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="ad-using-a-simple-update-statement"></a>AD 합니다. 단순 UPDATE 문 사용  
 다음 예제에서는 보여 모든 행의 영향을 받을 수 있는 방법 WHERE 절 사용 하지 않는 경우 업데이트 하는 행 (또는 행)을 지정할 수 있습니다.  
  
 값을 업데이트 하는이 예제는 `EndDate` 및 `CurrentFlag` 의 모든 행에 대 한 열은 `DimEmployee` 테이블입니다.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET EndDate = '2010-12-31', CurrentFlag='False';  
```  
  
 UPDATE 문에서 계산된 값을 사용할 수도 있습니다. 다음 예에서는 `ListPrice` 테이블의 모든 행에 대해 `Product` 열의 값을 두 배로 만듭니다.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET BaseRate = BaseRate * 2;  
```  
  
### <a name="ae-using-the-update-statement-with-a-where-clause"></a>AE 합니다. WHERE 절과 함께 UPDATE 문 사용  
 다음 예에서는 WHERE 절을 사용하여 업데이트할 행을 지정합니다.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET FirstName = 'Gail'  
WHERE EmployeeKey = 500;  
```  
  
### <a name="af-using-the-update-statement-with-label"></a>AF 합니다. 레이블이 있는 UPDATE 문 사용  
 다음 예에서는 UPDATE 문에 대 한 레이블의 사용 방법을 보여 줍니다.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimProduct  
SET ProductSubcategoryKey = 2   
WHERE ProductKey = 313  
OPTION (LABEL = N'label1');  
```  
  
### <a name="ag-using-the-update-statement-with-information-from-another-table"></a>AG 합니다. 다른 테이블의 정보와 함께 UPDATE 문 사용  
 이 예에서는 연도별 총 판매액을 저장 하는 테이블을 만듭니다. 2004 년의 총 판매액 FactInternetSales 테이블에 대해 SELECT 문을 실행 하 여 업데이트 합니다.  
  
```sql  
-- Uses AdventureWorks  
  
CREATE TABLE YearlyTotalSales (  
    YearlySalesAmount money NOT NULL,  
    Year smallint NOT NULL )  
WITH ( DISTRIBUTION = REPLICATE );  
  
INSERT INTO YearlyTotalSales VALUES (0, 2004);  
INSERT INTO YearlyTotalSales VALUES (0, 2005);  
INSERT INTO YearlyTotalSales VALUES (0, 2006);  
  
UPDATE YearlyTotalSales  
SET YearlySalesAmount=  
(SELECT SUM(SalesAmount) FROM FactInternetSales WHERE OrderDateKey >=20040000 AND OrderDateKey < 20050000)  
WHERE Year=2004;  
  
SELECT * FROM YearlyTotalSales;   
```  

### <a name="ah-ansi-join-replacement-for-update-statements"></a>아 합니다. Update 문에 대 한 ANSI 조인 대체
UPDATE 또는 DELETE를 수행 하려면 ANSI 조인 구문을 사용 하 여 함께 두 개 이상의 테이블을 조인 하는 복잡 한 업데이트가 있는 알 수 있습니다.  

이 테이블을 업데이트 해야 했습니다 같이 가정해 봅니다.  

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(   [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,   [CalendarYear]                  SMALLINT        NOT NULL
,   [TotalSalesAmount]              MONEY           NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;  
```

원래 쿼리 다음과 같이 보지 못했을 수 있습니다.  

```
UPDATE  acs
SET     [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT  [EnglishProductCategoryName]
        ,       [CalendarYear]
        ,       SUM([SalesAmount])              AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]       AS s
        JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
        JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
        WHERE   [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,       [CalendarYear]
        ) AS fis
ON  [acs].[EnglishProductCategoryName]  = [fis].[EnglishProductCategoryName]
AND [acs].[CalendarYear]                = [fis].[CalendarYear]
;  
```

이후 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] ANSI는 UPDATE 문의 FROM 절에 조인 하는 지원 하지 않습니다, 약간 변경 하지 않고 위에이 코드를 복사할 수 없습니다.  

이 코드를 바꾸려면 CTAS에는 및 암시적 조인을의 조합을 사용할 수 있습니다.  

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT  ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,       ISNULL(CAST([CalendarYear] AS SMALLINT),0)                      AS [CalendarYear]
,       ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                     AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]       AS s
JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
WHERE   [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,       [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```
  
## <a name="see-also"></a>관련 항목:  
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [커서&#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [텍스트 및 이미지 함수 &#40; Transact SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [Common_table_expression &AMP;#40; Transact SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)   
 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
  
  
