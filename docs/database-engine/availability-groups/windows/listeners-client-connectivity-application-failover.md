---
title: 가용성 그룹 수신기에 연결
description: 주 복제본 및 읽기 전용 보조 복제본에 연결하는 방법, TLS/SSL 및 Kerberos를 사용하는 방법 등 Always On 가용성 그룹 수신기에 연결하는 방법에 대한 정보를 포함합니다.
ms.custom: seodec18
ms.date: 02/27/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c60b0dbb40c41a7d41971bffc0f44b89ad77eaaa
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882734"
---
# <a name="connect-to-an-always-on-availability-group-listener"></a>Always On 가용성 그룹 수신기에 연결 
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  
[가용성 그룹 수신기를 구성](create-or-configure-an-availability-group-listener-sql-server.md)한 후에는 연결 문자열을 업데이트하여 Always On 가용성 그룹 수신기에 연결해야 합니다. 그러면 장애 조치(failover)할 때마다 뒤이어 연결 문자열을 수동으로 업데이트하지 않고도 애플리케이션의 트래픽이 의도한 복제본으로 자동 라우팅됩니다. 
  

##  <a name="connect-to-the-primary-replica"></a><a name="ConnectToPrimary"></a> 주 복제본에 연결  

읽기/쓰기 권한을 허용하는 주 복제본에 연결하려면 연결 문자열에서 가용성 그룹 수신기 DNS 이름을 지정합니다. 

예를 들어 수신기를 통해 SQL Server Management Studio의 주 복제본에 연결하려면 서버 이름 필드에 수신기 DNS 이름을 입력합니다. 

![SSMS에서 수신기에 연결](media/listeners-client-connectivity-application-failover/connect-to-listener-in-ssms.png)


장애 조치(failover) 중에 주 복제본이 변경되면 기존의 수신기 연결이 끊어지고, 새 연결은 새로운 주 복제본으로 라우팅됩니다.  

ADO.NET 공급자(System.Data.SqlClient) 기본 연결 문자열의 예: 
  
```  
Server=tcp: AGListener,1433;Database=MyDB;Integrated Security=SSPI  
```  

다음 T-SQL(Transact-SQL) 명령을 실행하여 수신기를 통해 현재 연결된 복제본을 확인할 수 있습니다.

```sql
SELECT @@SERVERNAME
```

예를 들어 SQLVM1이 주 복제본인 경우 다음과 같습니다. 

![복제본 연결 확인](media/listeners-client-connectivity-application-failover/replica-server-name.png)


가용성 그룹 수신기를 사용하는 대신, 주 복제본 또는 보조 복제본의 인스턴스 이름을 사용하여 SQL Server 인스턴스에 직접 연결할 수 있습니다. 그러나 새 연결이 현재의 새로운 주 복제본에 자동으로 라우팅되는 기능을 사용할 수 없습니다. 또한 `read-intent`로 지정된 연결이 읽기 가능한 보조 복제본으로 자동 라우팅되는 읽기 전용 라우팅도 사용할 수 없습니다. 

##  <a name="connect-to-a-read-only-replica"></a><a name="ConnectToSecondary"></a> 읽기 전용 복제본에 연결 

_읽기 전용 라우팅_은 읽기 전용 워크로드를 허용하도록 구성된 읽기 가능한 보조 복제본으로 들어오는 수신기 연결을 자동 라우팅하는 기능을 말합니다. 

다음 조건이 충족되면 연결이 읽기 전용 복제본으로 자동 라우팅됩니다. 
 
-   하나 이상의 보조 복제본이 읽기 전용 액세스로 설정되었으며 각 읽기 전용 보조 복제본과 주 복제본은 [읽기 전용 라우팅을 지원하도록 구성](configure-read-only-routing-for-an-availability-group-sql-server.md)되었습니다. 

