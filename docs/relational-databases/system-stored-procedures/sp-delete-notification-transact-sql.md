---
title: sp_delete_notification (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_notification_TSQL
- sp_delete_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_notification
ms.assetid: b55d3898-596d-47a5-a4f0-d65dc736223b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 19c0a4d2a95b81c26b746a8ece9defce61fe712f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68009128"
---
# <a name="sp_delete_notification-transact-sql"></a>sp_delete_notification(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정 경고 및 운영자에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 알림 정의를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_notification  
     [ @alert_name = ] 'alert' ,   
     [ @operator_name = ] 'operator'   
```  
  
## <a name="arguments"></a>인수  
`[ @alert_name = ] 'alert'`경고의 이름입니다. *경고* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @operator_name = ] 'operator'`운영자의 이름입니다. *연산자* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 알림을 제거하는 경우 알림만 제거되며 경고 및 운영자는 그대로 유지됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행 하려면 사용자에 게 **sysadmin** 고정 서버 역할을 부여 해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `François Ajenstat` 경고가 발생하는 경우 운영자 `Test Alert`에게 보낸 알림을 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_notification  
    @alert_name = 'Test Alert',  
    @operator_name = 'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_alert &#40;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [Transact-sql&#41;sp_add_notification &#40;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [Transact-sql&#41;sp_add_operator &#40;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [Transact-sql&#41;sp_delete_alert &#40;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [Transact-sql&#41;sp_help_alert &#40;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [Transact-sql&#41;sp_help_notification &#40;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [Transact-sql&#41;sp_help_operator &#40;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [Transact-sql&#41;sp_update_notification &#40;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
