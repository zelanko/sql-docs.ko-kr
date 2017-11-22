---
title: "메모리 액세스에 최적화된 테이블에 필요한 메모리 예측 | Microsoft 문서"
ms.custom: 
ms.date: 12/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5c5cc1fc-1fdf-4562-9443-272ad9ab5ba8
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f8eb8029f9824ceaeee061fc829a89d0054e1244
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="estimate-memory-requirements-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에 필요한 메모리 예측
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

메모리 액세스에 최적화된 테이블을 사용하려면 모든 행과 인덱스를 메모리 내에 유지하는 데 충분한 메모리가 있어야 합니다. 메모리는 한정된 리소스이므로 시스템에서 메모리 사용량을 파악하고 관리해야 합니다. 이 섹션의 항목에서는 일반적인 메모리 사용 및 관리 시나리오를 다룹니다.

새로운 메모리 최적화 테이블을 만들든, 아니면 기존 디스크 기반 테이블을 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 메모리 최적화 테이블로 마이그레이션하든 간에 충분한 메모리로 서버를 프로비전할 수 있도록 각 테이블에 필요한 메모리를 적절히 예측하는 것이 중요합니다. 이 섹션에서는 메모리 최적화 테이블의 데이터를 저장하는 데 필요한 메모리 양을 예측하는 방법에 대해 설명합니다.  
  
디스크 기반 테이블에서 메모리 최적화 테이블로 마이그레이션을 고려하는 경우 이 항목을 진행하기 전에 마이그레이션에 가장 적합한 테이블에 대한 지침에 대해 [메모리 내 OLTP에 테이블 또는 저장 프로시저를 이식해야 하는지 확인](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) 항목을 참조하세요. 
            [메모리 내 OLTP로 마이그레이션](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md) 아래의 모든 항목은 디스크 기반 테이블에서 메모리 최적화 테이블로 마이그레이션하는 지침을 제공합니다. 
  
## <a name="basic-guidance-for-estimating-memory-requirements"></a>메모리 요구 사항을 예측하기 위한 기본 지침

테이블이 메모리에 적합해야 하지만 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 메모리 최적화 테이블의 크기에 제한이 없습니다.  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에서 SCHEMA_AND_DATA 테이블의 경우 지원되는 데이터 크기는 256GB입니다.

메모리 최적화 테이블의 크기는 데이터 크기에 행 머리글에 대한 약간의 오버헤드를 더한 것에 해당합니다. 디스크 기반 테이블을 메모리 최적화되도록 마이그레이션하는 경우 메모리 최적화 테이블의 크기는 대략 원래 디스크 기반 테이블의 힙 또는 클러스터형 인덱스 크기에 해당합니다.

메모리 최적화 테이블의 인덱스는 디스크 기반 테이블의 비클러스터형 인덱스보다 작은 경우가 많습니다. 비클러스터형 인덱스의 크기는 `[primary key size] * [row count]`순입니다. 해시 인덱스의 크기는 `[bucket count] * 8 bytes`입니다. 

활성 워크로드가 있는 경우 행 버전 관리 및 다양한 작업을 위해 추가 메모리를 고려해야 합니다. 실제로 필요한 메모리 양은 워크로드에 따라 다르지만 안전을 위해 메모리 최적화 테이블 및 인덱스의 예상 크기의 두 배로 시작하여 실제 필요한 메모리 요구 사항을 관측하는 것이 좋습니다. 행 버전 관리에 대한 오버헤드는 항상 워크로드의 특징에 따라 다릅니다. 특히 장기 실행 트랜잭션에서는 오버헤드가 증가합니다. 더 큰 데이터베이스를 사용하는 대부분의 워크로드(예: 100GB 초과)의 경우 오버헤드가 제한됩니다(25% 이하).

  
## <a name="detailed-computation-of-memory-requirements"></a>메모리 요구 사항의 상세 계산 
  
- 
            [메모리 최적화 테이블의 예](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_ExampleTable)  
  
- [테이블에 대한 메모리](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForTable)  
  
- [인덱스에 대한 메모리](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_IndexMeemory)  
  
- [행 버전 관리에 대한 메모리](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForRowVersions)  
  
- [테이블 변수에 대한 메모리](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_TableVariables)  
  
- [증가에 대한 메모리](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForGrowth)  
  
###  
            <a name="bkmk_ExampleTable">
            </a> 메모리 최적화 테이블의 예  

다음 메모리 최적화 테이블 스키마를 살펴봅니다.
  
```tsql  
CREATE TABLE t_hk
(  
  col1 int NOT NULL  PRIMARY KEY NONCLUSTERED,  

  col2 int NOT NULL  INDEX t1c2_index   
      HASH WITH (bucket_count = 5000000),  

  col3 int NOT NULL  INDEX t1c3_index   
      HASH WITH (bucket_count = 5000000),  

  col4 int NOT NULL  INDEX t1c4_index   
      HASH WITH (bucket_count = 5000000),  

  col5 int NOT NULL  INDEX t1c5_index NONCLUSTERED,  

  col6 char (50) NOT NULL,  
  col7 char (50) NOT NULL,   
  col8 char (30) NOT NULL,   
  col9 char (50) NOT NULL  

  WITH (memory_optimized = on)  
);
GO  
```  

