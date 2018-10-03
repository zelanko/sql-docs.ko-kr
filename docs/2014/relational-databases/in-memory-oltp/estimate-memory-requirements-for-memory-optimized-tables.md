---
title: 메모리 액세스에 최적화된 테이블에 필요한 메모리 예측 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5c5cc1fc-1fdf-4562-9443-272ad9ab5ba8
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3471abb7a551de576dfdf01de2a5fcf980b60527
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061273"
---
# <a name="estimate-memory-requirements-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에 필요한 메모리 예측
  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 메모리 최적화 새 테이블을 만들든, 기존 디스크 기반 테이블을 메모리 최적화 테이블로 마이그레이션하든 간에 충분한 메모리로 서버를 프로비전할 수 있도록 각 테이블에 필요한 메모리를 적절히 예측하는 것이 중요합니다. 이 섹션에서는 메모리 최적화 테이블의 데이터를 저장하는 데 필요한 메모리 양을 예측하는 방법에 대해 설명합니다.  
  
 디스크 기반 테이블에서 메모리 최적화 테이블로 마이그레이션을 고려하는 경우 이 항목을 진행하기 전에 마이그레이션에 가장 적합한 테이블에 대한 지침에 대해 [메모리 내 OLTP에 테이블 또는 저장 프로시저를 이식해야 하는지 확인](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) 항목을 참조하세요. [메모리 내 OLTP로 마이그레이션](migrating-to-in-memory-oltp.md) 아래의 모든 항목은 디스크 기반 테이블에서 메모리 최적화 테이블로 마이그레이션하는 지침을 제공합니다.  
  
## <a name="sections-in-this-topic"></a>이 항목의 단원  
  
