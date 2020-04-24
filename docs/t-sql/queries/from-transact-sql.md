---
title: 'FROM: JOIN, APPLY, PIVOT (T-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 06/01/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 246cf0c526e04c5f4df33067286b0cefaf9913cd
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81636198"
---
# <a name="from-clause-plus-join-apply-pivot-transact-sql"></a>FROM 절과 JOIN, APPLY, PIVOT(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

Transact-SQL에서 FROM 절은 다음 명령문에서 사용할 수 있습니다.

- [DELETE](../statements/delete-transact-sql.md)
- [UPDATE](update-transact-sql.md)
- [SELECT](select-transact-sql.md)

일반적으로 FROM 절은 SELECT 문에 필요합니다. 예외는 테이블 열이 나열되지 않고 나열된 항목만 리터럴, 변수 또는 산술 식입니다.

이 문서에서는 FROM 절에서 사용할 수 있는 다음 키워드도 설명합니다.

- JOIN
- APPLY
- PIVOT

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
[ FROM { <table_source> } [ ,...n ] ]   
<table_source> ::=   
{  
    table_or_view_name [ FOR SYSTEM_TIME <system_time> ] [ AS ] table_alias ]   
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
  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
FROM { <table_source> [ ,...n ] }  
  
<table_source> ::=   
{  
    [ database_name . [ schema_name ] . | schema_name . ] table_or_view_name [ AS ] table_or_view_alias 
    [<tablesample_clause>]  
    | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]  
    | <joined_table>  
}  
  
<tablesample_clause> ::=
    TABLESAMPLE ( sample_number [ PERCENT ] ) -- SQL Data Warehouse only  
 
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
\<table_source>  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 사용할 테이블, 뷰, 테이블 변수 또는 파생된 테이블 원본을 별칭과 함께 또는 별칭 없이 지정합니다. 사용 가능한 메모리 및 쿼리에 있는 다른 식의 복잡성에 따라 다르지만 최대 256개의 테이블 원본을 문에 사용할 수 있습니다. 개별 쿼리는 최대 256개 테이블 원본을 지원하지 않을 수 있습니다.  
  
> [!NOTE]  
>  쿼리에서 많은 수의 테이블을 참조하면 쿼리 성능이 저하될 수 있습니다. 컴파일 및 최적화 시간 역시 다른 요소들의 영향을 받습니다. 여기에는 각 \<table_source>에 대한 인덱스 및 인덱싱된 뷰의 존재 여부와 SELECT 문의 \<select_list> 크기가 포함됩니다.  
  
 FROM 키워드 뒤의 테이블 원본 순서는 반환되는 결과 집합에 영향을 주지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FROM 절에 중복된 이름이 있으면 오류를 반환합니다.  
  
 *table_or_view_name*  
 테이블 또는 뷰의 이름입니다.  
  
 테이블 또는 뷰가 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 다른 데이터베이스에 있는 경우 *database*.*schema*.*object_name* 형식의 정규화된 이름을 사용합니다.  
  
 테이블 또는 뷰가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 외부에 있는 경우 네 부분으로 구성된 *linked_server*.*catalog*.*schema*.*object* 형식의 이름을 사용합니다. 자세한 내용은 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)의 데이터에 액세스하는 방법을 보여 줍니다. [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) 함수를 이름의 서버 부분으로 사용하여 생성되는 네 부분으로 구성된 이름은 원격 테이블 원본을 지정하는 데 사용할 수도 있습니다. OPENDATASOURCE가 지정되면 *database_name* 및 *schema_name*이 모든 데이터 원본에 적용되지 않을 수 있으며, 원격 개체에 액세스하는 OLE DB 공급자 기능이 적용됩니다.  
  
 [AS] *table_alias*  
 편의상 또는 자체 조인이나 하위 쿼리에서 테이블 또는 뷰를 구분하는 데 거나 편리하게 사용할 수 있는 *table_source*에 대한 별칭입니다. 별칭은 조인 내의 테이블의 특정 열을 지칭하는 데 사용하는 단축 테이블 이름인 경우가 많습니다. 조인에서 둘 이상의 테이블에 동일한 열 이름이 있는 경우, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 열 이름을 테이블 이름, 뷰 이름 또는 별칭으로 정규화해야 합니다. 별칭이 정의되어 있으면 테이블 이름을 사용할 수 없습니다.  
  
 파생 테이블, 행 집합, 테이블 반환 함수 또는 연산자 절(예: PIVOT 또는 UNPIVOT)을 사용하는 경우, 절의 끝 부분에 필요한 *table_alias*는 그룹화 열을 포함하여 반환되는 모든 열에 대해 연결된 테이블 이름입니다.  
  
 WITH (\<table_hint> )  
 쿼리 최적화 프로그램이 이 테이블과 이 문에 최적화 또는 잠금 전략을 사용하도록 지정합니다. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
 *rowset_function*  

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]  

  
 테이블 참조 대신 사용할 수 있는 개체를 반환하는 행 집합 함수 중 하나(예: OPENROWSET)를 지정합니다. 행 집합 함수의 목록에 자세한 내용은 [행 집합 함수&#40;Transact-SQL&#41;](../../t-sql/functions/rowset-functions-transact-sql.md)를 참조하세요.  
  
 OPENROWSET 및 OPENQUERY 함수를 사용하여 원격 개체를 지정하는 것은 개체를 액세스하는 OLE DB 공급자의 기능에 따라 달라집니다.  
  
 *bulk_column_alias*  

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]  

  
 결과 집합의 열 이름을 대체할 선택적인 별칭입니다. 열의 별칭은 BULK 옵션과 함께 OPENROWSET 함수를 사용하는 SELECT 문에서만 허용됩니다. *bulk_column_alias*를 사용하는 경우 파일의 열과 동일한 순서로 모든 테이블 열에 대한 별칭을 지정합니다.  
  
