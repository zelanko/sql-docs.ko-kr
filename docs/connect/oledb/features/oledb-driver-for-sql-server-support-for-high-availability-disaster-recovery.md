---
title: OLE DB Driver for SQL Server Support for High Availability, Disaster Recovery | Microsoft Docs
description: OLE DB Driver for SQL Server 고가용성, 재해 복구에 대 한 지원
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c915af2ec748c4b2c15882c9a643c8e200442e98
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="ole-db-driver-for-sql-server-support-for-high-availability-disaster-recovery"></a>OLE DB Driver for SQL Server Support for High Availability, Disaster Recovery
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 문서에서는 SQL Server 지원에 대 한 OLE DB Driver 설명 (에 추가 된 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)])에 대 한 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]합니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(Failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md), [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [장애 조치(Failover) 클러스터링 및 AlwaysOn 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) 및 [활성 보조: 읽기 가능한 보조 복제본&#40;AlwaysOn 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)을 참조하세요.  
  
 연결 문자열에서 특정 AG(가용성 그룹)에 대한 가용성 그룹 수신기를 지정할 수 있습니다. OLE DB Driver for SQL Server 응용 프로그램 장애 조치 되 가용성 그룹의 데이터베이스에 연결 되 면 원래 연결이 끊어지고, 및 응용 프로그램 장애 조치 후 작업을 계속 하려면 새 연결을 열어야 합니다.  
  
 가용성 그룹 수신기에 연결 하지 경우와 여러 IP 주소가 호스트 이름에 연결 되어 있는 경우 OLE DB Driver for SQL Server가 DNS 항목과 연결 된 모든 IP 주소 순차적으로 반복 합니다. DNS 서버가 반환한 첫 번째 IP 주소가 NIC(네트워크 인터페이스 카드)에 바인딩되지 않은 경우 시간이 오래 걸릴 수 있습니다. 가용성 그룹 수신기에 연결할 때 OLE DB Driver for SQL Server에 병렬 모든 IP 주소에 대 한 연결을 설정 하 고 연결 시도가 성공 하면 드라이버는 보류 중인 연결 시도 삭제 합니다.  
  
> [!NOTE]  
> 연결 제한 시간을 늘리고 연결 재시도 논리를 구현하면 응용 프로그램이 가용성 그룹에 연결될 가능성이 증가합니다. 또한 가용성 그룹 장애 조치(failover)로 인해 연결이 실패할 수 있으므로 실패한 연결을 다시 연결할 때까지 다시 시도하는 연결 재시도 논리를 구현해야 합니다.  
  
## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover로 연결  
 항상 지정 **MultiSubnetFailover = Yes** SQL Server Always On 가용성 그룹 수신기에 연결할 때 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치 클러스터 인스턴스의 합니다. **MultiSubnetFailover** 모든 Always On 가용성 그룹 및 장애 조치 클러스터 인스턴스에 대 한 보다 빠르게 장애 조치할 수 있도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 및 토폴로지에 대 한 단일 및 다중 서브넷 Always On 장애 조치 시간을 크게 저하 됩니다. 다중 서브넷 장애 조치(Failover) 중에는 클라이언트가 연결을 병렬로 시도합니다. 서브넷 장애 조치 하는 동안 OLE DB Driver for SQL Server는 TCP 연결을 다시 시도 합니다.  
  
 **MultiSubnetFailover** 연결 속성을 응용 프로그램 장애 조치 클러스터 인스턴스 또는 가용성 그룹에 배포 되 고 해당 OLE DB Driver for SQL Server는 데이터베이스에 연결 하려고 나타냅니다는 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 모든 IP에 연결 하려고 시도 하 여 인스턴스 주소입니다. 연결에 대해 **MultiSubnetFailover=Yes**를 지정하면 클라이언트는 운영 체제의 기본 TCP 재전송 간격보다 빠르게 TCP 연결을 다시 시도합니다. 이 Always On 가용성 그룹 또는 장애 조치 클러스터 인스턴스의 장애 조치 후 더 빠르게 다시 연결할 수 있도록 하며 모두 단일 및 다중 서브넷 가용성 그룹과 장애 조치 클러스터 인스턴스에 적용 합니다.  
  
 연결 문자열 키워드에 대 한 자세한 내용은 참조 [OLE DB 드라이버와 SQL Server에 대 한 연결 문자열 키워드를 사용 하 여](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)합니다.  
  
 가용성 그룹 수신기 또는 장애 조치(Failover) 클러스터 인스턴스 이외의 다른 항목에 연결할 때 **MultiSubnetFailover=Yes**를 지정하면 성능에 상당히 부정적인 영향을 줄 수 있으므로 이러한 설정은 지원되지 않습니다.  
  
 다음 지침에 따라 장애 조치(Failover) 클러스터 인스턴스 또는 가용성 그룹의 서버에 연결하십시오.  
  
-   단일 서브넷 또는 다중 서브넷에 연결할 때 **MultiSubnetFailover** 연결 속성을 사용하면 두 서브넷의 성능이 향상됩니다.  
  
-   가용성 그룹에 연결하려면 가용성 그룹에 대한 가용성 그룹 수신기를 연결 문자열의 서버로 지정합니다.  
  
-   IP 주소가 64개 이상으로 구성된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 연결 오류가 발생합니다.  
  
-   **MultiSubnetFailover** 연결 속성을 사용하는 응용 프로그램 동작은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증, Kerberos 인증, Windows 인증과 같은 인증 유형의 영향을 받지 않습니다.  
  
-   장애 조치(failover) 시간을 수용하고 응용 프로그램의 연결 재시도 횟수를 줄이기 위해 **loginTimeout** 값을 늘릴 수 있습니다.  
  
-   분산 트랜잭션은 지원되지 않습니다.  
  
읽기 전용 라우팅이 적용되지 않으면 다음과 같은 경우 가용성 그룹의 보조 복제본 위치에 대한 연결이 실패합니다.  
  
1.  보조 복제본 위치가 연결을 허용하도록 구성되어 있지 않은 경우  
  
2.  응용 프로그램에서 **ApplicationIntent=ReadWrite**(아래에서 설명)를 사용하고 보조 복제본 위치가 읽기 전용 액세스용으로 구성되어 있는 경우  
  
주 복제본이 읽기 전용 작업을 거부하도록 구성되어 있고 연결 문자열에 **ApplicationIntent=ReadOnly**가 포함되어 있으면 연결이 실패합니다.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>데이터베이스 미러링에서 다중 서브넷 클러스터를 사용하도록 업그레이드  
연결 문자열에 **MultiSubnetFailover** 및 **Failover_Partner** 연결 키워드가 있으면 연결 오류가 발생합니다. **MultiSubnetFailover**가 사용되고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 데이터베이스 미러링 쌍의 일부임을 나타내는 장애 조치(failover) 파트너 응답을 반환하는 경우에도 오류가 발생합니다.  
  
OLE DB Driver for SQL Server 응용 프로그램 현재 사용 하 여 데이터베이스 미러링 다중 서브넷 시나리오를 업그레이드 하는 경우, 제거 해야는 **에서 Failover_Partner** 연결 속성 및 사용 하 여 바꾸기  **MultiSubnetFailover** 로 설정 **예** 연결 문자열에서 서버 이름을 가용성 그룹 수신기로 바꿉니다. 연결 문자열에서 **Failover_Partner** 및 **MultiSubnetFailover=Yes**를 사용하는 경우 드라이버에서 오류가 발생합니다. 그러나 연결 문자열에서 **Failover_Partner** 및 **MultiSubnetFailover=No**(또는 **ApplicationIntent=ReadWrite**)를 사용하면 응용 프로그램에서 데이터베이스 미러링을 사용합니다.  
  
가용성 그룹의 주 데이터베이스에서 데이터베이스 미러링이 사용되고 가용성 그룹 수신기가 아닌 주 데이터베이스에 연결하는 연결 문자열에 **MultiSubnetFailover=Yes**가 사용될 경우 드라이버에서 오류를 반환합니다.  
  
## <a name="specifying-application-intent"></a>응용 프로그램 의도 지정  
때 **ApplicationIntent = ReadOnly**, 클라이언트 설정에 항상 데이터베이스에 연결할 때 읽기 작업을 요청 합니다. 서버 연결 시 및 시 의도 적용 합니다는 `USE` 문 사용에 항상 데이터베이스에만 데이터베이스입니다.  
  
**ApplicationIntent** 키워드는 레거시 읽기 전용 데이터베이스에 적용되지 않습니다.  
  
데이터베이스 허용 하거나 차단할 수는 대상된 Alwayson 데이터베이스에 대 한 읽기 작업입니다. 이 작업은 **PRIMARY_ROLE** 및 **SECONDARY_ROLE**[!INCLUDE[tsql](../../../includes/tsql-md.md)] 문의 **ALLOW_CONNECTIONS** 절로 수행됩니다.  
  
**ApplicationIntent** 키워드는 읽기 전용 라우팅을 설정하는 데 사용됩니다.  
  
## <a name="read-only-routing"></a>읽기 전용 라우팅  
읽기 전용 라우팅은 데이터베이스의 읽기 전용 복제 가용성을 보장할 수 있는 기능입니다. 읽기 전용 라우팅을 활성화하려면:  
  
1.  AlwaysOn 가용성 그룹의 가용성 그룹 수신기에 연결해야 합니다.  
  
2.  **ApplicationIntent** 연결 문자열 키워드는 **ReadOnly**로 설정해야 합니다.  
  
3.  Always On 가용성 그룹을 읽기 전용 라우팅을 사용 하려면 데이터베이스 관리자가 구성 되어야 합니다.  
  
읽기 전용 라우팅을 사용하는 여러 연결 중 일부가 동일한 읽기 전용 복사본에 연결되지 않을 수 있습니다. 데이터베이스 동기화를 변경하거나 서버 라우팅 구성을 변경하면 클라이언트를 다른 읽기 전용 복사본에 연결할 수 있습니다. 모든 읽기 전용 요청이 동일한 읽기 전용 복제본에 연결 되도록 하는 Always On 가용성 그룹 수신기를 통과 하지 못한는 **서버** 연결 문자열 키워드입니다. 대신, 읽기 전용 인스턴스의 이름을 지정합니다.  
  
읽기 전용 라우팅은 먼저 기본 복제에 연결한 다음 가장 사용 가능한 읽기 가능 보조 복제를 찾으므로 읽기 전용 라우팅은 기본 복제에 연결하는 것보다 시간이 오래 걸릴 수 있습니다. 따라서 로그인 제한 시간을 늘려야 합니다.  
  
## <a name="ole-db"></a>OLE DB  
OLE DB Driver for SQL Server 모두를 지원 합니다.는 **ApplicationIntent** 및 **MultiSubnetFailover** 키워드입니다.   
  
두 개의 OLE DB 연결 문자열 키워드가 추가 된 지원 하기 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] OLE DB driver for SQL Server:  
  
-   **ApplicationIntent** 
-   **MultiSubnetFailover**  
  
 SQL Server 용 OLE DB Driver의 연결 문자열 키워드에 대 한 자세한 내용은 참조 [OLE DB 드라이버와 SQL Server에 대 한 연결 문자열 키워드를 사용 하 여](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)합니다.  

### <a name="application-intent"></a>응용 프로그램 의도 

해당하는 연결 속성은 다음과 같습니다.  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
OLE DB Driver for SQL Server 응용 프로그램 방법 중 하나를 사용 하 여 응용 프로그램 의도 지정 수 있습니다.  
  
 -   **Idbinitialize:: Initialize**  
 **IDBInitialize::Initialize**는 이전에 구성한 속성 집합을 사용하여 데이터 원본을 초기화하고 데이터 원본 개체를 만듭니다. 응용 프로그램 의도를 공급자 속성 또는 확장 속성 문자열의 일부로 지정합니다.  
  
 -   **Idatainitialize:: Getdatasource**  
 **IDataInitialize::GetDataSource**는 **응용 프로그램 의도** 키워드를 포함할 수 있는 입력 연결 문자열을 사용합니다.  
  
 -   **IDBProperties::SetProperties**  
 **ApplicationIntent** 속성 값을 설정하려면 값이 "**ReadWrite**" 또는 "**ReadOnly**"인 **SSPROP_INIT_APPLICATIONINTENT** 속성이나 값이 "**ApplicationIntent=ReadOnly**" 또는 "**ApplicationIntent=ReadWrite**"를 포함하는 **DBPROP_INIT_PROVIDERSTRING** 속성을 전달하여 **IDBProperties::SetProperties**를 호출합니다.  
  
**데이터 연결 속성** 대화 상자의 모두 탭에 있는 응용 프로그램 의도 속성 필드에서 응용 프로그램 의도를 지정할 수 있습니다.  
  
암시적 연결을 설정하면 암시적 연결이 부모 연결의 응용 프로그램 의도 설정을 사용합니다. 마찬가지로 동일한 데이터 원본에서 만들어진 여러 개의 세션은 데이터 원본의 응용 프로그램 의도 설정을 상속합니다.  
  
### <a name="multisubnetfailover"></a>MultiSubnetFailover

해당하는 연결 속성은 다음과 같습니다.  
  
-   **SSPROP_INIT_MULTISUBNETFAILOVER**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  

OLE DB Driver for SQL Server 응용 프로그램 MultiSubnetFailover 옵션을 설정 하려면 다음 방법 중 하나를 사용할 수 있습니다.  

 -   **Idbinitialize:: Initialize**  
 **IDBInitialize::Initialize**는 이전에 구성한 속성 집합을 사용하여 데이터 원본을 초기화하고 데이터 원본 개체를 만듭니다. 응용 프로그램 의도를 공급자 속성 또는 확장 속성 문자열의 일부로 지정합니다.  
  
 -   **Idatainitialize:: Getdatasource**  
 **Idatainitialize:: Getdatasource** 포함 될 수 있는 입력된 연결 문자열은 **MultiSubnetFailover** 키워드입니다.  

-   **IDBProperties::SetProperties**  
설정 하는 **MultiSubnetFailover** 속성 값, 호출 **idbproperties:: Setproperties** 전달는 **SSPROP_INIT_MULTISUBNETFAILOVER** 값을갖는속성 **VARIANT_TRUE** 또는 **VARIANT_FALSE** 또는 **DBPROP_INIT_PROVIDERSTRING** 속성 들어 있는 값을 "**MultiSubnetFailover = Yes** "또는"**MultiSubnetFailover = No**"입니다.

#### <a name="example"></a>예제

```
DBPROP rgPropMultisubnet;

rgPropMultisubnet.dwPropertyID = SSPROP_INIT_MULTISUBNETFAILOVER;
rgPropMultisubnet.dwOptions = DBPROPOPTIONS_REQUIRED;
rgPropMultisubnet.dwStatus = DBPROPSTATUS_OK;
rgPropMultisubnet.colid = DB_NULLID;
V_VT(&(rgPropMultisubnet.vValue)) = VT_BOOL;
V_BOOL(&(rgPropMultisubnet.vValue)) = VARIANT_TRUE;

DBPROPSET PropSet;

PropSet.rgProperties = &rgPropMultisubnet;
PropSet.cProperties = 1;
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;
IDBProperties* pIDBProperties = NULL;
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);
pIDBProperties->SetProperties(1, &PropSet);
```

## <a name="see-also"></a>관련 항목:  
 [OLE DB Driver for SQL Server 기능](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)  
  
  
