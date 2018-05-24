---
title: ALTER ROUTE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_ROUTE_TSQL
- ALTER ROUTE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER ROUTE statement
- dropping routes
- modifying routes
- removing routes
- routes [Service Broker], modifying
ms.assetid: 8dfb7b16-3dac-4e1e-8c97-adf2aad07830
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f84ed9bb1a02658938f6e5d9eca9389547763b85
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="alter-route-transact-sql"></a>ALTER ROUTE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기존 경로에 대한 경로 정보를 수정합니다. 


[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)] 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER ROUTE route_name  
WITH    
  [ SERVICE_NAME = 'service_name' [ , ] ]  
  [ BROKER_INSTANCE = 'broker_instance' [ , ] ]  
  [ LIFETIME = route_lifetime [ , ] ]  
  [ ADDRESS =  'next_hop_address' [ , ] ]  
  [ MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
  
```  
  
## <a name="arguments"></a>인수  
 *route_name*  
 변경할 경로의 이름입니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다.  
  
 의 모든 멘션을  
 변경되는 경로를 정의하는 절을 지정합니다.  
  
 SERVICE_NAME **='***service_name***'**  
 이 경로가 가리키는 원격 서비스 이름을 지정합니다. *service_name*은 원격 서비스에서 사용되는 이름과 정확히 일치해야 합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서는 바이트 단위로 비교하여 일치하는 *service_name*을 찾습니다. 즉, 비교 시 대/소문자가 구분되고 현재 데이터 정렬은 고려되지 않습니다. 서비스 이름이 **‘SQL/ServiceBroker/BrokerConfiguration’** 인 경로는 Broker Configuration Notice 서비스에 대한 경로입니다. 이 서비스에 대한 경로에서 broker 인스턴스를 지정하지 않을 수 있습니다.  
  
 SERVICE_NAME 절이 생략되면 경로의 서비스 이름이 변경되지 않습니다.  
  
 BROKER_INSTANCE **='***broker_instance***'**  
 대상 서비스를 호스팅하는 데이터베이스를 지정합니다. *broker_instance* 매개 변수는 선택한 데이터베이스에서 다음 쿼리를 실행하여 가져올 수 있는 원격 데이터베이스의 Broker 인스턴스 식별자여야 합니다.  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID();  
```  
  
 BROKER_INSTANCE 절이 생략되면 경로의 Broker 인스턴스가 변경되지 않습니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 LIFETIME **=***route_lifetime*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 라우팅 테이블에 경로를 유지하는 시간(초)을 지정합니다. 수명이 다되어 경로가 만료되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 새 대화를 위한 경로를 선택할 때 더 이상 해당 경로를 고려하지 않습니다. 이 절이 생략되면 경로의 수명이 변경되지 않습니다.  
  
 ADDRESS **='***next_hop_address'*  

 SQL Database 관리되는 인스턴스의 경우 `ADDRESS`는 로컬이어야 합니다.

 이 경로에 대한 네트워크 주소를 지정합니다. *next_hop_address*는 다음과 같은 형식으로 TCP/IP 주소를 지정합니다.  
  
 **TCP://** { *dns_name* | *netbios_name* |*ip_address* } **:** *port_number*  
  
 지정된 *port_number*는 지정된 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 엔드포인트의 포트 번호와 일치해야 합니다. 선택한 데이터베이스에서 다음 쿼리를 실행하여 얻을 수 있습니다.  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 경로에 *next_hop_address*가 **‘LOCAL’** 로 지정되어 있으면 메시지는 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내의 서비스로 배달됩니다.  
  
 경로에 *next_hop_address*가 **'TRANSPORT'** 로 지정되어 있으면 네트워크 주소는 서비스 이름의 네트워크 주소를 기준으로 결정됩니다. **'TRANSPORT'** 를 지정하는 경로는 서비스 이름이나 broker 인스턴스를 지정할 수 있습니다.  
  
 *next_hop_address*가 데이터베이스 미러의 주 서버인 경우에는 미러 서버에 대해 MIRROR_ADDRESS도 지정해야 합니다. 그렇지 않으면 이 경로는 미러 서버에 대해 자동으로 장애 조치(Failover)하지 않습니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 MIRROR_ADDRESS **='***next_hop_mirror_address***'**  
 주 서버가 *next_hop_address*에 있는 미러링된 쌍의 미러 서버에 대해 네트워크 주소를 지정합니다. *next_hop_mirror_address*는 다음과 같은 형식으로 TCP/IP 주소를 지정합니다.  
  
 **TCP://**{ *dns_name* | *netbios_name* | *ip_address* } **:** *port_number*  
  
 지정된 *port_number*는 지정된 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 엔드포인트의 포트 번호와 일치해야 합니다. 선택한 데이터베이스에서 다음 쿼리를 실행하여 얻을 수 있습니다.  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 MIRROR_ADDRESS가 지정된 경로에는 SERVICE_NAME 절 및 BROKER_INSTANCE 절을 지정해야 합니다. *next_hop_address*가 **‘LOCAL’** 또는 **‘TRANSPORT’** 로 지정된 경로에는 미러 주소가 지정되지 않을 수 있습니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
## <a name="remarks"></a>Remarks  
 경로를 저장하는 라우팅 테이블은 **sys.routes** 카탈로그 뷰를 통해 읽을 수 있는 메타데이터 테이블입니다. 라우팅 테이블은 CREATE ROUTE, ALTER ROUTE 및 DROP ROUTE 문으로만 업데이트할 수 있습니다.  
  
 ALTER ROUTE 명령에서 지정하지 않은 절은 변경되지 않은 상태로 유지됩니다. 따라서 경로를 변경하여 경로의 제한 시간이 초과되지 않거나, 경로가 서비스 이름과 일치하거나, 경로가 모든 broker 인스턴스와 일치하도록 지정할 수는 없습니다. 이러한 경로의 특성을 변경하려면 기존 경로를 삭제하고 새 정보로 새 경로를 만들어야 합니다.  
  
 경로에 *next_hop_address*가 **‘TRANSPORT’** 로 지정되어 있으면 네트워크 주소는 서비스 이름의 네트워크 주소를 기준으로 결정됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 *next_hop_address*에 유효한 형식의 네트워크 주소로 시작하는 서비스 이름을 처리할 수 있습니다. 유효한 네트워크 경로를 포함하는 이름의 서비스는 서비스 이름에 있는 네트워크 경로로 라우팅됩니다.  
  
 라우팅 테이블에는 동일한 서비스, 네트워크 주소 및 broker 인스턴스 식별자를 지정하는 경로가 여러 개일 수 있습니다. 이 경우 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 라우팅 테이블의 정보 중 대화에 지정된 정보와 가장 정확하게 일치하는 정보를 찾을 수 있도록 개발된 프로시저를 사용하여 경로를 선택합니다.  
  
 서비스에 대한 AUTHORIZATION을 변경하려면 ALTER AUTHORIZATION 문을 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
 경로 변경 권한은 기본적으로 경로 소유자, **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할의 멤버 및 **sysadmin** 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-service-for-a-route"></a>1. 경로에 대한 서비스 변경  
 다음 예에서는 `ExpenseRoute` 원격 서비스를 가리키도록 `//Adventure-Works.com/Expenses` 경로를 수정합니다.  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     SERVICE_NAME = '//Adventure-Works.com/Expenses';  
```  
  
### <a name="b-changing-the-target-database-for-a-route"></a>2. 경로의 대상 데이터베이스 변경  
 다음 예에서는 `ExpenseRoute` 경로의 대상 데이터베이스를 `D8D4D268-00A3-4C62-8F91-634B89B1E317.` 고유 식별자로 식별되는 데이터베이스로 변경합니다.  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317';  
```  
  
### <a name="c-changing-the-address-for-a-route"></a>3. 경로의 주소 변경  
 다음 예에서는 `ExpenseRoute` 경로의 네트워크 주소를 IP 주소가 `1234`인 호스트의 TCP 포트 `10.2.19.72`로 변경합니다.  
  
```  
ALTER ROUTE ExpenseRoute   
   WITH   
     ADDRESS = 'TCP://10.2.19.72:1234';  
```  
  
### <a name="d-changing-the-database-and-address-for-a-route"></a>4. 경로의 데이터베이스 및 주소 변경  
 다음 예에서는 `ExpenseRoute` 경로의 네트워크 주소를 DNS 이름이 `1234`인 호스트의 TCP 포트 `www.Adventure-Works.com`로 변경합니다. 또한 대상 데이터베이스를 고유 식별자 `D8D4D268-00A3-4C62-8F91-634B89B1E317`로 식별되는 데이터베이스로 변경합니다.  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317',  
     ADDRESS = 'TCP://www.Adventure-Works.com:1234';  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE ROUTE&#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [DROP ROUTE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
