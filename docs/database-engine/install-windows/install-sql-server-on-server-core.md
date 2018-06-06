---
title: Server Core에 SQL Server 2016 설치 | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1dd294cc-5b69-4d0c-9005-3e307b75678b
caps.latest.revision: 43
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 979cb0b59ba0528ef7450de0fc4a7b96dd9d4338
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34770919"
---
# <a name="install-sql-server-on-server-core"></a>Server Core에 SQL Server 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Server Core 설치에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 수 있습니다.   
  
Server Core 설치 옵션은 특정 서버 역할을 실행하기 위한 최소 환경을 제공합니다. 이렇게 하면 유지 관리 및 관리 요구 사항이 줄어들고 이러한 서버 역할에 대한 공격 노출 영역이 감소합니다. Server Core에 대한 자세한 내용은 [Server Core 설치](http://docs.microsoft.com/windows-server/get-started/getting-started-with-server-core)를 참조하세요. [!INCLUDE[win8srv](../../includes/win8srv-md.md)]에서 구현되는 Server Core에 대한 자세한 내용은 [Windows Server 2012용 Server Core](http://msdn.microsoft.com/library/hh846323\(VS.85\).aspx)(http://msdn.microsoft.com/library/hh846323(VS.85).aspx)를 참조하세요.  
  
 현재 지원되는 운영 체제 목록은 [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항  
  
|요구 사항|설치 방법|  
|-----------------|--------------------|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6.1 |[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]를 제외한 모든 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 경우 설치 프로그램에는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6.1 Server Core Profile이 필요합니다. 아직 설치되지 않은 경우 SQL Server 설치 프로그램에서 이를 자동으로 설치합니다. 설치에는 다시 부팅이 필요합니다. 설치 프로그램을 실행하기 전에 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]를 설치하여 다시 부팅을 방지할 수 있습니다.|  
|Windows  Installer  4.5|Server Core 설치와 함께 제공됩니다.|  
|Windows PowerShell|Server Core 설치와 함께 제공됩니다.|  
|Java Runtime |PolyBase를 사용하려면 적절한 Java Runtime을 설치해야 합니다. 자세한 내용은 [PolyBase 설치](../../relational-databases/polybase/polybase-installation.md)를 참조하세요.|
  
##  <a name="BK_SupportedFeatures"></a> 지원되는 기능  
 다음 표를 사용하여 Server Core 설치 시 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되는 기능을 찾습니다.  
  
|기능|지원됨|추가 정보|  
|-------------|---------------|----------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제|예||  
|전체 텍스트 검색|예||  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|예||  
|[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]|예||  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|아니요||  
|SSDT([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Tools)|아니요||  
|클라이언트 도구 연결|예||  
|Integration Services 서버|예||  
|클라이언트 도구 이전 버전과의 호환성|아니요||  
|클라이언트 도구 SDK|아니요||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서|아니요||  
|관리 도구 -  기본|원격 전용|Server Core에는 이러한 기능을 설치할 수 없습니다. 이러한 구성 요소는 Server Core가 아닌 다른 서버에 설치되고, Server Core에 설치된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스에 연결됩니다.|  
|관리 도구 -  전체|원격 전용|Server Core에는 이러한 기능을 설치할 수 없습니다. 이러한 구성 요소는 Server Core가 아닌 다른 서버에 설치되고, Server Core에 설치된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스에 연결됩니다.|  
|Distributed  Replay  Controller|아니요||  
|Distributed  Replay  Client|원격 전용|Server Core에는 이러한 기능을 설치할 수 없습니다. 이러한 구성 요소는 Server Core가 아닌 다른 서버에 설치되고, Server Core에 설치된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스에 연결됩니다.|  
|SQL  클라이언트 연결 SDK|예||  
|Microsoft  Sync  Framework|예|Microsoft Sync Framework는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 패키지에 포함되지 않습니다. [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=221788)(http://go.microsoft.com/fwlink/?LinkId=221788) 페이지에서 적절한 버전의 Sync Framework를 다운로드하여 Server Core를 실행하는 컴퓨터에 설치할 수 있습니다.|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|아니요||  
|[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]|아니요||  
  
## <a name="supported-scenarios"></a>지원되는 시나리오  
 다음 표에서는 Server Core에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 설치하는 데 지원되는 시나리오 매트릭스를 보여 줍니다.  
  
|||  
|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전|모든 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64비트 버전 |  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어|모든 언어|  
|OS 언어/로캘에서[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어(조합)|JPN(일본어) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> GER(독일어) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> CHS(중국어-중국) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ARA(아라비아어 (SA)) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> THA(태국) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> TRK(터키어) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> pt-PT(포르투갈어 포르투갈) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ENG(영어) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Windows  버전|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
  
## <a name="upgrade"></a>업그레이드 
 Server Core 설치 시 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에서 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 로 업그레이드는 지원됩니다.  
  
## <a name="install"></a>Install  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 Server  Core  운영 체제의 설치 마법사를 사용하는 설치를 지원하지 않습니다. Server Core에 설치할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치는 /Q 매개 변수를 사용하는 완전 자동 모드 또는 /QS 매개 변수를 사용하는 단순 자동 모드를 지원합니다. 자세한 내용은 명령 프롬프트에서 [SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요.  
  
 소프트웨어 사용이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 볼륨 라이선스 계약 또는 공급 업체와의 ISV  또는 OEM  계약과 같은 별도의 계약에 의해 관리되지 않는 한 설치 방법에 상관없이 개인 또는 업체 대표로서 소프트웨어 사용 조건에 대한 동의를 확인해야 합니다.  
  
 사용 조건은 검토 및 동의를 위해 설치 프로그램 사용자 인터페이스에 표시됩니다. /Q 또는 /QS 매개 변수를 사용하는 무인 설치는 /IACCEPTSQLSERVERLICENSETERMS 매개 변수를 포함해야 합니다. [Microsoft 소프트웨어 사용권 계약(Microsoft Software License Terms)](http://go.microsoft.com/fwlink/?LinkId=148209)에서 사용 조건을 별도로 검토할 수 있습니다.  
  
> [!NOTE]  
>  소프트웨어의 수령 방법(예: [!INCLUDE[msCoName](../../includes/msconame-md.md)] 볼륨 라이선스를 통해 수령)에 따라 사용자의 소프트웨어 사용에 추가 조건이 적용될 수 있습니다.  
  
 특정 기능을 설치하려면 /FEATURES  매개 변수를 사용하여 부모 기능 또는 기능 값을 지정하십시오. 기능 매개 변수 및 사용에 대한 자세한 내용은 다음 섹션을 참조하십시오.  
  
### <a name="feature-parameters"></a>기능 매개 변수  
  
|기능 매개 변수|설명|  
|-----------------------|-----------------|  
|SQLENGINE|[!INCLUDE[ssDE](../../includes/ssde-md.md)]만 설치합니다.|  
|복제|[!INCLUDE[ssDE](../../includes/ssde-md.md)]과 함께 복제 구성 요소를 설치합니다.|  
|FULLTEXT|[!INCLUDE[ssDE](../../includes/ssde-md.md)]과 함께 전체 텍스트 구성 요소를 설치합니다.|  
|AS|모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 요소를 설치합니다.|  
|IS|모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소를 설치합니다.|  
|CONN|연결 구성 요소를 설치합니다.| 
|ADVANCEDANALYTICS |R Services를 설치하며, 데이터베이스 엔진이 필요합니다. 무인 설치에는 /IACCEPTROPENLICENSETERMS 매개 변수가 필요합니다.  |


 기능 매개 변수에 대한 다음과 같은 사용 예를 참조하십시오.  
  
|매개 변수 및 값|설명|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|[!INCLUDE[ssDE](../../includes/ssde-md.md)]만 설치합니다.|  
|/FEATURES=SQLEngine,FullText|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 전체 텍스트를 설치합니다.|  
|/FEATURES=SQLEngine,Conn|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 연결 구성 요소를 설치합니다.|  
|/FEATURES=SQLEngine,AS,IS,Conn|[!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]및 연결 구성 요소를 설치합니다.|  
|/FEATURES=SQLENGINE,ADVANCEDANALYTICS /IACCEPTROPENLICENSETERMS |[!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]를 설치합니다.|  

  
### <a name="installation-options"></a>설치 옵션  
 설치 프로그램에서는 Server  Core  운영 체제에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 설치할 때 다음과 같은 설치 옵션이 지원됩니다.  
  
1.  **명령줄에서 설치**  
  
     명령 프롬프트 설치 옵션을 사용하여 특정 기능을 설치하려면 /FEATURES  매개 변수를 사용하여 부모 기능 또는 기능 값을 지정하십시오. 다음은 명령줄 매개 변수를 사용한 예입니다.  
  
    ```  
    Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /TCPENABLED=1 /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
2.  **구성 파일을 사용하여 설치**  
  
     구성 파일은 명령 프롬프트에서 설치할 경우에만 사용할 수 있습니다. 구성 파일은 기본 구조의 매개 변수(이름/값 쌍)  및 설명 주석이 포함된 텍스트 파일입니다. 명령 프롬프트에 지정된 구성 파일은 파일 확장명이 .INI여야 합니다. 다음 ConfigurationFile.INI에 대한 예를 참조하십시오.  
  
    - [!INCLUDE[ssDE](../../includes/ssde-md.md)]설치 
    
    다음 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]을 포함하는 새로운 독립 실행형 인스턴스를 설치하는 방법을 보여 줍니다.  
  
        ```  
        ; SQL Server Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine, and Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="\<DomainName\UserName>"  
  
        ; Accept the License agreement to continue with Installation  
  
        IAcceptSQLServerLicenseTerms="True"  
  
        ```  
  
    -   연결 구성 요소 설치 다음 예에서는 연결 구성 요소를 설치하는 방법을 보여 줍니다.  
  
        ```  
        ; SQL Server Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=Conn  
  
        ; Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True  
  
        ```  
  
    -   모든 지원 기능 설치  
  
        다음 예에서는 Server  Core에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 모든 지원되는 기능을 설치하는 방법을 보여 줍니다.  
  
        ```  
        ; SQL Server Configuration File  
        [OPTIONS]  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE,FullText,Replication,AS,IS,Conn  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine (SQL), or Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="\<DomainName\UserName>"  
  
        ; The name of the account that the Analysis Services service runs under.   
  
        ASSVCACCOUNT= "NT Service\MSSQLServerOLAPService"  
  
        ; Specifies the list of administrator accounts that need to be provisioned.   
  
        ASSYSADMINACCOUNTS="\<DomainName\UserName>"  
  
        ; Specifies the server mode of the Analysis Services instance. Valid values are MULTIDIMENSIONAL, POWERPIVOT or TABULAR. ASSERVERMODE is case-sensitive. All values must be expressed in upper case.   
  
        ASSERVERMODE="MULTIDIMENSIONAL"  
  
        ; Optional value, which specifies the state of the TCP protocol for the ssNoVersion service. Supported values are: 0 to disable the TCP protocol, and 1 to enable the TCP protocol.  
  
        TCPENABLED=1  
  
        ;Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True"  
        ```  
  
     아래에는 사용자 지정 또는 기본 구성 파일을 사용하여 설치 프로그램을 시작하는 방법이 나와 있습니다.  
  
    -   사용자 지정 구성 파일을 사용하여 설치 프로그램 시작  
  
         명령 프롬프트에 구성 파일을 지정하기  
  
        ```  
        Setup.exe /QS /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
         구성 파일 대신 명령 프롬프트에 암호 지정하기  
  
        ```  
        Setup.exe /QS /SQLSVCPASSWORD="************" /ASSVCPASSWORD="************"  /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
    -   DefaultSetup.ini를 사용하여 설치 프로그램 시작  
  
         [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 미디어의 루트 수준에서 \x86 및 \x64 폴더에 DefaultSetup.ini 파일이 있는 경우 DefaultSetup.ini 파일을 연 다음 *Features* 매개 변수를 파일에 추가합니다.  
  
         DefaultSetup.ini 파일이 없는 경우 파일을 생성하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 미디어의 루트 레벨에서 \x86 및 \x64 폴더에 복사합니다.  
  
## <a name="configure-remote-access-of-includessnoversionincludesssnoversion-mdmd-on-server-core"></a>Server Core에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 원격 액세스 구성  
 아래 설명된 작업을 수행하여 Server Core에서 실행하는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스의 원격 액세스를 구성합니다.  
  
### <a name="enable-remote-connections-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  

원격 연결을 설정하려면 SQLCMD.exe를 로컬로 사용하고 Server Core 인스턴스에 대해 다음 문을 실행합니다.  

   ```Transact-SQL
   EXEC sys.sp_configure N'remote access', N'1'  
   GO
   RECONFIGURE WITH OVERRIDE
   GO
   ```  
  
### <a name="enable-and-start-the-includessnoversionincludesssnoversion-mdmd-browser-service"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] browser service  
 Browser 서비스는 기본적으로 해제되어 있습니다.  Server Core에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 해제된 경우 명령 프롬프트에서 다음 명령을 실행하여 설정합니다.  
  
 `sc config SQLBROWSER start= auto`  
  
 설정한 후 명령 프롬프트에서 다음 명령을 실행하여 서비스를 시작합니다.  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Windows 방화벽에서 예외 생성  
 Windows 방화벽에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 관련 예외를 만들려면 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)에 지정된 단계를 참조하세요.  
  
### <a name="enable-tcpip-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 TCP/IP 프로토콜은 Server Core에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 Windows PowerShell을 통해 설정할 수 있습니다. 다음 단계를 수행하십시오.  
  
1.  서버에서 작업 관리자를 시작합니다.  
  
2.  **응용 프로그램** 탭에서 **새 작업**을 클릭합니다.  
  
3.  **새 작업 만들기** 대화 상자에서 **열기** 필드에 **sqlps.exe** 를 입력하고 **확인**을 클릭합니다. 이렇게 하면 **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell** 창이 열립니다.  
  
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
  
## <a name="uninstall"></a>Uninstall

 Server Core를 실행하는 컴퓨터에 로그인하면 관리자 명령 프롬프트를 사용하는 제한된 데스크톱 환경이 제공됩니다. 이 명령 프롬프트를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 제거를 시작할 수 있습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스를 제거하려면 /Q  매개 변수를 사용하는 완전 자동 모드 또는 /QS  매개 변수를 사용하는 단순 자동 모드로 명령 프롬프트에서 제거를 시작합니다. /QS  매개 변수는 UI를 통해 진행률을 표시하지만 입력은 허용하지 않습니다. /Q는 사용자 인터페이스 없이 자동 모드로 실행됩니다.  
  
 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 제거하려면:  
  
```  
Setup.exe /Q /Action=Uninstall /FEATURES=SQLEngine,AS,IS /INSTANCENAME=MSSQLSERVER  
```  
  
 명명된 인스턴스를 제거하려면 앞에 서 설명한 예제에서 `MSSQLSERVER` 대신 인스턴스 이름을 사용합니다.  
  
## <a name="start-a-new-command-prompt"></a>새 명령 프롬프트 시작

실수로 명령 프롬프트를 닫은 경우 다음 단계에 따라 새 명령 프롬프트를 시작할 수 있습니다.  
 
1.  Ctrl+Shift+Esc를 눌러 작업 관리자를 표시합니다.  
2.  **응용 프로그램** 탭에서 **새 작업**을 클릭합니다.  
3.  **새 태스크 만들기** 대화 상자에서 **열기** 필드에 **cmd** 를 입력한 다음 [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
## <a name="see-also"></a>관련 항목:  
 [구성 파일을 사용하여 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)   
 [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [버전 및 SQL Server 2017의 지원되는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)   
 [Server Core 설치](http://technet.microsoft.com/windows-server-docs/get-started/getting-started-with-server-core)   
 [Sconfig.cmd로 Windows Server 2016의 Server Core 설치 구성](http://technet.microsoft.com/windows-server-docs/get-started/sconfig-on-ws2016)   
 [Windows PowerShell의 장애 조치 클러스터 Cmdlet(영문)](http://technet.microsoft.com/itpro/powershell/windows/failover-clusters/index)   

  
  

