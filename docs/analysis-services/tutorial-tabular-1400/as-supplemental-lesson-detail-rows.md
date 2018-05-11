---
title: 'Analysis Services tutorial 추가 단원: 정보 행 | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 69a962bcb518040c88763b65004a89f5277546c5
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="supplemental-lesson---detail-rows"></a>추가 단원-정보 행

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 추가 단원에서는 DAX 편집기를 사용 하 여 사용자 지정 세부 행 식을 정의 합니다. 세부 정보 행 식 최종 사용자에 게 측정값의 집계 된 결과 대 한 자세한 정보를 제공 하는 측정값에 속성입니다. 
  
이 단원에 소요되는 예상 시간: **10분**  
  
## <a name="prerequisites"></a>필수 구성 요소  

이 추가 단원은 문서는 테이블 형식 모델링 자습서의 일부입니다. 이 추가 단원 태스크를 수행 하기 전에 완료 해야 이전 단원을 모두 완료 된 Adventure Works Internet Sales 샘플 모델 프로젝트 수도 있고 합니다.  
  
## <a name="whats-the-issue"></a>이 문제는 무엇입니까?

세부 정보 행 식을 추가 하기 전에 InternetTotalSales 측정값의 세부 정보에 살펴보겠습니다.

1.  SSDT에서는 클릭는 **모델** 메뉴 > **Excel에서 분석** Excel을 열고 빈 피벗 테이블을 만듭니다.
  
2.  **피벗 테이블 필드**, 추가 **InternetTotalSales** FactInternetSales 테이블에서 측정값 **값**, **y e a r** DimDate 테이블에서 **열**, 및 **EnglishCountryRegionName** 를 **행**합니다. 이제 피벗 테이블 영역 및 연도별 InternetTotalSales 측정값에서 집계 된 결과 제공합니다. 

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. 피벗 테이블의 지역 이름과 1 년에 대 한 집계 값을 두 번 클릭 합니다. 여기에서는 두 번 클릭 한 오스트레일리아 및 2014 년에 대 한 값입니다. 유용 하지 데이터가 아니라 데이터가 포함 된 새 시트를 엽니다.

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
필요한 것 같습니다. InternetTotalSales 측정값의 집계 된 결과에 영향을 주는 데이터의 열과 행을 포함 하는 테이블을 참조 하십시오. 이렇게 하려면 측정값의 속성으로 정보 행 식을 추가할 수 있습니다.

## <a name="add-a-detail-rows-expression"></a>세부 정보 행 식 추가

#### <a name="to-create-a-detail-rows-expression"></a>세부 정보 행 식을 만들려면 
  
1. FactInternetSales 테이블의 측정값 표에서 클릭 된 **InternetTotalSales** 측정값입니다. 

2. **속성** > **세부 행 식**, DAX 편집기를 열려면 편집기 단추를 클릭 합니다.

    ![as-lesson-detail-rows-ellipse](../tutorial-tabular-1400/media/as-lesson-detail-rows-ellipse.png)

3. DAX 편집기에서 다음 식을 입력 합니다.

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    이 식 이름, 열를 지정 하 고 사용자가 피벗 테이블 또는 보고서에는 집계 된 결과 두 번 클릭할 경우 FactInternetSales 테이블과 관련된 테이블에서 측정값 결과가 반환 됩니다.

4. Excel에서 다시 3 단계에서에서 만든 시트 삭제 한 다음 집계 값을 두 번 클릭 합니다. 이 이번에는 측정값에 대해 정의 된 세부 행 식 속성을 새 시트가 열립니다 훨씬 더 유용한 데이터가 포함 된.

    ![as-lesson-detail-rows-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. 모델 다시 배포 합니다.

  
## <a name="see-also"></a>참고 항목  

[SELECTCOLUMNS 함수 (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)  
[추가 단원 - 동적 보안](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[추가 단원-비정형 계층 구조](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
