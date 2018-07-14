---
title: 빈 요소에는 차트 추가 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2b056119-439f-494f-83cf-ee0c05dc6487
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 317ada15f03de74dc25767a17036623d7479220a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37181590"
---
# <a name="add-empty-points-to-the-chart-report-builder-and-ssrs"></a>차트에 빈 요소 추가(보고서 작성기 및 SSRS)
  Null 값은 차트에서 계열의 데이터 요소 사이에 있는 빈 공간 또는 간격으로 표시됩니다. 빈 요소는 Null 값에 의해 만들어진 빈 공간에 삽입될 수 있는 데이터 요소입니다.  
  
 기본적으로 빈 요소는 값을 포함하는 이전 및 다음 데이터 요소의 평균을 사용하여 계산됩니다. 모든 빈 요소가 0 지점에서 삽입되도록 이를 변경할 수 있습니다.  
  
 자세한 내용은 [차트의 빈 데이터 요소 및 Null 데이터 요소&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-empty-points-on-a-chart"></a>차트에 빈 요소를 지정하려면  
  
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
  
## <a name="see-also"></a>관련 항목  
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [차트 종류&#40;보고서 작성기 및 SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [차트에 배율 구분선 추가&#40;보고서 작성기 및 SSRS&#41;](add-scale-breaks-to-a-chart-report-builder-and-ssrs.md)   
 [차트 &#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
