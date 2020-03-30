---
title: CREATE EVENT NOTIFICATION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_EVENT_NOTIFICATION_TSQL
- NOTIFICATION_TSQL
- EVENT
- NOTIFICATION
- CREATE EVENT NOTIFICATION
- EVENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EVENT NOTIFICATION statement
- events [SQL Server], notifications
- event notifications [SQL Server], creating
ms.assetid: dbbff0e8-9e25-4f12-a1ba-e12221d16ac2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 98e784be4bbe4e939ed4413a33d6a3ed36872558
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67902808"
---
# <a name="create-event-notification-transact-sql"></a>CREATE EVENT NOTIFICATION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 또는 서버 이벤트에 대한 정보를 service broker 서비스로 보내는 개체를 만듭니다. 이벤트 알림은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 통해서만 생성됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE EVENT NOTIFICATION event_notification_name   
ON { SERVER | DATABASE | QUEUE queue_name }   
[ WITH FAN_IN ]  
FOR { event_type | event_group } [ ,...n ]  
TO SERVICE 'broker_service' , { 'broker_instance_specifier' | 'current database' }  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *event_notification_name*  
 이벤트 알림의 이름입니다. 이벤트 알림 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 준수하고 이들을 만든 SERVER, DATABASE 또는 *object_name* 범위 내에서 고유해야 합니다.  
  
 SERVER  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 인스턴스에 이벤트 알림 범위를 적용합니다. 지정한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에서 FOR 절에 지정한 이벤트가 발생할 때마다 알림이 발생합니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 DATABASE  
 현재 데이터베이스에 이벤트 알림의 범위를 적용합니다. 지정한 경우 현재 데이터베이스에서 FOR 절에 지정한 이벤트가 발생할 때마다 알림이 발생합니다.  
  
 QUEUE  
 현재 데이터베이스의 특정 큐에 알림의 범위를 적용합니다. FOR QUEUE_ACTIVATION이나 FOR BROKER_QUEUE_DISABLED도 지정한 경우에만 QUEUE를 지정할 수 있습니다.  
  
 *queue_name*  
 이벤트 알림이 적용되는 큐의 이름입니다. *queue_name*은 QUEUE가 지정된 경우에만 지정할 수 있습니다.  
  
 WITH FAN_IN  
 다음과 같은 모든 이벤트 알림에 대해 지정한 모든 서비스에 이벤트당 하나씩만 메시지를 보내도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 지시합니다.  
  
-   같은 이벤트에서 생성된 이벤트 알림  
  
-   같은 보안 주체(같은 SID로 식별됨)가 생성한 이벤트 알림  
  
-   같은 서비스 및 *broker_instance_specifier*를 지정합니다.  
  
