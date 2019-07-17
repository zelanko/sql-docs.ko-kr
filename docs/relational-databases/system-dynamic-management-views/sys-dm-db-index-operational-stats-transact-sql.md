---
title: sys.dm_db_index_operational_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_index_operational_stats
- sys.dm_db_index_operational_stats_TSQL
- sys.dm_db_index_operational_stats
- dm_db_index_operational_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_operational_stats dynamic management function
ms.assetid: 13adf2e5-2150-40a6-b346-e74a33ce29c6
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b8222454d5e016733abef3c086e38add777cd304
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004890"
---
# <a name="sysdmdbindexoperationalstats-transact-sql"></a>sys.dm_db_index_operational_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스의 현재 하위 수준 I/O, 잠금, 래치 및 액세스 방법 작업 테이블이 나 인덱스의 각 파티션에 대해를 반환 합니다.    
    
 메모리 액세스에 최적화된 인덱스는 이 DMV에 나타나지 않습니다.    
    
> [!NOTE]    
>  **sys.dm_db_index_operational_stats** 메모리 최적화 인덱스에 대 한 정보를 반환 하지 않습니다. 메모리 최적화 인덱스 사용에 대 한 정보를 참조 하세요 [sys.dm_db_xtp_index_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)합니다.    
        
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>구문    
    
```    
    
sys.dm_db_index_operational_stats (    
    { database_id | NULL | 0 | DEFAULT }    
  , { object_id | NULL | 0 | DEFAULT }    
  , { index_id | 0 | NULL | -1 | DEFAULT }    
  , { partition_number | NULL | 0 | DEFAULT }    
)    
```    
    
## <a name="arguments"></a>인수    
 *database_id* | NULL | 0 | DEFAULT    
 데이터베이스의 ID입니다. *database_id* 됩니다 **smallint**합니다. 올바른 입력은 데이터베이스의 ID 번호, NULL, 0 또는 DEFAULT입니다. 기본값은 0입니다. 이 컨텍스트에서 NULL, 0 및 DEFAULT는 동등한 값입니다.    
    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 데이터베이스에 대한 정보를 반환하려면 NULL을 지정합니다. NULL을 지정 하는 경우 *database_id*, NULL을 지정 해야 *object_id*합니다 *index_id*, 및 *partition_number*합니다.    
    
 기본 제공 함수 [DB_ID](../../t-sql/functions/db-id-transact-sql.md) 지정할 수 있습니다.    
    
 *object_id* | NULL | 0 | DEFAULT    
 인덱스가 있는 테이블 또는 뷰의 개체 ID입니다. *object_id* 는 **int**입니다.    
    
 올바른 입력은 테이블 및 뷰의 ID 번호, NULL, 0 또는 DEFAULT입니다. 기본값은 0입니다. 이 컨텍스트에서 NULL, 0 및 DEFAULT는 동등한 값입니다.    
    
 지정된 데이터베이스에 있는 모든 테이블 및 뷰에 대한 캐시된 정보를 반환하려면 NULL을 지정합니다. NULL을 지정 하는 경우 *object_id*에 NULL을 지정 해야 *index_id* 하 고 *partition_number*합니다.    
    
 *index_id* | 0 | NULL | -1 | DEFAULT    
 인덱스의 ID입니다. *index_id* 됩니다 **int**합니다. 유효한 입력은 ID 번호를 인덱스 0의 경우 *object_id* 힙, NULL,-1 또는 DEFAULT입니다. 기본값은 -1입니다. 이 경우 NULL, -1 및 DEFAULT는 동등한 값입니다.    
    
 기본 테이블 또는 뷰의 모든 인덱스에 대한 캐시된 정보를 반환하려면 NULL을 지정합니다. NULL을 지정 하는 경우 *index_id*에 NULL을 지정 해야 *partition_number*합니다.    
    
 *partition_number* | NULL | 0 | 기본    
 개체의 파티션 번호입니다. *partition_number* 됩니다 **int**합니다. 유효한 입력은는 *partion_number* 인덱스 또는 힙의 경우 NULL, 0 또는 DEFAULT입니다. 기본값은 0입니다. 이 컨텍스트에서 NULL, 0 및 DEFAULT는 동등한 값입니다.    
    
 인덱스 또는 힙의 모든 파티션에 대한 캐시된 정보를 반환하려면 NULL을 지정합니다.    
    
 *partition_number* 는 1부터 시작 합니다. 분할 되지 않은 인덱스 또는 힙 *partition_number* 1로 설정 합니다.    
    
