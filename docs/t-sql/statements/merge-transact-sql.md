---
description: MERGE(Transact-SQL)
title: MERGE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MERGE
- MERGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- updating data [SQL Server]
- modifying data [SQL Server], MERGE statement
- MERGE statement [SQL Server]
- adding data
- DML [SQL Server], MERGE statement
- table modifications [SQL Server], MERGE statement
- data manipulation language [SQL Server], MERGE statement
- inserting data
ms.assetid: c17996d6-56a6-482f-80d8-086a3423eecc
author: XiaoyuMSFT
ms.author: XiaoyuL
ms.openlocfilehash: 86f620b1c99345134a0768574d44da2bbae11c6b
ms.sourcegitcommit: 9774e2cb8c07d4f6027fa3a5bb2852e4396b3f68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92098852"
---
# <a name="merge-transact-sql"></a>MERGE(Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb-asa.md)]

원본 테이블과의 조인 결과를 기반으로 대상 테이블에서 삽입, 업데이트 또는 삭제 작업을 실행합니다. 예를 들어 원본 테이블과의 차이점에 따라 대상 테이블에서 행을 삽입, 업데이트 및 삭제하여 두 테이블을 동기화합니다.  
  
**성능 팁:** MERGE 문에 대해 설명된 조건부 동작은 두 테이블에 일치하는 특성이 복합적으로 혼합되어 있는 경우 가장 효과적입니다. 예를 들어, 행이 없는 경우 행을 삽입하고 행이 일치하지 않는 경우 행을 업데이트합니다. 다른 테이블의 행을 기반으로 한 테이블을 단순히 업데이트하는 경우 기본 INSERT, UPDATE 및 DELETE 문을 사용하여 성능 및 확장성을 향상합니다. 다음은 그 예입니다.   
  
```sql
INSERT tbl_A (col, col2)  
SELECT col, col2
FROM tbl_B
WHERE NOT EXISTS (SELECT col FROM tbl_A A2 WHERE A2.col = tbl_B.col);  
```  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql

