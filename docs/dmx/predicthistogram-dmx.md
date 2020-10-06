---
description: PredictHistogram(DMX)
title: PredictHistogram (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cbeaa08cd118e032465f8456c0d7d7e111562f88
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727707"
---
# <a name="predicthistogram-dmx"></a>PredictHistogram(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  지정된 열의 예측에 대한 히스토그램을 나타내는 테이블을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 스칼라 열 참조 또는 클러스터 열 참조. [!INCLUDE[msCoName](../includes/msconame-md.md)] 연결 알고리즘을 제외한 모든 알고리즘 유형에 사용할 수 있습니다.  
  
## <a name="return-type"></a>반환 형식  
 테이블입니다.  
  
## <a name="remarks"></a>설명  
 히스토그램은 통계 열을 생성합니다. 반환 된 히스토그램의 열 구조는 **PredictHistogram** 함수와 함께 사용 되는 열 참조의 유형에 따라 달라 집니다.  
  
## <a name="scalar-columns"></a>스칼라 열  
 의 경우 \<scalar column reference> **PredictHistogram** 함수가 반환 하는 히스토그램은 다음과 같은 열로 구성 됩니다.  
  
-   예측되는 값  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터 마이닝 알고리즘은 **$ProbabilityVariance**를 지원 하지 않습니다. 이 열은 항상 [!INCLUDE[msCoName](../includes/msconame-md.md)] 알고리즘에 대해 0을 포함합니다.  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터 마이닝 알고리즘은 **$ProbabilityStdev**를 지원 하지 않습니다. 이 열은 항상 [!INCLUDE[msCoName](../includes/msconame-md.md)] 알고리즘에 대해 0을 포함합니다.  
  
-   **$AdjustedProbability**  
  
     **$AdjustedProbability** 열은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터 마이닝 사양의 OLE DB에 대 한 확장입니다.  
  
## <a name="cluster-columns"></a>클러스터 열  
 **PredictHistogram** 함수가에 대해 반환 하는 히스토그램은 \<cluster column reference> 다음과 같은 열로 구성 됩니다.  
  
-   **$Cluster** (클러스터 이름을 나타냄)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>예제  
 다음 예에서는 단일 쿼리를 사용하여 Bike Buyer 열의 예측 상태를 반환합니다. 또한이 쿼리는 **PredictHistogram** 함수를 사용 하 여 얻은 조정 된 확률에 따라 자전거 구매자 특성의 가장 중요 한 두 가지 상태를 반환 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [클러스터 &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [데이터 마이닝 알고리즘 &#40;Analysis Services 데이터 마이닝&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
