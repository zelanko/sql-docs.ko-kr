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
ms.openlocfilehash: 6e4c7df84bc7bf3a4804db76d952b1219100ef5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008366"
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
  
## <a name="remarks"></a>설명  
 **IsInNode** 는 [SELECT FROM &#60;모델&#62; 에서만 사용 됩니다. DMX&#41;&#40;사례](../dmx/select-from-model-cases-dmx.md) [&#60;모델&#62;에서 선택 합니다. DMX&#41;쿼리를 &#40;SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md) .  
  
## <a name="examples"></a>예  
 다음 예에서는 IsInNode 함수에서 지정한 노드와 연관된 모델을 만드는 데 사용된 모든 사례를 반환합니다.  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
