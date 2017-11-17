---
title: "(Transact SQL)에서 | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JOIN
- FROM_TSQL
- FROM
- JOIN_TSQL
- CROSS_TSQL
- CROSS_APPLY_TSQL
- APPLY_TSQL
- CROSS_JOIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- OUTER APPLY operator
- hints [SQL Server], FROM clause
- SELECT statement [SQL Server], FROM clause
- ISO syntax
- DELETE statement [SQL Server], FROM clause
- CROSS APPLY operator
- FROM clause
- APPLY operator
- joins [SQL Server], FROM clause
- UPDATE statement [SQL Server], FROM clause
- derived tables
ms.assetid: 36b19e68-94f6-4539-aeb1-79f5312e4263
caps.latest.revision: 97
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 6ae83ccf18cac45339d63e4ce1326c72a58c0339
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="from-transact-sql"></a>FROM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 DELETE, SELECT, UPDATE 문에 사용되는 테이블, 뷰, 파생된 테이블 문 조인된 테이블을 지정합니다. SELECT 문에서 SELECT 목록에 상수, 변수 및 산술식(열 이름 없이)만 포함되는 경우를 제외하고는 FROM 절이 필요합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ FROM { <table_source> } [ ,...n ] ]   
<table_source> ::=   
{  
    table_or_view_name [ [ AS ] table_alias ]   
        [ <tablesample_clause> ]   
        [ WITH ( < table_hint > [ [ , ]...n ] ) ]   
    | rowset_function [ [ AS ] table_alias ]   
        [ ( bulk_column_alias [ ,...n ] ) ]   
    | user_defined_function [ [ AS ] table_alias ]  
    | OPENXML <openxml_clause>   
    | derived_table [ [ AS ] table_alias ] [ ( column_alias [ ,...n ] ) ]   
    | <joined_table>   
    | <pivoted_table>   
    | <unpivoted_table>  
    | @variable [ [ AS ] table_alias ]  
    | @variable.function_call ( expression [ ,...n ] )   
        [ [ AS ] table_alias ] [ (column_alias [ ,...n ] ) ]  
    | FOR SYSTEM_TIME <system_time>   
}  
<tablesample_clause> ::=  
    TABLESAMPLE [SYSTEM] ( sample_number [ PERCENT | ROWS ] )   
        [ REPEATABLE ( repeat_seed ) ]   
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON <search_condition>   
    | <table_source> CROSS JOIN <table_source>   
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
<join_type> ::=   
    [ { INNER | { { LEFT | RIGHT | FULL } [ OUTER ] } } [ <join_hint> ] ]  
    JOIN  
  
<pivoted_table> ::=  
    table_source PIVOT <pivot_clause> [ [ AS ] table_alias ]  
  
<pivot_clause> ::=  
        ( aggregate_function ( value_column [ [ , ]...n ])   
        FOR pivot_column   
        IN ( <column_list> )   
    )   
  
<unpivoted_table> ::=  
    table_source UNPIVOT <unpivot_clause> [ [ AS ] table_alias ]  
  
<unpivot_clause> ::=  
    ( value_column FOR pivot_column IN ( <column_list> ) )   
  
<column_list> ::=  
    column_name [ ,...n ]   
  
<system_time> ::=  
{  
       AS OF <date_time>  
    |  FROM <start_date_time> TO <end_date_time>  
    |  BETWEEN <start_date_time> AND <end_date_time>  
    |  CONTAINED IN (<start_date_time> , <end_date_time>)   
    |  ALL  
}  
  
    <date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <start_date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <end_date_time>::=  
        <date_time_literal> | @date_time_variable  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
FROM { <table_source> [ ,...n ] }  
  
<table_source> ::=   
{  
    [ database_name . [ schema_name ] . | schema_name . ] table_or_view_name [ AS ] table_or_view_alias  
    | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]  
    | <joined_table>  
}  
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON search_condition   
    | <table_source> CROSS JOIN <table_source> 
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
  
<join_type> ::=   
    [ INNER ] [ <join hint> ] JOIN  
    | LEFT  [ OUTER ] JOIN  
    | RIGHT [ OUTER ] JOIN  
    | FULL  [ OUTER ] JOIN  
  
<join_hint> ::=   
    REDUCE  
    | REPLICATE  
    | REDISTRIBUTE  
