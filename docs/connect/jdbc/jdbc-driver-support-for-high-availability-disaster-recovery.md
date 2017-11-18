---
title: "고가용성, 재해 복구에 대 한 JDBC 드라이버 지원 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 27b51025180a1c9a2463c49401589ab459e7ecaf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>고가용성, 재해 복구를 위한 JDBC 드라이브 지원
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 항목에서는 설명 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 고가용성, 재해 복구를 위한 지원 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]합니다. [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]에 대한 자세한 내용은 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 온라인 설명서를 참조하십시오.  
  
 4.0 버전부터는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]의 가용성 그룹 수신기를 지정할 수 있습니다 (고가용성, 재해 복구) 가용성 그룹 (AG) 연결 속성에 있습니다. 경우는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 응용 프로그램이 장애 조치 되는 AlwaysOn 데이터베이스에 연결 되어, 원래 연결이 끊어지고 및 응용 프로그램 장애 조치 후 작업을 계속 하려면 새 연결을 열어야 합니다. 다음 [연결 속성](../../connect/jdbc/setting-the-connection-properties.md) 에 추가 된 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]:  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
지정 multiSubnetFailover = true 장애 조치 클러스터 인스턴스 또는 가용성 그룹의 가용성 그룹 수신기에 연결할 때. **multiSubnetFailover** 는 기본적으로 false입니다. 사용 하 여 **applicationIntent** 를 응용 프로그램 작업 유형을 선언 합니다. 자세한 내용은 아래 섹션을 참조 하십시오.
 
SQL Server, 새 연결 속성에 대 한 Microsoft JDBC 드라이버의 버전 6.0부터 **transparentNetworkIPResolution** (TNIR)에 추가 됩니다 한 투명 한 연결에 대 한 Always On 가용성 그룹을 서버에는 연결 된 여러 IP 주소입니다. 때 **transparentNetworkIPResolution** 가 true 이면 드라이버 사용 가능한 첫 번째 IP 주소에 연결 하려고 시도 합니다. 첫 번째 시도가 실패 하면 드라이버는 둘 중 하나에 성공 하면 삭제 보류 중인 연결 시도 제한 시간이 만료 될 때까지 병렬로 모든 IP 주소에 연결을 시도 합니다.   

note 하십시오.
* transparentNetworkIPResolution은 기본적으로 true
* multiSubnetFailover 참인 경우 transparentNetworkIPResolution은 무시 됩니다.
* 데이터베이스 미러링이 사용 되는 경우 transparentNetworkIPResolution은 무시 됩니다.
* 64 개 이상의 IP 주소가 있는 경우 transparentNetworkIPResolution는 무시 됩니다.
* TransparentNetworkIPResolution true 이면 첫 번째 연결 시도가 500 밀리초의 시간 제한 값을 사용 합니다. 연결 시도의 나머지 부분 multiSubnetFailover 기능에서와 같은 논리를 따릅니다. 

