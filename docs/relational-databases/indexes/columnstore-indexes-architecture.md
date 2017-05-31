---
title: "Columnstore 인덱스 - 아키텍처 | Microsoft 문서"
ms.custom: 
ms.date: 01/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 96b8e884-8244-425f-b856-72a8ff6895a6
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 835e3acd76972eef01b4d286cbc1f6ecf6fac605
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="columnstore-indexes---architecture"></a>Columnstore 인덱스 - 아키텍처
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Columnstore 인덱스의 설계 방식을 알아봅니다. 이러한 기본 사항을 알면 효과적인 사용 방법을 설명하는 다른 columnstore 문서를 더 쉽게 이해할 수 있습니다.

## <a name="data-storage-uses-columnstore-and-rowstore-compression"></a>데이터 저장소는 columnstore 및 rowstore 압축을 사용함
Columnstore 인덱스에 대한 설명에서는 데이터 저장소에 대한 형식을 강조하기 위해 *rowstore* 및 *columnstore* 라는 용어를 사용합니다.  Columnstore 인덱스는 두 가지 유형의 저장소를 사용합니다.

 ![Clustered Columnstore Index](../../relational-databases/indexes/media/sql-server-pdw-columnstore-physicalstorage.gif "Clustered Columnstore Index")

- **columnstore** 는 열과 행이 있는 테이블로 논리적으로 구성되고 열 데이터 형식으로 물리적으로 저장되는 데이터입니다.
  
columnstore 인덱스는 물리적으로 대부분의 데이터를 columnstore 형식으로 저장합니다. columnstore 형식에서는 데이터가 열로 압축되고 압축 해제됩니다. 쿼리에서 요청되지 않은 다른 값은 각 행에 압축을 풀지 않아도 됩니다. 이렇게 하면 큰 테이블의 전체 열을 빠르게 검색할 수 있습니다. 

- **rowstore** 는 열과 행이 있는 테이블로 논리적으로 구성되고 행 데이터 형식으로 물리적으로 저장되는 데이터입니다. 이는 힙 또는 클러스터형 "btree" 인덱스와 같은 관계형 테이블 데이터를 저장하는 기존 방법이었습니다.

또한 columnstore 인덱스는 물리적으로 일부 행을 deltastore라는 rowstore 형식으로 저장합니다. 델타 행 그룹이라고도 하는 deltastore는 개수가 너무 적어서 columnstore로 압축할 수 없는 행을 보관하는 장소입니다. 각 델타 행 그룹은 클러스터형 btree 인덱스로 구현됩니다. 

- **deltastore**는 개수가 너무 적어서 columnstore로 압축할 수 없는 행을 보관하는 장소입니다. deltastore는 rowstore입니다. 
  
## <a name="operations-are-performed-on-rowgroups-and-column-segments"></a>행 그룹 및 열 세그먼트에서 작업이 수행됨

columnstore 인덱스는 행을 관리할 수 있는 단위로 그룹화합니다. 이러한 각 단위를 행 그룹이라고 합니다. 성능을 최적화하려면 행 그룹의 행 수가 압축률을 높일 만큼 크고, 메모리 내 작업을 활용할 만큼 작아야 합니다.

* **행 그룹**은 columnstore 인덱스가 관리 및 압축 작업을 수행하는 행 그룹입니다. 

예를 들어 columnstore 인덱스는 행 그룹에서 다음 작업을 수행합니다.

* 행 그룹을 columnstore로 압축합니다. 압축은 행 그룹 내의 각 열 세그먼트에서 수행됩니다.
* ALTER INDEX REORGANIZE 작업 중에 행 그룹을 병합합니다.
* ALTER INDEX REBUILD 작업 중에 새 행 그룹을 만듭니다.
* DMV(동적 관리 뷰)에서 행 그룹 상태 및 조각화를 보고합니다.

deltastore는 델타 행 그룹이라는 하나 이상의 행 그룹으로 구성됩니다. 각 델타 행 그룹은 개수가 너무 적어서 columnstore로 압축할 수 없는 경우 행을 저장하는 클러스터형 btree 인덱스입니다.  

