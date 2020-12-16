---
title: SQL Server 설치 - 명령 프롬프트 매개 변수
description: 이 문서에서는 SQL Server 설치를 위한 명령 매개 변수를 설명합니다. 설치 및 구성할 기능을 지정할 수 있습니다.
ms.prod: sql
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, command prompt
- installation scripts [SQL Server]
- maintenance scripts [SQL Server]
- REMOVENODE property
- components [SQL Server], removing
- command prompt [SQL Server], SQL Server installations
- ASACCOUNT parameter
- failover clustering [SQL Server], installing
- master database [SQL Server], rebuilding
- SQLCOLLATION parameter
- clusters [SQL Server], installing
- unattended installations [SQL Server]
- modifying collations
- AGTPASSWORD parameter
- USESYSDB parameter
- RSPASSWORD parameter
- AUTOSTART parameter
- ASPASSWORD parameter
- stand-alone installations [SQL Server]
- SAMPLEDATABASESERVER parameter
- adding components
- SAPWD parameter
- scripts [SQL Server], uninstallations
- remote installations [SQL Server]
- components [SQL Server], installing
- TARGETCOMPUTER parameter
- REMOVENODE parameter
- REINSTALLMODE parameter
- scripts [SQL Server], maintenance
- rebuilding registry
- SQLPASSWORD parameter
- rebuilding databases
- IP property
- PIDKEY parameter
- RSCONFIGURATION parameter
- ADDLOCAL parameter
- Setup [SQL Server], command prompt
- REBUILDDATABASE parameter
- SECURITYMODE parameter
- REMOVE property
- DISABLENETWORKPROTOCOLS parameter
- INSTALLDATADIR parameter
- REMOVE parameter
- removing components
- SQLACCOUNT parameter
- parameters [SQL Server], SQL Server installations
- UPGRADE parameter
- shortcuts [SQL Server]
- updating components
- removing SQL Server
- clustered instance of SQL Server
- INSTALLSQLDATADIR parameter
- RSACCOUNT parameter
- ADMINPASSWORD parameter
- GROUP property
- ERRORREPORTING property
- uninstallation scripts [SQL Server]
- AGTACCOUNT parameter
- SAVESYSDB parameter
- INSTALLVS parameter
- INSTANCENAME parameter
- scripts [SQL Server], installations
- rebuilding database, master
- uninstalling SQL Server
- ASCOLLATION parameter
- .ini files
- ADDNODE parameter
- command line installations [SQL Server]
- VS parameter
- INSTALLASDATADIR parameter
- INSTALLSQLDIR parameter
- nodes [Faillover Clustering], command prompt
- INSTALLSQLSHAREDDIR parameter
ms.assetid: df40c888-691c-4962-a420-78a57852364d
author: cawrites
ms.author: chadam
ms.reviewer: ''
ms.custom: ''
ms.date: 07/26/2019
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 6d815a88b9ac185871ed12b8192f6a5a7741f23a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440244"
---
# <a name="install-sql-server-from-the-command-prompt"></a>방법: 명령 프롬프트에서 SQL Server 2008 R2 설치

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

SQL Server 설치 프로그램을 실행하기 전에 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)을 검토하세요.  

명령 프롬프트에서 새 SQL Server 인스턴스를 설치할 경우 설치할 기능과 그 기능을 어떻게 구성할지 지정할 수 있습니다. 또한 자동, 기본, 전체 상호 작용 등 설치 프로그램 사용자 인터페이스 사용 방식을 지정할 수도 있습니다.  

