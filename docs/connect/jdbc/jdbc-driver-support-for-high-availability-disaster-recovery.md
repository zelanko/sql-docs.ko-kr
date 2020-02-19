---
title: 고가용성, 재해 복구를 위한 JDBC 드라이버 지원 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a959292b7adc2b5bb547d447f67f2a392de8af4c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027949"
---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>고가용성, 재해 복구를 위한 JDBC 드라이브 지원
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 항목에서는 고가용성 재해 복구를 위한 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 지원인 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]에 대해 설명합니다. [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]에 대한 자세한 내용은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 온라인 설명서를 참조하십시오.  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 4.0 버전부터 연결 속성에 (고가용성, 재해 복구) 가용성 그룹(AG)의 가용성 그룹 수신기를 지정할 수 있습니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 애플리케이션이 장애 조치되는 AlwaysOn 데이터베이스에 연결되는 경우 장애 조치 후 작업을 계속하기 위해 원래 연결이 끊어지고 애플리케이션은 새 연결을 열어야 합니다. 다음 [연결 속성](../../connect/jdbc/setting-the-connection-properties.md)이 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]에 추가되었습니다.  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
가용성 그룹 또는 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결하는 경우 multiSubnetFailover=true를 지정합니다. **multiSubnetFailover**는 기본적으로 false입니다. **applicationIntent**를 사용하여 애플리케이션 워크로드 유형을 선언합니다. 자세한 내용은 아래 섹션을 참조하세요.
 
Microsoft JDBC Driver for SQL Server 버전 6.0부터, Always On 가용성 그룹 또는 여러 IP 주소가 연결된 서버에 대한 투명 연결에 대해 새로운 연결 속성인 **transparentNetworkIPResolution**(TNIR)이 추가되었습니다. **transparentNetworkIPResolution**이 true 이면 드라이버는 사용 가능한 첫 번째 IP 주소에 연결을 시도합니다. 첫 번째 시도가 실패하면 제한 시간이 만료될 때까지 드라이버는 모든 IP 주소에 병렬로 연결을 시도하고, 그 중 하나가 성공할 때 보류 중인 연결 시도를 모두 삭제합니다.   

다음 사항에 유의하세요.
* transparentNetworkIPResolution는 기본적으로 true입니다.
* multiSubnetFailover가 true 이면 transparentNetworkIPResolution이 무시됩니다.
* 데이터베이스 미러링이 사용되면 transparentNetworkIPResolution이 무시됩니다.
* IP 주소가 64개를 초과하면 transparentNetworkIPResolution이 무시됩니다.
* transparentNetworkIPResolution이 true인 경우 첫 번째 연결 시도는 500ms의 시간 제한 값을 사용합니다. 나머지 연결 시도는 multiSubnetFailover 기능과 동일한 논리를 따릅니다. 

> [!NOTE]
> Microsoft JDBC Driver 4.2 for SQL Server(이하)를 사용하는 경우 **multiSubnetFailover**가 false이면 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 첫 번째 IP 주소에 연결을 시도합니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 첫 번째 IP 주소와 연결을 설정할 수 없는 경우 연결은 실패합니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 서버와 연결된 후속 IP 주소에는 연결을 시도하지 않습니다. 
> 
> 
> [!NOTE]
>  연결 제한 시간을 늘리고 연결 재시도 논리를 구현하면 애플리케이션이 가용성 그룹에 연결될 가능성이 증가합니다. 또한 가용성 그룹 장애 조치(failover)로 인해 연결이 실패할 수 있으므로 실패한 연결을 다시 연결할 때까지 다시 시도하는 연결 재시도 논리를 구현해야 합니다.  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>multiSubnetFailover로 연결  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 가용성 그룹 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 **multiSubnetFailover=true**를 지정합니다. **multiSubnetFailover**를 사용하면 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 모든 가용성 그룹 및 장애 조치(Failover) 클러스터 인스턴스에 대한 장애 조치(Failover)를 빠르게 수행하고 단일 및 다중 서브넷 Always On 토폴로지에 대한 장애 조치(Failover) 시간을 크게 줄일 수 있습니다. 다중 서브넷 장애 조치(Failover) 중에는 클라이언트가 연결을 병렬로 시도합니다. 서브넷을 장애 조치하는 동안 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 TCP 연결을 공격적으로 재시도합니다.  
  
 **multiSubnetFailover** 연결 속성은 애플리케이션을 가용성 그룹 또는 장애 조치(Failover) 클러스터 인스턴스에 배포하는 중이며 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 모든 IP 주소에 연결을 시도하여 주 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터베이스에 연결을 시도함을 나타냅니다. 연결에 대해 **MultiSubnetFailover=true**를 지정하면 클라이언트는 운영 체제의 기본 TCP 재전송 간격보다 빠르게 TCP 연결을 다시 시도합니다. 이렇게 하면 AlwaysOn 가용성 그룹 또는 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스의 장애 조치(Failover) 후 더 빠르게 다시 연결할 수 있습니다. 이 설정은 단일/다중 서브넷 가용성 그룹 및 장애 조치(Failover) 클러스터 인스턴스에 모두 적용됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]의 연결 문자열 키워드에 대한 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.  
  
 가용성 그룹 수신기 또는 장애 조치(Failover) 클러스터 인스턴스 이외의 다른 항목에 연결할 때 **multiSubnetFailover=true**를 지정하면 성능에 상당히 부정적인 영향을 줄 수 있으므로 이러한 설정은 지원되지 않습니다.  
  
 보안 관리자가 설치되지 않은 경우 Java Virtual Machine은 기본적으로 JDK 구현 및 Java 속성 networkaddress.cache.ttl 및 networkaddress.cache.negative.ttl에 정의된 제한 시간 동안 VIP(가상 IP 주소)를 캐시합니다. JDK 보안 관리자가 설치된 경우 Java Virtual Machine은 VIP를 캐시하고 기본적으로 캐시를 새로 고치지 않습니다. Java Virtual Machine 캐시에 대해 "TTL(time-to-live)"(networkaddress.cache.ttl)을 1일로 설정해야 합니다. 기본값을 1일(정도)로 변경하지 않으면 VIP를 추가하거나 업데이트할 때 Java Virtual Machine 캐시에서 기존 값이 삭제되지 않습니다. networkaddress.cache.ttl 및 networkaddress.cache.negative.ttl에 대한 자세한 내용은 [https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html](https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html)를 참조하세요.  
  
 다음 지침에 따라 장애 조치(Failover) 클러스터 인스턴스 또는 가용성 그룹의 서버에 연결하십시오.  
  
