---
description: PredictNodeId(DMX)
title: PredictNodeId (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3fac7baa2f30d20c8e5043a405156a36f43a29a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426135"
---
# <a name="predictnodeid-dmx"></a>PredictNodeId(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  사례가 분류되어 있는 노드의 Node_ID를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictNodeId(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 스칼라 열  
  
## <a name="return-type"></a>반환 형식  
 \<scalar expression>  
  
## <a name="examples"></a>예제  
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
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
