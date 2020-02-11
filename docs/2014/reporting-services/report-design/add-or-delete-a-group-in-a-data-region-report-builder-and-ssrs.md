---
title: 데이터 영역에서 그룹 추가 또는 삭제(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4de53c3c-c6fc-49ce-b692-3609fc0b3ec5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 66883f42947ba54205a5f272bb6bbfd5a90376f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106571"
---
# <a name="add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs"></a>데이터 영역에서 그룹 추가 또는 삭제(보고서 작성기 및 SSRS)
  표시 및 계산을 위해 데이터를 특정 값 또는 식 집합에 따라 구성하려는 경우 데이터 영역에 그룹을 추가할 수 있습니다. 그룹에는 그룹에 속한 데이터 세트의 데이터를 구분하는 식과 이름이 있습니다. 그룹에 대한 자세한 내용은 [그룹 이해&#40;보고서 작성기 및 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
 테이블릭스 데이터 영역에서 테이블, 행렬 또는 목록을 클릭하여 그룹화 창을 표시하고, 데이터 세트 필드를 행 그룹 및 열 그룹 창으로 끌어 부모 또는 자식 그룹을 만듭니다. 기존 그룹을 마우스 오른쪽 단추로 클릭하여 인접 그룹을 추가합니다. 정의에 따르면 세부 정보 그룹은 가장 안쪽 그룹이며 하위 그룹으로만 추가할 수 있습니다. 기존 그룹을 삭제하려면 마우스 오른쪽 단추로 클릭합니다. 그룹 값을 표시할 행과 열은 자동으로 추가됩니다. 자세한 내용은 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)를 참조하세요.  
  
 차트 데이터 영역에서 차트를 클릭하여 끌어 놓기 영역을 표시합니다. 데이터 세트 필드를 범주 및 계열 끌어 놓기 영역으로 끌어서 그룹을 만듭니다. 중첩된 그룹을 추가하려면 끌어 놓기 영역에 여러 필드를 추가합니다.  
  
 기본적으로 계기에서는 그룹이 정의되지 않습니다. 계기의 기본 동작은 지정한 필드의 모든 값을 계기에 표시되는 하나의 값으로 집계하는 것이기 때문입니다. 자세한 내용은 [계기&#40;보고서 작성기 및 SSRS&#41;](gauges-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-parent-or-child-row-or-column-group-to-a-tablix-data-region"></a>테이블릭스 데이터 영역에 부모 또는 자식 행이나 열 그룹을 추가하려면  
  
1.  필드를 **보고서 데이터** 창에서 **행 그룹** 창 또는 **열 그룹** 창으로 끕니다.  
  
    > [!NOTE]  
    >  그룹화 창이 표시되지 않는 경우 보기 탭에서 **그룹화**를 클릭합니다.  
  
2.  안내 막대를 사용하여 필드를 그룹 계층 구조 위 또는 아래로 끌어 놓아서 그룹을 기존 그룹에 부모 그룹이나 자식 그룹으로 배치합니다.  
  
     기본 이름, 그룹 식 및 필드 이름을 기반으로 하는 정렬 식이 적용된 그룹이 추가됩니다.  
  
### <a name="to-add-an-adjacent-row-or-column-group-to-a-tablix-data-region"></a>테이블릭스 데이터 영역에 인접 행 또는 열 그룹을 추가하려면  
  
1.  그룹화 창에서 추가할 그룹의 피어 그룹을 마우스 오른쪽 단추로 클릭합니다. **그룹 추가**를 클릭하고 **앞에 인접** 또는 **뒤에 인접** 을 클릭하여 그룹을 추가할 위치를 지정합니다. **테이블릭스 그룹** 대화 상자가 열립니다.  
  
2.  **이름**에 그룹의 이름을 입력합니다.  
  
3.  **그룹 식**에서 식을 입력하거나 식 단추(**fx**)를 클릭하여 식을 만듭니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     새 그룹이 그룹화 창에 추가되고 그룹 값이 표시되는 행 또는 열이 디자인 화면의 테이블릭스 데이터 영역에 추가됩니다.  
  
### <a name="to-add-a-details-group-to-a-tablix-data-region"></a>테이블릭스 데이터 영역에 세부 정보 그룹을 추가하려면  
  
1.  그룹화 창에서 가장 안쪽 자식 그룹( **세부 정보** 그룹 아님)을 마우스 오른쪽 단추로 클릭합니다. **그룹 추가**를 클릭한 다음 **자식 그룹**을 클릭합니다. **테이블릭스 그룹** 대화 상자가 열립니다.  
  
2.  **그룹 식**에서 식을 공백으로 둡니다. 세부 정보 그룹에는 식이 없습니다.  
  
3.  **세부 데이터 표시**를 선택합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     새로운 세부 정보 그룹이 그룹화 창에 자식 그룹으로 추가되고 1단계에서 선택한 그룹의 행 핸들에 세부 정보 그룹 아이콘이 표시됩니다. 핸들에 대한 자세한 내용은 [테이블릭스 데이터 영역 셀, 행 및 열&#40;보고서 작성기 및 SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="to-edit-a-row-or-column-group-in-a-tablix-data-region"></a>테이블릭스 데이터 영역에서 행 또는 열 그룹을 편집하려면  
  
1.  보고서 디자인 화면에서 테이블릭스 데이터 영역의 아무 곳이나 클릭하여 선택합니다. 그룹화 창에 행 및 열 그룹이 표시됩니다.  
  
2.  그룹을 마우스 오른쪽 단추로 클릭한 다음 **그룹 속성**을 클릭합니다.  
  
3.  **이름**에 그룹의 이름을 입력합니다.  
  
4.  **그룹 식**에서 단순 식을 입력 또는 선택하거나 식 단추(**fx**)를 클릭하여 그룹 식을 만듭니다.  
  
5.  식을 더 만들려면 **추가** 를 클릭합니다. 지정하는 모든 식은 논리 AND로 연결되어 이 그룹의 데이터가 지정됩니다.  
  
6.  (옵션) **페이지 나누기** 를 클릭하여 페이지 나누기 옵션을 설정합니다.  
  
7.  (옵션) **정렬** 을 클릭하여 그룹의 값에 대한 정렬 순서를 지정하는 식을 선택하거나 입력합니다.  
  
8.  (옵션) **표시 유형** 을 클릭하여 항목의 표시 유형 옵션을 선택합니다.  
  
9. (옵션) **필터** 를 클릭하여 이 그룹에 대한 필터를 설정합니다.  
  
10. (옵션) **변수** 를 클릭하여 이 그룹을 범위로 하며 모든 자식 그룹에서 액세스할 수 있는 변수를 정의합니다.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-group-from-a-tablix-data-region"></a>테이블릭스 데이터 영역에서 그룹을 삭제하려면  
  
1.  그룹화 창에서 그룹을 마우스 오른쪽 단추로 클릭한 다음 **그룹 삭제**를 클릭합니다.  
  
2.  **그룹 삭제** 대화 상자에서 다음 옵션 중 하나를 선택합니다.  
  
    -   **그룹 및 관련 행과 열 삭제** 그룹 데이터를 표시하는 그룹 정의와 모든 관련 행을 삭제하려면 이 옵션을 선택합니다. 세부 정보 그룹의 경우 같은 행이 세부 데이터와 그룹 데이터 모두에 포함되는 경우에는 세부 데이터 행만 삭제됩니다.  
  
    -   **그룹만 삭제** 테이블릭스 데이터 영역의 구조는 그대로 유지하고 그룹 정의만 삭제하려면 이 옵션을 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-details-group-from-a-tablix-data-region"></a>테이블릭스 데이터 영역에서 세부 정보 그룹을 삭제하려면  
  
1.  그룹화 창에서 세부 정보 그룹을 마우스 오른쪽 단추로 클릭한 다음 **그룹 삭제**를 클릭합니다.  
  
2.  **그룹 삭제** 대화 상자에서 다음 옵션 중 하나를 선택합니다.  
  
    -   **그룹 및 관련 행과 열 삭제** 그룹 데이터를 표시하는 그룹 정의와 모든 관련 행을 삭제하려면 이 옵션을 선택합니다. 세부 정보 그룹의 경우 같은 행이 세부 데이터와 그룹 데이터 모두에 포함되는 경우에는 세부 데이터 행만 삭제됩니다.  
  
    -   **그룹만 삭제** 테이블릭스 데이터 영역의 구조는 그대로 유지하고 그룹 정의만 삭제하려면 이 옵션을 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     세부 정보 그룹이 삭제됩니다.  
  
    > [!NOTE]  
    >  정보 행을 제거한 후 각 셀의 식에 적절한 집계 식이 지정되어 있는지 확인합니다. 필요한 경우 식을 편집하여 집계 함수를 원하는 대로 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 및 그룹 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md)   
 [그룹 식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [테이블&#40;보고서 작성기 및 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [행렬&#40;보고서 작성기 및 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
