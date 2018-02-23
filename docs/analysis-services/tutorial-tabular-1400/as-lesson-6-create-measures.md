---
title: "Analysis Services 자습서 6 단원: 측정값 만들기 | Microsoft Docs"
description: "Analysis Services tutorial 프로젝트에서 측정값을 만드는 방법을 설명 합니다."
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: b4de99f18366afefaeb5411e0fc5454d378b87f7
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="create-measures"></a>측정값 만들기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 모델에 포함할 측정값을 만들 수 있습니다. 만든 계산된 열과 마찬가지로 측정값은 DAX 수식을 사용 하 여 만든 계산입니다. 그러나 계산된 열과 달리 측정값은 평가 기반으로 사용자가 선택한 *필터*합니다. 예를 들어는 특정 열 이나 슬라이서는 피벗 테이블의 행 레이블 필드에 추가 합니다. 적용된 측정값에 따라 필터의 각 셀에 대한 값이 계산됩니다. 측정값은 숫자 데이터에 대해 동적 계산을 수행 하는 거의 모든 테이블 형식 모델에 포함 시킬 하는 강력 하 고 유연한 계산입니다. 자세한 내용은 참고 [측정값](../tabular-models/measures-ssas-tabular.md)합니다.
  
측정값을 만들려면 사용 하는 *측정값 표*합니다. 기본적으로 각 테이블에는 빈 측정값 표가 있습니다. 그러나 일반적으로 하지 만들면 모든 테이블에 대 한 측정값입니다. 측정값 표는 모델 디자이너의 데이터 보기에서 테이블 아래에 나타납니다. 테이블의 측정값 표를 숨기거나 표시하려면 **테이블** 메뉴를 클릭한 다음 **측정값 표 표시**를 클릭합니다.  
  
측정값 표에서 빈 셀을 클릭 하 고 수식 입력줄에 DAX 수식을 입력 하 여 측정값을 만들 수 있습니다. 측정값 수식을 완성 enter 키를 눌러 다음 셀에 나타납니다. 열을 클릭 하 고 자동 합계 단추를 클릭 한 다음 표준 집계 함수를 사용 하 여 측정값을 만들 수도 있습니다 (**∑**) 도구 모음입니다. 자동 합계 기능을 이용해 만든 측정값은 해당 열 바로 아래에 있는 측정값 표 셀에 나타나지만 이동할 수 있습니다.  
  
이 단원에서는 두 수식을 입력 하 여 DAX 수식 입력줄에서 및 자동 합계 기능을 사용 하 여 측정값을 만듭니다.  
  
이 단원에 소요되는 예상 시간: **30분**  
  
## <a name="prerequisites"></a>필수 구성 요소  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [5 단원: 계산된 열 만들기](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)합니다.  
  
## <a name="create-measures"></a>측정값 만들기  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>DimDate 테이블에서 DaysCurrentQuarterToDate 측정값을 만들려면  
  
1.  모델 디자이너에서 클릭 된 **DimDate** 테이블입니다.  
  
2.  측정값 표에서 왼쪽 위에 있는 빈 셀을 클릭합니다.  
  
3.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    왼쪽 위 셀에 측정값 이름이 표시, **DaysCurrentQuarterToDate**결과 **92**합니다. 결과 관련이 없습니다이 시점에서 사용자 필터가 적용 되었습니다.
    
      ![as-lesson6-newmeasure](../tutorial-tabular-1400/media/as-lesson6-newmeasure.png) 
    
    측정값 수식으로 계산 된 열과 달리 측정값 이름, 수식 식 뒤에 오는 콜론을 입력할 수 있습니다.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>DimDate 테이블에서 DaysInCurrentQuarter 측정값을 만들려면  
  
1.  와 **DimDate** 모델 디자이너의 측정값 표 내에서 계속 활성 테이블에서 만든 측정값 아래의 빈 셀을 클릭 합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    불완전 한 기간과 이전 기간 사이의 비교 비율을 만들면 됩니다. 수식은 경과 되 고 이전 기간의 동일한 부분과 비교 된 기간의 비율을 계산 해야 합니다. 이 경우 [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 비율을 제공 하며 현재 기간에서 경과한 합니다.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>측정값을 만들려면 InternetDistinctCountSalesOrder FactInternetSales 테이블에  
  
1.  클릭는 **FactInternetSales** 테이블입니다.   
  
2.  클릭는 **SalesOrderNumber** 열 머리글입니다.  
  
3.  도구 모음에서 자동 합계(**∑**) 단추 옆의 아래쪽 화살표를 클릭한 다음 **DistinctCount**를 선택합니다.  
  
    자동 합계 기능은 DistinctCount 표준 집계 수식을 사용하여 선택한 열에 대한 측정값을 자동으로 만듭니다.  
    
       ![as-lesson6-newmeasure2](../tutorial-tabular-1400/media/as-lesson6-newmeasure2.png)
  
4.  측정값 표에서 새 측정값을 클릭 한 다음는 **속성** 창, **측정값 이름**에 측정값 이름을 바꿀 **InternetDistinctCountSalesOrder**합니다. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>FactInternetSales 테이블의 측정값을 추가로 만들려면  
  
1.  자동 합계 기능을 사용하여 다음과 같이 측정값을 만들고 이름을 지정합니다.  

    |열|측정값 이름|자동 합계(∑)|수식|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|합계|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|합계|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|합계|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|합계|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|합계|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|합계|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|합계|=SUM([Freight])|  
  
2.  측정값 표에서 빈 셀을 클릭 하 여 및 수식 입력줄을 사용 하 여,에서 만든 순서 대로 다음과 같은 사용자 지정 측정:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
FactInternetSales 테이블에 대해 만든 측정값 매출, 비용, 이익률 사용자 선택한 필터에 의해 정의 된 항목에 대 한 등의 중요 회계 데이터를 분석 하려면 사용할 수 있습니다.  
  
## <a name="whats-next"></a>다음 단계

[7 단원: 핵심 성과 지표 만들기](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)합니다.  

  