> [!NOTE]  
Microsoft JDBC Driver 4.2를 사용 하 여 (또는 경우를 줄이려면) SQL Server에 대 한 한 경우 **multiSubnetFailover** 이 false 이면는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 첫 번째 IP 주소에 연결 하려고 시도 합니다. 경우는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 첫 번째 IP 주소로 연결이 실패 한 연결을 설정할 수 없습니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 서버와 연결 된 후속 IP 주소에 연결 하는 시도 하지 것입니다. 

  
> [!NOTE]  
>  연결 제한 시간을 늘리고 연결 재시도 논리를 구현하면 응용 프로그램이 가용성 그룹에 연결될 가능성이 증가합니다. 또한 가용성 그룹 장애 조치(failover)로 인해 연결이 실패할 수 있으므로 실패한 연결을 다시 연결할 때까지 다시 시도하는 연결 재시도 논리를 구현해야 합니다.  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover로 연결  
 항상 지정 **multiSubnetFailover = true** 의 가용성 그룹 수신기에 연결할 때는 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 가용성 그룹 또는 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 장애 조치 클러스터 인스턴스의 합니다. **multiSubnetFailover** 모든 가용성 그룹 및 장애 조치 클러스터 인스턴스에 대 한 보다 빠르게 장애 조치할 수 있도록 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 및 단일 및 다중 서브넷 AlwaysOn 토폴로지에 대 한 장애 조치 시간을 크게 저하 됩니다. 다중 서브넷 장애 조치(Failover) 중에는 클라이언트가 연결을 병렬로 시도합니다. 서브넷 장애 조치 동안는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] TCP 연결을 공격적으로 재시도 합니다.  
  
 **multiSubnetFailover** 가용성 그룹 또는 장애 조치 클러스터 인스턴스 및 사용 하는 응용 프로그램은 배포 되는 연결 속성 나타냅니다는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 주데이터베이스에연결하려고합니다[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 모든 IP에 연결 하려고 시도 하 여 인스턴스 주소입니다. 때 **MultiSubnetFailover = true** 연결에 대해 지정 된 클라이언트 운영 체제의 기본 TCP 재전송 간격 보다 빠르게 TCP 연결 시도 다시 시도 합니다. 이렇게 하면 AlwaysOn 가용성 그룹 또는 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스의 장애 조치(Failover) 후 더 빠르게 다시 연결할 수 있습니다. 이 설정은 단일/다중 서브넷 가용성 그룹 및 장애 조치(Failover) 클러스터 인스턴스에 모두 적용됩니다.  
  
 연결 문자열 키워드에 대 한 자세한 내용은 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], 참조 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
 지정 **multiSubnetFailover = true** 때 가용성 그룹 수신기 또는 장애 조치 클러스터 인스턴스 이외의 대상에 연결할 성능에 부정적인 영향이 있으며 지원 되지 않습니다.  
  
 보안 관리자가 설치되지 않은 경우 Java Virtual Machine은 기본적으로 JDK 구현 및 Java 속성 networkaddress.cache.ttl 및 networkaddress.cache.negative.ttl에 정의된 제한 시간 동안 VIP(가상 IP 주소)를 캐시합니다. JDK 보안 관리자가 설치된 경우 Java Virtual Machine은 VIP를 캐시하고 기본적으로 캐시를 새로 고치지 않습니다. Java Virtual Machine 캐시에 대해 "TTL(time-to-live)"(networkaddress.cache.ttl)을 1일로 설정해야 합니다. 기본값을 1일(정도)로 변경하지 않으면 VIP를 추가하거나 업데이트할 때 Java Virtual Machine 캐시에서 기존 값이 삭제되지 않습니다. Networkaddress.cache.ttl 및 networkaddress.cache.negative.ttl에 대 한 자세한 내용은 참조 [http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html](http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html)합니다.  
  
 다음 지침에 따라 장애 조치(Failover) 클러스터 인스턴스 또는 가용성 그룹의 서버에 연결하십시오.  
  
-   경우 드라이버에서 오류를 생성 합니다는 **instanceName** 연결 속성을 같은 연결 문자열에 사용 되는 **multiSubnetFailover** 연결 속성입니다. 이는 SQL Browser가 가용성 그룹에 사용되지 않는다는 사실을 반영합니다. 그러나 경우는 **portNumber** 연결 속성을 함께 지정, 드라이버는 무시 **instanceName** 사용 하 여 **portNumber**합니다.  
  
-   사용 하 여는 **multiSubnetFailover** 연결 속성을 단일 서브넷 또는 다중 서브넷에 연결할 때 두 경우 모두 성능이 향상 됩니다.  
  
-   가용성 그룹에 연결하려면 가용성 그룹에 대한 가용성 그룹 수신기를 연결 문자열의 서버로 지정합니다. 예를 들어, jdbc:sqlserver://VNN1입니다.  
  
-   IP 주소가 64개 이상으로 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스에 연결하면 연결 오류가 발생합니다.  
  
