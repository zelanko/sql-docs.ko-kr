---
title: sys.dm_column_store_object_pool (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: f77b7f9ac514de77825f3f0ce1f201e293da2698
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39551633"
---
# <a name="sysdmcolumnstoreobjectpool-transact-sql"></a>sys.dm_column_store_object_pool (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 반환 개체 메모리 풀 사용량 columnstore 인덱스 개체에 대 한 다양 한 유형의 계산 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|데이터베이스의 ID입니다. 이 SQL Server 데이터베이스 또는 Azure SQL database 서버를 인스턴스 내에서 고유 합니다. |  
|`object_id`|`int`|개체의 ID입니다. 개체는 object_types 중 하나입니다. | 
|`index_id`|`int`|Columnstore 인덱스의 ID입니다.|  
|`partition_number`|`bigint`|인덱스 또는 힙 내의 1부터 시작하는 파티션 번호입니다. 모든 테이블 또는 뷰의 하나 이상의 파티션이 있습니다.| 
|`column_id`|`int`|Columnstore 열의 ID입니다. 이것이 DELETE_BITMAP에 대해 NULL입니다.| 
|`row_group_id`|`int`|행 그룹의 ID입니다.|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT – 열 세그먼트입니다. `object_id` 세그먼트 ID입니다. 세그먼트 내의 행 그룹이 하나 이상의 열에 대 한 모든 값을 저장합니다. 예를 들어 테이블에 있는 경우 10 개의 열, 그룹당 10 열 세그먼트는 합니다. <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY – 테이블의 열 세그먼트의 모든 조회 정보를 포함 하는 전역 사전입니다.<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY-하나의 열과 관련 된 로컬 사전입니다.<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY – 전역 사전의 다른 표현 합니다. 이 역 조회 dictionary_id 값을 제공합니다. 튜플 이동 기 또는 대량 로드의 일환으로 압축 된 세그먼트를 만드는 데 사용 합니다.<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP – 세그먼트를 추적 하는 비트맵을 삭제 합니다. 파티션당 하나의 삭제 비트맵이 있습니다.|  
|`access_count`|`int`|읽기 또는이 개체에 액세스를 쓸 수입니다.|  
|`memory_used_in_bytes`|`bigint`|개체 풀에서이 개체에서 사용 하는 메모리입니다.|  
|`object_load_time`|`datetime`|Object_id 개체 풀에 되돌렸습니다. 경우에 대 한 클럭 시간입니다.|  
  
## <a name="permissions"></a>사용 권한  

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
 
## <a name="see-also"></a>관련 항목  
  
 [인덱스 관련 동적 관리 뷰 및 함수 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
