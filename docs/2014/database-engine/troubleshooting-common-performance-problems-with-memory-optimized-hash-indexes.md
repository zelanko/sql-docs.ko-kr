---
title: 메모리 액세스에 최적화 된 해시 인덱스와 함께 일반적인 성능 문제 해결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1954a997-7585-4713-81fd-76d429b8d095
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 625bde655c6d95ac30966dd39a52534fc5a84299
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092042"
---
# <a name="troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes"></a>메모리 액세스에 최적화된 해시 인덱스의 일반적인 성능 문제 해결
  이 항목에서는 해시 인덱스의 일반적인 문제 해결을 집중적으로 다룹니다.  
  
## <a name="search-requires-a-subset-of-hash-index-key-columns"></a>검색에 해시 인덱스 키 열의 하위 집합 필요  
 **문제:** 모든 값을 해시 값을 계산 하기 위해 인덱스 키 열 및 해시 테이블에서 해당 행을 찾으려면 해시 인덱스가 필요 합니다. 따라서 쿼리의 WHERE 절에 인덱스 키의 하위 집합에만 적용되는 같음 조건자가 있는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 Index Seek를 사용하여 WHERE 절의 조건자에 해당하는 행을 찾을 수 없습니다.  
  
 반대로 디스크 기반 비클러스터형 인덱스 및 메모리 최적화 비클러스터형 인덱스와 같은 정렬된 인덱스는 인덱스 키 열의 하위 집합에서 Index Seek를 지원합니다(해당 열이 인덱스의 선행 열인 한에서).  
  
 **증상:** 이 인해 성능이 저하 되는로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 하는 일반적으로 더 빠른 연산인 index seek 대신 전체 테이블 검색의 실행 해야 합니다.  
  
 **해결 방법:** 성능 저하 외에도 쿼리 계획의 검사 하면 index seek 대신에 검색이 표시 됩니다. 쿼리가 매우 간단한 경우 쿼리 텍스트와 인덱스 정의를 검사해도 검색에 인덱스 키 열의 하위 집합이 필요한지 여부가 표시됩니다.  
  
 다음 테이블과 쿼리를 살펴 보십시오.  
  
```tsql  
CREATE TABLE [dbo].[od]  
(  
     o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
     CONSTRAINT PK_od PRIMARY KEY NONCLUSTERED HASH (o_id, od_id) WITH (BUCKET_COUNT = 10000)  
)  
WITH (MEMORY_OPTIMIZED = ON)  
  
 SELECT p_id  
 FROM dbo.od  
 WHERE o_id=1  
```  
  
 테이블에는 두 열(o_id, od_id)에 해시 인덱스가 있지만 쿼리에는 (o_id)에 같음 조건자가 있습니다. 쿼리에는 인덱스 키 열의 하위 집합에만 같음 연산자가 있으므로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 PK_od를 사용하여 Index Seek 연산을 수행할 수 없습니다. 그 대신, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 전체 인덱스 검색으로 돌아가야 합니다.  
  
 **해결 방법:** 해결할 수 있는 방법은 여러 가지가 있습니다. 예를 들어:  
  
-   비클러스터형 해시 대신 비클러스터형 유형으로 인덱스를 다시 만듭니다. 메모리 최적화 비클러스터형 인덱스가 정렬되므로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 선행 인덱스 키 열에서 Index Seek를 수행할 수 있습니다. 결과적으로 이 예의 기본 키 정의는 `constraint PK_od primary key nonclustered`가 됩니다.  
  
-   현재 인덱스 키를 WHERE 절의 열과 일치하도록 변경합니다.  
  
-   쿼리의 WHERE 절에 있는 열과 일치하는 새 해시 인덱스를 추가합니다. 이 예에서는 결과 테이블 정의가 다음과 같은 모양이 됩니다.  
  
    ```tsql  
    CREATE TABLE dbo.od  
     ( o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
  
     CONSTRAINT PK_od PRIMARY KEY   
     NONCLUSTERED HASH (o_id,od_id) WITH (BUCKET_COUNT=10000),  
  
     INDEX ix_o_id NONCLUSTERED HASH (o_id) WITH (BUCKET_COUNT=10000)  
  
     ) WITH (MEMORY_OPTIMIZED=ON)  
    ```  
  
 지정 된 인덱스 키 값에 대 한 중복 행을 많이 있는 경우 메모리 액세스에 최적화 된 해시 인덱스를 최적 상태로 수행 되지 않는 참고: 예제에서는 o_id 열의 고유 값 수가 테이블의 행 수보다 훨씬 작은 경우 최적의 인덱스 (o_id);에 추가할 수 없습니다 대신 해시에서 비클러스터형으로 PK_od 인덱스의 형식을 변경 것 더 나은 솔루션입니다. 자세한 내용은 참조 [해시 인덱스에 대 한 올바른 버킷 수 결정](../relational-databases/indexes/indexes.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 액세스에 최적화된 테이블의 인덱스](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  