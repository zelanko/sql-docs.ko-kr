---
title: BottomPercent (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9d8b1665c6e6978af7dc673f7dd51a363da5c48d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892876"
---
# <a name="bottompercent-dmx"></a>BottomPercent(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  누적 합계가 지정한 비율 이상이 되는 테이블의 맨 아래 행을 오름차순으로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BottomPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="arguments"></a>인수  
 *\<테이블 식>*  
 중첩 테이블 열이나 테이블 반환 식의 이름입니다.  
  
 *\<rank 식>*  
 중첩 테이블의 열이거나 열로 계산되는 식입니다.  
  
 *\<백분율>*  
 총 대상 백분율을 나타내는 double 값입니다.  
  
## <a name="result-type"></a>결과 형식  
 테이블입니다.  
  
## <a name="remarks"></a>설명  
 **BottomPercent** 함수는 최하위 행을 차수 보다 오름차순으로 반환 합니다. Rank는 rank 식의 \<계산 된 값을 기준으로 하 여 각 행에 대 한 값> 값의 \<합계가 적어도 \<percent> 인수로 지정 된 비율 이상> 합니다. **BottomPercent** 는 지정 된 백분율 값을 충족 하는 동안 가능한 가장 작은 수의 요소를 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [기본 데이터 마이닝 자습서](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)에서 만든 연결 모델에 대 한 예측 쿼리를 만듭니다.  
  
 BottomPercent이 어떻게 작동 하는지 이해 하려면 먼저 중첩 테이블만 반환 하는 예측 쿼리를 실행 하는 것이 도움이 될 수 있습니다.  
  
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
  
 BottomPercent 함수는이 쿼리의 결과를 받아 합계가 지정 된 백분율에 해당 하는 가장 작은 값의 행을 반환 합니다.  
  
```  
SELECT   
BottomPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 BottomPercent 함수에 대 한 첫 번째 인수는 테이블 열의 이름입니다. 이 예에서는 Predict 함수를 호출 하 고 INCLUDE_STATISTICS 인수를 사용 하 여 중첩 테이블을 반환 합니다.  
  
 BottomPercent 함수에 대 한 두 번째 인수는 결과를 정렬 하는 데 사용 하는 중첩 테이블의 열입니다. 이 예에서 INCLUDE_STATISTICS 옵션은 $SUPPORT, $PROBABILTY 및 $ADJUSTED PROBABILITY 열을 반환합니다. 지원 값이 확인하기 쉬운 정수이므로 이 예에서는 $SUPPORT를 사용합니다.  
  
 BottomPercent 함수의 세 번째 인수는 백분율을 double로 지정 합니다. 지원의 하위 50%를 나타내는 행을 가져오려면 50을 입력합니다.  
  
 결과 예:  
  
|모델|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
  
 **참고** 이 예제는 BottomPercent의 사용법을 보여 주기 위해서만 제공 됩니다. 데이터 집합의 크기에 따라 이 쿼리를 실행하는 데 시간이 오래 걸릴 수 있습니다.  
  
> [!WARNING]  
>  TOPPERCENT 및 BOTTOMPERCENT에 대한 MDX 함수는 백분율 계산에 사용되는 값에 음수가 포함될 경우 예기치 않은 결과를 생성할 수 있습니다. 이 동작은 DMX 함수에는 영향을 주지 않습니다. 자세한 내용은 [BottomPercent &#40;MDX&#41;](../mdx/bottompercent-mdx.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;함수&#41;](../dmx/functions-dmx.md)  
  
  
