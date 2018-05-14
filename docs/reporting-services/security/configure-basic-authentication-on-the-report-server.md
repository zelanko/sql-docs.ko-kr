---
title: 보고서 서버의 기본 인증 구성 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: security
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- Basic authentication
ms.assetid: 8faf2938-b71b-4e61-a172-46da2209ff55
caps.latest.revision: 28
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 999ebd9aad00dff3418e48d3768588cd16d3fbbb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-basic-authentication-on-the-report-server"></a>보고서 서버에서 기본 인증 구성
  기본적으로 Reporting Services는 Negotiate 및 NTLM 인증을 지정하는 요청을 수락합니다. 현재 배포에 기본 인증을 사용하는 클라이언트 응용 프로그램 또는 브라우저가 포함된 경우 지원되는 유형 목록에 기본 인증을 추가해야 합니다. 또한 보고서 작성기를 사용하려면 보고서 작성기 파일에 대한 익명 액세스를 설정해야 합니다.  
  
 보고서 서버에 기본 인증을 구성하려면 RSReportServer.config 파일의 XML 요소 및 값을 편집해야 합니다. 이 항목의 예를 복사하고 붙여넣어 기본값을 대체할 수 있습니다.  
  
 기본 인증을 설정하기 전에 보안 인프라에서 기본 인증을 지원하는지 확인하십시오. 기본 인증에서 보고서 서버 웹 서비스는 로컬 보안 기관에 자격 증명을 전달합니다. 자격 증명이 로컬 사용자 계정을 지정하는 경우 사용자는 보고서 서버 컴퓨터의 로컬 보안 기관에 의해 인증되며 로컬 리소스에 대해 유효한 보안 토큰을 받게 됩니다. 도메인 사용자 계정에 대한 자격 증명은 도메인 컨트롤러로 전달되어 인증됩니다. 인증 후 발급되는 티켓은 네트워크 리소스에 대해 유효합니다.  
  
 자격 증명이 네트워크의 도메인 컨트롤러로 전송되는 동안 도청될 위험을 완화하려면 SSL(Secure Sockets Layer)과 같은 채널 암호화가 필요합니다. 기본 인증은 자체적으로 사용자 이름을 일반 텍스트로, 암호는 Base-64 인코딩으로 전송합니다. 채널 암호화를 추가하면 패킷을 읽기가 불가능하게 됩니다. 자세한 내용은 [기본 모드 보고서 서버에서 SSL 연결 구성](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)을 참조하세요.  
  
 기본 인증을 설정한 다음에는 보고서에 데이터를 제공하는 외부 데이터 원본에 대한 연결 속성을 설정할 때 사용자가 **Windows 통합 보안** 옵션을 선택할 수 없다는 점을 유의하십시오. 이 옵션은 데이터 원본 속성 페이지에서 회색으로 나타납니다.  
  
> [!NOTE]  
>  다음은 기본 모드 보고서 서버에 대한 지침입니다. 보고서 서버가 SharePoint 통합 모드로 배포된 경우 Windows 통합 보안을 지정하는 기본 인증 설정을 사용해야 합니다. 보고서 서버는 기본 Windows 인증 확장 프로그램의 내부 기능을 사용하여 SharePoint 통합 모드의 보고서 서버를 지원합니다.  
  
### <a name="to-configure-a-report-server-to-use-basic-authentication"></a>기본 인증을 사용하도록 보고서 서버를 구성하려면  
  
1.  텍스트 편집기에서 RSReportServer.config를 엽니다.  
  
     이 파일은 *\<드라이브>:* \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer에 있습니다.  
  
2.  \<**인증**>을 찾습니다.  
  
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
  
4.  \<**인증**>의 기존 항목 위에 붙여넣습니다.  
  
     여러 인증 유형을 사용하는 경우 **RSWindowsBasic** 요소만 추가하고 **RSWindowsNegotiate**, **RSWindowsNTLM**또는 **RSWindowsKerberos**에 대한 요소는 삭제하지 마십시오.  
  
     **Custom** 은 다른 인증 유형과 함께 사용할 수 없습니다.  
  
5.  \<**Realm**> 또는 \<**DefaultDomain**>에 대한 빈 값을 현재 환경에 유효한 값으로 대체합니다.  
  
6.  파일을 저장합니다.  
  
7.  스케일 아웃 배포를 구성한 경우 배포의 다른 보고서 서버에 대해 이러한 단계를 반복합니다.  
  
8.  보고서 서버를 다시 시작하여 현재 열려 있는 모든 세션을 지웁니다.  
  
## <a name="rswindowsbasic-reference"></a>RSWindowsBasic 참조  
 기본 인증을 구성할 때 다음 요소를 지정할 수 있습니다.  
  
|요소|필수|유효한 값|  
|-------------|--------------|------------------|  
|LogonMethod|예<br /><br /> 값을 지정하지 않으면 3이 사용됩니다.|**2** = 일반 텍스트 암호를 인증하는 고성능 서버를 위한 네트워크 로그온입니다.<br /><br /> **3** = 각 HTTP 요청과 함께 전송되는 인증 패키지에 로그온 자격 증명을 유지하여 서버가 네트워크의 다른 서버에 연결할 때 사용자를 가장할 수 있도록 하는 일반 텍스트 로그온입니다. (기본값)<br /><br /> 참고: 값 0(대화형 로그온) 및 1(일괄 처리 로그온)은 **에서 지원되지** 않습니다 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].|  
|Realm|선택 사항|조직의 보호된 리소스에 대한 액세스를 제어하는 데 사용되는 권한 부여 및 인증 기능이 포함된 리소스 파티션을 지정합니다.|  
|DefaultDomain|선택 사항|사용자를 인증할 때 서버가 사용하는 도메인을 지정합니다. 이 값은 선택 사항이지만 생략하면 보고서 서버가 컴퓨터 이름을 도메인으로 사용합니다. 컴퓨터가 도메인 멤버인 경우 해당 도메인이 기본 도메인입니다. 도메인 컨트롤러에 보고서 서버를 설치한 경우에는 컴퓨터에서 제어되는 도메인이 사용됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 응용 프로그램의 응용 프로그램 도메인](../../reporting-services/report-server/application-domains-for-report-server-applications.md)   
 [Reporting Services 보안 및 보호](../../reporting-services/security/reporting-services-security-and-protection.md)  
  
  
