---
title: '5단원: 예측 쿼리를 실행 합니다. | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0037bd2f-aa2d-464b-bf86-b0210f0438b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a5f4d6dd79f62541e207df688349f694680e2421
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56038414"
---
# <a name="lesson-5-executing-prediction-queries"></a>5단원: 예측 쿼리 실행
  이 단원에서는 사용할지 합니다 [SELECT FROM \<모델 > PREDICTION JOIN (DMX)](/sql/dmx/select-from-model-cases-dmx) 형식의 두 가지 유형의 의사 결정 트리를 기반으로 예측을 만드는 SELECT 문은 모델에서 만든 [ 2 단원: 연결 마이닝 구조에 마이닝 모델 추가](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)합니다. 이러한 예측 유형은 다음과 같습니다.  
  
 단일 쿼리  
 예측을 만들 때는 단일 쿼리를 사용하여 임시 값을 제공합니다. 예를 들어 한 고객의 통근 거리, 지역 번호 또는 자녀 수와 같은 입력을 쿼리에 전달하여 해당 고객이 자전거를 구입할 가능성이 있는지를 확인할 수 있습니다. 단일 쿼리는 이러한 입력을 기준으로 해당 고객이 자전거를 구입할 가능성을 나타내는 값을 반환합니다.  
  
 일괄 처리 쿼리  
 일괄 처리 쿼리를 사용하여 잠재 고객 테이블에서 자전거를 구입할 가능성이 있는 고객을 확인할 수 있습니다. 예를 들어 마케팅 부서에서 고객 및 고객 특성 목록을 제공한 경우 일괄 처리 예측을 사용하여 해당 테이블에서 자전거를 구입할 가능성이 있는 고객을 확인할 수 있습니다.  
  
 [SELECT FROM \<모델 > PREDICTION JOIN (DMX)](/sql/dmx/select-from-model-cases-dmx) SELECT 문의 양식을 세 부분이 있습니다.  
  
-   결과에 반환된 마이닝 모델 열 및 예측 함수 목록. 결과에는 원본 데이터의 입력 열도 포함될 수 있습니다.  
  
-   예측 생성에 사용되는 데이터를 정의하는 원본 쿼리. 예를 들어 일괄 처리 쿼리에서는 고객 목록이 원본 쿼리가 될 수 있습니다.  
  
