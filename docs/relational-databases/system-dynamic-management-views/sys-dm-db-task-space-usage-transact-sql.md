---
title: sys.dm_db_task_space_usage (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_task_space_usage_TSQL
- sys.dm_db_task_space_usage_TSQL
- dm_db_task_space_usage
- sys.dm_db_task_space_usage
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_task_space_usage dynamic management view
ms.assetid: fb0c87e5-43b9-466a-a8df-11b3851dc6d0
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4ee20a77440fd769e813f8335148c2b67a34d7bf
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263960"
---
# <a name="sysdm_db_task_space_usage-transact-sql"></a>sys.dm_db_task_space_usage(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스에서 발생하는 태스크별로 페이지 할당 및 할당 취소 작업을 반환합니다.  
  
> [!NOTE]  
>  이 보기에만 적용 됩니다는 [tempdb 데이터베이스](../../relational-databases/databases/tempdb-database.md)합니다.  
  
> [!NOTE]  
>  이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_db_task_space_usage**합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|세션 ID입니다.|  
|**request_id**|**int**|세션 내의 요청 ID입니다.<br /><br /> 요청은 일괄 처리라고도 하며 하나 이상의 쿼리를 포함할 수 있습니다. 하나의 세션은 동시에 활성 상태에 있는 요청을 여러 개 포함할 수 있습니다. 병렬 실행 계획이 사용되는 경우 요청의 각 쿼리가 여러 개의 스레드(태스크)를 시작할 수도 있습니다.|  
|**exec_context_id**|**int**|태스크의 실행 컨텍스트 ID입니다. 자세한 내용은 [sys.dm_os_tasks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)합니다.|  
|**database_id**|**smallint**|데이터베이스 ID입니다.|  
|**user_objects_alloc_page_count**|**bigint**|이 태스크에 의해 사용자 개체에 예약되거나 할당된 페이지 수입니다.|  
|**user_objects_dealloc_page_count**|**bigint**|이 태스크에 의해 사용자 개체에서 할당 취소되고 더 이상 예약되지 않는 페이지 수입니다.|  
|**internal_objects_alloc_page_count**|**bigint**|이 태스크에 의해 내부 개체에 예약되거나 할당된 페이지 수입니다.|  
|**internal_objects_dealloc_page_count**|**bigint**|이 태스크에 의해 내부 개체에서 할당 취소되고 더 이상 예약되지 않는 페이지 수입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 프리미엄 계층 필요는 `VIEW DATABASE STATE` 데이터베이스의 권한. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층에 필요 합니다 **서버 관리자** 요소나 **Azure Active Directory 관리자** 계정.   

## <a name="remarks"></a>설명  
 IAM 페이지는 이 뷰에서 보고되는 페이지 수에 포함되지 않습니다.  
  
 요청이 시작될 때 페이지 카운터는 영(0)으로 초기화됩니다. 이 값은 요청이 완료될 때 세션 수준에서 집계됩니다. 자세한 내용은 [sys.dm_db_session_space_usage&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)를 참조하세요.  
  
 작업 테이블 캐싱, 임시 테이블 캐싱, 지연된 삭제 작업은 지정한 태스크에서 할당 및 할당 취소되는 페이지 수에 영향을 줍니다.  
  
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
  
-   커서 또는 스풀 작업에 대한 작업 테이블 및 임시 LOB(Large Object) 스토리지  
  
-   해시 조인과 같은 작업에 대한 작업 파일  
  
-   정렬 실행  
  
## <a name="physical-joins"></a>물리적 조인  
 ![Sys.dm_db_session_task_usage에 대 한 물리적 조인](../../relational-databases/system-dynamic-management-views/media/join-dm-db-task-space-usage-1.gif "sys.dm_db_session_task_usage에 대 한 물리적 조인")  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|관계|  
|----------|--------|------------------|  
|dm_db_task_space_usage.request_id|dm_exec_requests.request_id|일 대 일|  
|dm_db_task_space_usage.session_id|dm_exec_requests.session_id|일 대 일|  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_os_tasks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_db_session_space_usage &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)   
 [sys.dm_db_file_space_usage&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
  


