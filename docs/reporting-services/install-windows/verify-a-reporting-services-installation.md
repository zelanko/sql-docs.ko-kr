---
title: Reporting Services 설치 확인 | Microsoft Docs
ms.date: 06/03/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- checking report server installations
- verifying report server installations
- Report Designer [Reporting Services], verifying installations
- installing Reporting Services, verifying installations
- report servers [Reporting Services], verifying installations
- Setup [Reporting Services], verifying installations
ms.assetid: 82a51a99-66f0-4b0c-b05b-07d22387adb0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0628f715be90586e851fee55301e8c82032739c3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73593923"
---
# <a name="verify-a-reporting-services-installation"></a>Reporting Services 설치 확인
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버는 기본 모드 또는 SharePoint 모드 중 하나로 설치할 수 있습니다. 설치를 확인하기 위해 수행해야 하는 단계는 보고서 서버 모드에 따라 다릅니다.  

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
##  <a name="verify-sharepoint-mode-installation"></a><a name="bkmk_sharepointmode"></a> SharePoint 모드 설치 확인  
  
### <a name="to-verify-the-reporting-services-service"></a>Reporting Services 서비스를 확인하려면  
  
1.  SharePoint 중앙 관리의 **시스템 설정** 그룹에서 **서버의 서비스 관리** 를 클릭합니다.  
  
2.  **SQL Server Reporting Services 서비스** 가 설치되어 있고 **실행 중** 상태인지 확인합니다.  
  
     목록에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스가 표시되지 않으면 해당 서비스가 설치되어 있는지 확인합니다. 자세한 내용은 [SharePoint 모드에서 첫 번째 보고서 서버 설치](install-the-first-report-server-in-sharepoint-mode.md)를 참조하세요.  
  
### <a name="to-verify-the-service-application"></a>서비스 애플리케이션을 확인하려면  
  
1.  중앙 관리에서 적어도 하나의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션이 있는지 확인하려면 **애플리케이션 관리** 그룹에서 **서비스 애플리케이션 관리** 를 클릭합니다.  
  
2.  **SQL Server Reporting Services 서비스 애플리케이션** 유형의 서비스 애플리케이션과 해당 애플리케이션 프록시가 있는지 확인합니다.  
  
3.  서비스 애플리케이션 이름 **근처** 를 클릭한 다음 SharePoint 도구 모음에서 **속성** 을 클릭합니다.  서비스 애플리케이션 이름을 클릭하면 서비스 애플리케이션의 속성 페이지가 아닌 관리 페이지가 열립니다.  
  
4.  원하는 웹 애플리케이션을 가리키기 위해 **웹 애플리케이션 연결** 이 구성되어 있는지 확인합니다.  
  
### <a name="to-verify-the-site-collection-feature"></a>사이트 모음 기능을 확인하려면  
  
1.  사이트 설정의 **사이트 모음 관리** 그룹에서 **사이트 모음 기능** 을 클릭합니다.  
  
2.  **보고서 서버 통합 기능** 이 활성 상태인지 확인합니다.  
  
### <a name="to-verify-reporting-server-content-types"></a>보고 서버 내용 유형을 확인하려면  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 콘텐츠 형식을 확인하거나 추가하려면 [SharePoint 라이브러리에 Reporting Services 콘텐츠 형식 추가](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)를 참조하세요.  
  
### <a name="to-verify-you-can-launch-report-builder"></a>보고서 작성기를 실행할 수 있는지 확인하려면  
  
1.  문서 라이브러리의 SharePoint 리본에서 **문서** 를 클릭합니다.  
  
2.  **새 문서** 를 클릭하고 **보고서 작성기 보고서**를 클릭합니다. 이 옵션이 표시되지 않으면 라이브러리에 보고서 서버 내용 유형을 추가하는 방법에 대한 이전 절차를 검토하세요.  
  
### <a name="create-a-basic-report"></a>기본 보고서 만들기  
  
1.  SharePoint 문서 라이브러리에서 텍스트 상자(예: 제목)만 포함된 기본 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서를 만듭니다. 이 보고서에는 어떠한 데이터 원본 또는 데이터 세트도 포함되지 않습니다. 이 보고서의 목적은 보고서 작성기를 열고 기본 보고서를 미리 볼 수 있는지 확인하기 위한 것입니다.  
  
2.  보고서를 문서 라이브러리에 저장하고 라이브러리에서 보고서를 실행합니다. 보고서 작성기로 보고서를 만드는 방법은 [보고서 작성기 시작](../report-builder/start-report-builder.md)을 참조하세요.  
  
### <a name="reporting-services-samples"></a>Reporting Services 예제  
  
