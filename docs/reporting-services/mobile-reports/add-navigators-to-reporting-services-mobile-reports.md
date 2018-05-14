---
title: Reporting Services 모바일 보고서에 탐색기 추가 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: mobile-reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e141f50e-49a9-46c6-983c-f656013aa07c
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a4a4b4c717ae7a8d7fffa772738c6bdb4aeb2fee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="add-navigators-to-reporting-services-mobile-reports"></a>Add navigators to Reporting Services mobile reports
[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]에서 시각화의 데이터를 시간별 또는 선택 항목별로 필터링하려면 *탐색기* 를 추가합니다. 

탐색기는 Power BI 및 Excel 피벗 테이블의 슬라이서와 비슷하지만 몇 가지 고유한 특성도 가지고 있습니다.

**시간 기반 탐색기** 는 지정된 시간 범위에 속하는 행을 선택하여 테이블을 필터링합니다. 

**선택 기반 탐색기** 는 특정 열 값이 선택된 키 값과 일치하는 행을 선택하거나 계층적 트리의 경우 특정 열 값이 선택된 키 값의 하위 트리에 속하는 행을 선택하여 테이블을 필터링합니다. 선택 탐색기 형식은 두 가지가 있습니다.
* 선택 목록은 Power BI 및 Excel의 슬라이서와 유사한 모바일 보고서를 필터링하는 데 사용할 수 있는 단일 열 테이블입니다.
* 성과 기록표 표는 모바일 보고서를 필터링하고 다음을 포함할 수도 있습니다. 
  
## <a name="time-navigators"></a>시간 탐색기   
  
이름에서 알 수 있듯이 시간 범위에 의해 제한되는 데이터 범위를 필터링하는 데 시간 탐색기를 사용합니다.   
  
![SSMRP_TimeNav](../../reporting-services/mobile-reports/media/ssmrp-timenav.png)  
*왼쪽에서 네 개의 꺾은선형 차트는 시간 범위 사전 설정에서 설정됩니다. 오른쪽의 꺾은선형 차트가 필터입니다.*  
  
미리 보기 또는 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 웹 포털에서 보고서를 볼 때 시간 탐색기에 있는 화살표를 끌어 보고서의 나머지를 필터링합니다.  
  
![SSMRP_TimeNavPreview](../../reporting-services/mobile-reports/media/ssmrp-timenavpreview.png)  
  
기본적으로 시간 탐색기는 시간 기반 데이터에 연결된 보고서의 모든 시각적 개체를 필터링합니다. 테이블에 둘 이상의 시간 기반 열이 포함된 경우 첫 번째 열만 필터링에 사용됩니다. 계열 테이블은 포함된 시각화를 구동하고 모바일 보고서의 전체 날짜 범위를 결정합니다.  
  
시간 탐색기에서 시각화의 연결을 끊을 수 있습니다.   
1. 시각화를 선택한 다음 **데이터** 탭을 선택합니다.  
2. **데이터 속성**에서 **옵션**을 선택합니다.  
3. **필터링 기준** 확인란의 선택을 취소합니다.  
  
   ![SSMRP_ClearTimeFilter](../../reporting-services/mobile-reports/media/ssmrp-cleartimefilter.png)  
  
## <a name="selection-lists"></a>선택 목록   
  
선택 목록은 목록에서 선택한 값을 필터링된 테이블의 각 행에 지정된 열의 값과 비교하여 모바일 보고서의 데이터를 필터링합니다. 

1. **레이아웃** 탭에서 **선택 목록** 을 디자인 화면으로 끌어서 원하는 방법으로 크기를 조정합니다.

2. **데이터** 탭을 선택하고 **키** 아래의 **데이터 속성**창에서 필터로 사용할 테이블 및 열을 선택합니다. 

3. **레이블**아래에서 표시되는 레이블이 있는 열을 선택합니다. 키 열과 레이블 열은 같을 수 있습니다.  
  
   계층적 트리 데이터의 경우 부모 키 열을 선택합니다.  
  
4. 데이터 속성을 설정한 후 **선택 목록으로 필터링된 테이블**아래에서 필터링할 테이블 및 필터링 기준이 되는 열을 선택합니다. 이 열은 선택 목록의 키 열에 있는 값과 일치해야 합니다. 

선택 목록에서 필터링하려는 모바일 보고서의 각 시각화의 경우:

1. 시각화를 선택하고 **데이터** 탭을 선택한 다음 **데이터 속성** 창에서 필드 이름 옆의 **옵션** 을 선택합니다.

   ![mobile-report-set-selection-list](../../reporting-services/mobile-reports/media/mobile-report-set-selection-list.png)

2. **필터링 기준**아래에서 선택 목록을 선택합니다.

미리 보기 또는 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 웹 포털에서 모바일 보고서를 보고 선택 목록에서 값을 선택할 때 모바일 보고서의 다른 시각화 요소가 필터링됩니다.

![mobile-report-selection-list-filtering](../../reporting-services/mobile-reports/media/mobile-report-selection-list-filtering.png) 
     
## <a name="scorecard-grid"></a>성과 기록표 표  
  
성과 기록표 표에서는 선택 목록을 필터링하는 것과 같이 함수를 필터링하지만 값 열과 점수 표시기도 표시합니다. 점수 표시기는 표시기 데이터 표의 표시기와 동일합니다. 키, 레이블 및 선택적 부모 키 열을 선택한 후 성과 기록표에 데이터를 제공하려면 입력 테이블과 열을 선택합니다. 점수표 데이터 열은 키 열을 기준으로 정렬할 수 있습니다.  

1. **레이아웃** 탭에서 **성과 기록표 표** 를 디자인 화면으로 끌어서 원하는 방법으로 크기를 조정합니다.

2. **데이터** 탭을 선택하고 **키** 아래의 **데이터 속성**창에서 필터로 사용할 테이블 및 열을 선택합니다. 

3. **레이블**아래에서 표시되는 레이블이 있는 열을 선택합니다. 키 열과 레이블 열은 같을 수 있습니다.  
  
4. 점수 표시기를 추가하려면 **데이터 열** 창에서 **점수 추가**를 선택합니다.   
  
5. 점수 표시기의 이름을 지정하고 **옵션** 을 선택하여 데이터 표의 표시기에 설정한 것과 동일한 속성을 설정합니다.  
  
   * 계기 유형
   * 값 필드
   * 비교 필드
   * 값 방향
  
6. 값 표시기를 추가하려면 **데이터 열** 창에서 **값 추가**를 선택합니다.

7. 이름을 원하는 대로 지정하고 테이블에서 원본 열을 선택한 후 포맷 방법을 선택합니다.  

   ![mobile-report-scorecard-grid-data-properties](../../reporting-services/mobile-reports/media/mobile-report-scorecard-grid-data-properties.png)

8. 데이터 속성을 설정한 후 **선택 목록으로 필터링된 테이블**아래에서 필터링할 테이블 및 필터링 기준이 되는 열을 선택합니다. 이 열은 선택 목록의 키 열에 있는 값과 일치해야 합니다. 

미리 보기 또는 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 웹 포털에서 모바일 보고서를 보고 성과 기록표 표에서 값을 선택할 때 모바일 보고서의 다른 시각화 요소가 필터링됩니다.

![mobile-report-scorecard-grid](../../reporting-services/mobile-reports/media/mobile-report-scorecard-grid.png)
    
## <a name="set-which-visualizations-are-filtered"></a>필터링될 시각화 설정  
  
갤러리 요소는 데이터 뷰의 특정 입력에 대한 옵션 단추를 클릭하여 필터를 사용하기 위해 구성될 수 있습니다. 필터는 해당 확인란을 설정/해제하여 활성화됩니다.  

탐색기에서 필터링하는 모바일 보고서의 시각화를 결정할 수 있습니다.

1. 시각화를 선택하고 **데이터** 탭을 선택한 다음 **데이터 속성** 창에서 필드 이름 옆의 **옵션** 을 선택합니다.

   ![mobile-report-set-selection-list](../../reporting-services/mobile-reports/media/mobile-report-set-selection-list.png)

2. **필터링 기준**아래에서 탐색기를 선택합니다. 각 시각화는 여러 탐색기에서 필터링될 수 있습니다.
  
## <a name="cascading-filters"></a>필터 캐스케이드   
  
또한, 필터를 함께 캐스케이드하여 선택한 첫 번째 값으로 두 번째 이용 가능 값을 필터링할 수 있습니다. 필터를 캐스케이드하려면 일반 갤러리 요소와 마찬가지로 키 열에 필터를 적용합니다.  

### <a name="see-also"></a>관련 항목: 
  
* [Reporting Services 모바일 보고서의 지도](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services 모바일 보고서의 시각화](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Reporting Services 모바일 보고서의 계기](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
* [Reporting Services 모바일 보고서의 데이터 표](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)  
