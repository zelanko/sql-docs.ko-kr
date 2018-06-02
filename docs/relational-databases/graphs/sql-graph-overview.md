---
title: SQL Server 및 Azure SQL 데이터베이스를 사용 하 여 처리 하는 그래프 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: graphs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 8c2ad7f5b31a97de5d0bfb22074b55bd61bb825b
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707051"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL 데이터베이스를 사용 하 여 처리 하는 그래프
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모델의 다 대 다 관계를 그래프 데이터베이스 기능도 제공합니다. 그래프 관계에 통합 되어 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 수신 사용의 이점 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본적인 데이터베이스 관리 시스템으로 합니다.


## <a name="what-is-a-graph-database"></a>그래프 데이터베이스 이란?  
그래프 데이터베이스는 노드 (또는 꼭지점)의 컬렉션 및 가장자리 (또는 관계). 노드를 나타냅니다 (예: 사용자 또는 조직) 엔터티 및 가장자리 (예, like 또는 친구)에 연결 하는 두 노드 간의 관계를 나타냅니다. 노드와 가장자리에 관련 된 속성이 있을 수 있습니다. 다음은 그래프 데이터베이스를 고유 하 게 설정 하는 기능:  
-   가장자리 또는 관계 그래프 데이터베이스의 엔터티를 첫 번째 클래스 이며 수 특성 또는 속성이 연결 된입니다. 
-   가장자리가 하나 그래프 데이터베이스의 여러 노드에서 연결할 유연 하 게 수 있습니다.
-   패턴 일치 및 다중 홉 탐색 쿼리를 쉽게 표현할 수 있습니다.
-   전이적 및 다형 쿼리를 쉽게 표현할 수 있습니다.

## <a name="when-to-use-a-graph-database"></a>그래프 데이터베이스를 사용 하는 경우

없는 그래프 데이터베이스 얻을 수 있는 관계형 데이터베이스를 사용 하 여 얻을 수 없는 됩니다. 그러나 그래프 데이터베이스 쉽게 만들 수 특정 종류의 쿼리를 표현할 수 있습니다. 또한 특정 최적화 기능이 특정 쿼리 성능이 좋아질 수 있습니다. 다음과 같은 요인에 따라 호출이 하나를 선택 하 여 결정:  
-   응용 프로그램에 계층적 데이터. HierarchyID 데이터 형식 계층 구조를 구현 하려면 사용할 수 했으나 몇 가지 제한 사항이 있습니다. 예를 들어이 없도록 노드에 대 한 여러 부모를 저장할 수 있습니다.
-   응용 프로그램에 복잡 한 다 대 다 관계입니다. 응용 프로그램 진화 함에 따라 새 관계 추가 됩니다.
-   상호 연결 된 데이터 및 관계를 분석 해야 합니다.

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>에 도입 된 그래프 기능 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
SQL server에 저장 하 고 쿼리 그래프 데이터를 쉽게 수행할 수 있도록 그래프 확장을 추가 합니다. 사용 하기 시작 합니다. 다음과 같은 기능이 첫 번째 릴리스에서 도입 됩니다. 


### <a name="create-graph-objects"></a>그래프 개체 만들기
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] 확장 노드 또는 edge 테이블을 만드는 데는 사용자를 수 있습니다. 노드와 가장자리에 연결 된 속성에 있을 수 있습니다. 이후, 노드 및 가장자리 테이블로 저장 됩니다, 그리고 노드 또는 edge 테이블에 관계형 테이블에서 지원 되는 모든 작업이 지원 됩니다. 다음 예를 참조하세요.  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![사용자 친구 테이블](../../relational-databases/graphs/media/person-friends-tables.png "Person 노드 및 friend 가장자리 테이블")  
노드 및 가장자리 테이블로 저장 됩니다.  

### <a name="query-language-extensions"></a>쿼리 언어 확장  
새 `MATCH` 절 패턴 일치와 그래프를 통해 다중 홉 탐색을 지원 하기 위해 도입 됩니다. `MATCH` 함수 패턴 일치에 대 한 ASCII 아트 스타일 구문을 사용 합니다. 예를 들어:  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>에 완전히 통합 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔진 
Graph 확장에 통합 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔진입니다. 저장 하 고 그래프 데이터를 쿼리는 동일한 저장소 엔진 메타 데이터, 쿼리 프로세서, 등 사용 합니다. 그러면 사용자가 단일 쿼리에서 관계형 데이터의 그래프 및 간에 쿼리할 수 있습니다. 사용자가 다른 그래프 기능을 결합에서 활용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] columnstore, HA, R 서비스와 같은 기술은 등입니다. SQL 그래프 데이터베이스에도 모든 보안 및 규정 준수 기능에서 사용할 수 있는 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.
 
### <a name="tooling-and-ecosystem"></a>도구 및 에코 시스템  
기존 도구 및 에코 시스템에서 사용자가 활용 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제공 합니다. 백업 및 복원와 같은 도구 가져오기 및 내보내기, 즉시 BCP 순조롭게 진행 합니다. 관계형 테이블을 사용할 방식으로 다른 도구 또는 SSIS, SSRS 또는 PowerBI와 같은 서비스 그래프 테이블과 함께 작동 합니다.
 
 ## <a name="next-steps"></a>다음 단계  
읽기는 [SQL 그래프 데이터베이스-아키텍처](./sql-graph-architecture.md)
   

