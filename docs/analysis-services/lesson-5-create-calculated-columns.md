---
title: '6 단원: 계산된 열 만들기 | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c3b86f84567e85fb604883e7cd7f8de83feb252e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-5-create-calculated-columns"></a>5단원: 계산 열 만들기
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 계산 열을 추가하여 모델에 새 데이터를 만듭니다. 계산 열은 모델에 이미 있는 데이터를 기반으로 합니다. 자세한 내용은 참고 [계산 열](../analysis-services/tabular-models/ssas-calculated-columns.md)합니다.  
  
서로 다른 세 테이블에 다섯 개의 새 계산 열을 만듭니다. 태스크마다 단계가 조금씩 다릅니다. 이는 새 열을 만들고 열의 이름을 바꾸고 테이블의 다양한 위치에 열을 배치하는 데 여러 가지 방법이 있음을 보여 주기 위한 것입니다.  
  
이 단원에 소요되는 예상 시간: **15분**  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [4 단원: 관계 만들기](../analysis-services/lesson-4-create-relationships.md)합니다. 
  
## <a name="create-calculated-columns"></a>계산 열 만들기  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>DimDate 테이블에서 MonthCalendar 계산된 열 만들기  
  
1.  클릭는 **모델** 메뉴 > **모델 뷰** > **데이터 뷰**합니다.  
  
    데이터 뷰에서는 모델 디자이너를 사용하여 계산 열만 만들 수 있습니다.  
  
2.  모델 디자이너에서 클릭 된 **DimDate** 테이블 (탭).  
  
3.  마우스 오른쪽 단추로 클릭는 **CalendarQuarter** 열 머리글을 클릭 한 다음 **열 삽입**합니다.  
  
    **계산 열 1** 이라는 새 열이 **Calendar Quarter** 열의 왼쪽에 삽입됩니다.  
  
4.  테이블 위의 수식 입력줄에 다음 수식을 입력합니다. 자동 완성 기능을 사용하면 정규화된 열 및 테이블 이름을 입력하고 사용 가능한 함수를 나열할 수 있습니다.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    계산 열의 모든 행에 값이 채워집니다. 테이블의 아래쪽으로 스크롤하면 각 행의 데이터에 따라 이 열에서 행마다 서로 다른 값을 포함할 수 있음을 알 수 있습니다.    
  
5.  이 열을 이름 바꾸기 **MonthCalendar**합니다. 

    ![로-테이블 형식-lesson5-newcolumn](../analysis-services/media/as-tabular-lesson5-newcolumn.png) 
  
MonthCalendar의 월에 대 한 정렬 가능한 이름을 제공 하는 열을 계산 합니다.  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>DimDate 테이블의 DayOfWeek 계산된 열 만들기  
  
1.  와 **DimDate** 여전히 활성 상태 테이블을 클릭는 **열** 메뉴를 차례로 클릭 **열 추가**합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    수식 작성을 마쳤으면 ENTER 키를 누릅니다. 새 열이 테이블의 맨 오른쪽에 추가됩니다.  
  
3.  열 이름 바꾸기 **DayOfWeek**합니다.  
  
4.  열 머리글을 클릭 하 고 다음 사이 열을 끌어는 **EnglishDayNameOfWeek** 열 및 **DayNumberOfMonth** 열입니다.  
  
    > [!TIP]  
    > 테이블에서 열을 이동하여 쉽게 탐색할 수 있습니다.  
  
DayOfWeek 요일에 대 한 정렬 가능한 이름을 제공 하는 열을 계산 합니다.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>DimProduct 테이블의 ProductSubcategoryName 계산된 열 만들기  
  
  
1.  에 **DimProduct** 테이블, 테이블의 맨 오른쪽으로 스크롤합니다. 맨 오른쪽 열 이름은 **열 추가** (기울임꼴)입니다. 열 제목을 클릭합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  열 이름 바꾸기 **ProductSubcategoryName**합니다.  
  
ProductSubcategoryName 계산 된 열 DimProductSubcategory 테이블에는 s u b c 열에서 데이터를 포함 하는 DimProduct 테이블의 계층 구조를 만들 사용 됩니다. 계층은 둘 이상의 테이블에 걸쳐 있을 수 없습니다. 9 단원에서 나중에 계층 만들어집니다.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>DimProduct 테이블의 ProductCategoryName 계산된 열 만들기  
  
1.  와 **DimProduct** 테이블 아직 활성 상태인 경우 클릭은 **열** 메뉴를 차례로 클릭 **열 추가**합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  열 이름 바꾸기 **ProductCategoryName**합니다.  
  
ProductCategoryName 계산 된 열 DimProductCategory 테이블에 EnglishProductCategoryName 열에서 데이터를 포함 하는 DimProduct 테이블의 계층 구조를 만들 사용 됩니다. 계층은 둘 이상의 테이블에 걸쳐 있을 수 없습니다.  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>FactInternetSales 테이블에서 Margin 계산된 열 만들기  
  
1.  모델 디자이너에서 선택 된 **FactInternetSales** 테이블입니다.  
  
2.  새 열을 추가합니다.  
  
3.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  열 이름을 **Margin**으로 바꿉니다.  
  
5.  열 사이로 끕니다는 **SalesAmount** 열 및 **TaxAmt** 열입니다. 
 
      ![로-테이블 형식-lesson5-newmargin](../analysis-services/media/as-tabular-lesson5-newmargin.png)
      
    Margin 계산된 열은 각 판매의 매출 이익률을 분석에 사용 됩니다.  
  
## <a name="whats-next"></a>다음 단계
다음 단원으로 이동: [6 단원: 측정값 만들기](../analysis-services/lesson-6-create-measures.md)합니다.
  
  
  
