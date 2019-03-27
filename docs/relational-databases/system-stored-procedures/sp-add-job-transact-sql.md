---
title: sp_add_job (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_job_TSQL
- sp_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_job
ms.assetid: 6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eb371603230c0c3b6fbee0012c89ce402711fb6e
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493235"
---
# <a name="spaddjob-transact-sql"></a>sp_add_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  SQLServerAgent 서비스에서 실행하는 새 작업을 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_job [ @job_name = ] 'job_name'  
     [ , [ @enabled = ] enabled ]   
     [ , [ @description = ] 'description' ]   
     [ , [ @start_step_id = ] step_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @category_id = ] category_id ]   
     [ , [ @owner_login_name = ] 'login' ]   
     [ , [ @notify_level_eventlog = ] eventlog_level ]   
     [ , [ @notify_level_email = ] email_level ]   
     [ , [ @notify_level_netsend = ] netsend_level ]   
     [ , [ @notify_level_page = ] page_level ]   
     [ , [ @notify_email_operator_name = ] 'email_name' ]   
          [ , [ @notify_netsend_operator_name = ] 'netsend_name' ]   
     [ , [ @notify_page_operator_name = ] 'page_name' ]   
     [ , [ @delete_level = ] delete_level ]   
     [ , [ @job_id = ] job_id OUTPUT ]   
```  
  
## <a name="arguments"></a>인수  
`[ @job_name = ] 'job_name'` 작업의 이름입니다. 이름은 고유 해야 하며 퍼센트를 포함할 수 없습니다 (**%**) 문자입니다. *job_name*됩니다 **nvarchar (128)**, 기본값은 없습니다.  
  
`[ @enabled = ] enabled` 추가 된 작업의 상태를 나타냅니다. *사용 하도록 설정*됩니다 **tinyint**, 기본값은 1 (사용). 그러나 하는 경우 **0**, 실행할 수 있습니다 수동으로; 작업이 사용 되지 않으며 해당 일정에 따라 실행 되지 않습니다.  
  
`[ @description = ] 'description'` 작업의 설명입니다. *설명* 됩니다 **nvarchar(512)**, 기본값은 NULL입니다. 하는 경우 *설명을* 는 생략 하면 "설명이 없습니다"가 사용 됩니다.  
  
`[ @start_step_id = ] step_id` 작업에 대해 실행 될 첫 번째 단계의 id. *step_id*됩니다 **int**, 기본값은 1입니다.  
  
`[ @category_name = ] 'category'` 작업 범주입니다. *범주*됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @category_id = ] category_id` 작업 범주를 지정 하는 것에 대 한 언어 독립 메커니즘입니다. *category_id*됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @owner_login_name = ] 'login'` 작업을 소유한 로그인의 이름입니다. *로그인*됩니다 **sysname**, 기본값은 NULL 사용 하 여 현재 로그인 이름으로 해석 됩니다. 멤버는 **sysadmin** 고정된 서버 역할 설정 하거나 값을 변경할 수 있습니다 **@owner_login_name**합니다. 경우 멤버가 아닌 사용자의 합니다 **sysadmin** 역할을 설정 하거나 값을 변경 **@owner_login_name**이 저장된 프로시저의 실행이 실패 하 고 오류가 반환 됩니다.  
  
`[ @notify_level_eventlog = ] eventlog_level` 이 작업에 대 한 Microsoft Windows 응용 프로그램 로그에 항목을 저장 하는 경우를 나타내는 값입니다. *eventlog_level*됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|안 함|  
|**1**|성공한 경우|  
|**2** (기본값)|실패한 경우|  
|**3**|Always|  
  
`[ @notify_level_email = ] email_level` 이 작업이 완료 될 때 전자 메일을 보낼 시기를 지정 하는 값입니다. *email_level*됩니다 **int**, 기본값은 **0**에 없음을 나타냅니다. *email_level*와 동일한 값을 사용 하 여 *eventlog_level*합니다.  
  
`[ @notify_level_netsend = ] netsend_level` 이 작업 완료 시 네트워크 메시지를 보낼 시기를 지정 하는 값입니다. *netsend_level*됩니다 **int**, 기본값은 **0**에 없음을 나타냅니다. *netsend_level* 와 동일한 값을 사용 하 여 *eventlog_level*합니다.  
  
`[ @notify_level_page = ] page_level` 이 작업이 완료 되 면 페이지를 보낼 시기를 지정 하는 값입니다. *page_level*됩니다 **int**, 기본값은 **0**에 없음을 나타냅니다. *page_level*와 동일한 값을 사용 하 여 *eventlog_level*합니다.  
  
`[ @notify_email_operator_name = ] 'email_name'` 전자 메일을 보낼 때 사용자의 전자 메일 이름 *email_level* 에 도달 합니다. *email_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @notify_netsend_operator_name = ] 'netsend_name'` 이 작업 완료 시 네트워크 메시지를 보낼 부여한 운영자의 이름입니다. *netsend_name*됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @notify_page_operator_name = ] 'page_name'` 이 작업 완료 시 호출할 사람의 이름입니다. *page_name*됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @delete_level = ] delete_level` 작업 삭제 시기를 나타내는 값입니다. *delete_value*됩니다 **int**, 기본값은 0으로 없음을 의미 합니다. *delete_level*와 동일한 값을 사용 하 여 *eventlog_level*합니다.  
  
