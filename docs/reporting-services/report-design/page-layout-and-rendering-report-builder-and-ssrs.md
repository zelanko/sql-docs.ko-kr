---
title: 페이지 레이아웃 및 렌더링(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: e2358653-35bc-4496-810a-d3ccf02f229f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d525d686b8be1e17214dd8908017b86358f87ec2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606001"
---
# <a name="page-layout-and-rendering-report-builder-and-ssrs"></a>페이지 레이아웃 및 렌더링(보고서 작성기 및 SSRS)
페이지 레이아웃, 페이지 나누기 및 페이지 크기를 비롯하여 원하는 방식으로 보고서를 작성해야 하므로 페이지를 매긴 보고서에 대한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 렌더링 확장을 읽어보세요. 

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 또는 보고서 작성기나 보고서 디자이너의 미리 보기 창에서 보고서를 보면 보고서가 HTML 렌더러에 의해 처음 렌더링됩니다. 그런 다음 Excel 또는 쉼표로 분리된(CSV) 파일과 같은 여러 가지 형식으로 보고서를 내보낼 수 있습니다. 내보낸 보고서는 Excel에서 자세히 분석하기 위해 사용하거나 CSV 파일을 가져오고 사용할 수 있는 응용 프로그램의 데이터 원본으로 사용할 수 있습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 보고서를 여러 다른 형식으로 내보내는 데 사용할 수 있는 렌더러 집합이 포함되어 있습니다. 각 렌더러는 보고서를 렌더링할 때 규칙을 적용합니다. 보고서를 다른 파일 형식으로 내보낼 때, 특히 실제 페이지 크기에 따라 페이지 매김을 사용하는 Adobe Acrobat(PDF) 렌더러와 같은 렌더러의 경우 내보낸 보고서 모양을 유지하고 렌더링 규칙이 적용된 후 제대로 인쇄되도록 보고서의 레이아웃을 변경해야 할 수 있습니다.  
  
 내보낸 보고서에 대한 최상의 결과를 얻는 것은 일반적으로 반복적인 프로세스입니다. 즉, 보고서 작성기 또는 보고서 디자이너에서 보고서를 작성하고 미리 본 후 원하는 형식으로 보고서를 내보내고 내보낸 보고서를 검토한 다음 보고서를 변경합니다.  
    
##  <a name="PageLayout"></a> 보고서 항목  
 보고서 항목은 서로 다른 유형의 보고서 데이터와 관련된 레이아웃 요소입니다. 
 
* 테이블, 행렬, 목록, 차트 및 계기는 각각 보고서 데이터 집합에 연결되는 데이터 영역 보고서 항목입니다. 보고서를 처리하면 데이터 영역이 보고서 페이지의 가로 및 아래쪽으로 확장되어 데이터를 표시합니다. 

다른 보고서 항목은 단일 항목에 연결되고 단일 항목을 표시합니다. 
* **이미지** 보고서 항목은 그림에 연결됩니다. 
* **입력란** 보고서 항목에는 제목과 같은 단순 텍스트 또는 기본 제공 필드, 보고서 매개 변수 또는 데이터 집합 필드에 대한 참조를 포함할 수 있는 식이 포함될 수 있습니다. 
* **선** 및 **사각형** 보고서 항목은 보고서 페이지에 단순 그래픽 요소를 제공합니다. **사각형** 은 다른 보고서 항목의 컨테이너가 될 수도 있습니다. 

보고서에는 하위 보고서가 포함될 수도 있습니다.  
  
## <a name="page-layout"></a>페이지 레이아웃

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 사용하면 보고서 항목을 디자인 화면의 어느 위치에든 자유롭게 배치할 수 있습니다. 맞춤 선 및 크기 조정 핸들을 사용하여 보고서 항목의 초기 모양을 대화형으로 배치, 확장 및 축소할 수 있습니다. 여러 데이터 집합(또는 서로 다른 형식의 동일한 데이터인 경우)이 나란히 위치하도록 데이터 영역을 배치할 수 있습니다. 디자인 화면에 보고서 항목을 배치할 때 보고서 항목의 크기와 모양은 기본값으로 적용되며 해당 보고서 항목은 다른 모든 보고서 항목과 초기 관계를 형성합니다. 
 
 보고서 항목을 다른 보고서 항목 안에 배치하여 더 복잡한 보고서 디자인을 만들 수 있습니다. 예를 들어 테이블 셀에 차트 또는 이미지를 배치하고, 테이블 셀에 테이블을 배치하고, 사각형에 여러 이미지를 배치할 수 있습니다. 보고서에 원하는 구성과 모양을 제공하는 이외에도 사각형 등의 컨테이너에 보고서 항목을 배치하여 보고서 페이지에 보고서 항목을 표시하는 방식을 제어할 수도 있습니다.  
  
 보고서는 각 페이지에서 반복되는 페이지 머리글 및 페이지 바닥글과 함께 여러 페이지를 확장할 수 있습니다. 보고서는 이미지 및 선과 같은 그래픽 요소를 포함할 수 있으며 식을 기반으로 할 수 있는 여러 글꼴, 색 및 스타일을 포함할 수 있습니다.  
  
##  <a name="ReportSections"></a> 보고서 섹션  
 보고서는 3개의 주요 구역인 선택적 *페이지* 머리글, 선택적 *페이지* 바닥글 및 보고서 본문으로 구성됩니다. *보고서* 머리글과 바닥글은 보고서의 개별 구역이 아니지만 오히려 보고서 본문의 맨 위 및 맨 아래에 배치되는 보고서 항목으로 구성됩니다. 보고서 각 페이지의 맨 위와 맨 아래에 배치되는 페이지 머리글과 페이지 바닥글에는 같은 내용이 반복되어 나타납니다. 머리글과 바닥글에 이미지, 입력란 및 선을 배치할 수 있습니다. 보고서 본문에 모든 유형의 보고서 항목을 배치할 수 있습니다.  
  
 보고서 항목의 속성을 설정하여 페이지에서 보고서 항목을 처음에 숨기거나 표시할 수 있습니다. 데이터 영역의 행이나 열 또는 그룹에 표시 유형 속성을 설정할 수 있으며 사용자가 보고서 데이터를 대화형으로 표시 또는 숨길 수 있도록 토글 단추를 제공할 수 있습니다. 보고서 매개 변수를 기반으로 하는 식을 비롯한 식을 사용하여 표시 유형 또는 초기 표시 유형을 설정할 수 있습니다.  
  
 보고서가 처리되면 보고서 데이터가 보고서 레이아웃 요소와 결합되고 결합된 데이터가 보고서 렌더러로 전송됩니다. 렌더러는 보고서 항목 확장에 대한 미리 정의된 규칙을 따르고 각 페이지에 들어가는 데이터의 양을 판단합니다. 사용할 렌더러에 대해 최적화된 쉽게 읽을 수 있는 보고서를 디자인하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 페이지 매김을 제어하는 데 사용되는 규칙을 이해해야 합니다. 자세한 내용은 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="RenderingExtensions"></a> 렌더러  
 Reporting Services에는 보고서를 다른 형식으로 내보내는 데 사용할 수 있는 렌더러의 집합이 포함되어 있습니다. 렌더러를 렌더링 확장 프로그램이라고도 합니다. 렌더러에는 세 가지 종류가 있습니다.  
  
-   **데이터 렌더러** 데이터 렌더러는 보고서에서 서식 및 레이아웃 정보를 모두 제거하고 데이터만 표시합니다. 생성된 파일은 Excel 등의 다른 파일 형식, 다른 데이터베이스, XML 데이터 메시지 또는 사용자 지정 응용 프로그램으로 원시 보고서 데이터를 가져오는 데 사용할 수 있습니다. 사용 가능한 데이터 렌더러는 CSV 및 XML입니다.  
  
    > [!NOTE]  
    >  Atom 렌더링은 다른 형식으로 직접 내보낼 수는 없지만 보고서에서 데이터 파일을 생성합니다.  
  
-   **소프트 페이지 나누기 렌더러** 소프트 페이지 나누기 렌더러에서는 보고서 레이아웃과 서식이 유지됩니다. 생성된 파일은 웹 페이지 등의 화면 중심 보기 및 배달용으로 최적화됩니다. 사용할 수 있는 소프트 페이지 나누기 렌더러는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word, 웹 보관 파일(MHTML) 및 HTML입니다.  
  
-   **하드 페이지 나누기 렌더러** 하드 페이지 나누기 렌더러에서는 보고서 레이아웃과 서식이 유지됩니다. 생성되는 파일은 인쇄 환경을 일정하게 유지하거나 온라인에서 책 형태로 보고서를 볼 수 있도록 최적화됩니다. 사용할 수 있는 하드 페이지 나누기 렌더러는 TIFF 및 PDF입니다.  
  
 보고서 작성기 또는 보고서 디자이너에서 보고서를 미리 보거나 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에서 보고서를 실행하면 보고서는 항상 먼저 HTML로 렌더링됩니다. 보고서를 실행한 후에는 다른 파일 형식으로 내보낼 수 있습니다. 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)에서 페이지 매김을 제어하는 데 사용되는 규칙을 이해해야 합니다.  
  