-- SQL Server and Azure SQL Database
[ WITH <common_table_expression> [,...n] ]  
MERGE
    [ TOP ( expression ) [ PERCENT ] ]
    [ INTO ] <target_table> [ WITH ( <merge_hint> ) ] [ [ AS ] table_alias ]  
    USING <table_source> [ [ AS ] table_alias ]
    ON <merge_search_condition>  
    [ WHEN MATCHED [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ WHEN NOT MATCHED [ BY TARGET ] [ AND <clause_search_condition> ]  
        THEN <merge_not_matched> ]  
    [ WHEN NOT MATCHED BY SOURCE [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ <output_clause> ]  
    [ OPTION ( <query_hint> [ ,...n ] ) ]
;  
  
<target_table> ::=  
{
    [ database_name . schema_name . | schema_name . ]  
  target_table  
}  
  
<merge_hint>::=  
{  
    { [ <table_hint_limited> [ ,...n ] ]  
    [ [ , ] INDEX ( index_val [ ,...n ] ) ] }  
}  

<merge_search_condition> ::=  
    <search_condition>  
  
<merge_matched>::=  
    { UPDATE SET <set_clause> | DELETE }  
  
<merge_not_matched>::=  
{  
    INSERT [ ( column_list ) ]
        { VALUES ( values_list )  
        | DEFAULT VALUES }  
}  
  
<clause_search_condition> ::=  
    <search_condition> 
```  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

```syntaxsql
-- MERGE (Preview) for Azure Synapse Analytics 
[ WITH <common_table_expression> [,...n] ]  
MERGE
    [ INTO ] <target_table> [ [ AS ] table_alias ]  
    USING <table_source> [ [ AS ] table_alias ]
    ON <merge_search_condition>  
    [ WHEN MATCHED [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ WHEN NOT MATCHED [ BY TARGET ] [ AND <clause_search_condition> ]  
        THEN <merge_not_matched> ]  
    [ WHEN NOT MATCHED BY SOURCE [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]
    [ OPTION ( <query_hint> [ ,...n ] ) ]
;  -- The semi-colon is required, or the query will return syntax  error. 
```
 
## <a name="arguments"></a>인수

WITH \<common_table_expression>  
MERGE 문의 범위 내에 정의된 임시로 명명된 결과 집합 또는 뷰(공통 테이블 식)를 지정합니다. 결과 집합은 단순 쿼리에서 파생되며 MERGE 문에서 참조됩니다. 자세한 내용은 [WITH common_table_expression&#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)을 참조하세요.  
  
TOP ( *expression* ) [ PERCENT ]  
영향을 받는 행의 개수 또는 비율을 지정합니다. *식*은 행의 수 또는 비율일 수 있습니다. TOP 식에서 참조하는 행은 어떠한 순서로도 정렬되지 않습니다. 자세한 내용은 [TOP&#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)을 참조하세요.  
  
TOP 절은 전체 원본 테이블과 전체 대상 테이블이 조인되고 조인된 행 중 삽입, 업데이트 또는 삭제 동작에 적합하지 않은 행이 제거된 후에 적용됩니다. TOP 절은 조인된 행 수를 지정된 값으로 더 줄입니다. 삽입, 업데이트 또는 삭제 동작은 나머지 조인된 행에 순서 없이 적용됩니다. 즉, 행은 WHEN 절에 정의된 동작에 순서 없이 분산됩니다. 예를 들어 TOP (10)을 지정하면 10개 행이 영향을 받습니다. 이 10개의 행 중 7개가 업데이트되고 3개가 삽입되거나, 1개가 삭제되고 5개가 업데이트되고 4개가 삽입될 수 있습니다.  
  
MERGE 문은 원본과 대상 테이블 모두에 전체 테이블 검색을 수행하므로 큰 테이블을 수정하기 위해 TOP 절을 사용하여 다중 일괄 처리를 생성하는 경우에는 I/O 성능에 영향을 주는 경우도 있습니다. 이러한 시나리오에서 연속된 모든 일괄 처리는 새로운 행을 대상으로 해야 합니다.  
  
*database_name*  
*target_table*이 있는 데이터베이스의 이름입니다.  
  
*schema_name*  
*target_table*이 속해 있는 스키마의 이름입니다.  
  
*target_table*  
\<clause_search_condition>을 기준으로 \<table_source>의 데이터 행과 일치하는 테이블이나 뷰입니다. *target_table*은 MERGE 문의 WHEN 절에 지정된 삽입, 업데이트 또는 삭제 작업의 대상입니다.  
  
*target_table*이 뷰일 경우 이에 대한 모든 동작은 뷰 업데이트 조건을 충족해야 합니다. 자세한 내용은 [뷰를 통해 데이터 수정](../../relational-databases/views/modify-data-through-a-view.md)을 참조하세요.  
  
*target_table*은 원격 테이블일 수 없습니다. 또한 *target_table*은 정의된 규칙을 포함할 수 없습니다.  
  
[ AS ] *table_alias*  
*target_table*의 테이블을 참조하기 위한 대체 이름입니다.  
  
USING \<table_source>  
\<merge_search condition>을 기준으로 *target_table*의 데이터 행과 일치하는 데이터 원본을 지정합니다. 이 결과는 MERGE 문의 WHEN 절에서 수행할 동작을 나타냅니다. \<table_source>는 원격 테이블이나 원격 테이블에 액세스하는 파생 테이블일 수 있습니다.
  
\<table_source>는 [!INCLUDE[tsql](../../includes/tsql-md.md)] [테이블 값 생성자](../../t-sql/queries/table-value-constructor-transact-sql.md)를 사용해 여러 행을 지정하여 테이블을 생성하는 파생 테이블일 수 있습니다.  
  
 [ AS ] *table_alias*  
table_source의 테이블을 참조하기 위한 대체 이름입니다.   
  
이 절의 구문 및 인수에 대한 자세한 내용은 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)을 참조하세요.  
  
ON \<merge_search_condition>  
일치하는 부분을 확인하기 위해 \<table_source>와 *target_table*을 조인하는 조건을 지정합니다.
  
> [!CAUTION]  
> 일치 용도로 사용되는 대상 테이블에서는 열만 지정하는 것이 중요합니다. 즉, 대상 테이블에서 원본 테이블의 해당 열과 비교할 열을 지정해야 합니다. 예를 들어 `AND NOT target_table.column_x = value`를 지정하는 것과 같이 ON 절에서 대상 테이블의 행을 필터링하여 쿼리 성능을 향상하려고 하면 안 됩니다. 그렇게 하면 예기치 않은 잘못된 결과가 반환될 수 있습니다.  
  
WHEN MATCHED THEN \<merge_matched>  
\<table_source> ON \<merge_search_condition>에서 반환되는 행과 일치하고 추가 검색 조건을 만족하는 *target_table의 모든 행이 \<merge_matched> 절에 따라 업데이트되거나 삭제되도록 지정합니다.  
  
MERGE 문에는 최대 두 개의 WHEN MATCHED 절이 포함될 수 있습니다. WHEN MATCHED 절을 두 개 지정할 경우 첫 번째 절과 함께 AND \<search_condition> 절을 지정해야 합니다. 지정된 행에 대해 두 번째 WHEN MATCHED 절은 첫 번째 WHEN MATCHED 절이 적용되지 않은 경우에만 적용됩니다. WHEN MATCHED 절이 두 개 있는 경우 하나는 UPDATE 동작을 지정해야 하고 다른 하나는 DELETE 동작을 지정해야 합니다. UPDATE가 \<merge_matched> 절에 지정되어 있고 \<merge_search_condition>을 기준으로 둘 이상의 \<table_source> 행이 *target_table*의 행과 일치하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 오류를 반환합니다. MERGE 문은 동일한 행을 여러 번 업데이트하거나 업데이트하고 삭제할 수 없습니다.  
  
WHEN NOT MATCHED [ BY TARGET ] THEN \<merge_not_matched>  
\<table_source> ON \<merge_search_condition>에서 반환되는 행 중 *target_table*의 행과 일치하지 않지만 추가 검색 조건(있을 경우)을 충족하는 모든 행에 대해 *target_table*에 행이 삽입되도록 지정합니다. 삽입할 값은 \<merge_not_matched> 절에 지정됩니다. MERGE 문에는 WHEN NOT MATCHED [ BY TARGET ] 절이 하나만 포함될 수 있습니다.

WHEN NOT MATCHED BY SOURCE THEN \<merge_matched>  
\<table_source> ON \<merge_search_condition>에서 반환되는 행과 일치하지 않고 추가 검색 조건을 만족하는 *target_table의 모든 행이 \<merge_matched> 절에 따라 업데이트되거나 삭제되도록 지정합니다.  
  
MERGE 문에는 최대 두 개의 WHEN NOT MATCHED BY SOURCE 절이 포함될 수 있습니다. 절을 두 개 지정할 경우 첫 번째 절과 함께 AND \<clause_search_condition> 절을 지정해야 합니다. 지정된 행에 대해 두 번째 WHEN NOT MATCHED BY SOURCE 절은 첫 번째 WHEN MATCHED 절이 적용되지 않은 경우에만 적용됩니다. WHEN NOT MATCHED BY SOURCE 절이 두 개 있는 경우 하나는 UPDATE 동작을 지정해야 하고 다른 하나는 DELETE 동작을 지정해야 합니다. \<clause_search_condition>에서는 대상 테이블의 열만 참조할 수 있습니다.  
  
\<table_source>에서 아무 행도 반환되지 않으면 원본 테이블의 열에 액세스할 수 없습니다. \<merge_matched> 절에 지정된 업데이트 또는 삭제 동작이 원본 테이블의 열을 참조하는 경우 오류 207(잘못된 열 이름)이 반환됩니다. 예를 들어 원본 테이블의 `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1`에 액세스할 수 없기 때문에 `Col1` 절을 지정하면 이 문이 실패할 수 있습니다.  
  
AND \<clause_search_condition>  
유효한 검색 조건을 지정합니다. 자세한 내용은 [검색 조건&#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)을 참조하세요.  
  
\<table_hint_limited>  
MERGE 문이 수행하는 각 삽입, 업데이트 또는 삭제 동작의 대상 테이블에 적용되는 하나 이상의 테이블 힌트를 지정합니다. WITH 키워드와 괄호가 필요합니다.  
  
NOLOCK 및 READUNCOMMITTED는 허용되지 않습니다. 테이블 힌트에 대한 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
INSERT 문의 대상 테이블에 TABLOCK 힌트를 지정하는 것은 TABLOCKX 힌트를 지정하는 것과 결과가 같습니다. 두 경우 모두 테이블이 배타적으로 잠깁니다. FORCESEEK를 지정할 경우 원본 테이블과 조인된 대상 테이블의 암시적 인스턴스에 이 힌트가 적용됩니다.  
  
> [!CAUTION]  
> READPAST와 함께 WHEN NOT MATCHED [ BY TARGET ] THEN INSERT를 지정하면 INSERT 작업이 UNIQUE 제약 조건을 위반할 수 있습니다.  
  
INDEX ( index_val [ ,...n ] )  
원본 테이블과의 암시적 조인을 수행하는 대상 테이블에 있는 하나 이상의 인덱스에 대한 이름 또는 ID를 지정합니다. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
\<output_clause>  
업데이트, 삽입 또는 삭제되는 *target_table*의 모든 행과 일치하는 행을 임의의 순서로 반환합니다. **$action**은 OUTPUT 절에서 지정할 수 있습니다. **$action**은 각 행에 대한 세 가지 값 중 하나를 반환하는 **nvarchar(10)** 형식의 열입니다. 이 열은 해당 행에서 수행된 동작에 따라 'INSERT', 'UPDATE' 또는 'DELETE' 중 하나를 각 행의 값으로 반환합니다. 이 절의 인수 및 동작에 대한 자세한 내용은 [OUTPUT Clause &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)을 참조하세요.  
  
OPTION ( \<query_hint> [ ,...n ] )  
최적화 프로그램 힌트를 사용하여 데이터베이스 엔진이 문을 처리하는 방법을 사용자 지정하도록 지정합니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
\<merge_matched>  
\<table_source> ON \<merge_search_condition>에서 반환되는 행과 일치하지 않고 추가 검색 조건을 만족하는 *target_table*의 모든 행에 적용되는 업데이트 또는 삭제 동작을 지정합니다.  
  
UPDATE SET \<set_clause>  
대상 테이블에서 업데이트할 열 또는 변수 이름의 목록 및 이 목록을 업데이트하는 데 사용할 값을 지정합니다.  
  
이 절의 인수에 대한 자세한 내용은 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)을 참조하세요. 변수를 열과 동일한 값으로 설정할 수는 없습니다.  
  
Delete  
*target_table*의 행과 일치하는 행이 삭제되도록 지정합니다.  
  
\<merge_not_matched>  
대상 테이블에 삽입할 값을 지정합니다.  
  
(*column_list*)  
데이터를 삽입할 대상 테이블에 있는 하나 이상의 열 목록입니다. 열은 한 부분으로 구성된 이름으로 지정해야 합니다. 그러지 않으면 MERGE 문이 실패합니다. *column_list*는 괄호로 묶고 쉼표로 구분해야 합니다.  
  
VALUES ( *values_list*)  
대상 테이블에 삽입할 값을 반환하는 상수, 변수 또는 식의 쉼표로 구분된 목록입니다. 식에는 EXECUTE 문이 포함될 수 없습니다.  
  
DEFAULT VALUES  
삽입된 행에 각 열에 대해 정의된 기본값이 포함되도록 합니다.  
  
이 절에 대한 자세한 내용은 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)을 참조하세요.  
  
\<search_condition>  
\<merge_search_condition> 또는 \<clause_search_condition>을 지정하는 검색 조건을 지정합니다. 이 절의 인수에 대한 자세한 내용은 [검색 조건 &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)을 참조하세요.  

\<graph search pattern>  
그래프 일치 패턴을 지정합니다. 이 절의 인수에 대한 자세한 내용은 [MATCH &#40;Transact-SQL&#41;](../../t-sql/queries/match-sql-graph.md)을 참조하세요.
  
## <a name="remarks"></a>설명
>[!NOTE]
> Azure Synapse Analytics에서 MERGE 명령(미리 보기)은 SQL Server 및 Azure SQL Database에 비해 다음과 같은 차이점이 있습니다.  
> - MERGE 업데이트는 삭제 및 삽입 쌍으로 구현됩니다. MERGE 업데이트의 영향을 받는 행 수에는 삭제된 행과 삽입된 행이 포함됩니다. 
> - 다음 표에서는 배포 유형이 다른 테이블에 대한 지원을 설명합니다.

>|Azure Synapse Analytics의 MERGE CLAUSE|지원되는 대상 배포 테이블| 지원되는 원본 배포 테이블|의견|  
>|-----------------|---------------|-----------------|-----------|  
>|**WHEN MATCHED**| HASH, ROUND_ROBIN, REPLICATE |모든 배포 유형||  
>|**NOT MATCHED BY TARGET**|HASH |모든 배포 유형|UPDATE/DELETE FROM…JOIN을 사용하여 두 테이블을 동기화합니다. |
>|**NOT MATCHED BY SOURCE**|모든 배포 유형|모든 배포 유형|UPDATE/DELETE FROM…JOIN을 사용하여 두 테이블을 동기화합니다.||  

세 개의 MATCHED 절 중 최소한 하나를 지정해야 하지만 임의의 순서로 지정할 수 있습니다. 변수는 동일한 MATCHED 절에서 두 번 이상 업데이트할 수 없습니다.  
  
MERGE 문에 의해 대상 테이블에 지정된 삽입, 업데이트 또는 삭제 동작은 연계 참조 무결성 제약 조건을 포함하여 해당 테이블에 정의된 제약 조건의 제한을 받습니다. IGNORE_DUP_KEY가 대상 테이블의 고유 인덱스에 대해 ON인 경우 MERGE는 이 설정을 무시합니다.  
  
MERGE 문에는 문 종결자로 세미콜론(;)이 필요합니다. MERGE 문이 종결자 없이 실행되면 오류 10713이 발생합니다.  
  
MERGE 후에 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)을 사용하면 삽입, 업데이트 및 삭제된 행의 총 개수가 클라이언트에 반환됩니다.  
  
MERGE는 데이터베이스 호환성 수준이 100 이상으로 설정된 경우 완전 예약 키워드입니다. MERGE 문은 데이터베이스 호환성 수준이 90 미만인 경우나 100 미만인 경우 모두 사용 가능합니다. 그러나 데이터베이스 호환성 수준이 90으로 설정된 경우에는 키워드가 완전히 예약되지 않습니다.  
  
지연 업데이트 복제를 사용하는 경우 **MERGE** 문을 사용하지 마세요. **MERGE** 및 지연된 업데이트 트리거는 호환되지 않습니다. **MERGE** 문을 insert 또는 update 문으로 바꾸세요.  


## <a name="trigger-implementation"></a>트리거 구현

MERGE 문에 지정된 모든 삽입, 업데이트 또는 삭제 동작에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 대상 테이블에 정의된 해당 AFTER 트리거를 실행하지만 트리거를 첫 번째 또는 마지막으로 실행하는 동작을 지정하지는 않습니다. 동일한 동작에 대해 정의된 트리거는 사용자가 지정하는 순서대로 실행됩니다. 트리거 실행 순서를 설정하는 방법은 [시작 및 끝 트리거 지정](../../relational-databases/triggers/specify-first-and-last-triggers.md)을 참조하세요.  
  
대상 테이블에 MERGE 문에서 수행하는 삽입, 업데이트 또는 삭제 동작에 대해 정의된 INSTEAD OF 트리거가 활성화되어 있으면 MERGE 문에 지정된 모든 동작에 대해서도 INSTEAD OF 트리거가 활성화되어 있어야 합니다.  
  
*target_table*에 INSTEAD OF UPDATE 또는 INSTEAD OF DELETE 트리거가 정의되어 있으면 업데이트 또는 삭제 작업이 실행되지 않습니다. 대신 트리거가 실행되고 이에 따라 **inserted** 및 **deleted** 테이블이 채워집니다.  
  
*target_table*에 INSTEAD OF INSERT 트리거가 정의되어 있으면 삽입 작업이 수행되지 않습니다. 대신, 이에 따라 테이블이 채워집니다.  
  
## <a name="permissions"></a>사용 권한

원본 테이블에 대해서는 SELECT 권한이 필요하고 대상 테이블에 대해서는 INSERT, UPDATE 또는 DELETE 권한이 필요합니다. 자세한 내용은 [SELECT](../../t-sql/queries/select-transact-sql.md), [INSERT](../../t-sql/statements/insert-transact-sql.md), [UPDATE](../../t-sql/queries/update-transact-sql.md) 및 [DELETE](../../t-sql/statements/delete-transact-sql.md) 문서의 권한 섹션을 참조하세요.  
  
## <a name="optimizing-merge-statement-performance"></a>MERGE 문 성능 최적화

MERGE 문을 사용하면 여러 개의 개별 DML 문을 단일 문으로 대체할 수 있습니다. 이렇게 하면 작업이 하나의 문 내에서 수행되므로 원본 및 대상 테이블의 데이터가 처리되는 횟수가 최소화되어 쿼리 성능이 향상됩니다. 단, 성능 향상을 위해서는 인덱스, 조인 및 기타 고려 사항이 올바르게 설정되어야 합니다.

### <a name="index-best-practices"></a>인덱스를 위한 최선의 방법

MERGE 문의 성능을 높이려면 다음 인덱스 지침을 따르는 것이 좋습니다.

- 원본 테이블의 조인 열에 고유한 포함 인덱스를 만듭니다.
- 대상 테이블의 조인 열에 고유한 클러스터형 인덱스를 만듭니다.

이러한 인덱스를 통해 조인 키의 고유성을 확보하고 테이블의 데이터가 정렬되도록 할 수 있습니다. 쿼리 최적화 프로그램이 중복 행을 찾아 업데이트하기 위해 별도로 유효성 검사를 수행할 필요가 없고 추가 정렬 작업도 필요 없으므로 쿼리 성능이 개선됩니다.

### <a name="join-best-practices"></a>JOIN을 위한 최선의 방법

MERGE 문의 성능을 높이고 정확한 결과를 얻으려면 다음 조인 지침을 따르는 것이 좋습니다.

- ON <merge_search_condition> 절에는 원본 및 대상 테이블의 데이터 비교를 위한 조건을 나타내는 검색 조건만 지정합니다. 즉, 대상 테이블에서 원본 테이블의 해당 열과 비교할 열만 지정해야 합니다. 
- 상수와 같은 다른 값에 대한 비교는 포함하지 않습니다.

원본 또는 대상 테이블에서 행을 필터링하려면 다음 방법 중 하나를 사용합니다.

- 적절한 WHEN 절에 행 필터링을 위한 검색 조건을 지정합니다(예: WHEN NOT MATCHED AND S.EmployeeName LIKE 'S%' THEN INSERT....)
- 필터링된 행을 반환하는 원본 또는 대상에 대한 뷰를 정의하고 이 뷰를 원본 또는 대상 테이블로 참조합니다. 대상 테이블에 대해 정의된 뷰의 모든 동작은 뷰 업데이트를 위한 조건을 충족해야 합니다. 뷰를 사용하여 데이터를 업데이트하는 방법은 뷰를 통해 데이터 수정을 참조하세요.
- `WITH <common table expression>` 절을 사용하여 원본 또는 대상 테이블에서 행을 필터링합니다. 이 방법은 ON 절에 추가 검색 조건을 지정하는 것과 비슷하며 잘못된 결과를 생성할 수 있으므로 사용하지 않는 것이 좋으며 사용할 경우 구현 전에 철저히 테스트해야 합니다.

MERGE 문의 조인 작업은 SELECT 문의 조인과 동일한 방식으로 최적화됩니다. 즉, SQL Server에서 조인을 처리할 때 쿼리 최적화 프로그램은 여러 가지 가능한 방법 중 가장 효율적인 방법을 선택합니다. 원본 및 대상의 크기가 비슷하고 ‘인덱스를 위한 최선의 방법’ 섹션에 설명된 인덱스 지침을 원본 및 대상 테이블에 적용한 경우 병합 조인 연산자가 가장 효율적인 쿼리 계획입니다. 두 테이블 모두 한 번만 검색되고 데이터를 정렬할 필요가 없기 때문입니다. 원본 테이블이 대상 테이블보다 작은 경우 중첩 루프 연산자가 좋습니다.

MERGE 문에서 `OPTION (<query_hint>)` 절을 지정하여 특정 조인을 사용하도록 강제할 수 있습니다. 해시 조인은 인덱스를 사용하지 않으므로 MERGE 문에 대한 쿼리 힌트로는 사용하지 않는 것이 좋습니다.

### <a name="parameterization-best-practices"></a>매개 변수화를 위한 최선의 방법

SELECT, INSERT, UPDATE 또는 DELETE 문이 매개 변수 없이 실행되는 경우 SQL Server 쿼리 최적화 프로그램은 내부적으로 문을 매개 변수화하는 방법을 선택할 수 있습니다. 즉, 쿼리에 포함된 모든 리터럴 값이 매개 변수로 대체됩니다. 예를 들어 INSERT dbo.MyTable (Col1, Col2) VALUES (1, 10) 문은 내부적으로 INSERT dbo.MyTable (Col1, Col2) VALUES (@p1, @p2)로 구현될 수 있습니다. 단순 매개 변수화라고 하는 이 프로세스는 새 SQL 문을 이전에 컴파일된 기존의 실행 계획과 비교하는 관계형 엔진의 기능을 개선합니다. 쿼리 컴파일 및 다시 컴파일 빈도가 낮아지므로 쿼리 성능이 개선될 수 있습니다. 쿼리 최적화 프로그램은 MERGE 문에 단순 매개 변수화 프로세스를 적용하지 않습니다. 따라서 리터럴 값을 포함하는 MERGE 문의 경우 MERGE 문이 실행될 때마다 새 계획이 컴파일되므로 개별 INSERT, UPDATE 또는 DELETE 문보다 성능이 떨어집니다.

쿼리 성능을 높이려면 다음 매개 변수화 지침을 따르는 것이 좋습니다.

- `ON <merge_search_condition>` 절과 MERGE 문의 `WHEN` 절에 있는 모든 리터럴 값을 매개 변수화합니다. 예를 들어 리터럴 값을 적절한 입력 매개 변수로 대체하여 MERGE 문을 저장 프로시저에 통합할 수 있습니다.
- 문을 매개 변수화할 수 없는 경우 `TEMPLATE` 형식의 계획 지침을 만들고 `PARAMETERIZATION FORCED` 쿼리 힌트를 이 계획 지침에 지정합니다.
- MERGE 문이 데이터베이스에서 자주 실행되는 경우 데이터베이스의 PARAMETERIZATION 옵션을 FORCED로 설정하는 것이 좋습니다. 이 옵션을 설정할 때는 신중해야 합니다. `PARAMETERIZATION` 옵션은 데이터베이스 수준 설정이므로 데이터베이스에 대한 모든 쿼리의 처리 방식에 영향을 미칩니다.

### <a name="top-clause-best-practices"></a>TOP 절을 위한 최선의 방법

MERGE 문에서 TOP 절은 원본 테이블과 대상 테이블이 조인되고 삽입, 업데이트 또는 삭제 동작에 적합하지 않은 행이 제거된 후에 영향을 받는 행의 개수나 비율을 지정합니다. TOP 절은 조인된 행 수를 지정된 값으로 더 줄이며, 삽입, 업데이트 또는 삭제 동작은 나머지 조인된 행에 순서 없이 적용됩니다. 즉, 행은 WHEN 절에 정의된 동작에 순서 없이 분산됩니다. 예를 들어 TOP (10)을 지정하면 10개 행이 영향을 받습니다. 이 10개의 행 중 7개가 업데이트되고 3개가 삽입되거나, 1개가 삭제되고 5개가 업데이트되고 4개가 삽입될 수 있습니다.

일반적으로 TOP 절을 사용하여 큰 테이블에서 일괄 처리로 DML(데이터 조작 언어) 작업을 수행합니다. MERGE 문에서 TOP 절을 이러한 용도로 사용하는 경우 다음 내용을 알고 있어야 합니다.

- I/O 성능이 영향을 받을 수 있습니다.

  MERGE 문은 원본 테이블과 대상 테이블 모두에서 전체 테이블 검색을 수행합니다. 작업을 여러 일괄 처리로 나누면 일괄 처리 하나당 수행되는 쓰기 작업의 수를 줄일 수 있지만 각 일괄 처리에서는 원본 테이블과 대상 테이블에서 전체 테이블 검색을 수행합니다. 그 결과 읽기 작업이 쿼리의 성능에 영향을 줄 수 있습니다.

- 잘못된 결과가 발생할 수 있습니다.

  연속된 모든 일괄 처리는 새로운 행을 대상으로 해야 합니다. 그렇지 않은 경우 대상 테이블에 중복 행을 잘못 삽입하는 등의 원하지 않는 동작이 발생할 수 있습니다. 이러한 현상은 대상 일괄 처리에는 없었지만 전체 대상 테이블에는 있었던 행이 원본 테이블에 포함되는 경우 발생할 수 있습니다.

- 정확한 결과를 보장하려면

  - ON 절을 사용하여 기존 대상 행에 영향을 미치는 원본 행과 완전히 새로운 행을 확인합니다.
  - WHEN MATCHED 절에 추가 조건을 사용하여 이전 일괄 처리에 의해 대상 행이 이미 업데이트되었는지 여부를 확인합니다.

TOP 절은 이러한 절이 적용된 후에 적용되므로 문을 실행할 때마다 하나의 완전히 일치하지 않는 행이 삽입되거나 하나의 기존 행이 업데이트됩니다.

### <a name="bulk-load-best-practices"></a>대량 로드를 위한 최선의 방법

MERGE 문을 사용하여 `OPENROWSET(BULK…)` 절을 테이블 원본으로 지정하면 원본 데이터 파일의 데이터를 대상 테이블로 효율적으로 대량 로드할 수 있습니다. 이렇게 하면 전체 파일이 하나의 일괄 처리에서 처리됩니다.

대량 병합 프로세스의 성능을 높이려면 다음 지침을 따르는 것이 좋습니다.

- 대상 테이블의 조인 열에 클러스터형 인덱스를 만듭니다.
- `OPENROWSET(BULK…)` 절에 ORDER 및 UNIQUE 힌트를 사용하여 원본 데이터 파일의 정렬 방식을 지정합니다.

  기본적으로 대량 작업은 데이터 파일이 정렬되지 않았음을 전제로 합니다. 따라서 쿼리 최적화 프로그램이 보다 효율적인 쿼리 계획을 생성할 수 있도록 원본 데이터를 대상 테이블의 클러스터형 인덱스에 따라 정렬하고, ORDER 힌트를 사용하여 순서를 나타내야 합니다. 힌트는 런타임에 유효성이 검사됩니다. 데이터 스트림이 지정된 힌트를 따르지 않으면 오류가 발생합니다.

이러한 지침을 통해 조인 키의 고유성을 확보하고 원본 파일의 데이터 정렬 순서가 대상 테이블과 일치하도록 할 수 있습니다. 추가 정렬 작업이 필요 없고 불필요한 데이터 복사가 없으므로 쿼리 성능이 향상됩니다.

### <a name="measuring-and-diagnosing-merge-performance"></a>MERGE 성능 측정 및 진단

다음 기능을 사용하여 MERGE 문의 성능을 측정 및 진단할 수 있습니다.

- [sys.dm_exec_query_optimizer_info](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-optimizer-info-transact-sql.md) 동적 관리의 병합 stmt 카운터를 사용하여 MERGE 문에 대한 쿼리 최적화 횟수를 반환할 수 있습니다.
- [sys.dm_exec_plan_attributes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md) 동적 관리 함수의 merge_action_type 특성을 사용하여 MERGE 문의 결과로 사용되는 트리거 실행 계획의 유형을 반환할 수 있습니다.
- SQL 추적을 사용하여 다른 DML(데이터 조작 언어) 문에 대해 사용하는 것과 동일한 방식으로 MERGE 문에 대한 문제 해결 데이터를 수집할 수 있습니다. 자세한 내용은 [SQL Trace](../../relational-databases/sql-trace/sql-trace.md)을(를) 참조하세요.

## <a name="examples"></a>예  

### <a name="a-using-merge-to-do-insert-and-update-operations-on-a-table-in-a-single-statement"></a>A. MERGE를 사용하여 단일 문에서 테이블에 INSERT 및 UPDATE 작업 수행

일반적인 시나리오에서는 일치하는 행이 있으면 테이블에서 하나 이상의 열을 업데이트합니다. 또는 일치하는 행이 없으면 새 행으로 데이터를 테이블에 삽입합니다. 일반적으로 해당하는 UPDATE 및 INSERT 문이 포함된 저장 프로시저에 매개 변수를 전달하여 하나의 시나리오를 수행합니다. MERGE 문으로 단일 문에서 두 태스크를 수행할 수 있습니다. 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]데이터베이스에서 INSERT 문과 UPDATE 문이 모두 포함된 저장 프로시저를 보여 줍니다. 해당 프로시저는 단일 MERGE 문을 사용하여 동일한 작업을 실행하기 위해 수정됩니다.  
  
```sql  
CREATE PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS
BEGIN  
    SET NOCOUNT ON;  
-- Update the row if it exists.
    UPDATE Production.UnitMeasure  
SET Name = @Name  
WHERE UnitMeasureCode = @UnitMeasureCode  
-- Insert the row if the UPDATE statement failed.  
IF (@@ROWCOUNT = 0 )  
BEGIN  
    INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name)  
    VALUES (@UnitMeasureCode, @Name)  
END  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Test Value';  
SELECT UnitMeasureCode, Name FROM Production.UnitMeasure  
WHERE UnitMeasureCode = 'ABC';  
GO  
  
-- Rewrite the procedure to perform the same operations using the
-- MERGE statement.  
-- Create a temporary table to hold the updated or inserted values
-- from the OUTPUT clause.  
CREATE TABLE #MyTempTable  
    (ExistingCode nchar(3),  
     ExistingName nvarchar(50),  
     ExistingDate datetime,  
     ActionTaken nvarchar(10),  
     NewCode nchar(3),  
     NewName nvarchar(50),  
     NewDate datetime  
    );  
GO  
ALTER PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS
BEGIN  
    SET NOCOUNT ON;  
  
    MERGE Production.UnitMeasure AS target  
    USING (SELECT @UnitMeasureCode, @Name) AS source (UnitMeasureCode, Name)  
    ON (target.UnitMeasureCode = source.UnitMeasureCode)  
    WHEN MATCHED THEN
        UPDATE SET Name = source.Name  
    WHEN NOT MATCHED THEN  
        INSERT (UnitMeasureCode, Name)  
        VALUES (source.UnitMeasureCode, source.Name)  
    OUTPUT deleted.*, $action, inserted.* INTO #MyTempTable;  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'New Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'XYZ', @Name = 'Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Another Test Value';  
  
SELECT * FROM #MyTempTable;  
-- Cleanup
DELETE FROM Production.UnitMeasure WHERE UnitMeasureCode IN ('ABC','XYZ');  
DROP TABLE #MyTempTable;  
GO  
```  
  
### <a name="b-using-merge-to-do-update-and-delete-operations-on-a-table-in-a-single-statement"></a>B. MERGE를 사용하여 단일 문에서 테이블에 UPDATE 및 DELETE 작업 수행

다음 예에서는 MERGE를 사용하여 `ProductInventory` 테이블의 처리된 주문을 기반으로 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 예제 데이터베이스의 `SalesOrderDetail` 테이블을 매일 업데이트합니다. `Quantity` 테이블의 `ProductInventory` 열은 `SalesOrderDetail` 테이블에서 매일 제품별로 접수되는 주문의 수를 빼는 방식으로 업데이트됩니다. 제품에 대한 주문 수로 인해 제품의 재고 수준이 0 이하로 떨어지면 해당 제품에 대한 행이 `ProductInventory` 테이블에서 삭제됩니다.  
  
```sql  
CREATE PROCEDURE Production.usp_UpdateInventory  
    @OrderDate datetime  
AS  
MERGE Production.ProductInventory AS target  
USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
    JOIN Sales.SalesOrderHeader AS soh  
    ON sod.SalesOrderID = soh.SalesOrderID  
    AND soh.OrderDate = @OrderDate  
    GROUP BY ProductID) AS source (ProductID, OrderQty)  
ON (target.ProductID = source.ProductID)  
WHEN MATCHED AND target.Quantity - source.OrderQty <= 0  
    THEN DELETE  
WHEN MATCHED
    THEN UPDATE SET target.Quantity = target.Quantity - source.OrderQty,
                    target.ModifiedDate = GETDATE()  
OUTPUT $action, Inserted.ProductID, Inserted.Quantity,
    Inserted.ModifiedDate, Deleted.ProductID,  
    Deleted.Quantity, Deleted.ModifiedDate;  
GO  
  
EXECUTE Production.usp_UpdateInventory '20030501'  
```  
  
### <a name="c-using-merge-to-do-update-and-insert-operations-on-a-target-table-by-using-a-derived-source-table"></a>C. MERGE를 사용하여 파생된 원본 테이블을 통해 대상 테이블에 UPDATE 및 INSERT 작업 수행

다음 예에서는 MERGE를 사용하여 행을 업데이트하거나 삽입하는 방식으로 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `SalesReason` 테이블을 수정합니다. 원본 테이블의 `NewName` 값이 대상 테이블 `Name`의 `SalesReason` 열에 있는 값과 일치하는 경우 대상 테이블에서 `ReasonType` 열이 업데이트됩니다. `NewName` 값이 일치하지 않으면 원본 행이 대상 테이블에 삽입됩니다. 원본 테이블은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 테이블 값 생성자를 사용하여 원본 테이블의 여러 행을 지정하는 파생 테이블입니다. 파생 테이블에서 테이블 값 생성자를 사용하는 방법에 대한 자세한 내용은 [Table Value Constructor &#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)을 참조하세요. 또한 이 예에서는 OUTPUT 절의 결과를 테이블 변수에 저장하는 방법을 보여 줍니다. 그런 다음, 삽입되거나 업데이트된 행의 개수를 반환하는 단순한 select 작업을 실행하여 MERGE 문의 결과를 요약합니다.  
  
```sql  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'),
              ('Internet', 'Promotion'))  
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
  
### <a name="d-inserting-the-results-of-the-merge-statement-into-another-table"></a>D. MERGE 문의 결과를 다른 테이블에 삽입

다음 예에서는 MERGE 문의 OUTPUT 절에서 반환된 데이터를 캡처하고 이 데이터를 다른 테이블에 삽입합니다. MERGE 문은 `Quantity` 데이터베이스에서 `ProductInventory` 테이블의 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 열을 `SalesOrderDetail` 테이블에서 처리되는 순서대로 업데이트합니다. 이 예에서는 업데이트된 행을 캡처하여 재고 변경 내용을 추적하는 데 사용되는 다른 테이블에 삽입합니다.  
  
```sql  
CREATE TABLE Production.UpdatedInventory  
    (ProductID INT NOT NULL, LocationID int, NewQty int, PreviousQty int,  
     CONSTRAINT PK_Inventory PRIMARY KEY CLUSTERED (ProductID, LocationID));  
GO  
INSERT INTO Production.UpdatedInventory  
SELECT ProductID, LocationID, NewQty, PreviousQty
FROM  
(    MERGE Production.ProductInventory AS pi  
     USING (SELECT ProductID, SUM(OrderQty)
            FROM Sales.SalesOrderDetail AS sod  
            JOIN Sales.SalesOrderHeader AS soh  
            ON sod.SalesOrderID = soh.SalesOrderID  
            AND soh.OrderDate BETWEEN '20030701' AND '20030731'  
            GROUP BY ProductID) AS src (ProductID, OrderQty)  
     ON pi.ProductID = src.ProductID  
    WHEN MATCHED AND pi.Quantity - src.OrderQty >= 0
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0
        THEN DELETE  
    OUTPUT $action, Inserted.ProductID, Inserted.LocationID,
        Inserted.Quantity AS NewQty, Deleted.Quantity AS PreviousQty)  
 AS Changes (Action, ProductID, LocationID, NewQty, PreviousQty)
 WHERE Action = 'UPDATE';  
GO  
```  

### <a name="e-using-merge-to-do-insert-or-update-on-a-target-edge-table-in-a-graph-database"></a>E. MERGE를 사용하여 그래프 데이터베이스의 대상 에지 테이블에 대해 INSERT 또는 UPDATE 수행

이 예제에서는 노드 테이블 `Person` 및 `City`와 에지 테이블 `livesIn`을 만듭니다. `livesIn` 에지가 `Person` 및 `City` 사이에 아직 없으면 이 에지에 대해 MERGE 문을 사용하여 새 행을 삽입합니다. 에지가 이미 있는 경우 `livesIn` 에지에 대해 StreetAddress 특성만 업데이트하면 됩니다.

```sql
-- CREATE node and edge tables
CREATE TABLE Person
    (
        ID INTEGER PRIMARY KEY,
        PersonName VARCHAR(100)
    )
AS NODE
GO

CREATE TABLE City
    (
        ID INTEGER PRIMARY KEY,
        CityName VARCHAR(100),
        StateName VARCHAR(100)
    )
AS NODE
GO

CREATE TABLE livesIn
    (
        StreetAddress VARCHAR(100)
    )
AS EDGE
GO

-- INSERT some test data into node and edge tables
INSERT INTO Person VALUES (1, 'Ron'), (2, 'David'), (3, 'Nancy')
GO

INSERT INTO City VALUES (1, 'Redmond', 'Washington'), (2, 'Seattle', 'Washington')
GO

INSERT livesIn SELECT P.$node_id, C.$node_id, c
FROM Person P, City C, (values (1,1, '123 Avenue'), (2,2,'Main Street')) v(a,b,c)
WHERE P.id = a AND C.id = b
GO

-- Use MERGE to update/insert edge data
CREATE OR ALTER PROCEDURE mergeEdge
    @PersonId integer,
    @CityId integer,
    @StreetAddress varchar(100)
AS
BEGIN
    MERGE livesIn
        USING ((SELECT @PersonId, @CityId, @StreetAddress) AS T (PersonId, CityId, StreetAddress)
                JOIN Person ON T.PersonId = Person.ID
                JOIN City ON T.CityId = City.ID)
        ON MATCH (Person-(livesIn)->City)
    WHEN MATCHED THEN
        UPDATE SET StreetAddress = @StreetAddress
    WHEN NOT MATCHED THEN
        INSERT ($from_id, $to_id, StreetAddress)
        VALUES (Person.$node_id, City.$node_id, @StreetAddress) ;
END
GO

-- Following will insert a new edge in the livesIn edge table
EXEC mergeEdge 3, 2, '4444th Avenue'
GO

-- Following will update the StreetAddress on the edge that connects Ron to Redmond
EXEC mergeEdge 1, 1, '321 Avenue'
GO

-- Verify that all the address were added/updated correctly
SELECT PersonName, CityName, StreetAddress
FROM Person , City , livesIn
WHERE MATCH(Person-(livesIn)->city)
GO
```
  
## <a name="see-also"></a>참고 항목

- [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)
- [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)
- [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
- [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)
- [OUTPUT 절&#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)
- [Integration Services 패키지의 MERGE](../../integration-services/control-flow/merge-in-integration-services-packages.md)
- [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)
- [테이블 값 생성자 &#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)  
