---
title: RangeMid (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e3f13f1d110c26ee590df3a09296f6d861e34e37
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970670"
---
# <a name="rangemid-dmx"></a>RangeMid(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  불연속화된 열에 대해 발견한 예측 버킷의 중간점을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RangeMid(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 불연속화된 스칼라 열  
  
## <a name="return-type"></a>반환 형식  
 스칼라 값  
  
## <a name="remarks"></a>설명  
 [SELECT FROM &#60;모델&#62; 예측 조인 &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)에서 사용 하는 경우 **RangeMin**, **RangeMid**및 **RangeMax** 함수는 지정 된 버킷의 실제 경계 값을 반환 합니다. 예를 들어 불연속화된 열에 대해 예측을 수행하면 해당 쿼리는 불연속화된 열의 예측 버킷 번호를 반환합니다. **RangeMin**, **RangeMid**및 **RangeMax** 함수는 예측이 지정 하는 버킷을 설명 합니다. **RangeMid** 함수를 예측 조인 문과 함께 사용 하는 경우 스칼라 열 참조는 불연속 하 고 예측 가능한 열만 포함할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 TM Decision Tree 마이닝 모델의 Yearly Income 연속 열에 대한 최대값, 최소값 및 평균값을 반환합니다.  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)   
 [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
  
