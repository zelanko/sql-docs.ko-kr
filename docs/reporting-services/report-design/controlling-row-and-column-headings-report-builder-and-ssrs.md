---
title: 행 및 열 머리글 제어(보고서 작성기 및 SSRS) | Microsoft Docs
description: 페이지를 매긴 보고서에서 테이블, 행렬 또는 목록 데이터 영역을 사용하는 방법을 알아봅니다. 이를 통해 보고서 작성기에서 여러 페이지를 가로 또는 세로로 확장할 수 있습니다.
ms.date: 12/19/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4be6e836-158e-4bc9-8870-7f394d7c7e11
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 654ec769905d17534a3896465909a14c41d60b54
ms.sourcegitcommit: 93e4fd75e8fe0cc85e7949c9adf23b0e1c275465
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84255346"
---
# <a name="control-row--column-headings-report-builder--ssrs"></a>행 및 열 머리글 제어(보고서 작성기 및 SSRS)
  페이지가 매겨진 보고서의 테이블, 행렬 또는 목록 데이터 영역은 가로 또는 세로로 여러 페이지에 분산되어 있을 수 있습니다. 각 페이지에 행 또는 열 머리글을 반복 표시할지 여부를 지정할 수 있습니다. 웹 포털이나 보고서 미리 보기와 같은 대화형 렌더러에서 보고서를 스크롤할 때 행 또는 열 머리글이 항상 화면에 표시되도록 고정시킬 수 있습니다. 테이블이나 행렬의 첫 번째 행에는 각 열의 데이터에 대한 레이블이 있는 열 머리글이 있고, 첫 번째 열에는 각 행의 데이터에 대한 레이블이 있는 행 머리글이 있습니다. 중첩된 그룹의 경우 그룹 레이블이 있는 열 머리글과 처음 몇 개의 행을 반복 표시할 수 있습니다. 기본적으로 목록 데이터 영역에는 머리글이 포함되지 않습니다.  
  
 머리글을 반복 표시하거나 고정하는 방법은 다음에 따라 달라집니다.  
  
-   각 페이지 맨 위에 반복되는 열 머리글의 경우  
  
    -   테이블이나 행렬에 가로로 확장되는 열 그룹 영역이 있는지 여부  
  
    -   열 그룹과 연결된 모든 행을 하나의 단위로 제어할지 여부  
  
-   각 페이지 옆쪽에 반복되는 행 머리글의 경우  
  
    -   테이블이나 행렬에 세로로 확장되는 행 그룹 영역이 있는지 여부. 행 머리글은 행 그룹 머리글이 있는 행 그룹에 대해서만 지원됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-rows-and-columns-in-a-tablix-data-region"></a>테이블릭스 데이터 영역의 행 및 열 이해  
 테이블이나 행렬은 기본 테이블릭스 데이터 영역의 템플릿입니다. 테이블릭스 데이터 영역에는 보고서 아래쪽으로 확장되는 행을 제어하는 행 그룹 영역, 보고서 양쪽으로 확장되는 열을 제어하는 열 그룹 영역, 데이터를 표시하는 본문 및 모퉁이와 같이 4개의 영역이 있습니다. 반복 또는 고정 머리글을 제어하는 속성을 설정하려면 테이블릭스 데이터 영역을 표시하는 두 가지 방법을 이해해야 합니다.  
  
-   **보고서 정의에서** 테이블릭스 데이터 영역 정의에 있는 각 행이나 열은 특정 행이나 열 그룹의 테이블릭스 멤버입니다. 테이블릭스 멤버는 정적 또는 동적입니다. 정적 테이블릭스 멤버는 그룹당 한 번씩 반복되며 일반적으로 레이블 또는 부분합을 포함합니다. 동적 테이블릭스 멤버는 그룹 값을 포함하며 그룹 인스턴스라고도 하는 그룹의 고유 값마다 한 번씩 반복됩니다.  
  
