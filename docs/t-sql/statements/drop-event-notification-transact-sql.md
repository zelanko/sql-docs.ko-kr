---
title: DROP EVENT NOTIFICATION (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EVENT NOTIFICATION
- DROP_EVENT_NOTIFICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event notifications [SQL Server], removing
- deleting event notifications
- dropping event notifications
- DROP EVENT NOTIFICATION statement
- removing event notifications
ms.assetid: 0ffd8f47-4ea3-4238-9e73-c318df710cf7
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ab32a9ffadce83635e8ef987607af913fe0f2472
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-event-notification-transact-sql"></a>DROP EVENT NOTIFICATION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에서 이벤트 알림 트리거를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP EVENT NOTIFICATION notification_name [ ,...n ]  
ON { SERVER | DATABASE | QUEUE queue_name }  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *notification_name*  
 제거할 이벤트 알림의 이름입니다. 이벤트 알림을 여러 개 지정할 수 있습니다. 현재 생성된 된 이벤트 알림 목록을 보려면 [sys.event_notifications&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md).  
  
 SERVER  
 이벤트 알림의 범위가 현재 서버로 적용됨을 나타냅니다. 이벤트 알림이 생성될 때 SERVER를 지정한 경우 반드시 SERVER를 지정해야 합니다.  
  
 DATABASE  
 이벤트 알림의 범위가 현재 데이터베이스로 적용됨을 나타냅니다. 이벤트 알림이 생성될 때 DATABASE를 지정한 경우 반드시 DATABASE를 지정해야 합니다.  
  
 큐 *queue_name*  
 에 지정 된 큐에 적용 되는 이벤트 알림의 범위를 나타냅니다 *queue_name*합니다. 이벤트 알림이 생성될 때 QUEUE를 지정한 경우 반드시 QUEUE를 지정해야 합니다. *queue_name* 큐의 이름이 며도 지정 해야 합니다.  
  
## <a name="remarks"></a>주의  
 트랜잭션 내에서 이벤트 알림이 발생하고 같은 트랜잭션 내에서 삭제되는 경우 이벤트 알림 인스턴스가 전달된 다음 이벤트 알림이 삭제됩니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스 수준 범위의 이벤트 알림을 삭제하려면 사용자는 최소한 해당 이벤트 알림의 소유자이거나 현재 데이터베이스에서 ALTER ANY DATABASE EVENT NOTIFICATION 권한을 가지고 있어야 합니다.  
  
 서버 수준 범위의 이벤트 알림을 삭제하려면 사용자는 최소한 해당 이벤트 알림의 소유자이거나 현재 서버에서 ALTER ANY EVENT NOTIFICATION 권한을 가지고 있어야 합니다.  
  
 특정 큐의 이벤트 알림을 삭제하려면 사용자는 최소한 해당 이벤트 알림의 소유자이거나 부모 큐에 대한 ALTER 권한을 가지고 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스 범위 이벤트 알림을 만든 다음 삭제합니다.  
  
```tsql  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
GO  
DROP EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [EVENT notification&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-event-notification-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.event_notifications&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [sys.events &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)  
  
  