명령 프롬프트에서 설치하려면 관리 명령 프롬프트를 열고 [SQL Server 설치 미디어](https://www.microsoft.com/sql-server/sql-server-downloads) 내에 있는 setup.exe 위치로 이동합니다. 수행하려는 작업을 실현하는 필수 및 선택적 매개 변수와 함께 `setup.exe` 명령을 실행합니다.

`C:\SQLMedia\SQLServer2019> setup.exe /[Option] /[Option] = {value}`

다음의 예에서 SQL Server 데이터베이스 엔진, SQL Server Analysis Services, SQL Server Integration Services 및 SQL Server 도구를 자동 모드로 설치합니다.

```console
C:\SQLMedia\SQLServer2019> setup.exe /Q /IACCEPTSQLSERVERLICENSETERMS /ACTION="install" /PID="AAAAA-BBBBB-CCCCC-DDDDD-EEEEE" /FEATURES=SQL,AS,IS,Tools
/INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="MyDomain\MyAccount"
/SQLSVCPASSWORD="************" /SQLSYSADMINACCOUNTS="MyDomain\MyAccount "
/AGTSVCACCOUNT="MyDomain\MyAccount" /AGTSVCPASSWORD="************"
/ASSVCACCOUNT="MyDomain\MyAccount" /ASSVCPASSWORD="************"
/ISSVCAccount="MyDomain\MyAccount" /ISSVCPASSWORD="************"
/ASSYSADMINACCOUNTS="MyDomain\MyAccount"
```

콘솔 내에서 사용할 수 있는 모든 명령 목록을 보려면 /help 플래그를 사용하여 실행 파일을 실행합니다. 

```console
C:\SQLMedia\SQLServer2019> setup.exe /help
```

문서의 나머지 부분에서는 사용 가능한 매개 변수에 관해 자세히 설명합니다. 

  
> [!NOTE]
> 명령 프롬프트에서 설치할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 /Q 매개 변수를 사용하는 완전 자동 모드 또는 /QS 매개 변수를 사용하는 단순 자동 모드를 지원합니다. /QS 스위치를 사용하면 진행률만 표시되고 입력이 허용되지 않으므로 오류가 발생해도 오류 메시지가 표시되지 않습니다. /QS 매개 변수는 /Action=install이 지정된 경우에만 지원됩니다.  
  
 Microsoft 볼륨 라이선스 계약 또는 공급 업체와의 ISV 또는 OEM 계약과 같은 별도의 계약에 의해 보호되지 않는 한 설치 방법에 상관없이 개인 또는 업체 대표로서 소프트웨어 사용 조건에 대한 동의를 확인해야 합니다.  
  
 사용 조건은 검토 및 동의를 위해 설치 프로그램 사용자 인터페이스에 표시됩니다. /Q 또는 /QS 매개 변수를 사용하는 무인 설치는 /IACCEPTSQLSERVERLICENSETERMS 매개 변수를 포함해야 합니다. [Microsoft 소프트웨어 사용권 계약(Microsoft Software License Terms)](https://go.microsoft.com/fwlink/?LinkId=148209)에서 사용 조건을 별도로 검토할 수 있습니다.  
  
> [!NOTE] 
> 소프트웨어의 수령 방법(예: Microsoft 볼륨 라이선스를 통해 수령)에 따라 사용자의 소프트웨어 사용에 추가 조건이 적용될 수 있습니다.  
  
 명령 프롬프트 설치는 다음과 같은 경우에 지원됩니다.  
  
-   명령 프롬프트에 지정된 구문과 매개 변수를 사용하여 로컬 컴퓨터에서 SQL Server의 인스턴스 및 공유 구성 요소를 설치, 업그레이드 또는 제거합니다.    
-   장애 조치(Failover) 클러스터 인스턴스를 설치, 업그레이드 또는 제거합니다.   
-   한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전으로 업그레이드합니다.    
-   구성 파일에 지정된 구문과 매개 변수를 사용하여 로컬 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 설치하는 경우. 이 방법은 설치 구성을 여러 컴퓨터에 복사하거나 장애 조치 클러스터 설치의 여러 노드를 설치하는 데 사용할 수 있습니다.  
  
 
> [!NOTE]
> 로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다. 장애 조치 클러스터를 설치하려면 서비스로 로그인할 수 있고 모든 장애 조치 클러스터 노드에서 운영 체제의 일부로 작동할 수 있는 권한을 갖고 있는 로컬 관리자여야 합니다.  
  
##  <a name="proper-use-of-setup-parameters"></a><a name="ProperUse"></a> 적절한 설치 매개 변수 사용  
올바른 구문으로 설치 명령을 작성하려면 다음 지침을 따르십시오.  
  
-   /PARAMETER (예: `/INDICATEPROGRESS`)
-   /PARAMETER=true/false(예: `/SQLSVCINSTANTFILEINIT=True` )
-   /PARAMETER=1/0 부울 형식인 경우(예: `/TCPENABLED=1`)
-   /PARAMETER="value"(모두 단일 값 매개 변수인 경우). (예: `/PID="PID" /SQLSVCSTARTUPTYPE="Automatic"`)
    - 경로가 필요한 매개 변수의 경우: `/INSTANCEDIR=c:\Path` 또는 `/INSTANCEDIR="c:\Path"`가 지원됩니다.  
-   /PARAMETER="value1" "value2" "value3"(모두 다중 값 매개 변수인 경우). (예: `/SQLSYSADMINACCOUNTS="Contoso\John" "Contoso\Mary"`)
    - **예외**: `/FEATURES`는 다중 값 매개 변수이지만 해당 형식은 공백 없이 쉼표로 구분되는 `/FEATURES=AS,RS,IS`임 

  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 때 INSTANCEDIR과 SQLUSERDBDIR에 대해 동일한 디렉터리 경로를 지정한 경우 권한 누락으로 인해 SQL Server 에이전트 및 전체 텍스트 검색이 시작되지 않습니다.  
  
> [!NOTE]  
> 관계형 서버 값은 경로에 대해 추가 종료 백슬래시 형식(백슬래시 또는 두 개의 백슬래시 문자)을 지원합니다.  

다음 섹션에서는 설치, 업데이트 및 복구 시나리오를 위한 명령줄 설치 스크립트를 개발하는 데 필요한 매개 변수를 제공합니다.  
  
[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소의 매개 변수 목록은 해당 구성 요소에만 적용됩니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 설치할 때 SQL Server 에이전트 및 SQL Server Browser 매개 변수가 적용됩니다.  


##  <a name="installation-parameters"></a><a name="Install"></a> 설치 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 설치 명령줄 스크립트를 개발할 수 있습니다.  
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|설치 워크플로를 지정하는 데 필요합니다.<br /><br /> 지원되는 값: **Install**.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/SUPPRESSPRIVACYSTATEMENTNOTICE<br /><br /> **무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.**|개인정보취급방침을 무시합니다. 이 플래그를 사용하면 [개인정보취급방침](../../sql-server/sql-server-privacy.md)에 동의하는 것입니다.  |  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.**|사용 조건에 대한 동의를 확인하는 데 필요합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Python 설치 컨트롤|/IACCEPTPYTHONLICENSETERMS <br /><br /> **Anaconda Python 패키지가 포함된 무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.**|사용 조건에 대한 동의를 확인하는 데 필요합니다.| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R 설치 컨트롤|/IACCEPTROPENLICENSETERMS <br /><br /> **Microsoft R Open 패키지가 포함된 무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.**|사용 조건에 대한 동의를 확인하는 데 필요합니다.| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/ENU<br /><br /> **선택 사항**|설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 이 매개 변수를 사용하여 지역화된 운영 체제에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 영어 버전을 설치할 수 있습니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/UpdateEnabled<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 제품 업데이트를 검색하고 포함하는지 여부를 지정합니다. 유효한 값은 True와 False 또는 1과 0입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에는 검색된 업데이트가 포함됩니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/UpdateSource<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 제품 업데이트를 가져올 위치를 지정합니다. 유효한 값은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update를 검색하는 경우 “MU”, 유효한 폴더 경로, 상대 경로(예: `.\MyUpdates`) 또는 UNC 공유입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 Windows Server Update Services를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update 또는 Windows Update 서비스를 검색합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/CONFIGURATIONFILE<br /><br /> **선택 사항**|사용할 [ConfigurationFile](./install-sql-server-using-a-configuration-file.md) 을 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/ERRORREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상에서는 영향을 주지 않습니다. <br/><br/> Microsoft로 오류 피드백을 보내는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 SQL Server 2016 이상을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 SQL Server의 오류 보고를 지정합니다.<br /><br /> 자세한 내용은 [Microsoft 오류 보고 서비스에 대한 개인 정보 취급 방침](../../sql-server/sql-server-privacy.md)을 참조하십시오.<br /><br /> 지원되는 값:<br /><br /> 0 = 사용 안 함<br /><br /> 1 = 사용|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/FEATURES<br /><br /> - 또는 -<br /><br /> /ROLE<br /><br /> **필수**|설치할 구성 요소를 지정합니다.<br /><br /> 설치할 개별 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 지정하려면 **/FEATURES** 를 선택합니다. 자세한 내용은 [기능 매개 변수](#Feature) 를 참조하세요.<br /><br /> 설치 역할을 지정하려면 **/ROLE** 을 선택합니다. 설치 역할은 미리 결정된 구성으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/HELP, ?<br /><br /> **선택 사항**|설치 매개 변수에 대한 사용 옵션을 표시합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INDICATEPROGRESS<br /><br /> **선택 사항**|세부 설치 로그 파일이 콘솔로 전달되도록 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INSTALLSHAREDDIR<br /><br /> **선택 사항**|64비트 공유 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다.<br /><br /> 기본값은 `%Program Files%\Microsoft SQL Server`<br /><br /> `%Program Files(x86)%\Microsoft SQL Server`로 설정할 수 없음|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INSTALLSHAREDWOWDIR<br /><br /> **선택 사항**|32비트 공유 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다. 64비트 시스템에서만 지원됩니다.<br /><br /> 기본값은 `%Program Files(x86)%\Microsoft SQL Server`<br /><br /> `%Program Files%\Microsoft SQL Server`로 설정할 수 없음|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INSTANCEDIR<br /><br /> **선택 사항**|인스턴스 관련 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INSTANCEID<br /><br /> **선택 사항**|[InstanceID](#InstanceID)에 대해 기본값이 아닌 다른 값을 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> **필수**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **선택 사항**|엔진 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE** 입니다.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **선택 사항**|엔진 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **선택 사항**|PolyBase 엔진 서비스의 시작 모드를 지정합니다. Automatic(기본값), Disabled 및 Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **선택 사항**|PolyBase 서비스용 6개 이상의 포트로 포트 범위를 지정합니다. 예제:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **선택 사항**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스가 PolyBase 규모 확장 계산 그룹의 일부로 사용될지를 지정합니다. 헤드 노드를 포함하는 PolyBase 스케일 아웃 계산 그룹을 구성할 경우 이 옵션을 사용합니다. 지원되는 값: **True**, **False**|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/PID<br /><br /> **선택 사항**|SQL Server 버전의 제품 키를 지정합니다. 이 매개 변수를 지정하지 않으면 Evaluation이 사용됩니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET<br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다. /Q 매개 변수는 /QS 매개 변수의 입력을 재정의합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/QS 또는 /QUIETSIMPLE <br /><br /> **선택 사항**|설치 프로그램이 UI를 통해 실행되고 진행률을 표시하지만 입력을 받거나 오류 메시지를 표시하지 않도록 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/UIMODE<br /><br /> **선택 사항**|설치 중에 최소 수의 대화 상자만 표시할지 여부를 지정합니다.<br /><br /> **/UIMode** 는 **/ACTION=INSTALL** 및 **UPGRADE** 매개 변수와만 사용할 수 있습니다. 지원되는 값:<br /><br /> **/UIMODE=Normal** 은 Express 이외의 버전에서 기본값이며 선택한 기능에 대해 모든 설치 대화 상자를 표시합니다.<br /><br /> **/UIMODE=AutoAdvance** 는 Express 버전의 기본값이며 필요하지 않은 대화 상자는 건너뜁니다.<br /><br /> <br /><br /> 다른 매개 변수와 조합해 사용하는 경우 **UIMODE** 는 무시됩니다. 예를 들어 **/UIMODE=AutoAdvance** 와 **/ADDCURRENTUSERASSQLADMIN=FALSE** 를 모두 제공하는 경우 프로비전 대화 상자에 현재 사용자가 자동으로 채워지지 않습니다.<br /><br /> **UIMode** 설정은 **/Q** 또는 **/QS** 매개 변수와 사용할 수 없습니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/SQMREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 SQL Server의 기능 사용 보고를 지정합니다.<br /><br />지원되는 값:<br /><br /> 0 = 사용 안 함<br /><br /> 1 = 사용|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트|/AGTSVCACCOUNT<br /><br /> **필수**|SQL Server 에이전트 서비스의 계정을 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트|/AGTSVCPASSWORD<br /><br /> [필수](#Accounts)|SQL Server 에이전트 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트|/AGTSVCSTARTUPTYPE<br /><br /> **선택 사항**|SQL Server 에이전트 서비스의 [시작](#Accounts) 모드를 지정합니다.<br /><br /> 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 백업 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Backup`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Backup`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 데이터 정렬 설정을 지정합니다.<br /><br /> 기본값: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Config`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Config`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Data`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Data`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 로그 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Log`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Log`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 서버 모드를 지정합니다. 유효한 값은 MULTIDIMENSIONAL, POWERPIVOT 또는 TABULAR입니다. **ASSERVERMODE** 는 대/소문자를 구분합니다. 모든 값은 대문자로 표시해야 합니다. 유효한 값에 대한 자세한 내용은 [Analysis Services 설치](/analysis-services/instances/install-windows/install-analysis-services)를 참조하세요.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **필수**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스 계정을 지정합니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [필수](#Accounts)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCSTARTUPTYPE<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **필수**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 관리자 자격 증명을 지정합니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 임시 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server \<INSTANCEDIR>\<ASInstanceID>\OLAP\Temp`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Temp`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **선택 사항**|MSOLAP 공급자를 in-process로 실행할 수 있는지 여부를 지정합니다.<br /><br /> 기본값: 1 = 사용|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMACCOUNT<br /><br /> **SPI_AS_NewFarm의 경우 필수**|팜에서 SharePoint 중앙 관리 서비스 및 기타 필수 서비스를 실행하는 데 사용할 도메인 사용자 계정을 지정합니다.<br /><br /> 이 매개 변수는 /ROLE = SPI_AS_NEWFARM을 통해 설치된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에만 사용됩니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMPASSWORD<br /><br /> **SPI_AS_NewFarm의 경우 필수**|팜 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/PASSPHRASE<br /><br /> **SPI_AS_NewFarm의 경우 필수**|SharePoint 팜에 애플리케이션 서버 또는 웹 프런트 엔드 서버를 더 추가하는 데 사용되는 암호를 지정합니다.<br /><br /> 이 매개 변수는 /ROLE = SPI_AS_NEWFARM을 통해 설치된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에만 사용됩니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMADMINIPORT<br /><br /> **SPI_AS_NewFarm의 경우 필수**|SharePoint 중앙 관리 웹 애플리케이션에 연결하는 데 사용되는 포트를 지정합니다.<br /><br /> 이 매개 변수는 /ROLE = SPI_AS_NEWFARM을 통해 설치된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에만 사용됩니다.|  
|SQL Server Browser|/BROWSERSVCSTARTUPTYPE<br /><br /> **선택 사항**|SQL Server Browser 서비스의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ENABLERANU<br /><br /> **선택 사항**|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 설치에 대해 '다음 계정으로 실행' 자격 증명을 사용하도록 설정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일의 데이터 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **/SECURITYMODE=SQL인 경우에 필수입니다.**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sa** 계정의 암호를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 보안 모드를 지정합니다.<br /><br /> 이 매개 변수가 제공되지 않은 경우 Windows 전용 인증 모드가 지원됩니다.<br /><br /> 지원되는 값: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **선택 사항**|백업 파일의 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Backup`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 데이터 정렬 설정을 지정합니다.<br /><br /> 기본 설치 설정은 OS(운영 체제) 로캘에 의해 결정됩니다. 설치 도중 서버 수준 데이터 정렬을 변경할 수도 있고, 설치하기 전에 OS 로캘을 변경할 수도 있습니다. 기본 데이터 정렬은 각 특정 로캘에 연결된 사용 가능 버전 중 가장 오래된 버전으로 설정됩니다. 이는 이전 버전과의 호환성을 유지하기 위함이므로 권장되는 데이터 정렬이 아닐 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 활용하려면 Windows 데이터 정렬을 사용하기 위한 기본 설치 설정을 변경하세요. 예를 들어 OS 로캘 **영어(미국)** (코드 페이지 1252)의 경우 설치 중의 기본 데이터 정렬은 **SQL_Latin1_General_CP1_CI_AS** 이고 가장 가까운 Windows 데이터 정렬인 **Latin1_General_100_CI_AS_SC** 로 변경될 수 있습니다. <br /><br />자세한 내용은 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ADDCURRENTUSERASSQLADMIN<br /><br /> **선택 사항**|현재 사용자를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysadmin** 고정 서버 역할에 추가합니다. /ADDCURRENTUSERASSQLADMIN 매개 변수는 /Role=ALLFeatures_WithDefaults를 사용하거나 Expression 버전을 설치할 때 사용할 수 있습니다. 자세한 내용은 아래의 /ROLE을 참조하세요.<br /><br /> /ADDCURRENTUSERASSQLADMIN은 원하는 경우 사용할 수 있지만 /ADDCURRENTUSERASSQLADMIN 또는 /SQLSYSADMINACCOUNTS는 반드시 사용해야 합니다. 기본값:<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 버전의 경우 **True**<br /><br /> 기타 모든 버전의 경우 **False**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **필수**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 시작 계정을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [필수](#Accounts)|SQLSVCACCOUNT의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다. |  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCSTARTUPTYPE<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **필수**|이 매개 변수를 사용하여 로그인을 sysadmin 역할의 멤버로 프로비전합니다.<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 이외의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서는 /SQLSYSADMINACCOUNTS가 필수 항목입니다. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 버전에서 /SQLSYSADMINACCOUNTS는 원하는 경우 사용할 수 있지만 /SQLSYSADMINACCOUNTS 또는 /ADDCURRENTUSERASSQLADMIN은 반드시 사용해야 합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **선택 사항**|tempdb 데이터 파일에 대한 디렉터리를 지정합니다. 둘 이상의 디렉터리를 지정할 경우 각 계정 이름을 공백으로 구분합니다. 여러 디렉터리가 지정된 경우 tempdb 데이터 파일은 라운드 로빈 방식으로 여러 디렉터리에 분배됩니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`(시스템 데이터 디렉터리)<br /><br /> **참고:** 이 매개 변수는 RebuildDatabase 시나리오에도 추가됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **선택 사항**|tempdb 로그 파일의 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`(시스템 데이터 디렉터리)<br /><br /> 참고: 이 매개 변수는 RebuildDatabase 시나리오에도 추가됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **선택 사항**|설치 프로그램에서 추가할 tempdb 데이터 파일 수를 지정합니다. 이 값은 코어 수까지 증가할 수 있습니다. 기본값:<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 1<br /><br /> 8 또는 코어 수 중에서 모든 기타 버전의 경우 낮은 값<br /><br /> **중요** tempdb에 대한 주 데이터베이스 파일은 여전히 tempdb.mdf입니다. 추가 tempdb 파일은 이름이 tempdb_mssql_#.ndf로 지정됩니다(여기서 #은 설치하는 동안 만들어진 각 추가 tempdb 데이터베이스 파일의 고유 개수를 나타냄). 이 명명 규칙의 목적은 고유한 파일 이름을 지정하는 것입니다. SQL Server 인스턴스를 제거하면 tempdb_mssql_#.ndf 명명 규칙을 사용하는 파일이 삭제됩니다. 사용자 데이터베이스 파일에 tempdb_mssql_\*.ndf 명명 규칙을 사용하지 마세요.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 도입되었습니다. 각 tempdb 데이터 파일의 초기 크기를 지정합니다.<br/><br/>기본값 = [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4MB, 다른 모든 버전의 경우 8MB.<br/><br/>최소 = (4MB 또는 8MB).<br/><br/>최댓값 = 1,024MB([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 262,144MB|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **선택 사항**|각 tempdb 데이터 파일의 파일 증가 증분을 MB 단위로 지정합니다. 값이 0이면 자동 증가가 해제되어 있고 추가 공간이 허용되지 않음을 나타냅니다. 설치에서는 최대 1,024MB의 크기를 허용합니다.<br /><br /> 기본값: 64. 허용 범위: 최소 = 0, 최대 = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 도입되었습니다. 각 tempdb 로그 파일의 초기 크기를 지정합니다.<br/><br/>기본값 = [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4MB, 다른 모든 버전의 경우 8MB.<br/><br/>최소 = (4MB 또는 8MB).<br/><br/>최댓값 = 1,024MB([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 262,144MB|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **선택 사항**|각 tempdb 데이터 파일의 파일 증가 증분을 MB 단위로 지정합니다. 값이 0이면 자동 증가가 해제되어 있고 추가 공간이 허용되지 않음을 나타냅니다. 설치에서는 최대 1,024MB의 크기를 허용합니다.<br /><br /> 기본값: 64. 허용 범위: 최소 = 0, 최대 = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **선택 사항**|사용자 데이터베이스의 데이터 파일에 대한 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCINSTANTFILEINIT<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 빠른 파일 초기화를 사용하도록 설정합니다. 보안 및 성능 고려 사항은 [데이터베이스 즉시 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)을 참조하세요.<br /><br /> 기본값: "False"<br /><br /> 선택적 값: "True"|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **선택 사항**|사용자 데이터베이스의 로그 파일에 대한 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLMAXDOP=매개 변수 <br /><br /> **선택 사항** <br /> 무인(자동) 설치에서 누락된 경우 MAXDOP는 [최대 병렬 처리 수준 지침](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)과 일치합니다. |단일 문 실행 중에 단일 문을 사용할 수 있는 프로세서 수를 결정하는 최대 병렬 처리 수준을 지정합니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터만 사용할 수 있습니다. <br /><br /> 기본값은 [최대 병렬 처리 수준 지침](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)과 일치합니다.|
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/USESQLRECOMMENDEDMEMORYLIMITS<br /><br /> **선택 사항** <br /> 무인(자동) 설치에서 /USESQLRECOMMENDEDMEMORYLIMITS, /SQLMINMEMORY 및 /SQLMAXMEMORY를 생략하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 구성을 사용합니다.|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 [서버 메모리 구성 지침](../../database-engine/configure-windows/server-memory-server-configuration-options.md#manually)과 일치하는 계산된 권장 값을 사용하도록 지정합니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터만 사용할 수 있습니다.<br /><br /> **참고:** 이 매개 변수는 /SQLMINMEMORY 및 /SQLMAXMEMORY와 함께 사용할 수 없습니다. |  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLMINMEMORY<br /><br /> **선택 사항** <br /> 무인(자동) 설치에서 /USESQLRECOMMENDEDMEMORYLIMITS, /SQLMINMEMORY 및 /SQLMAXMEMORY를 생략하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 구성을 사용합니다.|MB에 최소 서버 메모리 구성을 지정합니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터만 사용할 수 있습니다.<br /><br /> 기본값: 0.<br /><br /> **참고:** 이 매개 변수는 /USESQLRECOMMENDEDMEMORYLIMITS와 함께 사용할 수 없습니다. |  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLMAXMEMORY<br /><br /> **선택 사항** <br /> 무인(자동) 설치에서 /USESQLRECOMMENDEDMEMORYLIMITS, /SQLMINMEMORY 및 /SQLMAXMEMORY를 생략하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 구성을 사용합니다.|MB에 최대 서버 메모리 구성을 지정합니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터만 사용할 수 있습니다.<br /><br /> 기본값: 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 [서버 메모리 구성 지침](../../database-engine/configure-windows/server-memory-server-configuration-options.md#manually)과 일치하는 계산된 권장 값입니다.<br /><br /> **참고:** 이 매개 변수는 /USESQLRECOMMENDEDMEMORYLIMITS와 함께 사용할 수 없습니다. |  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **선택 사항**|FILESTREAM 기능의 액세스 수준을 지정합니다. 지원되는 값:<br /><br /> 0 = 이 인스턴스에 대한 FILESTREAM 지원을 해제합니다. (기본값)<br /><br /> 1 = [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스에 FILESTREAM을 사용하도록 설정합니다.<br /><br /> 2 = [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 파일 I/O 스트리밍 액세스에 FILESTREAM을 사용하도록 설정합니다. (클러스터 시나리오에는 적합하지 않습니다)<br /><br /> 3 = 원격 클라이언트가 FILESTREAM 데이터에 대한 스트리밍 액세스 권한을 가질 수 있도록 허용합니다.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **선택 사항**<br /><br /> **FILESTREAMLEVEL이 1보다 큰 경우 필수입니다.**|FILESTREAM 데이터가 저장될 Windows 공유의 이름을 지정합니다.|  
|SQL Server 전체 텍스트|/FTSVCACCOUNT<br /><br /> **선택 사항**|전체 텍스트 필터 시작 관리자 서비스의 계정을 지정합니다.<br /><br /> 이 매개 변수는 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 이상에서 무시됩니다. ServiceSID는 SQL Server와 전체 텍스트 필터 데몬 간 통신의 보안을 유지하는 데 도움을 주기 위해 사용됩니다. 값이 제공되지 않으면 전체 텍스트 필터 시작 관리자 서비스를 사용할 수 없습니다. 서비스 계정을 변경하고 전체 텍스트 기능을 사용하려면 SQL Server 제어 관리자를 사용해야 합니다.<br /><br /> 기본값: Local Service Account|  
|SQL Server 전체 텍스트|/FTSVCPASSWORD<br /><br /> **선택 사항**|전체 텍스트 필터 시작 관리자 서비스의 암호를 지정합니다.<br /><br /> 이 매개 변수는 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 이상에서 무시됩니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **필수**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 계정을 지정합니다.<br /><br /> 기본값: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [필수](#Accounts)|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **선택 사항**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 [시작](#Accounts) 모드를 지정합니다.|  
|SQL Server 네트워크 구성|/NPENABLED<br /><br /> **선택 사항**|SQL Server 서비스의 명명된 파이프 프로토콜 상태를 지정합니다. 지원되는 값:<br /><br /> 0 = 명명된 파이프 프로토콜 해제<br /><br /> 1 = 명명된 파이프 프로토콜을 사용하도록 설정|  
|SQL Server 네트워크 구성|/TCPENABLED<br /><br /> **선택 사항**|SQL Server 서비스의 TCP 프로토콜 상태를 지정합니다. 지원되는 값:<br /><br /> 0 = TCP 프로토콜 해제<br /><br /> 1 = TCP 프로토콜을 사용하도록 설정|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **선택 사항**| SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 설치 모드를 지정합니다. 지원되는 값:<br /><br /> **SharePointFilesOnlyMode**<br /><br /> **DefaultNativeMode**<br /><br /> **FilesOnlyMode**<br /><br /> <br /><br /> 참고: 설치에 SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 포함되는 경우 기본 RSINSTALLMODE는 DefaultNativeMode입니다.<br /><br /> 설치에 SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 포함되지 않는 경우 기본 RSINSTALLMODE는 FilesOnlyMode입니다.<br /><br /> DefaultNativeMode를 선택해도 설치에 SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 포함되지 않는 경우 설치 시 RSINSTALLMODE가 FilesOnlyMode로 자동 변경됩니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **필수**| SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 시작 계정을 지정합니다. |  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [필수](#Accounts)|SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 시작 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **선택 사항**|SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
|Python/Machine Learning Services(데이터베이스 내)|/MPYCACHEDIRECTORY|다음에 사용하도록 예약됩니다. 인터넷 연결이 되지 않은 컴퓨터에 설치하기 위한 Python .CAB 파일을 저장하려면 %TEMP%를 사용합니다. |  
|R/Machine Learning Services(데이터베이스 내)|/MRCACHEDIRECTORY|이 매개 변수를 사용하여 SQL Server Machine Learning Services 또는 Machine Learning Server(독립 실행형)에서 Microsoft R Open, SQL Server 2016 R Services, SQL Server 2016 R Server(독립 실행형) 또는 R 기능을 지원하는 데 사용할 캐시 디렉터리를 지정할 수 있습니다. 일반적으로 이 설정은 [인터넷에 액세스할 수 없는 컴퓨터의 명령줄](../../machine-learning/install/sql-ml-component-install-without-internet-access.md)에서 R 구성 요소를 설치하는 경우에 사용됩니다.|  
|Java/언어 확장| /SQL_INST_JAVA,<br /> /SQLJAVADIR = "path"<br /><br /> **선택 사항** | SQL Server 2019부터 언어 확장을 사용하여 Java를 설치하도록 지정합니다. /SQLJAVADIR 매개 변수 없이 /SQL_INST_JAVA를 제공하면 설치 미디어에서 제공되는 Zulu Open JRE를 설치하려는 것으로 가정합니다. <br /><br /> /SQLJAVADIR의 경로를 제공하면 이미 설치된 JRE 또는 JDK를 사용하려는 것임을 나타냅니다. |
  
###### <a name="sample-syntax"></a>예제 구문:  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], 복제 및 전체 텍스트 Search 구성 요소가 포함된 새로운 독립 실행형 인스턴스를 설치하고 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 빠른 파일 초기화를 사용하도록 설정합니다. 
  
```  
setup.exe /q /ACTION=Install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /SQLSVCINSTANTFILEINIT="True" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
##  <a name="sysprep-parameters"></a><a name="SysPrep"></a> SysPrep 매개 변수  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep에 대한 자세한 내용은 다음 항목을 참조  
  
 [SysPrep을 사용하여 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 설치](../../database-engine/install-windows/install-sql-server-using-sysprep.md). 
  
#### <a name="prepare-image-parameters"></a>이미지 매개 변수 준비  
 다음 표에 나와 있는 매개 변수를 사용하여 SQL Server 인스턴스를 구성하지 않고 준비하는 명령줄 스크립트를 개발할 수 있습니다. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|설치 워크플로를 지정하는 데 필요합니다.<br /><br /> 지원되는 값: **PrepareImage**|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.**|사용 조건에 대한 동의를 확인하는 데 필요합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/ENU<br /><br /> **선택 사항**|설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 이 매개 변수를 사용하여 지역화된 운영 체제에 SQL Server 영어 버전을 설치할 수 있습니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/UpdateEnabled<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 제품 업데이트를 검색하고 포함하는지 여부를 지정합니다. 유효한 값은 True와 False 또는 1과 0입니다. 기본적으로 SQL Server 설치 프로그램에는 검색된 업데이트가 포함됩니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/UpdateSource<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 제품 업데이트를 가져올 위치를 지정합니다. 유효한 값은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update를 검색하는 경우 “MU”, 유효한 폴더 경로, 상대 경로(예: `.\MyUpdates`) 또는 UNC 공유입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 Windows Server Update Services를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update 또는 Windows Update 서비스를 검색합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/CONFIGURATIONFILE<br /><br /> **선택 사항**|사용할 [ConfigurationFile](./install-sql-server-using-a-configuration-file.md) 을 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/FEATURES<br /><br /> **필수**|설치할 [구성 요소](#Feature) 를 지정합니다.<br /><br /> 지원되는 값은 SQLEngine, Replication, FullText, DQ, AS, AS_SPI, RS, RS_SHP, RS_SHPWFE, DQC, Conn, IS, BC, SDK, DREPLAY_CTLR, DREPLAY_CLT, SNAC_SDK, SQLODBC, SQLODBC_SDK, LocalDB, MDS, POLYBASE임|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/HELP, ?<br /><br /> **선택 사항**|설치 매개 변수에 대한 사용 옵션을 표시합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INDICATEPROGRESS<br /><br /> **선택 사항**|세부 설치 로그 파일이 콘솔로 전달되도록 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INSTALLSHAREDDIR<br /><br /> **선택 사항**|64비트 공유 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다.<br /><br /> 기본값은 `%Program Files%\Microsoft SQL Server`<br /><br /> `%Program Files(x86)%\Microsoft SQL Server`로 설정할 수 없음|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INSTANCEDIR<br /><br /> **선택 사항**|인스턴스 관련 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INSTANCEID<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2(2013년 1월) 이전 버전은 **필수**<br /><br /> 인스턴스 기능은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2부터 **필수**.|준비 중인 인스턴스의 InstanceID를 지정합니다.|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **선택 사항**|엔진 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE** 입니다.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **선택 사항**|엔진 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **선택 사항**|PolyBase 엔진 서비스의 시작 모드를 지정합니다. Automatic(기본값), Disabled 및 Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **선택 사항**|PolyBase 서비스용 6개 이상의 포트로 포트 범위를 지정합니다. 예제:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **선택 사항**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스가 PolyBase 규모 확장 계산 그룹의 일부로 사용될지를 지정합니다. 지원되는 값: **True**, **False**|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET <br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다. /Q 매개 변수는 /QS 매개 변수의 입력을 재정의합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/QS 또는 /QUIETSIMPLE<br /><br /> **선택 사항**|설치 프로그램이 UI를 통해 실행되고 진행률을 표시하지만 입력을 받거나 오류 메시지를 표시하지 않도록 지정합니다.|  
  
###### <a name="sample-syntax"></a>예제 구문:  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], 복제, 전체 텍스트 검색 구성 요소 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]가 포함된 새로운 독립 실행형 인스턴스를 준비합니다. 
  
```  
setup.exe /q /ACTION=PrepareImage /FEATURES=SQL,RS /InstanceID =<MYINST> /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="complete-image-parameters"></a>이미지 완료 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 준비된 SQL Server 인스턴스를 구성하고 완료하는 명령줄 스크립트를 개발할 수 있습니다. 
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|설치 워크플로를 지정하는 데 필요합니다.<br /><br /> 지원되는 값: **CompleteImage**|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.**|사용 조건에 대한 동의를 확인하는 데 필요합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/ENU<br /><br /> **선택 사항**|설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 이 매개 변수를 사용하여 지역화된 운영 체제에 SQL Server 영어 버전을 설치할 수 있습니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/CONFIGURATIONFILE<br /><br /> **선택 사항**|사용할 [ConfigurationFile](./install-sql-server-using-a-configuration-file.md) 을 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/ERRORREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 SQL Server의 오류 보고를 지정합니다.<br /><br /> 자세한 내용은 [Microsoft 오류 보고 서비스에 대한 개인 정보 취급 방침](../../sql-server/sql-server-privacy.md)을 참조하십시오. 지원되는 값:<br /><br /> 1 = 사용<br /><br /> 0 = 사용 안 함|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/HELP, ?<br /><br /> **선택 사항**|설치 매개 변수에 대한 사용 옵션을 표시합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INDICATEPROGRESS<br /><br /> **선택 사항**|세부 설치 로그 파일이 콘솔로 전달되도록 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INSTANCEID<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2(2013년 1월) 이전 버전은 **필수**<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2부터 **선택**|이미지 준비 단계 중에 지정한 인스턴스 ID를 사용합니다.<br /><br /> 지원되는 값: 준비된 인스턴스의 InstanceID|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2(2013년 1월) 이전 버전은 **필수**<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2부터 **선택**|완료 중인 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **선택 사항**|엔진 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE** 입니다.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **선택 사항**|엔진 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **선택 사항**|PolyBase 엔진 서비스의 시작 모드를 지정합니다. Automatic(기본값), Disabled 및 Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **선택 사항**|PolyBase 서비스용 6개 이상의 포트로 포트 범위를 지정합니다. 예제:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **선택 사항**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스가 PolyBase 규모 확장 계산 그룹의 일부로 사용될지를 지정합니다. 지원되는 값: **True**, **False**|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/PID<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 제품 키를 지정합니다. 이 매개 변수를 지정하지 않으면 Evaluation이 사용됩니다.<br /><br /> **참고:** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Tools 또는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services를 설치하는 경우에는 PID가 미리 정의됩니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET <br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다. /Q 매개 변수는 /QS 매개 변수의 입력을 재정의합니다. |  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/QS 또는 /QUIETSIMPLE<br /><br /> **선택 사항**|설치 프로그램이 UI를 통해 실행되고 진행률을 표시하지만 입력을 받거나 오류 메시지를 표시하지 않도록 지정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/SQMREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 SQL Server의 기능 사용 보고를 지정합니다.<br /><br />지원되는 값:<br /><br /> 0 = 사용 안 함<br /><br /> 1 = 사용|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
|SQL Server 에이전트|/AGTSVCACCOUNT<br /><br /> **필수**|SQL Server 에이전트 서비스의 계정을 지정합니다.|  
|SQL Server 에이전트|/AGTSVCPASSWORD<br /><br /> [필수](#Accounts)|SQL Server 에이전트 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|SQL Server 에이전트|/AGTSVCSTARTUPTYPE<br /><br /> **선택 사항**|SQL Server 에이전트 서비스의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
|SQL Server Browser|/BROWSERSVCSTARTUPTYPE<br /><br /> **선택 사항**|SQL Server Browser 서비스의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ENABLERANU<br /><br /> **선택 사항**|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 설치에 대해 '다음 계정으로 실행' 자격 증명을 사용하도록 설정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일의 데이터 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **/SECURITYMODE=SQL인 경우에 필수입니다.**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sa** 계정의 암호를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 보안 모드를 지정합니다.<br /><br /> 이 매개 변수가 제공되지 않은 경우 Windows 전용 인증 모드가 지원됩니다.<br /><br /> 지원되는 값: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **선택 사항**|백업 파일의 디렉터리를 지정합니다.<br /><br /> 기본값:<br /><br /> `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Backup`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 데이터 정렬 설정을 지정합니다.<br /><br /> 기본값은 Windows 운영 체제의 로캘을 기반으로 합니다. 자세한 내용은 [설치 프로그램에서 데이터 정렬 설정](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하십시오.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **필수**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 시작 계정을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [필수](#Accounts)|SQLSVCACCOUNT의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCSTARTUPTYPE<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **필수**|이 매개 변수를 사용하여 로그인을 sysadmin 역할의 멤버로 프로비전합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **선택 사항**|tempdb 데이터 파일에 대한 디렉터리를 지정합니다. 둘 이상의 디렉터리를 지정할 경우 각 계정 이름을 공백으로 구분합니다. 여러 디렉터리가 지정된 경우 tempdb 데이터 파일은 라운드 로빈 방식으로 여러 디렉터리에 분배됩니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`(시스템 데이터 디렉터리)<br /><br /> 참고:  이 매개 변수는 RebuildDatabase 시나리오에도 추가됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **선택 사항**|tempdb 로그 파일의 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`(시스템 데이터 디렉터리)<br /><br /> 참고: 이 매개 변수는 RebuildDatabase 시나리오에도 추가됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 도입되었습니다. 각 tempdb 데이터 파일의 초기 크기를 지정합니다.<br/><br/>기본값 = [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4MB, 다른 모든 버전의 경우 8MB.<br/><br/>최소 = (4MB 또는 8MB).<br/><br/>최댓값 = 1,024MB([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 262,144MB.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **선택 사항**|각 tempdb 데이터 파일의 파일 증가 증분을 MB 단위로 지정합니다. 값이 0이면 자동 증가가 해제되어 있고 추가 공간이 허용되지 않음을 나타냅니다. 설치에서는 최대 1,024MB의 크기를 허용합니다.<br /><br /> 기본값: 64<br /><br /> 허용 범위: 최소 = 0, 최대 = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **선택 사항**|tempdb 로그 파일의 초기 크기를 MB 단위로 지정합니다. 설치에서는 최대 1,024MB의 크기를 허용합니다.<br /><br /> 기본값:<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4<br /><br /> 기타 모든 버전의 경우 8<br /><br /> 허용 범위: 최소 = 기본값(4 또는 8), 최대 = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 도입되었습니다. 각 tempdb 로그 파일의 초기 크기를 지정합니다.<br/><br/>기본값 = [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4MB, 다른 모든 버전의 경우 8MB.<br/><br/>최소 = (4MB 또는 8MB).<br/><br/>최댓값 = 1,024MB([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 262,144MB|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **선택 사항**|설치 프로그램에서 추가할 tempdb 데이터 파일 수를 지정합니다. 이 값은 코어 수까지 증가할 수 있습니다. 기본값:<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 1<br /><br /> 8 또는 코어 수 중에서 모든 기타 버전의 경우 낮은 값<br /><br /> **중요:** tempdb에 대한 주 데이터베이스 파일은 여전히 tempdb.mdf입니다. 추가 tempdb 파일은 이름이 tempdb_mssql_#.ndf로 지정됩니다(여기서 #은 설치하는 동안 만들어진 각 추가 tempdb 데이터베이스 파일의 고유 개수를 나타냄). 이 명명 규칙의 목적은 고유한 파일 이름을 지정하는 것입니다. SQL Server 인스턴스를 제거하면 tempdb_mssql_#.ndf 명명 규칙을 사용하는 파일이 삭제됩니다. 사용자 데이터베이스 파일에 tempdb_mssql_\*.ndf 명명 규칙을 사용하지 마세요.<br /><br /> **경고:** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]는 이 매개 변수를 구성하는 데 지원되지 않습니다. 설치 프로그램은 1개의 tempdb 데이터 파일만 설치합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **선택 사항**|사용자 데이터베이스의 데이터 파일에 대한 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **선택 사항**|사용자 데이터베이스의 로그 파일에 대한 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **선택 사항**|FILESTREAM 기능의 액세스 수준을 지정합니다. 지원되는 값:<br /><br /> 0 = 이 인스턴스에 대한 FILESTREAM 지원을 해제합니다. (기본값)<br /><br /> 1 = [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스에 FILESTREAM을 사용하도록 설정합니다.<br /><br /> 2 = [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 파일 I/O 스트리밍 액세스에 FILESTREAM을 사용하도록 설정합니다. (클러스터 시나리오에는 적합하지 않습니다)<br /><br /> 3 = 원격 클라이언트가 FILESTREAM 데이터에 대한 스트리밍 액세스 권한을 가질 수 있도록 허용합니다.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **선택 사항**<br /><br /> **FILESTREAMLEVEL이 1보다 큰 경우 필수입니다.**|FILESTREAM 데이터가 저장될 Windows 공유의 이름을 지정합니다.|  
|SQL Server 전체 텍스트|/FTSVCACCOUNT<br /><br /> **선택 사항**|전체 텍스트 필터 시작 관리자 서비스의 계정을 지정합니다.<br /><br /> 이 매개 변수는 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 이상에서 무시됩니다. ServiceSID는 SQL Server와 전체 텍스트 필터 데몬 간 통신의 보안을 유지하는 데 도움을 주기 위해 사용됩니다. 값이 제공되지 않으면 전체 텍스트 필터 시작 관리자 서비스를 사용할 수 없습니다. 서비스 계정을 변경하고 전체 텍스트 기능을 사용하려면 SQL Server 제어 관리자를 사용해야 합니다.<br /><br /> 기본값: Local Service Account|  
|SQL Server 전체 텍스트|/FTSVCPASSWORD<br /><br /> **선택 사항**|전체 텍스트 필터 시작 관리자 서비스의 암호를 지정합니다.<br /><br /> 이 매개 변수는 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 이상에서 무시됩니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다. |  
|SQL Server 네트워크 구성|/NPENABLED<br /><br /> **선택 사항**|SQL Server 서비스의 명명된 파이프 프로토콜 상태를 지정합니다. 지원되는 값:<br /><br /> 0 = 명명된 파이프 프로토콜 해제<br /><br /> 1 = 명명된 파이프 프로토콜을 사용하도록 설정|  
|SQL Server 네트워크 구성|/TCPENABLED<br /><br /> **선택 사항**|SQL Server 서비스의 TCP 프로토콜 상태를 지정합니다. 지원되는 값:<br /><br /> 0 = TCP 프로토콜 해제<br /><br /> 1 = TCP 프로토콜을 사용하도록 설정|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **선택 사항**|SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 설치 모드를 지정합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **필수**|SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 시작 계정을 지정합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [필수](#Accounts)| SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 시작 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **선택 사항**|SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
  
###### <a name="sample-syntax"></a>예제 구문:  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], 복제 및 전체 텍스트 검색 구성 요소가 포함된 준비된 독립 실행형 인스턴스를 완료합니다. 
  
```  
setup.exe /q /ACTION=CompleteImage /INSTANCENAME=MYNEWINST /INSTANCEID=<MYINST> /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
##  <a name="upgrade-parameters"></a><a name="Upgrade"></a> 업그레이드 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 업그레이드 명령줄 스크립트를 개발할 수 있습니다. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|설치 워크플로를 지정하는 데 필요합니다. 지원되는 값:<br /><br /> **업그레이드**<br /><br /> **EditionUpgrade**<br /><br /> <br /><br /> **EditionUpgrade** 값은 기존 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전을 다른 버전으로 업그레이드하는 데 사용됩니다. 지원되는 버전 및 버전 업그레이드에 대한 자세한 내용은 [지원되는 버전 및 버전 업그레이드](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)를 참조하세요.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.**|사용 조건에 대한 동의를 확인하는 데 필요합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ENU<br /><br /> **선택 사항**|설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 이 매개 변수를 사용하여 지역화된 운영 체제에 SQL Server 영어 버전을 설치할 수 있습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/*UpdateEnabled*<br /><br /> **선택 사항**|SQL Server 설치 프로그램이 제품 업데이트를 검색하고 포함하는지 여부를 지정합니다. 유효한 값은 True와 False 또는 1과 0입니다. 기본적으로 SQL Server 설치 프로그램에는 검색된 업데이트가 포함됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/*UpdateSource*<br /><br /> **선택 사항**|SQL Server 설치 프로그램이 제품 업데이트를 가져올 위치를 지정합니다. 유효한 값은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update를 검색하는 경우 “MU”, 유효한 폴더 경로, 상대 경로(예: .\MyUpdates) 또는 UNC 공유입니다. 기본적으로 SQL Server 설치 프로그램은 Windows Server Update Services를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 업데이트 또는 Windows Server 업데이트 서비스를 검색합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/CONFIGURATIONFILE<br /><br /> **선택 사항**|사용할 [ConfigurationFile](./install-sql-server-using-a-configuration-file.md) 을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ERRORREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 SQL Server의 오류 보고를 지정합니다.<br /><br /> 자세한 내용은 [Microsoft 오류 보고 서비스에 대한 개인 정보 취급 방침](../../sql-server/sql-server-privacy.md)을 참조하십시오. 지원되는 값:<br /><br /> 1 = 사용<br /><br /> 0 = 사용 안 함|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HELP, ?<br /><br /> **선택 사항**|매개 변수에 대한 사용 옵션을 표시합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INDICATEPROGRESS<br /><br /> **선택 사항**|세부 설치 로그 파일이 콘솔로 전달되도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ INSTANCEDIR<br /><br /> **선택 사항**|공유 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCEID<br /><br /> **[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]** 이상에서 업그레이드하는 경우 필수입니다.<br /><br /> **[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 업그레이드하는 경우 선택 사항**|[InstanceID](#InstanceID)에 대해 기본값이 아닌 다른 값을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> **필수**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/PID<br /><br /> **선택 사항**|SQL Server 버전의 제품 키를 지정합니다. 이 매개 변수를 지정하지 않으면 Evaluation이 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/Q<br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/UIMODE<br /><br /> **선택 사항**|설치 중에 최소 수의 대화 상자만 표시할지 여부를 지정합니다. <br />                **/UIMode** 는 **/ACTION=INSTALL** 및 **UPGRADE** 매개 변수와만 사용할 수 있습니다. 지원되는 값:<br /><br /> **/UIMODE=Normal** 은 Express 이외의 버전에서 기본값이며 선택한 기능에 대해 모든 설치 대화 상자를 표시합니다.<br /><br /> **/UIMODE=AutoAdvance** 는 Express 버전의 기본값이며 필요하지 않은 대화 상자는 건너뜁니다.<br /><br /> **UIMode** 설정은 **/Q** 또는 **/QS** 매개 변수와 사용할 수 없습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/SQMREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 SQL Server의 기능 사용 보고를 지정합니다.<br /><br />지원되는 값:<br /><br /> 1 = 사용<br /><br /> 0 = 사용 안 함|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
|SQL Server Browser 서비스|/BROWSERSVCSTARTUPTYPE<br /><br /> **선택 사항**|SQL Server Browser 서비스의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
|SQL Server 전체 텍스트|/FTUPGRADEOPTION<br /><br /> **선택 사항**|전체 텍스트 카탈로그 업그레이드 옵션을 지정합니다. 지원되는 값:<br /><br /> **REBUILD**<br /><br /> **RESET**<br /><br /> **IMPORT**|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **필수**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 계정을 지정합니다.<br /><br /> 기본값: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [필수](#Accounts)|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **선택 사항**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 [시작](#Accounts) 모드를 지정합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEDATABASEACCOUNT<br /><br /> **선택 사항**|이 속성은 2008 R2 버전 이상의 SharePoint 모드 보고서 서버를 업그레이드할 때만 사용됩니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 변경된 이전 SharePoint 모드 아키텍처를 사용하는 보고서 서버에서는 추가 업그레이드 작업이 수행됩니다. 이 옵션이 명령줄 설치에 포함되지 않은 경우 이전 보고서 서버 인스턴스의 기본 서비스 계정이 사용됩니다. 이 속성이 사용된 경우에는 **/RSUPGRADEPASSWORD** 속성을 사용해서 계정 암호를 제공하십시오.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEPASSWORD<br /><br /> **선택 사항**|기존 보고서 서버 서비스 계정 암호입니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/ALLOWUPGRADEFORSSRSSHAREPOINTMODE|SharePoint 공유 서비스 아키텍처를 기반으로 하는 SharePoint 모드 설치를 업그레이드할 때 스위치가 필요합니다. 공유 서비스 이외의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]버전을 업그레이드할 때는 이 스위치가 필요하지 않습니다.|  
  
###### <a name="sample-syntax"></a>예제 구문:  
 이전 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 버전에서 기존 인스턴스 또는 장애 조치(failover) 클러스터 노드를 업그레이드하려면  
  
```  
setup.exe /q /ACTION=upgrade /INSTANCEID = <INSTANCEID>/INSTANCENAME=MSSQLSERVER /RSUPGRADEDATABASEACCOUNT="<Provide a SQL Server logon account that can connect to the report server during upgrade>" /RSUPGRADEPASSWORD="<Provide a password for the report server upgrade account>" /ISSVCAccount="NT Authority\Network Service" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
##  <a name="repair-parameters"></a><a name="Repair"></a> 복구 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 복구 명령줄 스크립트를 개발할 수 있습니다. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|복구 워크플로를 나타내는 데 필요합니다.<br /><br /> 지원되는 값: **Repair**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ENU<br /><br /> **선택 사항**|설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 이 매개 변수를 사용하여 지역화된 운영 체제에 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 영어 버전을 설치할 수 있습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FEATURES<br /><br /> **필수**|복구할 [구성 요소](#Feature) 를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> **필수**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **선택 사항**|엔진 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE** 입니다.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **선택 사항**|엔진 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **선택 사항**|PolyBase 엔진 서비스의 시작 모드를 지정합니다. Automatic(기본값), Disabled 및 Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **선택 사항**|PolyBase 서비스용 6개 이상의 포트로 포트 범위를 지정합니다. 예제:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **선택 사항**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스가 PolyBase 규모 확장 계산 그룹의 일부로 사용될지를 지정합니다. 지원되는 값: **True**, **False**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET <br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
  
###### <a name="sample-syntax"></a>예제 구문:  
 인스턴스 및 공유 구성 요소를 복구합니다. 
  
```  
setup.exe /q /ACTION=Repair /INSTANCENAME=<instancename>  
```  
  
##  <a name="rebuild-system-database-parameters"></a><a name="Rebuild"></a> 시스템 데이터베이스 다시 작성 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 master, model, msdb 및 tempdb 시스템 데이터베이스를 다시 작성하는 명령줄 스크립트를 개발할 수 있습니다. 자세한 내용은 [시스템 데이터베이스 다시 작성](../../relational-databases/databases/rebuild-system-databases.md)을 참조하세요. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|데이터베이스 다시 작성 워크플로를 나타내는 데 필요합니다.<br /><br /> 지원되는 값: **Rebuilddatabase**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> **필수**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET <br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **선택 사항**|서버 수준 데이터 정렬을 새로 지정합니다.<br /><br /> 기본값은 Windows 운영 체제의 로캘을 기반으로 합니다. 자세한 내용은 [설치 프로그램에서 데이터 정렬 설정](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하십시오.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **인스턴스를 설치하는 동안 /SECURITYMODE=SQL을 지정한 경우 필수입니다.**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SA** 계정의 암호를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **필수**|이 매개 변수를 사용하여 로그인을 sysadmin 역할의 멤버로 프로비전합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **선택 사항**|tempdb 데이터 파일에 대한 디렉터리를 지정합니다. 둘 이상의 디렉터리를 지정할 경우 각 계정 이름을 공백으로 구분합니다. 여러 디렉터리가 지정된 경우 tempdb 데이터 파일은 라운드 로빈 방식으로 여러 디렉터리에 분배됩니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`(시스템 데이터 디렉터리)<br /><br /> 참고:  이 매개 변수는 RebuildDatabase 시나리오에도 추가됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **선택 사항**|tempdb 로그 파일의 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`(시스템 데이터 디렉터리)<br /><br /> **참고:** 이 매개 변수는 RebuildDatabase 시나리오에도 추가됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **선택 사항**|설치 프로그램에서 추가할 tempdb 데이터 파일 수를 지정합니다. 이 값은 코어 수까지 증가할 수 있습니다. 기본값:<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 1<br /><br /> 8 또는 코어 수 중에서 모든 기타 버전의 경우 낮은 값<br /><br /> **중요:** tempdb에 대한 주 데이터베이스 파일은 여전히 tempdb.mdf입니다. 추가 tempdb 파일은 이름이 tempdb_mssql_#.ndf로 지정됩니다(여기서 #은 설치하는 동안 만들어진 각 추가 tempdb 데이터베이스 파일의 고유 개수를 나타냄). 이 명명 규칙의 목적은 고유한 파일 이름을 지정하는 것입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 제거하면 tempdb_mssql_#.ndf 명명 규칙을 사용하는 파일이 삭제됩니다. 사용자 데이터베이스 파일에 tempdb_mssql_\*.ndf 명명 규칙을 사용하지 마세요.<br /><br /> **경고:** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]는 이 매개 변수를 구성하는 데 지원되지 않습니다. 설치 프로그램은 1개의 tempdb 데이터 파일만 설치합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 도입되었습니다. 각 tempdb 데이터 파일의 초기 크기를 지정합니다.<br/><br/>기본값 = [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4MB, 다른 모든 버전의 경우 8MB.<br/><br/>최소 = (4MB 또는 8MB).<br/><br/>최댓값 = 1,024MB([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 262,144MB.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **선택 사항**|각 tempdb 데이터 파일의 파일 증가 증분을 MB 단위로 지정합니다. 값이 0이면 자동 증가가 해제되어 있고 추가 공간이 허용되지 않음을 나타냅니다. 설치에서는 최대 1,024MB의 크기를 허용합니다.<br /><br /> 기본값: 64<br /><br /> 허용 범위: 최소 = 0, 최대 = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **선택 사항**|tempdb 로그 파일의 초기 크기를 MB 단위로 지정합니다. 설치에서는 최대 1,024MB의 크기를 허용합니다. 기본값:<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4<br /><br /> 기타 모든 버전의 경우 8<br /><br /> 허용 범위: 최소 = 기본값(4 또는 8), 최대 = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 도입되었습니다. 각 tempdb 로그 파일의 초기 크기를 지정합니다.<br/><br/>기본값 = [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4MB, 다른 모든 버전의 경우 8MB.<br/><br/>최소 = (4MB 또는 8MB).<br/><br/>최댓값 = 1,024MB([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 262,144MB|  
  
##  <a name="uninstall-parameters"></a><a name="Uninstall"></a> 제거 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 제거 명령줄 스크립트를 개발할 수 있습니다. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|제거 워크플로를 나타내는 데 필요합니다.<br /><br /> 지원되는 값: **제거**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/CONFIGURATIONFILE<br /><br /> **선택 사항**|사용할 [ConfigurationFile](./install-sql-server-using-a-configuration-file.md) 을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FEATURES<br /><br /> **필수**|제거할 [구성 요소](#Feature) 를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HELP, H,?<br /><br /> **선택 사항**|매개 변수에 대한 사용 옵션을 표시합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INDICATEPROGRESS<br /><br /> **선택 사항**|세부 설치 로그 파일이 콘솔로 전달되도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> **필수**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET <br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
  
###### <a name="sample-syntax"></a>예제 구문:  
 기존 SQL Server 인스턴스를 제거합니다. 
  
```  
setup.exe /Action=Uninstall /FEATURES=SQL,AS,RS,IS,Tools /INSTANCENAME=MSSQLSERVER  
```  
  
 명명된 인스턴스를 제거하려면 이 문서의 앞부분에서 설명한 예에서 "MSSQLSERVER" 대신 인스턴스 이름을 사용합니다. 
  
##  <a name="failover-cluster-parameters"></a><a name="ClusterInstall"></a> 장애 조치 클러스터 매개 변수  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치 클러스터 인스턴스를 설치하기 전에 다음 문서를 검토합니다.  
  
-   [[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)
  
-   [장애 조치(Failover) 클러스터링을 설치하기 전에](../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)  
  
-   [Always On 장애 조치(failover) 클러스터 인스턴스&#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
    > [!IMPORTANT]  
    > 모든 장애 조치 클러스터 설치 명령에는 기본 Windows 클러스터가 필요합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치 클러스터에 속하는 모든 노드는 동일한 Windows 클러스터에 속해야 합니다. 
  
 조직의 필요에 따라 다음 장애 조치 클러스터 설치 스크립트를 테스트하고 수정하십시오. 
  
#### <a name="integrated-install-failover-cluster-parameters"></a>장애 조치 클러스터 통합 설치 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 장애 조치(Failover) 클러스터 설치 명령줄 스크립트를 개발할 수 있습니다. 
  
 통합 설치에 대한 자세한 내용은 [Always On 장애 조치 클러스터 인스턴스&#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)를 참조하세요. 
  
> [!NOTE]
> 설치 후에 다른 노드를 추가하려면 [노드 추가](#AddNode) 동작을 사용하십시오. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|세부 정보|  
|-----------------------------------------|---------------|-------------|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|장애 조치(Failover) 클러스터 설치 워크플로를 나타내는 데 필요합니다.<br /><br /> 지원되는 값: **InstallFailoverCluster**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.**|사용 조건에 대한 동의를 확인하는 데 필요합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ENU<br /><br /> **선택 사항**|설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 이 매개 변수를 사용하여 지역화된 운영 체제에 SQL Server 영어 버전을 설치할 수 있습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FAILOVERCLUSTERGROUP<br /><br /> **선택 사항**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(Failover) 클러스터에 사용되는 리소스 그룹의 이름을 지정합니다. 기존 클러스터 그룹의 이름이거나 새 리소스 그룹의 이름일 수 있습니다.<br /><br /> 기본값:<br /><br /> SQL Server (\<InstanceName>)|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **선택 사항**|엔진 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE** 입니다.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **선택 사항**|엔진 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다. |  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **선택 사항**|PolyBase 엔진 서비스의 시작 모드를 지정합니다. Automatic(기본값), Disabled 및 Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **선택 사항**|PolyBase 서비스용 6개 이상의 포트로 포트 범위를 지정합니다. 예제:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **선택 사항**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스가 PolyBase 규모 확장 계산 그룹의 일부로 사용될지를 지정합니다. 지원되는 값: **True**, **False**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/*UpdateEnabled*<br /><br /> **선택 사항**|SQL Server 설치 프로그램이 제품 업데이트를 검색하고 포함하는지 여부를 지정합니다. 유효한 값은 True와 False 또는 1과 0입니다. 기본적으로 SQL Server 설치 프로그램에는 검색된 업데이트가 포함됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/*UpdateSource*<br /><br /> **선택 사항**|SQL Server 설치 프로그램이 제품 업데이트를 가져올 위치를 지정합니다. 유효한 값은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update를 검색하는 경우 “MU”, 유효한 폴더 경로, 상대 경로(예: .\MyUpdates) 또는 UNC 공유입니다. 기본적으로 SQL Server 설치 프로그램은 Windows Server Update Services를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 업데이트 또는 Windows Server 업데이트 서비스를 검색합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/CONFIGURATIONFILE<br /><br /> **선택 사항**|사용할 [ConfigurationFile](./install-sql-server-using-a-configuration-file.md) 을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ERRORREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 SQL Server의 오류 보고를 지정합니다.<br /><br /> 자세한 내용은 [Microsoft 오류 보고 서비스에 대한 개인 정보 취급 방침](../../sql-server/sql-server-privacy.md)을 참조하십시오. 지원되는 값:<br /><br /> 1 = 사용<br /><br /> 0 = 사용 안 함|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FEATURES<br /><br /> **필수**|설치할 [구성 요소](#Feature) 를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HELP, ?<br /><br /> **선택 사항**|매개 변수에 대한 사용 옵션을 표시합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INDICATEPROGRESS<br /><br /> **선택 사항**|세부 설치 로그 파일이 콘솔로 전달되도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTALLSHAREDDIR<br /><br /> **선택 사항**|64비트 공유 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다.<br /><br /> 기본값은 `%Program Files%\Microsoft SQL Server`<br /><br /> `%Program Files(x86)%\Microsoft SQL Server`로 설정할 수 없음|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTALLSHAREDWOWDIR<br /><br /> **선택 사항**|32비트 공유 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다. 64비트 시스템에서만 지원됩니다.<br /><br /> 기본값은 `%Program Files(x86)%\Microsoft SQL Server`<br /><br /> `%Program Files%\Microsoft SQL Server`로 설정할 수 없음|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCEDIR<br /><br /> **선택 사항**|인스턴스 관련 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCEID<br /><br /> **선택 사항**|[InstanceID](#InstanceID)에 대해 기본값이 아닌 다른 값을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> **필수**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/PID<br /><br /> **선택 사항**|SQL Server 버전의 제품 키를 지정합니다. 이 매개 변수를 지정하지 않으면 Evaluation이 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET <br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다. /Q 매개 변수는 /QS 매개 변수의 입력을 재정의합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/QS 또는 /QUIETSIMPLE <br /><br /> **선택 사항**|설치 프로그램이 UI를 통해 실행되고 진행률을 표시하지만 입력을 받거나 오류 메시지를 표시하지 않도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/SQMREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 SQL Server의 기능 사용 보고를 지정합니다.<br /><br />지원되는 값:<br /><br /> 1 = 사용<br /><br /> 0 = 사용 안 함|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FAILOVERCLUSTERDISKS<br /><br /> **선택 사항**|공유 디스크 목록이 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(failover) 클러스터 리소스 그룹에 포함되도록 지정합니다.<br /><br /> 기본값: 첫 번째 드라이브가 모든 데이터베이스의 기본 드라이브로 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **필수**|인코딩된 IP 주소를 지정합니다. 인코딩은 세미콜론(;)으로 구분되며 \<IP Type>;\<address>;\<network name>;\<subnet mask> 형식을 따릅니다. 지원되는 IP 유형에는 DHCP, IPv4 및 IPv6이 있습니다.<br />주소 사이에 공백을 넣어 여러 장애 조치(failover) 클러스터 IP 주소를 지정할 수 있습니다. 다음 예제를 참조하세요.<br /><br /> `FAILOVERCLUSTERIPADDRESSES=DEFAULT`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FAILOVERCLUSTERNETWORKNAME<br /><br /> **필수**|새 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(failover) 클러스터의 네트워크 이름을 지정합니다. 이 이름은 네트워크에서 새 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스를 식별하는 데 사용됩니다.|  
|SQL Server 에이전트|/AGTSVCACCOUNT<br /><br /> **필수**|SQL Server 에이전트 서비스의 계정을 지정합니다.|  
|SQL Server 에이전트|/AGTSVCPASSWORD<br /><br /> [필수](#Accounts)|SQL Server 에이전트 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 백업 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Backup`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Backup`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 데이터 정렬 설정을 지정합니다.<br /><br /> 기본값: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Config`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Config`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Data`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Data`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 로그 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Log`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Log`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **필수**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 관리자 자격 증명을 지정합니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 임시 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Temp`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Temp`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **선택 사항**|MSOLAP 공급자를 in-process로 실행할 수 있는지 여부를 지정합니다.<br /><br /> 기본값: 1 = 사용|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 서버 모드를 지정합니다. 클러스터 시나리오에서 유효한 값은 MULTIDIMENSIONAL 또는 TABULAR입니다. **ASSERVERMODE** 는 대/소문자를 구분합니다. 모든 값은 대문자로 표시해야 합니다. 유효한 값에 대한 자세한 내용은 테이블 형식 모드에서 Analysis Services 설치를 참조하십시오.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **필수**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일의 데이터 디렉터리를 지정합니다.<br /><br /> 데이터 디렉터리는 공유 클러스터 디스크에 지정되어야 합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **/SECURITYMODE=SQL인 경우에 필수입니다.**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sa** 계정의 암호를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 보안 모드를 지정합니다.<br /><br /> 이 매개 변수가 제공되지 않은 경우 Windows 전용 인증 모드가 지원됩니다.<br /><br /> 지원되는 값: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **선택 사항**|백업 파일의 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Backup`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 데이터 정렬 설정을 지정합니다.<br /><br /> 기본값은 Windows 운영 체제의 로캘을 기반으로 합니다. 자세한 내용은 [설치 프로그램에서 데이터 정렬 설정](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하십시오.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **필수**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 시작 계정을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [필수](#Accounts)|SQLSVCACCOUNT의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **필수**|이 매개 변수를 사용하여 로그인을 **sysadmin** 역할의 멤버로 프로비전합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **선택 사항**|사용자 데이터베이스의 데이터 파일에 대한 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **선택 사항**|tempdb 데이터 파일에 대한 디렉터리를 지정합니다. 둘 이상의 디렉터리를 지정할 경우 각 계정 이름을 공백으로 구분합니다. 여러 디렉터리가 지정된 경우 tempdb 데이터 파일은 라운드 로빈 방식으로 여러 디렉터리에 분배됩니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`(시스템 데이터 디렉터리)<br /><br /> 참고:  이 매개 변수는 RebuildDatabase 시나리오에도 추가됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **선택 사항**|tempdb 로그 파일의 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`(시스템 데이터 디렉터리)<br /><br /> 참고: 이 매개 변수는 RebuildDatabase 시나리오에도 추가됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **선택 사항**|설치 프로그램에서 추가할 tempdb 데이터 파일 수를 지정합니다. 이 값은 코어 수까지 증가할 수 있습니다. 기본값:<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 1<br /><br /> 8 또는 코어 수 중에서 모든 기타 버전의 경우 낮은 값<br /><br /> **중요:** tempdb에 대한 주 데이터베이스 파일은 여전히 tempdb.mdf입니다. 추가 tempdb 파일은 이름이 tempdb_mssql_#.ndf로 지정됩니다(여기서 #은 설치하는 동안 만들어진 각 추가 tempdb 데이터베이스 파일의 고유 개수를 나타냄). 이 명명 규칙의 목적은 고유한 파일 이름을 지정하는 것입니다. SQL Server 인스턴스를 제거하면 tempdb_mssql_#.ndf 명명 규칙을 사용하는 파일이 삭제됩니다. 사용자 데이터베이스 파일에 tempdb_mssql_\*.ndf 명명 규칙을 사용하지 마세요.<br /><br /> **경고:** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]는 이 매개 변수를 구성하는 데 지원되지 않습니다. 설치 프로그램은 1개의 tempdb 데이터 파일만 설치합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 도입되었습니다. 각 tempdb 데이터 파일의 초기 크기를 지정합니다.<br/><br/>기본값 = 8MB.<br/><br/>최솟값 = 8MB.<br/><br/>최댓값 = 1,024MB([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 262,144MB.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **선택 사항**|각 tempdb 데이터 파일의 파일 증가 증분을 MB 단위로 지정합니다. 값이 0이면 자동 증가가 해제되어 있고 추가 공간이 허용되지 않음을 나타냅니다. 설치에서는 최대 1,024MB의 크기를 허용합니다.<br /><br /> 기본값: 64<br /><br /> 허용 범위: 최소 = 0, 최대 = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **선택 사항**|tempdb 로그 파일의 초기 크기를 MB 단위로 지정합니다. 설치에서는 최대 1,024MB의 크기를 허용합니다. <br /> 기본값:<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4<br /><br /> 기타 모든 버전의 경우 8<br /><br /> 허용 범위: 최소 = 기본값(4 또는 8), 최대 = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 도입되었습니다. 각 tempdb 로그 파일의 초기 크기를 지정합니다.<br/><br/>기본값 = [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4MB, 다른 모든 버전의 경우 8MB.<br/><br/>최소 = (4MB 또는 8MB).<br/><br/>최댓값 = 1,024MB([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 262,144MB|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **선택 사항**|사용자 데이터베이스의 로그 파일에 대한 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **선택 사항**|FILESTREAM 기능의 액세스 수준을 지정합니다. 지원되는 값:<br /><br /> 0 = 이 인스턴스에 대한 FILESTREAM 지원을 해제합니다. (기본값)<br /><br /> 1 = [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스에 FILESTREAM을 사용하도록 설정합니다.<br /><br /> 2 = [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 파일 I/O 스트리밍 액세스에 FILESTREAM을 사용하도록 설정합니다. (클러스터 시나리오에는 적합하지 않습니다)<br /><br /> 3 = 원격 클라이언트가 FILESTREAM 데이터에 대한 스트리밍 액세스 권한을 가질 수 있도록 허용합니다.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **선택 사항**<br /><br /> **FILESTREAMLEVEL이 1보다 큰 경우 필수입니다.**|FILESTREAM 데이터가 저장될 Windows 공유의 이름을 지정합니다.|  
|SQL Server 전체 텍스트|/FTSVCACCOUNT<br /><br /> **선택 사항**|전체 텍스트 필터 시작 관리자 서비스의 계정을 지정합니다.<br /><br /> 이 매개 변수는 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 이상에서 무시됩니다. ServiceSID는 SQL Server와 전체 텍스트 필터 데몬 간 통신의 보안을 유지하는 데 도움을 주기 위해 사용됩니다.<br /><br /> 값이 제공되지 않으면 전체 텍스트 필터 시작 관리자 서비스를 사용할 수 없습니다. 서비스 계정을 변경하고 전체 텍스트 기능을 사용하려면 SQL Server 제어 관리자를 사용해야 합니다.<br /><br /> 기본값: Local Service Account|  
|SQL Server 전체 텍스트|/FTSVCPASSWORD<br /><br /> **선택 사항**|전체 텍스트 필터 시작 관리자 서비스의 암호를 지정합니다.<br /><br /> 이 매개 변수는 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 이상에서 무시됩니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **필수**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 계정을 지정합니다.<br /><br /> 기본값: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [필수](#Accounts)|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **선택 사항**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 [시작](#Accounts) 모드를 지정합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **선택 사항**|SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 설치 모드를 지정합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **필수**|SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 시작 계정을 지정합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [필수](#Accounts)| SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 시작 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **선택 사항**|SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
  
 도메인 그룹 대신 서비스 SID를 사용하는 것이 좋습니다. 
  
##### <a name="additional-notes"></a>참고 사항:  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 클러스터를 인식하는 유일한 구성 요소입니다. 기타 기능은 클러스터를 인식하지 않으므로 장애 조치(Failover)에서 가용성이 높지 않습니다. 
  
###### <a name="sample-syntax"></a>예제 구문:  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)]와 함께 기본 인스턴스로 단일 노드 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스를 설치합니다. 
  
```  
setup.exe /q /ACTION=InstallFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'" /FAILOVERCLUSTERNETWORKNAME="<Insert Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /Features=AS,SQL /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /SQLSYSADMINACCOUNTS="<DomainName\UserName> /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="prepare-failover-cluster-parameters"></a>장애 조치 클러스터 준비 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 장애 조치(Failover) 클러스터 준비 명령줄 스크립트를 개발할 수 있습니다. 이것은 클러스터 고급 설치의 첫째 단계이며 여기서 모든 장애 조치(Failover) 클러스터 노드의 장애 조치(Failover) 클러스터 인스턴스를 준비해야 합니다. 자세한 내용은 [Always On 장애 조치(failover) 클러스터 인스턴스&#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)를 참조하세요. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|장애 조치(Failover) 클러스터 준비 워크플로를 나타내는 데 필요합니다.<br /><br /> 지원되는 값: **PrepareFailoverCluster**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.**|사용 조건에 대한 동의를 확인하는 데 필요합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ENU<br /><br /> **선택 사항**|설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 이 매개 변수를 사용하여 지역화된 운영 체제에 SQL Server 영어 버전을 설치할 수 있습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/*UpdateEnabled*<br /><br /> **선택 사항**|SQL Server 설치 프로그램이 제품 업데이트를 검색하고 포함하는지 여부를 지정합니다. 유효한 값은 True와 False 또는 1과 0입니다. 기본적으로 SQL Server 설치 프로그램에는 검색된 업데이트가 포함됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/*UpdateSource*<br /><br /> **선택 사항**|SQL Server 설치 프로그램이 제품 업데이트를 가져올 위치를 지정합니다. 유효한 값은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update를 검색하는 경우 “MU”, 유효한 폴더 경로, 상대 경로(예: `.\MyUpdates`) 또는 UNC 공유입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 Windows Server Update Services를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update 또는 Windows Update 서비스를 검색합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/CONFIGURATIONFILE<br /><br /> **선택 사항**|사용할 [ConfigurationFile](./install-sql-server-using-a-configuration-file.md) 을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ERRORREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 SQL Server의 오류 보고를 지정합니다.<br /><br /> 자세한 내용은 [Microsoft 오류 보고 서비스에 대한 개인 정보 취급 방침](../../sql-server/sql-server-privacy.md)을 참조하십시오. 지원되는 값:<br /><br /> 0 = 사용 안 함<br /><br /> 1 = 사용|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FEATURES<br /><br /> **필수**|설치할 [구성 요소](#Feature) 를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HELP, ?<br /><br /> **선택 사항**|매개 변수에 대한 사용 옵션을 표시합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INDICATEPROGRESS<br /><br /> **선택 사항**|세부 설치 로그 파일이 콘솔로 전달되도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTALLSHAREDDIR<br /><br /> **선택 사항**|64비트 공유 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다.<br /><br /> 기본값은 `%Program Files%\Microsoft SQL Server`<br /><br /> `%Program Files(x86)%\Microsoft SQL Server`로 설정할 수 없음|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTALLSHAREDWOWDIR<br /><br /> **선택 사항**|32비트 공유 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다. 64비트 시스템에서만 지원됩니다.<br /><br /> 기본값은 `%Program Files(x86)%\Microsoft SQL Server`<br /><br /> `%Program Files%\Microsoft SQL Server`로 설정할 수 없음|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCEDIR<br /><br /> **선택 사항**|인스턴스 관련 구성 요소에 대해 기본 디렉터리가 아닌 다른 설치 디렉터리를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCEID<br /><br /> **선택 사항**|[InstanceID](#InstanceID)에 대해 기본값이 아닌 다른 값을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> **필수**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **선택 사항**|엔진 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE** 입니다.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **선택 사항**|엔진 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **선택 사항**|PolyBase 엔진 서비스의 시작 모드를 지정합니다. Automatic(기본값), Disabled 및 Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **선택 사항**|PolyBase 서비스용 6개 이상의 포트로 포트 범위를 지정합니다. 예제:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **선택 사항**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스가 PolyBase 규모 확장 계산 그룹의 일부로 사용될지를 지정합니다. 지원되는 값: **True**, **False**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/PID<br /><br /> **선택 사항**|SQL Server 버전의 제품 키를 지정합니다. 이 매개 변수가 지정되지 않은 경우<br /><br /> Evaluation이 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET <br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다. /Q 매개 변수는 /QS 매개 변수의 입력을 재정의합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/QS 또는 /QUIETSIMPLE <br /><br /> **선택 사항**|설치 프로그램이 UI를 통해 실행되고 진행률을 표시하지만 입력을 받거나 오류 메시지를 표시하지 않도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/SQMREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 SQL Server의 기능 사용 보고를 지정합니다.<br /><br />지원되는 값:<br /><br /> 0 = 사용 안 함<br /><br /> 1 = 사용|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
|SQL Server 에이전트|/AGTSVCACCOUNT<br /><br /> **필수**|SQL Server 에이전트 서비스의 계정을 지정합니다.|  
|SQL Server 에이전트|/AGTSVCPASSWORD<br /><br /> [필수](#Accounts)|SQL Server 에이전트 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다. |  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **필수**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스 계정을 지정합니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [필수](#Accounts)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **필수**|SQL Server 서비스의 시작 계정을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [필수](#Accounts)|SQLSVCACCOUNT의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **선택 사항**|FILESTREAM 기능의 액세스 수준을 지정합니다. 지원되는 값:<br /><br /> 0 = 이 인스턴스에 대한 FILESTREAM 지원을 해제합니다. (기본값)<br /><br /> 1 = [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스에 FILESTREAM을 사용하도록 설정합니다.<br /><br /> 2 = [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 파일 I/O 스트리밍 액세스에 FILESTREAM을 사용하도록 설정합니다. (클러스터 시나리오에는 적합하지 않습니다)<br /><br /> 3 = 원격 클라이언트가 FILESTREAM 데이터에 대한 스트리밍 액세스 권한을 가질 수 있도록 허용합니다.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **선택 사항**<br /><br /> FILESTREAMLEVEL이 1보다 큰 경우 **필수** 입니다.|FILESTREAM 데이터가 저장될 Windows 공유의 이름을 지정합니다.|  
|SQL Server 전체 텍스트|/FTSVCACCOUNT<br /><br /> **선택 사항**|전체 텍스트 필터 시작 관리자 서비스의 계정을 지정합니다.<br /><br /> 이 매개 변수는 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 이상에서 무시됩니다. ServiceSID는 SQL Server와 전체 텍스트 필터 데몬 간 통신의 보안을 유지하는 데 도움을 주기 위해 사용됩니다.<br /><br /> 값이 제공되지 않으면 전체 텍스트 필터 시작 관리자 서비스를 사용할 수 없습니다. 서비스 계정을 변경하고 전체 텍스트 기능을 사용하려면 SQL Server 제어 관리자를 사용해야 합니다.<br /><br /> 기본값: Local Service Account|  
|SQL Server 전체 텍스트|/FTSVCPASSWORD<br /><br /> **선택 사항**|전체 텍스트 필터 시작 관리자 서비스의 암호를 지정합니다.<br /><br /> 이 매개 변수는 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 이상에서 무시됩니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **필수**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 계정을 지정합니다.<br /><br /> 기본값: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [필수](#Accounts)|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **선택 사항**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 [시작](#Accounts) 모드를 지정합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **파일만 모드에서 사용 가능**| SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 설치 모드를 지정합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **필수**| SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 시작 계정을 지정합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [필수](#Accounts)| SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 시작 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **선택 사항**| SQL Server 2017부터 더 이상 적용할 수 없습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
  
 도메인 그룹 대신 서비스 SID를 사용하는 것이 좋습니다. 
  
###### <a name="sample-syntax"></a>예제 구문:  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 위한 장애 조치(Failover) 클러스터 고급 설치 시나리오의 "준비" 단계를 수행합니다. 
  
 명령 프롬프트에서 다음 명령을 실행하여 기본 인스턴스를 준비합니다.  
  
```  
setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName=MSSQLSERVER /Features=AS,SQL /INDICATEPROGRESS /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
 명령 프롬프트에서 다음 명령을 실행하여 명명된 인스턴스를 준비합니다.  
  
```  
setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName="<Insert Instance name>" /Features=AS,SQL /INDICATEPROGRESS /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="complete-failover-cluster-parameters"></a>장애 조치 클러스터 완료 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 장애 조치(Failover) 클러스터 완료를 위한 명령줄 스크립트를 개발할 수 있습니다. 이것은 장애 조치(Failover) 클러스터 고급 설치 옵션의 두 번째 단계입니다. 모든 장애 조치(Failover) 클러스터 노드 준비를 실행한 다음, 공유 디스크를 소유하는 노드에서 이 명령을 실행합니다. 자세한 내용은 [Always On 장애 조치(failover) 클러스터 인스턴스&#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)를 참조하세요. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|장애 조치(Failover) 클러스터 완료 워크플로를 나타내는 데 필요합니다.<br /><br /> 지원되는 값: **CompleteFailoverCluster**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ENU<br /><br /> **선택 사항**|설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 이 매개 변수를 사용하여 지역화된 운영 체제에 SQL Server 영어 버전을 설치할 수 있습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FAILOVERCLUSTERGROUP<br /><br /> **선택 사항**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(Failover) 클러스터에 사용되는 리소스 그룹의 이름을 지정합니다. 기존 클러스터 그룹의 이름이거나 새 리소스 그룹의 이름일 수 있습니다.<br /><br /> 기본값:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](\<InstanceName>)|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/CONFIGURATIONFILE<br /><br /> **선택 사항**|사용할 [ConfigurationFile](./install-sql-server-using-a-configuration-file.md) 을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ERRORREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 오류 보고를 지정합니다.<br /><br /> 자세한 내용은 [Microsoft 오류 보고 서비스에 대한 개인 정보 취급 방침](../../sql-server/sql-server-privacy.md)을 참조하십시오. 지원되는 값:<br /><br /> 1 = 사용<br /><br /> 0 = 사용 안 함|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HELP, ?<br /><br /> **선택 사항**|매개 변수에 대한 사용 옵션을 표시합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INDICATEPROGRESS<br /><br /> **선택 사항**|세부 설치 로그 파일이 콘솔로 전달되도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> **필수**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [인스턴스 구성](../../sql-server/install/instance-configuration.md) 참조  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/PID<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 제품 키를 지정합니다. 이 매개 변수를 지정하지 않으면 Evaluation이 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET <br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다. /Q 매개 변수는 /QS 매개 변수의 입력을 재정의합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/QS 또는 /QUIETSIMPLE <br /><br /> **선택 사항**|설치 프로그램이 UI를 통해 실행되고 진행률을 표시하지만 입력을 받거나 오류 메시지를 표시하지 않도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/SQMREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기능 사용 보고를 지정합니다.<br /><br />지원되는 값:<br /><br /> 1 = 사용<br /><br /> 0 = 사용 안 함|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FAILOVERCLUSTERDISKS<br /><br /> **선택 사항**|공유 디스크 목록이 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(failover) 클러스터 리소스 그룹에 포함되도록 지정합니다.<br /><br /> 기본값:<br /><br /> 첫 번째 드라이브가 모든 데이터베이스의 기본 드라이브로 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **필수**|인코딩된 IP 주소를 지정합니다. 인코딩은 세미콜론(;)으로 구분되며 \<IP Type>;\<address>;\<network name>;\<subnet mask> 형식을 따릅니다. 지원되는 IP 유형에는 DHCP, IPv4 및 IPv6이 있습니다.<br />주소 사이에 공백을 넣어 여러 장애 조치(failover) 클러스터 IP 주소를 지정할 수 있습니다. 다음 예제를 참조하세요.<br /><br /> `FAILOVERCLUSTERIPADDRESSES=DEFAULT`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FAILOVERCLUSTERNETWORKNAME<br /><br /> **필수**|새 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(failover) 클러스터의 네트워크 이름을 지정합니다. 이 이름은 네트워크에서 새 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스를 식별하는 데 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/CONFIRMIPDEPENDENCYCHANGE|다중 서브넷 장애 조치(Failover) 클러스터의 IP 주소 리소스 종속성을 OR로 설정하는 데 대한 동의를 나타냅니다. 자세한 내용은 [새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)를 참조하세요. 지원되는 값:<br /><br /> 0 = False(기본값)<br /><br /> 1 = True|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 백업 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Backup`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Backup`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 데이터 정렬 설정을 지정합니다.<br /><br /> 기본값: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Config`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Config`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Data`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Data`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 로그 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Log`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Log`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **선택 사항**|Analysis Services 인스턴스의 서버 모드를 지정합니다. 클러스터 시나리오에서 유효한 값은 MULTIDIMENSIONAL 또는 TABULAR입니다. **ASSERVERMODE** 는 대/소문자를 구분합니다. 모든 값은 대문자로 표시해야 합니다. 유효한 값에 대한 자세한 내용은 테이블 형식 모드에서 Analysis Services 설치를 참조하십시오.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **필수**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 관리자 자격 증명을 지정합니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **선택 사항**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 임시 파일의 디렉터리를 지정합니다. 기본값:<br /><br /> 64비트 WOW 모드의 경우: `%Program Files(x86)%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Temp`<br /><br /> 기타 모든 설치의 경우: `%Program Files%\Microsoft SQL Server\<INSTANCEDIR>\<ASInstanceID>\OLAP\Temp`|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **선택 사항**|MSOLAP 공급자를 in-process로 실행할 수 있는지 여부를 지정합니다.<br /><br /> 기본값: 1 = 사용|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **필수**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일의 데이터 디렉터리를 지정합니다.<br /><br /> 데이터 디렉터리는 공유 클러스터 디스크에 지정되어야 합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **/SECURITYMODE=SQL인 경우에 필수입니다.**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sa** 계정의 암호를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 보안 모드를 지정합니다.<br /><br /> 이 매개 변수가 제공되지 않은 경우 Windows 전용 인증 모드가 지원됨<br /><br /> 지원되는 값: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **선택 사항**|백업 파일의 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Backup`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 데이터 정렬 설정을 지정합니다.<br /><br /> 기본값은 Windows 운영 체제의 로캘을 기반으로 합니다. 자세한 내용은 [설치 프로그램에서 데이터 정렬 설정](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하십시오.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **필수**|이 매개 변수를 사용하여 로그인을 sysadmin 역할의 멤버로 프로비전합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **선택 사항**|사용자 데이터베이스의 데이터 파일에 대한 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **선택 사항**|사용자 데이터베이스의 로그 파일에 대한 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **파일만 모드에서 사용 가능**| SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 설치 모드를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **선택 사항**|tempdb 데이터 파일에 대한 디렉터리를 지정합니다. 둘 이상의 디렉터리를 지정할 경우 각 계정 이름을 공백으로 구분합니다. 여러 디렉터리가 지정된 경우 tempdb 데이터 파일은 라운드 로빈 방식으로 여러 디렉터리에 분배됩니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`(시스템 데이터 디렉터리)<br /><br /> 참고:  이 매개 변수는 RebuildDatabase 시나리오에도 추가됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **선택 사항**|tempdb 로그 파일의 디렉터리를 지정합니다.<br /><br /> 기본값: `<InstallSQLDataDir>\<SQLInstanceID>\MSSQL\Data`(시스템 데이터 디렉터리)<br /><br /> 참고: 이 매개 변수는 RebuildDatabase 시나리오에도 추가됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **선택 사항**|설치 프로그램에서 추가할 tempdb 데이터 파일 수를 지정합니다. 이 값은 코어 수까지 증가할 수 있습니다. 기본값:<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 1<br /><br /> 8 또는 코어 수 중에서 모든 기타 버전의 경우 낮은 값입니다.<br /><br /> **중요:** tempdb에 대한 주 데이터베이스 파일은 여전히 tempdb.mdf입니다. 추가 tempdb 파일은 이름이 tempdb_mssql_#.ndf로 지정됩니다(여기서 #은 설치하는 동안 만들어진 각 추가 tempdb 데이터베이스 파일의 고유 개수를 나타냄). 이 명명 규칙의 목적은 고유한 파일 이름을 지정하는 것입니다. SQL Server 인스턴스를 제거하면 tempdb_mssql_#.ndf 명명 규칙을 사용하는 파일이 삭제됩니다. 사용자 데이터베이스 파일에 tempdb_mssql_\*.ndf 명명 규칙을 사용하지 마세요.<br /><br /> **경고:** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]는 이 매개 변수를 구성하는 데 지원되지 않습니다. 설치 프로그램은 1개의 tempdb 데이터 파일만 설치합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 도입되었습니다. 각 tempdb 데이터 파일의 초기 크기를 지정합니다.<br/><br/>기본값 = 8MB.<br/><br/>최솟값 = 8MB.<br/><br/>최댓값 = 1,024MB([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 262,144MB).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **선택 사항**|각 tempdb 데이터 파일의 파일 증가 증분을 MB 단위로 지정합니다. 값이 0이면 자동 증가가 해제되어 있고 추가 공간이 허용되지 않음을 나타냅니다. 설치에서는 최대 1,024MB의 크기를 허용합니다.<br /><br /> 기본값: 64<br /><br /> 허용 범위: 최소 = 0, 최대 = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **선택 사항**|tempdb 로그 파일의 초기 크기를 MB 단위로 지정합니다. 설치에서는 최대 1,024MB의 크기를 허용합니다. <br /> 기본값:<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4<br /><br /> 기타 모든 버전의 경우 8<br /><br /> 허용 범위: 최소 = 기본값(4 또는 8), 최대 = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 도입되었습니다. 각 tempdb 로그 파일의 초기 크기를 지정합니다.<br/><br/>기본값 = [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 경우 4MB, 다른 모든 버전의 경우 8MB.<br/><br/>최소 = (4MB 또는 8MB).<br/><br/>최댓값 = 1,024MB([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 262,144MB|  
  
###### <a name="sample-syntax"></a>예제 구문:  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 위한 장애 조치(Failover) 클러스터 고급 설치 시나리오의 "완료" 단계를 수행하려면 장애 조치(Failover) 클러스터의 액티브 노드가 될 컴퓨터에서 다음 명령을 실행하여 이 노드를 사용 가능한 상태로 만듭니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 장애 조치(Failover) 클러스터의 공유 디스크를 소유하는 노드에서 "CompleteFailoverCluster" 동작을 실행해야 합니다. 
  
 명령 프롬프트에서 다음 명령을 실행하여 기본 인스턴스에 대한 장애 조치(Failover) 클러스터 설치를 완료합니다.  
  
```  
setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\Username>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>:" /FAILOVERCLUSTERNETWORKNAME="<Insert FOI Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
```  
  
 명령 프롬프트에서 다음 명령을 실행하여 명명된 인스턴스에 대한 장애 조치 클러스터 설치를 완료합니다.  
  
```  
setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName="<Insert Instance Name>" /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\KATMAI\Data /ASLOGDIR=<drive>:\KATMAI\Log /ASBACKUPDIR=<Drive>:\KATMAI\Backup /ASCONFIGDIR=<Drive>:\KATMAI\Config /ASTEMPDIR=<Drive>:\KATMAI\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>" /FAILOVERCLUSTERNETWORKNAME="CompNamedFOI" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;ClusterNetwork1;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="<Insert New Group Name>" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER_KATMAI" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\Username>"  
```  
  
#### <a name="upgrade-failover-cluster-parameters"></a>장애 조치 클러스터 업그레이드 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 장애 조치(Failover) 클러스터 업그레이드 명령줄 스크립트를 개발할 수 있습니다. 자세한 내용은 [[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스 업그레이드&#40;설치&#41;](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) 및 [Always On 장애 조치(failover) 클러스터 인스턴스&#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)를 참조하세요. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|설치 워크플로를 지정하는 데 필요합니다.<br /><br /> 지원되는 값: **업그레이드**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.**|사용 조건에 대한 동의를 확인하는 데 필요합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ENU<br /><br /> **선택 사항**|설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 이 매개 변수를 사용하여 지역화된 운영 체제에 SQL Server 영어 버전을 설치할 수 있습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/*UpdateEnabled*<br /><br /> **선택 사항**|SQL Server 설치 프로그램이 제품 업데이트를 검색하고 포함하는지 여부를 지정합니다. 유효한 값은 True와 False 또는 1과 0입니다. 기본적으로 SQL Server 설치 프로그램에는 검색된 업데이트가 포함됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/*UpdateSource*<br /><br /> **선택 사항**|SQL Server 설치 프로그램이 제품 업데이트를 가져올 위치를 지정합니다. 유효한 값은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update를 검색하는 경우 “MU”, 유효한 폴더 경로, 상대 경로(예: `.\MyUpdates`) 또는 UNC 공유입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 Windows Server Update Services를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update 또는 Windows Update 서비스를 검색합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/CONFIGURATIONFILE<br /><br /> **선택 사항**|사용할 [ConfigurationFile](./install-sql-server-using-a-configuration-file.md) 을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ERRORREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. <br/><br/>Microsoft로 오류 피드백을 전송하는 방법을 관리하려면 [Microsoft에 피드백을 보내도록 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 구성하는 방법](https://support.microsoft.com/kb/3153756)을 참조하세요. <br/><br/>이전 버전에서는 SQL Server의 오류 보고를 지정합니다.<br /><br /> 자세한 내용은 [Microsoft 오류 보고 서비스에 대한 개인 정보 취급 방침](../../sql-server/sql-server-privacy.md)을 참조하십시오. 지원되는 값:<br /><br /> 0 = 사용 안 함<br /><br /> 1 = 사용|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HELP, ?<br /><br /> **선택 사항**|매개 변수에 대한 사용 옵션을 표시합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INDICATEPROGRESS<br /><br /> **선택 사항**|세부 설치 로그 파일이 콘솔로 전달되도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ INSTANCEDIR<br /><br /> **선택 사항**|공유 구성 요소에 대해 기본 디렉터리가 아닌 다른 디렉터리를 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCEID<br /><br /> **[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상에서 업그레이드하는 경우 필수입니다.**<br /><br /> **[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 업그레이드하는 경우 선택 사항**|[InstanceID](#InstanceID)에 대해 기본값이 아닌 다른 값을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> **필수**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/PID<br /><br /> **선택 사항**|SQL Server 버전의 제품 키를 지정합니다. 이 매개 변수를 지정하지 않으면 Evaluation이 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET <br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/SQMREPORTING<br /><br /> **선택 사항**|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에는 아무런 영향이 없습니다. 이전 버전에서는 SQL Server의 기능 사용 보고를 지정합니다.<br /><br />지원되는 값:<br /><br /> 0 = 사용 안 함<br /><br /> 1 = 사용|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FAILOVERCLUSTERROLLOWNERSHIP|업그레이드하는 동안 [장애 조치 동작](#RollOwnership) 을 지정합니다.|  
|SQL Server Browser 서비스|/BROWSERSVCSTARTUPTYPE<br /><br /> **선택 사항**|SQL Server Browser 서비스의 [시작](#Accounts) 모드를 지정합니다. 지원되는 값:<br /><br /> **자동**<br /><br /> **사용 안 함**<br /><br /> **수동**|  
|SQL Server 전체 텍스트|/FTUPGRADEOPTION<br /><br /> **선택 사항**|전체 텍스트 카탈로그 업그레이드 옵션을 지정합니다. 지원되는 값:<br /><br /> **REBUILD**<br /><br /> **RESET**<br /><br /> **IMPORT**|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **필수**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 계정을 지정합니다.<br /><br /> 기본값: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [필수](#Accounts)|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **선택 사항**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 [시작](#Accounts) 모드를 지정합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEDATABASEACCOUNT<br /><br /> **선택 사항**|이 속성은 2008 R2 버전 이상의 SharePoint 모드 보고서 서버를 업그레이드할 때만 사용됩니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 변경된 이전 SharePoint 모드 아키텍처를 사용하는 보고서 서버에서는 추가 업그레이드 작업이 수행됩니다. 이 옵션이 명령줄 설치에 포함되지 않은 경우 이전 보고서 서버 인스턴스의 기본 서비스 계정이 사용됩니다. 이 속성이 사용된 경우에는 **/RSUPGRADEPASSWORD** 속성을 사용해서 계정 암호를 제공하십시오.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEPASSWORD<br /><br /> **선택 사항**|기존 보고서 서버 서비스 계정 암호입니다.|  
  
####  <a name="add-node-parameters"></a><a name="AddNode"></a> 노드 추가 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 노드 추가 명령줄 스크립트를 개발할 수 있습니다. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|AddNode 워크플로를 나타내는 데 필요합니다.<br /><br /> 지원되는 값: **AddNode**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.**|사용 조건에 대한 동의를 확인하는 데 필요합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ENU<br /><br /> **선택 사항**|설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 이 매개 변수를 사용하여 지역화된 운영 체제에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 영어 버전을 설치할 수 있습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/*UpdateEnabled*<br /><br /> **선택 사항**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 제품 업데이트를 검색하고 포함하는지 여부를 지정합니다. 유효한 값은 True와 False 또는 1과 0입니다. 기본적으로 SQL Server 설치 프로그램에는 검색된 업데이트가 포함됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/*UpdateSource*<br /><br /> **선택 사항**|SQL Server 설치 프로그램이 제품 업데이트를 가져올 위치를 지정합니다. 유효한 값은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update를 검색하는 경우 “MU”, 유효한 폴더 경로, 상대 경로(예: `.\MyUpdates`) 또는 UNC 공유입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 Windows Server Update Services를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update 또는 Windows Update 서비스를 검색합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/CONFIGURATIONFILE<br /><br /> **선택 사항**|사용할 [ConfigurationFile](./install-sql-server-using-a-configuration-file.md) 을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HELP, ?<br /><br /> **선택 사항**|매개 변수에 대한 사용 옵션을 표시합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INDICATEPROGRESS<br /><br /> **선택 사항**|세부 설치 로그 파일이 콘솔로 전달되도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> **필수**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **선택 사항**|엔진 서비스의 계정을 지정합니다. 기본값은 **NT Authority\NETWORK SERVICE** 입니다.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **선택 사항**|엔진 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **선택 사항**|PolyBase 엔진 서비스의 시작 모드를 지정합니다. Automatic(기본값), Disabled 및 Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **선택 사항**|PolyBase 서비스용 6개 이상의 포트로 포트 범위를 지정합니다. 예제:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **선택 사항**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스가 PolyBase 규모 확장 계산 그룹의 일부로 사용될지를 지정합니다. 지원되는 값: **True**, **False**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/PID<br /><br /> **선택 사항**|SQL Server 버전의 제품 키를 지정합니다. 이 매개 변수를 지정하지 않으면 Evaluation이 사용됩니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET <br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다. /Q 매개 변수는 /QS 매개 변수의 입력을 재정의합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/QS 또는 /QUIETSIMPLE <br /><br /> **선택 사항**|설치 프로그램이 UI를 통해 실행되고 진행률을 표시하지만 입력을 받거나 오류 메시지를 표시하지 않도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **필수**|인코딩된 IP 주소를 지정합니다. 인코딩은 세미콜론(;)으로 구분되며 \<IP Type>;\<address>;\<network name>;\<subnet mask> 형식을 따릅니다. 지원되는 IP 유형에는 DHCP, IPv4 및 IPv6이 있습니다.<br />주소 사이에 공백을 넣어 여러 장애 조치(failover) 클러스터 IP 주소를 지정할 수 있습니다. 다음 예제를 참조하세요.<br /><br /> `FAILOVERCLUSTERIPADDRESSES=DEFAULT`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1`<br /><br /> `FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1`<br /><br /> <br /><br /> 자세한 내용은 [[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)을 참조하세요.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/CONFIRMIPDEPENDENCYCHANGE<br /><br /> **필수**|다중 서브넷 장애 조치(Failover) 클러스터의 IP 주소 리소스 종속성을 OR로 설정하는 데 대한 동의를 나타냅니다. 자세한 내용은 [[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)을 참조하세요. 지원되는 값:<br /><br /> 0 = False(기본값)<br /><br /> 1 = True|  
|SQL Server 에이전트|/AGTSVCACCOUNT<br /><br /> **필수**|SQL Server 에이전트 서비스의 계정을 지정합니다.|  
|SQL Server 에이전트|/AGTSVCPASSWORD<br /><br /> [필수](#Accounts)|SQL Server 에이전트 서비스 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **필수**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스 계정을 지정합니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [필수](#Accounts)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **필수**|SQL Server 서비스의 시작 계정을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [필수](#Accounts)|SQLSVCACCOUNT의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [필수](#Accounts)|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **파일만 모드에서 사용 가능**| SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 설치 모드를 지정합니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [필수](#Accounts)|SQL Server 2017부터 더 이상 적용할 수 없습니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 시작 계정의 암호를 지정합니다. 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때는 이 매개 변수를 생략할 수 있습니다.|  
  
##### <a name="additional-notes"></a>참고 사항:  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 클러스터를 인식하는 유일한 구성 요소입니다. 기타 기능은 클러스터를 인식하지 않으므로 장애 조치(Failover)에서 가용성이 높지 않습니다. 
  
###### <a name="sample-syntax"></a>예제 구문:  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]와 함께 기존 장애 조치(Failover) 클러스터 인스턴스에 노드를 추가합니다. 
  
```  
setup.exe /q /ACTION=AddNode /INSTANCENAME="<Insert Instance Name>" /SQLSVCACCOUNT="<SQL account that is used on other nodes>" /SQLSVCPASSWORD="<password for SQL account>" /AGTSVCACCOUNT="<SQL Server Agent account that is used on other nodes>", /AGTSVCPASSWORD="<SQL Server Agent account password>" /ASSVCACCOUNT="<AS account that is used on other nodes>" /ASSVCPASSWORD="<password for AS account>" /INDICATEPROGRESS /IACCEPTSQLSERVERLICENSETERMS /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;ClusterNetwork1;xxx.xxx.xxx.x" /CONFIRMIPDEPENDENCYCHANGE=0  
```  
  
#### <a name="remove-node-parameters"></a>노드 제거 매개 변수  
 다음 표에 나와 있는 매개 변수를 사용하여 노드 제거 명령줄 스크립트를 개발할 수 있습니다. 장애 조치(Failover) 클러스터를 제거하려면 각 장애 조치(Failover) 클러스터 노드에서 RemoveNode를 실행해야 합니다. 자세한 내용은 [Always On 장애 조치(failover) 클러스터 인스턴스&#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)를 참조하세요. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|매개 변수|Description|  
|-----------------------------------------|---------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/ACTION<br /><br /> **필수**|RemoveNode 워크플로를 나타내는 데 필요합니다.<br /><br /> 지원되는 값: **RemoveNode**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/CONFIGURATIONFILE<br /><br /> **선택 사항**|사용할 [ConfigurationFile](./install-sql-server-using-a-configuration-file.md) 을 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HELP, ?<br /><br /> **선택 사항**|매개 변수에 대한 사용 옵션을 표시합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INDICATEPROGRESS<br /><br /> **선택 사항**|세부 설치 로그 파일이 콘솔로 전달되도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/INSTANCENAME<br /><br /> **필수**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스 이름을 지정합니다.<br /><br /> 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/Q 또는 /QUIET <br /><br /> **선택 사항**|설치 프로그램이 사용자 인터페이스 없이 자동 모드에서 실행되도록 지정합니다. 이 옵션은 무인 설치에 사용됩니다. /Q 매개 변수는 /QS 매개 변수의 입력을 재정의합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/QS 또는 /QUIETSIMPLE<br /><br /> **선택 사항**|설치 프로그램이 UI를 통해 실행되고 진행률을 표시하지만 입력을 받거나 오류 메시지를 표시하지 않도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/HIDECONSOLE<br /><br /> **선택 사항**|콘솔 창을 숨기거나 닫도록 지정합니다.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치 컨트롤|/CONFIRMIPDEPENDENCYCHANGE<br /><br /> **필수**|다중 서브넷 장애 조치(Failover) 클러스터의 IP 주소 리소스 종속성을 OR에서 AND로 설정하는 데 대한 동의를 나타냅니다. 자세한 내용은 [[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)을 참조하세요. 지원되는 값:<br /><br /> 0 = False(기본값)<br /><br /> 1 = True|  
  
###### <a name="sample-syntax"></a>예제 구문:  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]와 함께 기존 장애 조치(Failover) 클러스터 인스턴스에서 노드를 제거합니다. 
  
```  
setup.exe /q /ACTION=RemoveNode /INSTANCENAME="<Insert Instance Name>" [/INDICATEPROGRESS] /CONFIRMIPDEPENDENCYCHANGE=0  
```  
  
##  <a name="service-account-parameters"></a><a name="Accounts"></a> 서비스 계정 매개 변수  
 기본 제공 계정, 로컬 계정 또는 도메인 계정을 사용하여 SQL Server 서비스를 구성할 수 있습니다. 
  
> [!NOTE] 
> 관리 서비스 계정, 가상 계정 또는 기본 제공 계정을 사용할 때 해당 암호 매개 변수를 지정하면 안 됩니다. 이러한 서비스 계정에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)의 **[!INCLUDE[win7](../../includes/win7-md.md)] 및 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]에 사용할 수 있는 새 계정 유형** 섹션을 참조하세요. 
  
 서비스 계정에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요. 
  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 요소|계정 매개 변수|암호 매개 변수|시작 유형|  
|-----------------------------------------|-----------------------|------------------------|------------------|  
|SQL Server 에이전트|/AGTSVCACCOUNT|/AGTSVCPASSWORD|/AGTSVCSTARTUPTYPE|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT|/ASSVCPASSWORD|/ASSVCSTARTUPTYPE|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT|/SQLSVCPASSWORD|/SQLSVCSTARTUPTYPE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT|/ISSVCPASSWORD|/ISSVCSTARTUPTYPE|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT|/RSSVCPASSWORD|/RSSVCSTARTUPTYPE|  
  
  > [!NOTE]
  > 보고서 서비스 기능은 SQL Server 2017에서 제거되었습니다. SQL Server Reporting Services의 계정 매개 변수는 SQL Server 2017 이전 버전에만 적용됩니다. 


##  <a name="feature-parameters"></a><a name="Feature"></a> 기능 매개 변수  
 특정 기능을 설치하려면 /FEATURES 매개 변수를 사용하여 다음 표에 나와 있는 부모 기능 또는 기능 값을 지정하십시오. SQL Server 버전에서 지원되는 기능 목록은 [[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 버전 및 지원되는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요. 
  
|부모 기능 매개 변수|기능 매개 변수|Description|  
|:---|:---|:---|  
|SQL||[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Replication, Fulltext 및 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]를 설치합니다.|  
||SQLEngine|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]만 설치합니다.|  
||복제|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]과 함께 복제 구성 요소를 설치합니다.|  
||FullText|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]과 함께 전체 텍스트 구성 요소를 설치합니다.|  
||DQ|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 설치를 완료하는 데 필요한 파일을 복사합니다. SQL Server 설치를 완료한 후에는 DQSInstaller.exe 파일을 실행하여 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 설치를 완료해야 합니다. 자세한 내용은 [DQSInstaller.exe를 실행하여 Data Quality 서버 설치 완료](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)를 참조하세요. 또한 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]도 설치합니다.|  
||PolyBase |PolyBase 구성 요소를 설치합니다.|
||PolyBaseCore | SQL Server 2019부터 **PolyBase** 와 연결하여 표준 T-SQL 문을 사용하는 Oracle, Teradata, SQL Server 및 기타 관계형 및 비관계형 데이터에 걸쳐 진정한 통합 쿼리를 수행하도록 해주는 Polybase 기술을 설치합니다. |
|| PolyBaseJava | SQL Server 2019부터 **PolyBase** 와 연결하여 표준 T-SQL 문을 사용하는 HDFS 데이터에 걸쳐 진정한 통합 쿼리를 수행하도록 해주는 PolyBase Java 커넥터를 설치합니다.
||AdvancedAnalytics |[SQL Server Machine Learning Services](../../machine-learning/install/sql-machine-learning-services-windows-install.md) 또는 [SQL Server 2016 R Services(데이터베이스 내)](../../machine-learning/install/sql-r-services-windows-install.md)를 설치합니다.|  
||SQL_INST_MR |[SQL Server Machine Learning Services](../../machine-learning/install/sql-machine-learning-services-windows-install.md)에 적용됩니다. **AdvancedAnalytics** 와 쌍으로 R Open 및 전용 R 패키지를 설치합니다.|  
||SQL_INST_MPY|[SQL Server Machine Learning Services](../../machine-learning/install/sql-machine-learning-services-windows-install.md)에 적용됩니다. **AdvancedAnalytics** 와 쌍으로 Anaconda 및 전용 Python 패키지를 설치합니다.|  
||SQL_INST_JAVA |[SQL Server Machine Learning Services](../../machine-learning/install/sql-machine-learning-services-windows-install.md)에 적용됩니다. 표준 T-SQL 문을 사용하여 Java와 통합할 수 있도록 하는 확장을 설치하려면 **AdvancedAnalytics** 와 연결합니다.|  
|AS||모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 요소를 설치합니다.|  
|RS||모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소를 설치합니다. SQL Server 2017부터 제거되었습니다. |  
|RS_SHP||SharePoint용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소를 설치합니다. SQL Server 2017부터 제거되었습니다.|  
|RS_SHPWFE||SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치합니다. SQL Server 2017부터 제거되었습니다. |  
|DQC||[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]를 설치합니다.|  
|IS||모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소를 설치합니다.|  
||IS_Master|Integration Services 규모 확장을 위한 규모 확장 마스터가 포함됩니다.| 
||IS_Worker|Integration Services 규모 확장을 위한 규모 확장 마스터가 포함됩니다.| 
|MDS||[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]를 설치합니다.|  
|SQL_SHARED_MPY||[SQL Server 2017 Machine Learning 서버(독립 실행형)](../../machine-learning/install/sql-machine-learning-standalone-windows-install.md)용 Python 패키지 설치 |  
|SQL_SHARED_MR||[SQL Server 2016 R Server(독립 실행형)](../../machine-learning/install/sql-machine-learning-standalone-windows-install.md) 또는 [SQL Server Machine Learning 서버(독립 실행형)](../../machine-learning/install/sql-machine-learning-standalone-windows-install.md)용 R 패키지를 설치합니다. |  
|Tools*||클라이언트 도구와 SQL Server 온라인 설명서 구성 요소를 설치합니다.|  
||BC|이전 버전과의 호환성 구성 요소를 설치합니다.|  
||Conn|연결 구성 요소를 설치합니다.|
||DREPLAY_CTLR|Distributed Replay Controller 설치|  
||DREPLAY_CLT|Distributed Replay 클라이언트 설치|  
||SNAC_SDK|[!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server Native Client용 SDK 설치|  
||SDK)|소프트웨어 개발 키트를 설치합니다.|  
||LocalDB**|프로그램 개발자를 대상으로 하는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 의 실행 모드인 LocalDB를 설치합니다.|  

*SSMS([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)])은 이제 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 관리자와 별도인 독립 실행형 설치 관리자에 제공됩니다. 자세한 내용은 [SQL Server Management Studio 설치](../../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.

### <a name="feature-parameter-examples"></a>기능 매개 변수 예:
  
|매개 변수 및 값|Description| 
|---------------|-----------------|  
|/FEATURES=SQLEngine|복제 및 전체 텍스트 없이 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 설치합니다.|  
|/FEATURES=SQLEngine,FullText|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 전체 텍스트를 설치합니다.|  
|/FEATURES=SQL,Tools|전체 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 도구를 모두 설치합니다.|  
|/FEATURES=BOL|도움말 내용을 보고 관리할 수 있도록 SQL Server 온라인 설명서 구성 요소를 설치합니다.|  
|/FEATURES=SQLEngine,PolyBase|PolyBase 엔진을 설치합니다.|  
  
##  <a name="role-parameters"></a><a name="RoleParameters"></a> 역할 매개 변수

설치 역할 또는 /Role 매개 변수는 미리 구성된 기능 선택 항목을 설치하는 데 사용됩니다. SSAS 역할은 기존 SharePoint 팜이나 구성되지 않은 새 팜에 SSAS 인스턴스를 설치합니다. 각 시나리오를 지원하는 두 가지 설치 역할이 제공됩니다. 설치할 설치 역할은 한 번에 하나씩만 선택할 수 있습니다. 설치 역할을 선택하면 설치 프로그램에서 해당 역할에 속하는 기능 및 구성 요소를 설치합니다. 특정 역할에 지정된 기능과 구성 요소를 변경할 수는 없습니다. 기능 역할 매개 변수를 사용하는 방법에 대한 자세한 내용은 [명령 프롬프트에서 PowerPivot 설치](/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)를 참조하세요.

AllFeatures_WithDefaults 역할은 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 버전의 기본 동작으로, 사용자에게 표시되는 대화 상자 수를 줄입니다. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]이외의 SQL Server 버전을 설치할 때는 이 역할을 명령줄에서 지정할 수 있습니다.

|역할|Description|설치합니다...|  
|----------|-----------------|---------------|  
|SPI_AS_ExistingFarm|기존 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 팜 또는 독립 실행형 서버에 명명된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 인스턴스로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 설치합니다.|메모리 내 데이터 스토리지 및 처리를 위해 미리 구성된[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 계산 엔진<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 솔루션 패키지<br /><br /> [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]용 설치 관리자 프로그램<br /><br /> SQL Server 온라인 설명서|  
|SPI_AS_NewFarm|구성되지 않은 새 Office [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 팜 또는 독립 실행형 서버에 명명된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 인스턴스로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)]를 설치합니다. SQL Server 설치 프로그램은 기능 역할 설치 중에 팜을 구성합니다.|메모리 내 데이터 스토리지 및 처리를 위해 미리 구성된[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 계산 엔진<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 솔루션 패키지<br /><br /> SQL Server 온라인 설명서<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)]<br /><br /> 구성 도구<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|AllFeatures_WithDefaults|현재 버전에서 사용할 수 있는 모든 기능을 설치합니다.<br /><br /> 현재 사용자를 SQL Server **sysadmin** 고정 서버 역할에 추가합니다.<br /><br /> [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 이상을 사용하고 운영 체제가 도메인 컨트롤러가 아닌 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 기본적으로 NTAUTHORITY\NETWORK SERVICE 계정을 사용하고, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 기본적으로 NTAUTHORITY\NETWORK SERVICE 계정을 사용합니다.<br /><br /> [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 버전에서는 이러한 역할이 기본적으로 사용하도록 설정됩니다. 기타 모든 버전의 경우 이 역할은 사용하도록 설정되지 않지만 UI나 명령줄 매개 변수를 통해 지정할 수 있습니다.|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 버전의 경우에는 해당 버전에서 사용 가능한 기능만 설치하세요. 기타 버전의 경우에는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 설치하십시오.<br /><br /> **AllFeatures_WithDefaults** 매개 변수는 **AllFeatures_WithDefaults** 매개 변수 설정을 재정의하는 다른 매개 변수와 결합해 사용할 수 있습니다. 예를 들어 **AllFeatures_WithDefaults** 매개 변수와 **/Features=RS** 매개 변수를 함께 사용하면 모든 기능을 설치하는 명령이 무시되고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]만 설치되지만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대해 기본 서비스 계정을 사용하는 **AllFeatures_WithDefaults** 매개 변수 설정은 그대로 적용됩니다.<br /><br /> **AllFeatures_WithDefaults** 매개 변수를 **/ADDCURRENTUSERASSQLADMIN=FALSE** 와 함께 사용하는 경우에는 프로비전 대화 상자에 현재 사용자가 자동으로 채워지지 않습니다. SQL Server 에이전트에 대한 서비스 계정과 암호를 지정하려면 **/AGTSVCACCOUNT** 및 **/AGTSVCPASSWORD** 를 추가하세요.|

## <a name="controlling-failover-behavior-using-the-failoverclusterrollownership-parameter"></a><a name="RollOwnership"></a> /FAILOVERCLUSTERROLLOWNERSHIP 매개 변수를 사용하여 장애 조치 동작 제어  
[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 장애 조치(failover) 클러스터를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하려면 패시브 노드부터 시작하여 한 번에 하나의 장애 조치(failover) 클러스터 노드에서 설치 프로그램을 실행해야 합니다. 설치 프로그램에서는 장애 조치(Failover) 클러스터 인스턴스의 총 노드 수 및 이미 업그레이드된 노드 수에 따라 업그레이드된 노드로 장애 조치(Failover)를 실행할 시기를 결정합니다. 절반 이상의 노드가 이미 업그레이드된 경우 기본적으로 설치 프로그램에서는 업그레이드된 노드로 장애 조치(Failover)를 실행합니다.

업그레이드 프로세스를 진행하는 동안 클러스터 노드의 장애 조치(Failover) 동작을 제어하려면 명령 프롬프트에서 업그레이드 작업을 실행한 다음, 업그레이드 작업을 통해 노드가 오프라인으로 전환되기 전에 /FAILOVERCLUSTERROLLOWNERSHIP 매개 변수를 사용하여 장애 조치(Failover) 동작을 제어하십시오. 이 매개 변수의 사용 방법은 다음과 같습니다.

- /FAILOVERCLUSTERROLLOWNERSHIP=0은 클러스터 소유권(그룹 이동)을 업그레이드된 노드에 넘겨 주지 않으며 업그레이드 종료 시 가능한 SQL Server 클러스터 소유자 목록에 이 노드를 추가하지 않습니다. 

- /FAILOVERCLUSTERROLLOWNERSHIP=1은 클러스터 소유권(그룹 이동)을 업그레이드된 노드에 넘겨 주며 업그레이드 종료 시 가능한 SQL Server 클러스터 소유자 목록에 이 노드를 추가합니다. 

- /FAILOVERCLUSTERROLLOWNERSHIP=2는 기본 설정입니다. 매개 변수가 지정되지 않은 경우 이 값이 사용됩니다. 이 설정은 SQL Server 설치 프로그램이 필요에 따라 클러스터 소유권(그룹 이동)을 관리함을 나타냅니다. 

##  <a name="instance-id-or-instanceid-configuration"></a><a name="InstanceID"></a> Instance ID 또는 InstanceID 구성

Instance ID 또는 /InstanceID 매개 변수는 인스턴스 구성 요소를 설치할 수 있는 위치와 인스턴스의 레지스트리 경로를 지정하는 데 사용됩니다. INSTANCEID의 값은 고유한 문자열이어야 합니다. 

- SQL 인스턴스 ID: `MSSQLxx.<INSTANCEID>`

- AS 인스턴스 ID: `MSASxx.<INSTANCEID>`

- RS 인스턴스 ID: `MSRSxx.<INSTANCEID>`

인스턴스 인식형 구성 요소는 다음 위치에 설치됩니다.  

`%Program Files%\Microsoft SQL Server\<SQLInstanceID>`

`%Program Files%\Microsoft SQL Server\<ASInstanceID>`

`%Program Files%\Microsoft SQL Server\<RSInstanceID>`

> [!NOTE]
> INSTANCEID가 명령줄에 지정되지 않은 경우 기본적으로 설치 프로그램에서 \<INSTANCEID>를 \<INSTANCENAME>으로 대체합니다. 

## <a name="see-also"></a>참고 항목
- [설치 마법사에서 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [SQL Server 장애 조치(Failover) 클러스터 설치](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)
- [SQL Server 2016 비즈니스 인텔리전스 기능 설치](../../sql-server/install/install-sql-server-business-intelligence-features.md)
