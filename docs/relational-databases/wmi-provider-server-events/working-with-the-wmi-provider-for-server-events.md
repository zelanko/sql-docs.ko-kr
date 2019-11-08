---
title: 서버 이벤트용 WMI 공급자 작업
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- event notifications [WMI]
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- Service Broker [WMI]
- WMI Provider for Server Events, connection strings
- WMI Provider for Server Events, Service Broker
- notifications [WMI]
- WMI Provider for Server Events, security
ms.assetid: cd974b3b-2309-4a20-b9be-7cfc93fc4389
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9134b2964c27129b5ccc9d6a5992dda7c638dc7a
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658127"
---
# <a name="working-with-the-wmi-provider-for-server-events"></a>서버 이벤트용 WMI 공급자 작업
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 서버 이벤트용 WMI 공급자를 사용하여 프로그래밍하기 전에 고려해야 할 사항에 대한 지침을 제공합니다.  
  
## <a name="enabling-service-broker"></a>Service Broker 사용  
 서버 이벤트용 WMI 공급자는 이벤트에 대한 WQL 쿼리를 대상 데이터베이스의 이벤트 알림으로 변환하는 방식으로 작동합니다. 이벤트 알림의 작동 방식에 대해 알고 있으면 공급자를 프로그래밍할 때 유용합니다. 자세한 내용은 [서버 이벤트용 WMI 공급자 개념](https://technet.microsoft.com/library/ms180560.aspx)을 참조하십시오.  
  
 특히 WMI 공급자가 만드는 이벤트 알림은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 서버 이벤트에 대한 메시지를 보내기 때문에 이 서비스는 이벤트가 생성되는 경우에는 반드시 사용할 수 있어야 합니다. 프로그램에서 서버 인스턴스의 이벤트를 쿼리하는 경우 해당 인스턴스의 msdb에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용할 수 있어야 합니다. 그 이유는 이 위치가 공급자가 만든 대상 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스(이름: SQL/Notifications/ProcessWMIEventProviderNotification/v1.0)의 위치이기 때문입니다. 프로그램에서 데이터베이스 또는 특정 데이터베이스 개체의 이벤트를 쿼리하는 경우에는 대상 데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 를 사용할 수 있어야 합니다. 애플리케이션이 배포된 후 해당하는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 를 사용할 수 있게 설정하지 않으면 기본 이벤트 알림을 통해 생성되는 모든 이벤트가 이벤트 알림에 사용되는 서비스의 큐에 전송되지만 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 를 사용할 수 있게 설정할 때까지는 WMI 관리 애플리케이션에 반환되지 않습니다.  
  
 다음 쿼리에서는 서버 인스턴스에서 사용할 수 있는 Service Broker와 Broker 인스턴스 GUID를 확인합니다.  
  
```  
SELECT name, is_broker_enabled, service_broker_guid FROM sys.databases;  
```  
  
 msdb의 Service Broker GUID는 공급자의 대상 서비스에 대한 위치이기 때문에 특별한 관심 대상입니다.  
  
 데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 를 사용하려면 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문의 ENABLE_BROKER SET 옵션을 사용합니다.  
  
## <a name="specifying-a-connection-string"></a>연결 문자열 지정  
 애플리케이션에서는 공급자가 정의한 WMI 네임스페이스에 연결하여 서버 이벤트용 WMI 공급자를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에 전달합니다. Windows WMI 서비스는 이 네임스페이스를 공급자 DLL인 Sqlwep.dll에 매핑하여 메모리에 로드합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 각 인스턴스에는 고유한 WMI 네임 스페이스가 있으며 기본값은 \\\\입니다.\\*root*\Microsoft\SqlServer\ServerEvents\\*instance_name*. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]기본 설치에서 *instance_name* 기본값은 MSSQLSERVER입니다.  
  
## <a name="permissions-and-server-authentication"></a>권한과 서버 인증  
 서버 이벤트용 WMI 공급자에 액세스하려면 WMI 관리 애플리케이션이 시작된 클라이언트는 애플리케이션의 연결 문자열에 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 Windows 인증 로그인 또는 그룹과 일치해야 합니다.  
  
## <a name="permissions-and-event-notification-scope"></a>권한과 이벤트 알림 범위  
 서버 이벤트용 WMI 공급자는 WQL 쿼리를 대상 데이터베이스의 이벤트 알림으로 변환합니다. 따라서 호출 애플리케이션은 공급자에 액세스하는 데 필요한 최소 권한뿐만 아니라 데이터베이스에 대한 올바른 권한을 가지고 있어야 필요한 이벤트 알림을 생성할 수 있습니다. 권한은 다음과 같습니다.  
  
-   범위가 데이터베이스에 한정되는 이벤트 알림을 생성하려면 최소한 현재 데이터베이스에 대해 CREATE DATABASE DDL EVENT NOTIFICATION 권한이 필요합니다.  
  
-   범위가 서버에 한정되는 DDL 문에 대한 이벤트 알림을 생성하려면 최소한 해당 서버에 대해 CREATE DDL EVENT NOTIFICATION 권한이 필요합니다.  
  
-   추적 이벤트에 대한 이벤트 알림을 생성하려면 최소한 해당 서버에 대해 CREATE TRACE EVENT NOTIFICATION 권한이 필요합니다.  
  
-   범위가 큐에 한정되는 이벤트 알림을 생성하려면 최소한 해당 큐에 대해 ALTER 권한이 필요합니다.  
  
 WQL 쿼리의 범위에 대한 자세한 내용은 [서버 이벤트용 WMI 공급자에 WQL 사용](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)을 참조하십시오.  
  
 예를 들어 다음과 같은 WQL 쿼리가 포함된 WMI 공급자 애플리케이션을 생각해 볼 수 있습니다.  
  