* **델타 행 그룹**은 행 그룹에 1,048,576개의 행이 포함되거나 인덱스가 다시 작성될 때까지 작은 대량 로드 및 삽입을 저장하는 클러스터형 btree 인덱스입니다.  델타 행 그룹에 1,048,576개의 행이 포함된 경우 닫힘으로 표시되고 tuple-mover라는 프로세스가 columnstore로 압축할 때까지 기다립니다. 


행 그룹마다 각 열의 일부 값이 있습니다. 이러한 값을 열 세그먼트라고 합니다. columnstore 인덱스는 행 그룹을 압축할 때 각 열 세그먼트를 개별적으로 압축합니다. 전체 열의 압축을 풀려면 columnstore 인덱스가 각 행 그룹에서 하나의 열 세그먼트 압축만 풀면 됩니다.

* **열 세그먼트**는 행 그룹에 포함된 열 값의 일부입니다. 각 행 그룹에는 테이블의 모든 열에 대해 각각 하나의 열 세그먼트가 포함됩니다. 행 그룹마다 각 열의 열 세그먼트 하나가 있습니다.| 
  
 ![Column segment](../../relational-databases/indexes/media/sql-server-pdw-columnstore-columnsegment.gif "Column segment")  
 
## <a name="small-loads-and-inserts-go-to-the-deltastore"></a>작은 로드 및 삽입은 deltastore로 이동함
columnstore 인덱스는 한 번에 102,400개 이상의 행을 columnstore 인덱스로 압축하여 columnstore 압축 및 성능을 향상합니다. 행을 대량으로 압축하기 위해 columnstore 인덱스는 작은 로드 및 삽입을 deltastore에 누적합니다. deltastore 작업은 백그라운드에서 처리됩니다. 정확한 쿼리 결과를 반환하기 위해 클러스터형 columnstore 인덱스는 columnstore와 deltastore의 쿼리 결과를 모두 결합합니다. 

다음과 같은 경우 행이 deltastore로 이동함
* INSERT INTO VALUES 문을 사용하여 삽입된 경우
* 대량 로드가 끝나고 개수가 102,400개보다 적은 경우
* 업데이트된 경우. 각 업데이트는 삭제와 삽입으로 구현됩니다.

deltastore는 삭제된 것으로 표시되었지만 columnstore에서 물리적으로 삭제되지 않은 삭제된 행의 ID 목록도 저장합니다. 

## <a name="when-delta-rowgroups-are-full-they-get-compressed-into-the-columnstore"></a>델타 행 그룹이 꽉 차면 columnstore로 압축됨

클러스터형 columnstore 인덱스는 행 그룹을 columnstore로 압축하기 전에 각 델타 행 그룹에 최대 1,048,576개의 행을 수집합니다. 이를 통해 columnstore 인덱스의 압축이 개선됩니다. 델타 행 그룹에 1,048,576개의 행이 포함되면 columnstore 인덱스가 행 그룹을 닫힘으로 표시합니다. *tuple-mover*라는 백그라운드 프로세스가 각 닫힌 행 그룹을 발견하고 columnstore로 압축합니다. 

[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)를 사용하여 인덱스를 다시 작성하거나 다시 구성하면 델타 행 그룹을 columnstore로 강제로 보낼 수 있습니다.  압축하는 동안 메모리 압력이 있을 경우 columnstore 인덱스가 압축된 행 그룹의 행 수를 줄일 수도 있습니다.

## <a name="each-table-partition-has-its-own-rowgroups-and-delta-rowgroups"></a>각 테이블 파티션에 고유한 행 그룹과 델타 행 그룹이 있음

분할 개념은 클러스터형 인덱스, 힙, columnstore 인덱스에서 모두 동일합니다. 테이블을 분할하면 열 값의 범위에 따라 테이블이 더 작은 행 그룹으로 나뉩니다. 데이터 관리를 위해 자주 사용됩니다. 예를 들어 각 연도의 데이터에 대한 파티션을 만들고 파티션 전환을 사용하여 더 저렴한 저장소에 데이터를 보관할 수 있습니다. 파티션 전환은 columnstore 인덱스에서 수행되며 데이터 파티션을 다른 위치로 쉽게 이동할 수 있게 합니다.

