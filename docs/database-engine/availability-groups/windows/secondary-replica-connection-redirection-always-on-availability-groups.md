---
title: 주 복제본에 대한 읽기/쓰기 연결 리디렉션
description: 연결 문자열에 지정된 서버와 관계없이 Always On 가용성 그룹의 주 복제본에 대한 읽기/쓰기 연결을 리디렉션하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 01/09/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: article
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- readable secondary replicas
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 794d2f682c5a32ee348d229cfd2413687a57843e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637819"
---
# <a name="secondary-to-primary-replica-readwrite-connection-redirection-always-on-availability-groups"></a>보조-주 복제본 읽기/쓰기 연결 리디렉션(Always On 가용성 그룹)

[!INCLUDE[appliesto](../../../includes/applies-to-version/sqlserver2019.md)]

[!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)] CTP 2.0은 Always On 가용성 그룹에 대해 *보조-주 복제본 읽기/쓰기 연결 리디렉션*을 도입했습니다. 읽기/쓰기 연결 리디렉션은 모든 운영 체제 플랫폼에서 사용할 수 있습니다. 이 기능은 연결 문자열에 지정된 대상 서버에 관계없이, 클라이언트 애플리케이션 연결이 주 복제본으로 전송되도록 합니다. 

예를 들어 연결 문자열은 보조 복제본을 대상으로 지정할 수 있습니다. AG(가용성 그룹) 복제본 구성 및 연결 문자열의 설정에 따라 연결이 주 복제본으로 자동으로 리디렉션될 수 있습니다. 

## <a name="use-cases"></a>사용 사례

[!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)] 이전에는 장애 조치(Failover) 후에 다시 연결되도록 하기 위해 AG 수신기 및 해당 클러스터 리소스가 사용자 트래픽을 주 복제본으로 리디렉션합니다. [!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)]에서는 AG 수신기 기능을 계속 지원하고 수신기를 포함할 수 없는 시나리오를 위해 복제본 연결 리디렉션을 추가합니다. 예를 들면 다음과 같습니다.

* SQL Server 가용성 그룹과 통합되는 클러스터 기술은 수신기 유사 기능을 제공하지 않습니다. 
* 클라우드 또는 다중 서브넷 부동 IP(Pacemaker 포함)의 다중 서브넷 구성(관련된 여러 구성 요소로 인해 구성이 복잡해지고 오류가 발생하기 쉬우며 문제 해결이 어려움)
* 수동 장애 조치(Failover) 시 투명한 연결을 보장하기 위한 간편한 메커니즘이 없으므로 읽기 스케일 아웃 또는 재해 복구 및 클러스터 형식은 `NONE`입니다.

## <a name="requirement"></a>요구 사항

보조 복제본이 읽기/쓰기 연결 요청을 리디렉션하려면 다음이 충족되어야 합니다.
* 보조 복제본이 온라인 상태여야 합니다. 
* 복제본 사양 `PRIMARY_ROLE`에는 `READ_WRITE_ROUTING_URL`이 포함되어야 합니다.
* `ApplicationIntent`를 `ReadWrite`로 정의하거나 `ApplicationIntent`를 설정하지 않고 기본값(`ReadWrite`)이 적용되도록 함으로써 연결 문자열은 `ReadWrite`가 되어야 합니다.

## <a name="set-read_write_routing_url-option"></a>READ_WRITE_ROUTING_URL 옵션 설정

읽기/쓰기 연결 리디렉션을 구성하려면 AG를 만들 주 복제본에 대해 `READ_WRITE_ROUTING_URL`을 설정합니다. 

[!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)]에서 `READ_WRITE_ROUTING_URL`이 `<add_replica_option>` 사양에 추가되었습니다. 다음 항목을 참조하세요. 

* [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)
* [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)


### <a name="primary_roleread_write_routing_url-not-set-default"></a>PRIMARY_ROLE(READ_WRITE_ROUTING_URL)이 설정되지 않음(기본값) 

기본적으로 읽기/쓰기 복제본 연결 리디렉션은 복제본에 대해 설정되지 않습니다. 보조 복제본이 연결 요청을 처리하는 방식은 보조 복제본이 연결을 허용하도록 설정되어 있는지 여부와 연결 문자열의 `ApplicationIntent` 설정에 따라 좌우됩니다. 다음 표에서는 보조 복제본이 `SECONDARY_ROLE (ALLOW CONNECTIONS = )` 및 `ApplicationIntent`에 따라 연결을 처리하는 방법을 보여 줍니다.

||`SECONDARY_ROLE (ALLOW CONNECTIONS = NO)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = READ_ONLY)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = ALL)`|
|-----|-----|-----|-----|
|`ApplicationIntent=ReadWrite`<br/> 기본값|연결 실패|연결 실패|연결 성공<br/>읽기 성공<br/>쓰기 실패|
|`ApplicationIntent=ReadOnly`|연결 실패|연결 성공|연결 성공

앞의 표는 [!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)] 이전의 SQL Server 버전과 동일한 기본 동작을 보여 줍니다. 

### <a name="primary_roleread_write_routing_url-set"></a>PRIMARY_ROLE(READ_WRITE_ROUTING_URL) 설정 

