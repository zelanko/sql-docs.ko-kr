---
title: HTML로 렌더링(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: cf559b0a-499a-4d74-b520-b382b87e0b17
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 83485916e0dcfeb02555e3068931415801691692
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56296851"
---
# <a name="rendering-to-html-report-builder-and-ssrs"></a>HTML로 렌더링(보고서 작성기 및 SSRS)
  HTML 렌더링 확장 프로그램은 보고서를 HTML 형식으로 렌더링합니다. 완전한 형식의 HTML 페이지 또는 HTML 조각을 만들어 다른 HTML 페이지에 포함시킬 수도 있습니다. 모든 HTML은 UTF-8 인코딩을 사용하여 만들어집니다.  
  
 HTML 렌더링 확장 프로그램은 보고서 관리자에서 실행될 때를 포함하여 브라우저에 표시되는 보고서의 기본 렌더링 확장 프로그램입니다.  
  
 HTML 렌더링 확장 프로그램은 보고서 관리자에서 실행될 때를 포함하여 브라우저에 표시되는 보고서의 기본 렌더링 확장 프로그램입니다. HTML 렌더링 확장 프로그램은 HTML을 조각 또는 전체 HTML 문서로 렌더링할 수 있습니다. HTML이 조각인 경우 HTML 문서의 `HEAD`, `HTML` 및 `BODY` 태그는 제거되고 `BODY` 태그의 내용만 렌더링됩니다. 이 기능은 다른 애플리케이션에서 만든 HTML에 HTML을 포함하는 경우에 유용합니다.  
  
 일부 시나리오에서는 보고서를 HTML로 렌더링할 때 보고서 매개 변수를 사용하여 스크립트 삽입 공격을 시작할 수 있습니다. 보고서를 안전하게 보호하는 방법에 대한 자세한 내용은 [보고서 및 리소스 보안](../security/secure-reports-and-resources.md)을 참조하세요.  
  
 브라우저에 대 한 자세한 내용은 참조 하세요. [Reporting Services 및 파워 뷰 브라우저 지원 계획 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RenderingMHTML"></a> MHTML로 렌더링  
 HTML 렌더링 확장 프로그램은 보고서를 MHTML(MIME Encapsulation of Aggregate HTML Documents)로도 렌더링할 수 있습니다. MHTML은 HTML을 확장하여 이미지와 같이 인코딩된 개체를 HTML에 포함합니다. MHTML 렌더링 확장 프로그램을 사용하여 이미지, 문서 또는 다른 이진 파일과 같은 리소스를 보고서 HTML 내의 MIME 구조로 단일 파일에 포함할 수 있습니다. MHTML 보고서에는 모든 리소스가 포함되어 있으므로 MHTML 보고서는 전자 메일 메시지 내에 포함하는 데에도 유용합니다. 이 기능은 실제로는 MHTML을 렌더링하는 HTML 렌더링 확장 프로그램이지만, MHTML 렌더링 확장 프로그램이라고 부릅니다.  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘") [맨 위로 이동](#BackToTop)  
  
##  <a name="BrowserSupport"></a> 브라우저 지원  
 이 렌더링 확장 프로그램은 다음 브라우저 버전을 지원합니다.  
  
-   Internet Explorer 5.5 이상  
  
-   Firefox 1.5 이상  
  
-   Safari 3.0 이상  
  
 브라우저 간 고려 사항으로 인해 렌더링된 보고서는 브라우저마다 조금씩 다를 수 있습니다. 예를 들어 입력란에는 WritingMode라는 속성이 들어 있습니다. 이 속성은 Firefox에서 지원되지 않습니다.  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘") [맨 위로 이동](#BackToTop)  
  
##  <a name="HTMLSpecificRenderingRules"></a> HTML 관련 렌더링 규칙  
 렌더링할 때에는 다음과 같은 HTML 관련 규칙이 적용됩니다.  
  
-   렌더러는 항목이 여러 개인 경우 각 `ReportItems` 컬렉션의 모든 항목을 포함하기 위한 HTML 테이블 구조를 작성합니다.  
  
-   테이블 구조 내부의 모든 항목은 각각 단일 셀을 차지합니다.  
  
-   빈 셀은 HTML 크기를 줄이기 위해 가능한 한 축소됩니다.  
  
-   브라우저가 테이블을 렌더링하는 속도가 향상되도록 빈 셀로 구성된 행은 위쪽 가장자리에 추가되고 다른 열은 왼쪽 가장자리에 추가됩니다.  
  
-   항목이 들어있지 않으므로 항목 간 간격에 불과한 테이블의 행 또는 열에는 고정 너비 및 높이가 부여됩니다.  
  
-   다른 모든 행 및 열은 각 보고서 항목의 크기에 따라 커질 수 있습니다.  
  
-   모든 좌표 및 보고서 항목 크기는 밀리미터로 변환됩니다. 스타일 속성을 비롯한 다른 모든 크기에는 원래의 단위가 유지됩니다. 0.2mm보다 작은 크기 및 위치 차이는 0mm로 처리됩니다.  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘") [맨 위로 이동](#BackToTop)  
  
##  <a name="Interactivity"></a> 상호 작용  
 HTML에서는 일부 대화형 요소가 지원됩니다. 다음은 특정 동작에 대한 설명입니다.  
  
### <a name="show-and-hide"></a>표시 및 숨기기  
 표시 유형을 전환할 수 있는 보고서 항목은 +/- 토글 이미지와 함께 렌더링되며 클릭할 수 있습니다. 항목을 클릭하면 서버에 대한 콜백이 발생하여 변경된 표시/숨기기 상태로 출력이 다시 렌더링됩니다.  
  
### <a name="document-map"></a>문서 구조  
 문서 구조 레이블이 렌더링되고 뷰어 컨트롤에서 문서 구조를 사용하여 탐색할 수 있습니다. 데이터 영역 머리글이 생략된 경우 레이블은 첫 번째 자식 셀에 렌더링됩니다. 자식 셀이 없으면 레이블은 그 앞에 있는 자식에 렌더링됩니다.  
  
### <a name="bookmarks"></a>책갈피  
 책갈피 링크는 렌더링되어 하이퍼링크로 표시됩니다. 책갈피 대상이 렌더링되고 책갈피 링크를 클릭하여 탐색할 수 있습니다. 책갈피 링크를 클릭하면 제일 앞에 있는 대상 책갈피 레이블로 보고서가 이동하며 가능한 경우 해당 책갈피 링크가 창의 맨 위에 오도록 브라우저가 스크롤됩니다. HTML 앵커(\<a>) 태그를 사용하여 책갈피 대상이 표시됩니다.  
  
### <a name="interactive-sorting"></a>대화형 정렬  
 입력란에 사용자 정렬이 정의되어 있으면 HTML 렌더링 확장 프로그램은 입력란의 정렬 아이콘을 입력란 내용의 오른쪽에 렌더링합니다. 보고서에 사용자 정렬이 정의된 입력란이 포함되어 있으면 정렬 이미지가 클릭될 때 서버로 포스트백을 보낼 JavaScript가 렌더링됩니다.  
  
### <a name="hyperlinks-and-drillthrough"></a>하이퍼링크 및 드릴스루  
 하이퍼링크 및 드릴스루 링크는 해당 링크가 정의된 보고서 항목 주위의 HTML 앵커(\<a>) 태그를 사용하여 보고서 항목에 대한 하이퍼링크로 렌더링됩니다.  
  
### <a name="search"></a>검색  
 검색 기능을 통해 사용자는 보고서 내의 텍스트 문자열을 검색할 수 있습니다.  
  
 ReportViewer Web Forms 컨트롤을 통해 추가 검색 및 찾기 기능이 제공됩니다.  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘") [맨 위로 이동](#BackToTop)  
  
##  <a name="DeviceInfo"></a> 장치 정보 설정  
 디바이스 정보 설정을 변경하여 렌더링할 모드를 비롯한 이 렌더러의 일부 기본 설정을 변경할 수 있습니다. 자세한 내용은 [HTML Device Information Settings](../html-device-information-settings.md)을 참조하세요.  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘") [맨 위로 이동](#BackToTop)  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [여러 보고서 렌더링 확장 프로그램의 대화형 기능&#40;보고서 작성기 및 SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [보고서 항목 렌더링&#40;보고서 작성기 및 SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
