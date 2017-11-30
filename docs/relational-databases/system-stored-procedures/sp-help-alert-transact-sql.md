---
title: sp_help_alert (Transact SQL) | Microsoft Docs
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
- sp_help_alert
- sp_help_alert_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_alert
ms.assetid: 850cef4e-6348-4439-8e79-fd1bca712091
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d574d40ff9c65f9a677fd0a4946428598b91476d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpalert-transact-sql"></a>sp_help_alert(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버에 대해 정의된 경고에 관한 정보를 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_alert [ [ @alert_name = ] 'alert_name' ]   
     [ , [ @order_by = ] 'order_by' ]   
     [ , [ @alert_id = ] alert_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @legacy_format = ] legacy_format ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@alert_name =**] **'***alert_name***'**  
 경고 이름입니다. *alert_name* 은 **nvarchar (128)**합니다. 경우 *alert_name* 은 지정 하지 않으면 모든 경고에 대 한 정보가 반환 됩니다.  
  
 [  **@order_by =**] **'***order_by***'**  
 결과를 생성하는 데 사용할 정렬 순서입니다. *order_by*은 **sysname**, N의 기본값 '*이름*'.  
  
 [  **@alert_id =**] *alert_id*  
 보고할 정보가 있는 경고의 ID입니다. *alert_id*은 **int**, 기본값은 NULL입니다.  
  
 [  **@category_name =**] **'***범주***'**  
 경고의 범주입니다. *범주* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@legacy_format** =] *legacy_format*  
 레거시 결과 집합을 생성할지 여부입니다. *legacy_format* 은 **비트**, 기본값은 **0**합니다. 때 *legacy_format* 은 **1**, **sp_help_alert** 반환한 결과 집합을 반환 **sp_help_alert** Microsoft SQL Server 2000에 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 때  **@legacy_format**  은 **0**, **sp_help_alert** 다음과 같은 결과 집합을 생성 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**id**|**int**|시스템이 할당한 고유한 정수 ID입니다.|  
|**name**|**sysname**|경고 이름 (예를 들어 데모: 전체 **msdb** 로그).|  
|**event_source**|**nvarchar (100)**|이벤트의 원본입니다. 항상 **MSSQLServer** 에 대 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 7.0|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|경고를 정의하는 메시지 오류 번호로서 (의 오류 번호에 해당 하는 일반적으로 **sysmessages** 테이블). 심각도 경고를 정의 하는 데 사용 되는 경우 **message_id** 은 **0** 또는 NULL입니다.|  
|**심각도**|**int**|심각도 수준 (에서 **9** 통해 **25**, **110**, **120**, **130**, 또는 **140**) 경고를 정의 하는입니다.|  
|**사용 하도록 설정**|**tinyint**|경고가 현재 활성화 되어 있는지 여부의 상태 (**1**) 아닌지 (**0**). 사용할 수 없는 경고는 전달되지 않습니다.|  
|**delay_between_responses**|**int**|경고에 대한 응답 간의 대기 시간(초)입니다.|  
|**last_occurrence_date**|**int**|마지막으로 경고가 발생한 날짜입니다.|  
|**last_occurrence_time**|**int**|마지막으로 경고가 발생한 시간입니다.|  
|**last_response_date**|**int**|날짜 경고가 마지막으로 응답 하는 **SQLServerAgent** 서비스입니다.|  
|**last_response_time**|**int**|시간 경고가 마지막으로 응답 하는 **SQLServerAgent** 서비스입니다.|  
|**notification_message**|**nvarchar(512)**|전자 메일 또는 호출기 알림의 일부로서 운영자에게 선택적으로 전달되는 추가 메시지입니다.|  
|**include_event_description**|**tinyint**|Microsoft Windows 응용 프로그램 로그의 SQL Server 오류에 대한 설명을 알림 메시지의 일부로 포함할지 여부입니다.|  
|**database_name**|**sysname**|오류가 있는 경우 경고가 시작되도록 해 놓은 데이터베이스입니다. 데이터베이스 이름이 NULL인 경우에는 오류 발생 위치에 상관 없이 경고가 시작됩니다.|  
|**event_description_keyword**|**nvarchar (100)**|제공된 문자 시퀀스와 동일해야 하는 Windows 응용 프로그램 로그 내의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류에 대한 설명입니다.|  
|**occurrence_count**|**int**|경고가 발생한 횟수입니다.|  
|**count_reset_date**|**int**|날짜는 **occurrence_count** 마지막으로 다시 설정 합니다.|  
|**count_reset_time**|**int**|시간은 **occurrence_count** 마지막으로 다시 설정 합니다.|  
|**job_id**|**uniqueidentifier**|경고에 응답하여 실행할 작업의 ID입니다.|  
|**job_name**|**sysname**|경고에 대한 응답으로 실행할 작업의 이름입니다.|  
|**has_notification**|**int**|이 경고를 한 명 이상의 운영자에게 알려 주는 경우에는 0이 아닌 값을 사용합니다. 값은 다음 중 하나 이상이 될 수 있습니다(OR 연산 사용).<br /><br /> **1**= 전자 메일 알림<br /><br /> **2**= 호출기 알림<br /><br /> **4**=에 **net send** 알림입니다.|  
|**플래그**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**performance_condition**|**nvarchar(512)**|경우 **형식** 은 **2**,이 열은 성능 조건의 정의 보여 줍니다. 그렇지 않으면 열은 NULL입니다.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0의 경우 항상 '[범주화되지 않음]'입니다.|  
|**wmi_namespace**|**sysname**|경우 **형식** 은 **3**,이 열은 WMI 이벤트에 대 한 네임 스페이스를 표시 합니다.|  
|**wmi_query**|**nvarchar(512)**|경우 **형식** 은 **3**,이 열은 WMI 이벤트에 대 한 쿼리를 보여 줍니다.|  
|**유형**|**int**|이벤트의 유형은 다음과 같습니다.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트 경고<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능 경고<br /><br /> **3** = WMI 이벤트 경고|  
  
 때  **@legacy_format**  은 **1**, **sp_help_alert** 다음과 같은 결과 집합을 생성 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**id**|**int**|시스템이 할당한 고유한 정수 ID입니다.|  
