---
title: sp_update_notification (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_notification_TSQL
- sp_update_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatenotification
ms.assetid: 3e1c3d40-8c24-46ce-a68e-ce6c6a237fda
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc08790ad08ce6bb4e94e61a8c3bdfc58615edf9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spupdatenotification-transact-sql"></a>sp_update_notification(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  경고 알림의 알림 방법을 업데이트합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_update_notification  
          [@alert_name =] 'alert' ,  
     [@operator_name =] 'operator' ,  
     [@notification_method =] notification  
```  
  
## <a name="arguments"></a>인수  
 [ **@alert_name =**] **'***alert***'**  
 이 알림과 연결된 경고의 이름입니다. *경고* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@operator_name =**]  **'***operator***'**  
 경고가 발생할 경우 알림을 받을 운영자입니다. *연산자* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@notification_method =**] *알림*  
 운영자에게 알림을 보내는 방법입니다. *알림*은 **tinyint**, 수 및 기본값은 없고 다음이 값 중 하나 이상이 될 합니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**1**|전자 메일|  
|**2**|호출기|  
|**4**|**Net Send**|  
|**7**|모든 방법|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_update_notification** 에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
 알림을 사용 하 여 필요한 주소 정보가 없는 운영자를 업데이트할 수 있는 *notification_method*합니다. 전자 메일 메시지 또는 호출기 알림을 보내는 중에 실패하면 Microsoft SQL Server 에이전트 오류 로그에 실패가 보고됩니다.  
  
## <a name="permissions"></a>Permissions  
 이 저장된 프로시저를 실행 하려면 사용자에 게 부여 해야 합니다는 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 수정에 게 알림 보내는 알림 방법을 `François Ajenstat`경고에 대 한 `Test Alert`합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_notification  
   @alert_name = N'Test Alert',  
   @operator_name = N'François Ajenstat',  
   @notification_method = 7;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
