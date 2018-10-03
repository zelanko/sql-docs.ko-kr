---
title: 신경망 모델 쿼리 예제 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- neural network algorithms [Analysis Services]
- content queries [DMX]
- neural network model [Analysis Services]
ms.assetid: 81b06183-620f-4e0c-bc10-532e6a1f0829
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ed0ba22087a12f08e7a951a89a7ca989bb6487f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48110601"
---
# <a name="neural-network-model-query-examples"></a>신경망 모델 쿼리 예제
  데이터 마이닝 모델에 대한 쿼리를 작성할 때 분석 중에 발견된 패턴에 대한 세부 정보를 제공하는 내용 쿼리를 작성하거나, 모델의 패턴을 사용하여 새 데이터에 대한 예측을 만드는 예측 쿼리를 작성할 수 있습니다. 예를 들어 신경망 모델에 대한 내용 쿼리에서는 숨겨진 계층 수와 같은 모델 메타데이터를 검색할 수 있습니다. 또한 예측 쿼리는 입력에 따른 분류를 제안하고 선택적으로 각 분류에 대한 확률을 제공할 수 있습니다.  
  
 이 섹션에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 신경망 알고리즘을 기반으로 하는 모델에 대해 쿼리를 만드는 방법을 설명합니다.  
  
 **내용 쿼리**  
  
 [DMX를 사용하여 모델 메타데이터 가져오기](#bkmk_Query1)  
  
 [스키마 행 집합에서 모델 메타데이터 검색](#bkmk_Query2)  
  
 [모델에 대한 입력 특성 검색](#bkmk_Query3)  
  
 [숨겨진 계층에서 가중치 검색](#bkmk_Query4)  
  
 **예측 쿼리**  
  
 [단일 예측 만들기](#bkmk_Query5)  
  
## <a name="finding-information-about-a-neural-network-model"></a>신경망 모델에 대한 정보 찾기  
 모든 마이닝 모델은 마이닝 모델 스키마 행 집합이라고 하는 표준화된 스키마에 따라, 알고리즘을 통해 학습한 내용을 표시합니다. 이 정보는 기본 메타데이터, 분석 시 발견된 구조 및 처리할 때 사용된 매개 변수를 포함하여 모델에 대한 세부 정보를 제공합니다. 모델 콘텐츠에 대한 쿼리는 DMX(Data Mining Extensions) 문을 사용하여 만들 수 있습니다.  
  
###  <a name="bkmk_Query1"></a> 예제 쿼리 1: DMX를 사용하여 모델 메타데이터 가져오기  
 다음 쿼리는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 신경망 알고리즘을 사용하여 작성한 모델에 대한 몇 가지 기본 메타데이터를 반환합니다. 신경망 모델에서 모델의 부모 노드에는 모델의 이름, 모델이 저장된 데이터베이스의 이름 및 자식 노드의 수만 들어 있습니다. 그러나 marginal statistics node(NODE_TYPE = 24)는 이 기본 메타데이터와 모델에 사용된 입력 열에 대한 몇 가지 파생된 통계를 모두 제공합니다.  
  
 다음 예제 쿼리는 [중급 데이터 마이닝 자습서](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)에서 만든 `Call Center Default NN`이라고 하는 마이닝 모델을 기반으로 합니다. 이 모델은 콜 센터의 데이터를 사용하여 직원 배치, 호출 수, 주문 수 및 문제 수 간의 가능한 상관 관계를 탐색합니다. DMX 문은 신경망 모델의 marginal statistics node에서 데이터를 검색합니다. 관심 있는 입력 특성 통계가 NODE_DISTRIBUTION 중첩 테이블에 저장되어 있으므로 이 쿼리에는 FLATTENED 키워드가 포함됩니다. 그러나 쿼리 공급자가 계층적 행 집합을 지원하는 경우에는 FLATTENED 키워드를 사용할 필요가 없습니다.  
  
```  
SELECT FLATTENED MODEL_CATALOG, MODEL_NAME,   
(    SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
     [SUPPORT], [PROBABILITY], VALUETYPE   
     FROM NODE_DISTRIBUTION  
) AS t  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 24  
```  
  
> [!NOTE]  
>  중첩 테이블 열 이름인 `[SUPPORT]` 및 `[PROBABILITY]`는 대괄호로 묶어 동일한 이름의 예약 키워드와 구별해야 합니다.  
  
 예제 결과:  
  
|MODEL_CATALOG|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|--------------------|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Average Time Per Issue|Missing|0|0|1|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Average Time Per Issue|< 64.7094100096|11|0.407407407|5|  
  
 신경망 모델의 컨텍스트에서 의미 스키마 행 집합의 열 정의 참조 하세요 [마이닝 모델 콘텐츠 신경망 모델에 대 한 &#40;Analysis Services-데이터 마이닝&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)합니다.  
  
###  <a name="bkmk_Query2"></a> 예제 쿼리 2: 스키마 행 집합에서 모델 메타데이터 검색  
 데이터 마이닝 스키마 행 집합을 쿼리하여 DMX 내용 쿼리에 반환되는 것과 동일한 정보를 찾을 수 있는데, 스키마 행 집합은 몇 개의 열을 추가로 제공합니다. 다음 예제 쿼리에서는 모델이 생성되고 수정되고 마지막으로 처리된 날짜를 반환합니다. 또한 이 쿼리에서는 모델 콘텐츠에서 쉽게 사용할 수 없는 예측 가능한 열과 모델을 작성하는 데 사용된 매개 변수에 대한 세부 정보도 반환합니다. 이 정보는 모델을 문서화하는 데 유용할 수 있습니다.  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center Default NN'  
```  
  
 예제 결과:  
  
|||  
|-|-|  
|MODEL_NAME|Call Center Default NN|  
|DATE_CREATED|1/10/2008 5:07:38 PM|  
|LAST_PROCESSED|1/10/2008 5:24:02 PM|  
|PREDICTION_ENTITY|Average Time Per Issue,<br /><br /> Grade Of Service,<br /><br /> Number Of Orders|  
|MINING_PARAMETERS|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=0,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100, SAMPLE_SIZE=10000, HIDDEN_NODE_RATIO=4|  
  
###  <a name="bkmk_Query3"></a> 예제 쿼리 3: 모델에 대한 입력 특성 검색  
 입력 계층(NODE_TYPE = 18)의 자식 노드(NODE_TYPE = 20)를 쿼리하여 모델을 만드는 데 사용된 정확한 입력 특성-값 쌍을 검색할 수 있습니다. 다음 쿼리는 노드 설명에서 입력 특성 목록을 반환합니다.  
  
```  
SELECT NODE_DESCRIPTION  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 예제 결과:  
  
|NODE_DESCRIPTION|  
|-----------------------|  
|Average Time Per Issue=64.7094100096 - 77.4002099712|  
|Day Of Week=Fri.|  
|Level 1 Operators|  
  
 여기에는 결과에 포함된 행 중 일부 대표 행만 표시되어 있습니다. 그러나 NODE_DESCRIPTION이 입력 특성의 데이터 형식에 따라 약간씩 다른 정보를 제공한다는 것을 알 수 있습니다.  
  
-   특성이 불연속 값 또는 불연속화된 값인 경우 특성과 해당 값 또는 불연속화된 범위가 반환됩니다.  
  
-   특성이 연속 숫자 데이터 형식일 경우에는 NODE_DESCRIPTION에 특성 이름만 포함됩니다. 그러나 NODE_DISTRIBUTION 중첩 테이블을 검색하여 평균을 가져오거나 NODE_RULE을 반환하여 숫자 범위의 최소값 및 최대값을 가져올 수 있습니다.  
  
 다음 쿼리에서는 NODE_DISTRIBUTION 중첩 테이블을 쿼리하여 한 열에 있는 특성과 다른 열에 있는 해당 특성의 값을 반환하는 방법을 보여 줍니다. 연속 특성의 경우에는 특성 값은 특성 평균으로 나타냅니다.  
  
```  
SELECT FLATTENED   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE  
FROM NODE_DISTRIBUTION) as t  
FROM [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 21  
```  
  
 예제 결과:  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|-----------------------|------------------------|  
|Average Time Per Issue|64.7094100096 - 77.4002099712|  
|Day Of Week|Fri.|  
|Level 1 Operators|3.2962962962963|  
  
 최소 및 최대 범위 값은 NODE_RULE 열에 저장되어 있으며 다음 예에 표시된 것과 같이 XML 조각으로 표현됩니다.  
  
```  
<NormContinuous field="Level 1 Operators">    
  <LinearNorm orig="2.83967303681711" norm="-1" />    
  <LinearNorm orig="3.75291955577548" norm="1" />    
</NormContinuous>    
```  
  
###  <a name="bkmk_Query4"></a> 예제 쿼리 4: 숨겨진 계층에서 가중치 검색  
 신경망 모델의 모델 콘텐츠는 네트워크의 모든 노드에 대한 세부 정보를 쉽게 가져올 수 있도록 구조화되어 있습니다. 또한 노드의 ID 번호는 노드 유형 간의 관계를 파악하는 데 도움이 되는 정보를 제공합니다.  
  
 다음 쿼리에서는 숨겨진 계층의 특정 노드에 저장된 계수를 검색하는 방법을 보여 줍니다. 숨겨진 계층은 메타데이터만 포함하는 구성 도우미 노드(NODE_TYPE = 19)와 특성 및 값의 다양한 조합에 대한 계수를 포함하는 여러 자식 노드(NODE_TYPE = 22)로 구성됩니다. 이 쿼리에서는 계수 노드만 반환합니다.  
  
```  
SELECT FLATTENED TOP 1 NODE_UNIQUE_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM  [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 22  
AND [PARENT_UNIQUE_NAME] = '40000000200000000' FROM [Call Center Default NN].CONTENT  
```  
  
 예제 결과:  
  
|NODE_UNIQUE_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|------------------------|-----------------------|------------------------|-----------------|  
|70000000200000000|6000000000000000a|-0.178616518|7|  
|70000000200000000|6000000000000000b|-0.267561918|7|  
|70000000200000000|6000000000000000c|0.11069497|7|  
|70000000200000000|6000000000000000d|0.123757712|7|  
|70000000200000000|6000000000000000e|0.294565343|7|  
|70000000200000000|6000000000000000f|0.22245318|7|  
|70000000200000000||0.188805045|7|  
  
 여기에 표시된 일부 결과는 신경망 모델 콘텐츠에서 숨겨진 노드가 입력 노드에 관련되는 방식을 보여 줍니다.  
  
-   숨겨진 계층에 있는 노드의 고유 이름은 항상 70000000으로 시작합니다.  
  
-   입력 계층에 있는 노드의 고유 이름은 항상 60000000으로 시작합니다.  
  
 따라서 이러한 결과를 보면 ID 70000000200000000으로 표시된 노드에는 6개의 다른 계수(VALUETYPE = 7)가 전달되었음을 알 수 있습니다. 계수 값은 ATTRIBUTE_VALUE 열에 있습니다. ATTRIBUTE_NAME 열의 노드 ID를 사용하면 해당 계수가 어떤 입력 특성에 대한 계수인지 확인할 수 있습니다. 예를 들어 노드 ID 6000000000000000a는 입력 특성 및 값 `Day of Week = 'Tue.'` 를 참조합니다. 이 노드 ID를 사용하여 쿼리를 만들거나, [Microsoft 일반 콘텐츠 트리 뷰어](../microsoft-generic-content-tree-viewer-data-mining.md)를 사용하여 이 노드를 찾아볼 수 있습니다.  
  
 마찬가지로 출력 계층(NODE_TYPE = 23)에 있는 노드의 NODE_DISTRIBUTION 테이블을 쿼리하면 각 출력 값의 계수를 확인할 수 있습니다. 그러나 출력 계층에서 포인터는 다시 숨겨진 계층의 노드를 참조합니다. 자세한 내용은 [마이닝 모델 콘텐츠 신경망 모델에 대 한 &#40;Analysis Services-데이터 마이닝&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)합니다.  
  
## <a name="using-a-neural-network-model-to-make-predictions"></a>신경망 모델을 사용하여 예측 만들기  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 신경망 알고리즘은 분류와 회귀를 모두 지원합니다. 이러한 모델에서 예측 함수를 사용하여 새 데이터를 제공하고 단일 또는 일괄 처리 예측을 만들 수 있습니다.  
  
###  <a name="bkmk_Query5"></a> 예측 쿼리 5: 단일 예측 쿼리 만들기  
 신경망 모델에 대한 예측 쿼리를 작성하는 가장 쉬운 방법은 **와** 의 데이터 마이닝 디자이너에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 마이닝 모델 예측 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]탭에 제공되는 예측 쿼리 작성기를 사용하는 것입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 신경망 뷰어에서 모델을 찾아서 관심 있는 특성을 필터링하고 추세를 확인한 다음 **마이닝 모델 예측** 탭으로 전환하여 쿼리를 만들고 해당 추세에 대한 새 값을 예측할 수 있습니다.  
  
 예를 들어 콜 센터 모델을 찾아서 주문량과 다른 특성 간의 상관 관계를 확인할 수 있습니다. 이 위해 열고 모델 뷰어에서 **입력**를 선택  **\<모든 >** 합니다.  그런 다음 **출력**에서 **Number of Orders**를 선택합니다. **값 1**에서 가장 많은 주문 횟수를 나타내는 범위를 선택하고 **값 2**에서 가장 적은 주문 횟수를 나타내는 범위를 선택합니다. 그러면 해당 모델에서 주문량과 상관 관계가 있는 모든 특성을 한눈에 볼 수 있습니다.  
  
 뷰어에서 결과를 보면 특정 요일에 주문량이 적고 운영자의 수를 늘릴수록 판매량이 많아지는 상관 관계가 있다는 것을 알 수 있습니다. 그런 다음 모델에 대한 예측 쿼리를 사용하여 "가상 분석" 가설을 테스트하고 주문량이 적은 요일의 수준 2 운영자 수를 늘리면 주문이 늘어날지 예측할 수 있습니다. 이렇게 하려면 다음과 같은 쿼리를 만듭니다.  
  
```  
SELECT Predict([Call Center Default NN].[Number of Orders]) AS [Predicted Orders],  
PredictProbability([Call Center Default NN].[Number of Orders]) AS [Probability]  
FROM [Call Center Default NN]  
NATURAL PREDICTION JOIN   
(SELECT 'Tue.' AS [Day of Week],  
13 AS [Level 2 Operators]) AS t  
```  
  
 예제 결과:  
  
|Predicted Orders|Probability|  
|----------------------|-----------------|  
|364|0.9532…|  
  
 예측된 판매량은 화요일의 현재 판매량 범위보다 높으며 예측 확률은 매우 높습니다. 그러나 일괄 처리를 통해 여러 개의 예측을 만들어 모델에 대한 다양한 가설을 테스트할 수도 있습니다.  
  
> [!NOTE]  
>  Excel 2007용 데이터 마이닝 추가 기능에서는 로지스틱 회귀 마법사를 제공하기 때문에 서비스 등급을 특정 교대조에 대한 대상 수준으로 개선하는 데 필요한 두 번째 수준의 전화 상담원의 수와 같은 복잡한 질문에 보다 쉽게 대답할 수 있습니다. 데이터 마이닝 추가 기능은 무료로 다운로드할 수 있으며 신경망 및/또는 로지스틱 회귀 알고리즘을 기반으로 하는 마법사를 포함합니다. 자세한 내용은 [Data Mining Add-ins for Office 2007](http://go.microsoft.com/fwlink/?LinkID=117790) (Office 2007용 데이터 마이닝 추가 기능) 웹 사이트를 참조하세요.  
  
## <a name="list-of-prediction-functions"></a>예측 함수 목록  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘은 공통 함수 집합을 지원합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 신경망 알고리즘에만 사용되는 예측 함수는 없지만 이 알고리즘은 다음 표에 나열된 함수를 지원합니다.  
  
|||  
|-|-|  
|예측 함수|사용법|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|한 노드가 신경망 그래프에서 다른 노드의 자식인지 여부를 확인합니다.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|가중치 확률을 반환합니다.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|현재 예측된 값과 관련 된 값의 테이블을 반환 합니다.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|예측 값의 분산을 반환합니다.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|예측 값의 확률을 반환합니다.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|예측 값의 표준 편차를 반환합니다.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|신경망 및 로지스틱 회귀 모델의 경우에는 모델 전체에 대한 학습 집합의 크기를 나타내는 단일 값을 반환합니다.|  
  
 특정 함수의 구문은 [DMX&#40;Data Mining Extensions&#41; 함수 참조](/sql/dmx/data-mining-extensions-dmx-function-reference)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 신경망 알고리즘](microsoft-neural-network-algorithm.md)   
 [Microsoft 신경망 알고리즘 기술 참조](microsoft-neural-network-algorithm-technical-reference.md)   
 [마이닝 모델 콘텐츠 신경망 모델에 대 한 &#40;Analysis Services-데이터 마이닝&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [5 단원: 신경망 및 로지스틱 회귀 모델 작성 &#40;중급 데이터 마이닝 자습서&#41;](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
  