```  
  
## <a name="arguments"></a>인수  
\<b l e _ >  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 사용할 테이블, 뷰, 테이블 변수 또는 파생된 테이블 원본을 별칭과 함께 또는 별칭 없이 지정합니다. 사용 가능한 메모리 및 쿼리에 있는 다른 식의 복잡성에 따라 다르지만 최대 256개의 테이블 원본을 문에 사용할 수 있습니다. 개별 쿼리는 최대 256개 테이블 원본을 지원하지 않을 수 있습니다.  
  
> [!NOTE]  
>  쿼리에서 많은 수의 테이블을 참조하면 쿼리 성능이 저하될 수 있습니다. 컴파일 및 최적화 시간 역시 다른 요소들의 영향을 받습니다. 여기에 인덱스 및 인덱싱된 뷰의 각 있는지 \<b l e _ >와의 크기는 \<select_list > SELECT 문에 합니다.  
  
 FROM 키워드 뒤의 테이블 원본 순서는 반환되는 결과 집합에 영향을 주지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FROM 절에 중복된 이름이 있으면 오류를 반환합니다.  
  
 *table_or_view_name*  
 테이블 또는 뷰의 이름입니다.  
  
 테이블 또는 뷰의의 같은 인스턴스 상에 다른 데이터베이스에 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 형태로 정규화 된 이름을 사용 하 여 *데이터베이스*. *스키마*. *object_name*합니다.  
  
 테이블 또는 뷰의의 인스턴스 밖에 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]l, 폼 네 부분으로 된 이름을 사용 하 여 *linked_server*. *카탈로그*. *스키마*. *개체*합니다. 자세한 내용은 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)의 데이터에 액세스하는 방법을 보여 줍니다. 네 부분으로 된 이름을 사용 하 여 생성 되는 [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) 작동 이름의 서버 부분은 원격 테이블 원본을 지정 하려면 사용할 수도 있습니다. OPENDATASOURCE는 지정 된 경우 *database_name* 및 *schema_name* 원격 개체에 액세스 하는 OLE DB 공급자의 기능에 따라 되며 모든 데이터 원본에는 적용 되지 않을 수 있습니다.  
  
 [로] *table_alias*  
 에 대 한 별칭은 *b l e _* 편의 위해 또는 하려면 테이블 또는 뷰 자체 조인에서 구분 또는 하위 쿼리는 사용할 수 있는 합니다. 별칭은 조인 내의 테이블의 특정 열을 지칭하는 데 사용하는 단축 테이블 이름인 경우가 많습니다. 동일한 열 이름을 조인에서 둘 이상의 테이블에 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열 이름은 테이블 이름, 뷰 이름 또는 별칭으로 한정 되어야 있어야 합니다. 별칭이 정의되어 있으면 테이블 이름을 사용할 수 없습니다.  
  
 파생된 테이블, 행 집합 또는 테이블 반환 함수 또는 연산자 절 (예: PIVOT 또는 UNPIVOT) 사용 되는 경우, 필요한 *table_alias* 절 끝에는 모든 열을 포함 하는 그룹화 열에 대 한 연결 된 테이블 이름 반환 됩니다.  
  
 와 (\<테이블 힌트 >)  
 쿼리 최적화 프로그램이 이 테이블과 이 문에 최적화 또는 잠금 전략을 사용하도록 지정합니다. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
 *rowset_function*  

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  

  
 테이블 참조 대신 사용할 수 있는 개체를 반환하는 행 집합 함수 중 하나(예: OPENROWSET)를 지정합니다. 행 집합 함수는 목록에 대 한 자세한 내용은 참조 [행 집합 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/rowset-functions-transact-sql.md).  
  
 OPENROWSET 및 OPENQUERY 함수를 사용하여 원격 개체를 지정하는 것은 개체를 액세스하는 OLE DB 공급자의 기능에 따라 달라집니다.  
  
 *bulk_column_alias*  

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  

  
 결과 집합의 열 이름을 대체할 선택적인 별칭입니다. 열의 별칭은 BULK 옵션과 함께 OPENROWSET 함수를 사용하는 SELECT 문에서만 허용됩니다. 사용 하는 경우 *bulk_column_alias*, 파일의 열과 동일한 순서로 모든 테이블 열에 별칭을 지정 합니다.  
  
> [!NOTE]  
>  이 별칭은 XML 서식 파일(있는 경우)의 COLUMN 요소에 있는 NAME 특성보다 우선합니다.  
  
 *user_defined_function*  
 테이블 반환 함수를 지정합니다.  
  
 OPENXML \<openxml_clause >  

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  

  
 XML 문서를 통해 행 집합 뷰를 제공합니다. 자세한 내용은 참조 [OPENXML &#40; Transact SQL &#41; ](../../t-sql/functions/openxml-transact-sql.md).  
  
 *파생 _ 테이블*  
 데이터베이스의 행을 검색하는 하위 쿼리입니다. *파생 _ 테이블* 외부 쿼리에 대 한 입력으로 사용 됩니다.  
  
 *파생 된* *_table* צ ְ ײ는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 테이블 값 생성자 기능을 여러 행을 지정 합니다. `SELECT * FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);`)을 입력합니다. 자세한 내용은 참조 [테이블 값 생성자 &#40; Transact SQL &#41; ](../../t-sql/queries/table-value-constructor-transact-sql.md).  
  
 *column_alias를 사용할*  
 파생된 테이블의 결과 집합에서 열 이름을 대체할 선택적인 별칭입니다. SELECT 목록의 각 열당 한 개의 열 별칭을 포함하고 열 별칭의 전체 목록을 괄호로 묶습니다.  
  
 *table_or_view_name* FOR SYSTEM_TIME \<system_time >  

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  

  
 지정 된 데이터의 특정 버전을 지정된 된 임시 테이블 및 연결 된 시스템 버전 관리 기록 테이블에서 반환 됩니다.  
  
\<tablesample_clause >  
 테이블의 데이터 샘플이 반환되도록 지정합니다. 샘플은 근사치일 수 있습니다. 이 절은 SELECT, UPDATE 또는 DELETE 문에서 기본 테이블 또는 조인된 테이블에 사용될 수 있습니다. 뷰를 대상으로 TABLESAMPLE을 지정할 수는 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드된 데이터베이스에 대해 TABLESAMPLE을 사용할 때는 데이터베이스의 호환성 수준을 110 이상으로 설정해야 합니다. PIVOT이 CTE(공통 테이블 식) 쿼리에서 허용되지 않습니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
 SYSTEM  
 ISO 표준에 의해 지정된 구현 방식에 따라 달라지는 샘플링 방법입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 방법이 사용 가능한 유일한 샘플링 방법이므로 기본적으로 적용됩니다. SYSTEM은 테이블의 임의 페이지 집합을 샘플로 선택하는 페이지 기반 샘플링 방법을 적용하고 해당 페이지의 모든 행을 샘플 하위 집합으로 반환합니다.  
  
 *sample_number*  
 행의 비율 또는 개수를 나타내는 정확하거나 대략적인 상수 식입니다. %로 지정 되 면 *sample_number* 암시적으로 변환 됩니다는 **float** 값; 그렇지 않은 경우 변환할 **bigint**합니다. PERCENT는 기본값입니다.  
  
 PERCENT  
 지정 하는 *sample_number* 테이블에서 테이블의 행 비율을 검색 해야 합니다. PERCENT를 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 지정된 비율에 가장 가까운 결과를 반환합니다. % 지정 된 경우에 *sample_number* 식은 0에서 100 사이의 값으로 계산 되어야 합니다.  
  
 ROWS  
 약 지정 *sample_number* 행 검색 됩니다. ROWS가 지정되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 지정된 행 개수에 가장 가까운 결과를 반환합니다. ROWS가 지정 된 *sample_number* 식은 0 보다 큰 정수 값으로 계산 되어야 합니다.  
  
 REPEATABLE  
 선택된 샘플이 다시 반환될 수 있음을 나타냅니다. 동일한로 지정 되 면 *repeat_seed* 값 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 으로 변경 테이블의 모든 행에 적용 된 행의 동일한 하위 집합을 반환 합니다. 지정 된 여러 개의 *repeat_seed* 값 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 몇 가지 다른 샘플 테이블의 행을 반환 합니다. 테이블에 대한 삽입, 업데이트, 삭제, 인덱스 다시 작성, 인덱스 조각 모음, 데이터베이스 복원 및 데이터베이스 연결 동작은 변경 사항으로 간주됩니다.  
  
 *repeat_seed*  
 난수를 생성하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 상수 식입니다. *repeat_seed* 은 **bigint**합니다. 경우 *repeat_seed* 를 지정 하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값을 임의로 할당 합니다. 특정 *repeat_seed* 값을 샘플링 결과 항상 동일한 변경 테이블에 적용 된 경우. *repeat_seed* 식은 0 보다 큰 정수로 계산 되어야 합니다.  
  
 \<조인 된 테이블 >  
 두 개 이상의 테이블을 곱한 결과 집합입니다. 여러 조인이 있을 경우 괄호를 사용하여 조인의 기본 순서를 바꿀 수 있습니다.  
  
\<조인 유형 >  
 조인 작업의 유형을 지정합니다.  
  
 **내부**  
 일치하는 모든 행의 쌍이 반환되도록 지정합니다. 양 테이블에서 서로 일치하지 않는 행은 제외됩니다. 조인 유형을 지정하지 않는 경우 이것이 기본값입니다.  
  
 FULL [OUTER]  
 조인 조건에 맞지 않는 왼쪽 또는 오른쪽 테이블의 행을 결과 집합에 포함시키고 다른 테이블에 해당되는 출력 열을 NULL로 설정하도록 지정합니다. 여기에는 INNER JOIN에서 일반적으로 반환되는 모든 행도 포함됩니다.  
  
 LEFT [OUTER]  
 왼쪽 테이블에서 조인 조건에 맞지 않는 모든 행을 결과 집합에 포함시키고 내부 조인에서 반환된 모든 행과 오른쪽 테이블의 출력 열을 NULL로 설정하도록 지정합니다.  
  
 RIGHT [OUTER]  
 오른쪽 테이블에서 조인 조건에 맞지 않는 모든 행을 결과 집합에 포함하고 내부 조인에서 반환된 모든 행과 다른 테이블에 해당되는 출력 열을 NULL로 설정하도록 지정합니다.  
  
\<알아서 >  
 에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]를 지정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 쿼리의 FROM 절에 지정 된 조인 당 한 개의 조인 힌트, 즉 실행 알고리즘을 사용 합니다. 자세한 내용은 참조 [조인 힌트 &#40; Transact SQL &#41; ](../../t-sql/queries/hints-transact-sql-join.md).  
  
 에 대 한 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이러한 조인 힌트는 INNER 조인의 두 배포 호환 되지 않는 열에에 적용 합니다. 쿼리 처리 중에 발생 하는 데이터 이동의 양을 제한 하 여 쿼리 성능을 향상 시킬 수 있습니다. 에 대 한 허용 가능한 조인 힌트 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 는 다음과 같습니다.  
  
 줄이기  
 테이블에 대 한 두 배포 호환 되지 않는 테이블을 호환 되도록 하기 위해 조인의 오른쪽에 이동할 수는 행의 수를 줄입니다. REDUCE 힌트는 세미 조인 힌트를 라고도 합니다.  
  
 REPLICATE  
 모든 노드에 복제 조인의 왼쪽에 있는 테이블의 조인 열에서 값을 발생 합니다. 오른쪽에 있는 테이블은 이러한 열을 복제 된 버전으로 조인 됩니다.  
  
 재배포  
 JOIN 절에 지정 된 열에 배포 하기 강제로 두 데이터 원본. 분산된 테이블에 대 한 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 순서 섞기 이동을 수행 합니다. 복제 된 테이블에 대 한 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 트림 이동을 수행 합니다. 이러한 이동 유형을 이해 하려면 "쿼리 계획 이해" 항목에 있는 "DMS 쿼리 계획 작업" 섹션을 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다. 이 힌트는 쿼리 계획은 브로드캐스트 이동을 사용 하 여 해결 배포 호환 되지 않는 조인 하는 경우 성능을 향상 시킬 수 있습니다.  
  
 JOIN  
 지정된 테이블 원본 또는 뷰 간에 지정된 조인 작업이 이루어져야 함을 나타냅니다.  
  
 ON \<c h _ c >  
 조인의 기준이 되는 조건을 지정합니다. 열과 비교 연산자를 주로 사용하지만 조건에서는 모든 조건자를 지정할 수 있습니다. 예를 들어 다음과 같습니다.  
  
```tsql
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);  
  
