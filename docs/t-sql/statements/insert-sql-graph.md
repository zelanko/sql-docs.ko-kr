---
title: "INSERT (SQL 그래프) | Microsoft Docs"
description: "SQL 그래프 노드 또는 edge 테이블에 대 한 구문을 삽입 합니다."
ms.date: 05/12/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: 
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e694d89efef130d2abcd5cd6424e2be576ef09de
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---

# <a name="insert-sql-graph"></a>INSERT (SQL 그래프)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]  

  하나 이상의 행이 추가 `node` 또는 `edge` 테이블에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 

> [!NOTE]   
>  표준 TRANSACT-SQL 문을 참조 하십시오. [표 삽입 (Transact SQL)](../../t-sql/statements/insert-transact-sql.md)합니다.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>노드 테이블 구문에 삽입 
노드 테이블에 삽입 하기 위한 구문은 일반 테이블의와 동일 합니다. 

```  
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
 이 문서에서는 SQL 그래프와 관련 된 인수에 설명 합니다. 전체 목록과 설명은 INSERT 문에서 지원 되는 인수에 대 한 참조 [표 삽입 (Transact SQL)](../../t-sql/statements/insert-transact-sql.md)

 INTO  
 간에 사용할 수 있는 선택적 키워드 `INSERT` 와 대상 테이블입니다.  
  
 *search_condition_with_match*   
 `MATCH`노드 또는 edge 테이블에 삽입 하는 동안 절 하위 쿼리에 사용할 수 있습니다. 에 대 한 `MATCH` 문 구문 참조 [그래프 일치 (Transact SQL)](../../t-sql/queries/match-sql-graph.md)

 *graph_search_pattern*   
 제공 된 검색 패턴 `MATCH` 그래프 조건자의 일부로 절.

 *edge_table_column_list*   
 사용자에 대 한 값을 제공 해야 `$from_id` 및 `$to_id` 가장자리에 삽입 하는 중입니다. 값을 제공 하지 않으면 또는 Null이이 열에 삽입 하는 경우 오류가 반환 됩니다. 
  

## <a name="remarks"></a>주의  
노드를 삽입 하는 모든 관계형 테이블에 삽입 일치 합니다. $Node_id 열의 값을 자동으로 생성 됩니다.

Edge 테이블을 삽입 하는 동안 사용자에 대 한 값을 제공 해야 `$from_id` 및 `$to_id` 열입니다.   

대량 삽입 노드 테이블은 남아 있는 관계형 테이블의 동일한 있습니다.

Edge 테이블에 삽입 하는 대량, 전에 노드 테이블 가져와야 합니다. 에 대 한 값 `$from_id` 및 `$to_id` 에서 추출할 수 있습니다는 `$node_id` 노드 테이블의 열 및 가장자리도 삽입 합니다. 

  
### <a name="permissions"></a>Permissions  
 대상 테이블에 대해 INSERT 권한이 필요합니다.  
  
 멤버에 대 한 기본 권한을 삽입는 **sysadmin** 고정 서버 역할의 **db_owner** 및 **db_datawriter** 고정 데이터베이스 역할 및 테이블 소유자입니다. 멤버는 **sysadmin**, **db_owner**, 및 **db_securityadmin** 역할 및 테이블 소유자 권한을 다른 사용자에 게 위임할 수 있습니다.  
  
 INSERT OPENROWSET 함수의 BULK 옵션을 실행 하려면의 구성원 이어야는 **sysadmin** 고정된 서버 역할 또는 **bulkadmin** 고정된 서버 역할입니다.  
  

## <a name="examples"></a>예  
  
#### <a name="a--insert-into-node-table"></a>1.  노드 테이블에 삽입  
 다음 예에서는 Person 노드 테이블을 만들고 해당 테이블에 2 개의 행을 삽입 합니다.

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
 -- Insert records for Alice and John
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 ```
  
#### <a name="b--insert-into-edge-table"></a>2.  Edge 테이블에 삽입  
 다음 예제에서는 friend edge 테이블을 만들고 테이블에는 지를 삽입 합니다.

 ```
 -- Create friend edge table
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Create a friend edge, that connect Alice and John
 INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
 ```

  
## <a name="see-also"></a>관련 항목:  
 [테이블 삽입 &#40; Transact SQL &#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SQL Server 2017을 사용 하 여 처리 하는 그래프](../../relational-databases/graphs/sql-graph-overview.md)  



