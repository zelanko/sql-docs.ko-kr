---
title: sp_help_notification (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_notification
- sp_help_notification_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_notification
ms.assetid: 0273457f-9d2a-4a6f-9a16-6a6bf281cba0
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cfc84d05393174ba804a5c3fc407da0e2fbe2159
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpnotification-transact-sql"></a>sp_help_notification(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 운영자에 관한 경고 목록 또는 지정된 경고에 관한 운영자 목록을 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@object_type =**] **'***object_type***'**  
 반환할 정보 유형입니다. *object_type*은 **char (9)**, 기본값은 없습니다. *object_type* 수 경고를 제공된 된 운영자 이름에 할당 된 경고를 나열 하 *,* 또는 제공된 된 경고 이름을 담당 운영자를 나열 하는 연산자*합니다.*  
  
 [ **@name =**]  **'***name***'**  
 운영자 이름 (경우 *object_type* 운영자) 또는 경고 이름 (경우 *object_type* 가 경고). *이름* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@enum_type =**] **'***enum_type***'**  
 *object_type*반환 되는 정보입니다. *enum_type* 은 대부분의 경우에서 ACTUAL입니다. *enum_type*은 **char (10)** 이며 기본값은 없고 수 있습니다 이러한 값 중 하나 여야 합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|ACTUAL|만 나열 된 *object_types* 연관 *이름*합니다.|  
|ALL|모든 나열 된*object_types* 에 연결 되지 않은 것을 비롯 하 *이름*합니다.|  
|TARGET|만 나열 된 *object_types* 제공 된 일치 하는 *target_name*와 관계 없이*이름*합니다.|  
  
 [  **@notification_method =**] *notification_method*  
 반환할 알림 방법 열을 결정하는 숫자 값입니다. *notification_method* 은 **tinyint**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**1**|전자 메일:만 반환 된 **use_email** 열입니다.|  
|**2**|페이징:만 반환 된 **use_pager** 열입니다.|  
|**4**|NetSend:만 반환 된 **use_netsend** 열입니다.|  
|**7**|All: 모든 열을 반환합니다.|  
  
 [ **@target_name =**] **'***target_name***'**  
 검색할 경고 이름 (경우 *object_type* 가 경고) 또는 검색할 운영자 이름 (경우 *object_type* is 연산자). *target_name* 경우에 필요 *enum_type* 대상입니다. *target_name* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-valves"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 경우 *object_type* 은 **경고**, 결과 집합의 지정된 된 연산자에 대 한 모든 경고를 나열 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|경고 ID 번호입니다.|  
|**alert_name**|**sysname**|경고 이름입니다.|  
|**use_email**|**int**|운영자에게 알리는 데 전자 메일을 사용합니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**use_pager**|**int**|운영자에게 알리는 데 호출기를 사용합니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**use_netsend**|**int**|운영자에게 알리는 데 네트워크 팝업을 사용합니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**has_email**|**int**|해당 경고에 대해 전자 메일 알림을 전달한 횟수입니다.|  
|**has_pager**|**int**|해당 경고에 대해 호출기 알림을 전달한 횟수입니다.|  
|**has_netsend**|**int**|수가 **net send** 이 경고에 대 한 보낸 알림입니다.|  
  
 경우 **object_type** 은 **연산자**, 결과 집합의 지정된 된 경고에 관한 모든 운영자를 나열 합니다.  
  
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
  
## <a name="remarks"></a>주의  
 이 저장된 프로시저에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-alerts-for-a-specific-operator"></a>1. 특정 운영자에 대한 경고 나열  
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
  
### <a name="b-listing-operators-for-a-specific-alert"></a>2. 특정 경고에 대한 운영자 나열  
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
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_update_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
