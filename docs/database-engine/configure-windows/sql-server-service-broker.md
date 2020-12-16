---
title: SQL Server Service Broker | Microsoft Docs
description: Service Broker에 대해 알아봅니다. Service Broker가 SQL Server 데이터베이스 엔진 및 Azure SQL Managed Instance의 메시징에 대한 기본 지원을 어떻게 제공하는지 알아봅니다.
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.SSBMSGTYPEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBCONTRACTPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBQUEUEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBREMSVCBINDPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBROUTEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBPRIORITYPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBSERVICEPROPERTIES.GENERAL.F1
helpviewer_keywords:
- Broker See Service Broker
- SQL Server Service Broker
- Service Broker
ms.assetid: 8b8b3b57-fd46-44de-9a4e-e3a8e3999c1e
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017
ms.openlocfilehash: cf37305f773f4b417ed3cac1bc5a31ad8d910505
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465704"
---
# <a name="service-broker"></a>Service Broker
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 및 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance-index)의 메시징 및 큐에 대한 기본 지원을 제공합니다. 개발자는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성 요소를 사용하여 서로 다른 데이터베이스 간에 통신하는 복잡한 애플리케이션을 쉽게 만들고, 안정적인 분산형 애플리케이션을 빌드할 수 있습니다.  
  
## <a name="when-to-use-service-broker"></a>Service Broker를 사용하는 경우

 Service Broker 구성 요소를 사용하여 기본 데이터베이스 내 비동기 메시지 처리 기능을 구현합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 를 사용하는 애플리케이션 개발자는 복잡한 통신 및 메시징 내부 사항을 프로그래밍하지 않고도 데이터 작업을 여러 데이터베이스에 분산시킬 수 있습니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 대화 컨텍스트에서 통신 경로를 처리하므로 Service Broker를 통해 개발 및 테스트 작업이 줄어들 뿐만 아니라 성능이 향상됩니다. 예를 들어, 웹 사이트를 지원하는 프런트 엔드 데이터베이스는 정보를 기록하고 프로세스를 많이 사용하는 태스크를 백 엔드 데이터베이스의 큐로 보낼 수 있습니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 는 모든 태스크가 트랜잭션 컨텍스트에서 관리되도록 하여 안정성과 기술 일관성을 유지합니다.  
  
## <a name="overview"></a>개요

  Service Broker는 기본 데이터베이스 내 서비스 지향 애플리케이션을 만들 수 있는 메시지 배달 프레임워크입니다. 테이블에서 지속적으로 데이터를 읽고 쿼리 수명 주기 중에 처리하는 클래식 쿼리 처리 기능과 달리, 서비스 지향 애플리케이션에는 메시지를 교환하는 데이터베이스 서비스가 있습니다. 모든 서비스에는 메시지가 처리될 때까지 배치되는 큐가 있습니다.
  
![Service Broker](media/service-broker.png)
  
  Transact-SQL `RECEIVE` 명령을 사용하거나 메시지가 큐에 도달할 때마다 호출되는 활성화 프로시저를 통해 큐의 메시지를 가져올 수 있습니다.
  
### <a name="creating-services"></a>서비스 만들기
 
  데이터베이스 서비스는 [CREATE SERVICE](../../t-sql/statements/create-service-transact-sql.md) Transact SQL 문으로 만듭니다. 서비스는 [CREATE QUEUE](../../t-sql/statements/create-queue-transact-sql.md) 문을 사용하여 만든 메시지 큐에 연결할 수 있습니다.
  
```sql
CREATE QUEUE dbo.ExpenseQueue;
GO
CREATE SERVICE ExpensesService
    ON QUEUE dbo.ExpenseQueue; 
```

### <a name="sending-messages"></a>메시지 보내기
  
  메시지는 [SEND](../../t-sql/statements/send-transact-sql.md) Transact SQL 문을 사용한 서비스 간의 대화를 통해 보내집니다. 대화는 `BEGIN DIALOG` Transact SQL 문을 통해 서비스 간에 수립된 통신 채널입니다. 
  
```sql
DECLARE @dialog_handle UNIQUEIDENTIFIER;

BEGIN DIALOG @dialog_handle  
FROM SERVICE ExpensesClient  
TO SERVICE 'ExpensesService';  
  
SEND ON CONVERSATION @dialog_handle (@Message) ;  
```
   메시지는 `ExpenssesService`에 전송되고 `dbo.ExpenseQueue`에 배치됩니다. 이 큐에 연결된 활성화 프로시저가 없으므로 메시지는 누군가 읽을 때까지 큐에 남아 있습니다.

