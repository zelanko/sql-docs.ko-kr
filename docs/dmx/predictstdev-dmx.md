---
title: PredictStdev (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: def9b352b97921b080e379d235972bb9dfc84510
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83666748"
---
# <a name="predictstdev-dmx"></a>PredictStdev(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정된 열의 예측 표준 편차를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PredictStdev(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 스칼라 열  
  
## <a name="return-type"></a>반환 형식  
 * \<>스칼라 열 참조 *로 지정 된 형식의 스칼라 값입니다.  
  
## <a name="remarks"></a>설명  
 열 참조가 불연속 이면 불연속 값에서 표준 편차를 계산할 수 없기 때문에 **Predictstdev** 는 0을 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 자연 예측 조인을 사용하여 TM Decision Tree 트리 마이닝 모델을 기반으로 개별 고객이 자전거를 구입할 가능성이 있는지 여부를 확인하고 예측의 표준 편차도 확인합니다.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictStdev([Bike Buyer]) AS [Standard Deviation]  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
