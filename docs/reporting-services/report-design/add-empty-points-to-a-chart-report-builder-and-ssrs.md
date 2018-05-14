---
title: 차트에 빈 요소 추가(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2b056119-439f-494f-83cf-ee0c05dc6487
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dfa20f918ae7c5c932e298c371ee9253af7b8d6e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="add-empty-points-to-a-chart-report-builder-and-ssrs"></a>차트에 빈 요소 추가(보고서 작성기 및 SSRS)
Null 값은 차트에서 계열의 데이터 요소 사이에 있는 빈 공간 또는 간격으로 표시됩니다. 페이지가 매겨진 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 빈 요소는 Null 값에 의해 만들어진 빈 공간에 삽입될 수 있는 데이터 요소입니다.  
  
 기본적으로 빈 요소는 값을 포함하는 이전 및 다음 데이터 요소의 평균을 사용하여 계산됩니다. 모든 빈 요소가 0 지점에서 삽입되도록 이를 변경할 수 있습니다.  
  
 자세한 내용은 [차트의 빈 데이터 요소 및 Null 데이터 요소&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-empty-points-on-a-chart"></a>차트에 빈 요소를 지정하려면  
  
1.  속성 창을 엽니다.  
  
2.  디자인 화면에서 Null 값을 포함하는 계열을 마우스 오른쪽 단추로 클릭합니다. 계열의 속성이 속성 창에 표시됩니다.  
  
3.  **EmptyPoint** 노드를 확장합니다.  
  
4.  Color 속성의 색 값을 선택합니다.  
  
5.  **EmptyPoint** 노드에서 Marker 노드를 확장합니다.  
  
6.  MarkerType 속성의 표식 유형을 선택합니다.  
  
    > [!NOTE]  
    >  가로 막대형 차트, 세로 막대형 차트 또는 분산형 차트에 빈 요소를 추가하려면 표식 유형을 선택해야 합니다. 그러나 영역형 차트, 꺾은선형 차트 및 방사형 차트의 경우 표식을 지정하지 않아도 차트에서 빈 공간 또는 간격이 자동으로 채워지므로 표식 유형을 선택하지 않아도 됩니다.  
  
7.  빈 요소의 값을 설정합니다.  
  
    1.  속성 창에서 **CustomAttributes** 노드를 확장합니다.  
  
    2.  EmptyPointValue 속성을 설정합니다. 이전 및 다음 데이터 요소의 평균 지점에서 빈 요소를 삽입하려면 **Average**를 선택합니다. 0 지점에서 빈 요소를 삽입하려면 **Zero**를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [차트 종류&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [차트에 배율 구분선 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-scale-breaks-to-a-chart-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
