---
title: "rsconfig 유틸리티 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [Reporting Services], configuring
- rsconfig utility
- report servers [Reporting Services], connections
- command prompt utilities [Reporting Services]
- command prompt utilities [SQL Server], rsconfig
ms.assetid: 84e45a2f-3ca6-4c16-8259-c15ff49d72ad
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68b5e38f2b4e71298fbf7b6ec6970fc7824c3cde
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="rsconfig-utility-ssrs"></a>rsconfig 유틸리티(SSRS)
  **rsconfig.exe** 유틸리티는 연결 및 계정 값을 암호화하여 RSReportServer.config 파일에 저장합니다. 암호화되는 값에는 무인 보고서 처리에 사용되는 보고서 서버 데이터베이스 연결 정보 및 계정 값이 포함됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
rsconfig {-?}  
{–cconnection}  
{–eunattendedaccount}  
{–mcomputername}  
{–iinstancename}  
{–sservername}  
{–ddatabasename}  
{–aauthmethod}  
{-uusername}  
{-ppassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>인수  
  
|용어|선택/필수|정의|  
|----------|------------------------|----------------|  
|**-?**|(선택 사항)|Rsconfig.exe 인수의 구문을 표시합니다.|  
|**-c**|**-e** 인수를 사용하지 않는 경우 필요합니다.|보고서 서버에서 보고서 서버 데이터베이스에 연결하는 데 사용되는 연결 문자열, 자격 증명 및 데이터 원본 값을 지정합니다.<br /><br /> 이 인수는 값을 가지지 않습니다. 그러나 모든 필수 연결 값을 제공하려면 이 인수와 함께 추가 인수를 지정해야 합니다.<br /><br /> **-c** 를 사용하여 지정할 수 있는 인수에는 **-m**, **-s**, **-i**,**-d**,**-a**,**-u**,**-p**및**-t**가 있습니다.|  
|**-e**|**-c** 인수를 사용하지 않는 경우 필요합니다.|무인 보고서 실행 계정을 지정합니다.<br /><br /> 이 인수는 값을 가지지 않습니다. 그러나 구성 파일에 암호화된 값을 지정하려면 명령줄에 추가 인수를 포함해야 합니다.<br /><br /> **-e** 를 사용하여 지정할 수 있는 인수에는 **-u** 및 **-p**가 있습니다. **-t**도 설정할 수 있습니다.|  
|**-m**  *computername*|원격 보고서 서버 인스턴스를 구성하는 경우 필요합니다.|보고서 서버를 호스팅하는 컴퓨터의 이름입니다. 이 인수를 생략할 경우 기본값은 **localhost**입니다.|  
|**-s**  *servername*|필수 사항입니다.|보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정합니다.|  
|**-i**  *instancename*|명명된 인스턴스를 사용하는 경우 필요합니다.|명명된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 사용하여 보고서 서버 데이터베이스를 호스팅하는 경우 이 값은 명명된 인스턴스를 지정합니다.|  
|**-d**  *databasename*|필수 사항입니다.|보고서 서버 데이터베이스의 이름을 지정합니다.|  
|**-a**  *authmethod*|필수 사항입니다.|보고서 서버에서 보고서 서버 데이터베이스에 연결할 때 사용하는 인증 방법을 지정합니다. 유효한 값은 **Windows** 또는 **SQL** 입니다. 이 인수는 대/소문자를 구분하지 않습니다.<br /><br /> **Windows** 에서는 보고서 서버가 Windows 인증을 사용하도록 지정합니다.<br /><br /> **SQL** 에서는 보고서 서버가 SQL Server 인증을 사용하도록 지정합니다.|  
|**-u***[도메인\\] 사용자 이름* |**-e** 에서는 필수이고, **-c**에서는 옵션입니다.|보고서 서버 데이터베이스 연결 또는 무인 계정을 위한 사용자 계정을 지정합니다.<br /><br /> **rsconfig -e**의 경우 이 인수는 필수입니다. 도메인 사용자 계정이어야 합니다.<br /><br /> **rsconfig -c** 및 **-a SQL**의 경우 이 인수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정해야 합니다.<br /><br /> **rsconfig -c** 및 **-a Windows**의 경우 이 인수는 도메인 사용자, 기본 제공 계정 또는 서비스 계정 자격 증명을 지정할 수 있습니다. 도메인 계정을 지정하는 경우 *domain* 및 *username* 을 *domain\username*형식으로 지정합니다. 기본 제공 계정을 사용하는 경우 이 인수는 선택 인수입니다. 서비스 계정 자격 증명을 사용하려면 이 인수를 생략합니다.|  
|**-p**  *password*|**-u** 를 지정하는 경우 필수입니다.|*username* 인수와 함께 사용할 암호를 지정합니다. 계정에 암호가 필요하지 않은 경우에는 이 인수를 비워 둘 수 있습니다. 도메인 계정의 경우 이 값은 대/소문자를 구분합니다.|  
|**-t**|(선택 사항)|추적 로그에 오류 메시지를 출력합니다. 이 인수는 값을 가지지 않습니다. 자세한 내용은 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)을 참조하세요.|  
  