위의 스키마를 사용하여 이 메모리 최적화 테이블에 필요한 최소 메모리를 결정할 것입니다.  
  
###  <a name="bkmk_MemoryForTable"></a> 테이블에 대한 메모리  

메모리 최적화 테이블 행은 다음 세 부분으로 구성되어 있습니다.
  
- **타임스탬프**   
    행 머리글/타임스탬프 = 24바이트  
  
- **인덱스 포인터**   
    테이블의 각 해시 인덱스의 경우, 각 행의 인덱스에는 다음 행에 대한 8바이트 주소 포인터가 있습니다.  인덱스가 4개 있으므로 각 행에 인덱스 포인터에 대한 32바이트가 할당됩니다(인덱스당 8바이트 포인터).  
  
- **데이터**   
    행의 데이터 부분 크기는 각 데이터 열의 형식 크기를 합하여 결정됩니다.  예제 테이블에는 4바이트 정수 5개, 50바이트 문자 열 3개, 30바이트 문자 열 1개가 있습니다.  따라서 각 행의 데이터 부분은 4 + 4 + 4 + 4 + 4 + 50 + 50 + 50 + 30 또는 200바이트입니다.  
  
다음은 메모리 최적화 테이블에 있는 5,000,000(5백만)개 행에 대한 크기 계산입니다. 데이터 행에서 사용하는 총 메모리는 다음과 같이 예상됩니다.  
  
#### <a name="memory-for-the-tables-rows"></a>테이블의 행에 대한 메모리  
  
위의 계산에서 메모리 최적화 테이블의 각 행 크기는 24 + 32 + 200 또는 256바이트입니다.  행이 5백만 개이므로 테이블은 5,000,000 * 256바이트 또는 1,280,000,000바이트, 즉 1.28GB 정도를 사용합니다.  
  
###  <a name="bkmk_IndexMeemory"></a> 인덱스에 대한 메모리  

#### <a name="memory-for-each-hash-index"></a>각 해시 인덱스에 대한 메모리  
  
각 해시 인덱스는 8바이트 주소 포인터의 해시 배열입니다.  배열의 크기는 해당 인덱스에 대한 고유한 인덱스 값의 수에 따라 최적으로 결정됩니다. 예를 들어 고유한 Col2 값의 수는 t1c2_index의 배열 크기를 계산하기 위한 좋은 출발점입니다. 해시 배열이 너무 크면 메모리가 낭비되고,  해시 배열이 너무 작으면 동일한 인덱스로 해시되는 인덱스 값에 의한 충돌이 너무 많이 발생하므로 성능이 저하됩니다.  
  
해시 인덱스는 같은지 여부를 확인하는 다음과 같은 조회를 매우 빠르게 수행합니다.  
  
```tsql  
SELECT * FROM t_hk  
   WHERE Col2 = 3;
```  
  
비클러스터형 인덱스는 다음과 같은 범위 조회의 경우 더욱 빠릅니다.  
  
```tsql  
SELECT * FROM t_hk  
   WHERE Col2 >= 3;
```  
  
디스크 기반 테이블을 마이그레이션하는 경우 다음을 사용하여 t1c2_index 인덱스에 대한 고유 값의 수를 확인할 수 있습니다.  
  
```tsql
SELECT COUNT(DISTINCT [Col2])  
  FROM t_hk;
```  
  
새 테이블을 만드는 경우 배열 크기를 예측하거나 배포 전에 테스트에서 데이터를 수집해야 합니다.  
  
