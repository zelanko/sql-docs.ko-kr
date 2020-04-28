---
title: 그래프 처리 중
titleSuffix: SQL Server and Azure SQL Database
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
author: shkale-msft
ms.author: shkale
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2b0934562f2f0ff1a2dd3ec8df1ed15f10d955ee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "79428154"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database를 사용한 Graph 처리
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]다대다 관계를 모델링 하는 그래프 데이터베이스 기능을 제공 합니다. 그래프 관계는에 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 통합 되며를 기본 데이터베이스 관리 시스템으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하는 이점을 제공 합니다.


## <a name="what-is-a-graph-database"></a>그래프 데이터베이스란?  
그래프 데이터베이스는 노드(또는 꼭짓점) 및 모서리(또는 관계) 컬렉션입니다. 노드는 엔터티(예: 개인 또는 조직)를 나타내고 에지는 에지가 연결하는 두 노드 간의 관계(예: 좋아요 또는 친구)를 나타냅니다. 노드와 가장자리 모두에 연결 된 속성이 있을 수 있습니다. 그래프 데이터베이스를 고유하게 만드는 몇 가지 기능은 다음과 같습니다.  
-    에지 또는 관계는 그래프 데이터베이스의 첫 번째 클래스 엔터티이며 엔터티와 연결된 특성 또는 속성을 포함할 수 있습니다. 
-    단일 에지는 유연하게 그래프 데이터베이스의 여러 노드를 연결할 수 있습니다.
-    패턴 일치 및 멀티 홉 탐색 쿼리를 쉽게 표현할 수 있습니다.
-    이행적 폐쇄 및 다형적 쿼리를 쉽게 표현할 수 있습니다.

## <a name="when-to-use-a-graph-database"></a>그래프 데이터베이스를 사용 하는 경우

관계형 데이터베이스는 그래프 데이터베이스에서 수행할 수 있는 모든 작업을 수행할 수 있습니다. 그러나 graph 데이터베이스를 사용 하면 특정 종류의 쿼리를 보다 쉽게 표현할 수 있습니다. 또한 특정 최적화를 사용 하면 특정 쿼리를 보다 효율적으로 수행할 수 있습니다. 관계형 데이터베이스 또는 그래프 데이터베이스를 선택 하는 것은 다음 요소에 따라 결정 됩니다.  
-    응용 프로그램에 계층적 데이터가 있습니다. HierarchyID 데이터 형식은 계층을 구현 하는 데 사용할 수 있지만 몇 가지 제한 사항이 있습니다. 예를 들어 노드에 대 한 여러 부모를 저장 하는 것은 허용 되지 않습니다.
-    응용 프로그램에 복잡 한 다 대 다 관계가 있습니다. 응용 프로그램이 진화 함에 따라 새 관계가 추가 됩니다.
-    상호 연결된 데이터 및 관계를 분석해야 합니다.

## <a name="graph-features-introduced-in-sssqlv14"></a>에서 도입 된 그래프 기능[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
그래프 데이터를 보다 쉽게 저장 하 고 쿼리할 수 있도록 SQL Server에 그래프 확장을 추가 하기 시작 합니다. 첫 번째 릴리스에서는 다음과 같은 기능이 도입 되었습니다. 


### <a name="create-graph-objects"></a>그래프 개체 만들기
[!INCLUDE[tsql-md](../../includes/tsql-md.md)]확장을 통해 사용자는 노드 또는에 지 테이블을 만들 수 있습니다. 노드와 가장자리 모두에 연결 된 속성을 가질 수 있습니다. 에서는 노드와 가장자리가 테이블로 저장 되므로 관계형 테이블에서 지원 되는 모든 작업은 노드 또는에 지 테이블에서 지원 됩니다. 다음은 예제입니다.  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![사람-친구-테이블](../../relational-databases/graphs/media/person-friends-tables.png "Person 노드 및 친구에 지 테이블")  
노드 및 가장자리가 테이블로 저장 됩니다.  

