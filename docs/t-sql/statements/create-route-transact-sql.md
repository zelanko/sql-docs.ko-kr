---
title: "경로 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7268b5c9b43505d3c66fb6573a9a41c3cd62e3a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-route-transact-sql"></a>CREATE ROUTE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에 대한 라우팅 테이블에 새 경로를 추가합니다. 보내는 메시지에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 로컬 데이터베이스의 라우팅 테이블을 확인하여 라우팅을 결정합니다. 다른 인스턴스에서 나오는 대화에서 메시지를 전달 될 메시지를 포함 하 여 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 에서 경로 확인 **msdb**합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 생성할 경로의 이름입니다. 새 경로는 현재 데이터베이스에 생성되고 AUTHORIZATION 절에서 지정한 보안 주체가 소유합니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다. *route_name* 은 유효한 **sysname**합니다.  
  
 권한 부여 *owner_name*  
 지정한 데이터베이스 사용자 또는 역할로 경로의 소유자를 설정합니다. *owner_name* 현재 사용자의 구성원 인 경우 모든 유효한 사용자 또는 역할의 이름일 수는 **db_owner** 고정된 데이터베이스 역할 또는 **sysadmin** 고정된 서버 역할입니다. 그렇지 않으면 *owner_name* 현재 사용자의 이름, 현재 사용자가을 대 한 IMPERSONATE 권한이 있는 사용자의 이름 또는 현재 사용자가 속해 있는 역할의 이름 이어야 합니다. 이 절을 생략하면 경로가 현재 사용자에 속합니다.  
  
 의 모든 멘션을  
 생성할 경로를 정의하는 절을 보여 줍니다.  
  
 SERVICE_NAME = **'***service_name***'**  
 이 경로가 가리키는 원격 서비스 이름을 지정합니다. *service_name* 원격 서비스 이름을 사용 하 여 정확히 일치 해야 합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]바이트 단위 비교를 사용 하 여 일치 하는 *service_name*합니다. 즉, 비교 시 대/소문자가 구분되고 현재 데이터 정렬은 고려되지 않습니다. SERVICE_NAME을 생략하면 이 경로는 서비스 이름과 일치하지만 SERVICE_NAME을 지정하는 경로보다 일치에 대한 우선 순위가 낮습니다. 서비스 이름 사용 하는 경로가 **' SQL/ServiceBroker/BrokerConfiguration '** Broker Configuration Notice 서비스에 대 한 경로입니다. 이 서비스에 대한 경로에서 broker 인스턴스를 지정하지 않을 수 있습니다.  
  
 BROKER_INSTANCE = **'***broker_instance_identifier***'**  
 대상 서비스를 호스팅하는 데이터베이스를 지정합니다. *broker_instance_identifier* 매개 변수는 선택한 데이터베이스에서 다음 쿼리를 실행 하 여 가져올 수 있는 원격 데이터베이스에 대 한 broker 인스턴스 식별자 여야 합니다.  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID()  