> [!NOTE]  
>  이 별칭은 XML 서식 파일(있는 경우)의 COLUMN 요소에 있는 NAME 특성보다 우선합니다.  
  
 *user_defined_function*  
 테이블 반환 함수를 지정합니다.  
  
 OPENXML \<openxml_clause>  

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]  

  
 XML 문서를 통해 행 집합 뷰를 제공합니다. 자세한 내용은 [OPENXML&#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)을 참조하세요.  
  
 *derived_table*  
 데이터베이스의 행을 검색하는 하위 쿼리입니다. *derived_table*은 외부 쿼리에 대한 입력으로 사용됩니다.  
  
 *derived* *_table*은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 테이블 값 생성자 기능을 사용하여 여러 행을 지정할 수 있습니다. `SELECT * FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);`)을 입력합니다. 자세한 내용은 [테이블 값 생성자&#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)를 참조하세요.  
  
 *column_alias*  
 파생된 테이블의 결과 집합에서 열 이름을 대체할 선택적인 별칭입니다. SELECT 목록의 각 열당 한 개의 열 별칭을 포함하고 열 별칭의 전체 목록을 괄호로 묶습니다.  
  
 *table_or_view_name* FOR SYSTEM_TIME \<system_time>  

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]  

  
 지정된 임시 테이블 및 연결된 해당 시스템 버전 관리 기록 테이블에서 특정 버전의 데이터가 반환되도록 지정합니다.  
  
### <a name="tablesample-clause"></a>Tablesample 절
**적용 대상:** SQL Server, SQL Database 
 
 테이블의 데이터 샘플이 반환되도록 지정합니다. 샘플은 근사치일 수 있습니다. 이 절은 SELECT 또는 UPDATE 문에서 기본 테이블 또는 조인된 테이블에 사용될 수 있습니다. 뷰를 대상으로 TABLESAMPLE을 지정할 수는 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드된 데이터베이스에 대해 TABLESAMPLE을 사용할 때는 데이터베이스의 호환성 수준을 110 이상으로 설정해야 합니다. PIVOT이 CTE(공통 테이블 식) 쿼리에서 허용되지 않습니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
 SYSTEM  
 ISO 표준에 의해 지정된 구현 방식에 따라 달라지는 샘플링 방법입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 방법이 사용 가능한 유일한 샘플링 방법이므로 기본적으로 적용됩니다. SYSTEM은 테이블의 임의 페이지 집합을 샘플로 선택하는 페이지 기반 샘플링 방법을 적용하고 해당 페이지의 모든 행을 샘플 하위 집합으로 반환합니다.  
  
 *sample_number*  
 행의 비율 또는 개수를 나타내는 정확하거나 대략적인 상수 식입니다. PERCENT를 사용하여 지정되는 경우 *sample_number*는 암시적으로 **float** 값으로 변환되며, 그렇지 않으면 **bigint**로 변환됩니다. PERCENT는 기본값입니다.  
  
 PERCENT  
 테이블에서 테이블 행의 *sample_number*%를 검색하도록 지정합니다. PERCENT를 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 지정된 비율에 가장 가까운 결과를 반환합니다. PERCENT가 지정되면 *sample_number* 식은 0부터 100까지의 값으로 계산되어야 합니다.  
  
 ROWS  
 대략 *sample_number*개의 행을 검색하도록 지정합니다. ROWS가 지정되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 지정된 행 개수에 가장 가까운 결과를 반환합니다. ROWS가 지정되면 *sample_number* 식은 0보다 큰 정수 값으로 계산되어야 합니다.  
  
 REPEATABLE  
 선택된 샘플이 다시 반환될 수 있음을 나타냅니다. 동일한 *repeat_seed* 값으로 지정되면 테이블의 모든 행이 변경되지 않은 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 동일한 행의 하위 집합을 반환합니다. 다른 *repeat_seed* 값으로 지정되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 테이블의 일부 다른 행 샘플을 반환합니다. 테이블에 대한 삽입, 업데이트, 삭제, 인덱스 다시 작성, 인덱스 조각 모음, 데이터베이스 복원 및 데이터베이스 연결 동작은 변경 사항으로 간주됩니다.  
  
 *repeat_seed*  
 난수를 생성하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 상수 식입니다. *repeat_seed*는 **bigint**입니다. *repeat_seed*를 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 임의로 값을 할당합니다. 테이블에 변경내용이 적용되지 않은 경우 특정 *repeat_seed* 값에 대한 샘플링 결과는 항상 동일합니다. *repeat_seed* 식은 0보다 큰 정수로 계산되어야 합니다.  
  
### <a name="tablesample-clause"></a>Tablesample 절
**적용 대상:** SQL Data Warehouse

 테이블의 데이터 샘플이 반환되도록 지정합니다. 샘플은 근사치일 수 있습니다. 이 절은 SELECT 또는 UPDATE 문에서 기본 테이블 또는 조인된 테이블에 사용될 수 있습니다. 뷰를 대상으로 TABLESAMPLE을 지정할 수는 없습니다. 

 PERCENT  
 테이블에서 테이블 행의 *sample_number*%를 검색하도록 지정합니다. PERCENT를 지정하면 SQL Data Warehouse는 지정된 비율에 가장 가까운 결과를 반환합니다. PERCENT가 지정되면 *sample_number* 식은 0부터 100까지의 값으로 계산되어야 합니다.  


### <a name="joined-table"></a>조인된 테이블 
조인된 테이블은 두 개 이상의 테이블을 곱한 결과 집합입니다. 여러 조인이 있을 경우 괄호를 사용하여 조인의 기본 순서를 바꿀 수 있습니다.  
  