-   연결 문자열은 가용성 그룹에 포함된 데이터베이스를 참조합니다. 이 방법의 대안으로, 연결에 사용되는 로그인에는 데이터베이스가 기본 데이터베이스로 구성되어 있습니다. 자세한 내용은 [알고리즘이 읽기 전용 라우팅을 사용하는 방법에 대한 문서](https://blogs.msdn.microsoft.com/mattn/2012/04/25/calculating-read_only_routing_url-for-alwayson/)를 참조하세요.

-   연결 문자열은 가용성 그룹 수신기를 참조하며 들어오는 연결의 애플리케이션 의도는 ODBC 또는 OLEDB 연결 문자열이나 연결 특성 또는 속성에서 **Application Intent=ReadOnly** 키워드를 사용하는 등과 같은 방법으로 읽기 전용으로 설정됩니다. 

애플리케이션 의도 특성은 로그인 중에 클라이언트의 세션에 저장됩니다. 그러면 SQL Server의 인스턴스에서 이 의도를 처리하고 보조 복제본에 있는 대상 데이터베이스의 현재 읽기/쓰기 상태와 가용성 그룹의 구성에 따라 수행할 작업을 결정합니다.  

예를 들어 SQL Server Management Studio를 사용하여 읽기 전용 복제본에 연결하려면 **서버에 연결** 대화 상자에서 **옵션**을 선택하고 **추가 연결 매개 변수** 탭을 선택한 다음, 텍스트 상자에 `ApplicationIntent=ReadOnly`를 지정합니다.

![SSMS의 읽기 전용 연결](media/listeners-client-connectivity-application-failover/read-only-intent-in-ssms.png)
  
읽기 전용 애플리케이션 의도를 지정하는 ADO.NET 공급자(System.Data.SqlClient) 연결 문자열의 예: 

```  
Server=tcp:AGListener;Database=AdventureWorks;Integrated Security=SSPI;ApplicationIntent=ReadOnly  
```  
  
자세한 내용은 [가용성 복제본에 대한 읽기 전용 권한 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)을 참조하세요.  

## <a name="non-default-port"></a>기본이 아닌 포트

수신기를 만들 때 수신기에서 사용할 포트를 지정합니다. 포트가 기본 포트인 1433인 경우에는 수신기에 연결할 때 포트 번호를 지정할 필요가 없습니다. 그러나 포트가 1433이 아닌 경우 다음과 같이 연결 문자열에서 포트를 `listenername,port` 형식으로 지정해야 합니다.

![기본이 아닌 포트를 사용하여 연결](media/listeners-client-connectivity-application-failover/specify-port-in-ssms.png)

수신기에서 사용할 기본이 아닌 포트를 지정하는 ADO.NET 공급자(System.Data.SqlClient) 연결 문자열의 예: 

```  
Server=tcp:AGListener,1445;Database=AdventureWorks;Integrated Security=SSPI 
```  

##  <a name="bypass-listeners"></a><a name="BypassAGl"></a> 수신기 무시:  

가용성 그룹 수신기에서 장애 조치(Failover) 리디렉션 및 읽기 전용 라우팅을 지원하지만 클라이언트 연결에서 해당 기능을 사용할 필요는 없습니다. 클라이언트 연결에서 가용성 그룹 수신기에 연결하는 대신 SQL Server의 인스턴스를 직접 참조할 수도 있습니다.  
  
SQL Server의 인스턴스에서 가용성 그룹 수신기를 사용하거나 다른 인스턴스 엔드포인트를 사용하여 연결이 로그인되는지 여부는 관계가 없습니다.  SQL Server 인스턴스는 대상 데이터베이스의 상태를 확인하고 가용성 그룹의 구성과 인스턴스에 대한 데이터베이스의 현재 상태를 기반으로 연결을 허용하거나 허용하지 않습니다.  예를 들어 클라이언트 애플리케이션이 SQL Server 포트의 인스턴스에 직접 연결하고 가용성 그룹에 호스팅된 대상 데이터베이스에 연결하고 대상 데이터베이스가 기본 온라인 상태인 경우 연결이 성공합니다.  대상 데이터베이스가 오프라인 상태이거나 전환 상태이면 데이터베이스 연결이 실패합니다.  
  
보조 복제본이 하나만 있고 사용자 연결을 허용하는 않는 경우 데이터베이스 미러링을 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]로 마이그레이션하는 동안 애플리케이션에서 데이터베이스 미러링 연결 문자열을 지정할 수 있습니다. 

