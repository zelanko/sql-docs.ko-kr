---
title: 데이터 필터링, 그룹화 및 정렬(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.categorygroupproperties.general.f1
- "10403"
- sql13.rtp.rptdesigner.categorygroupproperties.sorting.f1
- sql13.rtp.rptdesigner.seriesgroupproperties.general.f1
- "10402"
- "10410"
- sql13.rtp.rptdesigner.seriesgroupproperties.sorting.f1
- "10412"
ms.assetid: 4dda2a7f-3f31-47e9-a88b-28d770ebd65e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 74f047ddc136ae1b117f533d45391ef8b2048441
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50031132"
---
# <a name="filter-group-and-sort-data-report-builder-and-ssrs"></a>데이터 필터링, 그룹화 및 정렬(보고서 작성기 및 SSRS)
  보고서에서 식은 보고서 데이터를 제어, 구성 및 정렬하는 데 사용됩니다. 기본적으로 데이터 집합을 만들고 보고서 레이아웃을 디자인하면 보고서 항목의 속성이 데이터 집합 필드, 매개 변수 및 보고서 데이터 창에 표시되는 기타 항목을 기반으로 자동으로 식에 설정됩니다. 또한 테이블 또는 행렬 셀에 대화형 정렬 단추를 추가하여 사용자가 그룹의 행 정렬 순서 또는 그룹 내 행을 대화형으로 변경하도록 할 수 있습니다.  
  
-   **필터 식** 필터 식은 지정된 비교 기준을 기반으로 데이터의 포함 또는 제외를 테스트합니다. 데이터를 데이터 연결에서 검색한 후에 필터가 보고서의 데이터에 적용됩니다. 필터 조합을 보고서 서버의 공유 데이터 집합 정의, 보고서의 공유 데이터 집합 인스턴스 또는 포함된 데이터 집합, 테이블 또는 차트와 같은 데이터 영역, 테이블의 행 그룹 또는 차트의 범주 그룹 같은 데이터 영역 그룹 등의 항목에 추가할 수 있습니다.  
  
-   **그룹 식** 그룹 식은 데이터 집합 필드 또는 기타 값을 기반으로 데이터를 구성합니다. 그룹 식은 보고서 레이아웃을 만들 때 자동으로 만들어집니다. 보고서 처리기에서는 필터가 데이터에 적용된 후 보고서 데이터와 데이터 영역이 결합될 때 그룹 식을 평가합니다. 그룹 식을 만든 후 사용자 지정할 수 있습니다.  
  
-   **정렬 식** 정렬 식은 데이터가 데이터 영역에 표시되는 순서를 제어합니다. 정렬 식은 보고서 레이아웃을 만들 때 자동으로 만들어집니다. 기본적으로 그룹의 정렬 식은 그룹 식과 같은 값으로 설정됩니다. 정렬 식을 만든 후 사용자 지정할 수 있습니다.  
  
-   **대화형 정렬** 사용자가 열의 정렬 순서를 정렬하거나 역순으로 정렬할 수 있도록 테이블이나 행렬의 열 머리글 또는 그룹 머리글 셀에 대화형 정렬 단추를 추가할 수 있습니다.  
  
 사용자가 필터, 그룹 또는 정렬 식을 사용자 지정할 수 있도록 식을 변경하여 보고서 매개 변수에 참조를 추가할 수 있습니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)에 대해 자세히 알아봅니다.  
  
 자세한 내용 및 예제는 다음 항목을 참조하십시오.  
  
