---
title: 보고서 서버의 기본 인증 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- Basic authentication
ms.assetid: 8faf2938-b71b-4e61-a172-46da2209ff55
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 32b46265b5da376bc974b55c48bf54bad88917d8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66102154"
---
# <a name="configure-basic-authentication-on-the-report-server"></a>보고서 서버에서 기본 인증 구성
  기본적으로 Reporting Services는 Negotiate 및 NTLM 인증을 지정하는 요청을 수락합니다. 현재 배포에 기본 인증을 사용하는 클라이언트 애플리케이션 또는 브라우저가 포함된 경우 지원되는 유형 목록에 기본 인증을 추가해야 합니다. 또한 보고서 작성기를 사용하려면 보고서 작성기 파일에 대한 익명 액세스를 설정해야 합니다.  
  
 보고서 서버에 기본 인증을 구성하려면 RSReportServer.config 파일의 XML 요소 및 값을 편집해야 합니다. 이 항목의 예를 복사하고 붙여넣어 기본값을 대체할 수 있습니다.  
  
 기본 인증을 설정하기 전에 보안 인프라에서 기본 인증을 지원하는지 확인하십시오. 기본 인증에서 보고서 서버 웹 서비스는 로컬 보안 기관에 자격 증명을 전달합니다. 자격 증명이 로컬 사용자 계정을 지정하는 경우 사용자는 보고서 서버 컴퓨터의 로컬 보안 기관에 의해 인증되며 로컬 리소스에 대해 유효한 보안 토큰을 받게 됩니다. 도메인 사용자 계정에 대한 자격 증명은 도메인 컨트롤러로 전달되어 인증됩니다. 인증 후 발급되는 티켓은 네트워크 리소스에 대해 유효합니다.  
  
 자격 증명이 네트워크의 도메인 컨트롤러로 전송되는 동안 도청될 위험을 완화하려면 SSL(Secure Sockets Layer)과 같은 채널 암호화가 필요합니다. 기본 인증은 자체적으로 사용자 이름을 일반 텍스트로, 암호는 Base-64 인코딩으로 전송합니다. 채널 암호화를 추가하면 패킷을 읽기가 불가능하게 됩니다. 자세한 내용은 [기본 모드 보고서 서버에서 SSL 연결 구성](configure-ssl-connections-on-a-native-mode-report-server.md)을 참조하세요.  
  
 기본 인증을 설정한 다음에는 보고서에 데이터를 제공하는 외부 데이터 원본에 대한 연결 속성을 설정할 때 사용자가 **Windows 통합 보안** 옵션을 선택할 수 없다는 점을 유의하십시오. 이 옵션은 데이터 원본 속성 페이지에서 회색으로 나타납니다.  
  
> [!NOTE]  
>  다음은 기본 모드 보고서 서버에 대한 지침입니다. 보고서 서버가 SharePoint 통합 모드로 배포된 경우 Windows 통합 보안을 지정하는 기본 인증 설정을 사용해야 합니다. 보고서 서버는 기본 Windows 인증 확장 프로그램의 내부 기능을 사용하여 SharePoint 통합 모드의 보고서 서버를 지원합니다.  
  
### <a name="to-configure-a-report-server-to-use-basic-authentication"></a>기본 인증을 사용하도록 보고서 서버를 구성하려면  
  
1.  텍스트 편집기에서 RSReportServer.config를 엽니다.  
  
     파일에 위치한  *\<드라이브 >:* \Program Files\Microsoft SQL Server\MSRS12. MSSQLSERVER\Reporting Services\ReportServer입니다.  
  
2.  찾을 <`Authentication`>.  
  
