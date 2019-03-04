---
title: SQL Server의 보고서 작성기 | Microsoft Docs
ms.date: 11/29/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- "10428"
helpviewer_keywords:
- overview of Report Builder
- getting started
ms.assetid: 55bf4f9c-d037-412f-ae57-3fc39ce32fa5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f37319c07856f0e31abcb2afb047bdea2904063a
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290301"
---
# <a name="report-builder-in-sql-server"></a>SQL Server의 보고서 작성기
  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]는 Visual Studio의 보고서 디자이너를 사용하는 대신 독립 실행형 환경에서 작업하려는 비즈니스 사용자가 페이지를 매긴 보고서를 작성하는 데 사용할 수 있는 도구입니다.  페이지를 매긴 보고서를 디자인할 때는 데이터를 가져올 위치, 가져올 데이터 및 데이터를 표시할 방법을 지정하는 보고서 정의를 만듭니다. 보고서를 실행하면 보고서 처리기는 지정된 보고서 정의를 가져와 데이터를 검색한 다음 보고서 레이아웃에 따라 정렬하여 보고서를 생성합니다. [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]에서 보고서를 미리 볼 수 있습니다. 그런 다음, 보고서를 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에 기본 모드 또는 SharePoint 통합 모드(2016 이하)로 게시할 수 있습니다. 페이지를 매긴 보고서를 Power BI 서비스에 게시할 수도 있습니다. [Power BI Premium의 페이지를 매긴 보고서](https://docs.microsoft.com/power-bi/paginated-reports-report-builder-power-bi)(미리 보기)에 대해 자세히 알아보세요.
  
 ![rs_GettingStartedReport](../../reporting-services/report-builder/media/rs-gettingstartedreport.png "rs_GettingStartedReport")  
  
 이 페이지를 매긴 보고서에는 행/열 그룹, 스파크라인, 표시기, 모서리 셀의 요약 원형 차트가 포함된 행렬이 나와 있습니다. 그리고 색과 원 크기로 구분되어 표시된 두 가지 지리 데이터 집합을 보여 주는 지도도 함께 포함되어 있습니다.  
  
##  <a name="JumpStartReptCreation"></a> 빠른 보고서 만들기  
  
-   **공유 데이터 세트를 사용하여 보고서를 작성**합니다. 공유 데이터 세트는 공유 데이터 원본을 기반으로 하는 쿼리이며 기본 모드 또는 SharePoint 통합 모드에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에 저장됩니다.  
  
-   **테이블, 행렬 또는 차트 마법사를 사용하여 보고서를 작성**합니다. 데이터 원본 연결을 선택하고, 필드를 끌어다 놓는 방법으로 데이터 세트 쿼리를 만들고, 레이아웃과 스타일을 선택하고, 보고서를 사용자 지정합니다.  
  
-   **지도 마법사를 사용** 하여 지리적 또는 기하학적 배경을 바탕으로 집계된 데이터를 표시하는 보고서를 작성합니다. 지도 데이터는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리의 공간 데이터 또는 ESRI(Environmental Systems Research Institute, Inc.) 셰이프 파일일 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing 지도 타일 배경을 추가할 수도 있습니다.  
  
-   **먼저 보고서 파트를 보고서에 포함**합니다. 보고서 파트는 기본 모드 또는 SharePoint 통합 모드에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에 별도로 게시된 보고서 항목이며 다른 보고서에서 다시 사용할 수 있습니다. 테이블, 행렬, 차트 및 이미지와 같은 보고서 항목은 보고서 파트로 게시할 수 있습니다.  
  
##  <a name="DesignRept"></a> 보고서 디자인  
  
-   **테이블, 행렬, 차트, 자유 형식 보고서 레이아웃을 사용하여 페이지를 매긴 보고서를 작성합니다.** 열 중심의 데이터에 대한 테이블 보고서, 요약된 데이터에 대한 행렬 보고서(예: 크로스탭 또는 피벗 테이블 보고서), 그래픽 데이터에 대한 차트 보고서, 그 외 모든 데이터에 대한 자유 형식 보고서를 만듭니다. 목록, 그래픽, 동적 웹 기반 애플리케이션을 위한 컨트롤 등과 함께 다른 보고서 및 차트를 보고서에 포함할 수 있습니다.  
  
-   **다양한 데이터 원본을 사용하여 보고서를 작성합니다.** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]관리 데이터 공급자, OLE DB 공급자 또는 ODBC 데이터 원본이 있는 데이터 원본 유형의 데이터를 사용하여 보고서를 작성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Oracle, Hyperion 및 기타 데이터베이스에서 관계형 및 다차원 데이터를 사용하는 보고서를 만들 수 있습니다. XML 데이터 처리 확장 프로그램을 사용하면 어떠한 XML 데이터 원본에서도 데이터를 검색할 수 있습니다. 테이블 반환 함수를 사용하여 사용자 지정 데이터 원본을 디자인할 수 있습니다.  
  
