---
title: Server Core 설치 구성
description: 이 문서에서는 Server Core 설치 시 SQL Server를 구성하는 방법과 문제 해결 도구에 대해 자세히 설명합니다.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- IsHadrEnabled server property
- Server Core Installation [SQL Server]
ms.assetid: ed6e5e94-4b8d-422a-a17e-61b05a4df903
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: a66564763c8689b13b8660f0a35dd4d9b29bcfc0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460736"
---
# <a name="configure-sql-server-on-a-server-core-installation"></a>Server Core 설치 시 SQL Server 구성

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

이 문서에서는 Server Core 설치에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 구성하는 방법에 대한 자세한 내용을 다룹니다.  

##  <a name="configure-and-manage-server-core-on-windows-server"></a><a name="BKMK_ConfigureWindows"></a> Windows Server에서 Server Core 구성 및 관리  
이 섹션에서는 Server Core 설치를 구성 및 관리하는 문서에 대한 참조를 제공합니다.  
  
Server Core 모드에서 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 의 일부 기능은 지원되지 않습니다.  일부 구성 요소는 클라이언트 컴퓨터 또는 Server Core를 실행하지 않는 다른 서버에 설치하거나 Server Core에 설치된 데이터베이스 엔진 서비스에 연결할 수 있습니다.  
  
Server Core 설치를 원격으로 구성하고 관리하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.  
  
- [Server Core 설치](/windows-server/get-started/getting-started-with-server-core)  
  
- [Sconfig.cmd로 Windows Server 2016의 Server Core 설치 구성](/windows-server/get-started/sconfig-on-ws2016)  
  
- [Server Core 서버 Windows Server 2012 R2에 서버 역할 및 기능 설치](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574158(v=ws.11))
  
- [Server Core 설치 관리: 개요](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee441255(v=ws.10))  
  
- [Server Core 설치 관리](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee441258(v=ws.10))
  
##  <a name="install-ssnoversion-updates"></a><a name="BKMK_InstallSQLUpdates"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트 설치  
이 섹션에서는 Windows Server Core 시스템에서 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 업데이트 설치에 대한 정보를 제공합니다. 시스템이 최신 보안 업데이트로 업데이트되도록 고객이 적절한 시기에 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트를 확인하고 설치하는 것이 좋습니다. Windows Server Core 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]을 설치하는 방법에 대한 자세한 내용은 [Server Core에 SQL Server 설치](../../database-engine/install-windows/install-sql-server-on-server-core.md)를 참조하세요.  
  
제품 업데이트를 설치하기 위한 두 가지 시나리오는 다음과 같습니다.  
  