읽기/쓰기 연결 리디렉션을 설정한 후에는 복제본이 연결 요청을 처리하는 방식이 다르게 동작합니다. 연결 동작은 여전히 `SECONDARY_ROLE (ALLOW CONNECTIONS = )` 및 `ApplicationIntent` 설정에 따라 좌우됩니다. 다음 표에서는 `READ_WRITE_ROUTING`이 설정된 보조 복제본이 `SECONDARY_ROLE (ALLOW CONNECTIONS = )` 및 `ApplicationIntent`에 따라 연결을 처리하는 방법을 보여 줍니다.

||`SECONDARY_ROLE (ALLOW CONNECTIONS = NO)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = READ_ONLY)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = ALL)`|
|-----|-----|-----|-----|
|`ApplicationIntent=ReadWrite`<br/>기본값|연결 실패|연결 실패|연결 경로가 주 복제본으로 지정|
|`ApplicationIntent=ReadOnly`|연결 실패|연결 성공|연결 성공

앞의 표에서는 주 복제본에 `READ_WRITE_ROUTING_URL`이 설정되어 있을 때 `SECONDARY_ROLE (ALLOW CONNECTIONS = ALL)`이면 보조 복제본이 연결을 주 복제본으로 리디렉션하며 연결은 `ReadWrite`를 지정함을 나타냅니다.

## <a name="example"></a>예제 

이 예제에서 가용성 그룹에는 다음 3개의 복제본이 있습니다.
* COMPUTER01의 주 복제본
* COMPUTER02의 동기 보조 복제본
* COMPUTER03의 비동기 보조 복제본

다음 그림은 가용성 그룹을 나타냅니다.

![원래 가용성 그룹](media/replica-connection-redirection-always-on-availability-groups/01_originalAG.png)

다음 Transact-SQL 스크립트는 이 AG를 만듭니다. 이 예제에서 각 복제본은 `READ_WRITE_ROUTING_URL`을 지정합니다.
```sql
CREATE AVAILABILITY GROUP MyAg   
     WITH ( CLUSTER_TYPE =  NONE )  
   FOR   
     DATABASE  <Database1>   
   REPLICA ON   
      'COMPUTER01' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01.<domain>.<tld>:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = MANUAL,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01.<domain>.<tld>:1433' ),
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER02, COMPUTER03),
            READ_WRITE_ROUTING_URL = 'TCP://COMPUTER01.<domain>.<tld>:1433' )   
         SESSION_TIMEOUT = 10  
         ),   
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02.<domain>.<tld>:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = MANUAL, 
         SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02.<domain>.<tld>:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER01, COMPUTER03),  
            READ_WRITE_ROUTING_URL = 'TCP://COMPUTER02.<domain>.<tld>:1433' )   
         SESSION_TIMEOUT = 10  
         ),   
      'COMPUTER03' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03.<domain>.<tld>:5022',  
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = MANUAL,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03.<domain>.<tld>:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER01, COMPUTER02),  
            READ_WRITE_ROUTING_URL = 'TCP://COMPUTER03.<domain>.<tld>:1433' )  
         SESSION_TIMEOUT = 10  
         );
GO  
```
   - `<domain>.<tld>`
      - 전체 정규화된 도메인 이름의 도메인 및 최상위 도메인 예들 들어 `corporation.com`입니다.


### <a name="connection-behaviors"></a>연결 동작

다음 다이어그램에서 클라이언트 애플리케이션은 `ApplicationIntent=ReadWrite`를 사용하여 COMPUTER02에 연결됩니다. 연결은 주 복제본으로 리디렉션됩니다. 

![원래 가용성 그룹](media/replica-connection-redirection-always-on-availability-groups/02_redirectionAG.png)

보조 복제본은 읽기/쓰기 호출을 주 복제본으로 리디렉션합니다. 각 복제본에 대한 읽기/쓰기 연결이 주 복제본으로 리디렉션됩니다. 

다음 다이어그램에서는 주 복제본이 COMPUTER02로 수동 장애 조치(Failover)되었습니다. 클라이언트 애플리케이션은 `ApplicationIntent=ReadWrite`를 사용하여 COMPUTER01에 연결합니다. 연결은 주 복제본으로 리디렉션됩니다. 

![원래 가용성 그룹](media/replica-connection-redirection-always-on-availability-groups/03_redirectionAG.png)


## <a name="sql-server-instance-offline"></a>SQL Server 인스턴스 오프라인

연결 문자열에 지정된 SQL Server 인스턴스를 사용할 수 없는 경우(가동 중단의 경우) 대상 서버에서 해당 복제본의 역할에 관계없이 연결이 실패합니다. 애플리케이션이 장시간 가동 중지되는 것을 방지하려면 연결 문자열에 대체 `FailoverPartner`를 구성합니다. 애플리케이션은 실제 장애 조치(Failover) 동안 주 및 보조 복제본을 수용하기 위해 다시 시도 논리를 구현해야 합니다. 연결 문자열에 대한 자세한 내용은 [SqlConnection.ConnectionString Property](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)를 참조하세요.

## <a name="see-also"></a>참고 항목

[Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 
[가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   

[가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md) 
