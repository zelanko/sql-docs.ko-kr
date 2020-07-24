---
title: PredictTimeSeries (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ececf16131544b0a450d877b5c4ba43c2cd80466
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970691"
---
# <a name="predicttimeseries-dmx"></a>PredictTimeSeries(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  시계열 데이터에 대한 예측 미래 값을 반환합니다. 시계열 데이터는 연속적이며 중첩 테이블이나 사례 테이블에 저장할 수 있습니다. **PredictTimeSeries** 함수는 항상 중첩 테이블을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictTimeSeries(<table column reference>)  
PredictTimeSeries(<table column reference>, n)  
PredictTimeSeries(<table column reference>, n-start, n-end)  
PredictTimeSeries(<scalar column reference>)  
PredictTimeSeries(<scalar column reference>, n)  
PredictTimeSeries(<scalar column reference>, n-start, n-end)  
PredictTimeSeries(<table column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<table column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
```  
  
## <a name="arguments"></a>인수  
 *\<table column reference>*, *\<scalar column referenc>*  
 예측할 열의 이름을 지정합니다. 열에는 스칼라 또는 테이블 형식 데이터가 포함될 수 있습니다.  
  
 *n*  
 예측할 다음 단계의 수를 지정합니다. *N*에 값을 지정 하지 않으면 기본값은 1입니다.  
  
 *n* 은 0 일 수 없습니다. 하나 이상의 예측을 만들지 않으면 함수에서 오류가 반환됩니다.  
  
 *n-시작, n-끝*  
 시계열 단계의 범위를 지정합니다.  
  
 *n-start* 는 정수 여야 하며 0 일 수 없습니다.  
  
 *n 끝* 은 *n-시작*보다 큰 정수 여야 합니다.  
  
 *\<source query>*  
 예측을 수행하는 데 사용되는 외부 데이터를 정의합니다.  
  
 REPLACE_MODEL_CASES | EXTEND_MODEL_CASES  
 새 데이터를 처리하는 방법을 나타냅니다.  
  
 REPLACE_MODEL_CASES는 모델의 데이터 요소가 새 데이터로 바뀌도록 지정합니다. 그러나 예측은 기존 마이닝 모델의 패턴을 기반으로 합니다.  
  
 EXTEND_MODEL_CASES는 새 데이터가 원래의 학습 데이터 집합에 추가되도록 지정합니다. 이후의 예측은 새 데이터가 모두 사용된 후에만 복합 데이터 집합에 대해 생성됩니다.  
  
 이러한 인수는 PREDICTION JOIN 문을 사용하여 새 데이터가 추가되는 경우에만 사용할 수 있습니다. PREDICTION JOIN 쿼리를 사용하고 인수를 지정하지 않을 경우 기본값은 EXTEND_MODEL_CASES입니다.  
  
## <a name="return-type"></a>반환 형식  
 \<*table expression*>.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시계열 알고리즘은 PREDICTION JOIN 문을 사용하여 새 데이터를 추가하는 경우 기록 예측을 지원하지 않습니다.  
  
 PREDICTION JOIN에서 예측 프로세스는 항상 원래 학습 계열이 끝난 직후의 시간 단계에서 시작됩니다. 이는 새 데이터를 추가하는 경우에도 마찬가지입니다. 따라서 *n* 매개 변수 및 *n-시작* 매개 변수 값은 0 보다 큰 정수 여야 합니다.  
  
> [!NOTE]  
>  새 데이터의 길이는 예측의 시작 지점에 영향을 미치지 않습니다. 따라서 새 데이터를 추가하고 새 예측도 수행하려면 예측 시작 지점을 새 데이터의 길이보다 큰 값으로 설정하거나 예측 종료 지점을 새 데이터 길이만큼 늘려야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 기존 시계열 모델에 대해 예측을 수행하는 방법을 보여 줍니다.  
  
-   첫 번째 예는 현재 모델을 기반으로 지정된 수만큼의 예측을 수행하는 방법을 보여 줍니다.  
  
-   두 번째 예는 REPLACE_MODEL_CASES 매개 변수를 사용하여 지정 모델의 패턴을 새 데이터 집합에 적용하는 방법을 보여 줍니다.  
  
-   세 번째 예는 EXTEND_MODEL_CASES 매개 변수를 사용하여 마이닝 모델을 새 데이터로 업데이트하는 방법을 보여 줍니다.  
  
 시계열 모델을 사용 하는 방법에 대 한 자세한 내용은 데이터 마이닝 자습서, [2 단원: 예측 시나리오 빌드 &#40;중급 데이터 마이닝 자습서&#41;](https://msdn.microsoft.com/library/9a988156-c900-4c22-97fa-f6b0c1aea9e2) 및 [시계열 예측 DMX 자습서](https://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2)를 참조 하세요.  
  
> [!NOTE]  
>  사용자 모델의 결과는 다를 수 있습니다. 아래 예의 결과는 결과 형식을 보여 주기 위한 것입니다.  
  
### <a name="example-1-predicting-a-number-of-time-slices"></a>예제 1: 많은 시간 조각 예측  
 다음 예에서는 **PredictTimeSeries** 함수를 사용 하 여 다음 세 시간 단계에 대 한 예측을 반환 하 고 유럽 및 태평양 지역의 M200 시리즈에 대 한 결과를 제한 합니다. 이 특정 모델에서 예측 가능한 특성은 Quantity 이므로 `[Quantity]` PredictTimeSeries 함수에 대 한 첫 번째 인수로를 사용 해야 합니다.  
  
```  
SELECT FLATTENED  
    [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity],3)AS t   
FROM  
    [Forecasting]  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 Pacific'  
```  
  
 예상 결과:  
  
|Model Region|t.$TIME|t.Quantity|  
|------------------|-------------|----------------|  
|M200 Europe|7/25/2008 12:00:00 AM|121|  
|M200 Europe|8/25/2008 12:00:00 AM|142|  
|M200 Europe|9/25/2008 12:00:00 AM|152|  
|M200 Pacific|7/25/2008 12:00:00 AM|46|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|42|  
  
 이 예에서는 결과를 읽기 쉽도록 FLATTENED 키워드가 사용되었습니다.  FLATTENED 키워드를 사용하지 않고 계층적 행 집합을 반환하면 이 쿼리에서 두 열을 반환합니다. 첫 번째 열에는 [ModelRegion]에 대한 값이 포함되고 두 번째 열에는 두 개의 열(예측되는 시간 조각을 보여 주는 $TIME 및 예측되는 값을 포함하는 Quantity)이 있는 중첩 테이블이 포함됩니다.  
  
### <a name="example-2-adding-new-data-and-using-replace_model_cases"></a>예제 2: 새 데이터 추가 및 REPLACE_MODEL_CASES 사용  
 특정 지역에 대한 데이터가 잘못된 것을 발견하고 모델의 패턴을 사용하여 새 데이터와 일치하도록 예측을 조정하려 한다고 가정합니다. 다른 지역의 추세가 더 안정적이라는 것을 발견하고 가장 안정적인 모델을 여러 지역의 데이터에 적용하려고 할 수도 있습니다.  
  
 이러한 시나리오에서는 REPLACE_MODEL_CASES 매개 변수를 사용하고 기록 데이터로 사용할 새 데이터 집합을 지정할 수 있습니다. 이렇게 하면 프로젝션이 지정된 모델의 패턴을 기반으로 하지만 새 데이터 요소의 끝에서 부드럽게 이어집니다. 이 시나리오에 대 한 전체 연습은 [고급 시계열 예측 &#40;중급 데이터 마이닝 자습서&#41;](https://msdn.microsoft.com/library/b614ebdb-07ca-44af-a0ff-893364bd4b71)를 참조 하세요.  
  
 다음 PREDICTION JOIN 쿼리에서는 데이터를 바꾸고 새 예측을 만드는 구문을 보여 줍니다. 데이터를 바꾸기 위해 이 예에서는 Amount 및 Quantity 열의 값을 검색하여 각 값에 2를 곱합니다.  
  
```  
SELECT [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 3, REPLACE_MODEL_CASES)   
FROM  
    [Forecasting]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT [ModelRegion],   
    ([Quantity] * 2) as Quantity,  
    ([Amount] * 2) as Amount,  
      [ReportingDate]  
    FROM [dbo].vTimeSeries  
    WHERE ModelRegion = N''M200 Pacific''  
    ') AS t  
ON  
  [Forecasting].[Model Region] = t.[ Model Region] AND  
[Forecasting].[Reporting Date] = t.[ReportingDate] AND  
[Forecasting].[Quantity] = t.[Quantity] AND  
[Forecasting].[Amount] = t.[Amount]  
```  
  
 다음 표에서는 예측의 결과를 비교 합니다.  
  
 원래 예측:  
  
||||  
|-|-|-|  
|M200 Pacific|7/25/2008 12:00:00 AM|46|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|42|  
  
 업데이트 된 예측:  
  
||||  
|-|-|-|  
|M200 Pacific|7/25/2008 12:00:00 AM|91|  
|M200 Pacific|8/25/2008 12:00:00 AM|89|  
|M200 Pacific|9/25/2008 12:00:00 AM|84|  
  
### <a name="example-3-adding-new-data-and-using-extend_model_cases"></a>예 3: 새 데이터 추가 및 EXTEND_MODEL_CASES 사용  
 예 3에서는 기존 데이터 계열의 끝에 추가 되는 새 데이터를 제공 하는 *EXTEND_MODEL_CASES* 옵션을 사용 하는 방법을 보여 줍니다. 기존 데이터 요소를 바꾸는 대신 새 데이터가 모델에 추가됩니다.  
  
 다음 예에서는 NATURAL PREDICTION JOIN 뒤에 오는 SELECT 문에 새 데이터가 제공됩니다. 이 구문을 사용하여 새로운 여러 입력 행을 제공할 수 있지만 새로운 각 입력 행에는 고유한 타임스탬프가 있어야 합니다.  
  
```  
SELECT [Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 5, EXTEND_MODEL_CASES)   
FROM  
    [Forecasting]  
NATURAL PREDICTION JOIN  
    (SELECT  
        1 as [Reporting Date],  
        10 as [Quantity],  
        'M200 Europe' AS [Model Region]  
    UNION SELECT   
        2 as [Reporting Date],  
        15 as [Quantity],  
        'M200 Europe' AS [Model Region]  
) AS T  
WHERE ([Model Region] = 'M200 Europe'  
 OR [Model Region] = 'M200 Pacific')  
```  
  
 쿼리에서는 *EXTEND_MODEL_CASES* 옵션을 사용 하기 때문에에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 예측에 대해 다음 작업을 수행 합니다.  
  
-   2개월에 상당하는 새 데이터를 모델에 추가하여 학습 사례의 전체 크기를 늘립니다.  
  
-   이전 사례 데이터의 끝에서 예측을 시작합니다. 이에 따라 첫 두 예측은 모델에 방금 추가한 새로운 실제 판매 데이터를 나타냅니다.  
  
-   새로 확장된 모델을 기반으로 나머지 세 개의 시간 조각에 대한 새 예측을 반환합니다.  
  
 다음 표에서는 예 2 쿼리의 결과를 보여 줍니다. M200 Europe에 대해 반환된 첫 두 값은 사용자가 제공한 새 값과 동일합니다. 이 동작은 의도적인 것으로, 새 데이터의 끝 이후부터 예측을 시작하려면 시작 및 종료 시간 단계를 지정해야 합니다. 이 작업을 수행 하는 방법에 대 한 예제는 [5 단원: 시계열 모델 확장](https://msdn.microsoft.com/library/7aad4946-c903-4e25-88b9-b087c20cb67d)을 참조 하세요.  
  
 Pacific 지역에 대한 새 데이터도 제공하지 않았습니다. 따라서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 5개의 시간 조각 모두에 대해 새 예측을 반환합니다.  
  
 수량: 유럽 M200. EXTEND_MODEL_CASES:  
  
|$TIME|수량|  
|-----------|--------------|  
|7/25/2008 0:00|10|  
|8/25/2008 0:00|15|  
|9/25/2008 0:00|72|  
|10/25/2008 0:00|69|  
|11/25/2008 0:00|68|  
  
 수량: 태평양 M200. EXTEND_MODEL_CASES:  
  
|$TIME|수량|  
|-----------|--------------|  
|7/25/2008 0:00|46|  
|8/25/2008 0:00|44|  
|9/25/2008 0:00|42|  
|10/25/2008 0:00|42|  
|11/25/2008 0:00|38|  
  
## <a name="example-4-returning-statistics-in-a-time-series-prediction"></a>예 4: 시계열 예측에서 통계 반환  
 **PredictTimeSeries** 함수는 매개 변수로 *INCLUDE_STATISTICS* 을 지원 하지 않습니다. 그러나 다음 쿼리를 사용하면 시계열 쿼리에 대한 예측 통계를 반환할 수 있습니다. 이 방법은 중첩 테이블 열이 있는 모델에도 사용할 수 있습니다.  
  
 이 특정 모델에서 예측 가능한 특성은 Quantity 이므로 `[Quantity]` PredictTimeSeries 함수에 대 한 첫 번째 인수로를 사용 해야 합니다. 모델에서 다른 예측 가능한 특성을 사용하는 경우 다른 열 이름으로 대체할 수 있습니다.  
  
```  
SELECT FLATTENED [Model Region],  
(SELECT   
     $Time,  
     [Quantity] as [PREDICTION],   
     PredictVariance([Quantity]) AS [VARIANCE],  
     PredictStdev([Quantity]) AS [STDEV]  
FROM  
      PredictTimeSeries([Quantity], 3) AS t  
) AS t  
FROM Forecasting  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 North America'  
```  
  
 예제 결과:  
  
|Model Region|t.$TIME|t.PREDICTION|t.VARIANCE|t.STDEV|  
|------------------|-------------|------------------|----------------|-------------|  
|M200 Europe|7/25/2008 12:00:00 AM|121|11.6050581415597|3.40661975300439|  
|M200 Europe|8/25/2008 12:00:00 AM|142|10.678201866621|3.26775180615374|  
|M200 Europe|9/25/2008 12:00:00 AM|152|9.86897842568614|3.14149302493037|  
|M200 North America|7/25/2008 12:00:00 AM|163|1.20434529288162|1.20434529288162|  
|M200 North America|8/25/2008 12:00:00 AM|178|1.65031343900634|1.65031343900634|  
|M200 North America|9/25/2008 12:00:00 AM|156|1.68969399185442|1.68969399185442|  
  
> [!NOTE]  
>  이 예에서는 결과를 보다 쉽게 표 형식으로 나타낼 수 있도록 FLATTENED 키워드가 사용되었지만, 공급자에서 계층적 행 집합을 지원하는 경우 FLATTENED 키워드를 생략할 수 있습니다. FLATTENED 키워드를 생략하면 쿼리에서 두 개의 열이 반환됩니다. 첫 번째 열에는 `[Model Region]` 데이터 계열을 식별하는 값이 포함되고 두 번째 열에는 통계 중첩 테이블이 포함됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [시계열 모델 쿼리 예제](https://docs.microsoft.com/analysis-services/data-mining/time-series-model-query-examples)   
 [예측&#40;DMX&#41;](../dmx/predict-dmx.md)  
  
  
