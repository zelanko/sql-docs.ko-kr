---
title: Columnstore 인덱스 - 새로운 기능 | Microsoft 문서
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8b25d7c767be077764407d3eb47704f35146c94c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025015"
---
# <a name="columnstore-indexes---what39s-new"></a>Columnstore 인덱스 - 새로운 기능
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 각 버전 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]의 최신 릴리스에 사용할 수 있는 columnstore 기능에 대한 요약입니다.  

 > [!NOTE]
 > [!INCLUDE[ssSDS](../../includes/sssds-md.md)]의 경우 columnstore 인덱스는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Premium 계층 및 Standard 계층(S3 이상) 및 모든 vCore 계층에서 제공됩니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 이상의 경우 columnstore 인덱스는 모든 버전에서 제공됩니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)](SP1 이전) 및 이하 버전의 경우 columnstore 인덱스는 엔터프라이즈 버전에서만 제공됩니다.
 
## <a name="feature-summary-for-product-releases"></a>제품 릴리스에 대한 기능 요약  
 이 테이블은 Columnstore 인덱스 및 이를 사용할 수 있는 제품에 대한 주요 기능을 요약합니다.  

|Columnstore 인덱스 기능|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]|  
|-------------------------------|---------------------------|---------------------------|---------------------------|--------------------------------------------|-------------------------|---|  
|다중 스레드 쿼리에 대한 일괄 처리 모드 실행|예|예|예|예|예|예| 
|단일 스레드 쿼리에 대한 일괄 처리 모드 실행|||예|예|예|예|  
|보관 압축 옵션||예|예|예|예|예|  
|스냅샷 격리 및 커밋된 읽기 스냅샷 격리|||예|예|예|예| 
|테이블을 만들 때 columnstore 인덱스 지정|||예|예|예|예|  
|AlwaysOn은 columnstore 인덱스 지원|예|예|예|예|예|예| 
|Always On 읽기 가능한 보조는 읽기 전용 비클러스터형 columnstore 인덱스 지원|예|예|예|예|예|예|  
|Always On 읽기 가능한 보조는 업데이트할 수 있는 columnstore 인덱스 지원|||예|예|||  
|힙 또는 B-tree에 대한 읽기 전용 비클러스터형 columnstore 인덱스|예|예|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>|  
|힙 또는 B-tree에 대해 업데이트할 수 있는 비클러스터형 columnstore 인덱스|||예|예|예|예|  
|비클러스터형 columnstore 인덱스를 가진 힙 또는 B-tree에 사용할 수 있는 추가 B-tree 인덱스|예|예|예|예|예|예|  
|업데이트할 수 있는 클러스터형 columnstore 인덱스||예|예|예|예|예|  
|클러스터형 columnstore 인덱스에 대한 B-tree 인덱스|||예|예|예|예|  
|메모리 최적화 테이블에 대한 columnstore 인덱스|||예|예|예|예|  
|비클러스터형 columnstore 인덱스 정의는 필터링된 조건 사용을 지원|||예|예|예|예|  
|`CREATE TABLE` 및 `ALTER TABLE`의 columnstore 인덱스에 대한 압축 지연 옵션|||예|예|예|예|
|Columnstore 인덱스에는 비지속형 계산 열이 있을 수 있음||||예|||   
  
 <sup>1</sup> 읽기 전용 비클러스터형 columnstore 인덱스를 만들려면 읽기 전용 파일 그룹에 인덱스를 저장합니다.  

## [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 
 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]에서는 이러한 새 기능을 추가합니다.

### <a name="functional"></a>기능
- [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]에서는 클러스터형 columnstore 인덱스에서 비지속형 계산 열을 지원합니다. 클러스터형 columnstore 인덱스에서는 지속형 계산 열이 지원되지 않습니다. 계산된 열이 있는 columnstore 인덱스에 비클러스터형 인덱스를 만들 수 없습니다. 

## [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 는 columnstore 인덱스의 성능 및 유연성을 개선하기 위해 주요 향상 기능을 추가합니다. 이러한 향상된 기능을 통해 데이터 웨어하우징 시나리오가 향상되며 실시간 운영 분석이 가능합니다.  
  
### <a name="functional"></a>기능  
  
-   Rowstore 테이블에는 업데이트할 수 있는 비클러스터형 columnstore 인덱스 한 개가 있을 수 있습니다. 이전에는 비클러스터형 columnstore 인덱스가 읽기 전용이었습니다.  
  
-   비클러스터형 columnstore 인덱스 정의는 필터링된 조건 사용을 지원합니다. OLTP 테이블에 columnstore 인덱스를 추가할 경우 성능에 미치는 영향을 최소화하려면 필터링된 조건을 사용하여 운영 워크로드의 콜드 데이터에 대해서만 비클러스터형 columnstore 인덱스를 만듭니다. 
  
