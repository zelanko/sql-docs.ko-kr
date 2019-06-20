---
title: sys.dm_db_column_store_row_group_physical_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_column_store_row_group_physical_stats_TSQL
- sys.dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_column_store_row_group_physical_stats
- sys.dm_db_column_store_row_group_physical_stats dynamic management view
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1460ef53098a9cdd7cf8bb1672c45cfd27adff57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822732"
---
# <a name="sysdmdbcolumnstorerowgroupphysicalstats-transact-sql"></a>sys.dm_db_column_store_row_group_physical_stats (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  모든 현재 데이터베이스에서 columnstore 인덱스에 대 한 현재 행 그룹 수준 정보를 제공합니다.  
  
 이 카탈로그 뷰를 확장 [sys.column_store_row_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|기본 테이블의 ID입니다.|  
|**index_id**|**int**|이 columnstore 인덱스의 ID *object_id* 테이블입니다.|  
|**partition_number**|**int**|ID를 보유 하는 테이블 파티션의 *row_group_id*합니다. partition_number를 사용하여 DMV를 sys.partitions에 조인할 수 있습니다.|  
|**row_group_id**|**int**|이 행 그룹의 ID입니다. 분할 된 테이블에는이 파티션 내에서 고유 합니다.<br /><br /> 메모리 내 꼬리가-1입니다.|  
|**delta_store_hobt_id**|**bigint**|델타 저장소에 행 그룹은 hobt_id 합니다.<br /><br /> 행 그룹 델타 저장소에 없는 경우 NULL입니다.<br /><br /> 메모리 내 테이블의 꼬리에 대 한 NULL입니다.|  
|**state**|**tinyint**|연결 된 ID 번호 *state_description*합니다.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = 삭제 표시<br /><br /> 압축은 메모리 내 테이블에 적용 되는 유일한 상태 이기 때문입니다.|  
|**state_desc**|**nvarchar(60)**|행 그룹 상태 설명:<br /><br /> 빌드되는 보이지 않는-A 행 그룹입니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다. <br />Columnstore에서 행 그룹 데이터를 압축 하는 동안 표시 되지 됩니다. 압축에는 메타 데이터 스위치 변경 완료 되 면 columnstore 행의 상태에서 그룹을 보이지 않는 압축, 및 삭제 표시 "에서" deltastore 행 그룹의 상태.<br /><br /> 열림-새 행을 수락 하는 deltastore 행 그룹입니다. 열린 행 그룹은 columnstore 형식으로 압축되지 않았고 여전히 rowstore 형식입니다.<br /><br /> 닫힘-행의 최대 수를 포함 하 고 columnstore로 압축할 tuple mover 프로세스에 대 한 기다리고 있는 델타 저장소에 행 그룹입니다.<br /><br /> 압축으로 columnstore 압축으로 압축 되 고 columnstore에 저장 되는 행 그룹.<br /><br /> 삭제 표시-는 deltastore에 있는 이전의 이며 더 이상 행 그룹을 사용 합니다.|  
|**total_rows**|**bigint**|행 그룹에 저장 된 실제 행 수입니다. 압축 된 행 그룹에 대 한 삭제 된 행으로 표시 된 포함 됩니다.|  
|**deleted_rows**|**bigint**|삭제 표시 되는 압축 된 행 그룹에 물리적으로 저장 하는 행 수입니다.<br /><br /> 델타 저장소에 있는 행 그룹에 대 한 0입니다.|  
|**size_in_bytes**|**bigint**|이 행 그룹의 모든 페이지를 바이트 단위로 결합 된 크기입니다. 이 크기는 메타 데이터 또는 공유 사전 제외를 저장 하는 데 필요한 크기로 포함 되지 않습니다.|  
|**trim_reason**|**tinyint**|압축 행 그룹에 있어야 하는 이유는 최대 행 개수 보다 작은 경우<br /><br /> 0-UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1-NO_TRIM<br /><br /> 2-BULKLOAD<br /><br /> 3-REORG<br /><br /> 4 - DICTIONARY_SIZE<br /><br /> 5-MEMORY_LIMITATION<br /><br /> 6 - RESIDUAL_ROW_GROUP<br /><br /> 7  -  STATS_MISMATCH<br /><br /> 8 비트 길이가 긴|  
|**trim_reason_desc**|**nvarchar(60)**|에 대 한 설명을 *trim_reason*합니다.<br /><br /> 0-UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION: 이전 버전에서 업그레이드 하는 경우에 발생 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.<br /><br /> 1-NO_TRIM: 행 그룹이 잘리지 되었습니다. 1,048,476 행의 최대 행 그룹 압축 되었습니다.  행 수가 행 subsset 델타 행 그룹이 닫힌 후에 삭제 된 경우 작을 수 없습니다.<br /><br /> 2-BULKLOAD: 대량 로드 일괄 처리 크기는 행 수가 제한 됩니다.<br /><br /> 3-REORG:  REORG 명령의 일환으로 압축을 강제 합니다.<br /><br /> 4-DICTIONARY_SIZE: 사전 크기의 모든 행을 함께 압축 하기에 너무 큰 증가 합니다.<br /><br /> 5-MEMORY_LIMITATION: 모든 행을 함께 압축에 사용 가능한 메모리가 부족 합니다.<br /><br /> 6 - RESIDUAL_ROW_GROUP:  인덱스 작성 작업 중에 백만 행 < 1을 사용 하 여 마지막 행 그룹의 일부로 닫는<br /><br /> STATS_MISMATCH: 메모리 내 테이블에서 columnstore에 대해서만 통계 올바르게 표시 되는 경우 없습니다 > = 1 백만 정규화 된 행 끝에 더 적은 알게 하지만 압축 된 rowgroup에 백만 행 < 1 해야 합니다.<br /><br /> 길이가 긴: 메모리 내 테이블에서 columnstore에 대해서만 마지막 일괄 처리 나머지 행 수가 100,000 개 사이의 1 백만 경우 압축 되는 비상 > 1 백만 정규화 된 행에 하는 경우|  
|**transition_to_compressed_state**|TINYINT|Columnstore에 압축 된 상태로이 rowgroup이 deltastore에서 이동 하는 방법을 보여 줍니다.<br /><br /> 1-NOT_APPLICABLE<br /><br /> 2 - INDEX_BUILD<br /><br /> 3-TUPLE_MOVER<br /><br /> 4 - REORG_NORMAL<br /><br /> 5 - REORG_FORCED<br /><br /> 6-BULKLOAD<br /><br /> 7-병합|  
|**transition_to_compressed_state_desc**|nvarchar(60)|NOT_APPLICABLE-작업은 deltastore에는 적용 되지 않습니다. 로 업그레이드 하기 전에 압축 된 행 그룹 또는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 경우 기록을 유지 되지 않습니다.<br /><br /> INDEX_BUILD-인덱스를 만들거나 인덱스를 다시 압축 행 그룹.<br /><br /> TUPLE_MOVER-백그라운드에서 실행 하는 튜플 이동 기 압축 행 그룹. 행 그룹 오픈에서 닫힘 상태를 변경 후 이런 상황이 발생 합니다.<br /><br /> REORG_NORMAL-재구성 작업을 ALTER INDEX... REORG 닫힌된 행 그룹을 deltastore에서 columnstore로 이동 합니다. 튜플 이동 기가 행 그룹을 이동 하는 시간 전에이 발생 했습니다.<br /><br /> REORG_FORCED-이 rowgroup이 deltastore에 열려 있었던 및 전체 행 수를 하기 전에 columnstore로 강제 적용 된 합니다.<br /><br /> BULKLOAD-대량 로드 작업을 deltastore를 사용 하지 않고 직접 행 그룹을 압축 합니다.<br /><br /> 병합-병합 작업을이 행 그룹에 하나 이상의 rowgroup을 통합 한 다음 columnstore 압축을 수행 합니다.|  
|**has_vertipaq_optimization**|bit|Vertipaq 최적화 높은 압축을 달성 하려면 행 그룹의 행 순서를 조정 하 여 columnstore 압축을 향상 시킵니다. 이 최적화는 대부분의 경우에서 자동으로 발생합니다. 두 가지 사례가 Vertipaq 최적화는 사용 되지 않습니다.<br/>  a. 델타 행 그룹을 columnstore로 이동 하 고 하나 이상의 비클러스터형 인덱스에 있는 columnstore 인덱스-이 경우 Vertipaq 최적화는 건너뜁니다 최소화 매핑 인덱스를 변경 하려면<br/> b. 메모리 최적화 테이블의 columnstore 인덱스에 대 한 <br /><br /> 0 = 아니요<br /><br /> 1 = 예|  
|**generation**|BIGINT|이 행 그룹과 행 그룹 생성 합니다.|  
|**created_time**|Datetime2|이 행 그룹을 만들 때에 대 한 클럭 시간입니다.<br /><br /> 메모리 내 테이블에 columnstore 인덱스에 대 한 NULL입니다.|  
|**closed_time**|Datetime2|이 행 그룹이 닫힌 경우에 대 한 클럭 시간입니다.<br /><br /> 메모리 내 테이블에 columnstore 인덱스에 대 한 NULL입니다.|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="results"></a>결과  
 현재 데이터베이스의 각 행 그룹에 대 한 하나의 행을 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 다음과 같은 사용 권한이 필요합니다.  
  
-   테이블에 대 한 CONTROL 권한입니다.  
  
-   데이터베이스에 VIEW DATABASE STATE 권한입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calculate-fragmentaton-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>1. Reorganize는 columnstore 인덱스 다시 작성 하는 시기를 결정 fragmentaton를 계산 합니다.  
 Columnstore 인덱스에 대해 삭제 된 행의 백분율 rowgroup의 조각화가 대 한 적절 한 측정값입니다. 경우 조각화를 20% 이상이 삭제 된 행을 제거 하는 것이 좋습니다.  예제를 보려면 [Columnstore 인덱스 조각 모음](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)합니다.  
  
 이 예제에서는 조인 **sys.dm_db_column_store_row_group_physical_stats** 다른 시스템으로 계산 되며 테이블을 `Fragmentation` 현재 데이터베이스의 각 행 그룹의 효율성 예상치로 열입니다.     앞의 주석 하이픈을 단일 테이블 제거에 대 한 정보를 찾을 수 합니다 **여기서** 절 하 고 테이블 이름을 제공 합니다.  
  
```sql  
SELECT i.object_id,   
    object_name(i.object_id) AS TableName,   
    i.name AS IndexName,   
    i.index_id,   
    i.type_desc,   
    CSRowGroups.*,  
    100*(ISNULL(deleted_rows,0))/NULLIF(total_rows,0) AS 'Fragmentation'
FROM sys.indexes AS i  
JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id AND i.index_id = CSRowGroups.index_id   
-- WHERE object_name(i.object_id) = 'table_name'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_dictionaries &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
