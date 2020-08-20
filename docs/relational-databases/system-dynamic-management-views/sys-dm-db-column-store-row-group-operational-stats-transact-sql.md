---
description: sys. dm_db_column_store_row_group_operational_stats (Transact-sql)
title: sys. dm_db_column_store_row_group_operational_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 42e7afbc0975c4f740eff21caaf86f783ac05f98
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646255"
---
# <a name="sysdm_db_column_store_row_group_operational_stats-transact-sql"></a>sys. dm_db_column_store_row_group_operational_stats (Transact-sql)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  Columnstore 인덱스의 압축 된 행 그룹에 대 한 현재 행 수준 i/o, 잠금 및 액세스 방법 작업을 반환 합니다. 행 그룹를 사용 하 여 사용자 쿼리가 columnstore 인덱스의 압축 된 또는 파티션에 대 한 읽기 또는 쓰기를 대기 해야 하는 시간을 추적 하 고, 상당한 i/o 작업 또는 핫 스폿이 발생 하는 행 그룹을 식별할 수 **있습니다 dm_db_column_store_row_group_operational_stats.**  
  
 메모리 내 columnstore 인덱스는이 DMV에 나타나지 않습니다.  
 
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Columnstore 인덱스가 있는 테이블의 ID입니다.|  
|**index_id**|**int**|Columnstore 인덱스의 ID입니다.|  
|**partition_number**|**int**|인덱스 또는 힙 내의 1부터 시작하는 파티션 번호입니다.|  
|**row_group_id**|**int**|Columnstore 인덱스에 있는 행 그룹의 ID입니다. 이는 파티션 내에서 고유 합니다.|  
|**scan_count**|**int**|마지막 SQL 다시 시작 이후 행 그룹의 검색 수입니다.|  
|**delete_buffer_scan_count**|**int**|삭제 버퍼가이 행 그룹에서 삭제 된 행을 확인 하는 데 사용 된 횟수입니다. 여기에는 메모리 내 해시 테이블 및 기본 btree에 대 한 액세스가 포함 됩니다.|  
|**index_scan_count**|**int**|Columnstore 인덱스 파티션을 검색 한 횟수입니다. 이는 파티션의 모든 행 그룹에 대해 동일 합니다.|  
|**rowgroup_lock_count**|**bigint**|마지막 SQL 다시 시작 이후이 행 그룹에 대 한 누적 잠금 요청 수입니다.|  
|**rowgroup_lock_wait_count**|**bigint**|마지막 SQL 다시 시작 이후 데이터베이스 엔진이이 행 그룹 잠금에서 대기한 누적 횟수입니다.|  
|**rowgroup_lock_wait_in_ms**|**bigint**|마지막 SQL 다시 시작 이후 데이터베이스 엔진이이 행 그룹 잠금에서 대기한 누적 시간 (밀리초)입니다.|  
  
## <a name="permissions"></a>사용 권한  
 다음 사용 권한이 필요합니다.  
  
-   Object_id에 지정 된 테이블에 대 한 CONTROL 권한  
  
-   개체 와일드 카드 @*object_id* = NULL을 사용 하 여 데이터베이스 내의 모든 개체에 대 한 정보를 반환 하는 VIEW database STATE 권한  
  
 VIEW DATABASE STATE를 허용하면 특정 개체에 대해 거부된 CONTROL 권한에 관계없이 데이터베이스의 모든 개체가 반환됩니다.  
  
 VIEW DATABASE STATE를 거부하면 특정 개체에 대해 허용된 CONTROL 권한에 관계없이 데이터베이스의 모든 개체가 반환되지 않습니다. 또한 데이터베이스 와일드 카드 @*database_id*= NULL을 지정 하면 데이터베이스가 생략 됩니다.  
  
 자세한 내용은 [동적 관리 뷰 및 함수 &#40;transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)를 참조 하세요.  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [인덱스 관련 동적 관리 뷰 및 함수 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [dm_db_index_usage_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [dm_db_partition_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