## <a name="permissions"></a>Permissions  
 구성 중인 보고서 서버를 호스팅하는 컴퓨터에 로컬 관리자 권한이 있어야 합니다.  
  
## <a name="file-location"></a>파일 위치  
 Rsconfig.exe는 **\Program Files\Microsoft SQL Server\110\Tools\Binn**에 있습니다. 파일 시스템의 모든 폴더에서 유틸리티를 실행할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 Rsconfig.exe는 다음 두 가지 목적으로 사용됩니다.  
  
-   보고서 서버에서 보고서 서버 데이터베이스에 연결하는 데 사용하는 연결 정보를 수정하려는 경우  
  
-   다른 자격 증명을 사용할 수 없을 때 보고서 서버에서 원격 데이터베이스 서버에 로그온하는 데 사용하는 특수 계정을 구성하려는 경우  
  
 **의 로컬 또는 원격 인스턴스에서** rsconfig [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]유틸리티를 실행할 수 있습니다. 이미 설정된 값을 해독하고 보는 데 **rsconfig** 유틸리티를 사용할 수 없습니다.  
  
 이 유틸리티를 실행하려면 구성 중인 컴퓨터에 WMI(Windows Management Instrumentation)가 설치되어 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **rsconfig**를 사용하는 방법을 보여 줍니다.  
  
#### <a name="specifying-a-domain-user-account"></a>도메인 사용자 계정 지정  
 이 예에서는 로컬 보고서 서버 데이터베이스에 연결할 때 도메인 사용자 계정을 사용하도록 보고서 서버를 구성하는 방법을 보여 줍니다.  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows -u <MYDOMAIN\MYACCOUNT> -p <PASSWORD>  
```  
  
#### <a name="specifying-a-sql-server-database-user-account"></a>SQL Server 데이터베이스 사용자 계정 지정  
 이 예에서는 원격 보고서 서버 데이터베이스에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하도록 보고서 서버를 구성하는 방법을 보여 줍니다.  
  
```  
rsconfig -c -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -d reportserver -a SQL -u SA -p <SAPASSWORD>  
```  
  
#### <a name="specifying-a-built-in-account"></a>기본 제공 계정 지정  
 이 예에서는 로컬 보고서 서버 데이터베이스에 연결할 때 기본 제공 계정을 사용하도록 보고서 서버를 구성하는 방법을 보여 줍니다. **-u** 는 사용되지 않습니다. 지원되는 기본 제공 계정 값의 예로는 로컬 시스템의 경우 NT AUTHORITY\SYSTEM, 네트워크 서비스의 경우 NT AUTHORITY\NETWORKSERVICE 등이 있습니다([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 만 해당).  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows "NT AUTHORITY\SYSTEM"  
```  
  
#### <a name="specifying-a-service-account"></a>서비스 계정 지정  
 이 예에서는 로컬 보고서 서버 데이터베이스에 연결할 때 보고서 서버 Windows 서비스 계정 및 웹 서비스 계정을 사용하도록 보고서 서버를 구성하는 방법을 보여 줍니다. **-u** 는 사용되지 않으며 계정 정보를 지정하지 않습니다. 명령에서 계정 값을 제거하는 경우 **rsconfig** 유틸리티는 각 서비스를 실행하는 통합된 보안 및 서비스 계정을 사용합니다.  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows  
```  
  
#### <a name="specifying-the-unattended-account-on-a-local-server"></a>로컬 서버에서 무인 계정 지정  
 이 예에서는 외부 데이터 원본으로 자격 증명을 전달하지 않는 보고서의 무인 보고서 실행에 사용되는 계정을 구성하는 방법을 보여 줍니다. 이 계정은 Windows 도메인 계정이어야 합니다. 사용자 이름 및 암호에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정할 수 없습니다. 이 계정은 로컬 보고서 서버 인스턴스에서 구성됩니다. ReportingServices\LogFiles 폴더의 추적 로그에 오류 메시지가 캡처됩니다.  
  
```  
rsconfig -e -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
#### <a name="specifying-the-unattended-account-on-a-remote-server"></a>원격 서버에서 무인 계정 지정  
 이 예에서는 Rsconfig.exe와 같은 버전의 원격 보고서 서버 인스턴스에서 계정을 구성하는 방법을 보여 줍니다(예: 보고서 서버와 Rsconfig.exe가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 R2 버전인 경우). 원격 서버의 추적 로그에 오류 메시지 정보가 캡처됩니다.  
  
```  
rsconfig -e -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 서버 데이터베이스 연결 &#40; 구성 합니다. SSRS 구성 관리자 &#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [무인된 실행 계정을 &#40; 구성 합니다. SSRS 구성 관리자 &#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [Reporting Services 보고서 서버 &#40; 기본 모드 &#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [저장소 암호화 된 보고서 서버 데이터 &#40; SSRS 구성 관리자 &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services 구성 파일](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [보고서 서버 명령 프롬프트 유틸리티 &#40; Ssrs&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)   
 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
