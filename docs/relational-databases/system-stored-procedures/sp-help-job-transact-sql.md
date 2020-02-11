---
title: sp_help_job (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_job_TSQL
- sp_help_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_job
ms.assetid: 8a8b6104-e0e4-4d07-a2c3-f4243ee0d6fa
author: stevestein
ms.author: sstein
ms.openlocfilehash: 29870a0ffb3d2c3b1872acbb40266aef0d16b62c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75546559"
---
# <a name="sp_help_job-transact-sql"></a>sp_help_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 자동화된 작업을 수행하는 데 사용하는 작업에 대한 정보를 반환합니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_job { [ @job_id = ] job_id  
[ @job_name = ] 'job_name' }   
     [ , [ @job_aspect = ] 'job_aspect' ]   
     [ , [ @job_type = ] 'job_type' ]   
     [ , [ @owner_login_name = ] 'login_name' ]   
     [ , [ @subsystem = ] 'subsystem' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @enabled = ] enabled ]   
     [ , [ @execution_status = ] status ]   
     [ , [ @date_comparator = ] 'date_comparison' ]   
     [ , [ @date_created = ] date_created ]   
     [ , [ @date_last_modified = ] date_modified ]   
     [ , [ @description = ] 'description_pattern' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id`작업 id입니다. *job_id* 은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'`작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  특정 작업을 보려면 *job_id* 또는 *job_name* 를 지정 해야 합니다.  *Job_id* 와 *job_name* 를 모두 생략 하 여 모든 작업에 대 한 정보를 반환 합니다.
  
`[ @job_aspect = ] 'job_aspect'`표시할 작업 특성입니다. *job_aspect* 는 **varchar (9)** 이며 기본값은 NULL이 고 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**ALL**|작업 항목 정보입니다.|  
|**직함**|작업 정보입니다.|  
|**일정**|일정 정보입니다.|  
|**위한**|작업 단계 정보입니다.|  
|**대상**|대상 정보입니다.|  
  
`[ @job_type = ] 'job_type'`보고서에 포함할 작업 유형입니다. *job_type* 는 **varchar (12)** 이며 기본값은 NULL입니다. *job_type* 는 **로컬** 또는 **다중 서버**일 수 있습니다.  
  
`[ @owner_login_name = ] 'login_name'`작업 소유자의 로그인 이름입니다. *login_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subsystem = ] 'subsystem'`하위 시스템의 이름입니다. *하위 시스템* 은 **nvarchar (40)** 이며 기본값은 NULL입니다.  
  
`[ @category_name = ] 'category'`범주의 이름입니다. *category* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @enabled = ] enabled`활성화 된 작업 또는 사용 하지 않는 작업에 대 한 정보가 표시 되는지 여부를 나타내는 숫자입니다. *enabled* 는 **tinyint**이며 기본값은 NULL입니다. **1** 은 사용 하도록 설정 된 작업을 나타내고 **0** 은 사용 안 함 작업을 나타냅니다.  
  
`[ @execution_status = ] status`작업의 실행 상태입니다. *status* 는 **int**이며 기본값은 NULL이 고 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|유휴 또는 일시 중지 상태가 아닌 작업만 반환합니다.|  
|**1**|실행 중입니다.|  
|**2**|스레드 대기 중입니다.|  
|**3**|재시도 중입니다.|  
|**4**|유휴 상태입니다.|  
|**5**|일시 중지 상태입니다.|  
|**일**|동작을 완전히 수행하였습니다.|  
  
`[ @date_comparator = ] 'date_comparison'`*Date_created* 와 *date_modified*을 비교 하는 데 사용할 비교 연산자입니다. *date_comparison* 은 **char (1)** 이 고 =, \<또는 > 수 있습니다.  
  
`[ @date_created = ] date_created`작업을 만든 날짜입니다. *date_created*은 **datetime**이며 기본값은 NULL입니다.  
  
`[ @date_last_modified = ] date_modified`작업을 마지막으로 수정한 날짜입니다. *date_modified* 은 **datetime**이며 기본값은 NULL입니다.  
  