-   [그룹 식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
-   [필터 수식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
-   [보고서 작성기 자습서](../../reporting-services/report-builder-tutorials.md)  
  
-   [Reporting Services&#40;SSRS&#41; 자습서](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
-   [보고서 예제(보고서 작성기 및 SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Filtering"></a> 보고서 데이터 필터링  
 필터는 데이터 연결에서 검색된 보고서 데이터를 제어하는 데 사용되는 보고서의 일부입니다. 필터는 데이터를 외부 데이터 원본에서 검색하기 전에 필터링하기 위해 데이터 집합 쿼리를 변경할 수 없는 경우에 사용합니다.  
  
 가능한 경우 보고서에 표시하기 위해 필요한 데이터만 반환하는 데이터 집합 쿼리를 작성합니다. 검색 및 처리해야 하는 데이터의 양을 줄이면 보고서 성능을 향상시키는 데 도움이 됩니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)이라는 데이터 집합이 들어 있습니다.  
  
 외부 데이터 원본에서 데이터를 검색한 후 데이터 집합, 데이터 영역 및 데이터 영역 그룹(세부 그룹 포함)에 필터를 추가할 수 있습니다. 필터는 런타임에 데이터 집합에 대해 가장 먼저 적용된 다음 데이터 영역과 그룹(그룹 계층 구조에 대해 하향식으로)에 차례로 적용됩니다. 테이블, 행렬 또는 목록에서 행 그룹, 열 그룹 및 인접 그룹의 필터는 독립적으로 적용됩니다. 또한 차트에서 범주 그룹 및 계열 그룹의 필터는 독립적으로 적용됩니다. 자세한 내용은 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)를 참조하세요.  
  
 각 필터에 *필터 수식*을 지정합니다. 필터 수식은 필터링할 데이터를 지정하는 데이터 집합 필드나 식, 연산자 및 비교할 값을 포함합니다. 필터 조건과 일치하는 데이터 값만 항목을 처리할 때 포함됩니다.  
  
 사용자가 보고서 데이터를 효율적으로 제어할 수 있도록 필터 식에 매개 변수를 추가할 수 있습니다. 자세한 내용은 [매개 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)를 참조하세요.  
  
 각 사용자에 대한 뷰를 사용자 지정하려면 필터에 기본 제공 필드 UserID에 대한 참조를 포함합니다. 자세한 내용은 [기본 제공 Globals 및 Users 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)를 참조하세요.  
  
  
##  <a name="Grouping"></a> 보고서 데이터 그룹화  
 그룹은 표시하거나 집계 값을 계산하기 위한 보고서 데이터를 구성합니다. 그룹을 정의하고 그룹 기능을 사용하는 방법을 이해하면 보고서를 더욱 간결하게 디자인할 수 있습니다.  
  
 그룹 식은 다음을 수행할 때 자동으로 만들어집니다.  
  
-   테이블, 행렬 또는 차트 마법사의 데이터 집합 필드를 정렬하거나 지도 마법사의 필드를 일치시킵니다.  
  
-   테이블, 행렬 또는 목록의 그룹화 창에서 행 그룹 또는 열 그룹 영역에 필드를 추가합니다.  
  
-   차트의 차트 데이터 창에서 범주 그룹 또는 계열 그룹 영역에 필드를 추가합니다.  
  
-   지도의 계층 데이터 상황에 맞는 메뉴 항목에서 지도 요소와 분석 데이터를 일치시킬 필드를 지정합니다.  
  
 그룹은 보고서 정의의 일부이며 각 그룹에는 이름이 있습니다. 기본적으로 그룹 이름은 그룹의 기반이 되는 데이터 집합 필드입니다.  
  
 테이블 또는 행렬 데이터 영역에서 여러 행 그룹과 열 그룹을 만들 수 있습니다. 중첩 그룹, 인접 그룹 및 재귀 계층 구조 그룹(예: 조직 차트)을 구성하여 데이터를 시각적 계층에 표시할 수 있습니다.  
  
 그룹 이름은 식 범위를 나타냅니다. 집계를 계산하고, 데이터를 계층적으로 구성하고 드릴다운 보고서에서 자식 노드 보기와 부모 노드 보기 간에 전환하고, 여러 데이터 영역에 있는 동일한 데이터에 대한 다양한 보기를 표시하고, 테이블, 행렬, 차트, 계기 또는 지도에 요약 데이터를 시각화하기 위해 그룹의 이름을 범위로 지정할 수 있습니다. 자세한 내용은 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 나타냅니다.  
  
 여러 데이터 집합 필드를 그룹화하려면 각 필드를 그룹 식 집합에 추가합니다. 또한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]에서 그룹 식을 직접 작성할 수도 있습니다. 예를 들어 값의 범위로 그룹화하거나 보고서 매개 변수를 사용하여 그룹화함으로써 데이터 영역의 데이터를 그룹화하는 방법을 사용자가 직접 선택하도록 할 수 있습니다. 자세한 내용은 [그룹 식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)를 참조하세요.  
  
 보고서 프레젠테이션을 위해 각 그룹의 전과 후 또는 그룹에 있는 각 인스턴스의 전과 후에 페이지 나누기를 추가하여 각 페이지에서 데이터의 양을 줄이고 보고서 렌더링 성능을 보다 원활하게 관리할 수 있습니다. 자세한 내용은 [페이지 나누기 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md)를 참조하세요.  
  
 데이터 영역 그룹을 만드는 것은 데이터를 보고서에 구성하기 위한 한 방법입니다. 데이터를 구성하는 데는 여러 가지 방법이 있으며 각 방법에는 장점이 있습니다. 자세한 내용은 [드릴스루, 드릴다운, 하위 보고서 및 중첩 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)을 참조하세요.  
  
### <a name="defining-group-variables"></a>그룹 변수 정의  
 그룹을 정의할 때 그룹으로 범위가 한정되고 중첩 그룹에서 액세스할 수 있는 식에서 사용하기 위한 그룹 변수를 만들 수 있습니다. 그룹 변수는 그룹 인스턴스당 한 번씩 계산되며 자식 그룹의 식에서 액세스할 수 있습니다. 예를 들어 영역과 부분 영역으로 그룹화된 데이터의 경우 각 영역에 대한 세금을 계산하고 해당 세금을 부분 영역 그룹의 계산에 사용할 수 있습니다.  
  
 자세한 내용은 [보고서 및 그룹 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
### <a name="groups-and-scope-in-data-regions"></a>데이터 영역의 그룹 및 범위  
 동일한 데이터 집합에서 다양한 데이터 보기를 제공하려면 각 데이터 영역에 동일한 그룹 식을 지정합니다. 예를 들어 범주화된 데이터를 테이블에 표시하면 모든 세부 데이터를 표시할 수 있고 원형 차트에 표시하면 집계를 표시하고 전체 데이터 집합과 관련된 각 범주를 시각화할 수 있습니다. 자세한 내용은 [동일한 데이터 집합에 여러 데이터 영역 연결&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)를 참조하세요.  
  
 테이블, 행렬 또는 목록의 셀에 있는 데이터 영역을 중첩시킬 경우 자동으로 데이터의 범위가 셀의 가장 안쪽 그룹 멤버 자격으로 지정됩니다. 예를 들어 행 그룹 및 열 그룹 모두에 있는 셀에 차트를 추가하면 런타임에 이 차트에서 데이터 사용 범위는 가장 안쪽 행 그룹 인스턴스와 가장 안쪽 열 그룹 인스턴스입니다. 자세한 내용은 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
  
##  <a name="Sorting"></a> 보고서 데이터 정렬  
 보고서에서 데이터의 정렬 순서를 제어하려면 데이터 집합 쿼리에서 데이터를 정렬하거나 데이터 영역 또는 그룹에 대한 정렬 식을 정의할 수 있습니다. 테이블 및 행렬에 대화형 정렬 단추를 추가하면 사용자가 행 정렬 순서를 변경할 수 있습니다.  
  
 동일한 보고서에서 세 가지 정렬 유형을 모두 사용할 수 있습니다. 기본적으로 정렬 순서는 데이터 집합 쿼리에서 반환되는 데이터의 순서에 따라 결정됩니다. 정렬 식은 데이터 영역과 데이터 영역 그룹에 적용됩니다. 대화형 정렬은 정렬 식 다음에 적용됩니다.  
  
 집계 함수가 포함된 식의 경우 대부분의 결과는 정렬 순서의 영향을 받지 않습니다. 집계 함수 First, Last 및 Previous에 대한 반환 값은 정렬 순서의 영향을 받습니다. 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)를 참조하세요.  
  
### <a name="sorting-data-in-a-dataset-query"></a>데이터 집합 쿼리에서 데이터 정렬  
 보고서에서 데이터를 가져오기 전에 미리 정렬하려면 데이터 집합 쿼리에 정렬 순서를 추가합니다. 쿼리에서 데이터를 정렬하면 보고서 처리기가 아닌 데이터 원본에 의해 정렬 작업이 수행됩니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본 유형의 경우에는 데이터 집합 쿼리에 ORDER BY 절을 추가할 수 있습니다. 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리인 `SELECT Sales, Region FROM SalesOrders ORDER BY Sales DESC`는 SalesOrders 테이블에서 Sales 및 Region 열을 Sales 기준의 내림차순으로 정렬합니다.  
  
> [!NOTE]  
>  쿼리에서 정렬 순서를 지정할 수 없는 데이터 원본도 있습니다.  
  
### <a name="sorting-data-with-sort-expressions"></a>정렬 식으로 데이터 정렬  
 데이터를 데이터 원본에서 가져온 후 보고서에서 정렬하려면 세부 정보 그룹을 포함하여 테이블릭스 데이터 영역 또는 그룹에 정렬 식을 설정할 수 있습니다. 아래에서는 여러 항목에 정렬 식을 설정할 때의 효과를 설명합니다.  
  
-   **테이블릭스 데이터 영역.** 런타임에 데이터 집합 필터와 데이터 영역 필터가 적용된 후 데이터 영역의 데이터 정렬 순서를 제어하려면 테이블, 행렬 또는 목록 데이터 영역에 정렬 식을 설정합니다.  
  
-   **테이블릭스 데이터 영역 그룹.** 그룹 인스턴스의 정렬 순서를 제어하려면 세부 정보 그룹을 포함하여 각 그룹에 대한 정렬 식을 설정합니다. 예를 들어 세부 정보 그룹의 경우에는 정보 행의 순서를 제어합니다. 자식 그룹의 경우에는 부모 그룹 내에서 자식 그룹에 대한 그룹 인스턴스의 순서를 제어합니다. 기본적으로 그룹을 만들 때 정렬 식은 그룹 식 및 오름차순으로 설정됩니다.  
  
     세부 정보 그룹이 하나인 경우에는 쿼리, 데이터 영역 또는 세부 정보 그룹에서 정렬 식을 정의한 결과가 같습니다.  
  
-   **차트 데이터 영역.** 데이터 요소의 정렬 순서를 제어하려면 범주 및 계열 그룹에 대한 정렬 식을 설정합니다. 기본적으로 데이터 요소의 순서는 차트 범례의 색상 순서에 해당됩니다. 자세한 내용은 [차트에서 계열 색 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)을 클릭합니다.  
  
-   **지도 보고서 항목.** 지도에서는 지도 요소에 표시하기 위해 데이터를 그룹화하므로 일반적으로 지도 데이터 영역의 데이터는 정렬할 필요가 없습니다.  
  
-   **계기 데이터 영역.** 계기에는 범위에 상대적인 단일 값이 표시되므로 일반적으로 계기 데이터 영역의 데이터는 정렬할 필요가 없습니다. 계기에서 데이터를 정렬할 필요가 없는 경우 그룹을 먼저 정의한 다음 그룹에 대한 정렬 식을 설정합니다.  
  
#### <a name="sorting-by-a-different-value"></a>다른 값으로 정렬  
 데이터 영역의 행을 필드 값 이외의 값으로 정렬할 수 있습니다. 예를 들어 Size라는 필드에 소형, 중형, 대형 및 특대형에 해당하는 텍스트 값이 들어 있는 경우 기본적으로 Size를 기반으로 하는 행 그룹의 정렬 식은 마찬가지로 [Size]입니다. 데이터를 다양한 방식으로 정렬하려면 원하는 정렬 순서를 정의하는 데이터 집합 쿼리를 필드에 추가합니다.  
  
 또는 원하는 순서만 지정하는 크기와 값만 포함하는 데이터 집합을 정의할 수 있습니다. 정렬 식을 변경하여 정렬 순서 값에 대해 Lookup 함수를 사용할 수 있습니다.  
  
 예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리는 Sizes라는 데이터 집합을 정의합니다. 이 쿼리는 CASE 문을 사용하여 각 Size 값에 대한 정렬 순서 값 SizeSortOrder를 정의합니다.  
  
```  
SELECT Size,   
  CASE Size  
        WHEN 'S' THEN 1  
        WHEN 'M' THEN 2    
        WHEN 'L' THEN 3  
        WHEN 'XL' THEN 4  
        ELSE 0  
  END as SizeSortOrder  
FROM Production.Product  
```  
  
 `[Size]`를 기반으로 하는 행 그룹이 들어 있는 테이블에서 그룹 정렬 식을 변경한 후 Lookup 함수를 사용하여 크기 값에 대응되는 숫자 필드를 찾을 수 있습니다. 식은 다음과 유사합니다.  
  
```  
=Lookup(Fields!Size.Value, Fields!Size.Value, Fields!SizeSortOrder.Value, "Sizes")  
```  
  
 자세한 내용은 [데이터 영역의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md) 및 [Lookup 함수&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md)를 참조하세요.  
  
###  <a name="Interactive"></a> 사용자를 위해 대화형 정렬 추가  
 사용자가 테이블 또는 행렬에 있는 보고서 데이터의 정렬 순서를 변경할 수 있도록 하려면 열 머리글 또는 그룹 머리글에 대화형 정렬 단추를 추가합니다. 사용자는 이 단추를 클릭하여 정렬 순서를 토글할 수 있습니다. 대화형 정렬은 HTML과 같이 사용자 상호 작용을 허용하는 렌더링 형식에서 지원됩니다.  
  
 테이블릭스 데이터 영역 셀의 입력란에 대화형 정렬 단추를 추가합니다. 기본적으로 모든 테이블릭스 셀은 입력란을 포함합니다. 입력란 속성에서, 테이블 또는 행렬 데이터 영역에서 정렬할 부분(부모 그룹 값, 자식 그룹 값 또는 정보 행), 정렬 기준 및 피어 관계에 있는 다른 보고서 항목에 정렬 식을 적용할지 여부를 지정합니다. 예를 들어 같은 데이터 집합에 대한 테이블과 차트가 사각형 안에 포함된 경우 이 둘은 피어 데이터 영역입니다. 사용자가 테이블에서 정렬 순서를 전환하면 차트의 정렬 순서도 전환됩니다. 자세한 내용은 [대화형 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md)을 참조하세요.  
  
  
##  <a name="HowTo"></a> 방법 도움말 항목  
 [보고서를 스크롤할 때 머리글 계속 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
 [그룹과 함께 머리글 및 바닥글 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [테이블 또는 행렬에 대화형 정렬 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
 [데이터 영역에 대한 데이터 없음 메시지 설정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [재귀 계층 구조 그룹 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)  
  
 [데이터 영역에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
 [그룹과 함께 머리글 및 바닥글 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [차트에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-chart-report-builder-and-ssrs.md)  
  
 [그룹 또는 테이블릭스 데이터 영역에 합계 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)  
  
##  <a name="Section"></a> 섹션 내용  
 [그룹 식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
 [필터 수식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)  
  
##  <a name="Related"></a> 관련 단원  
 [그룹 이해&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)  
  
 [재귀 계층 구조 그룹 생성&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)  
  
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
 [보고서 및 그룹 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)  
  
 [차트에 데이터 범위가 여러 개 있는 계열 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/displaying-a-series-with-multiple-data-ranges-on-a-chart.md)  
  
 [동일한 데이터 집합에 여러 데이터 영역 연결&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [지도&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [스파크라인 및 데이터 막대&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [계기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)   
 [표시기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
