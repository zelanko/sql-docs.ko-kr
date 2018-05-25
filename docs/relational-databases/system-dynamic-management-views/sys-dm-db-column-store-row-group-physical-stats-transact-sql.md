---
title: sys.dm_db_column_store_row_group_physical_stats (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9f48268c800345ed66f065e444a8d7cfe09a6a30
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdbcolumnstorerowgroupphysicalstats-transact-sql"></a>sys.dm_db_column_store_row_group_physical_stats (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  모든 현재 데이터베이스에 columnstore 인덱스에 대 한 현재 행 그룹 수준 정보를 제공합니다.  
  
 이 영역 카탈로그 뷰를 사용 하 고 확장 [sys.column_store_row_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|기본 테이블의 ID입니다.|  
|**index_id**|**int**|이 columnstore 인덱스의 ID *object_id* 테이블입니다.|  
|**partition_number**|**int**|ID를 보유 하는 테이블 파티션 *row_group_id*합니다. partition_number를 사용하여 DMV를 sys.partitions에 조인할 수 있습니다.|  
|**row_group_id**|**int**|이 행 그룹의 ID입니다. 분할 된 테이블에는이 파티션 내에서 고유 합니다.<br /><br /> 메모리 내 꼬리에 대 한-1입니다.|  
|**delta_store_hobt_id**|**bigint**|델타 저장소의 행 그룹에 대 한 hobt_id 합니다.<br /><br /> 델타 저장소에 행 그룹이 없는 경우 NULL입니다.<br /><br /> 메모리 내 테이블의 마지막 부분에 대 한 NULL입니다.|  
|**상태**|**tinyint**|연결 된 ID 번호 *state_description*합니다.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = 열기<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = 삭제 표시<br /><br /> 압축은 메모리 내 테이블에 적용 되는 유일한 상태입니다.|  
|**state_desc**|**nvarchar(60)**|행 그룹 상태 설명:<br /><br /> 작성 중인 보이지 않는 – A 행 그룹입니다. 예를 들어: <br />Columnstore에서 행 그룹 데이터를 압축 하는 동안 표시 되지 됩니다. 압축 메타 데이터 스위치 변경 완료 되 면 보이지 않는에서 삭제 표시 하려면 "에서" deltastore 행 그룹의 상태와 압축, columnstore 행의 상태가 그룹화 합니다.<br /><br /> OPEN – 새 행을 수락 하는 deltastore 행 그룹입니다. 열린 행 그룹은 columnstore 형식으로 압축되지 않았고 여전히 rowstore 형식입니다.<br /><br /> CLOSED – 행의 최대 수를 포함 하 고 columnstore로 압축 tuple mover 프로세스에 대 한 대기 하는 델타 저장소의 행 그룹입니다.<br /><br /> 압축 되어 columnstore 압축으로 압축 되며 columnstore에 저장 된 행 그룹입니다.<br /><br /> TOMBSTONE – 행 그룹이 있는 deltastore에 였던 이며 더 이상 사용 합니다.|  
|**total_rows**|**bigint**|행 그룹에 저장 된 실제 행 수입니다. 압축 된 행 그룹을 삭제 표시 된 행 포함 됩니다.|  
|**deleted_rows**|**bigint**|삭제 하도록 표시 된 압축 된 행 그룹에 물리적으로 저장 된 행 수입니다.<br /><br /> 델타 저장소에 있는 행 그룹에 대 한 0입니다.|  
|**size_in_bytes**|**bigint**|이 행 그룹의 모든 페이지를 바이트 단위로 결합 된 크기입니다. 이 크기는 메타 데이터 또는 공유 사전에 저장 하는 데 필요한 크기를 포함 되지 않습니다.|  
|**trim_reason**|**tinyint**|이유는 압축 행 그룹에 있어야 트리거되는 최대 행 개수 보다 작습니다.<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1-NO_TRIM<br /><br /> 2-BULKLOAD<br /><br /> 3 – REORG<br /><br /> 4 – DICTIONARY_SIZE<br /><br /> 5 – MEMORY_LIMITATION<br /><br /> 6-RESIDUAL_ROW_GROUP<br /><br /> 7  -  STATS_MISMATCH<br /><br /> 8GB – 길이가 긴|  
|**trim_reason_desc**|**nvarchar(60)**|에 대 한 설명 *trim_reason*합니다.<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION:의 이전 버전에서 업그레이드할 때 발생 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.<br /><br /> 1-NO_TRIM: 행 그룹을 잘라내지 않습니다. 1,048,476 행의 최대 행 그룹으로 압축 되었습니다.  행 수가 행 subsset 델타 행 그룹이 닫힌 후에 삭제 된 경우 작을 수 없습니다.<br /><br /> 2-BULKLOAD: 대량 로드 일괄 처리 크기는 행 수 제한.<br /><br /> 3 – REORG: REORG 명령의 일환으로 압축을 강제합니다.<br /><br /> 4 – DICTIONARY_SIZE: 사전 크기 증가 너무 크기 때문에 모든 행을 함께 압축 합니다.<br /><br /> 5 – MEMORY_LIMITATION: 사용 가능한 메모리가 부족 모든 행을 함께 압축 합니다.<br /><br /> 6-RESIDUAL_ROW_GROUP: 닫힌 마지막 행 그룹의 일부로 행 < 1 백만 인덱스 작성 작업 중<br /><br /> STATS_MISMATCH:만 columnstore에 대 한 메모리 내 테이블에 있습니다. Stats 올바르게 표시 되는 경우 없습니다 > = 1 백만 꼬리에 정식된 행 하지만 더 적은 알게, 압축 된 행 그룹 < 1 백만 개의 행을 갖습니다<br /><br /> 길이가 긴:만 columnstore에 대 한 메모리 내 테이블에 있습니다. 마지막 일괄 처리 나머지 행 수가 100 k 1 백만 사이의 경우 압축 되는 꼬리에 > 1 백만 정규화 된 행이 하는 경우|  
|**transition_to_compressed_state**|tinyint|Columnstore의 압축 된 상태로이 rowgroup이 deltastore에서 이동 방법을 보여 줍니다.<br /><br /> 1-NOT_APPLICABLE<br /><br /> 2-INDEX_BUILD<br /><br /> 3 – TUPLE_MOVER<br /><br /> 4 – REORG_NORMAL<br /><br /> 5 – REORG_FORCED<br /><br /> 6-BULKLOAD<br /><br /> 7-병합|  
|**transition_to_compressed_state_desc**|nvarchar(60)|NOT_APPLICABLE – 작업을 deltastore에 적용 되지 않습니다. 로 업그레이드 하기 전에 압축 된 행 그룹 또는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 는 쿼리에서 기록이 유지 되지 않습니다.<br /><br /> INDEX_BUILD – 인덱스를 만들거나 인덱스를 다시 압축 행 그룹.<br /><br /> TUPLE_MOVER – 백그라운드에서 실행 tuple mover 압축 행 그룹. 행 그룹 열에서 상태를 닫힘으로 변경 후 이런 상황이 발생 합니다.<br /><br /> REORG_NORMAL 재구성 작업이, ALTER INDEX... REORG 닫힌된 행 그룹을 deltastore에서 columnstore로 이동 합니다. Tuple mover 행 그룹을 이동 하려면 시간 전에이 발생 했습니다.<br /><br /> REORG_FORCED –이 rowgroup이 deltastore에 열려 있는 인시던트 였으며 전체 행 수를 하기 전에 columnstore로 강제 적용 된.<br /><br /> BULKLOAD – 대량 로드 작업 deltastore를 사용 하지 않고 직접 행 그룹을 압축 합니다.<br /><br /> 병합 – 병합 작업이 하나 이상의 rowgroup이 행이 그룹으로 통합 하 고 columnstore 압축을 수행 합니다.|  
|**has_vertipaq_optimization**|bit|Vertipaq 최적화 하려면 더 높은 압축률을 행 그룹의 행의 순서를 조정 하 여 columnstore 압축을 개선 합니다. 이 최적화는 대부분의 경우에서 자동으로 발생합니다. 다음 두 가지 경우 Vertipaq 최적화 사용 되지 않습니다.<br/>  a. 델타 rowgroup이 columnstore로 이동 하 고 하나 이상의 비클러스터형 인덱스는 columnstore 인덱스 기능에이 경우 Vertipaq 최적화는 건너뜁니다 최소화 매핑 인덱스;에 대 한 변경 하려면<br/> b. 메모리 액세스에 최적화 된 테이블의 columnstore 인덱스에 대 한 <br /><br /> 0 = 아니요<br /><br /> 1 = 예|  
|**generation**|bigint|이 행 그룹과 연결 된 행 그룹 생성 합니다.|  
|**created_time**|datetime2|이 행 그룹을 만들 때 클럭 시간입니다.<br /><br /> NULL – 메모리 내 테이블의 columnstore 인덱스입니다.|  
|**closed_time**|datetime2|이 행 그룹이 닫힌 경우에 대 한 클록 시간입니다.<br /><br /> NULL – 메모리 내 테이블의 columnstore 인덱스입니다.|  
  
## <a name="results"></a>결과  
 현재 데이터베이스의 각 행 그룹에 대해 한 행을 반환합니다.  
  
## <a name="permissions"></a>Permissions  
 다음과 같은 사용 권한이 필요합니다.  
  
-   테이블에 대 한 CONTROL 권한  
  
-   데이터베이스에 대 한 VIEW DATABASE STATE 권한  
  
## <a name="examples"></a>예  
  
### <a name="a-calculate-fragmentaton-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>1. Fragmentaton 다시 구성 하거나 columnstore 인덱스 다시 작성 하는 시점을 결정할 수를 계산 합니다.  
 Columnstore 인덱스에 대 한 삭제 된 행의 백분율은 행 그룹의 조각화에 대 한 유용한 척도입니다. 조각화가 경우 20% 이상을 삭제 된 행을 제거 하는 것이 좋습니다.  예제를 보려면 [Columnstore 인덱스 조각 모음](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)합니다.  
  
 이 예제에서는 조인 **sys.dm_db_column_store_row_group_physical_stats** 다른 시스템으로 계산 되며 테이블의 `Fragmentation` 현재 데이터베이스의 각 행 그룹의 효율성 예상치로 열입니다.     주석 하이픈의 앞 단일 테이블 제거에서 정보를 찾으려면는 **여기서** 절에 테이블 이름을 제공 합니다.  
  
```sql  
SELECT i.object_id,   
    object_name(i.object_id) AS TableName,   
    i.name AS IndexName,   
    i.index_id,   
    i.type_desc,   
    CSRowGroups.*,  
    100*(ISNULL(deleted_rows,0))/total_rows AS 'Fragmentation'  
FROM sys.indexes AS i  
JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id AND i.index_id = CSRowGroups.index_id   
-- WHERE object_name(i.object_id) = 'table_name'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_dictionaries &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