-   WITH FAN_IN을 지정하는 이벤트 알림  
  
 예를 들어 3개의 이벤트 알림이 생성됩니다. 모든 이벤트 알림에서 FOR ALTER_TABLE, WITH FAN_IN, 동일한 TO SERVICE 절을 지정하며 같은 SID로 생성됩니다. ALTER TABLE 문을 실행하면 이러한 3개 이벤트 알림에 의해 생성된 메시지가 하나로 병합됩니다. 따라서 대상 서비스는 하나의 이벤트 메시지만 받게 됩니다.  
  
 *event_type*  
 이벤트 알림을 실행하게 하는 이벤트 유형의 이름입니다. *event_type*은 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 이벤트 유형, SQL 추적 이벤트 유형 또는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 이벤트 유형이 될 수 있습니다. 한정 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 이벤트 유형의 목록은 [DDL 이벤트](../../relational-databases/triggers/ddl-events.md)를 참조하세요. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 이벤트 유형은 QUEUE_ACTIVATION 및 BROKER_QUEUE_DISABLED입니다. 자세한 내용은 [Event Notifications](../../relational-databases/service-broker/event-notifications.md)을 참조하세요.  
  
 *event_group*  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 SQL 추적 이벤트 유형의 미리 정의된 그룹 이름입니다. 이벤트 그룹에 속해 있는 이벤트를 실행한 후 이벤트 알림이 발생할 수 있습니다. DDL 이벤트 그룹, 이 그룹에 속한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이벤트 및 이 그룹을 정의할 수 있는 범위의 목록은 [DDL 이벤트 그룹](../../relational-databases/triggers/ddl-event-groups.md)을 참조하세요.  
  
 또한 *event_group*은 CREATE EVENT NOTIFICATION 문이 완료될 때 해당 그룹에 속한 이벤트 유형을 **sys.events** 카탈로그 뷰에 추가하여 매크로의 역할도 합니다.  
  
 **'** *broker_service* **'**  
 이벤트 인스턴스 데이터를 받는 대상 서비스를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이벤트 알림에 대한 대상 서비스에 대해 하나 이상의 대화를 엽니다. 이 서비스는 메시지를 보내는 데 사용하는 동일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트 메시지 유형 및 계약을 인식해야 합니다.  
  
 이벤트 알림이 삭제될 때까지 대화는 열려 있습니다. 특정 오류로 인해 대화가 일찍 닫힐 수 있습니다. 일부 또는 전체 대화를 명시적으로 종료하면 대상 서비스가 더 이상 메시지를 받지 못할 수 있습니다.  
  
 { **‘** _broker\_instance\_specifier_ **’**  |  **‘current database’** }  
 *broker_service*가 확인되는 Service Broker 인스턴스를 지정합니다. **sys.databases** 카탈로그 뷰의 **service_broker_guid** 열을 쿼리하면 특정 Service Broker 값을 얻을 수 있습니다. 현재 데이터베이스의 Service Broker 인스턴스를 지정하려면 **'current database'** 를 사용합니다. **'current database'** 는 대/소문자를 구분하지 않는 문자열 리터럴입니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에는 이벤트 알림용 메시지 유형과 계약이 포함되어 있습니다. 따라서 다음과 같은 계약 이름을 지정하는 Service Broker가 이미 있으므로 Service Broker 시작 서비스를 생성하지 않아도 됩니다. `https://schemas.microsoft.com/SQL/Notifications/PostEventNotification`  
  
 이벤트 알림을 받는 대상 서비스는 이러한 기존 계약을 인식해야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 보안을 구성해야 합니다. 대화 보안은 전체 보안 모델에 따라 수동으로 구성해야 합니다. 자세한 내용은 [이벤트 알림에 대한 대화 보안 구성](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)을 참조하세요.  
  
 알림을 활성화하는 이벤트 트랜잭션이 롤백되면 이벤트 알림을 보내는 작업도 롤백됩니다. 트랜잭션이 트리거 내부에서 커밋 또는 롤백되는 경우 트리거에 정의된 동작에 대해서는 이벤트 알림이 발생하지 않습니다. 추적 이벤트는 트랜잭션에 의해 바운드되지 않으므로 추적 이벤트 기반 이벤트 알림은 해당 알림을 활성화하는 트랜잭션의 롤백 여부와 관계없이 전송됩니다.  
  
 이벤트 알림이 발생한 이후에 서버와 대상 서비스 간의 대화가 중단되면 오류가 보고되고 이벤트 알림은 삭제됩니다.  
  
 해당 알림을 최초로 시작한 이벤트 트랜잭션은 이벤트 알림 보내기 작업의 성공 또는 실패에 영향을 받지 않습니다.  
  
 이벤트 알림 보내기 실패는 모두 기록됩니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스(ON DATABASE)에 한정되는 이벤트 알림을 생성하려면 현재 데이터베이스에 대해 CREATE DATABASE DDL EVENT NOTIFICATION 권한이 필요합니다.  
  
 DDL 문에서 서버(ON SERVER)에 한정되는 이벤트 알림을 생성하려면 해당 서버에 대해 CREATE DDL EVENT NOTIFICATION 권한이 필요합니다.  
  
 추적 이벤트에서 이벤트 알림을 생성하려면 해당 서버에 대해 CREATE TRACE EVENT NOTIFICATION 권한이 필요합니다.  
  
 큐에 한정되는 이벤트 알림을 생성하려면 해당 큐에 대해 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