`[ @description = ] 'description_pattern'`작업에 대 한 설명입니다. *description_pattern* 은 **nvarchar (512)** 이며 기본값은 NULL입니다. 패턴 일치를 위해 SQL Server 와일드 카드 문자를 포함할 수 *description_pattern* .  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 인수를 지정 하지 않으면 **sp_help_job** 이 결과 집합을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|작업의 고유 ID입니다.|  
|**originating_server**|**nvarchar (30)**|작업을 가져온 서버의 이름입니다.|  
|**name**|**sysname**|작업의 이름입니다.|  
|**사용**|**tinyint**|작업을 실행할 수 있는지를 표시합니다.|  
|**한**|**nvarchar(512)**|작업에 대한 설명입니다.|  
|**start_step_id**|**int**|실행을 시작해야 하는 작업 단계의 ID입니다.|  
|**범주**|**sysname**|작업 범주입니다.|  
|**소유자도**|**sysname**|작업 소유자입니다.|  
|**notify_level_eventlog**|**int**|Microsoft Windows 응용 프로그램 로그에 알림 이벤트를 기록해 야 하는 상황을 나타내는 **비트 마스크** 입니다. 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **0** = 안 함<br /><br /> **1** = 작업이 성공 하는 경우<br /><br /> **2** = 작업이 실패 하는 경우<br /><br /> **3** = 작업이 완료 될 때마다 (작업 결과에 관계 없음)|  
|**notify_level_email**|**int**|작업이 완료 될 때 알림 전자 메일을 보내야 하는 상황을 나타내는 **비트 마스크** 입니다. 가능한 값은 **notify_level_eventlog**와 동일 합니다.|  
|**notify_level_netsend**|**int**|작업이 완료 될 때 네트워크 메시지를 보내야 하는 상황을 나타내는 **비트 마스크** 입니다. 가능한 값은 **notify_level_eventlog**와 동일 합니다.|  
|**notify_level_page**|**int**|작업이 완료 될 때 페이지를 보내야 하는 상황을 나타내는 **비트 마스크** 입니다. 가능한 값은 **notify_level_eventlog**와 동일 합니다.|  
|**notify_email_operator**|**sysname**|정보를 알릴 운영자의 전자 메일 이름입니다.|  
|**notify_netsend_operator**|**sysname**|네트워크 메시지를 전달할 때 사용하는 컴퓨터 또는 사용자의 이름입니다.|  
|**notify_page_operator**|**sysname**|네트워크 메시지를 전달할 때 사용하는 컴퓨터 또는 사용자의 이름입니다.|  
|**delete_level**|**int**|작업이 완료 될 때 작업을 삭제 해야 하는 상황을 나타내는 **비트 마스크** 입니다. 가능한 값은 **notify_level_eventlog**와 동일 합니다.|  
|**date_created**|**datetime**|작업을 만든 날짜입니다.|  
|**date_modified**|**datetime**|작업을 마지막으로 수정한 날짜입니다.|  
|**version_number**|**int**|작업 버전입니다(작업이 수정될 때마다 자동으로 업데이트됨).|  
|**last_run_date**|**int**|작업이 마지막으로 실행을 시작한 날짜입니다.|  
|**last_run_time**|**int**|작업이 마지막으로 실행을 시작한 시간입니다.|  
|**last_run_outcome**|**int**|작업이 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **3** = 취소 됨<br /><br /> **5** = 알 수 없음|  
|**next_run_date**|**int**|다음 작업 실행 일정의 날짜입니다.|  
|**next_run_time**|**int**|다음 작업 실행 일정의 시간입니다.|  
|**next_run_schedule_id**|**int**|다음 실행 일정의 ID입니다.|  
|**current_execution_status**|**int**|현재 실행 상태:<br /><br /> **1** = 실행 중<br /><br /> **2** = 스레드 대기 중<br /><br /> **3** = 다시 시도 간격<br /><br /> **4** = 유휴 상태<br /><br /> **5** = 일시 중단 됨<br /><br /> **6** = 사용 되지 않음<br /><br /> **7** = PerformingCompletionActions|  
|**current_execution_step**|**sysname**|작업의 현재 실행 단계입니다.|  
|**current_retry_attempt**|**int**|작업이 실행 중이며 단계가 다시 시도된 경우의 현재 재시도입니다.|  
|**has_step**|**int**|작업이 갖고 있는 단계 수입니다.|  
|**has_schedule**|**int**|작업이 갖고 있는 작업 일정 수입니다.|  
|**has_target**|**int**|작업이 갖고 있는 대상 서버 수입니다.|  
|**type**|**int**|작업의 유형입니다.<br /><br /> 1 = 로컬 작업<br /><br /> **2** = 다중 서버 작업<br /><br /> **0** = 작업에 대상 서버가 없습니다.|  
  
 *Job_id* 또는 *job_name* 지정 된 경우 작업 단계, 작업 일정 및 작업 대상 서버에 대해 이러한 추가 결과 집합을 반환 **sp_help_job** .  
  
 다음은 작업 단계에 관한 결과 집합입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**step_id**|**int**|이 작업의 단계에 대한 고유 ID입니다.|  