-   메모리 내 테이블에는 columnstore 인덱스가 한 개만 있을 수 있습니다. 테이블을 만들 때 이 인덱스를 만들거나 나중에 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 사용하여 추가할 수 있습니다. 이전에는 디스크 기반 테이블에만 columnstore 인덱스가 있을 수 있었습니다.  
  
-   클러스터형 columnstore 인덱스에 하나 이상의 비클러스터형 rowstore 인덱스가 있을 수 있습니다. 이전에 columnstore 인덱스는 비클러스터형 인덱스를 지원하지 않았습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 DML 작업에 대해 비클러스터형 인덱스를 자동으로 유지 관리합니다.  
  
-   기본 키 및 외래 키에 대해 B-tree 인덱스를 사용하여 클러스터형 columnstore 인덱스에 이러한 제약 조건의 적용을 지원합니다.  
  
-   Columnstore 인덱스에는 트랜잭션 워크로드가 실시간 운영 분석에 미치는 영향을 최소화하는 압축 지연 옵션이 있습니다.  이 옵션을 사용하여 자주 변하는 행을 columnstore로 압축하기 전에 안정화할 수 있습니다. 자세한 내용은 [CREATE COLUMNSTORE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md) 및 [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)을 참조하세요.  
  
### <a name="performance-for-database-compatibility-level-120-or-130"></a>데이터베이스 호환성 수준 120 또는 130에 대한 성능  
  
-   Columnstore 인덱스는 읽기 커밋된 스냅샷 격리 수준(RCSI) 및 스냅샷 격리(SI)를 지원합니다. 이를 통해 트랜잭션을 잠금이 없는 분석 쿼리와 일관성을 유지할 수 있습니다.  
  
-   Columnstore는 인덱스를 명시적으로 다시 만들 필요 없이 삭제된 행을 제거하여 인덱스 조각 모음을 지원합니다. `ALTER INDEX ... REORGANIZE` 문은 내부에서 정의한 정책을 바탕으로 columnstore에서 온라인 작업으로 삭제된 행을 제거함  
  
-   Columnstore 인덱스는 AlwaysOn 읽기 가능 보조 복제본에 대한 액세스일 수 있습니다. 분석 쿼리를 AlwaysOn 보조 복제본으로 분산하여 운영 분석의 성능을 개선할 수 있습니다.  
  
-   성능 향상을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 데이터 형식이 8바이트 이하를 사용하고 문자열 형식이 아닌 경우 테이블 검색 중에 집계 함수 `MIN`, `MAX`, `SUM`, `COUNT` 및 `AVG`를 계산합니다. 클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스 둘 다에 대해 Group By 절을 사용하거나 사용하지 않는 집계 푸시다운을 지원합니다.  
  
-   조건자 푸시다운은 [v]archar 또는 n[v]archar 형식의 문자열을 비교하는 쿼리의 속도를 향상시킵니다. 이는 일반적인 비교 연산자에 적용되며 비트맵 필터를 사용하는 LIKE와 같은 연산자를 포함합니다. 이는 SQL Server가 지원하는 모든 데이터 정렬에서 작동합니다.  
  
### <a name="performance-for-database-compatibility-level-130"></a>데이터베이스 호환성 수준 130에 대한 성능  
  
-   다음 연산 중 하나 이상을 사용하는 쿼리에 대한 새 일괄 처리 모드 실행 지원:  
    -   SORT  
    -   여러 가지 고유 함수를 사용하여 집계합니다. 몇 가지 예: `COUNT/COUNT`, `AVG/SUM`, `CHECKSUM_AGG`, `STDEV/STDEVP`.  
    -   Window 집계 함수: `COUNT`, `COUNT_BIG`, `SUM`, `AVG`, `MIN`, `MAX`, `CLR`.  
    -   Window 사용자 정의 집계: `CHECKSUM_AGG`, `STDEV`, `STDEVP`, `VAR`, `VARP`, `GROUPING`.  
    -   Window 집계 분석 함수: `LAG`, `LEAD`, `FIRST_VALUE`, `LAST_VALUE`, `PERCENTILE_CONT`, `PERCENTILE_DISC`, `CUME_DIST`, `PERCENT_RANK`.  
-   `MAXDOP 1`에서 실행되거나 직렬 쿼리 계획을 사용하는 단일 스레드 쿼리는 일괄 처리 모드에서 실행됩니다. 이전에는 다중 스레드 쿼리만이 일괄 처리 실행으로 실행되었습니다.  
-   메모리 액세스에 최적화된 테이블 쿼리는 rowstore 또는 columnstore 인덱스의 데이터에 액세스하는 경우 SQL InterOp에 병렬 계획을 가질 수 있습니다.  
  
### <a name="supportability"></a>지원 가능성  
이러한 시스템 뷰는 columnstore의 새로운 특징임:  

||| 
|-|-|
|[sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)|[sys.dm_column_store_object_pool &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)|  
|[sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)|[sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)|  
|[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)|[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)|  
|[sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)||  
  
