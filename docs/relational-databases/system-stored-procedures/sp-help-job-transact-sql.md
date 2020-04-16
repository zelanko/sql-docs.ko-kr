---
title: sp_help_job (거래 -SQL) | 마이크로 소프트 문서
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
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
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
`[ @job_id = ] job_id`작업 식별 번호입니다. *job_id* 기본값인 NULL을 가진 **고유 식별자입니다.**  
  
`[ @job_name = ] 'job_name'`작업의 이름입니다. *job_name* **sysname이며**기본값은 NULL입니다.  
  
> [!NOTE]  
>  특정 작업을 보려면 *job_id* 또는 *job_name* 지정해야 합니다.  *job_id* *job_name* 모두 생략하여 모든 작업에 대한 정보를 반환합니다.
  
`[ @job_aspect = ] 'job_aspect'`표시할 작업 특성입니다. *job_aspect* **varchar(9)**- NULL의 기본값을 가지며 이러한 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**ALL**|작업 항목 정보입니다.|  
|**작업**|작업 정보입니다.|  
|**일정**|일정 정보입니다.|  
|**단계**|작업 단계 정보입니다.|  
|**대상**|대상 정보입니다.|  
  
`[ @job_type = ] 'job_type'`보고서에 포함할 작업 유형입니다. *job_type* **varchar(12)이며**기본값은 NULL입니다. *job_type* **로컬** 또는 **다중 서버일**수 있습니다.  
  
`[ @owner_login_name = ] 'login_name'`작업 소유자의 로그인 이름입니다. *login_name* **sysname이며**기본값은 NULL입니다.  
  
`[ @subsystem = ] 'subsystem'`하위 시스템의 이름입니다. *하위 시스템은* **nvarchar(40)이며**기본값은 NULL입니다.  
  
`[ @category_name = ] 'category'`범주의 이름입니다. *범주는* **sysname**, NULL의 기본값입니다.  
  
`[ @enabled = ] enabled`활성화된 작업 또는 비활성화된 작업에 대한 정보가 표시되는지 여부를 나타내는 숫자입니다. *사용은* NULL의 기본값으로 **tinyint입니다.** **1은** 사용 가능한 작업을 나타내고 **0은** 비활성화된 작업을 나타냅니다.  
  
`[ @execution_status = ] status`작업에 대한 실행 상태입니다. *상태는* NULL의 기본값을 가진 **int이며**이러한 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|유휴 또는 일시 중지 상태가 아닌 작업만 반환합니다.|  
|**1**|실행 중입니다.|  
|**2**|스레드 대기 중입니다.|  
|**3**|재시도 중입니다.|  
|**4**|유휴 상태입니다.|  
|**5**|일시 중지 상태입니다.|  
|**7**|동작을 완전히 수행하였습니다.|  
  
`[ @date_comparator = ] 'date_comparison'`*date_created* 및 *date_modified*비교하여 사용하는 비교 연산자 . *date_comparison* **char(1)이며**=, \<또는 > 수 있습니다.  
  
`[ @date_created = ] date_created`작업이 만들어진 날짜입니다. *date_created* **DATEtime이며**기본값은 NULL입니다.  
  
`[ @date_last_modified = ] date_modified`작업이 마지막으로 수정된 날짜입니다. *date_modified* **DATEtime이며**기본값은 NULL입니다.  
  
`[ @description = ] 'description_pattern'`작업에 대한 설명입니다. *description_pattern* **nvarchar (512)이며**기본값은 NULL입니다. *description_pattern* 패턴 일치를 위해 SQL Server 와일드카드 문자를 포함할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0(성공)** 또는 **1(실패)**  
  
## <a name="result-sets"></a>결과 집합  
 인수를 지정하지 않으면 **sp_help_job** 이 결과 집합을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**Job_id**|**uniqueidentifier**|작업의 고유 ID입니다.|  
