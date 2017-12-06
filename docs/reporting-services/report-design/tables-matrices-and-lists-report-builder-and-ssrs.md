---
title: "테이블, 행렬 및 목록(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.tablixgroup.f1
- "10045"
- sql13.rtp.rptdesigner.tablix.visibility.f1
- "10039"
- sql13.rtp.rptdesigner.groupproperties.visibility.f1
- "10104"
- "10047"
- sql13.rtp.rptdesigner.groupproperties.advanced.f1
- "10044"
- sql13.rtp.rptdesigner.groupproperties.filters.f1
- sql13.rtp.rptdesigner.tablix.sort.f1
- sql13.rtp.rptdesigner.tablix.general.f1
- sql13.rtp.rptdesigner.groupproperties.general.f1
- sql13.rtp.rptdesigner.groupproperties.variables.f1
- "10046"
- "10101"
- sql13.rtp.rptdesigner.tablix.filter.f1
- sql13.rtp.rptdesigner.groupproperties.sort.f1
- "10042"
- "10041"
- "10102"
- "10103"
- "10043"
- sql13.rtp.rptdesigner.groupproperties.pagebreaks.f1
ms.assetid: 9dcf3fc8-bf9c-4a14-a03d-e78254aa4098
caps.latest.revision: "11"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.openlocfilehash: 310e1f5c45187d5065203f86cafd384318d72ed3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="tables-matrices-and-lists-report-builder-and-ssrs"></a>테이블, 행렬 및 목록(보고서 작성기 및 SSRS)
 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]에서 테이블, 행렬 및 목록은 행과 열로 구성되는 셀에 페이지를 매긴 보고서 데이터를 표시하는 *데이터 영역* 입니다. 셀에는 보통 텍스트, 날짜, 숫자 등의 텍스트 데이터가 포함되지만 계기, 차트, 또는 보고서 항목(예: 이미지)도 포함될 수 있습니다. 테이블, 행렬 및 목록을 집합적으로 *테이블릭스* 데이터 영역이라고 하는 경우가 많습니다.  
  
 테이블, 행렬 및 목록 템플릿은 셀에 데이터를 표시할 수 있는 유동적 눈금인 테이블릭스 데이터 영역에 작성됩니다. 테이블 및 행렬 템플릿에서 셀은 행과 열로 구성됩니다. 템플릿은 일반적인 기본 테이블릭스 데이터 영역의 변형이므로 템플릿 형식의 조합으로 데이터를 표시할 수 있으며, 보고서를 개발할 때 다른 데이터 영역의 기능을 포함하도록 테이블, 행렬 또는 목록을 변경할 수 있습니다. 예를 들어 테이블을 추가했는데 용도에 맞지 않으면 열 그룹을 추가해 테이블을 행렬로 만들 수 있습니다.  
  
 테이블 및 행렬 데이터 영역에 중첩된 테이블, 행렬, 목록, 차트 및 계기를 포함해 복잡한 데이터 관계를 표시할 수 있습니다. 테이블 및 행렬에는 테이블 형식 레이아웃이 있으며 해당 데이터는 단일 데이터 원본에 작성된 단일 데이터 집합에서 제공됩니다. 테이블과 행렬의 가장 큰 차이점은 테이블의 경우 행 그룹만 포함할 수 있지만 행렬은 행 그룹과 열 그룹을 모두 포함할 수 있다는 것입니다.  
  
 목록은 이 두 항목과 약간 다릅니다. 즉, 목록은 자유 레이아웃을 지원하며 각각 다른 데이터 집합의 데이터를 사용하는 피어 테이블 또는 행렬을 여러 개 포함할 수 있습니다. 또한 목록은 송장 등의 양식에도 사용할 수 있습니다.  
  
 다음 그림에서는 테이블, 행렬 또는 목록이 포함된 간단한 보고서를 보여 줍니다.  
  
 ![RS_TableMatrixList](../../reporting-services/report-design/media/rs-tablematrixlist.gif "RS_TableMatrixList")  
  
 테이블, 행렬 및 목록으로 빠르게 시작하려면 [자습서: 기본 테이블 보고서 만들기&#40;보고서 작성기&#41;](../../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md), [자습서: 행렬 보고서 만들기&#40;보고서 작성기&#41;](../../reporting-services/tutorial-creating-a-matrix-report-report-builder.md) 및 [자습서: 자유 형식 보고서 만들기&#40;보고서 작성기&#41;](../../reporting-services/tutorial-creating-a-free-form-report-report-builder.md)를 참조하세요.  
  
> [!NOTE]  
>  테이블, 행렬 및 목록을 보고서와는 별도로 보고서 파트로 게시할 수 있습니다. [보고서 파트](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)에 대해 자세히 알아봅니다.  
  
##  <a name="Table"></a> 테이블  
 세부 데이터를 표시하거나, 데이터를 행 그룹으로 구성하거나, 두 가지 모두를 수행할 때 테이블을 사용합니다. 테이블 템플릿에는 테이블 머리글 행 및 데이터를 위한 정보 행이 있는 세 열이 들어 있습니다. 다음 그림에서는 디자인 화면에서 선택한 초기 테이블 템플릿을 보여 줍니다.  
  
 ![디자인 화면에서 테이블 템플릿 선택](../../reporting-services/report-design/media/rs-tabletemplatenewselected.gif "디자인 화면에서 테이블 템플릿 선택")  
  
 단일 필드, 여러 필드를 기준으로 하거나 사용자 고유의 식을 작성하여 데이터를 그룹화할 수 있습니다. 중첩된 그룹이나 인접한 독립 그룹을 만들고 그룹화된 데이터의 집계된 값을 표시하거나 합계를 그룹에 추가할 수 있습니다. 예를 들어 테이블에 [Category]라는 행 그룹이 있는 경우 각 그룹의 부분합과 보고서의 총합을 모두 추가할 수 있습니다. 테이블의 모양을 개선하고 뚜렷하게 표시할 데이터를 강조하려면 셀을 병합하고 데이터 및 테이블 제목에 서식을 적용할 수 있습니다.  
  
 처음에 정보 데이터나 그룹화된 데이터를 숨길 수 있으며 드릴다운 토글을 포함하여 사용자가 표시할 데이터의 양을 대화형으로 선택하도록 할 수 있습니다.  
  
 자세한 내용은 [테이블&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="Matrix"></a> 행렬  
 피벗 테이블 또는 크로스탭처럼 집계된 데이터 요약을 행 및 열로 그룹화하여 표시할 때 행렬을 사용합니다. 그룹의 행과 열 수는 각 행 및 열 그룹의 고유 값 수에 따라 결정됩니다. 다음 그림에서는 디자인 화면에서 선택한 초기 행렬 템플릿을 보여 줍니다.  
  
 ![도구 상자에서 추가된 새 행렬 선택](../../reporting-services/report-design/media/rs-matrixtemplatenewselected.gif "도구 상자에서 추가된 새 행렬 선택")  
  
 행 및 열 그룹의 여러 필드나 식으로 데이터를 그룹화할 수 있습니다. 런타임에 보고서 데이터 및 데이터 영역이 결합되면 열 그룹에는 열이, 행 그룹에는 행이 추가되면 페이지에서 행렬이 가로와 세로 방향으로 확장됩니다. 행렬 셀에는 셀이 속한 행 및 열 그룹의 교차점으로 한정된 집계 값이 표시됩니다. 예를 들어 행렬에 판매량 합계를 표시하는 행 그룹 하나(Category)와 열 그룹 두 개(Territory, Year)가 있는 경우 보고서에서는 두 개의 셀에 Category 그룹의 각 값에 대한 판매량 합계가 표시됩니다. 셀의 범위가 되는 두 교차점은 범주와 지역 및 범주와 연도입니다. 이 행렬에는 중첩된 그룹과 인접 그룹이 포함될 수 있습니다. 중첩된 그룹에는 부모-자식 관계가 있으며 인접 그룹에는 피어 관계가 있습니다. 행렬 내에 있는 중첩된 행 및 열 그룹의 일부 및 모든 수준에 대해 부분합을 추가할 수 있습니다.  
  
 행렬 데이터를 보다 읽기 쉽게 만들고 뚜렷하게 표시할 데이터를 강조하려면 셀을 가로 또는 세로로 병합하거나 분할하고 데이터 및 그룹 제목에 서식을 적용할 수 있습니다.  
  
 또한 처음에 정보 데이터를 숨기는 드릴다운 토글을 포함할 수도 있습니다. 사용자는 필요한 경우 이 토글을 클릭하여 내용을 자세히 또는 간략히 볼 수 있습니다.  
  
 자세한 내용은 [행렬 만들기](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)를 참조하세요.  
  
##  <a name="List"></a> 목록  
 자유 형식 레이아웃을 만들 때 목록을 사용합니다. 이를 사용하면 모눈 레이아웃에 제한되지 않고 목록 안에서 필드를 자유롭게 배치할 수 있습니다. 목록을 사용하여 여러 데이터 집합 필드를 표시하는 폼을 디자인할 수 있으며, 그룹화된 데이터를 위해 여러 데이터 영역을 나란히 표시하기 위한 컨테이너로 목록을 사용할 수도 있습니다. 예를 들어 직원 레코드나 환자 레코드에서 목록에 대한 그룹을 정의하고, 테이블, 차트 및 이미지를 추가하고, 각 그룹 값에 대해 테이블 및 그래픽 형식으로 값을 표시할 수 있습니다.  
  
 ![도구 상자에서 추가된 새 목록 선택](../../reporting-services/report-design/media/rs-listtemplatenewselected.gif "도구 상자에서 추가된 새 목록 선택")  
  
 자세한 내용은 [목록을 사용하여 송장 및 양식 만들기]를 참조하세요.  
  
##  <a name="PreparingData"></a> 데이터 준비  
 테이블, 행렬 및 목록 데이터 영역에는 데이터 집합의 데이터가 표시됩니다. 데이터 집합의 데이터를 검색하는 쿼리를 사용하거나 테이블, 행렬 또는 목록의 속성을 설정하여 데이터를 준비할 수 있습니다.  
  
 보고서 데이터 집합의 데이터를 검색하는 데 사용하는 [!INCLUDE[tsql](../../includes/tsql-md.md)]등의 쿼리 언어는 데이터 하위 집합만 포함하도록 필터를 적용하고, 보고서를 좀 더 쉽게 읽을 수 있도록 null 값이나 공백을 상수로 바꾸고, 데이터를 정렬 및 그룹화하여 데이터를 준비할 수 있습니다.  
  
 보고서의 테이블, 행렬 또는 목록 데이터 영역에서 데이터를 준비하려는 경우에는 데이터 영역 또는 데이터 영역 내의 셀에 대해 속성을 설정합니다. 데이터를 필터링하거나 정렬하려는 경우에는 데이터 영역에 대해 속성을 설정합니다. 예를 들어 데이터를 정렬하려면 정렬할 열과 정렬 방향을 지정합니다. 필드에 다른 값을 제공하려는 경우에는 필드를 표시하는 셀 텍스트의 값을 설정합니다. 예를 들어 필드가 비어 있거나 null인 경우 Blank를 표시하려면 식을 사용해 해당 값을 설정합니다.  
  
 자세한 내용은 [테이블릭스 데이터 영역에 표시하기 위한 데이터 준비&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/preparing-data-for-display-in-a-tablix-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
##  <a name="BuildingConfiguringTableMatrixList"></a> 테이블, 행렬 또는 목록 작성 및 구성  
 보고서에 테이블 또는 행렬을 추가할 때는 테이블 및 행렬 마법사를 사용하거나 보고서 작성기 및 보고서 디자이너가 제공하는 템플릿에서 수동으로 테이블 또는 행렬을 작성합니다. 목록은 목록 템플릿에서 수동으로 작성합니다.  
  
 마법사는 테이블 또는 행렬을 빠르게 작성 및 구성하는 과정을 단계별로 안내합니다. 마법사를 완료한 후 또는 테이블릭스 데이터 영역을 처음부터 작성하는 경우에는 테이블 또는 행렬을 보다 자세하게 구성하고 상세하게 설정할 수 있습니다. 데이터 영역에서 마우스 오른쪽 단추를 클릭하면 표시되는 대화 상자를 사용하면 페이지 나누기, 머리글/바닥글 반복 및 표시 여부, 표시 옵션, 필터 및 정렬에 가장 일반적으로 사용되는 속성을 쉽게 설정할 수 있습니다. 그러나 테이블릭스 데이터 영역에서는 보다 많은 속성이 추가로 제공되는데, 이들 속성은 보고서 작성기의 속성 창에서만 설정할 수 있습니다. 예를 들어 테이블, 행렬 또는 목록의 데이터 집합이 비어 있을 때 메시지를 표시하려면 속성 창의 NoRowsMessage 테이블릭스 속성에서 메시지 텍스트를 지정할 수 있습니다.  
  
##  <a name="ChangingBetweenTablixTemplates"></a> 테이블릭스 템플릿 간 변경  
 초기 테이블릭스 템플릿만 선택할 수 있는 것은 아닙니다. 그룹, 합계 및 레이블을 추가하다 보면 테이블릭스 디자인의 수정이 필요할 수 있습니다. 예를 들어 테이블로 시작했지만 나중에 정보 행을 삭제하고 열 그룹을 추가할 수 있습니다. 자세한 내용은 [테이블릭스 데이터 영역의 유연성 살펴보기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
 원하는 테이블릭스 기능을 추가하여 테이블, 행렬 또는 목록을 계속 개발할 수 있습니다. 테이블릭스 기능에는 세부 데이터를 표시하는 기능이나 그룹화된 데이터의 집계를 행과 열에 표시하는 기능이 포함됩니다. 중첩된 그룹, 독립적인 인접 그룹 또는 재귀적 그룹을 만들 수 있습니다. 그룹화된 데이터를 필터링하고 정렬할 수 있으며 그룹 정의에 여러 개의 그룹 식을 포함하여 그룹을 쉽게 결합할 수 있습니다.  
  
 또한 그룹 합계나 데이터 영역의 총합계도 추가할 수 있습니다. 드릴다운 보고서처럼 사용자가 숨겨진 데이터의 표시를 전환할 수 있도록 하고 보고서를 단순화하기 위해 행이나 열을 숨길 수 있습니다. 자세한 내용은 [보고서 페이지에서 테이블릭스 데이터 영역 표시 제어&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)를 참조하세요.  
  
##  <a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에는 보고서에서 테이블, 행렬 및 목록을 사용하는 방법, 행 및 열에 데이터를 표시하는 방법, 열을 추가/삭제하고 셀을 병합하고 행 및 열 그룹의 부분합을 포함하는 방법을 단계별로 보여 주는 절차가 나열되어 있습니다.  
  
-   [세부 정보 그룹 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-details-group-report-builder-and-ssrs.md)  
  
-   [그룹 또는 테이블릭스 데이터 영역에 합계 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)  
  
-   [셀 내 항목 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/change-an-item-within-a-cell-report-builder-and-ssrs.md)  
  
-   [행 높이 또는 열 너비 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/change-row-height-or-column-width-report-builder-and-ssrs.md)  
  
-   [열 삽입 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)  
  
-   [행 삽입 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-row-report-builder-and-ssrs.md)  
  
-   [데이터 영역의 셀 병합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/merge-cells-in-a-data-region-report-builder-and-ssrs.md)  
  
-   [재귀 계층 구조 그룹 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)  
  
-   [데이터 영역에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
-   [그룹과 함께 머리글 및 바닥글 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
-   [단계별 보고서 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/create-a-stepped-report-report-builder-and-ssrs.md)  
  
-   [테이블, 행렬 또는 목록 추가, 이동 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs.md)  
  
##  <a name="InThisSection"></a> 섹션 내용  
 다음 항목에서는 테이블릭스 데이터 영역 작업에 대한 추가 정보를 제공합니다.  
  
 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)  
 테이블릭스의 영역, 세부 데이터 및 그룹화된 데이터, 열 및 행 그룹, 정적/동적 행 및 열과 같은 테이블릭스 데이터 영역과 관련된 주요 개념에 대해 설명합니다.  
  
 [테이블릭스 데이터 영역에 데이터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/adding-data-to-a-tablix-data-region-report-builder-and-ssrs.md)  
 세부 데이터/그룹화된 데이터, 부분합/합계, 및 레이블을 테이블릭스 데이터 영역에 추가하는 방법에 대한 자세한 정보를 제공합니다.  
  
 [보고서 페이지에서 테이블릭스 데이터 영역 표시 제어&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)  
 보고서에서 테이블릭스 데이터 영역이 표시되는 방법을 변경할 수 있는 테이블릭스 데이터 영역의 속성에 대해 설명합니다.  
  
 [행 및 열 제목 제어&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/controlling-row-and-column-headings-report-builder-and-ssrs.md)  
 테이블, 행렬 또는 목록 데이터 영역이 가로 또는 세로로 여러 페이지에 걸쳐 있는 경우 행 및 열 머리글을 제어하는 방법에 대해 설명합니다.  
  
 [재귀 계층 구조 그룹 생성&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)  
 부모와 자식 간의 관계가 데이터 집합의 필드에 표시되는 재귀적 데이터를 표시하는 방법에 대해 설명합니다.  
  
 [그룹 이해&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)  
 그룹의 의미 및 그룹을 사용하는 경우와 각 테이블릭스 데이터 영역에 사용할 수 있는 그룹에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [중첩된 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [동일한 데이터 집합에 여러 데이터 영역 연결&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [계기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