-   마이닝 모델 열과 원본 데이터 간의 매핑. 이름이 일치하는 경우 NATURAL 구문을 사용할 수 있으며 열 매핑을 수행하지 않아도 됩니다.  
  
 예측 함수를 사용하여 쿼리의 질을 보다 향상시킬 수 있습니다. 예측 함수는 예측 사항의 발생 확률과 같은 추가 정보를 제공하고 학습 데이터 집합의 예측에 대한 지지도를 제공합니다. 예측 함수에 대 한 자세한 내용은 참조 하세요. [함수 &#40;DMX&#41;](/sql/dmx/functions-dmx)합니다.  
  
 이 자습서의 예측은 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 예제 데이터베이스의 ProspectiveBuyer 테이블을 기반으로 합니다. ProspectiveBuyer 테이블에는 잠재 고객 및 관련 특징 목록이 있습니다. 이 테이블의 고객은 의사 결정 트리 마이닝 모델을 만드는 데 사용된 고객과는 독립적입니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 예측 쿼리 작성기를 사용하여 예측을 만들 수도 있습니다.  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   단일 쿼리를 만들어 특정 고객이 자전거를 구입할 가능성이 있는지 여부 확인  
  
-   일괄 처리 쿼리를 사용하여 고객 테이블에서 자전거를 구입할 가능성이 있는 고객 확인  
  
## <a name="singleton-query"></a>단일 쿼리  
 첫 번째 단계는 사용 하는 [선택에서 &#60;모델&#62; PREDICTION JOIN &#40;DMX&#41; ](/sql/dmx/select-from-model-cases-dmx) 단일 예측 쿼리에서 합니다. 다음은 단일 문의 일반적인 예입니다.  
  
```  
SELECT <select list> FROM [<mining model name>]   
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
```  
  
 코드의 첫 번째 줄에서는 쿼리가 반환할 마이닝 모델의 열을 정의하고 예측을 생성하는 데 사용되는 마이닝 모델을 지정합니다.  
  
```  
SELECT <select list> FROM [<mining model name>]   
```  
  
 코드의 다음 줄에서는 예측 생성에 사용할 고객의 특징을 정의합니다.  
  
```  
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
ORDER BY <expression>  
```  
  
 NATURAL PREDICTION JOIN을 지정하는 경우 서버에서는 열 이름을 기반으로 모델의 각 열을 입력 열에 일치시킵니다. 열 이름이 일치하지 않는 경우에는 해당 열이 무시됩니다.  
  
#### <a name="to-create-a-singleton-prediction-query"></a>단일 예측 쿼리를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
2.  단일 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    <select list>   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Bike Buyer] AS Buyer, PredictHistogram([Bike Buyer]) AS Statistics  
    ```  
  
     AS 문은 쿼리에서 반환한 열의 별칭을 지정하는 데 사용됩니다. 합니다 [PredictHistogram](/sql/dmx/predicthistogram-dmx) 함수는 확률 및 지지도 포함 하 여 예측에 대 한 통계를 반환 합니다. 예측 문에서 사용할 수 있는 함수에 대 한 자세한 내용은 참조 하세요. [함수 &#40;DMX&#41;](/sql/dmx/functions-dmx)합니다.  
  
4.  다음 내용을  
  
    ```  
    [<mining model>]   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  다음 내용을  
  
    ```  
    (SELECT '<value>' AS [<column name>], ...)  AS t  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    (SELECT 35 AS [Age],  
      '5-10 Miles' AS [Commute Distance],  
      '1' AS [House Owner Flag],  
      2 AS [Number Cars Owned],  
      2 AS [Total Children]) AS t  
    ```  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    SELECT  
       [Bike Buyer] AS Buyer,  
       PredictHistogram([Bike Buyer]) AS Statistics  
    FROM  
       [Decision Tree]  
    NATURAL PREDICTION JOIN  
    (SELECT 35 AS [Age],  
       '5-10 Miles' AS [Commute Distance],  
       '1' AS [House Owner Flag],  
       2 AS [Number Cars Owned],  
       2 AS [Total Children]) AS t  
    ```  
  
6.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
7.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `Singleton_Query.dmx`입니다.  
  
8.  도구 모음에서 **실행** 단추를 클릭합니다.  
  
     쿼리가 지정 특징을 갖는 고객이 자전거를 구입할지 여부에 대한 예측과 이 예측에 대한 통계를 반환합니다.  
  
## <a name="batch-query"></a>일괄 처리 쿼리  
 다음 단계는 사용 하는 [선택에서 &#60;모델&#62; PREDICTION JOIN &#40;DMX&#41; ](/sql/dmx/select-from-model-cases-dmx) 일괄 처리 예측 쿼리에서 합니다. 다음은 일괄 처리 문의 일반적인 예입니다.  
  
```  
SELECT TOP <number> <select list>   
FROM [<mining model name>]  
PREDICTION JOIN  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
ON <on clause, mapping,>  
WHERE <where clause, boolean expression,>  
ORDER BY <expression>  
```  
  
 단일 쿼리의 경우와 같이 코드의 처음 두 줄에서는 예측 생성에 사용할 마이닝 모델의 이름과 쿼리가 반환하는 마이닝 모델의 열을 정의합니다. 맨 위에 \<번호 > 문은 지정 된 결과 또는 쿼리만 반환 됩니다 지정 \<수 >.  
  
 코드의 다음 줄에서는 예측의 토대가 되는 원본 데이터를 정의합니다.  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
```  
  
 원본 데이터를 검색하는 방법에는 여러 가지가 있지만 이 자습서에서는 OPENQUERY를 사용합니다. 사용 가능한 옵션에 대 한 자세한 내용은 참조 하세요. [ &#60;원본 데이터 쿼리&#62;](/sql/dmx/source-data-query)합니다.  
  
 다음 줄에서는 마이닝 모델의 원본 열과 원본 데이터 열 간의 매핑을 정의합니다.  
  
```  
ON <column mappings>  
```  
  
 WHERE 절은 예측 쿼리가 반환하는 결과를 필터링합니다.  
  
```  
WHERE <where clause, boolean expression,>  
```  
  
 선택 사항인 코드의 마지막 줄에서는 결과를 정렬할 기준 열을 지정합니다.  
  
```  
ORDER BY <expression> [DESC|ASC]  
```  
  
 ORDER BY는 TOP와 함께 사용 \<수 > 문에서 반환 되는 결과를 필터링 합니다. 예를 들어 이 예측에서는 예측의 정확도 예상률을 기준으로 정렬된 상위 10명의 자전거 구매자를 반환합니다. [DESC|ASC] 구문을 사용하여 결과 표시 순서를 조정할 수 있습니다.  
  
#### <a name="to-create-a-batch-prediction-query"></a>일괄 처리 예측 쿼리를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
2.  일괄 처리 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    <select list>   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    ```  
  
     TOP 10 절은 쿼리가 상위 10개의 결과만 반환하도록 지정합니다. 이 쿼리의 ORDER BY 문은 예측의 정확도 예상률을 기준으로 결과를 정렬하여 가능성이 가장 높은 상위 10개의 결과만 반환되도록 합니다.  
  
4.  다음 자리 표시자를  
  
    ```  
    [<mining model>]   
    ```  
  
     모델의 이름으로 바꿉니다.  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  다음 제네릭 OPENQUERY 문을  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     다음과 같은 현재 Adventureworks 데이터 웨어하우스를 참조하는 문으로 바꿉니다.  
  
    ```  
    OPENQUERY([Adventure Works DW 2014],  
      'SELECT  
        [LastName],  
        [FirstName],  
        [MaritalStatus],  
        [Gender],  
        [YearlyIncome],  
        [TotalChildren],  
        [NumberChildrenAtHome],  
        [Education],  
        [Occupation],  
        [HouseOwnerFlag],  
        [NumberCarsOwned]  
      FROM  
        [dbo].[ProspectiveBuyer]  
      ') AS t  
    ```  
  
6.  다음 일반 구문을  
  
    ```  
    <ON clause, mapping,>   
    WHERE <where clause, boolean expression,>  
    ORDER BY <expression>  
    ```  
  
     이 모델에 필요한 열 매핑과 입력 데이터 집합으로 바꿉니다.  
  
    ```  
    [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
     확률이 가장 높은 결과가 먼저 나열되도록 하려면 `DESC`를 지정합니다.  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    FROM  
      [Decision Tree]  
    PREDICTION JOIN  
      OPENQUERY([Adventure Works DW 2014],  
        'SELECT  
          [LastName],  
          [FirstName],  
          [MaritalStatus],  
          [Gender],  
          [YearlyIncome],  
          [TotalChildren],  
          [NumberChildrenAtHome],  
          [Education],  
          [Occupation],  
          [HouseOwnerFlag],  
          [NumberCarsOwned]  
        FROM  
          [dbo].[ProspectiveBuyer]  
        ') AS t  
    ON  
      [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
7.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
8.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `Batch_Prediction.dmx`입니다.  
  
9. 도구 모음에서 **실행** 단추를 클릭합니다.  
  
     쿼리에서 고객 이름, 각 고객의 자전거 구입 여부 예측 및 예측 사항의 발생 확률을 포함하는 테이블이 반환됩니다.  
  
 이 단원은 Bike Buyer 자습서의 마지막 단계입니다. 이제 생성된 마이닝 모델 집합을 사용하여 고객 간 유사성을 조사하고 잠재 고객이 자전거를 구입할 것인지 여부를 예측할 수 있습니다.  
  
 시장 바구니 시나리오에서 DMX를 사용 하는 방법에 알아보려면 참조 [Market Basket DMX 자습서](../../2014/tutorials/market-basket-dmx-tutorial.md)합니다.  
  
  
