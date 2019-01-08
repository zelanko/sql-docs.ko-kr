---
title: 보고서 서버에서 Windows 인증 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [Reporting Services]
- Reporting Services, configuration
ms.assetid: 4de9c3dd-0ee7-49b3-88bb-209465ca9d86
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6e2359a87dab19356f87574f9444962b5440c71b
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359257"
---
# <a name="configure-windows-authentication-on-the-report-server"></a>보고서 서버의 Windows 인증 구성
  기본적으로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 Negotiate 또는 NTLM 인증을 지정하는 요청을 허용합니다. 배포에 이러한 보안 공급자를 사용하는 클라이언트 애플리케이션 및 브라우저가 포함된 경우 추가 구성 없이 기본값을 사용할 수 있습니다. Windows 통합 보안을 위해 다른 보안 공급자를 사용하거나(예: Kerberos를 직접 사용하려는 경우) 기본값을 수정하고 원래 설정을 복원하려는 경우 이 항목의 정보를 사용하여 보고서 서버에서 인증 설정을 지정할 수 있습니다.  
  
 Windows 통합 보안을 사용하려면 보고서 서버에 액세스해야 하는 각 사용자가 유효한 Windows 로컬 또는 도메인 사용자 계정을 보유하고 있거나 Windows 로컬 또는 도메인 그룹 계정의 멤버여야 합니다. 트러스트된 도메인에 한하여 다른 도메인의 계정을 포함할 수 있습니다. 이 계정은 보고서 서버 컴퓨터에 액세스할 수 있어야 하며 이후에 특정 보고서 서버 작업에 액세스할 수 있도록 역할에 할당되어야 합니다.  
  
 다음의 추가 요구 사항도 만족해야 합니다.  
  
-   RSeportServer.config 파일에서 `AuthenticationType`을 `RSWindowsNegotiate`, `RSWindowsKerberos` 또는 `RSWindowsNTLM`으로 설정해야 합니다. 기본적으로 보고서 서버 서비스 계정이 NetworkService 또는 LocalSystem인 경우 RSReportServer.config 파일에는 `RSWindowsNegotiate` 설정이 들어 있습니다. 그렇지 않으면 `RSWindowsNTLM` 설정이 사용됩니다. Kerberos 인증만 사용하는 응용 프로그램이 있는 경우 `RSWindowsKerberos`를 추가할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  `RSWindowsNegotiate`를 사용할 경우 보고서 서버 서비스가 도메인 사용자 계정으로 실행되도록 구성하고 해당 계정의 SPN(서비스 사용자 이름)을 등록하지 않으면 Kerberos 인증 오류가 발생합니다. 자세한 내용은 이 항목의 [보고서 서버에 연결할 때 Kerberos 인증 오류 해결](#proxyfirewallRSWindowsNegotiate) 을 참조하십시오.  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 에는 Windows 인증을 구성해야 합니다. 보고서 서버 웹 서비스 및 보고서 관리자 Web.config 파일에는 기본적으로 포함 합니다 \<mode = "Windows" > 설정 합니다. 이를 \<authentication mode="Forms">로 변경하는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대한 Windows 인증이 실패합니다.  
  
-   보고서 서버 웹 서비스에 대 한 Web.config 파일 및 보고서 관리자 있어야 \<impersonate = "true" / >입니다.  
  
-   클라이언트 애플리케이션 또는 브라우저에서 Windows 통합 보안을 지원해야 합니다.  
  
 보고서 서버 인증 설정을 변경하려면 RSReportServer.config 파일에서 XML 요소 및 값을 편집합니다. 이 항목의 예를 복사하고 붙여 넣어 특정 조합을 구현할 수 있습니다.  
  
 모든 클라이언트 및 서버 컴퓨터가 동일한 도메인 또는 트러스트된 도메인에 있고 회사 방화벽을 통해 인트라넷으로 액세스되도록 보고서 서버가 배포된 경우 기본 설정이 가장 적합합니다. Windows 자격 증명을 전달하려면 트러스트된 단일 도메인이 필요합니다. 서버에 대해 Kerberos 버전 5 프로토콜을 사용하는 경우 자격 증명을 두 번 이상 전달할 수 있습니다. 그렇지 않으면 만료 전까지 자격 증명을 한 번만 전달할 수 있습니다. 여러 컴퓨터 연결에 대해 자격 증명을 구성하는 방법에 대한 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)을 참조하세요.  
  
 다음은 기본 모드 보고서 서버에 대한 지침입니다. 보고서 서버가 SharePoint 통합 모드로 배포된 경우 Windows 통합 보안을 지정하는 기본 인증 설정을 사용해야 합니다. 보고서 서버는 기본 Windows 인증 확장 프로그램의 내부 기능을 사용하여 SharePoint 통합 모드의 보고서 서버를 지원합니다.  
  
