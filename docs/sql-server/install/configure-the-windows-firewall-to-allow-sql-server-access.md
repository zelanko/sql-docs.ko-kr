---
title: SQL Server 액세스를 허용하도록 Windows 방화벽 구성 | Microsoft 문서
ms.custom: sqlfreshmay19
ms.date: 05/15/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Windows Firewall ports
- WMI firewall ports
- Windows Firewall [Database Engine]
- firewall systems, configuring
- advfirewall
- firewall systems
- rules firewall
- firewall systems, overview and port list
- 1433 TCP port
- portopening using netsh
- ports [SQL Server], TCP
- netsh to open firewall ports
ms.assetid: f55c6a0e-b6bd-4803-b51a-f3a419803024
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: abae05ff73ff1da46bda029b32320a9deccfbf51
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637976"
---
# <a name="configure-the-windows-firewall-to-allow-sql-server-access"></a>Configure the Windows Firewall to Allow SQL Server Access
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

방화벽 시스템은 컴퓨터 리소스에 대한 무단 액세스를 방지합니다. 방화벽을 설정하고 올바르게 구성하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 연결 시도가 차단될 수 있습니다.  
  
방화벽을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 액세스하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조하세요. 방화벽은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows의 구성 요소입니다. 다른 회사의 방화벽도 설치할 수 있습니다. 이 문서에서는 Windows 방화벽의 구성 방법에 대해 설명하지만 기본 원칙은 다른 방화벽 프로그램에도 적용됩니다.  
  
> [!NOTE]  
>  이 문서에서는 방화벽 구성의 개요를 제공하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자에게 유용한 정보를 요약하여 설명합니다. 방화벽에 대한 자세한 내용과 권위 있는 방화벽 정보를 보려면 [Windows 방화벽 보안 배포 가이드](/windows/security/threat-protection/windows-firewall/windows-firewall-with-advanced-security-deployment-guide) 등의 방화벽 설명서를 참조하세요.  
  
 **Windows 방화벽** 관리에 익숙한 사용자이며 어떤 방화벽 설정을 구성할지 알고 있다면 다음과 같은 고급 문서로 직접 이동할 수 있습니다.  
  
