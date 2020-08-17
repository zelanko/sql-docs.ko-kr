---
description: IsDescendant(DMX)
title: IsDescendant 항목 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9fe1c150f243e78c379823427e9940bba3680cb1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88352649"
---
# <a name="isdescendant-dmx"></a>IsDescendant(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  현재 노드가 지정한 노드의 하위 노드인지 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsDescendant(<NodeID>)  
```  
  
## <a name="return-type"></a>반환 형식  
 Boolean 형식입니다.  
  
## <a name="remarks"></a>설명  
 **Isdescendant 항목** 은 [SELECT FROM &#60;모델&#62; 에서만 사용 됩니다. DMX&#41;콘텐츠 &#40;](../dmx/select-from-model-content-dmx.md) [&#60;모델&#62;에서 선택 합니다. DMX&#41;쿼리를 &#40;DIMENSION_CONTENT ](../dmx/select-from-model-dimension-content-dmx.md) .  
  
## <a name="examples"></a>예제  
 다음 예에서는 IsDescendant 함수에서 지정한 노드의 하위 노드인 사례를 모두 반환합니다.  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
