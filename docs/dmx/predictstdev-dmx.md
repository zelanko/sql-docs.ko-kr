---
title: PredictStdev (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PredictStdev
dev_langs: DMX
helpviewer_keywords: PredictStdev function
ms.assetid: 2614aad0-f3f2-4f56-9dad-9c436f11a35f
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 80972c7888cab4c64e30e346064d321715e5f2ce
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
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
 지정 된 형식의 스칼라 값  *\<스칼라 열 참조 >*합니다.  
  
## <a name="remarks"></a>주의  
 열 참조가 불연속 유형인 경우 **PredictStdev** 불연속 값의 표준 편차를 계산할 수 없기 때문에 0을 반환 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
