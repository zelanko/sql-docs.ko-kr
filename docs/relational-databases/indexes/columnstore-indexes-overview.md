---
title: Columnstore 인덱스 - 개요 | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- indexes creation, columnstore
- indexes [SQL Server], columnstore
- columnstore index
- columnstore index, described
- xVelocity, columnstore indexes
ms.assetid: f98af4a5-4523-43b1-be8d-1b03c3217839
caps.latest.revision: 80
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: df76c7156e506fa9e01763e8f12ba1873c943f0e
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2018
---
# <a name="columnstore-indexes---overview"></a>Columnstore 인덱스 - 개요
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

*Columnstore 인덱스*는 대규모 데이터 웨어하우징 팩트 테이블을 저장하고 쿼리하는 표준입니다. 열 기반 데이터 저장소 및 쿼리 처리를 사용하여 데이터 웨어하우스에서 기존 행 기반 저장소보다 최대 **10배 높은 쿼리 성능** 을 실현하고 압축되지 않은 데이터 크기보다 최대 **10배 높은 데이터 압축** 을 실현합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 columnstore 인덱스는 트랜잭션 워크로드에 대해 고성능 실시간 분석을 실행하는 기능인 운영 분석을 지원합니다.  
  
 다음 시나리오로 이동:  
  
-   [데이터 웨어하우스용 Columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
-   [Get started with Columnstore for real time operational analytics(실시간 운영 분석을 위한 Columnstore 시작)](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
  
## <a name="what-is-a-columnstore-index"></a>columnstore 인덱스란?  
 *columnstore index* 는 columnstore라는 칼럼 데이터 형식을 사용하여 데이터를 저장, 검색 및 관리하는 기술입니다.  
  
### <a name="key-terms-and-concepts"></a>주요 용어 및 개념  
 다음은 columnstore 인덱스와 관련된 주요 용어와 개념입니다.  
  
 columnstore  
 *columnstore* 는 열과 행이 있는 테이블로 논리적으로 구성되고 열 데이터 형식으로 물리적으로 저장되는 데이터입니다.  
  
 rowstore  
 *rowstore* 는 열과 행이 있는 테이블로 논리적으로 구성되고 행 데이터 형식으로 물리적으로 저장되는 데이터입니다. 이 방식은 관계형 테이블 데이터를 저장하는 전통적인 방법이었습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 rowstore는 기본 데이터 저장소 형식이 힙, 클러스터형 인덱스인 테이블 또는 메모리 최적화 테이블을 참조합니다.  
  
> [!NOTE]  
> Columnstore 인덱스에 대한 설명에서는 데이터 저장소에 대한 형식을 강조하기 위해 *rowstore* 및 *columnstore* 라는 용어를 사용합니다.  
  
 행 그룹  
 *행 그룹* 은 columnstore 형식으로 동시에 압축되는 행의 그룹입니다. 열 그룹에는 대개 1,048,576개(행 그룹당 최대 행 수)의 행이 포함됩니다.  
  
 성능과 압축률을 높이기 위해 columnstore 인덱스는 테이블을 여러 행 그룹으로 조각화한 후 각 행 그룹을 열 방식으로 압축합니다. 행 그룹의 행 수는 압축률을 높일 만큼 크고, 메모리 내 작업을 활용할 만큼 작아야 합니다.  
 열 세그먼트  
 *열 세그먼트* 는 행 그룹 내의 데이터 열입니다.  
  
-   각 행 그룹에는 테이블의 모든 열에 대해 각각 하나의 열 세그먼트가 포함됩니다.  
-   각 열 세그먼트는 함께 압축되며 실제 미디어에 저장됩니다.  
  
 ![Column segment](../../relational-databases/indexes/media/sql-server-pdw-columnstore-columnsegment.gif "Column segment")  
  
 클러스터형 columnstore 인덱스  
 *클러스터형 columnstore 인덱스* 는 전체 테이블에 대한 물리적 저장소입니다.  
  
 ![Clustered Columnstore Index](../../relational-databases/indexes/media/sql-server-pdw-columnstore-physicalstorage.gif "Clustered Columnstore Index")  
  
 열 세그먼트의 조각화를 줄이고 성능을 향상시키기 위해 columnstore 인덱스는 삭제된 행에 대한 ID의 btree 목록과 함께 deltastore라는 클러스터형 인덱스에 일부 데이터를 임시로 저장할 수 있습니다. deltastore 작업은 백그라운드에서 처리됩니다. 정확한 쿼리 결과를 반환하기 위해 클러스터형 columnstore 인덱스는 columnstore와 deltastore의 쿼리 결과를 모두 결합합니다.  
  
 델타 행 그룹  
 열 저장소 인덱스에만 사용되는 *델타 행 그룹*은 행 수가 임계값에 도달한 다음 columnstore로 이동할 때까지 행을 저장하여 columnstore 압축 및 성능을 개선하는 클러스터형 인덱스입니다.  

 델타 행 그룹이 최대 행 수에 도달하면 닫힙니다. 튜플 이동기 프로세스는 닫힌 행 그룹이 있는지 확인합니다. 닫힌 행 그룹을 찾으면 압축하여 columnstore에 저장합니다.  
  
deltastore columnstore 인덱스는 둘 이상의 델타 행 그룹을 가질 수 있습니다.  모든 델타 행 그룹은 *deltastore*라고 통칭됩니다.   

대규모 대량 로드 중에 대부분의 행은 deltastore를 통과하지 않고 columnstore로 곧바로 이동합니다. 대량 로드 끝부분의 일부 행은 수가 너무 적어서 행 그룹의 최소 크기(102,400개 행)에 맞지 않을 수 있습니다. 이 경우 최종 행은 columnstore 대신 deltastore로 이동합니다. 행 수가 102,400개 미만인 소규모 대량 로드의 경우 모든 행이 deltastore로 곧바로 이동합니다.  
  

  
 비클러스터형 columnstore 인덱스  
 *비클러스터형 columnstore 인덱스* 와 클러스터형 columnstore 인덱스는 동일하게 작동합니다. 차이점은 비클러스터형 인덱스는 rowstore 테이블에 만들어지는 보조 인덱스인 반면, 클러스터형 columnstore 인덱스는 전체 테이블에 대한 기본 저장소라는 점입니다.  
  
 비클러스터형 인덱스는 기본 테이블에 있는 행과 열의 전체 또는 일부에 대한 복사본을 포함합니다. 이 인덱스는 테이블의 하나 이상의 열로 정의되며 행을 필터링하는 선택적 조건이 있습니다.  
  
 비클러스터형 columnstore 인덱스는 columnstore 인덱스에서 분석이 동시에 실행되는 동안 OLTP 워크로드에서 기본 클러스터형 인덱스를 사용하는 실시간 운영 분석을 지원합니다. 자세한 내용은 [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)을 참조하세요.  
  
 일괄 처리 실행  
 *일괄 처리 실행* 은 쿼리에서 여러 행을 함께 처리하는 쿼리 처리 방법입니다. Columnstore 인덱스에 대한 쿼리는 일반적으로 쿼리 성능을 2~4배 개선하는 일괄 처리 모드 실행을 사용합니다. 일괄 처리 모드 실행은 columnstore 저장소 형식과 긴밀히 통합되고 그에 맞게 최적화되어 있습니다. 배치 모드 실행을 벡터 기반 또는 벡터화된 실행이라고도 합니다.  
  
##  <a name="benefits"></a> Columnstore 인덱스를 사용해야 하는 이유  
 Columnstore 인덱스는 매우 높은 수준의 데이터 압축(일반적으로 10배)을 제공하여 데이터 웨어하우스 저장소 비용을 크게 줄일 수 있습니다. 또한 분석을 위해 btree 인덱스보다 몇 배 더 나은 성능을 제공합니다. 이는 데이터 웨어하우징 및 분석 작업에 대한 기본 설정된 데이터 저장소 형식입니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 운영 워크로드에 대한 실시간 분석에 columnstore 인덱스를 사용할 수 있습니다.  
  
 Columnstore 인덱스가 빠른 이유는 다음과 같습니다.  
  
-   열이 동일한 도메인의 값을 저장하고 일반적으로 유사한 값을 가지므로 압축 비율이 높습니다. 이는 시스템에서 IO 병목 현상을 최소화하거나 제거하는 동사에 메모리 사용 공간을 크게 줄입니다.  
  
-   압축 비율이 높으면 메모리 내 사용 공간이 감소되어 쿼리 성능이 향상됩니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 더 많은 쿼리 및 데이터 작업을 메모리 내에서 수행할 수 있으므로 쿼리 성능도 개선할 수 있습니다.  
  
-   일괄 처리 실행은 여러 행을 함께 처리하여 쿼리 성능을 개선합니다(일반적으로 2~4배).  
  
-   쿼리는 대개 테이블에서 적은 수의 열만 선택하므로 실제 미디어의 총 I/O가 감소됩니다.  
  
## <a name="when-should-i-use-a-columnstore-index"></a>Columnstore 인덱스를 사용해야 하는 경우  
 권장 사용 사례:  
  
-   클러스터형 columnstore 인덱스를 사용하여 데이터 웨어하우징 워크로드에 대한 팩트 테이블 및 대규모 차원 테이블을 저장할 수 있습니다. 이는 쿼리 성능 및 데이터 압축을 최대 10배 향상시킵니다. [Columnstore Indexes for Data Warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)을 참조하세요.  
  
-   비클러스터형 columnstore 인덱스를 사용하여 OLTP 워크로드에 대한 실시간 분석을 수행할 수 있습니다. [Get started with Columnstore for real time operational analytics](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)(실시간 운영 분석을 위한 Columnstore 시작)를 참조하세요.  
  
### <a name="how-do-i-choose-between-a-rowstore-index-and-a-columnstore-index"></a>Rowstore 인덱스와 Columnstore 인덱스 간에 선택하려면 어떻게 해야 합니까?  
 Rowstore 인덱스는 데이터를 찾는 쿼리, 특정 값을 검색하는 쿼리 또는 작은 범위의 값에 대한 쿼리에 가장 적합합니다. Rowstore 인덱스는 테이블 검색 대신 주로 테이블 찾기가 필요한 경향이 있으므로 트랜잭션 워크로드에서 사용됩니다.  
  
 Columnstore 인덱스는 특히 대규모 테이블에서 많은 양의 데이터를 검색하는 분석 쿼리에 대한 높은 성능 향상을 제공합니다.  Columnstore 인덱스는 테이블 찾기 대신 전체 테이블 검색이 필요한 경향이 있으므로 특히 팩트 테이블에서 데이터 웨어하우징 및 분석 워크로드에 사용됩니다.  
  
### <a name="can-i-combine-rowstore-and-columnstore-on-the-same-table"></a>Rowstore와 Columnstore를 동일한 테이블에서 결합할 수 있습니까?  
 예 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 rowstore 테이블에서 업데이트 가능한 비클러스터형 columnstore 인덱스를 만들 수 있습니다. Columnstore 인덱스는 선택한 열의 복사본을 저장하므로 복사본에 대한 추가 공간이 필요하지만 평균 10배로 압축됩니다. 따라서 columnstore 인덱스에서 분석을 실행하고 이와 동시에 rowstore 인덱스에서 트랜잭션을 실행할 수 있습니다. rowstore 테이블의 데이터가 변경되면 columnstore가 업데이트되므로 두 인덱스 모두 동일한 데이터에 대해 작동합니다.  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 하나의 클러스터형 columnstore 인덱스에서 하나 이상의 비클러스터형 rowstore 인덱스를 사용할 수 있습니다. 따라서 기본 columnstore에서 효율적인 테이블 찾기를 수행할 수 있습니다. 다른 옵션도 사용할 수 있습니다. 예를 들어 rowstore 테이블에서 UNIQUE 제약 조건을 사용하여 기본 키 제약 조건을 적용할 수 있습니다. 고유하지 않은 값은 rowstore 테이블에 삽입하지 못하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 columnstore에 값을 삽입할 수 없습니다.  
  
## <a name="metadata"></a>메타데이터  
 columnstore 인덱스에 있는 모든 열이 메타데이터에 포괄 열로 저장됩니다. columnstore 인덱스에는 키 열이 없습니다.  

|||
|-|-|  
|[sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)|[sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)|  
|[sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)|[sys.internal_partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)|  
|[sys.column_store_segments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)|[sys.column_store_dictionaries&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)|  
|[sys.column_store_row_groups&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)|[sys.dm_db_column_store_row_group_operational_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)|  
|[sys.dm_db_column_store_row_group_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)|[sys.dm_column_store_object_pool&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)|  
|[sys.dm_db_column_store_row_group_operational_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)|[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)|  
|[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)||  
  
## <a name="related-tasks"></a>관련 작업  
 모든 관계형 테이블은 클러스터형 columnstore 인덱스로 지정하지 않는 한 rowstore를 기본 데이터 형식으로 사용합니다. `WITH CLUSTERED COLUMNSTORE INDEX` 옵션을 지정하지 않으면 `CREATE TABLE`은 rowstore 테이블을 만듭니다.  
  
 CREATE `CREATE TABLE` 문을 사용하여 테이블을 만드는 경우 `WITH CLUSTERED COLUMNSTORE INDEX` 옵션을 지정하여 테이블을 columnstore로 만들 수 있습니다. rowstore 테이블이 이미 있는 경우 이를 columnstore로 변환하려면 `CREATE COLUMNSTORE INDEX` 문을 사용합니다.  
  
|태스크|참조 항목|참고|  
|----------|----------------------|-----------|  
|테이블을 columnstore로 만듭니다.|[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 테이블을 클러스터형 columnstore 인덱스로 만들 수 있습니다. 먼저 rowstore 테이블을 만든 다음 이를 columnstore로 변환할 필요가 없습니다.|  
|columnstore 인덱스가 포함된 메모리 테이블을 만듭니다.|[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|
            [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 columnstore 인덱스가 포함된 메모리 최적화 테이블을 만들 수 있습니다. 테이블을 만든 후 ALTER TABLE ADD INDEX 구문을 사용하여 columnstore 인덱스를 추가할 수도 있습니다.|  
|rowstore 테이블을 columnstore로 변환합니다.|[CREATE COLUMNSTORE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|기존 힙 또는 이진 트리를 columnstore로 변환합니다. 예제에서는 이 변환을 수행할 때 기존 인덱스 및 인덱스 이름을 처리하는 방법을 보여 줍니다.|  
|columnstore 테이블을 rowstore로 변환합니다.|[CREATE COLUMNSTORE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|일반적으로 이 작업은 필요하지 않지만 이 변환을 수행해야 하는 경우가 있을 수 있습니다. 예제에서는 columnstore를 힙 또는 클러스터형 인덱스로 변환하는 방법을 보여 줍니다.|  
|Rowstore 테이블에 columnstore 인덱스를 만듭니다.|[CREATE COLUMNSTORE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Rowstore 테이블에는 하나의 columnstore 인덱스가 있을 수 있습니다.  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 columnstore 인덱스에 필터링된 조건이 있을 수 있습니다. 예제에서는 기본 구문을 보여 줍니다.|  
|운영 분석에 대한 고성능 인덱스를 만듭니다.|[Get started with Columnstore for real time operational analytics(실시간 운영 분석을 위한 Columnstore 시작)](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)|OLTP 쿼리에서는 btree 인덱스를 사용하고 분석 쿼리에서는 columnstore 인덱스를 사용하도록 상호 보완적인 columnstore 및 btree 인덱스를 만드는 방법을 설명합니다.|  
|데이터 웨어하우징용 고성능 columnstore 인덱스를 만듭니다.|[데이터 웨어하우스용 Columnstore 인덱스](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)|Columnstore 테이블에서 btree 인덱스를 사용하여 고성능 데이터 웨어하우징 쿼리를 만드는 방법을 설명합니다.|  
|btree 인덱스를 사용하여 columnstore 테이블에서 기본 키 제약 조건을 적용합니다.|[데이터 웨어하우스용 Columnstore 인덱스](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)|btree 및 columnstore 인덱스를 결합하여 columnstore 인덱스에서 기본 키 제약 조건을 적용하는 방법을 보여 줍니다.|  
|Columnstore 인덱스를 삭제합니다.|[DROP INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)|Columnstore 인덱스 삭제에서는 btree 인덱스에서 사용하는 표준 DROP INDEX 구문을 사용합니다. 클러스터형 columnstore 인덱스를 삭제하면 columnstore 테이블이 힙으로 변환됩니다.|  
|Columnstore 인덱스에서 행을 삭제합니다.|[DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|행을 삭제하려면 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) 를 사용합니다.<br /><br /> **columnstore** 행: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 행을 논리적으로 삭제된 것으로 표시하지만, 인덱스가 다시 작성될 때까지는 행에 대한 물리적 저장소를 회수하지 않습니다.<br /><br /> **deltastore** 행: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 행을 논리적 및 물리적으로 삭제합니다.|  
|Columnstore 인덱스의 행을 업데이트합니다.|[UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)|행을 삭제하려면 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) 를 사용합니다.<br /><br /> **columnstore** 행:  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 행을 논리적으로 삭제됨으로 표시한 다음 업데이트된 행을 deltastore에 삽입합니다.<br /><br /> **deltastore** 행: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 deltastore에 있는 행을 업데이트합니다.|  
|데이터를 columnstore 인덱스로 로드합니다.|[Columnstore 인덱스 데이터 로드](~/relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)||  
|deltastore의 모든 행을 강제로 columnstore로 이동합니다.|[ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) ... REBUILD<br /><br /> [Columnstore 인덱스 조각 모음](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)|REBUILD 옵션과 함께 ALTER INDEX를 사용하면 모든 행이 강제로 columnstore로 이동합니다.|  
|Columnstore 인덱스를 조각 모음합니다.|[ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)|ALTER INDEX … REORGANIZE는 columnstore 인덱스를 온라인으로 조각 모음합니다.|  
|테이블을 columnstore 인덱스와 병합합니다.|[MERGE&#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)||  
  
## <a name="see-also"></a>참고 항목  
 [Columnstore 인덱스 데이터 로드](~/relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Columnstore 인덱스 버전형 기능 요약](~/relational-databases/indexes/columnstore-indexes-what-s-new.md)   
 [Columnstore 인덱스 쿼리 성능](~/relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Get started with Columnstore for real time operational analytics(실시간 운영 분석을 위한 Columnstore 시작)](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [데이터 웨어하우스용 Columnstore 인덱스](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [Columnstore 인덱스 조각 모음](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)   
 [SQL Server 인덱스 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)   
 [Columnstore 인덱스 아키텍처](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)   
  
  





