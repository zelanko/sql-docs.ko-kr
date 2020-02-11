---
title: URL 구성(SSRS 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], syntax
ms.assetid: 851e163a-ad2a-491e-bc1e-4df92327092f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 617a4e01b3fd4f8dcbc6d929c2a26d483f2fa1ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108858"
---
# <a name="configure-a-url--ssrs-configuration-manager"></a>URL 구성(SSRS 구성 관리자)
  보고서 관리자 또는 보고서 서버 웹 서비스를 사용하려면 먼저 각 애플리케이션에 대한 URL을 한 개 이상 구성해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 "파일만" 모드(즉, 설치 마법사의 보고서 서버 설치 옵션 페이지에서 **서버 구성 없이 설치** 옵션을 선택한 경우)에서 설치한 경우에는 URL을 반드시 구성해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 기본 구성으로 설치한 경우 각 애플리케이션에 대해 URL이 이미 구성되어 있습니다. 보고서 서버가 SharePoint 통합 모드를 사용하도록 구성되어 있고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 보고서 서버 웹 서비스 URL을 업데이트하는 경우 SharePoint 중앙 관리에서도 URL을 업데이트해야 합니다.  
  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하면 URL을 구성할 수 있습니다. URL의 모든 부분이 이 도구에 정의되어 있습니다. 이전 릴리스와는 달리 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 이상 버전에서는 IIS(인터넷 정보 서비스) 웹 사이트에서 더 이상 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 애플리케이션에 액세스할 수 없습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 다른 웹 서비스 및 응용 프로그램과의 병렬 배포를 비롯 하 여 대부분의 배포 시나리오에서 잘 작동 하는 기본값을 제공 합니다. 기본 URL은 인스턴스 이름을 통합함으로써 같은 컴퓨터에서 보고서 서버 인스턴스를 여러 개 실행하는 경우 URL이 충돌할 위험을 최소화합니다.  
  
 이 항목에서는 다음 태스크에 대한 지침을 제공합니다.  
  
-   보고서 서버 웹 서비스 URL 만들기  
  
-   보고서 관리자 URL 만들기  
  
-   추가 URL을 정의하는 고급 URL 속성 설정  
  
 Url을 저장 하 고 유지 관리 하는 방법에 대 한 자세한 내용 및 상호 운용성 문제에 대 한 자세한 내용은 온라인 설명서의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Url 예약 및 등록 &#40;ssrs Configuration Manager&#41;](about-url-reservations-and-registration-ssrs-configuration-manager.md) 및 [설치 Reporting Services 및 인터넷 정보 서비스 함께 ssrs 기본 모드 ](install-reporting-and-internet-information-services-side-by-side.md)&#40;을 참조 하세요. Reporting Services 설치에 자주 사용되는 URL에 대한 예를 검토하려면 이 항목에 포함된 [URL 예](#URLExamples) 를 참조하십시오.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 URL을 만들거나 수정하기 전에 다음 사항을 유념하십시오.  
  
-   보고서 서버 컴퓨터에서 로컬 관리자 그룹의 멤버여야 합니다.  
  
-   IIS 6.0 또는 7.0이 같은 컴퓨터에 설치되어 있는 경우 포트 80을 사용하는 웹 사이트의 가상 디렉터리 이름을 확인하십시오. 기본 Reporting Services 가상 디렉터리 이름("Reports" 및 "ReportServer")을 사용하는 가상 디렉터리가 존재하는 경우 구성할 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL에 대해 다른 가상 디렉터리 이름을 선택합니다.  
  
-   
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 URL을 구성해야 합니다. 시스템 유틸리티를 사용하지 마십시오. RSReportServer.config 파일의 `URLReservations` 섹션에서 URL 예약을 직접 수정하지 마십시오. 내부에 저장된 기본 URL 예약을 업데이트하고 RSReportServer.config 파일에 저장된 URL 설정을 동기화하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용해야 합니다.  
  
-   보고서 작업이 적은 시간을 선택합니다. URL 예약이 변경될 때마다 보고서 서버 웹 서비스 및 보고서 관리자에 대한 애플리케이션 도메인이 재활용될 수 있습니다.  
  
-   
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 URL 생성 및 사용에 대한 개요는 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](configure-report-server-urls-ssrs-configuration-manager.md)을 참조하세요.  
  
### <a name="to-configure-a-url-for-the-report-server-web-service"></a>보고서 서버 웹 서비스 URL을 구성하려면  
  