### <a name="processing-messages"></a>메시지 처리

   큐에 배치된 메시지는 표준 `SELECT` 쿼리를 사용하여 선택할 수 있습니다. `SELECT` 문은 큐를 수정하거나 메시지를 제거하지 않습니다. 큐에서 메시지를 읽고 끌어오려면 [RECEIVE](../../t-sql/statements/receive-transact-sql.md) Transact-SQL 문을 사용합니다.

```sql
RECEIVE conversation_handle, message_type_name, message_body  
FROM ExpenseQueue; 
```

  큐에서 모든 메시지를 처리한 후에는 [END CONVERSATION](../../t-sql/statements/end-conversation-transact-sql.md) Transact SQL 문을 사용하여 대화를 종료해야 합니다.

## <a name="where-is-the-documentation-for-service-broker"></a>Service Broker 설명서의 위치  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 에 대한 참조 설명서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설명서에 포함되어 있습니다. 이 참조 설명서는 다음과 같은 섹션으로 구성됩니다.  
  
-   CREATE, ALTER 및 DROP 문에 대한 [DDL&#40;데이터 정의 언어&#41; 문&#40;Transact-SQL&#41;](../../t-sql/statements/statements.md)  
  
-   [Service Broker 문](../../t-sql/statements/statements.md)  
  
-   [Service Broker 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)  
  
-   [Service Broker 관련 동적 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
-   [ssbdiagnose 유틸리티&#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
 [개념과 개발 및 관리 태스크에 대한 자세한 내용은](/previous-versions/sql/sql-server-2008-r2/bb522893(v=sql.105)) 이전에 게시된 설명서 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 를 참조하십시오. 이 설명서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 의 변경 사항이 적기 때문에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]설명서에서 다시 작성되지 않았습니다.  
  
## <a name="whats-new-in-service-broker"></a>Service Broker의 새로운 기능  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 도입된 큰 변경 내용은 없습니다.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서의 변경 내용은 다음과 같습니다.  

### <a name="service-broker-and-azure-sql-managed-instance"></a>Service Broker 및 Azure SQL Managed Instance

- 인스턴스 간 Service Broker는 지원되지 않습니다. 
 - `sys.routes` - 필수 조건: sys.routes에서 주소를 선택합니다. 주소는 모든 경로에서 LOCAL이어야 합니다. [sys.routes](../../relational-databases/system-catalog-views/sys-routes-transact-sql.md)를 참조하세요.
 - `CREATE ROUTE` - `LOCAL` 이외의 `ADDRESS`가 포함된 `CREATE ROUTE`는 사용할 수 없습니다. [CREATE ROUTE](../../t-sql/statements/create-route-transact-sql.md)를 참조하세요.
 - `ALTER ROUTE`는 `LOCAL` 외에 `ADDRESS`와 함께 `ALTER ROUTE`를 사용할 수 없습니다. [ALTER ROUTE](../../t-sql/statements/alter-route-transact-sql.md)를 참조하세요.  
  
### <a name="messages-can-be-sent-to-multiple-target-services-multicast"></a>메시지를 여러 대상 서비스에 보낼 수 있음(멀티캐스트)  
 [SEND&#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md) 문의 구문은 여러 대화 핸들을 지원하여 멀티캐스트를 설정하기 위해 확장되었습니다.  
  
### <a name="queues-expose-the-message-enqueued-time"></a>메시지가 큐에 유지된 시간이 큐에서 노출됨  
 메시지가 큐에 유지된 시간을 보여 주는 **message_enqueue_time** 이라는 새 열이 큐에 있습니다.  
  
### <a name="poison-message-handling-can-be-disabled"></a>포이즌 메시지 처리를 해제할 수 있음  
 [CREATE QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md) 및 [ALTER QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md) 문은 이제 `POISON_MESSAGE_HANDLING (STATUS = ON | OFF)` 절을 추가하여 포이즌 메시지 처리를 설정하거나 해제할 수 있습니다. 카탈로그 뷰 **sys.service_queues** 에는 이제 포이즌 메시지가 설정되었는지, 아니면 해제되었는지를 나타내는 **is_poison_message_handling_enabled** 열이 있습니다.  
  
### <a name="always-on-support-in-service-broker"></a>Service Broker의 Always On 지원  
 자세한 내용은 [Always On 가용성 그룹이 포함된 Service Broker(SQL Server)](../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
  
## <a name="next-steps"></a>다음 단계

가장 일반적으로 사용되는 Service Broker는 [이벤트 알림](../../relational-databases/service-broker/event-notifications.md)에 대한 것입니다. [이벤트 알림을 구현](../../relational-databases/service-broker/implement-event-notifications.md)하거나 [대화 상자 보안을 구성](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)하거나 [추가 정보를 가져오는](../../relational-databases/service-broker/get-information-about-event-notifications.md) 방법을 알아봅니다.