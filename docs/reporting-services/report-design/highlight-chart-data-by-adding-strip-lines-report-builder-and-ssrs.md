---
title: 줄무늬를 추가하여 차트 데이터 강조 표시(보고서 작성기) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: addd6137-4b6e-4e88-a7e8-9600fcd1ccce
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9fd7c4ee0998f7f0386272130e56bab47303b31c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082090"
---
# <a name="highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs"></a>줄무늬 선을 추가하여 차트 데이터 강조 표시(보고서 작성기 및 SSRS)
  간단히 줄무늬라고도 하는 줄무늬 선은 차트의 배경에 일정한 간격 또는 사용자 지정 간격으로 음영을 적용하는 수평 또는 수직 범위입니다. 다음과 같은 용도에 줄무늬 선을 사용할 수 있습니다.  
  
-   차트에서 개별 값을 조회하기 위한 가독성을 개선합니다. 일정한 간격으로 줄무늬 선을 지정하면 차트를 볼 때 데이터 요소를 구분하는 데 도움이 됩니다.  
  
-   일정한 간격으로 발생하는 날짜를 강조 표시합니다. 예를 들어 판매 보고서에서 줄무늬 선을 사용하여 주말 데이터 요소를 식별할 수 있습니다.  
  
-   특정 주요 범위를 강조 표시합니다. 앞의 판매 보고서 예에서 줄무늬 선을 사용하여 판매량이 가장 높은 80~100달러 범위를 강조 표시할 수 있습니다.  
  
 줄무늬 선은 셰이프 차트나 극좌표형 차트에는 적용할 수 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-interlaced-strip-lines-at-regular-intervals-on-a-chart"></a>차트에 인터레이스된 줄무늬 선을 일정한 간격으로 표시하려면  
  
1.  가로 줄무늬 선을 표시하려면 세로 차트 축을 마우스 오른쪽 단추로 클릭하고 **세로 축 속성**을 클릭합니다.  
  
     세로 줄무늬 선을 표시하려면 가로 차트 축을 마우스 오른쪽 단추로 클릭하고 **가로 축 속성**을 클릭합니다.  
  
2.  **인터레이스 사용** 옵션을 선택합니다. 차트에 회색 줄무늬 선이 나타납니다.  
  
3.  (옵션) 인접한 **색** 드롭다운 목록을 사용하여 줄무늬 선의 색을 지정합니다.  
  
### <a name="to-display-interlaced-strip-lines-at-custom-intervals-on-a-chart"></a>차트에 인터레이스된 줄무늬 선을 사용자 지정 간격으로 표시하려면  
  
1.  가로 줄무늬 선을 표시하려면 세로 차트 축을 마우스 오른쪽 단추로 클릭하고 **세로 축 속성**을 클릭합니다.  
  
     세로 줄무늬 선을 표시하려면 가로 차트 축을 마우스 오른쪽 단추로 클릭하고 **가로 축 속성**을 클릭합니다.  
  
     축 속성이 속성 창에 표시됩니다.  
  
2.  속성 창의 **모양** 섹션에서 StripLines 속성에 대한 컬렉션 편집(…) 단추를 클릭하여 **ChartStripLine 컬렉션 편집기**를 엽니다.  
  
3.  **추가** 를 클릭하여 컬렉션에 새 줄무늬 선을 추가합니다.  
  
4.  StripWidth를 클릭하여 보고서에서 인치 단위로 측정되는 줄무늬 선의 너비를 지정합니다. 날짜나 시간을 강조 표시하는 경우 StripWidthType을 클릭하고 시간 간격을 선택합니다.  
  
5.  에 줄무늬 선이 반복되는 빈도를 지정하려면 Interval에 값 또는 식을 입력합니다.  예를 들어 간격을 10으로 지정하고 줄무늬 선 너비가 5인 경우 줄무늬 선은 0~5, 15~20, 30~35 값에 표시됩니다.  
  
> [!NOTE]  
>  기본적으로 Interval은 Auto로 설정되며 이는 차트가 사용자 지정 줄무늬 선에 대한 간격을 계산하지 않음을 의미합니다. 차트는 간격 값이 설정된 경우에만 줄무늬 선의 간격을 계산합니다.  
  
## <a name="see-also"></a>참고 항목  
 [차트의 축 레이블 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [차트에 이동 평균 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)  
  
  
