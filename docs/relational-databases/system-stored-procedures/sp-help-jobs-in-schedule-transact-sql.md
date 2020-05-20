---
title: sp_help_jobs_in_schedule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobs_in_schedule_TSQL
- sp_help_jobs_in_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobs_in_schedule
ms.assetid: 1168aa2c-136b-4ba3-b18e-9070d95a26fa
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2567640f49beb0c1921811a9d04671833dca11be
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827588"
---
# <a name="sp_help_jobs_in_schedule-transact-sql"></a>sp_help_jobs_in_schedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정 일정이 연결된 작업에 대한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_jobs_in_schedule   
     [ @schedule_name = ] 'schedule_name' ,  
     [ @schedule_id = ] schedule_id   
```  
  
## <a name="arguments"></a>인수  
`[ @schedule_id = ] schedule_id`정보를 나열할 일정의 식별자입니다. *schedule_id* 는 **int**이며 기본값은 없습니다. *Schedule_id* 또는 *schedule_name* 를 지정할 수 있습니다.  
  
`[ @schedule_name = ] 'schedule_name'`정보를 나열할 일정의 이름입니다. *schedule_name* 는 **sysname**이며 기본값은 없습니다. *Schedule_id* 또는 *schedule_name* 를 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 결과 집합을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|작업의 고유 ID입니다.|  
|**originating_server**|**nvarchar(30)**|작업을 가져온 서버의 이름입니다.|  
|**name**|**sysname**|작업의 이름입니다.|  
|**사용**|**tinyint**|작업을 실행할 수 있는지를 표시합니다.|  
|**한**|**nvarchar(512)**|작업 설명입니다.|  
|**start_step_id**|**int**|실행을 시작해야 하는 작업 단계의 ID입니다.|  
|**category**|**sysname**|작업 범주입니다.|  
|**소유자도**|**sysname**|작업 소유자입니다.|  
|**notify_level_eventlog**|**int**|Microsoft Windows 애플리케이션 로그에 알림 이벤트를 기록해야 하는 상황을 나타내는 비트 마스크입니다. 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **0** = 안 함<br /><br /> **1** = 작업이 성공 하는 경우<br /><br /> **2** = 작업이 실패 하는 경우<br /><br /> **3** = 작업이 완료 될 때마다 (작업 결과에 관계 없음)|  
|**notify_level_email**|**int**|작업을 완료했을 때, 어떤 상황에서 알림 전자 메일을 전달해야 할지를 지정하는 비트 마스크입니다. 가능한 값은 **notify_level_eventlog**와 동일 합니다.|  
|**notify_level_netsend**|**int**|작업을 완료했을 때, 어떤 상황에서 네트워크 메시지를 전달해야 할지를 지정하는 비트 마스크입니다. 가능한 값은 **notify_level_eventlog**와 동일 합니다.|  
|**notify_level_page**|**int**|작업을 완료했을 때, 어떤 상황에서 메시지를 보내야 할지를 지정하는 비트 마스크입니다. 가능한 값은 **notify_level_eventlog**와 동일 합니다.|  
|**notify_email_operator**|**sysname**|정보를 알릴 운영자의 전자 메일 이름입니다.|  
|**notify_netsend_operator**|**sysname**|네트워크 메시지를 전달할 때 사용하는 컴퓨터 또는 사용자의 이름입니다.|  
|**notify_page_operator**|**sysname**|네트워크 메시지를 전달할 때 사용하는 컴퓨터 또는 사용자의 이름입니다.|  
|**delete_level**|**int**|작업을 완료했을 때, 어떤 상황에서 작업을 삭제해야 할지를 지정하는 비트 마스크입니다. 가능한 값은 **notify_level_eventlog**와 동일 합니다.|  
|**date_created**|**datetime**|작업을 만든 날짜입니다.|  
|**date_modified**|**datetime**|작업을 마지막으로 수정한 날짜입니다.|  
|**version_number**|**int**|작업의 버전입니다. 작업이 수정될 때마다 자동으로 업데이트됩니다.|  
|**last_run_date**|**int**|작업이 마지막으로 실행을 시작한 날짜입니다.|  
|**last_run_time**|**int**|작업이 마지막으로 실행을 시작한 시간입니다.|  
|**last_run_outcome**|**int**|작업이 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **3** = 취소 됨<br /><br /> **5** = 알 수 없음|  
|**next_run_date**|**int**|다음 작업 실행 일정의 날짜입니다.|  
|**next_run_time**|**int**|다음 작업 실행 일정의 시간입니다.|  
|**next_run_schedule_id**|**int**|다음 실행 일정의 ID입니다.|  
|**current_execution_status**|**int**|현재 실행 상태입니다.|  
|**current_execution_step**|**sysname**|작업의 현재 실행 단계입니다.|  
|**current_retry_attempt**|**int**|작업이 실행 중이며 단계가 다시 시도된 경우의 현재 재시도입니다.|  
|**has_step**|**int**|작업이 갖고 있는 단계 수입니다.|  
|**has_schedule**|**int**|작업이 갖고 있는 작업 일정 수입니다.|  
|**has_target**|**int**|작업이 갖고 있는 대상 서버 수입니다.|  
|**type**|**int**|작업의 유형입니다.<br /><br /> **1** = 로컬 작업<br /><br /> **2** = 다중 서버 작업<br /><br /> **0** = 작업에 대상 서버가 없습니다.|  
  
## <a name="remarks"></a>설명  
 이 프로시저는 지정한 일정에 연결된 작업에 대한 정보를 나열합니다.  
  
## <a name="permissions"></a>권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **SQLAgentUserRole** 의 멤버는 자신이 소유한 작업의 상태만 볼 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `NightlyJobs` 일정에 연결된 작업을 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_jobs_in_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_add_schedule &#40;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_attach_schedule &#40;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_delete_schedule &#40;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_detach_schedule &#40;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
