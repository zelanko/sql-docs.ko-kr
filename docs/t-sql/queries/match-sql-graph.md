---
title: MATCH (SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MATCH
- MATCH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0296f915e0731bac9e7a714fa1e307bd2cda86b6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606251"
---
# <a name="match-transact-sql"></a>MATCH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

  그래프의 검색 조건을 지정합니다. MATCH는 WHERE 절의 일부로 SELECT 문에서 그래프 노드와 에지 테이블과 함께만 사용할 수 있습니다. 
  
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
그래프에서 검색 패턴이나 이동하는 경로를 지정합니다. 이 패턴은 그래프의 경로를 이동하기 위해 ASCII art 구문을 사용합니다. 이 패턴은 제공된 화살표 방향으로 에지를 통해 한 노드에서 다른 노드로 이동합니다. 에지 이름 또는 별칭은 괄호에 묶어 제공합니다. 노드 이름 또는 별칭은 화살표의 양쪽 끝에 표시됩니다. 화살표는 패턴의 양방향으로 이동할 수 있습니다.

*node_alias*  
FROM 절에 제공된 노드 테이블의 이름 또는 별칭입니다.

*edge_alias*  
FROM 절에 제공된 에지 테이블의 이름 또는 별칭입니다.


## <a name="remarks"></a>Remarks  
MATCH 내 노드 이름은 반복이 가능합니다.  즉 노드는 같은 쿼리에서 임의의 횟수 만큼 통과할 수 있습니다.  
MATCH 내 에지 이름을 반복할 수 없습니다.  
에지는 어느 방향이든 가리킬 수 있지만 명시적인 방향이어야 합니다.  
OR 또는 NOT 연산자는 MATCH 패턴에서 지원되지 않습니다. MATCH는 WHERE 절에서 AND를 사용하여 다른 식과 결합할 수 있습니다. 그러나 OR나 NOT을 사용한 다른 식과의 결합은 지원되지 않습니다. 

## <a name="examples"></a>예  
### <a name="a--find-a-friend"></a>1.  친구 찾기 
 다음 예에서는 Person 노드 테이블 및 친구 Edge 테이블을 만들고 일부 데이터를 삽입한 다음, MATCH를 사용하여 그래프에 있는 사람인 Alice라는 친구를 찾습니다.

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
 다음 예제에서는 친구 Alice의 친구를 찾으려 합니다. 

 ```
SELECT Person3.name AS FriendName 
FROM Person Person1, friend, Person Person2, friend friend2, Person Person3
WHERE MATCH(Person1-(friend)->Person2-(friend2)->Person3)
AND Person1.name = 'Alice';

 ```

### <a name="c--more-match-patterns"></a>3.  다른 `MATCH` 패턴
 다음은 MATCH 안에서 패턴을 지정하는 몇 가지 다른 방법입니다.

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
 

## <a name="see-also"></a>참고 항목  
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017에서 그래프 처리](../../relational-databases/graphs/sql-graph-overview.md)  
