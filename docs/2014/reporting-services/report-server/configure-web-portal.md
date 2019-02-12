---
title: 보고서 관리자 (기본 모드) 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 005c9fe0ff5ba3f998e80a93ea19d85c87331403
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028585"
---
# <a name="configure-report-manager-native-mode"></a>보고서 관리자 구성(기본 모드)
  보고서 관리자는 보고서를 확인하고 보고서 서버 내용을 관리하며 사용자에게 기본 모드 보고서 서버에 대한 액세스 권한을 부여하는 데 사용되는 웹 프런트 엔드 애플리케이션입니다. 보고서 관리자는 보고서 서버 웹 서비스와 동일한 보고서 서버 인스턴스 내에 설치되며 설치 시 **기본값인 기본 모드 구성으로 설치** 옵션을 선택하면 구성됩니다. 보고서 관리자를 사후 설치 태스크로 구성할 수도 있습니다. 이 항목에서는 다음과 같은 보고서 관리자 구성 시나리오에 대한 정보를 제공합니다.  
  
-   [기본 URL을 사용하도록 보고서 관리자 구성](#ConfigureRMURL)  
  
     보고서 관리자는 웹 브라우저에서 사용자가 액세스하는 웹 애플리케이션입니다. 적어도 브라우저 창에서 이 애플리케이션을 여는 데 사용되는 URL은 정의해야 합니다. URL은 호스트 이름, 포트 및 가상 디렉터리로 구성됩니다. 이 URL에 대한 기본값에는 보고서 서버 웹 서비스 URL에 대해 정의된 호스트 이름 및 포트 값과 **reports** 가상 디렉터리 이름이 포함됩니다. 명명된 인스턴스가 있을 경우 가상 디렉터리는 **reports_instance**입니다. 여기서 **instance** 는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스의 이름입니다.  
  
-   **원격 컴퓨터에서 보고서 관리자를 실행합니다**. 네트워크의 구성에 따라 보고서 관리자를 통해 컴퓨터의 포트 80을 사용하여 요청할 수 있어야 합니다.  
  
    > [!TIP]  
    >  원격 컴퓨터에서 보고서 관리자에 액세스할 때 브라우저에 연결 오류 메시지가 표시되는 경우 일반적으로 방화벽 설정이 원인입니다. 자세한 내용은 [보고서 서버 액세스를 위한 방화벽 구성](configure-a-firewall-for-report-server-access.md)을 참조하세요.  
  
     필요한 경우 두 컴퓨터 모두에서 포트 80을 설정하여 요청이 해당 포트를 통과하도록 할 수 있습니다. 자세한 내용은 [보고서 서버 액세스를 위한 방화벽 구성](configure-a-firewall-for-report-server-access.md)을 참조하세요.  
  
-   [특정 보고서 서버 URL을 사용하도록 보고서 관리자 구성](#ConfigureSpecificURL)  
  
     기본적으로 보고서 관리자는 동일한 보고서 서버 서비스에서 실행되는 보고서 서버 웹 서비스에 연결하며, 이때 보고서 서버 웹 서비스 URL을 사용합니다. 보고서 서버 웹 서비스에 대한 URL을 여러 개 정의한 경우 보고서 관리자는 사용자가 마지막으로 정의한 것을 사용합니다. 하지만 어떤 배포에서는 보고서 관리자가 항상 정적 URL을 통해 웹 서비스에 연결하도록 해야 합니다. 특정 포트 또는 IP 주소에 대한 패킷 필터링을 구성한 후 보고서 서버에 대한 모든 연결이 사용자가 정의한 필터 규칙을 통과하도록 하려는 경우를 예로 들 수 있습니다.  
  
-   [보고서 관리자를 원격 보고서 서버에 연결](#ConfigureRemoteRS)  
  
     기본적으로 보고서 관리자는 동일한 서버 인스턴스에서 실행되는 보고서 서버 웹 서비스에 대한 프런트 엔드 액세스를 제공하지만 웹 서비스와 보고서 관리자를 별도의 프로세스에서 실행하려는 경우 또는 각 서버에 대해 서버 액세스를 다르게 구성하려는 경우(예: 보고서 관리자를 익스트라넷 또는 인터넷상의 사용자에게 배포하고 보고서 서버와 보고서 관리자 사이에 방화벽을 두려는 경우) 보고서 관리자가 원격 보고서 서버 웹 서비스에 연결되도록 구성할 수 있습니다.  
  
-   [스타일 및 응용 프로그램 제목 사용자 지정](#ModifyTitle)  
  
     스타일을 변경하고 보고서 관리자에 표시되는 애플리케이션 제목을 편집하여 보고서 관리자, HTML 보고서 뷰어 및 보고서 도구 모음을 제한적인 방법으로 사용자 지정할 수 있습니다.  
  
-   [보고서 관리자 해제](#DisableRM)  
  
     기본 모드를 사용하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스를 설치하면 기본적으로 보고서 관리자가 설정됩니다. 그러나 동일한 기능을 제공하는 사용자 지정 프런트 엔드 애플리케이션이 있는 경우, SOAP 또는 URL 액세스 인터페이스만 사용하여 보고서 서버에 액세스하려는 경우 또는 보고서 관리자를 다른 보고서 서버 인스턴스에서 사용하려는 경우 보고서 관리자를 해제할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 보고서 관리자를 사용하려면 다음과 같은 전제 조건을 충족해야 합니다.  
  
-   최소한으로 구성된 보고서 서버가 있어야 합니다. 보고서 서버를 최소한으로 구성하는 방법은 [보고서 서버 구성&#40;Reporting Services 기본 모드&#41;](configure-a-report-server-reporting-services-native-mode.md)을 참조하세요.  
  
-   보고서 서버를 기본 모드로 실행해야 합니다. SharePoint 통합 모드로 구성된 보고서 서버에는 보고서 관리자를 사용할 수 없습니다. SQL Server 2012 에서는 보고서 서버를 한 모드에서 다른 모드로 전환할 수 없습니다. 환경에 사용되는 보고서 서버 유형을 변경하려면 원하는 보고서 서버 모드를 설치하고 보고서 항목을 새 보고서 서버로 복사하거나 이동해야 합니다. 이러한 프로세스를 일반적으로 '마이그레이션'이라고 합니다. 마이그레이션하는 데 필요한 단계는 마이그레이션할 모드 및 원본 버전에 따라 달라집니다. 자세한 내용은 [Upgrade and Migrate Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md)을 참조하세요.  
  
-   스크립팅이 사용되는 Internet Explorer 7.0 이상도 필요합니다. 자세한 내용은 [Reporting Services 및 파워 뷰 브라우저 지원 계획 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)합니다.  
  
##  <a name="ConfigureRMURL"></a> 기본 URL을 사용하도록 보고서 관리자 구성  
 기본적으로 보고서 관리자 URL은 고유한 가상 디렉터리 이름과 동일 인스턴스에서 실행되는 보고서 서버 웹 서비스에 대해 정의된 포트 및 호스트 이름으로 구성됩니다. 대부분의 경우 호스트 이름은 보고서 서버 컴퓨터의 네트워크 이름이지만 이 컴퓨터를 식별하는 IP 주소나 호스트 헤더가 될 수도 있습니다. 보고서 관리자가 기본 URL을 사용하도록 구성하려면 **구성 도구의** 보고서 관리자 URL [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지를 사용하십시오.  
  
#### <a name="to-configure-the-default-report-manager-url-and-virtual-directory"></a>기본 보고서 관리자 URL 및 가상 디렉터리를 구성하려면  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작한 다음 보고서 서버 인스턴스에 연결합니다.  
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구에서 **보고서 관리자 URL** 을 URL을 구성하는 데 사용되는 페이지를 엽니다.  
  
3.  보고서 관리자의 고유한 가상 디렉터리 이름을 입력합니다.  
  
4.  **적용**을 클릭합니다.  
  
5.  [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 또는 Windows Server 2008을 사용하는 경우 보고서 관리자를 사용하기 위해서는 추가 단계를 수행해야 할 수 있습니다. 자세한 내용은 [로컬 관리에 대해 기본 모드 보고서 서버 구성&#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)을 참조하세요.  
  
##  <a name="ConfigureSpecificURL"></a> 특정 보고서 서버 URL을 사용하도록 보고서 관리자 구성  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구에서 URL을 구성할 때 보고서 관리자는 동일한 서버 인스턴스에서 실행되는 보고서 서버에 대한 새 URL 및 업데이트된 URL을 자동으로 검색하여 사용합니다. 배포에서 모든 보고서 서버 요청에 대해 단일 정적 URL을 사용해야 하는 경우 RSReportServer.config 파일에 해당 URL을 지정하면 됩니다.  
  
#### <a name="to-configure-a-static-report-server-url"></a>정적 보고서 서버 URL을 구성하려면  
  
1.  텍스트 편집기에서 **RSReportServer.config** 파일을 엽니다. 기본적으로 이 파일은 \Program Files\Microsoft SQL Server\MSRS12.\<*instancename*>\Reporting Services\ReportServer에 있습니다.  
  
2.  `ReportServerURL` 찾기.  
  
3.  이 URL을 보고서 서버 인스턴스의 URL로 바꿉니다.  
  
4.  변경 내용을 저장하고 파일을 닫습니다.  
  
 구성 파일에 대 한 자세한 내용은 참조 하세요. [Reporting Services 구성 파일 수정 &#40;RSreportserver.config&#41; ](modify-a-reporting-services-configuration-file-rsreportserver-config.md) 하 고 [RSReportServer Configuration File](rsreportserver-config-configuration-file.md).  
  
##  <a name="ConfigureRemoteRS"></a> 원격 보고서 서버를 사용하도록 보고서 관리자 구성  
 보고서 관리자와 보고서 서버가 각기 다른 컴퓨터에 배치되는 배포 구성의 경우 두 컴퓨터에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 각각 설치해야 합니다. 보고서 관리자는 보고서 서버 서비스에 포함되어 있으므로 단독으로 설치할 수 없습니다. 보고서 관리자를 다른 컴퓨터에서 자체 프로세스로 실행하려면 두 번째 보고서 서버를 설치해야 합니다. 두 서버 인스턴스는 모두 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보고서 서버여야 합니다.  
  
#### <a name="to-connect-report-manager-to-a-remote-report-server-instance"></a>보고서 관리자를 원격 보고서 서버 인스턴스에 연결하려면  
  
1.  보고서 서버 인스턴스를 두 개 설치합니다.  
  
2.  보고서 서버를 호스팅할 첫 번째 설치를 구성합니다.  
  
    1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작합니다.  
  
    2.  **웹 서비스 URL** 을 클릭하여 보고서 서버에 대한 호스트 이름, 포트 및 가상 디렉터리를 구성합니다.  
  
    3.  **데이터베이스** 를 클릭하여 보고서 서버 데이터베이스를 구성합니다.  
  
3.  보고서 관리자를 호스팅할 두 번째 설치를 구성합니다.  
  
    1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작합니다.  
  
    2.  **보고서 관리자 URL** 을 클릭하여 보고서 관리자의 가상 디렉터리 이름을 입력합니다.  
  
     데이터베이스를 구성하거나 URL을 테스트하지 마십시오.  
  
4.  보고서 관리자 컴퓨터에서 RSReportServer.config의 구성 설정을 수정하여 원격 보고서 서버 인스턴스를 가리키도록 만듭니다. 시작할 때 보고서 관리자는 구성 파일을 읽어 보고서 서버에 대한 URL을 가져옵니다.  
  
    1.  텍스트 편집기에서 RSReportServer.config를 엽니다. 기본적으로 SQL Server\MSRS11 \Program Files\Microsoft에 있습니다. \< *instancename*> services\reportserver입니다.  
  
    2.  `ReportServerURL` 찾기.  
  
    3.  이 URL을 원격 보고서 서버 인스턴스의 URL로 바꿉니다.  
  
    4.  변경 내용을 저장하고 파일을 닫습니다.  
  
5.  > [!TIP]  
    >  필요한 경우 두 컴퓨터 모두에서 포트 80을 설정하여 요청이 해당 포트를 통과하도록 할 수 있습니다. 자세한 내용은 [보고서 서버 액세스를 위한 방화벽 구성](configure-a-firewall-for-report-server-access.md)을 참조하세요.  
  
6.  보고서 서버를 다시 시작합니다.  
  
7.  브라우저 창에서 보고서 관리자를 엽니다. 이미 열려 있었다면 브라우저를 새로 고쳐 보고서 관리자가 원격 서버에 연결되어 있는지 확인합니다. 대상 서버의 내용을 확인해야 합니다.  
  
8.  사용하지 않을 서버 기능을 해제합니다.  
  
    -   보고서 관리자 컴퓨터에서 `WebServiceAndHTTPAccessEnabled` 및 `ScheduleEventsAndReportDeliveryEnabled`를 해제합니다.  
  
    -   보고서 서버 컴퓨터에서 `ReportManagerEnabled`를 해제합니다.  
  
 기능 해제에 대한 자세한 내용은 [Reporting Services 기능 설정 또는 해제](turn-reporting-services-features-on-or-off.md)를 참조하세요.  
  
##  <a name="ModifyTitle"></a> 스타일 또는 응용 프로그램 제목 사용자 지정  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 보고서 관리자 스타일시트에 대한 사용자 지정을 지원하지 않습니다. 하지만 웹 개발에 대한 전문 지식이 있다면 스타일을 수정할 수 있습니다. 단, 이로 인해 발생하는 모든 문제에 대한 책임은 자신에게 있습니다. 스타일 정보가 포함된 파일에 대한 자세한 내용은 [HTML 뷰어 및 보고서 관리자에 대한 스타일시트 사용자 지정](../customize-style-sheets-for-html-viewer-and-report-manager.md)을 참조하세요.  
  
 보고서 관리자의 페이지 맨 위에는 애플리케이션 제목이 표시됩니다. 기본적으로 이 제목은 **SQL Server Reporting Services**이며 사용자 지정할 수 있습니다. 제목을 변경하려면 보고서 관리자의 사이트 설정 페이지를 사용합니다. 보고서 관리자에서 애플리케이션 설정을 수정하려면 사이트 설정 페이지에서 속성을 설정할 수 있는 **시스템 관리자** 역할에 할당되어 있어야 합니다. 애플리케이션 제목을 보려면 사용자가 **시스템 사용자** 역할에 할당되어 있어야 합니다.  
  
#### <a name="to-modify-application-title"></a>애플리케이션 제목을 수정하려면  
  
1.  보고서 서버에 대한 **시스템 관리자** 권한이 할당된 계정을 사용하여 로그온합니다.  
  
2.  Internet Explorer를 엽니다.  
  
3.  보고서 관리자 URL을 입력합니다. 기본적으로 이 URL은 http://\<**your-server-name**>/reports이지만 Reporting Services를 명명된 인스턴스로 설치한 경우 기본 URL은 http://\<**your-server-name**>/reports\<**_instancename**>입니다.  
  
4.  **사이트 설정**을 클릭합니다.  
  
5.  **일반** 탭의 **이름**에서 **SQL Server Reporting Services** 를 다른 이름으로 바꿉니다.  
  
6.  **적용**을 클릭합니다.  
  
##  <a name="DisableRM"></a> Turn Off Report Manager  
 동일한 기능을 제공하는 사용자 지정 애플리케이션이 있거나 다른 서비스 인스턴스의 보고서 관리자 애플리케이션을 사용하려는 경우 보고서 관리자를 해제할 수 있습니다. 보고서 관리자를 해제하려면 RSReportServer.config 파일을 수정하면 됩니다.  
  
#### <a name="to-turn-off-report-manager"></a>보고서 관리자를 해제하려면  
  
1.  텍스트 편집기에서 RSReportServer.config 파일을 엽니다. 기본적으로 SQL Server\MSRS11 \Program Files\Microsoft에 있습니다. \< *instancename*> services\reportserver입니다.  
  
2.  **IsReportManagerEnabled**를 찾습니다.  
  
3.  값을 **False**로 설정합니다.  
  
4.  변경 내용을 저장하고 파일을 닫습니다.  
  
 이 구성 파일을 수정하는 방법은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)을 참조하세요. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 기능을 사용하지 않도록 설정하는 방법은 [Reporting Services 기능 설정 또는 해제](turn-reporting-services-features-on-or-off.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)   
 [Reporting Services 및 파워 뷰 브라우저 지원 계획 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [URL 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Reporting Services 설치 확인](../install-windows/verify-a-reporting-services-installation.md)   
 [HTML 뷰어 및 보고서 관리자에 대한 스타일시트 사용자 지정](../customize-style-sheets-for-html-viewer-and-report-manager.md)   
 [Reporting Services 기능 설정 또는 해제](turn-reporting-services-features-on-or-off.md)   
 [Reporting Services 기본 모드 보고서 서버 관리](manage-a-reporting-services-native-mode-report-server.md)   
 [RSReportServer 구성 파일](rsreportserver-config-configuration-file.md)   
 [로컬 관리에 대해 기본 모드 보고서 서버 구성&#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
  
  
