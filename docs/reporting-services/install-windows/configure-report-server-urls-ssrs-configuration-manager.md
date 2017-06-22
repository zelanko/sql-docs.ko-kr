---
title: "보고서 서버 Url (SSRS 구성 관리자) 구성 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Report Server Windows service, virtual directories
- report servers [Reporting Services], virtual directories
- virtual directories [Reporting Services]
- Report Manager [Reporting Services], virtual directories
ms.assetid: a0134ef0-086c-443e-93b9-7213a3d76393
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9e69b9e38fde1183d4bd77b7759faf25b6a4ec50
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="configure-report-server-urls--ssrs-configuration-manager"></a>보고서 서버 URL 구성(SSRS 구성 관리자)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 URL은 보고서 서버 웹 서비스 및 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]에 액세스하는 데 사용됩니다. 응용 프로그램을 사용하려면 먼저 웹 서비스와 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]마다 적어도 한 개의 URL을 구성해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 다른 웹 서비스와 응용 프로그램을 함께 배포하는 경우를 비롯한 대부분의 배포 시나리오에서 잘 작동하는 두 응용 프로그램 URL에 대한 기본값을 제공합니다.  
  
-   기본 구성을 설치한 경우 URL이 기본값을 사용하여 자동으로 생성됩니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 URL을 만들거나 수정하는 경우 URL에 대한 기본값을 그대로 사용하거나 사용자 지정 값을 지정할 수 있습니다. URL을 정의할 때 URL 테스트 링크가 페이지에 표시되므로 지정한 설정으로 올바르게 연결되는지 즉시 확인할 수 있습니다. URL을 구성하고 테스트하는 방법에 대한 단계별 지침은 [URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)에 액세스하는 데 사용됩니다.  
  
## <a name="defining-a-report-server-url"></a>보고서 서버 URL 정의  
 URL을 통해 네트워크에 있는 보고서 서버 응용 프로그램 인스턴스의 위치를 정확하게 식별할 수 있습니다. 보고서 서버 URL을 만들 때 다음 부분을 지정해야 합니다.  
  
|부분|설명|  
|----------|-----------------|  
|호스트 이름|TCP/IP 네트워크는 IP 주소를 사용하여 네트워크에 있는 장치를 고유하게 식별합니다. 물리적 IP 주소는 컴퓨터에 설치된 네트워크 어댑터 카드당 한 개가 있습니다. IP 주소가 호스트 헤더로 확인되면 호스트 헤더를 지정할 수 있습니다. 보고서 서버를 회사 네트워크에 배포하는 경우 컴퓨터의 네트워크 이름을 사용할 수 있습니다.|  
|포트|TCP 포트는 장치의 끝점입니다. 보고서 서버는 지정된 포트에서 요청을 수신합니다.|  
|가상 디렉터리|포트는 종종 여러 웹 서비스나 응용 프로그램에서 공유할 수 있습니다. 따라서 보고서 서버 URL에는 요청을 가져오는 응용 프로그램에 해당하는 가상 디렉터리가 항상 포함되어야 합니다. 같은 IP 주소와 포트를 수신하는 각각의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 응용 프로그램에 대해 고유한 가상 디렉터리 이름을 지정해야 합니다.|  
|SSL 설정|이전에 컴퓨터에 설치한 기존 SSL 인증서를 사용하도록 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 URL을 구성할 수 있습니다. 자세한 내용은 [온라인 설명서의](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) 기본 모드 보고서 서버에서 SSL 연결 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.|  
  
## <a name="default-urls"></a>기본 URL  
 URL을 통해 보고서 서버 또는 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 에 액세스하는 경우 URL에는 IP 주소가 아닌 호스트 이름이 포함되어야 합니다. TCP/IP 네트워크에서는 IP 주소가 호스트 이름(또는 컴퓨터의 네트워크 이름)으로 확인됩니다. 기본값을 사용하여 URL을 구성한 경우 다음과 같이 컴퓨터 이름 또는 localhost가 호스트 이름으로 지정된 URL을 사용하여 보고서 서버 웹 서비스에 액세스할 수 있어야 합니다.  
  
-   `http://<computername>/reportserver`  
  
-   `http://localhost/reportserver`  
  
 이러한 URL을 사용 가능하게 만드는 설정은 다음 표에 나와 있습니다. 이 표에서는 호스트 이름을 포함하는 URL을 통해 보고서 서버 연결을 가능하게 하는 기본값을 보여 줍니다.  
  
