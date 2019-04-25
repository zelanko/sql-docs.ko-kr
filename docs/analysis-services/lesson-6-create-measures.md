---
title: '6단원: 측정값 만들기 | Microsoft Docs'
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 05855af1bf6809c6977b22bfdb3915e4e6dbbe03
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469819"
---
# <a name="lesson-6-create-measures"></a>6단원: 측정값 만들기
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 모델에 포함할 측정값을 만듭니다. 이전 단원에서 만든 계산된 열과 마찬가지로 측정값은 DAX 수식을 사용 하 여 만든 계산입니다. 그러나 계산 열과는 달리 측정값은 사용자가 선택한 *필터*를 기반으로 계산됩니다. 피벗 테이블의 행 레이블 필드에 추가된 특정 열이나 슬라이서를 예로 들 수 있습니다. 적용된 측정값에 따라 필터의 각 셀에 대한 값이 계산됩니다. 측정값은 수치 데이터에 동적인 계산을 수행 하기 위해 거의 모든 테이블 형식 모델에 포함 하려는 강력 하 고 유연한 계산입니다. 자세한 내용은 참조 하세요 [측정값](../analysis-services/tabular-models/measures-ssas-tabular.md)합니다.  
  
측정값을 만들려면 사용 합니다 *측정값 표*합니다. 기본적으로 각 테이블에는 빈 측정값 표가 들어 있지만 일반적으로 모든 테이블에 대해 측정값을 만들지는 않습니다. 측정값 표는 모델 디자이너의 데이터 보기에서 테이블 아래에 나타납니다. 테이블의 측정값 표를 숨기거나 표시하려면 **테이블** 메뉴를 클릭한 다음 **측정값 표 표시**를 클릭합니다.  
  
측정값 표에서 빈 셀을 클릭한 다음 수식 입력줄에 DAX 수식을 입력하여 측정값을 만들 수 있습니다. Enter 키를 눌러 수식을 완성하면 셀에 측정값이 표시됩니다. 열을 클릭하고 도구 모음에서 자동 합계(**∑**) 단추를 클릭하여 표준 집계 함수를 이용해 측정값을 만들 수도 있습니다. 자동 합계 기능을 이용해 만든 측정값 열 바로 아래에 있는 측정값 표 셀에 나타나지만 이동할 수 있습니다.  
  
이 단원에서는 수식 입력줄에 DAX 수식을 입력하는 방법과 자동 합계 기능을 이용하는 방법을 모두 사용해 측정값을 만듭니다.  
  
예상이 단원을 완료 시간: **30 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 이전 단원을 완료 해야 합니다. [5단원: 계산된 열 만들기](../analysis-services/lesson-5-create-calculated-columns.md)합니다.  
  
## <a name="create-measures"></a>측정값 만들기  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>DimDate 테이블에 DaysCurrentQuarterToDate 측정값을 만들려면  
  
1.  모델 디자이너에서를 클릭 합니다 **DimDate** 테이블입니다.  
  
2.  측정값 표에서 왼쪽 위에 있는 빈 셀을 클릭합니다.  
  
3.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    왼쪽 위 셀이 이제 라는 측정값 이름이 포함 되어 있습니다 **DaysCurrentQuarterToDate**결과 차례로 **92**합니다.
    
      ![as-tabular-lesson6-newmeasure](../analysis-services/media/as-tabular-lesson6-newmeasure.png) 
    
    측정값 수식을 사용 하 여 계산 된 열을 달리 측정값 이름, 쉼표, 수식 순서로 입력할 수 있습니다.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>DimDate 테이블에 DaysInCurrentQuarter 측정값을 만들려면  
  
1.  사용 하 여 합니다 **DimDate** 테이블이 측정값 표의 모델 디자이너에서 활성 상태인, 방금 만든 측정값 아래의 빈 셀을 클릭 합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    불완전한 기간과 이전 기간 간의 비교 비율을 만들 경우 경과한 기간의 비율을 고려하여 이를 이전 기간의 동일한 비율과 비교하도록 수식을 작성해야 합니다. 이 경우 [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 제공 비율 현재 기간에서 경과한 합니다.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>FactInternetSales 테이블에서 InternetDistinctCountSalesOrder 측정값을 만들려면  
  
1.  클릭 합니다 **FactInternetSales** 테이블입니다.   
  
2.  클릭 합니다 **SalesOrderNumber** 열 머리글입니다.  
  
3.  도구 모음에서 자동 합계(**∑**) 단추 옆의 아래쪽 화살표를 클릭한 다음 **DistinctCount**를 선택합니다.  
  
    자동 합계 기능은 DistinctCount 표준 집계 수식을 사용하여 선택한 열에 대한 측정값을 자동으로 만듭니다.  
    
       ![as-tabular-lesson6-newmeasure2](../analysis-services/media/as-tabular-lesson6-newmeasure2.png)
  
4.  측정값 표에서 새 측정값을 클릭 한 다음 합니다 **속성** 창에서 **측정값 이름**, 측정값 이름 바꾸기 **InternetDistinctCountSalesOrder**합니다. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>FactInternetSales 테이블에서 측정값을 추가로 만들려면  
  
1.  자동 합계 기능을 사용하여 다음과 같이 측정값을 만들고 이름을 지정합니다.  
  
    |측정값 이름|Column|자동 합계(∑)|수식|  
    |----------------|----------|-----------------|-----------|  
    |InternetOrderLinesCount|SalesOrderLineNumber|개수|=COUNTA([SalesOrderLineNumber])|  
    |InternetTotalUnits|OrderQuantity|합계|=SUM([OrderQuantity])|  
    |InternetTotalDiscountAmount|DiscountAmount|합계|=SUM([DiscountAmount])|  
    |InternetTotalProductCost|TotalProductCost|합계|=SUM([TotalProductCost])|  
    |InternetTotalSales|SalesAmount|합계|=SUM([SalesAmount])|  
    |InternetTotalMargin|Margin|합계|=SUM([Margin])|  
    |InternetTotalTaxAmt|TaxAmt|합계|=SUM([TaxAmt])|  
    |InternetTotalFreight|Freight|합계|=SUM([Freight])|  
  
2.  측정값 표에서 빈 셀을 클릭 하 고 수식 입력줄을 사용 하 여 만들고 다음 측정값을 순서 대로 이름을 지정 합니다.  
  
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
  
FactInternetSales 테이블에 대해 만든 측정값은 판매와 비용, 이익률은 사용자가 선택한 필터로 정의 된 항목에 대 한 중요 한 재무 데이터를 분석 하려면 사용할 수 있습니다.  
  
## <a name="whats-next"></a>다음 단계
다음 단원으로 이동 합니다. [7단원: 핵심 성과 지표 만들기](../analysis-services/lesson-7-create-key-performance-indicators.md)합니다.  

  
