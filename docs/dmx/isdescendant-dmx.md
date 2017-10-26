---
title: IsDescendant (DMX) | Microsoft Docs
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
- IsDescendant
dev_langs:
- DMX
helpviewer_keywords:
- IsDescendant function
ms.assetid: d9fe7446-edb5-487b-8ea6-c9efaccf6d90
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4a1e7959a303b768851784af0ab9c88abd257674
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="isdescendant-dmx"></a>IsDescendant(DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>참고 항목  
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

