---
title: sp_help_alert (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_alert
- sp_help_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_alert
ms.assetid: 850cef4e-6348-4439-8e79-fd1bca712091
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 08569c2313bfb7c9d992c510ef4c9c7548f51e64
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827757"
---
# <a name="sp_help_alert-transact-sql"></a>sp_help_alert(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버에 대해 정의된 경고에 관한 정보를 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_alert [ [ @alert_name = ] 'alert_name' ]   
     [ , [ @order_by = ] 'order_by' ]   
     [ , [ @alert_id = ] alert_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @legacy_format = ] legacy_format ]  
```  
  
## <a name="arguments"></a>인수  
`[ @alert_name = ] 'alert_name'`경고 이름입니다. *alert_name* 은 **nvarchar (128)** 입니다. *Alert_name* 지정 하지 않으면 모든 경고에 대 한 정보가 반환 됩니다.  
  
`[ @order_by = ] 'order_by'`결과를 생성 하는 데 사용할 정렬 순서입니다. *order_by*는 **sysname**이며 기본값은 N '*이름*'입니다.  
  
`[ @alert_id = ] alert_id`보고할 정보에 대 한 경고의 id입니다. *alert_id*은 **int**이며 기본값은 NULL입니다.  
  
`[ @category_name = ] 'category'`경고의 범주입니다. *category* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @legacy_format = ] legacy_format`레거시 결과 집합을 생성할지 여부입니다. *legacy_format* 은 **bit**이며 기본값은 **0**입니다. *Legacy_format* **1**인 경우 **sp_help_alert** **sp_help_alert** 에서 반환 된 결과 집합을 Microsoft SQL Server 2000에 반환 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 ** \@ Legacy_format** **0**인 경우 **sp_help_alert** 는 다음 결과 집합을 생성 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|시스템이 할당한 고유한 정수 ID입니다.|  
|**name**|**sysname**|경고 이름 (예: Demo: Full **msdb** log).|  
|**event_source**|**nvarchar (100)**|이벤트의 원본입니다. 버전 7.0의 경우 항상 **MSSQLServer** 입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|경고를 정의하는 메시지 오류 번호로서 일반적으로 **sysmessages** 테이블의 오류 번호에 해당 합니다. 심각도를 사용 하 여 경고를 정의 하는 경우 **message_id** 은 **0** 또는 NULL입니다.|  
|**severity**|**int**|경고를 정의 하는 심각도 수준 ( **9** 부터 **25**, **110**, **120**, **130**또는 **140**)입니다.|  
|**사용**|**tinyint**|경고가 현재 활성화 되어 있는지 (**1**) 또는 그렇지 않은지 (**0**)의 상태입니다. 사용할 수 없는 경고는 전달되지 않습니다.|  
|**delay_between_responses**|**int**|경고에 대한 응답 간의 대기 시간(초)입니다.|  
|**last_occurrence_date**|**int**|마지막으로 경고가 발생한 날짜입니다.|  
|**last_occurrence_time**|**int**|마지막으로 경고가 발생한 시간입니다.|  
|**last_response_date**|**int**|**SQLServerAgent** 서비스가 마지막으로 경고에 응답 한 날짜입니다.|  
|**last_response_time**|**int**|**SQLServerAgent** 서비스가 마지막으로 경고에 응답 한 시간입니다.|  
|**notification_message**|**nvarchar(512)**|전자 메일 또는 호출기 알림의 일부로서 운영자에게 선택적으로 전달되는 추가 메시지입니다.|  
|**include_event_description**|**tinyint**|Microsoft Windows 애플리케이션 로그의 SQL Server 오류에 대한 설명을 알림 메시지의 일부로 포함할지 여부입니다.|  
|**database_name**|**sysname**|오류가 있는 경우 경고가 시작되도록 해 놓은 데이터베이스입니다. 데이터베이스 이름이 NULL인 경우에는 오류 발생 위치에 상관 없이 경고가 시작됩니다.|  
|**event_description_keyword**|**nvarchar (100)**|제공된 문자 시퀀스와 동일해야 하는 Windows 애플리케이션 로그 내의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류에 대한 설명입니다.|  
|**occurrence_count**|**int**|경고가 발생한 횟수입니다.|  
|**count_reset_date**|**int**|**Occurrence_count** 마지막으로 다시 설정 된 날짜입니다.|  
|**count_reset_time**|**int**|**Occurrence_count** 마지막으로 다시 설정 된 시간입니다.|  
|**job_id**|**uniqueidentifier**|경고에 응답하여 실행할 작업의 ID입니다.|  
|**job_name**|**sysname**|경고에 대한 응답으로 실행할 작업의 이름입니다.|  
|**has_notification**|**int**|이 경고를 한 명 이상의 운영자에게 알려 주는 경우에는 0이 아닌 값을 사용합니다. 값은 다음 중 하나 이상이 될 수 있습니다(OR 연산 사용).<br /><br /> **1**= 전자 메일 알림 포함<br /><br /> **2**= 호출기 알림<br /><br /> **4**= **net send** 알림을 가집니다.|  
|**flags**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**performance_condition**|**nvarchar(512)**|**Type** 이 **2**인 경우이 열은 성능 조건에 대 한 정의를 표시 합니다. 그렇지 않으면 열이 NULL입니다.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0의 경우 항상 '[범주화되지 않음]'입니다.|  
|**wmi_namespace**|**sysname**|**Type** 이 **3**인 경우이 열은 WMI 이벤트에 대 한 네임 스페이스를 표시 합니다.|  
|**wmi_query**|**nvarchar(512)**|**Type** 이 **3**인 경우이 열은 WMI 이벤트에 대 한 쿼리를 표시 합니다.|  
|**type**|**int**|이벤트의 유형은 다음과 같습니다.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트 경고<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능 경고<br /><br /> **3** = WMI 이벤트 경고|  
  
 ** \@ Legacy_format** **1**이면 **sp_help_alert** 는 다음 결과 집합을 생성 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|시스템이 할당한 고유한 정수 ID입니다.|  
