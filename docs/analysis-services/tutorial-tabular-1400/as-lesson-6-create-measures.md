---
title: 'Analysis Services 자습서 단원 6: 측정값 만들기 | Microsoft Docs'
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9b466a703dd04a53c6ebf7c6fac624476abcc52
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43093966"
---
# <a name="create-measures"></a>측정값 만들기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 모델에 포함할 측정값을 만들 수 있습니다. 만든 계산된 열과 마찬가지로 측정값은 DAX 수식을 사용 하 여 만든 계산입니다. 그러나 계산된 열과 달리 측정값은 평가 선택한 사용자를 기반으로 *필터*합니다. 예를 들어,는 특정 열 이나 슬라이서 피벗 테이블에서 행 레이블 필드에 추가 합니다. 적용된 측정값에 따라 필터의 각 셀에 대한 값이 계산됩니다. 측정값은 수치 데이터에 동적인 계산을 수행 하기 위해 거의 모든 테이블 형식 모델에 포함 하려는 강력 하 고 유연한 계산입니다. 자세한 내용은 참조 하세요 [측정값](../tabular-models/measures-ssas-tabular.md)합니다.
  
측정값을 만들려면 사용 합니다 *측정값 표*합니다. 기본적으로 각 테이블에는 빈 측정값 표가 있습니다. 그러나 일반적으로 만들지 모든 테이블에 대 한 측정값입니다. 측정값 표는 모델 디자이너의 데이터 보기에서 테이블 아래에 나타납니다. 테이블의 측정값 표를 숨기거나 표시하려면 **테이블** 메뉴를 클릭한 다음 **측정값 표 표시**를 클릭합니다.  
  
측정값 표에서 빈 셀을 클릭 하 고 다음 수식 입력줄에 DAX 수식을 입력 하 여 측정값을 만들 수 있습니다. 측정값 수식을 완성 하려면 enter 키를 눌러 다음 셀에 나타납니다. 열을 클릭 하 고 자동 합계 단추를 클릭 하 여 표준 집계 함수를 사용 하 여 측정값을 만들 수도 있습니다 (**∑**) 도구 모음에서 합니다. 자동 합계 기능을 이용해 만든 측정값 열 바로 아래에 있는 측정값 표 셀에 나타나지만 이동할 수 있습니다.  
  
이 단원에서는 입력 하 여 둘 다 DAX 수식을 수식 입력줄 및 자동 합계 기능을 사용 하 여 측정값을 만듭니다.  
  
이 단원에 소요되는 예상 시간: **30분**  
  
## <a name="prerequisites"></a>필수 구성 요소  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [5 단원: 계산된 열 만들기](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)합니다.  
  
## <a name="create-measures"></a>측정값 만들기  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>DimDate 테이블에 DaysCurrentQuarterToDate 측정값을 만들려면  
  
1.  모델 디자이너에서를 클릭 합니다 **DimDate** 테이블입니다.  
  
2.  측정값 표에서 왼쪽 위에 있는 빈 셀을 클릭합니다.  
  
3.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    왼쪽 위 셀이 이제 라는 측정값 이름이 포함 되어 있습니다 **DaysCurrentQuarterToDate**결과 차례로 **92**합니다. 결과 아니므로 관련이 시점에서 사용자 필터가 적용 되었습니다.
    
      ![as-lesson6-newmeasure](../tutorial-tabular-1400/media/as-lesson6-newmeasure.png) 
    
    측정값 수식을 사용 하 여 계산된 열과 달리 측정값 이름, 콜론, 수식 순서로 입력할 수 있습니다.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>DimDate 테이블에 DaysInCurrentQuarter 측정값을 만들려면  
  
1.  사용 하 여 합니다 **DimDate** 테이블이 측정값 표의 모델 디자이너에서 활성 상태인 사용자가 만든 측정값 아래의 빈 셀을 클릭 합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    불완전 한 기간과 이전 기간 사이의 비교 비율을 만들 때 수식은 경과 되 고 이전 기간의 동일한 부분과 비교 된 기간의 비율을 계산 해야 합니다. 이 경우 [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 제공 비율 현재 기간에서 경과한 합니다.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>FactInternetSales 테이블에서 InternetDistinctCountSalesOrder 측정값을 만들려면  
  
1.  클릭 합니다 **FactInternetSales** 테이블입니다.   
  
2.  클릭 합니다 **SalesOrderNumber** 열 머리글입니다.  
  
3.  도구 모음에서 자동 합계(**∑**) 단추 옆의 아래쪽 화살표를 클릭한 다음 **DistinctCount**를 선택합니다.  
  
    자동 합계 기능은 DistinctCount 표준 집계 수식을 사용하여 선택한 열에 대한 측정값을 자동으로 만듭니다.  
    
       ![as-lesson6-newmeasure2](../tutorial-tabular-1400/media/as-lesson6-newmeasure2.png)
  
4.  측정값 표에서 새 측정값을 클릭 한 다음 합니다 **속성** 창에서 **측정값 이름**, 측정값 이름 바꾸기 **InternetDistinctCountSalesOrder**합니다. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>FactInternetSales 테이블에서 측정값을 추가로 만들려면  
  
1.  자동 합계 기능을 사용하여 다음과 같이 측정값을 만들고 이름을 지정합니다.  

    |Column|측정값 이름|자동 합계(∑)|수식|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|개수|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|합계|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|합계|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|합계|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|합계|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|합계|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|합계|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|합계|=SUM([Freight])|  
  
2.  측정값 표에서 빈 셀을 클릭 하 고 수식 입력줄을 사용 하 여를 만들려면 다음 사용자 지정 측정값을 순서 대로:  
  
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

[7 단원: 핵심 성과 지표 만들기](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)합니다.  

  
