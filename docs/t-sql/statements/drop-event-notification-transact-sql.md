---
description: DROP EVENT NOTIFICATION(Transact-SQL)
title: DROP EVENT NOTIFICATION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9c3faeeac400e02f9cb01fcfc4af66c2ee5fe09d
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96131290"
---
# <a name="drop-event-notification-transact-sql"></a>DROP EVENT NOTIFICATION(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스에서 이벤트 알림 트리거를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
DROP EVENT NOTIFICATION notification_name [ ,...n ]  
ON { SERVER | DATABASE | QUEUE queue_name }  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *notification_name*  
 제거할 이벤트 알림의 이름입니다. 이벤트 알림을 여러 개 지정할 수 있습니다. 현재 생성된 이벤트 알림 목록을 보려면 [sys.event_notifications&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)를 사용하세요.  
  
 SERVER  
 이벤트 알림의 범위가 현재 서버로 적용됨을 나타냅니다. 이벤트 알림이 생성될 때 SERVER를 지정한 경우 반드시 SERVER를 지정해야 합니다.  
  
 DATABASE  
 이벤트 알림의 범위가 현재 데이터베이스로 적용됨을 나타냅니다. 이벤트 알림이 생성될 때 DATABASE를 지정한 경우 반드시 DATABASE를 지정해야 합니다.  
  
 QUEUE *queue_name*  
 이벤트 알림의 범위가 *queue_name* 에 지정된 큐로 적용됨을 나타냅니다. 이벤트 알림이 생성될 때 QUEUE를 지정한 경우 반드시 QUEUE를 지정해야 합니다. *queue_name* 은 큐의 이름이며 반드시 함께 지정해야 합니다.  
  
## <a name="remarks"></a>설명  
 트랜잭션 내에서 이벤트 알림이 발생하고 같은 트랜잭션 내에서 삭제되는 경우 이벤트 알림 인스턴스가 전달된 다음 이벤트 알림이 삭제됩니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스 수준 범위의 이벤트 알림을 삭제하려면 사용자는 최소한 해당 이벤트 알림의 소유자이거나 현재 데이터베이스에서 ALTER ANY DATABASE EVENT NOTIFICATION 권한을 가지고 있어야 합니다.  
  
 서버 수준 범위의 이벤트 알림을 삭제하려면 사용자는 최소한 해당 이벤트 알림의 소유자이거나 현재 서버에서 ALTER ANY EVENT NOTIFICATION 권한을 가지고 있어야 합니다.  
  
 특정 큐의 이벤트 알림을 삭제하려면 사용자는 최소한 해당 이벤트 알림의 소유자이거나 부모 큐에 대한 ALTER 권한을 가지고 있어야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 데이터베이스 범위 이벤트 알림을 만든 다음 삭제합니다.  
  
```sql  
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
  
## <a name="see-also"></a>참고 항목  
 [CREATE EVENT NOTIFICATION&#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.event_notifications&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [sys.events&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)  
  
  
