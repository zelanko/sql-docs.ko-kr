---
title: 'Analysis Services 자습서 단원 5: 계산된 열 만들기 | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d1e2c4df54313ecc66e5e49904bdc40393c410f7
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685560"
---
# <a name="create-calculated-columns"></a>계산 열 만들기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 계산된 열을 추가 하 여 모델에 데이터를 만듭니다. (사용자 지정 열)로 계산 된 열을 만들면 데이터 가져오기를 사용할 때 모델 디자이너 같은 또는 나중에 쿼리 편집기를 사용 하 여 할 여기 있습니다. 자세한 내용은 참조 하세요 [계산 된 열](../tabular-models/ssas-calculated-columns.md)합니다.
  
서로 다른 세 테이블에서 5 개의 새 계산된 열을 만듭니다. 단계는 열을 만들고 이름을 바꾸고, 테이블의 다양 한 위치에 배치 하는 방법은 여러 가지를 보여 주는 각 작업에 대해 약간 다릅니다.  

이 단원에서는 먼저 데이터 분석 식 (DAX)를 사용할 이기도 합니다. DAX는 테이블 형식 모델에 대 한 고도로 사용자 지정 가능한 수식 식을 만들기 위한 특별 한 언어입니다. 이 자습서에서는 DAX를 사용 하 여 계산된 열, 측정값 및 역할 필터를 만듭니다. 자세한 내용은 참조 하세요 [테이블 형식 모델에서 DAX](../tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)합니다. 
  
이 단원에 소요되는 예상 시간: **15 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원을 완료해야 합니다. [4단원: 관계를 만들](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)합니다. 
  
## <a name="create-calculated-columns"></a>계산 열 만들기  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>DimDate 테이블에서 MonthCalendar 계산된 열 만들기  
  
1.  클릭 합니다 **모델** 메뉴 > **모델 뷰** > **데이터 뷰**합니다.  
  
    데이터 뷰에서는 모델 디자이너를 사용하여 계산 열만 만들 수 있습니다.  
  
2.  모델 디자이너에서를 클릭 합니다 **DimDate** 테이블 (탭).  
  
3.  마우스 오른쪽 단추로 클릭 합니다 **CalendarQuarter** 열 머리글을 클릭 한 다음 **열 삽입**합니다.  
  
    **계산 열 1** 이라는 새 열이 **Calendar Quarter** 열의 왼쪽에 삽입됩니다.  
  
4.  테이블 위의 수식 입력줄에 다음 DAX 수식을 입력 합니다. 자동 완성 기능을 사용하면 정규화된 열 및 테이블 이름을 입력하고 사용 가능한 함수를 나열할 수 있습니다.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    계산 열의 모든 행에 값이 채워집니다. 테이블 아래로 스크롤하면 하는 경우에 행이 열에서 각 행의 데이터를 기반으로 다른 값을 가질 수 있습니다 하는 것이 표시 됩니다.    
  
5.  이 열의 이름을 바꿀 **MonthCalendar**합니다. 

    ![as-lesson5-newcolumn](../tutorial-tabular-1400/media/as-lesson5-newcolumn.png) 
  
MonthCalendar 계산 열은 월에 대 한 정렬 가능한 이름을 제공 합니다.  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>DimDate 테이블에서 DayOfWeek 계산된 열 만들기  
  
1.  사용 하 여는 **DimDate** 테이블 아직 활성 상태인 경우 클릭 합니다 **열** 메뉴를 클릭 한 다음 **열 추가**합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    수식 작성을 마쳤으면 enter 키를 누릅니다. 새 열이 테이블의 맨 오른쪽에 추가됩니다.  
  
3.  열 이름 바꾸기 **DayOfWeek**합니다.  
  
4.  열 머리글을 클릭 한 다음 사이는 열을 끌어 합니다 **EnglishDayNameOfWeek** 열 및 **DayNumberOfMonth** 열입니다.  
  
    > [!TIP]  
    > 테이블에서 열을 이동하여 쉽게 탐색할 수 있습니다.  
  
DayOfWeek 계산 열은 요일에 대 한 정렬 가능한 이름을 제공 합니다.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>DimProduct 테이블의 ProductSubcategoryName 계산 된 열 만들기  
  
  
1.  에 **DimProduct** 테이블, 테이블의 맨 오른쪽으로 스크롤합니다. 맨 오른쪽 열 이름은 **열 추가** (기울임꼴)입니다. 열 제목을 클릭합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  열 이름 바꾸기 **ProductSubcategoryName**합니다.  
  
ProductSubcategoryName 계산 된 열은 DimProductSubcategory 테이블에서 EnglishProductSubcategoryName 열의 데이터를에서 포함 하는 DimProduct 테이블의 계층 구조를 만들 사용 됩니다. 계층은 둘 이상의 테이블에 걸쳐 있을 수 없습니다. 단원 9에서 나중에 계층을 만듭니다.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>DimProduct 테이블의 ProductCategoryName 계산된 열 만들기  
  
1.  사용 하 여는 **DimProduct** 테이블 아직 활성 상태인 경우 클릭 합니다 **열** 메뉴를 클릭 한 다음 **열 추가**합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  열 이름 바꾸기 **ProductCategoryName**합니다.  
  
ProductCategoryName 계산 된 열은 DimProductCategory 테이블에서 EnglishProductCategoryName 열의 데이터를에서 포함 하는 DimProduct 테이블의 계층 구조를 만들 사용 됩니다. 계층은 둘 이상의 테이블에 걸쳐 있을 수 없습니다.  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>FactInternetSales 테이블에서 Margin 계산된 열 만들기  
  
1.  모델 디자이너에서 선택 합니다 **FactInternetSales** 테이블입니다.  
  
2.  사이 새 계산된 열 만들기 합니다 **SalesAmount** 열 및 **TaxAmt** 열입니다.  
  
3.  수식 입력줄에 다음 수식을 입력합니다.  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  열 이름을 **Margin**으로 바꿉니다.  
 
      ![as-lesson5-newmargin](../tutorial-tabular-1400/media/as-lesson5-newmargin.png)
      
    Margin 계산된 열은 각 판매의 이익률을 분석에 사용 됩니다.  
  
## <a name="whats-next"></a>다음 단계

[6단원: 측정값 만들기](../tutorial-tabular-1400/as-lesson-6-create-measures.md)합니다.
  
  
  