```  
  
 조건에 지정된 열은 이름이나 데이터 형식이 동일할 필요는 없습니다. 하지만 데이터 형식이 다를 경우 서로 호환이 가능하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 암시적으로 변환할 수 있는 형식이어야 합니다. 데이터 형식을 암시적으로 변환할 수 없을 경우 조건에서는 CONVERT 함수를 사용하여 데이터 형식을 명시적으로 변환해야 합니다.  
  
 ON 절에 단 하나의 조인된 테이블을 수반하는 조건자가 있을 수 있습니다. 또한 쿼리의 WHERE 절에도 이러한 조건자가 있을 수 있습니다. INNER 조인의 경우에는 이러한 조건자가 있어도 아무런 차이가 없지만 OUTER 조인에는 다른 결과가 만들어질 수 있습니다. ON 절의 조건자는 조인 이전의 테이블에 적용되는 반면 WHERE 절은 기능적으로 조인의 결과에 적용되기 때문입니다.  
  
 검색 조건과 조건자에 대 한 자세한 내용은 참조 [검색 조건 &#40; Transact SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
 CROSS JOIN  
 두 테이블의 교차곱을 지정합니다. SQL-92 형식이 아닌 이전 형식의 조인에서 WHERE 절이 지정되지 않은 경우와 동일한 행을 반환합니다.  
  
 *left_table_source* {교차 | (를) OUTER APPLY *right_table_source*  
 지정 된 *right_table_source* 의 APPLY 연산자의 모든 행에 대해 계산 됩니다는 *left_table_source*합니다. 이 기능을 유용는 *right_table_source* 의 열 값을 사용 하는 테이블 반환 함수를 포함 된 *left_table_source* 인수 중 하나로 합니다.  
  
 CROSS 또는 OUTER를 APPLY와 함께 지정해야 합니다. CROSS를 지정 하는 경우 아무 행도 생성 때는 *right_table_source* 의 지정된 된 행에 대해 평가 됩니다는 *left_table_source* 빈 결과 집합을 반환 합니다.  
  
 각 행에 대해 하나의 행이 생성 OUTER를 지정 하는 경우는 *left_table_source* 경우에는 *right_table_source* 해당 행에 대해 계산 하 고 빈 결과 집합을 반환 합니다.  
  
 자세한 내용은 주의 섹션을 참조하세요.  
  
 *left_table_source*  
 이전 인수에 정의된 테이블 원본입니다. 자세한 내용은 주의 섹션을 참조하세요.  
  
 *right_table_source*  
 이전 인수에 정의된 테이블 원본입니다. 자세한 내용은 주의 섹션을 참조하세요.  
  
 *테이블 원본* 피벗 \<pivot_clause >  
 지정 된 *b l e _* 에 따라 피벗는 *pivot_column*합니다. *테이블 원본* 는 테이블 또는 테이블 식입니다. 출력의 모든 열이 포함 된 테이블은는 *b l e _* 제외 하 고는 *pivot_column* 및 *value_column*합니다. 열에는 *b l e _*를 제외 하 고는 *pivot_column* 및 *value_column*, pivot 연산자의 그룹화 열 이라고 합니다. PIVOT 및 UNPIVOT 하는 방법에 대 한 자세한 내용은 참조 [를 사용 하 여 PIVOT 및 UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md)합니다.  
  
 PIVOT은 그룹화 열과 관련해 입력 테이블에서 그룹화 연산을 수행하고 각각의 그룹마다 한 개의 행을 반환합니다. 또한 출력에 지정 된 각 값에 대 한 하나의 열에 포함 되어는 *column_list* 에 표시 되는 *pivot_column* 의 *input_table*합니다.  
  
 자세한 내용은 다음에 나오는 주의 섹션을 참조하세요.  
  
 *aggregate_function*  
 하나 이상의 입력을 받는 시스템 또는 사용자 정의 집계 함수입니다. 집계 함수는 Null 값에 따라 결과가 달라지지 않아야 합니다. Null 값에 영향을 받지 않는 집계 함수는 집계 값을 계산하는 동안 그룹의 Null 값을 계산에 감안하지 않습니다.  
  
 COUNT(*) 시스템 집계 함수는 허용되지 않습니다.  
  
 *value_column*  
 PIVOT 연산자의 값 열입니다. UNPIVOT과 함께 사용할 때 *value_column* 입력의 기존 열 이름이 될 수 없습니다 *b l e _*합니다.  
  
 에 대 한 *pivot_column*  
 PIVOT 연산자의 피벗 열입니다. *pivot_column* 로 암시적으로 또는 명시적으로 변환할 수는 형식 이어야 합니다 **nvarchar()**합니다. 이 열이 될 수 없는 **이미지** 또는 **rowversion**합니다.  
  
 UNPIVOT을 사용할 경우 *pivot_column* 에서 좁혀진 출력 열의 이름인는 *b l e _*합니다. 기존 열 수 없습니다 *b l e _* 해당 이름의 합니다.  
  
 IN (*column_list* )  
 에 따라 피벗 절에 값을 나열는 *pivot_column* 고유 출력 테이블의 열 이름입니다. 목록 입력에 이미 존재 하는 열 이름을 지정할 수 없습니다 *b l e _* 피벗 되는 합니다.  
  
 UNPIVOT 절에 열이 나열 *b l e _* 를 하나의 좁혀 질 *pivot_column*합니다.  
  
 *table_alias*  
 출력 테이블의 별칭 이름입니다. *pivot_table_alias* 지정 해야 합니다.  
  
 UNPIVOT \< unpivot_clause >  
 입력된 테이블의 여러 열에서 범위를 좁힙니다 지정 *column_list* 라는 하나의 열으로 *pivot_column*합니다. PIVOT 및 UNPIVOT 하는 방법에 대 한 자세한 내용은 참조 [를 사용 하 여 PIVOT 및 UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md)합니다.  
  
 일부로 \<날짜 _ 시간 >  

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  

  
 과거의 지정된 시간에 실제(현재)였던 값이 포함된 각 행에 대한 단일 레코드를 포함하는 테이블을 반환합니다. 내부적으로 임시 테이블과 기록 테이블 간에 합집합이 및에 지정 된 시간에 유효 했던 행의 값을 반환 하도록 결과가 필터링 되는  *\<날짜 _ 시간 >* 매개 변수입니다. 행에 대 한 값의 유효성을 확인 하는 경우는 *system_start_time_column_name* 값 보다 작거나 같음는  *\<날짜 _ 시간 >* 매개 변수 값 및 *system_end_time_ column_name* 값 보다 크면는  *\<날짜 _ 시간 >* 매개 변수 값입니다.   
  
 \<start_date_time > TO \<end_date_time >

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.

  
 시작 하기 전에 활성 되었든 관계 없이 지정 된 시간 범위 내에 활성 상태 였던 모든 레코드 버전에 대 한 값이 있는 테이블이 반환는  *\<start_date_time >* FROM에 대 한 매개 변수 값 인수 또는 후에 활성화 되 고 상태가 중단 된  *\<end_date_time >* TO 인수에 대 한 매개 변수 값입니다. 내부적으로 temporal 테이블과 기록 테이블 간에 합집합이 계산되며, 지정된 시간 범위 중 임의의 시점에 활성 상태였던 모든 행 버전을 반환하도록 결과가 필터링됩니다. 정확히 FROM 끝점으로 정의 된 하위 경계에서 활성화 하는 행 포함 되며 정확히 TO 끝점으로 정의 된 상위 경계에서 활성화 된 행이 포함 되지 않습니다.  
  
 사이의 \<start_date_time > AND \<end_date_time >  

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  
  
 위와에 **FROM \<start_date_time > TO \<end_date_time >** 설명에 정의 된 상위 경계에서 활성화 된 행을 포함 하는 제외는 \<end_date_time > 끝점입니다.  
  
 CONTAINED IN (\<start_date_time >, \<end_date_time >)  

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  

  
 CONTAINED IN 인수에 대한 두 개의 datetime 값으로 정의된 지정된 시간 범위 내에 열리고 닫힌 모든 레코드 버전의 값을 포함하는 테이블을 반환합니다. 정확히 하위 경계에서 활성화되거나 상위 경계에서 활성 상태가 중단된 행이 포함됩니다.  
  
 ALL  
 현재 테이블과 기록 테이블의 모든 행에서 값을 가진 테이블을 반환합니다.  
  
## <a name="remarks"></a>주의  
 FROM 절은 조인된 테이블과 파생된 테이블에 대해 SQL-92-SQL 구문을 지원합니다. SQL-92 구문은 INNER, LEFT OUTER, RIGHT OUTER, FULL OUTER, CROSS 조인 연산자를 제공합니다.  
  
 FROM 절의 UNION과 JOIN은 뷰, 파생된 테이블 및 하위 쿼리에서 지원됩니다.  
  
 자체 조인은 자신을 조인하는 테이블을 말합니다. 자체 조인을 기반으로 하는 삽입이나 업데이트 작업은 FROM 절에 지정된 순서를 따릅니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 열 배포 통계를 제공하는 연결된 서버에서 배포 통계와 카디널리티 통계를 고려하므로, 조인을 원격에서 수행하기 위해 REMOTE 조인 힌트가 필요하지는 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 프로세서는 원격 통계를 고려하여 원격 조인 전략이 적절한지 결정합니다. REMOTE 조인 힌트는 열 배포 통계를 제공하지 않는 공급자에게 유용합니다.  
  
## <a name="using-apply"></a>APPLY 사용  
 APPLY 연산자의 좌우 피연산자는 모두 테이블 식입니다. 이 피연산자 간의 주요 차이점은는 *right_table_source* 에서 열을 사용 하는 테이블 반환 함수를 사용할 수는 *left_table_source* 함수의 인수 중 하나로 합니다. *left_table_source* 테이블 반환 함수를 포함할 수 있지만 인수는 열을 포함할 수 없습니다는 *right_table_source*합니다.  
  
 APPLY 연산자는 다음과 같은 방식으로 FROM 절에 지정될 테이블 원본을 생성합니다.  
  
1.  평가 *right_table_source* 의 각 행에 대해는 *left_table_source* 를 행 집합을 생성 합니다.  
  
     값은 *right_table_source* 에 따라 달라 집니다 *left_table_source*합니다. *right_table_source* 이 같이 표현 될 수 있습니다: `TVF(left_table_source.row)`여기서 `TVF` 는 테이블 반환 함수입니다.  
  
2.  결과 집합을 결합 하 여 평가의 각 행에 대해 생성 될 *right_table_source* 와 *left_table_source* UNION ALL 연산을 수행 하 여 합니다.  
  
     APPLY 연산자의 결과로 생성 된 열 목록에서 열 집합은는 *left_table_source* 에서 열의 목록을 결합 하는 *right_table_source*합니다.  
  
## <a name="using-pivot-and-unpivot"></a>PIVOT 및 UNPIVOT 사용  
 *pivot_column* 및 *value_column* PIVOT 연산자에서 사용 되는 열이 그룹화 합니다. PIVOT은 다음과 같은 방식으로 출력 결과 집합을 가져옵니다.  
  
1.  에 대해 GROUP BY 수행 해당 *input_table* 는 그룹화 열과이 생성 한 개의 출력 행 각 그룹에 대 한 합니다.  
  
     출력 행의 그룹화 열에서 해당 그룹에 대 한 해당 열 값을 가져올는 *input_table*합니다.  
  
2.  다음 작업을 수행해 각각의 출력 행에 대한 열 목록의 열 값을 생성합니다.  
  
    1.  GROUP BY에 대해 이전 단계에서에서 생성 하는 행 그룹화는 *pivot_column*합니다.  
  
         각 출력 열에 대해서는 *column_list*, 조건을 충족 하는 하위 그룹을 선택 하면:  
  
         `pivot_column = CONVERT(<data type of pivot_column>, 'output_column')`  
  
    2.  *aggregate_function* 기준으로 평가 되는 *value_column* 이 하위 그룹 / 결과 해당 값으로 반환 됩니다 *output_column*합니다. 하위 그룹이 비어 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] null 값을 생성 하는 *output_column*합니다. 집계 함수가 COUNT이고 하위 그룹이 비어 있으면 0이 반환됩니다.  

> [!NOTE]
> 열 식별자는 `UNPIVOT` 카탈로그 데이터 정렬에 따라 절. 에 대 한 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 데이터 정렬은 항상 `SQL_Latin1_General_CP1_CI_AS`합니다. 에 대 한 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 부분적으로 포함 된 데이터베이스를 데이터 정렬은 항상 `Latin1_General_100_CI_AS_KS_WS_SC`합니다. 열은 다른 열을 다음 collate 절과 결합 되어 있으면 (`COLLATE DATABASE_DEFAULT`) 충돌을 방지 하려면 필요 합니다.   
  
 PIVOT 및 UNPIVOT 예제를 포함 하는 방법에 대 한 자세한 내용은 참조 [를 사용 하 여 PIVOT 및 UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 DELETE, SELECT 또는 UPDATE 문의 사용 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-a-simple-from-clause"></a>1. 간단한 FROM 절 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 샘플 데이터베이스에서 `TerritoryID` 테이블의 `Name` 및 `SalesTerritory`을 검색합니다.  
  
```tsql    
SELECT TerritoryID, Name  
FROM Sales.SalesTerritory  
ORDER BY TerritoryID ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
TerritoryID Name                            
----------- ------------------------------  
1           Northwest                       
2           Northeast                       
3           Central                         
4           Southwest                       
5           Southeast                       
6           Canada                          
7           France                          
8           Germany                         
9           Australia                       
10          United Kingdom                  
(10 row(s) affected)  
```  
  
### <a name="b-using-the-tablock-and-holdlock-optimizer-hints"></a>2. TABLOCK 및 HOLDLOCK 최적화 프로그램 힌트 사용  
 다음의 부분 트랜잭션은 `Employee`에 명시적인 공유 테이블 잠금을 설정하고 인덱스를 읽는 방법을 보여 줍니다. 잠금은 전체 트랜잭션 동안 유지됩니다.  
  
```tsql    
BEGIN TRAN  
SELECT COUNT(*)   
FROM HumanResources.Employee WITH (TABLOCK, HOLDLOCK) ;  
```  
  
### <a name="c-using-the-sql-92-cross-join-syntax"></a>3. SQL-92 CROSS JOIN 구문 사용  
 다음 예는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Employee` 및 `Department` 두 테이블의 교차곱을 반환합니다. 가능한 모든 조합 목록이 `BusinessEntityID` 행과 모든 `Department` 이름 행이 반환 됩니다.  
  
