---
title: 테이블릭스 데이터 영역에 데이터 추가(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8f1d0a76-afed-480f-98fb-89e2d4eb09b1
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b8a4d21b2db6673fda184bdd7ed391dd2af8b48d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105873"
---
# <a name="adding-data-to-a-tablix-data-region-report-builder-and-ssrs"></a>테이블릭스 데이터 영역에 데이터 추가(보고서 작성기 및 SSRS)
  보고서 데이터 세트의 데이터를 테이블 또는 행렬에 표시하려면 각 데이터 셀에서 표시할 데이터 세트 필드의 이름을 지정합니다. 세부 데이터 또는 그룹화된 데이터를 표시할 수 있습니다. 테이블 또는 행렬에 그룹을 추가하면 그룹 값 및 그룹 데이터를 위한 행과 열이 자동으로 추가됩니다. 그런 다음 데이터의 부분합과 합계를 추가할 수 있습니다.  
  
 데이터 영역의 모든 데이터는 하나 이상의 그룹에 속합니다. 세부 데이터는 세부 정보 그룹의 멤버입니다. 세부 정보 및 그룹화된 데이터에 대한 자세한 내용은 [그룹 이해&#40;보고서 작성기 및 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-detail-data"></a>세부 데이터 추가  
 세부 데이터는 데이터 세트, 데이터 영역 및 세부 정보 그룹에 필터가 적용된 후 보고서 데이터 세트에 포함되는 모든 데이터입니다. 단일 테이블릭스 데이터 영역에 표시되는 모든 세부 데이터는 동일한 보고서 데이터 세트에서 제공되어야 합니다.  
  
 보고서 데이터 세트의 세부 데이터를 테이블릭스 데이터 영역에 추가하려면 데이터 세트 필드를 보고서 데이터 창에서 정보 행의 각 셀로 끕니다. 테이블릭스 데이터 영역에 있는 기존 셀의 경우 각 셀에서 필드 선택기를 사용하거나 필드를 보고서 데이터 창에서 셀로 끌어 데이터 세트 필드 식을 추가하거나 편집할 수 있습니다. 추가 열을 만들려면 필드를 보고서 데이터 창에서 끌어 기존 테이블릭스 데이터 영역에 삽입하면 됩니다.  
  
 기본적으로 런타임에 정보 행의 셀에는 세부 데이터가 표시되고 그룹 행의 셀에는 집계 값이 표시됩니다. 테이블릭스 행 및 열에 대한 자세한 내용은 [테이블릭스 데이터 영역 셀, 행 및 열&#40;보고서 작성기&#41; 및 SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)를 참조하세요.  
  
 테이블 템플릿 및 목록 템플릿은 정보 행을 제공하지만 행렬 템플릿에는 정보 행이 없습니다. 테이블릭스 데이터 영역에 정보 행이 없는 경우 세부 정보 그룹을 정의하여 정보 행을 추가할 수 있습니다. 자세한 내용은 [세부 정보 그룹 추가&#40;보고서 작성기 및 SSRS&#41;](add-a-details-group-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="adding-grouped-data"></a>그룹화된 데이터 추가  
 그룹화된 데이터는 데이터 세트, 데이터 영역 및 그룹에 필터가 적용된 후 그룹 식으로 지정되는 모든 세부 데이터입니다. 세부 데이터를 그룹으로 구성하려면 보고서 데이터 창의 필드를 그룹화 창으로 끕니다. 그룹을 추가할 때 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 그룹화된 데이터를 표시할 테이블릭스 데이터 영역에 관련 행이나 열을 자동으로 추가합니다. 이러한 행 또는 열의 셀은 그룹화된 데이터와 연결됩니다. 자세한 내용은 [데이터 영역에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
 숫자 데이터를 나타내는 데이터 세트 필드를 그룹 행 또는 열의 셀에 추가하는 경우 기본적으로 셀의 값은 가장 안쪽 행과 해당 셀에 대한 열 그룹 멤버 자격을 범위로 하는 그룹화된 데이터의 합계로 지정됩니다. 기본 집계 함수 Sum을 Avg 또는 Count와 같은 다른 집계 함수로 변경할 수 있습니다. 예를 들어 집계 계산의 기본 범위를 변경하여 행 그룹에 대한 값의 백분율을 계산할 수 있습니다. 자세한 내용은 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 나타냅니다.  
  
 기본적으로 그룹화된 데이터는 모두 동일한 보고서 데이터 세트에서 가져옵니다. 테이블릭스 데이터 영역에서 데이터 세트 이름을 범위로 지정하여 다른 데이터 세트의 집계 값을 포함할 수 있습니다. 단일 테이블릭스 데이터 영역 안에 있는 여러 데이터 세트의 여러 집계 값을 지정할 수 있습니다. 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)를 참조하세요.  
  
## <a name="adding-subtotals-and-totals"></a>부분합 및 합계 추가  
 그룹에 대한 부분합과 데이터 영역에 대한 총합계를 추가하려면 셀 또는 그룹화 창에서 바로 가기 메뉴의 합계 추가 기능을 사용합니다. 합계를 표시할 행과 열이 자동으로 추가됩니다. 부분합 및 합계 식은 기본적으로 [Sum](report-builder-functions-sum-function.md) 집계 함수를 사용합니다. 식을 추가한 뒤에는 기본 함수를 변경할 수 있습니다. 자세한 내용은 [그룹 또는 테이블릭스 데이터 영역에 합계 추가&#40;보고서 작성기 및 SSRS&#41;](add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md) 및 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
## <a name="adding-labels"></a>레이블 추가  
 그룹 또는 데이터 영역의 레이블을 추가하려면 레이블을 지정할 그룹 외부에 행 또는 열을 추가합니다. 레이블 행 및 열은 합계 표시를 위해 추가하는 행 및 열과 비슷합니다. 자세한 내용은 [행 삽입 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](insert-or-delete-a-row-report-builder-and-ssrs.md) 또는 [열 삽입 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](insert-or-delete-a-column-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="adding-an-existing-tablix-data-region-from-another-report"></a>다른 보고서의 기존 테이블릭스 데이터 영역 추가  
 다른 보고서에서 데이터 영역을 복사하여 새 보고서나 기존 보고서에 붙여넣을 수 있습니다. 데이터 영역을 붙여 넣은 후 데이터 영역에서 사용하는 데이터 세트가 정의되어 있고 데이터 세트 필드의 이름 및 데이터 형식이 원래 보고서의 해당 이름 및 데이터 형식과 동일한지 확인해야 합니다. 한 보고서에서 다른 보고서로 데이터 세트를 복사할 수 없지만 보고서에서 공유 데이터 원본을 사용하는 경우 다른 보고서의 데이터 세트를 신속하게 복제할 수 있습니다. 또한 데이터 세트의 데이터를 검색하는 쿼리의 쿼리 텍스트를 가져올 수 있으므로 보고서의 쿼리를 간단하게 복제할 수 있습니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)이라는 데이터 집합이 들어 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](report-parameters-report-builder-and-report-designer.md)   
 [대화형 정렬, 문서 구조 및 링크&#40;보고서 작성기 및 SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [보고서 데이터 창에서 필드 추가, 편집, 새로 고침&#40;보고서 작성기 및 SSRS&#41;](../report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)   
 [식 추가&#40;보고서 작성기 및 SSRS&#41;](add-an-expression-report-builder-and-ssrs.md)  
  
  
