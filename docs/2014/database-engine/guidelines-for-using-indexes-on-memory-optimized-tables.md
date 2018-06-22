---
title: 메모리 액세스에 최적화 된 테이블에서 인덱스 사용 지침 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- hash indexes
ms.assetid: 16ef63a4-367a-46ac-917d-9eebc81ab29b
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: e047c19deb12d67b23a4627410b998e8c2465107
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090495"
---
# <a name="guidelines-for-using-indexes-on-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 인덱스 사용 지침
  인덱스는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블에서 데이터에 효율적으로 액세스하는 데 사용됩니다. 올바른 인덱스를 지정하면 쿼리 성능을 크게 개선할 수 있습니다. 예를 들어, 다음 쿼리를 살펴보세요.  
  
```tsql  
SELECT c1, c2 FROM t WHERE c1 = 1;  
```  
  
 열 c1에 인덱스가 없는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]은 전체 테이블 t를 검색한 다음 조건 c1=1을 만족하는 행을 필터링해야 합니다. 그러나 열 c1에 인덱스가 있는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]은 값 1을 직접 검색하고 행을 검색할 수 있습니다.  
  
 테이블에 있는 하나 이상의 열에 대해 특정한 값 또는 값의 범위를 갖는 레코드를 검색할 때 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]은 이러한 열에 있는 인덱스를 사용하여 해당 레코드를 신속하게 찾을 수 있습니다. 디스크 기반 및 메모리 최적화 테이블 모두 인덱스를 이용할 수 있습니다. 그러나 메모리 최적화 테이블을 사용하는 경우에는 인덱스 구조 사이의 특정한 차이를 고려해야 합니다. 메모리 최적화 테이블의 인덱스를 메모리 최적화 인덱스라고 합니다. 주요 차이점은 다음과 같습니다.  
  
-   메모리 액세스에 최적화 된 인덱스를 사용 하 여 만들어야 합니다 [CREATE TABLE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)합니다. 디스크 기반 인덱스는 `CREATE TABLE` 및 `CREATE INDEX`를 사용하여 만들 수 있습니다.  
  
-   메모리 액세스에 최적화된 인덱스는 메모리에만 존재합니다. 인덱스 구조는 디스크에 유지되지 않으며 인덱스 작업은 트랜잭션 로그에 기록되지 않습니다. CREATE TABLE 실행 중과 데이터베이스 시작 중에 메모리 최적화 테이블이 메모리에 만들어질 때 인덱스 구조가 만들어집니다.  
  
-   메모리 액세스에 최적화된 인덱스는 본질적으로 포함됩니다. 포함이란 모든 열이 인덱스에 거의 포함되며 메모리 최적화 테이블의 경우 책갈피 조회가 필요하지 않음을 의미합니다. 기본 키를 참조하는 대신 메모리 최적화 인덱스는 테이블 데이터 구조에서 실제 행에 대한 메모리 포인터만 포함합니다.  
  
-   조각화 및 fillfactor는 메모리 최적화 인덱스에 적용되지 않습니다. 디스크 기반 인덱스에서 조각화는 디스크에 순서 없이 쓰여지는 B-트리의 페이지를 참조합니다. 메모리 액세스에 최적화된 인덱스는 디스크에 쓰거나 디스크에서 읽지 않습니다. 디스크 기반 B-트리 인덱스의 Fillfactor는 물리적 페이지 구조가 실제 데이터로 채워지는 정도를 나타냅니다. 메모리 최적화 인덱스 구조에는 크기가 고정된 페이지가 포함되지 않습니다.  
  
 메모리 최적화 인덱스의 종류는 다음 두 가지입니다.  
  
-   포인트 조회를 위해 만들어진 비클러스터형 해시 인덱스. 해시 인덱스에 대 한 자세한 내용은 참조 [해시 인덱스](hash-indexes.md)합니다.  
  
