---
title: "Data Mining Extensions (DMX) 함수 참조 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- DMX [Analysis Services], functions
- functions [DMX]
- Data Mining Extensions [Analysis Services], functions
ms.assetid: fadd105b-9c8e-4118-a1f7-c0518b9ad970
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a1871de9ebb81ef5bd88063a3a26067e86b32ad3
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="data-mining-extensions-dmx-function-reference"></a>DMX(Data Mining Extensions) 함수 참조
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 DMX(Data Mining Extensions) 언어의 일부 함수를 지원합니다. 이러한 함수는 예측 쿼리의 결과를 확장하여 예측에 대한 더 많은 정보를 제공합니다. 함수는 또한 예측 결과의 반환 방법에 대한 제어 기능도 제공합니다. 다음 표에서는 DMX의 함수를 사용하는 방법을 이해하는 데 도움이 되는 리소스의 링크를 제공합니다.  
  
|함수|Description|  
|--------------|-----------------|  
|[일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)|모든 모델 유형과 함께 사용할 수 있는 함수를 나열하고, 특정 마이닝 모델 유형을 쿼리하는 방법에 대한 자세한 내용의 링크를 제공합니다.|  
|[DMX 예측 쿼리의 구조 및 사용법](../dmx/structure-and-usage-of-dmx-prediction-queries.md)|DMX를 사용하여 예측 쿼리를 생성하는 방법을 개괄적으로 설명합니다.|  
|[BottomCount &#40; DMX &#41;](../dmx/bottomcount-dmx.md)|차수 식에 따라 차수의 오름차순으로 제한된 개수의 최하위 행이 포함된 테이블을 반환합니다.|  
  
 다음 표에서는 DMX에서 지원하는 함수를 나열합니다.  
  
|함수|Description|  
|--------------|-----------------|  
|[BottomCount &#40; DMX &#41;](../dmx/bottomcount-dmx.md)|테이블 식의 마지막 n개 항목 행을 차수 식에 따라 오름차순으로 정렬한 테이블을 반환합니다.|  
|[BottomPercent &#40; DMX &#41;](../dmx/bottompercent-dmx.md)|차수 식에 따라 차수의 오름차순으로 지정된 백분율 식을 만족하는 가장 적은 수의 최하위 행이 포함된 테이블을 반환합니다.|  
|[BottomSum &#40; DMX &#41;](../dmx/bottomsum-dmx.md)|차수 식에 따라 차수의 오름차순으로 지정된 합계 식을 만족하는 가장 적은 수의 최하위 행이 포함된 테이블을 반환합니다.|  
|[클러스터 &#40; DMX &#41;](../dmx/cluster-dmx.md)|입력 사례가 포함되었을 가능성이 가장 높은 클러스터를 반환합니다.|  
|[ClusterProbability &#40; DMX &#41;](../dmx/clusterprobability-dmx.md)|입력 사례가 클러스터에 속할 확률을 반환합니다.|  
|[존재 &#40; DMX &#41;](../dmx/exists-dmx.md)|지정된 SELECT 문에서 반환한 결과 집합에 하나 이상의 행이 들어 있으면 true를 반환합니다.|  
|[IsDescendant &#40; DMX &#41;](../dmx/isdescendant-dmx.md)|현재 노드가 지정한 노드의 하위 노드인지 나타냅니다.|  
|[IsInNode &#40; DMX &#41;](../dmx/isinnode-dmx.md)|지정한 노드에 사례가 포함되었는지 여부를 나타냅니다.|  
|[IsTestCase &#40; DMX &#41;](../dmx/istestcase-dmx.md)|사례가 테스트 사례 집합에 속하는지 여부를 나타냅니다.|  
|[IsTrainingCase &#40; DMX &#41;](../dmx/istrainingcase-dmx.md)|사례가 학습 사례 집합에 속하는지 여부를 나타냅니다.|  
|[Lag &#40; DMX &#41;](../dmx/lag-dmx.md)|현재 사례의 날짜와 데이터의 마지막 날짜 간의 시간 조각을 반환합니다.|  
|[예측 &#40; DMX &#41;](../dmx/predict-dmx.md)|지정된 열에서 예측을 수행합니다.|  
|[PredictAdjustedProbability &#40; DMX &#41;](../dmx/predictadjustedprobability-dmx.md)|지정된 예측 열의 조정된 확률을 반환합니다.|  
|[PredictAssociation &#40; DMX &#41;](../dmx/predictassociation-dmx.md)|한 열에서 연관된 멤버 자격을 예측합니다.|  
|[PredictCaseLikelihood &#40; DMX &#41;](../dmx/predictcaselikelihood-dmx.md)|입력 사례가 기존 모델에 적합할 가능성을 반환합니다. 이 함수는 클러스터링 모델에서만 사용될 수 있습니다.|  
|[PredictHistogram &#40; DMX &#41;](../dmx/predicthistogram-dmx.md)|지정된 열에 대한 히스토그램을 나타내는 테이블을 반환합니다.|  
|[PredictNodeId &#40; DMX &#41;](../dmx/predictnodeid-dmx.md)|선택한 사례에 대한 노드 ID를 반환합니다.|  
|[PredictProbability &#40; DMX &#41;](../dmx/predictprobability-dmx.md)|지정된 열의 확률을 반환합니다.|  
|[PredictSequence &#40; DMX &#41;](../dmx/predictsequence-dmx.md)|순서에서 다음 값을 예측합니다.|  
|[PredictStdev &#40; DMX &#41;](../dmx/predictstdev-dmx.md)|지정된 열에 대한 표준 편차 값을 검색합니다.|  
|[PredictSupport &#40; DMX &#41;](../dmx/predictsupport-dmx.md)|열의 지원 값을 반환합니다.|  
|[PredictTimeSeries &#40; DMX &#41;](../dmx/predicttimeseries-dmx.md)|시계열의 미래 가치를 예측합니다.|  
|[PredictVariance &#40; DMX &#41;](../dmx/predictvariance-dmx.md)|지정된 열의 편차 값을 반환합니다.|  
|[RangeMax &#40; DMX &#41;](../dmx/rangemax-dmx.md)|지정된 불연속화된 열에 대해 발견한 예측 버킷의 상위 값을 반환합니다.|  
|[RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)|지정된 불연속화된 열에 대해 발견한 예측 버킷의 중간점 값을 반환합니다.|  
|[RangeMin &#40; DMX &#41;](../dmx/rangemin-dmx.md)|지정된 불연속화된 열에 대해 발견한 예측 버킷의 하위 값을 반환합니다.|  
|[StructureColumn &#40; DMX &#41;](../dmx/structurecolumn-dmx.md)|지정된 테이블 마이닝 구조 열의 값을 반환합니다.|  
|[TopCount &#40; DMX &#41;](../dmx/topcount-dmx.md)|차수 식에 따라 차수의 내림차순으로 제한된 개수의 최상위 행이 포함된 테이블을 반환합니다.|  
|[TopPercent &#40; DMX &#41;](../dmx/toppercent-dmx.md)|차수 식에 따라 차수의 내림차순으로 지정된 백분율 식을 만족하는 가장 적은 수의 최상위 행이 포함된 테이블을 반환합니다.|  
|[TopSum &#40; DMX &#41;](../dmx/topsum-dmx.md)|차수 식에 따라 차수의 내림차순으로 지정된 합계 식을 만족하는 가장 적은 수의 최상위 행이 포함된 테이블을 반환합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40; DMX &#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40; DMX &#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [구조 및 DMX 예측 쿼리 사용](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  

