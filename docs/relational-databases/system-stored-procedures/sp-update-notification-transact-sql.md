---
description: sp_update_notification(Transact-SQL)
title: sp_update_notification (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_notification_TSQL
- sp_update_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatenotification
ms.assetid: 3e1c3d40-8c24-46ce-a68e-ce6c6a237fda
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 32ddc8e2afae79b458d39f577d75176ba6f9dec1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473533"
---
# <a name="sp_update_notification-transact-sql"></a>sp_update_notification(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  경고 알림의 알림 방법을 업데이트합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_update_notification  
          [@alert_name =] 'alert' ,  
     [@operator_name =] 'operator' ,  
     [@notification_method =] notification  
```  
  
## <a name="arguments"></a>인수  
`[ @alert_name = ] 'alert'` 이 알림과 연결 된 경고의 이름입니다. *경고* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @operator_name = ] 'operator'` 경고가 발생 하는 경우 알림을 받을 운영자입니다. *연산자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @notification_method = ] notification` 운영자에 게 알리는 방법입니다. *알림은* **tinyint**이며 기본값은 없고 다음 값 중 하나 이상이 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|전자 메일|  
|**2**|호출기|  
|**4**|**net send**|  
|**7**|모든 방법|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_update_notification** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
 지정 된 *notification_method*를 사용 하 여 필요한 주소 정보가 없는 운영자에 대 한 알림을 업데이트할 수 있습니다. 전자 메일 메시지 또는 호출기 알림을 보내는 중에 실패하면 Microsoft SQL Server 에이전트 오류 로그에 실패가 보고됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행 하려면 사용자에 게 **sysadmin** 고정 서버 역할을 부여 해야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 경고에 대해로 전송 된 알림에 대 한 알림 방법을 수정 합니다 `François Ajenstat` `Test Alert` .  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_notification  
   @alert_name = N'Test Alert',  
   @operator_name = N'François Ajenstat',  
   @notification_method = 7;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_notification &#40;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [Transact-sql&#41;sp_delete_notification &#40;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [Transact-sql&#41;sp_help_notification &#40;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
