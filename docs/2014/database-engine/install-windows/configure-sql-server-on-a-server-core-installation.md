---
title: Server Core 설치 시 SQL Server 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- IsHadrEnabled server property
- Server Core Installation [SQL Server]
ms.assetid: ed6e5e94-4b8d-422a-a17e-61b05a4df903
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c2a82aac84777c0601d234162135f9404184c39
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797911"
---
# <a name="configure-sql-server-on-a-server-core-installation"></a>Server Core 설치 시 SQL Server 구성
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SP1의 Server Core 설치에서 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 를 구성하는 방법에 대한 자세한 내용을 다룹니다. 
  
##  <a name="configure-and-manage-server-core-on-windows-server"></a>Windows Server에서 Server Core 구성 및 관리  
 이 섹션에서는 Server Core 설치를 구성 및 관리하는 항목에 대한 참조를 제공합니다.  
  
 Server Core 모드에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 일부 기능은 지원되지 않습니다.  일부 구성 요소는 클라이언트 컴퓨터 또는 Server Core를 실행하지 않는 다른 서버에 설치하거나 Server Core에 설치된 데이터베이스 엔진 서비스에 연결할 수 있습니다.  
  
 Server Core 설치를 원격으로 구성하고 관리하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [Windows server 2008 R2: Server Core 배포에 대 한 모범 사례](https://go.microsoft.com/fwlink/?LinkID=245957) (https://go.microsoft.com/fwlink/?LinkID=245957)  
  
-   [Server Core 설치 구성: 개요](https://go.microsoft.com/fwlink/?LinkId=245958) (https://go.microsoft.com/fwlink/?LinkId=245958)  
  
-   [Sconfig .cmd를 사용 하 여 Windows server 2008 r 2의 Server Core 설치 구성](https://go.microsoft.com/fwlink/?LinkId=245959) (https://go.microsoft.com/fwlink/?LinkId=245959)  
  
-   [Windows server 2008 r 2의 Server Core 설치를 실행 하는 서버에 서버 역할 설치: 개요](https://go.microsoft.com/fwlink/?LinkId=245960) (https://go.microsoft.com/fwlink/?LinkId=245960)  
  
-   [Windows server 2008 r 2의 Server Core 설치를 실행 하는 서버에 Windows 기능 설치: 개요](https://go.microsoft.com/fwlink/?LinkId=245961) (https://go.microsoft.com/fwlink/?LinkId=245961)  
  
-   [Server Core 설치 관리: 개요](https://go.microsoft.com/fwlink/?LinkId=245962) (https://go.microsoft.com/fwlink/?LinkId=245962)  
  
-   [Server Core 설치 관리](https://go.microsoft.com/fwlink/?LinkId=245963) (https://go.microsoft.com/fwlink/?LinkId=245963)  
  
##  <a name="install-updates"></a>업데이트 설치  
 이 섹션에서는 Windows Server Core 시스템에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업데이트 설치에 대한 정보를 제공합니다. 시스템이 최신 보안 업데이트로 업데이트되도록 고객이 적절한 시기에 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트를 확인하고 설치하는 것이 좋습니다. Windows Server Core 컴퓨터에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 설치 하는 방법에 대 한 자세한 내용은 [Server core에 SQL Server 2014 설치](install-sql-server-on-server-core.md)를 참조 하세요.  
  
 제품 업데이트를 설치하기 위한 두 가지 시나리오는 다음과 같습니다.  
  
-   [새로 설치 하는 동안 SQL Server 2014에 대 한 업데이트 설치](#installing-updates-during-a-new-installation) 
  
-   [설치 후 SQL Server 2014에 대 한 업데이트 설치](#installing-updates-after-installation) 
  
### <a name="installing-updates-during-a-new-installation"></a>새로 설치 하는 동안 업데이트 설치  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 Server Core 운영 체제에서 명령 프롬프트 설치만 지원합니다. 자세한 내용은 [명령 프롬프트에서 SQL Server 2014 설치](install-sql-server-from-the-command-prompt.md)를 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 최신 제품 업데이트를 주 제품 설치와 통합하여 주 제품과 해당 업데이트가 동시에 설치되게 할 수 있습니다.  
  
 설치 프로그램에서 최신 버전의 적용 가능한 업데이트를 찾으면 이를 다운로드하고 현재의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로세스와 통합합니다. 제품 업데이트에는 누적 업데이트, 서비스 팩 또는 서비스 팩과 누적 업데이트가 포함될 수 있습니다.  
  
 주 제품 설치에 최신 제품 업데이트를 포함하려면 UpdateEnabled 및 UpdateSource 매개 변수를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 제품 업데이트를 사용하려면 다음 예제를 참조하십시오.  
  
```cmd 
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /UpdateEnabled=True /UpdateSource="<SourcePath>" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
### <a name="installing-updates-after-installation"></a>설치 후 업데이트 설치 
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스가 설치된 경우 GDR(General Distribution Release) 및 SP(서비스 팩)를 포함한 최신 보안 업데이트와 중요 업데이트를 적용하는 것이 좋습니다. 개별 누적 업데이트와 보안 업데이트는 "필요할 때" 사례별로 채택해야 합니다. 업데이트를 확인하여 필요하면 적용합니다.  
  
 명령 프롬프트에서 <package_name>을 해당 업데이트 패키지 이름으로 바꾸어 업데이트를 적용합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 모든 구성 요소의 단일 인스턴스를 업데이트합니다. InstanceName 매개 변수 또는 InstanceID 매개 변수를 사용하여 인스턴스를 지정할 수 있습니다.  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공유 구성 요소만 업데이트:  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터의 모든 인스턴스 및 모든 공유 구성 요소 업데이트:  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances  
    ```  
  
##  <a name="startstop-sql-server-service"></a>SQL Server 서비스 시작/중지  
 [sqlservr Application](../../tools/sqlservr-application.md) 애플리케이션은 명령 프롬프트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 시작, 중지, 일시 중지 및 계속합니다.  
  
 Net 서비스를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 시작하고 중지할 수도 있습니다.  
  
## <a name="enable-alwayson-availability-groups"></a>AlwaysOn 가용성 그룹 사용  
 서버 인스턴스에서 고가용성 및 재해 복구 솔루션으로 가용성 그룹을 사용하려면 먼저 AlwaysOn 가용성 그룹을 사용하도록 설정해야 합니다. AlwaysOn 가용성 그룹 관리에 대한 자세한 내용은 [AlwaysOn 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
### <a name="using-sql-server-configuration-manager-remotely"></a>원격으로 SQL Server 구성 관리자 사용  
 이러한 단계는 [!INCLUDE[win7](../../includes/win7-md.md)] 이상의 클라이언트 버전을 실행하는 PC 또는 서버 그래픽 셸이 설치된 다른 서버에서 수행됨을 의미합니다( [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 전체 설치 또는 서버 그래픽 셸 기능이 활성화된 Windows Server 8 설치).  
  
1.  컴퓨터 관리를 엽니다. 컴퓨터 관리를 열려면 다음 중 하나를 수행합니다.  
  
    1.  [!INCLUDE[win7](../../includes/win7-md.md)], Windows Server 2008 또는 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]:  
  
        1.  시작, 모든 프로그램을 클릭하고 관리 도구를 클릭한 다음 컴퓨터 관리를 클릭합니다.  
  
        2.  시작을 클릭하고 실행을 클릭한 다음 COMPMGMT를 입력하고 확인을 클릭합니다.  
  
    2.  서버 그래픽 셸이 활성화된 Windows 8:  
  
        1.  화면의 왼쪽 아래 모서리에 마우스를 이동하고 시작 오버레이가 나타나면 마우스 오른쪽 단추로 클릭합니다.  
  
        2.  상황에 맞는 메뉴에서 컴퓨터 관리를 선택합니다.  
  
2.  콘솔 트리에서 컴퓨터 관리를 마우스 오른쪽 단추로 클릭하고 다른 컴퓨터로 연결을 클릭합니다.  
  
3.  컴퓨터 선택 대화 상자에서 관리할 Server Core 컴퓨터의 이름을 입력하거나 찾아보기를 클릭하여 찾은 다음 확인을 클릭합니다.  
  
4.  콘솔 트리에 있는 Server Core 컴퓨터의 컴퓨터 관리에서 서비스 및 애플리케이션을 클릭합니다.  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 두 번 클릭합니다.  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 클릭 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (\<instance name >)을 마우스 오른쪽 단추로 클릭 한 다음 \<인스턴스 이름 >을 사용 하도록 설정할 로컬 서버 인스턴스의 이름이 고 속성을 클릭 합니다.  
  
7.  AlwaysOn 고가용성 탭을 선택합니다.  
  
8.  Windows 장애 조치(failover) 클러스터 이름 필드에 로컬 장애 조치(failover) 클러스터 노드의 이름이 포함되어 있는지 확인합니다. 이 필드가 비어 있으면 이 서버 인스턴스는 현재 AlwaysOn 가용성 그룹을 지원하지 않습니다. 로컬 컴퓨터가 클러스터 노드가 아니거나 WSFC 클러스터가 종료되었거나 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전이 AlwaysOn 가용성 그룹을 지원하지 않습니다.  
  
9. AlwaysOn 가용성 그룹 사용 확인란을 선택하고 확인을 클릭합니다.  
  
10. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자가 변경 내용을 저장합니다. 그런 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 수동으로 다시 시작해야 합니다. 이렇게 하면 비즈니스 요구 사항에 가장 적합한 다시 시작 시간을 선택할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 다시 시작하면 AlwaysOn을 사용할 수 있으며 IsHadrEnabled 서버 속성이 1로 설정됩니다.  
  
> [!NOTE]
>  -   적절한 사용자 권한이 있거나 해당 컴퓨터에 연결하기 위해 대상 컴퓨터에 대한 적절한 권한을 위임해야 합니다.  
> -   관리하는 컴퓨터의 이름이 콘솔 트리의 컴퓨터 관리 옆에 괄호로 나타납니다.  
  
### <a name="using-powershell-cmdlets-to-enable-alwayson-availability-groups"></a>AlwaysOn 가용성 그룹 설정을 위해 PowerShell Cmdlet 사용

 PowerShell Cmdlet Enable-SqlAlwaysOn은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에서 AlwaysOn 가용성 그룹을 설정하는 데 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되고 있을 때 AlwaysOn 가용성 그룹이 설정되면 데이터베이스 엔진 서비스를 다시 시작해야 변경이 완료됩니다. -Force 매개 변수를 지정하지 않으면 cmdlet이 서비스를 다시 시작할 것인지를 묻는 메시지를 표시합니다. 취소할 경우 아무 작업도 발생하지 않습니다.  
  
 이 cmdlet을 실행하려면 관리자 권한이 있어야 합니다.  
  
 다음 구문 중 하나를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 AlwaysOn 가용성 그룹을 설정할 수 있습니다.  
  
```  
Enable-SqlAlwaysOn [-Path <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn -InputObject <Server> [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn [-ServerInstance <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
 다음 PowerShell 명령을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스(Machine\Instance)에 대한 AlwaysOn 가용성 그룹을 설정할 수 있습니다.  
  
```powershell
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Machine\Instance  
```  
  
## <a name="configuring-remote-access-of-sql-server-running-on-server-core"></a>Server Core에서 실행 되는 SQL Server의 원격 액세스 구성  
 아래 설명된 작업을 수행하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Server Core SP1에서 실행하는 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 인스턴스의 원격 액세스를 구성합니다.  
  
### <a name="enable-remote-connections-on-an-instance-of-sql-server"></a>SQL Server의 인스턴스에서 원격 연결을 사용 하도록 설정 
 원격 연결을 설정하려면 SQLCMD.exe를 로컬로 사용하고 Server Core 인스턴스에 대해 다음 문을 실행합니다.  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-sql-server-browser-service"></a>SQL  Server  Browser  서비스 설정 및 시작  
 Browser 서비스는 기본적으로 해제되어 있습니다.  Server Core에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 해제된 경우 명령 프롬프트에서 다음 명령을 실행하여 설정합니다.  
  
 `sc config SQLBROWSER start= auto`  
  
 설정한 후 명령 프롬프트에서 다음 명령을 실행하여 서비스를 시작합니다.  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Windows 방화벽에서 예외 생성  
 Windows 방화벽에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 관련 예외를 만들려면 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)에 지정된 단계를 참조하세요.  
  
### <a name="enable-tcpip-on-an-instance-of-sql-server"></a>SQL Server 인스턴스에서 TCP/IP를 사용 하도록 설정
 TCP/IP 프로토콜은 Server Core에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 Windows PowerShell을 통해 설정할 수 있습니다. 다음 단계를 수행하세요.  
  
1.  Windows Server 2008 R2 Server Core SP1을 실행하는 컴퓨터에서 작업 관리자를 실행합니다.  
  
2.  **애플리케이션** 탭에서 **새 작업**을 클릭합니다.  
  
3.  **새 작업 만들기** 대화 상자에서 **열기** 필드에 **sqlps.exe** 를 입력하고 **확인**을 클릭합니다. 이렇게 하면 **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell** 창이 열립니다.  
  
4.  **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell** 창에서 다음 스크립트를 실행하여 TCP/IP 프로토콜을 사용하도록 설정합니다.  
  
```powershell
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = new-object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
##  <a name="sql-server-profiler"></a>SQL Server 프로파일러  
 원격 컴퓨터에서 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 시작하고 파일 메뉴에서 새 추적을 선택하면 Server Core 시스템에 있는 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정할 수 있는 서버에 연결 대화 상자가 표시됩니다. 자세한 내용은 [Start SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md)을 참조하세요.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]실행에 필요한 권한에 대한 자세한 내용은 [SQL Server Profiler 실행에 필요한 권한](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)을 참조하세요.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에 대한 자세한 내용은 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)를 참조하세요.  
  
##  <a name="sql-server-auditing"></a>SQL Server 감사  
 원격으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] or [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 감사를 정의할 수 있습니다. 감사가 생성되고 활성화되면 대상이 항목을 받습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 감사 만들기 및 관리에 대한 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)를 참조하세요.  
  
##  <a name="sql-servevr-command-prompt-utilities"></a>SQL server 명령 프롬프트 유틸리티  
 Server Core 시스템에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업을 스크립팅할 수 있게 해 주는 다음과 같은 명령 프롬프트 유틸리티를 사용할 수 있습니다. 다음 표에서는 Server Core용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 제공하는 명령 프롬프트 유틸리티를 보여 줍니다.  
  
|**유틸리티**|**설명**|**설치 위치**|  
|-----------------|---------------------|----------------------|  
|[bcp 유틸리티](../../tools/bcp-utility.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 사용자가 지정한 형식의 데이터 파일 간에 데이터를 복사하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec 유틸리티](../../integration-services/packages/dtexec-utility.md)|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 구성 및 실행하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil 유틸리티](../../integration-services/dtutil-utility.md)|SSIS 패키지를 관리하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[osql 유틸리티](../../tools/osql-utility.md)|명령 프롬프트에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 애플리케이션](../../tools/sqlagent90-application.md)|명령 프롬프트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 시작하는 데 사용합니다.|\<드라이브>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*instance_name*>\MSSQL\Binn|  
|[sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)|명령 프롬프트에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SQLdiag 유틸리티](../../tools/sqldiag-utility.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 고객 서비스 지원 센터에 제공할 진단 정보를 수집하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint 유틸리티](../../tools/sqlmaint-utility.md)|이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 만든 데이터베이스 유지 관리 계획을 실행하는 데 사용합니다.|\<drive>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.MSSQLSERVER\MSSQL\Binn|  
|[sqlps 유틸리티](../../tools/sqlps-utility.md)|PowerShell 명령 및 스크립트를 실행하는 데 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 공급자 및 cmdlet을 로드하고 등록합니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr 애플리케이션](../../tools/sqlservr-application.md)|문제 해결을 위해 명령 프롬프트에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 시작 및 중지하는 데 사용합니다.|\<drive>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.MSSQLSERVER\MSSQL\Binn|  
  
##  <a name="use-troubleshooting-tools"></a>문제 해결 도구 사용  
 [SQLdiag 유틸리티](../../tools/sqldiag-utility.md) 를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 기타 서버 유형에서 로그 및 데이터 파일을 수집할 수 있으며 이러한 파일을 사용하여 지속적으로 서버를 모니터링하거나 특정 서버 문제를 해결할 수 있습니다. SQLdiag는 Microsoft 고객 지원 서비스에서 진단 정보를 빠르고 간편하게 수집할 수 있도록 지원하는 유틸리티입니다.  
  
 항목에 지정된 구문 [SQLdiag Utility](../../tools/sqldiag-utility.md)을(를) 사용하여 Server Core의 관리자 명령 프롬프트에서 유틸리티를 시작할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Server Core 에 SQL Server 2014을 설치](install-sql-server-on-server-core.md) 합니다.  
 [설치 방법 도움말 항목](../../sql-server/install/installation-how-to-topics.md)  
