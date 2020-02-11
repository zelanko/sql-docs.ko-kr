---
title: sp_help_jobschedule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobschedule
- sp_help_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobschedule
ms.assetid: 2cded902-9272-4667-ac4b-a4f95a9f008e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 72e321b74f3e949030a6d599c082acf36db12687
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054916"
---
# <a name="sp_help_jobschedule-transact-sql"></a>sp_help_jobschedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]가 자동화된 작업을 수행하는 데 사용하는 작업의 일정에 관한 정보를 반환합니다.  
 
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_jobschedule { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @schedule_name = ] 'schedule_name' ]  
     [ , [ @schedule_id = ] schedule_id ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id`작업 id입니다. *job_id*은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'`작업의 이름입니다. *job_name*는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]
> *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.

`[ @schedule_name = ] 'schedule_name'`작업에 대 한 일정 항목의 이름입니다. *schedule_name*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @schedule_id = ] schedule_id`작업에 대 한 일정 항목의 id 번호입니다. *schedule_id*은 **int**이며 기본값은 NULL입니다.  
  
`[ @include_description = ] include_description`결과 집합에 일정에 대 한 설명을 포함할지 여부를 지정 합니다. *include_description* 은 **bit**이며 기본값은 **0**입니다. *Include_description* **0**이면 일정에 대 한 설명이 결과 집합에 포함 되지 않습니다. *Include_description* **1**이면 일정에 대 한 설명이 결과 집합에 포함 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|일정 ID입니다.|  
|**schedule_name**|**sysname**|일정 이름입니다.|  
|**사용**|**int**|일정 사용 (**1**) 또는 사용 안 함 (**0**)을 지정 합니다.|  
|**freq_type**|**int**|작업을 실행할 때를 지정하는 값입니다.<br /><br /> **1** = 한 번<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 매월<br /><br /> **32** = 매월, **freq_interval** 기준<br /><br /> **64** = **SQLServerAgent** 서비스를 시작할 때 실행 합니다.|  
|**freq_interval**|**int**|작업이 실행되는 요일입니다. 값은 **freq_type**값에 따라 달라 집니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)를 참조 하세요.|  
|**freq_subday_type**|**int**|**Freq_subday_interval**단위입니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)를 참조 하세요.|  
|**freq_subday_interval**|**int**|각 작업 실행 사이에 발생 하는 **freq_subday_type** 기간 수입니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)를 참조 하세요.|  
|**freq_relative_interval**|**int**|매월 **freq_interval** 예약 된 작업의 발생입니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)를 참조 하세요.|  
|**freq_recurrence_factor**|**int**|작업의 예정된 실행 간의 개월 수입니다.|  
|**active_start_date**|**int**|일정을 활성화하는 날짜입니다.|  
|**active_end_date**|**int**|일정을 종료하는 날짜입니다.|  
|**active_start_time**|**int**|일정을 시작하는 시간입니다.|  
|**active_end_time**|**int**|일정을 종료하는 시간입니다.|  
|**date_created**|**datetime**|일정을 만든 날짜입니다.|  
|**schedule_description**|**nvarchar(4000)**|**Msdb**의 값에서 파생 된 일정에 대 한 영어 설명입니다. *Include_description* **0**인 경우이 열에는 설명이 요청 되지 않았음을 나타내는 텍스트가 포함 됩니다.|  
|**next_run_date**|**int**|일정이 다음에 작업을 실행할 날짜입니다.|  
|**next_run_time**|**int**|일정이 다음에 작업을 실행할 시간입니다.|  
|**schedule_uid**|**uniqueidentifier**|일정에 대한 식별자입니다.|  
|**job_count**|**int**|반환된 작업 수입니다.|  
  
> **참고: sp_help_jobschedule** **은 (는**) **dbo. sysjobschedules** 및 **dbo. sys일정** 시스템 테이블의 값을 반환 합니다. **sysjobschedules** 분 마다 업데이트를 예약 합니다. 이는 저장 프로시저에서 반환하는 값에 영향을 줄 수 있습니다.  
  
## <a name="remarks"></a>설명  
 **Sp_help_jobschedule** 매개 변수는 특정 조합 에서만 사용할 수 있습니다. *Schedule_id* 지정 된 경우에는 *job_id* 와 *job_name* 를 지정할 수 없습니다. 그렇지 않으면 *job_id* 또는 *job_name* 매개 변수를 *schedule_name*와 함께 사용할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **SQLAgentUserRole** 의 멤버는 자신이 소유한 작업 일정 속성만 볼 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-job-schedule-for-a-specific-job"></a>A. 특정 작업에 대한 작업 일정 반환  
 다음 예에서는 `BackupDatabase`라는 작업에 관한 일정 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'BackupDatabase' ;  
GO  
```  
  
### <a name="b-returning-the-job-schedule-for-a-specific-schedule"></a>B. 특정 일정에 대한 작업 일정 반환  
 다음 예에서는 `NightlyJobs`라는 일정과 `RunReports`라는 작업에 관한 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule   
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="c-returning-the-job-schedule-and-schedule-description-for-a-specific-schedule"></a>C. 특정 일정에 대한 작업 일정 및 일정 설명 반환  
 다음 예에서는 `NightlyJobs`라는 일정과 `RunReports`라는 작업에 관한 정보를 반환합니다. 반환된 결과 집합에는 일정 설명이 포함됩니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs',  
    @include_description = 1 ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_schedule &#40;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_delete_schedule &#40;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_update_schedule &#40;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