### <a name="query-language-extensions"></a>쿼리 언어 확장  
New `MATCH` 절은 그래프를 통해 패턴 일치 및 다중 홉 탐색을 지원 하기 위해 도입 되었습니다. 함수 `MATCH` 는 패턴 일치에 ASCII 아트 스타일 구문을 사용 합니다. 예를 들면 다음과 같습니다.  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-ssnoversion-engine"></a>엔진에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 완벽 하 게 통합 
그래프 확장은 엔진에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 완벽 하 게 통합 됩니다. 동일한 저장소 엔진, 메타 데이터, 쿼리 프로세서 등을 사용 하 여 그래프 데이터를 저장 하 고 쿼리 합니다. 단일 쿼리에서 그래프 및 관계형 데이터에 대해 쿼리 합니다. 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 (예: COLUMNSTORE, HA, R services 등)과 그래프 기능 결합 SQL graph 데이터베이스는 에서도 사용할 수 있는 모든 보안 및 규정 준수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]기능을 지원 합니다.
 
### <a name="tooling-and-ecosystem"></a>도구 및 에코 시스템

에서 제공 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기존 도구 및 에코 시스템을 활용 합니다. 백업 및 복원, 가져오기 및 내보내기와 같은 도구는 기본적으로 작동 합니다. SSIS, SSRS 또는 Power BI와 같은 다른 도구나 서비스는 관계형 테이블로 작업 하는 방법만 그래프 테이블에 사용할 수 있습니다.

## <a name="edge-constraints"></a>에지 제약 조건
에 지 제약 조건은 그래프에 지 테이블에 정의 되 고 지정 된 가장자리 유형에 서 연결할 수 있는 노드 테이블 쌍입니다. 이렇게 하면 사용자가 graph 스키마를 더 효율적으로 제어할 수 있습니다. 에 지 제약 조건에 대 한 도움을 받아 사용자는 지정 된 edge가 연결할 수 있는 노드 유형을 제한할 수 있습니다. 

에 지 제약 조건을 만들고 사용 하는 방법에 대 한 자세한 내용은 [가장자리 제약 조건](../../relational-databases/tables/graph-edge-constraints.md) 을 참조 하세요.

## <a name="merge-dml"></a>DML 병합 
[MERGE](../../t-sql/statements/merge-transact-sql.md) 문은 원본 테이블과의 조인 결과에 따라 대상 테이블에서 삽입, 업데이트 또는 삭제 작업을 수행 합니다. 예를 들어 대상 테이블 및 원본 테이블 간의 차이점에 따라 대상 테이블에서 행을 삽입, 업데이트 또는 삭제 하 여 두 테이블을 동기화 할 수 있습니다. 이제 Azure SQL Database 및 SQL Server vNext에서 MERGE 문에 MATCH 조건자를 사용할 수 있습니다. 즉, 이제 개별 INSERT/UPDATE/DELETE 문을 사용 하는 대신 일치 조건자를 사용 하 여 현재 그래프 데이터 (노드 또는 가장자리 테이블)를 새 데이터와 병합 하 여 단일 문에서 그래프 관계를 지정할 수 있습니다.

Merge DML에서 일치를 사용할 수 있는 방법에 대 한 자세한 내용은 merge [문](../../t-sql/statements/merge-transact-sql.md) 참조

## <a name="shortest-path"></a>최단 경로
[SHORTEST_PATH](./sql-graph-shortest-path.md) 함수는 그래프의 노드 2 개 사이에서 가장 짧은 경로를 찾거나 지정 된 노드에서 그래프의 다른 노드로 시작 하는 최단 경로를 찾습니다. 최단 경로를 사용 하 여 그래프에서 전이적 클로저 또는 임의 길이의 순회를 찾을 수도 있습니다. 

 ## <a name="next-steps"></a>다음 단계  
[SQL Graph 데이터베이스-아키텍처](./sql-graph-architecture.md) 읽기
   

