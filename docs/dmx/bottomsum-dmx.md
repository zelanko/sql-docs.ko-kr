---
title: BottomSum (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 51ebd164ae5c184177367f59b5643712b14718a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071132"
---
# <a name="bottomsum-dmx"></a>BottomSum(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  집합을 오름차순으로 정렬하고 누적 합계가 지정한 값 이상이 되는 맨 아래 테이블 행을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BottomSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 같은 테이블을 반환 하는 식은 \<테이블 열 참조 >, 또는 테이블을 반환 하는 함수입니다.  
  
## <a name="return-type"></a>반환 형식  
 \<테이블 식 >  
  
## <a name="remarks"></a>설명  
 합니다 **BottomSum** 함수 오름차순에서 맨 아래 행을 반환 합니다. 순위 계산된 된 값에 기반 합니다 \<식의 순위를 지정 > 각 행에 대 한 인수는의 합계를 \<식의 순위를 지정 > 값으로 지정 된 지정한 합계 이상이 \<합계 > 인수. **BottomSum** 지정 된 합계 값에 맞추어 가능한 가장 작은 요소 수를 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 사용 하 여 작성 하는 연결 모델에 대해 예측 쿼리를 [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)합니다.  
  
 BottomSum의 작동 원리를 이해 하려면 우선 중첩된 테이블만 반환 하는 예측 쿼리를 실행 하는 데 도움이 수 있습니다.  
  
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
  
 BottomSum 함수는이 쿼리의 결과 받아 및 지정 된 개수 가장 낮은 값을 사용 하 여 행 합계를 반환 합니다.  
  
```  
SELECT   
BottomSum  
    (  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $PROBABILITY,  
    .1)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 BottomSum 함수는 첫 번째 인수는 테이블 열의 이름입니다. 이 예제에서는 중첩된 테이블은 Predict 함수를 호출 하 고 INCLUDE_STATISTICS 인수를 사용 하 여 반환 됩니다.  
  
 BottomSum 함수에서 두 번째 인수는 결과 정렬 하는 데 사용 하는 중첩된 테이블의 열입니다. 이 예에서 INCLUDE_STATISTICS 옵션은 $SUPPORT, $PROBABILTY 및 $ADJUSTED PROBABILITY 열을 반환합니다. 이 예에서는 $PROBABILITY를 사용하여 확률 합계가 최소 50%인 행을 반환합니다.  
  
 BottomSum 함수는 세 번째 인수를 double 값으로는 대상 합계를 지정합니다. 확률 합계가 10%인 가장 낮은 개수의 제품에 대한 행을 가져오려면 1을 입력합니다.  
  
 예제 결과:  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.08...|0.07...|  
|Mountain Bottle Cage|1367|0.09...|0.08...|  
  
 **참고** 이 예제만 제공 됩니다 BottomSum의 사용법을 보여 줍니다. 데이터 집합의 크기에 따라 이 쿼리를 실행하는 데 시간이 오래 걸릴 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [함수 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)  
  
  
