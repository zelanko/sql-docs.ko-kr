---
title: 보고서 서버 인증 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], configuring
- connections [Reporting Services], accounts
- Windows authentication [Reporting Services]
- authentication [Reporting Services]
- Forms authentication
ms.assetid: 753c2542-0e97-4d8f-a5dd-4b07a5cd10ab
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 712ae71efdf9ac4faea36dcacd6842406dff358f
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357111"
---
# <a name="authentication-with-the-report-server"></a>보고서 서버 인증
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS)는 보고서 서버에 대해 사용자 및 클라이언트 응용 프로그램을 인증하는 몇 가지 구성 가능 옵션을 제공합니다. 기본적으로 보고서 서버는 Windows 통합 인증을 사용하며 클라이언트 및 네트워크 리소스가 같은 도메인 또는 트러스트된 도메인에 있는 트러스트된 관계를 가정합니다. 네트워크 토폴로지 및 조직의 요구에 따라 Windows 통합 인증에 사용되는 인증 프로토콜을 사용자 지정하거나, 기본 인증을 사용하거나, 제공된 폼 기반 인증 확장 프로그램을 사용자 지정할 수 있습니다. 각 인증 유형을 개별적으로 설정 또는 해제할 수 있습니다. 보고서 서버에서 여러 유형의 요청을 수락하도록 두 개 이상의 인증 유형을 설정할 수 있습니다.  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 IIS를 통해 모든 인증 지원을 제공했습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 릴리스부터는 IIS가 더 이상 사용되지 않고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 모든 인증 요청을 내부적으로 처리합니다.  
  
 보고서 서버 내용 또는 작업에 대한 액세스 권한을 요청하는 모든 사용자나 애플리케이션은 인증을 받아야 액세스 권한을 받을 수 있습니다.  
  
## <a name="authentication-types"></a>인증 유형  
 보고서 서버 내용 또는 작업에 대한 액세스 권한을 요청하는 모든 사용자나 애플리케이션은 보고서 서버에 구성된 인증 유형을 사용하여 인증을 받아야 액세스 권한을 받을 수 있습니다. 다음 표에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 지원되는 인증 유형에 대해 설명합니다.  
  
|인증 유형 이름|HTTP 인증 계층 값|기본적으로 사용|Description|  
|-----------------------------|-------------------------------------|---------------------|-----------------|  
|RSWindowsNegotiate|Negotiate|사용자 계정 컨트롤|Windows 통합 Kerberos 인증을 먼저 시도하지만 Active Directory가 보고서 서버에 클라이언트 요청에 대한 티켓을 부여하지 못할 경우 NTLM으로 대체됩니다. Negotiate는 티켓을 사용할 수 없는 경우에만 NTLM으로 대체됩니다. 첫 번째 시도 결과가 티켓 누락이 아닌 오류인 경우 보고서 서버는 두 번째 시도를 하지 않습니다.|  
|RSWindowsNTLM|NTLM|사용자 계정 컨트롤|Windows 통합 인증에 NTLM이 사용됩니다.<br /><br /> 자격 증명은 다른 요청에 대해 위임되거나 가장되지 않습니다. 이후 요청은 새 시도-응답 시퀀스를 따릅니다. 네트워크 보안 설정에 따라 사용자에게 자격 증명을 요구하는 메시지가 표시되거나 인증 요청이 투명하게 처리됩니다.|  
|RSWindowsKerberos|Kerberos|아니요|Windows 통합 인증에 Kerberos를 사용합니다. 서비스 계정에 대해 SPN(서비스 사용자 이름)을 설정하여 Kerberos를 구성해서는 안 됩니다. 여기에는 도메인 관리자 권한이 요구됩니다. Kerberos에 ID 위임을 설정하는 경우 보고서에 데이터를 제공하는 외부 데이터 원본에 대한 추가 연결에 보고서를 요청하는 사용자의 토큰을 사용할 수도 있습니다.<br /><br /> RSWindowsKerberos를 지정하기 전에 사용 중인 브라우저 종류가 이를 실제로 지원하는지 확인해야 합니다. Internet Explorer를 사용하는 경우 Kerberos 인증은 Negotiate를 통해서만 지원됩니다. Internet Explorer는 Kerberos를 직접 지정하는 인증 요청은 작성하지 않습니다.|  
|RSWindowsBasic|Basic|아니요|기본 인증은 HTTP 프로토콜에 정의되며 보고서 서버에 대한 HTTP 요청을 인증하는 데만 사용됩니다.<br /><br /> 자격 증명이 Base-64 인코딩으로 HTTP 요청에 전달됩니다. 기본 인증을 사용하는 경우 사용자 계정 정보를 네트워크를 통해 보내기 전에 SSL(Secure Sockets Layer)을 사용하여 암호화합니다. SSL은 HTTP TCP/IP 연결을 통해 클라이언트에서 보고서 서버로 연결 요청을 보내는 데 암호화된 채널을 제공합니다. 자세한 내용은 [TechNet 웹 사이트의](https://go.microsoft.com/fwlink/?LinkId=71123) SSL을 사용하여 기밀 데이터 암호화(Using SSL to Encrypt Confidential Data) [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 참조하십시오.|  
|사용자 지정|(Anonymous)|아니요|익명 인증은 HTTP 요청의 인증 헤더를 무시하도록 보고서 서버에 지시합니다. 보고서 서버는 사용자 인증을 위해 제공한 사용자 지정 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] Forms 인증에 대한 호출을 제외한 모든 요청을 수락합니다.<br /><br /> 보고서 서버의 모든 인증 요청을 처리하는 사용자 지정 인증 모듈을 배포하는 경우에만 `Custom`을 지정하십시오. 사용자 지정 인증 유형은 기본 Windows 인증 확장 프로그램에서 사용할 수 없습니다.|  
  