1.  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작한 다음 로컬 보고서 서버 인스턴스에 연결합니다.  
  
2.  
  **웹 서비스 URL**을 클릭합니다.  
  
3.  가상 디렉터리를 지정합니다. 가상 디렉터리 이름으로 요청을 수신할 애플리케이션을 식별할 수 있습니다. IP 주소와 포트는 여러 애플리케이션에서 공유할 수 있으므로 가상 디렉터리 이름이 요청을 수신할 애플리케이션을 지정합니다.  
  
     요청이 원하는 대상에 도달하게 하려면 이 값이 고유해야 합니다. 이 값은 필수입니다. 대/소문자를 구분하지 않습니다. 가상 디렉터리 이름과 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 애플리케이션의 인스턴스는 일 대 일 대응됩니다. 같은 애플리케이션 인스턴스에 대한 URL을 여러 개 만든 경우 이 애플리케이션 인스턴스에 대해 정의한 모든 URL에 같은 가상 디렉터리 이름을 사용해야 합니다.  
  
     보고서 서버 웹 서비스의 기본 가상 디렉터리 이름은 **ReportServer**입니다.  
  
4.  네트워크에서 보고서 서버 컴퓨터를 고유하게 식별하는 IP 주소를 지정합니다. 호스트 헤더를 지정하거나 같은 애플리케이션 인스턴스에 대한 URL을 추가로 정의하려는 경우 **고급**을 클릭해야 합니다. 고급 URL 속성을 설정하는 방법은 이 항목의 뒷부분에 나오는 지침을 참조하십시오. 또는 **웹 서비스 URL** 페이지에서 다음 값 중 하나를 선택합니다.  
  
    -   **모두 할당** 됨-컴퓨터에 할당 된 모든 IP 주소를 보고서 서버 응용 프로그램을 가리키는 URL에 사용할 수 있도록 지정 합니다. 또한 이 값은 도메인 이름 서버에서 확인할 수 있는 호스트 이름(예: 컴퓨터 이름)부터 컴퓨터에 할당된 IP 주소까지 포함합니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL에 대한 기본값입니다.  
  
    -   **모두 할당 되지 않음** -다른 응용 프로그램에서 처리 하지 않은 모든 요청을 보고서 서버에서 수신 하도록 지정 합니다. 이 옵션은 사용하지 않는 것이 좋습니다. 이 옵션을 선택하면 보다 강력한 URL 예약을 사용하는 다른 애플리케이션이 보고서 서버에서 처리해야 할 요청을 가로챌 수 있습니다.  
  
    -   **127.0.0.1** 은 localhost에 액세스 하는 데 사용 되는 IPv4 주소입니다. 보고서 서버 컴퓨터에 대한 로컬 관리를 지원합니다. 이 값만 선택할 경우 보고서 서버 컴퓨터에 로컬로 로그온한 사용자만 애플리케이션에 액세스할 수 있습니다.  
  
    -   **:: 1** -IPv6 형식의 루프백 주소입니다.  
  
    -   특정 IP 주소가 이 목록에 표시될 수도 있습니다. IP 주소는 IPv4 및 IPv6 형식일 수 있습니다. *Nnn* . nnn. nnn. nnn은 컴퓨터에 있는 네트워크 어댑터 카드의 32 비트 IPv4 주소입니다. IPv6 주소는 128비트이며 8개의 4바이트 필드가 콜론으로 구분되어 있습니다. \<prefix>:*nnnn:nnnn:nnnn:nnnn:nnnn:nnnn*  
  
         카드가 여러 개 있거나 네트워크에서 IPv4와 IPv6 주소를 모두 지원하는 경우 IP 주소가 여러 개 표시됩니다. IP 주소를 한 개만 선택할 경우 선택한 IP 주소(및 도메인 이름 서버가 이 IP 주소에 매핑한 호스트 이름)만 애플리케이션에 액세스할 수 있습니다. localhost를 사용하여 보고서 서버에 액세스할 수 없으며, 보고서 서버 컴퓨터에 설치된 다른 네트워크 어댑터 카드의 IP 주소를 사용할 수 없습니다. 일반적으로 이 값을 선택하는 경우는 명시적 IP 주소 또는 호스트 이름도 지정하는 URL 예약을 여러 개 구성하고 있기 때문입니다. 예를 들면 한 개는 인트라넷 연결에 사용되는 네트워크 어댑터 카드용으로, 다른 한 개는 익스트라넷 연결에 사용되는 네트워크 어댑터 카드용으로 구성할 수 있습니다.  
  
