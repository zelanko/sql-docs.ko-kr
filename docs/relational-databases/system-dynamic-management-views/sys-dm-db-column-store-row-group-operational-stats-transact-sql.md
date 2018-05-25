---
title: sys.dm_db_column_store_row_group_operational_stats (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 655f5838456fd72566405c453cecfd8858d7d6dd
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdbcolumnstorerowgroupoperationalstats-transact-sql"></a>sys.dm_db_column_store_row_group_operational_stats (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  반환 현재 행 수준 I/O, 잠금, 및 columnstore 인덱스에 압축 된 행 그룹에 대 한 방법 작업에 액세스 합니다. 사용 하 여 **sys.dm_db_column_store_row_group_operational_stats** 시간의 길이 추적 하는 사용자 쿼리나 읽기 또는 압축 된 행 그룹 또는 columnstore 인덱스의 파티션을 쓰기 위해 대기 하며 발생 하는 행 그룹을 식별 상당한 I/O 작업 또는 문제가 있습니다.  
  
 메모리 내 columnstore 인덱스는이 DMV에 나타나지 않습니다.  
 
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Columnstore 인덱스가 있는 테이블의 ID입니다.|  
|**index_id**|**int**|Columnstore 인덱스의 ID입니다.|  
|**partition_number**|**int**|인덱스 또는 힙 내의 1부터 시작하는 파티션 번호입니다.|  
|**row_group_id**|**int**|Columnstore 인덱스에 행 그룹의 ID입니다. 이 옵션은 파티션 내에서 고유 합니다.|  
|**scan_count**|**int**|마지막 SQL 다시 시작 이후 행 그룹을 통해 검색 수입니다.|  
|**delete_buffer_scan_count**|**int**|삭제 버퍼는이 행 그룹의 삭제 된 행을 결정 하는 데 사용 된 횟수입니다. 여기에 기본 btree 및 인-메모리 해시 테이블에 액세스 합니다.|  
|**index_scan_count**|**int**|Columnstore 인덱스 파티션이 검사가 수행 된 횟수입니다. 파티션에서 모든 행 그룹에 대해 같습니다.|  
|**rowgroup_lock_count**|**bigint**|마지막 SQL 다시 시작 이후 행이 그룹에 대 한 잠금 요청 누적 횟수입니다.|  
|**rowgroup_lock_wait_count**|**bigint**|누적 횟수 데이터베이스 엔진에서 대기한이 행 그룹 잠금이 마지막 SQL 다시 시작 이후입니다.|  
|**rowgroup_lock_wait_in_ms**|**bigint**|누적 기간 (밀리초)는 데이터베이스 엔진에서 대기한이 행 그룹 잠금이 마지막 SQL 다시 시작 이후입니다.|  
  
## <a name="permissions"></a>Permissions  
 다음 사용 권한이 필요합니다.  
  
-   Object_id 하 여 지정 된 테이블에 대 한 CONTROL 권한  
  
-   @ 개체 와일드 카드를 사용 하 여 데이터베이스 내 모든 개체에 대 한 정보를 반환 하는 VIEW DATABASE STATE 권한이*object_id* = NULL  
  
 VIEW DATABASE STATE를 허용하면 특정 개체에 대해 거부된 CONTROL 권한에 관계없이 데이터베이스의 모든 개체가 반환됩니다.  
  
 VIEW DATABASE STATE를 거부하면 특정 개체에 대해 허용된 CONTROL 권한에 관계없이 데이터베이스의 모든 개체가 반환되지 않습니다. 또한, 데이터베이스 와일드 카드 @*database_id*= NULL을 지정 하면 해당 데이터베이스가 생략 됩니다.  
  
 자세한 내용은 참조 [동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [인덱스 관련 동적 관리 뷰 및 함수 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

