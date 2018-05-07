---
title: sys.dm_column_store_object_pool (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6a2fdbc738d173dfeb6a1c37b99c35520574ece3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmcolumnstoreobjectpool-transact-sql"></a>sys.dm_column_store_object_pool (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 다양 한 유형의 columnstore 인덱스 개체에 대 한 개체 메모리 풀 사용 횟수를 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|데이터베이스의 ID입니다. 이 SQL Server 데이터베이스 또는 Azure SQL 데이터베이스 서버 인스턴스 내에서 고유 합니다. |  
|`object_id`|`int`|개체의 ID입니다. 개체는 object_types 중 하나입니다. | 
|`index_id`|`int`|Columnstore 인덱스의 ID입니다.|  
|`partition_number`|`bigint`|인덱스 또는 힙 내의 1부터 시작하는 파티션 번호입니다. 모든 테이블 또는 뷰는 파티션이 하나 이상에 있습니다.| 
|`column_id`|`int`|Columnstore 열의 ID입니다. DELETE_BITMAP의 경우 NULL입니다.| 
|`row_group_id`|`int`|행 그룹의 ID입니다.|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|– COLUMN_SEGMENT 열 세그먼트입니다. `object_id` 세그먼트 ID입니다. 세그먼트는 한 행 그룹 내에서 하나의 열에 대 한 모든 값을 저장합니다. 예를 들어 테이블에 있는 경우 10 개의 열, 행 그룹당 최대 10 개의 열 세그먼트는 합니다. <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY – 모든 테이블의 열 세그먼트의 조회 정보를 포함 하는 전역 사전입니다.<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY-한 열과 관련 된 로컬 사전입니다.<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY 전역 사전의 다른 표현 합니다. 이 값이 dictionary_id 역방향 조회를 제공합니다. 튜플 이동 기가 또는 대량 로드의 일환으로 압축 된 세그먼트를 만드는 데 사용 합니다.<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP – 세그먼트를 추적 하는 비트맵을 삭제 합니다. 파티션당 하나의 delete 비트맵이 있습니다.|  
|`access_count`|`int`|읽기 또는이 개체에 액세스를 쓸 수입니다.|  
|`memory_used_in_bytes`|`bigint`|개체 풀에서이 개체에서 사용 하는 메모리입니다.|  
|`object_load_time`|`datetime`|개체 풀에 object_id 상태로 전환 된 경우에 대 한 클록 시간입니다.|  
  
## <a name="permissions"></a>Permissions  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   
 
## <a name="see-also"></a>관련 항목:  
  
 [인덱스 관련 동적 관리 뷰 및 함수 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