### <a name="join-type"></a>조인 유형
조인 작업의 유형을 지정합니다.  
  
 INNER  
 일치하는 모든 행의 쌍이 반환되도록 지정합니다. 양 테이블에서 서로 일치하지 않는 행은 제외됩니다. 조인 유형을 지정하지 않는 경우 이것이 기본값입니다.  
  
 FULL [OUTER]  
 조인 조건에 맞지 않는 왼쪽 또는 오른쪽 테이블의 행을 결과 집합에 포함시키고 다른 테이블에 해당되는 출력 열을 NULL로 설정하도록 지정합니다. 여기에는 INNER JOIN에서 일반적으로 반환되는 모든 행도 포함됩니다.  
  
 LEFT [OUTER]  
 왼쪽 테이블에서 조인 조건에 맞지 않는 모든 행을 결과 집합에 포함시키고 내부 조인에서 반환된 모든 행과 오른쪽 테이블의 출력 열을 NULL로 설정하도록 지정합니다.  
  
 RIGHT [OUTER]  
 오른쪽 테이블에서 조인 조건에 맞지 않는 모든 행을 결과 집합에 포함하고 내부 조인에서 반환된 모든 행과 다른 테이블에 해당되는 출력 열을 NULL로 설정하도록 지정합니다.  
  
### <a name="join-hint"></a>조인 힌트  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램에서 쿼리의 FROM 절에 지정된 조인마다 하나의 조인 힌트 또는 실행 알고리즘을 사용하도록 지정합니다. 자세한 내용은 [조인 힌트#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-join.md)를 참조하세요.  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]의 경우 이러한 조인 힌트는 호환되지 않는 두 개의 배포 열에 대한 INNER 조인에 적용됩니다. 쿼리 처리 중에 발생하는 데이터 이동의 양을 제한하여 쿼리 성능을 향상시킬 수 있습니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 허용되는 조인 힌트는 다음과 같습니다.  
  
 REDUCE  
 호환되지 않는 두 개의 배포 테이블을 호환되도록 만들기 위해 조인의 오른쪽에 있는 테이블에 대해 이동할 행 수를 줄입니다. REDUCE 힌트는 세미조인 힌트라고도 합니다.  
  
 REPLICATE  
 조인의 왼쪽에 있는 테이블에서 조인 열의 값을 모든 노드로 복제합니다. 오른쪽 테이블은 복제된 버전의 해당 열과 조인됩니다.  
  
 REDISTRIBUTE  
 두 개의 데이터 원본이 JOIN 절에 지정된 열에 배포되도록 합니다. 분산된 테이블의 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 순서 섞기 이동을 수행합니다. 복제된 테이블의 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 자르기 이동을 수행합니다. 이러한 이동 유형을 이해하려면 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]의 "쿼리 계획 이해" 항목에 있는 "DMS 쿼리 계획 작업" 섹션을 참조하세요. 이 힌트는 쿼리 계획에서 브로드캐스트 이동을 사용하여 호환되지 않는 배포 조인을 해결할 때 성능을 향상시킬 수 있습니다.  
  
 JOIN  
 지정된 테이블 원본 또는 뷰 간에 지정된 조인 작업이 이루어져야 함을 나타냅니다.  
  
 ON \<search_condition>  
 조인의 기준이 되는 조건을 지정합니다. 열과 비교 연산자를 주로 사용하지만 조건에서는 모든 조건자를 지정할 수 있습니다. 예를 들어 다음과 같습니다.  
  