- [새로 설치하는 동안 SQL Server용 업데이트 설치](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#bkmk_NewInstall)  
  
- [설치 후 SQL Server용 업데이트 설치](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#bkmk_alreadyInstall)  
  
###  <a name="installing-updates-for-ssnoversion-during-a-new-installation"></a><a name="bkmk_NewInstall"></a> 새로 설치하는 동안 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 용 업데이트 설치  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 Server Core 운영 체제에서 명령 프롬프트 설치만 지원합니다. 자세한 내용은 [명령 프롬프트에서 SQL Server 설치](./install-sql-server-from-the-command-prompt.md)를 참조하세요.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 최신 제품 업데이트를 주 제품 설치와 통합하여 주 제품과 해당 업데이트가 동시에 설치되게 할 수 있습니다.  
  
설치 프로그램에서 최신 버전의 적용 가능한 업데이트를 찾으면 이를 다운로드하고 현재의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로세스와 통합합니다. 제품 업데이트에는 누적 업데이트, 서비스 팩 또는 서비스 팩과 누적 업데이트가 포함될 수 있습니다.  
  
주 제품 설치에 최신 제품 업데이트를 포함하려면 UpdateEnabled 및 UpdateSource 매개 변수를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 제품 업데이트를 사용하려면 다음 예제를 참조하십시오.  
  
```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /UpdateEnabled=True /UpdateSource="<SourcePath>" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
###  <a name="installing-updates-for-ssnoversion-after-it-has-been-installed"></a><a name="bkmk_alreadyInstall"></a> 설치 후 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 용 업데이트 설치.  
[!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]인스턴스가 설치된 경우 GDR(General Distribution Release) 및 SP(서비스 팩)를 포함한 최신 보안 업데이트와 중요 업데이트를 적용하는 것이 좋습니다. 개별 누적 업데이트와 보안 업데이트는 "필요할 때" 사례별로 채택해야 합니다. 업데이트를 확인하여 필요하면 적용합니다.  
  
명령 프롬프트에서 <package_name>을 해당하는 업데이트 패키지 이름으로 바꾸어 업데이트를 적용합니다.  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 모든 구성 요소의 단일 인스턴스를 업데이트합니다. InstanceName 매개 변수 또는 InstanceID 매개 변수를 사용하여 인스턴스를 지정할 수 있습니다.  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance  
    ```  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공유 구성 요소만 업데이트:  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
    ```  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터의 모든 인스턴스 및 모든 공유 구성 요소 업데이트:  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances  
    ```  
  
## <a name="startstop-ssnoversion-service"></a><a name="BKMK_StartStopServices"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작/중지  
[sqlservr 애플리케이션](../../tools/sqlservr-application.md) 은 명령 프롬프트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 시작, 중지, 일시 중지 및 계속합니다.  
  
Net 서비스를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 시작하고 중지할 수도 있습니다.  
  
## <a name="enable-alwayson-availability-groups"></a><a name="BKMK_EnableAlwaysON"></a> AlwaysOn 가용성 그룹 사용  
서버 인스턴스에서 고가용성 및 재해 복구 솔루션으로 가용성 그룹을 사용하려면 먼저 AlwaysOn 가용성 그룹을 사용하도록 설정해야 합니다. Always On 가용성 그룹 관리에 대한 자세한 내용은 [Always On 가용성 그룹 활성화 및 비활성(SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
### <a name="using-ssnoversion-configuration-manager-remotely"></a>원격으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 사용  
이러한 단계는 서버 그래픽 셸이 설치된 Windows 또는 Windows Server 클라이언트 버전을 실행하는 PC에서 수행해야 합니다.  
  
1. **컴퓨터 관리** 를 엽니다. **컴퓨터 관리** 를 열려면 **시작** 을 클릭하고 `compmgmt.msc`를 입력한 다음 **확인** 을 클릭합니다.    
  
2. 콘솔 트리에서 **컴퓨터 관리** 를 마우스 오른쪽 단추로 클릭한 다음 **다른 컴퓨터에 연결...** 을 클릭합니다.  
  
3. **컴퓨터 선택** 대화 상자에서 관리할 Server Core 컴퓨터의 이름을 입력하거나 **찾아보기** 를 클릭하여 찾은 다음 **확인** 을 클릭합니다.  
  
4. 콘솔 트리에 있는 Server Core 컴퓨터의 **컴퓨터 관리** 아래에서 **서비스 및 애플리케이션** 을 클릭합니다.  
  
5. **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]구성 관리자** 를 두 번 클릭합니다.  
  
6. **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]구성 관리자** 에서 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스** 를 클릭하고 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** (\<instance name>)를 마우스 오른쪽 단추로 클릭한 다음 [속성]을 클릭합니다. 여기서 \<instance name>은 Always On 가용성 그룹을 사용하도록 설정하려는 로컬 서버 인스턴스의 이름입니다.  
  
7. **AlwaysOn 고가용성** 탭을 선택합니다.  
  
8. Windows 장애 조치(failover) 클러스터 이름 필드에 로컬 장애 조치(failover) 클러스터 노드의 이름이 포함되어 있는지 확인합니다. 이 필드가 비어 있으면 이 서버 인스턴스는 현재 AlwaysOn 가용성 그룹을 지원하지 않습니다. 로컬 컴퓨터가 클러스터 노드가 아니거나 WSFC 클러스터가 종료되었거나 이 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 버전이 AlwaysOn 가용성 그룹을 지원하지 않습니다.  
  
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
  
```  
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Machine\Instance  
```  
  
##  <a name="configuring-remote-access-of-ssnoversion-running-on-server-core"></a><a name="BKMK_ConfigureRemoteAccess"></a> Server Core에서 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 원격 액세스 구성  
 아래에서 설명하는 작업을 수행하여 Windows Server Core에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 인스턴스의 원격 액세스를 구성합니다.  
  
### <a name="enable-remote-connections-on-the-instance-of-ssnoversion"></a>다음 인스턴스에서 원격 연결 설정: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 원격 연결을 설정하려면 SQLCMD.exe를 로컬로 사용하고 Server Core 인스턴스에 대해 다음 문을 실행합니다.  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-ssnoversion-browser-service"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스 설정 및 시작  
 Browser 서비스는 기본적으로 해제되어 있습니다.  Server Core에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 해제된 경우 명령 프롬프트에서 다음 명령을 실행하여 설정합니다.  
  
 `sc config SQLBROWSER start= auto`  
  
 설정한 후 명령 프롬프트에서 다음 명령을 실행하여 서비스를 시작합니다.  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Windows 방화벽에서 예외 생성  
 Windows 방화벽에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 관련 예외를 만들려면 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)에 지정된 단계를 참조하세요.  
  
### <a name="enable-tcpip-on-the-instance-of-ssnoversion"></a>다음 인스턴스에서 TCP/IP 사용: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 TCP/IP 프로토콜은 Server Core에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 Windows PowerShell을 통해 설정할 수 있습니다. 다음 단계를 수행하세요.  
  
1.  Windows Server Core를 실행하는 컴퓨터에서 **작업 관리자** 를 시작합니다.  
  
2.  **애플리케이션** 탭에서 **새 작업** 을 클릭합니다.  
  
3.  **새 작업 만들기** 대화 상자에서 **열기** 필드에 **sqlps.exe** 를 입력하고 **확인** 을 클릭합니다. 이렇게 하면 **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell** 창이 열립니다.  
  
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
  
##  <a name="ssnoversion-profiler"></a><a name="BKMK_Profiler"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler  
 원격 컴퓨터에서 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 시작하고 파일 메뉴에서 새 추적을 선택하면 Server Core 시스템에 있는 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정할 수 있는 서버에 연결 대화 상자가 표시됩니다. 자세한 내용은 [Start SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md)을 참조하세요.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]실행에 필요한 권한에 대한 자세한 내용은 [SQL Server Profiler 실행에 필요한 권한](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)을 참조하세요.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에 대한 자세한 내용은 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)를 참조하세요.  
  
