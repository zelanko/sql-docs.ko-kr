---
title: RangeMax (DMX) | Microsoft Docs
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
- RangeMax
dev_langs:
- DMX
helpviewer_keywords:
- RangeMax function
ms.assetid: 6798d9d7-c3dc-40fb-bd8e-56cb1a6d0e5f
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8b8cb363e9d5db767ed172206f497ff300bb29a6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="rangemax-dmx"></a>RangeMax(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  불연속화된 열에 대해 발견한 예측 버킷의 최대값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RangeMax(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 스칼라 열  
  
## <a name="return-type"></a>반환 형식  
 스칼라 값  
  
## <a name="remarks"></a>주의  
 **RangeMax** 함수에서 사용할 수 있습니다 [SELECT DISTINCT FROM &#60; 모델 &#62; &#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md) 쿼리 합니다. 이 쿼리 유형에 스칼라 열 참조를 사용하면 해당 참조에 예측 가능 또는 입력 형식에 해당하는 연속 열이나 불연속 열이 포함될 수 있습니다.  
  
 와 함께 사용할 경우 [SELECT FROM &#60; 모델 &#62; 예측 조인 &#40; DMX &#41; ](../dmx/select-from-model-prediction-join-dmx.md), **RangeMin**, **RangeMid**, 및 **RangeMax** 함수 지정 된 버킷의 실제 경계 값을 반환 합니다. 예를 들어 불연속화된 열에 대해 예측을 수행하면 해당 쿼리는 불연속화된 열의 예측 버킷 번호를 반환합니다. **RangeMin**, **RangeMid**, 및 **RangeMax** 함수는 예측이 지정 하는 버킷을 설명 합니다. 경우는 **RangeMax** 함수는 PREDICTION JOIN 문을 함께 사용, 스칼라 열 참조에는 예측 가능한 불연속 열만 포함할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Decision Tree 마이닝 모델의 Yearly Income 연속 열에 대한 최대값, 최소값 및 평균값을 반환합니다.  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>참고 항목  
 [Data Mining Extensions &#40; DMX &#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)   
 [RangeMin &#40; DMX &#41;](../dmx/rangemin-dmx.md)  
  
  

