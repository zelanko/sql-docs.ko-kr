---
title: sp_add_schedule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_schedule_TSQL
- sp_add_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_schedule
ms.assetid: 9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 88dafeff6621a181b3720917235705d4e0b12e2d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85878288"
---
# <a name="sp_add_schedule-transact-sql"></a>sp_add_schedule(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  여러 작업에서 사용할 수 있는 일정을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_schedule [ @schedule_name = ] 'schedule_name'   
    [ , [ @enabled = ] enabled ]  
    [ , [ @freq_type = ] freq_type ]  
    [ , [ @freq_interval = ] freq_interval ]   
    [ , [ @freq_subday_type = ] freq_subday_type ]   
    [ , [ @freq_subday_interval = ] freq_subday_interval ]   
    [ , [ @freq_relative_interval = ] freq_relative_interval ]   
    [ , [ @freq_recurrence_factor = ] freq_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time = ] active_start_time ]   
    [ , [ @active_end_time = ] active_end_time ]   
    [ , [ @owner_login_name = ] 'owner_login_name' ]  
    [ , [ @schedule_uid = ] schedule_uid OUTPUT ]  
    [ , [ @schedule_id = ] schedule_id OUTPUT ]
    [ , [ @originating_server = ] server_name ] /* internal */  
```  
  
## <a name="arguments"></a>인수  
`[ @schedule_name = ] 'schedule_name'`일정의 이름입니다. *schedule_name* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @enabled = ] enabled`일정의 현재 상태를 나타냅니다. *enabled* 는 **tinyint**이며 기본값은 **1** (사용)입니다. **0**인 경우 일정을 사용할 수 없습니다. 일정을 사용할 수 없는 경우 이 일정에 따라 어떠한 작업도 실행되지 않습니다.  
  
`[ @freq_type = ] freq_type`작업이 실행 될 시기를 나타내는 값입니다. *freq_type* 은 **int**이며 기본값은 **0**이 고 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**4**|매일|  
|**8**|매주|  
|**16**|매월|  
|**32**|매월, *freq_interval* 기준|  
|**64**|SQL 에이전트 서비스를 시작할 때 실행|  
|**128**|컴퓨터가 유휴 상태일 때 실행 됩니다 ( [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)에서 지원 되지 않음). |  
  
`[ @freq_interval = ] freq_interval`작업이 실행 되는 요일입니다. *freq_interval* 은 **int**이며 기본값은 **1**이 고 *freq_type*의 값에 따라 달라 집니다.  
  
|*Freq_type* 의 값|*Freq_interval* 에 대 한 영향|  
|---------------------------|--------------------------------|  
|**1** (한 번)|*freq_interval* 사용 되지 않습니다.|  
|**4** (매일)|*Freq_interval* 일 마다.|  
|**8** (매주)|*freq_interval* 는 or 논리 연산자와 결합 된 다음 중 하나 이상입니다.<br /><br /> **1** = 일요일<br /><br /> **2** = 월요일<br /><br /> **4** = 화요일<br /><br /> **8** = 수요일<br /><br /> **16** = 목요일<br /><br /> **32** = 금요일<br /><br /> **64** = 토요일|  
|**16** (매월)|월의 *freq_interval* 날짜|  
|**32** (매월 상대적)|*freq_interval* 은 다음 중 하나입니다.<br /><br /> **1** = 일요일<br /><br /> **2** = 월요일<br /><br /> **3** = 화요일<br /><br /> **4** = 수요일<br /><br /> **5** = 목요일<br /><br /> **6** = 금요일<br /><br /> **7** = 토요일<br /><br /> **8** = 일<br /><br /> **9** = 평일<br /><br /> **10** = 주말|  
|**64** (SQLServerAgent 서비스가 시작 되는 경우)|*freq_interval* 사용 되지 않습니다.|  
|**128**|*freq_interval* 사용 되지 않습니다.|  
  
`[ @freq_subday_type = ] freq_subday_type`*Freq_subday_interval*단위를 지정 합니다. *freq_subday_type* 은 **int**이며 기본값은 **0**이 고 다음 값 중 하나일 수 있습니다.  
  
|값|설명(단위)|  
|-----------|--------------------------|  
|**0x1**|지정된 시간|  
|**0x2**|초|  
|**0x4**|분|  
|**0x8**|시간|  
  
`[ @freq_subday_interval = ] freq_subday_interval`각 작업 실행 사이에 발생 하는 *freq_subday_type* 기간 수입니다. *freq_subday_interval* 은 **int**이며 기본값은 **0**입니다. 참고: 간격은 10 초 보다 길어야 합니다. *freq_subday_type* 가 **1**과 같은 경우 *freq_subday_interval* 은 무시 됩니다.  
  
`[ @freq_relative_interval = ] freq_relative_interval`*Freq_interval* 32 (매월 상대적) 인 경우 매월 *freq_interval* 작업의 발생입니다. *freq_relative_interval* 은 **int**이며 기본값은 **0**이 고 다음 값 중 하나일 수 있습니다. *freq_type* 32와 같지 않은 경우에는 *freq_relative_interval* 무시 됩니다.  
  
