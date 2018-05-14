---
title: 이벤트 알림 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: service-broker
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications, about
- events [SQL Server], notifications
ms.assetid: 4da73ca1-6c06-4e96-8ab8-2ecba30b6c86
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37602cb45dabc2c00d47dd3c7be28ed6e8fe63e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="event-notifications"></a>이벤트 알림
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이벤트 알림은 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스에 이벤트 정보를 보냅니다. 이벤트 알림은 다양한 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL(데이터 언어 정의) 문과 SQL 추적 이벤트에 대한 응답으로 실행되어 이러한 이벤트에 대한 정보를 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스로 보냅니다.  
  
 이벤트 알림을 사용하여 다음을 수행할 수 있습니다.  
  
-   데이터베이스에서 발생하는 변경 내용이나 작업 기록 및 검토  
  
-   동기 방식이 아닌 비동기 방식으로 이벤트에 응답하여 동작 수행  
  
 이벤트 알림은 DDL 트리거 및 SQL 추적에 대한 대체 프로그래밍 기능을 제공합니다.  
  
## <a name="event-notifications-benefits"></a>이벤트 알림의 이점  
 이벤트 알림은 트랜잭션 범위 밖에서 비동기적으로 실행됩니다. 따라서 DDL 트리거와 달리 이벤트 알림은 데이터베이스 응용 프로그램 내에서 사용되어 최근 트랜잭션에서 정의한 리소스를 사용하지 않고 이벤트에 응답할 수 있습니다.  
  
 SQL 추적과 달리 이벤트 알림을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 SQL 추적 이벤트에 응답하는 동작을 수행할 수 있습니다.  
  
 이벤트 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 함께 실행되어 진행률을 추적하고 의사 결정을 내리는 응용 프로그램에 의해 사용될 수 있습니다. 예를 들어 다음 이벤트 알림은 `ALTER TABLE` 예제 데이터베이스에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 문이 실행될 때마다 특정 서비스에 알림을 보냅니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE '//Adventure-Works.com/ArchiveService' ,  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
## <a name="event-notifications-concepts"></a>이벤트 알림 개념  
 이벤트 알림이 생성되면 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 인스턴스와 지정한 대상 서비스 간에 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대화가 열립니다. 대화는 일반적으로 이벤트 알림이 서버 인스턴스의 개체로 존재하는 한 열린 상태로 유지됩니다. 몇몇 오류가 발생하는 경우에는 이벤트 알림을 삭제하기 전에 대화가 종료될 수 있습니다. 이러한 대화는 이벤트 알림 간에 공유되지 않습니다. 각 이벤트 알림에는 자체적인 배타 대화가 있습니다. 대화를 명시적으로 종료하면 대상 서비스가 더 이상의 메시지를 받지 못하게 되며 이벤트 알림이 다음에 실행될 때 해당 대화가 다시 열리지 않습니다.  
  
 이벤트 정보는 이벤트 발생 시기, 영향을 받는 데이터베이스 개체, 관련된 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 일괄 처리 문 및 기타 정보를 제공하는 **xml** 유형의 변수로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서비스에 전달됩니다. 이벤트 알림이 만드는 XML 스키마에 대한 자세한 내용은 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)를 참조하세요.  
  
### <a name="event-notifications-vs-triggers"></a>이벤트 알림과 트리거  
 다음 표에서는 트리거와 이벤트 알림을 비교 및 대조합니다.  
  
|트리거|이벤트 알림|  
|--------------|-------------------------|  
|DML 트리거는 DML(데이터 조작 언어) 이벤트에 응답하고 DDL 트리거는 DDL(데이터 정의 언어) 이벤트에 응답합니다.|이벤트 알림은 DDL 이벤트와 SQL 추적 이벤트의 하위 집합에 응답합니다.|  
|트리거는 Transact-SQL 또는 CLR(공용 언어 런타임) 관리 코드를 실행할 수 있습니다.|이벤트 알림은 코드를 실행하지 않는 대신 Service Broker 서비스에 **xml** 메시지를 보냅니다.|  
|트리거는 트리거를 시작하는 트랜잭션 범위 내에서 동기적으로 처리됩니다.|이벤트 알림은 비동기적으로 처리될 수 있으며 해당 이벤트 알림을 시작하는 트랜잭션 범위 내에서 실행되지 않습니다.|  
|트리거의 소비자는 트리거를 실행하는 이벤트에 밀접하게 결합됩니다.|이벤트 알림의 소비자는 이벤트 알림을 시작하는 이벤트와 분리됩니다.|  
|트리거는 로컬 서버에서 처리해야 합니다.|이벤트 알림은 원격 서버에서 처리할 수 있습니다.|  
|트리거는 롤백할 수 있습니다.|이벤트 알림은 롤백할 수 없습니다.|  
|DML 트리거 이름은 스키마 범위입니다. DDL 트리거 이름은 데이터베이스 범위이거나 서버 범위입니다.|이벤트 알림 이름은 서버 또는 데이터베이스 범위입니다. QUEUE_ACTIVATION 이벤트에 대한 이벤트 알림의 범위는 특정 큐로 한정됩니다.|  
|DML 트리거는 트리거가 적용되는 테이블과 동일한 소유자에 의해 소유됩니다.|큐에 대한 이벤트 알림의 소유자는 해당 이벤트 알림이 적용되는 개체의 소유자와 다를 수 있습니다.|  
|트리거는 EXECUTE AS 절을 지원합니다.|이벤트 알림은 EXECUTE AS 절을 지원하지 않습니다.|  
|DDL 트리거 이벤트 정보는 **xml** 데이터 형식을 반환하는 EVENTDATA 함수를 사용하여 캡처할 수 있습니다.|이벤트 알림은 Service Broker 서비스에 **xml** 이벤트 정보를 보냅니다. 해당 정보는 EVENTDATA 함수와 같은 스키마 형식으로 지정됩니다.|  
|트리거의 메타데이터는 **sys.triggers** 및 **sys.server_triggers** 카탈로그 뷰에 포함됩니다.|이벤트 알림의 메타데이터는 **sys.event_notifications** 및 **sys.server_event_notifications** 카탈로그 뷰에 포함됩니다.|  
  