## <a name="table-returned"></a>반환된 테이블    
    
|열 이름|데이터 형식|설명|    
|-----------------|---------------|-----------------|    
|**database_id**|**smallint**|데이터베이스 ID입니다.|    
|**object_id**|**int**|테이블 또는 뷰의 ID입니다.|    
|**index_id**|**int**|인덱스 또는 힙의 ID입니다.<br /><br /> 0 = 힙| 
|**partition_number**|**int**|인덱스 또는 힙 내의 1부터 시작하는 파티션 번호입니다.| 
|**hobt_id**|**bigint**|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> 데이터 힙 또는 columnstore 인덱스에 대 한 내부 데이터를 추적 하는 B-트리 행 집합 ID입니다.<br /><br /> NULL-내부 columnstore 행 집합을이 아닙니다.<br /><br /> 자세한 내용은 참조 하세요. [sys.internal_partitions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)|       
|**leaf_insert_count**|**bigint**|리프 수준 삽입의 누적 횟수입니다.|    
|**leaf_delete_count**|**bigint**|리프 수준 삭제의 누적 횟수입니다. 삭제 된 레코드를 먼저 삭제할 변수로 표시 되지 않는 leaf_delete_count만 증가 됩니다. 먼저 고스팅는 삭제 된 레코드에 대 한 **leaf_ghost_count** 대신 증분됩니다.|    
|**leaf_update_count**|**bigint**|리프 수준 업데이트의 누적 횟수입니다.|    
|**leaf_ghost_count**|**bigint**|삭제하도록 표시되어 있지만 아직 제거되지 않은 리프 수준 행의 누적 개수입니다. 이 개수 유령으로 표시 하지 않아도 즉시 삭제 된 레코드를 포함 하지 않습니다. 이러한 행은 지정된 간격을 두고 정리 스레드를 통해 제거됩니다. 처리 중인 스냅샷 격리 트랜잭션으로 인해 보유된 행은 이 값에 포함되지 않습니다.|    
|**nonleaf_insert_count**|**bigint**|리프 수준 위에서 발생한 삽입의 누적 횟수입니다.<br /><br /> 0 = 힙 또는 columnstore|    
|**nonleaf_delete_count**|**bigint**|리프 수준 위에서 발생한 삭제의 누적 횟수입니다.<br /><br /> 0 = 힙 또는 columnstore|    
|**nonleaf_update_count**|**bigint**|리프 수준 위에서 발생한 업데이트의 누적 횟수입니다.<br /><br /> 0 = 힙 또는 columnstore|    
|**leaf_allocation_count**|**bigint**|인덱스 또는 힙에서 발생한 리프 수준 페이지 할당의 누적 횟수입니다.<br /><br /> 인덱스의 경우 페이지 할당은 페이지 분할에 해당됩니다.|    
|**nonleaf_allocation_count**|**bigint**|리프 수준 위에서 페이지 분할로 인해 발생한 페이지 할당의 누적 횟수입니다.<br /><br /> 0 = 힙 또는 columnstore|    
|**leaf_page_merge_count**|**bigint**|리프 수준에서 발생한 페이지 병합의 누적 횟수입니다. columnstore 인덱스의 경우 항상 0입니다.|    
|**nonleaf_page_merge_count**|**bigint**|리프 수준 위에서 발생한 페이지 병합의 누적 횟수입니다.<br /><br /> 0 = 힙 또는 columnstore|    
|**range_scan_count**|**bigint**|인덱스 또는 힙에서 시작된 범위 및 테이블 검색의 누적 횟수입니다.|    
|**singleton_lookup_count**|**bigint**|인덱스 또는 힙에서 발생한 단일 행 검색의 누적 횟수입니다.|    
|**forwarded_fetch_count**|**bigint**|전달된 레코드를 통해 인출된 행 수입니다.<br /><br /> 0 = 인덱스|    
|**lob_fetch_in_pages**|**bigint**|LOB_DATA 할당 단위에서 검색된 LOB(Large Object) 페이지의 누적 개수입니다. 이러한 페이지 형식의 열에 저장 된 데이터가 **텍스트**, **ntext**, **이미지**, **(는) 트랜잭션**, **nvarchar ( max)** , **varbinary (max)** , 및 **xml**. 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.|    
|**lob_fetch_in_bytes**|**bigint**|검색된 LOB 데이터 바이트의 누적값입니다.|    
|**lob_orphan_create_count**|**bigint**|대량 작업 중에 생성된 고아 LOB의 누적값입니다.<br /><br /> 0 = 비클러스터형 인덱스|    
|**lob_orphan_insert_count**|**bigint**|대량 작업 중에 삽입된 고아 LOB의 누적값입니다.<br /><br /> 0 = 비클러스터형 인덱스|    
|**row_overflow_fetch_in_pages**|**bigint**|ROW_OVERFLOW_DATA 할당 단위에서 검색된 행 오버플로 데이터 페이지의 누적 개수입니다.<br /><br /> 이러한 페이지는 데이터 형식의 열에 저장 된 포함 **varchar (n)** , **nvarchar (n)** 합니다 **varbinary (n)** , 및 **sql_variant** 를 행 외부로 푸시됩니다.|    
|**row_overflow_fetch_in_bytes**|**bigint**|검색된 행 오버플로 데이터 바이트의 누적값입니다.|    
|**column_value_push_off_row_count**|**bigint**|삽입되거나 업데이트된 행을 페이지에 맞추기 위해 행 외부로 밀어넣은 LOB 데이터 및 행 오버플로 데이터에 대한 열 값의 누적값입니다.|    
|**column_value_pull_in_row_count**|**bigint**|행 내부로 밀어넣은 LOB 데이터 및 행 오버플로 데이터에 대한 열 값의 누적값입니다. 업데이트 작업이 레코드의 공간을 비울 때 발생하며 LOB_DATA 또는 ROW_OVERFLOW_DATA 할당 단위에서 IN_ROW_DATA 할당 단위로 하나 이상의 행 외부 값을 밀어넣을 수 있게 됩니다.|    
|**row_lock_count**|**bigint**|요청된 행 잠금의 누적 개수입니다.|    
|**row_lock_wait_count**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 행 잠금으로 인해 대기한 누적 횟수입니다.|    
|**row_lock_wait_in_ms**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 행 잠금으로 인해 대기한 총 시간(밀리초)입니다.|    
|**page_lock_count**|**bigint**|요청된 페이지 잠금의 누적 개수입니다.|    
|**page_lock_wait_count**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 페이지 잠금으로 인해 대기한 누적 횟수입니다.|    
|**page_lock_wait_in_ms**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 페이지 잠금으로 인해 대기한 총 시간(밀리초)입니다.|    
|**index_lock_promotion_attempt_count**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 잠금 에스컬레이션을 시도한 누적 횟수입니다.|    
|**index_lock_promotion_count**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 잠금을 에스컬레이션한 누적 횟수입니다.|    
|**page_latch_wait_count**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 래치 경합으로 인해 대기한 누적 횟수입니다.|    
|**page_latch_wait_in_ms**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 래치 경합으로 인해 대기한 누적 시간(밀리초)입니다.|    
|**page_io_latch_wait_count**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 I/O 페이지 래치로 인해 대기한 누적 횟수입니다.|    
|**page_io_latch_wait_in_ms**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 페이지 I/O 래치로 인해 대기한 누적 시간(밀리초)입니다.|    
|**tree_page_latch_wait_count**|**bigint**|하위 집합 **page_latch_wait_count** 상위 수준 B-트리 페이지만 포함 하는 합니다. 힙 또는 columnstore 인덱스의 경우 항상 0입니다.|    
|**tree_page_latch_wait_in_ms**|**bigint**|하위 집합 **page_latch_wait_in_ms** 상위 수준 B-트리 페이지만 포함 하는 합니다. 힙 또는 columnstore 인덱스의 경우 항상 0입니다.|    
|**tree_page_io_latch_wait_count**|**bigint**|하위 집합 **page_io_latch_wait_count** 상위 수준 B-트리 페이지만 포함 하는 합니다. 힙 또는 columnstore 인덱스의 경우 항상 0입니다.|    
|**tree_page_io_latch_wait_in_ms**|**bigint**|하위 집합 **page_io_latch_wait_in_ms** 상위 수준 B-트리 페이지만 포함 하는 합니다. 힙 또는 columnstore 인덱스의 경우 항상 0입니다.|    
|**page_compression_attempt_count**|**bigint**|테이블, 인덱스 또는 인덱싱된 뷰의 특정 파티션에 대한 PAGE 수준 압축을 계산한 페이지 수입니다. 공간 절약 효과가 크지 않기 때문에 압축되지 않은 페이지도 포함됩니다. columnstore 인덱스의 경우 항상 0입니다.|    
|**page_compression_success_count**|**bigint**|테이블, 인덱스 또는 인덱싱된 뷰의 특정 파티션의 PAGE 압축을 사용하여 압축된 데이터 페이지 수입니다. columnstore 인덱스의 경우 항상 0입니다.|    
    
