---
title: 데이터 영역의 데이터 정렬(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2fcb9be2-1daa-4c92-ad00-5f63cdf39f70
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dac2694101678f8728de4a4bcdd3db416ad4c17f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104914"
---
# <a name="sort-data-in-a-data-region-report-builder-and-ssrs"></a>데이터 영역의 데이터 정렬(보고서 작성기 및 SSRS)
  보고서를 처음 실행할 때 데이터 영역에 있는 데이터의 정렬 순서를 변경하려면 데이터 영역 또는 그룹에서 정렬 식을 설정해야 합니다. 기본적으로 그룹의 정렬 식은 그룹 식과 같은 값으로 자동으로 설정됩니다.  
  
-   테이블릭스 데이터 영역에서는 세부 정보 그룹을 포함한 데이터 영역 또는 각 그룹에 대한 정렬 식을 설정합니다. 테이블릭스 데이터 영역에 하나의 세부 정보 그룹만 있는 경우 데이터 영역이나 세부 정보 그룹에서 쿼리로 정렬 식을 정의할 수 있으며 모두 동일한 결과를 얻을 수 있습니다.  
  
-   차트 데이터 영역에서는 범주 및 계열 그룹에 대한 정렬 식을 설정하여 각 그룹에 대한 정렬 순서를 제어합니다. 차트 범례에서 색 순서는 범주 그룹의 데이터 요소에 대한 정렬 식으로 결정됩니다.  
  
-   계기 데이터 영역에서는 범위에 상대적인 단일 값이 계기에 표시되므로 일반적으로 데이터를 정렬하지 않아도 됩니다. 계기에서 데이터를 정렬해야 하는 경우 그룹을 먼저 정의한 다음 그룹에 대한 정렬 식을 설정해야 합니다.  
  
 자세한 내용은 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)를 참조하세요.  
  
 테이블릭스 데이터 영역의 경우 열 머리글 위쪽에 대화형 정렬 단추를 추가하면 사용자가 그룹 또는 정보 행의 정렬 순서를 변경할 수 있습니다. 자세한 내용은 [대화형 정렬&#40;보고서 작성기 및 SSRS&#41;](interactive-sort-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-sort-data-in-a-tablix-data-region"></a>테이블릭스 데이터 영역에서 데이터를 정렬하려면  
  
1.  디자인 화면에서 행 핸들을 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 클릭합니다.  
  
2.  **정렬**을 클릭합니다.  
  
3.  각 정렬 식에 대해 다음 단계를 수행합니다.  
  
    1.  **추가**를 클릭합니다.  
  
    2.  데이터를 정렬할 식을 입력하거나 선택합니다.  
  
    3.  **순서** 열 드롭다운 목록에서 각 식에 대한 정렬 방향을 선택합니다. **A-Z** 를 선택하면 식이 오름차순으로 정렬되고 **Z-A** 를 선택하면 식이 내림차순으로 정렬됩니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-values-in-a-group-including-the-details-group-for-a-tablix"></a>테이블릭스에 대해 세부 정보 그룹을 포함한 그룹 내 값을 정렬하려면  
  
1.  디자인 화면에서 테이블릭스 데이터 영역을 클릭하여 선택합니다. 그룹화 창에 테이블릭스 데이터 영역에 대한 행 그룹과 열 그룹이 표시됩니다.  
  
2.  행 그룹 창에서 그룹 이름을 마우스 오른쪽 단추로 클릭한 다음 **그룹 편집**을 클릭합니다.  
  
3.  **테이블릭스 그룹** 대화 상자에서 **정렬**을 클릭합니다.  
  
4.  각 정렬 식에 대해 다음 단계를 수행합니다.  
  
    1.  **추가**를 클릭합니다.  
  
    2.  데이터를 정렬할 식을 입력하거나 선택합니다.  
  
    3.  **순서** 열 드롭다운 목록에서 각 식에 대한 정렬 방향을 선택합니다. **A-Z** 를 선택하면 식이 오름차순으로 정렬되고 **Z-A** 를 선택하면 식이 내림차순으로 정렬됩니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-x-axis-labels-in-alphabetical-order-on-a-chart"></a>차트에서 x축 레이블을 사전순으로 정렬하려면  
  
1.  범주 필드 끌어 놓기 영역의 필드를 마우스 오른쪽 단추로 클릭하고 **범주 그룹 속성**을 클릭합니다.  
  
2.  **범주 그룹 속성** 대화 상자에서 **정렬**을 클릭합니다.  
  
3.  각 정렬 식에 대해 다음 단계를 수행합니다.  
  
    1.  **추가**를 클릭합니다.  
  
    2.  그룹화 필드와 일치하는 식을 선택합니다. **그룹화**를 클릭하여 그룹화 필드에 대한 식을 확인할 수 있습니다.  
  
    3.  **순서** 열 드롭다운 목록에서 각 식에 대한 정렬 방향을 선택합니다. **A-Z** 를 선택하면 식이 오름차순 영문자 순서로 정렬되고 **Z-A** 를 선택하면 식이 내림차순 영문자 순서로 정렬됩니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-the-data-points-in-ascending-or-descending-order-on-a-chart"></a>차트에서 데이터 요소를 오름차순 또는 내림차순으로 정렬하려면  
  
1.  범주 필드 끌어 놓기 영역의 필드를 마우스 오른쪽 단추로 클릭하고 **범주 그룹 속성**을 클릭합니다.  
  
2.  **범주 그룹 속성** 대화 상자에서 **정렬**을 클릭합니다.  
  
3.  각 정렬 식에 대해 다음 단계를 수행합니다.  
  
    1.  **추가**를 클릭합니다.  
  
    2.  데이터 필드와 일치하는 식을 선택합니다. 대부분의 경우 `=Sum(Fields!Quantity.Value)`과 같은 집계 값입니다.  
  
    3.  **순서** 열 드롭다운 목록에서 각 식에 대한 정렬 방향을 선택합니다. **A-Z** 를 선택하면 식이 오름차순으로 정렬되고 **Z-A** 를 선택하면 식이 내림차순으로 정렬됩니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-data-in-ascending-or-descending-order-for-display-on-a-gauge"></a>계기 화면에서 데이터를 오름차순 또는 내림차순으로 정렬하려면  
  
1.  계기를 마우스 오른쪽 단추로 클릭하고 **데이터 그룹 추가**를 클릭합니다.  
  
2.  필요한 경우 **계기 패널 그룹 속성** 대화 상자에서 **일반** 을 클릭합니다.  
  
3.  **그룹 식**에서 **추가**를 클릭합니다.  
  
4.  **그룹화 대상**에서 데이터를 그룹화할 식을 입력하거나 선택합니다.  
  
5.  사용할 그룹 식을 모두 추가할 때까지 3-4단계를 반복합니다.  
  
6.  **정렬**을 클릭합니다.  
  
7.  각 정렬 식에 대해 다음 단계를 수행합니다.  
  
    1.  **추가**를 클릭합니다.  
  
    2.  그룹화 필드와 일치하는 식을 선택합니다. **그룹화**를 클릭하여 그룹화 필드에 대한 식을 확인할 수 있습니다.  
  
    3.  **순서** 열 드롭다운 목록에서 각 식에 대한 정렬 방향을 선택합니다. **A-Z** 를 선택하면 식이 오름차순으로 정렬되고 **Z-A** 를 선택하면 식이 내림차순으로 정렬됩니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 계기에서 데이터를 그룹화하는 방법에 대한 자세한 내용은 [계기&#40;보고서 작성기 및 SSRS&#41;](gauges-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [대화 상자, 창 및 마법사에 대 한 보고서 작성기 도움말](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [차트 &#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [차트의 축 레이블 서식 지정 &#40;보고서 작성기 및 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [여러 셰이프 차트에 일관된 색 지정&#40;보고서 작성기 및 SSRS&#41;](shape-charts-report-builder-and-ssrs.md)  
  
  
