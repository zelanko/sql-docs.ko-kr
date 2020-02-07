---
title: 모바일 보고서에서 열 또는 행을 기준으로 데이터 그룹화 | Reporting Services | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: b9ebd36c-a337-47ae-83e5-6c2f2144eb52
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c3a4db20da76fa0188db3171f879e6fdcaefdacd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63200909"
---
# <a name="group-data-by-columns-or-rows-in-a-mobile-report--reporting-services"></a>모바일 보고서에서 열 또는 행을 기준으로 데이터 그룹화 | Reporting Services
[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]의 많은 차트 종류에서 열 또는 행을 기준으로 데이터를 구성할 수 있습니다. 이 단계별 지침을 따릅니다.

시간, 합계, 원형 및 깔때기형 차트에서 열 또는 행을 기준으로 데이터를 구성할 수 있습니다. 
* 테이블에 비교하려는 데이터 열이 여러 개 있는 경우 열을 기준으로 구성하는 것이 좋습니다. 
* 테이블의 한 열에 다른 범주의 이름이 있는 경우 행을 기준으로 구성하는 것이 더 좋습니다. 

다음 단계에서는 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 에서 시뮬레이트된 데이터와 비교 합계 테이블을 사용하여 차트의 행 또는 열 기준의 데이터 구조 간의 차이를 설명합니다.  

1. **레이아웃** 탭에서 **비교 합계 차트** 를 디자인 화면으로 끌어 놓고 확장합니다.

2. **데이터** 탭을 선택합니다. SimulatedTable 테이블에는 **Metric1**부터 **Metric5**까지, **Comparison1**부터 **Comparison5**까지의 열 계열이 있습니다. 

   ![mobile-report-data-group-column](../../reporting-services/mobile-reports/media/mobile-report-data-group-column.png)

3. **데이터 속성** 창에서 **주 계열** 은 **SimulatedTable**입니다. **주 계열**옆의 상자에 있는 화살표를 선택하면 **Metric1** 부터 **Metric5** 까지 선택됩니다.

   ![mobile-report-properties-columns](../../reporting-services/mobile-reports/media/mobile-report-properties-columns.png)

   **비교 계열** -- **Comparison1** 부터 **Comparison5** 까지에 대해서도 선택됩니다.
   
4. **미리 보기**를 선택합니다.

   ![mobile-report-chart-by-columns](../../reporting-services/mobile-reports/media/mobile-report-chart-by-columns.png)

   차트의 각 막대는 테이블의 한 열을 나타냅니다. 더 두꺼운 막대가 Metrics 열이고 더 얇은 막대가 Comparison 열입니다.

5. 미리 보기 모드를 종료하려면 왼쪽 위의 뒤로 화살표를 선택합니다.

6. **시각적 속성** 창의 **레이아웃** 탭에서 **데이터 구조** 가 **열별** 에서 **행별**로 변경됩니다.  

7. **데이터** 탭을 선택합니다. 이제 SimulatedTable 테이블에는 **Category** 열뿐만 아니라 **Metric** 및 **Comparison** 열, 범주 A부터 E까지 있습니다. 

   ![mobile-report-data-group-rows](../../reporting-services/mobile-reports/media/mobile-report-data-group-rows.png)

8.  이제 **데이터 속성** 창의 범주 열 상자에 SimulatedTable의 범주 열이 나열됩니다. 주 계열에서 값에 사용할 열을 선택할 수 있습니다. 기본적으로 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 는 주 계열에서 Metric1부터 Metric5까지, 비교 계열에서 Comparison1부터 Comparison5까지 선택합니다. 

    ![mobile-report-properties-rows](../../reporting-services/mobile-reports/media/mobile-report-properties-rows.png)

9. **미리 보기**를 선택합니다.

   ![mobile-report-chart-by-rows](../../reporting-services/mobile-reports/media/mobile-report-chart-by-rows.png)

   이제 차트의 각 막대는 Category 열의 각 범주에 대한 값을 나타냅니다.

### <a name="see-also"></a>참고 항목
* [Reporting Services 모바일 보고서의 시각화](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