```wql    
SELECT e.BusinessEntityID, d.Name AS Department  
FROM HumanResources.Employee AS e  
CROSS JOIN HumanResources.Department AS d  
ORDER BY e.BusinessEntityID, d.Name ;  
```  
  
### <a name="d-using-the-sql-92-full-outer-join-syntax"></a>4. SQL-92 FULL OUTER JOIN 구문 사용  
 다음 예는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `SalesOrderDetail` 테이블의 제품 이름 및 해당되는 모든 판매 주문을 반환합니다. 또한 `Product` 테이블에 나열되어 있는 제품이 없는 모든 판매 주문, 그리고 `Product` 테이블에 나열된 것 이외의 주문된 모든 제품을 반환합니다.  
  
```tsql  
-- The OUTER keyword following the FULL keyword is optional.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
FULL OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="e-using-the-sql-92-left-outer-join-syntax"></a>5. SQL-92 LEFT OUTER JOIN 구문 사용  
 다음 예에서는 `ProductID`로 두 테이블을 조인하고 왼쪽 테이블에서 일치하지 않는 행도 함께 반환합니다. `Product` 테이블은 `SalesOrderDetail` 열에서 각 `ProductID` 테이블과 일치합니다. 모든 제품은 주문 여부에 관계없이 결과 집합에 나타납니다.  
  
```tsql    
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
LEFT OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="f-using-the-sql-92-inner-join-syntax"></a>6. SQL-92 INNER JOIN 구문 사용  
 다음 예에서는 모든 제품 이름과 판매 주문 ID를 반환합니다.  
  