## <a name="remarks"></a>설명    
 이 동적 관리 개체는 CROSS APPLY 및 OUTER APPLY의 상호 관련된 매개 변수를 받지 않습니다.    
    
 사용할 수 있습니다 **sys.dm_db_index_operational_stats** 사용자 읽기 또는 테이블, 인덱스 또는 파티션에 쓰기 및 테이블이 나 인덱스는 상당한 I/O 작업을 발생 하는 또는 핫 식별 하기 위해 대기 해야 하는 시간의 길이 추적 하려면 스폿 합니다.    
    
 다음 열을 사용하여 경합 영역을 식별할 수 있습니다.    
    
 **테이블 또는 인덱스 파티션에 일반적인 액세스 패턴을 분석 하려면**, 이러한 열을 사용 합니다.    
    
-   **leaf_insert_count**    
    
-   **leaf_delete_count**    
    
-   **leaf_update_count**    
    
-   **leaf_ghost_count**    
    
-   **range_scan_count**    
    
-   **singleton_lookup_count**    
    
 래치 및 잠금 경합을 식별하려면 다음 열을 사용합니다.    
    
-   **page_latch_wait_count** 고 **page_latch_wait_in_ms**    
    
     이 두 열은 인덱스 또는 힙에 래치 경합이 있는지 여부와 해당 경합의 의미를 나타냅니다.    
    
