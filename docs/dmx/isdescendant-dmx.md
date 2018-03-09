---
title: IsDescendant (DMX) | Microsoft Docs
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
f1_keywords: IsDescendant
dev_langs: DMX
helpviewer_keywords: IsDescendant function
ms.assetid: d9fe7446-edb5-487b-8ea6-c9efaccf6d90
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 179a9f3f04db55cffb74f6417c3339ceeb20aa11
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="isdescendant-dmx"></a>IsDescendant(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  현재 노드가 지정한 노드의 하위 노드인지 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsDescendant(<NodeID>)  
```  
  
## <a name="return-type"></a>반환 형식  
 부울 유형입니다.  
  
## <a name="remarks"></a>주의  
 **IsDescendant** 에서만 사용 되는지 [SELECT FROM &#60; 모델 &#62;. 콘텐츠 &#40; DMX &#41; ](../dmx/select-from-model-content-dmx.md) 및 [SELECT FROM &#60; 모델 &#62;. DIMENSION_CONTENT &#40; DMX &#41; ](../dmx/select-from-model-dimension-content-dmx.md) 쿼리 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 IsDescendant 함수에서 지정한 노드의 하위 노드인 사례를 모두 반환합니다.  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
