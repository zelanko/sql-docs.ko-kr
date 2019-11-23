---
title: Analysis Services 액세스를 허용 하도록 Windows 방화벽 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ports [Analysis Services]
- Windows Firewall [Analysis Services]
- firewall systems [Analysis Services]
ms.assetid: 7673acc5-75f0-4703-9ce2-87425ea39d49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b74c767c50e8a62c2d65ad089e386a94b9c8a5e
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70151856"
---
# <a name="configure-the-windows-firewall-to-allow-analysis-services-access"></a>Analysis Services 액세스를 허용하도록 Windows 방화벽 구성
  네트워크에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 을 사용할 수 있도록 만드는 데 필수적인 첫 번째 단계는 방화벽에서 포트를 차단 해제해야 할지 여부를 결정하는 것입니다. 대부분 설치의 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 연결을 허용하는 하나 이상의 인바운드 방화벽 규칙을 만들어야 합니다.  
  
 방화벽 구성에 대한 요구 사항은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 설치한 방법에 따라 다릅니다.  
  
-   기본 인스턴스를 설치하거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 장애 조치(Failover) 클러스터를 만들 때 TCP 포트 2383을 엽니다.  
  
-   명명된 인스턴스를 설치할 때 TCP 포트 2382를 엽니다. 명명된 인스턴스는 동적 포트 할당을 사용합니다. Analysis Services용 검색 서비스인 SQL Server Browser 서비스는 TCP 포트 2382에서 수신 대기하고 연결 요청을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 현재 사용되는 포트로 리디렉션합니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 2013을 지원하도록 SharePoint 모드에서 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 를 설치할 때 TCP 포트 2382를 엽니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 SharePoint 외부에 있습니다. 명명된 'PowerPivot' 인스턴스에 대한 인바운드 요청은 네트워크 연결을 통해 SharePoint 웹 애플리케이션에서 이루어지며 열린 포트가 필요합니다. 다른 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명명된 인스턴스와 마찬가지로 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]에 대한 액세스를 허용하도록 TCP 2382의 SQL Server Browser 서비스에 대한 인바운드 규칙을 만드십시오.  
  