```sql
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);  
  
```  
  
 조건에 지정된 열은 이름이나 데이터 형식이 동일할 필요는 없습니다. 하지만 데이터 형식이 다를 경우 서로 호환이 가능하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 암시적으로 변환할 수 있는 형식이어야 합니다. 데이터 형식을 암시적으로 변환할 수 없을 경우 조건에서는 CONVERT 함수를 사용하여 데이터 형식을 명시적으로 변환해야 합니다.  
  
 ON 절에 단 하나의 조인된 테이블을 수반하는 조건자가 있을 수 있습니다. 또한 쿼리의 WHERE 절에도 이러한 조건자가 있을 수 있습니다. INNER 조인의 경우에는 이러한 조건자가 있어도 아무런 차이가 없지만 OUTER 조인에는 다른 결과가 만들어질 수 있습니다. ON 절의 조건자는 조인 이전의 테이블에 적용되는 반면 WHERE 절은 기능적으로 조인의 결과에 적용되기 때문입니다.  
  
 검색 조건 및 조건자에 대한 자세한 내용은 [검색 조건&#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)을 참조하세요.  
  
 CROSS JOIN  
 두 테이블의 교차곱을 지정합니다. SQL-92 형식이 아닌 이전 형식의 조인에서 WHERE 절이 지정되지 않은 경우와 동일한 행을 반환합니다.  
  
 *left_table_source* { CROSS | OUTER } APPLY *right_table_source*  
 APPLY 연산자의 *right_table_source*가 *left_table_source*의 모든 행에 대해 계산되도록 지정합니다. 이 기능은 *right_table_source*에 *left_table_source*의 열 값을 해당 인수 중 하나로 사용하는 테이블 반환 함수가 포함된 경우에 유용합니다.  
  
 CROSS 또는 OUTER를 APPLY와 함께 지정해야 합니다. CROSS가 지정되면 *right_table_source*가 *left_table_source*의 지정된 행에 대해 계산되고 빈 결과 집합을 반환할 때 아무 행도 생성되지 않습니다.  
  
 OUTER가 지정되면 *right_table_source*가 해당 행에 대해 계산되고 빈 결과 집합을 반환하는 경우에도 *left_table_source*의 각 행에 대한 하나의 행이 생성됩니다.  
  
 자세한 내용은 주의 섹션을 참조하세요.  
  
 *left_table_source*  
 이전 인수에 정의된 테이블 원본입니다. 자세한 내용은 주의 섹션을 참조하세요.  
  
 *right_table_source*  
 이전 인수에 정의된 테이블 원본입니다. 자세한 내용은 주의 섹션을 참조하세요.  
  
### <a name="pivot-clause"></a>PIVOT 절

 *table_source* PIVOT \<pivot_clause>  
 *table_source*가 *pivot_column*에 따라 피벗되도록 지정합니다. *table_source*는 테이블 또는 테이블 식입니다. 출력은 *pivot_column* 및 *value_column*을 제외한 *table_source*의 모든 열을 포함하는 테이블입니다. *pivot_column* 및 *value_column*을 제외한 *table_source*의 열은 PIVOT 연산자의 그룹화 열이라고 합니다. PIVOT 및 UNPIVOT에 대한 자세한 내용은 [PIVOT 및 UNPIVOT 사용](../../t-sql/queries/from-using-pivot-and-unpivot.md)을 참조하세요.  
  
 PIVOT은 그룹화 열과 관련해 입력 테이블에서 그룹화 연산을 수행하고 각각의 그룹마다 한 개의 행을 반환합니다. 또한 출력에는 *input_table*의 *pivot_column*에 나타나는 *column_list*에 지정된 각 값에 대한 하나의 열이 포함됩니다.  
  
 자세한 내용은 다음에 나오는 주의 섹션을 참조하세요.  
  
 *aggregate_function*  
 하나 이상의 입력을 받는 시스템 또는 사용자 정의 집계 함수입니다. 집계 함수는 Null 값에 따라 결과가 달라지지 않아야 합니다. Null 값에 영향을 받지 않는 집계 함수는 집계 값을 계산하는 동안 그룹의 Null 값을 계산에 감안하지 않습니다.  
  
 COUNT(*) 시스템 집계 함수는 허용되지 않습니다.  
  
 *value_column*  
 PIVOT 연산자의 값 열입니다. UNPIVOT과 함께 사용되면 *value_column*은 입력 *table_source*에 있는 기존 열의 이름이 될 수 없습니다.  
  
 FOR *pivot_column*  
 PIVOT 연산자의 피벗 열입니다. *pivot_column*은 암시적 또는 명시적으로 **nvarchar()** 로 변환할 수 있는 형식이어야 합니다. 이 열은 **image** 또는 **rowversion**일 수 없습니다.  
  
 UNPIVOT이 사용되면 *pivot_column*은 *table_source*에서 좁혀진 출력 열의 이름입니다. 해당 이름의 *table_source*에 기존 열이 있을 수 없습니다.  
  
 IN (*column_list* )  
 PIVOT 절에는 출력 테이블의 열 이름이 될 *pivot_column*의 값이 나열됩니다. 이 목록에는 피벗되는 입력 *table_source*에 이미 있는 열 이름이 지정될 수 없습니다.  
  
 UNPIVOT 절에는 단일 *pivot_column*으로 좁혀질 *table_source*의 열이 나열됩니다.  
  
 *table_alias*  
 출력 테이블의 별칭 이름입니다. *pivot_table_alias*는 지정해야 합니다.  
  
 UNPIVOT \<unpivot_clause>  
 입력 테이블이 *column_list*의 여러 열에서 *pivot_column*이라는 단일 열로 좁혀지도록 지정합니다. PIVOT 및 UNPIVOT에 대한 자세한 내용은 [PIVOT 및 UNPIVOT 사용](../../t-sql/queries/from-using-pivot-and-unpivot.md)을 참조하세요.  
  
 AS OF \<date_time>  

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]  

  
 과거의 지정된 시간에 실제(현재)였던 값이 포함된 각 행에 대한 단일 레코드를 포함하는 테이블을 반환합니다. 내부적으로 임시 테이블과 해당 기록 테이블 간에 합집합이 계산되고, 결과가 필터링되어 *\<date_time>* 매개 변수로 지정된 시점에 유효했던 행의 값을 반환합니다. *system_start_time_column_name* 값이 *\<date_time>* 매개 변수 값보다 작거나 같고, *system_end_time_column_name* 값이 *\<date_time>* 매개 변수 값보다 큰 경우 행에 대한 값이 유효한 것으로 간주됩니다.   
  
 FROM \<start_date_time> TO \<end_date_time>

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]

  
 FROM 인수에 대한 *\<start_date_time>* 매개 변수 값 이전에 활성 상태가 시작되었는지, 아니면 TO 인수에 대한 *\<end_date_time>* 매개 변수 값 이후에 활성 상태가 중단되었는지 여부에 관계없이, 지정된 시간 범위 내에 활성 상태였던 모든 레코드 버전에 대한 값이 포함된 테이블을 반환합니다. 내부적으로 temporal 테이블과 기록 테이블 간에 합집합이 계산되며, 지정된 시간 범위 중 임의의 시점에 활성 상태였던 모든 행 버전을 반환하도록 결과가 필터링됩니다. FROM 엔드포인트에서 정의된 하위 경계에서 정확히 활성화된 행은 포함되고, TO 엔드포인트에서 정의된 상위 경계에서 정확히 활성화된 행은 포함되지 않습니다.  
  
 BETWEEN \<start_date_time> AND \<end_date_time>  

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]  
  
 \<end_date_time> 엔드포인트에서 정의된 상위 경계에서 활성화된 행이 포함된다는 점을 제외하고는 위의 **FROM \<start_date_time> TO \<end_date_time>** 설명과 동일합니다.  
  
 CONTAINED IN (\<start_date_time> , \<end_date_time>)  