-   [메모리 최적화 테이블의 예](#bkmk_ExampleTable)  
  
-   [테이블에 대한 메모리](#bkmk_MemoryForTable)  
  
-   [인덱스에 대한 메모리](#bkmk_IndexMeemory)  
  
-   [행 버전 관리에 대한 메모리](#bkmk_MemoryForRowVersions)  
  
-   [테이블 변수에 대한 메모리](#bkmk_TableVariables)  
  
-   [증가에 대한 메모리](#bkmk_MemoryForGrowth)  
  
##  <a name="bkmk_ExampleTable"></a> 메모리 최적화 테이블의 예  
 다음 메모리 최적화 테이블 스키마를 살펴봅니다.  
  
```tsql  
  
CREATE TABLE t_hk (  
col1 int NOT NULL PRIMARY KEY NONCLUSTERED,  
col2 int NOT NULL INDEX t1c2_index   
     HASH WITH (bucket_count = 5000000),  
col3 int NOT NULL INDEX t1c3_index   
     HASH WITH (bucket_count = 5000000),  
col4 int NOT NULL INDEX t1c4_index   
     HASH WITH (bucket_count = 5000000),  
col5 int NOT NULL INDEX t1c5_index NONCLUSTERED,  
col6 char (50) NOT NULL,  
col7 char (50) NOT NULL,   
col8 char (30) NOT NULL,   
col9 char (50) NOT NULL  
     WITH (memory_optimized = on)  
GO  
  
```  
  
 위의 스키마를 사용하여 이 메모리 최적화 테이블에 필요한 최소 메모리를 결정할 것입니다.  
  
##  <a name="bkmk_MemoryForTable"></a> 테이블에 대한 메모리  
 메모리 최적화 테이블 행은 다음 세 부분으로 구성되어 있습니다.  
  
-   **타임스탬프**   
    행 머리글/타임스탬프 = 24바이트  
  
-   **인덱스 포인터**   
    테이블의 각 해시 인덱스의 경우, 각 행의 인덱스에는 다음 행에 대한 8바이트 주소 포인터가 있습니다.  인덱스가 4개 있으므로 각 행에 인덱스 포인터에 대한 32바이트가 할당됩니다(인덱스당 8바이트 포인터).  
  
-   **데이터**   
    행의 데이터 부분 크기는 각 데이터 열의 형식 크기를 합하여 결정됩니다.  예제 테이블에는 4바이트 정수 5개, 50바이트 문자 열 3개, 30바이트 문자 열 1개가 있습니다.  따라서 각 행의 데이터 부분은 4 + 4 + 4 + 4 + 4 + 50 + 50 + 50 + 30 또는 200바이트입니다.  
  
 다음은 메모리 최적화 테이블에 있는 5,000,000(5백만)개 행에 대한 크기 계산입니다. 데이터 행에서 사용하는 총 메모리는 다음과 같이 예상됩니다.  
  
 **테이블의 행에 대 한 메모리**  
  
 위의 계산에서 메모리 최적화 테이블의 각 행 크기는 24 + 32 + 200 또는 256바이트입니다.  행이 5백만 개이므로 테이블은 5,000,000 * 256바이트 또는 1,280,000,000바이트, 즉 1.28GB 정도를 사용합니다.  
  
##  <a name="bkmk_IndexMeemory"></a> 인덱스에 대한 메모리  
 **각 해시 인덱스에 대 한 메모리**  
  
 각 해시 인덱스는 8바이트 주소 포인터의 해시 배열입니다.  배열의 크기는 해당 인덱스에 대한 고유한 인덱스 값의 수에 따라 최적으로 결정됩니다. 예를 들어 고유한 Col2 값의 수는 t1c2_index의 배열 크기를 계산하기 위한 좋은 출발점입니다. 해시 배열이 너무 크면 메모리가 낭비되고,  해시 배열이 너무 작으면 동일한 인덱스로 해시되는 인덱스 값에 의한 충돌이 너무 많이 발생하므로 성능이 저하됩니다.  
  
 해시 인덱스는 같은지 여부를 확인하는 다음과 같은 조회를 매우 빠르게 수행합니다.  
  
```tsql  
  
SELECT * FROM t_hk  
   WHERE Col2 = 3  
  
```  
  
 비클러스터형 인덱스는 다음과 같은 범위 조회의 경우 더욱 빠릅니다.  
  
```tsql  
  
SELECT * FROM t_hk  
   WHERE Col2 >= 3  
  
```  
  
 디스크 기반 테이블을 마이그레이션하는 경우 다음을 사용하여 t1c2_index 인덱스에 대한 고유 값의 수를 확인할 수 있습니다.  
  
```tsql  
  
SELECT COUNT(DISTINCT [Col2])  
  FROM t_hk  
  
```  
  
 새 테이블을 만드는 경우 배열 크기를 예측하거나 배포 전에 테스트에서 데이터를 수집해야 합니다.  
  
 해시 인덱스가 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 메모리 최적화 테이블에서 작동하는 방식에 대한 자세한 내용은 [해시 인덱스](../../database-engine/hash-indexes.md)를 참조하세요.  
  
 **참고:** 즉석에서 해시 인덱스 배열 크기를 변경할 수 없습니다. 해시 인덱스 배열 크기를 변경하려면 테이블을 삭제하고 bucket_count 값을 변경한 다음 테이블을 다시 만들어야 합니다.  
  
 **해시 인덱스 배열 크기를 설정합니다.**  
  
 해시 배열 크기는 설정한 `(bucket_count= <value>)` 여기서 \<값 > 정수 값을 0 보다 큽니다. 경우 \<값 >은 제곱이 아니므로 2 인 실제 bucket_count는 가장 가까운 다음 2의 제곱으로 반올림 됩니다.  예제 테이블, (bucket_count = 5000000)에서 5,000,000은 2의 제곱이 아니므로 실제 버킷 수 반올림 8388608 (2<sup>23</sup>).  해시 배열에 필요한 메모리를 계산할 때는 5,000,000이 아니라 이 수를 사용해야 합니다.  
  
 따라서 이 예제에서 각 해시 배열에 필요한 메모리는 다음과 같습니다.  
  
 8,388,608 * 8 = 2<sup>23</sup> \* 8 = 2<sup>23</sup> \* 2<sup>3</sup> = 2<sup>26</sup> = 67,108,864 또는 약 64MB.  
  
 해시 인덱스가 3개 있으므로 해시 인덱스에 필요한 메모리는 3 * 64MB = 192MB입니다.  
  
 **비클러스터형 인덱스에 대 한 메모리**  
  
 비클러스터형 인덱스는 인덱스 값과 이후 노드에 대한 포인터가 포함된 내부 노드가 있는 BTrees로 구현됩니다.  리프 노드에는 인덱스 값과 메모리의 테이블 행에 대한 포인터가 포함됩니다.  
  
 해시 인덱스와 달리 비클러스터형 인덱스에는 고정된 버킷 크기가 없습니다. 인덱스는 데이터와 함께 동적으로 증가하고 감소합니다.  
  
 비클러스터형 인덱스에 필요한 메모리는 다음과 같이 계산할 수 있습니다.  
  
-   **리프가 아닌 노드에 할당된 메모리**   
    일반적인 구성에서 리프가 아닌 노드에 할당된 메모리는 인덱스에 사용되는 전체 메모리의 작은 비율을 차지합니다. 이 비율은 매우 작으므로 무시해도 괜찮습니다.  
  
-   **리프 노드에 대한 메모리**   
    리프 노드에는 테이블의 고유 키마다 행이 하나씩 있으며 이 행은 해당 고유 키가 있는 데이터 행을 가리킵니다.  동일한 키가 있는 행이 여러 개인 경우(즉, 고유하지 않은 비클러스터형 인덱스가 있는 경우), 인덱스 리프 노드에는 행이 하나만 있으며 이 행은 다른 행과 서로 연결된 행 중 하나를 가리킵니다.  따라서 필요한 총 메모리는 대략적으로 다음과 같이 계산될 수 있습니다.   
    memoryForNonClusteredIndex = (pointerSize + sum(keyColumnDataTypeSizes)) * rowsWithUniqueKeys  
  
 비클러스터형 인덱스는 다음 쿼리로 예시된 범위 조회에 사용될 때 가장 효과적입니다.  
  
```tsql  
  
SELECT * FROM t_hk  
   WHERE c2 > 5  
```  
  
##  <a name="bkmk_MemoryForRowVersions"></a> 행 버전 관리에 대한 메모리  
 잠금을 방지하기 위해 메모리 내 OLTP는 행을 업데이트하거나 삭제할 때 낙관적 동시성을 사용합니다. 즉, 행이 업데이트될 때 행의 추가 버전이 만들어집니다. 시스템은 이전 버전을 사용할 수도 있는 모든 트랜잭션의 실행이 완료될 때까지 해당 버전을 사용 가능한 상태로 유지합니다. 행이 삭제될 때 시스템은 업데이트와 유사한 방식으로 작동하며 버전이 더 이상 필요하지 않을 때까지 버전을 사용 가능한 상태로 유지합니다. 읽을 때와 삽입할 때는 행의 추가 버전이 만들어지지 않습니다.  
  
 언제든지 가비지 수집 주기에 따라 메모리가 해제되기를 기다리는 많은 추가 행이 메모리에 있을 수 있기 때문에 이러한 추가 행을 수용하는 데 충분한 메모리가 있어야 합니다.  
  
 추가 행 수는 행 업데이트 및 삭제의 초당 최대 수를 계산한 다음 가장 긴 트랜잭션에 소요되는 초 단위 시간(최소값 1)과 곱하여 예측할 수 있습니다.  
  
 그런 다음 이 값을 행 크기와 곱하면 행 버전 관리에 필요한 바이트 수를 얻을 수 있습니다.  
  
 `rowVersions = durationOfLongestTransactionInSeconds * peakNumberOfRowUpdatesOrDeletesPerSecond`  
  
 유효 하지 않은 행에 필요한 메모리는 메모리 최적화 테이블 행의 크기에 따라 유효 하지 않은 행의 수를 곱하여 예측 됩니다 (참조 [테이블에 대 한 메모리](#bkmk_MemoryForTable) 위에).  
  
 `memoryForRowVersions = rowVersions * rowSize`  
  
##  <a name="bkmk_TableVariables"></a> 테이블 변수에 대한 메모리  
 테이블 변수에 사용되는 메모리는 테이블 변수가 범위를 벗어날 때만 해제됩니다. 업데이트의 일부로 삭제된 행을 포함하여 테이블 변수에서 삭제된 행은 가비지 수집의 대상이 아닙니다. 테이블 변수가 범위를 벗어날 때까지는 메모리가 해제되지 않습니다.  
  
 프로시저 범위와 반대로 많은 트랜잭션에서 사용되는 큰 SQL 일괄 처리에서 정의된 테이블 변수는 다량의 메모리를 사용할 수 있습니다. 테이블 변수는 가비지 수집되지 않기 때문에 테이블 변수의 삭제된 행은 다량의 메모리를 사용할 수 있으며 읽기 작업이 삭제된 행을 통과하여 검색해야 하므로 성능이 저하될 수 있습니다.  
  
##  <a name="bkmk_MemoryForGrowth"></a> 증가에 대한 메모리  
 위의 계산에서는 현재 상태의 테이블에 필요한 메모리를 예측합니다. 이 메모리 외에도 테이블의 증가를 예측하고 이러한 증가를 수용하는 데 충분한 메모리를 제공해야 합니다.  예를 들어 10% 증가를 예상하는 경우 위의 결과에 1.1을 곱하여 테이블에 필요한 총 메모리를 얻어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP로 마이그레이션](migrating-to-in-memory-oltp.md)  
  
  
