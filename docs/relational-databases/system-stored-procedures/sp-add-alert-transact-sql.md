---
title: sp_add_alert (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_alert
- sp_add_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_alert
ms.assetid: d9b41853-e22d-4813-a79f-57efb4511f09
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 750d299b951b403ed6fe51baa43b047505860c3f
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493805"
---
# <a name="spaddalert-transact-sql"></a>sp_add_alert(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  경고를 작성합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_alert [ @name = ] 'name'   
     [ , [ @message_id = ] message_id ]   
     [ , [ @severity = ] severity ]   
     [ , [ @enabled = ] enabled ]  
     [ , [ @delay_between_responses = ] delay_between_responses ]   
     [ , [ @notification_message = ] 'notification_message' ]   
     [ , [ @include_event_description_in = ] include_event_description_in ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @event_description_keyword = ] 'event_description_keyword_pattern' ]   
     [ , { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ]   
     [ , [ @raise_snmp_trap = ] raise_snmp_trap ]   
     [ , [ @performance_condition = ] 'performance_condition' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @name = ] 'name'` 경고의 이름입니다. 이름은 경고에 대한 응답으로 메시지가 전달된 전자 메일 또는 호출기에 표시됩니다. 고유 해야 하며 퍼센트 (**%**) 문자입니다. *이름을* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @message_id = ] message_id` 경고를 정의 하는 메시지 오류 번호입니다. (일반적으로 오류 번호에 해당 합니다 **sysmessages** 테이블입니다.) *message_id* 됩니다 **int**, 기본값은 **0**합니다. 하는 경우 *심각도* 경고를 정의 하는 데 사용 됩니다 *message_id* 여야 **0** 또는 NULL입니다.  
  
> [!NOTE]  
>  만 **sysmessages** Microsoft Windows 응용 프로그램 로그에 기록 하는 오류를 보내도록 경고를 발생할 수 있습니다.  
  
`[ @severity = ] severity` 심각도 수준 (에서 **1** 를 통해 **25**) 경고를 정의 하는 합니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 저장 된 메시지를 **sysmessages** 테이블에 전송 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 표시 된 심각도로 Windows 응용 프로그램 로그에 경고를 전송 하면 합니다. *심각도* 됩니다 **int**, 기본값은 0입니다. 하는 경우 *message_id* 경고를 정의 하는 데 사용 됩니다 *심각도* 여야 **0**합니다.  
  
`[ @enabled = ] enabled` 경고의 현재 상태를 나타냅니다. *사용 하도록 설정* 됩니다 **tinyint**, 기본값은 1 (사용). 하는 경우 **0**, 경고가 사용 되지 않으며 발생 하지 않습니다.  
  
`[ @delay_between_responses = ] delay_between_responses` 대기 시간, 경고에 대 한 응답 간격 (초)입니다. *delay_between_responses*됩니다 **int**, 기본값은 **0**, 있습니다 (각 경고의 발생 응답을 생성 하는 데 사용) 하는 응답에 걸리는 대기 시간이 없음 됨을 의미 합니다. 응답은 다음 두 가지 형식 중 한 가지 또는 두 가지 모두를 사용할 수 있습니다.  
  
-   전자 메일 또는 호출기를 통해 전달된 한 개 이상의 알림  
  
-   실행할 작업  
  
 이 값을 설정함으로써 단기간에 경고가 반복적으로 발생하는 경우, 원하지 않는 전자 메일 메시지가 전달되지 않도록 하는 등의 작업을 할 수 있습니다.  
  
`[ @notification_message = ] 'notification_message'` 전자 메일의 일부로 운영자에 게 전송 하는 선택적 추가 메시지는 **net send**, 또는 호출기 알림의 합니다. *notification_message* 됩니다 **nvarchar(512)**, 기본값은 NULL입니다. 지정 *notification_message* 교정 프로시저와 같은 특별 한 메모를 추가 하는 데 유용 합니다.  
  
`[ @include_event_description_in = ] include_event_description_in` 가 있는지 여부를 대 한 설명을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 알림 메시지의 일부로 포함 해야 합니다. *include_event_description_in*됩니다 **tinyint**, 기본값은 **5** (전자 메일 및 **net send**), 하나를 가질 수와 함께 다음이 값 중 더는 **또는** 논리 연산자입니다.  
  
> [!IMPORTANT]
>  **이후 버전에서는** 에이전트에서 호출기 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net send [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]옵션이 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 말고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|없음|  
|**1**|전자 메일|  
|**2**|호출기|  
|**4**|**Net Send**|  
  
`[ @database_name = ] 'database'` 데이터베이스 오류는 경고가 발생 해야 합니다. 하는 경우 *데이터베이스*제공 되지 않으면 오류가 발생 하는 것에 관계 없이 경고가 발생 합니다. *데이터베이스* 됩니다 **sysname**합니다. 이름을 대괄호([ ])로 묶는 것은 허용되지 않습니다. 기본값은 NULL입니다.  
  
`[ @event_description_keyword = ] 'event_description_keyword_pattern'` 문자 시퀀스에 대 한 설명을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 같아야 합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 식 패턴 일치 문자를 사용할 수 있습니다. *event_description_keyword_pattern* 됩니다 **nvarchar(100)**, 기본값은 NULL입니다. 이 매개 변수는 개체 이름을 필터링 하는 데 (예를 들어 **%customer_table%**).  
  
`[ @job_id = ] job_id` 이 경고에 대 한 응답에서 실행 작업의 작업 id. *job_id* 됩니다 **uniqueidentifier**, 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'` 이 경고에 대 한 응답으로 실행할 작업의 이름입니다. *job_name*됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
`[ @raise_snmp_trap = ] raise_snmp_trap` 구현 되지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 7.0입니다. *raise_snmp_trap* 됩니다 **tinyint**, 기본값은 0입니다.  
  
`[ @performance_condition = ] 'performance_condition'` 형식으로 표시 되는 값은 '*itemcomparatorvalue*'. *performance_condition* 은 **nvarchar(512)** 이며 기본값은 NULL 이며 다음이 요소로 구성 됩니다.  
  
|형식 요소|Description|  
|--------------------|-----------------|  
|*항목*|성능 개체, 성능 카운터 또는 카운터의 명명된 인스턴스|  
|*비교 연산자*|이러한 연산자 중 하나: >, <, 또는 =|  
|*Value*|카운터의 숫자 값|  
  
`[ @category_name = ] 'category'` 경고 범주의 이름입니다. *범주* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @wmi_namespace = ] 'wmi_namespace'` 이벤트에 대 한 쿼리는 WMI 네임 스페이스입니다. *wmi_namespace* 됩니다 **sysname**, 기본값은 NULL입니다. 로컬 서버의 네임스페이스만 지원됩니다.  
  
`[ @wmi_query = ] 'wmi_query'` WMI 이벤트 경고를 지정 하는 쿼리. *wmi_query* 됩니다 **nvarchar(512)**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 **sp_add_alert** 에서 실행 해야 합니다 **msdb** 데이터베이스입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 응용 프로그램에 의해 생성된 오류 또는 메시지가 Windows 응용 프로그램 로그로 전달되어 경고가 발생하는 상황입니다.  
  
-   심각도 19 이상인 **sys.messages** 오류  
  
-   WITH LOG 구문과 함께 호출된 모든 RAISERROR 문  
  
-   모든 **sys.messages** 오류 수정 되거나 사용 하 여 만든 **sp_altermessage**  
  
-   사용 하 여 로깅된 모든 이벤트 **xp_logevent**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 전체 경고 시스템을 간편하게 그래픽 방식으로 관리할 수 있도록 해 줄 뿐만 아니라 경고 인프라를 구성하는 데 있어서도 권장되는 방법입니다.  
  
 경고가 제대로 작동하지 않는 경우에는 다음 사항을 확인하세요.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 실행 중인지 여부  
  
-   Windows 응용 프로그램 로그에 표시된 이벤트  
  
-   경고의 설정 여부  
  
-   master 데이터베이스에서 **xp_logevent** 로 생성된 이벤트가 발생합니다. 따라서 경고에 대한 **xp_logevent** 이 **@database_name** 또는 NULL이 아닌 경우 **xp_logevent** 는 경고를 트리거하지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버만 **sp_add_alert**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 시작할 때 `Back up the AdventureWorks2012 Database` 작업을 실행하는 경고(Test Alert)를 추가합니다.  
  
> [!NOTE]  
>  이 예에서는 메시지 55001 및 `Back up the AdventureWorks2012 Database` 작업이 이미 있다고 가정합니다. 이 예는 설명을 목적으로 사용한 것입니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_alert  
    @name = N'Test Alert',  
    @message_id = 55001,   
   @severity = 0,   
   @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
   @job_name = N'Back up the AdventureWorks2012 Database' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_add_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_altermessage &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_delete_alert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_update_alert &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