## <a name="extended-protection-for-authentication"></a>인증에 대한 확장된 보호  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]부터는 인증에 대한 확장된 보호가 지원됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능은 채널 바인딩 및 서비스 바인딩을 사용해 인증 보호를 향상시킬 수 있도록 지원합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능은 확장된 보호를 지원하는 운영 체제에서 사용해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성은 RSReportServer.config 파일의 설정에 의해 결정됩니다. 이 파일은 WMI API를 사용하거나 파일을 편집하여 업데이트할 수 있습니다. 자세한 내용은 [Extended Protection for Authentication with Reporting Services](extended-protection-for-authentication-with-reporting-services.md)을(를) 참조하세요.  
  
### <a name="to-configure-a-report-server-to-use-windows-integrated-security"></a>Windows 통합 보안을 사용하도록 보고서 서버를 구성하려면  
  
1.  텍스트 편집기에서 RSReportServer.config를 엽니다.  
  
2.  <`Authentication`>을(를) 찾습니다.  
  
3.  다음 중 필요에 가장 맞는 XML 구조를 복사합니다. `RSWindowsNegotiate`, `RSWindowsNTLM` 및 `RSWindowsKerberos`를 순서에 상관없이 지정할 수 있습니다. 각 개별 요청이 아닌 연결을 인증하려는 경우 인증 지속성을 사용해야 합니다. 인증 지속성을 사용하면 인증이 필요한 모든 요청이 연결 기간 동안 허용됩니다.  
  
     보고서 서버 서비스 계정이 NetworkService 또는 LocalSystem인 경우 첫 번째 XML 구조가 기본 구성입니다.  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsNegotiate />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     보고서 서버 서비스 계정이 NetworkService 또는 LocalSystem이 아닌 경우 두 번째 XML 구조가 기본 구성입니다.  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    ```  
  
     \</Authentication>  
  
     세 번째 XML 구조는 Windows 통합 보안에서 사용되는 모든 보안 패키지를 지정합니다.  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsNegotiate />  
                 <RSWindowsKerberos />  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
    ```  
  
     네 번째 XML 구조는 Kerberos를 지원하지 않는 배포에 대해서만 또는 Kerberos 인증 오류를 해결하기 위해 NTLM을 지정합니다.  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
    ```  
  
4.  <`Authentication`>의 기존 항목을 선택하고 붙여넣어 덮어씁니다.  
  
     `Custom` 유형에서는 `RSWindows`을 사용할 수 없습니다.  
  
5.  확장된 보호에 적합하게 설정을 수정합니다. 확장된 보호는 기본적으로 사용되지 않습니다.  이러한 항목이 없는 경우 현재 컴퓨터에서 확장된 보호를 지원하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 실행 중이지 않은 것일 수 있습니다. 자세한 내용은 [Extended Protection for Authentication with Reporting Services](extended-protection-for-authentication-with-reporting-services.md)를 참조하세요.  
  
    ```  
          <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>  
          <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>  
    ```  
  
6.  파일을 저장합니다.  
  
7.  스케일 아웃 배포를 구성한 경우 배포의 다른 보고서 서버에 대해 이러한 단계를 반복합니다.  
  
8.  보고서 서버를 다시 시작하여 현재 열려 있는 모든 세션을 지웁니다.  
  
##  <a name="proxyfirewallRSWindowsNegotiate"></a> 보고서 서버에 연결할 때 Kerberos 인증 오류 해결  
 Negotiate 또는 Kerberos 인증용으로 구성된 보고서 서버에서 Kerberos 인증 오류가 발생하면 보고서 서버에 대한 클라이언트 연결이 실패합니다. Kerberos 인증 오류는 다음과 같은 경우 발생합니다.  
  
-   보고서 서버 서비스가 Windows 도메인 사용자 계정으로 실행되는데 해당 계정의 SPN(서비스 사용자 이름)을 등록하지 않은 경우  
  
-   보고서 서버가 `RSWindowsNegotiate` 설정으로 구성된 경우  
  
-   브라우저가 보고서 서버에 보내는 요청의 인증 헤더에서 NTLM 대신 Kerberos를 선택하는 경우  
  
 Kerberos 로깅을 사용하는 경우 오류를 감지할 수 있습니다. 자격 증명을 요청하는 메시지가 여러 번 표시된 다음 빈 브라우저 창이 표시되는 것도 오류의 다른 증상입니다.  
  
 발생 하는 것인지 Kerberos 인증 오류를 제거 하 여 확인할 수 있습니다 < `RSWindowsNegotiate` / > 구성 파일 및 연결을 다시 시도 합니다.  
  
 문제를 확인한 후에는 다음과 같은 방법으로 해결할 수 있습니다.  
  
-   도메인 사용자 계정으로 실행되는 보고서 서버 서비스의 SPN을 등록합니다. 자세한 내용은 [보고서 서버의 SPN&#40;서비스 사용자 이름&#41; 등록](../report-server/register-a-service-principal-name-spn-for-a-report-server.md)을 참조하세요.  
  
-   서비스 계정이 네트워크 서비스와 같은 기본 제공 계정으로 실행되도록 변경합니다. 기본 제공 계정은 컴퓨터를 네트워크에 조인할 때 정의한 Host SPN에 HTTP SPN을 매핑합니다. 자세한 내용은 [서비스 계정 구성&#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)를 참조하세요.  
  
-   NTLM을 사용합니다. NTLM은 Kerberos 인증이 실패하는 경우에도 일반적으로 작동합니다. NTLM을 사용하려면 RSReportServer.config 파일에서 `RSWindowsNegotiate`를 제거하고 `RSWindowsNTLM`만 지정되어 있는지 확인합니다. 이 방법을 선택하는 경우 보고서 서버 서비스의 SPN을 정의하지 않아도 해당 서비스의 도메인 사용자 계정을 계속 사용할 수 있습니다.  
  
#### <a name="logging-information"></a>로깅 정보  
 다양한 로깅 정보 출처를 통해 Kerberos 관련 문제를 해결할 수 있습니다.  
  
##### <a name="user-account-control-attribute"></a>UserAccountControl 특성  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 계정이 Active Directory에서 충분한 특성 집합을 포함하는지 확인합니다. Reporting Services 서비스 추적 로그 파일을 검토하여 UserAccountControl 특성에 대해 기록되는 값을 찾습니다. 이 값은 10진수 형식으로 기록됩니다. 10진수 값을 16진수 형식으로 변환한 다음 UserAccountControl 특성에 대해 설명하는 MSDN 항목에서 해당 값을 찾아야 합니다.  
  
-   Reporting Services 서비스 추적 로그 항목은 다음과 같습니다.  
  
    ```  
    appdomainmanager!DefaultDomain!8f8!01/14/2010-14:42:28:: i INFO: The UserAccountControl value for the service account is 590336  
    ```  
  
-   10진수 값을 16진수 형식으로 변환하는 옵션 중 하나는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계산기를 사용하는 것입니다. Windows 계산기는 ‘Dec’ 옵션과 ‘Hex’ 옵션을 표시하는 여러 모드를 지원합니다. ‘Dec’ 옵션을 선택하고 로그 파일에서 찾은 10진수 값을 붙여 넣거나 입력한 후에 ‘Hex’ 옵션을 선택합니다.  
  
-   그런 다음 [User-Account-Control 특성](https://go.microsoft.com/fwlink/?LinkId=183366) 항목을 참조하여 서비스 계정의 특성을 파생시킵니다.  
  
##### <a name="spns-configured-in-active-directory-for-the-reporting-services-service-account"></a>Reporting Services 서비스 계정에 대해 Active Directory에서 구성된 SPN  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 추적 로그 파일에 SPN을 기록하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 확장된 보호 기능을 일시적으로 사용하도록 설정할 수 있습니다.  
  
-   다음을 설정하여 `rsreportserver.config` 구성 파일을 수정합니다.  
  
    ```  
    <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>   
    <RSWindowsExtendedProtectionScenario>Any</RSWindowsExtendedProtectionScenario>  
    ```  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스를 다시 시작하고 추적 로그 파일에서 다음과 같은 항목을 찾습니다.  
  
    ```  
    rshost!rshost!e44!01/14/2010-14:43:51:: i INFO: Registered valid SPNs list for endpoint 2: rshost!rshost!e44!01/14/2010-14:43:52:: i INFO: SPN Whitelist Added <Explicit> - <HTTP/sqlpod064-13.w2k3.net>.  
    ```  
  
-   \<Explicit> 아래의 값은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 계정에 대해 Active Directory에 구성된 SPN을 포함합니다.  
  
 확장된 보호를 계속 사용하지 않으려면 구성 값을 다시 기본값으로 설정하고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 계정을 다시 시작합니다.  
  
```  
<RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>  
<RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>  
```  
  
 자세한 내용은 [Extended Protection for Authentication with Reporting Services](extended-protection-for-authentication-with-reporting-services.md)를 참조하세요.  
  
#### <a name="how-the-browser-chooses-negotiated-kerberos-or-negotiated-ntlm"></a>브라우저가 Negotiated Kerberos 또는 Negotiated NTLM을 선택하는 방법  
 Internet Explorer를 사용하여 보고서 서버에 연결하는 경우 브라우저에서는 인증 헤더에 Negotiated Kerberos 또는 NTLM을 지정합니다. NTLM은 다음과 같은 경우에 Kerberos 대신 사용됩니다.  
  
-   요청을 로컬 보고서 서버로 보내는 경우  
  
-   요청을 호스트 헤더 또는 서버 이름이 아닌 보고서 서버 컴퓨터의 IP 주소로 보내는 경우  
  
-   방화벽 소프트웨어가 Kerberos 인증에 사용되는 포트를 차단하는 경우  
  
-   특정 서버의 운영 체제에서 Kerberos를 사용하지 않는 경우  
  
-   최신 버전의 운영 체제에서 기본적으로 제공하는 Kerberos 인증 기능을 지원하지 않는 이전 버전의 Windows 클라이언트 및 서버 운영 체제가 도메인에 포함된 경우  
  
 Internet Explorer는 URL, LAN 및 프록시 설정을 구성한 방법에 따라 Negotiated Kerberos 또는 NTLM을 선택할 수도 있습니다.  
  
###### <a name="report-server-url"></a>보고서 서버 URL  
 URL에 정규화된 도메인 이름이 포함된 경우 Internet Explorer는 NTLM을 선택합니다. URL에서 localhost를 지정하는 경우에도 Internet Explorer는 NTLM을 선택합니다. URL에서 컴퓨터의 네트워크 이름을 지정하는 경우에는 Internet Explorer가 Negotiate를 선택합니다. 이 경우 보고서 서버 서비스 계정의 SPN이 있는지 여부에 따라 성공 여부가 결정됩니다.  
  
###### <a name="lan-and-proxy-settings-on-the-client"></a>클라이언트에 대한 LAN 및 프록시 설정  
 Internet Explorer에서 설정하는 LAN 및 프록시 설정에 따라 Kerberos 대신 NTLM이 선택되는지 여부가 결정될 수 있습니다. 그러나 LAN 및 프록시 설정은 조직마다 다르므로 Kerberos 인증 오류에 영향을 주는 정확한 설정을 확인할 수는 없습니다. 예를 들어 사용자 조직에서 URL을 인트라넷 URL에서 인터넷 연결을 통해 확인되는 정규화된 도메인 이름 URL로 변환하는 프록시 설정을 적용할 수 있습니다. URL 유형마다 서로 다른 인증 공급자를 사용하는 경우 실패할 것으로 예상한 일부 연결이 성공할 수도 있습니다.  
  
 발생한 연결 오류가 인증 실패 때문인 것으로 판단되는 경우 다른 LAN 및 프록시 설정 조합을 시도하여 문제를 확인할 수 있습니다. Internet Explorer에서 LAN 및 프록시 설정은 **인터넷 옵션** 의 **연결** 탭에서 **LAN 설정** 을 클릭하여 여는 **LAN 설정**대화 상자에 있습니다.  
  
## <a name="external-resources"></a>외부 리소스  
  
-   Kerberos 및 보고서 서버에 대한 자세한 내용은 [Kerberos와 함께 SharePoint, Reporting Services 및 PerformancePoint Monitoring Server를 사용하여 비즈니스 인텔리전스 솔루션 배포(Deploying a Business Intelligence Solution Using SharePoint, Reporting Services, and PerformancePoint Monitoring Server with Kerberos)](https://go.microsoft.com/fwlink/?LinkID=177751)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 인증](authentication-with-the-report-server.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](granting-permissions-on-a-native-mode-report-server.md)   
 [RSReportServer 구성 파일](../report-server/rsreportserver-config-configuration-file.md)   
 [보고서 서버의 기본 인증 구성](configure-basic-authentication-on-the-report-server.md)   
 [보고서 서버에서 사용자 지정 또는 폼 인증 구성](configure-custom-or-forms-authentication-on-the-report-server.md)   
 [Reporting Services 인증에 대한 확장된 보호](extended-protection-for-authentication-with-reporting-services.md)  
  
  
