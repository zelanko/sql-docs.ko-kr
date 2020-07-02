---
title: SQL Graph 데이터베이스 샘플 | Microsoft Docs
description: SQL graph 데이터베이스에 도입 된 새 구문을 시작 하는 데 도움이 되는 빠른 샘플입니다.
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, tsql reference
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b08fdf07bf73b8d485ce9334d8998e055454dcb2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751150"
---
# <a name="create-a-graph-database-and-run-some-pattern-matching-queries-using-t-sql"></a>T-sql을 사용 하 여 그래프 데이터베이스 만들기 및 일부 패턴 일치 쿼리 실행

[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

이 샘플에서는 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 노드 및 가장자리가 포함 된 그래프 데이터베이스를 만든 다음 새 MATCH 절을 사용 하 여 일부 패턴과 일치 하 고 그래프를 통과 하는 스크립트를 제공 합니다. 이 샘플 스크립트는 두 Azure SQL Database 모두에서 작동 합니다.[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]  

## <a name="sample-schema"></a>샘플 스키마

이 샘플은 그림 1에 표시 된 것 처럼 사람, 식당 및 도시 노드가 있는 가상 소셜 네트워크에 대 한 그래프 스키마를 만듭니다. 이러한 노드는에 지에서 친구, 좋아요, LivesIn 및 LocatedIn을 사용 하 여 서로 연결 됩니다.

![개인-도시-식당-테이블](../../relational-databases/graphs/media/person-cities-restaurants-tables.png "Sql graph 데이터베이스 샘플")  
그림 1: 식당, 구/군/시, person 노드 및 LivesIn, LocatedIn, 좋아요를 포함 하는 샘플 스키마

## <a name="sample-script"></a>예제 스크립트

```
-- Create a graph demo database
CREATE DATABASE graphdemo;
go

USE  graphdemo;
go

-- Create NODE tables
CREATE TABLE Person (
  ID INTEGER PRIMARY KEY,
  name VARCHAR(100)
) AS NODE;

CREATE TABLE Restaurant (
  ID INTEGER NOT NULL,
  name VARCHAR(100),
  city VARCHAR(100)
) AS NODE;

CREATE TABLE City (
  ID INTEGER PRIMARY KEY,
  name VARCHAR(100),
  stateName VARCHAR(100)
) AS NODE;

-- Create EDGE tables. 
CREATE TABLE likes (rating INTEGER) AS EDGE;
CREATE TABLE friendOf AS EDGE;
CREATE TABLE livesIn AS EDGE;
CREATE TABLE locatedIn AS EDGE;

-- Insert data into node tables. Inserting into a node table is same as inserting into a regular table
INSERT INTO Person VALUES (1,'John');
INSERT INTO Person VALUES (2,'Mary');
INSERT INTO Person VALUES (3,'Alice');
INSERT INTO Person VALUES (4,'Jacob');
INSERT INTO Person VALUES (5,'Julie');

INSERT INTO Restaurant VALUES (1,'Taco Dell','Bellevue');
INSERT INTO Restaurant VALUES (2,'Ginger and Spice','Seattle');
INSERT INTO Restaurant VALUES (3,'Noodle Land', 'Redmond');

INSERT INTO City VALUES (1,'Bellevue','wa');
INSERT INTO City VALUES (2,'Seattle','wa');
INSERT INTO City VALUES (3,'Redmond','wa');

-- Insert into edge table. While inserting into an edge table,
-- you need to provide the $node_id from $from_id and $to_id columns.
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE ID = 1), 
       (SELECT $node_id FROM Restaurant WHERE ID = 1),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE ID = 2), 
      (SELECT $node_id FROM Restaurant WHERE ID = 2),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE ID = 3), 
      (SELECT $node_id FROM Restaurant WHERE ID = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE ID = 4), 
      (SELECT $node_id FROM Restaurant WHERE ID = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE ID = 5), 
      (SELECT $node_id FROM Restaurant WHERE ID = 3),9);

INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE ID = 1),
      (SELECT $node_id FROM City WHERE ID = 1));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE ID = 2),
      (SELECT $node_id FROM City WHERE ID = 2));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE ID = 3),
      (SELECT $node_id FROM City WHERE ID = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE ID = 4),
      (SELECT $node_id FROM City WHERE ID = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE ID = 5),
      (SELECT $node_id FROM City WHERE ID = 1));

INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE ID = 1),
      (SELECT $node_id FROM City WHERE ID =1));
INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE ID = 2),
      (SELECT $node_id FROM City WHERE ID =2));
INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE ID = 3),
      (SELECT $node_id FROM City WHERE ID =3));

-- Insert data into the friendOf edge.
INSERT INTO friendOf VALUES ((SELECT $NODE_ID FROM Person WHERE ID = 1), (SELECT $NODE_ID FROM Person WHERE ID = 2));
INSERT INTO friendOf VALUES ((SELECT $NODE_ID FROM Person WHERE ID = 2), (SELECT $NODE_ID FROM Person WHERE ID = 3));
INSERT INTO friendOf VALUES ((SELECT $NODE_ID FROM Person WHERE ID = 3), (SELECT $NODE_ID FROM Person WHERE ID = 1));
INSERT INTO friendOf VALUES ((SELECT $NODE_ID FROM Person WHERE ID = 4), (SELECT $NODE_ID FROM Person WHERE ID = 2));
INSERT INTO friendOf VALUES ((SELECT $NODE_ID FROM Person WHERE ID = 5), (SELECT $NODE_ID FROM Person WHERE ID = 4));


-- Find Restaurants that John likes
SELECT Restaurant.name
FROM Person, likes, Restaurant
WHERE MATCH (Person-(likes)->Restaurant)
AND Person.name = 'John';

-- Find Restaurants that John's friends like
SELECT Restaurant.name 
FROM Person person1, Person person2, likes, friendOf, Restaurant
WHERE MATCH(person1-(friendOf)->person2-(likes)->Restaurant)
AND person1.name='John';

-- Find people who like a restaurant in the same city they live in
SELECT Person.name
FROM Person, likes, Restaurant, livesIn, City, locatedIn
WHERE MATCH (Person-(likes)->Restaurant-(locatedIn)->City AND Person-(livesIn)->City);
```

## <a name="clean-up"></a>정리  
예제에 대해 만든 스키마 및 데이터베이스를 정리 합니다.

```
USE graphdemo;
go

DROP TABLE IF EXISTS likes;
DROP TABLE IF EXISTS Person;
DROP TABLE IF EXISTS Restaurant;
DROP TABLE IF EXISTS City;
DROP TABLE IF EXISTS friendOf;
DROP TABLE IF EXISTS livesIn;
DROP TABLE IF EXISTS locatedIn;

USE master;
go
DROP DATABASE graphdemo;
go
```

## <a name="script-explanation"></a>스크립트 설명  
이 스크립트는 새 T-sql 구문을 사용 하 여 노드 및에 지 테이블을 만듭니다. 문을 사용 하 여 노드 및에 지 테이블에 데이터를 삽입 하는 방법과 `INSERT` `MATCH` 패턴 일치 및 탐색을 위해 절을 사용 하는 방법을 보여 줍니다.

|명령    |메모
|---  |---  |
|[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)  |그래프 노드 또는에 지 테이블 만들기  |
|[INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)  |노드 또는에 지 테이블에 삽입  |
|[Transact-sql&#41;일치 &#40;](../../t-sql/queries/match-sql-graph.md)  |MATCH를 사용 하 여 패턴을 일치 하거나 그래프를 통과  |
