---
title: Linux 및 macOS의 ODBC 드라이버 - 고가용성 및 재해 복구 | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fa656c5b-a935-40bf-bc20-e517ca5cd0ba
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4f307efedd62a1fcc923a2e61da8636a89e40bb
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59042382"
---
# <a name="odbc-driver-on-linux-and-macos-support-for-high-availability-and-disaster-recovery"></a>Linux 및 macOS의 ODBC 드라이버 - 고가용성 및 재해 복구
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Linux 및 macOS용 ODBC 드라이버는 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]를 지원합니다. [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)(SQL Server)](https://msdn.microsoft.com/library/hh213417.aspx)  
  
-   [가용성 그룹의 생성 및 구성(SQL Server)](https://msdn.microsoft.com/library/ff878265.aspx)  
  
-   [장애 조치(Failover) 클러스터링 및 Always On 가용성 그룹(SQL Server)](https://msdn.microsoft.com/library/ff929171.aspx)  
  
-   [활성 보조: 읽기 가능한 보조 복제본(Always On 가용성 그룹)](https://msdn.microsoft.com/library/ff878253.aspx)  
  
연결 문자열에서 특정 AG(가용성 그룹)에 대한 가용성 그룹 수신기를 지정할 수 있습니다. Linux 또는 macOS의 ODBC 애플리케이션이 장애 조치(Failover)되는 가용성 그룹의 데이터베이스에 연결된 경우, 원래 연결은 끊어지며 장애 조치 후 애플리케이션이 계속 작동하려면 새 연결을 열어야 합니다.

가용성 그룹 수신기에 연결하지 않았고 여러 IP 주소가 호스트 이름과 연결된 경우 Linux 및 macOS 기반 ODBC 드라이버는 
DNS 호스트 이름과 연결된 모든 IP 주소를 순차적으로 반복합니다.

DNS 서버의 첫 번째 반환된 IP 주소가 연결 가능하지 않은 경우 해당 반복에 시간이 오래 걸릴 수 있습니다. 가용성 그룹 수신기에 연결할 경우 드라이버가 모든 IP 주소에 대해 병렬 연결을 설정하려고 합니다. 연결 시도에 성공하면 드라이버가 모든 보류 중인 연결 시도를 삭제합니다.

> [!NOTE]  
> 가용성 그룹 장애 조치(failover)로 인해 연결이 실패할 수 있으므로 실패한 연결을 다시 연결할 때까지 다시 시도하는 연결 재시도 논리를 구현합니다. 연결 시간 제한을 늘리고 연결 재시도 논리를 구현하면 가용성 그룹에 대한 연결 가능성이 높아집니다.

## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover로 연결

[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 가용성 그룹 수신기 또는 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 장애 조치(failover) 클러스터 인스턴스에 연결할 때 항상 **MultiSubnetFailover=Yes**를 지정합니다. **MultiSubnetFailover**는 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]의 모든 가용성 그룹 및 장애 조치(failover) 클러스터 인스턴스에 대해 보다 빠르게 장애 조치(failover)를 수행할 수 있도록 합니다. **MultiSubnetFailover**는 단일 및 다중 서브넷 Always On 토폴로지에 대한 장애 조치(failover) 시간도 크게 줄여 줍니다. 다중 서브넷 장애 조치(failover) 중에는 클라이언트가 병렬로 연결을 시도합니다. 서브넷 장애 조치(failover) 동안 드라이버에서 TCP 연결을 적극적으로 다시 시도합니다.

**MultiSubnetFailover** 연결 속성은 애플리케이션이 가용성 그룹 또는 장애 조치(failover) 클러스터 인스턴스에서 배포되는 중이라는 것을 나타냅니다. 드라이버는 모든 IP 주소에 연결하려고 시도하여 주 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 데이터베이스에 연결하려고 합니다. **MultiSubnetFailover=Yes**를 사용하여 연결하면 클라이언트는 운영 체제의 기본 TCP 재전송 간격보다 빠르게 TCP 연결을 다시 시도합니다. **MultiSubnetFailover=Yes** 는 AlwaysOn 가용성 그룹 또는 AlwaysOn 장애 조치(failover) 클러스터 인스턴스의 장애 조치(failover) 후 더 빠르게 다시 연결할 수 있도록 합니다. **MultiSubnetFailover=Yes**는 단일 및 다중 서브넷 가용성 그룹과 장애 조치(failover) 클러스터 인스턴스에 모두 적용됩니다.  

가용성 그룹 수신기 또는 장애 조치(failover) 클러스터 인스턴스에 연결할 때 **MultiSubnetFailover=Yes** 를 사용합니다. 그렇지 않으면 애플리케이션의 성능에 부정적인 영향을 미칠 수 있습니다.

장애 조치(Failover) 클러스터 인스턴스 또는 가용성 그룹의 서버에 연결할 때 다음 내용을 참고하십시오.
  
-   단일 서브넷 또는 다중 서브넷 가용성 그룹에 연결할 때 성능을 개선하려면 **MultiSubnetFailover=Yes**를 지정합니다.

-   연결 문자열에 가용성 그룹의 가용성 그룹 수신기를 서버로 지정합니다.
  
-   64개 이상의 IP 주소로 구성된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 없습니다.

-   **MultiSubnetFailover=Yes**를 지정하면 애플리케이션의 동작에 영향을 주지 않고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 또는 Kerberos 인증을 모두 사용할 수 있습니다.

-   장애 조치(failover) 시간을 수용하고 애플리케이션의 연결 재시도 횟수를 줄이기 위해 **loginTimeout** 값을 늘릴 수 있습니다.

-   분산 트랜잭션은 지원되지 않습니다.  
  
읽기 전용 라우팅이 적용되지 않으면 다음과 같은 경우 가용성 그룹의 보조 복제본 위치에 대한 연결이 실패합니다.  
  
1.  보조 복제본 위치가 연결을 허용하도록 구성되어 있지 않은 경우  
  
2.  애플리케이션에서 **ApplicationIntent=ReadWrite** 를 사용하고 보조 복제본 위치가 읽기 전용 액세스용으로 구성되어 있는 경우  
  
주 복제본이 읽기 전용 작업을 거부하도록 구성되어 있고 연결 문자열에 **ApplicationIntent=ReadOnly**가 포함되어 있으면 연결이 실패합니다.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="odbc-syntax"></a>ODBC 구문

두 개의 ODBC 연결 문자열 키워드가 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]을 지원합니다.  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
ODBC 연결 문자열 키워드에 대한 자세한 내용은 [SQL Server Native Client에서 연결 문자열 키워드 사용](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하세요.  
  
해당하는 연결 특성은 다음과 같습니다.
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
ODBC 연결 속성에 대한 자세한 내용은 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)을 참조하세요.  
  
[!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]을 사용하는 ODBC 애플리케이션은 연결을 만들 때 두 가지 함수 중 하나를 사용할 수 있습니다.  
  
|함수|설명|  
|------------|---------------|  
|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|**SQLConnect**는 DSN(데이터 원본 이름) 또는 연결 속성을 통해 **ApplicationIntent**와 **MultiSubnetFailover**를 모두 지원합니다.|  
|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|**SQLDriverConnect**는 DSN, 연결 문자열 키워드 또는 연결 속성을 통해 **ApplicationIntent** 및 **MultiSubnetFailover**를 지원합니다.|
  
## <a name="see-also"></a>참고 항목  

[연결 문자열 키워드 및 DSN(데이터 원본 이름)](../../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)

[프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)

[릴리스 정보](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