> [!NOTE]  
>  때 *delete_level* 됩니다 **3**작업이 한 번만 실행 되, 작업에 대 한 일정에 관계 없이 정의 합니다. 또한 작업 자체를 삭제하는 경우 작업에 대한 모든 기록도 함께 삭제됩니다.  
  
`[ @job_id = ] _job_idOUTPUT` 성공적으로 생성 된 작업에 할당 된 작업 id. *job_id*는 형식의 출력 변수 **uniqueidentifier**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 **@originating_server** 에 존재 **sp_add_job** 인수 아래 나열 되지 않으면 있지만. **@originating_server** 내부 용도로 예약 되어 있습니다.  
  
 후 **sp_add_job** 작업을 추가한 실행 **sp_add_jobstep** 작업에 대 한 작업을 수행 하는 단계를 추가할 수 있습니다. **sp_add_jobschedule** 에 사용할 수 있습니다 일정을 만들는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 작업을 실행 하는 데 사용 하 합니다. 사용 하 여 **sp_add_jobserver** 설정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업이 실행 되는 인스턴스 및 **sp_delete_jobserver** 작업을 제거 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.  
  
 사용 하 여 작업을 다중 서버 환경에서 하나 이상의 대상 서버에서 실행 하는 경우 **sp_apply_job_to_targets** 대상 서버를 설정 하거나 작업에 대 한 서버 그룹을 대상으로 합니다. 사용 하 여 작업 대상 서버나 대상 서버 그룹에서 제거할 **sp_remove_job_from_targets**합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 작업 구조를 만들고 관리할 수 있는 바람직한 방법을 제공하는데 이는 그래픽을 사용하여 쉽게 작업을 관리할 수 있는 방법입니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장된 프로시저를 실행 하려면 사용자의 구성원 이어야 합니다는 **sysadmin** 고정 서버 역할 또는 다음 중 하나를 부여 받아야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할에 있는 합니다 **msdb** 데이터베이스:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 각 고정와 연관 된 특정 사용 권한에 대 한 정보에 대 한 데이터베이스 역할, 참조 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)입니다.  
  
 멤버는 **sysadmin** 고정된 서버 역할 설정 하거나 값을 변경할 수 있습니다 **@owner_login_name**합니다. 경우 멤버가 아닌 사용자의 합니다 **sysadmin** 역할을 설정 하거나 값을 변경 **@owner_login_name**이 저장된 프로시저의 실행이 실패 하 고 오류가 반환 됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-adding-a-job"></a>1. 작업 추가  
 다음 예에서는 `NightlyBackups`라는 새 작업을 추가합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-adding-a-job-with-pager-e-mail-and-net-send-information"></a>2. 호출기, 전자 메일 및 Net Send 정보를 사용한 작업 추가  
 다음 예에서는 호출기, 전자 메일 또는 네트워크 팝업 메시지를 사용하여 `Ad hoc Sales Data Backup`에게 알리는 `François Ajenstat`이라는 작업을 만들고 성공적으로 완료되면 해당 작업을 삭제합니다.  
  
> [!NOTE]  
>  다음 예에서는 `François Ajenstat`라는 운영자와 `françoisa`라는 로그인이 이미 있는 것으로 가정합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'Ad hoc Sales Data Backup',   
    @enabled = 1,  
    @description = N'Ad hoc backup of sales data',  
    @owner_login_name = N'françoisa',  
    @notify_level_eventlog = 2,  
    @notify_level_email = 2,  
    @notify_level_netsend = 2,  
    @notify_level_page = 2,  
    @notify_email_operator_name = N'François Ajenstat',  
    @notify_netsend_operator_name = N'François Ajenstat',   
    @notify_page_operator_name = N'François Ajenstat',  
    @delete_level = 1 ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_add_jobserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_apply_job_to_targets &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [sp_help_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
