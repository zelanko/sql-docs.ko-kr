---
title: sys.dm_db_file_space_usage (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_file_space_usage
- sys.dm_db_file_space_usage_TSQL
- sys.dm_db_file_space_usage
- dm_db_file_space_usage_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_file_space_usage dynamic management view
ms.assetid: 148a5276-a8d5-49d2-8146-3c63d24c2144
caps.latest.revision: "45"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: da7c61f339c0d8d66c8c0bcd00514a6ecf58286f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbfilespaceusage-transact-sql"></a>sys.dm_db_file_space_usage(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스의 각 파일에 대한 공간 사용량 정보를 반환합니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_db_file_space_usage**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|데이터베이스 ID입니다.|  
|file_id|**smallint**|파일의 ID입니다.<br /><br /> file_id에 file_id 매핑됩니다 [sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) 및의 fileid에 [sys.sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md)합니다.|  
|filegroup_id|**smallint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 파일 그룹 ID입니다.|  
|total_page_count|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 파일의 총 페이지 수입니다.|  
|allocated_extent_page_count|**bigint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 파일에서 할당된 익스텐트에 있는 총 페이지 수입니다.|  
|unallocated_extent_page_count|**bigint**|파일에서 할당되지 않은 익스텐트에 있는 총 페이지 수입니다.<br /><br /> 할당된 익스텐트에서 사용되지 않은 페이지는 포함되지 않습니다.|  
|version_store_reserved_page_count|**bigint**|버전 저장소에 대해 할당된 단일 익스텐트에 있는 총 페이지 수입니다. 버전 저장소 페이지는 혼합 익스텐트에서 할당되지 않습니다.<br /><br /> IAM 페이지는 항상 혼합 익스텐트에서 할당되기 때문에 포함되지 않습니다. PFS 페이지는 단일 익스텐트에서 할당된 경우에 포함됩니다.<br /><br /> 자세한 내용은 참조 [sys.dm_tran_version_store &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md).|  
|user_object_reserved_page_count|**bigint**|데이터베이스에서 사용자 개체에 대해 단일 익스텐트에서 할당된 총 페이지 수입니다. 할당된 익스텐트에서 사용되지 않은 페이지도 포함됩니다.<br /><br /> IAM 페이지는 항상 혼합 익스텐트에서 할당되기 때문에 포함되지 않습니다. PFS 페이지는 단일 익스텐트에서 할당된 경우에 포함됩니다.<br /><br /> Total_pages 열을 사용할 수 있습니다는 [sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) 카탈로그 뷰를 사용자 개체에 각 할당 단위의 예약 된 페이지 수를 반환 합니다. 하지만 total_pages 열에는 IAM 페이지가 포함됩니다.|  
|internal_object_reserved_page_count|**bigint**|파일에서 내부 개체에 대해 할당된 단일 익스텐트의 총 페이지 수입니다. 할당된 익스텐트에서 사용되지 않은 페이지도 포함됩니다.<br /><br /> IAM 페이지는 항상 혼합 익스텐트에서 할당되기 때문에 포함되지 않습니다. PFS 페이지는 단일 익스텐트에서 할당된 경우에 포함됩니다.<br /><br /> 각 내부 개체의 페이지 수를 반환하는 카탈로그 뷰나 동적 관리 개체는 없습니다.|  
|mixed_extent_page_count|**bigint**|파일에서 할당된 혼합 익스텐트의 할당된 페이지와 할당되지 않은 페이지의 총 수입니다. 혼합 익스텐트에는 여러 다른 개체에 할당된 페이지가 포함됩니다. 이 값에는 파일에 있는 모든 IAM 페이지가 포함됩니다.|
|modified_extent_page_count|**bigint**|**부터는**:[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]<br /><br />마지막 전체 데이터베이스 백업 이후 파일의 익스텐트를 할당 하는 총 페이지에서 수정할 수 있습니다. 차등 백업이 더 유용 하는 경우를 결정 하는 마지막 전체 백업 이후 데이터베이스에 차등 변경 내용을 추적 하려면 수정 된 페이지 수를 사용할 수 있습니다.|
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
|distribution_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 분포에 관련 된 고유 숫자 id입니다.|  
  
## <a name="remarks"></a>주의  
 페이지 수는 항상 익스텐트 수준에 대한 값입니다. 따라서 페이지 수는 항상 8의 배수입니다. GAM(Global Allocation Map) 및 SGAM(Shared Global Allocation Map) 할당 페이지를 포함하는 익스텐트는 할당된 단일 익스텐트로, 앞서 설명된 페이지 수에 포함되지 않습니다.  
  
 현재 버전 저장소의 콘텐츠는 [sys.dm_tran_version_store](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md)합니다. 버전 저장소 페이지는 전역 리소스이기 때문에 세션 및 태스크 수준이 아닌 파일 수준에서 추적됩니다. 세션에서 버전을 생성할 수 있지만 버전은 세션 종료 시 제거할 수 없습니다. 버전 저장소를 정리할 때는 특정 버전에 대한 액세스가 필요한 가장 오래 실행 중인 트랜잭션을 고려해야 합니다. elapsed_time_seconds 열을 확인 하 여 버전 저장소 정리와 관련 하 여 가장 오래 실행 중인 트랜잭션을 검색할 수 [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)합니다.  
  
 mixed_extent_page_count 열이 빈번하게 변경되면 SGAM 페이지가 자주 사용되는 것일 수 있습니다. 이 경우 대기 리소스가 SGAM 페이지인 PAGELATCH_UP 대기를 많이 볼 수 있습니다. 자세한 내용은 참조 [sys.dm_os_waiting_tasks &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md), [sys.dm_os_wait_stats&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md), 및 [sys.dm_os_latch_stats &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md).  
  
## <a name="user-objects"></a>사용자 개체  
 사용자 개체 페이지 카운터에 포함되는 개체는 다음과 같습니다.  
  
-   사용자 정의 테이블 및 인덱스  
  
-   시스템 테이블 및 인덱스  
  
-   전역 임시 테이블 및 인덱스  
  
-   로컬 임시 테이블 및 인덱스  
  
-   테이블 변수  
  
-   테이블 반환 함수에서 반환된 테이블  
  
## <a name="internal-objects"></a>내부 개체  
 내부 개체는 tempdb에만 있습니다. 내부 개체 페이지 카운터에 포함되는 개체는 다음과 같습니다.  
  
-   커서 또는 스풀 작업에 대한 작업 테이블 및 임시 LOB(Large Object) 저장소  
  
-   해시 조인과 같은 작업에 대한 작업 파일  
  
-   정렬 실행  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|원본|수행할 작업|관계|  
|----------|--------|------------------|  
|sys.dm_db_file_space_usage.database_id, file_id|sys.dm_io_virtual_file_stats.database_id, file_id|일 대 일|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 대 한 VIEW SERVER STATE 권한이 필요 합니다.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 프리미엄 계층 데이터베이스에서 VIEW DATABASE STATE 권한이 필요 합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 표준 및 기본 계층 필요는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 관리자 계정.  
  
## <a name="examples"></a>예  
  
### <a name="determing-the-amount-of-free-space-in-tempdb"></a>tempdb의 빈 공간 확인  
 다음 쿼리 (mb) 사용할 수 있는 모든 파일에서 사용 가능한 페이지 및 총 사용 가능 공간의 총 수를 반환 **tempdb**합니다.  
  
```tsql
USE tempdb;  
GO  
SELECT SUM(unallocated_extent_page_count) AS [free pages],   
(SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]  
FROM sys.dm_db_file_space_usage;  
```  

### <a name="determining-the-amount-of-space-used-by-user-objects"></a>사용자 개체에 의해 사용되는 공간 확인  
 다음 쿼리는 tempdb에서 사용자 개체에 의해 사용되는 전체 페이지 수와 공간(MB)을 반환합니다.  
  
```tsql  
USE tempdb;  
GO  
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],  
(SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]  
FROM sys.dm_db_file_space_usage;
```  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련된 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_db_task_space_usage&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_session_space_usage&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