```tsql    
-- By default, SQL Server performs an INNER JOIN if only the JOIN   
-- keyword is specified.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
INNER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="g-using-the-sql-92-right-outer-join-syntax"></a>7. SQL-92 RIGHT OUTER JOIN 구문 사용  
 다음 예에서는 `TerritoryID`로 두 테이블을 조인하고 오른쪽 테이블에서 일치하지 않는 행도 함께 반환합니다. `SalesTerritory` 테이블은 `SalesPerson` 열에서 각 `TerritoryID` 테이블과 일치합니다. 판매 직원에게 담당 구역이 할당되었는지 여부에 관계없이 모든 판매 직원이 결과 집합에 표시됩니다.  
  
```tsql    
SELECT st.Name AS Territory, sp.BusinessEntityID  
FROM Sales.SalesTerritory AS st   
RIGHT OUTER JOIN Sales.SalesPerson AS sp  
ON st.TerritoryID = sp.TerritoryID ;  
```  
  
### <a name="h-using-hash-and-merge-join-hints"></a>8. HASH 및 MERGE 조인 힌트 사용  
 다음 예에서는 `Product`, `ProductVendor` 및 `Vendor` 테이블 간의 3개 테이블 조인을 수행하여 제품 및 제품 공급업체 목록을 생성합니다. 쿼리 최적화 프로그램은 MERGE 조인을 사용하여 `Product`와 `ProductVendor`(`p`와 `pv`)를 조인합니다. 그런 다음 `Product`와 `ProductVendor`(`p`와 `pv`)의 MERGE 조인이 `Vendor` 테이블에 HASH 조인되어 (`p`와 `pv`) 및 `v`를 생성합니다.  
  
> [!IMPORTANT]  
>  조인 힌트를 지정한 이후에는 INNER 키워드가 더 이상 선택 사항이 아니며 INNER JOIN을 수행하도록 명시적으로 지정해야 합니다.  
  
```tsql    
SELECT p.Name AS ProductName, v.Name AS VendorName  
FROM Production.Product AS p   
INNER MERGE JOIN Purchasing.ProductVendor AS pv   
ON p.ProductID = pv.ProductID  
INNER HASH JOIN Purchasing.Vendor AS v  
ON pv.BusinessEntityID = v.BusinessEntityID  
ORDER BY p.Name, v.Name ;  
```  
  
### <a name="i-using-a-derived-table"></a>9. 파생된 테이블 사용  
 다음 예에서는 파생된 테이블과 `SELECT` 문을 `FROM` 절 다음에 사용하여 모든 직원의 성과 이름, 직원이 거주하는 도시를 반환합니다.  
  
```tsql    
SELECT RTRIM(p.FirstName) + ' ' + LTRIM(p.LastName) AS Name, d.City  
FROM Person.Person AS p  
INNER JOIN HumanResources.Employee e ON p.BusinessEntityID = e.BusinessEntityID   
INNER JOIN  
   (SELECT bea.BusinessEntityID, a.City   
    FROM Person.Address AS a  
    INNER JOIN Person.BusinessEntityAddress AS bea  
    ON a.AddressID = bea.AddressID) AS d  
