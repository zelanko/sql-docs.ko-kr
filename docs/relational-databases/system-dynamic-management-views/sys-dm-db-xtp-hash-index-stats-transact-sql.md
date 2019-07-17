---
title: sys.dm_db_xtp_hash_index_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_hash_index_stats
- sys.dm_db_xtp_hash_index_stats_TSQL
- dm_db_xtp_hash_index_stats
- dm_db_xtp_hash_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_hash_index_stats (dynamic management view)
ms.assetid: 45969884-cd61-48e8-aee5-c725c78e3e4c
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2bbaaaa6770c5644da227c7e64a9ff9e0fc2c13
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026845"
---
# <a name="sysdmdbxtphashindexstats-transact-sql"></a>sys.dm_db_xtp_hash_index_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  이러한 통계는 버킷 수를 이해하고 조정하는 데 유용합니다. 또한 인덱스 키에 중복이 많은 경우 사례를 검색하는 데 사용할 수 있습니다.  
  
 큰 평균 체인 길이는 동일한 버킷에 많은 행이 해시되었다는 것을 나타냅니다. 이로 인해 다음이 발생할 수 있습니다.  
  
-   빈 버킷 수가 적거나 평균 및 최대 체인 길이가 비슷한 경우 총 버킷 수가 너무 적을 가능성이 높습니다. 그러면 많은 다른 인덱스 키가 동일한 버킷으로 해시됩니다.  
  
-   빈 버킷 수가 많거나 최대 체인 길이가 평균 체인 길이 대비 높은 경우에는 인덱스 키 값이 중복된 행이 많거나 키 값이 왜곡되었을 가능성이 높습니다. 인덱스 키 값이 동일한 모든 행은 동일한 버킷으로 해시되므로 해당 버킷의 체인 길이는 깁니다.  
  
긴 체인 길이는 SELECT 및 INSERT를 포함하여 개별 행에 대한 모든 DML 작업의 성능에 상당한 영향을 미칠 수 있습니다. 빈 버킷 수가 많은 짧은 체인 길이는 bucket_count가 너무 높다는 것을 나타냅니다. 이것은 인덱스 스캔 성능을 저하시킵니다.  
  
> [!WARNING]
> **sys.dm_db_xtp_hash_index_stats** 전체 테이블을 검색 합니다. 따라서 데이터베이스에 큰 테이블이 있는 경우 **sys.dm_db_xtp_hash_index_stats** 실행 시간이 오래 걸릴 수 있습니다.  
  
자세한 내용은 [메모리 최적화 테이블의 해시 인덱스](../../relational-databases/sql-server-index-design-guide.md#hash_index)합니다.  
  
|열 이름|형식|설명|  
|-----------------|----------|-----------------|  
|object_id|**int**|부모 테이블의 개체 ID입니다.|  
|xtp_object_id|**bigint**|메모리 최적화 테이블의 ID입니다.|  
|index_id|**int**|인덱스 ID입니다.|  
|total_bucket_count|**bigint**|인덱스에서 해시 버킷의 총 수입니다.|  
|empty_bucket_count|**bigint**|인덱스에서 빈 해시 버킷의 총 수입니다.|  
|avg_chain_length|**bigint**|인덱스에서 모든 해시 버킷의 낮은 체인 평균 길이입니다.|  
|max_chain_length|**bigint**|해시 버킷에 있는 행 체인의 최대 길이입니다.|  
|xtp_object_id|**bigint**|메모리 최적화 테이블에 해당 하는 메모리 내 OLTP 개체 ID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 VIEW DATABASE STATE 권한이 필요합니다.  

## <a name="examples"></a>예  
  
### <a name="a-troubleshooting-hash-index-bucket-count"></a>A. 해시 인덱스 버킷 수 문제 해결

기존 테이블의 해시 인덱스 버킷 수 문제를 해결 하려면 다음 쿼리를 사용할 수 있습니다. 쿼리는 사용자 테이블에서 모든 해시 인덱스의 체인 길이 및 빈 버킷 백분율에 대 한 통계를 반환합니다.

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
``` 

이 쿼리의 결과 해석 하는 방법에 대 한 자세한 내용은 참조 하세요. [메모리 최적화 테이블의 해시 인덱스 문제 해결](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) 합니다.  

### <a name="b-hash-index-statistics-for-internal-tables"></a>2\. 내부 테이블에 대 한 해시 인덱스 통계

특정 기능 해시 인덱스의 경우 예를 들어 메모리 최적화 테이블에서 columnstore 인덱스를 활용 하는 내부 테이블을 사용 합니다. 다음 쿼리는 사용자 테이블에 연결 된 내부 테이블에 해시 인덱스에 대 한 통계를 반환 합니다.

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [user_table],
    ia.type_desc as [internal_table_type],
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type!=1
  ORDER BY [user_table], [internal_table_type], [index]; 
```

내부 테이블 인덱스의 BUCKET_COUNT를 변경할 수 없습니다, 따라서이 쿼리의 출력 고려해 야 정보만 note 합니다. 사용자가 조치할 필요는 없습니다.  

이 쿼리는 내부 테이블의 해시 인덱스를 활용 하는 기능을 사용 하지 않는 행을 반환 하려면 사용할 수 없습니다. 다음 메모리 최적화 테이블에 columnstore 인덱스를 포함합니다. 이 테이블을 만든 후 내부 테이블에 해시 인덱스가 표시 됩니다.

```sql
  CREATE TABLE dbo.table_columnstore
  (
    c1 INT NOT NULL PRIMARY KEY NONCLUSTERED,
    INDEX ix_columnstore CLUSTERED COLUMNSTORE
  ) WITH (MEMORY_OPTIMIZED=ON)
```

## <a name="see-also"></a>관련 항목  
 [메모리 최적화 테이블 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
