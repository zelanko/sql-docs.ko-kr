---
title: sp_update_alert (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 24cd1864fc31524dcd661cd9eb108d8cb4fa1b77
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846731"
---
# <a name="spupdatealert-transact-sql"></a>sp_update_alert(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 경고의 설정을 업데이트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@name =**] **'***name***'**  
 업데이트할 경고의 이름입니다. *이름을* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@new_name =**] **'***new_name***'**  
 경고의 새 이름입니다. 이름은 고유해야 합니다. *new_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [ **@enabled =**] *enabled*  
 경고 사용 되는지 여부를 지정 합니다 (**1**) 또는 사용 안 함 (**0**). *사용 하도록 설정* 됩니다 **tinyint**, 기본값은 NULL입니다. 경고는 반드시 발생하도록 설정해야 합니다.  
  
 [ **@message_id =**] *message_id*  
 경고 정의에 대한 새 메시지 또는 오류 번호입니다. 일반적으로 *message_id* 의 오류 번호에 해당 하는 **sysmessages** 테이블입니다. *message_id* 됩니다 **int**, 기본값은 NULL입니다. 메시지 ID는 경고의 심각도 수준 설정을 인 경우에 사용할 수 있습니다 **0**합니다.  
  
 [ **@severity =**] *severity*  
 새 심각도 (에서 **1** 를 통해 **25**) 경고 정의 합니다. 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정한 심각도로 Windows 응용 프로그램 로그에 전송 된 메시지는 경고를 활성화 합니다. *심각도* 됩니다 **int**, 기본값은 NULL입니다. 심각도 경고에 대 한 메시지 ID 설정이 하는 경우에 사용할 수 있습니다 **0**합니다.  
  
 [ **@delay_between_responses =**] *delay_between_responses*  
 경고에 대한 응답 간의 새로운 대기 기간(초)입니다. *delay_between_responses* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [ **@notification_message =**] **'***notification_message***'**  
 전자 메일의 일부로 운영자에 게 전송 하는 추가 메시지의 수정 된 텍스트 **net send**, 또는 호출기 알림의 합니다. *notification_message* 됩니다 **nvarchar(512)**, 기본값은 NULL입니다.  
  
 [ **@include_event_description_in =**] *include_event_description_in*  
 Windows 응용 프로그램 로그에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류에 대한 설명을 알림 메시지에 포함시킬지 여부를 지정합니다. *include_event_description_in* 은 **tinyint**, 기본값은 NULL 이며 다음이 값 중 하나 이상의 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|없음|  
|**1**|전자 메일|  
|**2**|호출기|  
|**4**|**Net Send**|  
|**7**|All|  
  
 [ **@database_name =**] **'***database***'**  
 해당 오류가 발생해야 경고가 발생되는 데이터베이스의 이름입니다. *데이터베이스* 는 **sysname 합니다.** 이름을 대괄호([ ])로 묶는 것은 허용되지 않습니다. 기본값은 NULL입니다.  
  
 [ **@event_description_keyword =**] **'***event_description_keyword***'**  
 오류 메시지 로그에서 오류에 대한 설명에 반드시 있어야 하는 문자 시퀀스입니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 식 패턴 일치 문자를 사용할 수 있습니다. *event_description_keyword* 됩니다 **nvarchar(100)**, 기본값은 NULL입니다. 이 매개 변수는 개체 이름을 필터링 하는 데 (예를 들어 **%customer_table%**).  
  
 [ **@job_id =**] *job_id*  
 작업 ID입니다. *job_id* 됩니다 **uniqueidentifier**, 기본값은 NULL입니다. 하는 경우 *job_id* 를 지정 하면 *job_name* 생략 해야 합니다.  
  
 [ **@job_name =**] **'***job_name***'**  
 해당 경고에 대한 응답으로 실행되는 작업의 이름입니다. *job_name* 됩니다 **sysname**, 기본값은 NULL입니다. 하는 경우 *job_name* 를 지정 하면 *job_id* 생략 해야 합니다.  
  
 [  **@occurrence_count =** ] *occurrence_count*  
 경고가 발생한 횟수를 다시 설정합니다. *occurrence_count* 됩니다 **int**, 기본값은 NULL 사용 하 여에 설정할 수 있습니다 **0**합니다.  
  
 [ **@count_reset_date =**] *count_reset_date*  
 발생한 횟수가 마지막으로 다시 설정된 날짜를 다시 설정합니다. *count_reset_date* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [ **@count_reset_time =**] *count_reset_time*  
 발생한 횟수가 마지막으로 다시 설정된 시간을 다시 설정합니다. *count_reset_time* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [ **@last_occurrence_date =**] *last_occurrence_date*  
 경고가 마지막으로 발생한 날짜를 다시 설정합니다. *last_occurrence_date* 됩니다 **int**, 기본값은 NULL 사용 하 여에 설정할 수 있습니다 **0**합니다.  
  
 [ **@last_occurrence_time =**] *last_occurrence_time*  
 경고가 마지막으로 발생한 시간을 다시 설정합니다. *last_occurrence_time* 됩니다 **int**, 기본값은 NULL 사용 하 여에 설정할 수 있습니다 **0**합니다.  
  
 [ **@last_response_date =**] *last_response_date*  
 SQLServerAgent 서비스가 경고에 마지막으로 응답한 날짜를 다시 설정합니다. *last_response_date* 됩니다 **int**, 기본값은 NULL 사용 하 여에 설정할 수 있습니다 **0**합니다.  
  
 [ **@last_response_time =**] *last_response_time*  
 SQLServerAgent 서비스가 경고에 마지막으로 응답한 시간을 다시 설정합니다. *last_response_time* 됩니다 **int**, 기본값은 NULL 사용 하 여에 설정할 수 있습니다 **0**합니다.  
  
 [ **@raise_snmp_trap =**] *raise_snmp_trap*  
 예약되어 있습니다.  
  
 [ **@performance_condition =**] **'***performance_condition***'**  
 형식으로 표시 되는 값 **'***itemcomparatorvalue***'** 합니다. *performance_condition* 는 **nvarchar(512)**, 기본값은 NULL 이며 다음이 요소로 구성 됩니다.  
  
|형식 요소|Description|  
|--------------------|-----------------|  
|*항목*|성능 개체, 성능 카운터 또는 카운터의 명명된 인스턴스|  
|*비교 연산자*|이러한 연산자 중 하나: **>** 하십시오 **<**, **=**|  
|*Value*|카운터의 숫자 값|  
  
 [ **@category_name =**] **'***category***'**  
 경고 범주의 이름입니다. *범주* 됩니다 **sysname** 이며 기본값은 NULL입니다.  
  
 [ **@wmi_namespace**= ] **'***wmi_namespace***'**  
 이벤트를 쿼리하는 WMI 네임스페이스입니다. *wmi_namespace* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [ **@wmi_query**= ] **'***wmi_query***'**  
 경고에 대한 WMI 이벤트를 지정하는 쿼리입니다. *wmi_query* 됩니다 **nvarchar(512)**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 만 **sysmessages** 에 기록 된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 응용 프로그램 로그에 경고를 발생 시킬 수 있습니다.  
  
 **sp_update_alert** 매개 변수 값이 제공 된 경고 설정만 변경 합니다. 매개 변수가 생략되면 현재 설정이 보존됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장된 프로시저를 실행 하려면 사용자의 구성원 이어야 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [sp_add_alert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_help_alert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