##  <a name="database-mirroring-connection-strings"></a><a name="DbmConnectionString"></a> 데이터베이스 미러링 연결 문자열 
 가용성 그룹에 보조 복제본이 하나만 있고 보조 복제본에 대해 ALLOW_CONNECTIONS = READ_ONLY 또는 ALLOW_CONNECTIONS = NONE으로 구성되어 있으면, 클라이언트에서 데이터베이스 미러링 연결 문자열을 사용하여 주 복제본에 연결할 수 있습니다. 가용성 그룹에 두 개의 가용성 복제본(주 복제본과 보조 복제본)만 포함되도록 제한한 경우 이 방법은 데이터베이스 미러링의 기존 애플리케이션을 가용성 그룹으로 마이그레이션하는 데 유용합니다. 보조 복제본을 더 추가하려면 가용성 그룹의 가용성 그룹 수신기를 만들고 가용성 그룹 수신기 DNS 이름을 사용하도록 애플리케이션을 업데이트해야 합니다.  
  
 데이터베이스 미러링 연결 문자열을 사용할 경우 클라이언트에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client나 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용할 수 있습니다. 연결하려는 가용성 복제본을 처음에 호스팅할 서버 인스턴스를 식별하려면 클라이언트가 제공하는 연결 문자열에 최소한 하나의 서버 인스턴스 이름, 즉 *초기 파트너 이름*이 있어야 합니다. 필요한 경우 연결 문자열에 다른 서버 인스턴스의 이름, 즉 *장애 조치(failover) 파트너 이름*을 제공하여 초기에 보조 복제본을 호스팅할 서버 인스턴스를 장애 조치(failover) 파트너 이름으로 식별할 수도 있습니다.  
  
 데이터베이스 미러링 연결 문자열에 대한 자세한 내용은 [데이터베이스 미러링 세션에 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)을 참조하세요.  
  
  
##  <a name="multi-subnet-failovers"></a><a name="SupportAgMultiSubnetFailover"></a> 다중 서브넷 장애 조치(failover)  
 
 연결 문자열에서 MultiSubnetFailover 연결 옵션을 지원하는 클라이언트 라이브러리를 사용 중인 경우, 사용하는 공급자의 구문에 따라 MultiSubnetFailover를 “True” 또는 “Yes”로 설정하여 다른 서브넷에 대한 가용성 그룹 장애 조치(failover)를 최적화할 수 있습니다.  
  
> [!NOTE]  
>  가용성 그룹 수신기와 SQL Server 장애 조치(Failover) 클러스터 인스턴스 이름에 대한 단일 및 다중 서브넷 연결 모두에 대해 이 설정을 사용하는 것이 좋습니다.  이 옵션을 사용하면 단일 서브넷 시나리오에 대해서도 최적화가 추가됩니다.  
  
 **MultiSubnetFailover** 연결 옵션은 TCP 네트워크 프로토콜에 대해서만 작동하며 가용성 그룹 수신기에 연결할 때 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에 연결하는 모든 가상 네트워크 이름에 대해서만 지원됩니다.  
  
 다중 서브넷 장애 조치를 사용할 수 있게 하는 ADO.NET 공급자(System.Data.SqlClient) 연결 문자열의 예제는 다음과 같습니다.  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;Integrated Security=SSPI; MultiSubnetFailover=True  