**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]  

  
 CONTAINED IN 인수에 대한 두 개의 datetime 값으로 정의된 지정된 시간 범위 내에 열리고 닫힌 모든 레코드 버전의 값을 포함하는 테이블을 반환합니다. 정확히 하위 경계에서 활성화되거나 상위 경계에서 활성 상태가 중단된 행이 포함됩니다.  
  
 ALL  
 현재 테이블과 기록 테이블의 모든 행에 있는 값이 포함된 테이블을 반환합니다.  
  
## <a name="remarks"></a>설명  
 FROM 절은 조인된 테이블과 파생된 테이블에 대해 SQL-92-SQL 구문을 지원합니다. SQL-92 구문은 INNER, LEFT OUTER, RIGHT OUTER, FULL OUTER, CROSS 조인 연산자를 제공합니다.  
  
 FROM 절의 UNION과 JOIN은 뷰, 파생된 테이블 및 하위 쿼리에서 지원됩니다.  
  
 자체 조인은 자신을 조인하는 테이블을 말합니다. 자체 조인을 기반으로 하는 삽입이나 업데이트 작업은 FROM 절에 지정된 순서를 따릅니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 열 배포 통계를 제공하는 연결된 서버에서 배포 통계와 카디널리티 통계를 고려하므로, 조인을 원격에서 수행하기 위해 REMOTE 조인 힌트가 필요하지는 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 프로세서는 원격 통계를 고려하여 원격 조인 전략이 적절한지 결정합니다. REMOTE 조인 힌트는 열 배포 통계를 제공하지 않는 공급자에게 유용합니다.  
  
## <a name="using-apply"></a>APPLY 사용  
 APPLY 연산자의 좌우 피연산자는 모두 테이블 식입니다. 이러한 피연산자 간의 주요 차이점은 *right_table_source*에서 *left_table_source*의 열을 함수의 인수 중 하나로 사용하는 테이블 반환 함수를 사용할 수 있다는 것입니다. *left_table_source*는 테이블 반환 함수를 포함할 수 있지만 *right_table_source*의 열인 인수는 포함할 수 없습니다.  
  
APPLY 연산자는 다음과 같은 방식으로 FROM 절에 지정될 테이블 원본을 생성합니다.  
  
1.  *left_table_source*의 각 행에 대해 *right_table_source*를 평가하여 행 집합을 생성합니다.  
  
    *right_table_source*의 값은 *left_table_source*에 따라 달라집니다. *right_table_source*는 대략 `TVF(left_table_source.row)`와 같이 표현될 수 있습니다. 여기서 `TVF`는 테이블 반환 함수입니다.  
  
2.  UNION ALL 연산을 수행하여 *right_table_source*를 평가할 때 각 행에 대해 생성된 결과 집합을 *left_table_source*와 결합합니다.  
  
    APPLY 연산자의 결과로 생성된 열 목록은 *right_table_source*의 열 목록과 결합된 *left_table_source*의 열 집합입니다.  
  
## <a name="using-pivot-and-unpivot"></a>PIVOT 및 UNPIVOT 사용  
 *pivot_column* 및 *value_column*은 PIVOT 연산자에서 사용되는 그룹화 열입니다. PIVOT은 다음과 같은 방식으로 출력 결과 집합을 가져옵니다.  
  
1.  *input_table*에서 그룹화 열을 기준으로 GROUP BY를 수행하고 각 그룹에 대해 하나의 출력 행을 생성합니다.  
  
     출력 행의 그룹화 열은 *input_table*에서 해당 그룹에 대한 해당 열 값을 가져옵니다.  
  
2.  다음 작업을 수행해 각각의 출력 행에 대한 열 목록의 열 값을 생성합니다.  
  
    1.  추가적으로 이전 단계의 GROUP BY에서 생성된 행을 *pivot_column*을 기준으로 그룹화합니다.  
  
         *column_list*의 각 출력 열에 대해 조건에 맞는 하위 그룹을 선택합니다.  
  
         `pivot_column = CONVERT(<data type of pivot_column>, 'output_column')`  
  
    2.  *aggregate_function*이 이 하위 그룹의 *value_column*에 대해 계산되고, 그 결과는 해당 *output_column*의 값으로 반환됩니다. 하위 그룹이 비어 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 해당 *output_column*에 대해 null 값을 생성합니다. 집계 함수가 COUNT이고 하위 그룹이 비어 있으면 0이 반환됩니다.  