-   [데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)    
-   [Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)    
-   [보고서 서버 액세스를 위한 방화벽 구성](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
##  <a name="BKMK_basic"></a> 기본 방화벽 정보  
 방화벽은 들어오는 패킷을 검사하고 규칙 집합과 이 패킷을 비교합니다. 패킷이 규칙에서 요구하는 표준에 부합하면 방화벽은 추가 처리를 위한 TCP/IP 프로토콜로 이 패킷을 전달합니다. 패킷이 규칙에서 지정한 표준에 부합하지 않는 경우 방화벽은 이 패킷을 삭제하고 로깅이 설정된 경우 방화벽 로깅 파일에 항목을 작성합니다.  
  
 허용된 트래픽 목록은 다음 방식 중 하나로 채워집니다.  

- **자동**: 방화벽을 사용하는 컴퓨터에서 통신을 시작하면 방화벽은 목록에 항목을 만들어 응답이 허용되도록 합니다. 이 응답은 요청된 트래픽으로 간주되며 구성이 필요한 항목이 없습니다. 
  
-   **수동**: 관리자가 방화벽에 대한 예외를 구성합니다. 컴퓨터에서 지정된 프로그램이나 포트에 대한 액세스를 허용합니다. 이 경우 컴퓨터는 서버, 수신기 또는 피어로 작동할 때 요청하지 않은 트래픽의 수신을 허용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하려면 이 유형의 구성을 완료해야 합니다.  
  
 방화벽 전략 선택은 단순히 특정 포트를 열거나 닫을지를 결정하는 것 이상으로 복잡한 과정입니다. 기업에 맞는 방화벽 전략을 설계할 때는 사용 가능한 모든 규칙과 구성 옵션을 고려해야 합니다. 이 문서에서는 방화벽에 사용할 수 있는 모든 옵션을 검토하지는 않습니다. 자세한 내용을 보려면 다음 문서를 참조하세요.  
  
 [Windows 방화벽 배포 가이드 ](/windows/security/threat-protection/windows-firewall/windows-firewall-with-advanced-security-deployment-guide)    
 [Windows 방화벽 디자인 가이드 ](/windows/security/threat-protection/windows-firewall/windows-firewall-with-advanced-security-design-guide)    
 [서버 및 도메인 격리 소개(Introduction to Server and Domain Isolation)](/windows/security/threat-protection/windows-firewall/domain-isolation-policy-design)  
  
##  <a name="BKMK_default"></a> 기본 방화벽 설정  
 방화벽 구성을 계획하는 첫째 단계는 운영 체제의 현재 방화벽 상태를 확인하는 것입니다. 운영 체제를 이전 버전에서 업그레이드한 경우 이전 버전의 방화벽 설정이 그대로 남아 있을 수 있습니다. 또한 다른 관리자나 도메인의 그룹 정책에 의해 방화벽 설정이 변경되었을 수도 있습니다.  
  
> [!NOTE]  
>  방화벽을 켜면 파일 및 인쇄 공유와 같이 이 컴퓨터에 액세스하는 다른 프로그램과 원격 데스크톱 연결이 영향을 받습니다. 관리자는 방화벽 설정을 조정하기 전에 컴퓨터에서 실행 중인 모든 애플리케이션을 고려해야 합니다.  
  
##  <a name="BKMK_programs"></a> 방화벽 구성 프로그램  
**Microsoft Management Console** 또는 **netsh**를 사용하여 Windows 방화벽 설정을 구성합니다.  

-  **MMC(Microsoft Management Console)**  
  
     고급 보안이 설정된 Windows 방화벽 MMC 스냅인을 사용하면 고급 방화벽 설정을 구성할 수 있습니다. 이 스냅인은 대부분의 방화벽 옵션을 쉽게 사용할 수 있도록 제공하고 모든 방화벽 프로필을 제공합니다. 자세한 내용은 이 문서의 뒷부분에 나오는 [고급 보안이 설정된 Windows 방화벽 스냅인 사용](#BKMK_WF_msc) 을 참조하세요.  
  
-   **netsh**  
  
     관리자는 **netsh.exe** 도구를 사용하여 명령 프롬프트 또는 배치 파일을 통해 Windows 기반 컴퓨터를 구성하고 모니터링할 수 있습니다 **.** **netsh** 도구를 사용하면 상황에 맞는 명령을 입력하여 적절한 도우미에 전달할 수 있습니다. 그러면 도우미가 명령을 수행합니다. 도우미는 하나 이상의 서비스, 유틸리티 또는 프로토콜에 대한 구성, 모니터링 및 지원을 제공하여 **netsh** 도구의 기능을 확장하는 동적 연결 라이브러리 파일(.dll)입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 지원하는 모든 운영 체제에는 방화벽 도우미가 포함되어 있습니다. [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 에는 **advfirewall**이라는 고급 방화벽 도우미도 있습니다. **netsh** 사용에 대한 자세한 내용은 이 문서에서 다루지 않습니다. 그러나 여기서 설명하는 대부분의 구성 옵션은 **netsh**를 사용하여 구성할 수 있습니다. 예를 들어 명령 프롬프트에서 다음 스크립트를 실행하여 TCP 포트 1433을 엽니다.  
  
    ```  
    netsh firewall set portopening protocol = TCP port = 1433 name = SQLPort mode = ENABLE scope = SUBNET profile = CURRENT  
    ```  
  
     고급 보안이 포함된 Windows 방화벽 도우미를 사용하는 비슷한 예는 다음과 같습니다.  
  
    ```  
    netsh advfirewall firewall add rule name = SQLPort dir = in protocol = tcp action = allow localport = 1433 remoteip = localsubnet profile = DOMAIN  
    ```  
  
     **netsh**에 대한 자세한 내용은 다음 링크를 참조하세요.  
  
    -   [Netsh 명령 구문, 컨텍스트 및 서식 지정](/windows-server/networking/technologies/netsh/netsh-contexts)    
    -   ["netsh firewall" 컨텍스트 대신 "netsh advfirewall firewall" 컨텍스트를 사용하여 Windows Server 2008 및 Windows Vista의 Windows 방화벽 동작을 제어하는 방법](https://support.microsoft.com/kb/947709)    

    
- **Linux**: Linux에서는 액세스 권한이 필요한 서비스와 연결된 포트도 열어야 합니다. 서로 다른 Linux 배포와 다양한 방화벽에는 고유한 프로시저가 있습니다. 두 가지 예를 [SQL Server on Red Hat](../../linux/quickstart-install-connect-red-hat.md)(Red Hat의 SQL Server) 및 [SQL Server on SUSE](../../linux/quickstart-install-connect-suse.md)(SUSE의 SQL Server)에서 참조하세요. 
  
## <a name="ports-used-by-includessnoversionincludesssnoversion-mdmd"></a>다음에서 사용하는 포트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 다음 표를 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 포트를 확인할 수 있습니다.  
  
###  <a name="BKMK_ssde"></a> Ports Used By the Database Engine  
 

기본적으로 SQL Server 및 관련 데이터베이스 엔진 서비스에서 사용되는 일반적인 포트는 다음과 같습니다. TCP **1433**, **4022**, **135**, **1434**, UDP **1434**. 아래 표에는 이러한 포트가 자세히 설명되어 있습니다. 명명된 인스턴스는 [동적 포트](#BKMK_dynamic_ports)를 사용합니다.
 
 다음 표에서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 자주 사용하는 포트를 보여 줍니다.  
  
|시나리오|포트|주석|  
|--------------|----------|--------------|  
|TCP를 통해 실행되는 기본 인스턴스|TCP 포트 1433|방화벽에서 허용되는 가장 일반적인 포트입니다. 기본 [!INCLUDE[ssDE](../../includes/ssde-md.md)]설치에 대한 일상적인 연결 또는 컴퓨터에서 실행 중인 유일한 인스턴스인 명명된 인스턴스에 적용됩니다. 명명된 인스턴스에는 특별 고려 사항이 있습니다. 이 문서의 뒷부분에 나오는 [동적 포트](#BKMK_dynamic_ports)를 참조하세요.|  
|기본 포트를 통해 명명된 인스턴스|TCP 포트는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 시작할 때 결정되는 동적 포트입니다.|아래 [동적 포트](#BKMK_dynamic_ports)섹션의 설명을 참조하세요. 명명된 인스턴스를 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스에 UDP 포트 1434가 필요할 수 있습니다.|  
| 고정 포트를 통해 명명된 인스턴스 |관리자가 구성한 포트 번호입니다.|아래 [동적 포트](#BKMK_dynamic_ports)섹션의 설명을 참조하세요.|  
|관리자 전용 연결|기본 인스턴스에 대한 TCP 포트 1434. 다른 포트는 명명된 인스턴스에 사용됩니다. 오류 로그에서 포트 번호를 확인하세요.|기본적으로 DAC(관리자 전용 연결)에 대한 원격 연결은 설정되지 않습니다. 원격 DAC를 설정하려면 노출 영역 구성 패싯을 사용하세요. 자세한 내용은 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)을 참조하세요.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스|UDP 포트 1434|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스는 명명된 인스턴스에 대한 들어오는 연결을 수신하고 이 명명된 인스턴스에 해당하는 TCP 포트 번호를 클라이언트에 제공합니다. 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 명명된 인스턴스가 사용될 때마다 시작됩니다. 명명된 인스턴스의 특정 포트에 연결되도록 클라이언트를 구성한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 시작할 필요가 없습니다.|  
|HTTP 엔드포인트가 있는 인스턴스.|HTTP 엔드포인트를 만들 때 지정할 수 있습니다. 기본값은 CLEAR_PORT 트래픽의 경우 TCP 포트 80이고, SSL_PORT 트래픽의 경우 443입니다.|URL을 통한 HTTP 연결에 사용됩니다.|  
|HTTPS 엔드포인트가 있는 기본 인스턴스. |TCP 포트 443|URL을 통한 HTTPS 연결에 사용됩니다. HTTPS는 SSL(Secure Sockets Layer)을 사용하는 HTTP 연결입니다.|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|TCP 포트 4022. 사용되는 포트를 확인하려면 다음 쿼리를 실행합니다.<br /><br /> `SELECT name, protocol_desc, port, state_desc`<br /><br /> `FROM sys.tcp_endpoints`<br /><br /> `WHERE type_desc = 'SERVICE_BROKER'`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSB](../../includes/sssb-md.md)]에 대한 기본 포트는 없지만 이는 온라인 설명서 예에서는 이 구성이 일반적으로 사용됩니다.|  
|데이터베이스 미러링|관리자가 선택한 포트입니다. 포트를 확인하려면 다음 쿼리를 실행합니다.<br /><br /> `SELECT name, protocol_desc, port, state_desc FROM sys.tcp_endpoints`<br /><br /> `WHERE type_desc = 'DATABASE_MIRRORING'`|데이터베이스 미러링에 대한 기본 포트는 없지만 온라인 설명서의 예에서는 TCP 포트 5022 또는 7022를 사용합니다. 특히 자동 장애 조치(Failover)를 사용하는 보안 수준이 높은 모드에서는 사용 중인 미러링 엔드포인트가 중단되지 않도록 하는 것이 중요합니다. 방화벽 구성으로 인해 쿼럼이 중단되면 안 됩니다. 자세햔 내용은 [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)을 사용합니다.|  
|복제|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 복제 연결에는 일반적인 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 포트(기본 인스턴스의 경우 TCP 포트 1433 등)가 사용됩니다.<br /><br /> 복제 스냅샷을 위한 웹 동기화 및 FTP/UNC 액세스를 위해서는 방화벽에서 추가 포트를 열어야 합니다. 복제는 초기 데이터 및 스키마를 다른 위치로 전송하기 위해 FTP(TCP 포트 21)를 사용하거나 HTTP(TCP 포트 80) 또는 파일 공유를 통해 동기화할 수 있습니다. 파일 공유에는 UDP 포트 137 및 138, TCP 포트 139가 사용됩니다(NetBIOS를 사용하는 경우). 파일 공유에는 TCP 포트 445가 사용됩니다.|HTTP를 통한 동기화의 경우 복제는 IIS 엔드포인트(포트를 구성할 수 있지만 기본 포트는 80)를 사용하지만 IIS 프로세스는 표준 포트(기본 인스턴스의 경우 1433)를 통해 백 엔드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결합니다.<br /><br /> FTP를 사용한 웹 동기화 중에 FTP 전송은 구독자와 IIS 사이가 아닌 IIS와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자 사이에 이뤄집니다.|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거|TCP 포트 135<br /><br /> [포트 135에 대한 특별 고려 사항](#BKMK_port_135)을 참조하세요.<br /><br /> [IPsec](#BKMK_IPsec) 예외가 필요할 수도 있습니다.|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]를 사용 중인 경우 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 호스트 컴퓨터에서 예외 목록에 **Devenv.exe** 를 추가하고 TCP 포트 135를 열어야 합니다.<br /><br /> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용 중인 경우 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 호스트 컴퓨터에서 예외 목록에 **ssms.exe** 를 추가하고 TCP 포트 135를 열어야 합니다. 자세한 내용은 [TSQL 디버거를 실행하기 전에 방화벽 규칙 구성](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md)을 참조하세요.|  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대해 Windows 방화벽을 구성하는 단계별 지침은 [데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)을 참조하세요.  
  
####  <a name="BKMK_dynamic_ports"></a> 동적 포트  
 기본적으로 명명된 인스턴스( [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]포함)는 동적 포트를 사용합니다. 즉, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 시작될 때마다 사용 가능한 포트를 식별하고 해당 포트 번호를 사용합니다. 명명된 인스턴스가 설치된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 유일한 인스턴스인 경우 보통 TCP 포트 1433을 사용합니다. 다른 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 설치된 경우 이 인스턴스는 다른 TCP 포트를 사용합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 시작될 때마다 선택되는 포트가 변경될 수 있기 때문에 올바른 포트 번호에 대한 액세스가 가능하도록 방화벽을 구성하기가 어렵습니다. 따라서 방화벽을 사용하는 경우 매번 동일한 포트 번호를 사용하도록 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 다시 구성하는 것이 좋습니다. 이러한 방식을 고정 포트 또는 정적 포트라고 합니다. 자세한 내용은 [특정 TCP 포트로 수신하도록 서버 구성&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)을 참조하세요.  
  
 고정 포트에서 수신하도록 명명된 인스턴스를 구성하는 또 다른 방법은 **sqlservr.exe**와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로그램에 대한 예외를 방화벽에서 만드는 것입니다([!INCLUDE[ssDE](../../includes/ssde-md.md)]의 경우). 이 방법은 편리하지만 고급 보안이 설정된 Windows 방화벽 MMC 스냅인을 사용할 경우 **인바운드 규칙** 페이지의 **로컬 포트** 열에 포트 번호가 표시되지 않습니다. 따라서 어떤 포트가 열려 있는지 감사하기가 더 어려워집니다. 또 다른 고려 사항은 서비스 팩 또는 누적 업데이트로 인해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 파일에 대한 경로가 변경되어 방화벽 규칙이 무효화될 수 있다는 점입니다.  
  
##### <a name="to-add-a-program-exception-to-the-firewall-using-windows-firewall-with-advanced-security"></a>고급 보안이 포함된 Windows 방화벽 항목을 사용하여 방화벽에 프로그램 예외를 추가하려면
  
1. 시작 메뉴에서 *wf.msc*를 입력합니다. **고급 보안이 포함된 Windows 방화벽**을 선택합니다.
1. 왼쪽 창에서 **인바운드 규칙**을 선택합니다.
1. 오른쪽 창의 **작업**에서 **새 규칙...** 을 선택합니다. **새 인바운드 규칙 마법사**가 열립니다.
1. **규칙 유형**에서 **프로그램**을 선택합니다. **다음**을 선택합니다.
1. **프로그램**에서 **다음 프로그램 경로**를 선택합니다. **찾아보기**를 선택하고 SQL Server의 인스턴스를 찾습니다. 이 프로그램을 sqlservr.exe라고 합니다. 파일은 일반적으로 다음 위치에 있습니다.

   `C:\Program Files\Microsoft SQL Server\MSSQL13.<InstanceName>\MSSQL\Binn\sqlservr.exe`

   **다음**을 선택합니다.

1. **작업**에서 **연결 허용**을 클릭합니다.  
1. 프로필에 세 개의 프로필을 모두 포함합니다. **다음**을 선택합니다.
1. **이름**에 규칙의 이름을 입력합니다. **마침**을 선택합니다.

엔드포인트에 대한 자세한 내용은 [여러 TCP 포트에서 수신하도록 데이터베이스 엔진 구성](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md) 및 [엔드포인트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)를 참조하세요. 
  
###  <a name="BKMK_ssas"></a> Analysis Services에서 사용하는 포트  
 
기본적으로 SQL Server Analysis Services 및 관련 서비스에서 사용되는 일반적인 포트는 다음과 같습니다. TCP **2382**, **2383**, **80**, **443**. 아래 표에는 이러한 포트가 자세히 설명되어 있습니다.  
 
 다음 표에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 자주 사용하는 포트를 보여 줍니다.  
  
|기능|포트|주석|  
|-------------|----------|--------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|기본 인스턴스에 대한 TCP 포트 2383|기본 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 대한 표준 포트입니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명명된 인스턴스에만 필요한 TCP 포트 2382|포트 번호를 지정하지 않는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 명명된 인스턴스에 대한 클라이언트 연결 요청은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser에서 수신하는 포트인 포트 2382로 전달됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser에서 해당 요청을 명명된 인스턴스가 사용하는 포트로 리디렉션합니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - IIS/HTTP를 통해 사용하도록 구성<br /><br /> (PivotTable® 서비스는 HTTP 또는 HTTPS 사용)|TCP 포트 80|URL을 통한 HTTP 연결에 사용됩니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - IIS/HTTPS를 통해 사용하도록 구성<br /><br /> (PivotTable® 서비스는 HTTP 또는 HTTPS 사용)|TCP 포트 443|URL을 통한 HTTPS 연결에 사용됩니다. HTTPS는 SSL(Secure Sockets Layer)을 사용하는 HTTP 연결입니다.|  
  
 사용자가 IIS 및 인터넷을 통해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 액세스하는 경우 IIS가 수신하고 있는 포트를 열고 클라이언트 연결 문자열에 해당 포트를 지정해야 합니다. 이 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 직접 액세스하는 포트를 열 필요가 없습니다. 기본 포트 2389 및 포트 2382는 필요 없는 다른 모든 포트와 함께 제한해야 합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대해 Windows 방화벽을 구성하는 단계별 지침은 [Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)을 참조하세요.  
  
###  <a name="BKMK_ssrs"></a> Reporting Services에서 사용하는 포트  

기본적으로 SQL Server Reporting SErvices 및 관련 서비스에서 사용되는 일반적인 포트는 다음과 같습니다. TCP **80**, **443**. 아래 표에는 이러한 포트가 자세히 설명되어 있습니다. 


다음 표에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 자주 사용하는 포트를 보여 줍니다.  
  
|기능|포트|주석|  
|-------------|----------|--------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 서비스|TCP 포트 80|URL을 통한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] HTTP 연결에 사용됩니다. 미리 구성된 규칙 **World Wide Web 서비스(HTTP)** 는 사용하지 않는 것이 좋습니다. 자세한 내용은 아래의 [다른 방화벽 규칙과의 상호 작용](#BKMK_other_rules) 섹션을 참조하세요.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - HTTPS를 통해 사용하도록 구성|TCP 포트 443|URL을 통한 HTTPS 연결에 사용됩니다. HTTPS는 SSL(Secure Sockets Layer)을 사용하는 HTTP 연결입니다. 미리 구성된 규칙 **보안 World Wide Web 서비스(HTTPS)** 는 사용하지 않는 것이 좋습니다. 자세한 내용은 아래의 [다른 방화벽 규칙과의 상호 작용](#BKMK_other_rules) 섹션을 참조하세요.|  
  
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결되는 경우 이러한 서비스에 대해 적절한 포트를 열어야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대해 Windows 방화벽을 구성하는 단계별 지침은 [보고서 서버 액세스를 위한 방화벽 구성](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)을 참조하세요.  
  
###  <a name="BKMK_ssis"></a> Integration Services에서 사용하는 포트  
 다음 표에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서 사용하는 포트를 보여 줍니다.  
  
|기능|포트|주석|  
|-------------|----------|--------------|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 원격 프로시저 호출(MS RPC)<br /><br /> [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임에 사용됩니다.|TCP 포트 135<br /><br /> [포트 135에 대한 특별 고려 사항](#BKMK_port_135)을 참조하세요.|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 포트 135에서 DCOM을 사용합니다. 서비스 제어 관리자는 포트 135를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 시작 및 중지, 실행 중인 서비스에 대한 제어 요청 전송과 같은 태스크를 수행합니다. 포트 번호는 변경할 수 없습니다.<br /><br /> 이 포트는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 또는 사용자 지정 애플리케이션에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 서비스의 원격 인스턴스에 연결하는 경우에만 열면 됩니다.|  
  
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 대해 Windows 방화벽을 구성하는 단계별 지침은 [Integration Services 서비스&#40;SSIS 서비스&#41;](../../integration-services/service/configure-a-windows-firewall-for-access-to-the-ssis-service.md?view=sql-server-2014)를 참조하세요.  
  
###  <a name="BKMK_additional_ports"></a> 추가 포트 및 서비스  
다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용할 수 있는 포트 및 서비스를 보여 줍니다.  
  
|시나리오|포트|주석|  
|--------------|----------|--------------|  
|Windows Management Instrumentation<br /><br /> WMI에 대한 자세한 내용은 [WMI Provider for Configuration Management Concepts](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)을 참조하세요.|WMI는 공유 서비스 호스트의 일부로 실행되며 포트는 DCOM을 통해 할당됩니다. WMI는 TCP 포트 135를 사용 중일 수 있습니다.<br /><br /> [포트 135에 대한 특별 고려 사항](#BKMK_port_135)을 참조하세요.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 WMI를 사용하여 서비스를 나열하고 관리합니다. 미리 구성된 규칙 그룹 **WMI(Windows Management Instrumentation)** 를 사용하는 것이 좋습니다. 자세한 내용은 아래의 [다른 방화벽 규칙과의 상호 작용](#BKMK_other_rules) 섹션을 참조하세요.|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator(MS DTC)|TCP 포트 135<br /><br /> [포트 135에 대한 특별 고려 사항](#BKMK_port_135)을 참조하세요.|애플리케이션에서 분산 트랜잭션을 사용하는 경우 MS DTC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator) 트래픽이 개별 MS DTC 인스턴스 간에, 그리고 MS DTC와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]등의 리소스 관리자 간에 전달될 수 있도록 방화벽을 구성해야 합니다. 미리 구성된 **Distributed Transaction Coordinator** 규칙 그룹을 사용하는 것이 좋습니다.<br /><br /> 별도의 리소스 그룹에 있는 전체 클러스터에 단일 공유 MS DTC가 구성된 경우 방화벽에 sqlservr.exe를 예외로 추가해야 합니다.|  
|[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 의 찾아보기 단추를 클릭하면 UDP를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스에 연결됩니다. 자세한 내용은 [SQL Server Browser 서비스&#40;데이터베이스 엔진 및 SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)를 참조하세요.|UDP 포트 1434|UDP는 연결 없는 프로토콜입니다.<br /><br /> 방화벽에는 브로드캐스트(또는 멀티캐스트) UDP 요청에 대한 유니캐스트 응답과 관련하여 방화벽의 동작을 제어하는 설정([INetFwProfile 인터페이스의 UnicastResponsesToMulticastBroadcastDisabled 속성](https://go.microsoft.com/fwlink/?LinkId=118371))이 포함됩니다.  여기에는 두 가지 동작이 있습니다.<br /><br /> 설정이 TRUE이면 브로드캐스트에 대한 유니캐스트 응답이 허용되지 않습니다. 서비스 열거는 실패합니다.<br /><br /> 설정이 FALSE(기본값)이면 유니캐스트 응답이 3초 동안 허용됩니다. 이 시간 길이는 구성할 수 없습니다. 혼잡하거나 지연 시간이 긴 네트워크 또는 부하가 높은 서버의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 열거하려고 시도하면 부분적인 목록만 반환되어 사용자에게 잘못된 정보를 줄 수 있습니다.|  
|<a name="BKMK_IPsec"></a> IPsec 트래픽|UDP 포트 500 및 UDP 포트 4500|도메인 정책에 따라 IPSec을 통해 네트워크 통신을 수행해야 하는 경우 예외 목록에 UDP 포트 4500 및 UDP 포트 500도 추가해야 합니다. IPsec은 Windows 방화벽 스냅인의 **새 인바운드 규칙 마법사** 를 사용하는 옵션입니다. 자세한 내용은 아래의 [고급 보안이 포함된 Windows 방화벽 스냅인 사용](#BKMK_WF_msc) 을 참조하세요.|  
|트러스트된 도메인에 Windows 인증 사용|인증 요청을 허용하도록 방화벽을 구성해야 합니다.|자세한 내용은 [도메인 및 트러스트를 위한 방화벽을 구성하는 방법](https://support.microsoft.com/kb/179442/)을 참조하세요.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 클러스터링|클러스터링을 위해서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 직접 관련되지 않은 추가 포트가 필요합니다.|자세한 내용은 [클러스터 사용을 위한 네트워크 설정(Enable a network for cluster use)](https://go.microsoft.com/fwlink/?LinkId=118372)을 참조하세요.|  
|HTTP 서버 API(HTTP.SYS)에 예약된 URL 네임스페이스|일반적으로 TCP 포트 80이지만 다른 포트로 구성할 수 있습니다. 자세한 내용은 [HTTP 및 HTTPS 구성(Configuring HTTP and HTTPS)](https://go.microsoft.com/fwlink/?LinkId=118373)을 참조하세요.|HttpCfg.exe를 사용한 HTTP.SYS 엔드포인트 예약에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 정보는 [URL 예약 및 등록 정보 &#40;SSRS 구성 관리자 &#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)를 참조하세요.|  
  
##  <a name="BKMK_port_135"></a> 포트 135에 대한 특별 고려 사항  
 TCP/IP 또는 UDP/IP를 전송 수단으로 하여 RPC를 사용하는 경우 인바운드 포트는 필요에 따라 시스템 서비스에 동적으로 할당되는 경우가 많습니다. 포트 1024보다 큰 TCP/IP 및 UDP/IP 포트가 사용됩니다. 이러한 포트를 비공식적으로 "임의 RPC 포트"라고 합니다. 이 경우 RPC 클라이언트는 RPC 엔드포인트 매퍼를 사용하여 서버에 할당된 동적 포트를 알려 줍니다. 일부 RPC 기반 서비스의 경우 RPC가 포트를 동적으로 할당하도록 하는 대신 사용자가 직접 특정 포트를 구성할 수 있습니다. 또한 서비스에 관계없이 RPC가 동적으로 할당하는 포트의 범위를 좁은 범위로 제한할 수도 있습니다. 포트 135는 많은 서비스에서 사용되기 때문에 악의적인 사용자로부터 자주 공격을 받습니다. 포트 135를 열 때는 방화벽 규칙의 범위를 제한하는 것이 좋습니다.  
  
 포트 135에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [Windows 서버 시스템의 서비스 개요 및 네트워크 포트 요구 사항](https://support.microsoft.com/kb/832017)   
-   [제품 CD에 포함된 Windows Server 2003 지원 도구를 사용하여 RPC 엔드포인트 매퍼 오류 문제 해결](https://support.microsoft.com/kb/839880)  
-   [RPC(원격 프로시저 호출)(Remote procedure call (RPC))](https://go.microsoft.com/fwlink/?LinkId=118375)    
-   [방화벽에 사용할 RPC 동적 포트 할당을 구성하는 방법](https://support.microsoft.com/kb/154596/)  
  
##  <a name="BKMK_other_rules"></a> 다른 방화벽 규칙과의 상호 작용  
 Windows 방화벽은 규칙 및 규칙 그룹을 사용하여 구성을 설정합니다. 각 규칙 또는 규칙 그룹은 일반적으로 특정 프로그램이나 서비스와 연결되며, 이 프로그램 또는 서비스는 사용자 모르게 규칙을 수정하거나 삭제할 수 있습니다. 예를 들어 **World Wide Web 서비스(HTTP)** 및 **World Wide Web 서비스(HTTPS)** 규칙 그룹은 IIS와 연결됩니다. 이러한 규칙을 사용하도록 설정하면 포트 80 및 443이 열리고 포트 80 및 443을 이용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능이 작동합니다. 그러나 IIS를 구성 중인 관리자가 이러한 규칙을 수정하거나 해제할 수 있습니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포트 80 또는 포트 443을 사용하는 경우 다른 IIS 규칙에 관계없이 자신이 원하는 포트 구성을 유지하는 고유한 규칙 또는 규칙 그룹을 만들어야 합니다.  
  
 고급 보안이 설정된 Windows 방화벽 MMC 스냅인은 적용 가능한 모든 허용 규칙에 일치하는 모든 트래픽을 허용합니다. 따라서 포트 80에 두 개의 규칙이 서로 다른 매개 변수를 사용하여 적용되는 경우 트래픽은 어느 한쪽의 규칙에만 일치하면 허용됩니다. 즉, 한 규칙은 로컬 서브넷에서 포트 80을 통한 트래픽을 허용하고 다른 규칙은 모든 주소의 트래픽을 허용한다면 결과적으로 트래픽의 출처에 관계없이 포트 80에 대한 모든 트래픽이 허용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스를 효율적으로 관리하려면 관리자는 서버에 설정된 모든 방화벽 규칙을 정기적으로 검토해야 합니다.  
  
##  <a name="BKMK_profiles"></a> 방화벽 프로필 개요  
 방화벽 프로필은 운영 체제가 연결된 각 네트워크를 연결 상태, 연결 방식 및 범주에 따라 식별하고 기억하기 위해 사용합니다.  
  
 고급 보안이 설정된 Windows 방화벽에는 3개의 네트워크 위치 유형이 있습니다.  
  
-   **도메인**: Windows는 컴퓨터가 참여하고 있는 도메인의 도메인 컨트롤러에 대한 액세스를 인증할 수 있습니다.
-   **공용**: 도메인 네트워크 이외의 모든 네트워크는 처음에 공용 네트워크로 분류됩니다. 인터넷에 직접 연결되는 네트워크 또는 공항 및 커피숍과 같이 공개된 위치에 있는 네트워크는 공용으로 유지해야 합니다.
-   **프라이빗**: 사용자 또는 애플리케이션에 의해 프라이빗 네트워크로 식별되는 네트워크입니다. 트러스트된 네트워크만 프라이빗 네트워크로 식별되어야 합니다. 홈 네트워크 또는 소규모 기업 네트워크를 프라이빗 네트워크로 식별하는 경우가 많습니다.  
  
 관리자는 서로 다른 방화벽 정책이 포함된 각 프로필을 사용하여 각 네트워크 위치 유형에 대한 프로필을 만들 수 있습니다. 항상 하나의 프로필만 적용됩니다. 프로필 순서는 다음과 같이 적용됩니다.  
  
1.  컴퓨터가 멤버로 속해 있는 도메인에 대한 도메인 컨트롤러에 모든 인터페이스가 인증될 경우 도메인 프로필이 적용됩니다.    
2.  모든 인터페이스가 도메인 컨트롤러에 인증되거나 프라이빗 네트워크 위치로 분류되는 네트워크에 연결된 경우 프라이빗 프로필이 적용됩니다.    
3.  그렇지 않으면 공용 프로필이 적용됩니다.  
  
 고급 보안이 설정된 Windows 방화벽 MMC 스냅인을 사용하여 모든 방화벽 프로필을 보고 구성할 수 있습니다. 제어판의 **Windows 방화벽** 항목에서는 현재 프로필만 구성할 수 있습니다.  
  
##  <a name="BKMK_additional_settings"></a> 제어판의 Windows 방화벽을 사용한 추가 방화벽 설정  
 방화벽에 예외를 추가하여 특정 컴퓨터나 로컬 서브넷에서 들어오는 연결에 대해 포트 열기를 제한할 수 있습니다. 포트 열기 범위에 대한 이러한 제한은 컴퓨터가 악의적인 사용자에게 노출되는 정도를 줄여줄 수 있는 권장되는 방법입니다.  
  
> [!NOTE]  
>  제어판의 **Windows 방화벽** 항목을 사용하면 현재 방화벽 프로필만 구성됩니다.  
  
### <a name="to-change-the-scope-of-a-firewall-exception-using-the-windows-firewall-item-in-control-panel"></a>제어판의 Windows 방화벽 항목을 사용하여 방화벽 예외 범위를 변경하려면  
  
1.  제어판의 **Windows 방화벽** 항목에 있는 **예외** 탭에서 프로그램 또는 포트를 선택한 다음 **속성** 또는 **편집**을 클릭합니다.  
  
2.  **프로그램 편집** 또는 **포트 편집** 대화 상자에서 **범위 변경**을 클릭합니다.  
  
3.  다음 옵션 중 하나를 선택합니다.  
  
    -   **모든 컴퓨터(인터넷의 컴퓨터를 포함)** : 이 옵션은 사용하지 않는 것이 좋습니다. 이 옵션을 사용하면 사용자의 컴퓨터를 식별할 수 있는 모든 컴퓨터가 지정된 프로그램 또는 포트에 연결할 수 있습니다. 인터넷의 익명 사용자에게 정보를 제공할 때는 이 설정이 필요할 수 있지만 악의적인 사용자에 대한 노출 위험도 높아집니다. 이 옵션을 설정하고 에지 통과 허용 옵션과 같은 NAT(네트워크 주소 변환) 통과를 허용할 경우 노출 위험이 더 높아질 수 있습니다.  
  
    -   **내 네트워크(서브넷)만**: **모든 컴퓨터**보다 안전한 설정입니다. 사용자 네트워크의 로컬 서브넷에 있는 컴퓨터만 프로그램 또는 포트에 연결할 수 있습니다.  
  
    -   **사용자 지정 목록**: 목록에 있는 IP 주소의 컴퓨터만 연결할 수 있습니다. 이 옵션은 **내 네트워크(서브넷)만**보다 안전할 수 있지만 DHCP를 사용하는 클라이언트 컴퓨터의 IP 주소는 가끔 변경될 수 있습니다. 이 경우 연결이 허용된 컴퓨터가 연결하지 못하게 됩니다. 또한 권한을 부여하지 않은 다른 컴퓨터가 목록에 있는 IP 주소를 획득하여 연결할 수 있습니다. **사용자 지정 목록** 옵션은 고정 IP 주소를 사용하도록 구성된 다른 서버를 나열하는 데는 적합하지만 IP 주소는 침입자의 스푸핑 공격을 받을 수 있습니다. 방화벽 제한 규칙은 네트워크 인프라 자체의 보안 수준 내에서 보호 기능을 제공할 뿐입니다.  
  
##  <a name="BKMK_WF_msc"></a> 고급 보안이 설정된 Windows 방화벽 스냅인 사용  
 고급 보안이 포함된 Windows 방화벽 MMC 스냅인을 사용하여 추가 고급 방화벽 설정을 구성할 수 있습니다. 이 스냅인은 규칙 마법사를 포함하며 제어판의 **Windows 방화벽** 항목에는 제공되지 않는 추가 설정을 제공합니다. 여기에는 다음과 같은 설정이 포함됩니다.  
  
-   암호화 설정  
-   서비스 제한   
-   컴퓨터 이름별 연결 제한    
-   특정 사용자 또는 프로필에 대한 연결 제한  
-   NAT(네트워크 주소 변환) 라우터를 우회하는 에지 통과 허용 트래픽    
-   아웃바운드 규칙 구성    
-   보안 규칙 구성    
-   들어오는 연결에 IPsec 요구  
  
### <a name="to-create-a-new-firewall-rule-using-the-new-rule-wizard"></a>새 규칙 마법사를 사용하여 새 방화벽 규칙을 만들려면  
  
1.  시작 메뉴에서 **실행**을 클릭한 다음, **WF.msc**를 입력하고 **확인**을 클릭합니다.    
2.  **고급 보안이 포함된 Windows 방화벽**의 왼쪽 창에서 **인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 다음, **새 규칙**을 선택합니다.   
3.  원하는 설정을 사용하여 **새 인바운드 규칙 마법사** 를 완료합니다.  
  
##  <a name="BKMK_troubleshooting"></a> 방화벽 설정 문제 해결  
 다음 도구 및 기술은 방화벽 문제를 해결하는 데 유용합니다.  
  
-   유효 포트 상태는 포트와 관련된 모든 규칙의 합집합입니다. 포트를 통한 액세스를 차단하려는 경우 해당 포트 번호가 포함된 모든 규칙을 검토하는 것이 좋습니다. 이렇게 하려면 고급 보안이 설정된 Windows 방화벽 MMC 스냅인을 사용하여 포트 번호별로 인바운드 및 아웃바운드 규칙을 정렬합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행 중인 컴퓨터에서 활성 상태인 포트를 검토합니다. 이 검토 과정에는 수신하고 있는 TCP/IP 포트를 확인하는 단계와 포트 상태를 확인하는 단계도 포함됩니다.  
  
     수신 대기 중인 포트를 확인하려면 **netstat** 명령줄 유틸리티를 사용합니다. **netstat** 유틸리티는 활성 TCP 연결을 표시할 뿐 아니라 다양한 IP 통계와 정보도 표시합니다.  
  
    #### <a name="to-list-which-tcpip-ports-are-listening"></a>수신하고 있는 TCP/IP 포트를 나열하려면  
  
    1.  명령 프롬프트 창을 엽니다.  
  
    2.  명령 프롬프트에서 **netstat -n -a**를 입력합니다.  
  
         **-n** 스위치를 지정하면 **netstat** 에서 활성 TCP 연결의 주소와 포트 번호를 숫자로 표시합니다. **-a** 스위치를 지정하면 **netstat** 에서 컴퓨터가 수신 대기 중인 TCP 및 UDP 포트를 표시합니다.  
  
-   **PortQry** 유틸리티를 사용하면 TCP/IP 포트 상태를 수신 대기 중, 수신 대기 중 아님 또는 필터링됨으로 보고할 수 있습니다. 필터링됨(filtered) 상태의 경우 포트가 수신 중일 수도 있고 수신 중이 아닐 수도 있습니다. 이 상태는 유틸리티가 포트로부터 응답을 수신하지 못했음을 나타냅니다. **PortQry** 유틸리티는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=17148)에서 다운로드할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Windows 서버 시스템의 서비스 개요 및 네트워크 포트 요구 사항](https://support.microsoft.com/kb/832017)   
 [방법: 방화벽 설정 구성(Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  
