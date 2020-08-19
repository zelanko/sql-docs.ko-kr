---
description: Predict(DMX)
title: Predict (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4f53f331b078fce4f02e548a83a145dce8ba6a91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426205"
---
# <a name="predict-dmx"></a>Predict(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  **Predict** 함수는 지정 된 열에 대 한 예측 값 또는 값 집합을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>적용 대상  
 스칼라 열 참조 또는 테이블 열 참조  
  
## <a name="return-type"></a>반환 형식  
 \<scalar column reference>  
  
 또는  
  
 \<table column reference>  
  
 반환 형식은 이 함수가 적용되는 열 유형에 따라 다릅니다.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY 및 INCLUDE_STATISTICS는 테이블 열 참조에만 적용되고 EXCLUDE_NULL 및 INCLUDE_NULL은 스칼라 열 참조에만 적용됩니다.  
  
## <a name="remarks"></a>설명  
 옵션에는 EXCLUDE_NULL(기본값), INCLUDE_NULL, INCLUSIVE, EXCLUSIVE(기본값), INPUT_ONLY, INCLUDE_STATISTICS 등이 있습니다.  
  
> [!NOTE]  
>  시계열 모델의 경우 Predict 함수는 INCLUDE_STATISTICS을 지원 하지 않습니다.  
  
 INCLUDE_NODE_ID 매개 변수는 결과로 $NODEID 열을 반환합니다. NODE_ID는 특정 사례에 대한 예측이 실행되는 내용 노드입니다. 이 매개 변수는 테이블 열에서 Predict를 사용할 때 선택 사항입니다.  
  
 *N* 매개 변수는 테이블 열에 적용 됩니다. 이 매개 변수는 예측 유형을 기반으로 반환되는 행 수를 설정합니다. 기본 열이 시퀀스인 경우 **PredictSequence** 함수를 호출 합니다. 기본 열이 시계열 인 경우 **PredictTimeSeries** 함수를 호출 합니다. 연관 형식의 예측에는 **PredictAssociation** 함수를 호출 합니다.  
  
 **Predict** 함수는 다형성을 지원 합니다.  
  
 대개는 다음과 같은 간략한 형식이 사용되는 경우가 많습니다.  
  
-   [성별]은 (는) **Predict**([성별], EXCLUDE_NULL)에 대 한 대안입니다.  
  
-   [제품 구매]는 **Predict**([products 구매], EXCLUDE_NULL, EXCLUSIVE)의 대안입니다.  
  
    > [!NOTE]  
    >  이 함수의 반환 형식은 열 참조로 간주됩니다. 즉 **, predict 함수** 자체를 제외 하 고 열 참조를 인수로 사용 하는 다른 함수에서 **predict** 함수를 인수로 사용할 수 있습니다.  
  
 테이블 반환 열에 대 한 예측에 INCLUDE_STATISTICS를 전달 하면 **$Probability** 열과 **$Support** 결과 테이블에 추가 됩니다. 이러한 열은 연관된 중첩 테이블 레코드가 있을 가능성을 나타냅니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 Predict 함수를 사용 하 여 함께 판매 될 가능성이 가장 높은 놀이 Works 데이터베이스의 4 개 제품을 반환 합니다. 함수는 연결 규칙 마이닝 모델에 대해 예측 하므로 앞에서 설명한 대로 자동으로 **PredictAssociation** 함수를 사용 합니다.  
  
```  
SELECT  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,4)  
FROM     [Association]  
```  
  
 예제 결과:  
  
 이 쿼리는 `Expression`이라는 열만 있는 단일 데이터 행을 반환하지만, 이 열에는 다음과 같은 중첩 테이블이 들어 있습니다.  
  
|모델|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016331743|0.252695851192499|  
|Water Bottle|2866|0.192620471805901|0.175205052318795|  
|Patch Kit|2113|0.142012232004839|0.132389356196586|  
|Mountain Tire Tube|1992|0.133879965051415|0.125304947722259|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
