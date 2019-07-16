---
title: sys.dm_db_index_usage_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_index_usage_stats_TSQL
- sys.dm_db_index_usage_stats
- sys.dm_db_index_usage_stats_TSQL
- dm_db_index_usage_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_usage_stats dynamic management view
ms.assetid: d06a001f-0f72-4679-bc2f-66fff7958b86
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c9f44724282761f071cd28d8cbe200855cb14f69
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004856"
---
# <a name="sysdmdbindexusagestats-transact-sql"></a>sys.dm_db_index_usage_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  서로 다른 유형의 인덱스 작업 수와 각 유형의 작업이 마지막으로 수행된 시간을 반환합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이 정보 공개를 방지 하려면 연결 된 테 넌 트에 속하지 않는 데이터가 포함 된 모든 행 필터링 됩니다.  
  
> [!NOTE]  
>  **sys.dm_db_index_usage_stats** 메모리 최적화 인덱스에 대 한 정보를 반환 하지 않습니다. 메모리 최적화 인덱스 사용에 대 한 정보를 참조 하세요 [sys.dm_db_xtp_index_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)합니다.  
  
> [!NOTE]  
>  호출에서이 뷰를 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]를 사용 하 여 **sys.dm_pdw_nodes_db_index_usage_stats**합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**database_id**|**smallint**|테이블 또는 뷰가 정의되어 있는 데이터베이스의 ID입니다.|  
|**object_id**|**int**|인덱스가 정의되어 있는 테이블 또는 뷰의 ID입니다.|  
|**index_id**|**int**|인덱스의 ID입니다.|  
|**user_seeks**|**bigint**|사용자 쿼리별 검색(Seek) 수입니다.|  
|**user_scans**|**bigint**|사용 하지 않는 사용자 쿼리 별 검색 횟수 ' 검색 ' 조건자입니다.|  
|**user_lookups**|**bigint**|사용자 쿼리별 책갈피 수입니다.|  
|**user_updates**|**bigint**|사용자 쿼리별 업데이트 수입니다. 이 삽입, 삭제를 포함 하 고 작업을 수행 하지 실제을 받는 행의 개수를 나타내는 업데이트 합니다. 예를 들어, 하나의 문에서 1000 개의 행을 삭제 하면이 수가 1 씩 증가|  
|**last_user_seek**|**datetime**|마지막 사용자 검색(Seek) 시간입니다.|  
|**last_user_scan**|**datetime**|마지막 사용자 검색(Scan) 시간입니다.|  
|**last_user_lookup**|**datetime**|마지막 사용자 조회 시간입니다.|  
|**last_user_update**|**datetime**|마지막 사용자 업데이트 시간입니다.|  
|**system_seeks**|**bigint**|시스템 쿼리별 검색(Seek) 수입니다.|  
|**system_scans**|**bigint**|시스템 쿼리별 검색(Scan) 수입니다.|  
|**system_lookups**|**bigint**|시스템 쿼리별 조회 수입니다.|  
|**system_updates**|**bigint**|시스템 쿼리별 업데이트 수입니다.|  
|**last_system_seek**|**datetime**|마지막 시스템 검색(Seek) 시간입니다.|  
|**last_system_scan**|**datetime**|마지막 시스템 검색(Scan) 시간입니다.|  
|**last_system_lookup**|**datetime**|마지막 시스템 조회 시간입니다.|  
|**last_system_update**|**datetime**|마지막 시스템 업데이트 시간입니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="remarks"></a>설명  
 한 번의 쿼리 실행으로 지정된 인덱스에 대한 개별적인 검색(Seek), 검색(Scan), 조회 또는 업데이트를 수행하면 해당 인덱스를 사용하는 것으로 계산되어 이 뷰에서 해당 카운터를 증가시킵니다. 통계 수집을 위한 검색과 같이 내부적으로 생성된 쿼리에 의한 작업과 사용자 제공 쿼리에 의한 작업의 경우 모두 정보가 보고됩니다.  
  
 합니다 **user_updates** 카운터에서 삽입 된 인덱스 유지 관리의 수준을 나타내는, 업데이트 또는 삭제 작업을 기본 테이블 또는 보기에 있습니다. 이 뷰를 사용하여 어떤 인덱스가 사용자 응용 프로그램에서만 조금 사용되는지 또는 유지 관리 오버헤드를 유발하는지를 확인할 수 있습니다. 필요한 경우 유지 관리 오버헤드를 유발하지만 쿼리에 거의 사용되지 않거나 전혀 사용되지 않는 인덱스를 삭제할 수도 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](MSSQLSERVER) 서비스를 시작할 때마다 카운터는 빈 상태로 초기화됩니다. 또한 데이터베이스가 분리되거나 종료될 때마다(예: AUTO_CLOSE가 ON으로 설정된 경우) 데이터베이스와 관련된 모든 행이 제거됩니다.  
  
 에 행이 추가 인덱스를 사용 하면 **sys.dm_db_index_usage_stats** 인덱스에 대 한 행을 아직 없는 경우. 행이 추가되면 초기에 해당 카운터가 0으로 설정됩니다.  
  
 업그레이드 하는 동안 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], 또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], sys.dm_db_index_usage_stats에서 항목이 제거 됩니다. 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], 이전 처럼 엔트리가 유지 되 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]합니다.  
  
## <a name="permissions"></a>사용 권한  
온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]에서 데이터베이스에 대한 `VIEW DATABASE STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  

 [인덱스 관련 동적 관리 뷰 및 함수 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  


