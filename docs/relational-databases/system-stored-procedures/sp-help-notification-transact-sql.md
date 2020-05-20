---
title: sp_help_notification (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_notification
- sp_help_notification_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_notification
ms.assetid: 0273457f-9d2a-4a6f-9a16-6a6bf281cba0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dbba9ea2f9df7e9a9fd154193c8f52fe904899c7
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820450"
---
# <a name="sp_help_notification-transact-sql"></a>sp_help_notification(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 운영자에 관한 경고 목록 또는 지정된 경고에 관한 운영자 목록을 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_notification  
     [ @object_type = ] 'object_type' ,  
     [ @name = ] 'name' ,  
     [ @enum_type = ] 'enum_type' ,   
     [ @notification_method = ] notification_method   
     [ , [ @target_name = ] 'target_name' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @object_type = ] 'object_type'`반환 될 정보의 형식입니다. *object_type*은 **char (9)** 이며 기본값은 없습니다. *object_type* 은 제공 된 운영자 이름에 할당 된 경고를 나열 하는 경고*또는 제공* 된 경고 이름을 담당 하는 운영자를 나열 하는 연산자 일 수 있습니다 *.*  
  
`[ @name = ] 'name'`운영자 이름 ( *object_type* 가 OPERATORS 인 경우) 또는 경고 이름 ( *object_type* 가 ALERTS 인 경우)입니다. *name* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @enum_type = ] 'enum_type'`반환 되는 *object_type*정보입니다. 대부분의 경우 *enum_type* 는 실제입니다. *enum_type*은 **char (10)** 이며 기본값은 없고 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|ACTUAL|*이름*에 연결 된 *object_types* 나열 합니다.|  
|ALL|*이름*에 연결 되지 않은 object_types를 포함 하 여 모든*object_types* 을 나열 합니다.|  
|TARGET|*이름과*의 연결에 관계 없이 제공 된 *target_name*일치 하는 *object_types* 나열 합니다.|  
  
`[ @notification_method = ] notification_method`반환할 알림 방법 열을 결정 하는 숫자 값입니다. *notification_method* 은 **tinyint**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1**|전자 메일: **use_email** 열만 반환 합니다.|  
|**2**|Pager: **use_pager** 열만 반환 합니다.|  
|**4**|NetSend: **use_netsend** 열만 반환 합니다.|  
|**7**|All: 모든 열을 반환합니다.|  
  
`[ @target_name = ] 'target_name'`검색할 경고 이름 ( *object_type* 가 ALERTS 인 경우) 또는 검색할 운영자 이름 ( *object_type* 가 OPERATORS 인 경우)입니다. *target_name* 은 *enum_type* 대상인 경우에만 필요 합니다. *target_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-valves"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 *Object_type* **경고**인 경우에는 결과 집합에 지정 된 운영자에 대 한 모든 경고가 나열 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|경고 ID 번호입니다.|  
|**alert_name**|**sysname**|경고 이름입니다.|  
|**use_email**|**int**|운영자에게 알리는 데 전자 메일을 사용합니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**use_pager**|**int**|운영자에게 알리는 데 호출기를 사용합니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**use_netsend**|**int**|운영자에게 알리는 데 네트워크 팝업을 사용합니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**has_email**|**int**|해당 경고에 대해 전자 메일 알림을 전달한 횟수입니다.|  
|**has_pager**|**int**|해당 경고에 대해 호출기 알림을 전달한 횟수입니다.|  
|**has_netsend**|**int**|이 경고에 대해 전송 된 **net send** 알림 수입니다.|  
  
 **Object_type** 가 **operators**인 경우 결과 집합에 지정 된 경고에 대 한 모든 연산자가 나열 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**operator_id**|**int**|운영자의 ID입니다.|  
|**operator_name**|**sysname**|운영자 이름입니다.|  
|**use_email**|**int**|운영자에게 알리는 데 전자 메일을 사용합니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**use_pager**|**int**|운영자에게 알리는 데 호출기를 사용합니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**use_netsend**|**int**|운영자에게 알리는 데 네트워크 팝업을 사용합니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**has_email**|**int**|운영자에게 전자 메일 주소가 있습니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**has_pager**|**int**|운영자에게 호출기 주소가 있습니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**has_netsend**|**int**|운영자가 Net Send 알림을 구성했습니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
  
## <a name="remarks"></a>설명  
 이 저장 프로시저는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-alerts-for-a-specific-operator"></a>A. 특정 운영자에 대한 경고 나열  
 다음 예에서는 `François Ajenstat`라는 운영자가 받는 모든 종류의 알림에 관한 경고를 모두 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_notification   
    @object_type = N'ALERTS',  
    @name = N'François Ajenstat',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
### <a name="b-listing-operators-for-a-specific-alert"></a>B. 특정 경고에 대한 운영자 나열  
 다음 예에서는 `Test Alert`라는 경고에 관한 모든 종류의 알림을 받는 운영자를 모두 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_notification  
    @object_type = N'OPERATORS',  
    @name = N'Test Alert',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_notification &#40;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [Transact-sql&#41;sp_delete_notification &#40;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [Transact-sql&#41;sp_update_notification &#40;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