-   범위 검색 및 정렬된 검색을 위해 만들어진 비클러스터형 인덱스  
  
 해시 인덱스를 사용하면 메모리의 해시 테이블을 통해 데이터에 액세스할 수 있습니다. 해시 인덱스에는 페이지가 없으며 크기가 항상 고정되어 있습니다. 그러나 해시 인덱스는 빈 해시 버킷을 가질 수 있어 낭비되는 공간이 제한적입니다. 해시 인덱스를 사용하여 쿼리에서 반환되는 값은 정렬되지 않습니다. 해시 인덱스는 같음 조건자에 대한 인덱스 검색에 최적화되며 전체 인덱스 검색도 지원합니다.  
  
 비클러스터형 인덱스(해시 인덱스가 아님)는 해시 인덱스가 지원하는 모든 것을 지원하며 보다 큼 또는 보다 작음과 같은 같지 않음 조건자에 대한 Seek 연산 및 정렬 순서를 추가로 지원합니다. 인덱스 생성 시 지정한 순서에 따라 행을 검색할 수 있습니다. 인덱스 정렬 순서가 특정 쿼리에 필요한 정렬 순서와 일치하면, 예를 들어, 인덱스 키가 ORDER BY 절과 일치하면 쿼리 실행의 일부로 행을 정렬할 필요가 없습니다. 메모리 액세스에 최적화된 비클러스터형 인덱스는 단방향이며 따라서 인덱스 정렬 순서의 역방향으로 행을 검색하는 것은 지원하지 않습니다. 예를 들어, (c1 ASC)로 지정된 경우 역방향(c1 DESC) 인덱스 검색은 수행할 수 없습니다.  
  
 각 인덱스는 메모리를 소모합니다. 해시 인덱스는 고정된 크기의 메모리를 소모하며, 버킷 수의 함수입니다. 비클러스터형 인덱스의 경우 메모리 사용은 행 개수, 인덱스 키 열의 크기, 작업에 따라 발생하는 일정량의 추가 오버헤드를 반영합니다. 메모리 최적화 인덱스용 메모리는 메모리 최적화 테이블에 행을 저장하는 데 사용되는 메모리와 별개로 추가됩니다.  
  
 중복 키 값은 항상 동일한 해시 버킷을 공유합니다. 해시 인덱스에 여러 중복 키 값이 포함되어 있어 긴 해시 체인이 만들어지면 성능에 악영향을 줄 수 있습니다. 해시 충돌이 해시 인덱스에서 발생하면 이 시나리오의 성능이 한층 낮아집니다. 이런 이유로 고유한 인덱스 키 수가 행 수보다 100 배 이상 작은 경우 줄일 수 있습니다 해시 충돌의 위험이 훨씬 더 큰 계산 버킷 함으로써 (8 배 이상 고유 인덱스 키 수가 참조; [결정은 해시 인덱스에 대 한 올바른 버킷 수](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md) 자세한 정보에 대 한) 또는 비클러스터형 인덱스를 사용 하 여 완전히 해시 충돌을 제거할 수 있습니다.  
  
## <a name="determining-which-indexes-to-use-for-a-memory-optimized-table"></a>메모리 액세스에 최적화된 테이블에 사용할 인덱스 결정  
 메모리 최적화 각 테이블에는 하나 이상의 인덱스가 있어야 합니다. 각 PRIMARY KEY 제약 조건은 인덱스를 암시적으로 만듭니다. 따라서 테이블에 기본 키가 있는 경우 인덱스가 있는 것입니다. 기본 키는 내구성 있는 메모리 최적화 테이블에 대한 요구 사항입니다.  
  
 메모리 최적화 테이블을 쿼리하는 경우 조건자 절에 같음 조건자만 포함되어 있으면 해시 인덱스의 성능이 향상됩니다. 조건자에는 해시 인덱스 키의 모든 열이 포함되어야 합니다. 해시 인덱스는 같지 않음 조건자가 주어진 경우 검색으로 되돌아갑니다.  
  
 메모리 최적화 테이블의 열은 해시 인덱스와 비클러스터형 인덱스 둘 다에 포함될 수 있습니다.  
  
 같지 않음 조건자를 사용하여 메모리 최적화 테이블을 쿼리하는 경우 비클러스터형 인덱스는 비클러스터형 해시 인덱스보다 성능이 우수합니다.  
  
 해시 인덱스는 인덱스를 검색하기 위해 해시할 키를 필요로 합니다. 인덱스 키가 두 열로 구성된 경우 첫 번째 열만 제공하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 해시할 완전한 키를 갖추지 못합니다. 이 때문에 인덱스 검색 쿼리 계획이 만들어집니다. 인덱싱되어야 하는 열은 사용 사례에 따라 결정됩니다.  
  
 비클러스터형 인덱스의 열 값이 많은 행에서 같은 경우(인덱스 키 열에 중복 값이 많은 경우) 업데이트, 삽입 및 삭제 성능이 저하될 수 있습니다.  이 상황에서 성능을 향상시키는 한 가지 방법은 비클러스터형 인덱스에 다른 열을 추가하는 것입니다.  
  