ON p.BusinessEntityID = d.BusinessEntityID  
ORDER BY p.LastName, p.FirstName;  
```  
  
### <a name="j-using-tablesample-to-read-data-from-a-sample-of-rows-in-a-table"></a>10. TABLESAMPLE을 사용하여 테이블의 행 샘플 데이터 읽기  
 다음 예에서는 `TABLESAMPLE` 절에 `FROM`을 사용하여 `10` 테이블에 있는 모든 행 중 대략 `Customer` 퍼센트를 반환합니다.  
  
```tsql    
SELECT *  
FROM Sales.Customer TABLESAMPLE SYSTEM (10 PERCENT) ;  
```  
  
### <a name="k-using-apply"></a>11. APPLY 사용  
 다음 예에서는 다음 스키마를 가진 테이블이 데이터베이스에 존재하는 것으로 가정합니다.  
  
-   `Departments`: `DeptID`, `DivisionID`, `DeptName`, `DeptMgrID`  
  
-   `EmpMgr`: `MgrID`, `EmpID`  
  
-   `Employees`: `EmpID`, `EmpLastName`, `EmpFirstName`, `EmpSalary`  
  
 또 다른 테이블 반환 함수인 `GetReports(MgrID)`는 지정된 `EmpID`에 직접 또는 간접적으로 보고하는 모든 직원의 목록(`EmpLastName`, `EmpSalary`, `MgrID`)을 반환합니다.  
  
 이 예에서는 `APPLY`를 사용하여 모든 부서와 해당 부서의 모든 직원을 반환합니다. 특정 부서에 직원이 한 명도 없으면 해당 부서에 대해서는 행이 반환되지 않습니다.  
  
```tsql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d CROSS APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
 쿼리가 직원이 없는 부서의 행도 생성하도록 하려면 `EmpID`를 사용하세요. 이 때 `EmpLastName`, `EmpSalary` 및 `OUTER APPLY` 열에 대해서는 Null 값이 생성됩니다.  
  
