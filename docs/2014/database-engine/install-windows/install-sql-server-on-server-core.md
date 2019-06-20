---
title: Server Core에 SQL Server 2014 설치 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1dd294cc-5b69-4d0c-9005-3e307b75678b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 29523dba8417a89261fed72da801898513796c17
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775779"
---
# <a name="install-sql-server-2014-on-server-core"></a>Server Core에 SQL Server 2014 설치
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 또는 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]의 Server Core 설치에 설치할 수 있습니다. 이 항목에서는 Server  Core에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 설치하기 위한 설치 관련 세부 정보를 제공합니다.  
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 또는 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 운영 체제의 Server  Core  설치 옵션은 특정 서버 역할을 실행하기 위한 최소 환경을 제공합니다. 이렇게 하면 유지 관리 및 관리 요구 사항이 줄어들고 이러한 서버 역할에 대한 공격 노출 영역이 감소합니다. 구현 되는 Server Core에 대 한 자세한 내용은 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]를 참조 하세요 [Server Core에 대 한 Windows Server 2008 R2](https://go.microsoft.com/fwlink/?LinkId=202439) (https://go.microsoft.com/fwlink/?LinkId=202439) 합니다. [!INCLUDE[win8srv](../../includes/win8srv-md.md)]에서 구현되는 Server Core에 대한 자세한 내용은 [Windows Server 2012용 Server Core](https://msdn.microsoft.com/library/hh846323\(VS.85\).aspx)(https://msdn.microsoft.com/library/hh846323(VS.85).aspx) 를 참조하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
|요구 사항|설치 방법|  
|-----------------|--------------------|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 SP2|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1  및 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]의 Server  Core  설치에 포함되어 있습니다. 활성화되어 있지 않은 경우 설치 프로그램이 기본적으로 활성화합니다.<br /><br /> 한 컴퓨터에서 2.0, 3.0, 3.5 버전을 함께 실행할 수는 없습니다. .NET  Framework  3.5  SP1을 설치하면 2.0  및 3.0  레이어가 자동으로 설치됩니다.|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 3.5  SP1  Full  Profile|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1의 Server  Core  설치에 포함되어 있습니다. 활성화되어 있지 않은 경우 설치 프로그램이 기본적으로 활성화합니다.<br /><br /> Windows 서버 운영 체제가 설치된 컴퓨터에서 .NET 3.5 SP1에 종속된 구성 요소를 설치하려면 설치 프로그램을 실행하기 전에 .NET Framework 3.5 SP1을 다운로드하고 설치해야 합니다.<br /><br /> 획득에서.NET Framework 3.5를 사용 하도록 설정 하는 방법에 대 한 권장 사항 및 지침 대 한 자세한 내용은 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]를 참조 하세요 [Microsoft.NET Framework 3.5 배포 고려 사항](https://msdn.microsoft.com/library/windows/hardware/hh975396) (https://msdn.microsoft.com/library/windows/hardware/hh975396) 합니다.|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4  Server  Core  Profile|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 제외한 모든 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]버전의 경우,  설치 프로그램은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4  Server  Core  Profile을 필수 구성 요소로 설치합니다.<br /><br /> 에 대 한 [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)]를 다운로드 합니다 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 에서 4 Server Core Profile [Server Core 용 Microsoft.NET Framework 4 (독립 실행형 설치 관리자)](https://go.microsoft.com/fwlink/?LinkId=220467) (https://go.microsoft.com/fwlink/?LinkId=220467) , 하 고 설치를 진행 하기 전에 설치.|  
|Windows  Installer  4.5|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1  및 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]의 Server  Core  설치와 함께 제공됩니다.|  
|Windows  PowerShell  2.0|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1  및 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]의 Server  Core  설치와 함께 제공됩니다.|  
  
##  <a name="BK_SupportedFeatures"></a> Supported Features  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1  및 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server  Core  설치의 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]에서 지원하는 기능을 다음 표에서 찾을 수 있습니다.  
  
