---
title: "이벤트 알림 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 64
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 82d4f844c44f92232c8ac9bebd5841460f93051c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-event-notification-transact-sql"></a>CREATE EVENT NOTIFICATION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 또는 서버 이벤트에 대한 정보를 service broker 서비스로 보내는 개체를 만듭니다. 이벤트 알림은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 통해서만 생성됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 이벤트 알림의 이름입니다. 이벤트 알림 이름은 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md) 생성 되는 범위 내에서 고유 해야 하 고: 서버, 데이터베이스 또는 *object_name*합니다.  
  
 SERVER  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 인스턴스에 이벤트 알림 범위를 적용합니다. 지정한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에서 FOR 절에 지정한 이벤트가 발생할 때마다 알림이 발생합니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 DATABASE  
 현재 데이터베이스에 이벤트 알림의 범위를 적용합니다. 지정한 경우 현재 데이터베이스에서 FOR 절에 지정한 이벤트가 발생할 때마다 알림이 발생합니다.  
  
 QUEUE  
 현재 데이터베이스의 특정 큐에 알림의 범위를 적용합니다. FOR QUEUE_ACTIVATION이나 FOR BROKER_QUEUE_DISABLED도 지정한 경우에만 QUEUE를 지정할 수 있습니다.  
  
 *queue_name*  
 이벤트 알림이 적용되는 큐의 이름입니다. *queue_name* 만 지정할 수 있습니다 하는 경우 큐를 지정 합니다.  
  
 WITH FAN_IN  
 다음과 같은 모든 이벤트 알림에 대해 지정한 모든 서비스에 이벤트당 하나씩만 메시지를 보내도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 지시합니다.  
  
-   같은 이벤트에서 생성된 이벤트 알림  
  
-   같은 보안 주체(같은 SID로 식별됨)가 생성한 이벤트 알림  
  
-   동일한 서비스를 지정 하 고 *broker_instance_specifier*합니다.  
  
-   WITH FAN_IN을 지정하는 이벤트 알림  
  
 예를 들어 3개의 이벤트 알림이 생성됩니다. 모든 이벤트 알림에서 FOR ALTER_TABLE, WITH FAN_IN, 동일한 TO SERVICE 절을 지정하며 같은 SID로 생성됩니다. ALTER TABLE 문을 실행하면 이러한 3개 이벤트 알림에 의해 생성된 메시지가 하나로 병합됩니다. 따라서 대상 서비스는 하나의 이벤트 메시지만 받게 됩니다.  
  
 *event_type*  
 이벤트 알림을 실행하게 하는 이벤트 유형의 이름입니다. *event_type* 수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 이벤트 유형, SQL 추적 이벤트 유형 또는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 이벤트 유형입니다. 조건에 맞는 목록에 대 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 이벤트 유형을 참조 [DDL 이벤트](../../relational-databases/triggers/ddl-events.md)합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 이벤트 유형은 QUEUE_ACTIVATION 및 BROKER_QUEUE_DISABLED입니다. 자세한 내용은 [Event Notifications](../../relational-databases/service-broker/event-notifications.md)을 참조하세요.  
  
 *event_group*  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 SQL 추적 이벤트 유형의 미리 정의된 그룹 이름입니다. 이벤트 그룹에 속해 있는 이벤트를 실행한 후 이벤트 알림이 발생할 수 있습니다. DDL 이벤트 그룹의 목록에 대 한는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이벤트를 처리 하 고을 정의할 수 있습니다, 범위 참조 [DDL 이벤트 그룹](../../relational-databases/triggers/ddl-event-groups.md)합니다.  
  
 *event_group* 도 매크로 역할도, CREATE EVENT NOTIFICATION 문이 완료 될 때 이벤트 유형을 추가 하 여 적용 하는 **sys.events** 카탈로그 뷰에 있습니다.  
  
 **'** *broker_service* **'**  
 이벤트 인스턴스 데이터를 받는 대상 서비스를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이벤트 알림에 대한 대상 서비스에 대해 하나 이상의 대화를 엽니다. 이 서비스는 메시지를 보내는 데 사용하는 동일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트 메시지 유형 및 계약을 인식해야 합니다.  
  
 이벤트 알림이 삭제될 때까지 대화는 열려 있습니다. 특정 오류로 인해 대화가 일찍 닫힐 수 있습니다. 일부 또는 전체 대화를 명시적으로 종료하면 대상 서비스가 더 이상 메시지를 받지 못할 수 있습니다.  
  
 { **'***broker_instance_specifier***'** | **'current database'** }  
 지정 된 service broker 인스턴스 *broker_service* 확인 됩니다. 쿼리하여 특정 service broker에 대 한 값을 획득할 수 있습니다는 **service_broker_guid** 의 열은 **sys.databases** 카탈로그 뷰. 사용 하 여 **'current database'** 현재 데이터베이스에서 service broker 인스턴스를 지정할 수 있습니다. **'current database'** 는 대/소문자 구분 문자열 리터럴.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에는 이벤트 알림용 메시지 유형과 계약이 포함되어 있습니다. 따라서 시작 서비스를 이미 존재 하는 만들 수 없는 Service Broker에는 다음과 같은 계약 이름을 지정 합니다.`http://schemas.microsoft.com/SQL/Notifications/PostEventNotification`  
  
 이벤트 알림을 받는 대상 서비스는 이러한 기존 계약을 인식해야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 보안을 구성해야 합니다. 대화 보안은 전체 보안 모델에 따라 수동으로 구성해야 합니다. 자세한 내용은 참조 [이벤트 알림에 대 한 대화 보안 구성](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)합니다.  
  
 알림을 활성화하는 이벤트 트랜잭션이 롤백되면 이벤트 알림을 보내는 작업도 롤백됩니다. 트랜잭션이 트리거 내부에서 커밋 또는 롤백되는 경우 트리거에 정의된 동작에 대해서는 이벤트 알림이 발생하지 않습니다. 추적 이벤트는 트랜잭션에 의해 바운드되지 않으므로 추적 이벤트 기반 이벤트 알림은 해당 알림을 활성화하는 트랜잭션의 롤백 여부와 관계없이 전송됩니다.  
  
 이벤트 알림이 발생한 이후에 서버와 대상 서비스 간의 대화가 중단되면 오류가 보고되고 이벤트 알림은 삭제됩니다.  
  
 해당 알림을 최초로 시작한 이벤트 트랜잭션은 이벤트 알림 보내기 작업의 성공 또는 실패에 영향을 받지 않습니다.  
  
 이벤트 알림 보내기 실패는 모두 기록됩니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스(ON DATABASE)에 한정되는 이벤트 알림을 생성하려면 현재 데이터베이스에 대해 CREATE DATABASE DDL EVENT NOTIFICATION 권한이 필요합니다.  
  
 DDL 문에서 서버(ON SERVER)에 한정되는 이벤트 알림을 생성하려면 해당 서버에 대해 CREATE DDL EVENT NOTIFICATION 권한이 필요합니다.  
  
 추적 이벤트에서 이벤트 알림을 생성하려면 해당 서버에 대해 CREATE TRACE EVENT NOTIFICATION 권한이 필요합니다.  
  
 큐에 한정되는 이벤트 알림을 생성하려면 해당 큐에 대해 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