|**step_name**|**sysname**|단계의 이름입니다.|  
|**하위**|**nvarchar (40)**|단계 명령을 실행할 하위 시스템입니다.|  
|**명령**|**nvarchar (3200)**|실행할 명령입니다.|  
|**flags**|**nvarchar(4000)**|단계 동작을 제어 하는 값의 **비트 마스크** 입니다.|  
|**cmdexec_success_code**|**int**|**CmdExec** 단계의 경우 성공한 명령의 프로세스 종료 코드입니다.|  
|**on_success_action**|**nvarchar(4000)**|단계가 성공할 경우 수행되는 작업입니다.<br /><br /> **1** = 성공으로 종료 합니다.<br /><br /> **2** = 실패로 종료<br /><br /> **3** = 다음 단계로 이동 합니다.<br /><br /> **4** = 단계로 이동 합니다.|  
|**on_success_step_id**|**int**|**On_success_action** 이 **4**인 경우 실행할 다음 단계를 나타냅니다.|  
|**on_fail_action**|**nvarchar(4000)**|단계가 실패한 경우에 수행할 동작입니다. 값은 **on_success_action**와 동일 합니다.|  
|**on_fail_step_id**|**int**|**On_fail_action** 이 **4**인 경우 실행할 다음 단계를 나타냅니다.|  
|**서버인**|**sysname**|예약되어 있습니다.|  
|**database_name**|**sysname**|
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 단계의 경우 명령이 실행될 데이터베이스입니다.|  
|**database_user_name**|**sysname**|
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 단계의 경우 명령이 실행되는 데이터베이스 사용자 컨텍스트입니다.|  
|**retry_attempts**|**int**|단계가 성공하지 못한 경우에 해당 단계를 실패로 간주하기 전에 명령을 재시도할 최대 횟수입니다.|  
|**retry_interval**|**int**|재시도 간의 간격(분)입니다.|  
|**os_run_priority**|**varchar (4000)**|예약되어 있습니다.|  
|**output_file_name**|**varchar (200)**|명령 출력을 써야 하는 파일입니다 ([!INCLUDE[tsql](../../includes/tsql-md.md)] 및 **CmdExec** 단계에만 해당).|  
|**last_run_outcome**|**int**|단계가 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **3** = 취소 됨<br /><br /> **5** = 알 수 없음|  
|**last_run_duration**|**int**|단계를 마지막으로 실행했을 때의 기간(초)입니다.|  
|**last_run_retries**|**int**|단계를 마지막으로 실행했을 때 명령을 재시도할 횟수입니다.|  
|**last_run_date**|**int**|단계가 마지막으로 실행을 시작했을 때의 날짜입니다.|  
|**last_run_time**|**int**|단계가 마지막으로 실행을 시작했을 때의 시간입니다.|  
|**proxy_id**|**int**|작업 단계에 대한 프록시입니다.|  
  
 다음은 작업 일정에 관한 결과 집합입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|모든 작업에서 고유한 일정의 ID입니다.|  