|부분|값|설명|  
|----------|-----------|-----------------|  
|IP 주소|모두 할당됨|네트워크의 도메인 이름 서비스는 URL의 호스트 이름을 컴퓨터의 IP 주소로 확인합니다. 정의한 URL에 IP 주소가 지정되어 있으면 한 특정 호스트로 전송된 요청이 원하는 대상에 도달합니다.|  
|포트|80|포트 80은 컴퓨터에 있는 TCP/IP 연결의 기본 포트입니다. 보고서 서버는 포트 80에서 수신하므로 URL에서 포트 번호를 생략할 수 있습니다. 다른 포트를 지정할 경우에는 URL에 포트를 지정해야 합니다.|  
|가상 디렉터리|ReportServer|두 URL 예에는 가상 디렉터리 이름이 포함되어 있습니다. URL 정의를 사용자 지정하지 않는 한 응용 프로그램의 가상 디렉터리 이름을 항상 URL에 지정해야 합니다.|  
  
> [!NOTE]  
>  기본 URL 예약을 사용하면 유효한 호스트 이름이 URL에 사용됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구는 변형된 호스트 이름을 특정 보고서 서버 인스턴스로 확인할 수 있는 구문을 사용하여 HTTP.SYS에 URL 예약을 만듭니다. URL 예약에 대한 자세한 내용은 [URL 예약 및 등록 정보&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)에 액세스하는 데 사용됩니다.  
  
## <a name="server-side-permissions-on-a-report-server-url"></a>보고서 서버 URL에 대한 서버 쪽 사용 권한  
 각 URL 끝점에 대한 사용 권한은 보고서 서버 서비스 계정에 배타적으로 부여됩니다. 따라서 이 계정만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL로 전송된 요청을 받아들일 수 있습니다. 설치 프로그램 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 통해 서비스 ID를 구성할 경우 해당 계정에 대한 DACL(Discretionary Access Control List)이 생성되어 유지 관리됩니다. 서비스 계정을 변경하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구가 새 계정 정보를 선택하기 위해 만든 모든 URL 예약을 업데이트합니다. 자세한 내용은 [URL 예약 구문&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)에 액세스하는 데 사용됩니다.  
  
## <a name="authenticating-client-requests-sent-to-a-report-server-url"></a>보고서 서버 URL로 전송된 클라이언트 요청 인증  
 기본적으로 URL 끝점에서 지원되는 인증 유형은 Windows 인증으로 이는 기본 보안 확장 프로그램입니다. 사용자 정의 또는 폼 인증 공급자를 구현하는 경우 보고서 서버에서 인증 설정을 수정해야 합니다. 선택적으로 네트워크에 사용된 인증 하위 시스템과 일치하도록 Windows 인증 설정을 변경할 수도 있습니다. 자세한 내용은 [온라인 설명서의](../../reporting-services/security/authentication-with-the-report-server.md) 보고서 서버 인증 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
 이 항목에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구에서 URL 예약을 설정하고 구성하는 지침을 제공합니다.  
  
 [URL 예약 및 등록 정보&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)  
 URL은 응용 프로그램과 보고서에 액세스하는 데 사용됩니다. 이 항목에서는 응용 프로그램 URL, 기본 URL, URL 예약 및 등록이 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 작동하는 방식에 대해 설명합니다.  
  
 [URL 예약 구문&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 사용하는 기본 URL 예약은 대부분의 시나리오에 적합합니다. 그러나 액세스를 제한하거나 인터넷 또는 익스트라넷 액세스가 가능하도록 배포를 확장하려는 경우 요구 사항에 맞게 설정을 사용자 지정해야 할 수도 있습니다. 이 항목에서는 URL 예약 구문에 대해 설명하고 배포에 대한 사용자 지정 예약 만들기에 대한 권장 사항을 제공합니다.  
  
 [구성 파일의 URL&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)  
 RSReportServer.config 파일에는 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 가 사용하는 URL 예약과 URL 및 보고서 서버 메일 배달에 대한 여러 항목이 포함되어 있습니다. 이 항목에서는 URL 구성 설정이 비교되는 방식을 이해할 수 있도록 URL 구성 설정에 대해 간략하게 설명합니다.  
  
 [다중 인스턴스 보고서 서버 배포를 위한 URL 예약&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md)  
 단일 컴퓨터에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스를 여러 개 설치할 경우 URL을 등록할 때 URL이 중복될 가능성이 높아집니다. 이러한 오류를 피하려면 이 항목에 설명된 인스턴스별 URL 예약 만들기에 대한 권장 사항을 따르십시오.  
  
## <a name="see-also"></a>참고 항목  
 [URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 

