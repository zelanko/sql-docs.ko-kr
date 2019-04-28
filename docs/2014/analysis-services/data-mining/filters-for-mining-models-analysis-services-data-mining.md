---
title: 마이닝 모델에 대 한 필터 (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- filter syntax [data mining]
- models [Analysis Services], filtering
- filters [data mining]
- filtering data [Analysis Services]
ms.assetid: 0f29c19c-4be3-4bc7-ab60-f4130a10d59c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 213768938a4fb9497fcbebad15f1dc4b84e1dba9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722425"
---
# <a name="filters-for-mining-models-analysis-services---data-mining"></a>마이닝 모델에 대한 필터(Analysis Services - 데이터 마이닝)
  데이터 기반 모델 필터링을 사용하면 마이닝 구조에서 데이터의 하위 집합을 사용하는 마이닝 모델을 만들 수 있습니다. 포괄적인 데이터 원본 뷰를 기반으로 단일 마이닝 구조를 만들 수 있으므로 필터링을 사용하면 마이닝 구조 및 데이터 원본을 유연하게 디자인할 수 있습니다. 그런 다음 데이터의 각 하위 집합에 대해 서로 다른 구조 및 관련 모델을 작성하는 대신 다양한 모델의 학습 및 테스트에 해당 데이터의 일부만 사용하기 위한 필터를 만들 수 있습니다.  
  
 예를 들어 Customers 테이블 및 관련 테이블에 대한 데이터 원본 뷰를 정의합니다. 그런 다음 필요한 모든 필드를 포함하는 단일 마이닝 구조를 정의합니다. 마지막으로 Region과 같은 특정 고객 특성으로 필터링되는 모델을 만듭니다. 그러면 해당 모델의 복사본을 쉽게 만들고, 필터 조건만 변경하여 다른 지역을 기반으로 하는 새 모델을 생성할 수 있습니다.  
  
 이 기능이 유용할 수 있는 일부 실제 시나리오는 다음과 같습니다.  
  
-   성별, 지역 등과 같은 불연속 값에 대한 별도의 모델 만들기. 예를 들어 모든 고객에 대한 단일 데이터 원본에서 판매 데이터를 가져온 경우에도 의류점에서는 고객 인구 통계를 사용하여 성별에 따른 별도의 모델을 작성할 수 있습니다.  
  
-   20-30세, 20-40세, 20-25세 연령과 같이 동일한 데이터에 대한 여러 그룹화를 만든 다음 테스트하여 모델 시험  
  
-   고객이 특정 항목을 두 개 이상 구매한 경우에만 사례가 모델에 포함되도록 요구하는 경우에서와 같이 중첩 테이블 내용에 복잡한 필터 지정  
  
 이 섹션에서는 마이닝 모델에 대해 필터를 작성하고 사용하며 관리하는 방법에 대해 설명합니다.  
  
## <a name="creating-model-filters"></a>모델 필터 만들기  
 다음과 같은 방법으로 필터를 만들고 적용할 수 있습니다.  
  
-   데이터 마이닝 디자이너의 **마이닝 모델** 탭을 사용하여 필터 편집기 대화 상자를 통해 조건 작성  
  
-   필터 식에 직접 입력 된 `Filter` 마이닝 모델의 속성입니다.  
  
-   AMO를 사용하여 모델에 대한 필터 조건을 프로그래밍 방식으로 설정  
  
### <a name="creating-model-filters-using-data-mining-designer"></a>데이터 마이닝 디자이너를 사용하여 모델 필터 만들기  
 데이터 마이닝 디자이너에서 마이닝 모델의 `Filter` 속성을 변경하여 모델을 필터링합니다. 필터 식을 **속성** 창에 직접 입력하거나 필터 대화 상자를 열어 조건을 작성할 수 있습니다.  
  
 두 개의 필터 대화 상자가 있습니다. 첫 번째 대화 상자를 사용하면 사례 테이블에 적용되는 조건을 만들 수 있습니다. 데이터 원본에 여러 테이블이 포함되어 있는 경우 먼저 테이블을 선택한 다음 열을 선택하고 해당 열에 적용할 연산자와 조건을 지정합니다. 사용 하 여 여러 조건을 연결할 수 있습니다 `AND` / `OR` 연산자입니다. 값을 정의하는 데 사용할 수 있는 연산자는 열에 불연속 값이 포함되어 있는지, 아니면 연속 값이 포함되어 있는지에 따라 달라집니다. 예를 들어 연속 값의 경우 `greater than` 및 `less than` 연산자를 사용할 수 있습니다. 그러나 불연속 값의 경우에는 `= (equal to)`, `!= (not equal to)` 및 `is null` 연산자만 사용할 수 있습니다.  
  
> [!NOTE]  
>  `LIKE` 키워드는 지원되지 않습니다. 여러 불연속 특성을 포함하려는 경우 별도의 조건을 만들고 `OR` 연산자를 사용하여 연결해야 합니다.  
  
 조건이 복잡한 경우 두 번째 필터 대화 상자를 사용하여 한 번에 한 테이블로 작업할 수 있습니다. 두 번째 필터 대화 상자를 닫으면 식이 평가된 다음 사례 테이블의 다른 열에 설정된 필터 조건과 결합됩니다.  
  
### <a name="creating-filters-on-nested-tables"></a>중첩 테이블에 필터 만들기  
 데이터 원본 뷰에 중첩 테이블이 포함되어 있는 경우 두 번째 필터 대화 상자를 사용하여 중첩 테이블의 행에 대한 조건을 작성할 수 있습니다.  
  
 예를 들어 사례 테이블이 고객과 관련되어 있고 중첩 테이블에 고객이 구매한 제품이 표시되는 경우 중첩 테이블 필터에 다음 `[ProductName]='Water Bottle' OR ProductName='Water Bottle Cage'`구문을 사용하여 특정 항목을 구매한 고객에 대한 필터를 만들 수 있습니다.  
  
 `EXISTS` 또는 `NOT EXISTS` 키워드 및 하위 쿼리를 사용하여 중첩 테이블에 특정 값이 있는지 여부를 필터링할 수도 있습니다. 이렇게 하면 `EXISTS (SELECT * FROM Products WHERE ProductName='Water Bottle')`와 같은 조건을 만들 수 있습니다. 중첩 테이블에 값 `EXISTS SELECT(<subquery>)`을 포함하는 하나 이상의 행이 포함되어 있는 경우 `Water Bottle`는 `true`를 반환합니다.  
  
 사례 테이블에 대한 조건을 중첩 테이블에 대한 조건과 결합할 수 있습니다. 예를 들어 다음 구문에는 사례 테이블에 대한 조건(`Age > 30` ), 중첩 테이블에 대한 하위 쿼리(`EXISTS (SELECT * FROM Products)`) 및 중첩 테이블에 대한 여러 조건(`WHERE ProductName='Milk'  AND Quantity>2`)이 포함되어 있습니다.  
  
```  
(Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName='Milk'  AND Quantity>2) )  
```  
  
 필터 작성이 완료되면 필터 텍스트가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 평가되고 DMX 식으로 번역된 다음 모델과 함께 저장됩니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 필터 대화 상자를 사용하는 방법에 대한 자세한 내용은 [마이닝 모델에 필터 적용](apply-a-filter-to-a-mining-model.md)을 참조하세요.  
  
## <a name="managing-mining-model-filters"></a>마이닝 모델 필터 관리  
 같은 구조를 기반으로 하는 여러 모델을 쉽게 작성할 수 있으므로 데이터 기반 모델 필터링을 사용하면 마이닝 구조 및 마이닝 모델 관리 태스크가 간단해집니다. 또한 기존 마이닝 모델의 복사본을 빠르게 만든 다음 필터 조건만 변경할 수 있습니다. 그러나 필터로 인해 일부 혼란이 발생할 수 있습니다.  
  
 다음은 마이닝 모델에서 필터를 관리하고 해석하는 방법에 대한 질문과 대답입니다.  
  
### <a name="how-can-i-tell-whether-a-filter-is-being-used"></a>필터가 사용 중인지 여부를 어떻게 알 수 있습니까?  
 필터가 모델에 적용되어 있는지 여부를 판단하는 방법은 여러 가지가 있습니다.  
  
-   디자이너에서 클릭 합니다 **마이닝 모델** 탭을 엽니다 **속성**, 및 보기는 `Filter` 마이닝 모델의 속성.  
  
-   DMV, DMSCHEMA_MINING_MODELS는 필터의 텍스트를 포함하는 열을 출력합니다. DMV에서 다음 쿼리를 사용하여 모델 이름과 해당 필터를 반환할 수 있습니다.  
  
    ```  
    SELECT MODEL_NAME, [FILTER]   
    FROM $SYSTEM.DMSCHEMA_MINING_MODELS  
  
    ```  
  
-   AMO에서 MiningModel 개체의 Filter 속성 값을 가져오거나 XMLA의 Filter 요소를 검사할 수 있습니다.  
  
 모델에 대한 명명 규칙을 만들어 필터 내용을 반영할 수도 있습니다. 이렇게 하면 관련 모델을 쉽게 구분할 수 있습니다.  
  
### <a name="how-can-i-save-a-filter"></a>필터를 저장하려면 어떻게 합니까?  
 필터 식은 연결된 마이닝 모델 또는 중첩 테이블과 함께 저장되는 스크립트로 저장됩니다. 필터 텍스트를 삭제하는 경우 필터 식을 수동으로 다시 만들어야만 해당 텍스트를 복원할 수 있습니다. 따라서 복잡한 필터 식을 만드는 경우 필터 텍스트의 백업 복사본을 만들어야 합니다.  
  
### <a name="why-cant-i-see-any-effects-from-the-filter"></a>필터에서 효과가 보이지 표시 되지 않는 이유  
 필터 식을 변경하거나 추가할 때마다 구조 및 모델을 다시 처리해야 필터 효과를 확인할 수 있습니다.  
  
### <a name="why-do-i-see-filtered-attributes-in-prediction-query-results"></a>예측 쿼리 결과에 필터링된 특성이 나타나는 이유는 무엇입니까?  
 모델에 필터를 적용할 때는 모델 학습에 사용된 선택한 클래스에만 영향을 미칩니다. 필터는 모델에 알려진 특성에 영향을 미치지 않고 데이터 원본에 있는 데이터를 변경하거나 압축하지도 않습니다. 따라서 모델에 대한 쿼리는 다른 사례 유형에 대한 예측을 반환하고 모델에서 사용한 값의 드롭다운 목록에 필터에서 제외된 특성 값이 표시될 수 있습니다.  
  
 예를 들어 20-30세 사이의 여성과 관련된 경우만 사용하는 [Bike Buyer] 모델을 학습한다고 가정합니다. 자전거를 구입하는 남성의 확률을 예측하는 예측 쿼리를 여전히 실행하거나 30-40세 사이의 여성의 결과를 예측할 수 있습니다. 이는 데이터 원본에 있는 특성 및 값이 이론상으로 가능한 내용을 정의하지만 사례는 학습에 사용된 발생 횟수를 정의합니다. 그러나 학습 데이터는 대상 값을 가진 사례를 포함하지 않으므로 이러한 쿼리는 매우 작은 확률을 반환합니다.  
  
 모델에서 특성 값을 완전히 숨기거나 익명화해야 하는 경우 다음과 같은 여러 가지 방법이 있습니다.  
  
-   데이터 원본 뷰 정의의 일부로 또는 관계형 데이터 원본에 있는 수신 데이터를 필터링  
  
-   특성 값을 마스킹 또는 인코딩  
  
-   마이닝 구조 정의의 일부로 제외된 값을 범주로 축소  
  
## <a name="related-resources"></a>관련 리소스  
 필터 구문에 대한 자세한 내용 및 필터 식의 예를 보려면 [모델 필터 구문 및 예&#40;Analysis Services - 데이터 마이닝&#41;](model-filter-syntax-and-examples-analysis-services-data-mining.md)구문을 사용하여 특정 항목을 구매한 고객에 대한 필터를 만들 수 있습니다.  
  
 마이닝 모델을 테스트할 때 모델 필터를 사용하는 방법에 대한 자세한 내용은 [정확도 차트 유형 선택 및 차트 옵션 설정](choose-an-accuracy-chart-type-and-set-chart-options.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [모델 필터 구문 및 예&#40;Analysis Services - 데이터 마이닝&#41;](model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [테스트 및 유효성 검사&#40;데이터 마이닝&#41;](testing-and-validation-data-mining.md)  
  
  