|값|설명(단위)|  
|-----------|--------------------------|  
|**1**|첫째|  
|**2**|Second|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
`[ @freq_recurrence_factor = ] freq_recurrence_factor`예약 된 작업 실행 사이에 발생 하는 주 또는 월 수입니다. *freq_recurrence_factor* 는 *freq_type* 이 **8**, **16**또는 **32**인 경우에만 사용 됩니다. *freq_recurrence_factor* 은 **int**이며 기본값은 **0**입니다.  
  
`[ @active_start_date = ] active_start_date`작업 실행을 시작할 수 있는 날짜입니다. *active_start_date* 은 **int**이며 기본값은 오늘 날짜를 나타내는 NULL입니다. 날짜 형식은 YYYYMMDD입니다. *ACTIVE_START_DATE* NULL이 아닌 경우 날짜는 19900101 보다 크거나 같아야 합니다.  
  
 일정을 만든 다음 시작 날짜를 검토하여 날짜가 제대로 되어 있는지 확인하십시오. 자세한 내용은 [작업에 대 한 일정 만들기 및 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)의 "시작 날짜 예약" 섹션을 참조 하세요.  
  
 주별 또는 월별 일정의 경우 에이전트는 active_start_date가 과거 날짜인 경우 이를 무시하고 대신 현재 날짜를 사용합니다. sp_add_schedule을 사용하여 SQL 에이전트 일정을 만드는 경우 작업 실행이 시작되는 날짜인 active_start_date 매개 변수를 지정할 수 있습니다. 일정 유형이 주별이거나 월별이고 active_start_date 매개 변수가 과거 날짜로 설정되는 경우 active_start_date 매개 변수는 무시되고 현재 날짜가 active_start_date로 사용됩니다.  
  
`[ @active_end_date = ] active_end_date`작업 실행을 중지할 수 있는 날짜입니다. *active_end_date* 는 **int**이며 기본값은 9999 년 12 월 31 일을 나타내는 **99991231**입니다. 날짜 형식은 YYYYMMDD입니다.  
  
`[ @active_start_time = ] active_start_time`*Active_start_date* 와 *active_end_date* 사이의 모든 날짜에서 작업 실행을 시작할 시간입니다. *active_start_time* 는 **int**이며 기본값은 **000000**이며 오전 12:00:00을 나타냅니다. 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
`[ @active_end_time = ] active_end_time`*Active_start_date* 와 *active_end_date* 사이의 모든 날짜에 대 한 시간으로, 작업의 실행을 종료 합니다. *active_end_time* 는 **int**이며 기본값은 **235959**입니다 .이는 11:59:59 P.M.를 나타냅니다. 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
`[ @owner_login_name = ] 'owner_login_name'`일정을 소유 하는 서버 보안 주체의 이름입니다. *owner_login_name* 는 **sysname**이며 기본값은 작성자가 일정을 소유 하 고 있음을 나타내는 NULL입니다.  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT`일정의 고유 식별자입니다. *schedule_uid* 은 **uniqueidentifier**형식의 변수입니다.  
  
`[ @schedule_id = ] _schedule_idOUTPUT`일정의 식별자입니다. *schedule_id* 은 **int**형식의 변수입니다.  
  
`[ @originating_server = ] server_name` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 작업 구조를 만들고 관리할 수 있는 바람직한 방법을 제공하는데 이는 그래픽을 사용하여 쉽게 작업을 관리할 수 있는 방법입니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-schedule"></a>A. 일정 만들기  
 다음 예에서는 `RunOnce`라는 일정을 만듭니다. 일정은 일정이 생성된 날짜의 `23:30`에 한 번 실행됩니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_schedule  
    @schedule_name = N'RunOnce',  
    @freq_type = 1,  
    @active_start_time = 233000 ;  
  
GO  
```  
  
### <a name="b-creating-a-schedule-attaching-the-schedule-to-multiple-jobs"></a>B. 일정 만들기, 여러 작업에 일정 연결  
 다음 예에서는 `NightlyJobs`라는 일정을 만듭니다. 서버 시간이 `01:00`일 때 이 일정을 사용하는 작업이 매일 실행됩니다. 이 예에서는 `BackupDatabase` 작업과 `RunReports` 작업에 일정을 연결합니다.  
  
> [!NOTE]  
>  이 예에서는 `BackupDatabase` 작업 및 `RunReports` 작업이 이미 있다고 가정합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [일정을 만들고 작업에 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [작업 예약](../../ssms/agent/schedule-a-job.md)   
 [일정 만들기](../../ssms/agent/create-a-schedule.md)   
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_add_jobschedule &#40;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [Transact-sql&#41;sp_update_schedule &#40;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_delete_schedule &#40;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_help_schedule &#40;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
