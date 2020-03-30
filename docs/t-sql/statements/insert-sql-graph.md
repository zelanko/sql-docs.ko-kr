---
title: INSERT(SQL Graph) | Microsoft Docs
description: SQL 그래프 노드 또는 에지 테이블에 대한 INSERT 구문입니다.
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c4cfba19dc16e043ba6325fb6c9acb1665a597f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68071168"
---
# <a name="insert-sql-graph"></a>INSERT(SQL Graph)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

`node`의 `edge` 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 새 행을 하나 이상 추가합니다. 

> [!NOTE]   
>  표준 Transact-SQL 문의 경우 [INSERT TABLE(Transact SQL)](../../t-sql/statements/insert-transact-sql.md)을 참조하세요.
  
![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>노드 테이블 구문에 INSERT 
노드 테이블에 삽입하는 구문은 일반 테이블과 동일합니다. 

```sql
[ WITH <common_table_expression> [ ,...n ] ]  
INSERT   
{  
        [ TOP ( expression ) [ PERCENT ] ]   
        [ INTO ]   
        { <object> | rowset_function_limited   
          [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
        }  
    {  
        [ (column_list) ] | [(<edge_table_column_list>)]  
        [ <OUTPUT Clause> ]  
        { VALUES ( { DEFAULT | NULL | expression } [ ,...n ] ) [ ,...n     ]   
        | derived_table   
        | execute_statement  
        | <dml_table_source>  
        | DEFAULT VALUES   
        }  
    }  
}  
[;]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
      | database_name .[ schema_name ] .   
      | schema_name .   
    ]  
    node_table_name  | edge_table_name
}  
  
<dml_table_source> ::=  
    SELECT <select_list>  
    FROM ( <dml_statement_with_output_clause> )   
      [AS] table_alias [ ( column_alias [ ,...n ] ) ]  
    [ WHERE <on_or_where_search_condition> ]  
        [ OPTION ( <query_hint> [ ,...n ] ) ]  

<on_or_where_search_condition> ::=
    {  <search_condition_with_match> | <search_condition> }

<search_condition_with_match> ::=
    { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) }
    [ AND { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<search_condition> ::=
    { [ NOT ] <predicate> | ( <search_condition> ) }
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<graph_predicate> ::=
    MATCH( <graph_search_pattern> [ AND <graph_search_pattern> ] [ , ...n] )

<graph_search_pattern>::=
    <node_alias> { { <-( <edge_alias> )- | -( <edge_alias> )-> } <node_alias> }

<edge_table_column_list> ::=
    ($from_id, $to_id, [column_list])

```  
  
 
## <a name="arguments"></a>인수  
이 문서에서는 SQL 그래프와 관련된 인수를 설명합니다. INSERT 문에서 지원되는 인수에 대한 전체 목록과 설명은 [INSERT TABLE(Transact SQL)](../../t-sql/statements/insert-transact-sql.md)을 참조하세요.

INTO  
`INSERT`와 대상 테이블 사이에 사용할 수 있는 선택적 키워드입니다.  
  
*search_condition_with_match*   
`MATCH` 절은 노드 또는 에지 테이블에 삽입하는 동안 하위 쿼리에 사용할 수 있습니다. `MATCH` 문 구문의 경우 [GRAPH MATCH(Transact SQL)](../../t-sql/queries/match-sql-graph.md)를 참조하세요.

*graph_search_pattern*   
그래프 조건자의 일부로 `MATCH` 절에 제공된 검색 패턴입니다.

*edge_table_column_list*   
사용자는 에지에 삽입하는 동안 `$from_id` 및 `$to_id`에 대한 값을 제공해야 합니다. 값을 제공하지 않거나 NULL을 이러한 열에 삽입하는 경우 오류가 반환됩니다. 
  

## <a name="remarks"></a>설명  
노드에 삽입은 관계형 테이블에 삽입과 동일합니다. $node_id 열의 값은 자동으로 생성됩니다.

에지 테이블에 삽입하는 동안 사용자는 `$from_id` 및 `$to_id` 열에 대한 값을 제공해야 합니다.   

노드 테이블에 대한 BULK 삽입은 관계형 테이블과 동일합니다.

에지 테이블에 대량 삽입을 수행하기 전에 노드 테이블을 가져와야 합니다. 그런 다음, `$from_id` 및 `$to_id`에 대한 값을 노드 테이블의 `$node_id` 열에서 추출하여 에지로 삽입할 수 있습니다. 

  
### <a name="permissions"></a>사용 권한  
대상 테이블에 대해 INSERT 권한이 필요합니다.  
  
**sysadmin** 고정 서버 역할, **db_owner** 및 **db_datawriter** 고정 데이터베이스 역할의 멤버 및 테이블 소유자에게는 기본적으로 INSERT 권한이 부여됩니다. **sysadmin**, **db_owner** 및 **db_securityadmin** 역할의 멤버와 테이블 소유자는 다른 사용자에게 권한을 위임할 수 있습니다.  
  
OPENROWSET 함수에 BULK 옵션을 사용하여 INSERT를 실행하려면 **sysadmin** 고정 서버 역할 또는 **bulkadmin** 고정 서버 역할의 멤버여야 합니다.  
  

## <a name="examples"></a>예  
  
#### <a name="a--insert-into-node-table"></a>A.  노드 테이블에 삽입  
다음 예제에서는 Person 노드 테이블을 만들고 두 개의 행을 해당 테이블에 삽입합니다.

```sql
-- Create person node table
CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
-- Insert records for Alice and John
INSERT INTO dbo.Person VALUES (1, 'Alice');
INSERT INTO dbo.Person VALUES (2,'John');
```
  
#### <a name="b--insert-into-edge-table"></a>B.  에지 테이블에 삽입  
다음 예에서는 친구 에지 테이블을 만든 후 에지를 테이블에 삽입합니다.

```sql
-- Create friend edge table
CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

-- Create a friend edge, that connect Alice and John
INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
```

  
## <a name="see-also"></a>참고 항목  
[INSERT TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
[SQL Server 2017에서 그래프 처리](../../relational-databases/graphs/sql-graph-overview.md)  


