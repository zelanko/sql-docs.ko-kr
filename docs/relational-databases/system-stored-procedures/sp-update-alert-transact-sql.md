---
title: sp_update_alert (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_alert_TSQL
- sp_update_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_alert
ms.assetid: 4bbaeaab-8aca-4c9e-abc1-82ce73090bd3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2856f89264994b9f1812653450d94e2cb2e2b0c2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "69890842"
---
# <a name="sp_update_alert-transact-sql"></a>sp_update_alert(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 경고의 설정을 업데이트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_update_alert   
     [ @name =] 'name'   
     [ , [ @new_name =] 'new_name']   
     [ , [ @enabled =] enabled]   
     [ , [ @message_id =] message_id]   
     [ , [ @severity =] severity]   
     [ , [ @delay_between_responses =] delay_between_responses]   
     [ , [ @notification_message =] 'notification_message']   
     [ , [ @include_event_description_in =] include_event_description_in]   
     [ , [ @database_name =] 'database']   
     [ , [ @event_description_keyword =] 'event_description_keyword']   
     [ , [ @job_id =] job_id | [@job_name =] 'job_name']   
     [ , [ @occurrence_count = ] occurrence_count]   
     [ , [ @count_reset_date =] count_reset_date]   
     [ , [ @count_reset_time =] count_reset_time]   
     [ , [ @last_occurrence_date =] last_occurrence_date]   
     [ , [ @last_occurrence_time =] last_occurrence_time]   
     [ , [ @last_response_date =] last_response_date]   
     [ , [ @last_response_time =] last_response _time]  
     [ , [ @raise_snmp_trap =] raise_snmp_trap]  
     [ , [ @performance_condition =] 'performance_condition' ]   
     [ , [ @category_name =] 'category']  
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @name = ] 'name'`업데이트할 경고의 이름입니다. *name* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @new_name = ] 'new_name'`경고의 새 이름입니다. 이름은 고유해야 합니다. *new_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @enabled = ] enabled`경고의 사용 여부 (**1**) 또는 사용 안 함 (**0**)을 지정 합니다. *enabled* 는 **tinyint**이며 기본값은 NULL입니다. 경고는 반드시 발생하도록 설정해야 합니다.  
  
`[ @message_id = ] message_id`경고 정의에 대 한 새 메시지 또는 오류 번호입니다. 일반적으로 *message_id* 는 **sysmessages** 테이블의 오류 번호에 해당 합니다. *message_id* 은 **int**이며 기본값은 NULL입니다. 경고에 대 한 심각도 수준 설정이 **0**인 경우에만 메시지 ID를 사용할 수 있습니다.  
  
`[ @severity = ] severity`경고 정의에 대 한 새 심각도 수준 ( **1** 에서 **25**까지)입니다. 지정 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 된 심각도를 사용 하 여 Windows 응용 프로그램 로그에 전송 된 모든 메시지는 경고를 활성화 합니다. *심각도* 는 **int**이며 기본값은 NULL입니다. 심각도 수준은 경고에 대 한 메시지 ID 설정이 **0**인 경우에만 사용할 수 있습니다.  
  
`[ @delay_between_responses = ] delay_between_responses`경고에 대 한 응답 간의 새로운 대기 기간 (초)입니다. *delay_between_responses* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @notification_message = ] 'notification_message'`전자 메일, **net send**또는 호출기 알림의 일부로 운영자에 게 전달 되는 추가 메시지의 수정 된 텍스트입니다. *notification_message* 은 **nvarchar (512)** 이며 기본값은 NULL입니다.  
  
`[ @include_event_description_in = ] include_event_description_in`Windows 응용 프로그램 로그의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류에 대 한 설명을 알림 메시지에 포함시킬지 여부를 지정 합니다. *include_event_description_in* 은 **tinyint**이며 기본값은 NULL이 고 다음 값 중 하나 이상이 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|None|  
|**1**|전자 메일|  
|**2**|호출기|  
|**4**|**net send**|  
|**7**|모두|  
  
`[ @database_name = ] 'database'`경고가 발생 하기 위해 오류가 발생 해야 하는 데이터베이스의 이름입니다. *데이터베이스* 는 **sysname입니다.** 이름을 대괄호([ ])로 묶는 것은 허용되지 않습니다. 기본값은 NULL입니다.  
  
