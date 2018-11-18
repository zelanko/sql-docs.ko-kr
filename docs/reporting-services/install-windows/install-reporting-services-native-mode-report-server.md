---
title: Reporting Services 2016 기본 모드 보고서 서버 설치 | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ac129843dafffbc53c32f639e0ed1113d53eec6b
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51813666"
---
# <a name="install-reporting-services-2016-native-mode-report-server"></a>Reporting Services 2016 기본 모드 보고서 서버 설치

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 기본 모드로 설치하는 방법을 알아 봅니다. 이 보고서 및 기타 항목을 관리할 수 있는 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 에 대한 액세스 권한을 제공합니다.

> [!NOTE]
> Power BI Report Server를 찾고 있나요? [Power BI Report Server 설치](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/)를 참조하세요.

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 보고서 서버는 기본 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서버 모드이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사 또는 명령줄에서 설치할 수 있습니다. 설치 마법사에서 파일을 설치하고 기본 설정을 사용하여 서버를 구성하거나 파일 설치만 하도록 선택할 수 있습니다. 이 항목에서는 설치 프로그램이 보고서 서버 인스턴스를 설치하고 구성하는 *기본 모드용 기본 구성* 을 검토합니다. 설치가 완료되면 보고서 서버가 실행되고 기본 보고서 보기 및 보고서 관리에 사용할 준비가 됩니다.  구독 처리와 함께 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 통합 및 메일 배달과 같은 추가 기능에는 추가 구성이 필요합니다.  
  
##  <a name="bkmk_whatisdefaultconfiguration"></a> 기본 구성이란?  
 기본 모드 옵션에 대해 기본 구성을 선택하면 다음과 같은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능이 설치됩니다.  
  
-   보고서 서버 서비스(보고서 서버 웹 서비스, 백그라운드 처리 응용 프로그램, 보고서 및 권한을 보고 관리하는 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 포함)  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 명령줄 유틸리티(rsconfig.exe, rskeymgmt.exe 및 rs.exe).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 및 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 이 이제 별도로 다운로드됩니다.  
  
 기본 모드 보고서 서버 설치에 대해 구성되는 항목은 다음과 같습니다.  
  
-   보고서 서버 서비스 계정  
  
-   보고서 서버 웹 서비스 URL  
  
-   [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] URL입니다.  
  
-   보고서 서버 데이터베이스  
  
-   보고서 서버 데이터베이스에 대한 서비스 계정 액세스  
  
-   DSN(데이터 원본 이름)이라고도 하는 보고서 서버 데이터베이스에 대한 연결 정보입니다.  
  
 설치 프로그램은 무인 실행 계정, 보고서 서버 전자 메일, 암호화 키 백업 또는 스케일 아웃 배포는 구성하지 않습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 이러한 속성을 구성할 수 있습니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)을 참조하세요.
  
##  <a name="bkmk_whentoinstalldefaultconfig"></a> 기본 모드용 기본 구성을 설치하는 경우  
 기본 구성은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 작동 상태로 설치하므로 설치가 완료되면 보고서 서버를 즉시 사용할 수 있습니다. 필수 구성 태스크를 생략하여 단계를 줄이려는 경우 이 모드를 지정하세요. 그렇지 않을 경우 이 필수 구성 태스크는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구에서 수행해야 합니다.  
  
 기본 구성을 설치해도 설치가 완료된 후 보고서 서버가 완전하게 작동하지 않을 수 있습니다. 따라서 서비스가 시작되어도 기본 URL이 등록되지 않을 수 있습니다. 서비스가 실행되어 예상대로 작동하는지 항상 설치를 테스트하세요.  [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)을 참조하세요.
  
##  <a name="bkmk_requirements"></a> 요구 사항  
 이 기본 구성 옵션은 기본값을 사용하여 보고서 서버 작동에 필요한 핵심 설정을 구성합니다. 요구 사항은 다음과 같습니다.  
  
-   [Hardware and Software Requirements for Installing SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md) 을 검토합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 같은 인스턴스에 함께 설치해야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스는 설치 프로그램에서 만들어 구성한 보고서 서버 데이터베이스를 호스팅합니다.  
  
-   설치 프로그램을 실행하는 데 사용된 사용자 계정은 로컬 Administrators 그룹에 속해야 하고, 보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 데이터베이스에 액세스하고 이러한 데이터베이스를 만들 수 있는 권한이 있어야 합니다.  
  