-   사용 하는 응용 프로그램의 동작에서 **multiSubnetFailover** 연결 속성이 인증 형식에 따라 영향을 받지 않습니다: [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인증, Kerberos 인증 또는 Windows 인증입니다.  
  
-   값 늘리기 **loginTimeout** 하 장애 조치 시간을 수용 하 고 응용 프로그램 연결 재시도 횟수를 줄입니다.  
  
-   분산 트랜잭션은 지원되지 않습니다.  
  
 읽기 전용 라우팅이 적용되지 않으면 다음과 같은 경우 가용성 그룹의 보조 복제본 위치에 대한 연결이 실패합니다.  
  
1.  보조 복제본 위치가 연결을 허용하도록 구성되어 있지 않은 경우  
  
2.  응용 프로그램에서 사용 하는 경우 **applicationIntent = ReadWrite** (아래 설명 참조) 보조 복제본 위치가 읽기 전용 액세스를 위해 구성 되어 있습니다.  
  
 주 복제본이 읽기 전용 작업을 거부하도록 구성되어 있고 연결 문자열에 **ApplicationIntent=ReadOnly**가 포함되어 있으면 연결이 실패합니다.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>데이터베이스 미러링에서 다중 서브넷 클러스터를 사용하도록 업그레이드  
 업그레이드 하는 경우는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 제거 해야 하는 다중 서브넷 시나리오에 데이터베이스 미러링을 사용 중인 응용 프로그램의 **failoverPartner** 연결 속성이로 바꿉니다 **multiSubnetFailover**  로 설정 **true** 가용성 그룹 수신기를 연결 문자열에서 서버 이름을 바꿉니다. 연결 문자열을 사용 하는 경우 **failoverPartner** 및 **multiSubnetFailover = true**, 드라이버에서 오류가 발생 합니다. 그러나 연결 문자열을 사용 하는 경우 **failoverPartner** 및 **multiSubnetFailover = false** (또는 **ApplicationIntent = ReadWrite**), 응용 프로그램에서는 데이터베이스를 사용 합니다. 미러링입니다.  
  
 드라이버는 AG의 주 데이터베이스에서 데이터베이스 미러링이 사용 되 고 오류가 반환 됩니다 **multiSubnetFailover = true** 대신 가용성 그룹에 주 데이터베이스에 연결 하는 연결 문자열에 사용 됩니다 수신기 수 있습니다.  
  
## <a name="specifying-application-intent"></a>응용 프로그램 의도 지정  
 때 **applicationIntent = ReadOnly**, 클라이언트는 AlwaysOn 사용 데이터베이스에 연결할 때 읽기 전용 작업을 요청 합니다. 서버는 연결 시간 및 USE 데이터베이스 문 동안 AlwaysOn이 활성화된 데이터베이스에만 의도를 시행합니다.  
  
 **applicationIntent** 키워드는 레거시, 읽기 전용 데이터베이스와 함께 작동 하지 않습니다.  
  
 데이터베이스는 대상 AlwaysOn 데이터베이스에 대한 읽기 작업을 허용하거나 허용하지 않을 수 있습니다. 이 작업은 **PRIMARY_ROLE** 및 **SECONDARY_ROLE**[!INCLUDE[tsql](../../includes/tsql_md.md)] 문의 **ALLOW_CONNECTIONS** 절로 수행됩니다.  
  
 **applicationIntent** 키워드는 읽기 전용 라우팅을 사용 하도록 설정 하는 데 사용 됩니다.  
  
## <a name="read-only-routing"></a>읽기 전용 라우팅  
 읽기 전용 라우팅은 데이터베이스의 읽기 전용 복제 가용성을 보장할 수 있는 기능입니다. 읽기 전용 라우팅을 활성화하려면:  
  
1.  AlwaysOn 가용성 그룹 가용성 그룹 수신기에 연결해야 합니다.  
  
2.  **applicationIntent** 연결 문자열 키워드도 설정 되어 있어야 **ReadOnly**합니다.  
  
3.  읽기 전용 라우팅을 설정하려면 데이터베이스 관리자가 가용성 그룹을 구성해야 합니다.  
  
 읽기 전용 라우팅을 사용하는 여러 연결 중 일부가 동일한 읽기 전용 복사본에 연결되지 않을 수 있습니다. 데이터베이스 동기화를 변경하거나 서버 라우팅 구성을 변경하면 클라이언트를 다른 읽기 전용 복사본에 연결할 수 있습니다. 모든 읽기 전용 요청이 동일한 읽기 전용 복제본에 연결 되도록 전달 하지 마십시오 가용성 그룹 수신기 또는 가상 IP 주소는 **serverName** 연결 문자열 키워드입니다. 대신, 읽기 전용 인스턴스의 이름을 지정합니다.  
  
 읽기 전용 라우팅은 먼저 기본 복제에 연결한 다음 가장 사용 가능한 읽기 가능 보조 복제를 찾으므로 읽기 전용 라우팅은 기본 복제에 연결하는 것보다 시간이 오래 걸릴 수 있습니다. 따라서 로그인 제한 시간을 늘려야 합니다.  
  
## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>multiSubnetFailover 및 applicationIntent를 지원하는 새 메서드  
 다음 방법에 대 한 프로그래밍 방식의 액세스를 제공 된 **multiSubnetFailover**, **applicationIntent** 및 **transparentNetworkIPResolution** 연결 문자열 키워드:  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 **getMultiSubnetFailover**, **setMultiSubnetFailover**, **getApplicationIntent**, **setApplicationIntent**, **getTransparentNetworkIPResolution** 및 **setTransparentNetworkIPResolution** 메서드를 추가 [SQLServerDataSource 클래스](../../connect/jdbc/reference/sqlserverdatasource-class.md), [ SQLServerConnectionPoolDataSource 클래스](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md), 및 [SQLServerXADataSource 클래스](../../connect/jdbc/reference/sqlserverxadatasource-class.md)합니다.  
  
## <a name="ssl-certificate-validation"></a>SSL 인증서의 유효성 검사  
 가용성 그룹은 여러 물리적 서버로 구성되어 있습니다. [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]에 대 한 지원을 추가 **주체 대체 이름** 여러 호스트가 같은 인증서와 연결 될 수 있도록 SSL 인증서에 있습니다. SSL에 대 한 자세한 내용은 참조 하십시오. [SSL 지원 이해](../../connect/jdbc/understanding-ssl-support.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버와 함께 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)  
  
  

