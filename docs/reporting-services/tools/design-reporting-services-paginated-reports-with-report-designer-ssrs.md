---
title: "(SSRS) 보고서 디자이너로 보고서 디자인 | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Report Designer [Reporting Services], report creation
ms.assetid: 3a26dccc-6ad6-48f5-a882-f96c6c0dd405
caps.latest.revision: 77
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 02e1eb6504ae66ba6e48cedc0c511c4cd9505fb2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---

# <a name="design-reporting-services-paginated-reports-with-report-designer-ssrs"></a>Reporting Services (SSRS) 보고서 디자이너로 페이지가 매겨진된 보고서 디자인

보고서 디자이너를 사용하여 완전한 기능을 갖추고 페이지 매김 처리한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 및 보고 솔루션을 만들 수 있습니다. 보고서 디자이너에서 제공하는 그래픽 인터페이스를 통해 데이터 원본과 데이터 집합 및 쿼리, 보고서의 데이터 영역과 필드의 레이아웃 위치, 매개 변수와 같은 대화형 기능, 함께 작동하는 보고서 집합을 정의할 수 있습니다.  

보고서 디자이너는  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 기능으로, 비즈니스 인텔리전스 솔루션을 만들기 위한 Microsoft Visual Studio 환경입니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]SQL Server와 함께 포함 되지 않습니다. [SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714)를 다운로드합니다. 
  
## <a name="benefits-of-report-projects"></a>보고서 프로젝트의 이점  
보고서 프로젝트는 보고서 정의 및 리소스를 위한 컨테이너 역할을 합니다. 프로젝트를 사용하면 다음을 수행할 수 있습니다.  
  
-   보고서 및 관련 항목을 하나의 컨테이너에 구성합니다.  
  
-   보고서 및 관련 항목이 포함된 보고서 솔루션을 로컬에서 테스트합니다.  
  
-   관련 항목을 함께 배포합니다. 프로젝트 속성 및 구성 관리를 사용하여 여러 환경에 배포합니다.  
  
-   보고서 및 관련 항목에 대한 마스터 복사본 집합을 유지합니다. 배포 후 게시된 보고서를 실수로 수정할 수 있습니다.  
  
 이 항목의 정보를 참조하여 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 솔루션에서 단일 보고 프로젝트의 페이지 매김 처리한 보고서 및 관련 항목을 디자인하세요. SQL Server Data Tools의 솔루션 및 여러 프로젝트에 자세한 내용은 [SQL Server Data Tools의 Reporting Services](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)를 참조하세요.  

  
