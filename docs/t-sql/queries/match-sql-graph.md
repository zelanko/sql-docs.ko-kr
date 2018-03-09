---
title: "일치 항목 (SQL 그래프) | Microsoft Docs"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MATCH
- MATCH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
ms.assetid: 
caps.latest.revision: 
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cbfa524cb9957ba557cfd239dae16a93aed919bf
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="match-transact-sql"></a>일치 항목 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

  그래프에 대 한 검색 조건을 지정합니다. 일치 하는 SELECT 문에서 WHERE 절의 일부로 그래프 노드와 edge 테이블에만 사용할 수 있습니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
MATCH (<graph_search_pattern>)

<graph_search_pattern>::=
    {<node_alias> { 
                     { <-( <edge_alias> )- } 
                   | { -( <edge_alias> )-> }
                 <node_alias> 
                 } 
     }
     [ { AND } { ( <graph_search_pattern> ) } ]
     [ ,...n ]
  
<node_alias> ::=
    node_table_name | node_alias 

<edge_alias> ::=
    edge_table_name | edge_alias
```

## <a name="arguments"></a>인수  
*graph_search_pattern*  
검색 또는 그래프에서 이동 하는 경로를 지정 합니다. 이 패턴 ASCII 아트 구문을 사용 하 여 그래프의 경로 순회 하도록 합니다. 패턴 한 노드에서 다른 구독자로 이동 가장자리에서 제공 되는 화살표의 방향을 통해 합니다. 가장자리 이름이 나 별칭 parantheses 안에 제공 됩니다. 노드 이름 또는 별칭 화살표의 양쪽에 나타납니다. 화살표는 패턴의 양방향으로 이동할 수 있습니다.

*node_alias*  
이름 또는 FROM 절에 제공 된 노드 테이블의 별칭입니다.

*edge_alias*  
이름 또는 FROM 절에 제공 된 edge 테이블의 별칭입니다.


## <a name="remarks"></a>주의  
일치 하는 노드 이름은 반복할 수 있습니다.  즉, 노드 수 있습니다는 임의 개수의 동일한 쿼리에서 한 번 통과 합니다.  
일치 항목 내 가장자리 이름을 반복할 수 없습니다.  
에 지 어느 방향으로든에서 가리킬 수 있지만 명시적 시계 반대 방향으로 있어야 합니다.  
또는 NOT 연산자 일치 패턴에서 지원 되지 않습니다. 일치 하는 WHERE 절에 및를 사용 하 여 다른 식과 결합할 수 있습니다. 그러나를 사용 하 여 다른 식과 결합 OR 하지 지원 되지 않습니다. 

## <a name="examples"></a>예  
### <a name="a--find-a-friend"></a>1.  친구를 찾아 
 다음 예에서는 Person 노드 테이블 및 친구 Edge 테이블을 만듭니다, 그리고 일부 데이터를 삽입 및 다음 일치 항목을 사용 하 여 그래프에 있는 사람은 Alice의 friend를 찾으려고 합니다.

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
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

 ### <a name="b--find-friend-of-a-friend"></a>2.  친구의 친구 찾기
 다음 예제에서는 Alice의 친구의 친구 찾으려고 합니다. 

 ```
SELECT Person3.name AS FriendName 
FROM Person Person1, friend, Person Person2, friend friend2, Person Person3
WHERE MATCH(Person1-(friend)->Person2-(friend2)->Person3)
AND Person1.name = 'Alice';

 ```

### <a name="c--more-match-patterns"></a>3.  더 많은 `MATCH` 패턴
 다음 몇 가지 더 많은 일치 항목 내 패턴을 지정할 수 있습니다는 합니다.

 ```
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
 

## <a name="see-also"></a>관련 항목:  
 [테이블 &#40; 만들기 SQL 그래프 &#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL 그래프)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017을 사용 하 여 처리 하는 그래프](../../relational-databases/graphs/sql-graph-overview.md)  