## <a name="unsupported-authentication-methods"></a>지원되지 않는 인증 방법  
 다음 인증 방법 및 요청은 지원되지 않습니다.  
  
|인증 방법|설명|  
|---------------------------|-----------------|  
|익명|보고서 서버는 사용자 지정 인증 확장 프로그램이 포함된 배포를 제외하고 익명 사용자의 인증되지 않은 요청을 수락하지 않습니다.<br /><br /> 기본 인증용으로 구성된 보고서 서버에 대한 보고서 작성기 액세스를 사용하도록 설정한 경우 보고서 작성기는 인증되지 않은 요청을 수락합니다.<br /><br /> 다른 모든 경우 익명 요청은 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]에 도착하기 전에 HTTP 상태 401 액세스 거부 오류와 함께 거부됩니다. 401 액세스 거부를 수신하는 클라이언트는 유효한 인증 유형을 사용하여 요청을 다시 작성해야 합니다.|  
|SSO(Single Sign-On) 기술|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 Single-Sign-On 기술에 대한 기본 지원을 제공하지 않습니다. Single-Sign-On 기술을 사용하려면 사용자 지정 인증 확장 프로그램을 만들어야 합니다.<br /><br /> 보고서 서버 호스팅 환경은 ISAPI 필터를 지원하지 않습니다. 사용 중인 SSO 기술이 ISAPI 필터로 구현된 경우 RSASecueID에 대한 ISA Server 기본 제공 지원 또는 RADIUS 프로토콜을 사용하는 것이 좋습니다. ISA Server ISAPI 또는 RS용 HTTPModule을 만드는 방법도 있지만 ISA Server를 직접 사용하는 것이 좋습니다.|  
|Passport|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되지 않습니다.|  
|다이제스트|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되지 않습니다.|  
  
## <a name="configuration-of-authentication-settings"></a>인증 설정 구성  
 인증 설정은 보고서 서버 URL이 예약될 때 기본 보안용으로 구성됩니다. 이 설정을 잘못 수정하면 보고서 서버는 인증할 수 없는 HTTP 요청에 대해 HTTP 401 액세스 거부 오류를 반환합니다. 인증 유형을 선택하려면 현재 네트워크에서 Windows 인증이 지원되는 방식을 먼저 알아야 합니다. 적어도 하나의 인증 유형을 지정해야 합니다. RSWindows에 대해 여러 인증 유형을 지정할 수 있습니다. RSWindows 인증 유형 (즉, `RSWindowsBasic`, `RSWindowsNTLM`를 `RSWindowsKerberos`, 및 **RSWindowsNegotiate**) 사용자 지정을 사용 하 여 함께 사용할 수 없습니다.  
  
