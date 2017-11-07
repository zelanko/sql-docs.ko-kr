---
title: "7 단원: 측정값 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f486e0094e66ed503b63fb52c4cba88dbcadbb62
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-6-create-measures"></a>6 단원: 측정값 만들기
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 모델에 포함할 측정값을 만듭니다. 이전 단원에서 만든 계산된 열과 마찬가지로 측정값은 DAX 수식을 사용 하 여 만든 계산입니다. 그러나 계산 열과는 달리 측정값은 사용자가 선택한 *필터*를 기반으로 계산됩니다. 피벗 테이블의 행 레이블 필드에 추가된 특정 열이나 슬라이서를 예로 들 수 있습니다. 적용된 측정값에 따라 필터의 각 셀에 대한 값이 계산됩니다. 측정값은 숫자 데이터에 대해 동적 계산을 수행 하는 거의 모든 테이블 형식 모델에 포함 하려는 하는 강력 하 고 유연한 계산입니다. 자세한 내용은 참고 [측정값](../analysis-services/tabular-models/measures-ssas-tabular.md)합니다.  
  
측정값을 만들려면 사용할는 *측정값 표*합니다. 기본적으로 각 테이블에는 빈 측정값 표가 들어 있지만 일반적으로 모든 테이블에 대해 측정값을 만들지는 않습니다. 측정값 표는 모델 디자이너의 데이터 보기에서 테이블 아래에 나타납니다. 테이블의 측정값 표를 숨기거나 표시하려면 **테이블** 메뉴를 클릭한 다음 **측정값 표 표시**를 클릭합니다.  
  
측정값 표에서 빈 셀을 클릭한 다음 수식 입력줄에 DAX 수식을 입력하여 측정값을 만들 수 있습니다. Enter 키를 눌러 수식을 완성하면 셀에 측정값이 표시됩니다. 열을 클릭하고 도구 모음에서 자동 합계(**∑**) 단추를 클릭하여 표준 집계 함수를 이용해 측정값을 만들 수도 있습니다. 자동 합계 기능을 이용해 만든 측정값은 해당 열 바로 아래에 있는 측정값 표 셀에 표시 되지만 이동할 수 있습니다.  
  
이 단원에서는 수식 입력줄에 DAX 수식을 입력하는 방법과 자동 합계 기능을 이용하는 방법을 모두 사용해 측정값을 만듭니다.  
  
이 단원에 소요되는 예상 시간: **30분**  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [5 단원: 계산 열 만들기](../analysis-services/lesson-5-create-calculated-columns.md)합니다.  
  
## <a name="create-measures"></a>측정값 만들기  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>DimDate 테이블에서 DaysCurrentQuarterToDate 측정값을 만들려면  
  
1.  모델 디자이너에서 클릭 된 **DimDate** 테이블입니다.  
  
2.  측정값 표에서 왼쪽 위에 있는 빈 셀을 클릭합니다.  
  
3.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    왼쪽 위 셀에 측정값 이름이 표시, **DaysCurrentQuarterToDate**결과 **92**합니다.
    
      ![로-테이블 형식-6 단원에서는-newmeasure](../analysis-services/media/as-tabular-lesson6-newmeasure.png) 
    
    측정값 수식으로 계산 된 열과 달리 수식 식 옵니다 쉼표 측정값 이름을 입력할 수 있습니다.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>DimDate 테이블에서 DaysInCurrentQuarter 측정값을 만들려면  
  
1.  와 **DimDate** 모델 디자이너의 측정값 표 내에서 계속 활성 테이블에서 방금 만든 측정값 아래의 빈 셀을 클릭 합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    불완전한 기간과 이전 기간 간의 비교 비율을 만들 경우 경과한 기간의 비율을 고려하여 이를 이전 기간의 동일한 비율과 비교하도록 수식을 작성해야 합니다. 이 경우 [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 비율을 제공 하며 현재 기간에서 경과한 합니다.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>측정값을 만들려면 InternetDistinctCountSalesOrder FactInternetSales 테이블에  
  
1.  클릭는 **FactInternetSales** 테이블입니다.   
  
2.  클릭는 **SalesOrderNumber** 열 머리글입니다.  
  
3.  도구 모음에서 자동 합계(**∑**) 단추 옆의 아래쪽 화살표를 클릭한 다음 **DistinctCount**를 선택합니다.  
  
    자동 합계 기능은 DistinctCount 표준 집계 수식을 사용하여 선택한 열에 대한 측정값을 자동으로 만듭니다.  
    
       ![로-테이블 형식-6 단원에서는-newmeasure2](../analysis-services/media/as-tabular-lesson6-newmeasure2.png)
  
4.  측정값 표에서 새 측정값을 클릭 한 다음는 **속성** 창, **측정값 이름**에 측정값 이름을 바꿀 **InternetDistinctCountSalesOrder**합니다. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>FactInternetSales 테이블의 측정값을 추가로 만들려면  
  
1.  자동 합계 기능을 사용하여 다음과 같이 측정값을 만들고 이름을 지정합니다.  
  
    |측정값 이름|열|자동 합계(∑)|수식|  
    |----------------|----------|-----------------|-----------|  
    |InternetOrderLinesCount|SalesOrderLineNumber|개수|=COUNTA([SalesOrderLineNumber])|  
    |InternetTotalUnits|OrderQuantity|합계|=SUM([OrderQuantity])|  
    |InternetTotalDiscountAmount|DiscountAmount|합계|=SUM([DiscountAmount])|  
    |InternetTotalProductCost|TotalProductCost|합계|=SUM([TotalProductCost])|  
    |InternetTotalSales|SalesAmount|합계|=SUM([SalesAmount])|  
    |InternetTotalMargin|Margin|합계|=SUM([Margin])|  
    |InternetTotalTaxAmt|TaxAmt|합계|=SUM([TaxAmt])|  
    |InternetTotalFreight|Freight|합계|=SUM([Freight])|  
  
2.  측정값 표에서 빈 셀을 클릭 하 고 수식 입력줄을 사용 하 여 만들고 순서 대로 다음 측정값 이름을 지정 합니다.  
  
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
다음 단원으로 이동: [7 단원: 핵심 성과 지표 만들기](../analysis-services/lesson-7-create-key-performance-indicators.md)합니다.  

  