##  <a name="ssnoversion-auditing"></a><a name="BKMK_Auditing"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 감사  
 원격으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] or [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 감사를 정의할 수 있습니다. 감사가 생성되고 활성화되면 대상이 항목을 받습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 감사 만들기 및 관리에 대한 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)를 참조하세요.  
  
##  <a name="command-prompt-utilities"></a><a name="BKMK_CMD"></a> 명령 프롬프트 유틸리티  
 Server Core 시스템에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업을 스크립팅할 수 있게 해 주는 다음과 같은 명령 프롬프트 유틸리티를 사용할 수 있습니다. 다음 표에서는 Server Core용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 제공하는 명령 프롬프트 유틸리티를 보여 줍니다.  
  
|**유틸리티**|**설명**|**설치 위치**|  
|-----------------|---------------------|----------------------|  
|[bcp 유틸리티](../../tools/bcp-utility.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 사용자가 지정한 형식의 데이터 파일 간에 데이터를 복사하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec 유틸리티](../../integration-services/packages/dtexec-utility.md)|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 구성 및 실행하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil 유틸리티](../../integration-services/dtutil-utility.md)|SSIS 패키지를 관리하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[osql 유틸리티](../../tools/osql-utility.md)|명령 프롬프트에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 애플리케이션](../../tools/sqlagent90-application.md)|명령 프롬프트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 시작하는 데 사용합니다.|\<drive>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*instance_name*>\MSSQL\Binn|  
|[sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)|명령 프롬프트에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SQLdiag 유틸리티](../../tools/sqldiag-utility.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 고객 서비스 지원 센터에 제공할 진단 정보를 수집하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint 유틸리티](../../tools/sqlmaint-utility.md)|이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 만든 데이터베이스 유지 관리 계획을 실행하는 데 사용합니다.|\<drive>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.MSSQLSERVER\MSSQL\Binn|  
|[sqlps 유틸리티](../../tools/sqlps-utility.md)|PowerShell 명령 및 스크립트를 실행하는 데 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 공급자 및 cmdlet을 로드하고 등록합니다.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr 애플리케이션](../../tools/sqlservr-application.md)|문제 해결을 위해 명령 프롬프트에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 시작 및 중지하는 데 사용합니다.|\<drive>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.MSSQLSERVER\MSSQL\Binn|  
  
##  <a name="use-troubleshooting-tools"></a><a name="BKMK_troubleshoot"></a> 문제 해결 도구 사용  
 [SQLdiag 유틸리티](../../tools/sqldiag-utility.md) 를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 기타 서버 유형에서 로그 및 데이터 파일을 수집할 수 있으며 이러한 파일을 사용하여 지속적으로 서버를 모니터링하거나 특정 서버 문제를 해결할 수 있습니다. SQLdiag는 Microsoft 고객 지원 서비스에서 진단 정보를 빠르고 간편하게 수집할 수 있도록 지원하는 유틸리티입니다.  
  
 문서에 지정된 구문을 사용하여 Server Core의 관리자 명령 프롬프트에서 유틸리티를 시작할 수 있습니다. [SQLdiag 유틸리티](../../tools/sqldiag-utility.md).  
  
## <a name="see-also"></a>참고 항목  
 [Server Core에 SQL Server 설치](../../database-engine/install-windows/install-sql-server-on-server-core.md)   
 [설치 방법 도움말 문서](/previous-versions/sql/)  
  