행 그룹은 항상 테이블 파티션 내에서 정의됩니다. columnstore 인덱스를 분할하는 경우 각 파티션에 압축된 행 그룹과 델타 행 그룹이 있습니다.

### <a name="each-partition-can-have-multiple-delta-rowgroups"></a>각 파티션에 델타 행 그룹이 여러 개 있을 수 있습니다.
각 파티션에 델타 행 그룹이 둘 이상 포함될 수 있습니다. columnstore 인덱스가 델타 행 그룹에 데이터를 추가해야 하고 델타 행 그룹이 잠겨 있는 경우 columnstore 인덱스는 다른 델타 행 그룹에 대한 잠금을 획득하려고 합니다. 사용할 수 있는 델타 행 그룹이 없으면 columnstore 인덱스에서 새 델타 행 그룹을 만듭니다.  예를 들어 10개의 파티션이 있는 테이블에 20개 이상의 델타 행 그룹이 쉽게 포함될 수 있습니다. 

  
## <a name="you-can-combine-columnstore-and-rowstore-indexes-on-the-same-table"></a>동일한 테이블에서 columnstore 및 rowstore 인덱스를 결합할 수 있습니다.
비클러스터형 인덱스는 기본 테이블에 있는 행과 열의 전체 또는 일부에 대한 복사본을 포함합니다. 이 인덱스는 테이블의 하나 이상의 열로 정의되며 행을 필터링하는 선택적 조건이 있습니다. 

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 rowstore 테이블에서 업데이트 가능한 비클러스터형 columnstore 인덱스를 만들 수 있습니다. columnstore 인덱스는 데이터 복사본을 저장하므로 추가 저장소가 필요합니다. 그러나 columnstore 인덱스의 데이터는 rowstore 테이블보다 작은 크기로 압축됩니다.  따라서 columnstore 인덱스에서 분석을 실행하고 이와 동시에 rowstore 인덱스에서 트랜잭션을 실행할 수 있습니다. rowstore 테이블의 데이터가 변경되면 columnstore가 업데이트되므로 두 인덱스 모두 동일한 데이터에 대해 작동합니다.  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 하나의 클러스터형 columnstore 인덱스에서 하나 이상의 비클러스터형 rowstore 인덱스를 사용할 수 있습니다. 따라서 기본 columnstore에서 효율적인 테이블 찾기를 수행할 수 있습니다. 다른 옵션도 사용할 수 있습니다. 예를 들어 rowstore 테이블에서 UNIQUE 제약 조건을 사용하여 기본 키 제약 조건을 적용할 수 있습니다. 고유하지 않은 값은 rowstore 테이블에 삽입하지 못하므로 SQL Server에서 columnstore에 값을 삽입할 수 없습니다.  
 

## <a name="metadata"></a>메타데이터  
이러한 메타데이터 뷰를 사용하여 columnstore 인덱스의 특성을 확인할 수 있습니다. 자세한 아키텍처 정보는 이러한 뷰 중 일부에 포함됩니다.

columnstore 인덱스에 있는 모든 열이 메타데이터에 포괄 열로 저장됩니다. columnstore 인덱스에는 키 열이 없습니다.  
  
-   [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
-   [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
-   [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
  
-   [sys.internal_partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)  
  
-   [sys.column_store_segments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
-   [sys.column_store_dictionaries&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
-   [sys.column_store_row_groups&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_operational_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)  
  
-   [sys.dm_column_store_object_pool&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_operational_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_operational_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
|  


## <a name="next-steps"></a>다음 단계
 columnstore 인덱스를 디자인하는 방법에 대한 지침은 [Columnstore 인덱스 - 디자인 지침](../../relational-databases/indexes/columnstore-indexes-design-guidance.md)을 참조하세요.

