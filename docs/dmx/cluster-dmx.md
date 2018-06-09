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
manager: kfile
ms.openlocfilehash: 41f835a93e5976945281b6b04258c516b0322236
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841306"
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
 **클러스터** 함수 매개 변수가 필요 하지 않습니다.  
  
 **클러스터** 함수는 클러스터 이름의 스칼라 값을 반환 합니다. 그러나 다른 함수의 인수로 서이 함수를 사용 하는 경우 간주 해야로 \<클러스터 열 참조 > 합니다.  
  
## <a name="remarks"></a>Remarks  
 **클러스터** 으로 사용할 수는 `<`클러스터 열 참조`>` 에 대 한는 **PredictHistogram** 함수입니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 단일 쿼리를 사용 하 여는 [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md) 클러스터 TM Clustering 마이닝 모델의 각 클러스터에서 개별 사례의 거리를 반환 하는 함수 및 확률은 개별 사례를 각 클러스터에 있는지입니다.  
  
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
  
  
