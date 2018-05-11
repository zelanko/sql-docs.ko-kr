---
title: 로지스틱 회귀 모델 쿼리 예제 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 52889e51b4492907b6b9293bb84ab46a256ad944
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="logistic-regression-model-query-examples"></a>로지스틱 회귀 모델 쿼리 예제
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  데이터 마이닝 모델에 대한 쿼리를 작성할 때 분석 중에 발견된 패턴에 대한 세부 정보를 제공하는 내용 쿼리를 작성하거나, 모델의 패턴을 사용하여 새 데이터를 사용한 예측을 만드는 예측 쿼리를 작성할 수 있습니다.  
  
 이 섹션에서는 Microsoft 로지스틱 회귀 알고리즘을 기반으로 하는 모델에 대해 쿼리를 만드는 방법을 설명합니다.  
  
 **내용 쿼리**  
  
 [데이터 마이닝 스키마 행 집합을 사용하여 모델 매개 변수 검색](#bkmk_Query1)  
  
 [DMX를 사용하여 모델에 대한 추가 세부 정보 찾기](#bkmk_Query2)  
  
 **예측 쿼리**  
  
 [연속 값에 대한 예측 만들기](#bkmk_Query3)  
  
 [불연속 값에 대한 예측 만들기](#bkmk_Query4)  
  
##  <a name="bkmk_top"></a> 로지스틱 회귀 모델에 대한 정보 가져오기  
 로지스틱 회귀 모델은 Microsoft 신경망 알고리즘과 특수한 매개 변수 집합을 사용하여 만듭니다. 따라서 로지스틱 회귀 모델은 신경망 모델과 동일한 정보를 일부 포함하지만 신경망 모델보다는 덜 복잡합니다. 모델 콘텐츠의 구조와 노드 유형에 따라 저장되는 정보의 종류를 이해하려면 [로지스틱 회귀 분석 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)를 참조하세요.  
  
 중급 데이터 마이닝 자습서의 [5단원: 신경망 및 로지스틱 회귀 모델 작성&#40;중급 데이터 마이닝 자습서&#41;](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b) 섹션에서 설명하는 대로 로지스틱 회귀 모델을 만들어 쿼리 시나리오를 연습할 수 있습니다.  
  
 [기본 데이터 마이닝 자습서](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)의 마이닝 구조인 타겟 메일링을 사용할 수도 있습니다.  
  
```  
ALTER MINING STRUCTURE [Targeted Mailing]  
ADD MINING MODEL [TM_Logistic Regression]  
([Customer Key],  
[Age],  
[Bike Buyer] PREDICT,  
[Yearly Income] PREDICT,  
[Commute Distance],  
[English Education],  
Gender,  
[House Owner Flag],  
[Marital Status],  
[Number Cars Owned],  
[Number Children At Home],  
[Region],  
[Total Children]  
)  
USING Microsoft_Logistic_Regression  
```  
  
###  <a name="bkmk_Query1"></a> 예제 쿼리 1: 데이터 마이닝 스키마 행 집합을 사용하여 모델 매개 변수 검색  
 데이터 마이닝 스키마 행 집합을 쿼리하면 모델이 만들어진 날짜, 모델이 마지막으로 처리된 날짜, 모델의 기반이 되는 마이닝 구조의 이름, 예측 가능한 특성으로 사용된 열 이름 등 모델에 대한 메타데이터를 찾을 수 있습니다. 다음 예에서는 모델을 처음 만들 때 사용한 매개 변수와 함께 모델의 이름, 유형 및 작성 날짜를 반환합니다.  
  
```  
SELECT MODEL_NAME, SERVICE_NAME, DATE_CREATED, MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center_LR'  
```  
  
 예제 결과:  
  
|MODEL_NAME|SERVICE_NAME|DATE_CREATED|MINING_PARAMETERS|  
|-----------------|-------------------|-------------------|------------------------|  
|Call Center_LR|Microsoft_Logistic_Regression|04/07/2009 20:38:33|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=1, MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255, MAXIMUM_STATES=100, SAMPLE_SIZE=10000|  
  
###  <a name="bkmk_Query2"></a> 예제 쿼리 2: DMX를 사용하여 모델에 대한 추가 세부 정보 찾기  
 다음 쿼리에서는 로지스틱 회귀 모델에 대한 몇 가지 기본 정보를 반환합니다. 로지스틱 회귀 모델은 입력으로 사용된 값을 설명하는 한계 통계 노드(NODE_TYPE = 24)가 있다는 점을 비롯하여 여러 면에서 신경망 모델과 비슷합니다. 이 예제 쿼리에서는 Targeted Mailing 모델을 사용하며 NODE_DISTRIBUTION이라는 중첩 테이블에서 값을 검색해 모든 입력의 값을 가져옵니다.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM [TM_Logistic Regression].CONTENT   
```  
  
 일부 결과:  
  
|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Age|Missing|0|0|0|1.|  
|Age|45.43491192|17484|1.|126.9544114|3|  
|Bike Buyer|Missing|0|0|0|1.|  
|Bike Buyer|0|8869|0.507263784|0|4|  
|Bike Buyer|1.|8615|0.492736216|0|4|  
|Commute Distance|Missing|0|0|0|1.|  
|Commute Distance|5-10 Miles|3033|0.173472889|0|4|  
  
 실제 쿼리는 보다 많은 행을 반환하지만 이 예제에서는 입력에 대해 제공된 정보 유형을 보여 줍니다. 불연속 입력에 가능한 각 값은 테이블에 나열됩니다. Age와 같은 연속 값 입력의 경우 전체를 나열하는 것이 가능하지 않으므로 입력이 평균값으로 불연속화됩니다. 한계 통계 노드의 정보를 사용하는 방법에 대한 자세한 내용은 [로지스틱 회귀 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)를 참조하세요.  
  
> [!NOTE]  
>  이 결과는 보기 쉽도록 평면화되었지만 사용 중인 공급자가 계층적 행 집합을 지원하는 경우에는 중첩 테이블을 단일 열에 반환할 수 있습니다.  
  
## <a name="prediction-queries-on-a-logistic-regression-model"></a>로지스틱 회귀 모델에 대한 예측 쿼리  
 모든 종류의 마이닝 모델에 [Predict&#40;DMX&#41;](../../dmx/predict-dmx.md) 함수를 사용하여 모델에 새 데이터를 제공하고 새 값을 기반으로 예측을 만들 수 있습니다. 함수를 사용하여 예측이 올바를 확률 등 예측에 대한 추가 정보를 반환할 수도 있습니다. 이 섹션에서는 로지스틱 회귀 모델에 대한 예측 쿼리의 몇 가지 예를 제공합니다.  
  
###  <a name="bkmk_Query3"></a> 예제 쿼리 3: 연속 값에 대한 예측 만들기  
 로지스틱 회귀에서는 입력 및 예측 모두에 연속 특성을 사용할 수 있으므로 데이터에 포함된 다양한 요소와 상관 관계가 있는 모델을 쉽게 만들 수 있습니다. 예측 쿼리를 사용하여 이러한 요소 간의 관계를 탐색할 수 있습니다.  
  
 다음 예제 쿼리는 중급 자습서에서 만든 콜 센터 모델을 기반으로 하며 금요일 오전 근무조의 서비스 등급을 예측하는 단일 쿼리를 만듭니다. [PredictHistogram(DMX)](../../dmx/predicthistogram-dmx.md) 함수는 예측 값의 유효성을 이해하는 데 관련된 통계를 제공하는 중첩 테이블을 반환합니다.  
  
```  
SELECT  
  Predict([Call Center_LR].[Service Grade]) as Predicted ServiceGrade,  
  PredictHistogram([Call Center_LR].[Service Grade]) as [Results],  
FROM  
  [Call Center_LR]  
NATURAL PREDICTION JOIN  
(SELECT 'Friday' AS [Day Of Week],  
  'AM' AS [Shift]) AS t  
```  
  
 예제 결과:  
  
|Predicted Service Grade|Service Grade|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-----------------------------|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.102601830123659|0.102601830123659|83.0232558139535|0.988372093023256|0|0.00120552660600087|0.034720694203902|  
|||0.976744186046512|0.0116279069767442|0.0116279069767442|0|0|  
  
 중첩 NODE_DISTRIBUTION 테이블의 확률, 지지도 및 표준 편차 값에 대한 자세한 내용은 [로지스틱 회귀 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)를 참조하세요.  
  
###  <a name="bkmk_Query4"></a> 예제 쿼리 4: 불연속 값에 대한 예측 만들기  
 로지스틱 회귀는 일반적으로 이진 결과에 영향을 주는 요소를 분석하려는 경우에 사용됩니다. 자습서에서 사용된 모델은 **ServiceGrade**라는 연속 값을 예측하지만, 실제 환경에서는 서비스 등급이 불연속화된 목표 값을 만족하는지 여부를 예측하도록 모델을 설정해야 합니다. 또는 연속 값을 사용하여 예측을 출력한 후 나중에 예측된 출력을 **Good**, **Fair**또는 **Poor**로 그룹화하는 방법도 있습니다.  
  
 다음 예제에서는 예측 가능한 특성의 그룹화 방식을 변경하는 방법을 보여 줍니다. 이 작업은 마이닝 구조의 복사본을 만든 다음 값이 연속되는 대신 그룹화되도록 대상 열의 분할 방법을 변경하여 수행할 수 있습니다.  
  
 다음 절차에서는 콜 센터 데이터에 있는 Service Grade 값의 그룹화를 변경하는 방법을 설명합니다.  
  
##### <a name="to-create-a-discretized-version-of-the-call-center-mining-structure-and-models"></a>콜 센터 마이닝 구조 및 모델의 불연속 버전을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 솔루션 탐색기에서 **마이닝 구조**를 확장합니다.  
  
2.  Call Center.dmm을 마우스 오른쪽 단추로 클릭하고 **복사**를 선택합니다.  
  
3.  **마이닝 구조** 를 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 선택합니다. Call Center 1이라는 새 마이닝 구조가 추가됩니다.  
  
4.  새 마이닝 구조를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택합니다. **Call Center Discretized**라는 새 이름을 입력합니다.  
  
5.  새 마이닝 구조를 두 번 클릭하여 디자이너에서 엽니다. 마이닝 모델까지 모두 복사되었으며 확장명은 모두 1입니다. 지금은 이름을 그대로 둡니다.  
  
6.  **마이닝 구조** 탭에서 Service Grade에 대한 열을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
7.  **Content** 속성의 값을 **연속** 에서 **불연속**으로 변경합니다. **DiscretizationMethod** 속성의 값을 **클러스터**로 변경합니다. Discretization BucketCount에 **3**을 입력합니다.  
  
    > [!NOTE]  
    >  이러한 매개 변수는 프로세스에 대한 이해를 돕기 위해 사용된 것일 뿐 이러한 매개 변수를 통해 유효한 모델이 반드시 생성되는 것은 아닙니다.  
  
8.  **마이닝 모델** 메뉴에서 **마이닝 구조 및 모든 모델 처리**를 선택합니다.  
  
 다음 예제 쿼리는 이 불연속 모델을 기반으로 하며 특정 요일의 서비스 등급 및 예측된 각 결과에 대한 확률을 예측합니다.  
  
```  
SELECT  
  (PredictHistogram([Call Center_LR 1].[Service Grade])) as [Predictions]  
FROM  
  [Call Center_LR 1]  
NATURAL PREDICTION JOIN  
(SELECT 'Saturday' AS [Day Of Week]) AS t    
```  
  
 예상 결과:  
  
 **예측:**  
  
|Service Grade|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.10872718383125|35.7246504770641|0.425293458060287|0.0170168360030293|0|0|  
|0.05855769230625|31.7098880800703|0.377498667619885|0.020882020060454|0|0|  
|0.170169491525|15.6109159883202|0.185844237956192|0.0661386571386049|0|0|  
||0.954545454545455|0.0113636363636364|0.0113636363636364|0|0|  
  
 예측된 결과는 지정된 세 개의 범주별로 그룹화되었지만 이러한 그룹화는 사용자가 비즈니스 목표로 설정한 임의의 값이 아니라 데이터의 실제 값 집합을 기반으로 수행되었습니다.  
  
## <a name="list-of-prediction-functions"></a>예측 함수 목록  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘은 공통 함수 집합을 지원합니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 로지스틱 회귀 알고리즘은 다음 표에 나열된 추가 함수도 지원합니다.  
  
|||  
|-|-|  
|예측 함수|사용법|  
|[IsDescendant & #40; DMX & #41;](../../dmx/isdescendant-dmx.md)|한 노드가 모델에서 다른 노드의 자식인지 여부를 확인합니다.|  
|[PredictAdjustedProbability & #40; DMX & #41;](../../dmx/predictadjustedprobability-dmx.md)|지정한 상태에 대한 조정된 확률을 반환합니다.|  
|[PredictHistogram & #40; DMX & #41;](../../dmx/predicthistogram-dmx.md)|지정한 열에 대한 예측 값을 반환합니다.|  
|[PredictProbability & #40; DMX & #41;](../../dmx/predictprobability-dmx.md)|지정한 상태에 대한 확률을 반환합니다.|  
|[PredictStdev & #40; DMX & #41;](../../dmx/predictstdev-dmx.md)|예측 값의 표준 편차를 반환합니다.|  
|[PredictSupport & #40; DMX & #41;](../../dmx/predictsupport-dmx.md)|지정한 상태에 대한 지원 값을 반환합니다.|  
|[PredictVariance & #40; DMX & #41;](../../dmx/predictvariance-dmx.md)|지정한 열의 분산을 반환합니다.|  
  
 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘에 공통된 함수 목록은 [일반 예측 함수&#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md)를 참조하세요. 특정 함수의 구문은 [DMX&#40;Data Mining Extensions&#41; 함수 참조](../../dmx/data-mining-extensions-dmx-function-reference.md)를 참조하세요.  
  
> [!NOTE]  
>  신경망 및 로지스틱 회귀 모델의 경우 [PredictSupport&#40;DMX&#41;](../../dmx/predictsupport-dmx.md) 함수는 모델 전체에 대한 학습 집합의 크기를 나타내는 단일 값을 반환합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft 로지스틱 회귀 알고리즘](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Microsoft 로지스틱 회귀 알고리즘 기술 참조](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)   
 [로지스틱 회귀 모델 & #40;에 대 한 마이닝 모델 콘텐츠 Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)   
 [5 단원: 구축 신경망 네트워크 및 로지스틱 회귀 모델 & #40; 중급 데이터 마이닝 자습서 & #41;](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b)  
  
  
