---
title: "2단원: 다른 컴퓨터에서 연결 | Microsoft 문서"
ms.custom: 
ms.date: 03/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: fd4ddeb8-0cb6-441b-9704-03575c07020f
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 3e860fc71d2f9e5efcf68324040d267d9de6fce9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-2-connecting-from-another-computer"></a>2단원: 다른 컴퓨터에서 연결
보안을 강화하기 위해 처음 설치 시에는 [!INCLUDE[ssDE](../includes/ssde-md.md)] Developer, Express 및 Evaluation 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 을 다른 컴퓨터에서 액세스할 수 없습니다. 이 단원에서는 다른 컴퓨터에서 연결하기 위해 프로토콜을 설정하고 포트를 구성하며 Windows 방화벽을 구성하는 방법을 보여 줍니다.  
  
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [프로토콜 설정](#protocols)  
  
-   [고정 포트 구성](#port)  
  
-   [방화벽에서 포트 열기](#firewall)  
  
-   [다른 컴퓨터에서 데이터베이스 엔진에 연결](#otherComp)  
  
-   [SQL Server Browser 서비스를 사용하여 연결](#browser)  
  
## <a name="protocols"></a>프로토콜 설정  
보안을 강화하기 위해 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], Developer 및 Evaluation에는 제한된 네트워크 연결만 설치됩니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 에는 동일한 컴퓨터에서 실행하는 도구를 사용하여 연결할 수 있지만 다른 컴퓨터에서는 연결할 수 없습니다. [!INCLUDE[ssDE](../includes/ssde-md.md)]과 동일한 컴퓨터에서 개발 작업을 수행하려는 경우 추가 프로토콜을 사용할 필요가 없습니다. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 는 공유 메모리 프로토콜을 사용하여 [!INCLUDE[ssDE](../includes/ssde-md.md)] 에 연결합니다. 연결합니다.  
  
다른 컴퓨터에서 [!INCLUDE[ssDE](../includes/ssde-md.md)] 에 연결하려는 경우에는 TCP/IP와 같은 프로토콜을 설정해야 합니다.  
  
#### <a name="how-to-enable-tcpip-connections-from-another-computer"></a>다른 컴퓨터에서 TCP/IP 연결을 설정하는 방법  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
    > [!NOTE]  
    > 32비트 및 64비트 옵션을 모두 사용할 수 있습니다.  
  
    > [!NOTE]  
    > [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자는 독립 실행형 프로그램이 아니라 [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console 프로그램용 스냅인이므로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자는 최신 버전의 Windows에서 응용 프로그램으로 표시되지 않습니다. 파일 이름에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 버전 번호를 나타내는 번호가 포함됩니다. 실행 명령에서 구성 관리자를 열려면 Windows가 C 드라이브에 설치되어 있는 경우 최신 4개 버전의 경로는 다음과 같습니다.  
  
    |||  
    |-|-|  
    |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|  
    |[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
    |[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|  
    |[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|C:\Windows\SysWOW64\SQLServerManager10.msc|  
  
2.  **SQL Server 구성 관리자**에서 **SQL Server 네트워크 구성**을 확장한 다음 ***<InstanceName>*에 대한 프로토콜**을 클릭합니다.  
  
    기본 인스턴스(명명되지 않은 인스턴스)는 **MSSQLSERVER**로 나열됩니다. 명명된 인스턴스를 설치한 경우 제공한 이름이 나열됩니다. [!INCLUDE[ssExpressEd11](../includes/ssexpressed11-md.md)] 는 설치하는 동안 이름을 변경하지 않는 한 **SQLEXPRESS**로 설치됩니다.  
  
3.  프로토콜 목록에서 사용하도록 설정할 프로토콜(**TCP/IP**)을 마우스 오른쪽 단추로 클릭한 다음 **사용**을 클릭합니다.  
  
    > [!NOTE]  
    > 네트워크 프로토콜을 변경한 후에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스를 다시 시작해야 합니다. 이 부분은 다음 태스크에서 완료됩니다.  
  
## <a name="port"></a>고정 포트 구성  
보안을 강화하기 위해 Windows Server 2008, [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]및 Windows 7에서는 모두 Windows 방화벽을 설정합니다. 다른 컴퓨터에서 이 인스턴스에 연결하려면 방화벽에서 통신 포트를 열어야 합니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 의 기본 인스턴스는 포트 1433에서 수신하므로 고정 포트를 구성하지 않아도 됩니다. 그러나 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 을 포함한 명명된 인스턴스는 동적 포트에서 수신합니다. 방화벽에서 포트를 열려면 먼저 고정 포트 또는 정적 포트로 지정된 특정 포트에서 수신하도록 [!INCLUDE[ssDE](../includes/ssde-md.md)] 을 구성해야 합니다. 이렇게 하지 않으면 [!INCLUDE[ssDE](../includes/ssde-md.md)] 이 시작할 때마다 다른 포트에서 수신할 수 있습니다. 방화벽 및 기본 Windows 방화벽 설정에 대한 자세한 내용과 데이터베이스 엔진, Analysis Services, Reporting Services 및 Integration Services에 영향을 주는 TCP 포트에 대한 설명은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
> [!NOTE]  
> 포트 번호 할당은 Internet Assigned Numbers Authority에서 관리하며 이 목록은 [http://www.iana.org](http://go.microsoft.com/fwlink/?LinkId=48844)에서 볼 수 있습니다. 포트 번호는 49152에서 65535 사이의 숫자에서 할당해야 합니다.  
  
#### <a name="configure-sql-server-to-listen-on-a-specific-port"></a>SQL Server가 특정 포트에서 수신하도록 구성  
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자에서 **SQL Server 네트워크 구성**을 확장한 다음 구성할 서버 인스턴스를 클릭합니다.  
  
2.  오른쪽 창에서 **TCP/IP**를 두 번 클릭합니다.  
  
3.  **TCP/IP 속성** 대화 상자에서 **IP 주소** 탭을 클릭합니다.  
  
4.  **IPAll** 섹션의 **TCP 포트** 상자에 사용 가능한 포트 번호를 입력합니다. 이 자습서에서는 **49172**을 사용합니다.  
  
5.  **확인** 을 클릭하여 대화 상자를 닫고 서비스를 다시 시작해야 한다는 경고에 대해 **확인** 을 클릭합니다.  
  
6.  왼쪽 창에서 **SQL Server 서비스**를 클릭하고  
  
7.  오른쪽 창에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 클릭합니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 이 다시 시작되면 포트 **49172**에서 수신합니다.  
  
## <a name="firewall"></a>방화벽에서 포트 열기  
방화벽 시스템은 컴퓨터 리소스에 대한 무단 액세스를 방지합니다. 방화벽이 설정된 경우 다른 컴퓨터에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 연결하려면 방화벽에서 포트를 열어야 합니다.  
  
> [!IMPORTANT]  
> 방화벽의 포트를 열면 서버가 악의적인 공격에 노출될 수 있습니다. 포트를 열기 전에 방화벽 시스템을 잘 이해해야 합니다. 자세한 내용은 [Security Considerations for a SQL Server Installation](../sql-server/install/security-considerations-for-a-sql-server-installation.md)을 참조하세요.  
  
[!INCLUDE[ssDE](../includes/ssde-md.md)] 에서 고정 포트를 사용하도록 구성한 후 다음 지침에 따라 Windows 방화벽에서 해당 포트를 엽니다. 기본 인스턴스의 고정 포트는 이미 TCP 포트 1433에 고정되어 있기 때문에 구성할 필요가 없습니다.  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access-windows-7"></a>Windows 방화벽에서 TCP 액세스용 포트를 열려면(Windows 7)  
  
1.  **시작** 메뉴에서 **실행**을 클릭한 다음 **WF.msc**를 입력하고 **확인**을 클릭합니다.  
  
2.  **고급 보안이 포함된 Windows 방화벽**의 왼쪽 창에서 **인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 다음 동작 창에서 **새 규칙** 을 클릭합니다.  
  
3.  **규칙 유형** 대화 상자에서 **포트**를 선택한 다음 **다음**을 클릭합니다.  
  
4.  **프로토콜 및 포트** 대화 상자에서 **TCP**를 선택합니다. **특정 로컬 포트**를 선택한 다음 [!INCLUDE[ssDE](../includes/ssde-md.md)]인스턴스의 포트 번호를 입력합니다. 기본 인스턴스의 경우 1433을 입력합니다. 명명된 인스턴스를 구성하여 이전 태스크에서 고정 포트를 구성한 경우에는 **49172** 을 입력합니다. **다음**을 클릭합니다.  
  
5.  **동작** 대화 상자에서 **연결 허용**을 선택한 다음 **다음**을 클릭합니다.  
  
6.  **프로필** 대화 상자에서 [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결할 때의 컴퓨터 연결 환경을 설명하는 프로필을 선택한 다음 **다음**을 클릭합니다.  
  
7.  **이름** 대화 상자에 이 규칙의 이름 및 설명을 입력한 다음 **마침**을 클릭합니다.  
  
[!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]에 대한 지침을 포함하여 방화벽 구성 방법에 대한 자세한 내용은 [데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)을 참조하세요. 기본 Windows 방화벽 설정 방법과 데이터베이스 엔진, Analysis Services, Reporting Services 및 Integration Services에 영향을 주는 TCP 포트에 대한 설명은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
## <a name="otherComp"></a>다른 컴퓨터에서 데이터베이스 엔진에 연결  
[!INCLUDE[ssDE](../includes/ssde-md.md)] 에서 고정된 포트를 사용하여 수신하도록 구성하고 방화벽에서 해당 포트를 열었으므로 이제 다른 컴퓨터에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 연결할 수 있습니다.  
  
서버 컴퓨터에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 서비스를 실행 중인 상태에서 방화벽이 UDP 포트 1434를 열면 컴퓨터 이름과 인스턴스 이름을 사용하여 연결을 설정할 수 있습니다. 보안을 강화하기 위해 이 예에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 서비스를 사용하지 않습니다.  
  
#### <a name="to-connect-to-the-database-engine-from-another-computer"></a>다른 컴퓨터에서 데이터베이스 엔진에 연결하려면  
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 클라이언트 도구가 있는 두 번째 컴퓨터에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 연결할 수 있는 권한이 있는 계정으로 로그인한 다음 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]를 엽니다.  
  
2.  **서버에 연결** 대화 상자의 **서버 유형** 상자에서 **데이터베이스 엔진** 을 선택합니다.  
  
3.  **서버 이름** 상자에 **tcp:** 를 입력하여 프로토콜을 지정한 다음 컴퓨터 이름, 쉼표, 포트 번호를 차례로 입력합니다. 기본 인스턴스 연결 시에는 포트 1433이 적용되므로 포트를 생략할 수 있습니다. 따라서 **tcp:***<computer_name>*을 입력합니다. 이 예제에서 사용하는 명명된 인스턴스의 경우 **tcp:***<computer_name>***,49172**를 입력합니다.  
  
    > [!NOTE]  
    > **서버 이름** 상자에서 **tcp:**를 생략하면 클라이언트에서 설정된 모든 프로토콜을 클라이언트 구성에 지정된 순서대로 시도합니다.  
  
4.  **인증** 상자에서 **Windows 인증**을 확인한 다음 **연결**을 클릭합니다.  
  
## <a name="browser"></a>SQL Server Browser 서비스를 사용하여 연결  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 서비스에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 리소스에 대해 들어오는 요청을 수신하고 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 대한 정보를 제공합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 서비스가 실행 중인 경우 사용자는 컴퓨터 이름과 포트 번호 대신 컴퓨터 이름과 인스턴스 이름을 제공하여 명명된 인스턴스에 연결할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser에서는 인증되지 않은 UDP 요청도 수신하므로 설치 중에 설정되지 않는 경우도 있습니다. SQL Server Browser 서비스 및 이 서비스가 설정되는 경우에 대한 설명은 [SQL Server Browser 서비스&#40;데이터베이스 엔진 및 SSAS&#41;](../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)를 참조하세요.  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser를 사용하려면 이전과 동일한 단계를 따르고 방화벽에서 UDP 포트 1434를 열어야 합니다.  
  
이것으로 기본 연결에 대한 간단한 자습서를 마칩니다.  
  
## <a name="return-to-tutorials-portal"></a>자습서 포털로 돌아가기  
[자습서: 데이터베이스 엔진 시작](../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  

