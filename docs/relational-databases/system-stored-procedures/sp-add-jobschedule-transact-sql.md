---
title: sp_add_jobschedule (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobschedule
- sp_add_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobschedule
ms.assetid: ffce19d9-d1d6-45b4-89fd-ad0f60822ba0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e20d30b63a1cc387c6b997c8a8a11bab835e21f8
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493365"
---
# <a name="spaddjobschedule-transact-sql"></a>sp_add_jobschedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  작업의 일정을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_jobschedule [ @job_id = ] job_id, | [ @job_name = ] 'job_name', [ @name = ] 'name'  
     [ , [ @enabled = ] enabled_flag ]  
     [ , [ @freq_type = ] frequency_type ]  
     [ , [ @freq_interval = ] frequency_interval ]  
     [ , [ @freq_subday_type = ] frequency_subday_type ]  
     [ , [ @freq_subday_interval = ] frequency_subday_interval ]  
     [ , [ @freq_relative_interval = ] frequency_relative_interval ]  
     [ , [ @freq_recurrence_factor = ] frequency_recurrence_factor ]  
     [ , [ @active_start_date = ] active_start_date ]  
     [ , [ @active_end_date = ] active_end_date ]  
     [ , [ @active_start_time = ] active_start_time ]  
     [ , [ @active_end_time = ] active_end_time ]  
     [ , [ @schedule_id = ] schedule_id OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id` 작업 일정을 추가한 작업의 id. *job_id* 됩니다 **uniqueidentifier**, 기본값은 없습니다.  
  
`[ @job_name = ] 'job_name'` 일정을 추가할 작업의 이름입니다. *job_name* 됩니다 **nvarchar (128)**, 기본값은 없습니다.  
  
> [!NOTE]  
>  어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
`[ @name = ] 'name'` 일정의 이름입니다. *이름을* 됩니다 **nvarchar (128)**, 기본값은 없습니다.  
  
`[ @enabled = ] enabled_flag` 일정의 현재 상태를 나타냅니다. *enabled_flag* 됩니다 **tinyint**, 기본값은 **1** (사용). 하는 경우 **0**, 일정은 사용할 수 없습니다. 일정을 사용하지 않으면 작업이 실행되지 않습니다.  
  
`[ @freq_type = ] frequency_type` 작업이 실행 되는 경우를 나타내는 값입니다. *frequency_type* 됩니다 **int**, 기본값은 **0**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**4**|일별|  
|**8**|매주|  
|**16**|매월|  
|**32**|기준으로 월별 *frequency_interval 합니다.*|  
|**64**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 시작할 때 실행됩니다.|  
|**128**|컴퓨터가 유휴 상태일 때 실행됩니다.|  
  
`[ @freq_interval = ] frequency_interval` 작업이 실행 되는 날짜입니다. *frequency_interval* 됩니다 **int**, 기본값은 0 사용 하 여 값에 따라 달라 집니다 *frequency_type* 다음 표와 같이:  
  
|값|영향|  
|-----------|------------|  
|**1** (한 번)|*frequency_interval* 사용 되지 않습니다.|  
|**4** (매일)|모든 *frequency_interval* 일입니다.|  
|**8** (매주)|*frequency_interval* (OR 논리 연산자와 결합) 다음 중 하나 이상입니다.<br /><br /> 1 = 일요일<br /><br /> 2 = 월요일<br /><br /> 4 = 화요일<br /><br /> 8 = 수요일<br /><br /> 16 = 목요일<br /><br /> 32 = 금요일<br /><br /> 64 = 토요일|  
|**16** (매월)|에 *frequency_interval* 월의 일입니다.|  
|**32** (매월 상대적)|*frequency_interval* 다음 중 하나입니다.<br /><br /> 1 = 일요일<br /><br /> 2 = 월요일<br /><br /> 3 = 화요일<br /><br /> 4 = 수요일<br /><br /> 5 = 목요일<br /><br /> 6 = 금요일<br /><br /> 7 = 토요일<br /><br /> 8 = 일<br /><br /> 9 = 평일<br /><br /> 10 = 주말|  
|**64** (때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 시작)|*frequency_interval* 사용 되지 않습니다.|  
|**128**|*frequency_interval* 사용 되지 않습니다.|  
  
`[ @freq_subday_type = ] frequency_subday_type` 단위를 지정 *frequency_subday_interval*합니다. *frequency_subday_type* 됩니다 **int**기본값은 없고 수 이며 다음 값 중 하나일 수:  
  
|값|설명(단위)|  
|-----------|--------------------------|  
|**0x1**|지정된 시간|  
|**0x4**|분|  
|**0x8**|시간|  
  
`[ @freq_subday_interval = ] frequency_subday_interval` 수가 *frequency_subday_type* 작업의 각 실행 간에 발생 하는 기간. *frequency_subday_interval* 됩니다 **int**, 기본값은 0입니다.  
  
`[ @freq_relative_interval = ] frequency_relative_interval` 추가 정의 *frequency_interval* 때 *frequency_type* 로 설정 되어 **32** (매월 상대적)입니다.  
  
 *frequency_relative_interval* 됩니다 **int**기본값은 없고 수 이며 다음 값 중 하나일 수:  
  
|값|설명(단위)|  
|-----------|--------------------------|  
|**1**|첫째|  
|**2**|Second|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
 *frequency_relative_interval* 간격의 발생 빈도 나타냅니다. 예를 들어 경우 *frequency_relative_interval* 로 설정 된 **2**에 *frequency_type* 로 설정 되어 **32**, 및 *frequency_ 간격* 로 설정 된 **3**, 예약된 된 작업을 매월 두 번째 화요일에 발생 합니다.  
  
`[ @freq_recurrence_factor = ] frequency_recurrence_factor` 예약된 된 작업 실행 간의 주 또는 월 수입니다. *frequency_recurrence_factor* 경우에 사용 됩니다 *frequency_type* 로 설정 되어 **8**를 **16**, 또는 **32**합니다. *frequency_recurrence_factor* 됩니다 **int**, 기본값은 0입니다.  
  
`[ @active_start_date = ] active_start_date` 날짜는 작업 실행을 시작할 수 있습니다. *active_start_date* 됩니다 **int**, 기본값은 없습니다. 날짜 형식은 YYYYMMDD입니다. 하는 경우 *active_start_date* 설정 날짜 보다 크거나 19900101 이어야 합니다.  
  
 일정을 만든 다음 시작 날짜를 검토하여 날짜가 제대로 되어 있는지 확인하십시오. 자세한 내용은 "시작 날짜 예약" 섹션을 참조 [만들기 및 작업에 일정 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)합니다.  
  
`[ @active_end_date = ] active_end_date` 날짜는 작업 실행이 중지 수 있습니다. *active_end_date* 됩니다 **int**, 기본값은 없습니다. 날짜 형식은 YYYYMMDD입니다.  
  
`[ @active_start_time = ] active_start_time` 사이의 임의의 날짜에서 시간 *active_start_date* 하 고 *active_end_date* 작업 실행을 시작 합니다. *active_start_time* 됩니다 **int**, 기본값은 없습니다. 시간 형식은 HHMMSS이며 24시간제를 사용합니다.  
  
`[ @active_end_time = active_end_time_` 사이의 임의의 날짜에서 시간 *active_start_date* 하 고 *active_end_date* 작업 실행을 종료 합니다. *active_end_time* 됩니다 **int**, 기본값은 없습니다. 시간 형식은 HHMMSS이며 24시간제를 사용합니다.  
  
`[ @schedule_id = schedule_idOUTPUT` 성공적으로 만들어진 경우 일정에 할당 된 id 번호를 예약 합니다. *schedule_id* 는 형식의 출력 변수 **int**, 기본값은 없습니다.  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT` 일정에 대 한 고유 식별자입니다. *schedule_uid* 형식의 변수가 **uniqueidentifier**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 이제 작업 일정을 작업과 독립적으로 관리할 수 있습니다. 작업에 일정을 추가 하려면 사용 **sp_add_schedule** 일정을 만들 및 **sp_attach_schedule** 작업에 일정을 연결 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
 
 ## <a name="example"></a>예제
 다음 예제에서는 할당 하는 작업 일정 `SaturdayReports` 는 매주 토요일 오전 2 시에 실행 됩니다.
```sql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>관련 항목  
 [만들기 및 작업에 일정 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [작업 예약](../../ssms/agent/schedule-a-job.md)   
 [일정 만들기](../../ssms/agent/create-a-schedule.md)   
 [SQL Server 에이전트 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_update_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
