---
title: IsInNode (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 21c90bea43972f1c9088c228d6810b18308f93f4
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841706"
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
  
## <a name="remarks"></a>Remarks  
 **IsInNode** 에서만 사용 되는지 [SELECT FROM &#60;모델&#62;합니다. 경우 &#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md) 및 [SELECT FROM &#60;모델&#62;합니다. SAMPLE_CASES &#40;DMX&#41; ](../dmx/select-from-model-sample-cases-dmx.md) 쿼리 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 IsInNode 함수에서 지정한 노드와 연관된 모델을 만드는 데 사용된 모든 사례를 반환합니다.  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
