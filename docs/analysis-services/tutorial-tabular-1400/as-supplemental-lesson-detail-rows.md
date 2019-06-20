---
title: 'Analysis Services 자습서 추가 단원: 행에 자세히 설명 | Microsoft Docs'
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
ms.openlocfilehash: bad45d18c351e838ec944b1ae67e3ce88c7e1d20
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263312"
---
# <a name="supplemental-lesson---detail-rows"></a>추가 단원 - 세부 정보 행

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 추가 단원에서는 DAX 편집기를 사용 하 여 사용자 지정 세부 정보 행 식을 정의 합니다. 세부 정보 행 식을 측정값의 집계 된 결과 대 한 자세한 내용은 최종 사용자에 게 제공 측정값을 속성입니다. 
  
예상이 단원을 완료 시간: **10 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  

이 추가 단원 문서는 테이블 형식 모델링 자습서의 일부입니다. 이 추가 단원의 작업을 수행 하기 전에 완료 해야 이전의 단원을 모두 완료 된 Adventure Works Internet Sales 샘플 모델 프로젝트가 또는 합니다.  
  
## <a name="whats-the-issue"></a>문제가 무엇 인가요?

세부 정보 행 식을 추가 하기 전에 InternetTotalSales 측정값의 세부 정보에 살펴보겠습니다.

1.  SSDT에서를 클릭 합니다 **모델** 메뉴 > **Excel에서 분석** Excel을 열고 빈 피벗 테이블을 만듭니다.
  
2.  **피벗 테이블 필드**를 추가 합니다 **InternetTotalSales** FactInternetSales 테이블 측정값 **값**를 **CalendarYear** 에서 DimDate 테이블 **열**, 및 **EnglishCountryRegionName** 하 **행**합니다. 이제 피벗 테이블은 InternetTotalSales 측정값에서 지역 및 연도별로 집계 된 결과를 제공합니다. 

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. 피벗 테이블에서 연도 및 지역 이름에 대 한 집계 된 값을 두 번 클릭 합니다. 다음 두 번 클릭 했습니다 2014 년 오스트레일리아에 대 한 값입니다. 새 시트가 열리지만 유용한 데이터가 아닙니다 데이터가 포함 된 합니다.

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
원하는 같습니다.은 InternetTotalSales 측정값의 집계 결과에 영향을 주는 데이터의 열과 행을 포함 하는 테이블을 볼 수 있습니다. 이렇게 하려면 세부 정보 행 식을 측정값의 속성으로 추가할 수 있습니다.

## <a name="add-a-detail-rows-expression"></a>세부 정보 행 식을 추가 합니다.

#### <a name="to-create-a-detail-rows-expression"></a>세부 정보 행 식을 만들려면 
  
1. FactInternetSales 테이블의 측정값 표를 클릭 합니다 **InternetTotalSales** 측정값입니다. 

2. **속성** > **세부 정보 행 식을**, DAX 편집기를 열려면 편집기 단추를 클릭 합니다.

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

    이 식 이름, 열을 지정 하 고 사용자는 피벗 테이블 또는 보고서에서 집계 된 결과 두 번 클릭할 때 관련된 테이블에서 FactInternetSales 테이블 측정값 결과가 반환 됩니다.

4. 다시 Excel에서에서 3 단계에서에서 만든 시트를 삭제 한 후 집계 된 값을 두 번 클릭 합니다. 이 이번에는 측정값에 대해 정의 된 세부 정보 행 식 속성을 사용 하 여 새 시트가 열리지만 훨씬 유용한 데이터가 포함 된 합니다.

    ![as-lesson-detail-rows-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. 모델을 다시 배포 합니다.

  
## <a name="see-also"></a>참고자료  

[SELECTCOLUMNS 함수 (DAX)](/dax/selectcolumns-function-dax)  
[추가 단원 - 동적 보안](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[추가 단원-비정형 계층 구조](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
