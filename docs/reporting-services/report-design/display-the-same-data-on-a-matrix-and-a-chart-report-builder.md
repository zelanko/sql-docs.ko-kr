---
title: 행렬 및 차트에 같은 데이터 표시(보고서 작성기) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 1262f283-9fc2-4bc1-9c79-457f7642abc7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f3eafaec96e27d6e78521b0c4ef7580af103a12e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792251"
---
# <a name="display-the-same-data-on-a-matrix-and-a-chart-report-builder"></a>행렬 및 차트에 같은 데이터 표시(보고서 작성기)
  행렬 및 차트에 같은 데이터를 표시하려면 두 데이터 영역에서 같은 데이터 집합을 지정하는 속성을 설정해야 하고 필터, 그룹, 정렬 및 데이터에 대한 동일한 식도 지정해야 합니다.  
  
 두 데이터 영역에는 동일한 데이터 상위 항목(보고서 데이터 집합)이 있으므로 행렬에 대화형 정렬 단추를 추가하여 사용자가 단추를 클릭할 때 행렬 및 차트에 대한 정렬 순서를 변경할 수 있습니다. 자세한 내용은 [테이블 또는 행렬에 대화형 정렬 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)를 참조하세요.  
  
 행렬 열 그룹 값을 차트에 대한 범례로 사용하려면 차트의 계열 데이터에 대한 색을 지정한 다음 같은 색을 그룹 값을 표시하는 행렬 셀의 입력란 배경색으로 사용해야 합니다. 자세한 내용은 [여러 셰이프 차트에 일관된 색 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)을 참조하세요.  
  
 보고서에 그룹 정의에 대한 그룹 값이 너무 많은 경우 런타임에 보고서가 복잡하게 표시될 수 있습니다. 값을 필터링하고 그룹을 결합하거나 차트에서 그룹을 결합하는 임계값을 조정해야 할 수 있습니다. 자세한 내용은 [동일한 데이터 집합에 여러 데이터 영역 연결&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-matrix-and-chart-to-display-the-same-data"></a>같은 데이터를 표시하는 행렬 및 차트를 추가하려면  
  
1.  디자인 뷰에서 보고서를 엽니다.  
  
2.  **삽입** 탭의 **데이터 영역** 그룹에서 **행렬**을 클릭한 다음 보고서 본문이나 보고서 본문의 사각형을 클릭합니다. 보고서에 행렬이 추가됩니다.  
  
3.  **삽입** 탭의 **데이터 영역** 그룹에서 **차트**를 클릭한 다음 차트 종류를 선택합니다. 보고서에 차트가 추가됩니다.  
  
4.  (옵션) **삽입** 탭의 **보고서 항목** 그룹에서 **사각형**을 클릭한 다음 보고서를 클릭합니다. 보고서에 사각형이 추가됩니다. 2단계와 3단계에서 만든 행렬과 차트를 이 사각형으로 끕니다.  
  
     사각형 컨테이너에 여러 데이터 영역을 배치하면 보고서를 볼 때 행렬과 차트의 렌더링 방식을 제어하는 데 도움이 됩니다.  
  
     다음 단계에서는 행렬 및 차트에 같은 데이터 집합 필드가 표시되도록 선택합니다.  
  
5.  보고서 데이터 창에서 행렬의 데이터 셀로 숫자 데이터 집합 필드를 끕니다.  
  
     기본적으로 그룹 값을 계산하는 데는 Sum 집계 함수가 사용됩니다. 행렬의 집계 함수를 변경할 경우에는 차트의 함수도 변경해야 합니다.  
  
6.  행렬에서 데이터가 있는 셀을 마우스 오른쪽 단추로 클릭하고 **입력란 속성**을 클릭한 다음 **숫자**를 클릭합니다. 데이터 집합 필드 값에 적합한 형식을 선택합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  3단계에서 선택한 같은 데이터 집합 필드를 끌어 차트의 **값** 영역에 놓습니다.  
  
9. 차트에서 Y 축을 마우스 오른쪽 단추로 클릭하고 **축 속성**을 클릭한 다음 **숫자**를 클릭합니다. 4단계에서 선택한 것과 같은 데이터 형식을 선택합니다.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     다음 단계에서는 행렬 행 그룹 및 차트 계열 그룹을 같은 식으로 설정하고 차트 계열 그룹에 대한 정렬 순서도 설정합니다.  
  
11. 보고서 데이터 창에서 행렬 행에 대해 그룹화할 데이터 집합 필드를 행 그룹 창으로 끌어옵니다.  
  
     기본적으로 행렬 행 그룹은 그룹 식과 동일한 정렬 식을 추가합니다.  
  
12. 9단계에서 사용한 것과 같은 데이터 집합 필드를 끌어 차트의 **계열 그룹** 영역에 놓습니다.  
  
13. **계열 그룹** 영역에서 해당 그룹을 마우스 오른쪽 단추로 클릭한 다음 **계열 그룹 속성**을 클릭합니다.  
  
14. **정렬**을 클릭합니다.  
  
15. **추가**를 클릭합니다. 새로운 행이 정렬 식 표에 나타납니다.  
  
16. **정렬 기준**의 드롭다운 목록에서 9단계에서 그룹화할 대상으로 선택했던 데이터 집합 필드를 선택합니다.  
  
17. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     다음 단계에서는 행렬 열 그룹 및 차트 범주 그룹을 같은 식으로 설정하고 차트 범주 그룹에 대한 정렬 순서도 설정합니다.  
  
18. 보고서 데이터 창에서 행렬 열에 대한 그룹화할 데이터 집합 필드를 열 그룹 창으로 끌어옵니다.  
  
     기본적으로 행렬 열 그룹은 그룹 식과 동일한 정렬 식을 추가합니다.  
  
19. 16단계에서 사용한 것과 같은 데이터 집합 필드를 끌어 차트의 **범주 그룹** 영역에 놓습니다.  
  
20. **범주 그룹** 영역에서 그룹을 마우스 오른쪽 단추로 클릭한 다음 **범주 그룹 속성**을 클릭합니다.  
  
21. **정렬**을 클릭합니다.  
  
22. **추가**를 클릭합니다. 새로운 행이 정렬 식 표에 나타납니다.  
  
23. **정렬 기준**의 드롭다운 목록에서 16단계에서 그룹화할 대상으로 선택했던 데이터 집합 필드를 선택합니다.  
  
24. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
25. 결과를 미리 봅니다. 행렬 행 및 열 그룹에 차트 계열 및 범주 그룹과 같은 데이터가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [동일한 데이터 집합에 여러 데이터 영역 연결&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