```tsql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d OUTER APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
### <a name="l-using-cross-apply"></a>12. CROSS APPLY 사용  
 다음 예제는 `sys.dm_exec_cached_plans` 동적 관리 뷰를 쿼리하여 캐시에 있는 모든 쿼리 계획의 계획 핸들을 검색함으로써 계획 캐시에 있는 모든 쿼리 계획의 스냅숏을 검색합니다. 그런 다음 `CROSS APPLY`에 계획 핸들을 전달할 `sys.dm_exec_query_plan` 연산자를 지정합니다. 계획 캐시에 있는 각 계획의 XML 실행 계획 출력은 현재 반환된 테이블의 `query_plan` 열에 있습니다.  
  
```tsql
USE master;  
GO  
SELECT dbid, object_id, query_plan   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);   
GO  
```  
  
### <a name="m-using-for-systemtime"></a>13. FOR SYSTEM_TIME을 사용 하 여  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  
  
 다음 예제에서는 SYSTEM_TIME AS OF date_time_literal_or_variable 인수를 사용 하 여 실제 (현재) 2014 년 1 월 1 일을 기준으로 된 테이블 행을 반환 합니다.  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME AS OF '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 다음 예제에서는 date_time_literal_or_variable 인수에 FOR SYSTEM_TIME FROM date_time_literal_or_variable를 사용 하 여 2013 년 1 월 1 일부터 2014 년 1 월 1 일에 끝나는으로 정의 된 기간 동안 활성 상태 였던 모든 행을 반환 상위 경계 전용입니다.  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM '2013-01-01' TO '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 다음 예제에서는 사용에 대 한 SYSTEM_TIME 사이의 date_time_literal_or_variable 및 2013 년 1 월 1 일부터 2014 년 1 월 1 일에 끝나는으로 정의 된 기간 동안 활성화 된 모든 행을 반환할 date_time_literal_or_variable 인수 상위 경계 (포함).  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME BETWEEN '2013-01-01' AND '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 다음 예제에서는 FOR SYSTEM_TIME CONTAINED IN (date_time_literal_or_variable, date_time_literal_or_variable) 인수를에 열리고 닫힌 2013 년 1 월 1 일 시작 해 서 끝나는으로 정의 된 기간 동안 모든 행 반환 하려면 2014 년 1 월 1 일입니다.  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME CONTAINED IN ( '2013-01-01', '2014-01-01' )  
WHERE ManagerID = 5;
```  
  
 다음 예에서는 리터럴 대신 변수를 사용 하 여 쿼리에 대 한 날짜 경계 값을 제공 하도록 합니다.  
  
```tsql
DECLARE @AsOfFrom datetime2 = dateadd(month,-12, sysutcdatetime());
DECLARE @AsOfTo datetime2 = dateadd(month,-6, sysutcdatetime());
  
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM @AsOfFrom TO @AsOfTo  
WHERE ManagerID = 5;
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="n-using-the-inner-join-syntax"></a>14. INNER JOIN 구문 사용  
 다음 예제에서는 반환 된 `SalesOrderNumber`, `ProductKey`, 및 `EnglishProductName` 열을는 `FactInternetSales` 및 `DimProduct` where 테이블 조인 키 `ProductKey`, 두 테이블에서 일치 합니다. `SalesOrderNumber` 및 `EnglishProductName` 이러한 별칭은 가독성을 위해 포함; 열에는 각각 있으므로 같이 이러한 열이 있는 테이블 별칭을 지정할 필요가 없습니다만, 테이블 중 하나에 존재 합니다. 단어 **AS** 별칭 하기 전에 이름을 필요 하지 않지만 가독성을 높이기 위해 및 ANSI 표준을 준수 하는 것이 좋습니다.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
INNER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 이후는 `INNER` 키워드가 내부 조인에 필요 하지 않습니다이 동일한 쿼리를 작성할 수도 있습니다.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
ON dp.ProductKey = fis.ProductKey;  
```  
  
 A `WHERE` 절 사용 될 수도이 쿼리의 결과 제한 하려면. 이 예에서는 결과를 제한 `SalesOrderNumber` 'SO5000' 보다 높은 값:  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey  