```  
SELECT * FROM ALTER_TABLE  
WHERE DatabaseName = "AdventureWorks2012"   
    AND SchemaName = "Person"  
    AND ObjectName = "Person"  
    AND ObjectType = "TABLE";  
```  
  
 WMI 공급자는 이 쿼리를 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 생성되는 이벤트 알림으로 변환합니다. 이는 호출자가 이러한 이벤트 알림을 생성하는 데 필요한 권한, 즉 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 CREATE DATABASE DDL EVENT NOTIFICATION 권한을 가지고 있어야 함을 의미합니다.  
  
 범위가 서버 수준에 한정되는 이벤트 알림을 WQL 쿼리에서 지정할 경우(예: SELECT * FROM ALTER_TABLE 쿼리 실행), 호출 애플리케이션은 서버 수준의 REATE DDL EVENT NOTIFICATION 권한을 가지고 있어야 합니다. 범위가 서버에 한정되는 이벤트 알림은 master 데이터베이스에 저장됩니다. 이러한 알림의 메타데이터는 [sys.server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md) 카탈로그 뷰를 사용하여 볼 수 있습니다.  
  
> [!NOTE]  
>  WMI 공급자가 생성하는 이벤트 알림의 범위(서버, 데이터베이스 또는 개체)는 궁극적으로 WMI 공급자에서 사용하는 권한 확인 프로세스의 결과에 따라 달라집니다. 이는 공급자를 호출하는 사용자의 권한 집합 및 쿼리 대상 데이터베이스에 대한 확인 결과의 영향을 받습니다.  
>   
>  위의 예에서 공급자는 먼저 범위가 데이터베이스(`ON DATABASE`)에 한정되는 이벤트 알림을 생성하려고 시도합니다. 공급자의 확인 결과 데이터베이스가 존재하고 호출자가 이벤트 알림을 생성하는 데 필요한 권한을 가지고 있으면 등록이 성공적으로 이루어집니다. 제대로 등록되지 않으면 공급자는 서버(`ON SERVER`)에서 이벤트 알림을 생성하려고 시도합니다. 이 시도가 성공적으로 이루어지면 서버에서 발생하는 모든 `ALTER_TABLE` 이벤트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 WMI 서비스 프로세스로 전송됩니다. 그러나 공급자는 `AdventureWorks` 데이터베이스에 적용되지 않는 모든 이벤트를 필터링합니다. 이 프로세스를 사용하면 이벤트의 범위에 필요한 것보다 네트워크 트래픽이 증가할 수 있지만 필요에 따라 데이터베이스가 생성되기 전에 데이터베이스에 WQL 쿼리를 등록한 다음 데이터베이스 생성 후 DDL 작업이 시작되기 전에 이벤트 데이터를 받을 수 있습니다.  
  
## <a name="permissions-and-message-verification"></a>권한과 메시지 확인  
 다음 두 가지 조건 모두에 해당하면 WMI 공급자가 이벤트 알림에 대한 메시지를 보내지 않습니다.  
  
-   WMI 공급자를 통해 이벤트 알림을 만든 사용자가 데이터베이스에 더 이상 없거나, 유사한 이벤트 알림을 생성하는 데 필요한 권한을 더 이상 가지고 있지 않은 경우  
  
-   다음과 같은 이벤트에 대해 이벤트 알림이 생성된 경우  
  
    -   DROP_LOGIN  
  
    -   ALTER_LOGIN  
  
    -   DROP_USER  
  
    -   ALTER_USER  
  
    -   ADD_ROLE_MEMBER  
  
    -   DROP_ROLE_MEMBER  
  
    -   ADD_SERVER_ROLE_MEMBER  
  
    -   DROP_SERVER_ROLE_MEMBER  
  
    -   DENY 또는 REVOKE(ALTER DATABASE, ALTER ANY DATABASE EVENT NOTIFICATION, CREATE DATABASE DDL EVENT NOTIFICATION, CONTROL SERVER, ALTER ANY EVENT NOTIFICATION, CREATE DDL EVENT NOTIFICATION 또는 CREATE TRACE EVENT NOTIFICATION 권한에만 적용됨)  
  
## <a name="working-with-event-data-on-the-client-side"></a>클라이언트 쪽에서의 이벤트 데이터 작업  
 서버 이벤트 용 WMI 공급자가 대상 데이터베이스에 필요한 이벤트 알림을 생성 하면 이벤트 알림이 **SQL/notification/ProcessWMIEventProviderNotification/** v1.0 이라는 msdb의 대상 서비스에 이벤트 데이터를 보냅니다. . 대상 서비스는 이름이 **WMIEventProviderNotificationQueue** 인 **msdb**큐에 이벤트를 추가합니다. 서비스와 큐는 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 처음 연결할 때 공급자에 의해 동적으로 만들어집니다. 그런 다음 공급자는이 큐에서 XML 이벤트 데이터를 읽고 MOF (managed object format)로 변환한 후 클라이언트 응용 프로그램에 반환 합니다. MOF 데이터는 WQL 쿼리에서 CIM(Common Information Model) 클래스 정의로 요청되는 이벤트의 속성으로 구성되며 각 속성에는 해당되는 CIM 형식이 있습니다. 예를 들어 `SPID` 속성은 CIM 형식 **Sint32**으로 반환 됩니다. 각 속성의 CIM 형식은 [서버 이벤트용 WMI 공급자 클래스 및 속성](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md)의 각 이벤트 클래스 아래에 나열되어 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [서버 이벤트용 WMI 공급자 개념](https://technet.microsoft.com/library/ms180560.aspx)  
  
  
