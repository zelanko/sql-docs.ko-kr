---
title: "Reporting Services의 보고서 디자인 문제 해결 | Microsoft Docs"
ms.custom: 
ms.date: 02/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a0d103da-5a3e-475c-a71a-9e23476095e2
caps.latest.revision: "5"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6d9a5cbd4b8065a7344eeec2d7cd495e656ec941
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="troubleshoot-report-design-issues-with-reporting-services"></a>Reporting Services의 보고서 디자인 문제 해결
보고서 디자인 문제는 보고서 제작 응용 프로그램의 디자인 뷰에서 보고서 레이아웃을 만들 때 발생할 수 있습니다. 이 항목에서는 이러한 문제를 해결하는 데 유용한 정보를 제공합니다.   
  
## <a name="why-does-my-text-box-show-only-a-single-value-and-not-repeat-for-every-row"></a>입력란에 단일 값만 표시되고 모든 행에 대해 반복되지 않는 이유  
데이터 집합 필드 참조를 포함하는 입력란이 한 번만 렌더링되고 데이터 집합에 첫 번째 값이 표시됩니다.   
  
**입력란 부모가 보고서 본문인 경우**  
  
  
디자인 화면에 직접 추가된 입력란은 데이터 집합의 집계 값만 표시할 수 있습니다.  
  
입력란의 부모 컨테이너를 확인하려면 입력란을 선택하고 속성 창에서 **부모**로 스크롤합니다.   
  
각 값을 데이터 집합에 표시하는 입력란이 필요할 경우 테이블 또는 행렬과 같은 데이터 영역을 사용합니다. 기본적으로 테이블 또는 행렬의 각 셀은 입력란을 포함합니다. 데이터 집합 필드를 각 셀로 드래그합니다.   
  
## <a name="why-cant-i-add-total-pages-to-my-report"></a>보고서에 전체 페이지 수를 추가할 수 없는 이유  
기본 제공 필드 `[&PageNumber]` 및 `[&TotalPages]` 는 보고서 본문에서 유효하지 않습니다.   
  
PageNumber 및 TotalPages는 페이지 머리글 및 페이지 바닥글에서만 유효합니다.  
  
  
기본 제공 필드 [&PageNumber] 및 [&TotalPages]는 페이지 머리글 및 페이지 바닥글에서만 사용할 수 있습니다.   
  
보고서에 [&PageNumber] 또는 [&TotalPages]를 추가하려면 먼저 페이지 머리글 또는 페이지 바닥글을 추가해야 합니다. 자세한 내용은 [페이지 머리글 추가 또는 제거](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
> 페이지 머리글 또는 페이지 바닥글에 [&TotalPages]를 포함하면 보고서 처리에 영향을 줄 수 있습니다. 자세한 내용은 보고서 문제 해결: 특정 파일 형식으로 내보낸 보고서를 참조하세요.  
[Reporting Services 보고서의 처리 문제 해결](../../reporting-services/troubleshooting/troubleshoot-processing-of-reporting-services-reports.md).  
  
## <a name="how-do-i-design-two-tables-or-a-chart-and-a-table-to-display-side-by-side"></a>두 테이블 또는 한 차트와 한 테이블을 나란히 표시하도록 디자인하는 방법  
보고서 디자인 환경은 현재 화면에 표시된 내용과 출력 내용이 동일한 WYSISYG 환경이 아닙니다. 보고서 처리기는 공백, 컨테이너 및 식과 같은 보고서 레이아웃 정보와 데이터 및 보고서 항목을 조합하여 컴파일된 보고서를 생성하고, 이렇게 생성된 보고서는 보고서 렌더러로 전달되고, 보고서 렌더러는 지정된 보기 환경에 맞게 보고서의 "레이아웃"을 지정하여 HTML 브라우저 또는 파일 형식에 대한 대화형 기능을 제공합니다. 자동 레이아웃 알고리즘에서 생성한 보고서 레이아웃을 변경할 수도 있습니다.   
  
### <a name="rendering-rules-use-page-size-containers-peer-objects-relative-placement-and-white-space-to-determine-layout"></a>렌더링 규칙에서 페이지 크기, 컨테이너, 피어 개체, 상대 위치 및 공백을 사용하여 레이아웃을 결정  
일반적으로 보고서는 데이터의 크기에 맞게 커지고 다른 보고서 항목을 밀어냅니다.   
  
여러 데이터 영역 또는 보고서 항목을 하나로 그룹화하려면 이를 동일 부모 컨테이너에 넣습니다. 예를 들어 차트 및 테이블을 사각형 컨테이너에 넣고 각 요소의 위쪽 가장자리를 정렬하여 나란히 표시할 수 있습니다. 자세한 내용은 [보고서 작성기에서 렌더링 동작](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
[Reporting Services 보고서에서 데이터 검색 문제 해결](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Reporting Services 구독 및 배달 문제 해결](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]

