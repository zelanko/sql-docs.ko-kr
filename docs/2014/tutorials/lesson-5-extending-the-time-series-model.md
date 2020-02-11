---
title: '5 단원: 시계열 모델 확장 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7aad4946-c903-4e25-88b9-b087c20cb67d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2716e985897f8115d189d9410b7cdb13fb1af291
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62822075"
---
# <a name="lesson-5-extending-the-time-series-model"></a>5단원: 시계열 모델 확장
  
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise에서는 시계열 모델에 새 데이터를 추가하고 새 데이터를 모델에 자동으로 통합할 수 있습니다. 다음 두 가지 방법 중 하나를 사용하여 시계열 마이닝 모델에 새 데이터를 추가할 수 있습니다.  
  
-   PREDICTION JOIN을 사용하여 외부 원본의 데이터를 학습 데이터에 조인합니다.  
  
-   단일 예측 쿼리를 사용하여 한 번에 한 조각씩 데이터를 제공합니다.  
  
 예를 들어 몇 개월 전에 기존 판매 데이터에 대해 마이닝 모델을 학습했다고 가정할 때 새로운 판매 데이터를 얻어 판매 예측 업데이트를 통해 새 데이터를 통합하려고 할 수 있습니다. 이 작업은 새 매출 수치를 입력 데이터로 제공하고 복합 데이터 집합을 기반으로 새 예측을 생성하여 간단하게 수행할 수 있습니다.  
  
## <a name="making-predictions-with-extend_model_cases"></a>EXTEND_MODEL_CASES로 예측 수행  
 다음은 EXTEND_MODEL_CASES를 사용한 일반적인 시계열 예측 예입니다. 첫 번째 예를 사용하면 원래 모델의 마지막 시간 단계에서 시작되는 예측 수를 지정할 수 있습니다.  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>]  
```  
  
 두 번째 예를 사용하면 예측을 시작하고 종료할 시간 단계를 지정할 수 있습니다. 기본적으로 예측 쿼리에 사용되는 시간 단계는 항상 원래 계열의 끝에서 시작되므로 모델 사례를 확장할 때 이 옵션이 중요합니다.  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n-start, n-end, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>}  
```  
  
 이 자습서에서는 두 종류 모두의 쿼리를 만듭니다.  
  
#### <a name="to-create-a-singleton-prediction-query-on-a-time-series-model"></a>시계열 모델에 대한 단일 예측 쿼리를 만들려면  
  
1.  
  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
2.  단일 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    ```  
  
     첫 번째 줄에서는 모델에서 계열을 식별하는 값을 검색합니다.  
  
     두 번째 줄에는 Quantity에 대한 6개의 예측을 가져오는 예측 함수가 포함되어 있습니다. 결과를 보다 쉽게 이해할 수 있도록 예측 결과 열에 별칭 `PredictQty`가 할당됩니다.  
  
4.  다음 내용을  
  
    ```  
    FROM <mining model>  
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    FROM [Forecasting_MIXED]  
    ```  
  
5.  다음 내용을  
  
    ```  
    PREDICTION JOIN <source query>  
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    NATURAL PREDICTION JOIN   
    (  
       SELECT 1 AS [Reporting Date],  
       '10' AS [Quantity],  
       'M200 Europe' AS [Model Region]  
       UNION SELECT  
       2 AS [Reporting Date],  
       15 AS [Quantity]),  
       'M200 Europe' AS [Model Region]  
    ) AS t  
    ```  
  
6.  다음 내용을  
  
    ```  
    [WHERE <criteria>]  
    ```  
  
     다음으로 바꿀 수 있습니다.  
  
    ```  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    FROM  
       [Forecasting_MIXED]  
    NATURAL PREDICTION JOIN   
       SELECT 1 AS [ReportingDate],  
      '10' AS [Quantity],  
      'M200 Europe' AS [ModelRegion]  
    UNION SELECT  
      2 AS [ReportingDate],  
      15 AS [Quantity]),  
      'M200 Europe' AS [ModelRegion]  
    ) AS t  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
7.  
  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
8.  다른 이름 **으로 저장** 대화 상자에서 해당 폴더로 이동한 다음 파일 `Singleton_TimeSeries_Query.dmx`이름을로 합니다.  
  
9. 도구 모음에서 **실행** 단추를 클릭합니다.  
  
     쿼리가 Europe 및 Pacific 지역에서의 M200 자전거 판매 수량 예측 값을 반환합니다.  
  
## <a name="understanding-prediction-start-with-extend_model_cases"></a>EXTEND_MODEL_CASES로 예측 시작 지점 이해  
 원래 모델을 기반으로 예측을 만들었으므로 이제 새 데이터로 결과를 비교하여, 판매 데이터를 업데이트할 경우 예측에 어떠한 영향이 있는지 확인할 수 있습니다. 이렇게 하기 전에 방금 만든 코드를 검토하고 다음 사항을 확인합니다.  
  
-   Europe 지역에 대해서만 새 데이터를 제공했습니다.  
  
-   2개월에 상당하는 새 데이터만 제공했습니다.  
  
 다음 표에서는 M200 Europe에 대해 제공된 새 값이 예측에 어떠한 영향을 주는지 보여 줍니다. Pacific 지역의 M200 제품에 대해서는 새 데이터를 제공하지 않았지만 이 계열은 비교용으로 제공됩니다.  
  
 **제품 및 지역: 유럽 M200**  
  