|기능|지원됨|  
|-------------|---------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스|사용자 계정 컨트롤|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제|사용자 계정 컨트롤|  
|전체 텍스트 검색|사용자 계정 컨트롤|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|예|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|아니요|  
|SSDT([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Tools)|아니요|  
|클라이언트 도구 연결|사용자 계정 컨트롤|  
|Integration Services 서버<sup>[1]</sup>|사용자 계정 컨트롤|  
|클라이언트 도구 이전 버전과의 호환성|아니요|  
|클라이언트 도구 SDK|아니요|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서|아니요|  
|관리 도구 -  기본|원격 전용<sup>[2]</sup>|  
|관리 도구 - 전체|원격 전용<sup>[2]</sup>|  
|Distributed Replay Controller|아니요|  
|Distributed Replay Client|원격 전용<sup>[2]</sup>|  
|SQL  클라이언트 연결 SDK|사용자 계정 컨트롤|  
|Microsoft  Sync  Framework|예<sup>[3]</sup>|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|아니요|  
|[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]|아니요|  
  
 <sup>[1] </sup>새 Integration Services 서버 및 해당 기능에 대 한 자세한 내용은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 참조 하십시오 [Integration Services &#40;SSIS&#41; 서버](../../integration-services/catalog/integration-services-ssis-server-and-catalog.md).  
  
 <sup>[2] </sup>설치가 Server Core에서 이러한 기능의 지원 되지 않습니다. 이러한 구성 요소는 Server Core에 설치된 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 서비스에 연결되어 있는 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core SP1 또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Server Core 이외의 서버에 설치할 수 있습니다.  
  
 <sup>[3] </sup>Microsoft Sync Framework에 포함 되지 않습니다는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 패키지입니다. 이 적합 한 Sync Framework 버전을 다운로드할 수 있습니다 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?LinkId=221788) (https://go.microsoft.com/fwlink/?LinkId=221788) 페이지 및의 Server Core 설치를 실행 하는 컴퓨터에 설치할 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 또는 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 합니다.  
  
## <a name="supported-scenario-matrix"></a>지원되는 시나리오 매트릭스  
 다음 표에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 및 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 의 Server Core 설치에 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]를 설치할 때 지원되는 시나리오 매트릭스를 보여 줍니다.  
  
|||  
|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전|모든 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64 비트 버전<sup>[1]</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어|모든 언어|  
|OS 언어/로캘에서[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어(조합)|JPN(일본어) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> GER(독일어) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> CHS(중국어-중국) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ARA(아라비아어 (SA)) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> THA(태국) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> TRK(터키어) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> pt-PT(포르투갈어 포르투갈) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ENG(영어) Windows에서 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Windows  버전|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64비트 x64 Datacenter<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64비트 x64 Standard<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64비트 x64 Data Center Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64비트 x64 Enterprise Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64비트 x64 Standard Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64비트 x64 Web Server Core|  
  
 <sup>[1] </sup>32 비트 버전의 설치 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전 Server Core에서 지원 되지 않습니다.  
  
## <a name="upgrading"></a>업그레이드  
 Server Core 설치 시 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에서 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 로 업그레이드는 지원됩니다.  
  
## <a name="installation"></a>설치  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 Server  Core  운영 체제의 설치 마법사를 사용하는 설치를 지원하지 않습니다. Server Core에 설치할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치는 /Q 매개 변수를 사용하는 완전 자동 모드 또는 /QS 매개 변수를 사용하는 단순 자동 모드를 지원합니다. 자세한 내용은 [명령 프롬프트에서 SQL Server 2014 설치](install-sql-server-from-the-command-prompt.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]은 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 또는 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core를 실행하는 컴퓨터에서 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 함께 설치할 수 없습니다.  
  
 소프트웨어 사용이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 볼륨 라이선스 계약 또는 공급 업체와의 ISV  또는 OEM  계약과 같은 별도의 계약에 의해 관리되지 않는 한 설치 방법에 상관없이 개인 또는 업체 대표로서 소프트웨어 사용 조건에 대한 동의를 확인해야 합니다.  
  
 사용 조건은 검토 및 동의를 위해 설치 프로그램 사용자 인터페이스에 표시됩니다. /Q 또는 /QS 매개 변수를 사용하는 무인 설치는 /IACCEPTSQLSERVERLICENSETERMS 매개 변수를 포함해야 합니다. [Microsoft 소프트웨어 사용권 계약(Microsoft Software License Terms)](https://go.microsoft.com/fwlink/?LinkId=148209)에서 사용 조건을 별도로 검토할 수 있습니다.  
  
> [!NOTE]  
>  소프트웨어의 수령 방법(예: [!INCLUDE[msCoName](../../includes/msconame-md.md)] 볼륨 라이선스를 통해 수령)에 따라 사용자의 소프트웨어 사용에 추가 조건이 적용될 수 있습니다.  
  
 특정 기능을 설치하려면 /FEATURES  매개 변수를 사용하여 부모 기능 또는 기능 값을 지정하십시오. 기능 매개 변수 및 사용에 대한 자세한 내용은 다음 섹션을 참조하십시오.  
  
### <a name="feature-parameters"></a>기능 매개 변수  
  
|기능 매개 변수|Description|  
|-----------------------|-----------------|  
|SQLENGINE|[!INCLUDE[ssDE](../../includes/ssde-md.md)]만 설치합니다.|  
|복제|[!INCLUDE[ssDE](../../includes/ssde-md.md)]과 함께 복제 구성 요소를 설치합니다.|  
|FULLTEXT|[!INCLUDE[ssDE](../../includes/ssde-md.md)]과 함께 전체 텍스트 구성 요소를 설치합니다.|  
|AS|모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 요소를 설치합니다.|  
|IS|모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소를 설치합니다.|  
|CONN|연결 구성 요소를 설치합니다.|  
  
 기능 매개 변수에 대한 다음과 같은 사용 예를 참조하십시오.  
  
|매개 변수 및 값|설명|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|[!INCLUDE[ssDE](../../includes/ssde-md.md)]만 설치합니다.|  
|/FEATURES=SQLEngine,FullText|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 전체 텍스트를 설치합니다.|  
|/FEATURES=SQLEngine,Conn|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 연결 구성 요소를 설치합니다.|  
|/FEATURES=SQLEngine,AS,IS,Conn|[!INCLUDE[ssDE](../../includes/ssde-md.md)],  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)],  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 연결 구성 요소를 설치합니다.|  
  
### <a name="installation-options"></a>설치 옵션  
 설치 프로그램에서는 Server  Core  운영 체제에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 설치할 때 다음과 같은 설치 옵션이 지원됩니다.  
  
1.  **명령줄에서 설치**  
  
     명령 프롬프트 설치 옵션을 사용하여 특정 기능을 설치하려면 /FEATURES  매개 변수를 사용하여 부모 기능 또는 기능 값을 지정하십시오. 다음은 명령줄 매개 변수를 사용한 예입니다.  
  
    ```  
    Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /TCPENABLED=1 /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
2.  **구성 파일을 사용하여 설치**  
  
     구성 파일은 명령 프롬프트에서 설치할 경우에만 사용할 수 있습니다. 구성 파일은 기본 구조의 매개 변수(이름/값 쌍)  및 설명 주석이 포함된 텍스트 파일입니다. 명령 프롬프트에 지정된 구성 파일은 파일 확장명이 .INI여야 합니다. 다음 ConfigurationFile.INI에 대한 예를 참조하십시오.  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 설치  
  
         다음 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]을 포함하는 새 독립 실행형 인스턴스를 설치하는 방법을 보여 줍니다.  
  
        ```  
        ; ssNoVersion Configuration File  
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
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Accept the License agreement to continue with Installation  
  
        IAcceptSQLServerLicenseTerms="True"  
  
        ```  
  
    -   연결 구성 요소 설치  
  
         다음 예에서는 연결 구성 요소를 설치하는 방법을 보여 줍니다.  
  
        ```  
        ; ssNoVersion Configuration File  
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
        ; ssNoVersion Configuration File  
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
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; The name of the account that the Analysis Services service runs under.   
  
        ASSVCACCOUNT= "NT Service\MSSQLServerOLAPService"  
  
        ; Specifies the list of administrator accounts that need to be provisioned.   
  
        ASSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Specifies the server mode of the Analysis Services instance. Valid values are MULTIDIMENSIONAL, POWERPIVOT or TABULAR. ASSERVERMODE is case-sensitive. All values must be expressed in upper case.   
  
        ASSERVERMODE="MULTIDIMENSIONAL"  
  
        ; Optional value, which specifies the state of the TCP protocol for the ssNoVersion service. Supported values are: 0 to disable the TCP protocol, and 1 to enable the TCP protocol.  
  
        TCPENABLED=1  
  
        ;Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True"  
        ```  
  
     다음 예제에서는 구성 파일을 사용하여 설치 프로그램을 시작하는 방법을 보여 줍니다.  
  
    -   구성 파일  
  
         다음은 구성 파일을 사용하는 방법을 보여 주는 예입니다.  
  
        -   명령 프롬프트에 구성 파일을 지정하기  
  
        ```  
        Setup.exe /QS /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
        -   구성 파일 대신 명령 프롬프트에 암호 지정하기  
  
        ```  
        Setup.exe /QS /SQLSVCPASSWORD="************" /ASSVCPASSWORD="************"  /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
    -   DefaultSetup.ini  
  
         [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 미디어의 루트 수준에서 \x86 및 \x64 폴더에 DefaultSetup.ini 파일이 있는 경우 DefaultSetup.ini 파일을 연 다음 *Features* 매개 변수를 파일에 추가합니다.  
  
         DefaultSetup.ini 파일이 없는 경우 파일을 생성하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 미디어의 루트 레벨에서 \x86 및 \x64 폴더에 복사합니다.  
  
## <a name="configuring-remote-access-of-includessnoversionincludesssnoversion-mdmd-running-on-server-core"></a>Server Core에서 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 원격 액세스 구성  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 또는 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]의 Server Core 설치에서 실행되는 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 인스턴스의 원격 액세스를 구성하려면 아래에 설명된 작업을 수행합니다.  
  
### <a name="enable-remote-connections-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 원격 연결을 설정하려면 SQLCMD.exe를 로컬로 사용하고 Server Core 인스턴스에 대해 다음 문을 실행합니다.  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-includessnoversionincludesssnoversion-mdmd-browser-service"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스 설정 및 시작  
 Browser 서비스는 기본적으로 해제되어 있습니다.  Server Core에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 해제된 경우 명령 프롬프트에서 다음 명령을 실행하여 설정합니다.  
  
 `sc config SQLBROWSER start= auto`  
  
 설정한 후 명령 프롬프트에서 다음 명령을 실행하여 서비스를 시작합니다.  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Windows 방화벽에서 예외 생성  
 Windows 방화벽에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 관련 예외를 만들려면 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)에 지정된 단계를 참조하세요.  
  
### <a name="enable-tcpip-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 TCP/IP 프로토콜은 Server Core에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 Windows PowerShell을 통해 설정할 수 있습니다. 다음 단계를 수행하십시오.  
  
1.  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 또는 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core를 실행하는 컴퓨터에서 작업 관리자를 실행합니다.  
  
2.  **응용 프로그램** 탭에서 **새 작업**을 클릭합니다.  
  
3.  **새 작업 만들기** 대화 상자에서 **열기** 필드에 **sqlps.exe** 를 입력하고 **확인**을 클릭합니다. 이렇게 하면 **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell** 창이 열립니다.  
  
4.  **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell** 창에서 다음 스크립트를 실행하여 TCP/IP 프로토콜을 사용하도록 설정합니다.  
  
```  
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = new-object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
## <a name="uninstallation"></a>제거  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 또는 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core를 실행하는 컴퓨터에 로그인하면 관리자 명령 프롬프트를 통한 제한된 데스크톱 환경이 제공됩니다. 이 명령 프롬프트를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스 제거를 시작할 수 있습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스를 제거하려면 /Q  매개 변수를 사용하는 완전 자동 모드 또는 /QS  매개 변수를 사용하는 단순 자동 모드로 명령 프롬프트에서 제거를 시작합니다. /QS  매개 변수는 UI를 통해 진행률을 표시하지만 입력은 허용하지 않습니다. /Q는 사용자 인터페이스 없이 자동 모드로 실행됩니다.  
  
 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 제거하려면:  
  
```  
Setup.exe /Q /Action=Uninstall /FEATURES=SQLEngine,AS,IS /INSTANCENAME=MSSQLSERVER  
```  
  
 명명된 인스턴스를 제거하려면 앞서 설명한 예에서 "MSSQLSERVER"  대신 인스턴스 이름을 사용하십시오.  
  
> [!WARNING]
>  실수로 명령 프롬프트를 닫은 경우 다음 단계에 따라 새 명령 프롬프트를 시작할 수 있습니다.  
> 
>  1.  Ctrl+Shift+Esc를 눌러 작업 관리자를 표시합니다.  
> 2.  **응용 프로그램** 탭에서 **새 작업**을 클릭합니다.  
> 3.  **새 태스크 만들기** 대화 상자에서 **열기** 필드에 **cmd** 를 입력한 다음 [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
## <a name="see-also"></a>관련 항목  
 [Install SQL Server 2014 구성 파일을 사용 하 여](install-sql-server-using-a-configuration-file.md)   
 [명령 프롬프트에서 SQL Server 2014 설치](install-sql-server-from-the-command-prompt.md)   
 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Server Core 설치 옵션 시작 가이드](https://go.microsoft.com/fwlink/?LinkId=221422)   
 [Server Core 설치 구성: 개요](https://go.microsoft.com/fwlink/?LinkId=221423)   
 [태스크 기준으로 나열된 Windows PowerShell의 장애 조치(failover) 클러스터 Cmdlet](https://go.microsoft.com/fwlink/?LinkId=221419)   
 [Cluster.exe 명령을 장애 조치(failover) 클러스터용 Windows PowerShell Cmdlet에 매핑](https://go.microsoft.com/fwlink/?LinkId=221421)  
  
  
