---
title: sys.dm_db_session_space_usage (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_session_space_usage_TSQL
- dm_db_session_space_usage
- sys.dm_db_session_space_usage
- sys.dm_db_session_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_session_space_usage dynamic management view
ms.assetid: a67a6045-8e14-460a-9fe3-912b846c08c1
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 61926a7bde695d1ca8af605373cf666653c1cee5
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdbsessionspaceusage-transact-sql"></a>sys.dm_db_session_space_usage(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스의 각 세션에 의해 할당되고 할당 취소된 페이지 수를 반환합니다.  
  
> [!NOTE]  
>  이 보기에만 적용 됩니다.는 [tempdb 데이터베이스](../../relational-databases/databases/tempdb-database.md)합니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_db_session_space_usage**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|세션 ID입니다.<br /><br /> **session_id** 매핑됩니다 **session_id** 에 [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)합니다.|  
|**database_id**|**smallint**|데이터베이스 ID입니다.|  
|**user_objects_alloc_page_count**|**bigint**|이 세션에 의해 사용자 개체에 예약되거나 할당된 페이지 수입니다.|  
|**user_objects_dealloc_page_count**|**bigint**|이 세션에 의해 사용자 개체에서 할당 취소되고 더 이상 예약되지 않는 페이지 수입니다.|  
|**internal_objects_alloc_page_count**|**bigint**|이 세션에 의해 내부 개체에 예약되거나 할당된 페이지 수입니다.|  
|**internal_objects_dealloc_page_count**|**bigint**|이 세션에 의해 내부 개체에서 할당 취소되고 더 이상 예약되지 않는 페이지 수입니다.|  
|**user_objects_deferred_dealloc_page_count**|**bigint**|지연 된 할당 취소 상태로 표시 된 페이지 수입니다.<br /><br /> **참고:** 서비스 팩에 도입 된 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]합니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="remarks"></a>주의  
 IAM 페이지는 이 뷰에서 보고되는 모든 할당 또는 할당 취소 수에 포함되지 않습니다.  
  
 세션이 시작될 때 페이지 카운터는 영(0)으로 초기화됩니다. 이 카운터는 세션에서 이미 완료된 태스크에 할당되거나 할당 취소된 페이지의 총 수를 추적합니다. 카운터는 태스크가 끝난 경우에만 업데이트되며 실행 중인 작업을 반영하지 않습니다.  
  
 한 세션에서 여러 개의 요청이 동시에 활성화될 수 있습니다. 요청이 병렬 쿼리인 경우 여러 개의 스레드나 태스크를 시작할 수 있습니다.  
  
 세션, 요청 및 작업에 대 한 자세한 내용은 참조 [sys.dm_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md), [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md), 및 [sys.dm_os_tasks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)합니다.  
  
## <a name="user-objects"></a>사용자 개체  
 사용자 개체 페이지 카운터에 포함되는 개체는 다음과 같습니다.  
  
-   사용자 정의 테이블 및 인덱스  
  
-   시스템 테이블 및 인덱스  
  
-   전역 임시 테이블 및 인덱스  
  
-   로컬 임시 테이블 및 인덱스  
  
-   테이블 변수  
  
-   테이블 반환 함수에서 반환된 테이블  
  
## <a name="internal-objects"></a>내부 개체  
 내부 개체는만 **tempdb**합니다. 내부 개체 페이지 카운터에 포함되는 개체는 다음과 같습니다.  
  
-   커서 또는 스풀 작업에 대한 작업 테이블 및 임시 LOB(Large Object) 저장소  
  
-   해시 조인과 같은 작업에 대한 작업 파일  
  
-   정렬 실행  
  
## <a name="physical-joins"></a>물리적 조인  
 ![Sys.dm_db_session_space_usage에 대 한 물리적 조인](../../relational-databases/system-dynamic-management-views/media/join-dm-db-session-space-usage-1.gif "sys.dm_db_session_space_usage에 대 한 물리적 조인")  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|관계|  
|----------|--------|------------------|  
|dm_db_session_space_usage.session_id|dm_exec_sessions.session_id|일 대 일|  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_os_tasks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_db_task_space_usage &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_file_space_usage&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
  



