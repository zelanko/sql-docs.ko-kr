---
title: "선형 회귀 모델 쿼리 예제 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- linear regression algorithms [Analysis Services]
- linear regression [Analysis Services]
- content queries [DMX]
ms.assetid: fd3cf312-57a1-44b6-b772-fce6fc1c26d7
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 150ef98bd2c949f7b4eb47170ec7855173608fbc
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="linear-regression-model-query-examples"></a>선형 회귀 모델 쿼리 예제
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
데이터 마이닝 모델에 대한 쿼리를 만들 때 분석 중에 발견된 패턴에 대한 세부 정보를 제공하는 내용 쿼리를 만들거나, 모델의 패턴을 사용하여 새 데이터에 대한 예측을 수행하는 예측 쿼리를 만들 수 있습니다. 예를 들어 내용 쿼리는 회귀 수식에 대한 추가 정보를 제공하지만 예측 쿼리는 새 데이터 요소가 모델에 맞는지 여부를 알려 줍니다. 쿼리를 사용하여 모델에 대한 메타데이터를 검색할 수도 있습니다.  
  
 이 섹션에서는 Microsoft 선형 회귀 알고리즘을 기반으로 하는 모델에 대해 쿼리를 만드는 방법을 설명합니다.  
  
> [!NOTE]  
>  선형 회귀는 Microsoft 의사 결정 트리 알고리즘의 특수한 사례를 기반으로 하므로 비슷한 점이 많으며, 예측 가능한 연속 특성을 사용하는 일부 의사 결정 트리 모델에는 회귀 수식이 포함될 수 있습니다. 자세한 내용은 [Microsoft 의사 결정 트리 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)를 참조하세요.  
  
 **내용 쿼리**  
  
 [데이터 마이닝 스키마 행 집합을 사용하여 모델에 사용되는 매개 변수 확인](#bkmk_Query1)  
  
 [DMX를 사용하여 모델의 회귀 수식 반환](#bkmk_Query2)  
  
 [모델의 계수만 반환](#bkmk_Query3)  
  
 **예측 쿼리**  
  
 [단일 쿼리를 사용하여 수입 예측](#bkmk_Query4)  
  
 [회귀 모델에 예측 함수 사용](#bkmk_Query5)  
  
##  <a name="bkmk_top"></a> 선형 회귀 모델에 대한 정보 찾기  
 선형 회귀 모델의 구조는 매우 단순하여 마이닝 모델은 데이터를 단일 노드로 나타내고 이 노드는 회귀 수식을 정의합니다. 자세한 내용은 [로지스틱 회귀 분석 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)를 참조하세요.  
  
 [맨 위로 이동](#bkmk_top)  
  
###  <a name="bkmk_Query1"></a> 예제 쿼리 1: 데이터 마이닝 스키마 행 집합을 사용하여 모델에 사용된 매개 변수 확인  
 데이터 마이닝 스키마 행 집합을 쿼리하면 모델에 대한 메타데이터를 찾을 수 있습니다. 이러한 메타데이터로는 모델이 만들어진 시기, 모델이 마지막으로 처리된 시기, 모델의 기반이 되는 마이닝 구조의 이름, 예측 가능한 특성으로 지정된 열 이름 등이 포함됩니다. 모델을 처음으로 만들 때 사용한 매개 변수를 반환할 수도 있습니다.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_PredictIncome'  
```  
  
 예제 결과:  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY=0.9,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MINIMUM_SUPPORT=10,<br /><br /> SCORE_METHOD=4,<br /><br /> SPLIT_METHOD=3,<br /><br /> FORCE_REGRESSOR=|  
  
> [!NOTE]  
>  매개 변수 설정 "`FORCE_REGRESSOR =` "는 FORCE_REGRESSOR 매개 변수의 현재 값이 Null임을 나타냅니다.  
  
 [맨 위로 이동](#bkmk_top)  
  
###  <a name="bkmk_Query2"></a> 예제 쿼리 2: 모델의 회귀 수식 검색  
 다음 쿼리는 [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)에서 사용한 타겟 메일링 데이터 원본을 사용하여 작성한 선형 회귀 모델의 마이닝 모델 콘텐츠를 반환합니다. 이 모델은 나이에 따른 고객 수입을 예측합니다.  
  
 이 쿼리는 회귀 수식이 들어 있는 노드의 콘텐츠를 반환합니다. 각 변수 및 계수는 NODE_DISTRIBUTION 중첩 테이블의 개별 행에 저장되어 있습니다. 전체 회귀 수식을 보려면 [Microsoft 트리 뷰어](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)에서 **(All)** 노드를 클릭하고 **마이닝 범례**를 엽니다.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION as t  
FROM LR_PredictIncome.CONTENT  
```  
  
> [!NOTE]  
>  `SELECT <column name> from NODE_DISTRIBUTION`과 같은 쿼리를 사용하여 중첩 테이블의 개별 열을 참조하는 경우 **SUPPORT** 또는 **PROBABILITY**등의 일부 열은 대괄호로 묶어 동일한 이름의 예약 키워드와 구별해야 합니다.  
  
 예상 결과:  
  
|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|1.|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
|Age|471.687717702463|0|0|126.969442359327|7|  
|Age|234.680904692439|0|0|0|8|  
|Age|45.4269617936399|0|0|126.969442359327|9|  
||35793.5477381267|0|0|1012968919.28372|11|  
  
 반면 **마이닝 범례**에서 회귀 수식은 다음과 같이 나타납니다.  
  
 `Yearly Income = 57,220.919 + 471.688 * (Age - 45.427)`  
  
 **마이닝 범례**에서는 일부 숫자가 반올림되는 것을 알 수 있지만 NODE_DISTRIBUTION 테이블과 **마이닝 범례** 에 들어 있는 값은 기본적으로 동일합니다.  
  
 VALUETYPE 열의 값은 각 행에 들어 있는 정보의 종류를 나타내며 이는 결과를 프로그래밍 방식으로 처리할 경우에 유용합니다. 다음 표에서는 선형 회귀 수식에 대해 출력되는 값 유형을 보여 줍니다.  
  
|VALUETYPE|  
|---------------|  
|1(누락)|  
|3(연속)|  
|7(계수)|  
|8(득점)|  
|9(통계)|  
|7(계수)|  
|8(득점)|  
|9(통계)|  
|11(절편)|  
  
 회귀 모델에 대한 각각의 값 형식의 의미는 [선형 회귀 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)를 참조하세요.  
  
 [맨 위로 이동](#bkmk_top)  
  
###  <a name="bkmk_Query3"></a> 예제 쿼리 3: 모델의 계수만 반환  
 다음 쿼리와 같이 VALUETYPE 열거형을 사용하면 회귀 수식의 계수만 반환할 수 있습니다.  
  
```  
SELECT FLATTENED MODEL_NAME,  
    (SELECT ATTRIBUTE_VALUE, VALUETYPE  
     FROM NODE_DISTRIBUTION  
     WHERE VALUETYPE = 11)   
AS t  
FROM LR_PredictIncome.CONTENT  
```  
  
 이 쿼리는 두 개의 행을 반환합니다. 하나는 마이닝 모델 콘텐츠에서 가져온 것이고 다른 하나는 계수가 들어 있는 중첩 테이블의 행에서 가져온 것입니다. 계수의 경우 ATTRIBUTE_NAME 열은 항상 비어 있으므로 이 열은 여기에 포함되지 않습니다.  
  
|MODEL_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|-----------------|------------------------|-----------------|  
|LR_PredictIncome|||  
|LR_PredictIncome|35793.5477381267|11|  
  
 [맨 위로 이동](#bkmk_top)  
  
## <a name="making-predictions-from-a-linear-regression-model"></a>선형 회귀 모델을 사용하여 예측 만들기  
 데이터 마이닝 디자이너의 마이닝 모델 예측 탭에서 선형 회귀 모델에 대한 예측 쿼리를 작성할 수 있습니다. 예측 쿼리 작성기는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 와 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 사용할 수 있습니다.  
  
> [!NOTE]  
>  Excel용 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터 마이닝 추가 기능이나 Excel용 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 데이터 마이닝 추가 기능을 사용하여 회귀 모델에 대한 쿼리를 만들 수도 있습니다. Excel용 데이터 마이닝 추가 기능은 회귀 모델을 만들지 않지만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스에 저장된 마이닝 모델을 찾아보고 쿼리할 수 있습니다.  
  
 [맨 위로 이동](#bkmk_top)  
  
###  <a name="bkmk_Query4"></a> 예제 쿼리 4: 단일 쿼리를 사용하여 수입 예측  
 회귀 모델에서 단일 쿼리를 만드는 가장 쉬운 방법은 **단일 쿼리 입력** 대화 상자를 사용하는 것입니다. 예를 들어 적절한 회귀 모델을 선택하고 **단일 쿼리**를 선택한 다음 **Age** 값으로 **20**을 입력하여 다음과 같은 DMX 쿼리를 작성할 수 있습니다.  
  
```  
SELECT [LR_PredictIncome].[Yearly Income]  
From   [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 예제 결과:  
  
|Yearly Income|  
|-------------------|  
|45227.302092176|  
  
 [맨 위로 이동](#bkmk_top)  
  
###  <a name="bkmk_Query5"></a> 예제 쿼리 5: 회귀 모델에 예측 함수 사용  
 선형 회귀 모델에 여러 표준 예측 함수를 사용할 수 있습니다. 다음 예에서는 예측 쿼리 결과에 기술 통계를 추가하는 방법을 보여 줍니다. 이러한 결과에서 이 모델의 평균과 상당한 편차가 있다는 것을 알 수 있습니다.  
  
```  
SELECT  
  ([LR_PredictIncome].[Yearly Income]) as [PredIncome],  
  (PredictStdev([LR_PredictIncome].[Yearly Income])) as [StDev1]  
From  
  [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 예제 결과:  
  
|Yearly Income|StDev1|  
|-------------------|------------|  
|45227.302092176|31827.1726561396|  
  
 [맨 위로 이동](#bkmk_top)  
  
## <a name="list-of-prediction-functions"></a>예측 함수 목록  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘은 공통 함수 집합을 지원합니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 선형 회귀 알고리즘은 다음 표에 나열된 추가 함수도 지원합니다.  
  
|||  
|-|-|  
|예측 함수|사용법|  
|[IsDescendant &#40; DMX &#41;](../../dmx/isdescendant-dmx.md)|한 노드가 모델에서 다른 노드의 자식인지 여부를 확인합니다.|  
|[IsInNode &#40; DMX &#41;](../../dmx/isinnode-dmx.md)|지정한 노드에 현재 사례가 포함되었는지 여부를 나타냅니다.|  
|[PredictHistogram &#40; DMX &#41;](../../dmx/predicthistogram-dmx.md)|지정한 열에 대한 예측 값을 반환합니다.|  
|[PredictNodeId &#40; DMX &#41;](../../dmx/predictnodeid-dmx.md)|각 사례에 대한 Node_ID를 반환합니다.|  
|[PredictStdev &#40; DMX &#41;](../../dmx/predictstdev-dmx.md)|예측 값의 표준 편차를 반환합니다.|  
|[PredictSupport &#40; DMX &#41;](../../dmx/predictsupport-dmx.md)|지정한 상태에 대한 지원 값을 반환합니다.|  
|[PredictVariance &#40; DMX &#41;](../../dmx/predictvariance-dmx.md)|지정한 열의 분산을 반환합니다.|  
  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘에 공통적인 함수 목록에 대해서는 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)을 참조하세요. 이러한 함수를 사용하는 방법은 [DMX&#40;Data Mining Extensions&#41; 함수 참조](../../dmx/data-mining-extensions-dmx-function-reference.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft 선형 회귀 알고리즘](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)   
 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft 선형 회귀 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)   
 [선형 회귀 모델 &#40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 &#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