|**schedule_name**|**sysname**|해당 작업에 대해서만 고유한 일정의 이름입니다.|  
|**사용**|**int**|일정이 활성 (**1**) 인지 여부 (**0**) 인지 여부입니다.|  
|**freq_type**|**int**|작업을 실행할 때를 표시하는 값입니다.<br /><br /> **1** = 한 번<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 매월<br /><br /> **32** = 매월, **freq_interval** 기준<br /><br /> **64** = **SQLServerAgent** 서비스를 시작할 때 실행 합니다.|  
|**freq_interval**|**int**|작업이 실행되는 요일입니다. 값은 **freq_type**값에 따라 달라 집니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md) 을 참조 하세요&#41;|  
|**freq_subday_type**|**Int**|**Freq_subday_interval**단위입니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md) 을 참조 하세요&#41;|  
|**freq_subday_interval**|**int**|각 작업 실행 사이에 발생 하는 **freq_subday_type** 기간 수입니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md) 을 참조 하세요&#41;|  
|**freq_relative_interval**|**int**|매월 **freq_interval** 예약 된 작업의 발생입니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md) 을 참조 하세요&#41;|  
|**freq_recurrence_factor**|**int**|작업의 예정된 실행 간의 개월 수입니다.|  
|**active_start_date**|**int**|작업 실행을 시작할 날짜입니다.|  
|**active_end_date**|**int**|작업 실행을 종료할 날짜입니다.|  
|**active_start_time**|**int**|Active_start_date에서 작업 실행을 시작할 시간 **입니다.**|  
|**active_end_time**|**int**|**Active_end_date**에서 작업 실행을 종료 하는 시간입니다.|  
|**date_created**|**datetime**|일정을 만든 날짜입니다.|  
|**schedule_description**|**nvarchar(4000)**|일정에 관한 영어 설명입니다(요청된 경우에 한함).|  
|**next_run_date**|**int**|일정이 다음에 작업을 실행할 날짜입니다.|  
|**next_run_time**|**int**|일정이 다음에 작업을 실행할 시간입니다.|  
|**schedule_uid**|**uniqueidentifier**|일정에 대한 식별자입니다.|  
|**job_count**|**int**|이 일정을 참조하는 작업 수를 반환합니다.|  
  
 다음은 작업 대상 서버의 결과 집합입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|대상 서버의 ID입니다.|  
|**server_name**|**nvarchar (30)**|대상 서버의 컴퓨터 이름입니다.|  
|**enlist_date**|**datetime**|대상 서버가 마스터 서버에 참여한 날짜입니다.|  
|**last_poll_date**|**datetime**|대상 서버가 마지막으로 마스터 서버를 폴링한 날짜입니다.|  
|**last_run_date**|**int**|해당 대상 서버에서 작업이 마지막으로 실행을 시작한 날짜입니다.|  
|**last_run_time**|**int**|해당 대상 서버에서 작업이 마지막으로 실행을 시작한 시간입니다.|  
|**last_run_duration**|**int**|해당 서버에서 작업이 마지막으로 실행되었을 때의 기간입니다.|  
|**last_run_outcome**|**tinyint**|해당 서버에서 작업이 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **3** = 취소 됨<br /><br /> **5** = 알 수 없음|  
|**last_outcome_message**|**nvarchar(1024)**|해당 대상 서버에서 작업이 마지막으로 실행되었을 때의 결과 메시지입니다.|  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **SQLAgentUserRole** 의 멤버는 자신이 소유한 작업만 볼 수 있습니다. **Sysadmin**, **SQLAgentReaderRole**및 **SQLAgentOperatorRole** 의 멤버는 모든 로컬 및 다중 서버 작업을 볼 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-list-information-for-all-jobs"></a>A. 모든 작업에 관한 정보 나열  
 다음 예에서는 매개 변수 없이 `sp_help_job` 프로시저를 실행하여 `msdb` 데이터베이스에 현재 정의되어 있는 모든 작업에 대한 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-matching-a-specific-criteria"></a>B. 특정 조건에 맞는 작업 정보 나열  
 다음 예에서는 작업이 사용되고 실행되고 있는 `françoisa` 소유의 다중 서버 작업에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job   
   @job_type = N'MULTI-SERVER',  
   @owner_login_name = N'françoisa',  
   @enabled = 1,  
   @execution_status = 1 ;  
GO  
```  
  
### <a name="c-listing-all-aspects-of-information-for-a-job"></a>C. 작업에 대한 모든 정보 나열  
 다음 예에서는 `NightlyBackups` 작업에 대한 모든 측면의 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job  
    @job_name = N'NightlyBackups',  
    @job_aspect = N'ALL' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_job &#40;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [Transact-sql&#41;sp_delete_job &#40;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [Transact-sql&#41;sp_update_job &#40;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
