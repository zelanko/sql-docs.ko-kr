---
title: PredictHistogram (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7e7129985eac09d741ea9d00c551a9507ee92c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659177"
---
# <a name="predicthistogram-dmx"></a>PredictHistogram(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정된 열의 예측에 대한 히스토그램을 나타내는 테이블을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 스칼라 열 참조 또는 클러스터 열 참조. [!INCLUDE[msCoName](../includes/msconame-md.md)] 연결 알고리즘을 제외한 모든 알고리즘 유형에 사용할 수 있습니다.  
  
## <a name="return-type"></a>반환 형식  
 테이블입니다.  
  
## <a name="remarks"></a>Remarks  
 히스토그램은 통계 열을 생성합니다. 사용 되는 열 참조 유형에 따라 달라 집니다 반환된 된 히스토그램의 열 구조를 **PredictHistogram** 함수입니다.  
  
## <a name="scalar-columns"></a>스칼라 열  
 에 대 한는 \<스칼라 열 참조 >, 히스토그램은 합니다 **PredictHistogram** 다음 열으로 구성 함수 반환:  
  
-   예측되는 값  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터 마이닝 알고리즘을 지원 하지 않습니다 **$ProbabilityVariance**합니다. 이 열은 항상 [!INCLUDE[msCoName](../includes/msconame-md.md)] 알고리즘에 대해 0을 포함합니다.  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터 마이닝 알고리즘을 지원 하지 않습니다 **$ProbabilityStdev**합니다. 이 열은 항상 [!INCLUDE[msCoName](../includes/msconame-md.md)] 알고리즘에 대해 0을 포함합니다.  
  
-   **$AdjustedProbability**  
  
     **$AdjustedProbability** 열이를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 확장을 [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB for Data Mining 사양 합니다.  
  
## <a name="cluster-columns"></a>클러스터 열  
 히스토그램은를 **PredictHistogram** 함수에 대해 반환을 \<클러스터 열 참조 > 다음 열으로 구성 됩니다.  
  
-   **$Cluster** (클러스터 이름을 나타냄)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>예  
 다음 예에서는 단일 쿼리를 사용하여 Bike Buyer 열의 예측 상태를 반환합니다. 쿼리를 사용 하 여 얻은 조정 된 확률을 기반으로 Bike Buyer 특성의 맨 위 두 가능성이 가장 높은 상태를 반환 합니다 **PredictHistogram** 함수입니다.  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  TopCount(PredictHistogram([Bike Buyer]),$AdjustedProbability,3)  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>관련 항목  
 [클러스터 &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