```  
  
 BROKER_INSTANCE 절을 생략하면 이 경로는 Broker 인스턴스와 일치합니다. Broker 인스턴스와 일치하는 경로는 대화에서 Broker 인스턴스를 지정하지 않는 경우 명시적 Broker 인스턴스를 갖는 경로보다 일치에 대한 우선 순위가 높습니다. Broker 인스턴스를 지정하는 대화의 경우 Broker 인스턴스가 있는 경로는 Broker 인스턴스와 일치하는 경로보다 우선 순위가 높습니다.  
  
 수명  **=**  *route_lifetime*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 라우팅 테이블에 경로를 유지하는 시간(초)을 지정합니다. 수명이 다되어 경로가 만료되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 새 대화를 위한 경로를 선택할 때 더 이상 해당 경로를 고려하지 않습니다. 이 절을 생략 하는 경우는 *route_lifetime* NULL이 고 경로가 만료 되지 않습니다.  
  
 주소 **='***next_hop_address***'**  
 이 경로에 대한 네트워크 주소를 지정합니다. *next_hop_address* 다음 형식으로 TCP/IP 주소를 지정 합니다.  
  
 **TCP: / /**{ *dns_name* | *netbios_name* | *ip_address* } **:**  *port_number*  
  
 지정 된 *port_number* 에 대 한 포트 번호와 일치 해야 합니다는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 인스턴스의 끝점 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정 된 컴퓨터에서 합니다. 선택한 데이터베이스에서 다음 쿼리를 실행하여 얻을 수 있습니다.  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 서비스가 미러된 데이터베이스에서 호스팅되면 미러된 데이터베이스를 호스팅하는 다른 인스턴스에 대해서도 MIRROR_ADDRESS를 지정해야 합니다. 그렇지 않으면 이 경로는 미러에 대해 장애 조치(Failover)되지 않습니다.  
  
 경로 지정 하는 경우 **'LOCAL'** 에 대 한는 *next_hop_address*, 메시지의 현재 인스턴스 내의 서비스로 배달 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 경로 지정 하는 경우 **'TRANSPORT'** 에 대 한는 *next_hop_address*, 네트워크 주소는 서비스 이름에 네트워크 주소에 따라 결정 됩니다. 지정 하는 경로가 **'TRANSPORT'** 서비스 이름이 나 broker 인스턴스를 지정할 수 있습니다.  
  
 MIRROR_ADDRESS **='***next_hop_mirror_address***'**  
 호스트 되는 미러된 데이터베이스 하나로 미러된 데이터베이스에 대 한 네트워크 주소를 지정 된 *next_hop_address*합니다. *next_hop_mirror_address* 다음 형식으로 TCP/IP 주소를 지정 합니다.  
  
 **TCP: / /**{ *dns_name* | *netbios_name* | *ip_address* } **:**  *port_number*  
  
 지정 된 *port_number* 에 대 한 포트 번호와 일치 해야 합니다는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 인스턴스의 끝점 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정 된 컴퓨터에서 합니다. 선택한 데이터베이스에서 다음 쿼리를 실행하여 얻을 수 있습니다.  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 MIRROR_ADDRESS가 지정된 경로에는 SERVICE_NAME 절 및 BROKER_INSTANCE 절을 지정해야 합니다. 지정 하는 경로가 **'LOCAL'** 또는 **'TRANSPORT'** 에 대 한는 *next_hop_address* 미러 주소를 지정할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 경로 저장 하는 라우팅 테이블을 통해 읽을 수 있는 메타 데이터 테이블은는 **sys.routes** 카탈로그 뷰에 있습니다. 이 카탈로그 뷰는 CREATE ROUTE, ALTER ROUTE 및 DROP ROUTE 문을 통해서만 업데이트할 수 있습니다.  
  
 기본적으로 각 사용자 데이터베이스의 라우팅 테이블에는 한 경로가 들어 있습니다. 이 경로의 이름은 **AutoCreatedLocal**합니다. 경로 지정 **'LOCAL'** 에 대 한는 *next_hop_address* 모든 서비스 이름과 broker 인스턴스 식별자와 일치 합니다.  
  
 경로 지정 하는 경우 **'TRANSPORT'** 에 대 한는 *next_hop_address*, 네트워크 주소는 서비스의 이름에 따라 결정 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 유효한 형식의 네트워크 주소로 시작 하는 서비스 이름을 처리할 수 있습니다는 *next_hop_address*합니다.  
  
 라우팅 테이블에는 동일한 서비스, 네트워크 주소 및 Broker 인스턴스 식별자를 지정하는 경로가 여러 개일 수 있습니다. 이 경우 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 라우팅 테이블의 정보 중 대화에 지정된 정보와 가장 정확하게 일치하는 정보를 찾을 수 있도록 개발된 프로시저를 사용하여 경로를 선택합니다.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 라우팅 테이블에서 만료된 경로를 제거하지 않습니다. 만료된 경로는 ALTER ROUTE 문을 사용하여 활성 상태로 설정할 수 있습니다.  
  
 경로는 임시 개체가 아닐 수 있습니다. 로 시작 하는 이름을 라우팅  **#**  수 있지만 영구 개체입니다.  
  
## <a name="permissions"></a>Permissions  
 기본값의 멤버에 대 한 경로 만들기에 대 한 권한을 **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할 및 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-tcpip-route-by-using-a-dns-name"></a>1. DNS 이름을 사용하여 TCP/IP 경로 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 서비스에 대한 경로를 만듭니다. 경로는 이 서비스에 대한 메시지가 TCP를 통해 DNS 이름 `1234`으로 식별되는 호스트의 포트 `www.Adventure-Works.com`로 이동되도록 지정합니다. 메시지 도착 시 대상 서버는 고유 식별자 `D8D4D268-00A3-4C62-8F91-634B89C1E315`로 식별되는 Broker 인스턴스로 메시지를 배달합니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://www.Adventure-Works.com:1234' ;  
```  
  