### <a name="event-notifications-vs-sql-trace"></a>이벤트 알림과 SQL 추적  
 다음 표에서는 서버 이벤트 모니터링을 위한 이벤트 알림과 SQL 추적을 사용할 때의 차이점을 비교합니다.  
  
|SQL 추적|이벤트 알림|  
|---------------|-------------------------|  
|SQL 추적은 트랜잭션과 관련된 성능 오버헤드를 생성하지 않습니다. 데이터 패키징이 효율적입니다.|XML 형식 이벤트 데이터 작성 및 이벤트 알림 전송과 관련된 성능 오버헤드가 있습니다.|  
|SQL 추적은 모든 추적 이벤트 클래스를 모니터링할 수 있습니다.|이벤트 알림은 추적 이벤트 클래스의 하위 집합과 모든 DDL(데이터 정의 언어) 이벤트를 모니터링할 수 있습니다.|  
|추적 이벤트를 생성할 데이터 열을 사용자 지정할 수 있습니다.|이벤트 알림에서 반환되는 XML 형식 이벤트 데이터의 스키마가 고정되어 있습니다.|  
|DDL로 생성되는 추적 이벤트는 DDL 문이 롤백되는지 여부와 관계없이 항상 생성됩니다.|해당 DDL 문의 이벤트가 롤백되면 이벤트 알림이 실행되지 않습니다.|  
|추적 파일 또는 추적 테이블 채우기 및 관리 작업을 통해 추적 이벤트 데이터의 중간 흐름을 관리합니다.|이벤트 알림 데이터의 중간 관리는 Service Broker 큐를 통해 자동으로 수행됩니다.|  
|서버를 다시 시작할 때마다 추적을 다시 시작해야 합니다.|이벤트 알림을 등록하면 여러 서버 주기에서 이벤트 알림이 유지되고 트랜잭션됩니다.|  
|추적이 시작된 후에는 추적 실행을 제어할 수 없습니다. 중지 시간과 필터 시간을 사용하여 추적 시작 시기를 지정할 수 있습니다. 해당 추적 파일을 폴링하여 추적에 액세스할 수 있습니다.|이벤트 알림에서 생성되는 메시지를 받는 큐에 대해 WAITFOR 문을 사용하여 이벤트 알림을 제어할 수 있습니다. 큐를 폴링하여 이벤트 알림에 액세스할 수 있습니다.|  
|추적을 만드는 데 필요한 최소 사용 권한은 ALTER TRACE입니다. 해당 컴퓨터에 추적 파일을 만드는 데도 사용 권한이 필요합니다.|생성되는 이벤트 알림 유형에 따라 최소 사용 권한이 다릅니다. 해당 큐에 RECEIVE 사용 권한도 필요합니다.|  
|원격으로 추적을 받을 수 있습니다.|원격으로 이벤트 알림을 받을 수 있습니다.|  
|시스템 저장 프로시저를 사용하여 추적 이벤트를 구현합니다.|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssSB](../../includes/sssb-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] 문 조합을 사용하여 이벤트 알림을 구현합니다.|  
|해당 추적 테이블 쿼리, 추적 파일 구문 분석 또는 SMO( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 개체) TraceReader 클래스 사용을 통해 추적 이벤트 데이터에 프로그래밍 방식으로 액세스할 수 있습니다.|XML 형식 이벤트 데이터에 대한 XQuery 실행이나 SMO Event 클래스 사용을 통해 이벤트 데이터에 프로그래밍 방식으로 액세스할 수 있습니다.|  
  
## <a name="event-notification-tasks"></a>이벤트 알림 태스크  
  
|태스크|항목|  
|----------|-----------|  
|이벤트 알림을 만들고 구현하는 방법에 대해 설명합니다.|[이벤트 알림 구현](../../relational-databases/service-broker/implement-event-notifications.md)|  
|원격 서버의 Service Broker로 메시지를 보내는 이벤트 알림에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 보안을 구성하는 방법에 대해 설명합니다.|[이벤트 알림에 대한 대화 보안 구성](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)|  
|이벤트 알림에 대한 정보를 반환하는 방법에 대해 설명합니다.|[이벤트 알림에 대한 정보 가져오기](../../relational-databases/service-broker/get-information-about-event-notifications.md)|  
  
## <a name="see-also"></a>참고 항목  
 [DDL 트리거](../../relational-databases/triggers/ddl-triggers.md)   
 [DML 트리거](../../relational-databases/triggers/dml-triggers.md)   
 [SQL 추적](../../relational-databases/sql-trace/sql-trace.md)  
  
  