> [!NOTE]  
>  다음의 예 1과 예 2에서 `TO SERVICE 'NotifyService'` 절의 GUID('8140a771-3c4b-4479-8ac0-81008ab17984')는 예가 구성된 컴퓨터에만 해당됩니다. 예를 들어 이 GUID는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 GUID입니다.  
>   
>  이러한 예를 복사하고 실행하려면 이 GUID를 사용자의 컴퓨터 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 맞게 바꿔야 합니다. 위의 인수 섹션에서 설명한 것처럼 sys.databases 카탈로그 뷰의 service_broker_guid 열을 쿼리하여 **‘** _broker\_instance\_specifier_ **’** 를 얻을 수 있습니다.  
  
### <a name="a-creating-an-event-notification-that-is-server-scoped"></a>A. 서버에 한정되는 이벤트 알림 생성  
 다음 예에서는 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하여 대상 서비스를 설정하는 데 필요한 개체를 만듭니다. 대상 서비스는 이벤트 알림용 시작 서비스의 메시지 유형과 계약을 참조합니다. 그러면 `Object_Created`의 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 추적 이벤트가 발생할 때마다 알림을 보내는 대상 서비스에서 이벤트 알림이 생성됩니다.  
  
```sql  
--Create a queue to receive messages.  
CREATE QUEUE NotifyQueue ;  
GO  
--Create a service on the queue that references  
--the event notifications contract.  
CREATE SERVICE NotifyService  
ON QUEUE NotifyQueue  
([https://schemas.microsoft.com/SQL/Notifications/PostEventNotification]);  
GO  
--Create a route on the service to define the address   
--to which Service Broker sends messages for the service.  
CREATE ROUTE NotifyRoute  
WITH SERVICE_NAME = 'NotifyService',  
ADDRESS = 'LOCAL';  
GO  
--Create the event notification.  
CREATE EVENT NOTIFICATION log_ddl1   
ON SERVER   
FOR Object_Created   
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984' ;  
```  
  
### <a name="b-creating-an-event-notification-that-is-database-scoped"></a>B. 데이터베이스에 한정되는 이벤트 알림 생성  
 다음 예에서는 앞의 예와 같은 대상 서비스에서 이벤트 알림을 생성합니다. `ALTER_TABLE` 예제 데이터베이스에서 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 이벤트가 발생한 후 이벤트 알림이 발생합니다.  
  
```sql  
CREATE EVENT NOTIFICATION Notify_ALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
### <a name="c-getting-information-about-an-event-notification-that-is-server-scoped"></a>C. 서버에 한정되는 이벤트 알림에 대한 정보 얻기  
 다음 예에서는 서버 범위를 사용하여 생성한 이벤트 알림 `sys.server_event_notifications`에 대한 메타데이터에 대해 `log_ddl1` 카탈로그 뷰를 쿼리합니다.  
  
```  
SELECT * FROM sys.server_event_notifications  
WHERE name = 'log_ddl1';  
```  
  
### <a name="d-getting-information-about-an-event-notification-that-is-database-scoped"></a>D. 데이터베이스에 한정되는 이벤트 알림에 대한 정보 얻기  
 다음 예에서는 데이터베이스 범위를 사용하여 생성한 이벤트 알림 `sys.event_notifications`에 대한 메타데이터에 대해 `Notify_ALTER_T1` 카탈로그 뷰를 쿼리합니다.  
  
```sql  
SELECT * FROM sys.event_notifications  
WHERE name = 'Notify_ALTER_T1';  
```  
  
## <a name="see-also"></a>참고 항목  
 [이벤트 알림](../../relational-databases/service-broker/event-notifications.md)   
 [DROP EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-notification-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.event_notifications&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)   
 [sys.events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)   
 [sys.server_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-events-transact-sql.md)  
  
  
