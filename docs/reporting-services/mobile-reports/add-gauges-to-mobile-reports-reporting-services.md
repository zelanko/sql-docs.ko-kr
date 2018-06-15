---
title: 모바일 보고서에 계기 추가 | Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: mobile-reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76d8fc8f-c37f-44d3-ab44-45fbeed4e064
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 985bde62deff88231ff889e1f403ad82edc55a0d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33019420"
---
# <a name="add-gauges-to-mobile-reports--reporting-services"></a>모바일 보고서에 계기 추가 | Reporting Services
계기는 모바일 보고서에서 가장 기본적이고 가장 널리 사용되는 시각화 개체입니다. 데이터 집합의 단일 값을 표시합니다. 값만 표시하거나 목표와 비교하여 값을 표시합니다.

![PBI_SSMRP_Gauges](../../reporting-services/mobile-reports/media/pbi-ssmrp-gauges.png)  
  
*레이아웃 탭의 계기 시각화*  
  
SQL Server 모바일 보고서 게시자의 모든 계기에는 하나 이상의 공통 속성이 있습니다. 주 값은 모바일 보고서의 데이터 테이블 중 하나에 있는 숫자 필드에 설정됩니다.  

숫자 계기를 제외한 모든 계기는 비교 또는 주 값과 비교 값 간의 관계인 *델타*값을 표시할 수도 있습니다. 비교 값은 대체로 목표이고, 계기는 해당 목표에 대한 진행률의 시각적 표시기 또는 실제값과 목표 간의 델타입니다.

계기는 주 값으로 하나의 집계된 값과 비교 값으로 하나의 집계된 값만 나타낼 수 있습니다. 계기 집계는 합계, 평균, 최소값, 최대값 등의 표준입니다. 기본적으로 계기 값은 합계이며, 현재 필터링되어 계기 컨트롤에 사용할 수 있는 데이터에 포함된 모든 값의 합계를 표시합니다. 

모바일 보고서의 탐색기에 연결하여 계기 값을 필터링할 수 있습니다. 

## <a name="set-the-main-and-comparison-values-for-a-gauge"></a>계기에 대한 주 값과 비교 값 설정

1. **레이아웃** 탭에서 디자인 눈금으로 계기를 끌어서 원하는 크기로 만듭니다.

2. [Excel 또는 공유 데이터 집합의 데이터](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)를 가져옵니다.

3. **데이터** 탭을 선택하고 **데이터 속성** 창의 **주 값** 에서 데이터 테이블과 숫자 필드를 선택합니다.

3. 숫자 계기를 제외한 계기의 경우 **데이터 속성** 창의 **비교 값** 에서 데이터 테이블과 숫자 필드를 선택합니다.

4. [옵션] 집계를 변경하려면 **옵션** 을 선택한 후 다른 집계를 선택합니다.
   
   >**참고**: 주 값에 대한 집계를 변경하는 경우 비교 값에 대한 집계도 변경하는 것이 좋습니다. 여러 집계 방법을 함께 사용할 수도 있습니다.  

## <a name="filter-a-gauge"></a>계기 필터링
  
모바일 보고서에 탐색기가 있는 경우 계기를 하나 이상의 탐색기에 바인딩하여 필터링할 수 있습니다. 계기의 값과 비교 값을 하나 이상의 다른 탐색기에 바인딩하여 다양한 계기 옵션을 사용할 수 있습니다.  

1. 계기를 선택한 다음 **데이터 속성** 창의 **데이터** 탭에서 **주 값** 또는 **비교 값** 옆에 있는 **옵션**을 선택합니다.

2. 필터링 기준에서 계기를 필터링할 탐색기를 선택합니다.

   ![mobile-report-gauge-navigator](../../reporting-services/mobile-reports/media/mobile-report-gauge-navigator.png)
 
## <a name="set-visual-properties-for-a-gauge"></a>계기의 시각적 속성 설정
  
계기 요소를 데이터 필드에 연결하는 데이터 속성과 더불어 많은 기능 및 시각적 속성을 사용자 지정할 수도 있습니다. 

### <a name="set-value-direction-high-or-low-is-better"></a>값 방향(값이 높을수록 좋음 또는 값이 낮을수록 좋음) 설정
* 계기를 선택한 다음 **시각적 속성** 창의 **레이아웃** 탭에서 **값 방향** 을 **값이 높을수록 좋음** 또는 **값이 낮을수록 좋음**으로 설정합니다. 

**값이 높을수록 좋음** 에서는 양수 값을 녹색으로 지정하여 바람직한 방향으로 변경된 사항을 나타낼지, 낮은 값을 빨간색으로 지정하여 바람직하지 않은 방향으로 변경된 사항을 나타낼지 결정합니다. 

**값이 낮을수록 좋음** 의 색은 그 반대입니다.

값 방향 속성은 비교 값을 지원하는 계기 요소에만 관련이 있습니다. 계기의 색은 델타 정수의 부호와 값 방향 속성 설정에 의해 결정됩니다.  
  
### <a name="set-range-stops-for-a-gauge"></a>계기에 대한 범위 정지 설정
데이터가 아닌 계기 특정 속성 중 두 번째는 범위 중지입니다. 

* 계기를 선택한 다음 **시각적 속성** 창의 **레이아웃** 탭에서 **범위 정지**를 선택합니다.

범위 정지를 사용하여 대상에 맞는지(녹색), 중립적인지(주황색), 대상과 맞지 않는지(빨간색) 등 해당 비교 값 시각화를 표시할 비율을 백분율로 결정합니다. 여기서 계기의 비교 값이 대상이 됩니다. 마찬가지로, 비교 값이 있는 계기만 범위 정지를 지원합니다.  

### <a name="format-the-numbers-in-the-gauge"></a>계기의 숫자 형식 지정  
데이터가 아닌 또 다른 계기 요소 속성으로 다른 많은 요소에서 공유되는 숫자 형식 속성이 있습니다. 

* 계기를 선택한 다음 **시각적 속성** 창의 **레이아웃** 탭에서 **범위 정지**를 선택합니다.

계기에 표시된 숫자의 형식(예: 통화, 백분율, 시간 또는 일반)을 결정합니다. 모바일 보고서의 각 요소에 대해 숫자 형식을 설정합니다.
  
### <a name="see-also"></a>관련 항목: 

* [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
* [Reporting Services 모바일 보고서의 지도](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services 모바일 보고서의 탐색기](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services 모바일 보고서의 시각화](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Reporting Services 모바일 보고서의 데이터 표](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md) 
