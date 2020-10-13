---
title: 조각난 인덱스 검색 및 해결 | Microsoft Docs
description: 이 문서에서는 인덱스 조각화가 발생하는 방식, 얼마나 많은 조각이 존재하는지 검색하는 방법과 T-SQL 및 SQL Server Management Studio를 사용하여 인덱스 조각화를 해결하는 가장 좋은 옵션을 확인하는 방법을 설명합니다.
ms.custom: ''
ms.date: 03/19/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql13.swb.index.rebuild.f1
- sql13.swb.indexproperties.fragmentation.f1
- sql13.swb.index.reorg.f1
helpviewer_keywords:
- large object defragmenting
- indexes [SQL Server], reorganizing
- index reorganization [SQL Server]
- reorganizing indexes
- defragmenting large object data types
- index fragmentation [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- indexes [SQL Server], rebuilding
- defragmenting indexes
- nonclustered indexes [SQL Server], defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
- LOB data [SQL Server], defragmenting
- clustered indexes, defragmenting
ms.assetid: a28c684a-c4e9-4b24-a7ae-e248808b31e9
author: pmasl
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ba0eb3c9907acfe02939c49ea253869adbfc992b
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867351"
---
# <a name="resolve-index-fragmentation-by-reorganizing-or-rebuilding-indexes"></a>인덱스를 다시 구성하거나 다시 빌드하여 인덱스 조각화 해결

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 문서에서는 인덱스 조각 모음이 수행되는 방식과 이것이 쿼리 성능에 미치는 영향에 대해 설명합니다. [하나의 인덱스에 대해 존재하는 조각화의 양](#detecting-the-amount-of-fragmentation)을 확인한 후에는 원하는 도구에서 Transact-SQL 명령을 실행하거나 SQL Server Management Studio를 사용하여 [인덱스를 다시 빌드](#reorganize-an-index)하거나 [인덱스를 다시 빌드](#rebuild-an-index)하여 인덱스를 조각 모음할 수 있습니다.

## <a name="index-fragmentation-overview"></a>인덱스 조각화 개요

인덱스 조각화 정의 및 인덱스 조각화가 중요한 이유는 다음과 같습니다.

- 조각화는 인덱스의 키 값을 기준으로 하는 인덱스 내의 논리적 순서가 인덱스 페이지 내의 물리적 순서와 일치하지 않는 인덱스 페이지가 있는 경우에 발생합니다.
- [!INCLUDE[ssde_md](../../includes/ssde_md.md)]에서는 기본 데이터에 삽입, 업데이트 또는 삭제 작업을 수행할 때마다 인덱스를 자동으로 수정합니다. 예를 들어 테이블에 행을 추가하는 경우 새로운 키 값의 삽입 공간을 확보하기 위해 rowstore 인덱스의 기존 페이지가 분할될 수 있습니다. 이러한 수정이 거듭되면 시간이 흐름에 따라 인덱스의 정보가 조각화되어 데이터베이스 내에 흩어지게 될 수 있습니다. 조각화는 키 값을 기준으로 하는 인덱스의 논리적 페이지 순서가 데이터 파일 내의 물리적 순서와 일치하지 않을 때 나타납니다.
- 인덱스가 심하게 조각화된 경우 인덱스가 가리키는 데이터를 찾기 위해 추가 I/O가 필요하므로 쿼리 성능이 저하될 수 있습니다. I/O가 많을수록, 특히 검사 작업이 포함된 경우 애플리케이션이 느리게 응답합니다.

## <a name="detecting-the-amount-of-fragmentation"></a>조각화의 양 검색

사용할 인덱스 조각 모음 방법을 결정하기 위한 첫 번째 단계는 인덱스를 분석하여 조각화 수준을 확인하는 것입니다. rowstore 인덱스와 columnstore 인덱스의 조각화는 각각 다른 방법으로 검색됩니다.

> [!NOTE]
> 대량의 데이터가 삭제된 후에 인덱스 또는 힙 조각화를 검토하는 것이 특히 중요합니다. 힙의 경우, 업데이트가 자주 이루어지면 전달하는 레코드의 확산을 방지하기 위해 조각화를 검토해야 할 수도 있습니다. 힙에 대한 자세한 내용은 [힙(클러스터형 인덱스가 없는 테이블)](../../relational-databases/indexes/heaps-tables-without-clustered-indexes.md#heap-structures)을 참조하세요. 

### <a name="detecting-fragmentation-of-rowstore-indexes"></a>rowstore 인덱스의 조각화 검색

[sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)를 사용하면 특정 인덱스, 테이블이나 인덱싱된 뷰의 모든 인덱스, 데이터베이스의 모든 인덱스 또는 모든 데이터베이스 내 모든 인덱스에서 조각화를 검색할 수 있습니다. 분할된 인덱스의 경우 **sys.dm_db_index_physical_stats** 에서도 각 파티션의 조각화 정보를 제공합니다.

**sys.dm_db_index_physical_stats**에서 반환된 결과 집합은 다음 열을 포함합니다.

|열|Description|
|------------|-----------------|
|**avg_fragmentation_in_percent**|논리적 조각화(인덱스에서 순서가 잘못된 페이지) 비율|
|**fragment_count**|인덱스의 조각(물리적으로 연속되는 리프 페이지) 수|
|**avg_fragment_size_in_pages**|인덱스 한 조각의 평균 페이지 수|

조각화 수준을 파악한 후에는 다음 표를 참고하여 [인덱스 다시 구성](#reorganize-an-index) 또는 [인덱스 다시 빌드](#rebuild-an-index) 중에서 조각화를 제거하기에 적합한 방법을 확인합니다.

|**avg_fragmentation_in_percent** 값|수정문|
|-----------------------------------------------|--------------------------|
|> 5% 및 < = 30% <sup>1</sup>|ALTER INDEX REORGANIZE|
|> 30% <sup>1</sup>|ALTER INDEX REBUILD WITH (ONLINE = ON) <sup>2</sup>|

<sup>1</sup> 이러한 값은 `ALTER INDEX REORGANIZE` 및 `ALTER INDEX REBUILD`를 전환해야 하는 시점을 확인하기 위한 대략적인 지침을 제공합니다. 그러나 실제 값은 경우에 따라 달라질 수 있습니다. 실험을 통해 환경에 맞는 임계값을 확인하는 것이 중요합니다.      

> [!TIP] 
> 예를 들어 지정된 인덱스가 주로 스캔 작업에 사용되는 경우 조각화를 제거하면 해당 작업의 성능을 개선할 수 있습니다. 검색 작업에 주로 사용되는 인덱스의 경우 성능상 장점이 눈에 띄지 않을 수 있습니다.    
마찬가지로 힙(클러스터형 인덱스가 없는 테이블)에서 조각화를 제거하는 기능은 비클러스터형 인덱스 검색 작업에 특히 유용하지만 조회 작업에는 거의 영향을 주지 않습니다.

<sup>2</sup> 온라인 또는 오프라인으로 인덱스를 다시 작성할 수 있습니다. 인덱스를 다시 구성하는 과정은 항상 온라인으로 실행됩니다. 다시 구성할 때와 비슷한 가용성을 얻으려면 온라인으로 인덱스를 다시 작성해야 합니다. 자세한 내용은 [인덱스 다시 빌드](#rebuild-an-index) 및 [온라인으로 인덱스 작업 수행](../../relational-databases/indexes/perform-index-operations-online.md)을 참조하세요.

대체로 적은 양의 조각화를 제거할 경우 얻게 되는 이점보다 인덱스를 다시 구성하거나 다시 빌드하는 데 필요한 CPU 비용이 훨씬 크기 때문에, 조각화가 5% 미만인 인덱스는 조각 모음을 수행할 필요가 없습니다. 또한, 작은 rowstore 인덱스는 다시 빌드하거나 다시 구성해도 실제 조각화가 줄어들지 않는 경우가 많습니다. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]까지는, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]이 혼합 익스텐트를 사용하여 공간을 할당합니다. 따라서 작은 인덱스의 페이지는 종종 혼합 익스텐트에 저장됩니다. 혼합 익스텐트는 최대 8개의 개체가 공유할 수 있으므로 인덱스를 다시 작성하거나 다시 구성한 후에도 작은 인덱스의 조각화가 줄어들지 않을 수 있습니다. [rowstore 인덱스 다시 빌드 관련 고려 사항](#considerations-specific-to-rebuilding-rowstore-indexes)도 참조하세요. 익스텐트에 대한 자세한 내용은 [페이지 및 익스텐트 아키텍처 가이드](../../relational-databases/pages-and-extents-architecture-guide.md#extents)를 참조하세요.

### <a name="detecting-fragmentation-of-columnstore-indexes"></a>columnstore 인덱스의 조각화 검색

[sys.dm_db_column_store_row_group_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)를 사용하면 인덱스에서 삭제된 행의 백분율을 확인할 수 있으며, 이 백분율은 columnstore 인덱스에서 행 그룹의 조각화를 잘 보여 주는 측정값입니다. 이 정보를 사용하여 특정 인덱스, 테이블의 모든 인덱스, 데이터베이스의 모든 인덱스 또는 모든 데이터베이스의 모든 인덱스에서 조각화를 계산할 수 있습니다.

**_Db_column_store_row_group_physical_stats**에서 반환된 결과 집합은 다음 열을 포함합니다.

|열|Description|
|------------|-----------------|
|**total_rows**|행 그룹에 실제 저장된 행의 수입니다. 압축된 행 그룹의 경우 여기에 삭제된 것으로 표시된 행이 포함됩니다.|
|**deleted_rows**|삭제되도록 표시된 압축된 행 그룹에 물리적으로 저장된 행의 수입니다. 델타 저장소에 있는 행 그룹의 경우 0입니다.|

이 반환된 정보를 사용하여 다음 수식으로 인덱스 조각화를 계산할 수 있습니다.

```
100*(ISNULL(deleted_rows,0))/NULLIF(total_rows,0)
```

인덱스 조각화 수준을 파악한 후에는 다음 표를 참고하여 [인덱스 다시 구성](#reorganize-an-index) 또는 [인덱스 다시 빌드](#rebuild-an-index) 중에서 조각화를 제거하기에 적합한 방법을 확인합니다.

|**계산된 조각화(백분율)** 값|버전에 적용|수정문|
|-----------------------------------------------|--------------------------|--------------------------|
|> = 20%|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|ALTER INDEX REBUILD|
|> = 20%|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]로 시작|ALTER INDEX REORGANIZE|

### <a name="to-check-the-fragmentation-of-a-rowstore-index-using-tsql"></a>[!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 rowstore 인덱스의 조각화 확인

다음 예에서는 `AdventureWorks2016` 데이터베이스의 `HumanResources.Employee` 테이블에 있는 모든 인덱스의 평균 조각화 백분율을 찾습니다.

```sql
SELECT a.object_id, object_name(a.object_id) AS TableName,
    a.index_id, name AS IndedxName, avg_fragmentation_in_percent
FROM sys.dm_db_index_physical_stats
    (DB_ID (N'AdventureWorks2016_EXT')
        , OBJECT_ID(N'HumanResources.Employee')
        , NULL
        , NULL
        , NULL) AS a
INNER JOIN sys.indexes AS b
    ON a.object_id = b.object_id
    AND a.index_id = b.index_id;
GO
```

앞의 문은 다음과 비슷한 결과 세트를 반환합니다.

```
object_id   TableName    index_id    IndexName                                             avg_fragmentation_in_percent
----------- ------------ ----------- ----------------------------------------------------- ------------------------------
1557580587  Employee     1           PK_Employee_BusinessEntityID                          0
1557580587  Employee     2           IX_Employee_OrganizationalNode                        0
1557580587  Employee     3           IX_Employee_OrganizationalLevel_OrganizationalNode    0
1557580587  Employee     5           AK_Employee_LoginID                                   66.6666666666667
1557580587  Employee     6           AK_Employee_NationalIDNumber                          50
1557580587  Employee     7           AK_Employee_rowguid                                   0

(6 row(s) affected)
```

자세한 내용은 [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)를 참조하세요.

### <a name="to-check-the-fragmentation-of-a-columnstore-index-using-tsql"></a>[!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 columnstore 인덱스의 조각화 확인

다음 예에서는 `AdventureWorksDW2016` 데이터베이스의 `dbo.FactResellerSalesXL_CCI` 테이블에 있는 모든 인덱스의 평균 조각화 백분율을 찾습니다.

```sql
SELECT i.object_id,
    object_name(i.object_id) AS TableName,
    i.index_id,
    i.name AS IndexName,
    100*(ISNULL(SUM(CSRowGroups.deleted_rows),0))/NULLIF(SUM(CSRowGroups.total_rows),0) AS 'Fragmentation'
FROM sys.indexes AS i  
INNER JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups
    ON i.object_id = CSRowGroups.object_id
    AND i.index_id = CSRowGroups.index_id
WHERE object_name(i.object_id) = 'FactResellerSalesXL_CCI'
GROUP BY i.object_id, i.index_id, i.name
ORDER BY object_name(i.object_id), i.name;
```

앞의 문은 다음과 비슷한 결과 세트를 반환합니다.

```
object_id   TableName                   index_id    IndexName                       Fragmentation
----------- --------------------------- ----------- ------------------------------- ---------------
114099447   FactResellerSalesXL_CCI     1           IndFactResellerSalesXL_CCI      0

(1 row(s) affected)
```

### <a name="check-index-fragmentation-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 인덱스 조각화 확인

> [!NOTE]
> [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]는 SQL Server에서 columnstore 인덱스의 조각화를 컴퓨팅하는 데 사용할 수 없으며 Azure SQL Database에서 인덱스의 조각화를 컴퓨팅하는 데 사용할 수 없습니다. 이러한 시나리오에는 앞에 나온 [!INCLUDE[tsql](../../includes/tsql-md.md)] [예제](#to-check-the-fragmentation-of-a-columnstore-index-using-)를 사용하세요.

1. 개체 탐색기에서 인덱스의 조각화를 확인할 테이블이 포함된 데이터베이스를 확장합니다.
2. **테이블** 폴더를 확장합니다.
3. 인덱스의 조각화를 확인할 테이블을 확장합니다.
4. **인덱스** 폴더를 확장합니다.
5. 조각화를 확인할 인덱스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.
6. **페이지 선택**아래에서 **조각화**를 선택합니다.

**조각화** 페이지에서 다음 정보를 사용할 수 있습니다.

|값|Description|
|---|---|
|**페이지 사용률**|인덱스 페이지의 평균 사용률(%)을 나타냅니다. 즉, 인덱스 페이지가 모두 사용되고 있는 경우 100%로 표시되며, 50%인 경우 평균적으로 각 인덱스 페이지가 절반 정도 사용되고 있는 것입니다.|
|**총 조각화**|논리적 조각화 비율입니다. 이 값은 인덱스에서 순서대로 저장되어 있지 않은 페이지의 수를 나타냅니다.|
|**평균 행 크기**|리프 수준 행의 평균 크기입니다.|
|**깊이**|리프 수준을 포함한 인덱스의 수준 수입니다.|
|**전달된 레코드**|다른 데이터 위치로의 전달 포인터가 있는 힙의 레코드 수입니다. 이 상태는 업데이트하는 동안 원본 위치에 새 행을 저장할 공간이 충분하지 않은 경우에 발생합니다.|
|**삭제할 행**|삭제하도록 표시되어 있지만 아직 제거되지 않은 행의 수입니다. 이러한 행은 서버 사용량이 적을 때 정리 스레드에 의해 제거됩니다. 처리 중인 스냅샷 격리 트랜잭션으로 인해 보유된 행은 이 값에 포함되지 않습니다.|
|**인덱스 유형**|인덱스의 유형입니다. 가능한 값은 **클러스터형 인덱스**, **비클러스터형 인덱스**및 **기본 XML**입니다. 테이블을 인덱스가 없는 힙으로 저장할 수도 있지만, 그러한 경우 이 인덱스 속성 페이지를 열 수 없습니다.|
|**리프 수준 행**|리프 수준 행의 수입니다.|
|**최대 행 크기**|리프 수준 행의 최대 크기입니다.|
|**최소 행 크기**|리프 수준 행의 최소 크기입니다.|
|**페이지**|총 데이터 페이지 수입니다.|
|**파티션 ID**|인덱스를 포함하는 B-트리의 파티션 ID입니다.|
|**버전 삭제할 행**|처리 중인 스냅샷 격리 트랜잭션으로 인해 보유하고 있는 삭제할 레코드 수입니다.|

## <a name="defragmenting-indexes-by-rebuilding-or-reorganizing-the-index"></a>인덱스 다시 빌드 또는 다시 구성을 통한 인덱스 조각 모음

조각화된 인덱스는 다음 방법 중 하나를 사용하여 조각 모음합니다.

- 인덱스 다시 구성
- 인덱스 다시 빌드

> [!NOTE]
> 파티션 구성표에 빌드한 분할된 인덱스의 경우 전체 인덱스나 인덱스의 단일 파티션에서 다음 방법 중 하나를 사용할 수 있습니다.

### <a name="reorganize-an-index"></a>인덱스 재구성

인덱스 재구성은 최소한의 시스템 리소스를 사용하는 온라인 작업입니다. 즉, 장기간 차단 테이블 잠금이 유지되지 않으며 `ALTER INDEX REORGANIZE` 트랜잭션 중 기본 테이블에 대한 쿼리나 업데이트를 계속할 수 있습니다.

- [rowstore 인덱스](clustered-and-nonclustered-indexes-described.md)의 경우 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]이 리프 노드의 논리적 순서(왼쪽에서 오른쪽)에 맞게 리프 수준 페이지를 물리적으로 다시 정렬하여 테이블과 뷰에 대한 리프 수준의 클러스터형 및 비클러스터형 인덱스를 조각 모음합니다. 또한 재구성을 통해 인덱스 페이지가 인덱스의 채우기 비율 값에 따라 압축됩니다. 채우기 비율 설정을 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)를 사용하세요. 구문 예제는 [예제: Rowstore 재구성](../../t-sql/statements/alter-index-transact-sql.md#examples-rowstore-indexes)을 참조하세요.

- [columnstore 인덱스](columnstore-indexes-overview.md)를 사용하는 경우 시간 경과에 따라 데이터를 삽입, 업데이트 및 삭제함으로써 델타 저장소가 여러 개의 작은 행 그룹으로 분할될 수 있습니다. columnstore 인덱스를 재구성하면 모든 행 그룹이 columnstore에 강제로 포함되고, 행 그룹이 더 많은 행을 포함하는 소수의 행 그룹으로 결합됩니다. 또한 재구성 작업은 columnstore에서 삭제된 행을 제거합니다. 처음 재구성하는 경우 데이터 압축을 위해 추가 CPU 리소스가 필요하므로 전반적인 시스템 성능이 느려질 수 있습니다. 하지만 데이터가 압축되는 즉시 쿼리 성능이 향상됩니다. 구문 예제는 [예제: ColumnStore 재구성](../../t-sql/statements/alter-index-transact-sql.md#examples-columnstore-indexes)을 참조하세요.

### <a name="rebuild-an-index"></a>인덱스 다시 작성

인덱스를 다시 작성하면 이 인덱스가 삭제된 다음 다시 생성됩니다. 인덱스 유형 및 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 버전에 따라 온라인이나 오프라인에서 다시 빌드 작업을 수행할 수 있습니다. T-SQL 구문에 대한 자세한 내용은 [ALTER INDEX REBUILD](../../t-sql/statements/alter-index-transact-sql.md#rebuilding-indexes)를 참조하세요.

- [rowstore 인덱스](clustered-and-nonclustered-indexes-described.md)의 경우 다시 빌드하면 조각화가 제거되고, 지정된 채우기 비율 또는 기존 채우기 비율 설정을 기준으로 페이지를 압축하여 디스크 공간이 회수되며, 인덱스 행이 연속된 페이지로 다시 정렬됩니다. `ALL`을 지정하면 테이블의 모든 인덱스가 단일 트랜잭션으로 삭제되고 다시 작성됩니다. 외래 키 제약 조건은 미리 삭제하지 않아도 됩니다. 익스텐트가 128개 이상인 인덱스를 다시 작성하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 실제 페이지 할당 취소와 해당 관련 잠금이 트랜잭션 커밋 후까지 지연됩니다. 구문 예제는 [예제: Rowstore 재구성](../../t-sql/statements/alter-index-transact-sql.md#examples-rowstore-indexes)을 참조하세요.

- [columnstore 인덱스](columnstore-indexes-overview.md)의 경우 다시 빌드하면 조각화가 제거되고, 모든 행이 columnstore로 이동되며, 테이블에서 논리적으로 삭제된 행을 물리적으로 삭제하여 디스크 공간이 회수됩니다. 
  
  > [!TIP]
  > [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 온라인 작업과 같이 `REORGANIZE`가 백그라운드에서 필수 재빌드를 수행하므로 columnstore 인덱스를 다시 빌드할 필요가 없습니다. 
  
  구문 예제는 [예제: ColumnStore rebuild](../../t-sql/statements/alter-index-transact-sql.md#examples-columnstore-indexes)(ColumnStore 다시 빌드)를 참조하세요.

### <a name="permissions"></a><a name="Permissions"></a> 권한

테이블 또는 보기에 대한 `ALTER` 권한이 필요합니다. 사용자는 다음 역할 중 하나 이상의 멤버여야 합니다.

- **db_ddladmin** 데이터베이스 역할 <sup>1</sup>
- **db_owner** 데이터베이스 역할
- **sysadmin** 서버 역할

<sup>1</sup>**db_ddladmin** 데이터베이스 역할은 [최소 권한](/windows-server/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models)입니다.

### <a name="remove-fragmentation-using-ssmanstudiofull"></a><a name="SSMSProcedureReorg"></a>[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 조각화 제거

#### <a name="to-reorganize-or-rebuild-an-index"></a>인덱스를 다시 구성하거나 다시 작성하려면

1. 개체 탐색기에서 인덱스를 다시 구성할 테이블이 포함된 데이터베이스를 확장합니다.
2. **테이블** 폴더를 확장합니다.
3. 인덱스를 다시 구성할 테이블을 확장합니다.
4. **인덱스** 폴더를 확장합니다.
5. 다시 구성할 인덱스를 마우스 오른쪽 단추로 클릭하고 **다시 구성**을 선택합니다.
6. **인덱스 다시 구성** 대화 상자에서 **다시 구성할 인덱스** 표에 올바른 인덱스가 있는지 확인한 다음 **확인**을 클릭합니다.
7. **큰 개체 열 데이터 압축** 확인란을 선택하여 LOB(Large Object) 데이터가 포함된 모든 페이지도 압축되도록 지정합니다.
8. **확인.**

#### <a name="to-reorganize-all-indexes-in-a-table"></a>테이블의 모든 인덱스를 다시 구성하려면

1. 개체 탐색기에서 인덱스를 다시 구성할 테이블이 포함된 데이터베이스를 확장합니다.
2. **테이블** 폴더를 확장합니다.
3. 인덱스를 다시 구성할 테이블을 확장합니다.
4. **인덱스** 폴더를 마우스 오른쪽 단추로 클릭하고 **모두 다시 구성**을 선택합니다.
5. **인덱스 다시 구성** 대화 상자에서 **다시 구성할 인덱스**에 올바른 인덱스가 있는지 확인합니다. **다시 구성할 인덱스** 표에서 인덱스를 제거하려면 인덱스를 선택한 다음 Delete 키를 누릅니다.
6. **큰 개체 열 데이터 압축** 확인란을 선택하여 LOB(Large Object) 데이터가 포함된 모든 페이지도 압축되도록 지정합니다.
7. **확인.**

#### <a name="to-rebuild-an-index"></a>인덱스를 다시 작성하려면

1. 개체 탐색기에서 인덱스를 다시 구성할 테이블이 포함된 데이터베이스를 확장합니다.
2. **테이블** 폴더를 확장합니다.
3. 인덱스를 다시 구성할 테이블을 확장합니다.
4. **인덱스** 폴더를 확장합니다.
5. 다시 구성할 인덱스를 마우스 오른쪽 단추로 클릭하고 **다시 작성**을 선택합니다.
6. **인덱스 다시 작성** 대화 상자에서 **다시 작성할 인덱스** 표에 올바른 인덱스가 있는지 확인한 다음 **확인**을 클릭합니다.
7. **큰 개체 열 데이터 압축** 확인란을 선택하여 LOB(Large Object) 데이터가 포함된 모든 페이지도 압축되도록 지정합니다.
8. **확인.**

### <a name="remove-fragmentation-using-tsql"></a><a name="TsqlProcedureReorg"></a>[!INCLUDE[tsql](../../includes/tsql-md.md)]를 사용하여 조각화 제거

> [!NOTE]
> [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 인덱스를 다시 빌드하거나 다시 구성하는 방법에 대한 예를 알아보려면 [ALTER 인덱스 예: Columnstore 인덱스](../../t-sql/statements/alter-index-transact-sql.md#examples-columnstore-indexes) 및 [ALTER 인덱스 예: Rowstore 인덱스](../../t-sql/statements/alter-index-transact-sql.md#examples-rowstore-indexes)를 참조하세요.

#### <a name="to-reorganize-a-fragmented-index"></a>조각난 인덱스를 다시 구성하려면

다음 예에서는 `AdventureWorks2016` 데이터베이스에서 `HumanResources.Employee` 테이블의 `IX_Employee_OrganizationalLevel_OrganizationalNode` 인덱스를 다시 구성합니다.

```sql
ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode
    ON HumanResources.Employee
    REORGANIZE;
```

다음 예에서는 `AdventureWorksDW2016` 데이터베이스의 `dbo.FactResellerSalesXL_CCI` 테이블에서 `IndFactResellerSalesXL_CCI` columnstore 인덱스를 다시 구성합니다.

```sql
-- This command will force all CLOSED and OPEN rowgroups into the columnstore.
ALTER INDEX IndFactResellerSalesXL_CCI
    ON FactResellerSalesXL_CCI
    REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);
```

#### <a name="to-reorganize-all-indexes-in-a-table"></a>테이블의 모든 인덱스를 다시 구성하려면

다음 예에서는 `AdventureWorks2016` 데이터베이스의 `HumanResources.Employee` 테이블에 있는 모든 인덱스를 다시 구성합니다.

```sql
ALTER INDEX ALL ON HumanResources.Employee
   REORGANIZE;
```

#### <a name="to-rebuild-a-fragmented-index"></a>조각난 인덱스를 다시 작성하려면

다음 예에서는 `AdventureWorks2016` 데이터베이스에 있는 `Employee` 테이블의 단일 인덱스를 다시 작성합니다.

[!code-sql[IndexDDL#AlterIndex1](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_1.sql)]

#### <a name="to-rebuild-all-indexes-in-a-table"></a>테이블에서 모든 인덱스를 다시 작성하려면

다음 예에서는 `ALL` 키워드를 사용하여 `AdventureWorks2016` 데이터베이스의 테이블과 연결된 모든 인덱스를 다시 빌드합니다. 3개의 옵션이 지정됩니다.

[!code-sql[IndexDDL#AlterIndex2](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_2.sql)]

자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.

#### <a name="automatic-index-and-statistics-management"></a>자동 인덱스 및 통계 관리

[Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)와 같은 솔루션을 사용하여 하나 이상의 데이터베이스에 대한 인덱스 조각 모음 및 통계 업데이트를 자동으로 관리합니다. 이 절차는 다른 매개 변수 사이에서 조각화 수준에 따라 인덱스를 다시 작성하거나 다시 구성할지 여부를 자동으로 선택하고 통계를 선형 임계값으로 업데이트합니다.

## <a name="considerations-specific-to-rebuilding-rowstore-indexes"></a>rowstore 인덱스 다시 빌드 관련 고려 사항

클러스터형 인덱스를 다시 빌드할 경우 비클러스터형 인덱스 레코드에 포함된 물리적 또는 논리적 식별자를 변경해야 하면 클러스터링 키를 참조하는 비클러스터형 인덱스가 자동으로 다시 빌드됩니다.

다음 시나리오에서는 테이블의 모든 rowstore 비클러스터형 인덱스가 자동으로 다시 빌드되도록 강제 적용합니다.

- 테이블에서 클러스터형 인덱스 만들기
- 클러스터형 인덱스를 제거하면 테이블이 힙으로 저장됨
- 열을 포함하거나 제외하도록 클러스터링 키 변경

다음 시나리오에서는 테이블의 모든 rowstore 비클러스터형 인덱스가 자동으로 다시 빌드되도록 요구하지 않습니다.

- 고유한 클러스터형 인덱스 다시 작성
- 고유하지 않은 클러스터형 인덱스 다시 작성
- 인덱스 스키마 변경(예: 클러스터형 인덱스에 파티션 구성표 적용 또는 클러스터형 인덱스를 다른 파일 그룹으로 이동)

> [!IMPORTANT]
> 인덱스가 위치한 파일 그룹이 오프라인이거나 읽기 전용으로 설정되어 있으면 인덱스를 다시 구성할 수 없습니다. ALL 키워드를 지정하면 하나 이상의 인덱스가 오프라인 또는 읽기 전용 파일 그룹에 있을 경우 해당 문이 실패합니다.
>
> 인덱스를 다시 빌드하는 동안 물리적 미디어에는 인덱스의 두 복사본을 저장할 수 있는 충분한 공간이 있어야 합니다. 다시 빌드 작업이 끝나면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]이 원래 인덱스를 삭제합니다.

`ALL`을 `ALTER INDEX` 문으로 지정하면 테이블에서 관계형 인덱스, 클러스터형 및 비클러스터형 인덱스 모두와 XML 인덱스가 다시 구성됩니다.

## <a name="considerations-specific-to-rebuilding-a-columnstore-index"></a>Columnstore 인덱스 다시 빌드 관련 고려 사항

Columnstore 인덱스를 다시 빌드하는 경우 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]는 델타 저장소를 비롯하여 원래 columnstore 인덱스에서 모든 데이터를 읽습니다. 데이터를 새 행 그룹으로 결합하고 행 그룹을 columnstore로 압축합니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 테이블에서 논리적으로 삭제된 행을 물리적으로 삭제하여 columnstore를 조각 모음합니다. 삭제된 바이트는 디스크에서 회수됩니다.

> [!NOTE]
> [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]를 사용하여 columnstore 인덱스를 다시 구성하면 COMPRESSED 행 그룹이 함께 결합되지만 모든 행 그룹이 columnstore로 강제 압축되는 것은 아닙니다. CLOSED 행 그룹은 압축되지만 OPEN 행 그룹은 columnstore로 압축되지 않습니다. 모든 행 그룹을 강제 압축하려면 [아래](#TsqlProcedureReorg)의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 예를 사용하세요.

> [!NOTE]
> [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터는 내부 임계값에 따라 특정 시간 동안 존재하던 더 작은 OPEN 델타 행 그룹을 자동으로 압축하거나 다수의 행이 삭제된 위치에서 COMPRESSED 행 그룹을 병합하는 백그라운드 병합 작업이 튜플 이동기를 지원합니다. 이번 변경 덕분에 지속적으로 columnstore 인덱스 품질이 향상됩니다.    
> columnstore 용어 및 개념에 대한 자세한 내용은 [columnstore 인덱스: 개요](../../relational-databases/indexes/columnstore-indexes-overview.md)를 참조하세요.

### <a name="rebuild-a-partition-instead-of-the-entire-table"></a>전체 테이블 대신 파티션 다시 빌드

- 인덱스가 큰 경우 전체 테이블을 다시 작성하려면 많은 시간이 소요되고 다시 작성 중에 인덱스의 추가 복사본을 저장할 수 있는 충분한 디스크 공간이 필요합니다. 일반적으로 가장 최근에 사용한 파티션만 다시 작성하면 됩니다.
- 분할된 테이블의 경우 최근 수정된 파티션에서만 주로 조각화가 발생하므로 전체 columnstore 인덱스를 다시 작성할 필요는 없습니다. 팩트 테이블 및 대규모 차원 테이블은 일반적으로 테이블 청크에서 백업 및 관리 작업을 수행하기 위해 분할됩니다.

### <a name="rebuild-a-partition-after-heavy-dml-operations"></a>리소스 사용량이 많은 DML 작업 후 파티션 다시 빌드

파티션을 다시 빌드하면 파티션을 조각 모음하고 디스크 스토리지를 줄일 수 있습니다. 다시 빌드하면 columnstore에서 삭제 표시된 모든 행이 삭제되고, 델타 저장소의 모든 행 그룹이 columnstore로 이동됩니다. 델타 저장소에는 1백만 개 미만의 행을 포함하는 여러 행 그룹이 있을 수 있습니다.

### <a name="rebuild-a-partition-after-loading-data"></a>데이터를 로드한 후 파티션 다시 빌드

데이터를 로드한 후 파티션을 다시 빌드하면 모든 데이터가 columnstore에 저장됩니다. 동시에 동일한 파티션으로 100,000행 미만을 로드하는 각 동시 프로세스의 경우 파티션에는 여러 델타 저장소가 있을 수 있습니다. 다시 빌드하면 델타 저장소의 모든 행이 columnstore로 이동됩니다.

## <a name="considerations-specific-to-reorganizing-a-columnstore-index"></a>Columnstore 인덱스 다시 구성 관련 고려 사항

columnstore 인덱스를 다시 구성하는 경우 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]는 압축된 행 그룹으로 CLOSED 각 델타 행 그룹을 columnstore로 압축합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 `REORGANIZE` 명령은 다음과 같은 추가 조각 모음 최적화를 온라인으로 수행합니다.

- 행의 10% 이상이 논리적으로 삭제된 경우 rowgroup에서 행을 물리적으로 제거합니다. 삭제된 바이트는 물리적 미디어에서 회수됩니다. 예를 들어 행 1백만 개의 압축된 행 그룹이 삭제된 행 10만 개를 포함하는 경우, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 삭제된 행을 제거하고 행이 90만 개인 rowgroup을 다시 압축합니다. 즉, 삭제된 행을 제거하여 스토리지를 절약합니다.

- 하나 이상의 압축된 rowgroup을 결합하여 rowgroup당 행 수를 최대 1,048,576개로 증가시킵니다. 예를 들어 행 102,400개의 대량 가져오기 5회를 수행하면 압축된 rowgroup 5개를 얻습니다. REORGANIZE를 실행하면 이러한 rowgroup이 크기 512,000행의 압축된 rowgroup 1개로 병합됩니다. 이때 사전 크기 또는 메모리 제한이 없는 것으로 가정합니다.

- 행의 10% 이상이 논리적으로 삭제된 행 그룹의 경우 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]는 이 행 그룹을 하나 이상의 행 그룹과 결합하려고 시도합니다. 예를 들어 rowgroup 1이 행 500,000개를 사용하여 압축된다면 rowgroup 21은 최대 1,048,576개의 행을 사용하여 압축됩니다. 즉, rowgroup 21은 삭제된 행 60%와 남은 행 409,830개를 포함합니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)]는 이러한 두 행 그룹을 결합하여 909,830개의 행을 포함한 새 행 그룹을 압축하는 방법을 선호합니다.

데이터 로드를 수행하면 델타 저장소에 여러 개의 작은 행 그룹을 포함할 수 있습니다. `ALTER INDEX REORGANIZE`를 사용하여 모든 rowgroup을 columnstore로 강제한 후 rowgroup을 열이 더 많은 소수의 rowgroup으로 결합합니다. 또한, 재구성 작업은 columnstore에서 삭제된 행도 제거합니다.

## <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항

128 익스텐트가 넘는 Rowstore 인덱스는 논리적 단계와 물리적 단계로 나누어 다시 빌드합니다. 논리적 단계에서는 인덱스에 의해 사용되는 기존 할당 단위가 할당 취소 상태로 표시되며 데이터 행이 복사되어 정렬된 후 다시 작성된 인덱스를 저장하기 위해 생성된 새 할당 단위로 옮겨집니다. 물리적 단계에서는 이전에 할당 취소 상태로 표시된 할당 단위가 백그라운드로 실행되는 짧은 트랜잭션을 통해 물리적으로 삭제됩니다. 이 단계는 잠금을 많이 필요로 하지 않습니다. 익스텐트에 대한 자세한 내용은 [페이지 및 익스텐트 아키텍처 가이드](../../relational-databases/pages-and-extents-architecture-guide.md)를 참조하세요.

`ALTER INDEX REORGANIZE` 문을 사용하려는 경우 작업에서 파일 그룹 내의 다른 파일이 아닌 동일한 파일에만 임시 작업 페이지를 할당할 수 있으므로 인덱스가 포함된 데이터 파일에 사용 가능한 공간이 있어야 합니다. 따라서 파일 그룹에 사용 가능한 페이지가 있을 수 있지만 사용자는 여전히 오류 1105: `Could not allocate space for object '###' in database '###' because the '###' filegroup is full. Create disk space by deleting unneeded files, dropping objects in the filegroup, adding additional files to the filegroup, or setting autogrowth on for existing files in the filegroup.`이 발생할 수 있습니다.

> [!WARNING]
> 파티션 수가 1,000개를 초과하는 테이블에서 정렬되지 않은 인덱스를 만들거나 다시 작성할 수 있지만 해당 인덱스는 지원되지 않습니다. 그러면 작업 중에 성능이 저하되거나 메모리가 과도하게 소비될 수 있습니다. 파티션 수가 1,000개를 초과하는 경우[ 정렬된 인덱스](../partitions/partitioned-tables-and-indexes.md#aligned-index)만 사용하는 것이 좋습니다.

인덱스가 있는 파일 그룹이 **오프라인**이거나 **읽기 전용**으로 설정되어 있으면 인덱스를 다시 구성하거나 빌드할 수 없습니다. `ALL` 키워드를 지정하면 하나 이상의 인덱스가 오프라인 또는 읽기 전용 파일 그룹에 있을 경우 해당 문이 실패합니다.

통계:

- 인덱스를 **생성**하거나 **다시 빌드**하는 경우 테이블의 모든 행을 검사하여 통계가 생성되거나 업데이트됩니다. 하지만 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 분할된 인덱스를 만들거나 다시 작성할 때 테이블의 모든 행을 검사하여 통계를 만들거나 업데이트하지 않습니다. 대신 쿼리 최적화 프로그램에서 기본 샘플링 알고리즘을 사용하여 이러한 통계를 생성합니다. 테이블의 모든 행을 검사하여 분할된 인덱스에 대한 통계를 얻으려면 `FULLSCAN` 절에서 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 또는 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md)를 사용합니다.

- 인덱스를 **재구성**하는 경우에는 통계가 업데이트되지 않습니다.

`ALLOW_PAGE_LOCKS`가 OFF로 설정되면 인덱스를 다시 구성할 수 없습니다.

[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]까지는 클러스터형 columnstore 인덱스를 다시 빌드하는 것은 오프라인 작업입니다. 다시 빌드하는 동안 데이터베이스 엔진이 테이블 또는 파티션에 대한 배타적 잠금을 획득해야 합니다. 데이터는 오프라인 상태이며 `NOLOCK`, RCSI(읽기 커밋된 스냅숏 격리) 또는 스냅숏 격리를 사용하는 경우에도 다시 빌드하는 동안에는 사용할 수 없습니다.
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 `ONLINE = ON` 옵션을 사용하여 클러스터형 columnstore 인덱스를 다시 빌드할 수 있습니다.

순서가 지정된 클러스터형 columnstore 인덱스가 포함된 Azure Synapse Analytics(이전의 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]) 테이블에 대해 `ALTER INDEX REBUILD`를 실행하는 경우 TempDB를 사용하여 데이터가 다시 정렬됩니다. 다시 빌드 작업 중에 TempDB를 모니터링합니다. TempDB 공간이 더 필요하면 데이터 웨어하우스를 통해 규모를 확장할 수 있습니다. 인덱스 다시 빌드가 완료되면 다시 크기를 줄입니다.

순서가 지정된 클러스터형 columnstore 인덱스가 포함된 Azure Synapse Analytics(이전의 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]) 테이블에 대해 `ALTER INDEX REORGANIZE`가 데이터를 다시 정렬하지 않습니다. 데이터를 다시 정렬하려면 `ALTER INDEX REBUILD`를 사용하세요.

## <a name="using-index-rebuild-to-recover-from-hardware-failures"></a>INDEX REBUILD를 사용하여 하드웨어 오류 복구

이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 rowstore 비클러스터형 인덱스를 다시 빌드하여 하드웨어 오류로 인한 불일치를 해결할 수 있는 경우도 있습니다.
[!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 이상에서도 비클러스터형 인덱스를 오프라인으로 다시 빌드하여 인덱스와 클러스터형 인덱스 간의 불일치를 복구할 수 있습니다. 그러나 인덱스를 온라인으로 다시 빌드하는 경우에는 비클러스터형 인덱스 간의 불일치를 해결할 수 없습니다. 온라인으로 다시 빌드하는 경우 기존의 비클러스터형 인덱스를 사용하므로 불일치가 계속 남아 있게 됩니다. 경우에 따라 오프라인으로 인덱스를 다시 작성하면 클러스터형 인덱스 검색 또는 힙 검색이 수행되어 불일치가 제거됩니다. 클러스터형된 인덱스에서 다시 빌드되도록 하려면 비클러스터형 인덱스를 삭제한 후 다시 만드세요. 이전 버전의 경우처럼 영향을 받은 데이터를 백업한 후 복원하여 불일치를 제거하는 것이 좋습니다. 비클러스터형 인덱스의 경우에는 오프라인으로 인덱스를 다시 작성하여 인덱스 간 불일치를 해결할 수 있습니다. 자세한 내용은 [DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [SQL Server 인덱스 아키텍처 및 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)
- [온라인으로 인덱스 작업 수행](../../relational-databases/indexes/perform-index-operations-online.md)
- [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)
- [Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)
- [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)
- [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)
- [Columnstore 인덱스 쿼리 성능](../../relational-databases/indexes/columnstore-indexes-query-performance.md)
- [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)
- [데이터 웨어하우스용 Columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)
- [Columnstore 인덱스와 rowgroup에 대한 병합 정책](/archive/blogs/sqlserverstorageengine/columnstore-index-merge-policy-for-reorganize)