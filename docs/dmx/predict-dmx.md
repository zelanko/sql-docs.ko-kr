---
title: Predict (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb939c45d298117fa81b05d6188aa3a4c5cd7c4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008162"
---
# <a name="predict-dmx"></a>Predict(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  합니다 **Predict** 예측된 값 또는 지정된 된 열에 대 한 값 집합을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>적용 대상  
 스칼라 열 참조 또는 테이블 열 참조  
  
## <a name="return-type"></a>반환 형식  
 \<스칼라 열 참조 >  
  
 로 구분하거나 여러  
  
 \<테이블 열 참조 >  
  
 반환 형식은 이 함수가 적용되는 열 유형에 따라 다릅니다.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY 및 INCLUDE_STATISTICS는 테이블 열 참조에만 적용되고 EXCLUDE_NULL 및 INCLUDE_NULL은 스칼라 열 참조에만 적용됩니다.  
  
## <a name="remarks"></a>설명  
 옵션에는 EXCLUDE_NULL(기본값), INCLUDE_NULL, INCLUSIVE, EXCLUSIVE(기본값), INPUT_ONLY, INCLUDE_STATISTICS 등이 있습니다.  
  
> [!NOTE]  
>  시계열 모델에 대 한 Predict 함수는 INCLUDE_STATISTICS를 지원 하지 않습니다.  
  
 INCLUDE_NODE_ID 매개 변수는 결과로 $NODEID 열을 반환합니다. NODE_ID는 특정 사례에 대한 예측이 실행되는 내용 노드입니다. 테이블 열에서 예측을 사용 하는 경우이 매개 변수를 선택 사항입니다.  
  
 합니다 *n* 매개 변수를 테이블 열에 적용 됩니다. 이 매개 변수는 예측 유형을 기반으로 반환되는 행 수를 설정합니다. 기본 열이 시퀀스인 경우 호출 된 **PredictSequence** 함수입니다. 기본 열이 시계열 인 경우 호출 된 **PredictTimeSeries** 함수입니다. 예측의 관련 유형에 대 한 호출을 **PredictAssociation** 함수입니다.  
  
 합니다 **Predict** 함수는 다형성을 지원 합니다.  
  
 대개는 다음과 같은 간략한 형식이 사용되는 경우가 많습니다.  
  
-   [Gender]는에 대 한 대안 **Predict**([Gender], EXCLUDE_NULL).  
  
-   [Products Purchases]의 대 안으로 **Predict**([Products Purchases], EXCLUDE_NULL, 전용).  
  
    > [!NOTE]  
    >  이 함수의 반환 형식은 열 참조로 간주됩니다. 즉 합니다 **Predict** 함수를 인수로 열 참조를 사용 하는 다른 함수의 인수로 사용할 수 있습니다 (제외 하 고는 **Predict** 함수 자체).  
  
 열이 추가 테이블 반환 열에서 예측에 INCLUDE_STATISTICS를 전달 **$Probability** 하 고 **$Support** 결과 테이블에 있습니다. 이러한 열은 연관된 중첩 테이블 레코드가 있을 가능성을 나타냅니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 Predict 함수를 사용 하 여 함께 판매 될 가능성이 있는 Adventure Works 데이터베이스에는 네 가지 제품을 반환 합니다. 함수를 사용 하는 연결 규칙 마이닝 모델에 대해 예측할를 자동으로 사용 합니다 **PredictAssociation** 앞에서 설명한 대로 작동 합니다.  
  
```  
SELECT  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,4)  
FROM     [Association]  
```  
  
 예제 결과:  
  
 이 쿼리는 `Expression`이라는 열만 있는 단일 데이터 행을 반환하지만, 이 열에는 다음과 같은 중첩 테이블이 들어 있습니다.  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016331743|0.252695851192499|  
|Water Bottle|2866|0.192620471805901|0.175205052318795|  
|Patch Kit|2113|0.142012232004839|0.132389356196586|  
|Mountain Tire Tube|1992|0.133879965051415|0.125304947722259|  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
