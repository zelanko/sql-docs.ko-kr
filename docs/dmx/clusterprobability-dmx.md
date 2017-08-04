---
title: ClusterProbability (DMX) | Microsoft Docs
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
f1_keywords:
- ClusterProbability
dev_langs:
- DMX
helpviewer_keywords:
- ClusterProbability function
ms.assetid: a6447b3c-94ce-4122-a3eb-6f3827598d8f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b7f68000caa8fd90dd2a2396ff17f0fd701b96d2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="clusterprobability-dmx"></a>ClusterProbability(DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  입력 사례가 지정한 클러스터에 속할 확률을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>적용 대상  
 이 함수는 기본 데이터 마이닝 모델이 클러스터링을 지원할 때만 사용할 수 있습니다.  
  
## <a name="return-type"></a>반환 형식  
 스칼라 값  
  
## <a name="remarks"></a>주의  
 다음 구문은 마이닝 모델 콘텐츠 스키마 행 집합을 사용하여 마이닝 모델에 있는 노드 캡션을 반환합니다.  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 이 구문을 사용 하는 방법에 대 한 자세한 내용은 참조 [SELECT FROM &#60; 모델 &#62;. 콘텐츠 &#40; DMX &#41; ](../dmx/select-from-model-content-dmx.md). 마이닝 모델 콘텐츠 스키마 행 집합에 대 한 자세한 내용은 참조 [DMSCHEMA_MINING_MODEL_CONTENT 행 집합](../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)합니다.  
  
 경우는 \<노드 캡션 >을 지정 하지 않으면 함수는 입력된 사례와 가장 가능성 있는 클러스터에 속할 확률을 반환 합니다. 사용 하 여는 **클러스터** 가장 가능성이 높은 클러스터를 반환 하는 함수입니다.  
  
## <a name="examples"></a>예  
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
  
## <a name="see-also"></a>관련 항목:  
 [클러스터 &#40; DMX &#41;](../dmx/cluster-dmx.md)   
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

