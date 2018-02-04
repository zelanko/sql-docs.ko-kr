---
title: sp_add_notification (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_notification_TSQL
- sp_add_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_notification
ms.assetid: 0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 22e6f2373ba35b24d74b7045350c7cb78a504c05
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spaddnotification-transact-sql"></a>sp_add_notification(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  경고에 대한 알림을 설정합니다.  
  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_notification [ @alert_name = ] 'alert' ,   
    [ @operator_name = ] 'operator' ,   
    [ @notification_method = ] notification_method  
```  
  
## <a name="arguments"></a>인수  
 [ **@alert_name=** ] **'***alert***'**  
 이 알림에 대한 경고입니다. *경고* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@operator_name=** ] **'***operator***'**  
 경고가 발생할 경우 알림을 받을 운영자입니다. *연산자* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@notification_method=** ] *notification_method*  
 운영자에게 알림을 보내는 방법입니다. *notification_method* 은 **tinyint**, 기본값은 없습니다. *notification_method* 와 함께 다음이 값 중 하나 이상이 될 수는 **OR** 논리 연산자입니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**1**|전자 메일|  
|**2**|호출기|  
|**4**|**Net Send**|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_add_notification** 에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 그래픽 방식으로 전체 경고 시스템을 간편하게 관리할 수 있도록 해 줍니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하면 경고 인프라를 쉽게 구성할 수 있습니다.  
  
 경고에 대한 응답으로 알림을 보내려면 먼저 메일을 보낼 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성해야 합니다.  
  
 전자 메일 메시지 또는 호출기 알림을 전송하는 동안 오류가 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 오류 로그에 오류가 보고됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_add_notification**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 지정된 경고(`Test Alert`)에 전자 메일 알림을 추가합니다.  
  
> **참고:** 에 `Test Alert` 이미 존재 하 고 `François Ajenstat` 유효한 연산자 이름입니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_notification  
 @alert_name = N'Test Alert',  
 @operator_name = N'François Ajenstat',  
 @notification_method = 1 ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_delete_notification &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [sp_update_notification &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [sp_add_operator &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