1.  Reporting Services 자습서 중 하나를 완료합니다. 자세한 내용은 [Reporting Services 자습서&#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)를 참조하세요.  
  
2.  Adventure Works 예제 데이터베이스 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 예제 보고서를 GitHub에서 다운로드합니다. 자세한 내용은 [AdventureWorks 예제 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 참조하세요.  

::: moniker-end
  
##  <a name="verify-a-native-mode-installation"></a><a name="bkmk_nativemode"></a> 기본 모드 설치 확인  
 기본 구성을 사용하여 기본 모드 보고서 서버를 설치하는 경우 설치 프로그램은 서버를 설치하고 배포합니다. 몇 가지 간단한 테스트를 수행하여 보고서 서버의 배포 여부를 확인할 수 있습니다. 이러한 단계를 수행하기 위해서는 로컬 관리자여야 합니다. 다른 사용자가 테스트를 수행할 수 있도록 하려면 해당 사용자에 대한 보고서 서버 액세스 권한을 구성해야 합니다.  
  
### <a name="to-verify-that-the-report-server-is-installed-and-running"></a>보고서 서버가 설치되어 실행 중인지 확인하려면  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 실행하고 방금 설치한 보고서 서버 인스턴스에 연결합니다. 웹 서비스 URL 페이지에는 보고서 서버 웹 서비스에 대한 링크가 포함되어 있습니다. 이 링크를 클릭하면 서버에 액세스할 수 있는지 확인할 수 있습니다. 보고서 서버 데이터베이스가 구성되어 있지 않으면 링크를 클릭하기 전에 먼저 보고서 서버 데이터베이스를 구성합니다.  
  
2.  서비스 콘솔 애플리케이션을 열고 보고서 서버 서비스가 실행 중인지 확인합니다. 보고서 서버 서비스의 상태를 확인하려면 **시작**을 클릭하고 **제어판**을 가리킨 후 **관리 도구**를 두 번 클릭하고 **서비스**를 두 번 클릭합니다. 서비스 목록이 나타나면 **보고서 서버(MSSQLSERVER)** 로 스크롤합니다. 상태가 **시작됨**으로 바뀝니다.  
  
3.  브라우저를 열고 주소 표시줄에 보고서 서버 URL을 입력합니다. 주소는 설치 중에 보고서 서버에 지정한 서버 이름과 가상 디렉터리 이름으로 구성됩니다. 기본적으로 보고서 서버 가상 디렉터리 이름은 **ReportServer**입니다. https:// *\<computer name>* /ReportServer *\<_instance name>* URL을 사용하여 보고서 서버 설치를 확인할 수 있습니다. 보고서 서버를 명명된 인스턴스로 설치한 경우 URL이 달라질 수 있습니다. URL 형식에 대한 자세한 내용은 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)을 참조하세요. Windows Vista 또는 Windows Server 2008의 로컬 관리자인 경우 [로컬 관리에 대해 기본 모드 보고서 서버 구성&#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)을 참조하세요.  
  
4.  보고서를 실행하여 보고서 서버 작동을 테스트합니다. 이 단계에서는 자습서에서 샘플 보고서를 만들 수 있습니다. 자세한 내용은 [기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)를 참조하세요.  
  
### <a name="to-verify-that-the-ssrswebportal-is-installed-and-running"></a>[!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 이 설치되어 실행 중인지 확인하려면  
  
1.  브라우저를 열고 주소 표시줄에 웹 포털 URL을 입력합니다. 주소는 설치 중에 또는 Reporting Services 구성 도구의 웹 포털 URL 페이지에서 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 에 대해 지정한 서버 이름과 가상 디렉터리 이름으로 구성됩니다. 기본적으로 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 가상 디렉터리는 **Reports**입니다. 다음 URL을 사용하여 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 설치를 확인할 수 있습니다.  
  
     https:// *\<computer name>* /Reports *\<_instance name>* .  
  
2.  [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 에서 새 폴더를 만들거나 파일을 업로드하여 보고서 서버 데이터베이스로 정의가 다시 전달되었는지 여부를 테스트합니다. 이런 작업이 성공적으로 수행되면 연결 기능이 작동합니다.  
  
     자세한 내용은 [웹 포털&#40;SSRS 기본 모드&#41;](../../reporting-services/web-portal-ssrs-native-mode.md)을 참조하세요.  
  
### <a name="to-verify-that-report-designer-is-installed-and-running"></a>보고서 디자이너가 설치되어 실행 중인지 확인하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 열고 보고서 서버 프로젝트 유형을 기반으로 새 프로젝트를 만듭니다. 보고서 서버 프로젝트 마법사를 사용하는 방법은 [SQL Server Data Tools의 Reporting Services&#40;SSDT&#41;](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)를 참조하세요.  
  
2.  보고서 예제를 설치한 경우 예제 보고서 프로젝트 파일을 열고 해당 보고서를 보고서 서버에 게시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 설치 문제 해결](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
 [Reporting Services 오류의 원인 및 해결 방법](../../reporting-services/troubleshooting/cause-and-resolution-of-reporting-services-errors.md)  
  
  