이러한 메모리 내 OLTP 기반 DMV는 columnstore에 대한 업데이트를 포함합니다.  

||| 
|-|-|
|[sys.dm_db_xtp_hash_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql.md)|[sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)|  
|[sys.dm_db_xtp_memory_consumers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md)|[sys.dm_db_xtp_nonclustered_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-nonclustered-index-stats-transact-sql.md)|  
|[sys.dm_db_xtp_object_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-object-stats-transact-sql.md)|[sys.dm_db_xtp_table_memory_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)|  
  
### <a name="limitations"></a>제한 사항  
  

  
-   메모리 내 테이블의 경우 columnstore 인덱스는 모든 열을 포함해야 하며, columnstore 인덱스가 필터링된 조건을 가질 수 없습니다.  
-   메모리 내 테이블의 경우 columnstore 인덱스에 대한 쿼리는 InterOP 모드에서만 실행되며 메모리 내 고유 모드에서는 실행되지 않습니다. 병렬 실행은 지원됩니다.  
  
## [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서는 클러스터형 columnstore 인덱스를 기본 스토리지 형식으로 도입하였습니다. 이를 통해 일반 부하뿐만 아니라 업데이트, 삭제 및 삽입 작업도 사용할 수 있습니다.  
  
-   테이블에서 클러스터형 columnstore 인덱스를 기본 테이블 스토리지로 사용할 수 있습니다. 테이블에 다른 인덱스는 허용되지 않지만 클러스터형 columnstore 인덱스는 업데이트가 가능하므로 일반 부하를 수행하고 개별 행을 변경할 수 있습니다.  
-   비클러스터형 columnstore 인덱스는 이제 일괄 처리 모드로 실행될 수 있는 추가 연산자를 제외하고 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서와 같은 기능을 계속 가지고 있습니다. 다시 만들기 및 파티션 전환의 사용을 제외하고 여전히 업데이트는 불가능합니다. 비클러스터형 columnstore 인덱스는 디스크 기반 테이블에 대해서만 지원되며 메모리 내 테이블에 대해서는 지원되지 않습니다.  
-   클러스터형 및 비클러스터형 columnstore 인덱스에는 데이터를 추가로 압축하는 보관 압축 옵션이 있습니다. 보관 옵션은 메모리와 디스크에서 모두 데이터 크기를 줄이는 데 유용하지만 쿼리 성능이 저하됩니다. 이는 자주 액세스하지 않는 데이터에 적합합니다.  
-   클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스는 매우 유사하게 작동합니다. 즉, 같은 열 형식 스토리지 형식, 같은 쿼리 처리 엔진 및 같은 동적 관리 뷰 집합을 사용합니다. 차이점은 기본 인덱스 형식과 보조 인덱스 형식이며 비클러스터형 columnstore 인덱스는 읽기 전용입니다.  
-   이러한 연산자는 다중 스레드 쿼리, 즉 검색, 필터, 프로젝트, 조인, GROUP BY 및 UNION ALL에 대해 일괄 처리 모드에서 실행됩니다.  
  
## [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]는 columnstore 데이터에 대한 쿼리의 경우 rowstore 테이블 및 일괄 처리에 대한 또 다른 인덱스 형식으로 비클러스터형 columnstore 인덱스를 도입하였습니다.  
  
-   Rowstore 테이블에는 비클러스터형 columnstore 인덱스 한 개가 있을 수 있습니다.  
-   columnstore 인덱스는 읽기 전용입니다. Columnstore 인덱스를 만든 후에는 `INSERT`, `DELETE` 및 `UPDATE` 작업에 의해 테이블을 업데이트할 수 없으며, 이러한 작업을 수행하려면 인덱스를 삭제하고 테이블을 업데이트한 다음 columnstore 인덱스를 다시 만들어야 합니다. 파티션 전환을 사용하여 추가 데이터를 테이블에 로드할 수 있습니다. 파티션 전환의 장점은 columnstore 인덱스를 삭제한 다음 다시 만들지 않고 데이터를 로드할 수 있다는 것입니다.  
-   Columnstore 인덱스는 데이터의 복사본을 저장하기 때문에 이 인덱스를 사용하려면 언제나 추가 스토리지, 일반적으로 rowstore보다 10% 더 많은 스토리지가 필요합니다.  
-   일괄 처리는 2배 이상의 쿼리 성능을 제공하지만 병렬 쿼리 실행에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Columnstore 인덱스 디자인 지침](../../relational-databases/indexes/columnstore-indexes-design-guidance.md)   
 [Columnstore 인덱스 데이터 로드 지침](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Columnstore 인덱스 쿼리 성능](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [데이터 웨어하우스용 Columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [Columnstore 인덱스 조각 모음](../../relational-databases/indexes/columnstore-indexes-defragmentation.md) 
  
  
  
