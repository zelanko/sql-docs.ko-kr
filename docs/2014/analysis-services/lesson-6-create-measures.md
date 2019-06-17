---
title: '7단원: 측정값 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef207028ab1b4f6bc084f3f4e515ae37630b771d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078426"
---
# <a name="lesson-7-create-measures"></a>7단원: 측정값 만들기
  이 단원에서는 모델에 포함할 측정값을 만듭니다. 이전 단원에서 만든 계산 열과 마찬가지로 측정값은 기본적으로 DAX 수식을 사용해 만든 계산입니다. 그러나 계산 열과는 달리 측정값은 사용자가 선택한 *필터*를 기반으로 계산됩니다. 피벗 테이블의 행 레이블 필드에 추가된 특정 열이나 슬라이서를 예로 들 수 있습니다.   적용된 측정값에 따라 필터의 각 셀에 대한 값이 계산됩니다. 측정값은 숫자 데이터에 대해 동적 계산을 수행하기 위해 대부분의 테이블 형식 모델에 포함할 수 있는 강력하고 유연한 계산입니다. 자세한 내용은 [측정값&#40;SSAS 테이블 형식&#41;](tabular-models/measures-ssas-tabular.md)을 참조하세요.  
  
 측정값을 만들려면 측정값 표를 사용합니다. 기본적으로 각 테이블에는 빈 측정값 표가 들어 있지만 일반적으로 모든 테이블에 대해 측정값을 만들지는 않습니다. 측정값 표는 모델 디자이너의 데이터 보기에서 테이블 아래에 나타납니다. 테이블의 측정값 표를 숨기거나 표시하려면 **테이블** 메뉴를 클릭한 다음 **측정값 표 표시**를 클릭합니다.  
  
 측정값 표에서 빈 셀을 클릭한 다음 수식 입력줄에 DAX 수식을 입력하여 측정값을 만들 수 있습니다. Enter 키를 눌러 수식을 완성하면 셀에 측정값이 표시됩니다. 열을 클릭하고 도구 모음에서 자동 합계(**∑**) 단추를 클릭하여 표준 집계 함수를 이용해 측정값을 만들 수도 있습니다. 자동 합계 기능을 이용해 만든 측정값은 해당 열 바로 아래에 있는 측정값 표 셀에 표시되지만 필요하면 이동할 수 있습니다.  
  
 이 단원에서는 수식 입력줄에 DAX 수식을 입력하는 방법과 자동 합계 기능을 이용하는 방법을 모두 사용해 측정값을 만듭니다.  
  
 예상이 단원을 완료 시간: **30 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 이전 단원을 완료 해야 합니다. [6단원: 계산된 열 만들기](lesson-5-create-calculated-columns.md)합니다.  
  
## <a name="create-measures"></a>측정값 만들기  
  
#### <a name="to-create-a-days-current-quarter-to-date-measure-in-the-date-table"></a>날짜 테이블에서 Days Current Quarter to Date 측정값을 만들려면  
  
1.  모델 디자이너에서 **Date** 테이블을 클릭합니다.  
  
2.  테이블 아래에 빈 측정값 표가 표시되지 않으면 **테이블** 메뉴를 클릭한 다음 **측정값 표 표시**를 클릭합니다.  
  
3.  측정값 표에서 왼쪽 위에 있는 빈 셀을 클릭합니다.  
  
4.  테이블 위의 수식 입력줄에 다음 수식을 입력합니다.  
  
     `=COUNTROWS( DATESQTD( 'Date'[Date]))`  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
     이제 왼쪽 위 셀에 **Measure 1**이라는 측정값 이름과 **30**이라는 결과 값이 표시됩니다. 측정값 이름은 수식 입력줄의 수식 앞에도 표시됩니다.  
  
5.  강조 표시 이름, 수식 입력줄에서 측정값 이름을 바꾸려면 **Measure 1**를 입력 한 다음 `Days Current Quarter to Date`, 한 다음 ENTER를 누릅니다.  
  
    > [!TIP]  
    >  수식 입력줄에서 수식을 입력할 때 먼저 측정값 이름을 입력한 다음 콜론(:), 공백, 수식을 차례로 입력해도 됩니다. 이 방법을 사용하면 측정값 이름을 바꿀 필요가 없습니다.  
  
#### <a name="to-create-a-days-in-current-quarter-measure-in-the-date-table"></a>날짜 테이블에서 Days in Current Quarter 측정값을 만들려면  
  
1.  모델 디자이너에서 **Date** 테이블을 활성화한 상태로 측정값 표에서 방금 만든 측정값 아래의 빈 셀을 클릭합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
  
     `Days in Current Quarter :=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))`  
  
     이 수식에서 측정값 이름을 먼저 포함한 후 콜론(:)을 입력합니다.  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
 불완전한 기간과 이전 기간 간의 비교 비율을 만들 경우 경과한 기간의 비율을 고려하여 이를 이전 기간의 동일한 비율과 비교하도록 수식을 작성해야 합니다. 이 경우 [Days Current Quarter to Date]/[Days in Current Quarter]와 같이 수식을 작성하면 현재 기간에서 경과한 비율을 구할 수 있습니다.  
  
#### <a name="to-create-an-internet-distinct-count-sales-order-measure-in-the-internet-sales-table"></a>인터넷 판매 테이블에서 Internet Distinct Count Sales Order 측정값을 만들려면  
  
1.  모델 디자이너에서 **Internet Sales** 테이블(탭)을 클릭합니다.  
  
     측정값 표가 표시되지 않으면 **Internet Sales** 테이블(탭)을 마우스 오른쪽 단추로 클릭한 다음 **측정값 표 표시**를 클릭합니다.  
  
2.  **판매 주문 번호** 열 제목을 클릭합니다.  
  
3.  도구 모음에서 자동 합계(**∑**) 단추 옆의 아래쪽 화살표를 클릭한 다음 **DistinctCount**를 선택합니다.  
  
     자동 합계 기능은 DistinctCount 표준 집계 수식을 사용하여 선택한 열에 대한 측정값을 자동으로 만듭니다.  
  
     측정값 표에서 해당 열 아래에 있는 맨 위 셀에 **Distinct Count Sales Order Number**라는 측정값 이름이 표시됩니다. 자동 합계 기능을 이용해 만든 측정값은 측정값 표에서 관련 열 아래에 있는 맨 위 셀에 자동으로 배치됩니다.  
  
4.  측정값 표에서 새 측정값을 클릭한 다음 **속성** 창의 **측정값 이름**에서 측정값 이름을 **Internet Distinct Count Sales Order**로 바꿉니다.  
  
#### <a name="to-create-additional-measures-in-the-internet-sales-table"></a>인터넷 판매 테이블에서 측정값을 추가로 만들려면  
  
1.  자동 합계 기능을 사용하여 다음과 같이 측정값을 만들고 이름을 지정합니다.  
  
    |측정값 이름|Column|자동 합계(∑)|수식|  
    |------------------|------------|-------------------|-------------|  
    |Internet Order Lines Count|Sales Order Line Number|개수|=COUNT([Sales Order Line Number])|  
    |Internet Total Units|Order Quantity|합계|=SUM([Order Quantity])|  
    |Internet Total Discount Amount|Discount Amount|합계|=SUM([Discount Amount])|  
    |Internet Total Product Cost|Total Product Cost|합계|=SUM([Total Product Cost])|  
    |Internet Total Sales|Sales Amount|합계|=SUM([Sales Amount])|  
    |Internet Total Margin|Margin|합계|=SUM([Margin])|  
    |Internet Total Tax Amt|Tax Amt|합계|=SUM([Tax Amt])|  
    |Internet Total Freight|Freight|합계|=SUM([Freight])|  
  
2.  측정값 표에서 빈 셀을 클릭하고 수식 입력줄을 사용하여 다음과 같이 측정값을 만들고 이름을 지정합니다.  
  
    > [!IMPORTANT]  
    >  다음 측정값에서 뒤에 나오는 측정값의 수식은 이전 측정값을 참조하므로 순서대로 측정값을 만들어야 합니다.  
  
    |측정값 이름|수식|  
    |------------------|-------------|  
    |Internet Previous Quarter Margin|=CALCULATE([Internet Total Margin],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Margin|=TOTALQTD([Internet Total Margin],'Date'[Date])|  
    |Internet Previous Quarter Margin Proportion to QTD|=[Internet Previous Quarter Margin]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
    |Internet Previous Quarter Sales|=CALCULATE([Internet Total Sales],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Sales|=TOTALQTD([Internet Total Sales],'Date'[Date])|  
    |Internet Previous Quarter Sales Proportion to QTD|=[Internet Previous Quarter Sales]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
  
 인터넷 판매 테이블에서 만든 측정값을 사용하여 사용자가 선택한 필터로 필터링된 항목의 매출, 비용, 이익률 등의 중요 회계 데이터를 분석할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
 이 자습서를 계속 하려면 다음 단원으로 이동 합니다. [8단원: 핵심 성과 지표 만들기](lesson-7-create-key-performance-indicators.md)합니다.  
  
  
