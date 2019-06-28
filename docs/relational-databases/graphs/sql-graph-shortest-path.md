---
title: 가장 짧은 경로 (SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- SHORTEST PATH
- SHORTEST_PATH
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ed931a8b1918961b69cc0600f94aff6e4d68b9e1
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413990"
---
# <a name="shortestpath-transact-sql"></a>SHORTEST_PATH (Transact SQL)
[!INCLUDE[tsql-appliesto-ssver2015-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  그래프에 대 한 검색 조건을 재귀적으로 검색 하도록 지정 하거나 반복적입니다. SHORTEST_PATH SELECT 문에서 그래프 노드와 지 테이블을 사용 하 여 일치 항목 내에서 사용할 수 있습니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="shortest-path"></a>가장 짧은 경로
SHORTEST_PATH 함수를 통해 찾을 수 있습니다.    
* 두 개의 지정 된 노드/엔터티 간의 가장 짧은 경로
* 가장 짧은 경로 단일 소스입니다.
* 여러 대상 노드에 여러 소스 노드에서 가장 짧은 경로입니다.

입력으로는 임의 길이 패턴을 사용 하 고 두 노드 간 존재 하는 가장 짧은 경로 반환 합니다. 이 함수 일치 내 에서만 사용 될 수 있습니다. 임의 길이 패턴을 허용 하 고 해당 패턴과 일치 하는 그래프에서 최단 경로 찾습니다. 함수는 지정 된 두 노드 사이의 하나만 최단 경로 반환합니다. 경우에 있는 원본 및 대상 노드 쌍 간의 동일한 길이의 두 개 이상의 가장 짧은 경로 함수 첫 번째 통과 하는 동안 발견 된 하나의 경로 반환 됩니다. SHORTEST_PATH 함수 내에서을 임의 길이 패턴을 지정할 수는 참고 합니다. 

참조 된 [일치 항목 (SQL Graph)](../../t-sql/queries/match-sql-graph.md) 구문에 대 한 합니다. 

## <a name="for-path"></a>경로 대 한
FROM 절의 패턴을 임의 길이에 참여할 모든 노드 또는 지 테이블 이름을 가진 경로 사용 해야 합니다. 경로 대 한 노드 또는 지 테이블 노드 또는 가장자리 끝 노드로 시작 노드의 경로 따라 이동의 목록을 나타내는 정렬 된 컬렉션을 반환 하도록 엔진을 지시 합니다. SELECT 절에서 직접 이러한 테이블에서 특성을 나타낼 수 없습니다. 이러한 테이블에서 특성 프로젝트 경로 집계 함수를 그래프를 사용 해야 합니다.  

## <a name="arbitrary-length-pattern"></a>임의 길이 패턴
이 패턴에는 노드를 포함 하 고 원하는 노드에 도달할 때까지 또는 최대 패턴에 지정 된 반복 될 때까지 반복적으로 이동 해야 하는 가장자리에 부합 함. 쿼리가 실행 될 때마다가이 패턴을 실행 한 결과 순서가 지정 된 컬렉션의 노드 및 가장자리 끝 노드로 시작 노드의 경로 따라 이동 됩니다. 정규식 스타일 구문 패턴 이며 다음 두 가지 패턴 수량자 지원 됩니다.

* **‘+’** : 1 번 이상 반복 패턴을 반복 합니다. 가장 짧은 경로 찾을 수는 즉시 종료 합니다.
* **{1,n}** : ' N '로 패턴 1 반복 시간입니다. 가장 짧은 발견 되는 즉시 종료 합니다.

## <a name="lastnode"></a>LAST_NODE
LAST_NODE() 함수 두 임의 길이 순회 패턴의 연결을 허용 합니다. 시나리오에서 사용할 수 있는:    
* 이전 패턴의 마지막 노드를 시작 하는 한 가지 패턴 및 쿼리에서 둘 이상의 최단 경로 패턴이 사용 됩니다.
* 두 개의 가장 짧은 경로 패턴이 동일한 LAST_NODE()에 병합합니다.

## <a name="graph-path-order"></a>그래프의 경로 순서
그래프의 경로 순서 출력 경로에 데이터 순서는 참조합니다. 출력 경로 순서는 항상 뒤에 재귀 부분에 표시 된 노드/가장자리 패턴은 비재귀적 부분에서 시작 합니다. 쿼리 최적화/실행 하는 동안 그래프 트래버스 되는 순서는 출력에 표시 되는 순서를 사용 하 여 관련이 있습니다. 마찬가지로, 재귀 패턴의 화살표 방향으로도 영향이 없습니다 그래프 경로 순서. 

## <a name="graph-path-aggregate-functions"></a>그래프 경로 대 한 집계 함수
노드 및 가장자리 관련 반환 하는 임의 길이 패턴의 컬렉션인 (노드 및 해당 경로에 트래버스 edge(s)) 하므로 사용자 기존의 tablename.attributename 구문을 사용 하 여 직접 특성을 예상할 수 없습니다. 에 대 한 필요한 경우 특성 값을 예측 하는 중간 노드 또는 지 테이블에 이동 된 경로 사용 하 여 그래프 경로 대 한 집계 함수를 다음에서 쿼리 합니다. STRING_AGG LAST_VALUE, 합계, 평균, 최소, 최대 및 COUNT입니다. SELECT 절에 이러한 집계 함수를 사용 하는 일반 구문은 다음과 같습니다.

```
<GRAPH_PATH_AGGREGATE_FUNCTION>(<expression> , <separator>)  <order_clause>

    <order_clause> ::=
        { WITHIN GROUP (GRAPH PATH) }

    <GRAPH_PATH_AGGREGATE_FUNCTION> ::=
          STRING_AGG
        | LAST_VALUE
        | SUM
        | COUNT
        | AVG
        | MIN
        | MAX

```

### <a name="stringagg"></a>STRING_AGG
STRING_AGG 함수 식과 인수로 구분 기호를 사용 하 고 문자열을 반환 합니다. 사용자 중간 노드 또는 가장자리에서 이동 된 경로에서이 함수를 SELECT 절의 프로젝트 특성을 사용할 수 있습니다. 

### <a name="lastvalue"></a>LAST_VALUE
프로젝트를 마지막 노드 경로 트래버스 LAST_VALUE 집계 함수를에서 특성을 사용할 수 있습니다. 노드 테이블 이름에만이 함수에 대 한 입력으로에 지 테이블 별칭을 제공 하면 오류가 발생 하거나 별칭을 사용할 수 있습니다.

**노드의 마지막**: 마지막 노드 일치 조건자에서 화살표의 방향에 관계 없이 이동 된 경로에 마지막 표시 되는 노드를 가리킵니다. 예를 들어 `MATCH(SHORTEST_PATH(n(-(e)->p)+) )`을 참조하십시오. 다음 경로에 마지막 노드 마지막 방문한 P 노드가 됩니다. 

반면, 마지막 노드는이 패턴의 출력 그래프 경로에 마지막 n 번째 노드입니다. `MATCH(SHORTEST_PATH((n<-(e)-)+p))`    

### <a name="sum"></a>SUM
이 함수는 트래버스된 경로에 제공 된 노드/가장자리 특성 값 또는 표시 되는 식의 합계를 반환 합니다.

### <a name="count"></a>COUNT
이 함수는 경로에서 원하는 노드/가장자리 특성의 null이 아닌 값의 개수를 반환합니다. COUNT 함수를 지원 합니다 ' *' 연산자 노드 또는 지 테이블 별칭을 사용 합니다. 노드 또는 지 테이블 별칭을 사용 하지 않고 * 모호 하며 오류가 발생 합니다.

    {  COUNT( <expression> | <node_or_edge_alias>.* )  <order_clause>  }


### <a name="avg"></a>AVG
트래버스된 경로에 제공 된 노드/가장자리 특성 값 또는 표시 되는 식의 평균을 반환 합니다.

### <a name="min"></a>MIN
제공 된 노드/가장자리 특성 값 또는 트래버스된 경로에 표시 되는 식에서 최소값을 반환 합니다.

### <a name="max"></a>MAX
제공 된 노드/가장자리 특성 값 또는 트래버스된 경로에 표시 되는 식에서 최대값을 반환 합니다.

## <a name="remarks"></a>Remarks  
shortest_path 함수 일치 내 에서만 사용 될 수 있습니다.     
LAST_NODE는 shortest_path 내 에서만 지원 됩니다.     
가중치가 적용 된 최단 경로, 모든 경로 또는 모든 최단 경로 찾을 수 없습니다.         
일부 경우에는 더 높은 쿼리 실행 시간이 더 많은 수의 홉을 사용 하 여 쿼리에 대 한 잘못 된 계획을 생성할 수 있습니다. Hash 조인 힌트를 사용 하 여 도움이 될 수 있습니다.    


## <a name="examples"></a>예 
Ot 하겠습니다는 여기에 나와 있는 예제 쿼리 노드를 사용 하 고 edge 테이블에서 생성 한 [SQL 그래프 샘플](./sql-graph-sample.md)

### <a name="a--find-shortest-path-between-2-people"></a>1\.  2 간의 가장 짧은 경로 찾으려면
 다음 예제에서는 Jacob과 Alice 사이의 최단 경로 알게 됩니다. Person 노드 및 FriendOf edge 그래프 샘플 스크립트에서 생성 해야 합니다. 

 ```
SELECT PersonName, Friends
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

 ### <a name="b--find-shortest-path-from-a-given-node-to-all-other-nodes-in-the-graph"></a>2\.  그래프에서 다른 모든 노드에 지정 된 노드에서 가장 짧은 경로 찾습니다. 
 다음 예제에서는 그래프에 해당 하는 모든 사용자에 게 Jacob에서 시작 하는 가장 짧은 경로 Jacob에 연결 된 모든 사람을 찾습니다. 

 ```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
AND Person1.name = 'Jacob'
 ```

### <a name="c--count-the-number-of-hopslevels-traversed-to-go-from-one-person-to-another-in-the-graph"></a>3\.  그래프에서 다른 사람이에서 이동 하려면 이동 홉/수준 수를 계산 합니다.
 다음 예제에서는 Jacob과 Alice 사이의 최단 경로 찾아서 alice Jacob에서 이동 하는 홉 수를 출력 합니다. 

 ```
 SELECT PersonName, Friends, levels
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

### <a name="d-find-people-1-3-hops-away-from-a-given-person"></a>4\. 사용자 지정된 사람에서 1 ~ 3 홉 찾기
다음 예제에서 문의 사항이 있으면 그래프 1-3 홉에서 Jacob와 그에 연결 된 모든 사용자 간의 가장 짧은 경로 찾습니다. 

```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
AND Person1.name = 'Jacob'
```

### <a name="e-find-people-exactly-2-hops-away-from-a-given-person"></a>5\. 사용자 지정된 사람에서 정확히 2 개 홉 찾기
다음 예제에서는 그래프에서 문의 사항이 있으면 정확히 2 개 홉에 있는 사람과 Jacob 간 최단 경로 찾습니다. 

```
SELECT PersonName, Friends
FROM (
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
    AND Person1.name = 'Jacob'
) Q
WHERE Q.levels = 2
```

## <a name="see-also"></a>관련 항목  
 [일치 항목 (SQL Graph)](../../t-sql/queries/match-sql-graph.md)    
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017에서 그래프 처리](../../relational-databases/graphs/sql-graph-overview.md)     
 