|**originating_server**|**nvarchar(30)**|작업을 가져온 서버의 이름입니다.|  
|**name**|**Sysname**|작업의 이름입니다.|  
|**사용**|**tinyint**|작업을 실행할 수 있는지를 표시합니다.|  
|**설명**|**nvarchar(512)**|작업 설명입니다.|  
|**start_step_id**|**Int**|실행을 시작해야 하는 작업 단계의 ID입니다.|  
|**범주**|**Sysname**|작업 범주입니다.|  
|**소유자**|**Sysname**|작업 소유자입니다.|  
|**notify_level_eventlog**|**Int**|Microsoft Windows 응용 프로그램 로그에 알림 이벤트를 기록해야 하는 상황을 나타내는 **비트 마스크입니다.** 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **0** = 안 없음<br /><br /> **1** = 작업이 성공할 때<br /><br /> **2** = 작업이 실패할 때<br /><br /> **3** = 작업이 완료될 때마다(작업 결과에 관계 없음)|  
|**notify_level_email**|**Int**|작업이 완료될 때 알림 전자 메일을 보내야 하는 상황을 나타내는 **Bitmask입니다.** 가능한 값은 **notify_level_eventlog.**|  
|**notify_level_netsend**|**Int**|작업이 완료될 때 네트워크 메시지를 보내야 하는 상황을 나타내는 **비트 마스크입니다.** 가능한 값은 **notify_level_eventlog.**|  
|**notify_level_page**|**Int**|작업이 완료될 때 페이지를 보내야 하는 상황을 나타내는 **비트 마스크입니다.** 가능한 값은 **notify_level_eventlog.**|  
|**notify_email_operator**|**Sysname**|정보를 알릴 운영자의 전자 메일 이름입니다.|  
|**notify_netsend_operator**|**Sysname**|네트워크 메시지를 전달할 때 사용하는 컴퓨터 또는 사용자의 이름입니다.|  
|**notify_page_operator**|**Sysname**|네트워크 메시지를 전달할 때 사용하는 컴퓨터 또는 사용자의 이름입니다.|  
|**delete_level**|**Int**|**작업이** 완료될 때 작업을 삭제해야 하는 상황을 나타내는 비트 마스크입니다. 가능한 값은 **notify_level_eventlog.**|  
|**date_created**|**datetime**|작업을 만든 날짜입니다.|  
|**date_modified**|**datetime**|작업을 마지막으로 수정한 날짜입니다.|  
|**version_number**|**Int**|작업의 버전입니다. 작업이 수정될 때마다 자동으로 업데이트됩니다.|  
|**last_run_date**|**Int**|작업이 마지막으로 실행을 시작한 날짜입니다.|  
|**last_run_time**|**Int**|작업이 마지막으로 실행을 시작한 시간입니다.|  
|**last_run_outcome**|**Int**|작업이 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **3** = 취소<br /><br /> **5** = 알 수 없음|  
|**next_run_date**|**Int**|다음 작업 실행 일정의 날짜입니다.|  
|**next_run_time**|**Int**|다음 작업 실행 일정의 시간입니다.|  
|**next_run_schedule_id**|**Int**|다음 실행 일정의 ID입니다.|  
|**current_execution_status**|**Int**|현재 실행 상태:<br /><br /> **1** = 실행 중<br /><br /> **2** = 스레드 대기 중<br /><br /> **3** = 재시도 사이<br /><br /> **4** = 유휴 상태<br /><br /> **5** = 일시 중단됨<br /><br /> **6** = 더 이상 사용되지 않음<br /><br /> **7** = 완료 작업 수행|  
|**current_execution_step**|**Sysname**|작업의 현재 실행 단계입니다.|  
|**current_retry_attempt**|**Int**|작업이 실행 중이며 단계가 다시 시도된 경우의 현재 재시도입니다.|  
|**has_step**|**Int**|작업이 갖고 있는 단계 수입니다.|  
|**has_schedule**|**Int**|작업이 갖고 있는 작업 일정 수입니다.|  
|**has_target**|**Int**|작업이 갖고 있는 대상 서버 수입니다.|  
|**종류**|**Int**|작업의 유형입니다.<br /><br /> 1 = 로컬 작업<br /><br /> **2** = 멀티 서버 작업.<br /><br /> **0** = 작업에 대상 서버가 없습니다.|  
  
 *job_id* 또는 *job_name* 지정하면 **sp_help_job** 작업 단계, 작업 일정 및 작업 대상 서버에 대해 이러한 추가 결과 집합을 반환합니다.  
  
 다음은 작업 단계에 관한 결과 집합입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**step_id**|**Int**|해당 작업에 관한 단계의 고유 ID입니다.|  
|**step_name**|**Sysname**|단계의 이름입니다.|  
|**하위**|**nvarchar(40)**|단계 명령을 실행할 하위 시스템입니다.|  
|**명령**|**nvarchar (3200)**|실행할 명령입니다.|  
|**플래그**|**nvarchar(4000)**|단계 동작을 제어하는 값의 **비트 마스크입니다.**|  
|**cmdexec_success_code**|**Int**|**CmdExec** 단계의 경우 성공적인 명령의 프로세스 종료 코드입니다.|  
|**on_success_action**|**nvarchar(4000)**|단계가 성공할 경우 수행되는 작업입니다.<br /><br /> **1** = 성공으로 종료합니다.<br /><br /> **2** = 실패로 종료합니다.<br /><br /> **3** = 다음 단계로 이동합니다.<br /><br /> **4** = 단계로 이동합니다.|  
|**on_success_step_id**|**Int**|**on_success_action** **경우**실행해야 할 다음 단계를 나타냅니다.|  
|**on_fail_action**|**nvarchar(4000)**|단계가 실패한 경우에 수행할 동작입니다. 값은 **on_success_action.**|  
|**on_fail_step_id**|**Int**|**on_fail_action** **4이면**다음 단계를 실행합니다.|  
|**서버**|**Sysname**|예약되어 있습니다.|  
|**database_name**|**Sysname**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 단계의 경우 명령이 실행될 데이터베이스입니다.|  
|**database_user_name**|**Sysname**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 단계의 경우 명령이 실행되는 데이터베이스 사용자 컨텍스트입니다.|  
|**retry_attempts**|**Int**|단계가 성공하지 못한 경우에 해당 단계를 실패로 간주하기 전에 명령을 재시도할 최대 횟수입니다.|  
|**retry_interval**|**Int**|재시도 간의 간격(분)입니다.|  
|**os_run_priority**|**바르차르 (4000)**|예약되어 있습니다.|  
|**output_file_name**|**바르차르 (200)**|명령 출력을 작성해야 하는[!INCLUDE[tsql](../../includes/tsql-md.md)] 파일(및 **CmdExec** 단계만).|  
|**last_run_outcome**|**Int**|단계가 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **3** = 취소<br /><br /> **5** = 알 수 없음|  
|**last_run_duration**|**Int**|단계를 마지막으로 실행했을 때의 기간(초)입니다.|  
|**last_run_retries**|**Int**|단계를 마지막으로 실행했을 때 명령을 재시도할 횟수입니다.|  
|**last_run_date**|**Int**|단계가 마지막으로 실행을 시작했을 때의 날짜입니다.|  
|**last_run_time**|**Int**|단계가 마지막으로 실행을 시작했을 때의 시간입니다.|  
|**proxy_id**|**Int**|작업 단계에 대한 프록시입니다.|  
  
 다음은 작업 일정에 관한 결과 집합입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**Int**|모든 작업에서 고유한 일정의 ID입니다.|  