-   **row_lock_count** 고 **page_lock_count**    
    
     이 두 열은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 행 및 페이지 잠금을 획득하려고 시도한 횟수를 나타냅니다.    
    
-   **row_lock_wait_in_ms** 고 **page_lock_wait_in_ms**    
    
     이 두 열은 인덱스 또는 힙에 잠금 경합이 있는지 여부와 해당 경합의 의미를 나타냅니다.    
    
 **인덱스 또는 힙 파티션에서 실제 I/o의 통계를 분석 하려면**    
    
-   **page_io_latch_wait_count** 고 **page_io_latch_wait_in_ms**    
    
     이 두 열은 인덱스 또는 힙 페이지를 메모리로 가져가기 위한 물리적 I/O가 발생했는지 여부와 I/O 발생 횟수를 나타냅니다.    
    
## <a name="column-remarks"></a>열에 대한 주의    
 에 값 **lob_orphan_create_count** 하 고 **lob_orphan_insert_count** 은 항상 같아야 합니다.    
    
 열에 값 **lob_fetch_in_pages** 하 고 **lob_fetch_in_bytes** 포괄된 열으로 하나 이상의 LOB 열이 포함 된 비클러스터형 인덱스는 0 보다 클 수 있습니다. 자세한 내용은 [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md)을 참조하세요. 마찬가지로, 열에 값 **row_overflow_fetch_in_pages** 하 고 **row_overflow_fetch_in_bytes** 푸시할 수 있는 열을 포함 하는 경우 비클러스터형 인덱스는 0 보다 클 수 행 외부에 있습니다.    
    
## <a name="how-the-counters-in-the-metadata-cache-are-reset"></a>메타데이터 캐시의 카운터를 다시 설정하는 방법    
 반환한 데이터 **sys.dm_db_index_operational_stats** 동안만 힙 또는 인덱스를 나타내는 메타 데이터 캐시 개체를 사용할 수 있습니다. 이 데이터는 영구적이지도 않고 트랜잭션 측면에서 일관되지도 않습니다. 즉, 이러한 카운터로는 인덱스가 사용되었는지 여부나 인덱스가 마지막으로 사용된 시기를 확인할 수 없습니다. 이 대 한 정보를 참조 하세요 [sys.dm_db_index_usage_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)합니다.    
    
 힙 또는 인덱스에 대한 메타데이터를 메타데이터 캐시로 가져갈 때마다 각 열의 값이 0으로 설정되며 메타데이터 캐시에서 캐시 개체가 제거될 때까지 통계가 누적됩니다. 따라서 활성 힙 또는 인덱스의 메타데이터가 항상 캐시에 있으며 누적값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 마지막으로 시작된 이후의 작업을 반영합니다. 덜 활성화된 힙 또는 인덱스에 대한 메타데이터는 사용될 때 캐시에 들어왔다 나가기를 반복합니다. 따라서 사용 가능한 값이 있을 수도 있고 없을 수도 있습니다. 인덱스를 삭제하면 해당 통계가 메모리에서 제거되고 더 이상 보고되지 않습니다. 인덱스에 대한 다른 DDL 작업으로 인해 통계의 값이 0으로 다시 설정될 수도 있습니다.    
    
