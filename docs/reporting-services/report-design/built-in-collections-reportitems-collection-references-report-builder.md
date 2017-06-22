---
title: "ReportItems 컬렉션 참조 (보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edc0c75f-0530-4e6d-85aa-3385301bfd00
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: cfa69eca6201980d4449c28a8a7018846fd4e4a0
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="built-in-collections---reportitems-collection-references-report-builder"></a>기본 제공 컬렉션-ReportItems 컬렉션 참조 (보고서 작성기)
  **ReportItems** 기본 제공 컬렉션은 데이터 영역의 행 또는 보고서 디자인 화면의 입력란과 같은 보고서 항목의 입력란 집합입니다. **ReportItems** 컬렉션에는 페이지 머리글, 페이지 바닥글 또는 보고서 본문의 현재 범위에 있는 입력란이 포함됩니다. 이 컬렉션은 보고서 처리기 및 보고서 렌더러에 의해 런타임에 결정됩니다. 현재 범위는 사용자가 보고서 페이지를 볼 때 보고서 처리기가 보고서 데이터 및 보고서 항목 레이아웃 요소를 연속적으로 조합함에 따라 변경됩니다. **ReportItems** 기본 제공 컬렉션을 사용하여 각 페이지의 첫 번째 및 마지막 항목을 표시하는 사전 스타일의 페이지 머리글을 만들 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-reportitems-value-property"></a>ReportItems 값 속성 사용  
 **ReportItems** 컬렉션 내의 항목에는 Value라는 하나의 속성만 있습니다. **ReportItems** 항목의 값을 사용하면 보고서에 있는 다른 필드의 데이터를 표시하거나 계산할 수 있습니다. 현재 입력란의 값에 액세스하려는 경우 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 기본 제공 전역 Me.Value를 사용하거나 그냥 Value만 사용할 수 있습니다. First와 같은 보고서 함수 및 집계 함수에서는 정규화된 구문을 사용해야 합니다.  
  
 예를 들어  
  
-   이 식을 입력란에 배치하면 `Textbox1`이라는 **ReportItem** 입력란의 값이 표시됩니다.  
  
     `=ReportItems!Textbox1.Value`  
  
-   이 식을 **ReportItem** 입력란 Color 속성에 배치하면 값이 > 0인 경우 텍스트가 검정색으로 표시되고 그렇지 않으면 빨간색으로 표시됩니다.  
  
     `=IIF(Me.Value > 0,"Black","Red")`  
  
-   이 식을 페이지 머리글 또는 페이지 바닥글의 입력란에 배치하면 `LastName`이라는 입력란에 대해 렌더링된 보고서의 페이지별 첫 번째 값이 표시됩니다.  
  
     `=First(ReportItems("LastName").Value)`  
  
## <a name="dictionary-style-page-header-expressions"></a>사전 스타일의 페이지 머리글 식  
 페이지의 첫 번째 고객과 마지막 고객을 표시하는 페이지 머리글을 만들 수 있습니다. 페이지 머리글의 입력란은 식에서 **ReportItems** 기본 제공 컬렉션을 한 번만 참조할 수 있으므로 페이지 머리글에 두 개의 입력란을 추가해야 합니다. 하나는 첫 번째 고객 이름에 대한 입력란(`=First(ReportItems!textboxLastName.Value`)이고 다른 하나는 마지막 고객 이름에 대한 입력란(`=Last(ReportItems!textboxLastName.Value`)입니다.  
  
 페이지 머리글 또는 페이지 바닥글 섹션에서는 현재 페이지의 입력란만 **ReportItems** 컬렉션의 멤버로 사용할 수 있습니다. 예를 들어 `ReportItems!textboxLastName.Value` 가 다중 페이지 데이터 영역에 대한 첫 번째 페이지에만 표시되는 입력란을 참조할 경우 첫 번째 페이지에 대한 값은 볼 수 있지만 다른 모든 페이지에는 식이 작성된 대로 계산될 수 없음을 나타내는 **#오류** 가 표시됩니다.  
  
## <a name="scope-for-the-reportitems-collection"></a>ReportItems 컬렉션의 범위  
 보고서가 처리될 때 보고서 본문 또는 데이터 영역의 각 입력란은 해당 데이터 집합, 데이터 영역 및 그룹 연결의 컨텍스트에서 계산됩니다. **ReportItems** 컬렉션에 대한 참조의 범위는 현재 범위 또는 현재 범위보다 높은 모든 지점입니다.  
  
 예를 들어 부모 그룹에 있는 행의 입력란은 자식 그룹 행에 있는 입력란의 이름을 참조하는 식을 포함하면 안 됩니다. 이러한 식은 자식 행 입력란이 범위를 벗어나기 때문에 보고서의 값으로 확인되지 않습니다. 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
