---
title: 최단 경로 (SQL 그래프) | Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current
ms.openlocfilehash: 9318a34b4853937983b107491c9210de80e5506c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74056398"
---
# <a name="shortest_path-transact-sql"></a>SHORTEST_PATH (Transact-sql)
[!INCLUDE[tsql-appliesto-ssver2015-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  반복적으로 또는 반복적으로 검색 되는 그래프의 검색 조건을 지정 합니다. SELECT 문에서 그래프 노드 및에 지 테이블과 일치 하는 항목 내에 SHORTEST_PATH를 사용할 수 있습니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="shortest-path"></a>최단 경로
SHORTEST_PATH 함수를 사용 하 여 다음을 찾을 수 있습니다.    
* 지정 된 두 노드/엔터티 사이의 최단 경로입니다.
* 단일 원본 최단 경로입니다.
* 여러 원본 노드에서 여러 대상 노드로 최단 경로입니다.

임의의 길이 패턴을 입력으로 사용 하 고 두 노드 사이에 존재 하는 최단 경로를 반환 합니다. 이 함수는 MATCH 내 에서만 사용할 수 있습니다. 함수는 지정 된 두 노드 사이에 최단 경로를 하나만 반환 합니다. 원본 및 대상 노드 쌍 사이에 길이가 같은 두 개 이상의 최단 경로가 있는 경우 함수는 트래버스하는 동안 처음 발견 된 하나의 경로만 반환 합니다. 임의의 길이 패턴은 SHORTEST_PATH 함수 내부 에서만 지정할 수 있습니다. 

구문은 [일치 항목 (SQL 그래프)](../../t-sql/queries/match-sql-graph.md) 을 참조 하세요. 

## <a name="for-path"></a>경로
FOR PATH는 임의의 길이 패턴에 참여 하는 FROM 절에서 모든 노드 또는에 지 테이블 이름과 함께 사용 해야 합니다. PATH의 경우 노드 또는에 지 테이블에서 트래버스 된 경로에서 발견 된 노드 또는 가장자리 목록을 나타내는 순서가 지정 된 컬렉션을 반환 한다는 것을 엔진에 알립니다. 이러한 테이블의 특성은 SELECT 절에서 직접 프로젝션 할 수 없습니다. 이러한 테이블에서 특성을 프로젝션 하려면 그래프 경로 집계 함수를 사용 해야 합니다.  

## <a name="arbitrary-length-pattern"></a>임의 길이 패턴
이 패턴에는 원하는 노드에 도달할 때까지 또는 패턴에 지정 된 최대 반복 횟수가 충족 될 때까지 반복적으로 이동 해야 하는 노드 및 가장자리가 포함 됩니다. 쿼리가 실행 될 때마다이 패턴을 실행 한 결과는 시작 노드에서 끝 노드로 경로를 따라 이동 하는 노드의 정렬 된 컬렉션입니다. 정규식 스타일 구문 패턴이 며 다음 두 가지 패턴 수량자가 지원 됩니다.

* **' + '**: 패턴을 1 번 이상 반복 합니다. 최단 경로를 찾는 즉시 종료됩니다.
* **{1, n}**: 패턴 1 ~ ' n '을 반복 합니다. 가장 짧은 항목이 발견 되 면 즉시 종료 합니다.

## <a name="last_node"></a>LAST_NODE
LAST_NODE () 함수는 두 개의 임의 길이 트래버스 패턴의 체인을 허용 합니다. 다음과 같은 시나리오에서 사용할 수 있습니다.    
* 쿼리에서 가장 짧은 경로 패턴을 두 개 이상 사용 하 고 한 패턴이 이전 패턴의 마지막 노드에서 시작 됩니다.
* 가장 짧은 두 개의 경로 패턴이 동일한 LAST_NODE ()에서 병합 됩니다.

## <a name="graph-path-order"></a>그래프 경로 순서
그래프 경로 순서는 출력 경로에 있는 데이터의 순서를 나타냅니다. 출력 경로 순서는 항상 패턴의 비재귀적 부분에서 시작 하 여 재귀 부분에 표시 되는 노드/가장자리가 이어집니다. 쿼리 최적화/실행 중에 그래프가 트래버스하는 순서는 출력에 인쇄 된 순서와는 관련이 없습니다. 마찬가지로 재귀 패턴의 화살표 방향도 그래프 경로 순서에 영향을 주지 않습니다. 

## <a name="graph-path-aggregate-functions"></a>그래프 경로 집계 함수
임의 길이 패턴과 관련 된 노드 및 가장자리가 해당 경로에서 이동한 노드 및 가장자리의 컬렉션을 반환 하기 때문에 사용자는 기존 attributename 구문을 사용 하 여 직접 특성을 프로젝션 할 수 없습니다. 중간 노드 또는에 지 테이블에서 특성 값을 프로젝션 해야 하는 쿼리의 경우, 트래버스 된 경로에서 다음 그래프 경로 집계 함수를 사용 합니다. STRING_AGG, LAST_VALUE, SUM, AVG, MIN, MAX 및 COUNT. SELECT 절에서 이러한 집계 함수를 사용 하는 일반적인 구문은 다음과 같습니다.

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

### <a name="string_agg"></a>STRING_AGG
STRING_AGG 함수는 식과 구분 기호를 입력으로 사용 하 고 문자열을 반환 합니다. 사용자는 SELECT 절에서이 함수를 사용 하 여 이동 경로에서 중간 노드 또는 가장자리의 특성을 프로젝션 할 수 있습니다. 

### <a name="last_value"></a>LAST_VALUE
트래버스 된 경로에서 마지막 노드의 특성을 프로젝션 하려면 LAST_VALUE 집계 함수를 사용할 수 있습니다. Edge 테이블 별칭을이 함수에 대 한 입력으로 제공 하면 노드 테이블 이름 또는 별칭만 사용할 수 있습니다.

**마지막 노드**: 마지막 노드는 일치 조건자의 화살표 방향에 관계 없이 트래버스 된 경로에서 마지막으로 표시 되는 노드를 참조 합니다. 예: `MATCH(SHORTEST_PATH(n(-(e)->p)+) )` 여기서 경로의 마지막 노드는 마지막으로 방문한 P 노드가 됩니다. 

반면 마지막 노드는이 패턴에 대 한 출력 그래프 경로의 마지막 n 번째 노드입니다.`MATCH(SHORTEST_PATH((n<-(e)-)+p))`    

### <a name="sum"></a>합계
이 함수는 트래버스하 경로에 나타난 제공 된 노드/가장자리 특성 값 또는 식의 합계를 반환 합니다.

### <a name="count"></a>개수
이 함수는 경로에서 원하는 node/edge 특성의 null이 아닌 값의 개수를 반환 합니다. COUNT 함수는 노드 또는에\*지 테이블 별칭이 있는 ' ' 연산자를 지원 합니다. 노드 또는에 지 테이블 별칭이 없으면의 \* 사용법이 모호 하 고 오류가 발생 합니다.

    {  COUNT( <expression> | <node_or_edge_alias>.* )  <order_clause>  }


### <a name="avg"></a>평균
제공 된 노드/가장자리 특성 값 또는 트래버스 된 경로에 나타난 식의 평균을 반환 합니다.

### <a name="min"></a>최소
제공 된 노드/가장자리 특성 값 또는 트래버스 된 경로에 나타난 식의 최소값을 반환 합니다.

### <a name="max"></a>최대
제공 된 노드/가장자리 특성 값 또는 트래버스 된 경로에 나타난 식의 최대값을 반환 합니다.

## <a name="remarks"></a>설명  
shortest_path 함수는 MATCH 내 에서만 사용할 수 있습니다.     
LAST_NODE은 shortest_path 내 에서만 지원 됩니다.     
가중치가 적용 되는 가장 짧은 경로, 모든 경로 또는 최단 경로를 찾는 것은 지원 되지 않습니다.         
경우에 따라 홉 수가 더 많은 쿼리에 대해 잘못 된 계획이 생성 될 수 있으며이로 인해 쿼리 실행 시간이 더 높아질 수 있습니다. Hash join 힌트를 사용 하면 도움이 될 수 있습니다.    


## <a name="examples"></a>예 
여기에 표시 된 예제 쿼리의 경우 [SQL Graph 샘플](./sql-graph-sample.md) 에서 만든 노드와에 지 테이블을 사용 합니다.

### <a name="a--find-shortest-path-between-2-people"></a>A.  2 명 사이의 최단 경로 찾기
 다음 예제에서는 Jacob와 Alice 사이에서 가장 짧은 경로를 찾습니다. Graph 샘플 스크립트에서 만든 Person 노드 및 FriendOf edge가 필요 합니다. 

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

 ### <a name="b--find-shortest-path-from-a-given-node-to-all-other-nodes-in-the-graph"></a>B.  지정 된 노드에서 그래프의 다른 모든 노드로 최단 경로를 찾습니다. 
 다음 예에서는 그래프에서 Jacob가 연결 된 모든 사용자와 Jacob부터 모든 사람들까지 가장 짧은 경로를 찾습니다. 

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

### <a name="c--count-the-number-of-hopslevels-traversed-to-go-from-one-person-to-another-in-the-graph"></a>C.  그래프의 한 사용자에서 다른 사용자로 이동 하기 위해 트래버스하는 홉/수준의 수를 계산 합니다.
 다음 예제에서는 Jacob와 Alice 사이의 최단 경로를 찾아 Jacob에서 Alice로 이동 하는 데 걸리는 홉 수를 인쇄 합니다. 

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

### <a name="d-find-people-1-3-hops-away-from-a-given-person"></a>D. 지정 된 사용자 로부터 받은 사용자 1-3 홉 찾기
다음 예에서는 Jacob와 graph 1-3에서 연결 된 모든 사람 사이에서 가장 짧은 경로를 찾습니다. 

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

### <a name="e-find-people-exactly-2-hops-away-from-a-given-person"></a>E. 지정 된 사용자가 정확히 2 개의 홉을 찾습니다.
다음 예제에서는 Jacob 사이에서 가장 짧은 경로를 검색 하 고, 그래프에서 정확히 2 개의 홉을 말합니다. 

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

## <a name="see-also"></a>참고 항목  
 [MATCH (SQL 그래프)](../../t-sql/queries/match-sql-graph.md)    
 [SQL 그래프를 &#40;CREATE TABLE&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017에서 그래프 처리](../../relational-databases/graphs/sql-graph-overview.md)     
 
