---
title: 축 속성 대화 상자, 축 옵션 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.axisproperties.axisoptions.f1
- "10138"
ms.assetid: b276e210-7a12-48ae-971b-7dabae51df11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ff9f3281e47cf6dfdf8a189c653d0e061f4a761d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109955"
---
# <a name="axis-properties-dialog-box-axis-options-report-builder-and-ssrs"></a>축 속성 대화 상자, 축 옵션(보고서 작성기 및 SSRS)
  **가로** 또는 **세로 축 속성** 대화 상자에서 **축 옵션** 을 선택 하 여 차트의 지정 된 축 모양을 정의할 수 있습니다. 이전 버전의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 기본적으로 차트의 x축에 모든 레이블이 표시되었습니다. 그러나 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2008에서는 보다 깔끔한 차트 이미지를 제공하고 레이블이 겹치는 것을 방지하기 위해 레이블이 표시되지 않습니다. 자세한 내용은 [차트의 축 레이블 서식 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **배율 구분선 사용**  
 필요하다고 판단되는 경우 차트에 배율 구분선을 그릴 수 있도록 하려면 이 옵션을 선택합니다. 이 옵션을 활성화하면 데이터 세트의 높은 값 요소와 낮은 값 요소 사이의 차이가 충분하여 배율 구분선을 그릴 수 있는지 여부가 차트에서 자동으로 확인됩니다.  
  
 **방향 바꾸기**  
 차트를 반대 방향으로 바꾸려면 이 옵션을 선택합니다. 예를 들어 세로 막대형 차트에서는 기본적으로 차트 왼쪽에 y 축이 표시되고 왼쪽에서 오른쪽 순으로 각 범주가 배치되는데 이 옵션을 선택하면 차트 오른쪽에 y 축이 표시되고 오른쪽에서 왼쪽 순으로 범주가 배치됩니다.  
  
 **인터레이스 색 사용**  
 차트에 줄무늬 선을 추가한 다음 색을 선택하거나 식을 입력하려면 이 옵션을 선택합니다. 줄무늬 선은 눈금선 사이에 밝은 영역과 어두운 영역이 교대로 배치되는 효과를 주는 차트 영역의 음영 밴드입니다. 이러한 줄무늬 선은 축에서 반복되는 패턴을 강조 표시하는 데 유용합니다.  
  
 **항상 0 포함**  
 축 눈금에 항상 0을 포함하려면 이 옵션을 선택합니다. 이 옵션을 활성화하지 않으면 차트의 축에 0 값이 표시되지 않습니다. 데이터 세트에 음수 또는 0인 값이 들어 있으면 0 값을 포함하는 것이 좋을 수 있습니다.  
  
 **스칼라 축**  
 연속적인 눈금에 축 값의 집합을 표시하려면 이 옵션을 선택합니다. 예를 들어 데이터 세트에 1월, 3월 및 11월 데이터가 들어 있는 경우 축이 스칼라 형식이 아니면 해당 월만 표시되는 반면 스칼라 축에는 한 해의 모든 월이 표시됩니다.  
  
 **로그 눈금 간격 사용**  
 y 축 눈금을 로그 눈금으로 지정하려면 이 옵션을 선택합니다. 이 옵션은 축에 양수 값이 포함되어 있을 때 y 축에만 사용할 수 있습니다.  
  
 로그 눈금을 사용하도록 축을 설정한 경우 사용할 로그의 밑을 입력란에 입력합니다. 기본적으로 차트에는 축의 로그 눈금에 대한 밑으로 10이 사용됩니다. 이 옵션은 축이 숫자일 때 y 축에만 사용할 수 있습니다.  
  
 **최소**  
 x 축의 최소값 또는 이를 반환하는 식을 입력합니다. 생략한 경우 데이터 세트에서 반환한 데이터에 의해 최소값이 결정됩니다.  
  
 **최대화**  
 X축의 최대값 또는 이를 반환하는 식을 입력합니다. 생략한 경우 데이터 세트에서 반환한 데이터에 의해 최대값이 결정됩니다.  
  
 **간격은**  
 축 레이블 간의 간격 값 또는 이를 반환하는 식을 입력합니다. 예를 들어 축에 각 범주 레이블을 표시하려면 1을 입력하고, 범주 레이블을 하나 걸러 하나씩 표시하려면 2를 입력합니다. 간격을 지정하지 않으면 레이블은 데이터 세트의 값을 기준으로 자동으로 계산됩니다.  
  
 **간격 유형**  
 지정된 간격의 간격 유형을 나타내는 식이나 값을 입력합니다. 예를 들어 간격을 이틀로 설정하려면 간격으로 **2** 를 지정하고 간격 유형으로 **일** 을 지정합니다.  
  
 **양쪽 여백**  
 차트 요소와 차트의 양쪽 측면 사이의 여백을 지정하는 값을 선택하거나 이를 반환하는 식을 입력하여 여백을 추가 또는 제거합니다. 이 옵션을 **자동**으로 설정하면 양쪽 여백이 추가됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [차트의 축 레이블 서식 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](report-design/charts-report-builder-and-ssrs.md)   
 [차트에서 계열 색 서식 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [축 간격 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [축 레이블의 서식을 날짜 또는 통화로 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [보조 축에 데이터 플롯 &#40;보고서 작성기 및 SSRS&#41;](report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)   
 [보고서 작성기 및 SSRS &#40;스파크 라인과 데이터 막대&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [차트에서 여백 추가 또는 제거 &#40;보고서 작성기 및 SSRS&#41;](report-design/add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
  