-   **기존 보고서를 수정합니다.** [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]를 사용하면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]보고서 디자이너에서 만든 보고서를 사용자 지정하고 업데이트할 수 있습니다.  
  
-   **데이터를 수정** 합니다. 데이터를 필터링/그룹화/정렬하거나 수식 또는 식을 추가할 수 있습니다.  
  
-   **차트, 계기, 스파크라인 및 표시기** 를 추가하여 데이터를 시각적 형식으로 요약하고 많은 양의 집계 정보를 한눈에 볼 수 있게 표시합니다.  
  
-   문서 구조, 표시/숨기기 단추, 하위 보고서와 드릴스루 보고서에 대한 드릴스루 링크 등의**대화형 기능을 추가** 합니다. 매개 변수와 필터로 데이터를 필터링하여 사용자 지정 뷰를 만들 수 있습니다.  
  
-   **이미지** 및 외부 콘텐츠를 비롯한 기타 리소스를 포함시키거나 참조합니다.  
  
##  <a name="ManageRpt"></a> 보고서 관리  
  
-   **보고서 정의를 컴퓨터에 저장** 하거나, 다른 사람과 공유하고 직접 관리할 수 있도록 보고서 서버에 저장합니다.  
  
-   보고서를 열 때나 보고서를 연 후에**표시 형식을 선택** 합니다. 웹 기반 형식, 페이지 기반 형식 및 데스크톱 애플리케이션 형식을 선택할 수 있습니다. 표시 형식에는 HTML, MHTML, PDF, XML, CSV, TIFF, Word 및 Excel이 포함됩니다.  
  
-   **구독을 설정합니다.** 보고서 서버나 SharePoint 통합 모드의 보고서 서버에 보고서를 게시하면 보고서가 특정 시간에 실행되도록 구성하고, 보고서 기록을 만들고, 전자 메일 구독을 설정할 수 있습니다.  
  
-   보고서 서비스 Atom 렌더링 확장 프로그램을 사용하여**데이터 피드를 생성** 합니다.  
  
> [!NOTE]  
>  게시된 보고서는 보고서 서버 또는 SharePoint 통합 모드의 보고서 서버에서 보고서 서버 관리자가 관리합니다. 보고서 서버 관리자는 보안을 정의하고 속성을 설정하고 보고서 기록 및 전자 메일 보고서 배달과 같은 작업을 예약할 수 있으며, 공유 일정과 공유 데이터 원본을 만들어 일반적 용도로 사용 가능하도록 할 수 있습니다. 또한 관리자는 모든 보고서 서버 폴더도 관리합니다. 관리 태스크를 수행하는 능력은 사용자 권한에 따라 다릅니다.  
  
## <a name="see-also"></a>참고 항목  
  [보고서 작성기 시작](../../reporting-services/report-builder/start-report-builder.md)  
  
  [보고서 작성기 설치](../../reporting-services/install-windows/install-report-builder.md)

  [SQL Server Reporting Services 및 보고서 작성기의 새로운 기능](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)  
  이 버전의 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]의 새로운 기능에 대해 설명합니다.   
  [자습서: 오프라인에서 빠른 차트 보고서 만들기](../../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)  
 보고서를 만드는 데 사용할 수 있는 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 및 마법사를 소개합니다. 사용할 데이터 집합이 제공되므로 데이터 원본에 연결하지 않고도 시작할 수 있습니다.  
  
 [보고서 계획&#40;보고서 작성기&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md)  
 보고서 작성을 시작하기 전에 고려해야 할 점을 소개합니다.  
  
 [보고서 제작 개념&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 설명서에서 다루는 주요 개념을 정의합니다.  
  
 [보고서 디자인 뷰&#40;보고서 작성기&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)  
 보고서 디자인 뷰의 여러 창 및 영역에 대해 설명합니다.  
  
 [공유 데이터 세트 디자인 뷰&amp;#40;보고서 작성기&amp;#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)  
 공유 데이터 세트 디자인 뷰의 여러 창 및 영역에 대해 설명합니다.  
  
 [바로 가기 키&#40;보고서 작성기&#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]에서 보고서를 탐색 및 디자인하는 데 사용할 수 있는 단축 키에 대해 간단히 설명합니다.  
  

