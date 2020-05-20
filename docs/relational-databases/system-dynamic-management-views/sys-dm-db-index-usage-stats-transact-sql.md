---
title: sys. dm_db_index_usage_stats (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6bdacbebf64e372e757de6f2ba268404773f9c96
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830874"
---
# <a name="sysdm_db_index_usage_stats-transact-sql"></a>sys.dm_db_index_usage_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  서로 다른 유형의 인덱스 작업 수와 각 유형의 작업이 마지막으로 수행된 시간을 반환합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이 정보를 노출 하지 않도록 하기 위해 연결 된 테 넌 트에 속하지 않는 데이터를 포함 하는 모든 행이 필터링 됩니다.  
  
> [!NOTE]  
>  **dm_db_index_usage_stats** 는 메모리 최적화 인덱스에 대 한 정보를 반환 하지 않습니다. 메모리 최적화 인덱스 사용에 대 한 자세한 내용은 [dm_db_xtp_index_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)을 참조 하십시오.  
  
> [!NOTE]  
>  또는에서이 뷰를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **dm_pdw_nodes_db_index_usage_stats**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**smallint**|테이블 또는 뷰가 정의되어 있는 데이터베이스의 ID입니다.|  
|**object_id**|**int**|인덱스가 정의되어 있는 테이블 또는 뷰의 ID입니다.|  
|**index_id**|**int**|인덱스의 ID입니다.|  
|**user_seeks**|**bigint**|사용자 쿼리별 검색(Seek) 수입니다.|  
|**user_scans**|**bigint**|' Seek ' 조건자를 사용 하지 않는 사용자 쿼리 별 검색 수입니다.|  
|**user_lookups**|**bigint**|사용자 쿼리별 책갈피 수입니다.|  
|**user_updates**|**bigint**|사용자 쿼리별 업데이트 수입니다. 여기에는 영향을 받는 실제 행이 아닌 작업 수를 나타내는 삽입, 삭제 및 업데이트가 포함 됩니다. 예를 들어 한 문에서 1000 행을 삭제 하면이 수가 1 씩 증가 합니다.|  
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
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="remarks"></a>설명  
 한 번의 쿼리 실행으로 지정된 인덱스에 대한 개별적인 검색(Seek), 검색(Scan), 조회 또는 업데이트를 수행하면 해당 인덱스를 사용하는 것으로 계산되어 이 뷰에서 해당 카운터를 증가시킵니다. 통계 수집을 위한 검색과 같이 내부적으로 생성된 쿼리에 의한 작업과 사용자 제공 쿼리에 의한 작업의 경우 모두 정보가 보고됩니다.  
  
 **user_updates** 카운터는 기본 테이블 또는 뷰에 대한 삽입, 업데이트 또는 삭제 작업에 의해 실행된 인덱스의 유지 관리 수준을 나타냅니다. 이 뷰를 사용하여 어떤 인덱스가 사용자 애플리케이션에서만 조금 사용되는지 또는 유지 관리 오버헤드를 유발하는지를 확인할 수 있습니다. 필요한 경우 유지 관리 오버헤드를 유발하지만 쿼리에 거의 사용되지 않거나 전혀 사용되지 않는 인덱스를 삭제할 수도 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](MSSQLSERVER) 서비스를 시작할 때마다 카운터는 빈 상태로 초기화됩니다. 또한 데이터베이스가 분리되거나 종료될 때마다(예: AUTO_CLOSE가 ON으로 설정된 경우) 데이터베이스와 관련된 모든 행이 제거됩니다.  
  
 인덱스를 사용하면 해당 인덱스에 대해 아직 존재하지 않는 행도 **sys.dm_db_index_usage_stats**에 추가됩니다. 행이 추가되면 초기에 해당 카운터가 0으로 설정됩니다.  
  
 , 또는로 업그레이드 하는 동안에는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] dm_db_index_usage_stats의 항목이 제거 됩니다. 부터 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 항목은 이전과 동일 하 게 유지 됩니다 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
## <a name="permissions"></a>사용 권한  
에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  

 [Transact-sql&#41;&#40;인덱스 관련 동적 관리 뷰 및 함수](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [dm_db_index_operational_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.debug &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys. 개체 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  