### <a name="operations-on-memory-optimized-and-disk-based-indexes"></a>메모리 최적화 인덱스 및 디스크 기반 인덱스의 작업.  
  
|연산|메모리 액세스에 최적화된 비클러스터형 해시, 인덱스|메모리 액세스에 최적화된 비클러스터형 인덱스|디스크 기반 인덱스|  
|---------------|-------------------------------------------------|------------------------------------------|-----------------------|  
|색인 검색은 모든 테이블 행을 검색합니다.|예|예|예|  
|같음 조건자(=)의 인덱스 검색.|예<br /><br /> (전체 키 필요)|예 <sup>1</sup>|예|  
|같지 않음 조건자에서 인덱스 검색 (>, <, \<=, > =, BETWEEN).|아니요(인덱스 검색의 결과)|예 <sup>1</sup>|예|  
|인덱스 정의와 일치하는 정렬 순서로 행을 검색합니다.|아니요|예|예|  
|인덱스 정의의 역순과 일치하는 정렬 순서로 행을 검색합니다.|아니요|아니요|예|  
  
 이 표에서 테이블에서 "예"는 인덱스가 요청을 적절히 처리할 수 있음을 의미하며 "아니요"는 인덱스를 사용하여 요청을 충족할 수 없음을 의미합니다.  
  
 <sup>1</sup> 클러스터 되지 않은 메모리 액세스에 최적화 된 인덱스에 대 한 전체 키는 인덱스 검색을 수행 하지 않아도 됩니다. 하지만 인덱스 키의 열 순서가 지정된 경우 누락된 열 뒤에 열의 값이 나오면 검색이 발생합니다.  
  
## <a name="index-count"></a>인덱스 개수  
 메모리 최적화 테이블은 기본 키로 만들어진 인덱스를 포함하여 최대 8개의 인덱스를 가질 수 있습니다.  
  
 메모리 최적화 테이블에 만들어진 인덱스 개수는 다음 사항을 고려하세요.  
  
-   테이블을 만들 때 필요한 인덱스를 지정합니다. 테이블을 만든 후 메모리 최적화 테이블을 위한 인덱스는 만들 수 없습니다. 메모리 최적화 테이블에 인덱스를 추가하려면 해당 테이블을 삭제한 후 다시 만듭니다.  
  
-   거의 사용하지 않는 인덱스는 만들지 마세요.  
  
     가비지 컬렉션은 테이블의 모든 인덱스를 사용하는 경우 가장 잘 작동합니다. 드물게 사용되는 인덱스는 오래된 행 버전의 경우 가비지 컬렉션 시스템이 최적의 성능을 발휘하지 못하게 할 수 있습니다.  
  
## <a name="creating-a-memory-optimized-index-code-samples"></a>메모리 액세스에 최적화 된 인덱스 만들기: 코드 샘플  
 열 수준 해시 인덱스:  
  
```tsql  
CREATE TABLE t1   
   (c1 INT NOT NULL INDEX idx HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 테이블 수준 해시 인덱스:  
  
```tsql  
CREATE TABLE t1_1   
   (c1 INT NOT NULL,   
   INDEX IDX HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 열 수준 기본 키 해시 인덱스:  
  
```tsql  
CREATE TABLE t2   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 테이블 수준 기본 키 해시 인덱스:  
  
```tsql  
CREATE TABLE t2_2   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 열 수준 비클러스터형 인덱스:  
  
```tsql  
CREATE TABLE t3   
   (c1 INT NOT NULL INDEX ID)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 테이블 수준 비클러스터형 인덱스:  
  
```tsql  
CREATE TABLE t3_3   
   (c1 INT NOT NULL,   
   INDEX IDX NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 열 수준 기본 키 비클러스터형 인덱스:  
  
```tsql  
CREATE TABLE t4   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 테이블 수준 기본 키 비클러스터형 인덱스:  
  
```tsql  
CREATE TABLE t4_4   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 열이 정의된 후 정의된 다중 열 인덱스:  
  
```tsql  
create table t (  
       a int not null constraint ta primary key nonclustered,  
       b int not null,  
       c int not null,  
       d int not null,  
       index idx_t_b_c_d nonclustered (b, c asc, d desc)  
) with (memory_optimized = on, durability = SCHEMA_AND_DATA)  
go  
```  
  
## <a name="see-also"></a>관련 항목  
 [메모리 액세스에 최적화 된 테이블에 있는 인덱스](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [해시 인덱스에 대 한 올바른 버킷 수 결정](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md)   
 [해시 인덱스](hash-indexes.md)  
  
  
