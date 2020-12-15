---
description: sys.dm_db_session_space_usage(Transact-SQL)
title: sys.dm_db_session_space_usage (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3163e54ce0db39ac92b16584c0ca9dc57a6d2c76
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468494"
---
# <a name="sysdm_db_session_space_usage-transact-sql"></a>sys.dm_db_session_space_usage(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  데이터베이스의 각 세션에 의해 할당되고 할당 취소된 페이지 수를 반환합니다.  
  
> [!NOTE]  
>  이 뷰는 [tempdb 데이터베이스](../../relational-databases/databases/tempdb-database.md)에만 적용 됩니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **sys.dm_pdw_nodes_db_session_space_usage** 이름을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|세션 ID입니다.<br /><br /> **session_id** 는 [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)의 **session_id** 에 매핑됩니다.|  
|**database_id**|**smallint**|데이터베이스 ID입니다.|  
|**user_objects_alloc_page_count**|**bigint**|이 세션에 의해 사용자 개체에 예약되거나 할당된 페이지 수입니다.|  
|**user_objects_dealloc_page_count**|**bigint**|이 세션에 의해 사용자 개체에서 할당 취소되고 더 이상 예약되지 않는 페이지 수입니다.|  
|**internal_objects_alloc_page_count**|**bigint**|이 세션에 의해 내부 개체에 예약되거나 할당된 페이지 수입니다.|  
|**internal_objects_dealloc_page_count**|**bigint**|이 세션에 의해 내부 개체에서 할당 취소되고 더 이상 예약되지 않는 페이지 수입니다.|  
|**user_objects_deferred_dealloc_page_count**|**bigint**|지연 된 할당 취소로 표시 된 페이지 수입니다.<br /><br /> **참고:** 및 용 서비스 팩에 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 도입 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 되었습니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   

## <a name="remarks"></a>설명  
 IAM 페이지는 이 뷰에서 보고되는 모든 할당 또는 할당 취소 수에 포함되지 않습니다.  
  
 세션이 시작될 때 페이지 카운터는 영(0)으로 초기화됩니다. 이 카운터는 세션에서 이미 완료된 태스크에 할당되거나 할당 취소된 페이지의 총 수를 추적합니다. 카운터는 태스크가 끝난 경우에만 업데이트되며 실행 중인 작업을 반영하지 않습니다.  
  
 한 세션에서 여러 개의 요청이 동시에 활성화될 수 있습니다. 요청이 병렬 쿼리인 경우 여러 개의 스레드나 태스크를 시작할 수 있습니다.  
  
 세션, 요청 및 태스크에 대 한 자세한 내용은 [sys.dm_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md), [sys.dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)및 sys.dm_os_tasks [&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)을 참조 하세요.  
  
## <a name="user-objects"></a>사용자 개체  
 사용자 개체 페이지 카운터에 포함되는 개체는 다음과 같습니다.  
  
-   사용자 정의 테이블 및 인덱스  
  
-   시스템 테이블 및 인덱스  
  
-   전역 임시 테이블 및 인덱스  
  
-   로컬 임시 테이블 및 인덱스  
  
-   테이블 변수  
  
-   테이블 반환 함수에서 반환된 테이블  
  
## <a name="internal-objects"></a>내부 개체  
 내부 개체는 **tempdb** 에만 있습니다. 내부 개체 페이지 카운터에 포함되는 개체는 다음과 같습니다.  
  
-   커서 또는 스풀 작업에 대한 작업 테이블 및 임시 LOB(Large Object) 스토리지  
  
-   해시 조인과 같은 작업에 대한 작업 파일  
  
-   정렬 실행  
  
## <a name="physical-joins"></a>물리적 조인  
 ![sys.dm_db_session_space_usage에 대한 물리적 조인](../../relational-databases/system-dynamic-management-views/media/join-dm-db-session-space-usage-1.gif "sys.dm_db_session_space_usage에 대한 물리적 조인")  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|From|대상|관계|  
|----------|--------|------------------|  
|dm_db_session_space_usage.session_id|dm_exec_sessions.session_id|일대일|  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [Transact-sql&#41;sys.dm_os_tasks &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [Transact-sql&#41;sys.dm_db_task_space_usage &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_file_space_usage&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
  



