---
description: sys.dm_db_column_store_row_group_physical_stats (Transact-sql)
title: sys.dm_db_column_store_row_group_physical_stats (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ddbed928d4d7ef379b7d4c164ffcc150f035b8d4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475044"
---
# <a name="sysdm_db_column_store_row_group_physical_stats-transact-sql"></a>sys.dm_db_column_store_row_group_physical_stats (Transact-sql)


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

현재 데이터베이스의 모든 columnstore 인덱스에 대 한 현재 행 그룹 수준 정보를 제공 합니다.  

그러면 [transact-sql&#41;&#40;sys.column_store_row_groups ](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)카탈로그 뷰가 확장 됩니다.  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|기본 테이블의 ID입니다.|  
|**index_id**|**int**|*Object_id* 테이블에 대 한이 columnstore 인덱스의 ID입니다.|  
|**partition_number**|**int**|*Row_group_id* 를 보유 하는 테이블 파티션의 ID입니다. partition_number를 사용하여 DMV를 sys.partitions에 조인할 수 있습니다.|  
|**row_group_id**|**int**|이 행 그룹의 ID입니다. 분할 된 테이블의 경우 값은 파티션 내에서 고유 합니다.<br /><br /> -메모리 내 꼬리의 경우-1입니다.|  
|**delta_store_hobt_id**|**bigint**|델타 저장소의 행 그룹에 대 한 hobt_id입니다.<br /><br /> 행 그룹이 델타 저장소에 없는 경우 NULL입니다.<br /><br /> 메모리 내 테이블의 꼬리에 대해 NULL입니다.|  
|**state**|**tinyint**|*State_description* 연결 된 ID 번호입니다.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = 삭제 표시<br /><br /> 압축은 메모리 내 테이블에 적용 되는 유일한 상태입니다.|  
|**state_desc**|**nvarchar(60)**|행 그룹 상태에 대 한 설명입니다.<br /><br /> 0-보이지 않음-작성 중인 행 그룹입니다. 예를 들어: <br />데이터를 압축 하는 동안 columnstore의 행 그룹은 표시 되지 않습니다. 압축이 완료 되 면 메타 데이터 스위치는 columnstore 행 그룹의 상태를 보이지 않음에서 압축 됨으로 변경 하 고 deltastore 행 그룹의 상태를 닫힘에서 삭제 표시로 변경 합니다.<br /><br /> 1-OPEN-새 행을 수락 하는 deltastore 행 그룹입니다. 열린 행 그룹은 columnstore 형식으로 압축되지 않았고 여전히 rowstore 형식입니다.<br /><br /> 2-닫힘-최대 행 수를 포함 하는 델타 저장소의 행 그룹으로, 튜플 이동 기 프로세스가 columnstore로 압축 될 때까지 대기 합니다.<br /><br /> 3-압축-columnstore 압축으로 압축 되 고 columnstore에 저장 되는 행 그룹입니다.<br /><br /> 4-삭제 표시-이전에 deltastore에 있던 행 그룹이 더 이상 사용 되지 않습니다.|  
|**total_rows**|**bigint**|행 그룹에 물리적으로 저장 된 행의 수입니다. 압축 된 행 그룹의 경우 삭제 된 것으로 표시 된 행을 포함 합니다.|  
|**deleted_rows**|**bigint**|삭제되도록 표시된 압축된 행 그룹에 물리적으로 저장된 행의 수입니다.<br /><br /> 델타 저장소에 있는 행 그룹의 경우 0입니다.|  
|**size_in_bytes**|**bigint**|이 행 그룹에 있는 모든 페이지의 조합 된 크기 (바이트)입니다. 이 크기에는 메타 데이터 또는 공유 사전을 저장 하는 데 필요한 크기가 포함 되지 않습니다.|  
|**trim_reason**|**tinyint**|압축 된 행 그룹을 트리거한 행의 최대 개수 보다 작은 이유입니다.<br /><br /> 0-UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1-NO_TRIM<br /><br /> 2-BULKLOAD<br /><br /> 3-REORG<br /><br /> 4-DICTIONARY_SIZE<br /><br /> 5-MEMORY_LIMITATION<br /><br /> 6-RESIDUAL_ROW_GROUP<br /><br /> 7-STATS_MISMATCH<br /><br /> 8-SPILLOVER<br /><br /> 9-AUTO_MERGE|  
|**trim_reason_desc**|**nvarchar(60)**|*Trim_reason* 에 대 한 설명입니다.<br /><br /> 0-UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION: 이전 버전의에서 업그레이드 하는 경우 발생 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.<br /><br /> 1-NO_TRIM: 행 그룹이 잘리지 않았습니다. 행 그룹이 최대 1048576 행으로 압축 되었습니다.  델타 행 그룹 닫힌 후 행의 하위 집합이 삭제 된 경우 행 수가 줄어들 수 있습니다.<br /><br /> 2-BULKLOAD: 대량 로드 일괄 처리 크기는 행 수를 제한 합니다.<br /><br /> 3-REORG: REORG 명령의 일부로 강제 압축 합니다.<br /><br /> 4-DICTIONARY_SIZE: 사전 크기가 너무 커서 모든 행을 함께 압축할 수 없습니다.<br /><br /> 5-MEMORY_LIMITATION: 모든 행을 함께 압축 하는 데 사용할 수 있는 메모리가 부족 합니다.<br /><br /> 6-RESIDUAL_ROW_GROUP: 인덱스 작성 작업 중에 < 100만 행이 있는 마지막 행 그룹의 일부로 닫힘<br /><br /> 7-STATS_MISMATCH: 메모리 내 테이블의 columnstore에만 해당 합니다. 통계에 >= 100만의 정규화 된 행이 정확 하 게 표시 되어 있지만 더 적으면 압축 된 행 그룹에 < 100만 행이 포함 됩니다.<br /><br /> 8-SPILLOVER: 메모리 내 테이블의 columnstore에만 해당 합니다. Tail에 > 100만의 정규화 된 행이 있는 경우 해당 수가 10만에서 100만 사이인 경우 마지막 일괄 처리 남은 행이 압축 됩니다.<br /><br /> 9-AUTO_MERGE: 백그라운드에서 실행 중인 튜플 이동 기 병합 작업이 하나 이상의 행 그룹을이 행 그룹 통합 했습니다.|  
|**transition_to_compressed_state**|tinyint|이 행 그룹가 columnstore의 deltastore에서 압축 된 상태로 이동 하는 방법을 보여 줍니다.<br /><br /> 1-NOT_APPLICABLE<br /><br /> 2-INDEX_BUILD<br /><br /> 3-TUPLE_MOVER<br /><br /> 4-REORG_NORMAL<br /><br /> 5-REORG_FORCED<br /><br /> 6-BULKLOAD<br /><br /> 7-병합|  
|**transition_to_compressed_state_desc**|nvarchar(60)| 1-NOT_APPLICABLE-작업이 deltastore에 적용 되지 않습니다. 또는로 업그레이드 하기 전에 행 그룹이 압축 되었으므로 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 기록이 유지 되지 않습니다.<br /><br /> 2-INDEX_BUILD-행 그룹 압축 된 인덱스 만들기 또는 인덱스 다시 작성.<br /><br /> 3-TUPLE_MOVER-백그라운드에서 실행 중인 튜플 이동 기가 행 그룹을 압축 했습니다. 튜플 이동 기는 행 그룹 상태가 열림에서 닫힘으로 변경 된 후에 발생 합니다.<br /><br /> 4-REORG_NORMAL-재구성 작업, ALTER INDEX ... REORG는 CLOSED 행 그룹를 deltastore에서 columnstore로 이동 했습니다. 이는 튜플 이동 기가 행 그룹을 이동 하는 데 시간이 초과 되기 전에 발생 했습니다.<br /><br /> 5-REORG_FORCED-이 행 그룹는 deltastore에서 열려 있으며 전체 행 수를 포함 하기 전에 columnstore에 강제 적용 되었습니다.<br /><br /> 6-BULKLOAD-대량 로드 작업은 deltastore를 사용 하지 않고 직접 행 그룹을 압축 합니다.<br /><br /> 7-병합-병합 작업에서 하나 이상의 행 그룹을이 행 그룹 통합 한 다음 columnstore 압축을 수행 했습니다.|  
|**has_vertipaq_optimization**|bit|VertiPaq 최적화는 행 그룹의 행 순서를 다시 정렬 하 여 더 높은 압축을 얻도록 columnstore 압축을 향상 시킵니다. 이러한 최적화는 대부분의 경우 자동으로 수행 됩니다. VertiPaq 최적화를 사용 하지 않는 두 가지 경우는 다음과 같습니다.<br/>  a. 델타 행 그룹이 columnstore로 이동 하 고 columnstore 인덱스에 하나 이상의 비클러스터형 인덱스가 있는 경우-이 경우 매핑 인덱스에 대 한 변경 내용을 최소화 하기 위해 VertiPaq 최적화를 건너뜁니다.<br/> b. 메모리 최적화 테이블의 columnstore 인덱스 <br /><br /> 0 = 아니요<br /><br /> 1 = 예|  
|**작성**|bigint|이 행 그룹에 연결 된 행 그룹 생성입니다.|  
|**created_time**|datetime2|이 행 그룹를 만든 시간에 대 한 클록 시간입니다.<br /><br /> NULL-메모리 내 테이블의 columnstore 인덱스에 대 한입니다.|  
|**closed_time**|datetime2|이 행 그룹의 클록 시간입니다.<br /><br /> NULL-메모리 내 테이블의 columnstore 인덱스에 대 한입니다.|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="results"></a>결과  
 현재 데이터베이스의 각 행 그룹 한 개의 행을 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
`CONTROL`테이블에 대 한 권한과 `VIEW DATABASE STATE` 데이터베이스에 대 한 사용 권한이 필요 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calculate-fragmentation-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>A. 조각화를 계산 하 여 columnstore 인덱스를 다시 구성 하거나 다시 작성 하는 시기를 결정 합니다.  
 Columnstore 인덱스의 경우 삭제 된 행의 비율은 행 그룹의 조각화에 대해 좋은 척도입니다. 조각화가 20% 이상인 경우 삭제 된 행을 제거 합니다. 더 많은 예제는 [인덱스 다시 구성 및 다시 작성](~/relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조 하세요.  
  
 이 예에서는 **sys.dm_db_column_store_row_group_physical_stats** 을 다른 시스템 테이블과 조인한 다음 `Fragmentation` 현재 데이터베이스에 있는 각 행 그룹의 예상 효율성으로 열을 계산 합니다. 단일 테이블에 대 한 정보를 찾으려면 **where** 절 앞에서 주석 하이픈을 제거 하 고 테이블 이름을 제공 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)      
 [Columnstore 인덱스 아키텍처](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)         
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Transact-sql&#41;sys.all_columns &#40;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [Transact-sql&#41;sys.computed_columns &#40;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)  
 [Transact-sql&#41;sys.column_store_dictionaries &#40;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