5.  포트를 지정합니다. 포트 80은 다른 애플리케이션과 공유할 수 있기 때문에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 Windows Server 2008에서 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 에 대한 기본 포트는 포트 80입니다. 사용자 지정 포트 번호를 사용하려는 경우에는 보고서 서버에 액세스할 때 사용되는 URL에 항상 포트 번호를 지정해야 합니다. 사용 가능한 포트를 찾을 때 사용할 수 있는 기술은 다음과 같습니다.  
  
    -   명령 프롬프트에서 사용 중인 TCP 포트를 반환하는 다음 명령을 입력합니다.  
  
         `netstat -a -n -p tcp`  
  
    -   Microsoft 고객 지원 문서 [TCP/IP 포트 할당에 대한 정보](https://support.microsoft.com/kb/174904)에서 TCP 포트 할당 및 잘 알려진 포트(0 - 1023), 등록된 포트(1024 - 49151), 동적 또는 프라이빗 포트(49152 - 65535) 간의 차이를 검토합니다.  
  
    -   Windows 방화벽을 사용하고 있는 경우 포트를 열어야 합니다. 자세한 내용은 [Configure a Firewall for Report Server Access](../report-server/configure-a-firewall-for-report-server-access.md)를 참조하세요.  
  
6.  아직 확인하지 않은 경우 사용하려는 이름과 동일한 가상 디렉터리 이름을 IIS(설치된 경우)에서 사용하고 있지 않은지 확인합니다.  
  
7.  SSL 인증서를 설치한 경우 지금 이 인증서를 선택하여 컴퓨터에 설치된 SSL 인증서에 URL을 바인딩할 수 있습니다.  
  
8.  SSL 인증서를 선택하면 선택적으로 사용자 지정 포트를 지정할 수 있습니다. 기본 포트는 443이지만 사용 가능한 포트라면 모두 사용할 수 있습니다.  
  
9. 
  **적용** 을 클릭하여 URL을 만듭니다.  
  
10. 페이지의 **URL** 섹션에 있는 링크를 클릭하여 URL을 테스트합니다. URL을 테스트하려면 먼저 보고서 서버 데이터베이스를 만들어 구성해야 합니다. 자세한 내용은 [기본 모드 보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](ssrs-report-server-create-a-native-mode-report-server-database.md)를 참조하세요.  
  
11. 또한 보고서 서버가 SharePoint 통합 모드를 사용하도록 구성된 경우 SharePoint 중앙 관리에서 보고서 서버 웹 서비스 URL을 구성합니다. SharePoint 중앙 관리에서 보고서 서버 웹 서비스 URL을 업데이트 하는 방법에 대 한 자세한 내용은 sharepoint 모드 [&#41;Reporting Services 보고서 서버의 구성 및 관리 &#40;](../configure-administer-report-server-reporting-services-sharepoint-mode.md) 하 고 [보고서 서버 &#40;sharepoint 모드&#41;를 Reporting Services ](../reporting-services-report-server-sharepoint-mode.md).  
  
### <a name="to-create-a-url-reservation-for-report-manager"></a>보고서 관리자에 대한 URL 예약을 만들려면  
  
1.  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작한 다음 보고서 서버 인스턴스에 연결합니다.  
  
2.  
  **보고서 관리자 URL**을 클릭합니다.  
  
3.  가상 디렉터리를 지정합니다. 보고서 관리자는 보고서 서버 웹 서비스와 동일한 IP 주소와 포트를 수신합니다. 다른 보고서 서버 웹 서비스를 가리키도록 보고서 관리자를 구성한 경우 RSReportServer.config 파일에서 보고서 관리자 URL 설정을 수정해야 합니다. 지침은 온라인 설명서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 [&#41;보고서 관리자 &#40;기본 모드 구성](../report-server/configure-web-portal.md) 을 참조 하세요.  
  
4.  SSL 인증서를 설치한 경우 지금 이 인증서를 선택하여 보고서 관리자에 대한 모든 요청이 HTTPS를 통해 라우팅되도록 할 수 있습니다.  
  
     SSL 인증서를 선택하면 선택적으로 사용자 지정 포트를 지정할 수 있습니다. 기본 포트는 443이지만 사용 가능한 포트라면 모두 사용할 수 있습니다.  
  
5.  
  **적용** 을 클릭하여 URL을 만듭니다.  
  
6.  페이지의 **URL** 섹션에 있는 링크를 클릭하여 URL을 테스트합니다.  
  
## <a name="setting-advanced-properties-to-specify-additional-urls"></a>추가 URL을 지정하는 고급 속성 설정  
 포트 또는 호스트 이름(도메인 이름 서버가 컴퓨터에 할당된 IP 주소로 확인할 수 있는 호스트 헤더 이름 또는 IP 주소)을 여러 개 지정하여 보고서 서버 웹 서비스 또는 보고서 관리자에 대한 URL을 여러 개 예약할 수 있습니다. URL을 여러 개 만들면 같은 보고서 서버 인스턴스에 대해 서로 다른 액세스 경로를 설정할 수 있습니다. 예를 들어 보고서 서버에 대한 인트라넷 및 익스트라넷 액세스가 사용 가능하도록 하기 위해 다음과 같이 인트라넷을 통한 액세스에 대해서는 기본 URL을 사용하고 익스트라넷 액세스에 대해서는 정규화된 추가 호스트 이름을 사용할 수 있습니다.  
  
-   http://myserver01/reportserver  
  
-   http://www.adventure-works.com/reportserver  
  
 같은 애플리케이션 인스턴스에 대해서는 가상 디렉터리 이름을 여러 개 설정할 수 없습니다. 각 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 애플리케이션 인스턴스는 한 개의 가상 디렉터리 이름에 매핑됩니다. 같은 컴퓨터에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스가 여러 개 있는 경우 각 요청이 원하는 대상에 도달하게 하려면 애플리케이션에 대한 가상 디렉터리 이름에 인스턴스 이름이 포함되어 있어야 합니다.  
  
#### <a name="to-set-advanced-properties-on-a-url"></a>고급 URL 속성을 설정하려면  
  
1.  
  **웹 서비스 URL** 또는 **보고서 관리자 URL** 페이지에서 **고급**을 클릭합니다.  
  
2.  **추가**를 클릭합니다.  
  
3.  IP 주소 또는 호스트 헤더 이름을 클릭합니다. 호스트 헤더를 지정한 경우 DNS 서비스가 확인할 수 있는 이름을 지정해야 합니다. 공용으로 사용 가능한 도메인 이름을 지정한 경우 http://www를 포함한 전체 URL을 포함시킵니다.  
  
4.  포트를 지정합니다. 사용자 지정 포트를 지정한 경우 애플리케이션 URL에 항상 포트 번호가 포함되어야 합니다.  
  
5.  **확인**을 클릭합니다.  
  
6.  브라우저 창을 열고 URL을 입력하여 URL을 테스트합니다.  
  
## <a name="urls-for-multiple-report-server-instances-on-the-same-computer"></a>같은 컴퓨터에 있는 여러 보고서 서버 인스턴스에 대한 URL  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 여러 인스턴스에 대한 URL을 예약할 경우 이름이 충돌하지 않도록 다음 명명 규칙을 따라야 합니다. 자세한 내용은 [다중 인스턴스 보고서 서버 배포를 위한 URL 예약&#40;SSRS 구성 관리자&#41;](url-reservations-for-multi-instance-report-server-deployments.md)을 참조하세요.  
  
##  <a name="URLExamples"></a>URL 구성의 예  
 다음 목록에서는 보고서 서버 URL의 예를 보여 줍니다.  
  
-   http://localhost/reportserver  
  
-   http://localhost/reportserver_SQLEXPRESS  
  
-   http://sales01/reportserver  
  
-   http://sales01:8080/reportserver  
  
-   https://sales.adventure-works.com/reportserver  
  
-   https://www.adventure-works.com:8080/reportserver01  
  
 보고서 관리자에 액세스하는 데 사용하는 URL은 비슷한 형식으로 구성되며 일반적으로 보고서 서버를 호스팅하는 동일한 웹 사이트에서 생성됩니다. 가상 디렉터리 이름만 다릅니다. 이 경우에는 **reports** 이지만 원하는 이름으로 구성할 수 있습니다.  
  
-   http://localhost/reports  
  
-   http://localhost/reports_SQLEXPRESS  
  
-   http://sales01/reports  
  
-   http://sales01:8080/reports  
  
-   https://sales.adventure-works.com/reports  
  
-   https://www.adventure-works.com:8080/reports  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
