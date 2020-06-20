---
title: 고가용성, 재해 복구를 위한 SQL Server Native Client 지원 | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2b06186b-4090-4728-b96b-90d6ebd9f66f
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f2909747ba42aaa3ff5c07777149fbcff5500f4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011184"
---
# <a name="sql-server-native-client-support-for-high-availability-disaster-recovery"></a>고가용성 재해 복구를 위한 SQL Server Native Client 지원
  이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client 지원([!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 추가됨)에 대해 설명합니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(Failover)&#40;SQL Server&#41;](../../../database-engine/listeners-client-connectivity-application-failover.md), [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [장애 조치(Failover) 클러스터링 및 AlwaysOn 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) 및 [활성 보조: 읽기 가능한 보조 복제본(AlwaysOn 가용성 그룹)](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)을 참조하세요.  
  
 연결 문자열에서 특정 AG(가용성 그룹)에 대한 가용성 그룹 수신기를 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 애플리케이션이 장애 조치(Failover)되는 가용성 그룹의 데이터베이스에 연결된 경우, 원래 연결은 끊어지며 장애 조치 후 애플리케이션이 계속 작동하려면 새 연결을 열어야 합니다.  
  
 가용성 그룹 수신기에 연결하지 않았고 여러 IP 주소가 호스트 이름과 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 DNS 항목과 연결된 모든 IP 주소를 순차적으로 반복합니다. DNS 서버가 반환한 첫 번째 IP 주소가 NIC(네트워크 인터페이스 카드)에 바인딩되지 않은 경우 시간이 오래 걸릴 수 있습니다. 가용성 그룹 수신기에 연결할 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 모든 IP 주소에 대한 연결을 병렬로 시도하고, 그 중 한 연결 시도가 성공하면 드라이버가 보류 중인 모든 연결 시도를 삭제합니다.  
  
> [!NOTE]  
>  연결 제한 시간을 늘리고 연결 재시도 논리를 구현하면 애플리케이션이 가용성 그룹에 연결될 가능성이 증가합니다. 또한 가용성 그룹 장애 조치(failover)로 인해 연결이 실패할 수 있으므로 실패한 연결을 다시 연결할 때까지 다시 시도하는 연결 재시도 논리를 구현해야 합니다.  
  
## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover로 연결  
 SQL Server 2012 가용성 그룹 수신기 또는 SQL Server 2012 장애 조치(Failover) 클러스터 인스턴스에 연결할 때는 항상 `MultiSubnetFailover=Yes`를 지정하십시오. `MultiSubnetFailover`를 사용하면 SQL Server 2012에서 모든 가용성 그룹 및 장애 조치(Failover) 클러스터 인스턴스에 대한 장애 조치(Failover)를 빠르게 수행하고 단일 및 다중 서브넷 AlwaysOn 토폴로지에 대한 장애 조치(Failover) 시간을 크게 줄일 수 있습니다. 다중 서브넷 장애 조치(Failover) 중에는 클라이언트가 연결을 병렬로 시도합니다. 서브넷 장애 조치(Failover) 중에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 적극적으로 TCP 연결을 다시 시도합니다.  
  
 `MultiSubnetFailover` 연결 속성은 애플리케이션을 가용성 그룹 또는 장애 조치(Failover) 클러스터 인스턴스에 배치하는 중이고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 모든 IP 주소에 연결을 시도하여 주 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 데이터베이스에 연결을 시도함을 나타냅니다. `MultiSubnetFailover=Yes`연결에 대해를 지정 하면 클라이언트는 운영 체제의 기본 tcp 재전송 간격 보다 빠르게 TCP 연결을 다시 시도 합니다. 이렇게 하면 AlwaysOn 가용성 그룹 또는 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스의 장애 조치(Failover) 후 더 빠르게 다시 연결할 수 있습니다. 이 설정은 단일/다중 서브넷 가용성 그룹 및 장애 조치(Failover) 클러스터 인스턴스에 모두 적용됩니다.  
  
 연결 문자열 키워드에 대한 자세한 내용은 [SQL Server Native Client에서 연결 문자열 키워드 사용](../applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하세요.  
  
 가용성 그룹 수신기 또는 장애 조치(Failover) 클러스터 인스턴스 이외의 다른 항목에 연결할 때 `MultiSubnetFailover=Yes`를 지정하면 성능에 상당히 부정적인 영향을 줄 수 있으므로 이러한 설정은 지원되지 않습니다.  
  
 다음 지침에 따라 장애 조치(Failover) 클러스터 인스턴스 또는 가용성 그룹의 서버에 연결하십시오.  
  
-   단일 또는 다중 서브넷에 연결할 때 `MultiSubnetFailover` 연결 속성을 사용하십시오. 그러면 두 경우 모두 성능이 향상됩니다.  
  
-   가용성 그룹에 연결하려면 가용성 그룹에 대한 가용성 그룹 수신기를 연결 문자열의 서버로 지정합니다.  
  
-   IP 주소가 64개 이상으로 구성된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 연결 오류가 발생합니다.  
  
-   연결 속성을 사용 하는 응용 프로그램의 동작은 인증 `MultiSubnetFailover` 유형 ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증, Kerberos 인증 또는 Windows 인증)에 따라 영향을 받지 않습니다.  
  
-   장애 조치(Failover) 시간을 수용하고 애플리케이션 연결 재시도 횟수를 줄이기 위해 `loginTimeout` 값을 늘릴 수 있습니다.  
  
-   분산된 트랜잭션은 지원되지 않습니다.  
  
 읽기 전용 라우팅이 적용되지 않으면 다음과 같은 경우 가용성 그룹의 보조 복제본 위치에 대한 연결이 실패합니다.  
  
1.  보조 복제본 위치가 연결을 허용하도록 구성되어 있지 않은 경우  
  
2.  애플리케이션에서 `ApplicationIntent=ReadWrite`(아래 설명 참조)를 사용하고 보조 복제본 위치가 읽기 전용 액세스용으로 구성되어 있는 경우  
  
 주 복제본이 읽기 전용 작업을 거부하도록 구성되어 있고 연결 문자열에 `ApplicationIntent=ReadOnly`가 포함되어 있으면 연결이 실패합니다.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>데이터베이스 미러링에서 다중 서브넷 클러스터를 사용하도록 업그레이드  
 연결 문자열에 `MultiSubnetFailover` 및 `Failover_Partner` 연결 키워드가 있으면 연결 오류가 발생합니다. `MultiSubnetFailover`가 사용되고[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 데이터베이스 미러링 쌍의 일부임을 나타내는 장애 조치(Failover) 파트너 응답을 반환하는 경우에도 오류가 발생합니다.  
  
 현재 데이터베이스 미러링을 사용 중인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 애플리케이션을 다중 서브넷 시나리오로 업그레이드할 경우에는 `Failover_Partner` 연결 속성을 제거하고 이를 `MultiSubnetFailover`로 설정된 `Yes`로 바꾸고, 연결 문자열에서 서버 이름을 가용성 그룹 수신기로 바꿔야 합니다. 연결 문자열에 `Failover_Partner` 및 `MultiSubnetFailover=Yes`가 사용될 경우 드라이버에서 오류가 발생합니다. 하지만 연결 문자열에 `Failover_Partner` 및 `MultiSubnetFailover=No`(또는 `ApplicationIntent=ReadWrite`)가 사용될 경우 애플리케이션에 데이터베이스 미러링이 사용됩니다.  
  
 가용성 그룹의 주 데이터베이스에서 데이터베이스 미러링이 사용되고 가용성 그룹 수신기가 아닌 주 데이터베이스에 연결하는 연결 문자열에 `MultiSubnetFailover=Yes`가 사용될 경우 드라이버에서 오류를 반환합니다.  
  
## <a name="specifying-application-intent"></a>애플리케이션 의도 지정  
 `ApplicationIntent=ReadOnly`인 경우 클라이언트는 AlwaysOn이 설정된 데이터베이스에 연결할 때 읽기 작업을 요청합니다. 서버는 연결 시 그리고 USE 데이터베이스 문 중에 AlwaysOn이 설정된 데이터베이스에 한하여 의도를 강제 적용합니다.  
  
 `ApplicationIntent` 키워드는 레거시 읽기 전용 데이터베이스에 적용되지 않습니다.  
  
 데이터베이스는 대상 AlwaysOn 데이터베이스에 대한 읽기 작업을 허용하거나 허용하지 않을 수 있습니다. `ALLOW_CONNECTIONS` 및 `PRIMARY_ROLE``SECONDARY_ROLE` 문의 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 절을 사용하여 이를 수행할 수 있습니다.  
  
 `ApplicationIntent` 키워드는 읽기 전용 라우팅을 설정하는 데 사용됩니다.  
  
## <a name="read-only-routing"></a>읽기 전용 라우팅  
 읽기 전용 라우팅은 데이터베이스의 읽기 전용 복사본의 가용성을 유지할 수 있는 기능입니다. 읽기 전용 라우팅을 활성화하려면:  
  
1.  AlwaysOn 가용성 그룹의 가용성 그룹 수신기에 연결해야 합니다.  
  
2.  `ApplicationIntent` 연결 문자열 키워드를 `ReadOnly`로 설정해야 합니다.  
  
3.  읽기 전용 라우팅을 설정하려면 데이터베이스 관리자가 가용성 그룹을 구성해야 합니다.  
  
 읽기 전용 라우팅을 사용하는 여러 연결 중 일부가 동일한 읽기 전용 복사본에 연결되지 않을 수 있습니다. 데이터베이스 동기화를 변경하거나 서버 라우팅 구성을 변경하면 클라이언트를 다른 읽기 전용 복사본에 연결할 수 있습니다. 모든 읽기 전용 요청을 동일한 읽기 전용 복제본에 연결하려면 가용성 그룹 수신기를 `Server` 연결 문자열 키워드에 전달하지 마십시오. 대신, 읽기 전용 인스턴스의 이름을 지정합니다.  
  
 읽기 전용 라우팅은 먼저 주 데이터베이스에 연결한 후 사용 가능한 최선의 읽기 가능한 보조 데이터베이스를 검색하기 때문에 주 데이터베이스에 연결할 때보다 시간이 더 많이 걸릴 수 있습니다. 따라서 로그인 제한 시간을 늘려야 합니다.  
  
## <a name="odbc"></a>ODBC  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] Native Client에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]을 지원하기 위해 다음과 같은 두 개의 ODBC 연결 문자열 키워드가 추가되었습니다.  
  
-   `ApplicationIntent`  
  
-   `MultiSubnetFailover`  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 ODBC 연결 문자열 키워드에 대한 자세한 내용은 [SQL Server Native Client에서 연결 문자열 키워드 사용](../applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하세요.  
  
 해당하는 연결 속성은 다음과 같습니다.  
  
-   `SQL_COPT_SS_APPLICATION_INTENT`  
  
-   `SQL_COPT_SS_MULTISUBNET_FAILOVER`  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 ODBC 연결 속성에 대한 자세한 내용은 [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서부터 `ApplicationIntent` 및 `MultiSubnetFailover` 키워드의 기능은 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client 드라이버를 사용하는 DSN의 ODBC 데이터 원본 관리자에서 노출됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 애플리케이션에서는 다음 세 가지 함수 중 하나를 사용하여 연결할 수 있습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|[SQLBrowseConnect](../../native-client-odbc-api/sqlbrowseconnect.md)|`SQLBrowseConnect`에서 반환되는 서버 목록에는 VNN이 포함되지 않습니다. 서버가 독립 실행형 서버인지, 아니면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대해 사용하도록 설정된 둘 이상의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인스턴스를 포함하는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 클러스터의 주 또는 보조 서버인지는 표시되지 않고 서버 목록만 표시됩니다. 서버에 연결한 후 오류가 발생할 경우에는 서버에 연결은 되었지만 `ApplicationIntent` 설정이 서버 구성과 호환되지 않기 때문일 수 있습니다.<br /><br /> `SQLBrowseConnect`는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대해 사용하도록 설정된 둘 이상의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인스턴스를 포함하는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 클러스터의 서버를 인식하지 않으므로 `SQLBrowseConnect`는 `MultiSubnetFailover` 연결 문자열 키워드를 무시합니다.|  
|[SQLConnect](../../native-client-odbc-api/sqlconnect.md)|`SQLConnect`는 DSN(데이터 원본 이름) 또는 연결 속성을 통해 `ApplicationIntent`와 `MultiSubnetFailover`를 모두 지원합니다.|  
|[SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md)|`SQLDriverConnect`는 연결 문자열 키워드, 연결 속성 또는 DSN을 통해 `ApplicationIntent` 및 `MultiSubnetFailover`를 지원합니다.|  
  
## <a name="ole-db"></a>OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 OLE DB는 `MultiSubnetFailover` 키워드를 지원하지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client의 OLE DB는 애플리케이션 의도를 지원합니다. 애플리케이션 의도는 OLE DB 애플리케이션에 대해 ODBC 애플리케이션과 동일하게 동작합니다(위의 내용 참조).  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] Native Client에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]을 지원하기 위해 다음과 같은 하나의 OLE DB 연결 문자열 키워드가 추가되었습니다.  
  
-   `Application Intent`  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 연결 문자열 키워드에 대한 자세한 내용은 [SQL Server Native Client에서 연결 문자열 키워드 사용](../applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하세요.  
  
 해당하는 연결 속성은 다음과 같습니다.  
  
-   `SSPROP_INIT_APPLICATIONINTENT`  
  
-   `DBPROP_INIT_PROVIDERSTRING`  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 애플리케이션에서는 다음 메서드 중 하나를 사용하여 애플리케이션 의도를 지정할 수 있습니다.  
  
 `IDBInitialize::Initialize`  
 `IDBInitialize::Initialize`는 이전에 구성한 속성 집합을 사용하여 데이터 원본을 초기화하고 데이터 원본 개체를 만듭니다. 애플리케이션 의도를 공급자 속성 또는 확장 속성 문자열의 일부로 지정합니다.  
  
 `IDataInitialize::GetDataSource`  
 `IDataInitialize::GetDataSource`는 `Application Intent` 키워드를 포함할 수 있는 입력 연결 문자열을 받아들입니다.  
  
 `IDBProperties::GetProperties`  
 `IDBProperties::GetProperties`는 현재 데이터 원본에 설정된 속성 값을 검색합니다.  DBPROP_INIT_PROVIDERSTRING 속성과 SSPROP_INIT_APPLICATIONINTENT 속성을 통해 `Application Intent` 값을 검색할 수 있습니다.  
  
 `IDBProperties::SetProperties`  
 `ApplicationIntent` 속성 값을 설정하려면 값이 "`IDBProperties::SetProperties`" 또는 "`SSPROP_INIT_APPLICATIONINTENT`"인 `ReadWrite` 속성이나 값에 "`ReadOnly`" 또는 "`DBPROP_INIT_PROVIDERSTRING`"를 포함하는 `ApplicationIntent=ReadOnly` 속성을 전달하여 `ApplicationIntent=ReadWrite`를 호출합니다.  
  
 **데이터 연결 속성** 대화 상자의 모두 탭에 있는 애플리케이션 의도 속성 필드에서 애플리케이션 의도를 지정할 수 있습니다.  
  
 암시적 연결을 설정하면 암시적 연결이 부모 연결의 애플리케이션 의도 설정을 사용합니다. 마찬가지로 동일한 데이터 원본에서 만들어진 여러 개의 세션은 데이터 원본의 애플리케이션 의도 설정을 상속합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](sql-server-native-client-features.md)   
 [SQL Server Native Client에서 연결 문자열 키워드 사용](../applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
  
