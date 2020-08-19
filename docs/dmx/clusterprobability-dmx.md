---
description: ClusterProbability(DMX)
title: ClusterProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f27a901bbb45c48996c82bbedbbb3691c1a6cbc2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431115"
---
# <a name="clusterprobability-dmx"></a>ClusterProbability(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  입력 사례가 지정한 클러스터에 속할 확률을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>적용 대상  
 이 함수는 기본 데이터 마이닝 모델이 클러스터링을 지원할 때만 사용할 수 있습니다.  
  
## <a name="return-type"></a>반환 형식  
 스칼라 값  
  
## <a name="remarks"></a>설명  
 다음 구문은 마이닝 모델 콘텐츠 스키마 행 집합을 사용하여 마이닝 모델에 있는 노드 캡션을 반환합니다.  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 이 구문을 사용 하는 방법에 대 한 자세한 내용은 [SELECT FROM &#60;model&#62;을 참조 하세요. 콘텐츠 &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md). 마이닝 모델 콘텐츠 스키마 행 집합에 대 한 자세한 내용은 [DMSCHEMA_MINING_MODEL_CONTENT 행 집합](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126267(v=sql.110))을 참조 하세요.  
  
 \<node caption>가 지정 되지 않은 경우이 함수는 입력 사례가 가장 가능성이 높은 클러스터에 속할 확률을 반환 합니다. **클러스터** 함수를 사용 하 여 가장 가능성이 높은 클러스터를 반환 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 Cluster 2라는 클러스터에 지정한 사례가 나타날 확률을 반환합니다.  
  
```  
SELECT  
  ClusterProbability('Cluster 2')  
From  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>참고 항목  
 [클러스터 &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
