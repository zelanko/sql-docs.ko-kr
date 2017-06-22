---
title: "전체 텍스트 쿼리 성능 향상 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0658dc74-25eb-4486-bbd6-e85c1f92c272
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6ec53c06cb92a31b0488d2f6c4ef1f294e43c0a1
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="improve-the-performance-of-full-text-queries"></a>전체 텍스트 쿼리 성능 향상
  다음은 전체 텍스트 쿼리 성능 향상에 도움이 될 권장 사항 목록입니다.  
  
 전체 텍스트 쿼리의 성능은 메모리, 디스크 속도, CPU 속도 및 컴퓨터 아키텍처와 같은 하드웨어 리소스의 영향도 받습니다.  
  
-   [ALTER INDEX REORGANIZE](../../t-sql/statements/alter-index-transact-sql.md)를 사용하여 기본 테이블의 인덱스를 조각 모음합니다.  
  
-   [ALTER FULLTEXT CATALOG REORGANIZE](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)를 사용하여 전체 텍스트 카탈로그를 다시 구성합니다. 이 문을 실행하면 해당 카탈로그에 있는 전체 텍스트 인덱스의 마스터 병합이 수행되므로 성능 테스트 전에 실행해야 합니다.  
  
-   작은 열을 전체 텍스트 키 열로 선택합니다. 900바이트 열이 지원되지만 전체 텍스트 인덱스에서는 비교적 작은 키 열을 사용하는 것이 좋습니다. **int** 및 **bigint** 는 최적의 성능을 제공합니다.  
  
-   정수 전체 텍스트 키를 사용하면 **docid** 매핑 테이블과의 조인이 방지됩니다. 따라서 정수 전체 텍스트 키는 작업량을 줄여 쿼리 성능을 높이고 탐색 성능을 개선합니다. 전체 텍스트 키가 클러스터형 인덱스 키인 경우에도 또 다른 성능 이점을 얻을 수 있습니다.  
  
-   여러 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 조건자를 하나의 CONTAINS 조건자에 결합합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 CONTAINS 쿼리에 열 목록을 지정할 수 있습니다.  
  
-   전체 텍스트 키 또는 순위 정보만 필요한 경우 CONTAINS 또는 FREETEXT를 사용하는 대신 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 또는 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 을 각각 사용합니다.  
  
-   결과를 제한하고 성능을 향상시키려면 FREETEXTTABLE 및 CONTAINSTABLE 함수의 *top_n_by_rank* 매개 변수를 사용합니다. *top_n_by_rank* 를 사용하면 관련성이 가장 높은 항목만 회수할 수 있습니다. 이 매개 변수는 비즈니스 시나리오에서 일치하는 모든 항목을 회수하지 않아도 되는 경우, 즉 *전체 회수*가 필요 없는 경우에만 사용합니다.  
  
    > [!NOTE]  
    >  전체 회수는 대개 법률 시나리오에 필요하지만 e-비즈니스와 같은 비즈니스 시나리오에서는 성능보다 중요하지 않을 수 있습니다.  
  
-   전체 텍스트 쿼리 계획을 검사하여 적절한 조인 계획이 선택되었는지 확인합니다. 필요한 경우 조인 힌트 또는 쿼리 힌트를 사용합니다. 전체 텍스트 쿼리에서 매개 변수가 사용될 경우 매개 변수의 첫 번째 값이 쿼리 계획을 결정합니다. OPTIMIZE FOR [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md) 를 사용하여 쿼리를 원하는 값으로 컴파일하도록 지정할 수 있습니다. 이렇게 하면 결정적 쿼리 계획 및 향상된 성능을 실현하는 데 도움이 됩니다.  
  
-   전체 텍스트 인덱스에 전체 텍스트 인덱스 조각이 너무 많으면 쿼리 성능이 크게 저하될 수 있습니다. 조각 수를 줄이려면 [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 REORGANIZE 옵션을 사용하여 전체 텍스트 카탈로그를 다시 구성합니다. 이 문은 기본적으로 모든 조각을 비교적 큰 하나의 조각으로 병합하고 전체 텍스트 인덱스에서 사용되지 않는 항목을 모두 제거합니다.  
  
-   전체 텍스트 검색에서 CONTAINSTABLE에 지정되는 논리 연산자(AND, OR)는 SQL 조인으로 구현하거나 전체 텍스트 실행 STVF(스트리밍 테이블 반환 함수) 내에서 구현할 수 있습니다. 일반적으로 한 가지 논리 연산자만 포함된 쿼리는 전체 텍스트 실행으로만 구현되는 데 반해 논리 연산자가 혼합되어 있는 쿼리는 SQL 조인도 포함합니다. 전체 텍스트 실행 STVF 내 논리 연산자 구현에는 SQL 조인보다 실행 속도가 빠른 일부 특수한 인덱스 속성이 사용됩니다. 따라서 가능하면 단일 유형의 논리 연산자만 사용하여 쿼리를 작성하는 것이 좋습니다.  
  
-   선택적 관계 조건을 포함하는 응용 프로그램의 경우 선택적 관계 조건자와 비선택적 전체 텍스트 조건자를 사용하는 쿼리는 쿼리 최적화 프로그램을 사용하도록 작성되었을 때 최상의 성능을 발휘할 수 있습니다. 이렇게 하면 쿼리 최적화 프로그램이 효과적인 쿼리 계획을 생성하기 위해 조건자나 범위 축소 중 어느 것을 이용할지 결정할 수 있습니다. 이러한 방식은 관계형 데이터를 전체 텍스트 데이터로 인덱싱하는 것보다 간단하고 효율적일 때가 많습니다.  
  
## <a name="related-resources"></a>관련 리소스  
 [SQL Server 2008 전체 텍스트 검색: 내부 및 향상 내용](http://go.microsoft.com/fwlink/?LinkId=129544)  
  
## <a name="see-also"></a>참고 항목  
 [sys.dm_fts_memory_buffers&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)   
 [sys.dm_fts_memory_pools&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
  
  