##  <a name="bkmk_SharedDataSources"></a> Shared Data Sources  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 를 사용하여 보고 솔루션용 공유 데이터 원본을 정의하고 배포합니다. **OverwriteDataSources** 및 **TargetDataSourceFolder** 속성을 사용하면 공유 데이터 원본을 프로젝트의 다른 항목과 별도로 배포할 수 있습니다. 자세한 내용은 [배포 속성 설정&#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)을 참조하세요.  
  
 보고서 디자이너의 보고서 데이터 창 및 솔루션 탐색기에서 보고서에 사용될 데이터 원본을 정의할 수 있습니다. 자세한 내용은 [Report Data Pane](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_ReportDataPane)을 참조하세요. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 에서는 보고서 서버나 SharePoint 사이트에 게시되었지만 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 솔루션에는 포함되지 않은 데이터 원본을 열 수 없습니다. 해당 기능의 경우 [보고서 작성기 제작 환경&#40;SSRS&#41;](../../reporting-services/tools/report-builder-authoring-environment-ssrs.md)을 사용합니다.  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]는 클라이언트 도구입니다. 보고 솔루션을 로컬 컴퓨터에서 테스트하고, 서버 솔루션 테스트용으로 테스트 환경에 배포한 후, 프로덕션 환경에 배포할 수 있습니다. 배포 후 데이터 원본 처리 확장 프로그램 및 데이터 원본 자격 증명이 보고서 서버 환경에 맞게 구성되었는지 확인합니다. 구성 관리자를 사용하면 서로 다른 배포의 속성을 관리하는 데 유용합니다. 자세한 내용은 [SQL Server Data Tools의 Reporting Services&#40;SSDT&#41;](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)를 참조하세요.  
  
 자세한 내용은 [Data Connections, Data Sources, and Connection Strings &#40;Report Builder and SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)을 참조하세요.  
   
##  <a name="bkmk_SharedDatasets"></a> 공유 데이터 집합  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 를 사용하여 보고 솔루션용 공유 데이터 집합을 정의하고 배포합니다. **OverwriteDatasets** 및 **TargetDatasetFolder** 속성을 사용하면 공유 데이터 집합을 프로젝트의 다른 항목과 별도로 배포할 수 있습니다. 자세한 내용은 [배포 속성 설정&#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)을 참조하세요.  
  
 보고서 디자이너의 보고서 데이터 창 및 솔루션 탐색기에서 보고서에 사용될 공유 데이터 집합을 정의할 수 있습니다. 자세한 내용은 [Report Data Pane](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_ReportDataPane)을 참조하세요. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 에서는 보고서 서버 또는 SharePoint 사이트에서 직접 게시된 데이터 집합을 열 수 없습니다. 해당 기능의 경우 공유 데이터 집합 모드에서 [보고서 작성기 제작 환경&#40;SSRS&#41;](../../reporting-services/tools/report-builder-authoring-environment-ssrs.md)을 사용합니다.  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]는 클라이언트 도구입니다. 쿼리 디자이너를 사용하여 쿼리 결과를 만들고 로컬에서 미리 보기로 테스트할 수 있습니다. 배포 후 기반이 되는 공유 데이터 원분 및 보고서와는 별도로 공유 데이터 집합을 관리할 수 있습니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md), [쿼리 디자인 도구&#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md) 및 [공유 데이터 집합 관리](../../reporting-services/report-data/manage-shared-datasets.md)를 참조하세요.  
  
##  <a name="bkmk_Reports"></a> 페이지를 매긴 보고서  
페이지 매김 처리한 보고서는 보고서 프로젝트에 저장된 파일입니다. 보고서는 독립 실행형 보고서, 하위 보고서 또는 주 보고서의 드릴스루 동작 대상으로 사용할 수 없습니다. **TargetReportFolder** 및 기타 속성을 사용하면 보고서를 프로젝트의 다른 항목과 별도로 배포할 수 있습니다. 자세한 내용은 [배포 속성 설정&#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)을 참조하세요.  
  
> [!NOTE]  
>  SharePoint 모드 보고서 서버에 게시하려는 경우 보고서 디자이너 프로젝트에서 일부 보고서 솔루션 기능을 테스트할 수 없습니다. 보고서, 하위 보고서 및 드릴스루 보고서에 대한 참조는 보고서 프로젝트 배포 이후에만 테스트할 수 있는 정규화된 URL을 사용해야 합니다. 자세한 내용은 [SharePoint 모드의 보고서 서버에 게시된 보고서 항목에 대한 URL 예&#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)를 참조하세요.  
  
 다음과 같은 방법으로 보고서를 프로젝트에 추가할 수 있습니다.  
  
-   **새 보고서 프로젝트를 추가합니다.** 기본적으로 빈 보고서가 보고서 디자이너에 열립니다. 자세한 내용은 [보고서 프로젝트에 새 보고서 또는 기존 보고서 추가&#40;SSRS&#41;](../../reporting-services/tools/add-a-new-or-existing-report-to-a-report-project-ssrs.md)를 참조하세요.  
  
-   **보고서 마법사 프로젝트를 추가합니다.** 단계별 안내에 따라 보고서를 만듭니다. 보고서 마법사를 사용하면 일련의 단계에 따라 간단하게 데이터 정의 및 보고서 디자인 작업을 수행하여 훌륭한 보고서를 만들 수 있습니다. 스타일을 추가하여 조직에 맞게 마법사를 사용자 지정할 수 있습니다. 자세한 내용은 [보고서 프로젝트에 새 보고서 또는 기존 보고서 추가&#40;SSRS&#41;](../../reporting-services/tools/add-a-new-or-existing-report-to-a-report-project-ssrs.md)를 참조하세요.  
  
-   **보고서 유형의 새 항목을 추가합니다.** 빈 보고서가 보고서 디자이너에 열립니다.  
  
-   **기존 항목을 추가합니다.** 기존 보고서 정의 파일(.rdl)이 보고서 디자이너에 열립니다. 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 만든 보고서 또는 프로젝트를 열면 프로젝트가 현재 버전으로, 보고서가 현재 스키마로 자동 업그레이드될 수 있습니다. 자세한 내용은 [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md)을(를) 참조하세요.  
  
-   **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Access 보고서를 가져옵니다.** Access 데이터베이스 파일(.mdb, .accdb) 또는 프로젝트 파일(.adp)에서 모든 보고서를 가져옵니다. 보고서 디자이너가 데이터베이스 또는 프로젝트 파일의 각 보고서를 RDL로 변환하여 보고서 프로젝트에 저장합니다. Access 보고서의 일부 기능은 보고서 정의 파일(.rdl)로 전송되지 않습니다. 자세한 내용은 [Microsoft Access에서 보고서 가져오기&#40;Reporting Services&#41;](http://msdn.microsoft.com/library/4f29d5b8-b77d-4714-a84a-05523df55646) 및 [지원되는 Access 보고서 기능&#40;SSRS&#41;](http://msdn.microsoft.com/library/7ffec331-6365-4c13-8e58-b77a48cffb44)을 참조하세요.  
  
    > [!NOTE]  
    >  가져오기 기능을 사용하려면 보고서 디자이너가 설치된 컴퓨터에 Access 2002 이상이 설치되어 있어야 합니다. 보고서를 가져올 때 Access 보고서의 데이터 원본이 사용 가능한 상태여야 합니다.  
  
-   **직접 RDL로 작업합니다.** 보고서 디자이너에서 보고서를 작성하면 보고서가 XML 형식의 RDL(Report Definition Language) 파일로 저장됩니다. 보고서 디자이너, 텍스트 편집기 또는 XML을 편집할 수 있는 모든 도구에서 이 파일을 편집할 수 있습니다.  
  
     보고서 디자이너에서 보고서 정의 원본을 편집하는 경우 개발 도구를 설치한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 대한 현재 RDL 스키마로 작업하게 됩니다. 프로젝트를 구축하면 스키마 버전이 배포 속성에 따라 변경될 수 있습니다. 자세한 내용은 [Deployment and Version Support in SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)를 참조하세요.  
  
     RDL을 직접 편집하면 보고서를 보고서 서버에 게시할 수 없거나 실행할 수 없습니다. 다른 XML 파일에서처럼 요소 내에 사용된 XML 관련 문자는 제대로 인코딩되어야 합니다. 보고서를 게시하면 보고서 서버는 이 스키마를 사용하여 RDL 파일에 포함된 XML의 유효성을 검사합니다.  
  
     RDL 스키마의 일부가 아닌 요소를 포함하려면 사용자 지정 요소에 삽입합니다. 사용자 지정 요소는 사용자 지정 렌더링 확장 프로그램에서 읽을 수 있지만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 제공되는 렌더링 확장 프로그램에서는 무시됩니다. 예를 들어 사용자 지정 요소를 사용하여 보고서에 설명을 저장할 수 있습니다.  
  
     자세한 내용은 [RDL(Report Definition Language)&#40;SSRS&#41;](../../reporting-services/reports/report-definition-language-ssrs.md)을 참조하세요.  
  
##  <a name="bkmk_ReportParts"></a> 보고서 파트  
 보고서 디자이너에서 프로젝트에 테이블, 차트 및 페이지가 매겨진 기타 보고서 항목을 만든 후에는 자신과 다른 사람이 다른 보고서에서 다시 사용할 수 있도록 이들 항목을 보고서 서버 또는 보고서 서버와 통합된 SharePoint 사이트에 *보고서 파트* 로 게시할 수 있습니다. 자세한 내용은 [보고서 디자이너의 보고서 파트&#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)를 참조하세요.  
  
 **TargetReportPartFolder** 및 기타 속성을 사용하면 보고서 파트를 프로젝트의 다른 항목과 별도로 배포할 수 있습니다. 자세한 내용은 [배포 속성 설정&#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)을 참조하세요.  
  
##  <a name="bkmk_Resources"></a> 리소스  
 보고서와 관련되지만 보고서 서버에서 처리되지 않는 파일을 프로젝트에 추가할 수 있습니다. 예를 들어 사진의 경우 이미지를, 공간 데이터의 경우 ESRI 셰이프 파일을 추가할 수 있습니다. 자세한 내용은 [Resources](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md#bkmk_Resources)를 참조하세요.  
 
##  <a name="bkmk_ReportLayout"></a> Paginated Report Layout  
 보고서 레이아웃을 만들려면 보고서 항목 및 데이터 영역을 도구 상자에서 디자인 화면으로 끈 다음 해당 항목을 정렬합니다. 데이터 집합 필드를 디자인 화면의 항목으로 끌어 보고서에 데이터를 추가합니다. 테이블릭스 데이터 영역에서 데이터를 그룹으로 구성하려면 데이터 집합 필드를 그룹화 창으로 끕니다. 보고서 제작 도구는 기본적으로 보고서 정의를 만드는 방법이므로 보고서 디자인에 대한 접근 방식이 보고서 작성기와 보고서 디자이너 간에 유사합니다.  
   
##  <a name="bkmk_Preview"></a> Preview a Paginated Report  
 **미리 보기** 를 사용하여 보고서 데이터 및 레이아웃 디자인을 확인할 수 있습니다. 보고서를 미리 보는 경우 보고서 처리기에서 보고서 정의 스키마와 식 구문의 유효성을 검사하고 문제를 [Output](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_Output) 창에 나열합니다.  
  
> [!NOTE]  
>  보고서를 미리 보면 보고서의 데이터가 로컬 컴퓨터의 파일에 캐시됩니다. 동일한 쿼리, 매개 변수 및 자격 증명을 사용하여 동일한 보고서를 다시 미리 보면 보고서 디자이너는 쿼리를 다시 실행하지 않고 캐시된 복사본을 검색합니다. 데이터 파일으로 저장 됩니다  *\<reportname >*. 파일과 보고서 정의 파일과 같은 디렉터리에 있습니다. 이 파일은 보고서 디자이너를 닫아도 삭제되지 않습니다.  
  
 다음과 같은 방법으로 보고서를 미리 볼 수 있습니다.  
  
-   **미리 보기.** 미리 보기 도구 모음에서 **미리 보기** 탭을 클릭합니다. 보고서가 로컬로 실행되며 보고서 서버에 제공되는 동일한 보고서 처리 및 렌더링 기능을 사용합니다. 표시되는 보고서는 대화형 이미지이므로 매개 변수를 선택하고, 링크를 클릭하고, 문서 구조를 보고, 보고서의 숨겨진 영역을 확대 및 축소할 수 있습니다. 또한 설치된 렌더링 형식으로 보고서를 내보낼 수 있습니다.  
  
-   **독립 실행형 미리 보기.** 로컬 보고서를 브라우저에서 실행합니다. 디버그 구성을 사용하면 작성하는 사용자 지정 어셈블리를 이 모드에서 디버깅할 수 있습니다. 디버그 모드에서 프로젝트를 실행하는 데는 세 가지 방법이 있습니다.  
  
    -   **디버그** 메뉴에서 **디버깅 시작**을 클릭합니다.  
  
    -   [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 표준 도구 모음에서 **시작** 단추를 클릭합니다.  
  
    -   F5 키를 누릅니다.  
  
     보고서를 작성은 하지만 배포하지 않는 프로젝트 구성을 사용하면 현재 구성의 **StartItem** 속성에 지정된 보고서는 별도의 미리 보기 창에 열립니다.  
  
    > [!NOTE]  
    >  디버그 모드를 사용하려면 먼저 시작 항목을 설정해야 합니다. 솔루션 탐색기에서 보고서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 다음 **StartItem**에서 표시할 보고서의 이름을 선택하세요.  
  
     프로젝트의 시작 항목이 아닌 특정 보고서를 미리 보려면 보고서를 작성하지만 배포하지 않는 구성(예: DebugLocal 구성)을 선택하고 보고서를 마우스 오른쪽 단추로 클릭한 다음 **실행**을 클릭합니다. 보고서를 배포하지 않는 구성을 선택해야 합니다. 그렇지 않으면 보고서는 로컬 컴퓨터의 미리 보기 창에 표시되지 않고 보고서 서버에 게시됩니다.  
  
-   **인쇄 미리 보기.**  
  
     미리 보기 모드 또는 미리 보기 창에서 보고서를 처음으로 보면 해당 보고서가 HTML 렌더링 확장 프로그램에서 생성된 보고서와 유사하게 표시됩니다. 미리 보기는 HTML 형식은 아니지만 보고서의 레이아웃 및 페이지 매기기는 HTML 출력과 유사합니다.  
  
     인쇄 미리 보기 모드로 전환하여 인쇄될 보고서를 표시할 수 있습니다. 미리 보기 도구 모음에서 **인쇄 미리 보기** 단추를 클릭합니다. 보고서는 실제 인쇄된 페이지처럼 표시되며 이미지 및 PDF 렌더링 확장 프로그램에서 생성된 출력과도 유사합니다. 인쇄 미리 보기는 이미지나 PDF 파일 형식은 아니지만 보고서의 레이아웃 및 페이지 매기기는 해당 형식의 출력과 유사합니다. 보고서 이미지의 크기를 선택할 수 있습니다(예: 페이지 너비 설정).  
  
     인쇄 미리 보기는 보고서 인쇄 시 발생할 수 있는 다수의 렌더링 문제를 식별하는 데 유용합니다. 일반적으로 다음과 같은 렌더링 문제가 있습니다.  
  
    -   보고서 너비가 너무 커서 보고서에 대해 지정한 용지에 맞지 않기 때문에 추가 공백 페이지가 있습니다.  
  
    -   보고서가 지정된 용지 너비를 초과하도록 동적으로 확장되는 행렬을 포함하고 있기 때문에 공백 페이지가 있습니다.  
  
    -   그룹 사이에서 페이지 나누기가 원하는 방식으로 작동하지 않습니다.  
  
    -   머리글 및 바닥글이 예상대로 표시되지 않습니다.  
  
    -   인쇄 형식에서 더 읽기 쉽도록 보고서 레이아웃을 수정해야 합니다.  
   
##  <a name="bkmk_SaveandDeploy"></a> Save and Deploy Paginated Reports  
 보고서 디자이너에서 보고서 및 기타 프로젝트 파일을 로컬로 저장하거나 보고서 서버나 SharePoint 사이트에 배포할 수 있습니다. 구성한 프로젝트 배포 속성에 따라 공유 데이터 원본, 공유 데이터 집합, 보고서, 보고서 리소스 및 보고서 파트를 독립적으로 배포하거나 함께 배포할 수 있습니다. 자세한 내용은 [Configuration and Deployment Properties](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md#bkmk_ConfigurationandDeploymentProperties)을 참조하세요.  
  
 보고서 디자이너를 사용할 때는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 현재 버전의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 지원되는 보고서 정의 스키마를 사용하여 보고서를 디자인한다는 것을 이해해야 합니다. 특정 보고서 서버 또는 SharePoint 사이트에 대한 프로젝트 배포 속성을 설정한 후 보고서를 저장하는 경우 보고서 디자이너는 대상 보고서 서버의 버전과 일치하는 스키마로 디렉터리를 구축하는 보고서 정의를 저장합니다. 낮은 수준의 보고서 서버에 게시할 수 있는 보고서를 만들기 위해 보고서 디자이너는 대상 스키마에 존재하지 않는 보고서 항목을 삭제합니다. 이 동작은 메시지를 표시하지 않고 자동으로 수행됩니다. 이 동작이 수행되면 원본 보고서 정의가 프로젝트 폴더에 유지됩니다. 배포되는 수정된 보고서 정의는 작성기 폴더에 있습니다.  
  
> [!NOTE]  
>  디버깅 식 및 배포 오류를 확인하려면 작성기 폴더의 보고서 정의를 봐야 합니다. **소스 보기**를 사용하지 마세요. **소스 보기** 는 프로젝트 폴더에서 보고서 정의 원본을 표시합니다.  
  
 자세한 내용은 [Deployment and Version Support in SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)를 참조하세요.  
  
### <a name="save-a-report-locally"></a>로컬로 보고서 저장  
 보고서 디자이너에서 보고서 또는 기타 프로젝트 항목을 작업할 때 파일은 로컬 컴퓨터에 저장하거나 액세스 권한을 가진 다른 컴퓨터에서 공유할 수 있습니다.  
  
 원본 제어 소프트웨어를 사용하는 경우 보고서 저장 시 원본 제어 서버에 보고서를 체크 인할 수 있습니다. 자세한 내용은 [Source Control](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_SourceControl)를 참조하세요.  
  
### <a name="deploy-or-publish-paginated-reports"></a>페이지 매김 처리한 보고서 배포 또는 게시  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 보고서 또는 기타 프로젝트 항목을 여러 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에 배포할 수 있습니다. 프로젝트 구성을 사용하면 보고서 정의를 대상 보고서 서버 호환 스키마 버전으로 업그레이드하는 작업을 제어할 수 있습니다. 프로젝트 구성으로 제어되는 속성에는 대상 보고서 서버, 오류 수준, 빌드 프로세스에서 미리 보기 및 배포용으로 보고서 정의를 임시 저장하는 폴더 등이 포함됩니다. 자세한 내용은 [구성 및 배포 속성](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md#bkmk_ConfigurationandDeploymentProperties) 및 [배포 속성 설정&#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)을 참조하세요.  
  
### <a name="export-a-paginated-report-to-a-different-file-format"></a>페이지 매김 처리한 보고서를 다른 파일 형식으로 내보내기  
 보고서를 다양한 형식으로 내보낼 수 있으며, 이러한 형식은 일부 보고서 레이아웃 및 대화형 기능의 작동에 영향을 줍니다. 다양한 출력 형식의 디자인 고려 사항에 대한 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)를 참조하세요.  
   
##  <a name="bkmk_ReportValidationandErrorLevels"></a> 보고서 유효성 검사 및 오류 수준  
 보고서는 미리 보기 전과 배포 도중에 유효성이 검사됩니다. 보고서를 빌드할 때 여러 빌드 문제가 발생할 수 있습니다. 예를 들어 프로젝트 구성이 지정하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 버전과 호환되지 않는 식 또는 쿼리와 같은 문자열이 보고서에 포함될 수 있습니다.  
  
 ErrorLevel 속성을 사용하여 빌드 경고와 오류를 관리할 수 있습니다. ErrorLevel 속성은 0에서 4(포함) 사이의 값을 포함할 수 있습니다. 이 값은 오류로 보고되는 빌드 문제 및 경고로 보고되는 빌드 문제를 결정합니다. 기본값은 2입니다. 경고와 오류는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)][출력](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_Output) 창에 기록됩니다.  
  
 ErrorLevel 값보다 작거나 같은 심각도 수준을 가진 문제는 오류로 보고되고 그렇지 않은 문제는 경고로 보고됩니다.  
  
 다음 표에서는 오류 수준을 보여 줍니다.  
  
|오류 수준|Description|  
|-----------------|-----------------|  
|0|보고서 미리 보기 및 배포를 불가능하게 만드는 가장 심각하고 불가피한 빌드 문제|  
|1.|보고서 레이아웃을 대폭 변경하는 심각한 빌드 문제|  
|2|보고서 레이아웃을 상당히 변경하는 덜 심각한 빌드 문제|  
|3|알아차릴 수 없게 약간만 보고서 레이아웃을 변경하는 사소한 빌드 문제|  
|4|경고를 게시하기 위해서만 사용됩니다.|  
  
 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]의 새로운 보고서 항목을 포함하는 보고서를 미리 보거나 배포하려고 하면 이러한 보고서 항목이 보고서에서 제거될 수 있습니다. 기본적으로 구성의 ErrorLevel 속성은 2로 설정되므로 지도가 제거될 경우 보고서 빌드가 실패합니다. 그러나 ErrorLevel 속성 값을 0 또는 1로 변경할 경우 지도는 삭제되고 경고가 표시되며 빌드 프로세스가 계속됩니다.  

## <a name="next-steps"></a>다음 단계

[SQL Server Data Tools 다운로드](http://go.microsoft.com/fwlink/?LinkID=616714)  
[SQL Server Data Tools의 reporting Services](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)   
[쿼리 디자인 도구](../../reporting-services/report-data/query-design-tools-ssrs.md)   
[SQL Server Data Tools의 배포 및 버전 지원](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