-   [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010의 경우에는 Windows 방화벽에서 포트를 열지 마십시오. SharePoint의 추가 기능인 이 서비스는 SharePoint에 대해 구성된 포트를 사용하며 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 모델을 로드 및 쿼리하는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 인스턴스에 로컬로만 연결합니다.  
  
-   Azure Virtual Machines에서 실행 중인 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 경우 서버 액세스를 구성 하는 데 필요한 다른 지침을 사용 합니다. [Azure Virtual Machines에서 비즈니스 인텔리전스 SQL Server를](https://msdn.microsoft.com/library/windowsazure/jj992719.aspx)참조 하세요.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기본 인스턴스는 TCP 포트 2383에서 수신 대기 하지만 다른 고정 포트에서 수신 하도록 서버를 구성할 수 있습니다. \<servername >:\<portnumber > 형식으로 서버에 연결 합니다.  
  
 하나의 TCP 포트만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 사용할 수 있습니다. 여러 네트워크 카드 또는 여러 IP 주소가 있는 컴퓨터에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 컴퓨터에 할당되거나 컴퓨터의 별칭을 가진 모든 IP 주소에 대해 하나의 TCP 포트에서 수신 대기합니다. 여러 포트 요구 사항이 있는 경우 HTTP 액세스에 대해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 구성하는 것이 좋습니다. 그런 다음 선택한 포트에서 여러 HTTP 엔드포인트를 설정할 수 있습니다. [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](configure-http-access-to-analysis-services-on-iis-8-0.md)을 참조하세요.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [Analysis Services의 포트 및 방화벽 설정 확인](#bkmk_checkport)  
  
-   [Analysis Services의 기본 인스턴스에 대한 Windows 방화벽 구성](#bkmk_default)  
  
-   [Analysis Services의 명명된 인스턴스에 대한 Windows 방화벽 액세스 구성](#bkmk_named)  
  
-   [Analysis Services 클러스터에 대한 포트 구성](#bkmk_cluster)  
  
-   [SharePoint용 PowerPivot에 대 한 포트 구성](#bkmk_powerpivot)  
  
-   [Analysis Services의 기본 인스턴스 및 명명된 인스턴스에 대해 고정 포트 사용](#bkmk_fixed)  
  
 기본 Windows 방화벽 설정 방법과 데이터베이스 엔진, Analysis Services, Reporting Services 및 Integration Services에 영향을 주는 TCP 포트에 대한 설명은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
##  <a name="bkmk_checkport"></a> Analysis Services의 포트 및 방화벽 설정 확인  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]가 지원하는 Microsoft Windows 운영 체제에서는 기본적으로 Windows 방화벽이 설정되어 원격 연결을 차단합니다. 방화벽에서 수동으로 포트를 열어 Analysis Services에 대한 인바운드 요청을 허용해야 합니다. SQL Server 설치 프로그램에서는 이 단계를 수행하지 않습니다.  
  
 포트 설정은 msmdsrv.ini 파일 및 SQL Server Management Studio의 Analysis Services 인스턴스 일반 속성 페이지에서 지정됩니다. `Port`가 양수로 설정된 경우 서비스는 고정 포트에서 수신 대기합니다. `Port`가 0으로 설정된 경우 서비스는 기본 인스턴스인 경우 포트 2383에서, 명명된 인스턴스인 경우 동적으로 할당된 포트에서 수신 대기합니다.  
  
 동적 포트 할당은 명명된 인스턴스에서만 사용합니다. `MSOLAP$InstanceName` 서비스는 시작할 때, 사용할 포트를 결정합니다. 다음을 수행하여 명명된 인스턴스가 사용하는 실제 포트 번호를 확인할 수 있습니다.  
  
-   작업 관리자를 시작한 다음 **서비스** 를 클릭 하 여 `MSOLAP$InstanceName`의 PID를 가져옵니다.  
  
-   명령줄에서 `netstat -ao -p TCP`를 실행하여 해당 PID의 TCP 포트 정보를 확인합니다.  
  
-   SQL Server Management Studio를 사용 하 여 포트를 확인 하 고 Analysis Services 서버에 \<IPAddress >:\<portnumber > 형식으로 연결 합니다.  
  
 애플리케이션이 특정 포트에서 수신 대기하고 있더라도 방화벽에서 액세스를 차단하면 연결에 성공할 수 없습니다. 명명된 Analysis Services 인스턴스에 연결하려면 msmdsrv.exe 또는 msmdsrv.exe가 방화벽에서 수신 대기하고 있는 고정 포트에 대한 액세스 차단을 해제해야 합니다. 이 항목의 남은 섹션에서는 액세스 차단을 해제하는 방법에 대한 지침을 제공합니다.  
  
 Analysis Services에 대해 방화벽 설정이 이미 정의되어 있는지 확인하려면 제어판에서 고급 보안이 포함된 Windows 방화벽을 사용합니다. 모니터링 폴더의 방화벽 페이지에는 로컬 서버에 대해 정의된 전체 규칙 목록이 표시됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 경우 모든 방화벽 규칙을 수동으로 정의해야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 SQL Server Browser가 포트 2382와 2383을 예약하고 있기는 하지만, SQL Server 설치 프로그램도 어떤 구성 도구도 포트 또는 프로그램 실행 파일에 대한 액세스를 허용하는 방화벽 규칙을 정의하지는 않습니다.  
  
##  <a name="bkmk_default"></a> Analysis Services의 기본 인스턴스에 대한 Windows 방화벽 구성  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 기본 인스턴스는 TCP 포트 2383에서 수신 대기합니다. 설치한 기본 인스턴스에 이 포트를 사용하려는 경우 Windows 방화벽에서 TCP 포트 2383에 대한 인바운드 액세스의 차단을 해제해야만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 기본 인스턴스에 대한 원격 액세스를 설정할 수 있습니다. 기본 인스턴스를 설치했지만 고정 포트를 수신하도록 서비스를 구성하려는 경우 이 항목의 [Analysis Services의 기본 인스턴스 및 명명된 인스턴스에 대해 고정 포트 사용](#bkmk_fixed) 을 참조하십시오.  
  
 서비스가 기본 인스턴스(MSSQLServerOLAPService)로 실행되고 있는지 확인하려면 SQL Server 구성 관리자에서 서비스 이름을 확인하십시오. Analysis Services 기본 인스턴스는 언제나 **SQL Server Analysis Services(MSSQLSERVER)** 로 표시됩니다.  
  
> [!NOTE]  
>  다른 Windows 운영 체제에서는 다른 도구를 사용하여 Windows 방화벽을 구성할 수 있습니다. 대부분의 도구에서는 특정 포트 또는 프로그램 실행 파일 중 하나를 선택할 수 있습니다. 프로그램 실행 파일을 지정해야 하는 특별한 이유가 없다면 포트를 지정하는 것이 좋습니다.  
  
 인바운드 규칙을 지정할 때 나중에 규칙을 쉽게 찾을 수 있도록 명명 규칙을 적용해야 합니다(예: **SQL Server Analysis Services (TCP-in) 2383**).  
  
#### <a name="windows-firewall-with-advanced-security"></a>고급 보안이 포함된 Windows 방화벽  
  
1.  Windows 7 또는 Windows Vista에서는 제어판의 **시스템 및 보안**을 클릭하고 **Windows 방화벽**을 선택한 다음 **고급 설정**을 클릭합니다. Windows Server 2008 또는 2008 R2에서는 관리 도구를 열고 **고급 보안이 포함된 Windows 방화벽**을 클릭합니다. Windows Server 2012에서는 애플리케이션 페이지를 열고 **Windows 방화벽**을 입력합니다.  
  
2.  **인바운드 규칙** 을 마우스 오른쪽 단추로 클릭하고 **새 규칙**을 선택합니다.  
  
3.  규칙 유형에서 `Port` 클릭 하 **고 다음을 클릭 합니다.**  
  
4.  프로토콜 및 포트에서 **TCP** 를 선택한 다음 **특정 로컬 포트**에 `2383`을 입력 합니다.  
  
5.  동작에서 **연결 허용** 을 클릭하고 **다음**을 클릭합니다.  
  
6.  프로필에서 적용되지 않는 네트워크 위치의 선택을 모두 취소하고 **다음**을 클릭합니다.  
  
7.  이름에이 규칙을 설명 하는 이름 (예: `SQL Server Analysis Services (tcp-in) 2383`)을 입력 한 다음 **마침**을 클릭 합니다.  
  
8.  원격 연결이 설정되어 있는지 확인하려면 다른 컴퓨터에서 SQL Server Management Studio 또는 Excel을 열고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 이름 **에 서버의 네트워크 이름을 지정하여**에 연결합니다.  
  
    > [!NOTE]  
    >  서버에 대한 액세스 권한을 부여할 때까지 다른 사용자는 해당 서버에 액세스하지 못합니다. 자세한 내용은 [개체 및 작업에 대한 액세스 승인&#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)을 참조하세요.  
  
#### <a name="netsh-advfirewall-syntax"></a>Netsh AdvFirewall 구문  
  
-   다음 명령은 TCP 포트 2383에서 들어오는 요청을 허용하는 인바운드 규칙을 만듭니다.  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services inbound on TCP 2383" dir=in action=allow protocol=TCP localport=2383 profile=domain  
    ```  
  
##  <a name="bkmk_named"></a> Analysis Services의 명명된 인스턴스에 대한 Windows 방화벽 액세스 구성  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 명명된 인스턴스는 고정 포트 또는 동적으로 할당된 포트에서 수신 대기할 수 있습니다. 이러한 포트에서 SQL Server Browser 서비스는 연결 시 서비스의 현재 연결 정보를 제공합니다.  
  
 SQL Server Browser 서비스는 TCP 포트 2382에서 수신 대기합니다. UDP는 이 사용되지 않습니다. TCP는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 사용하는 유일한 전송 프로토콜입니다.  
  
 다음과 같은 방법을 선택하여 Analysis Services의 명명된 인스턴스에 대한 원격 액세스를 설정할 수 있습니다.  
  
-   동적 포트 할당 및 SQL Server Browser 서비스를 사용합니다. Windows 방화벽에서 SQL Server Browser 서비스에 사용되는 포트를 차단 해제합니다. 다음 형식으로 서버에 연결 합니다. \<servername >\\< instancename\>.  
  
-   고정 포트 및 SQL Server Browser 서비스를 함께 사용합니다. 이 방법에서는 동적 포트 할당 방법과 동일 하 게 \<servername >\\< instancename\>을 사용 하 여 연결할 수 있습니다. 단,이 경우 서버가 고정 포트에서 수신 대기 합니다. 이 시나리오에서 SQL Server Browser 서비스는 고정 포트에서 수신하는 Analysis Services 인스턴스에 이름 확인을 제공합니다. 이 방법을 사용하려면 고정 포트에서 수신하도록 서버를 구성하고, 해당 포트에 대한 액세스 및 SQL Server Browser 서비스에 사용되는 포트에 대한 액세스를 차단 해제합니다.  
  
 SQL Server Browser 서비스는 기본 인스턴스가 아닌 명명된 인스턴스와만 사용됩니다. 이 서비스는 SQL Server 기능을 명명된 인스턴스로 설치할 때마다 자동으로 설치되고 사용되도록 설정됩니다. SQL Server Browser 서비스가 필요한 방법을 선택한 경우 해당 서비스가 서버에서 사용되도록 설정되어 있고 시작되었는지 확인해야 합니다.  
  
 SQL Server Browser 서비스를 사용할 수 없는 경우에는 연결 문자열의 고정 포트를 할당하고 도메인 이름 확인을 무시해야 합니다. SQL Server Browser 서비스를 사용하지 않는 모든 클라이언트 연결은 연결 문자열에 포트 번호를 포함해야 합니다(예: AW-SRV01:54321).  
  
 **옵션 1: 동적 포트 할당을 사용하고 SQL Server Browser 서비스에 대한 액세스를 차단 해제합니다.**  
  
 Analysis Services의 명명된 인스턴스에 대한 동적 포트 할당은 `MSOLAP$InstanceName` 서비스가 시작될 때 이 서비스에 의해 설정됩니다. 기본적으로 서비스는 찾은 포트 번호 중 첫 번째로 사용 가능한 포트 번호를 사용합니다(서비스가 다시 시작될 때마다 다른 포트 번호 사용).  
  
 인스턴스 이름 확인은 SQL Server Browser 서비스에서 처리합니다. 명명된 인스턴스에 동적 포트 할당을 사용하는 경우에는 항상 SQL Server Browser 서비스에 대해 TCP 포트 2382를 차단 해제해야 합니다.  
  
> [!NOTE]  
>  SQL Server Browser 서비스는 Database Engine 및 Analysis Services에 대해 각각 UDP 포트 1434와 TCP 포트 2382에서 수신 대기합니다. SQL Server Browser 서비스에 대해 UDP 포트 1434의 차단을 이미 해제한 경우에도 Analysis Services에 대해 TCP 포트 2382의 차단을 해제해야 합니다.  
  
#### <a name="windows-firewall-with-advanced-security"></a>고급 보안이 포함된 Windows 방화벽  
  
1.  Windows 7 또는 Windows Vista에서는 제어판의 **시스템 및 보안**을 클릭하고 **Windows 방화벽**을 선택한 다음 **고급 설정**을 클릭합니다. Windows Server 2008 또는 2008 R2에서는 관리 도구를 열고 **고급 보안이 포함된 Windows 방화벽**을 클릭합니다. Windows Server 2012에서는 애플리케이션 페이지를 열고 **Windows 방화벽**을 입력합니다.  
  
2.  SQL Server Browser 서비스에 대한 액세스 차단을 해제하려면 **인바운드 규칙** 을 마우스 오른쪽 단추로 클릭한 후 **새 규칙**을 클릭합니다.  
  
3.  규칙 유형에서 `Port` 클릭 하 **고 다음을 클릭 합니다.**  
  
4.  프로토콜 및 포트에서 **TCP** 를 선택한 다음 **특정 로컬 포트**에 `2382`을 입력 합니다.  
  
5.  동작에서 **연결 허용** 을 클릭하고 **다음**을 클릭합니다.  
  
6.  프로필에서 적용되지 않는 네트워크 위치의 선택을 모두 취소하고 **다음**을 클릭합니다.  
  
7.  이름에이 규칙을 설명 하는 이름 (예: `SQL Server Browser Service (tcp-in) 2382`)을 입력 한 다음 **마침**을 클릭 합니다.  
  
8.  원격 연결이 설정 되어 있는지 확인 하려면 다른 컴퓨터에서 SQL Server Management Studio 또는 Excel을 열고 서버의 네트워크 이름 및 인스턴스 이름을 \<servername >\\< instancename\>형식으로 지정 하 여 Analysis Services에 연결 합니다. 예를 들어 서버 이름은 **AW-SRV01** 이고 명명된 인스턴스 이름은 **Finance**인 경우 네트워크 서버 이름은 **AW-SRV01\Finance**가 됩니다.  
  
 **옵션 2: 명명된 인스턴스에 고정 포트 사용**  
  
 고정 포트를 할당한 다음 해당 포트에 대한 액세스 차단을 해제할 수도 있습니다. 이 방법을 사용하면 프로그램 실행 파일에 대한 액세스를 허용하는 경우보다 감사 기능의 효율성이 더 높아집니다. 이러한 이유 때문에 Analysis Services 인스턴스에 액세스하기 위한 방법으로 고정 포트를 사용하도록 권장됩니다.  
  
 고정 포트를 할당하려면 이 항목의 [Analysis Services의 기본 인스턴스 및 명명된 인스턴스에 대해 고정 포트 사용](#bkmk_fixed) 에 있는 지침을 따르고 이 섹션으로 돌아와 포트를 차단 해제하십시오.  
  
#### <a name="windows-firewall-with-advanced-security"></a>고급 보안이 포함된 Windows 방화벽  
  
1.  Windows 7 또는 Windows Vista에서는 제어판의 **시스템 및 보안**을 클릭하고 **Windows 방화벽**을 선택한 다음 **고급 설정**을 클릭합니다. Windows Server 2008 또는 2008 R2에서는 관리 도구를 열고 **고급 보안이 포함된 Windows 방화벽**을 클릭합니다. Windows Server 2012에서는 애플리케이션 페이지를 열고 **Windows 방화벽**을 입력합니다.  
  
2.  Analysis Services에 대한 액세스 차단을 해제하려면 **인바운드 규칙** 을 마우스 오른쪽 단추로 클릭한 후 **새 규칙**을 클릭합니다.  
  
3.  규칙 유형에서 `Port` 클릭 하 **고 다음을 클릭 합니다.**  
  
4.  프로토콜 및 포트에서 **TCP** 를 선택한 다음 **특정 로컬 포트**에 고정 포트를 입력합니다.  
  
5.  동작에서 **연결 허용** 을 클릭하고 **다음**을 클릭합니다.  
  
6.  프로필에서 적용되지 않는 네트워크 위치의 선택을 모두 취소하고 **다음**을 클릭합니다.  
  
7.  이름에이 규칙을 설명 하는 이름 (예: `SQL Server Analysis Services on port 54321`)을 입력 한 다음 **마침**을 클릭 합니다.  
  
8.  원격 연결이 설정 되어 있는지 확인 하려면 다른 컴퓨터에서 SQL Server Management Studio 또는 Excel을 열고 서버의 네트워크 이름 및 포트 번호를 \<servername >:\<portnumber > 형식으로 지정 하 여 Analysis Services에 연결 합니다.  
  
#### <a name="netsh-advfirewall-syntax"></a>Netsh AdvFirewall 구문  
  
-   다음 명령은 SQL Server Browser용 TCP 2382를 차단 해제하고 Analysis Services 인스턴스에 대해 지정한 고정 포트의 차단을 해제하는 인바운드 규칙을 만듭니다. 해당 명령 중 하나를 실행하여 명명된 Analysis Services 인스턴스에 대한 액세스를 허용할 수 있습니다.  
  
     이 예제 명령에서 포트 54321은 고정 포트입니다. 이 포트를 시스템에서 실제로 사용하는 포트로 바꾸십시오.  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services (tcp-in) on 54321" dir=in action=allow protocol=TCP localport=54321 profile=domain  
    ```  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Browser Services inbound on TCP 2382" dir=in action=allow protocol=TCP localport=2382 profile=domain  
    ```  
  
##  <a name="bkmk_fixed"></a> Analysis Services의 기본 인스턴스 및 명명된 인스턴스에 대해 고정 포트 사용  
 이 섹션에서는 고정 포트에서 수신 대기하도록 Analysis Services를 구성하는 방법에 대해 설명합니다. Analysis Services를 명명된 인스턴스로 설치한 경우 고정 포트를 사용하는 것이 일반적이지만 비즈니스 또는 보안 요구 사항에 따라 기본이 아닌 포트 할당을 사용해야 하는 경우에도 이 방법을 사용할 수 있습니다.  
  
 고정 포트를 사용하면 서버 이름 뒤에 포트 번호를 추가해야 하므로 기본 인스턴스에 대한 연결 구문이 변경됩니다. 예를 들어 SQL Server Management Studio에서 포트 54321에서 수신하는 기본 로컬 Analysis Services 인스턴스에 연결하는 경우 Management Studio의 '서버에 연결' 대화 상자에 서버 이름으로 localhost:54321을 입력해야 합니다.  
  
 명명 된 인스턴스를 사용 하는 경우 서버 이름 지정 방법을 변경 하지 않고 고정 포트를 할당할 수 있습니다. 특히 \<servername\instancename >를 사용 하 여 고정 포트에서 수신 대기 하는 명명 된 인스턴스에 연결할 수 있습니다. SQL Server Browser 서비스가 실행되고 있으며 해당 서비스가 수신 대기 중인 포트를 차단 해제한 경우에만 이 방법이 가능합니다. SQL Server Browser 서비스는 \<servername\instancename >에 따라 고정 포트에 대 한 리디렉션을 제공 합니다. 고정 포트에서 수신 대기하는 SQL Server Browser 서비스 및 Analysis Services의 명명된 인스턴스 모두에 대해 포트를 열기만 하면 SQL Server Browser 서비스는 명명된 인스턴스에 대한 연결을 확인합니다.  
  
1.  사용 가능한 TCP/IP 포트 중에서 사용할 포트를 결정합니다.  
  
     사용하지 않아야 하는 예약된 포트와 등록된 포트의 목록을 보려면 [Port Numbers(IANA)](https://go.microsoft.com/fwlink/?LinkID=198469)(포트 번호)를 참조하세요. 시스템에서 이미 사용 중인 포트의 목록을 보려면 명령 프롬프트 창을 열고 `netstat -a -p TCP`를 입력하여 시스템에서 열려 있는 TCP 포트의 목록을 표시합니다.  
  
2.  사용할 포트를 결정한 후 SQL Server Management Studio의 Analysis Services 인스턴스 일반 속성 페이지 또는 msmdsrv.ini 파일에서 `Port` 구성 설정을 편집하여 포트를 지정합니다.  
  
3.  서비스를 다시 시작합니다.  
  
4.  지정한 TCP 포트의 차단을 해제하도록 Windows 방화벽을 구성합니다. 명명된 인스턴스에 고정 포트를 사용하는 경우에는 해당 인스턴스에 대해 지정한 TCP 포트 및 SQL Server Browser 서비스에 대한 TCP 포트 2382의 차단을 해제합니다.  
  
5.  Management Studio에서 로컬로 연결하여 확인한 다음 다른 컴퓨터의 클라이언트 애플리케이션에서 원격으로 연결하여 확인합니다. Management Studio를 사용 하려면 서버 이름을 \<servername >:\<portnumber > 형식으로 지정 하 여 Analysis Services 기본 인스턴스에 연결 합니다. 명명 된 인스턴스의 경우 서버 이름을 \<servername >\\< instancename\>으로 지정 합니다.  
  
##  <a name="bkmk_cluster"></a> Analysis Services 클러스터에 대한 포트 구성  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 장애 조치(failover) 클러스터는 기본 인스턴스 또는 명명된 인스턴스로 설치했는지 여부에 관계없이 항상 TCP 포트 2383에서 수신합니다. 동적 포트 할당은 Windows 장애 조치(failover) 클러스터에 설치되어 있는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 사용되지 않습니다. 클러스터에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 클러스터에.를 실행하는 모든 노드에서 TCP 2383을 열어야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]클러스터링에 대한 자세한 내용은 [SQL Server Analysis Services를 클러스터링하는 방법](https://go.microsoft.com/fwlink/p/?LinkId=396548)을 참조하십시오.  
  
##  <a name="bkmk_powerpivot"></a>SharePoint용 PowerPivot에 대 한 포트 구성  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 의 서버 아키텍처는 사용 중인 SharePoint 버전에 따라 근본적으로 다릅니다.  
  
 **SharePoint 2013**  
  
 SharePoint 2013에서 Excel 서비스는 SharePoint 환경 외부의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 이후에 로드되는 Power Pivot 모델에 대한 요청을 리디렉션합니다. 연결은 일반 패턴을 따르며 여기서 로컬 컴퓨터의 Analysis Services 클라이언트 라이브러리는 연결 요청을 같은 네트워크의 원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 보냅니다.  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 은 항상 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 명명된 인스턴스로 설치하기 때문에 SQL Server Browser 서비스 및 동적 포트 할당을 가정해야 합니다. 위에서 설명한 것처럼 SQL Server Browser 서비스는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명명된 인스턴스에 보낸 연결 요청을 위해 TCP 포트 2382에서 수신 대기하고 요청을 현재 포트로 리디렉션합니다.  
  
 SharePoint 2013의 Excel 서비스는 고정 포트 연결 구문을 지원하지 않으므로 SQL Server Browser 서비스에 액세스할 수 있는지 확인해야 합니다.  
  
 **SharePoint 2010**  
  
 SharePoint 2010을 설치하려는 경우에는 Windows 방화벽에서 포트를 열 필요가 없습니다. SharePoint는 필요한 포트 및 SharePoint 환경 내에서 작동하는 SharePoint용 PowerPivot과 같은 추가 기능을 엽니다. SharePoint 2010용 PowerPivot 설치에서는 PowerPivot 시스템 서비스가 같은 컴퓨터에 함께 설치된 로컬 SQL Server Analysis Services(PowerPivot) 서비스 인스턴스에 대한 독점적인 사용권을 가집니다. PowerPivot 시스템 서비스는 네트워크 연결이 아닌 로컬 연결을 사용하여 SharePoint 서버의 PowerPivot 데이터를 로드, 쿼리 및 처리하는 로컬 Analysis Services 엔진 서비스에 액세스합니다. 클라이언트 응용 프로그램에서 PowerPivot 데이터를 요청 하기 위해 요청은 SharePoint 설치 프로그램이 연 포트를 통해 라우팅됩니다. 즉, sharepoint-80, SharePoint 중앙 관리 v4, SharePoint 웹 서비스에 대 한 액세스를 허용 하도록 인바운드 규칙이 정의 됩니다. , 및 SPUserCodeV4). PowerPivot 웹 서비스는 SharePoint 팜 내부에서 실행되므로 SharePoint 팜의 PowerPivot 데이터에 원격 액세스하기 위해서는 SharePoint 방화벽 규칙만으로도 충분합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Browser 서비스&#40;데이터베이스 엔진 및 SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)   
 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
  
