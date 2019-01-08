---
title: TopCount (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0ec801da96735f15b6320c3f0372855c1ff3c2c8
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502827"
---
# <a name="topcount-dmx"></a>TopCount(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  식에서 지정한 수만큼 맨 위 행을 내림차순으로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 같은 테이블을 반환 하는 식은 \<테이블 열 참조 >, 또는 테이블을 반환 하는 함수입니다.  
  
## <a name="return-type"></a>반환 형식  
 \<테이블 식 >  
  
## <a name="remarks"></a>Remarks  
 제공 하는 값을 \<식의 순위를 지정 > 인수에서 제공 되는 행의 내림차순이 결정을 \<테이블 식 > 인수와 합니다 에지정된맨위행의수\<개수 > 인수가 반환 됩니다.  
  
 TopCount 함수는 원래 연결 예측을 사용 하도록 설정 하려면 도입 되었으며 일반적으로 포함 하는 문으로 동일한 결과 생성 **SELECT TOP** 하 고 **ORDER BY** 절. 사용 하는 경우 연결 예측에 대 한 성능 향상을 받습니다 합니다 **예측 (DMX)** 함수는 많은 예측이 반환 되도록 지정할 사양을 지원 합니다.  
  
 그러나 여기서 계속 해야 TopCount를 사용 하는 경우가 있습니다. 예를 들어 DMX 지원 하지 않습니다 합니다 **위쪽** 하위 select 문에서 한정자입니다. 합니다 [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md) 함수 또한 추가 지원 하지 않습니다 **위쪽**.  
  
## <a name="examples"></a>예  
 다음 예제는 사용 하 여 작성 하는 연결 모델에 대 한 예측 쿼리를 [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)합니다. 쿼리는 동일한 결과 반환 하지만 첫 번째 예제에서는 TopCount와 사용 하 고 두 번째 예제 Predict 함수를 사용 합니다.  
  
 TopCount의 작동 원리를 이해 하려면 우선 중첩된 테이블만 반환 하는 예측 쿼리를 실행 하는 데 도움이 수 있습니다.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  이 예에서 입력으로 제공된 값에는 작은따옴표가 들어 있으므로 작은따옴표를 앞에 추가하여 이스케이프해야 합니다. 이스케이프 문자를 삽입하는 구문을 모르는 경우 예측 쿼리 작성기를 사용하여 쿼리를 만들 수 있습니다. 드롭다운 목록에서 값을 선택하면 필요한 이스케이프 문자가 자동으로 삽입됩니다. 자세한 내용은 [데이터 마이닝 디자이너에서 단일 쿼리를 만들려면](../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md)합니다.  
  
 예제 결과:  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Water Bottle|2866|0.192620472|0.175205052|  
|Patch kit|2113|0.142012232|0.132389356|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
  
 TopCount 함수는이 쿼리의 결과 받아 및 지정된 된 백분율인 최소값 행 수를 반환 합니다.  
  
```  
SELECT   
TopCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 TopCount 함수는 첫 번째 인수는 테이블 열의 이름입니다. 이 예제에서는 중첩된 테이블은 Predict 함수를 호출 하 고 INCLUDE_STATISTICS 인수를 사용 하 여 반환 됩니다.  
  
 TopCount 함수에서 두 번째 인수는 결과 정렬 하는 데 사용 하는 중첩된 테이블의 열입니다. 이 예에서 INCLUDE_STATISTICS 옵션은 $SUPPORT, $PROBABILTY 및 $ADJUSTED PROBABILITY 열을 반환합니다. 이 예에서는 $SUPPORT를 사용하여 결과의 등급을 지정합니다.  
  
 TopCount 함수는 세 번째 인수를 정수로 반환할 행 수를 지정 합니다. $SUPPORT에서 정렬한 대로 최상위 3개 제품을 얻으려면 3을 입력합니다.  
  
 예제 결과:  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29...|0.25...|  
|Water Bottle|2866|0.19...|0.17...|  
|Patch kit|2113|0.14...|0.13...|  
  
 그러나 이 유형의 쿼리는 프로덕션 설정의 성능에 영향을 미칠 수 있습니다. 이는 이 쿼리가 알고리즘의 모든 예측 집합을 반환하고, 이러한 예측을 정렬하며 최상위 3개를 반환하기 때문입니다.  
  
 다음 예에서는 동일한 결과를 반환하지만 매우 빠르게 실행되는 대체 문을 제공합니다. 이 예제에서는 TopCount는 많은 예측을 인수로 허용 하는 예측 함수를 바꿉니다. 또한이 예제에서는 합니다 **$SUPPORT** 키워드를 직접 중첩된 테이블 열을 검색 합니다.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 결과에는 지원 값으로 정렬된 최상위 3개 예측이 포함됩니다. $SUPPORT를 $PROBABILITY 또는 $ADJUSTED_PROBABILITY로 대체하여 확률 또는 조정된 확률로 등급이 지정된 예측을 반환할 수 있습니다. 자세한 내용은 **예측 (DMX)** 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)   
 [TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)   
 [TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)  
  
  