3.  다음 중 필요에 가장 맞는 XML 구조를 복사합니다. 첫 번째 XML 구조는 다음 섹션에 설명되어 있는 모든 요소를 지정하기 위한 자리 표시자를 제공합니다.  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsBasic>  
                       <LogonMethod>3</LogonMethod>  
                       <Realm></Realm>  
                       <DefaultDomain></DefaultDomain>  
                 </RSWindowsBasic>  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     기본값을 사용하는 경우 최소 요소 구조를 복사할 수 있습니다.  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsBasic/>  
          </AuthenticationTypes>  
    ```  
  
4.  에 대 한 기존 항목 위에 붙여넣습니다 <`Authentication`>.  
  
     여러 인증 유형을 사용하는 경우 `RSWindowsBasic` 요소만 추가하고 `RSWindowsNegotiate`, `RSWindowsNTLM` 또는 `RSWindowsKerberos`에 대한 요소는 삭제하지 마십시오.  
  
     Safari 브라우저를 지원하려는 경우에는 여러 인증 유형을 사용하도록 보고서 서버를 구성할 수 없습니다. `RSWindowsBasic`만 지정하고 다른 항목은 삭제해야 합니다.  
  
     `Custom`은 다른 인증 유형과 함께 사용할 수 없습니다.  
  
5.  <`Realm`> 또는 <`DefaultDomain`>에 대한 빈 값을 현재 환경에 유효한 값으로 대체합니다.  
  
6.  파일을 저장합니다.  
  
7.  스케일 아웃 배포를 구성한 경우 배포의 다른 보고서 서버에 대해 이러한 단계를 반복합니다.  
  
8.  보고서 서버를 다시 시작하여 현재 열려 있는 모든 세션을 지웁니다.  
  
## <a name="rswindowsbasic-reference"></a>RSWindowsBasic 참조  
 기본 인증을 구성할 때 다음 요소를 지정할 수 있습니다.  
  
|요소|필수|유효한 값|  
|-------------|--------------|------------------|  
|LogonMethod|사용자 계정 컨트롤<br /><br /> 값을 지정하지 않으면 3이 사용됩니다.|`2` = 일반 텍스트 암호를 인증하는 고성능 서버를 위한 네트워크 로그온입니다.<br /><br /> `3` = 각 HTTP 요청과 함께 전송되는 인증 패키지에 로그온 자격 증명을 유지하여 서버가 네트워크의 다른 서버에 연결할 때 사용자를 가장할 수 있도록 하는 일반 텍스트 로그온입니다. (기본값)<br /><br /> 참고: 값 0 (대화형 로그온) 및 1 (일괄 처리 로그온)에서 지원 되지 않습니다 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]합니다.|  
|Realm|선택 사항|조직의 보호된 리소스에 대한 액세스를 제어하는 데 사용되는 권한 부여 및 인증 기능이 포함된 리소스 파티션을 지정합니다.|  
|DefaultDomain|선택 사항|사용자를 인증할 때 서버가 사용하는 도메인을 지정합니다. 이 값은 선택 사항이지만 생략하면 보고서 서버가 컴퓨터 이름을 도메인으로 사용합니다. 컴퓨터가 도메인 멤버인 경우 해당 도메인이 기본 도메인입니다. 도메인 컨트롤러에 보고서 서버를 설치한 경우에는 컴퓨터에서 제어되는 도메인이 사용됩니다.|  
  
## <a name="enabling-anonymous-access-to-report-builder-application-files"></a>보고서 작성기 애플리케이션 파일에 대한 익명 액세스 사용  
 보고서 작성기는 ClickOnce 기술을 사용하여 해당 애플리케이션 파일을 클라이언트 컴퓨터로 다운로드하고 설치합니다. 클라이언트 컴퓨터에서 시작된 ClickOnce 애플리케이션 실행 프로그램은 보고서 서버 컴퓨터의 추가 애플리케이션 파일을 요청합니다. 보고서 서버가 기본 인증용으로 구성된 경우 ClickOnce 애플리케이션 실행 프로그램은 기본 인증을 지원하지 않으므로 인증 검사에 실패하게 됩니다.  
  
 이 문제를 해결하려면 보고서 작성기 프로그램 파일에 대한 익명 액세스를 구성합니다. 이렇게 하면 ClickOnce가 파일을 검색할 때 인증 검사를 건너뛸 수 있습니다. 익명 액세스를 사용하려면 다음을 수행합니다.  
  
-   보고서 서버가 기본 인증용으로 구성되어 있는지 확인합니다.  
  
-   ReportBuilder 아래에 bin 폴더를 만들고 4개의 어셈블리를 이 폴더에 복사합니다.  
  
-   RSReportServer.config에 `IsReportBuilderAnonymousAccessEnabled` 요소를 추가하고 `True`로 설정합니다. 파일을 저장하면 보고서 서버가 보고서 작성기에 대한 새 엔드포인트를 만듭니다. 이 엔드포인트는 프로그램 파일에 액세스하기 위해 내부적으로 사용되며 코드에서 사용할 수 있는 프로그래밍 인터페이스는 제공하지 않습니다. 별도의 엔드포인트를 통해 보고서 작성기는 보고서 서버 서비스 프로세스 경계 내에 자체 애플리케이션 도메인을 실행할 수 있습니다.  
  
-   필요에 따라 최소 권한 계정을 지정하여 보고서 서버와 다른 보안 컨텍스트에서 요청을 처리할 수 있습니다. 이 계정은 보고서 서버의 보고서 작성기 파일에 액세스하기 위한 익명 계정이 됩니다. 이 계정은 ASP.NET 작업자 프로세스에 있는 스레드의 ID를 설정합니다. 이 스레드에서 실행되는 요청은 인증 검사 없이 보고서 서버로 전달됩니다. 이 계정이 IUSR_ 같음\<컴퓨터 > 계정에서 인터넷 정보 서비스 (IIS)를 ASP.NET 작업자에 대 한 보안 컨텍스트를 설정 하는 데 사용 되는 익명 액세스 및 가장이 사용 하는 경우를 처리 합니다. 계정을 지정하려면 보고서 작성기 Web.config 파일에 계정을 추가합니다.  
  
 보고서 작성기 프로그램 파일에 대한 익명 액세스를 사용하려면 보고서 서버를 기본 인증용으로 구성해야 합니다. 보고서 서버가 기본 인증으로 구성되지 않은 경우 익명 액세스를 허용하려고 하면 오류가 발생합니다.  
  
 인증 문제 및 보고서 작성기에 대한 자세한 내용은 [보고서 작성기 액세스 구성](../report-server/configure-report-builder-access.md)을 참조하세요.  
  
#### <a name="to-configure-report-builder-access-on-a-report-server-configured-for-basic-authentication"></a>기본 인증용으로 구성된 보고서 서버에서 보고서 작성기 액세스를 구성하려면  
  
1.  RSReportServer.config 파일의 인증 설정을 검사하여 보고서 서버가 기본 인증용으로 구성되어 있는지 확인합니다.  
  
2.  ReportBuilder 폴더 아래에 bin 폴더를 만듭니다. 기본적으로 이 폴더의 위치는 \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\ReportBuilder입니다.  
  
3.  ReportServer\Bin 폴더에서 다음 4개의 어셈블리를 ReportBuilder\BIN 폴더로 복사합니다.  
  
     Microsoft.ReportingServices.Diagnostics.dll  
  
     Microsoft.ReportingServices.Interfaces.dll  
  
     ReportingServicesAppDomainManager.dll  
  
     RSHttpRuntime.dll  
  
4.  필요에 따라 익명 계정에서 보고서 작성기 요청을 처리하기 위한 Web.config 파일을 만듭니다.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
    <system.web>  
    <authentication mode="Windows" />    
    <identity impersonate="true " userName="username" password="password"/>  
    </system.web>  
    </configuration>  
    ```  
  
     Web.config 파일을 포함하는 경우 인증 모드가 `Windows`로 설정되어 있어야 합니다.  
  
     `Identity impersonate`은 `True` 또는 `False`가 될 수 있습니다.  
  
    -   ASP.NET에서 보안 토큰을 읽지 않도록 하려면 `False`로 설정합니다. 요청은 보고서 서버 서비스의 보안 컨텍스트에서 실행됩니다.  
  
    -   ASP.NET이 호스트 계층에서 보안 토큰을 읽도록 하려면 `True`로 설정합니다. `True`로 설정하는 경우 `userName` 및 `password`도 지정하여 익명 계정을 지정해야 합니다. 지정하는 자격 증명은 요청이 실행되는 보안 컨텍스트를 결정합니다.  
  
5.  Web.config 파일을 ReportBuilder\bin 폴더에 저장합니다.  
  
6.  RSReportServer.config 파일을 열어 Services 섹션에서 `IsReportManagerEnabled`를 찾은 후 그 아래에 다음 설정을 추가합니다.  
  
    ```  
    <IsReportBuilderAnonymousAccessEnabled>True</IsReportBuilderAnonymousAccessEnabled>  
    ```  
  
7.  RSReportServer.config를 저장하고 파일을 닫습니다.  
  
8.  보고서 서버를 다시 시작합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 애플리케이션의 애플리케이션 도메인](../report-server/application-domains-for-report-server-applications.md)   
 [Reporting Services 보안 및 보호](reporting-services-security-and-protection.md)  
  
  
