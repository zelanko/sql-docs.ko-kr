---
description: sp_add_jobschedule(Transact-SQL)
title: sp_add_jobschedule (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 46f76ceeba699f614e19b494785c42591ab5299a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549991"
---
# <a name="sp_add_jobschedule-transact-sql"></a>sp_add_jobschedule(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  SQL 에이전트 작업에 대 한 일정을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  > [!IMPORTANT]  
  > [AZURE SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 대부분의 SQL Server 에이전트 기능은 현재 지원 되지 않습니다. 자세한 내용은 [AZURE sql Managed Instance SQL Server에서 t-sql 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) 을 참조 하세요.

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
     [ , [ @schedule_uid = ] _schedule_uid OUTPUT ]
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id` 일정이 추가 된 작업의 작업 id 번호입니다. *job_id* 은 **uniqueidentifier**이며 기본값은 없습니다.  
  
`[ @job_name = ] 'job_name'` 일정을 추가할 작업의 이름입니다. *job_name* 은 **nvarchar (128)** 이며 기본값은 없습니다.  
  
> [!NOTE]  
>  *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
`[ @name = ] 'name'` 일정의 이름입니다. *name* 은 **nvarchar (128)** 이며 기본값은 없습니다.  
  
`[ @enabled = ] enabled_flag` 일정의 현재 상태를 나타냅니다. *enabled_flag* 은 **tinyint**이며 기본값은 **1** (사용)입니다. **0**인 경우 일정을 사용할 수 없습니다. 일정을 사용하지 않으면 작업이 실행되지 않습니다.  
  
`[ @freq_type = ] frequency_type` 작업이 실행 될 시기를 나타내는 값입니다. *frequency_type* 은 **int**이며 기본값은 **0**이 고 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**4**|매일|  
|**8**|매주|  
|**16**|매월|  
|**32**|매월 *frequency_interval 기준입니다.*|  
|**64**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 시작할 때 실행됩니다.|  
|**128**|컴퓨터가 유휴 상태일 때 실행됩니다.|  
  
`[ @freq_interval = ] frequency_interval` 작업이 실행 되는 날짜입니다. *frequency_interval* 은 **int**이며 기본값은 0이 고 다음 표에 나와 있는 것 처럼 *frequency_type* 의 값에 따라 달라 집니다.  
  
|값|효과|  
|-----------|------------|  
|**1** (한 번)|*frequency_interval* 사용 되지 않습니다.|  
|**4** (매일)|*Frequency_interval* 일 마다.|  
|**8** (매주)|*frequency_interval* 는 or 논리 연산자와 결합 된 다음 중 하나 이상입니다.<br /><br /> 1 = 일요일<br /><br /> 2 = 월요일<br /><br /> 4 = 화요일<br /><br /> 8 = 수요일<br /><br /> 16 = 목요일<br /><br /> 32 = 금요일<br /><br /> 64 = 토요일|  
|**16** (매월)|월의 *frequency_interval* 날짜|  
|**32** (매월 상대적)|*frequency_interval* 은 다음 중 하나입니다.<br /><br /> 1 = 일요일<br /><br /> 2 = 월요일<br /><br /> 3 = 화요일<br /><br /> 4 = 수요일<br /><br /> 5 = 목요일<br /><br /> 6 = 금요일<br /><br /> 7 = 토요일<br /><br /> 8 = 일<br /><br /> 9 = 평일<br /><br /> 10 = 주말|  
|**64** ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 시작 되는 경우)|*frequency_interval* 사용 되지 않습니다.|  
|**128**|*frequency_interval* 사용 되지 않습니다.|  
  
`[ @freq_subday_type = ] frequency_subday_type`*Frequency_subday_interval*단위를 지정 합니다. *frequency_subday_type* 은 **int**이며 기본값은 없고 다음 값 중 하나일 수 있습니다.  
  
|값|설명(단위)|  
|-----------|--------------------------|  
|**0x1**|지정된 시간|  
|**0x4**|분|  
|**0x8**|시간|  
  
`[ @freq_subday_interval = ] frequency_subday_interval` 각 작업 실행 사이에 발생 하는 *frequency_subday_type* 기간 수입니다. *frequency_subday_interval* 은 **int**이며 기본값은 0입니다.  
  
`[ @freq_relative_interval = ] frequency_relative_interval`*Frequency_type* 가 **32** (매월 상대적)로 설정 된 경우 *frequency_interval* 를 추가로 정의 합니다.  
  
 *frequency_relative_interval* 은 **int**이며 기본값은 없고 다음 값 중 하나일 수 있습니다.  
  
|값|설명(단위)|  
|-----------|--------------------------|  
|**1**|첫째|  
|**2**|Second|  
|**4**|세 번째|  
|**8**|넷째|  
|**16**|마지막|  
  
 *frequency_relative_interval* 간격의 발생을 나타냅니다. 예를 들어 *frequency_relative_interval* 이 **2**로 설정 되어 있고 *frequency_type* 가 **32**로 설정 되어 있고 *frequency_interval* **3**으로 설정 된 경우 예약 된 작업은 매월 두 번째 화요일에 발생 합니다.  
  
`[ @freq_recurrence_factor = ] frequency_recurrence_factor` 예약 된 작업 실행 사이에 발생 하는 주 또는 월 수입니다. *frequency_recurrence_factor* 는 *frequency_type* 이 **8**, **16**또는 **32**로 설정 된 경우에만 사용 됩니다. *frequency_recurrence_factor* 은 **int**이며 기본값은 0입니다.  
  
`[ @active_start_date = ] active_start_date` 작업 실행을 시작할 수 있는 날짜입니다. *active_start_date* 는 **int**이며 기본값은 없습니다. 날짜 형식은 YYYYMMDD입니다. *Active_start_date* 설정 된 경우 날짜는 19900101 보다 크거나 같아야 합니다.  
  
 일정을 만든 다음 시작 날짜를 검토하여 날짜가 제대로 되어 있는지 확인하십시오. 자세한 내용은 [작업에 대 한 일정 만들기 및 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)의 "시작 날짜 예약" 섹션을 참조 하세요.  
  
`[ @active_end_date = ] active_end_date` 작업 실행을 중지할 수 있는 날짜입니다. *active_end_date* 는 **int**이며 기본값은 없습니다. 날짜 형식은 YYYYMMDD입니다.  
  
`[ @active_start_time = ] active_start_time`*Active_start_date* 와 *active_end_date* 사이의 모든 날짜에 대 한 시간으로 작업 실행을 시작 합니다. *active_start_time* 는 **int**이며 기본값은 없습니다. 시간 형식은 HHMMSS이며 24시간제를 사용합니다.  
  
`[ @active_end_time = active_end_time_`*Active_start_date* 와 *active_end_date* 사이의 모든 날짜에서 작업 실행이 종료 되는 시간입니다. *active_end_time* 는 **int**이며 기본값은 없습니다. 시간 형식은 HHMMSS이며 24시간제를 사용합니다.  
  
`[ @schedule_id = schedule_idOUTPUT` 성공적으로 만들어진 일정 id 번호를 일정에 할당 합니다. *schedule_id* 은 **int**형식의 출력 변수 이며 기본값은 없습니다.  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT` 일정의 고유 식별자입니다. *schedule_uid* 은 **uniqueidentifier**형식의 변수입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 이제 작업 일정을 작업과 독립적으로 관리할 수 있습니다. 작업에 일정을 추가 하려면 **sp_add_schedule** 를 사용 하 여 일정을 만들고 **sp_attach_schedule** 하 여 일정을 작업에 연결 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
 
 ## <a name="example"></a>예제
 다음 예에서는 `SaturdayReports` 매주 토요일 오전 2:00 시에 실행 되는 작업 일정을 할당 합니다.
```sql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>참고 항목  
 [일정을 만들고 작업에 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [작업 예약](../../ssms/agent/schedule-a-job.md)   
 [일정 만들기](../../ssms/agent/create-a-schedule.md)   
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트 ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_add_schedule &#40;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_update_schedule &#40;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_delete_schedule &#40;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_help_schedule &#40;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
