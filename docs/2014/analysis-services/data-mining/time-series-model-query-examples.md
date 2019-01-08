---
title: 시계열 모델 쿼리 예제 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time series algorithms [Analysis Services]
- MISSING_VALUE_SUBSTITUTION
- time series [Analysis Services]
- predictions [Analysis Services], time series
- EXTEND_MODEL_CASES parameter
- REPLACE_MODEL_CASES parameter
- prediction queries [DMX]
- PREDICTION_SMOOTHING
- content queries [DMX]
ms.assetid: 9a1c527e-2997-493b-ad6a-aaa71260b018
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4098a1b5eade3705e10ab609c47454564a18101d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511409"
---
# <a name="time-series-model-query-examples"></a>시계열 모델 쿼리 예제
  데이터 마이닝 모델에 대한 쿼리를 작성할 때 분석 중에 발견된 패턴에 대한 세부 정보를 제공하는 내용 쿼리를 작성하거나, 모델의 패턴을 사용하여 새 데이터에 대한 예측을 만드는 예측 쿼리를 작성할 수 있습니다. 예를 들어 시계열 모델에 대한 내용 쿼리는 검색된 주기 구조에 대한 추가 세부 정보를 제공할 수 있고 예측 쿼리는 다음 5-10개의 시간 조각에 대한 예측을 제공할 수 있습니다. 쿼리를 사용하여 모델에 대한 메타데이터를 검색할 수도 있습니다.  
  
 이 섹션에서는 Microsoft 시계열 알고리즘을 기반으로 하는 모델에 대해 이러한 두 종류의 쿼리를 만드는 방법에 대해 설명합니다.  
  
 **내용 쿼리**  
  
 [모델에 대한 주기 힌트 검색](#bkmk_Query1)  
  
 [ARIMA 모델에 대한 수식 검색](#bkmk_Query2)  
  
 [ARTxp 모델에 대한 수식 검색](#bkmk_Query3)  
  
 **예측 쿼리**  
  
 [시계열 데이터 대체 및 확장 시기 이해](#bkmk_ReplaceExtend)  
  
 [EXTEND_MODEL_CASES로 예측 수행](#bkmk_EXTEND)  
  
 [REPLACE_MODEL_CASES로 예측 수행](#bkmk_REPLACE)  
  
 [시계열 모델의 누락된 값 대체](#bkmk_MissingValues)  
  
## <a name="getting-information-about-a-time-series-model"></a>시계열 모델에 대한 정보 가져오기  
 모델 내용 쿼리는 모델을 만들 때 사용된 매개 변수, 모델이 마지막으로 처리된 시간 등과 같은 모델에 대한 기본 정보를 제공할 수 있습니다. 다음 예에서는 데이터 마이닝 스키마 행 집합을 사용하여 모델 콘텐츠를 쿼리하기 위한 기본 구문을 보여 줍니다.  
  
###  <a name="bkmk_Query1"></a> 예제 쿼리 1: 모델에 대한 주기 힌트 검색  
 ARIMA 트리나 ARTXP 트리를 쿼리하여 시계열 내에서 발견된 주기를 검색할 수 있습니다. 그러나 완성된 모델의 주기는 모델을 만들 때 힌트로 지정한 기간과 다를 수도 있습니다. 모델을 만들 때 매개 변수로 제공된 힌트를 검색하려면 다음 DMX 문을 사용하여 마이닝 모델 콘텐츠 스키마 행 집합을 쿼리합니다.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 일부 결과:  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY 0.1, MINIMUM_SUPPORT = = 10, PERIODICITY_HINT ={1,3},...|  
  
 기본 주기 힌트는 {1}이고 모든 모델에 나타납니다. 이 예제 모델은 최종 모델에 존재하지 않을 수도 있는 추가 힌트를 사용하여 만들어졌습니다.  
  
> [!NOTE]  
>  여기서는 읽기 쉽도록 결과를 잘라냈습니다.  
  
###  <a name="bkmk_Query2"></a> 예제 쿼리 2: ARIMA 모델에 대한 수식 검색  
 개별 트리에서 임의의 노드를 쿼리하여 ARIMA 모델에 대한 수식을 검색할 수 있습니다. ARIMA 모델 내의 각 트리는 다른 주기를 나타내며 여러 데이터 계열이 있는 경우 각 데이터 계열은 고유한 주기 트리 집합을 가집니다. 따라서 특정 데이터 계열에 대한 수식을 검색하려면 먼저 트리를 식별해야 합니다.  
  
 예를 들면 TA 접두사는 노드가 ARIMA 트리의 일부임을 나타내지만 TS 접두사는 ARTXP 트리에 사용됩니다. NODE_TYPE 값이 27인 노드의 모델 콘텐츠를 쿼리하여 모든 ARIMA 루트 트리를 찾을 수 있습니다. 또한 ATTRIBUTE_NAME 값을 사용하여 특정 데이터 계열에 대한 ARIMA 루트 노드를 찾을 수 있습니다. 이 쿼리 예는 유럽 지역에서 팔린 R250 모델의 수량을 나타내는 ARIMA 노드를 찾습니다.  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM Forecasting.CONTENT  
WHERE ATTRIBUTE_NAME = 'R250 Europe: Quantity"  
AND NODE_TYPE = 27  
```  
  
 이 노드 ID를 사용하여 이 트리의 ARIMA 수식에 대한 세부 사항을 검색할 수 있습니다. 다음 DMX 문은 데이터 계열에 대한 ARIMA 수식의 약식을 검색합니다. 또한 이 문은 중첩 테이블 NODE_DISTRIBUTION에서 절편을 검색합니다. 이 예에서 수식은 노드 고유의 ID TA00000007을 참조하여 얻습니다. 그러나 다른 노드 ID를 사용해야 하거나 모델에서 조금 다른 결과를 얻을 수 있습니다.  
  
```  
SELECT FLATTENED NODE_CAPTION as [Short equation],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE   
FROM NODE_DISTRIBUTION) as t  
FROM Forecasting.CONTENT  
WHERE NODE_NAME = 'TA00000007'  
```  
  
 예제 결과:  
  
|약식 수식|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|--------------------|-----------------------|------------------------|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Intercept)|15.24...|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|1|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|12|  
  
 이 정보를 해석하는 방법은 [시계열 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)를 참조하세요.  
  
###  <a name="bkmk_Query3"></a> 예제 쿼리 3: ARTXP 모델에 대한 수식 검색  
 ARTxp 모델의 경우 트리의 각 수준에 다른 정보가 저장됩니다. ARTxp 모델의 구조에 대한 자세한 내용과 수식에서 정보를 해석하는 방법은 [시계열 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)를 참조하세요.  
  
 다음 DMX 문은 유럽에서 R250 모델의 판매 수량을 나타내는 ARTxp 트리의 일부에 대한 정보를 검색합니다.  
  
> [!NOTE]  
>  중첩 테이블 열 이름인 VARIANCE는 동일한 이름의 예약 키워드와 구분하기 위해 대괄호로 묶어야 합니다. 중첩 테이블 열 PROBABILITY 및 SUPPORT는 대부분의 경우 비어 있으므로 포함되지 않습니다.  
  
```  
SELECT NODE_CAPTION as [Split information],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
   [VARIANCE]  
   FROM NODE_DISTRIBUTION) AS t  
FROM Forecasting.CONTENT  
WHERE NODE_ATTRIBUTE_NAME = 'R250 Europe:Quantity'  
AND NODE_TYPE = 15  
```  
  
 이 정보를 해석하는 방법은 [시계열 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)를 참조하세요.  
  
## <a name="creating-predictions-on-a-time-series-model"></a>시계열 모델에서 예측 만들기  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]이상의 버전에서는 시계열 모델에 새 데이터를 추가하고 새 데이터를 모델에 자동으로 수용할 수 있습니다. 다음 두 가지 방법 중 하나를 사용하여 시계열 마이닝 모델에 새 데이터를 추가할 수 있습니다.  
  
-   `PREDICTION JOIN`을 사용하여 외부 원본의 데이터를 학습 데이터에 조인합니다.  
  
-   단일 예측 쿼리를 사용하여 한 번에 한 조각씩 데이터를 제공합니다. 단일 예측 쿼리를 만드는 방법에 대 한 자세한 내용은 [데이터 마이닝 쿼리 인터페이스](data-mining-query-tools.md)합니다.  
  
###  <a name="bkmk_ReplaceExtend"></a> 바꾸기 및 확장 작업의 동작 이해  
 시계열 모델에 새 데이터를 추가할 때 학습 데이터를 확장할지 또는 대체할지 지정할 수 있습니다.  
  
-   **확장:** 데이터 계열을 확장하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 기존 학습 데이터의 끝에 새 데이터를 추가합니다. 학습 사례의 수도 증가합니다.  
  
     모델 사례 확장은 새 데이터로 계속해서 모델을 업데이트하는 경우 유용합니다. 예를 들어 시간이 지남에 따라 학습 집합이 증가하도록 하려는 경우 모델을 확장하면 됩니다.  
  
     데이터를 확장하려면 시계열 모델에 `PREDICTION JOIN`을 만들고 새 데이터의 원본을 지정하고 `EXTEND_MODEL_CASES` 인수를 사용합니다.  
  
-   **으로 바꿉니다.** 데이터 계열에서 데이터를 바꾸는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 학습된 된 모델을 유지 하지만 새 데이터 값을 사용 하 여 일부 또는 기존 학습 사례의 전체를 바꿉니다. 따라서 학습 데이터의 크기는 바뀌지 않지만 사례 자체는 더 새로운 데이터로 계속해서 대체됩니다. 새 데이터를 충분히 제공하면 완전히 새로운 계열로 학습 데이터를 대체할 수 있습니다.  
  
     모델 사례 대체는 하나의 사례 집합을 학습시킨 다음 이 모델을 다른 데이터 계열에 적용하려는 경우 유용합니다.  
  
     데이터를 대체하려면 시계열 모델에 `PREDICTION JOIN`을 만들고 새 데이터의 원본을 지정하고 `REPLACE_MODEL_CASES` 인수를 사용합니다.  
  
> [!NOTE]  
>  새 데이터를 추가할 때에는 기록 예측을 수행할 수 없습니다.  
  
 학습 데이터를 확장하든 대체하든 관계없이 예측은 항상 원래의 학습 집합을 종료하는 타임스탬프에 시작됩니다. 즉, 새 데이터에 n개의 시간 조각이 포함되어 있는 상태에서 시간 단계 1부터 n까지에 대한 예측을 요청할 경우 예측은 새 데이터와 동일한 기간에서 일치하게 되며 어떤 새로운 예측도 얻지 못합니다.  
  
 새 데이터와 겹치지 않는 시간 기간에 대한 새 예측을 구하려면 n+1 시간 조각에서 예측을 시작하거나 추가 시간 조각을 요청해야 합니다.  
  
 예를 들어 기존 모델에 6개월에 상당하는 데이터가 있다고 가정해 보겠습니다. 지난 3개월 동안의 판매 수치를 추가하여 이 모델을 확장하려고 합니다. 또한 이와 동시에 다음 3개월에 대한 예측을 수행하고자 합니다. 새 데이터를 추가하는 경우 새 예측만 구하려면 시작 지점을 시간 조각 4로, 끝 지점을 시간 조각 7로 지정합니다. 총 6개의 예측을 요청할 수도 있지만 처음 3개에 대한 시간 조각은 방금 추가한 새 데이터와 겹칩니다.  
  
 쿼리 예제 및 사용에 대 한 구문에 대 한 자세한 내용은 `REPLACE_MODEL_CASES` 하 고 `EXTEND_MODEL_CASES`를 참조 하십시오 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
###  <a name="bkmk_EXTEND"></a> EXTEND_MODEL_CASES로 예측 수행  
 예측 동작은 모델 사례를 확장하느냐, 대체하느냐에 따라 달라집니다. 모델을 확장하는 경우 새 데이터가 계열의 끝에 추가되며 학습 집합의 크기가 증가합니다. 그러나 예측 쿼리에 사용된 시간 조각은 항상 원래 계열의 끝에서 시작됩니다. 따라서 3개의 새 데이터 지점을 추가하고 6개의 예측을 요청할 경우 반환되는 첫 3개의 예측은 새 데이터와 겹칩니다. 이 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 모든 새 데이터 지점이 사용될 때까지 예측을 수행하지 않고 실제 새 데이터 지점을 반환합니다. 그런 다음 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 복합 계열을 기반으로 예측을 수행합니다.  
  
 이러한 동작 덕분에 새 데이터를 추가한 다음 추정을 보는 대신 예측 차트에 실제 판매 수치를 표시할 수 있습니다.  
  
 예를 들어 3개의 새 데이터 지점을 추가하고 3개의 새 예측을 수행하려면 다음과 같이 합니다.  
  
-   시계열 모델에 `PREDICTION JOIN`을 만들고 새로운 3개월 데이터의 원본을 지정합니다.  
  
-   6개의 시간 조각에 대한 예측을 요청합니다. 이렇게 하려면 6개의 시간 조각을 지정합니다. 여기에서 시작 지점은 시간 조각 1, 종료 지점은 시간 조각 7입니다. 이는 EXTEND_MODEL_CASES에만 해당합니다.  
  
-   새 예측만 구하려면 시작 지점을 4로 지정하고 종료 지점을 7로 지정합니다.  
  
-   `EXTEND_MODEL_CASES` 인수를 사용해야 합니다.  
  
     실제 판매 수치는 처음 3개의 시간 조각에 대해서 반환되며, 확장된 모델 기반의 예측은 다음 3개의 시간 조각에 대해 반환됩니다.  
  
###  <a name="bkmk_REPLACE"></a> REPLACE_MODEL_CASES로 예측 수행  
 모델의 사례를 대체하는 경우 모델의 크기는 그대로 유지되지만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 모델의 개별 사례를 대체합니다. 이는 학습 데이터 집합을 일정한 크기로 유지하는 것이 중요한 시나리오와 교차 예측에 유용합니다.  
  
 예를 들어 매장 중 하나의 판매 데이터가 충분하지 않다고 가정해 보겠습니다. 특정 지역의 모든 매장에 대한 판매의 평균을 구하여 일반 모델을 만든 다음 모델을 학습시킬 수 있습니다. 그런 다음 충분한 판매 데이터가 없는 매장에 대해 예측을 수행하려면 해당 매장에 대한 새 판매 데이터에 `PREDICTION JOIN`을 만듭니다. 이렇게 하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 지역 모델에서 파생된 패턴을 유지하되 기존 학습 사례를 개별 매장의 데이터로 대체합니다. 그 결과 예측 값은 개별 매장에 대한 추세 선에 근접하게 됩니다.  
  
 `REPLACE_MODEL_CASES` 인수를 사용하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 사례 집합의 끝에 새 사례를 계속해서 추가하고 해당되는 수만큼을 사례 집합의 시작부터 삭제합니다. 원래의 학습 집합에서보다 더 많은 수의 새 데이터를 추가할 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 가장 앞선 데이터를 버립니다. 새 값을 충분히 제공하면 예측은 완전히 새로운 데이터를 기반으로 할 수 있습니다.  
  
 예를 들어 1000개의 행을 포함하는 사례 데이터 집합에서 모델을 학습시켰습니다. 그 후 100개 행의 새 데이터를 추가합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 총 1000개의 행이 되도록 학습 집합에서 처음 100개의 행을 삭제하고 집합의 끝에 100개 행의 새 데이터를 추가합니다. 1100개 행의 새 데이터를 추가할 경우 최근 순서대로 1000개 행만 사용됩니다.  
  
 다른 예를 살펴보겠습니다. 3개월 분량의 새 데이터를 추가하고 3개의 새로운 예측을 수행하려면 다음과 같이 합니다.  
  
-   시계열 모델에 `PREDICTION JOIN`을 만들고 `REPLACE_MODEL_CASE` 인수를 사용합니다.  
  
-   3개월 분 새 데이터의 원본을 지정합니다. 이 데이터는 원래의 학습 데이터와 완전히 다른 원본에서 가져올 수 있습니다.  
  
-   6개의 시간 조각에 대한 예측을 요청합니다. 이렇게 하려면 6개의 시간 조각을 지정하거나 시작 지점은 시간 조각 1, 종료 지점은 시간 조각 7로 지정합니다.  
  
    > [!NOTE]  
    >  `EXTEND_MODEL_CASES`와 달리 입력 데이터로 추가한 값과 동일한 값은 반환할 수 없습니다. 반환되는 6개 값 모두는 기존 데이터와 새 데이터를 모두 포함하는 업데이트된 모델을 기반으로 하는 예측입니다.  
  
    > [!NOTE]  
    >  타임스탬프 1에서 시작하는 REPLACE_MODEL_CASES를 사용하면 이전 학습 데이터를 대체하는 새 데이터에 기반한 새 예측을 얻게 됩니다.  
  
 쿼리 예제 및 사용에 대 한 구문에 대 한 자세한 내용은 `REPLACE_MODEL_CASES` 하 고 `EXTEND_MODEL_CASES`를 참조 하십시오 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
###  <a name="bkmk_MissingValues"></a> 시계열 모델의 누락된 값 대체  
 `PREDICTION JOIN` 문을 사용하여 시계열 모델에 새 데이터를 추가하는 경우 새 데이터 집합에는 누락되는 값이 있을 수 없습니다. 완전하지 않은 계열이 있는 경우 모델은 null, 숫자 평균, 특정 숫자 평균 또는 예측된 값 중 하나를 사용하여 누락된 값을 제공해야 합니다. `EXTEND_MODEL_CASES`를 지정하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 원래 모델 기반의 예측으로 누락된 값을 대체합니다. 사용 하는 경우 `REPLACE_MODEL_CASES`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 지정 하는 값을 사용 하 여 누락 값을 대체 합니다 *MISSING_VALUE_SUBSTITUTION* 매개 변수입니다.  
  
## <a name="list-of-prediction-functions"></a>예측 함수 목록  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘은 공통 함수 집합을 지원합니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘은 다음 표에 나열된 함수를 추가로 지원합니다.  
  
|||  
|-|-|  
|예측 함수|사용법|  
|[Lag&#40;DMX&#41;](/sql/dmx/lag-dmx)|현재 사례의 날짜와 학습 집합의 마지막 날짜 간의 시간 조각을 여러 개 반환합니다.<br /><br /> 이 함수는 일반적으로 최근 학습 사례를 식별하여 해당 사례에 대한 자세한 데이터를 검색하는 데 사용됩니다.|  
|[PredictNodeId & #40; DMX & #41;](/sql/dmx/predictnodeid-dmx)|지정된 예측 가능한 열의 노드 ID를 반환합니다.<br /><br /> 이 함수는 일반적으로 특정 예측 값을 생성한 노드를 식별하여 노드와 관련된 사례를 검토하거나 수식 및 다른 세부 정보를 검색하는데 사용됩니다.|  
|[PredictStdev & #40; DMX & #41;](/sql/dmx/predictstdev-dmx)|지정된 예측 가능한 열에서 예측의 표준 편차를 반환합니다.<br /><br /> 이 함수는 시계열 모델을 지원하지 않는 INCLUDE_STATISTICS 인수를 대체합니다.|  
|[PredictVariance & #40; DMX & #41;](/sql/dmx/predictvariance-dmx)|지정된 예측 가능한 열에 대한 예측의 분산을 반환합니다.<br /><br /> 이 함수는 시계열 모델을 지원하지 않는 INCLUDE_STATISTICS 인수를 대체합니다.|  
|[PredictTimeSeries&#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)|시계열에 대한 예상 기록 값 또는 미래 예상 값을 반환합니다.<br /><br /> 일반 예측 함수인 [Predict&#40;DMX&#41;](/sql/dmx/predict-dmx)를 사용하여 시계열 모델을 쿼리할 수도 있습니다.|  
  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘에 공통된 함수 목록은 [일반 예측 함수&#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx)를 참조하세요. 특정 함수의 구문은 [DMX&#40;Data Mining Extensions&#41; 함수 참조](/sql/dmx/data-mining-extensions-dmx-function-reference)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 쿼리](data-mining-queries.md)   
 [Microsoft 시계열 알고리즘](microsoft-time-series-algorithm.md)   
 [Microsoft 시계열 알고리즘 기술 참조](microsoft-time-series-algorithm-technical-reference.md)   
 [시계열 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
