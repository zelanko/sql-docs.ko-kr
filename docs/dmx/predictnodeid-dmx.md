---
title: PredictNodeId (DMX) | Microsoft Docs
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
- PredictNodeId
dev_langs:
- DMX
helpviewer_keywords:
- PredictNodeId function
ms.assetid: fb236645-ad7e-4c54-9c4c-1af47cad7ad5
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1ee43efb37a9ea9d6a1455947665470909ef73e2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="predictnodeid-dmx"></a>PredictNodeId(DMX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  사례가 분류되어 있는 노드의 Node_ID를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictNodeId(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 스칼라 열  
  
## <a name="return-type"></a>반환 형식  
 \<스칼라 식 >  
  
## <a name="examples"></a>예  
 다음 예에서는 지정한 개별 고객이 자전거를 구입할 가능성이 있는지 여부를 반환하고 해당 고객이 속할 가능성이 가장 높은 노드의 노드 ID를 반환합니다.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictNodeId([Bike Buyer])  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 그리고 나서 다음 문을 사용하여 노드 내에 포함된 내용을 확인할 수 있습니다.  
  
```  
SELECT   
  NODE_CAPTION   
FROM   
  [TM Decision Tree].CONTENT  
WHERE NODE_UNIQUE_NAME= '00000000100'   
```  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