WHERE fis.SalesOrderNumber > 'SO50000'  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="o-using-the-left-outer-join-and-right-outer-join-syntax"></a>15. LEFT OUTER JOIN 및 RIGHT OUTER JOIN 구문 사용  
 다음 예제에서는 조인을 `FactInternetSales` 및 `DimProduct` 테이블에 `ProductKey` 열입니다. 왼쪽에서 일치 하지 않는 행을 유지 하는 왼쪽된 우선 외부 조인 구문 (`FactInternetSales`) 테이블입니다. 이후는 `FactInternetSales` 테이블 포함 하지 않는 `ProductKey` 값과 일치 하지 않는 `DimProduct` 테이블이이 쿼리는 위의 첫 번째 내부 조인 예제와 같은 행을 반환 합니다.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
LEFT OUTER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 하지 않고이 쿼리를 작성할 수도 있습니다는 `OUTER` 키워드입니다.  
  
 오른쪽 우선 외부 조인, 오른쪽 테이블에서 일치 하지 않는 행이 유지 됩니다. 다음 예제에서는 위 왼쪽된 우선 외부 조인 예제와 같은 행을 반환 합니다.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM DimProduct AS dp 
RIGHT OUTER JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 다음 쿼리에서 `DimSalesTerritory` 왼쪽된 우선 외부 조인에 왼쪽 테이블로 테이블입니다. 검색 된 `SalesOrderNumber` 에서 값의 `FactInternetSales` 테이블입니다. 특정에 대 한 주문이 있는 경우 `SalesTerritoryKey`, 쿼리는 NULL을 반환 된 `SalesOrderNumber` 해당 행에 대 한 합니다. 이 쿼리 별로 정렬 되는 `SalesOrderNumber` 열이이 열에 Null 모든 있도록 나타납니다 결과 맨 위에 있는 합니다.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
LEFT OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 이 쿼리는 동일한 결과 검색 하려면 오른쪽 우선 외부 조인으로 다시 작성할 수 있습니다.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM FactInternetSales AS fis 
RIGHT OUTER JOIN DimSalesTerritory AS dst  
    ON fis.SalesTerritoryKey = dst.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="p-using-the-full-outer-join-syntax"></a>16. FULL OUTER JOIN 구문 사용  
 다음 예제에서는 완전 외부 조인은 조인 된 두 테이블에서 모든 행을 반환 하지만 다른 테이블에서 일치 하지 않는 값에 대 한 NULL을 반환 하는 방법을 보여 줍니다.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 하지 않고이 쿼리를 작성할 수도 있습니다는 `OUTER` 키워드입니다.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="q-using-the-cross-join-syntax"></a>17. CROSS JOIN 구문 사용  
 교차곱을 반환 하는 다음 예제는 `FactInternetSales` 및 `DimSalesTerritory` 테이블입니다. 가능한 모든 조합 목록이 `SalesOrderNumber` 및 `SalesTerritoryKey` 반환 됩니다. `ON` 크로스 조인 쿼리에서 절.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
CROSS JOIN FactInternetSales AS fis  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="r-using-a-derived-table"></a>18. 파생된 테이블 사용  
 파생된 테이블을 사용 하 여 다음 예제 (한 `SELECT` 다음 문으로 `FROM` 절) 반환 하는 `CustomerKey` 및 `LastName` 열에 있는 모든 고객의는 `DimCustomer` 테이블의 `BirthDate` 년 1 월 1 일 이후의 값 1970 및 성 'Smith'.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT CustomerKey, LastName  
FROM  
   (SELECT * FROM DimCustomer  
    WHERE BirthDate > '01/01/1970') AS DimCustomerDerivedTable  
WHERE LastName = 'Smith'  
ORDER BY LastName;  
```  
  
### <a name="s-reduce-join-hint-example"></a>S.는 조인 힌트 예제 줄이기  
 다음 예제에서는 `REDUCE` 쿼리 내에서 파생 된 테이블의 처리를 변경 하는 조인 힌트입니다. 사용 하는 경우는 `REDUCE` 이 쿼리에서 조인 힌트는 `fis.ProductKey` 프로젝션, 복제 및 distinct, 만든에 `DimProduct` 의 순서 섞기 중 `DimProduct` 에 `ProductKey`합니다. 결과 파생된 테이블에 배포 됩니다 `fis.ProductKey`합니다.  
  
```tsql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REDUCE JOIN FactInternetSales AS fis   
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="t-replicate-join-hint-example"></a>20. 복제 조인 힌트 예제  
 다음 예제에서는이 점을 제외 하 고 앞의 예제와 동일한 쿼리를 보여 줍니다.는 `REPLICATE` 대신 조인 힌트가 사용 되어는 `REDUCE` 조인 힌트입니다. 사용은 `REPLICATE` 힌트에 있는 값 사용 하면는 `ProductKey` (조인) 열에서는 `FactInternetSales` 테이블에 모든 노드에 대해 복제 합니다. `DimProduct` 테이블은 해당 값의 복제 된 버전에 조인 합니다.  
  
```tsql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REPLICATE JOIN FactInternetSales AS fis  
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="u-using-the-redistribute-hint-to-guarantee-a-shuffle-move-for-a-distribution-incompatible-join"></a>21. 배포 호환 되지 않는 조인에 대 한 순서 섞기 이동 되도록 REDISTRIBUTE 힌트를 사용 하 여  
 다음 쿼리는 배포 호환 되지 않는 조인에서 REDISTRIBUTE 쿼리 힌트를 사용합니다. 이렇게 하면 쿼리 최적화 프로그램이 쿼리 계획의 순서 섞기 이동을 사용 합니다. 이렇게 하면 복제 된 테이블에 분산된 테이블을 이동 하는 브로드캐스트 이동 쿼리 계획을 사용 하지 않습니다.  
  
 다음 예제에서는 REDISTRIBUTE 힌트 ProductKey DimProduct에 대 한 배포 열은 FactInternetSales에 대 한 배포 열 없기 때문에 FactInternetSales 테이블에서 순서 섞기 이동을 강제로 수행 합니다.  
  
```tsql
-- Uses AdventureWorks  
  
EXPLAIN  
SELECT dp.ProductKey, fis.SalesOrderNumber, fis.TotalProductCost  
FROM DimProduct AS dp 
INNER REDISTRIBUTE JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FREETEXTTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENQUERY &#40; Transact SQL &#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  