##  <a name="RenderingBehaviors"></a> 렌더링 동작  
 선택한 렌더러에 따라 보고서를 렌더링할 때 특정 규칙이 적용됩니다. 여러 보고서 항목이 한 페이지에 함께 포함되는 방식은 다음과 같은 요소의 조합에 따라 결정됩니다.  
  
-   렌더링 규칙  
-   보고서 항목의 너비와 높이  
-   보고서 본문의 크기  
-   페이지의 너비와 높이  
-   렌더러별 페이징 지원  
  
 예를 들어 HTML 및 MHTML 형식으로 렌더링된 보고서는 다양한 길이의 페이지가 표시되는 컴퓨터 화면 기반 환경에 최적화됩니다.  
  
 자세한 내용은 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)을 참조하세요.  
   
##  <a name="Pagination"></a> 페이지 매김  
 페이지 매김이란 보고서 내의 페이지 수와 이러한 페이지에 보고서 항목이 정렬되는 방식을 의미합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서의 페이지 매김은 보고서를 보거나 배달하는 데 사용하는 렌더링 확장 프로그램과 보고서에서 사용하도록 구성하는 페이지 나누기 및 한 페이지에 표시 옵션에 따라 다릅니다.  
  
 보고서를 배달하는 데 사용할 렌더러에 최적화되고 사용자가 쉽게 읽을 수 있는 보고서를 성공적으로 디자인하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 페이지 매김을 제어하는 데 사용되는 규칙을 이해할 필요가 있습니다. **데이터** 와 **소프트 페이지** 렌더링 확장 프로그램을 사용하여 내보낸 보고서는 일반적으로 페이지 매김의 영향을 받지 않습니다. 데이터 렌더링 확장 프로그램을 사용하는 경우 보고서가 XML 또는 CSV 형식의 테이블 형식 행 집합으로 렌더링됩니다. 내보낸 보고서 데이터를 사용할 수 있도록 하려면 보고서에서 평면화된 표 형식 행 집합을 렌더링하기 위해 규칙이 적용되는 방식을 이해해야 합니다.  
  
 HTML 렌더링 확장 프로그램과 같은 **소프트 페이지** 렌더링 확장 프로그램을 사용하는 경우 보고서가 인쇄되는 모양과 PDF와 같은 하드 페이지 렌더러를 사용하여 보고서가 얼마나 효과적으로 렌더링되는지도 알아보고 싶을 수 있습니다. 보고서를 만들거나 업데이트하는 동안 보고서 작성기 및 보고서 디자이너에서 보고서를 미리 보고 내보낼 수 있습니다.  
  
 **하드 페이지** 렌더러는 보고서 레이아웃과 실제 페이지 크기에 가장 큰 영향을 미칩니다. 자세한 내용은 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)을 참조하세요.  
   
##  <a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에는 보고서에서 페이지 매김을 사용하여 작업하는 방법을 단계별로 보여 주는 절차가 나열되어 있습니다.  
  
-   [페이지 나누기 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md)  
  
-   [여러 페이지에 행 및 열 머리글 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)  
  
-   [페이지 머리글/바닥글 추가 또는 제거&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)  
  
-   [보고서를 스크롤할 때 머리글 계속 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
-   [페이지 번호 또는 기타 보고서 속성 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md)  
  
-   [첫 페이지 또는 마지막 페이지에서 페이지 머리글 또는 바닥글 숨기기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md)  
  
##  <a name="InThisSection"></a> 섹션 내용  
 다음 항목에서는 페이지 레이아웃 및 렌더링에 대한 추가 정보를 제공합니다.  
  
 [페이지 머리글 및 바닥글&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)  
 보고서의 머리글 및 바닥글을 사용하는 방법과 이를 사용하여 페이지 매김을 제어하는 방법에 대해 설명합니다.  
  
 [페이지 나누기, 머리글, 열 및 행 제어&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)  
 페이지 나누기를 사용하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [여러 보고서 렌더링 확장 프로그램의 대화형 기능&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