> [!NOTE]  
>  다음의 예 1과 예 2에서 `TO SERVICE 'NotifyService'` 절의 GUID('8140a771-3c4b-4479-8ac0-81008ab17984')는 예가 구성된 컴퓨터에만 해당됩니다. 예를 들어 이 GUID는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 GUID입니다.  
>   
>  이러한 예를 복사하고 실행하려면 이 GUID를 사용자의 컴퓨터 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 맞게 바꿔야 합니다. 위의 인수 섹션에서 설명 했 듯이 얻을 수 있습니다는 **'***broker_instance_specifier***'** service_broker_guid 열을는 sys.databases 쿼리하여 카탈로그 뷰입니다.  
  
### <a name="a-creating-an-event-notification-that-is-server-scoped"></a>1. 서버에 한정되는 이벤트 알림 생성  
 다음 예에서는 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하여 대상 서비스를 설정하는 데 필요한 개체를 만듭니다. 대상 서비스는 이벤트 알림용 시작 서비스의 메시지 유형과 계약을 참조합니다. 그러면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에서 `Object_Created` 추적 이벤트가 발생할 때마다 알림을 보내는 대상 서비스에서 이벤트 알림이 생성됩니다.  
  
```tsql  
--Create a queue to receive messages.  
CREATE QUEUE NotifyQueue ;  
GO  
--Create a service on the queue that references  
--the event notifications contract.  
CREATE SERVICE NotifyService  
ON QUEUE NotifyQueue  
([http://schemas.microsoft.com/SQL/Notifications/PostEventNotification]);  
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
  
### <a name="b-creating-an-event-notification-that-is-database-scoped"></a>2. 데이터베이스에 한정되는 이벤트 알림 생성  
 다음 예에서는 앞의 예와 같은 대상 서비스에서 이벤트 알림을 생성합니다. [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 예제 데이터베이스에서 `ALTER_TABLE` 이벤트가 발생한 후 이벤트 알림이 발생합니다.  
  
```tsql  
CREATE EVENT NOTIFICATION Notify_ALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
### <a name="c-getting-information-about-an-event-notification-that-is-server-scoped"></a>3. 서버에 한정되는 이벤트 알림에 대한 정보 얻기  
 다음 예에서는 서버 범위를 사용하여 생성한 이벤트 알림 `sys.server_event_notifications`에 대한 메타데이터에 대해 `log_ddl1` 카탈로그 뷰를 쿼리합니다.  
  
```  
SELECT * FROM sys.server_event_notifications  
WHERE name = 'log_ddl1';  
```  
  
### <a name="d-getting-information-about-an-event-notification-that-is-database-scoped"></a>4. 데이터베이스에 한정되는 이벤트 알림에 대한 정보 얻기  
 다음 예에서는 데이터베이스 범위를 사용하여 생성한 이벤트 알림 `sys.event_notifications`에 대한 메타데이터에 대해 `Notify_ALTER_T1` 카탈로그 뷰를 쿼리합니다.  
  
```tsql  
SELECT * FROM sys.event_notifications  
WHERE name = 'Notify_ALTER_T1';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [이벤트 알림](../../relational-databases/service-broker/event-notifications.md)   
 [DROP EVENT notification&#40; Transact SQL &#41;](../../t-sql/statements/drop-event-notification-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.event_notifications&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [sys.server_event_notifications&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)   
 [sys.events &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)   
 [sys.server_events &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-events-transact-sql.md)  
  
  

