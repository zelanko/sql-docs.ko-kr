---
title: TopPercent (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3f2f97ef9c7a1cdfa2bb1ba1b86dbe4cf60c8404
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669919"
---
# <a name="toppercent-dmx"></a>TopPercent(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **TopPercent** 함수는 누적 합계가 지정 된 비율 이상인 테이블의 맨 위 행을 내림차순으로 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
TopPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="applies-to"></a>적용 대상  
 테이블 열 참조>와 같이 테이블을 반환 하는 식 \< 또는 테이블을 반환 하는 함수입니다.  
  
## <a name="return-type"></a>반환 형식  
 \<테이블 식>  
  
## <a name="remarks"></a>설명  
 **TopPercent** 함수는 차수> 식의 계산 된 값을 기준으로 가장 높은 행을 차수 식의 계산 된 값을 기준으로 내림차순으로 반환 합니다 .이 값은 \< \< rank 식의 합계가 백분율> 인수로 지정 되는 지정 된 비율 이상> 합니다 \< . **TopPercent** 는 지정 된 백분율 값을 충족 하는 동안 가능한 가장 작은 수의 요소를 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [기본 데이터 마이닝 자습서](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)를 사용 하 여 작성 하는 연결 모델에 대 한 예측 쿼리를 만듭니다.  
  
 TopPercent이 어떻게 작동 하는지 이해 하려면 먼저 중첩 테이블만 반환 하는 예측 쿼리를 실행 하는 것이 유용할 수 있습니다.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  이 예에서 입력으로 제공된 값에는 작은따옴표가 들어 있으므로 작은따옴표를 앞에 추가하여 이스케이프해야 합니다. 이스케이프 문자를 삽입하는 구문을 모르는 경우 예측 쿼리 작성기를 사용하여 쿼리를 만들 수 있습니다. 드롭다운 목록에서 값을 선택하면 필요한 이스케이프 문자가 자동으로 삽입됩니다. 자세한 내용은 [데이터 마이닝 디자이너에서 단일 쿼리 만들기](https://docs.microsoft.com/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer)를 참조 하세요.  
  
 결과 예:  
  
|모델|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
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
  
 TopPercent 함수는이 쿼리의 결과를 사용 하 여 합계가 지정 된 백분율에 해당 하는 값이 가장 큰 행을 반환 합니다.  
  
```  
SELECT   
TopPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 TopPercent 함수에 대 한 첫 번째 인수는 테이블 열의 이름입니다. 이 예에서는 Predict 함수를 호출 하 고 INCLUDE_STATISTICS 인수를 사용 하 여 중첩 테이블을 반환 합니다.  
  
 TopPercent 함수에 대 한 두 번째 인수는 결과를 정렬 하는 데 사용 하는 중첩 테이블의 열입니다. 이 예에서 INCLUDE_STATISTICS 옵션은 $SUPPORT, $PROBABILTY 및 $ADJUSTED PROBABILITY 열을 반환합니다. 지원 값이 확인하기 쉬운 정수이므로 이 예에서는 $SUPPORT를 사용합니다.  
  
 TopPercent 함수의 세 번째 인수는 백분율을 double로 지정 합니다. 총 지원의 하위 50%를 나타내는 최상위 제품의 행을 가져오려면 50을 입력합니다.  
  
 결과 예:  
  
|모델|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29 ...|0.25 ...|  
|Water Bottle|2866|0.19 ...|0.17 ...|  
|Patch kit|2113|0.14 ...|0.13 ...|  
|Mountain Tire Tube|1992|0.133 ...|0.12 ...|  
  
 **참고** 이 예제는 TopPercent의 사용법을 보여 주기 위해서만 제공 됩니다. 데이터 집합의 크기에 따라 이 쿼리를 실행하는 데 시간이 오래 걸릴 수 있습니다.  
  
> [!WARNING]  
>  TOPPERCENT 및 BOTTOMPERCENT에 대한 MDX 함수는 백분율 계산에 사용되는 값에 음수가 포함될 경우 예기치 않은 결과를 생성할 수 있습니다. 이 동작은 DMX 함수에는 영향을 주지 않습니다. 자세한 내용은 [BottomPercent &#40;MDX&#41;](../mdx/bottompercent-mdx.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)  
  
  
