---
title: '자습서: Reporting Services 도구를 찾고 시작하는 방법(SSRS) | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder 1.0, locating and starting tool
- Reporting Services, tutorials
- Reporting Services, tools
- Reporting Services Configuration tool
- Business Intelligence Development Studio, locating and starting tool
- Model Designer [Reporting Services], locating and starting tool
- Report Designer [Reporting Services], tutorials
- tools [Reporting Services]
- tutorials [Reporting Services]
- Report Manager [Reporting Services]
ms.assetid: 51ad69d8-fe92-4662-a7cd-d235692f0c03
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4edd0b6e3928a2bc3a280403a87eda5bb797e620
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099475"
---
# <a name="tutorial-how-to-locate-and-start-reporting-services-tools-ssrs"></a>자습서: Reporting Services 도구를 찾고 시작하는 방법
  이 자습서에서는 보고서 서버를 구성하고 보고서 서버 내용 및 작업을 관리하며 보고서를 만들어 게시하는 데 사용되는 도구를 소개합니다. 이 자습서를 통해 새 사용자는 각 도구를 찾고 여는 방법을 이해할 수 있습니다. 이미 이 도구에 익숙한 경우 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]를 사용하는 데 중요한 기술을 배울 수 있는 다른 자습서로 이동할 수 있습니다. 다른 자습서에 대 한 자세한 내용은 [SSRS&#41;&#40;Reporting Services 자습서 ](../reporting-services-tutorials-ssrs.md)를 참조 하세요.  
  
 이 항목의 내용:  
  
-   [Reporting Services 구성 관리자(기본 모드)](#bkmk_configuration_manager)  
  
-   [보고서 관리자(기본 모드)](#bkmk_report_manager)  
  
-   [Management Studio](#bkmk_managements_studio)  
  
-   [보고서 디자이너 및 보고서 마법사가 포함된 SQL Server Data Tools](#bkmk_ssdt)  
  
-   [보고서 작성기](#bkmk_report_builder)  
  
##  <a name="reporting-services-configuration-manager-native-mode"></a><a name="bkmk_configuration_manager"></a>Reporting Services 구성 관리자 (기본 모드)  
 기본 모드 구성 관리자를 사용하여 다음을 완료합니다.  
  
-   서비스 계정을 지정합니다.  
  
-   보고서 서버 데이터베이스를 만들거나 업그레이드합니다.  
  
-   연결 속성을 수정합니다.  
  
-   URL을 지정합니다.  
  
-   암호화 키를 관리합니다.  
  
-   무인 보고서 처리 및 전자 메일 보고서 배달을 구성합니다.  
  
 **설치:** [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 기본 모드를 설치할 때 함께 설치됩니다. 자세한 내용은 [Reporting Services 기본 모드 보고서 서버 설치](../install-windows/install-reporting-services-native-mode-report-server.md)를 참조하세요.  
  
#### <a name="to-start-the-reporting-services-configuration-manager"></a>Reporting Services 구성 관리자를 시작하려면  
  
1.  Windows 시작 화면에서를 입력 `reporting` 하 고 **앱** 검색 결과에서 **Reporting Services 구성 관리자**를 클릭 합니다.  
  
     ![Reporting Services 구성 관리자 시작](../media/bi-ssrs-configmanager-win8-startscreen.gif "Reporting Services 구성 관리자 시작")  
  
     **디스크나**  
  
     **시작**, **프로그램**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 클릭한 다음 **Reporting Services 구성 관리자**를 클릭합니다.  
  
     구성할 보고서 서버 인스턴스를 선택할 수 있도록 **보고서 서버 설치 인스턴스 선택** 대화 상자가 나타납니다.  
  
2.  **서버 이름**에 보고서 서버 인스턴스가 설치된 컴퓨터의 이름을 지정합니다. 기본적으로 로컬 컴퓨터의 이름이 지정되지만 원격 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 입력할 수도 있습니다.  
  
     원격 컴퓨터를 지정하는 경우 **찾기** 를 클릭하여 연결을 설정합니다. 미리 보고서 서버를 원격 관리용으로 구성해야 합니다. 자세한 내용은 [원격 관리를 위한 보고서 서버 구성](../report-server/configure-a-report-server-for-remote-administration.md)을 참조하세요.  
  
3.  **인스턴스 이름**에서 구성할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 인스턴스를 선택합니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]및 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보고서 서버 인스턴스만 목록에 나타납니다. 이전 버전의 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 구성할 수 없습니다.  
  
4.  **연결**을 클릭합니다.  
  
5.  도구가 시작되었는지 확인하려면 결과를 다음 이미지와 비교합니다.  
  
     ![Reporting Services 구성 도구](../media/rs-ui-reportserverconfigkatmai.gif "Reporting Services 구성 도구")  
  
 **다음 단계:** [보고서 서버 구성 및 관리&#40;SSRS 기본 모드&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md) 및 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
##  <a name="report-manager-native-mode"></a><a name="bkmk_report_manager"></a>보고서 관리자 (기본 모드)  
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md) 사용 하 여 사용 권한을 설정 하 고, 구독 및 일정을 관리 하 고, 보고서 작업을 수행할 수 있습니다. 보고서 관리자를 사용하여 보고서를 볼 수 있습니다.  
  
 **설치:** 보고서 관리자는 기본 모드를 설치할 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 때 설치 됩니다. [Reporting Services 기본 모드 보고서 서버 설치](../install-windows/install-reporting-services-native-mode-report-server.md)  
  
 보고서 관리자를 열려면 먼저 충분한 권한이 있어야 합니다. 처음에는 로컬 관리자 그룹의 멤버만 보고서 관리자 기능에 액세스할 수 있습니다. 보고서 관리자는 현재 사용자의 역할 할당에 따라 다양한 페이지와 옵션을 제공합니다. 사용 권한이 없는 사용자에게는 빈 페이지가 나타납니다. 보고서를 볼 권한이 있는 사용자에게는 클릭하여 보고서를 열 수 있는 링크가 나타납니다. 권한에 대한 자세한 내용은 [역할 및 권한&#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md)를 참조하세요.  
  
#### <a name="to-start-report-manager"></a>보고서 관리자를 시작하려면  
  
1.  브라우저를 엽니다. 지원 되는 브라우저 및 브라우저 버전에 대 한 자세한 내용은 [Reporting Services 계획 및 파워 뷰 브라우저 지원 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)을 참조 하세요.  
  
2.  웹 브라우저의 주소 표시줄에 보고서 관리자 URL을 입력합니다. 기본적으로 URL은 **Http://\<serverName>/reports**입니다. Reporting Services 구성 도구를 사용하여 서버 이름과 URL을 확인할 수 있습니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 사용되는 URL에 대한 자세한 내용은 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)를 참조하세요.  
  
3.  보고서 관리자가 브라우저 창에서 열립니다. 시작 페이지는 홈 폴더입니다. 사용 권한에 따라 추가 폴더, 보고서에 대한 하이퍼링크 및 시작 페이지 내의 리소스 파일을 볼 수 있습니다. 또한 도구 모음에서 추가적인 단추와 명령을 볼 수 있습니다.  
  
4.  로컬 보고서 서버에서 보고서 관리자를 실행 하는 경우 [로컬 관리에 대해 기본 모드 보고서 서버 구성 &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)를 참조 하세요.  
  
 **다음 단계:** [기본 모드&#41;&#40;보고서 관리자 구성 ](../report-server/configure-web-portal.md)합니다.  
  
##  <a name="management-studio"></a><a name="bkmk_managements_studio"></a> Management Studio  
 보고서 서버 관리자는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하여 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 요소 서버와 함께 보고서 서버를 관리할 수 있습니다. 자세한 내용은 [Use SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)을 참조하세요.  
  
#### <a name="to-start-sql-server-management-studio"></a>SQL Server Management Studio를 시작하려면  
  
1.  Windows 시작 화면에서를 입력 `sql server` 하 고 **앱** 검색 결과에서 **SQL Server Management Studio**를 클릭 합니다.  
  
     ![Windows 시작 화면의 Management Studio](../media/bi-ssms-win8-startscreen.gif "Windows 시작 화면의 Management Studio")  
  
     **디스크나**  
  
     **시작**, **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]를 차례로 클릭한 후 **SQL Server Management Studio**를 클릭합니다. **서버에 연결** 대화 상자가 표시됩니다.  
  
2.  **서버에 연결** 대화 상자가 표시되지 않는 경우 **개체 탐색기**에서 **연결** 을 클릭한 다음 **Reporting Services**를 클릭합니다.  
  
3.  **서버 유형** 목록에서 **Reporting Services**를 선택합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 가 목록에 없다면 설치되지 않은 것입니다.  
  
4.  **서버 이름** 목록에서 보고서 서버 인스턴스를 선택합니다. 목록에 로컬 인스턴스가 표시됩니다. 원격 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 입력할 수도 있습니다.  
  
5.  **연결**을 클릭합니다. 루트 노드를 확장하여 서버 속성을 설정하거나 역할 정의를 수정하거나 보고서 서버 기능을 해제할 수 있습니다.  
  
##  <a name="sql-server-data-tools-with-report-designer-and-report-wizard"></a><a name="bkmk_ssdt"></a>보고서 디자이너 및 보고서 마법사를 사용 하 여 SQL Server Data Tools  
 보고서 디자이너는 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] - Visual Studio 2012용 Business Intelligence에서 사용할 수 있습니다. 이러한 도구의 디자인 화면에는 보고서 제작 기능에 액세스하는 데 사용되는 탭 창, 마법사 및 메뉴가 있습니다. 보고서 서버 프로젝트 또는 보고서 서버 마법사 템플릿을 선택하면 보고서 디자이너 도구를 사용할 수 있습니다. 자세한 내용은 [SQL Server Data Tools의 Reporting Services&#40;SSDT&#41;](reporting-services-in-sql-server-data-tools-ssdt.md)를 참조하세요.  
  
#### <a name="to-start-report-designer"></a>보고서 디자이너를 시작하려면  
  
1.  Windows 시작 화면에서 **data** 를 입력한 다음 **응용 프로그램** 검색 결과에서 **Visual Studio 2012용 SQL Server Data Tools**를 클릭합니다.  
  
     **디스크나**  
  
     **시작**을 클릭 하 고 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]을 차례로 가리킨 다음 **SQL Server Data Tools (SSDT)** 를 클릭 합니다.  
  
2.  **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.  
  
3.  **프로젝트 형식** 목록에서 **비즈니스 인텔리전스 프로젝트**를 클릭합니다.  
  
4.  **템플릿** 목록에서 **보고서 서버 프로젝트**를 클릭합니다. 다음 다이어그램에서는 프로젝트 템플릿이 대화 상자에 표시되는 방법을 보여 줍니다.  
  
     ![새 프로젝트 템플릿 대화 상자](../media/rs-ui-newrsproject.gif "새 프로젝트 템플릿 대화 상자")  
  
5.  프로젝트의 이름과 위치를 입력하거나 **찾아보기** 를 클릭하여 위치를 선택합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)][!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 시작 페이지와 함께 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 열립니다. 솔루션 탐색기는 보고서 및 데이터 원본을 만드는 범주를 제공합니다. 이러한 범주를 사용하여 새 보고서 및 데이터 원본을 만들 수 있습니다. 보고서 정의를 만들면 탭 창이 표시됩니다. 탭 창은 데이터, 레이아웃 및 미리 보기입니다.  
  
 첫 번째 보고서를 시작하려면 [기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](../create-a-basic-table-report-ssrs-tutorial.md)를 참조하세요. 보고서 디자이너 내에서 사용할 수 있는 쿼리 디자이너에 대 한 자세한 내용은 [SSRS&#41;&#40;보고서 디자이너 SQL Server Data Tools 쿼리 디자인 도구 ](../report-data/query-design-tools-ssrs.md)를 참조 하세요.  
  
##  <a name="report-builder"></a><a name="bkmk_report_builder"></a> 보고서 작성기  
 [보고서 작성기 &#40;SSRS&#41;](report-builder-authoring-environment-ssrs.md) 를 사용 하 여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office와 비슷한 제작 환경에서 보고서를 만들 수 있습니다. 또한 보고서를 보고서 디자이너에서 만들었는지 이전 버전의 보고서 작성기에서 만들었는지에 상관없이 모든 기존 보고서를 사용자 지정하고 업데이트할 수 있습니다. 로컬 컴퓨터에 보고서 작성기를 설치하기 위해 실행하는 ReportBuilder3.msi 파일의 위치에 대해 관리자에게 문의하세요.  
  
 **설치:** 보고서 작성기의 한 번 클릭 버전은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 기본 모드 또는 SharePoint 모드로 설치 됩니다. 독립 실행형 버전의 보고서 작성기는 별도로 다운로드해야 합니다.  [보고서 작성기 &#40;보고서 작성기의 독립 실행형 버전 설치를](../install-windows/install-report-builder.md) 참조 하세요&#41;  
  
#### <a name="to-start-report-builder-clickonce-from-report-manager-native-mode"></a>보고서 관리자(기본 모드)에서 보고서 작성기 ClickOnce를 시작하려면  
  
1.  웹 브라우저에서 보고서 서버의 보고서 관리자 URL을 입력합니다. 기본적으로 URL은 http://\<*servername*>/reports입니다. 보고서 관리자가 열립니다.  
  
2.  **보고서 작성기**를 클릭합니다.  
  
     보고서 작성기가 열립니다. 이제 보고서를 작성하거나 보고서 서버의 보고서를 열 수 있습니다.  
  
#### <a name="to-start-report-builder-clickonce-using-a-url"></a>URL을 사용하여 보고서 작성기 ClickOnce를 시작하려면  
  
1.  웹 브라우저의 주소 표시줄에 다음 URL을 입력합니다.  
  
     **http://\<servername>/reportserver/reportbuilder/ReportBuilder_3_0_0_0. 응용 프로그램**  
  
2.  Enter 키를 누릅니다.  
  
     보고서 작성기가 열립니다. 이제 보고서를 작성하거나 보고서 서버의 보고서를 열 수 있습니다.  
  
#### <a name="to-start-report-builder-clickonce-in-reporting-services-sharepoint-mode"></a>Reporting Services SharePoint 모드에서 보고서 작성기 ClickOnce를 시작하려면  
  
1.  새 보고서를 만들 라이브러리가 포함된 사이트로 이동합니다.  
  
2.  라이브러리를 엽니다.  
  
3.  **새로 만들기** 메뉴에서 **보고서 작성기 보고서**를 클릭합니다.  
  
     보고서 작성기가 열립니다. 이제 보고서를 작성하거나 보고서 서버의 보고서를 열 수 있습니다.  
  
#### <a name="to-start-report-builder-stand-alone"></a>보고서 작성기 독립 실행형을 시작하려면  
  
1.  Windows 시작 화면에서 **report builder** 를 입력한 다음 **보고서 작성기 3.0**을 클릭합니다.  
  
     **디스크나**  
  
     시작 메뉴에서 **모든 프로그램**을 클릭한 다음 **Microsoft SQL Server 2014 보고서 작성기**를 클릭합니다.  
  
2.  **보고서 작성기**를 클릭합니다.  
  
     보고서 작성기가 열립니다. 이제 보고서를 작성하거나 열 수 있습니다.  
  
3.  보고서 작성기 설명서를 열려면 **보고서 작성기 도움말** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [설치, 제거 및 보고서 작성기 지원](../install-uninstall-and-report-builder-support.md)   
 [Sharepoint 2010 및 sharepoint 2013 &#40;SharePoint 모드 설치 Reporting Services&#41;](../install-windows/install-reporting-services-sharepoint-mode.md)   
 [Reporting Services 보고서 서버](../reporting-services-report-server.md)   
 [SSRS&#41;&#40;보고서 디자이너 SQL Server Data Tools의 쿼리 디자인 도구](../report-data/query-design-tools-ssrs.md)   
 [Reporting Services&#40;SSRS&#41; 자습서](../reporting-services-tutorials-ssrs.md)  
  
  