```  
  
 가용성 그룹이 단일 서브넷에 대해서만 적용되는 경우에도 **MultiSubnetFailover** 연결 옵션을 **True** 로 설정해야 합니다.  그러면 나중에 클라이언트 연결 문자열을 변경하지 않고도 서브넷 확장을 지원하도록 새 클라이언트를 미리 구성하여 단일 서브넷 장애 조치(failover)에 대한 장애 조치(failover) 성능을 최적화할 수 있습니다.  **MultiSubnetFailover** 연결 옵션은 필수가 아니지만 서브넷 장애 조치(failover) 시간을 단축하는 이점이 있습니다.  클라이언트 드라이버가 가용성 그룹과 병렬로 연결된 각 IP 주소에 대해 TCP 소켓을 열려고 하기 때문입니다.  클라이언트 드라이버는 첫 번째 IP가 응답할 때까지 기다린 다음 성공적으로 응답하면 해당 IP를 사용하여 연결합니다.  
  
##  <a name="listeners--tlsssl-certificates"></a><a name="SSLcertificates"></a> 수신기 및 TLS/SSL 인증서  

가용성 그룹 수신기에 연결할 때 SQL Server의 참여 인스턴스에서 TLS/SSL 인증서를 세션 암호화와 함께 사용하는 경우 암호화를 적용하려면 연결하는 클라이언트 드라이버가 TLS/SSL 인증서에서 Subject Alternate 이름을 지원해야 합니다.  인증서 Subject Alternative 이름에 대한 SQL Server 드라이버 지원은 ADO.NET(SqlClient), Microsoft JDBC 및 SNAC(SQL Native Client)에 포함될 계획입니다.  
  
인증서의 Subject Alternate 이름에 모든 가용성 그룹 수신기 목록을 설정하여 참여하는 각 서버 노드에 대해 X.509 인증서를 구성해야 합니다. 

인증서 값의 형식은 다음과 같습니다. 

```  
CN = Server.FQDN  
SAN = Server.FQDN,Listener1.FQDN,Listener2.FQDN
```

예를 들어 다음과 같은 값이 있다고 가정합니다. 

```
Servername: Win2019   
Instance: SQL2019   
AG: AG2019   
Listener: Listener2019   
Domain: contoso.com  (which is also the FQDN)
```

단일 가용성 그룹을 포함하는 WSFC의 경우 인증서는 서버의 FQDN(정규화된 도메인 이름)과 수신기의 FQDN을 포함해야 합니다. 

```
CN: Win2019.contoso.com
SAN: Win2019.contoso.com, Listener2019.contoso.com 
```

이 구성을 사용하면 인스턴스(`WIN2019\SQL2019`) 또는 수신기(`Listener2019`)에 연결할 때 연결이 암호화됩니다. 

네트워킹이 구성된 방식에 따라, SAN에 NetBIOS를 추가해야 할 수 있는 작은 고객 하위 집합이 있습니다. 이 경우 인증서 값은 다음과 같아야 합니다. 

```
CN: Win2019.contoso.com
SAN: Win2019,Win2019.contoso.com,Listener2019,Listener2019.contoso.com
```

WSFC에 다음과 같은 세 개의 가용성 그룹 수신기가 있는 경우 (Listener1, Listener2, Listener3)

인증서 값은 다음과 같아야 합니다. 

```
CN: Win2019.contoso.com
SAN: Win2019.contoso.com,Listener1.contoso.com,Listener2.contoso.com,Listener3.contoso.com
```
  
  
##  <a name="listeners-and-kerberos-spns"></a><a name="SPNs"></a> 수신기 및 Kerberos(SPN) 

도메인 관리자가 수신기에 대한 클라이언트 연결에 Kerberos를 사용하도록 설정하려면 Active Directory에서 각 가용성 그룹 수신기의 SPN(서비스 사용자 이름)을 구성해야 합니다. SPN을 등록할 때 가용성 복제본을 호스트하는 서버 인스턴스의 서비스 계정을 사용해야 합니다. SPN을 모든 복제본에 대해 사용하려면 가용성 그룹을 호스팅하는 WSFC 클러스터의 모든 인스턴스에 대해 동일한 서비스 계정을 사용해야 합니다.  
  
 **setspn** Windows 명령줄 도구를 사용하여 SPN을 구성할 수 있습니다.  예를 들어 `AG1listener.Adventure-Works.com` 도메인 계정에서 실행하도록 구성된 모든 SQL Server 인스턴스 집합에 호스팅되는 `corp/svclogin2`이라는 가용성 그룹에 대한 SPN을 구성하려면  
  
```  
setspn -A MSSQLSvc/AG1listener.Adventure-Works.com:1433 corp/svclogin2  
```  
  
 SQL Server에 대한 SPN을 수동으로 등록하는 방법은 [Kerberos 연결의 서비스 사용자 이름 등록](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)을 참조하세요.  
  


## <a name="next-steps"></a>다음 단계

수신기에 연결되면 [읽기 전용 워크로드](overview-of-always-on-availability-groups-sql-server.md) 및 [백업](configure-backup-on-availability-replicas-sql-server.md)을 보조 복제본으로 오프로드하여 성능을 향상하는 것이 좋습니다. 다양한 [가용성 그룹 모니터링 전략](monitoring-of-availability-groups-sql-server.md)을 검토하여 가용성 그룹의 상태를 확인할 수도 있습니다. 

가용성 그룹에 대한 자세한 내용은 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요. 