|**schedule_name**|**Sysname**|해당 작업에 대해서만 고유한 일정의 이름입니다.|  
|**사용**|**Int**|일정이 활성 상태인지 여부 **(1)****(0).**|  
|**freq_type**|**Int**|작업을 실행할 때를 표시하는 값입니다.<br /><br /> **1** = 한 번<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 월간<br /><br /> **32** = 월별, **freq_interval** 상대<br /><br /> **64** = **SQLServerAgent** 서비스가 시작될 때 실행됩니다.|  
|**freq_interval**|**Int**|작업이 실행되는 요일입니다. 값은 **freq_type**값에 따라 달라집니다. 자세한 내용은 [sp_add_schedule &#40;거래-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_subday_type**|**Int**|**freq_subday_interval**단위입니다. 자세한 내용은 [sp_add_schedule &#40;거래-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_subday_interval**|**Int**|작업의 각 실행 사이에 발생하는 **freq_subday_type** 기간의 수입니다. 자세한 내용은 [sp_add_schedule &#40;거래-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_relative_interval**|**Int**|매월 **freq_interval** 예약된 작업의 발생입니다. 자세한 내용은 [sp_add_schedule &#40;거래-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_recurrence_factor**|**Int**|작업의 예정된 실행 간의 개월 수입니다.|  
|**active_start_date**|**Int**|작업 실행을 시작할 날짜입니다.|  
|**active_end_date**|**Int**|작업 실행을 종료할 날짜입니다.|  
|**active_start_time**|**Int**|active_start_date 작업 실행을 시작할 **시간입니다.**|  
|**active_end_time**|**Int**|**active_end_date**작업의 실행을 종료할 시간입니다.|  
|**date_created**|**datetime**|일정을 만든 날짜입니다.|  
|**schedule_description**|**nvarchar(4000)**|일정에 관한 영어 설명입니다(요청된 경우에 한함).|  
|**next_run_date**|**Int**|일정이 다음에 작업을 실행할 날짜입니다.|  
|**next_run_time**|**Int**|일정이 다음에 작업을 실행할 시간입니다.|  
|**schedule_uid**|**uniqueidentifier**|일정에 대한 식별자입니다.|  
|**job_count**|**Int**|이 일정을 참조하는 작업 수를 반환합니다.|  
  
 다음은 작업 대상 서버의 결과 집합입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**Int**|대상 서버의 ID입니다.|  
|**server_name**|**nvarchar(30)**|대상 서버의 컴퓨터 이름입니다.|  
|**enlist_date**|**datetime**|대상 서버가 마스터 서버에 참여한 날짜입니다.|  
|**last_poll_date**|**datetime**|대상 서버가 마지막으로 마스터 서버를 폴링한 날짜입니다.|  
|**last_run_date**|**Int**|해당 대상 서버에서 작업이 마지막으로 실행을 시작한 날짜입니다.|  
|**last_run_time**|**Int**|해당 대상 서버에서 작업이 마지막으로 실행을 시작한 시간입니다.|  
|**last_run_duration**|**Int**|해당 서버에서 작업이 마지막으로 실행되었을 때의 기간입니다.|  
|**last_run_outcome**|**tinyint**|해당 서버에서 작업이 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **3** = 취소<br /><br /> **5** = 알 수 없음|  
|**last_outcome_message**|**nvarchar(1024)**|해당 대상 서버에서 작업이 마지막으로 실행되었을 때의 결과 메시지입니다.|  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **SQLAgentUserRole의** 구성원은 자신이 소유한 작업만 볼 수 있습니다. 시스템 **관리자,** **SQLAgentReaderRole**및 **SQL에이전트연수롤의** 구성원은 모든 로컬 및 다중 서버 작업을 볼 수 있습니다.  
  
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
 [sp_add_job &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_update_job &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