-   **디자인 화면에서** 디자인 화면에서 점선은 테이블릭스 데이터 영역을 4개의 영역으로 구분합니다. 테이블릭스 데이터 영역의 각 셀은 행과 열을 구성합니다. 행과 열은 세부 정보 그룹 등의 그룹과 연결됩니다. 선택한 테이블릭스 데이터 영역에 대해 행과 열 핸들, 강조 표시 막대가 그룹 멤버 자격을 나타냅니다. 행 그룹이나 열 그룹 영역의 셀은 테이블릭스 멤버의 그룹 머리글을 나타냅니다. 단일 행이나 열을 여러 그룹에 연결시킬 수 있습니다.  
  
     자세한 내용은 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md) 및 [테이블릭스 데이터 영역 셀, 행 및 열&#40;보고서 작성기&#41; 및 SSRS](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)를 참조하세요.  
  
 행 그룹이나 열 그룹 영역이 있는 테이블릭스 데이터 영역의 경우 테이블릭스 데이터 영역의 속성을 설정하여 연결된 행과 열을 제어합니다. 그 밖의 경우에는 선택한 테이블릭스 멤버의 속성 창에서 속성을 설정하여 행과 열을 제어합니다. 단계별 지침은 [여러 페이지에 행 및 열 머리글 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md) 및 [보고서를 스크롤할 때 머리글 계속 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)를 참조하세요.  
  
##  <a name="examples"></a><a name="Top"></a> 예  
 테이블릭스 데이터 영역의 가장 일반적인 예는 행렬, 그룹이 없는 테이블, 행 그룹과 행 그룹 머리글이 있는 테이블, 행 그룹만 있고 행 그룹 머리글이 없는 테이블에 대한 것입니다. 머리글을 반복 또는 고정하는 방법을 제어하려면 제어하려는 행이나 열이 행 그룹 또는 열 그룹 영역에 있는 그룹 머리글과 연결이 있는지 확인해야 합니다.  
  
 다음 섹션에서는 테이블릭스 데이터 영역에 대한 일반 레이아웃의 예를 제공합니다.  
  
-   [행렬](#Matrix)  
  
-   [그룹이 없는 테이블](#TableNoGroups)  
  
-   [행 그룹과 행 그룹 영역이 있는 테이블](#TableRowGroupsGroupHeader)  
  
-   [행 그룹만 있고 행 그룹 영역은 없는 테이블](#TableRowGroupsNoGroupHeader)  
  
###  <a name="matrix"></a><a name="Matrix"></a> 행렬  
 기본적으로 간단한 행렬에는 하나의 행 그룹과 하나의 열 그룹이 있습니다. 다음 그림에서는 범주를 기반으로 한 행 그룹과 지리를 기반으로 한 열 그룹으로 구성된 행렬을 보여 줍니다.  
  
 ![행렬, Category 행 및 Geography 열 그룹](../../reporting-services/report-design/media/rs-basicmatrixdesign.gif "행렬, Category 행 및 Geography 열 그룹")  
  
 점선은 4개의 테이블릭스 영역을 보여 줍니다. 행 그룹 영역에는 첫 번째 열의 범주 레이블을 제어하는 행 그룹 머리글이 있습니다. 마찬가지로, 열 그룹 영역에는 첫 번째 행의 지리 레이블을 제어하는 열 그룹 머리글이 있습니다. 미리 보기에서 행렬이 여러 페이지에 걸쳐 있으면 다음 그림과 같이 첫 번째 행에 열 머리글이 나타납니다.  
  
 ![확장 그룹이 있는 렌더링된 행렬의 미리 보기](../../reporting-services/report-design/media/rs-basicmatrixpreview.gif "확장 그룹이 있는 렌더링된 행렬의 미리 보기")  
  
 첫 번째 행의 열 머리글을 반복하거나 고정하려면 테이블릭스 데이터 영역의 열 머리글 속성을 설정합니다. 중첩된 열 그룹의 열 머리글은 자동으로 포함됩니다.  
  
 첫 번째 열의 행 머리글을 반복하거나 고정하려면 테이블릭스 데이터 영역의 행 머리글 속성을 설정합니다. 중첩된 행 그룹의 행 머리글은 자동으로 포함됩니다.  
  
 [맨 위로 이동](#Top)  
  
###  <a name="table-with-no-row-groups"></a><a name="TableNoGroups"></a> 행 그룹이 없는 테이블  
 기본적으로 그룹이 없는 간단한 테이블에는 세부 정보 그룹이 포함되어 있습니다. 다음 그림에서는 범주, 주문 번호 및 판매 데이터를 표시하는 테이블을 보여 줍니다.  
  
 ![디자인, 1개의 정적 행과 1개의 동적 행이 있는 테이블](../../reporting-services/report-design/media/rs-tableheaderstaticdesign.gif "디자인, 1개의 정적 행과 1개의 동적 행이 있는 테이블")  
  
 이 테이블은 테이블릭스 본문 영역으로만 구성되어 있기 때문에 점선이 없습니다. 첫 번째 행에는 그룹과 연결되지 않은 정적 테이블릭스 멤버를 나타내는 열 머리글이 표시됩니다. 두 번째 행에는 세부 정보 그룹과 연결된 동적 테이블릭스 멤버를 나타내는 세부 정보 데이터가 표시됩니다. 다음 그림에서는 이러한 테이블의 미리 보기를 보여 줍니다.  
  
 ![미리 보기, 1개의 정적 행과 1개의 동적 행이 있는 테이블](../../reporting-services/report-design/media/rs-tableheaderstaticpreview.gif "미리 보기, 1개의 정적 행과 1개의 동적 행이 있는 테이블")  
  
 열 머리글을 반복하거나 고정하려면 테이블릭스 데이터 영역 정의의 일부인 정적 행의 테이블릭스 멤버 속성을 설정합니다. 정적 행을 선택하려면 그룹화 창의 고급 모드를 사용해야 합니다. 다음 그림에서는 행 그룹 창을 보여 줍니다.  
  
 ![행 그룹, 1개의 정적 행과 1개의 동적 행이 있는 테이블](../../reporting-services/report-design/media/rs-tableheaderstaticgroupingpanedefault.gif "행 그룹, 1개의 정적 행과 1개의 동적 행이 있는 테이블")  
  
 다음 그림은 고급 모드에서 테이블의 행 그룹에 대한 정적 및 동적 테이블릭스 멤버를 보여 줍니다.  
  
 ![행 그룹, 기본 테이블용 고급](../../reporting-services/report-design/media/rs-tableheaderstaticgroupingpaneadvanced.gif "행 그룹, 기본 테이블용 고급")  
  
 테이블릭스 멤버의 열 제목을 반복 또는 고정하려면 (**정적**)이라는 레이블이 있는 정적 행을 선택합니다. 선택한 테이블릭스 멤버의 속성이 속성 창에 표시됩니다. 이 테이블릭스 멤버의 속성을 설정하여 첫 번째 행을 반복할지 아니면 계속 표시할지 여부를 제어할 수 있습니다.  
  
 [맨 위로 이동](#Top)  
  
###  <a name="table-with-row-groups-and-a-row-group-area"></a><a name="TableRowGroupsGroupHeader"></a> 행 그룹과 행 그룹 영역이 있는 테이블  
 간단한 테이블에 행 그룹을 추가하면 디자인 화면에서 행 그룹 영역이 테이블에 추가됩니다. 다음 그림에서는 범주 기반의 행 그룹이 있는 테이블을 보여 줍니다.  
  
 ![디자인, 1개의 행 그룹과 세부 정보가 있는 테이블](../../reporting-services/report-design/media/rs-tableheaderdynamicwithgroupheadercelldesign.gif "디자인, 1개의 행 그룹과 세부 정보가 있는 테이블")  
  
 점선은 테이블릭스 행 그룹 영역과 테이블릭스 본문 영역을 보여 줍니다. 행 그룹 영역에는 행 그룹 머리글만 있고 열 그룹 머리글은 없습니다. 다음 그림에서는 이러한 테이블의 미리 보기를 보여 줍니다.  
  
 ![미리 보기, 1개의 행 그룹과 세부 정보가 있는 테이블](../../reporting-services/report-design/media/rs-tableheaderdynamicwithgroupheadercellpreview.gif "미리 보기, 1개의 행 그룹과 세부 정보가 있는 테이블")  
  
 열 머리글을 반복 또는 고정하려면 이전 예와 같은 방법을 사용합니다. 다음 그림에서는 행 그룹 창의 기본 보기를 보여 줍니다.  
  
 ![행 그룹, 동적 멤버로 구성된 기본 모드](../../reporting-services/report-design/media/rs-tableheaderdynamicgroupingpanedefault.gif "행 그룹, 동적 멤버로 구성된 기본 모드")  
  
 다음 그림과 같이 행 그룹 창의 **고급** 모드를 사용하여 테이블릭스 멤버를 표시합니다.  
  
 ![행 그룹, 정적 멤버로 구성된 고급 모드](../../reporting-services/report-design/media/rs-tableheaderdynamicwithgroupheadercelladvanced.gif "행 그룹, 정적 멤버로 구성된 고급 모드")  
  
 테이블릭스의 경우 멤버는 다음과 같습니다. **정적**, (**정적**), 범주 및 (**세부 정보**)가 나열됩니다. 괄호()가 포함된 테이블릭스 멤버는 해당 그룹 머리글이 없음을 나타냅니다. 열 머리글을 반복 또는 고정하려면 정적 테이블릭스 멤버를 선택하고 속성 창에서 속성을 설정합니다.  
  
 [맨 위로 이동](#Top)  
  
###  <a name="table-with-row-groups-and-no-row-group-area"></a><a name="TableRowGroupsNoGroupHeader"></a> 행 그룹만 있고 행 그룹 영역이 없는 테이블  
 여러 가지 방법으로 행 그룹만 포함하고 행 그룹 영역은 포함하지 않은 테이블을 만들 수 있습니다. 여기서는 두 가지 방법을 소개합니다.  
  
-   행 그룹과 행 그룹 영역을 포함하는 테이블을 만든 다음 행 그룹 영역에 해당하는 열을 삭제합니다. 열만 삭제하고 그룹은 그대로 둡니다. 예를 들어 테이블 서식을 간단한 모눈으로 변경할 수 있습니다.  
  
-   테이블릭스 데이터 영역을 도입하기 전에 이전 RDL 버전용으로 만든 보고서를 업그레이드합니다.  
  
 다음 그림에서는 디자인 화면에서 행 그룹만 있고 행 그룹 영역은 없는 테이블을 보여 줍니다.  
  
 ![디자인, 테이블에 행 그룹은 있지만 그룹 머리글은 없음](../../reporting-services/report-design/media/rs-tableheaderdynamicwithnogroupheadercelldesign.gif "디자인, 테이블에 행 그룹은 있지만 그룹 머리글은 없음")  
  
 테이블에 3개의 행이 있습니다. 첫 번째 행에는 열 머리글이 있고 두 번째 행에는 그룹 값과 부분합이 있습니다. 세 번째 행에는 세부 정보 데이터가 포함되어 있습니다. 이 테이블에는 테이블릭스 본문 영역만 있기 때문에 점선이 없습니다. 다음 그림에서는 이러한 테이블의 미리 보기를 보여 줍니다.  
  
 ![미리 보기, 테이블에 행 그룹은 있지만 그룹 머리글은 없음](../../reporting-services/report-design/media/rs-tableheaderdynamicwithnogroupheadercellpreview.gif "미리 보기, 테이블에 행 그룹은 있지만 그룹 머리글은 없음")  
  
 행을 반복할지 계속 표시할지 여부를 제어하려면 각 행의 테이블릭스 멤버에 대한 속성을 설정해야 합니다. 기본 모드에서 보면 이 예와 행 그룹과 그룹 머리글이 있는 이전 예와 차이가 없어 보입니다. 다음 그림에서는 이 테이블을 기본 모드로 표시한 그룹화 창을 보여 줍니다.  
  
 ![행 그룹, 동적 멤버로 구성된 기본 모드](../../reporting-services/report-design/media/rs-tableheaderdynamicgroupingpanedefault.gif "행 그룹, 동적 멤버로 구성된 기본 모드")  
  
 그러나 고급 모드에서는 레이아웃 구조의 테이블릭스 멤버가 조금 다르게 표시됩니다. 다음 그림에서는 이 테이블을 고급 모드로 표시한 그룹화 창을 보여 줍니다.  
  
 ![행 그룹, 고급, 그룹 머리글은 없음](../../reporting-services/report-design/media/rs-tableheaderdynamicwithnogroupheadercelladvanced.gif "행 그룹, 고급, 그룹 머리글은 없음")  
  
 행 그룹 창에 (**정적**), (범주), (**정적**) 및 (**세부 정보**) 테이블릭스 멤버가 나열됩니다. 열 제목을 반복 또는 고정하려면 맨 위의 (**정적**) 테이블릭스 멤버를 선택하고 속성 창에서 속성을 설정합니다.  
  
 [맨 위로 이동](#Top)  
  
## <a name="renderer-support-for-repeating-or-freezing-headers"></a>렌더러의 반복 또는 고정 머리글 지원  
 렌더러마다 반복 또는 고정 머리글에 대한 지원이 달라집니다.  
  
 물리적 페이지를 사용하는 렌더러(PDF, 이미지, 인쇄)는 다음 기능을 제공합니다.  
  
-   테이블릭스 데이터 영역이 가로로 여러 페이지에 걸쳐 있으면 행 머리글을 반복합니다.  
  
-   테이블릭스 데이터 영역이 세로로 여러 페이지에 걸쳐 있으면 열 머리글을 반복합니다.  
  
 또한 소프트 페이지 나누기를 사용하는 렌더러(웹 포털, 보고서 미리 보기 또는 보고서 뷰어 컨트롤)는 다음 기능을 지원합니다.  
  
-   보고서를 가로로 스크롤할 때 행 머리글을 계속 표시합니다.  
  
-   보고서를 세로로 스크롤할 때 열 머리글을 계속 표시합니다.  
  
 자세한 내용은 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