> [!NOTE]
> `UNPIVOT` 절의 열 식별자는 카탈로그 데이터 정렬을 따릅니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]의 경우 데이터 정렬은 항상 `SQL_Latin1_General_CP1_CI_AS`입니다. 부분적으로 포함된 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터베이스의 경우 데이터 정렬은 항상 `Latin1_General_100_CI_AS_KS_WS_SC`입니다. 열이 다른 열과 결합되면 충돌을 피하기 위해 collate 절(`COLLATE DATABASE_DEFAULT`)이 필요합니다.   
  
 예제를 포함하여 PIVOT 및 UNPIVOT에 대한 자세한 내용은 [PIVOT 및 UNPIVOT 사용](../../t-sql/queries/from-using-pivot-and-unpivot.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 DELETE, SELECT 또는 UPDATE 문의 사용 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-a-simple-from-clause"></a>A. 간단한 FROM 절 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 샘플 데이터베이스에서 `TerritoryID` 테이블의 `Name` 및 `SalesTerritory`을 검색합니다.  
  
```sql    
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
  
### <a name="b-using-the-tablock-and-holdlock-optimizer-hints"></a>B. TABLOCK 및 HOLDLOCK 최적화 프로그램 힌트 사용  
 다음의 부분 트랜잭션은 `Employee`에 명시적인 공유 테이블 잠금을 설정하고 인덱스를 읽는 방법을 보여 줍니다. 잠금은 전체 트랜잭션 동안 유지됩니다.  
  
```sql    
BEGIN TRAN  
SELECT COUNT(*)   
FROM HumanResources.Employee WITH (TABLOCK, HOLDLOCK) ;  
```  
  
### <a name="c-using-the-sql-92-cross-join-syntax"></a>C. SQL-92 CROSS JOIN 구문 사용  
 다음 예는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Employee` 및 `Department` 두 테이블의 교차곱을 반환합니다. `BusinessEntityID` 행과 모든 `Department` 이름 행의 가능한 모든 조합 목록이 반환됩니다.  
  
```sql    
SELECT e.BusinessEntityID, d.Name AS Department  
FROM HumanResources.Employee AS e  
CROSS JOIN HumanResources.Department AS d  
ORDER BY e.BusinessEntityID, d.Name ;  
```  
  
### <a name="d-using-the-sql-92-full-outer-join-syntax"></a>D. SQL-92 FULL OUTER JOIN 구문 사용  
 다음 예는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `SalesOrderDetail` 테이블의 제품 이름 및 해당되는 모든 판매 주문을 반환합니다. 또한 `Product` 테이블에 나열되어 있는 제품이 없는 모든 판매 주문, 그리고 `Product` 테이블에 나열된 것 이외의 주문된 모든 제품을 반환합니다.  
  
```sql  
-- The OUTER keyword following the FULL keyword is optional.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
FULL OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="e-using-the-sql-92-left-outer-join-syntax"></a>E. SQL-92 LEFT OUTER JOIN 구문 사용  
 다음 예에서는 `ProductID`로 두 테이블을 조인하고 왼쪽 테이블에서 일치하지 않는 행도 함께 반환합니다. `Product` 테이블은 `SalesOrderDetail` 열에서 각 `ProductID` 테이블과 일치합니다. 모든 제품은 주문 여부에 관계없이 결과 집합에 나타납니다.  
  
```sql    
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
LEFT OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="f-using-the-sql-92-inner-join-syntax"></a>F. SQL-92 INNER JOIN 구문 사용  
 다음 예에서는 모든 제품 이름과 판매 주문 ID를 반환합니다.  
  
```sql    
-- By default, SQL Server performs an INNER JOIN if only the JOIN   
-- keyword is specified.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
INNER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="g-using-the-sql-92-right-outer-join-syntax"></a>G. SQL-92 RIGHT OUTER JOIN 구문 사용  
 다음 예에서는 `TerritoryID`로 두 테이블을 조인하고 오른쪽 테이블에서 일치하지 않는 행도 함께 반환합니다. `SalesTerritory` 테이블은 `SalesPerson` 열에서 각 `TerritoryID` 테이블과 일치합니다. 판매 직원에게 담당 구역이 할당되었는지 여부에 관계없이 모든 판매 직원이 결과 집합에 표시됩니다.  
  
```sql    
SELECT st.Name AS Territory, sp.BusinessEntityID  
FROM Sales.SalesTerritory AS st   
RIGHT OUTER JOIN Sales.SalesPerson AS sp  
ON st.TerritoryID = sp.TerritoryID ;  
```  
  
### <a name="h-using-hash-and-merge-join-hints"></a>H. HASH 및 MERGE 조인 힌트 사용  
 다음 예에서는 `Product`, `ProductVendor` 및 `Vendor` 테이블 간의 3개 테이블 조인을 수행하여 제품 및 제품 공급업체 목록을 생성합니다. 쿼리 최적화 프로그램은 MERGE 조인을 사용하여 `Product`와 `ProductVendor`(`p`와 `pv`)를 조인합니다. 그런 다음 `Product`와 `ProductVendor`(`p`와 `pv`)의 MERGE 조인이 `Vendor` 테이블에 HASH 조인되어 (`p`와 `pv`) 및 `v`를 생성합니다.  
  
> [!IMPORTANT]  
>  조인 힌트를 지정한 이후에는 INNER 키워드가 더 이상 선택 사항이 아니며 INNER JOIN을 수행하도록 명시적으로 지정해야 합니다.  
  
```sql    
SELECT p.Name AS ProductName, v.Name AS VendorName  
FROM Production.Product AS p   
INNER MERGE JOIN Purchasing.ProductVendor AS pv   
ON p.ProductID = pv.ProductID  
INNER HASH JOIN Purchasing.Vendor AS v  
ON pv.BusinessEntityID = v.BusinessEntityID  
ORDER BY p.Name, v.Name ;  
```  
  
### <a name="i-using-a-derived-table"></a>9\. 파생된 테이블 사용  
 다음 예에서는 파생된 테이블과 `SELECT` 문을 `FROM` 절 다음에 사용하여 모든 직원의 성과 이름, 직원이 거주하는 도시를 반환합니다.  
  
```sql    
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
  
### <a name="j-using-tablesample-to-read-data-from-a-sample-of-rows-in-a-table"></a>J. TABLESAMPLE을 사용하여 테이블의 행 샘플 데이터 읽기  
 다음 예에서는 `TABLESAMPLE` 절에 `FROM`을 사용하여 `10` 테이블에 있는 모든 행 중 대략 `Customer` 퍼센트를 반환합니다.  
  
```sql    
SELECT *  
FROM Sales.Customer TABLESAMPLE SYSTEM (10 PERCENT) ;  
```  
  
### <a name="k-using-apply"></a>11. APPLY 사용  
다음 예제에서는 다음 테이블 및 테이블 반환 함수가 데이터베이스에 존재한다고 가정합니다.  

|개체 이름|열 이름|      
|---|---|   
|Departments|DeptID, DivisionID, DeptName, DeptMgrID|      
|EmpMgr|MgrID, EmpID|     
|Employees|EmpID, EmpLastName, EmpFirstName, EmpSalary|  
|GetReports(MgrID)|EmpID, EmpLastName, EmpSalary|     
  
`GetReports` 테이블 반환 함수는 지정된 `MgrID`에 직접 또는 간접적으로 보고하는 모든 직원의 목록을 반환합니다.  
  
이 예에서는 `APPLY`를 사용하여 모든 부서와 해당 부서의 모든 직원을 반환합니다. 특정 부서에 직원이 한 명도 없으면 해당 부서에 대해서는 행이 반환되지 않습니다.  
  
```sql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d    
CROSS APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
쿼리가 직원이 없는 부서의 행도 생성하도록 하려면 `EmpID`를 사용하세요. 이 때 `EmpLastName`, `EmpSalary` 및 `OUTER APPLY` 열에 대해서는 Null 값이 생성됩니다.  
  
```sql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d   
OUTER APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
### <a name="l-using-cross-apply"></a>12. CROSS APPLY 사용  
다음 예제는 `sys.dm_exec_cached_plans` 동적 관리 뷰를 쿼리하여 캐시에 있는 모든 쿼리 계획의 계획 핸들을 검색함으로써 계획 캐시에 있는 모든 쿼리 계획의 스냅샷을 검색합니다. 그런 다음 `CROSS APPLY`에 계획 핸들을 전달할 `sys.dm_exec_query_plan` 연산자를 지정합니다. 계획 캐시에 있는 각 계획의 XML 실행 계획 출력은 현재 반환된 테이블의 `query_plan` 열에 있습니다.  
  
```sql
USE master;  
GO  
SELECT dbid, object_id, query_plan   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);   
GO  
```  
  
### <a name="m-using-for-system_time"></a>13. FOR SYSTEM_TIME 사용  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]  
  
 다음 예제에서는 FOR SYSTEM_TIME AS OF date_time_literal_or_variable 인수를 사용하여 2014년 1월 1일 현재의 실제(현재) 테이블 행을 반환합니다.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME AS OF '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 다음 예제에서는 FOR SYSTEM_TIME FROM date_time_literal_or_variable TO date_time_literal_or_variable 인수를 사용하여 2013년 1월 1일부터 2014년 1월 1일까지로 정의된 기간(상위 경계 제외) 동안 활성화된 모든 행을 반환합니다.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM '2013-01-01' TO '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 다음 예제에서는 FOR SYSTEM_TIME BETWEEN date_time_literal_or_variable AND date_time_literal_or_variable 인수를 사용하여 2013년 1월 1일부터 2014년 1월 1일까지로 정의된 기간(상위 경계 포함) 동안 활성화된 모든 행을 반환합니다.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME BETWEEN '2013-01-01' AND '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 다음 예제에서는 FOR SYSTEM_TIME CONTAINED IN ( date_time_literal_or_variable, date_time_literal_or_variable ) 인수를 사용하여 2013년 1월 1일부터 2014년 1월 1일까지로 정의된 기간 동안 열리고 닫힌 모든 행을 반환합니다.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME CONTAINED IN ( '2013-01-01', '2014-01-01' )  
WHERE ManagerID = 5;
```  
  
 다음 예제에서는 리터럴이 아닌 변수를 사용하여 쿼리에 대한 날짜 경계 값을 제공합니다.  
  
```sql
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
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="n-using-the-inner-join-syntax"></a>14. INNER JOIN 구문 사용  
 다음 예제에서는 두 테이블 모두에서 `ProductKey` 조인 키가 일치하는 `FactInternetSales` 및 `DimProduct` 테이블에서 `SalesOrderNumber`, `ProductKey` 및 `EnglishProductName` 열을 반환합니다. `SalesOrderNumber` 및 `EnglishProductName` 열은 각각 테이블 중 하나에만 존재하므로 이러한 열을 표시된 대로 사용하여 테이블 별칭을 지정할 필요가 없습니다. 이러한 별칭은 가독성을 높이기 위해 포함되었습니다. **AS**라는 단어는 별칭 이름 앞에 필요하지 않지만, 가독성을 높이고 ANSI 표준을 준수하기 위해 사용하는 것이 좋습니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
INNER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 내부 조인에는 `INNER` 키워드가 필요하지 않으므로 이 동일한 쿼리는 다음과 같이 작성할 수 있습니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
ON dp.ProductKey = fis.ProductKey;  
```  
  
 또한 이 쿼리에 `WHERE` 절을 사용하여 결과를 제한할 수도 있습니다. 다음 예제에서는 결과를 'SO5000'보다 높은 `SalesOrderNumber` 값으로 제한합니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey  
WHERE fis.SalesOrderNumber > 'SO50000'  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="o-using-the-left-outer-join-and-right-outer-join-syntax"></a>15. LEFT OUTER JOIN 및 RIGHT OUTER JOIN 구문 사용  
 다음 예제에서는 `FactInternetSales` 및 `DimProduct` 테이블을 `ProductKey` 열에 조인합니다. 왼쪽 우선 외부 조인 구문은 왼쪽(`FactInternetSales`) 테이블에서 일치하지 않는 행을 유지합니다. `FactInternetSales` 테이블에는 `DimProduct` 테이블과 일치하지 않는 `ProductKey` 값이 포함되어 있지 않으므로 다음 쿼리는 위의 첫 번째 내부 조인 예제와 동일한 행을 반환합니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
LEFT OUTER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 또한 이 쿼리는 `OUTER` 키워드 없이 작성할 수도 있습니다.  
  
 오른쪽 우선 외부 조인에서는 오른쪽 테이블에서 일치하지 않는 행이 유지됩니다. 다음 예제에서는 위의 왼쪽 우선 외부 조인 예제와 동일한 행을 반환합니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM DimProduct AS dp 
RIGHT OUTER JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 다음 쿼리에서는 `DimSalesTerritory` 테이블을 왼쪽 우선 외부 조인의 왼쪽 테이블로 사용합니다. `FactInternetSales` 테이블에서 `SalesOrderNumber` 값을 검색합니다. 특정 `SalesTerritoryKey`에 대한 주문이 없으면 쿼리에서 해당 행의 `SalesOrderNumber`에 대해 NULL을 반환합니다. 이 쿼리는 `SalesOrderNumber` 열을 기준으로 정렬되므로 이 열의 모든 NULL이 결과의 맨 위에 표시됩니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
LEFT OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 이 쿼리는 동일한 결과를 검색하기 위해 오른쪽 우선 외부 조인으로 다시 작성할 수 있습니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM FactInternetSales AS fis 
RIGHT OUTER JOIN DimSalesTerritory AS dst  
    ON fis.SalesTerritoryKey = dst.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="p-using-the-full-outer-join-syntax"></a>16. FULL OUTER JOIN 구문 사용  
 다음 예제에서는 조인된 두 테이블의 모든 행을 반환하지만, 다른 테이블과 일치하지 않는 값에 대해 NULL을 반환하는 완전 외부 조인을 보여 줍니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 또한 이 쿼리는 `OUTER` 키워드 없이 작성할 수도 있습니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="q-using-the-cross-join-syntax"></a>17. CROSS JOIN 구문 사용  
 다음 예제에서는 `FactInternetSales` 및 `DimSalesTerritory` 테이블의 교차곱을 반환합니다. `SalesOrderNumber` 및 `SalesTerritoryKey`의 가능한 모든 조합 목록이 반환됩니다. 크로스 조인 쿼리에 `ON` 절이 없습니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
CROSS JOIN FactInternetSales AS fis  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="r-using-a-derived-table"></a>18. 파생된 테이블 사용  
 다음 예제에서는 파생 테이블(`FROM` 절 뒤의 `SELECT` 문)을 사용하여 `DimCustomer` 테이블에서 1970년 1월 1일 이후의 `BirthDate` 값과 'Smith' 성이 있는 모든 고객의 `CustomerKey` 및 `LastName` 열을 반환합니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT CustomerKey, LastName  
FROM  
   (SELECT * FROM DimCustomer  
    WHERE BirthDate > '01/01/1970') AS DimCustomerDerivedTable  
WHERE LastName = 'Smith'  
ORDER BY LastName;  
```  
  
### <a name="s-reduce-join-hint-example"></a>S.는 REDUCE 조인 힌트 예제  
 다음 예제에서는 `REDUCE` 조인 힌트를 사용하여 쿼리 내에서 파생 테이블의 처리를 변경합니다. 이 쿼리에서 `REDUCE` 조인 힌트를 사용하면 `fis.ProductKey`가 고유하게 투영되고, 복제되고, 만들어진 다음, `ProductKey`에서 `DimProduct`의 순서를 섞는 중에 `DimProduct`에 조인됩니다. 결과 파생 테이블은 `fis.ProductKey`에 배포됩니다.  
  
```sql
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
  
### <a name="t-replicate-join-hint-example"></a>20. REPLICATE 조인 힌트 예제  
 다음 예제에서는 `REDUCE` 조인 힌트 대신 `REPLICATE` 조인 힌트가 사용된다는 점을 제외하고는 위의 예제와 동일한 쿼리를 보여 줍니다. `REPLICATE` 힌트를 사용하면 `FactInternetSales` 테이블의 `ProductKey`(조인) 열의 값이 모든 노드에 복제됩니다. `DimProduct` 테이블은 해당 값의 복제된 버전에 조인됩니다.  
  
```sql
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
  
### <a name="u-using-the-redistribute-hint-to-guarantee-a-shuffle-move-for-a-distribution-incompatible-join"></a>21. REDISTRIBUTE 힌트를 사용하여 호환되지 않는 배포 조인에 대한 순서 섞기 이동 보장  
 다음 쿼리에서는 호환되지 않는 배포 조인에서 REDISTRIBUTE 쿼리 힌트를 사용합니다. 이렇게 하면 쿼리 최적화 프로그램이 쿼리 계획에서 순서 섞기 이동을 사용하도록 보장합니다. 또한 쿼리 계획에서 분산된 테이블을 복제된 테이블로 이동하는 브로드캐스트 이동을 사용하지 않도록 보장합니다.  
  
 다음 예제에서는 ProductKey가 DimProduct에 대한 배포 열이고 FactInternetSales에 대한 배포 열이 아니기 때문에 REDISTRIBUTE 힌트는 FactInternetSales 테이블에서 순서 섞기 이동을 수행하도록 합니다.  
  
```sql
-- Uses AdventureWorks  
  
EXPLAIN  
SELECT dp.ProductKey, fis.SalesOrderNumber, fis.TotalProductCost  
FROM DimProduct AS dp 
INNER REDISTRIBUTE JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  

### <a name="v-using-tablesample-to-read-data-from-a-sample-of-rows-in-a-table"></a>V. TABLESAMPLE을 사용하여 테이블의 행 샘플 데이터 읽기  
 다음 예에서는 `TABLESAMPLE` 절에 `FROM`을 사용하여 `10` 테이블에 있는 모든 행 중 대략 `Customer` 퍼센트를 반환합니다.  
  
```sql    
SELECT *  
FROM Sales.Customer TABLESAMPLE SYSTEM (10 PERCENT) ;
```
  
## <a name="see-also"></a>참고 항목  
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXTTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENQUERY&#40;Transact-SQL&#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
