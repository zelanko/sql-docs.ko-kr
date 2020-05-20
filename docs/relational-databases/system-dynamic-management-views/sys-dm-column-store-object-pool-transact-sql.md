---
title: sys. dm_column_store_object_pool (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c6bd55fb4bf466352a3aac861844669e70b762a1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824691"
---
# <a name="sysdm_column_store_object_pool-transact-sql"></a>sys. dm_column_store_object_pool (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Columnstore 인덱스 개체에 대 한 다양 한 유형의 개체 메모리 풀 사용 횟수를 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|데이터베이스의 ID입니다. 이는 SQL Server 데이터베이스 또는 Azure SQL database 서버 인스턴스 내에서 고유 합니다. |  
|`object_id`|`int`|개체의 ID입니다. 개체는 object_types 중 하나입니다. | 
|`index_id`|`int`|Columnstore 인덱스의 ID입니다.|  
|`partition_number`|`bigint`|인덱스 또는 힙 내의 1부터 시작하는 파티션 번호입니다. 모든 테이블 또는 뷰에는 하나 이상의 파티션이 있습니다.| 
|`column_id`|`int`|Columnstore 열의 ID입니다. DELETE_BITMAP의 경우 NULL입니다.| 
|`row_group_id`|`int`|행 그룹의 ID입니다.|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT-열 세그먼트입니다. `object_id`세그먼트 ID입니다. 세그먼트는 한 행 그룹 내에서 한 열의 모든 값을 저장 합니다. 예를 들어 테이블에 10 개의 열이 있는 경우 행 그룹 당 10 개의 열 세그먼트가 있습니다. <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY-테이블의 모든 열 세그먼트에 대 한 조회 정보를 포함 하는 전역 사전입니다.<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY-한 열과 연결 된 로컬 사전입니다.<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY-전역 사전의 다른 표현입니다. Dictionary_id에 대 한 값의 역방향 조회를 제공 합니다. 튜플 이동 기 또는 대량 로드의 일부로 압축 된 세그먼트를 만드는 데 사용 됩니다.<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP-세그먼트 삭제를 추적 하는 비트맵입니다. 파티션당 하나의 삭제 비트맵이 있습니다.|  
|`access_count`|`int`|이 개체에 대 한 읽기 또는 쓰기 액세스 수입니다.|  
|`memory_used_in_bytes`|`bigint`|개체 풀에서이 개체에 사용 되는 메모리입니다.|  
|`object_load_time`|`datetime`|Object_id 개체 풀로 가져온 클록 시간입니다.|  
  
## <a name="permissions"></a>권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
 
## <a name="see-also"></a>참고 항목  
  
 [Transact-sql&#41;&#40;인덱스 관련 동적 관리 뷰 및 함수](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [dm_db_index_operational_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.debug &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys. 개체 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
