---
title: sp_add_notification (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_notification_TSQL
- sp_add_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_notification
ms.assetid: 0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fcf55efd5b50f73d15e0fc488cfe4298b99d9eb7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85646489"
---
# <a name="sp_add_notification-transact-sql"></a>sp_add_notification(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  경고에 대한 알림을 설정합니다.  
  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_notification [ @alert_name = ] 'alert' ,   
    [ @operator_name = ] 'operator' ,   
    [ @notification_method = ] notification_method  
```  
  
## <a name="arguments"></a>인수  
`[ @alert_name = ] 'alert'`이 알림에 대 한 경고입니다. *경고* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @operator_name = ] 'operator'`경고가 발생할 때 알림을 받을 운영자입니다. *연산자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @notification_method = ] notification_method`운영자에 게 알리는 방법입니다. *notification_method* 은 **tinyint**이며 기본값은 없습니다. *notification_method* 는 **or** 논리 연산자와 함께 사용할 수 있는 값 중 하나 이상이 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|전자 메일|  
|**2**|호출기|  
|**4**|**net send**|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_add_notification** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 그래픽 방식으로 전체 경고 시스템을 간편하게 관리할 수 있도록 해 줍니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하면 경고 인프라를 쉽게 구성할 수 있습니다.  
  
 경고에 대한 응답으로 알림을 보내려면 먼저 메일을 보낼 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성해야 합니다.  
  
 전자 메일 메시지 또는 호출기 알림을 전송하는 동안 오류가 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 오류 로그에 오류가 보고됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_add_notification**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 지정된 경고(`Test Alert`)에 전자 메일 알림을 추가합니다.  
  
> **참고:** 이 예에서는가 `Test Alert` 이미 존재 하며이는 `François Ajenstat` 유효한 연산자 이름 이라고 가정 합니다.  
  
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
 [Transact-sql&#41;sp_delete_notification &#40;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [Transact-sql&#41;sp_help_notification &#40;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [Transact-sql&#41;sp_update_notification &#40;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [Transact-sql&#41;sp_add_operator &#40;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
