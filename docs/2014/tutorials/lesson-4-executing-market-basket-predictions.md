---
title: '4 단원: 시장 바구니 예측 실행 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b3238f1b-ea04-4253-ade2-838a806b62fe
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3b49fc242eb8b2242269c5af33cc094937bbe0de
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63312105"
---
# <a name="lesson-4-executing-market-basket-predictions"></a>4단원: Market Basket 예측 실행
  이 단원에서는 DMX `SELECT` 문을 사용 하 여 [2 단원: 시장 바구니 마이닝 구조에 마이닝 모델 추가](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)에서 만든 연결 모델을 기반으로 예측을 만듭니다. 예측 쿼리는 DMX `SELECT` 문을 사용하고 `PREDICTION JOIN` 절을 추가하여 만들어집니다. 예측 조인 구문에 대 한 자세한 내용은 [SELECT FROM &#60;model&#62; 예측 조인 &#40;DMX&#41;](/sql/dmx/select-from-model-cases-dmx)를 참조 하세요.  
  
 문의 **SELECT FROM \<MODEL> 예측 조인** 폼에는 다음과 같은 세 부분이 포함 되어 있습니다. `SELECT`  
  
-   결과 집합에 반환된 마이닝 모델 열 및 예측 함수 목록. 이 목록에는 원본 데이터의 입력 열도 포함될 수 있습니다.  
  
-   예측을 만드는 데 사용되는 데이터를 정의하는 원본 쿼리. 예를 들어 일괄 처리로 많은 예측을 만드는 경우 원본 쿼리가 고객 목록을 검색할 수 있습니다.  
  
-   마이닝 모델 열과 원본 데이터 간의 매핑. 열 이름이 일치하는 경우 `NATURAL PREDICTION JOIN` 구문을 사용할 수 있으며 열 매핑을 생략할 수 있습니다.  
  
 예측 함수를 사용하여 쿼리를 개선할 수 있습니다. 예측 함수는 예측 사항의 발생 확률과 같은 추가 정보를 제공하거나 학습 데이터 세트의 예측에 대한 지원을 제공합니다. 예측 함수에 대 한 자세한 내용은 [함수 &#40;DMX&#41;](/sql/dmx/functions-dmx)를 참조 하세요.  
  
 
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 예측 쿼리 작성기를 사용하여 예측 쿼리를 만들 수도 있습니다.  
  
## <a name="singleton-prediction-join-statement"></a>단일 PREDICTION JOIN 문  
 첫 번째 단계는 **SELECT FROM \<MODEL> 예측 조인** 구문을 사용 하 고 단일 값 집합을 입력으로 제공 하 여 단일 쿼리를 만드는 것입니다. 다음은 단일 문의 일반적인 예입니다.  
  
```  
SELECT <select list>  
    FROM [<mining model>]   
[NATURAL] PREDICTION JOIN  
(SELECT '<value>' AS [<column>],   
    (SELECT 'value' AS [<nested column>] UNION  
        SELECT 'value' AS [<nested column>] ...)   
    AS [<nested table>])  
AS [<input alias>]  
```  
  
 코드의 첫 번째 줄에서는 쿼리가 반환하는 마이닝 모델의 열을 정의하고 예측을 생성하는 데 사용되는 마이닝 모델의 이름을 지정합니다.  
  
```  
SELECT <select list> FROM [<mining model>]   
```  
  
 코드의 다음 줄은 수행할 작업을 나타냅니다. 각각의 열에 값을 지정하고 해당 모델과 일치하도록 정확한 열 이름을 입력할 것이기 때문에 `NATURAL PREDICTION JOIN` 구문을 사용할 수 있습니다. 그러나 열 이름이 서로 다른 경우 `ON` 절을 추가하여 모델 열과 새 데이터 열 사이의 매핑을 지정해야 합니다.  
  
```  
[NATURAL] PREDICTION JOIN  
```  
  
 코드의 다음 줄에서는 고객이 추가할 추가 제품 예측에 사용할 시장 바구니 제품을 정의합니다.  
  
```  
(SELECT '<value>' AS [<column>],   
    (SELECT 'value' AS [<nested column>] UNION  
        SELECT 'value' AS [<nested column>] ...)   
    AS [<nested table>])  
```  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   시장 바구니에 이미 있는 항목을 기반으로 고객이 구매할 가능성이 높은 다른 항목을 예측하는 쿼리를 만듭니다. 기본 *MINIMUM_PROBABILITY*와 함께 마이닝 모델을 사용 하 여이 쿼리를 만듭니다.  
  
-   시장 바구니에 이미 있는 항목을 기반으로 고객이 구매할 가능성이 높은 다른 항목을 예측하는 쿼리를 만듭니다. 이 쿼리는 *MINIMUM_PROBABILITY* 0.01으로 설정 된 다른 모델을 기반으로 합니다. 연결 모델에서 *MINIMUM_PROBABILITY* 의 기본값은 0.3 이므로이 모델에 대 한 쿼리는 기본 모델의 쿼리 보다 가능한 많은 항목을 반환 해야 합니다.  
  
## <a name="create-a-prediction-by-using-a-model-with-the-default-minimum_probability"></a>MINIMUM_PROBABILITY가 기본값인 모델을 사용하여 예측 만들기  
  
#### <a name="to-create-an-association-query"></a>연결 쿼리를 만들려면  
  
1.  **개체 탐색기**에서 인스턴스 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]를 마우스 오른쪽 단추로 클릭 하 고 **새 쿼리**를 가리킨 다음 **DMX** 를 클릭 하 여 쿼리 편집기를 엽니다.  
  
2.  
  `PREDICTION JOIN` 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    <select list>   
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
     열 이름 [Products]만 포함할 수 있지만 [Predict &#40;DMX&#41;](/sql/dmx/predict-dmx) 함수를 사용 하 여 알고리즘에서 반환 되는 제품 수를 3으로 제한할 수 있습니다. 또한 각 제품에 대한 지원, 확률 및 조정된 확률을 반환하는 `INCLUDE_STATISTICS`를 사용할 수 있습니다. 이러한 통계를 사용하면 예측 정확도의 등급을 매길 수 있습니다.  
  
4.  다음 내용을  
  
    ```  
    [<mining model>]   
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    [Default Association]  
    ```  
  
5.  다음 내용을  
  
    ```  
    (SELECT '<value>' AS [<column>],   
        (SELECT 'value' AS [<nested column>] UNION  
            SELECT 'value' AS [<nested column>] ...)   
        AS [<nested table>])  
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     이 문은 `UNION` 문을 사용하여 예측된 제품과 함께 시장 바구니에 포함되어야 하는 세 가지 제품을 지정합니다. 
  `SELECT` 문의 Model 열은 중첩된 제품 테이블에 포함된 모델 열에 해당합니다.  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    SELECT  
      PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    From  
      [Default Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
6.  
  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
7.  다른 이름 **으로 저장** 대화 상자에서 해당 폴더로 이동한 다음 파일 `Association Prediction.dmx`이름을로 합니다.  
  
8.  도구 모음에서 **실행** 단추를 클릭합니다.  
  
     이 쿼리는 HL 산악용 타이어, Fender 집합-산지 및 ML 산지 타이어의 세 가지 제품을 포함 하는 테이블을 반환 합니다. 테이블에는 반환된 이러한 제품이 확률 순서대로 나열됩니다. 반환된 제품 중 쿼리에 지정된 세 개의 제품과 동일한 시장 바구니에 포함될 가능성이 가장 높은 제품이 테이블 맨 위에 표시됩니다. 그 다음에 오는 두 개의 제품은 시장 바구니에 포함될 가능성이 다음으로 높은 제품입니다. 이 테이블은 예측의 정확도를 설명하는 통계도 포함합니다.  
  
## <a name="create-a-prediction-by-using-a-model-with-a-minimum_probability-of-001"></a>MINIMUM_PROBABILITY가 0.01인 모델을 사용하여 예측 만들기  
  
#### <a name="to-create-an-association-query"></a>연결 쿼리를 만들려면  
  
1.  **개체 탐색기**에서 인스턴스 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]를 마우스 오른쪽 단추로 클릭 하 고 **새 쿼리**를 가리킨 다음 **DMX** 를 클릭 하 여 쿼리 편집기를 엽니다.  
  
2.  
  `PREDICTION JOIN` 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    <select list>   
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    PREDICT([Modified Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
4.  다음 내용을  
  
    ```  
    [<mining model>]   
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    [Modified Association]  
    ```  
  
5.  다음 내용을  
  
    ```  
    (SELECT '<value>' AS [<column>],   
        (SELECT 'value' AS [<nested column>] UNION  
            SELECT 'value' AS [<nested column>] ...)   
        AS [<nested table>])  
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     이 문은 `UNION` 문을 사용하여 예측된 제품과 함께 시장 바구니에 포함되어야 하는 세 가지 제품을 지정합니다. 
  `[Model]` 문의 `SELECT` 열은 중첩된 제품 테이블의 열에 해당합니다.  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    SELECT  
      PREDICT([Modified Association].[Products],INCLUDE_STATISTICS,3)  
    From  
      [Modified Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
6.  
  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
7.  다른 이름 **으로 저장** 대화 상자에서 해당 폴더로 이동한 다음 파일 `Modified Association Prediction.dmx`이름을로 합니다.  
  
8.  도구 모음에서 **실행** 단추를 클릭합니다.  
  
     이 쿼리는 HL 산 타이어, 해상 병 및 Fender 설정-산지의 세 가지 제품을 포함 하는 테이블을 반환 합니다. 테이블에는 이러한 제품이 확률 순서대로 나열됩니다. 테이블 맨 위에 나타나는 제품은 쿼리에 지정된 세 개의 제품과 동일한 시장 바구니에 포함될 가능성이 가장 높은 제품입니다. 나머지 제품은 시장 바구니에 포함될 가능성이 다음으로 높은 제품입니다. 이 테이블은 예측의 정확도를 설명하는 통계도 포함합니다.  
  
     이 쿼리의 결과에서 *MINIMUM_PROBABILITY* 매개 변수의 값이 쿼리에서 반환 되는 결과에 영향을 줄 수 있습니다.  
  
 이 단원은 Market Basket 자습서의 마지막 단계입니다. 이제 고객이 동시에 구매할 수 있는 제품을 예측하는 데 사용할 수 있는 모델 집합이 완료되었습니다.  
  
 다른 예측 시나리오에서 DMX를 사용 하는 방법을 알아보려면 [자전거 구매자 DMX 자습서](../../2014/tutorials/bike-buyer-dmx-tutorial.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [연결 모델 쿼리 예제](../../2014/analysis-services/data-mining/association-model-query-examples.md)   
 [데이터 마이닝 쿼리 인터페이스](../../2014/analysis-services/data-mining/data-mining-query-tools.md)  
  
  