해시 인덱스가 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 메모리 최적화 테이블에서 작동하는 방식에 대한 자세한 내용은 [해시 인덱스](http://msdn.microsoft.com/library/f4bdc9c1-7922-4fac-8183-d11ec58fec4e)를 참조하세요.  
  
#### <a name="setting-the-hash-index-array-size"></a>해시 인덱스 배열 크기 설정  
  
해시 배열 크기는 `(bucket_count= value)` 에 의해 설정됩니다. 여기서 `value` 는 0보다 큰 정수 값입니다. `value` 가 2의 제곱이 아니면 실제 bucket_count는 가장 가까운 다음 2의 제곱으로 반올림됩니다.  예제 테이블, (bucket_count = 5000000)에서 5,000,000은 2의 제곱이 아니므로 실제 버킷 수는 8,388,608(2^23)로 반올림됩니다.  해시 배열에 필요한 메모리를 계산할 때는 5,000,000이 아니라 이 수를 사용해야 합니다.  
  
따라서 이 예제에서 각 해시 배열에 필요한 메모리는 다음과 같습니다.  
  
8,388,608 * 8 = 2^23 \* 8 = 2^23 \* 2^3 = 2^26 = 67,108,864 or approximately 64 MB.  
  
해시 인덱스가 3개 있으므로 해시 인덱스에 필요한 메모리는 3 * 64MB = 192MB입니다.  
  
#### <a name="memory-for-non-clustered-indexes"></a>비클러스터형 인덱스에 대한 메모리  
  
비클러스터형 인덱스는 인덱스 값과 이후 노드에 대한 포인터가 포함된 내부 노드가 있는 BTrees로 구현됩니다.  리프 노드에는 인덱스 값과 메모리의 테이블 행에 대한 포인터가 포함됩니다.  
  
해시 인덱스와 달리 비클러스터형 인덱스에는 고정된 버킷 크기가 없습니다. 인덱스는 데이터와 함께 동적으로 증가하고 감소합니다.  
  
비클러스터형 인덱스에 필요한 메모리는 다음과 같이 계산할 수 있습니다.  
  
- **리프가 아닌 노드에 할당된 메모리**   
    일반적인 구성에서 리프가 아닌 노드에 할당된 메모리는 인덱스에 사용되는 전체 메모리의 작은 비율을 차지합니다. 이 비율은 매우 작으므로 무시해도 괜찮습니다.  
  
- **리프 노드에 대한 메모리**   
    리프 노드에는 테이블의 고유 키마다 행이 하나씩 있으며 이 행은 해당 고유 키가 있는 데이터 행을 가리킵니다.  동일한 키가 있는 행이 여러 개인 경우(즉, 고유하지 않은 비클러스터형 인덱스가 있는 경우), 인덱스 리프 노드에는 행이 하나만 있으며 이 행은 다른 행과 서로 연결된 행 중 하나를 가리킵니다.  따라서 필요한 총 메모리는 대략적으로 다음과 같이 계산될 수 있습니다.
  - memoryForNonClusteredIndex = (pointerSize + sum(keyColumnDataTypeSizes)) * rowsWithUniqueKeys  
  
 비클러스터형 인덱스는 다음 쿼리로 예시된 범위 조회에 사용될 때 가장 효과적입니다.  
  
```tsql  
SELECT * FRON t_hk  
   WHERE c2 > 5;  
```  
  
###  <a name="bkmk_MemoryForRowVersions"></a> 행 버전 관리에 대한 메모리

잠금을 방지하기 위해 메모리 내 OLTP는 행을 업데이트하거나 삭제할 때 낙관적 동시성을 사용합니다. 즉, 행이 업데이트될 때 행의 추가 버전이 만들어집니다. 또한 삭제가 논리적으로 수행되어 기존 행이 삭제된 상태로 표시되지만 바로 제거되지는 않습니다. 시스템에서는 해당 버전을 사용할 수 있는 모든 트랜잭션 실행이 완료될 때까지 이전 행 버전(삭제된 행 포함)을 사용할 수 있는 상태로 보관합니다. 
  
언제든지 가비지 수집 주기에 따라 메모리가 해제되기를 기다리는 많은 추가 행이 메모리에 있을 수 있기 때문에 이러한 추가 행을 수용하는 데 충분한 메모리가 있어야 합니다.  
  
추가 행 수는 행 업데이트 및 삭제의 초당 최대 수를 계산한 다음 가장 긴 트랜잭션에 소요되는 초 단위 시간(최소값 1)과 곱하여 예측할 수 있습니다.  
  
그런 다음 이 값을 행 크기와 곱하면 행 버전 관리에 필요한 바이트 수를 얻을 수 있습니다.  
  
`rowVersions = durationOfLongestTransctoinInSeconds * peakNumberOfRowUpdatesOrDeletesPerSecond`  
  
유효하지 않은 행에 필요한 메모리는 유효하지 않은 행 수와 메모리 최적화 테이블 행의 크기(위의 [테이블에 대한 메모리](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForTable) 참조)를 곱하여 예측됩니다.  
  
`memoryForRowVersions = rowVersions * rowSize`  
  
###  <a name="bkmk_TableVariables"></a> 테이블 변수에 대한 메모리
  
테이블 변수에 사용되는 메모리는 테이블 변수가 범위를 벗어날 때만 해제됩니다. 업데이트의 일부로 삭제된 행을 포함하여 테이블 변수에서 삭제된 행은 가비지 수집의 대상이 아닙니다. 테이블 변수가 범위를 벗어날 때까지는 메모리가 해제되지 않습니다.  
  
프로시저 범위와 반대로 많은 트랜잭션에서 사용되는 큰 SQL 일괄 처리에서 정의된 테이블 변수는 다량의 메모리를 사용할 수 있습니다. 테이블 변수는 가비지 수집되지 않기 때문에 테이블 변수의 삭제된 행은 다량의 메모리를 사용할 수 있으며 읽기 작업이 삭제된 행을 통과하여 검색해야 하므로 성능이 저하될 수 있습니다.  
  
###  <a name="bkmk_MemoryForGrowth"></a> 증가에 대한 메모리

위의 계산에서는 현재 상태의 테이블에 필요한 메모리를 예측합니다. 이 메모리 외에도 테이블의 증가를 예측하고 이러한 증가를 수용하는 데 충분한 메모리를 제공해야 합니다.  예를 들어 10% 증가를 예상하는 경우 위의 결과에 1.1을 곱하여 테이블에 필요한 총 메모리를 얻어야 합니다.  
  
## <a name="see-also"></a>관련 항목:

[메모리 내 OLTP로 마이그레이션](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  

