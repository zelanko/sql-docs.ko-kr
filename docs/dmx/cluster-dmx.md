---
description: Cluster(DMX)
title: 클러스터 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0722e53752cfa01ffee086cb8cf1f6a84f82fd4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457858"
---
# <a name="cluster-dmx"></a>Cluster(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  입력 사례가 포함되었을 가능성이 가장 높은 클러스터를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>적용 대상  
 이 함수는 기본 데이터 마이닝 모델이 클러스터링을 지원할 때만 사용할 수 있습니다.  
  
## <a name="return-type"></a>반환 형식  
 **클러스터** 함수에는 매개 변수가 필요 하지 않습니다.  
  
 **클러스터** 함수는 클러스터 이름의 스칼라 값을 반환 합니다. 그러나이 함수를 다른 함수의 인수로 사용 하는 경우에는이 함수를로 간주 해야 합니다 \<cluster column reference> .  
  
## <a name="remarks"></a>설명  
 **클러스터** 를 `<` `>` **PredictHistogram** 함수에 대 한 클러스터 열 참조로 사용할 수도 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 [PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md) 및 클러스터 함수에서 단일 쿼리를 사용 하 여 TM 클러스터링 마이닝 모델의 각 클러스터에서 개별 사례의 거리와 개별 사례가 각 클러스터에 존재 하는 확률을 반환 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
