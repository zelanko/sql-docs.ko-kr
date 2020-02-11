---
title: 기본 모드 보고서 서버에서 SSL 연결 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Secure Sockets Layer (SSL)
ms.assetid: 212f2042-456a-4c0a-8d76-480b18f02431
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7fb33e6ccb5afbdee1bf6c3673a24548d6fe9961
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102114"
---
# <a name="configure-ssl-connections-on-a-native-mode-report-server"></a>기본 모드 보고서 서버에서 SSL 연결 구성
  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드는 HTTP SSL(Secure Sockets Layer) 서비스를 사용하여 보고서 서버에 대한 암호화된 연결을 설정합니다. 보고서 서버 컴퓨터의 로컬 인증서 저장소에 설치된 인증서(.cer) 파일이 있는 경우 인증서를 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 예약에 바인딩하여 암호화된 채널을 통한 보고서 서버 연결을 지원할 수 있습니다.  
  
> [!TIP]  
>  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드를 사용 중인 경우 자세한 내용은 SharePoint 설명서를 참조하십시오. 예를 들어 [SharePoint 2010 웹 애플리케이션에서 SSL을 사용하는 방법(https://blogs.msdn.com/b/sowmyancs/archive/2010/02/12/how-to-enable-ssl-on-a-sharepoint-web-application.aspx)](https://blogs.msdn.com/b/sowmyancs/archive/2010/02/12/how-to-enable-ssl-on-a-sharepoint-web-application.aspx)입니다.  
  
 인터넷 정보 서비스(IIS)도 HTTP SSL을 사용하므로 IIS와 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 동일한 컴퓨터에서 실행하는 경우 중요한 상호 운용성 문제를 고려해야 합니다. IIS와의 상호 운용성 문제 섹션에서 이러한 문제를 처리하는 방법에 대한 지침을 확인하십시오.  
  
## <a name="server-certificate-requirements"></a>서버 인증서 요구 사항  
 컴퓨터에 서버 인증서가 설치되어 있어야 합니다(클라이언트 인증서는 지원되지 않음). Reporting Services는 인증서 요청, 생성, 다운로드 또는 설치를 위한 기능을 제공하지 않습니다. 
  [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 은 신뢰할 수 있는 인증 기관의 인증서를 요청하는 데 사용할 수 있는 인증서 스냅인을 제공합니다.  
  
 테스트를 위해 로컬로 인증서를 생성할 수 있습니다. 
  **MakeCert** 유틸리티에서 예제 명령을 템플릿으로 사용하는 경우 명령을 실행하기 전에 서버 이름을 호스트로 지정하고 모든 줄 바꿈을 제거해야 합니다. DOS 창에서 명령을 실행하는 경우 전체 명령을 수용하기 위해 창의 버퍼 크기를 늘려야 할 수도 있습니다.  
  
 IIS와 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 동일한 컴퓨터에서 함께 실행하는 경우 IIS 관리자 콘솔 애플리케이션을 사용하여 컴퓨터에 설치된 인증서를 가져올 수 있습니다. IIS 관리자에는 신뢰할 수 있는 인증 기관의 후속 처리를 위해 인증서 요청(.crt) 파일을 만들고 패키징하는 옵션이 포함되어 있습니다. 사용 중인 인증 기관은 인증서(.cer) 파일을 만들어 돌려보냅니다. IIS 관리 콘솔을 사용하여 로컬 저장소의 인증서 파일을 설치할 수 있습니다. 자세한 내용은 Technet의 [SSL을 사용하여 기밀 데이터 암호화(Using SSL to Encrypt Confidential Data)](https://go.microsoft.com/fwlink/?LinkId=71123) 를 참조하십시오.  
  
## <a name="interoperability-issues-with-iis"></a>IIS와의 상호 운용성 문제  
 동일한 컴퓨터에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 IIS의 공존은 보고서 서버에 대한 SSL 연결에 중요한 영향을 미칩니다.  
  
-   IIS가 설치되면 W3SVC(World Wide Web) 서비스가 항상 실행되어야 합니다. 실행 중인 IIS가 검색되면 HTTP SSL 서비스는 IIS에 대한 종속성을 생성합니다. 이는 IIS와 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가 동일한 컴퓨터에 설치되고 SSL 연결을 위해 보고서 서버 URL을 구성하는 경우 W3SVC(World Wide Web service)가 항상 실행 중이어야 함을 의미합니다.  
  
-   IIS를 제거하면 SSL에 바인딩된 보고서 서버 URL에 대한 서비스가 일시적으로 끊어질 수 있습니다. 이러한 이유로 IIS를 제거한 다음 컴퓨터를 다시 시작하는 것이 좋습니다.  
  
     캐시에서 모든 SSL 세션을 지우려면 컴퓨터를 다시 부팅해야 합니다. 일부 운영 체제에서는 SSL 세션을 10시간까지 캐시하며 이로 인해 HTTP.SYS의 URL 예약에서 SSL 바인딩이 제거된 후에도 https:// URL이 계속 작동하게 됩니다. 컴퓨터를 다시 부팅하면 채널을 사용하는 모든 열린 연결이 닫힙니다.  
  
## <a name="bind-ssl-to-a-reporting-services-url-reservation"></a>SSL을 Reporting Services URL 예약에 바인딩  
 다음 단계에는 인증서 요청, 생성, 다운로드 또는 설치를 위한 지침이 포함되어 있지 않습니다. 사용할 수 있는 인증서가 설치되어 있어야 합니다. 지정하는 인증서 속성, 인증서를 가져오는 인증 기관, 인증서를 요청하고 설치하는 데 사용할 도구와 유틸리티는 각자의 재량에 따라 선택합니다.  
  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 인증서를 바인딩할 수 있습니다. 인증서가 로컬 컴퓨터 저장소에 올바르게 설치되면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구에서 이를 검색하여 **웹 서비스 URL** 및 **보고서 관리자 URL** 페이지에 **SSL 인증서** 목록을 표시합니다.  
  
### <a name="to-configure-a-report-server-url-for-ssl"></a>보고서 서버 URL을 SSL에 대해 구성하려면  
  
1.  Reporting Services 구성 도구를 시작한 후 보고서 서버에 연결합니다.  
  
2.  
  **웹 서비스 URL**을 클릭합니다.  
  
3.  SSL 인증서 목록을 확장합니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 로컬 저장소의 서버 인증 인증서를 검색합니다. 인증서를 설치했는데 목록에 표시되지 않을 경우 서비스를 다시 시작해야 할 수 있습니다. Reporting Services 구성 도구의 **보고서 서버 상태** 페이지에서 **중지** 및 **시작** 단추를 사용하여 서비스를 다시 시작할 수 있습니다.  
  
4.  인증서를 선택합니다.  
  
5.  **적용**을 클릭합니다.  
  
6.  URL을 클릭하여 제대로 작동하는지 확인합니다.  
  
 보고서 서버 데이터베이스 구성은 URL 테스트를 위한 요구 사항입니다. 보고서 서버 데이터베이스를 아직 만들지 않은 경우 URL을 테스트하기 전에 만듭니다.  
  
 보고서 관리자 및 보고서 서버 웹 서비스에 대한 URL 예약은 독립적으로 구성됩니다. SSL 암호화된 채널을 통한 보고서 관리자 액세스도 구성하려면 다음 단계를 계속 진행하십시오.  
  
1.  
  **보고서 관리자 URL**을 클릭합니다.  
  
2.  **고급**을 클릭합니다.  
  
3.  
  **보고서 관리자에 대한 여러 SSL ID**에서 **추가**를 클릭합니다.  
  
4.  인증서를 선택하고 **확인**을 클릭한 후 **적용**을 클릭합니다.  
  
5.  URL을 클릭하여 제대로 작동하는지 확인합니다.  
  
## <a name="how-certificate-bindings-are-stored"></a>인증서 바인딩의 저장 방식  
 인증서 바인딩은 HTTP.SYS에 저장됩니다. 정의한 바인딩의 표현은 RSReportServer.config 파일의 `URLReservations` 섹션에도 저장됩니다. 이 구성 파일의 설정은 다른 위치에서 지정되는 실제 값의 표현일 뿐입니다. 구성 파일에서 값을 직접 수정하지 마십시오. 구성 설정은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구 또는 보고서 서버 WMI(Windows Management Instrumentation) 공급자를 사용하여 인증서를 바인딩한 후에만 파일에 표시됩니다.  
  
> [!NOTE]  
>  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 SSL 인증서를 사용하여 바인딩을 구성하는 경우 나중에 컴퓨터에서 해당 인증서를 제거하려면 컴퓨터에서 인증서를 제거하기 전에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 바인딩을 제거해야 합니다. 그렇지 않으면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구 또는 WMI를 사용하여 바인딩을 제거할 수 없으며 "매개 변수가 잘못되었습니다" 오류가 표시됩니다. 컴퓨터에서 이미 인증서를 제거한 경우 Httpcfg.exe 도구를 사용하여 HTTP.SYS에서 바인딩을 제거할 수 있습니다. Httpcfg.exe에 대한 자세한 내용은 Windows 제품 설명서를 참조하십시오.  
  
 SSL 바인딩은 Microsoft Windows의 공유 리소스입니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자 또는 IIS 관리자와 같은 다른 도구에서 변경한 내용은 동일한 컴퓨터의 다른 애플리케이션에 영향을 줄 수 있습니다. 바인딩을 만들 때 사용한 것과 동일한 도구를 사용하여 바인딩을 편집하는 것이 가장 좋습니다.  예를 들어 구성 관리자를 사용하여 SSL 바인딩을 만든 경우 구성 관리자를 사용하여 바인딩의 수명을 관리하고, IIS 관리자를 사용하여 바인딩을 만드는 경우 IIS 관리자를 사용하여 바인딩의 수명을 관리하는 것이 좋습니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치하기 전에 IIS가 이미 컴퓨터에 설치되어 있는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 구성하기 전에 IIS에서 SSL 구성을 검토하는 것이 가장 좋습니다.  
  
 Reporting Services 구성 관리자를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 대한 SSL 바인딩을 제거하는 경우 인터넷 정보 서비스(IIS)를 실행하는 서버 또는 다른 HTTP.SYS 서버의 웹 사이트에 대해 SSL이 더 이상 작동하지 않을 수 있습니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 다음 레지스트리 키를 제거합니다. 이 레지스트리 키가 제거되면 IIS에 대한 SSL 바인딩도 제거됩니다. 이 바인딩이 없으면 HTTPS 프로토콜에 대해 SSL이 제공되지 않습니다. 이 문제를 진단하려면 IIS 관리자 또는 HTTPCFG.exe 명령줄 유틸리티를 사용합니다. 이 문제를 해결하려면 IIS 관리자를 사용하여 웹 사이트에 대한 SSL 바인딩을 복원합니다. 이 문제가 다시 발생하지 않도록 하려면 IIS 관리자를 사용하여 SSL 바인딩을 제거한 다음 IIS 관리자를 사용하여 원하는 웹 사이트에 대한 바인딩을 복원합니다. 자세한 내용은 기술 자료 문서 [SSL 바인딩을 제거한 후 SSL이 더 이상 작동하지 않습니다(https://support.microsoft.com/kb/956209/n)](https://support.microsoft.com/kb/956209/n)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 인증](authentication-with-the-report-server.md)   
 [보고서 서버 구성 및 관리&#40;SSRS 기본 모드&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Rsreportserver.config 구성 파일](../report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 구성 관리자 &#40;del&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
