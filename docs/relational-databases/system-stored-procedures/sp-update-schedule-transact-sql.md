---
title: sp_update_schedule (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_schedule
- sp_update_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_schedule
ms.assetid: 97b3119b-e43e-447a-bbfb-0b5499e2fefe
caps.latest.revision: 42
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed8a500af524796cf98a16f9da75aae003375c1a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262866"
---
# <a name="spupdateschedule-transact-sql"></a>sp_update_schedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 일정에 대한 설정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@schedule_id =** ] *schedule_id*  
 수정할 일정의 식별자입니다. *schedule_id* 은 **int**, 기본값은 없습니다. 어느 *schedule_id* 또는 *schedule_name* 지정 해야 합니다.  
  
 [ **@name =** ]  **'***schedule_name***'**  
 수정할 일정의 이름입니다. *schedule_name*은 **sysname**, 기본값은 없습니다. 어느 *schedule_id* 또는 *schedule_name* 지정 해야 합니다.  
  
 [ **@new_name**= ] *new_name*  
 일정의 새 이름입니다. *new_name* 은 **sysname**, 기본값은 NULL입니다. 때 *new_name* 가 NULL 이면 일정의 이름은 변경 되지 않습니다.  
  
 [  **@enabled =** ] *사용 하도록 설정*  
 일정의 현재 상태를 나타냅니다. *활성화*은 **tinyint**, 기본값은 **1** (사용). 경우 **0**, 일정을 사용할 수 없습니다. 일정을 사용할 수 없는 경우 이 일정에 따라 어떠한 작업도 실행되지 않습니다.  
  
 [ **@freq_type =** ] *freq_type*  
 작업이 실행될 시기를 나타내는 값입니다. *freq_type*은 **int**, 기본값은 **0**, 다음이 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**1**|한 번|  
|**4**|일별|  
|**8**|매주|  
|**16**|매월|  
|**32**|기준으로 월별 *등호 간격*|  
|**64**|SQLServerAgent 서비스를 시작할 때 실행|  
|**128**|컴퓨터가 유휴 상태일 때 실행|  
  
 [ **@freq_interval =** ] *freq_interval*  
 작업이 실행되는 날짜입니다. *freq_interval* 은 **int**, 기본값은 **0**의 값에 따라 달라 집니다 *freq_type*합니다.  
  
|값 *freq_type*|에 영향을 *freq_interval*|  
|---------------------------|--------------------------------|  
|**1** (한 번)|*freq_interval* 는 사용 되지 않습니다.|  
|**4** (매일)|모든 *freq_interval* 일 수 있습니다.|  
|**8** (매주)|*freq_interval* 은 다음 중 하나 이상을 (함께 **OR** 논리 연산자).<br /><br /> **1** = 일요일<br /><br /> **2** = 월요일<br /><br /> **4** = 화요일<br /><br /> **8** = 수요일<br /><br /> **16** = 목요일<br /><br /> **32** = 금요일<br /><br /> **64** = 토요일|  
|**16** (매월)|에 *freq_interval* 해당 월의 일 합니다.|  
|**32** (매월 상대적)|*freq_interval* 다음 중 하나입니다.<br /><br /> **1** = 일요일<br /><br /> **2** = 월요일<br /><br /> **3** = 화요일<br /><br /> **4** = 수요일<br /><br /> **5** = 목요일<br /><br /> **6** = 금요일<br /><br /> **7** = 토요일<br /><br /> **8** = 일<br /><br /> **9** = 평일<br /><br /> **10** = 주말|  
|**64** (SQLServerAgent 서비스가 시작할 때)|*freq_interval* 는 사용 되지 않습니다.|  
|**128**|*freq_interval* 는 사용 되지 않습니다.|  
  
 [ **@freq_subday_type =** ] *freq_subday_type*  
 단위를 지정 *freq_subday_interval * *입니다.* *freq_subday_type*은 **int**, 기본값은 **0**, 다음이 값 중 하나일 수 있습니다.  
  
|Value|설명(단위)|  
|-----------|--------------------------|  
|**0x1**|지정된 시간|  
|**0x2**|초|  
|**0x4**|분|  
|**0x8**|시간|  
  
 [ **@freq_subday_interval =** ] *freq_subday_interval*  
 수가 *freq_subday_type* 각 작업 실행 간에 발생 하는 기간. *freq_subday_interval*은 **int**, 기본값은 **0**합니다.  
  
 [ **@freq_relative_interval =** ] *freq_relative_interval*  
 작업의 발생 *freq_interval* 각 월에 경우 *freq_interval* 은 **32** (매월 상대)입니다. *freq_relative_interval*은 **int**, 기본값은 **0**, 다음이 값 중 하나일 수 있습니다.  
  
|Value|설명(단위)|  
|-----------|--------------------------|  
|**1**|첫째|  
|**2**|둘째|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
 [ **@freq_recurrence_factor =** ] *freq_recurrence_factor*  
 예약된 작업 실행 간에 발생하는 주 또는 월의 수입니다. *freq_recurrence_factor* 경우에 사용 *freq_type* 은 **8**, **16**, 또는 **32**합니다. *freq_recurrence_factor*은 **int**, 기본값은 **0**합니다.  
  
 [ **@active_start_date =** ]  *active_start_date*  
 작업 실행이 시작되는 날짜입니다. *active_start_date*은 **int**, 기본값은 NULL 이며 오늘 날짜를 나타내는입니다. 날짜 형식은 YYYYMMDD입니다. 경우 *active_start_date* NULL이 아니면 날짜 보다 크거나 19900101 이어야 합니다.  
  
 일정을 만든 다음 시작 날짜를 검토하여 날짜가 제대로 되어 있는지 확인하십시오. 자세한 내용은 "시작 날짜 예약" 섹션을 참조 [만들기 및 작업에 일정 연결](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)합니다.  
  
 [ **@active_end_date =** ] *active_end_date*  
 작업 실행이 중지되는 날짜입니다. *active_end_date*은 **int**, 기본값은 **99991231**를 나타내는 12 월 31 일에서 9999입니다. 날짜 형식은 YYYYMMDD입니다.  
  
 [ **@active_start_time =** ] *active_start_time*  
 시간 사이의 임의의 날짜에서 *active_start_date* 및 *active_end_date* 작업의 실행을 시작 합니다. *active_start_time*은 **int**, 오전 12시: 00을 나타내는 000000 기본값 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
 [ **@active_end_time =** ] *active_end_time*  
 시간 사이의 임의의 날짜에서 *active_start_date* 및 *active_end_date* 하는 작업의 실행을 종료 합니다. *active_end_time*은 **int**, 기본값은 **235959**, 오후 11시 59분: 59를 나타냄 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
 [ **@owner_login_name**= ] **'***owner_login_name***'**]  
 일정을 소유하는 서버 보안 주체의 이름입니다. *owner_login_name* 은 **sysname**, 기본값은 NULL, 만든이가 일정을 소유 나타냅니다.  
  
 [ **@automatic_post =**] *automatic_post*  
 예약되어 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 일정을 즉시 사용하는 모든 작업은 새 설정을 사용합니다. 그러나 일정을 변경해도 현재 실행 중인 작업은 중지되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
 구성원만 **sysadmin** 다른 사용자가 소유한 일정을 수정할 수 있습니다.  
  
## <a name="examples"></a>예  
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
  
## <a name="see-also"></a>관련 항목:  
 [만들기 및 작업에 일정 연결](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)   
 [작업 예약](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c)   
 [일정 만들기](http://msdn.microsoft.com/library/8c7ef3b3-c06d-4a27-802d-ed329dc86ef3)   
 [SQL Server 에이전트 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobschedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_delete_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
