---
description: sp_update_schedule(Transact-SQL)
title: sp_update_schedule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_schedule
- sp_update_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_schedule
ms.assetid: 97b3119b-e43e-447a-bbfb-0b5499e2fefe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a8616c3b10257440210f80de1ef45832d3b88e6f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480917"
---
# <a name="sp_update_schedule-transact-sql"></a>sp_update_schedule(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 일정에 대한 설정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_update_schedule   
    {   [ @schedule_id = ] schedule_id   
      | [ @name = ] 'schedule_name' }  
    [ , [ @new_name = ] new_name ]  
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
    [ , [ @automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>인수  
`[ @schedule_id = ] schedule_id` 수정할 일정의 식별자입니다. *schedule_id* 는 **int**이며 기본값은 없습니다. *Schedule_id* 또는 *schedule_name* 를 지정 해야 합니다.  
  
`[ @name = ] 'schedule_name'` 수정할 일정의 이름입니다. *schedule_name*는 **sysname**이며 기본값은 없습니다. *Schedule_id* 또는 *schedule_name* 를 지정 해야 합니다.  
  
`[ @new_name = ] new_name` 일정의 새 이름입니다. *new_name* 는 **sysname**이며 기본값은 NULL입니다. *NEW_NAME* NULL 인 경우 일정의 이름은 변경 되지 않습니다.  
  
`[ @enabled = ] enabled` 일정의 현재 상태를 나타냅니다. *enabled*는 **tinyint**이며 기본값은 **1** (사용)입니다. **0**인 경우 일정을 사용할 수 없습니다. 일정을 사용할 수 없는 경우 이 일정에 따라 어떠한 작업도 실행되지 않습니다.  
  
`[ @freq_type = ] freq_type` 작업이 실행 될 시기를 나타내는 값입니다. *freq_type*은 **int**이며 기본값은 **0**이 고 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**4**|매일|  
|**8**|매주|  
|**16**|매월|  
|**32**|매월, *freq 간격* 기준|  
|**64**|SQLServerAgent 서비스를 시작할 때 실행|  
|**128**|컴퓨터가 유휴 상태일 때 실행|  
  
`[ @freq_interval = ] freq_interval` 작업이 실행 되는 요일입니다. *freq_interval* 은 **int**이며 기본값은 **0**이 고 *freq_type*의 값에 따라 달라 집니다.  
  
|*Freq_type* 의 값|*Freq_interval* 에 대 한 영향|  
|---------------------------|--------------------------------|  
|**1** (한 번)|*freq_interval* 사용 되지 않습니다.|  
|**4** (매일)|*Freq_interval* 일 마다.|  
|**8** (매주)|*freq_interval* 는 **or** 논리 연산자와 결합 된 다음 중 하나 이상입니다.<br /><br /> **1** = 일요일<br /><br /> **2** = 월요일<br /><br /> **4** = 화요일<br /><br /> **8** = 수요일<br /><br /> **16** = 목요일<br /><br /> **32** = 금요일<br /><br /> **64** = 토요일|  
|**16** (매월)|월의 *freq_interval* 날짜|  
|**32** (매월 상대적)|*freq_interval* 은 다음 중 하나입니다.<br /><br /> **1** = 일요일<br /><br /> **2** = 월요일<br /><br /> **3** = 화요일<br /><br /> **4** = 수요일<br /><br /> **5** = 목요일<br /><br /> **6** = 금요일<br /><br /> **7** = 토요일<br /><br /> **8** = 일<br /><br /> **9** = 평일<br /><br /> **10** = 주말|  
|**64** (SQLServerAgent 서비스가 시작 되는 경우)|*freq_interval* 사용 되지 않습니다.|  
|**128**|*freq_interval* 사용 되지 않습니다.|  
  
`[ @freq_subday_type = ] freq_subday_type`*Freq_subday_interval * ** 의 단위를 지정 합니다. *freq_subday_type*은 **int**이며 기본값은 **0**이 고 다음 값 중 하나일 수 있습니다.  
  
|값|설명(단위)|  
|-----------|--------------------------|  
|**0x1**|지정된 시간|  
|**0x2**|초|  
|**0x4**|분|  
|**0x8**|시간|  
  
`[ @freq_subday_interval = ] freq_subday_interval` 각 작업 실행 사이에 발생 하는 *freq_subday_type* 기간 수입니다. *freq_subday_interval*은 **int**이며 기본값은 **0**입니다.  
  
`[ @freq_relative_interval = ] freq_relative_interval`*Freq_interval* **32** (매월 상대적) 인 경우 매월 *freq_interval* 작업의 발생입니다. *freq_relative_interval*은 **int**이며 기본값은 **0**이 고 다음 값 중 하나일 수 있습니다.  
  
|값|설명(단위)|  
|-----------|--------------------------|  
|**1**|처음|  
|**2**|초|  
|**4**|세 번째|  
|**8**|넷째|  
|**16**|마지막|  
  
`[ @freq_recurrence_factor = ] freq_recurrence_factor` 예약 된 작업 실행 사이에 발생 하는 주 또는 월 수입니다. *freq_recurrence_factor* 는 *freq_type* 이 **8**, **16**또는 **32**인 경우에만 사용 됩니다. *freq_recurrence_factor*은 **int**이며 기본값은 **0**입니다.  
  
`[ @active_start_date = ] active_start_date` 작업 실행을 시작할 수 있는 날짜입니다. *active_start_date*은 **int**이며 기본값은 오늘 날짜를 나타내는 NULL입니다. 날짜 형식은 YYYYMMDD입니다. *ACTIVE_START_DATE* NULL이 아닌 경우 날짜는 19900101 보다 크거나 같아야 합니다.  
  
 일정을 만든 다음 시작 날짜를 검토하여 날짜가 제대로 되어 있는지 확인하십시오. 자세한 내용은 [작업에 대 한 일정 만들기 및 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)의 "시작 날짜 예약" 섹션을 참조 하세요.  
  
`[ @active_end_date = ] active_end_date` 작업 실행을 중지할 수 있는 날짜입니다. *active_end_date*는 **int**이며 기본값은 9999 년 12 월 31 일을 나타내는 **99991231**입니다. 날짜 형식은 YYYYMMDD입니다.  
  
`[ @active_start_time = ] active_start_time`*Active_start_date* 와 *active_end_date* 사이의 모든 날짜에서 작업 실행을 시작할 시간입니다. *active_start_time*는 **int**이며 기본값은 000000 이며 오전 12:00:00을 나타냅니다. 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
`[ @active_end_time = ] active_end_time`*Active_start_date* 와 *active_end_date* 사이의 모든 날짜에 대 한 시간으로, 작업의 실행을 종료 합니다. *active_end_time*는 **int**이며 기본값은 **235959**입니다 .이는 11:59:59 P.M.를 나타냅니다. 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
`[ @owner_login_name = ] 'owner_login_name']` 일정을 소유 하는 서버 보안 주체의 이름입니다. *owner_login_name* 는 **sysname**이며 기본값은 작성자가 일정을 소유 하 고 있음을 나타내는 NULL입니다.  
  
`[ @automatic_post = ] automatic_post` 쓰이는.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 일정을 즉시 사용하는 모든 작업은 새 설정을 사용합니다. 그러나 일정을 변경해도 현재 실행 중인 작업은 중지되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **Sysadmin** 의 멤버만 다른 사용자가 소유한 일정을 수정할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `NightlyJobs` 일정의 활성화된 상태를 `0`으로 변경하고 소유자를 `terrid`로 설정합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_schedule  
    @name = 'NightlyJobs',  
    @enabled = 0,  
    @owner_login_name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [일정을 만들고 작업에 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [작업 예약](../../ssms/agent/schedule-a-job.md)   
 [일정 만들기](../../ssms/agent/create-a-schedule.md)   
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트 ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_add_schedule &#40;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_add_jobschedule &#40;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [Transact-sql&#41;sp_delete_schedule &#40;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_help_schedule &#40;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
