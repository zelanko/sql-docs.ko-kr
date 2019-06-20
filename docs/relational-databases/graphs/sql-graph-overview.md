---
title: SQL Server 및 Azure SQL Database에서 그래프 처리 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dcabc19d3c83cd1ed4c9ee7b8047759e2550863e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62502503"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 그래프 처리
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다 대 다 관계를 모델링 하는 그래프 데이터베이스 기능을 제공합니다. 그래프 관계에 통합 되어 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 사용 하는 이점은 받고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본적인 데이터베이스 관리 시스템으로 합니다.


## <a name="what-is-a-graph-database"></a>그래프 데이터베이스는 무엇입니까?  
그래프 데이터베이스는 노드(또는 꼭짓점) 및 모서리(또는 관계) 컬렉션입니다. 노드는 엔터티(예: 사용자 또는 조직)를 나타내고, 모서리는 연결된 두 노드 간 관계(예: 호감 또는 친구)를 나타냅니다. 노드 및에 지 모두 관련 된 속성이 있을 수 있습니다. 그래프 데이터베이스를 고유 하 게 설정 하는 일부 기능은 다음과 같습니다.  
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
새 `MATCH` 절 패턴 일치 및 graph 통해 다중 홉 탐색을 지원 하기 위해 도입 되었습니다. `MATCH` 함수 패턴 일치를 위해 ASCII art 스타일 구문을 사용 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>에 완전히 통합 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔진 
그래프 확장에 완전히 통합 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔진입니다. 저장 및 그래프 데이터를 쿼리 하는 동일한 저장소 엔진, 메타 데이터, 쿼리 프로세서 등을 사용 합니다. 그래프와 단일 쿼리에서 관계형 데이터에서 쿼리 합니다. 다른 그래프 기능을 결합 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] columnstore HA R services와 같은 기술이 등입니다. SQL 그래프 데이터베이스에서는 모든 보안 및 규정 준수 기능에서 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.
 
### <a name="tooling-and-ecosystem"></a>도구 및 에코 시스템

기존 도구 및 에코 시스템에서 활용 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제공 합니다. 백업 및 복원와 같은 도구 가져오기 및 내보내기에 BCP 즉시 작동 합니다. 관계형 테이블을 사용 하 여 작동 방식으로 다른 도구 또는 SSIS, SSRS, 또는 Power BI와 같은 서비스 그래프 테이블을 사용 하 여 작동 됩니다.

## <a name="edge-constraints"></a>에지 제약 조건
에 지 제약 그래프에 지 테이블에 정의 되 고 지정 된 가장자리 유형을 연결할 수 있는 노드 테이블의 쌍입니다. 사용자가 해당 그래프 스키마를 더 세부적으로 제어할을 이렇게 합니다. 에 지 제약 조건 사용 하 여 사용자 지정 된 가장자리를 연결할 수는 노드의 형식을 제한할 수 있습니다. 

참조 만들기 및에 지 제약 조건을 사용 하는 방법을 자세히 알아보려면 [에 지 제약 조건](../../relational-databases/tables/graph-edge-constraints.md)

## <a name="merge-dml"></a>DML 병합 
합니다 [병합](../../t-sql/statements/merge-transact-sql.md) 문은 insert를 수행 하 고, 업데이트 또는 삭제 작업의 원본 테이블에 조인 결과 따라 대상 테이블에 있습니다. 예를 들어, 삽입, 업데이트 또는 원본 테이블과 대상 테이블의 차이점에 따라 대상 테이블에서 행을 삭제 하 여 두 테이블을 동기화 할 수 있습니다. MERGE 문에서 일치 조건자를 사용 하 여 Azure SQL Database 및 SQL Server vNext에서 이제 지원 됩니다. 즉, 일치 조건자를 사용 하 여 별도 INSERT/UPDATE/DELETE 문 대신 단일 문에서 그래프 관계를 지정 하는 새 데이터를 사용 하 여 현재 그래프 데이터 (노드 또는 지 테이블)를 병합할 수 되었습니다.

참조 DML 병합에서 일치를 사용할 수 있는 방법을 자세히 알아보려면 [병합 문](../../t-sql/statements/merge-transact-sql.md)

 ## <a name="next-steps"></a>다음 단계  
읽기는 [SQL 그래프 데이터베이스-아키텍처](./sql-graph-architecture.md)
   