-   설치 프로그램은 기본값을 사용하여 보고서 서버와 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]에 액세스할 수 있는 URL을 예약할 수 있어야 합니다. 이러한 값은 포트 80, 강력한 와일드카드, **ReportServer_\<***instance_name***>** 및 **Reports_\<***instance_name***>** 형식의 가상 디렉터리 이름입니다.  
  
-   설치 프로그램은 기본값을 사용하여 보고서 서버 데이터베이스를 만들 수 있어야 합니다. 기본값은 **ReportServer** 및 **ReportServerTempDB**입니다. 이전에 설치한 기존 데이터베이스가 있는 경우 보고서 서버를 기본 모드용 기본 구성으로 구성할 수 없으므로 설치 프로그램이 차단됩니다. 설치 프로그램의 차단을 해제하려면 데이터베이스의 이름을 바꾸거나 데이터베이스를 이동 또는 삭제해야 합니다.  
  
 컴퓨터가 기본 설치에 대한 모든 요구 사항에 맞지 않는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 파일만 모드로 설치한 다음 설치가 완료된 후 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 구성해야 합니다.
 
 > [!IMPORTANT]
 > Reporting Services를 RODC(읽기 전용 도메인 컨트롤러)가 있는 환경에서 설치할 수 있는 동안 Reporting Services는 기능을 제대로 작동하기 위해 읽기 전용 도메인 컨트롤러에 대한 액세스가 필요합니다. Reporting Services에 RODC에 대한 액세스만 있는 경우 서비스를 관리하려고 할 때 오류가 발생할 수 있습니다.
  
##  <a name="bkmk_defaultURLreservations"></a> 기본 URL 예약  
 URL 예약은 접두사, 호스트 이름, 포트 및 가상 디렉터리로 구성됩니다.  
  
|부분|설명|  
|----------|-----------------|  
|접두사|기본 접두사는 HTTP입니다. 이전에 SSL(Secure Sockets Layer) 인증서를 설치한 경우 설치 프로그램에서 HTTPS 접두사를 사용하는 URL 예약을 만들려고 시도합니다.|  
|호스트 이름|기본 호스트 이름은 강력한 와일드카드(+)로서 보고서 서버가 `https://<computername>/reportserver`, `https://localhost/reportserver` 또는 `https://<IPAddress>/reportserver`를 포함하여 컴퓨터로 확인되는 모든 호스트 이름에 대해 지정된 포트에서 HTTP 요청을 수락하도록 지정합니다.|  
|포트|기본 포트는 80입니다. 80 이외의 포트를 사용하는 경우 브라우저 창에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 응용 프로그램을 열 때 URL에 해당 포트를 명시적으로 추가해야 합니다.|  
|가상 디렉터리|기본적으로 가상 디렉터리는 보고서 서버 웹 서비스의 경우 ReportServer_\<*instance_name*> 형식으로, [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]의 경우 Reports_\<*instance_name*> 형식으로 만들어집니다. 보고서 서버 웹 서비스의 기본 가상 디렉터리는 **reportserver**이고 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]의 기본 가상 디렉터리는 **reports**입니다.|  
  
 전체 URL 문자열의 예는 다음과 같습니다.  
  
-   `https://+:80/reportserver`, 보고서 서버에 대한 액세스를 제공합니다.  
  
-   `https://+:80/reports`, [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]에 대한 액세스를 제공합니다.
  
##  <a name="bkmk_installwithwizard"></a> SQL Server 설치 마법사로 기본 모드 설치  
 다음 목록에서는 SQL Server 설치 마법사에서 선택하는  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 특정 단계와 옵션에 대해 설명합니다. 설치 마법사에 표시될 각 페이지가 아니라 기본 모드 설치에 포함된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 관련 페이지에 대해서만 설명합니다.  
  
1.  SQL Server 설치 마법사(setup.exe)를 실행하고 다음 예비 페이지를 단계별로 실행합니다.  
  
    -   제품 키  
  
    -   사용 조건  
  
    -   전역 규칙  
  
    -   Microsoft Update  
  
    -   제품 업데이트  
  
    -   설치 정보 파일 설치  
  
    -   설치 규칙  
  
2.  **설치 역할** 페이지에서 **SQL Server 기능 설치**를 선택합니다.  
  
     ![설치 역할을 위한 SQL Server 기능 설치](../../reporting-services/install-windows/media/rs-setuprole.png "설치 역할을 위한 SQL Server 기능 설치")  
  