## <a name="using-system-functions-to-specify-parameter-values"></a>시스템 함수를 사용하여 매개 변수 값 지정    
 사용할 수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 [DB_ID](../../t-sql/functions/db-id-transact-sql.md) 및 [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) 에 대 한 값을 지정 하는 *database_id* 하 고 *object_id* 매개 변수입니다. 그러나 이러한 함수에 유효하지 않은 값을 전달하면 의도하지 않은 결과가 발생할 수 있습니다. DB_ID 또는 OBJECT_ID를 사용할 때는 항상 유효한 ID가 반환되는지 확인합니다. 자세한 내용은 주의 섹션을 참조 하세요 [sys.dm_db_index_physical_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)합니다.    
    
## <a name="permissions"></a>사용 권한    
 다음 사용 권한이 필요합니다.    
    
-   데이터베이스 내의 지정된 개체에 대한 CONTROL 권한    
    
-   @ 개체 와일드 카드를 사용 하 여 지정된 된 데이터베이스 내의 모든 개체에 대 한 정보를 반환 하는 VIEW DATABASE STATE 권한*object_id* = NULL    
    
-   @ 데이터베이스 와일드 카드를 사용 하 여 모든 데이터베이스에 대 한 정보를 반환 하려면 VIEW SERVER STATE 권한이*database_id* = NULL    
    
 VIEW DATABASE STATE를 허용하면 특정 개체에 대해 거부된 CONTROL 권한에 관계없이 데이터베이스의 모든 개체가 반환됩니다.    
    
 VIEW DATABASE STATE를 거부하면 특정 개체에 대해 허용된 CONTROL 권한에 관계없이 데이터베이스의 모든 개체가 반환되지 않습니다. 또한, @ 데이터베이스 와일드 카드*database_id*= NULL을 지정 하면 해당 데이터베이스가 생략 됩니다.    
    
 자세한 내용은 [동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)합니다.    
    
## <a name="examples"></a>예    
    
### <a name="a-returning-information-for-a-specified-table"></a>A. 지정된 테이블에 대한 정보 반환    
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 `Person.Address` 테이블의 모든 인덱스 및 파티션에 대한 정보를 반환합니다. 이 쿼리를 실행하려면 적어도 `Person.Address` 테이블에 대한 CONTROL 권한이 필요합니다.    
    
> [!IMPORTANT]    
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 DB_ID 및 OBJECT_ID를 사용해 매개 변수 값이 반환된 경우 유효한 ID가 반환되는지 항상 확인합니다. 존재하지 않는 이름을 입력하거나 철자를 잘못 입력하는 등의 이유로 데이터베이스 또는 개체 이름을 찾을 수 없으면 두 함수 모두 NULL을 반환합니다. **sys.dm_db_index_operational_stats** 함수는 NULL을 모든 데이터베이스나 모든 개체를 지정하는 와일드카드 값으로 해석합니다. 이는 의도하지 않은 결과일 수 있으므로 이 섹션의 예에서는 안전하게 데이터베이스 및 개체 ID를 확인하는 방법을 보여 줍니다.    
    
```    
DECLARE @db_id int;    
DECLARE @object_id int;    
SET @db_id = DB_ID(N'AdventureWorks2012');    
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');    
IF @db_id IS NULL     
  BEGIN;    
    PRINT N'Invalid database';    
  END;    
ELSE IF @object_id IS NULL    
  BEGIN;    
    PRINT N'Invalid object';    
  END;    
ELSE    
  BEGIN;    
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);    
  END;    
GO    
    
```    
    
### <a name="b-returning-information-for-all-tables-and-indexes"></a>2\. 모든 테이블 및 인덱스에 대한 정보 반환    
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내의 모든 테이블 및 인덱스에 대한 정보를 반환합니다. 이 쿼리를 실행 하려면 VIEW SERVER STATE 권한이 필요.    
    
```    
SELECT * FROM sys.dm_db_index_operational_stats( NULL, NULL, NULL, NULL);    
GO    
    
```    
    
## <a name="see-also"></a>관련 항목    
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)     
 [인덱스 관련 동적 관리 뷰 및 함수 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)     
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)     
 [sys.dm_db_index_usage_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)     
 [sys.dm_os_latch_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)     
 [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)     
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)     
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)    
    
  

