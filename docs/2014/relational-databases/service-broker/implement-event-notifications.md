---
title: 이벤트 알림 구현 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], target service
- target service [SQL Server]
- event notifications [SQL Server], creating
ms.assetid: 29ac8f68-a28a-4a77-b67b-a8663001308c
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aaef3c95e4f6a6ce9c24b4c4982e9f6ace428491
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251835"
---
# <a name="implement-event-notifications"></a>이벤트 알림 구현
  이벤트 알림을 구현하려면 먼저 이벤트 알림을 받을 대상 서비스를 만든 다음 이벤트 알림을 만들어야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 보안을 구성해야 합니다. 대화 보안은 전체 보안 모델에 따라 수동으로 구성해야 합니다.  
  
## <a name="creating-the-target-service"></a>대상 서비스 만들기  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에는 다음 특정 메시지 유형과 이벤트 알림에 대한 계약이 포함되어 있으므로 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 를 시작하는 서비스를 만들지 않아도 됩니다.  
  
```  
http://schemas.microsoft.com/SQL/Notifications/PostEventNotification  
```  
  
 이벤트 알림을 받는 대상 서비스는 이러한 기존 계약을 인식해야 합니다.  
  
 **대상 서비스를 만들려면**  
  
1.  메시지를 받을 큐를 만듭니다.  
  
    > [!NOTE]  
    >  큐에서 `http://schemas.microsoft.com/SQL/Notifications/QueryNotification`의 메시지 유형을 받습니다.  
  
2.  이벤트 알림 계약을 참조하는 큐에 서비스를 만듭니다.  
  
3.  서비스에 경로를 만들어 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 에서 서비스에 대한 메시지를 보낼 주소를 정의합니다. 같은 데이터베이스의 서비스를 대상으로 하는 이벤트 알림의 경우 `ADDRESS = 'LOCAL'`을 지정합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 라우팅에 의해 알림 메시지를 받는 서비스가 결정됩니다. 이벤트 알림 대상이 원격 서버의 서비스일 경우 양방향 통신을 위해 원본 서버와 대상 서버에 모두 경로가 정의되어 있어야 합니다.  
  
 다음 예에서는 이벤트 알림 계약의 메시지를 처리하기 위해 큐, 큐의 서비스 및 서비스의 경로를 만듭니다.  
  
```  
CREATE QUEUE NotifyQueue ;  
GO  
CREATE SERVICE NotifyService  
ON QUEUE NotifyQueue  
(  
[http://schemas.microsoft.com/SQL/Notifications/PostEventNotification]  
);  
GO  
CREATE ROUTE NotifyRoute  
WITH SERVICE_NAME = 'NotifyService',  
ADDRESS = 'LOCAL';  
GO  
```  
  
## <a name="creating-the-event-notification"></a>이벤트 알림 만들기  
 이벤트 알림은 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE EVENT NOTIFICATION 문으로 만들고 DROP EVENT NOTIFICATION 문으로 삭제합니다. 이벤트 알림을 수정하려면 해당 이벤트 알림을 삭제하고 다시 만들어야 합니다.  
  
 다음 예에서는 `CreateDatabaseNotification`이벤트 알림을 만듭니다. 이 알림은 서버에서 발생하는 `CREATE_DATABASE` 이벤트에 대한 메시지를 이전에 만든 `NotifyService` 서비스로 보냅니다.  
  
```  
CREATE EVENT NOTIFICATION CreateDatabaseNotification  
ON SERVER  
FOR CREATE_DATABASE  
TO SERVICE 'NotifyService', '8140a771-3c4b-4479-8ac0-81008ab17984' ;  
```  
  
> [!CAUTION]  
>  이벤트 알림은 CREATE_SCHEMA 이벤트와 CREATE SCHEMA 문의 <schema_element> 정의를 별도의 이벤트로 인식합니다. 예를 들어 CREATE_SCHEMA 및 CREATE_TABLE 이벤트에서 모두 이벤트 알림이 생성되며 다음 일괄 작업을 실행합니다.  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  이 경우 이벤트 알림은 CREATE_SCHEMA 이벤트가 발생할 때와 CREATE_TABLE 이벤트가 발생할 때 각각 한 번씩, 두 번 발생합니다. CREATE_SCHEMA 이벤트 및 해당하는 CREATE SCHEMA 정의의 <schema_element> 텍스트 둘 다에 대해 이벤트 알림이 생성되는 것을 방지하거나 필요 없는 이벤트 데이터의 캡처를 방지하는 논리를 응용 프로그램에 구축하는 것이 좋습니다.  
  
 **이벤트 알림을 만들려면**  
  
-   [CREATE EVENT NOTIFICATION&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-notification-transact-sql)  
  
 **이벤트 알림을 삭제하려면**  
  
-   [DROP EVENT NOTIFICATION&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-event-notification-transact-sql)  
  
## <a name="see-also"></a>관련 항목  
 [이벤트 알림에 대한 정보 가져오기](event-notifications.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