3.  **기능 선택** 페이지에서 다음을 선택합니다.  
  
    -   (1) 데이터베이스 엔진 인스턴스가 아직 설치되지 않은 경우 **데이터베이스 엔진 서비스**  
  
    -   (2) **Reporting Services-기본**  
  
     ![기능 선택에서 SSRS 기본 모드 선택](../../reporting-services/install-windows/media/rs-setupfeatureselection-native-withcircles.png "기능 선택에서 SSRS 기본 모드 선택")  
  
4.  통과한 **기능 규칙** 을 검토합니다.  
  
5.  인스턴스 구성 페이지에서 **명명된 인스턴스**를 구성하도록 선택한 경우 보고서 관리자 및 보고서 서버 자체를 탐색할 때 URLS에 인스턴스 이름을 사용해야 합니다. 인스턴스 이름이 "THESQLINSTANCE"인 경우 URLS는 다음과 같습니다.  
  
    -   `https://[ServerName]/ReportServer_THESQLINSTANCE`  
  
    -   `https://[ServerName]/Reports_THESQLINSTANCE`  
  
6.  **서버 구성**: [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독 기능을 사용하려는 경우 **서버 구성** 페이지에서 SQL Server 에이전트 **자동** 시작 유형을 구성합니다.   기본값은 수동입니다.  
  
7.  **데이터베이스 엔진 구성** 페이지에서 SQL Server 관리자를 추가합니다.  
  
8.  **Reporting Services 구성** 페이지에서 **설치 및 구성**을 선택합니다.  
  
     ![SSRS 기본 모드 구성](../../reporting-services/install-windows/media/rs-setupconfiguration-native-with-circles.png "SSRS 기본 모드 구성")  
  
    > [!NOTE]  
    >  데이터베이스 기능을 설치하도록 선택하지 않으면**설치 및 구성** 도 사용할 수 없습니다.  
  
9. 기능 구성 규칙: 통과한 규칙을 확인합니다. 규칙을 모두 통과하면 설치 마법사가 **설치 준비** 로 자동으로 진행합니다.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]와 관련하여, 이 규칙은 보고서 서버 카탈로그와 임시 카탈로그 데이터베이스가 아직 존재하지 않는지 확인합니다.  
  
10. **설치 준비** 페이지에서 구성 파일에 대한 경로를 나중에 참조할 수 있도록 메모해 둡니다. 이 정보는 설치된 구성 요소, 서비스 계정 및 관리자를 포함한 서버 초기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성에 대한 적절한 요약으로 활용합니다.  
  
11. SQL Server 설치 마법사를 완료한 후에 다음과 같은 기본 단계를 사용하여 기본 모드 설치를 확인합니다.  
  
    -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 열고 보고서 서버에 연결할 수 있는지 확인합니다.  
  
    -   **관리자 권한을 가진** 브라우저를 열고 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]에 연결합니다. 예를 들어 `https://localhost/Reports`입니다.  
  
    -   관리자 권한을 가진 브라우저를 열고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 페이지에 연결합니다. 예:  `https://localhost/ReportServer`  
  
 자세한 내용은 다음 두 항목의 기본 섹션을 참조하세요.  
  
 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
  
 [Reporting Services 설치 문제 해결](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
  
##  <a name="bkmk_additional_configuration"></a> 기타 고려 사항  
  
-   보고서 항목을 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 대시보드에 고정할 수 있도록 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 통합을 구성하려면 [Power BI Report Server 통합](../../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)을 참조하세요.  
  
-   구독 처리에 대한 메일을 구성하려면 [메일 설정 - Reporting Services 기본 모드](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md) 및 [Reporting Services의 메일 배달](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)을 참조하세요.  
  
-   보고서 컴퓨터에서 액세스하여 보고서를 보고 관리할 수 있도록 웹 포털을 구성하려면 [보고서 서버 액세스를 위한 방화벽 구성](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 및 [원격 관리를 위한 보고서 서버 구성](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

[Reporting Services 설치 문제 해결](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
[Reporting Services 설치 확인](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[보고서 서버 서비스 계정 구성](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
[보고서 서버 URL 구성](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[보고서 서버 데이터베이스 연결 구성](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[파일만 설치&#40;Reporting Services&#41;](../../reporting-services/install-windows/files-only-installation-reporting-services.md)   
[보고서 서버 초기화](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
[기본 모드 보고서 서버에서 SSL 연결 구성](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)   
[Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