> [!IMPORTANT]  
>  Reporting Services는 현재 컴퓨팅 환경에 올바른지 여부를 확인하기 위해 사용자가 지정하는 설정의 유효성을 검사하지 않습니다. 기본 보안이 현재 설치에서 작동하지 않는 경우 또는 현재 보안 인프라에 대해 유효하지 않은 구성 설정이 지정되는 경우가 있습니다. 따라서 보고서 서버 배포를 큰 규모의 조직에 적용하기 전에 통제된 테스트 환경에서 신중하게 테스트하는 것이 중요합니다.  
  
 보고서 서버 웹 서비스와 보고서 관리자는 항상 동일한 인증 유형을 사용합니다. 보고서 서버 서비스의 기능 영역에 대해 여러 인증 유형을 구성할 수 없습니다. 스케일 아웃 배포를 사용 중인 경우 배포에 있는 모든 노드의 모든 변경 내용을 복제해야 합니다. 동일한 확장에 있는 여러 노드에서 여러 가지 인증 유형을 사용하도록 구성할 수 없습니다.  
  
 백그라운드 처리는 최종 사용자의 요청을 수락하지 않지만 무인 실행을 위한 요청은 모두 인증합니다. 백그라운드 처리는 항상 Windows 인증을 사용하며 보고서 서버 서비스 또는 구성된 경우 무인 실행 계정을 사용하여 요청을 인증합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [보고서 서버의 Windows 인증 구성](configure-windows-authentication-on-the-report-server.md)  
  
-   [보고서 서버의 기본 인증 구성](configure-basic-authentication-on-the-report-server.md)  
  
-   [보고서 서버에서 사용자 지정 또는 폼 인증 구성](configure-custom-or-forms-authentication-on-the-report-server.md)  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|링크|  
|-----------------------|-----------|  
|Windows 통합 인증 유형을 구성합니다.|[보고서 서버의 Windows 인증 구성](configure-windows-authentication-on-the-report-server.md)|  
|기본 인증 유형을 구성합니다.|[보고서 서버의 기본 인증 구성](configure-basic-authentication-on-the-report-server.md)|  
|폼 인증 또는 사용자 지정 인증 유형을 구성합니다.|[보고서 서버에서 사용자 지정 또는 폼 인증 구성](configure-custom-or-forms-authentication-on-the-report-server.md)|  
|보고서 관리자에서 사용자 지정 인증 시나리오를 처리할 수 있도록 합니다.|[보고서 관리자에서 사용자 지정 인증 쿠키를 전달하도록 구성](configure-the-web-portal-to-pass-custom-authentication-cookies.md)|  
  
## <a name="see-also"></a>관련 항목  
 [기본 모드 보고서 서버에 대한 사용 권한 부여](granting-permissions-on-a-native-mode-report-server.md)   
 [RSReportServer 구성 파일](../report-server/rsreportserver-config-configuration-file.md)   
 (만들기-및-관리-역할-assignments.md)   
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
 [보안 확장 프로그램 구현](../extensions/security-extension/implementing-a-security-extension.md)   
 [기본 모드 보고서 서버에서 SSL 연결 구성](configure-ssl-connections-on-a-native-mode-report-server.md)   
 [보고서 작성기 액세스 구성](../report-server/configure-report-builder-access.md)   
 [보안 확장 프로그램 개요](../extensions/security-extension/security-extensions-overview.md)   
 [Reporting Services의 인증](../extensions/security-extension/authentication-in-reporting-services.md)   
 [Reporting Services의 권한 부여](../extensions/security-extension/authorization-in-reporting-services.md)  
  
  
