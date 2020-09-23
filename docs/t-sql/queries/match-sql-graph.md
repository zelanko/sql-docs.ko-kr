---
description: MATCH (Transact-SQL)
title: MATCH (SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MATCH
- MATCH_TSQL
- SHORTEST_PATH
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
- Shortest Path, shortest_path
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b3d0f5307b8a9b96dec8b81f00550dbcd639ac9a
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116266"
---
# <a name="match-transact-sql"></a>MATCH (Transact-SQL)
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

  그래프의 검색 조건을 지정합니다. MATCH는 WHERE 절의 일부로 SELECT 문에서 그래프 노드와 에지 테이블과 함께만 사용할 수 있습니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
MATCH (<graph_search_pattern>)

<graph_search_pattern>::=
  {  
      <simple_match_pattern> 
    | <arbitrary_length_match_pattern>  
    | <arbitrary_length_match_last_node_predicate> 
  }

<simple_match_pattern>::=
  {
      LAST_NODE(<node_alias>) | <node_alias>   { 
          { <-( <edge_alias> )- } 
        | { -( <edge_alias> )-> }
        <node_alias> | LAST_NODE(<node_alias>)
        } 
  }
  [ { AND } { ( <simple_match_pattern> ) } ]
  [ ,...n ]

<node_alias> ::=
  node_table_name | node_table_alias 

<edge_alias> ::=
  edge_table_name | edge_table_alias


<arbitrary_length_match_pattern>  ::=
  { 
    SHORTEST_PATH( 
      <arbitrary_length_pattern> 
      [ { AND } { <arbitrary_length_pattern> } ] 
      [ ,…n] 
    )
  } 

<arbitrary_length_match_last_node_predicate> ::=
  {  LAST_NODE( <node_alias> ) = LAST_NODE( <node_alias> ) }


<arbitrary_length_pattern> ::=
    {  LAST_NODE( <node_alias> )   | <node_alias>
     ( <edge_first_al_pattern> [<edge_first_al_pattern>…,n] )
     <al_pattern_quantifier> 
  }
    |  ( {<node_first_al_pattern> [<node_first_al_pattern> …,n] )
        <al_pattern_quantifier> 
        LAST_NODE( <node_alias> ) | <node_alias> 
 }
    
<edge_first_al_pattern> ::=
  { (  
        { -( <edge_alias> )->   } 
      | { <-( <edge_alias> )- } 
      <node_alias>
      ) 
  } 

<node_first_al_pattern> ::=
  { ( 
      <node_alias> 
        { <-( <edge_alias> )- } 
      | { -( <edge_alias> )-> }
      ) 
  } 


<al_pattern_quantifier> ::=
  {
        +
      | { 1 , n }
  }

n -  positive integer only.
 
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*graph_search_pattern*  
그래프에서 검색 패턴이나 이동하는 경로를 지정합니다. 이 패턴은 그래프의 경로를 이동하기 위해 ASCII art 구문을 사용합니다. 이 패턴은 제공된 화살표 방향으로 에지를 통해 한 노드에서 다른 노드로 이동합니다. 에지 이름 또는 별칭은 괄호 안에 제공됩니다. 노드 이름 또는 별칭은 화살표의 양쪽 끝에 표시됩니다. 화살표는 패턴의 양방향으로 이동할 수 있습니다.

*node_alias*  
FROM 절에 제공된 노드 테이블의 이름 또는 별칭입니다.

*edge_alias*  
FROM 절에 제공된 에지 테이블의 이름 또는 별칭입니다.

*SHORTEST_PATH*   
최단 경로 함수는 그래프에서 지정된 두 노드 간의 최단 경로 또는 그래프에서 지정된 노드와 다른 모든 노드 간의 최단 경로를 찾는 데 사용됩니다. 그래프에서 반복적으로 검색되는 임의 길이 패턴을 입력으로 사용합니다. 

*arbitrary_length_match_pattern*  
원하는 노드에 도달할 때까지 또는 패턴에 지정된 최대 반복 횟수를 충족할 때까지 반복적으로 트래버스해야 하는 노드와 에지를 지정합니다. 

*al_pattern_quantifier*   
임의 길이 패턴은 지정된 검색 패턴의 반복 횟수를 지정하기 위해 정규식 스타일 패턴 한정사를 사용합니다. 지원되는 검색 패턴 한정사는 다음과 같습니다.   
* **+** : 패턴을 1번 이상 반복합니다. 최단 경로를 찾는 즉시 종료됩니다.    
* **{1,n}** : 패턴을 1~‘n’번 반복합니다. 최단 경로를 찾는 즉시 종료됩니다.     

## <a name="remarks"></a>설명  
MATCH 내 노드 이름은 반복이 가능합니다.  즉 노드는 같은 쿼리에서 임의의 횟수 만큼 통과할 수 있습니다.  
MATCH 내 에지 이름을 반복할 수 없습니다.  
에지는 어느 방향이든 가리킬 수 있지만 명시적인 방향이어야 합니다.  
OR 또는 NOT 연산자는 MATCH 패턴에서 지원되지 않습니다. MATCH는 WHERE 절에서 AND를 사용하여 다른 식과 결합할 수 있습니다. 그러나 OR나 NOT을 사용한 다른 식과의 결합은 지원되지 않습니다. 

## <a name="examples"></a>예제  
### <a name="a--find-a-friend"></a>A.  친구 찾기 
 다음 예에서는 Person 노드 테이블 및 친구 Edge 테이블을 만들고 일부 데이터를 삽입한 다음, MATCH를 사용하여 그래프에 있는 사람인 Alice라는 친구를 찾습니다.

 ```sql
 -- Create person node table
 CREATE TABLE dbo.Person (ID INTEGER PRIMARY KEY, name VARCHAR(50)) AS NODE;
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Insert into node table
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 INSERT INTO dbo.Person VALUES (3, 'Jacob');

-- Insert into edge table
INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'John'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2012');

-- use MATCH in SELECT to find friends of Alice
SELECT Person2.name AS FriendName
FROM Person Person1, friend, Person Person2
WHERE MATCH(Person1-(friend)->Person2)
AND Person1.name = 'Alice';
 ```

 ### <a name="b--find-friend-of-a-friend"></a>B.  친구의 친구 찾기
 다음 예제에서는 친구 Alice의 친구를 찾으려 합니다. 

 ```sql
SELECT Person3.name AS FriendName 
FROM Person Person1, friend, Person Person2, friend friend2, Person Person3
WHERE MATCH(Person1-(friend)->Person2-(friend2)->Person3)
AND Person1.name = 'Alice';
 ```

### <a name="c--more-match-patterns"></a>C.  다른 `MATCH` 패턴
 다음은 MATCH 안에서 패턴을 지정하는 몇 가지 다른 방법입니다.

 ```sql
 -- Find a friend
    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2
    WHERE MATCH(Person1-(friend)->Person2);
    
-- The pattern can also be expressed as below

    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2 
    WHERE MATCH(Person2<-(friend)-Person1);


-- Find 2 people who are both friends with same person
    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0<-(friend2)-Person2);
    
-- this pattern can also be expressed as below

    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0 AND Person2-(friend2)->Person0);
 ```
 

## <a name="see-also"></a>참고 항목  
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT(SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017에서 그래프 처리](../../relational-databases/graphs/sql-graph-overview.md)  