|||||  
|-|-|-|-|  
|||기존 모델(`PredictTimeSeries`)|판매 데이터가 업데이트된 모델(`PredictTimeSeries`가 있는 `EXTEND_MODEL_CASES`)|  
|M200 Europe|7/25/2008 12:00:00 AM|77|10|  
|M200 Europe|8/25/2008 12:00:00 AM|64|15|  
|M200 Europe|9/25/2008 12:00:00 AM|59|72|  
|M200 Europe|10/25/2008 12:00:00 AM|56|69|  
|M200 Europe|11/25/2008 12:00:00 AM|56|68|  
|M200 Europe|12/25/2008 12:00:00 AM|74|89|  
  
 **제품 및 지역: M200 태평양**  
  
|||||  
|-|-|-|-|  
|||기존 모델(`PredictTimeSeries`)|판매 데이터가 업데이트된 모델(`PredictTimeSeries`가 있는 `EXTEND_MODEL_CASES`)|  
|M200 Pacific|7/25/2008 12:00:00 AM|41|41|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|38|38|  
|M200 Pacific|10/25/2008 12:00:00 AM|41|41|  
|M200 Pacific|11/25/2008 12:00:00 AM|36|36|  
|M200 Pacific|12/25/2008 12:00:00 AM|39|39|  
  
 이러한 결과를 통해 다음 두 가지 사실을 알 수 있습니다.  
  
-   M200 Europe 계열에 대한 처음 두 예측은 사용자가 제공한 새 데이터와 동일합니다. 기본적으로 Analysis Services에서는 예측을 만들지 않고 실제 새 데이터 요소를 반환합니다. 이는 모델 사례를 확장할 때 예측 쿼리에 사용되는 시간 단계가 항상 원래 계열의 끝에서 시작되기 때문입니다. 따라서 두 개의 새 데이터 요소를 추가하면 반환되는 처음 두 예측이 새 데이터와 겹치게 됩니다.  
  
-   새 데이터 요소가 모두 사용된 후 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 업데이트된 모델을 기반으로 예측을 만듭니다. 따라서 2005년 9월부터 왼쪽 열에 있는 원래 모델의 M200 Europe에 대한 예측과 오른쪽 열에 있는 EXTEND_MODEL_CASES 사용 모델의 M200 Europe에 대한 예측이 달라지는 것을 확인할 수 있습니다. 모델이 새 데이터로 업데이트되었기 때문에 예측이 다릅니다.  
  
## <a name="using-start-and-end-time-steps-to-control-predictions"></a>시작 및 종료 시간 단계를 사용하여 예측 제어  
 모델을 확장하면 새 데이터가 항상 계열의 끝에 연결됩니다. 그러나 예측을 위해 예측 쿼리에 사용되는 시간 조각은 원래 계열의 끝에서 시작됩니다. 새 데이터를 추가할 때 새 예측만 얻으려면 시작 지점을 시간 조각 수로 지정해야 합니다. 예를 들어 두 개의 새 데이터 요소를 추가하고 네 개의 새 예측을 만들려면 다음을 수행합니다.  
  
-   시계열 모델에 대해 PREDICTION JOIN을 만들고 2개월에 상당하는 새 데이터를 지정합니다.  
  
-   네 개의 시간 조각에 대한 예측을 요청합니다. 여기에서 시작 지점은 3, 종료 지점은 시간 조각 6입니다.  
  
 즉, 새 데이터에 n 개의 시간 조각이 포함 되어 있는 상태에서 시간 단계 1부터 n까지에 대 한 예측을 요청 하면 예측은 새 데이터와 동일한 기간에 일치 합니다. 가지고 있는 데이터의 범위를 벗어나는 기간에 대한 새 예측을 구하려면 새 데이터 계열 다음의 n+1 시간 조각에서 예측을 시작하거나 추가 시간 조각을 요청해야 합니다.  
  
> [!NOTE]  
>  새 데이터를 추가할 때에는 기록 예측을 수행할 수 없습니다.  
  
 다음 예에서는 이전 예의 두 계열에 대해 새 예측만 얻을 수 있도록 하는 DMX 문을 보여 줍니다.  
  
```  
SELECT [Model Region],  
PredictTimeSeries([Quantity],3,6, EXTEND_MODEL_CASES) AS PredictQty  
FROM  
   [Forecasting_MIXED]  
NATURAL PREDICTION JOIN   
   SELECT 1 AS [ReportingDate],  
  '10' AS [Quantity],  
  'M200 Europe' AS [ModelRegion]  
UNION SELECT  
  2 AS [ReportingDate],  
  15 AS [Quantity]),  
  'M200 Europe' AS [ModelRegion]  
) AS t  
WHERE [ModelRegion] = 'M200 Europe'  
```  
  
 예측 결과는 시간 조각 3에서 시작되며 이는 사용자가 제공한 2개월에 상당하는 새 데이터 다음입니다.  
  
 **제품 및 지역: 유럽 M200**  
  
 데이터가 업데이트된 모델(EXTEND_MODEL_CASES가 있는 PredictTimeSeries)  
  
||||  
|-|-|-|  
|M200 Europe|9/25/2008 12:00:00 AM|72|  
|M200 Europe|10/25/2008 12:00:00 AM|69|  
|M200 Europe|11/25/2008 12:00:00 AM|68|  
|M200 Europe|12/25/2008 12:00:00 AM|89|  
  
## <a name="making-predictions-with-replace_model_cases"></a>REPLACE_MODEL_CASES로 예측 수행  
 모델 사례 대체는 하나의 사례 집합을 학습시킨 다음 이 모델을 다른 데이터 계열에 적용하려는 경우 유용합니다. 이 시나리오에 대 한 자세한 연습은 [2 단원: &#40;중급 데이터 마이닝 자습서&#41;예측 시나리오 빌드를 ](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md).  
  
## <a name="see-also"></a>참고 항목  
 [시계열 모델 쿼리 예제](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