|**name**|**sysname**|경고 이름 (예를 들어 데모: 전체 **msdb** 로그).|  
|**event_source**|**nvarchar (100)**|이벤트의 원본입니다. 항상 **MSSQLServer** 에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 7.0|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|경고를 정의하는 메시지 오류 번호로서 (의 오류 번호에 해당 하는 일반적으로 **sysmessages** 테이블). 심각도 경고를 정의 하는 데 사용 되는 경우 **message_id** 은 **0** 또는 NULL입니다.|  
|**심각도**|**int**|심각도 수준 (에서 **9** 통해 **25**, **110**, **120**, **130**, 1 또는**40**) 경고를 정의 하는입니다.|  
|**사용 하도록 설정**|**tinyint**|경고가 현재 활성화 되어 있는지 여부의 상태 (**1**) 아닌지 (**0**). 사용할 수 없는 경고는 전달되지 않습니다.|  
|**delay_between_responses**|**int**|경고에 대한 응답 간의 대기 시간(초)입니다.|  
|**last_occurrence_date**|**int**|마지막으로 경고가 발생한 날짜입니다.|  
|**last_occurrence_time**|**int**|마지막으로 경고가 발생한 시간입니다.|  
|**last_response_date**|**int**|날짜 경고가 마지막으로 응답 하는 **SQLServerAgent** 서비스입니다.|  
|**last_response_time**|**int**|시간 경고가 마지막으로 응답 하는 **SQLServerAgent** 서비스입니다.|  
|**notification_message**|**nvarchar(512)**|전자 메일 또는 호출기 알림의 일부로서 운영자에게 선택적으로 전달되는 추가 메시지입니다.|  
|**include_event_description**|**tinyint**|Windows 응용 프로그램 로그의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류에 대한 설명을 알림 메시지의 일부로 포함할지 여부입니다.|  
|**database_name**|**sysname**|오류가 있는 경우 경고가 시작되도록 해 놓은 데이터베이스입니다. 데이터베이스 이름이 NULL인 경우에는 오류 발생 위치에 상관 없이 경고가 시작됩니다.|  
|**event_description_keyword**|**nvarchar (100)**|제공된 문자 시퀀스와 동일해야 하는 Windows 응용 프로그램 로그 내의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류에 대한 설명입니다.|  
|**occurrence_count**|**int**|경고가 발생한 횟수입니다.|  
|**count_reset_date**|**int**|날짜는 **occurrence_count** 마지막으로 다시 설정 합니다.|  
|**count_reset_time**|**int**|시간은 **occurrence_count** 마지막으로 다시 설정 합니다.|  
|**job_id**|**uniqueidentifier**|작업 ID입니다.|  
|**job_name**|**sysname**|요청 시 작업으로서 경고에 대한 응답으로 실행되어야 합니다.|  
|**has_notification**|**int**|이 경고를 한 명 이상의 운영자에게 알려 주는 경우에는 0이 아닌 값을 사용합니다. 값은 다음 중 하나 이상이 될 수 있습니다(OR 연산으로 조인).<br /><br /> **1**= 전자 메일 알림<br /><br /> **2**= 호출기 알림<br /><br /> **4**=에 **net send** 알림입니다.|  
|**플래그**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]을 참조하세요.|  
|**performance_condition**|**nvarchar(512)**|경우 **형식** 은 **2**,이 열은 성능 조건의 정의 보여 줍니다. 경우 **형식** 은 **3**,이 열은 WMI 이벤트에 대 한 쿼리를 보여 줍니다. 그렇지 않은 경우 이 열은 NULL입니다.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]항상 '**[범주화]**'에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0입니다.|  
|**유형**|**int**|경고의 유형은 다음과 같습니다.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트 경고<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능 경고<br /><br /> **3** = WMI 이벤트 경고|  
  
## <a name="remarks"></a>주의  
 **sp_help_alert** 에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 **msdb** 데이터베이스의 **SQLAgentOperatorRole** 고정 데이터베이스 역할을 부여 받아야 합니다.  
  
 에 대 한 내용은 **SQLAgentOperatorRole**, 참조 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Demo: Sev. 25 Errors` 경고에 대한 정보를 보고합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_alert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_update_alert &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
