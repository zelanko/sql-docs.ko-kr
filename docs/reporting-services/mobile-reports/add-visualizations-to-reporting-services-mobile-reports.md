---
title: "Reporting Services 모바일 보고서에 시각화 추가 | Microsoft Docs"
ms.custom: 
ms.date: 09/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3b220b74-9ecd-4084-93fb-545208d5d7a2
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7a6554de812f8f85c9adbd7a3338ab744555e9a0
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="add-visualizations-to-reporting-services-mobile-reports"></a>Reporting Services 모바일 보고서에 시각화 추가
차트는 데이터 시각화의 필수적인 부분입니다. [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 모바일 보고서에서 여러 시나리오를 처리할 수 있는 차트에 대해 알아보세요. 

[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-long.md)] 에는 세 가지 기본 차트 종류인 시간, 범주 및 요약이 있습니다. 이 세 가지 차트 종류에는 고유한 두 계열 집합을 비교하는 데 유용한 해당 비교 차트가 있습니다.  

## <a name="shared-chart-properties"></a>공유 차트 속성

모든 차트에 적용되는 속성도 있고 특정 차트에만 적용되는 속성도 있습니다. 몇 가지 공유 속성은 다음과 같습니다.

### <a name="number-format"></a>숫자 형식
[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 에서는 차트의 숫자에 일반, 소수점이 있거나 없는 통화, 소수점이 있거나 없는 백분율 등의 다양한 형식을 할당할 수 있습니다. 차트에서 숫자 형식은 데이터 요소 팝업과 축 주석에도 적용됩니다. 숫자 형식은 모바일 보고서 전체가 아니라 각 차트에 개별적으로 설정합니다. 

* 숫자 형식을 설정하려면 **레이아웃** 탭을 선택하고 디자인 화면에서 차트를 선택한 다음 **시각적 속성** 창에서 **숫자 형식**을 선택합니다. 
  
### <a name="legend"></a>범례
* 차트에 대한 범례를 표시하려면 **레이아웃** 탭을 선택하고 디자인 화면에서 차트를 선택한 다음 **시각적 속성** 창에서 **범례 표시** 를 **켜짐**으로 설정합니다.
  
### <a name="series"></a>계열
차트에 표시되는 각 개별 메트릭이나 값은 계열로 참조됩니다. 계열이 여러 개이면 공통 x축과 공통 y축을 공유할 수 있으며, 실제로 공유합니다. 계열은 데이터 뷰의 데이터 속성 패널에서 하나 이상의 데이터 테이블 및 필드를 선택하여 정의됩니다. 각 필드는 차트 시각화에서 개별 데이터 요소 계열을 고유한 색으로 정의합니다.  

### <a name="change-aggregation"></a>집계 변경 
차트에서 숫자 필드에 대한 기본 집계는 sum입니다. 집계를 average, count, minimum, maximum, first 또는 last로 변경할 수 있습니다.

* **데이터** 탭을 선택하고 **데이터 속성**에서 숫자 필드 옆에 있는 **옵션**을 선택한 후 > 다른 집계를 선택합니다.

### <a name="set-or-clear-filters"></a>필터 설정 또는 지우기

탐색기를 추가하여 모바일 보고서를 필터링하는 경우 필터링할 차트를 결정할 수 있습니다.

1. **데이터** 탭을 선택하고 **데이터 속성**에서 **옵션**을 선택합니다.

2. **필터링 기준**아래에 선택하거나 선택 취소할 수 있는 탐색기가 표시됩니다.

자세한 내용은 [탐색기를 추가하여 모바일 보고서 필터링](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)을 참조하세요.
   
## <a name="time-charts"></a>시간 차트  
  
시간 차트는 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]에서 가장 기본적인 차트입니다. 차트의 시간 및 날짜 축은 데이터 테이블에서 첫 번째로 유효한 날짜/시간 필드로 자동 설정됩니다.  

![mobile-report-time-chart](../../reporting-services/mobile-reports/media/mobile-report-time-chart.png)

1. **레이아웃** 탭에서 **시간 차트** 를 디자인 화면으로 끌어 놓고 크기를 조정합니다.

2. 기본적으로 누적 가로 막대형 차트입니다. 차트 종류는 **계열 시각화**에서 변경할 수 있습니다.

3. 차트에 필요한 데이터가 보고서에 아직 없는 경우 **데이터** 탭 > **데이터 추가**를 [Excel 또는 공유 데이터 집합에서 데이터 가져오기](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)로 선택합니다.

3. **데이터 속성** 창에서 **주 계열**은 **SimulatedTable**입니다. 상자에서 화살표를 선택한 다음 > 해당 테이블을 선택합니다.

5. **데이터 구조**를 **열 기준**로 설정한 경우(**레이아웃** 탭 > **시각적 속성** 창) **데이터 속성** 창에서 숫자 값의 여러 열을 선택할 수 있습니다.

   **데이터 구조**를 **행 기준**로 설정한 경우에는 **데이터 속성** 창에서 **계열 이름 필드** 하나와 숫자 값 열 하나를 선택할 수 있습니다.
   
