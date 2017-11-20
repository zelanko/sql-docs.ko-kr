---
title: IsInNode (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IsInNode
dev_langs:
- DMX
helpviewer_keywords:
- IsInNode function
ms.assetid: 47b2114f-9ad6-45cc-9498-193ad6fa5288
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d10cc8b335fa47eee2932da7805f97fb42ed6711
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="isinnode-dmx"></a>IsInNode(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 노드에 현재 사례가 포함되었는지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsInNode(<NodeID>)  
```  
  
## <a name="return-type"></a>반환 형식  
 부울 유형입니다.  
  
## <a name="remarks"></a>주의  
 **IsInNode** 에서만 사용 되는지 [SELECT FROM &#60; 모델 &#62;. 경우 &#40; DMX &#41; ](../dmx/select-from-model-cases-dmx.md) 및 [SELECT FROM &#60; 모델 &#62;. SAMPLE_CASES &#40; DMX &#41; ](../dmx/select-from-model-sample-cases-dmx.md) 쿼리 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 IsInNode 함수에서 지정한 노드와 연관된 모델을 만드는 데 사용된 모든 사례를 반환합니다.  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

