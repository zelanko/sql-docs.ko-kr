---
title: SQL Server 및 Azure SQL Database에서 그래프 처리 | Microsoft Docs
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
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38015679"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 그래프 처리
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다 대 다 관계를 모델링 하는 그래프 데이터베이스 기능을 제공합니다. 그래프 관계에 통합 되어 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 사용 하는 이점은 받고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본적인 데이터베이스 관리 시스템으로 합니다.


## <a name="what-is-a-graph-database"></a>그래프 데이터베이스는 무엇입니까?  
그래프 데이터베이스는 노드 (또는 꼭 짓 점)의 컬렉션 및 가장자리 (또는 관계). 노드 엔터티 (예: 사용자 또는 조직)를 나타내고,에 지 (예, 좋아요 또는 친구)에 연결 하는 두 노드 간의 관계를 나타냅니다. 노드 및에 지 모두 관련 된 속성이 있을 수 있습니다. 그래프 데이터베이스를 고유 하 게 설정 하는 일부 기능은 다음과 같습니다.  
-   가장자리 또는 관계는 그래프 데이터베이스에서 첫 번째 클래스 엔터티 및 수 있는 특성 또는 속성 하 합니다. 
-   가장자리가 하나 그래프 데이터베이스에서 여러 노드를 유연 하 게 연결 수 있습니다.
-   패턴 일치 및 다중 홉 탐색 쿼리를 쉽게 표현할 수 있습니다.
-   전이적 및 다형성 쿼리를 쉽게 표현할 수 있습니다.

## <a name="when-to-use-a-graph-database"></a>그래프 데이터베이스를 사용 하는 경우

항목이 없는 그래프 데이터베이스를 얻을 수 있는 관계형 데이터베이스를 사용 하 여 수행할 수 없습니다. 그러나 그래프 데이터베이스 수 쉽게 특정 유형의 쿼리를 표현할 수 있습니다. 또한 특정 최적화를 사용 하 여 특정 쿼리 성능이 더 뛰어나고 좀 합니다. 결정 호출이 하나를 선택 하는 다음 요인에 기반 할 수 있습니다.  
-   계층적 데이터에 응용 프로그램. HierarchyID 데이터 형식은 계층 구현에 사용할 수 하지만 몇 가지 제한 사항이 있습니다. 예를 들어이 없도록 노드에 대 한 여러 부모를 저장할 수 있습니다.
-   응용 프로그램에 복잡 한 다 대 다 관계입니다. 응용 프로그램 진화 함에 따라 새 관계 추가 됩니다.
-   상호 연결 된 데이터 및 관계를 분석 해야 합니다.

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>에 도입 된 그래프 기능 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
그래프 데이터를 저장 하 고 쿼리를 쉽게 수행할 수 있도록 SQL server에 그래프 확장을 추가 하기 시작 했습니다. 다음 기능은 첫 번째 릴리스에서 도입 되었습니다. 


### <a name="create-graph-objects"></a>그래프 개체 만들기
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] 확장 하면 노드 또는 지 테이블을 만듭니다. 노드와 가장자리에 연결 된 속성에 있을 수 있습니다. 하므로 노드 및에 지 테이블로 저장 됩니다, 그리고 노드 또는 지 테이블에서 관계형 테이블에서 지원 되는 모든 작업이 지원 됩니다. 다음 예를 참조하세요.  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![사용자 친구 테이블](../../relational-databases/graphs/media/person-friends-tables.png "Person 노드 및 친구 edge 테이블")  
노드 및에 지 테이블로 저장 됩니다.  

### <a name="query-language-extensions"></a>쿼리 언어 확장  
새 `MATCH` 절 패턴 일치 및 graph 통해 다중 홉 탐색을 지원 하기 위해 도입 되었습니다. `MATCH` 함수 패턴 일치를 위해 ASCII art 스타일 구문을 사용 합니다. 예를 들어:  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>에 완전히 통합 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔진 
그래프 확장에 완전히 통합 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔진입니다. 저장 및 그래프 데이터를 쿼리 하는 동일한 저장소 엔진, 메타 데이터, 쿼리 프로세서 등 사용 합니다. 따라서 사용자가 단일 쿼리에서 관계형 데이터와 그래프 데이터 간을 쿼리할 수 있습니다. 사용자가 다른 그래프 기능을 결합에서 활용할 수도 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] columnstore HA R services와 같은 기술이 등입니다. SQL 그래프 데이터베이스에서는 모든 보안 및 규정 준수 기능에서 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.
 
### <a name="tooling-and-ecosystem"></a>도구 및 에코 시스템  
기존 도구 및 에코 시스템에서 사용자 혜택는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제공 합니다. 백업 및 복원와 같은 도구 가져오기 및 내보내기에 BCP 즉시 작동 합니다. 관계형 테이블을 사용 하 여 작동 방식으로 다른 도구 또는 SSIS, SSRS 또는 PowerBI와 같은 서비스 그래프 테이블을 사용 하 여 작동 됩니다.
 
 ## <a name="next-steps"></a>다음 단계  
읽기는 [SQL 그래프 데이터베이스-아키텍처](./sql-graph-architecture.md)
   

