---
title: CREATE ROUTE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_ROUTE_TSQL
- ROUTE
- CREATE ROUTE
- ROUTE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lifetimes [Service Broker]
- routes [Service Broker], creating
- forwarding brokers [SQL Server]
- service names [Service Broker]
- database mirroring [SQL Server], routing
- expired routes [SQL Server]
- activating routes
- CREATE ROUTE statement
ms.assetid: 7e695364-1a98-4cfd-8ebd-137ac5a425b3
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b70035a1fc54d4b59978a3256b2ed3040ba4e8f9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68006512"
---
# <a name="create-route-transact-sql"></a>CREATE ROUTE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  현재 데이터베이스에 대한 라우팅 테이블에 새 경로를 추가합니다. 보내는 메시지에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 로컬 데이터베이스의 라우팅 테이블을 확인하여 라우팅을 결정합니다. 전달할 메시지를 포함하여 다른 인스턴스에서 나오는 대화의 메시지의 경우 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 **msdb**에서 경로를 확인합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE ROUTE route_name  
[ AUTHORIZATION owner_name ]  
WITH    
   [ SERVICE_NAME = 'service_name', ]  
   [ BROKER_INSTANCE = 'broker_instance_identifier' , ]  
   [ LIFETIME = route_lifetime , ]  
   ADDRESS =  'next_hop_address'  
   [ , MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *route_name*  
 생성할 경로의 이름입니다. 새 경로는 현재 데이터베이스에 생성되고 AUTHORIZATION 절에서 지정한 보안 주체가 소유합니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다. *route_name*은 유효한 **sysname**이어야 합니다.  
  
 AUTHORIZATION *owner_name*  
 지정한 데이터베이스 사용자 또는 역할로 경로의 소유자를 설정합니다. 현재 사용자가 **db_owner** 고정 데이터베이스 역할의 멤버이거나 **sysadmin** 고정 서버 역할의 멤버인 경우 *owner_name*은 유효한 사용자 또는 역할의 이름이 될 수 있습니다. 그렇지 않으면 *owner_name*은 현재 사용자 이름, 현재 사용자가 IMPERSONATE 권한을 갖는 사용자의 이름, 현재 사용자가 속해 있는 역할 이름 중 하나여야 합니다. 이 절을 생략하면 경로가 현재 사용자에 속합니다.  
  
 WITH  
 생성할 경로를 정의하는 절을 보여 줍니다.  
  
 SERVICE_NAME = **'** _service\_name_ **'**  
 이 경로가 가리키는 원격 서비스 이름을 지정합니다. *service_name*은 원격 서비스에서 사용되는 이름과 정확히 일치해야 합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서는 바이트 단위로 비교하여 일치하는 *service_name*을 찾습니다. 즉, 비교 시 대/소문자가 구분되고 현재 데이터 정렬은 고려되지 않습니다. SERVICE_NAME을 생략하면 이 경로는 서비스 이름과 일치하지만 SERVICE_NAME을 지정하는 경로보다 일치에 대한 우선 순위가 낮습니다. 서비스 이름이 **‘SQL/ServiceBroker/BrokerConfiguration’** 인 경로는 Broker Configuration Notice 서비스에 대한 경로입니다. 이 서비스에 대한 경로에서 broker 인스턴스를 지정하지 않을 수 있습니다.  
  
 BROKER_INSTANCE = **'** _broker\_instance\_identifier_ **'**  
 대상 서비스를 호스팅하는 데이터베이스를 지정합니다. *broker_instance_identifier* 매개 변수는 선택한 데이터베이스에서 다음 쿼리를 실행하여 가져올 수 있는 원격 데이터베이스의 Broker 인스턴스 식별자여야 합니다.  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID()  
```  
  
 BROKER_INSTANCE 절을 생략하면 이 경로는 Broker 인스턴스와 일치합니다. Broker 인스턴스와 일치하는 경로는 대화에서 Broker 인스턴스를 지정하지 않는 경우 명시적 Broker 인스턴스를 갖는 경로보다 일치에 대한 우선 순위가 높습니다. Broker 인스턴스를 지정하는 대화의 경우 Broker 인스턴스가 있는 경로는 Broker 인스턴스와 일치하는 경로보다 우선 순위가 높습니다.  
  
 LIFETIME **=** _route\_lifetime_  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 라우팅 테이블에 경로를 유지하는 시간(초)을 지정합니다. 수명이 다되어 경로가 만료되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 새 대화를 위한 경로를 선택할 때 더 이상 해당 경로를 고려하지 않습니다. 이 절을 생략하면 *route_lifetime*은 NULL이고 경로는 만료되지 않습니다.  
  
 ADDRESS **='** _next\_hop\_address_ **'**  
SQL Database 관리되는 인스턴스의 경우 `ADDRESS`는 로컬이어야 합니다. 

이 경로에 대한 네트워크 주소를 지정합니다. *next_hop_address*는 다음과 같은 형식으로 TCP/IP 주소를 지정합니다.  
  
 **TCP://** { *dns_name* | *netbios_name* | *ip_address* } **:** _port\_number_  
  
 지정된 *port_number*는 지정된 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 엔드포인트의 포트 번호와 일치해야 합니다. 선택한 데이터베이스에서 다음 쿼리를 실행하여 얻을 수 있습니다.  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 서비스가 미러된 데이터베이스에서 호스팅되면 미러된 데이터베이스를 호스팅하는 다른 인스턴스에 대해서도 MIRROR_ADDRESS를 지정해야 합니다. 그렇지 않으면 이 경로는 미러에 대해 장애 조치(Failover)되지 않습니다.  
  
 경로에 *next_hop_address*가 **‘LOCAL’** 로 지정되어 있으면 메시지는 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내의 서비스로 배달됩니다.  
  
 경로에 *next_hop_address*가 **‘TRANSPORT’** 로 지정되어 있으면 네트워크 주소는 서비스 이름의 네트워크 주소를 기준으로 결정됩니다. **‘TRANSPORT’** 를 지정하는 경로는 서비스 이름이나 broker 인스턴스를 지정하지 않을 수 있습니다.  
  
 MIRROR_ADDRESS **='** _next\_hop\_mirror\_address_ **'**  
 *next_hop_address*에서 호스팅되는 미러된 데이터베이스 하나로 미러된 데이터베이스의 네트워크 주소를 지정합니다. *next_hop_mirror_address*는 다음과 같은 형식으로 TCP/IP 주소를 지정합니다.  
  
 **TCP://** { *dns_name* | *netbios_name* | *ip_address* } **:** *port_number*  
  
 지정된 *port_number*는 지정된 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 엔드포인트의 포트 번호와 일치해야 합니다. 선택한 데이터베이스에서 다음 쿼리를 실행하여 얻을 수 있습니다.  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 MIRROR_ADDRESS가 지정된 경로에는 SERVICE_NAME 절 및 BROKER_INSTANCE 절을 지정해야 합니다. *next_hop_address*가 **‘LOCAL’** 또는 **‘TRANSPORT’** 로 지정된 경로에는 미러 주소가 지정되지 않을 수 있습니다.  
  
## <a name="remarks"></a>설명  
 경로를 저장하는 라우팅 테이블은 **sys.routes** 카탈로그 뷰를 통해 읽을 수 있는 메타데이터 테이블입니다. 이 카탈로그 뷰는 CREATE ROUTE, ALTER ROUTE 및 DROP ROUTE 문을 통해서만 업데이트할 수 있습니다.  
  
 기본적으로 각 사용자 데이터베이스의 라우팅 테이블에는 한 경로가 들어 있습니다. 이 경로의 이름은 **AutoCreatedLocal**입니다. 경로는 *next_hop_address*로 **‘LOCAL’** 을 지정하고 모든 서비스 이름 및 Broker 인스턴스 식별자와 일치합니다.  
  
 경로에 *next_hop_address*가 **‘TRANSPORT’** 로 지정되어 있으면 네트워크 주소는 서비스 이름의 네트워크 주소를 기준으로 결정됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 *next_hop_address*에 유효한 형식의 네트워크 주소로 시작하는 서비스 이름을 처리할 수 있습니다.  
  
 라우팅 테이블에는 동일한 서비스, 네트워크 주소 및 Broker 인스턴스 식별자를 지정하는 경로가 여러 개일 수 있습니다. 이 경우 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 라우팅 테이블의 정보 중 대화에 지정된 정보와 가장 정확하게 일치하는 정보를 찾을 수 있도록 개발된 프로시저를 사용하여 경로를 선택합니다.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 라우팅 테이블에서 만료된 경로를 제거하지 않습니다. 만료된 경로는 ALTER ROUTE 문을 사용하여 활성 상태로 설정할 수 있습니다.  
  
 경로는 임시 개체가 아닐 수 있습니다. 경로 이름은 **#** 으로 시작할 수 있지만 영구 개체입니다.  
  
## <a name="permissions"></a>사용 권한  
 경로 생성 권한은 기본적으로 **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할 및 **sysadmin** 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-tcpip-route-by-using-a-dns-name"></a>A. DNS 이름을 사용하여 TCP/IP 경로 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 서비스에 대한 경로를 만듭니다. 경로는 이 서비스에 대한 메시지가 TCP를 통해 DNS 이름 `1234`으로 식별되는 호스트의 포트 `www.Adventure-Works.com`로 이동되도록 지정합니다. 메시지 도착 시 대상 서버는 고유 식별자 `D8D4D268-00A3-4C62-8F91-634B89C1E315`로 식별되는 Broker 인스턴스로 메시지를 배달합니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://www.Adventure-Works.com:1234' ;  
```  
  
### <a name="b-creating-a-tcpip-route-by-using-a-netbios-name"></a>B. NetBIOS 이름을 사용하여 TCP/IP 경로 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 서비스에 대한 경로를 만듭니다. 경로는 이 서비스에 대한 메시지가 TCP를 통해 NetBIOS 이름 `1234`로 식별되는 호스트의 포트 `SERVER02`로 이동되도록 지정합니다. 메시지 도착 시 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 고유 식별자 `D8D4D268-00A3-4C62-8F91-634B89C1E315`로 식별되는 데이터베이스 인스턴스로 메시지를 배달합니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH   
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://SERVER02:1234' ;  
```  
  
### <a name="c-creating-a-tcpip-route-by-using-an-ip-address"></a>C. IP 주소를 사용하여 TCP/IP 경로 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 서비스에 대한 경로를 만듭니다. 경로는 이 서비스에 대한 메시지가 TCP를 통해 IP 주소가 `1234`인 호스트의 포트 `192.168.10.2`로 이동되도록 지정합니다. 메시지 도착 시 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 고유 식별자 `D8D4D268-00A3-4C62-8F91-634B89C1E315`로 식별되는 Broker 인스턴스로 메시지를 배달합니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://192.168.10.2:1234' ;  
```  
  
### <a name="d-creating-a-route-to-a-forwarding-broker"></a>D. 전달 Broker에 대한 경로 만들기  
 다음 예에서는 `dispatch.Adventure-Works.com` 서버의 전달 Broker에 대한 경로를 만듭니다. 서비스 이름과 broker 인스턴스 식별자를 둘 다 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 다른 경로가 정의되지 않은 서비스에 이 경로를 사용합니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    ADDRESS = 'TCP://dispatch.Adventure-Works.com' ;   
```  
  
### <a name="e-creating-a-route-to-a-local-service"></a>E. 로컬 서비스에 대한 경로 만들기  
 다음 예에서는 경로와 같은 인스턴스의 `//Adventure-Works.com/LogRequests` 서비스에 대한 경로를 만듭니다.  
  
```  
CREATE ROUTE LogRequests  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/LogRequests',  
    ADDRESS = 'LOCAL' ;  
```  
  
### <a name="f-creating-a-route-with-a-specified-lifetime"></a>F. 지정한 유효 기간으로 경로 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 서비스에 대한 경로를 만듭니다. 경로의 유효 기간은 `259200`초(72시간)입니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    LIFETIME = 259200,  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234' ;  
```  
  
### <a name="g-creating-a-route-to-a-mirrored-database"></a>G. 미러된 데이터베이스에 대한 경로 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 서비스에 대한 경로를 만듭니다. 서비스는 미러된 데이터베이스에서 호스팅됩니다. 미러된 데이터베이스 중 하나는 주소 `services.Adventure-Works.com:1234`에 있으며 다른 데이터베이스는 주소 `services-mirror.Adventure-Works.com:1234`에 있습니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = '69fcc80c-2239-4700-8437-1001ecddf933',  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234',   
    MIRROR_ADDRESS = 'TCP://services-mirror.Adventure-Works.com:1234' ;  
```  
  
### <a name="h-creating-a-route-that-uses-the-service-name-for-routing"></a>H. 라우팅에 서비스 이름을 사용하는 경로 만들기  
 다음 예에서는 메시지를 보낼 네트워크 주소를 확인하는 데 서비스 이름을 사용하는 경로를 만듭니다. 네트워크 주소로 `'TRANSPORT'`를 지정하는 경로는 다른 경로보다 일치 시 우선 순위가 낮습니다.  
  
```  
CREATE ROUTE TransportRoute  
    WITH ADDRESS = 'TRANSPORT' ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER ROUTE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [DROP ROUTE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
