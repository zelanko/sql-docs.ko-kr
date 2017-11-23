---
title: sp_help_jobschedule (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_jobschedule
- sp_help_jobschedule_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_jobschedule
ms.assetid: 2cded902-9272-4667-ac4b-a4f95a9f008e
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1f111a04bfe27fad284157082ec1bbbeadfb92c8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpjobschedule-transact-sql"></a>sp_help_jobschedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]가 자동화된 작업을 수행하는 데 사용하는 작업의 일정에 관한 정보를 반환합니다.  
 
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_jobschedule { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @schedule_name = ] 'schedule_name' ]  
     [ , [ @schedule_id = ] schedule_id ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@job_id=** ] *job_id*  
 작업 ID입니다. *job_id*은 **uniqueidentifier**, 기본값은 NULL입니다.  
  
 [  **@job_name=** ] **'***job_name***'**  
 작업의 이름입니다. *job_name*은 **sysname**, 기본값은 NULL입니다.  
  
> **참고:** 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [  **@schedule_name=** ] **'***schedule_name***'**  
 작업에 대한 일정 항목의 이름입니다. *schedule_name*은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@schedule_id=** ] *schedule_id*  
 작업에 대한 일정 항목의 ID입니다. *schedule_id*은 **int**, 기본값은 NULL입니다.  
  
 [  **@include_description=** ] *include_description*  
 결과 집합에 일정에 대한 설명을 포함할지 여부를 지정합니다. *include_description* 은 **비트**, 기본값은 **0**합니다. 때 *include_description* 은 **0**는 일정 설명이 결과 집합에 포함 되지 않습니다. 때 *include_description* 은 **1**는 일정 설명이 결과 집합에 포함 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|일정 ID입니다.|  
|**schedule_name**|**sysname**|일정 이름입니다.|  
|**사용 하도록 설정**|**int**|일정을 사용할지 (**1**) 또는 사용 안 함 (**0**).|  
|**freq_type**|**int**|작업을 실행할 때를 지정하는 값입니다.<br /><br /> **1** = 한 번<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 매월<br /><br /> **32** 기준으로 = 매월는 **freq_interval**<br /><br /> **64** = 때 실행할 **SQLServerAgent** 서비스가 시작 합니다.|  
|**freq_interval**|**int**|작업이 실행되는 요일입니다. 값의 값에 따라 **freq_type**합니다. 자세한 내용은 참조 [sp_add_schedule &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_type**|**int**|에 대 한 단위 **freq_subday_interval**합니다. 자세한 내용은 참조 [sp_add_schedule &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_interval**|**int**|수가 **freq_subday_type** 작업의 실행 사이 발생 하는 기간. 자세한 내용은 참조 [sp_add_schedule &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_relative_interval**|**int**|작업 발생 횟수의 예약 된 **freq_interval** 각 월에 합니다. 자세한 내용은 참조 [sp_add_schedule &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_recurrence_factor**|**int**|작업의 예정된 실행 간의 개월 수입니다.|  
|**active_start_date**|**int**|일정을 활성화하는 날짜입니다.|  
|**active_end_date**|**int**|일정을 종료하는 날짜입니다.|  
|**active_start_time**|**int**|일정을 시작하는 시간입니다.|  
|**active_end_time**|**int**|일정을 종료하는 시간입니다.|  
|**date_created**|**datetime**|일정을 만든 날짜입니다.|  
|**schedule_description**|**nvarchar(4000)**|값에서 파생 된 일정의 영어 설명 **msdb.dbo.sysschedules**합니다. 때 *include_description* 은 **0**,이 열에 대 한 설명을 요청 되지 않았다는 텍스트가 포함 됩니다.|  
|**next_run_date**|**int**|일정이 다음에 작업을 실행할 날짜입니다.|  
|**next_run_time**|**int**|일정이 다음에 작업을 실행할 시간입니다.|  
|**schedule_uid**|**uniqueidentifier**|일정에 대한 식별자입니다.|  
|**job_count**|**int**|반환된 작업 수입니다.|  
  
> **참고:****sp_help_jobschedule** 에서 값을 반환 된 **dbo.sysjobschedules** 및 **dbo.sysschedules** 시스템 테이블 **msdb** .   **sysjobschedules** 20 분 마다 업데이트 됩니다. 이는 저장 프로시저에서 반환하는 값에 영향을 줄 수 있습니다.  
  
## <a name="remarks"></a>주의  
 매개 변수 **sp_help_jobschedule** 특정 조합에만 사용할 수 있습니다. 경우 *schedule_id* 지정한 경우에 *job_id* 나 *job_name* 지정할 수 있습니다. 그렇지 않은 경우는 *job_id* 또는 *job_name* 매개 변수는 함께 사용할 수 있습니다 *schedule_name*합니다.  
  
## <a name="permissions"></a>Permissions  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
 멤버 **SQLAgentUserRole** 는 각자 소유한 작업 일정의 속성만 볼 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-job-schedule-for-a-specific-job"></a>1. 특정 작업에 대한 작업 일정 반환  
 다음 예에서는 `BackupDatabase`라는 작업에 관한 일정 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'BackupDatabase' ;  
GO  
```  
  
### <a name="b-returning-the-job-schedule-for-a-specific-schedule"></a>2. 특정 일정에 대한 작업 일정 반환  
 다음 예에서는 `NightlyJobs`라는 일정과 `RunReports`라는 작업에 관한 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule   
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="c-returning-the-job-schedule-and-schedule-description-for-a-specific-schedule"></a>3. 특정 일정에 대한 작업 일정 및 일정 설명 반환  
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
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_schedule&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_schedule &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_update_schedule &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