### <a name="b-creating-a-tcpip-route-by-using-a-netbios-name"></a>2. NetBIOS 이름을 사용하여 TCP/IP 경로 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 서비스에 대한 경로를 만듭니다. 경로는 이 서비스에 대한 메시지가 TCP를 통해 NetBIOS 이름 `1234`로 식별되는 호스트의 포트 `SERVER02`로 이동되도록 지정합니다. 메시지 도착 시 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 고유 식별자 `D8D4D268-00A3-4C62-8F91-634B89C1E315`로 식별되는 데이터베이스 인스턴스로 메시지를 배달합니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH   
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://SERVER02:1234' ;  
```  
  
### <a name="c-creating-a-tcpip-route-by-using-an-ip-address"></a>3. IP 주소를 사용하여 TCP/IP 경로 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 서비스에 대한 경로를 만듭니다. 경로는 이 서비스에 대한 메시지가 TCP를 통해 IP 주소가 `1234`인 호스트의 포트 `192.168.10.2`로 이동되도록 지정합니다. 메시지 도착 시 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 고유 식별자 `D8D4D268-00A3-4C62-8F91-634B89C1E315`로 식별되는 Broker 인스턴스로 메시지를 배달합니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://192.168.10.2:1234' ;  
```  
  
### <a name="d-creating-a-route-to-a-forwarding-broker"></a>4. 전달 Broker에 대한 경로 만들기  
 다음 예에서는 `dispatch.Adventure-Works.com` 서버의 전달 Broker에 대한 경로를 만듭니다. 서비스 이름과 broker 인스턴스 식별자를 둘 다 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 다른 경로가 정의되지 않은 서비스에 이 경로를 사용합니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    ADDRESS = 'TCP://dispatch.Adventure-Works.com' ;   
```  
  
### <a name="e-creating-a-route-to-a-local-service"></a>5. 로컬 서비스에 대한 경로 만들기  
 다음 예에서는 경로와 같은 인스턴스의 `//Adventure-Works.com/LogRequests` 서비스에 대한 경로를 만듭니다.  
  
```  
CREATE ROUTE LogRequests  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/LogRequests',  
    ADDRESS = 'LOCAL' ;  
```  
  
### <a name="f-creating-a-route-with-a-specified-lifetime"></a>6. 지정한 유효 기간으로 경로 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 서비스에 대한 경로를 만듭니다. 경로의 유효 기간은 `259200`초(72시간)입니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    LIFETIME = 259200,  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234' ;  
```  
  
### <a name="g-creating-a-route-to-a-mirrored-database"></a>7. 미러된 데이터베이스에 대한 경로 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 서비스에 대한 경로를 만듭니다. 서비스는 미러된 데이터베이스에서 호스팅됩니다. 미러된 데이터베이스 중 하나는 주소 `services.Adventure-Works.com:1234`에 있으며 다른 데이터베이스는 주소 `services-mirror.Adventure-Works.com:1234`에 있습니다.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = '69fcc80c-2239-4700-8437-1001ecddf933',  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234',   
    MIRROR_ADDRESS = 'TCP://services-mirror.Adventure-Works.com:1234' ;  
```  
  
### <a name="h-creating-a-route-that-uses-the-service-name-for-routing"></a>8. 라우팅에 서비스 이름을 사용하는 경로 만들기  
 다음 예에서는 메시지를 보낼 네트워크 주소를 확인하는 데 서비스 이름을 사용하는 경로를 만듭니다. 네트워크 주소로 `'TRANSPORT'`를 지정하는 경로는 다른 경로보다 일치 시 우선 순위가 낮습니다.  
  
```  
CREATE ROUTE TransportRoute  
    WITH ADDRESS = 'TRANSPORT' ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER ROUTE &#40; Transact SQL &#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [DROP ROUTE &#40; Transact SQL &#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