자세한 내용은 [열 또는 행을 기준으로 데이터 그룹화](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)를 참조하세요.
  
## <a name="category-charts"></a>범주 차트  
  
시간 차트와 달리 범주 차트에서는 x축에 있는 날짜/시간 필드 이외의 필드를 기준으로 그룹화합니다. *범주 좌표*라고도 하는 이 그룹화는 숫자 필드가 아니라 문자열 필드에 설정해야 합니다.

![mobile-report-category-chart](../../reporting-services/mobile-reports/media/mobile-report-category-chart.png)   

1. **레이아웃** 탭에서 **범주 차트** 를 디자인 화면으로 끌어 놓고 크기를 조정한 다음 필요한 경우 [해당 데이터를 가져옵니다](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

2. **데이터** 탭을 선택하고 **데이터 속성** 창의 **범주 좌표**에서 그룹화 기준으로 사용할 테이블과 필드를 선택합니다. 이 필드는 결과 차트의 x축에 있습니다.

3. **주 계열**에서 각 범주에 대해 집계할 테이블과 숫자 필드를 선택합니다. 
  
## <a name="totals-charts"></a>요약 차트  

![mobile-report-totals-chart](../../reporting-services/mobile-reports/media/mobile-report-totals-chart.png)
  
요약 차트는 다음 두 가지 작업을 수행합니다. 
* 여러 계열을 표시하지 않고 정의된 주 계열의 합계만 표시합니다. 
* 열 또는 행을 기준으로 데이터를 그룹화하는 옵션을 제공합니다. 열을 기준으로 그룹화하면 일반 데이터를 처리할 때 유용할 수 있습니다. 열을 기준으로 그룹화하는 경우 범주 열이 주 계열 속성에서 선택한 필드 수로 자동 결정되므로 주 계열 속성만 사용하면 됩니다.  

자세한 내용은 [열 또는 행을 기준으로 데이터 그룹화](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)를 참조하세요. 
  
## <a name="comparison-charts"></a>비교 차트  
  
시간, 범주 및 요약 차트를 *비교 차트*로 사용할 수도 있습니다. 비교 차트에서는 주 계열뿐만 아니라 두 번째 비교 계열도 지정할 수 있습니다. 주 계열과 비교 계열을 세 가지 방법으로 표시할 수 있습니다.

![mobile-report-comparison-time-chart](../../reporting-services/mobile-reports/media/mobile-report-comparison-time-chart.png)

1. **레이아웃** 탭에서 **비교 차트** 중 하나(시간, 범주 또는 요약)를 디자인 화면으로 끌어 놓고 크기를 조정한 다음 필요한 경우 [해당 데이터를 가져옵니다](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

2. **시각적 속성** 창의 **계열 시각화**에서 다음 중 하나를 선택합니다. 
   * 가로 막대형 및 가는 가로 막대형
   * 꺾은선형 및 가로 막대형
   * 가로 막대형 및 단계 영역 

비교 차트에서 계열의 주 값과 비교 값에 동일한 차트 색을 사용하도록 선택할 수 있습니다.

* **시각적 속성** 창에서 **비교 계열에서 색 재사용** 을 **켜짐**으로 설정합니다.

   **켜짐**으로 설정하면 주 계열과 비교 계열 그리기 사이에 색상표가 다시 시작되므로 주 계열과 비교 계열의 관련 값이 동일합니다. 

   **꺼짐**으로 설정하면 비교 계열 다음에 주 계열을 그릴 때 색상표가 계속 정상적으로 회전하여 두 계열 집합 간에 잠재적으로 색이 잘못 조정될 수 있는 문제를 방지합니다.  
  
## <a name="pie-and-funnel-charts"></a>원형 및 깔때기형 차트  
  
원형 및 깔때기형 차트는 시각화 중 가장 간단합니다. 행 또는 열을 기준으로 데이터를 구조화할 수 있습니다. 
* **모바일 보고서의** 원형 차트 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 는 원형, 도넛형 또는 중앙에 요약이 포함된 도넛형일 수 있습니다. 원형 차트는 전체에서 각 부분의 상대적 크기를 표시하는 데 유용합니다. 조각이 너무 많으면 읽기가 어렵습니다.
* **깔때기형 차트** 는 주로 판매량과 같은 프로세스의 단계를 표시하는 데 사용됩니다.

![mobile-report-funnel-chart](../../reporting-services/mobile-reports/media/mobile-report-funnel-chart.png)

### <a name="structure-pie-and-funnel-chart-data-by-rows-or-by-columns"></a>행 또는 열을 기준으로 원형 및 깔때기형 차트 데이터 구조화
1. **레이아웃** 탭에서 **원형 차트** 또는 **깔때기형 차트** 를 디자인 화면으로 끌어 놓고 크기를 조정한 다음 필요한 경우 [해당 데이터를 가져옵니다](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).
2. **시각적 속성** 창의 **데이터 구조**에서 다음 중 하나를 선택합니다.
   * **열 기준**
   * **행 기준**
3. **열 기준**을 선택한 경우 **데이터** 탭을 선택하고 **데이터 속성** 창의 **주 계열**에서 원형 또는 깔때기형 차트에 집계하려는 테이블과 모든 필드를 선택합니다. 필드 이름은 결과 차트의 각 영역에 레이블을 지정하는 데 사용됩니다.

   **행 기준**을 선택한 경우 **데이터** 탭을 선택하고 **데이터 속성** 창의 **범주 열**에서 원형의 그룹화 및 레이블에 사용할 값이 있는 테이블과 열을 선택합니다. 주 계열 열에서 차트의 값에 사용할 숫자 필드를 선택합니다.

자세한 내용은 [열 또는 행을 기준으로 데이터 그룹화](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)를 참조하세요. 

## <a name="treemaps"></a>트리맵  
  
트리맵은 사각형 그리드 안의 타일 크기와 색에 값을 적용하여 메트릭을 표시합니다. 

![mobile-report-group-treemap](../../reporting-services/mobile-reports/media/mobile-report-group-treemap.png)

1. **레이아웃** 탭에서 **트리맵** 을 디자인 화면으로 끌어 놓고 크기를 조정한 다음 필요한 경우 [해당 데이터를 가져옵니다](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).
2.  **데이터** 탭을 선택하고 **데이터 속성** 창에서 다음을 수행합니다. 

     * **크기** 에서 타일 크기에 대한 숫자 필드를 선택합니다.
     * **색** 에서 타일 색에 대한 숫자 필드를 선택합니다. 
     * [옵션] **사용자 지정 중앙값**: 시각화 형식이 HeatMapWithCustomCenterValue인 경우 **사용자 지정 중앙값** 만 사용할 수 있습니다.
     
         중앙값은 상자의 색을 결정합니다. 중앙값에 비해 메트릭이 좋을수록 더 녹색이 됩니다. 메트릭이 나쁠수록 더 빨간색이 됩니다.
     
     * [옵션] 조회자가 그리드에서 타일을 선택할 때 팝업을 표시하려면 **팝업 레이블** 에서 필드를 하나 또는 여러 개 선택합니다. 트리맵 팝업은 텍스트 및 숫자 필드를 둘 다 표시할 수 있습니다.  

기본적으로 트리맵은 계층적이며 먼저 범주를 기준으로 타일을 그룹화한 다음 크기 및 색을 기준으로 그룹화합니다.
* **데이터** 탭의 **그룹화 기준** 에서 테이블과 필드를 선택합니다.

타일이 크기 및 색을 기준으로만 정렬되도록 그룹화를 끌 수 있습니다. 

* **레이아웃** 탭을 선택하고 **2단계 트리맵** 을 **꺼짐**으로 설정합니다.   

## <a name="waterfall-charts"></a>폭포 차트

폭포 차트는 값을 더하거나 뺄 때의 누계를 보여 줍니다. 따라서 일련의 양수 및 음수 값을 변경하면 초기 값(예를 들어 순이익)이 어떻게 바뀌는지 쉽게 이해할 수 있습니다.

값이 증가하면 막대가 녹색으로 표시되고 감소하면 빨간색으로 표시되기 때문에 구분이 쉽습니다. 시작 값과 최종 값 막대는 0에서 시작하는 경우가 많으며 중간 값은 부동 세로 막대로 나타납니다. 이러한 "모양" 때문에 폭포 차트를 브리지 차트라고도 합니다.

### <a name="when-to-use-a-waterfall-chart"></a>폭포 차트가 유용한 경우

폭포 차트는 다음과 같은 경우에 유용합니다.
* 시계열 또는 다른 범주에서 측정값이 변하여 총 값에 영향을 주는 주요 변경 사항을 검토할 때.
* 수익의 다양한 요인을 표시하여 회사의 연간 수익을 플로팅하고 총 수익(또는 손실)을 얻을 때.
* 연간 회사의 시작 인원수와 최종 인원수를 표시할 때.
* 월별 수입과 지출, 계좌의 잔액 흐름을 시각화할 때. 

### <a name="create-a-waterfall-chart"></a>폭포 차트 만들기

1. **레이아웃** 탭에서 **폭포 차트** 를 디자인 화면으로 끌어 놓고 크기를 조정한 다음 필요한 경우 [해당 데이터를 가져옵니다](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

    ![모바일-보고서-폭포-차트-아이콘](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart-icon.png)
    
2.  **데이터** 탭을 선택하고 **데이터 속성** 창에서 **범주 좌표**에는 데이터의 범주 필드를, **주 계열**에는 숫자 필드를 선택합니다. 

    ![모바일-보고서-폭포-데이터](../../reporting-services/mobile-reports/media/mobile-report-waterfall-data.png)
    
3. 미리 보기로 폭포 차트를 보려면 **레이아웃** 을 탭합니다.

   ![모바일-보고서-폭포-차트](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart.png)
   
   2월, 6월, 7월 같이 손실이 난 달은 빨간색입니다. 
   9월, 10월, 11월 같이 수익이 난 달은 녹색입니다. 

## <a name="see-also"></a>참고 항목 
* [Maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services 모바일 보고서의 탐색기](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services 모바일 보고서의 데이터 표](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)
* [Reporting Services 모바일 보고서의 계기](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
  