`[ @event_description_keyword = ] 'event_description_keyword'`오류 메시지 로그에서 오류에 대 한 설명에 있어야 하는 문자 시퀀스입니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 식 패턴 일치 문자를 사용할 수 있습니다. *event_description_keyword* 은 **nvarchar (100)** 이며 기본값은 NULL입니다. 이 매개 변수는 개체 이름 (예: **% customer_table%**)을 필터링 하는 데 유용 합니다.  
  
`[ @job_id = ] job_id`작업 id입니다. *job_id* 은 **uniqueidentifier**이며 기본값은 NULL입니다. *Job_id* 지정 된 경우 *job_name* 생략 해야 합니다.  
  
`[ @job_name = ] 'job_name'`이 경고에 대 한 응답으로 실행 되는 작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다. *Job_name* 지정 된 경우 *job_id* 생략 해야 합니다.  
  
`[ @occurrence_count = ] occurrence_count`경고가 발생 한 횟수를 다시 설정 합니다. *occurrence_count* 은 **int**이며 기본값은 NULL이 고 **0**으로만 설정할 수 있습니다.  
  
`[ @count_reset_date = ] count_reset_date`발생 한 횟수가 마지막으로 다시 설정 된 날짜를 다시 설정 합니다. *count_reset_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @count_reset_time = ] count_reset_time`발생 한 횟수가 마지막으로 다시 설정 된 시간을 다시 설정 합니다. *count_reset_time* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @last_occurrence_date = ] last_occurrence_date`경고가 마지막으로 발생 한 날짜를 다시 설정 합니다. *last_occurrence_date* 은 **int**이며 기본값은 NULL이 고 **0**으로만 설정할 수 있습니다.  
  
`[ @last_occurrence_time = ] last_occurrence_time`경고가 마지막으로 발생 한 시간을 다시 설정 합니다. *last_occurrence_time* 은 **int**이며 기본값은 NULL이 고 **0**으로만 설정할 수 있습니다.  
  
`[ @last_response_date = ] last_response_date`SQLServerAgent 서비스가 마지막으로 경고에 응답 한 날짜를 다시 설정 합니다. *last_response_date* 은 **int**이며 기본값은 NULL이 고 **0**으로만 설정할 수 있습니다.  
  
`[ @last_response_time = ] last_response_time`SQLServerAgent 서비스가 마지막으로 경고에 응답 한 시간을 다시 설정 합니다. *last_response_time* 은 **int**이며 기본값은 NULL이 고 **0**으로만 설정할 수 있습니다.  
  
`[ @raise_snmp_trap = ] raise_snmp_trap`쓰이는.  
  
`[ @performance_condition = ] 'performance_condition'`**'**_Itemcomparatorvalue_**'** 형식으로 표시 된 값입니다. *performance_condition* 은 **nvarchar (512)** 이며 기본값은 NULL이 고이 요소로 구성 됩니다.  
  
|형식 요소|Description|  
|--------------------|-----------------|  
|*항목*|성능 개체, 성능 카운터 또는 카운터의 명명된 인스턴스|  
|*비교자*|다음 연산자 중 하나입니다 **>**. **<**,,**=**|  
|*값*|카운터의 숫자 값|  
  
`[ @category_name = ] 'category'`경고 범주의 이름입니다. *category* 는 **sysname** 이며 기본값은 NULL입니다.  
  
`[ @wmi_namespace = ] 'wmi_namespace'`이벤트를 쿼리 하는 WMI 네임 스페이스입니다. *wmi_namespace* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @wmi_query = ] 'wmi_query'`경고에 대 한 WMI 이벤트를 지정 하는 쿼리입니다. *wmi_query* 은 **nvarchar (512)** 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 Windows 응용 프로그램 로그에 기록 된 sysmessages만 경고를 발생 시킬 수 있습니다. **sysmessages** [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
 **sp_update_alert** 는 매개 변수 값이 제공 되는 경고 설정만 변경 합니다. 매개 변수가 생략되면 현재 설정이 보존됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행 하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버 여야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Test Alert`의 enabled 설정을 `0`으로 변경합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_alert  
    @name = N'Test Alert',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_alert &#40;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [Transact-sql&#41;sp_help_alert &#40;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
