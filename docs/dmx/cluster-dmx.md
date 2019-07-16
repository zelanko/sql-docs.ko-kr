---
title: Cluster (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa7df2782b8102e386c70d5e874a25f7868dbb1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071086"
---
# <a name="cluster-dmx"></a>Cluster(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  입력 사례가 포함되었을 가능성이 가장 높은 클러스터를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>적용 대상  
 이 함수는 기본 데이터 마이닝 모델이 클러스터링을 지원할 때만 사용할 수 있습니다.  
  
## <a name="return-type"></a>반환 형식  
 합니다 **클러스터** 함수 매개 변수가 필요 하지 않습니다.  
  
 합니다 **클러스터** 함수는 클러스터 이름의 스칼라 값을 반환 합니다. 그러나 다른 함수의 인수로 서이 함수를 사용 하는 경우 간주 해야 합니다로 \<클러스터 열 참조 >.  
  
## <a name="remarks"></a>설명  
 **클러스터** 으로 사용할 수는 `<`클러스터 열 참조`>` 에 대 한를 **PredictHistogram** 함수입니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 사용 하 여 단일 쿼리를 [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md) TM Clustering 마이닝 모델의 각 클러스터에서 개별 사례의 거리를 반환 하는 함수를 클러스터 및 개별 사례가 각 클러스터에 존재 하는 확률입니다.  
  
```  
SELECT  
  PredictHistogram(Cluster())  
FROM  
  [TM Clustering]  
  NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>관련 항목  
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