|**name**|**sysname**|경고 이름 (예: Demo: Full **msdb** log).|  
|**event_source**|**nvarchar (100)**|이벤트의 원본입니다. 버전 7.0의 경우 항상 **MSSQLServer** 입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|경고를 정의하는 메시지 오류 번호로서 일반적으로 **sysmessages** 테이블의 오류 번호에 해당 합니다. 심각도를 사용 하 여 경고를 정의 하는 경우 **message_id** 은 **0** 또는 NULL입니다.|  
|**severity**|**int**|경고를 정의 하는 심각도 수준 ( **9** 부터 **25**, **110**, **120**, **130**또는 1**40**)입니다.|  
|**사용**|**tinyint**|경고가 현재 활성화 되어 있는지 (**1**) 또는 그렇지 않은지 (**0**)의 상태입니다. 사용할 수 없는 경고는 전달되지 않습니다.|  
|**delay_between_responses**|**int**|경고에 대한 응답 간의 대기 시간(초)입니다.|  
|**last_occurrence_date**|**int**|마지막으로 경고가 발생한 날짜입니다.|  
|**last_occurrence_time**|**int**|마지막으로 경고가 발생한 시간입니다.|  
|**last_response_date**|**int**|**SQLServerAgent** 서비스가 마지막으로 경고에 응답 한 날짜입니다.|  
|**last_response_time**|**int**|**SQLServerAgent** 서비스가 마지막으로 경고에 응답 한 시간입니다.|  
|**notification_message**|**nvarchar(512)**|전자 메일 또는 호출기 알림의 일부로서 운영자에게 선택적으로 전달되는 추가 메시지입니다.|  
|**include_event_description**|**tinyint**|Windows 애플리케이션 로그의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류에 대한 설명을 알림 메시지의 일부로 포함할지 여부입니다.|  
|**database_name**|**sysname**|오류가 있는 경우 경고가 시작되도록 해 놓은 데이터베이스입니다. 데이터베이스 이름이 NULL인 경우에는 오류 발생 위치에 상관 없이 경고가 시작됩니다.|  
|**event_description_keyword**|**nvarchar (100)**|제공된 문자 시퀀스와 동일해야 하는 Windows 애플리케이션 로그 내의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류에 대한 설명입니다.|  
|**occurrence_count**|**int**|경고가 발생한 횟수입니다.|  
|**count_reset_date**|**int**|**Occurrence_count** 마지막으로 다시 설정 된 날짜입니다.|  
|**count_reset_time**|**int**|**Occurrence_count** 마지막으로 다시 설정 된 시간입니다.|  
|**job_id**|**uniqueidentifier**|작업 ID입니다.|  
|**job_name**|**sysname**|요청 시 작업으로서 경고에 대한 응답으로 실행되어야 합니다.|  
|**has_notification**|**int**|이 경고를 한 명 이상의 운영자에게 알려 주는 경우에는 0이 아닌 값을 사용합니다. 값은 다음 중 하나 이상이 될 수 있습니다(OR 연산으로 조인).<br /><br /> **1**= 전자 메일 알림 포함<br /><br /> **2**= 호출기 알림<br /><br /> **4**= **net send** 알림을 가집니다.|  
|**flags**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].|  
|**performance_condition**|**nvarchar(512)**|**Type** 이 **2**인 경우이 열은 성능 조건의 정의를 표시 합니다. **Type** 이 **3**인 경우이 열은 WMI 이벤트에 대 한 쿼리를 표시 합니다. 그렇지 않은 경우 이 열은 NULL입니다.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]7.0에 대해 항상 '**[범주화**되지 않음] '이 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**type**|**int**|경고의 유형은 다음과 같습니다.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트 경고<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능 경고<br /><br /> **3** = WMI 이벤트 경고|  
  
## <a name="remarks"></a>설명  
 **sp_help_alert** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
## <a name="permissions"></a>권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 **msdb** 데이터베이스의 **SQLAgentOperatorRole** 고정 데이터베이스 역할을 부여 받아야 합니다.  
  
 **SQLAgentOperatorRole**에 대 한 자세한 내용은 [고정 데이터베이스 역할 SQL Server 에이전트](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조 하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Demo: Sev. 25 Errors` 경고에 대한 정보를 보고합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_alert &#40;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [Transact-sql&#41;sp_update_alert &#40;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
