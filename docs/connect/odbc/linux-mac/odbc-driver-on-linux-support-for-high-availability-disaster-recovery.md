---
title: "MacOS-고가용성 및 재해 복구 및 Linux 기반 ODBC 드라이버 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fa656c5b-a935-40bf-bc20-e517ca5cd0ba
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d7b6c72d350b718a7676bffd72c261b7cfa72667
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-driver-on-linux-and-macos-support-for-high-availability-and-disaster-recovery"></a>MacOS 고가용성 및 재해 복구에 대 한 지원 및 Linux 기반 ODBC 드라이버
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Linux와 macOS 지원에 대 한 ODBC 드라이버 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]합니다. 에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]를 참조 하세요.  
  
-   [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치 (SQL Server)](http://msdn.microsoft.com/library/hh213417.aspx)  
  
-   [가용성 그룹 (SQL Server)의 생성 및 구성](http://msdn.microsoft.com/library/ff878265.aspx)  
  
-   [장애 조치 클러스터링 및 AlwaysOn 가용성 그룹 (SQL Server)](http://msdn.microsoft.com/library/ff929171.aspx)  
  
-   [활성 보조: 읽기 가능한 보조 복제본 (AlwaysOn 가용성 그룹)](http://msdn.microsoft.com/library/ff878253.aspx)  
  
연결 문자열에서 특정 AG(가용성 그룹)에 대한 가용성 그룹 수신기를 지정할 수 있습니다. Linux 또는 macOS에서 ODBC 응용 프로그램 장애 조치 되 가용성 그룹에 데이터베이스에 연결 된 경우 원래 연결이 끊어지고 및 응용 프로그램 장애 조치 후 작업을 계속 하려면 새 연결을 열어야 합니다.

Linux와 macOS에서 ODBC 드라이버는 가용성 그룹 수신기에 연결 하지 하며 여러 IP 주소가 호스트 이름으로 연결 되어 있는 경우 DNS 호스트 이름에 연결 된 모든 IP 주소를 순차적으로 검색 합니다.

반환 된 첫 번째 IP 주소가 DNS 서버를 연결 가능 없으면 이러한 반복 시간이 많이 걸릴 수 있습니다. 가용성 그룹 수신기에 연결할 때 드라이버에 병렬 모든 IP 주소에 대 한 연결을 설정 하려고 시도 합니다. 연결 시도에 성공하면 드라이버가 모든 보류 중인 연결 시도를 삭제합니다.

> [!NOTE]  
> 가용성 그룹 장애 조치는으로 인해 연결이 실패할 수, 연결 재시도 논리를 구현 다시 연결 될 때까지 실패 한 연결을 다시 시도 하십시오. 연결 시간 제한을 늘리고 연결 재시도 논리를 구현하면 가용성 그룹에 대한 연결 가능성이 높아집니다.

## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover로 연결

항상 지정 **MultiSubnetFailover = Yes** (또는 **= True**)에 연결할 때는 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] 가용성 그룹 수신기 또는 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] 장애 조치 클러스터 인스턴스의 합니다. **MultiSubnetFailover** 모든 가용성 그룹 및 장애 조치 클러스터 인스턴스를 보다 빠르게 장애 조치할 수 있도록 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]합니다. **MultiSubnetFailover** 단일 및 다중 서브넷 AlwaysOn 토폴로지에 대 한 장애 조치 시간을 크게 줄여 줍니다. 다중 서브넷 장애 조치(failover) 중에는 클라이언트가 병렬로 연결을 시도합니다. 서브넷 장애 조치 하는 동안 드라이버는 적극적으로 TCP 연결을 다시 시도합니다.

**MultiSubnetFailover** 연결 속성은 응용 프로그램이 가용성 그룹 또는 장애 조치(failover) 클러스터 인스턴스에서 배포되는 중이라는 것을 나타냅니다. 드라이버는 주 데이터베이스에 연결 하려고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 모든 IP에 연결 하려고 시도 하 여 인스턴스 주소입니다. 에 연결할 때 **MultiSubnetFailover = Yes**, 클라이언트 운영 체제의 기본 TCP 재전송 간격 보다 빠르게 TCP 연결 시도 다시 시도 합니다. **MultiSubnetFailover=Yes** 는 AlwaysOn 가용성 그룹 또는 AlwaysOn 장애 조치(failover) 클러스터 인스턴스의 장애 조치(failover) 후 더 빠르게 다시 연결할 수 있도록 합니다. **MultiSubnetFailover = Yes** 모두 단일 및 다중 서브넷 가용성 그룹과 장애 조치 클러스터 인스턴스에 적용 됩니다.  

가용성 그룹 수신기 또는 장애 조치(failover) 클러스터 인스턴스에 연결할 때 **MultiSubnetFailover=Yes** 를 사용합니다. 그렇지 않으면 응용 프로그램의 성능이 저하 될 수 있습니다.

장애 조치 클러스터 인스턴스 또는 가용성 그룹의 서버에 연결할 때 다음 note:
  
-   지정 **MultiSubnetFailover = Yes** 단일 서브넷 또는 다중 서브넷 가용성 그룹에 연결할 때 성능을 향상 시키기 합니다.

-   연결 문자열에서 서버와 가용성 그룹의 가용성 그룹 수신기를 지정 합니다.
  
-   에 연결할 수 없습니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 64 개 이상의 IP 주소로 구성 된 인스턴스.

-   둘 다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 인증 또는 Kerberos 인증을 사용 하 여 **MultiSubnetFailover = Yes** 의 응용 프로그램의 동작에 영향을 주지 않고 합니다.

-   장애 조치(failover) 시간을 수용하고 응용 프로그램의 연결 재시도 횟수를 줄이기 위해 **loginTimeout** 값을 늘릴 수 있습니다.

-   분산 트랜잭션은 지원되지 않습니다.  
  
읽기 전용 라우팅이 적용되지 않으면 다음과 같은 경우 가용성 그룹의 보조 복제본 위치에 대한 연결이 실패합니다.  
  
1.  보조 복제본 위치가 연결을 허용하도록 구성되어 있지 않은 경우  
  
2.  응용 프로그램에서 **ApplicationIntent=ReadWrite** 를 사용하고 보조 복제본 위치가 읽기 전용 액세스용으로 구성되어 있는 경우  
  
주 복제본이 읽기 전용 작업을 거부하도록 구성되어 있고 연결 문자열에 **ApplicationIntent=ReadOnly**가 포함되어 있으면 연결이 실패합니다.  
  
## <a name="specifying-application-intent"></a>응용 프로그램 의도 지정  
**ApplicationIntent=ReadOnly**인 경우 클라이언트는 AlwaysOn이 설정된 데이터베이스에 연결할 때 읽기 작업을 요청합니다. 서버 연결 시 및 USE 데이터베이스 문 동안 되지만 AlwaysOn이 설정 된 데이터베이스에만 의도 적용합니다.

**ApplicationIntent** 키워드는 레거시 읽기 전용 데이터베이스에 적용되지 않습니다.  

데이터베이스는 대상 AlwaysOn 데이터베이스에 대한 읽기 작업을 허용하거나 허용하지 않을 수 있습니다. (사용 하 여는 **ALLOW_CONNECTIONS** 절은 **PRIMARY_ROLE** 및 **SECONDARY_ROLE** [!INCLUDE[tsql](../../../includes/tsql_md.md)] 문.)  
  
**ApplicationIntent** 키워드는 읽기 전용 라우팅을 설정하는 데 사용됩니다.  
  
## <a name="read-only-routing"></a>읽기 전용 라우팅  
읽기 전용 라우팅은 데이터베이스의 읽기 전용 복제 가용성을 보장할 수 있는 기능입니다. 읽기 전용 라우팅을 활성화하려면:  
  
1.  AlwaysOn 가용성 그룹의 가용성 그룹 수신기에 연결합니다.  
  
2.  **ApplicationIntent** 연결 문자열 키워드는 **ReadOnly**로 설정해야 합니다.  
  
3.  읽기 전용 라우팅을 설정하려면 데이터베이스 관리자가 가용성 그룹을 구성해야 합니다.  
  
읽기 전용 라우팅을 사용하는 여러 연결이 여러 읽기 전용 복제본에 연결될 수 있습니다. 데이터베이스 동기화를 변경하거나 서버 라우팅 구성을 변경하면 클라이언트를 다른 읽기 전용 복사본에 연결할 수 있습니다. 모든 읽기 전용 요청을 동일한 읽기 전용 복제본에 연결하려면 가용성 그룹 수신기를 **Server** 연결 키워드에 전달하지 마세요. 대신, 읽기 전용 인스턴스의 이름을 지정합니다.  
  
읽기 전용 라우팅을 사용하면 주 복제본에 연결할 때보다 연결하는 데 시간이 더 걸립니다. 따라서 로그인 시간 제한을 늘립니다. 읽기 전용 라우팅은 먼저 주 복제본에 연결한 다음 가장 잘 읽을 수 있는 보조 복제본을 찾습니다.  
  
## <a name="odbc-syntax"></a>ODBC 구문

두 개의 ODBC 연결 문자열 키워드가 지원 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]:  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
ODBC 연결 문자열 키워드에 대한 자세한 내용은 [SQL Server Native Client에서 연결 문자열 키워드 사용](http://msdn.microsoft.com/library/ms130822.aspx)을 참조하세요.  
  
해당 하는 연결 특성은 합니다.
  
-   **된 SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
ODBC 연결 특성에 대 한 자세한 내용은 참조 [SQLSetConnectAttr](http://msdn.microsoft.com/library/ms131709.aspx)합니다.  
  
사용 하는 ODBC 응용 프로그램 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] 연결을 만드는 데 두 가지 함수 중 하나를 사용할 수 있습니다.  
  
|함수|Description|  
|------------|---------------|  
|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|**SQLConnect** 모두 지원 **ApplicationIntent** 및 **MultiSubnetFailover** 데이터 원본 이름 (DSN) 또는 연결 특성을 통해.|  
|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|**SQLDriverConnect** 지원 **ApplicationIntent** 및 **MultiSubnetFailover** DSN, 연결 문자열 키워드 또는 연결 특성을 통해.|
  
## <a name="see-also"></a>관련 항목:  

[연결 문자열 키워드 및 DSN(데이터 원본 이름)](../../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)

[프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)

[릴리스 정보](../../../connect/odbc/linux-mac/release-notes.md)  

