---
title: RangeMid (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- RangeMid
dev_langs:
- DMX
helpviewer_keywords:
- RangeMid function
ms.assetid: 23493d2d-4afd-43d6-b047-d110fcacee51
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9aa43de74489f380f453e12a417db911c414e6e8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="rangemid-dmx"></a>RangeMid(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  불연속화된 열에 대해 발견한 예측 버킷의 중간점을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RangeMid(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 불연속화된 스칼라 열  
  
## <a name="return-type"></a>반환 형식  
 스칼라 값  
  
## <a name="remarks"></a>주의  
 와 함께 사용할 경우 [SELECT FROM &#60;모델&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md), **RangeMin**, **RangeMid**, 및 **RangeMax**  함수 지정 된 버킷의 실제 경계 값을 반환 합니다. 예를 들어 불연속화된 열에 대해 예측을 수행하면 해당 쿼리는 불연속화된 열의 예측 버킷 번호를 반환합니다. **RangeMin**, **RangeMid**, 및 **RangeMax** 함수는 예측이 지정 하는 버킷을 설명 합니다. 경우는 **RangeMid** 함수는 PREDICTION JOIN 문을 함께 사용, 스칼라 열 참조에는 예측 가능한 불연속 열만 포함할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 TM Decision Tree 마이닝 모델의 Yearly Income 연속 열에 대한 최대값, 최소값 및 평균값을 반환합니다.  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)   
 [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
  