-   **instanceName** 연결 속성이 **multiSubnetFailover** 연결 속성과 같은 연결 문자열에 사용되는 경우 드라이버는 오류를 생성합니다. 이는 SQL Browser가 가용성 그룹에 사용되지 않는다는 사실을 반영합니다. 그러나 **portNumber** 연결 속성도 지정된 경우 드라이버는 **instanceName**을 무시하고 **portNumber**를 사용합니다.  
  
-   단일 서브넷 또는 다중 서브넷에 연결할 때 **multiSubnetFailover** 연결 속성을 사용하면 두 서브넷의 성능이 향상됩니다.  
  
-   가용성 그룹에 연결하려면 가용성 그룹에 대한 가용성 그룹 수신기를 연결 문자열의 서버로 지정합니다. 예를 들어, jdbc:sqlserver://VNN1입니다.  
  
-   IP 주소가 64개 이상으로 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 연결 오류가 발생합니다.  
  
-   **MultiSubnetFailover** 연결 속성을 사용하는 애플리케이션의 동작은 인증 유형([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증, Kerberos 인증 또는 Windows 인증)에 영향을 받지 않습니다.  
  
-   장애 조치(failover) 시간을 수용하고 애플리케이션의 연결 재시도 횟수를 줄이기 위해 **loginTimeout** 값을 증가시킵니다.  
  
-   분산된 트랜잭션은 지원되지 않습니다.  
  
 읽기 전용 라우팅이 적용되지 않으면 다음과 같은 경우 가용성 그룹의 보조 복제본 위치에 대한 연결이 실패합니다.  
  
1.  보조 복제본 위치가 연결을 허용하도록 구성되어 있지 않은 경우  
  
2.  애플리케이션에서 **applicationIntent=ReadWrite**(아래에서 설명)를 사용하고 보조 복제본 위치가 읽기 전용 액세스용으로 구성되어 있는 경우  
  
 주 복제본이 읽기 전용 작업을 거부하도록 구성되어 있고 연결 문자열에 **ApplicationIntent=ReadOnly**가 포함되어 있으면 연결이 실패합니다.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>데이터베이스 미러링에서 다중 서브넷 클러스터를 사용하도록 업그레이드  
 현재 데이터베이스 미러링을 사용 중인 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 애플리케이션을 다중 서브넷 시나리오로 업그레이드할 경우에는 **failoverPartner** 연결 속성을 제거하고, 이를 **true**로 설정된 **multiSubnetFailover**로 바꾸고, 연결 문자열에서 서버 이름을 가용성 그룹 수신기로 바꿔야 합니다. 연결 문자열에서 **failoverPartner** 및 **multiSubnetFailover=true**를 사용하는 경우 드라이버에서 오류가 발생합니다. 그러나 연결 문자열에서 **failoverPartner** 및 **multiSubnetFailover=false**(또는 **ApplicationIntent=ReadWrite**)를 사용하면 애플리케이션에서 데이터베이스 미러링을 사용합니다.  
  
 AG의 주 데이터베이스에서 데이터베이스 미러링이 사용되고 가용성 그룹 수신기가 아닌 주 데이터베이스에 연결하는 연결 문자열에 **multiSubnetFailover=true**가 사용될 경우 드라이버에서는 오류를 반환합니다.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>multiSubnetFailover 및 applicationIntent를 지원하는 새 메서드  
 다음 메서드는 **multiSubnetFailover**, **applicationIntent** 및 **transparentNetworkIPResolution** 연결 문자열 키워드에 대한 프로그래밍 방식 액세스를 제공합니다.  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 **getMultiSubnetFailover**, **setMultiSubnetFailover**, **getApplicationIntent**, **setApplicationIntent**, **getTransparentNetworkIPResolution** 및 **setTransparentNetworkIPResolution** 메서드는 [SQLServerDataSource 클래스](../../connect/jdbc/reference/sqlserverdatasource-class.md), [SQLServerConnectionPoolDataSource 클래스](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) 및 [SQLServerXADataSource 클래스](../../connect/jdbc/reference/sqlserverxadatasource-class.md)에도 추가됩니다.  
  
## <a name="ssl-certificate-validation"></a>SSL 인증서의 유효성 검사  
 가용성 그룹은 여러 물리적 서버로 구성되어 있습니다. [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]에서는 여러 호스트를 동일한 인증서에 연결할 수 있도록 SSL 인증서에서 **Subject Alternate Name**에 대한 지원을 추가했습니다. SSL에 대한 자세한 내용은 [SSL 지원 이해](../../connect/jdbc/understanding-ssl-support.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
