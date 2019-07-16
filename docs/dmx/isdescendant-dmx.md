---
title: IsDescendant (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7f6f3532165b8e958eb03cdf4954543159309a08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937712"
---
# <a name="isdescendant-dmx"></a>IsDescendant(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  현재 노드가 지정한 노드의 하위 노드인지 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsDescendant(<NodeID>)  
```  
  
## <a name="return-type"></a>반환 형식  
 Boolean 형식입니다.  
  
## <a name="remarks"></a>설명  
 **IsDescendant** 에서만 사용 됩니다 [SELECT FROM &#60;모델&#62;합니다. 콘텐츠 &#40;DMX&#41; ](../dmx/select-from-model-content-dmx.md) 하 고 [SELECT FROM &#60;모델&#62;합니다. DIMENSION_CONTENT &#40;DMX&#41; ](../dmx/select-from-model-dimension-content-dmx.md) 쿼리 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 IsDescendant 함수에서 지정한 노드의 하위 노드인 사례를 모두 반환합니다.  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
