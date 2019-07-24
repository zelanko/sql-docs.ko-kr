---
title: Analysis Services 테이블 형식 모델의 계산 그룹 | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: af63f41555a021fc720c7d1e15778265fe7de500
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419531"
---
# <a name="calculation-groups-preview"></a>계산 그룹 (미리 보기)
 
[!INCLUDE[ssas-appliesto-sql2019-aas](../../includes/ssas-appliesto-sql2019-aas.md)]

계산 그룹은 일반적인 측정값 식을 *계산 항목*으로 그룹화 하 여 중복 측정값 수를 크게 줄일 수 있습니다. 계산 그룹은 1470 이상의 [호환성 수준](compatibility-level-for-tabular-models-in-analysis-services.md)에서 Azure Analysis Services 및 SQL Server Analysis Services 2019 테이블 형식 모델에서 지원 됩니다. 1470 호환성 수준의 모델은 현재 **미리 보기로**제공 됩니다.  

이 문서에서는 다음에 대해 설명합니다. 

> [!div class="checklist"]
> * 이점 
> * 계산 그룹의 작동 방식
> * 동적 서식 문자열
> * 주
> * 우선 순위
> * Tools
> * 제한 사항



## <a name="benefits"></a>이점

계산 그룹은 동일한 계산을 사용 하 여 중복 측정값이 확산 될 수 있는 복잡 한 모델의 문제를 해결 합니다 .이는 시간 인텔리전스 계산과 가장 일반적입니다. 예를 들어 판매 분석가는 MTD (날짜), 분기별 누계 (QTD), 연간 누계 (YTD), 작년의 연간 누계 (PY) 등을 기준으로 판매 합계 및 주문을 보려는 경우를 예로 들 수 있습니다. 데이터 모델러는 각 계산에 대 한 별도의 측정값을 만들어야 하므로 수십 개의 측정값이 발생할 수 있습니다. 사용자의 경우에는 많은 측정값을 기준으로 정렬 하 고 보고서에 개별적으로 적용 하는 것을 의미할 수 있습니다. 

먼저 Power BI와 같은 보고 도구에서 계산 그룹이 사용자에 게 표시 되는 방식을 살펴보겠습니다. 그런 다음 계산 그룹을 구성 하는 항목과 모델에서 생성 되는 방법을 살펴봅니다.

계산 그룹은 보고하는 클라이언트에 단일 열이 있는 테이블로 표시됩니다. 열은 일반적인 열 또는 차원과 유사 하지 않으며, 대신 다시 사용할 수 있는 하나 이상의 계산 또는 시각화에 대 한 값 필터에 이미 추가 된 측정값에 적용 될 수 있는 *계산 항목* 을 나타냅니다.

다음 애니메이션에서 사용자는 연도 2012 및 2013에 대 한 판매 데이터를 분석 합니다. 계산 그룹을 적용 하기 전에 공통 기본 측정값 **판매량** 은 매월 총 판매량의 합계를 계산 합니다. 그런 다음 사용자는 월간 누계, 분기별 누계, 연간 누계 등에 대 한 판매량 합계를 얻기 위해 시간 인텔리전스 계산을 적용 하려고 합니다. 계산 그룹이 없는 경우 사용자는 개별 시간 인텔리전스 측정값을 선택 해야 합니다.

계산 그룹을 사용 하는 경우이 예제에서 **Time Intelligence**라는 사용자가 **시간 계산** 항목을 **열** 필터 영역으로 끌면 각 계산 항목이 개별 열로 표시 됩니다. 각 행에 대 한 값은 기본 측정값 **Sales**에서 계산 됩니다.  

![Power BI에서 적용 되는 계산 그룹](media/calculation-groups/calc-groups-pbi.gif)


계산 그룹은 **명시적인** DAX 측정값과 함께 작동 합니다. 이 예에서는 **Sales** 가 모델에 이미 생성 된 명시적 측정값입니다. 계산 그룹은 암시적 DAX 측정값과 함께 작동 하지 않습니다. 예를 들어 Power BI 암시적 측정값은 사용자가 명시적 측정값을 생성 하지 않고도 시각적 개체에 열을 끌어 집계 된 값을 볼 때 생성 됩니다. 현재는 Power BI 인라인 DAX 계산으로 작성 된 암시적 측정값에 대해 DAX를 생성 합니다. 즉, 암시적 측정값은 계산 그룹에서 사용할 수 없습니다. TOM (테이블 형식 개체 모델)에 표시 되는 새 모델 속성은 **DiscourageImplicitMeasures**가 도입 되었습니다. 현재 계산 그룹을 만들려면이 속성을 **true**로 설정 해야 합니다. True로 설정 하면 라이브 연결 모드에서 Power BI Desktop 하 여 암시적 측정값을 만들 수 없습니다.

## <a name="how-they-work"></a>작동 방식

계산 그룹이 사용자에 게 어떤 이점을 제공 하는지 살펴보았으므로 이제 표시 된 시간 인텔리전스 계산 그룹 예제가 어떻게 만들어졌는지 살펴보겠습니다.

자세히 설명 하기 전에 계산 그룹에 대 한 몇 가지 새로운 DAX 함수를 소개 하겠습니다. 

[Selectedmeasure](https://docs.microsoft.com/dax/selectedmeasure-function-dax) -계산 항목에서 현재 컨텍스트에 있는 측정값을 참조 하는 데 사용 되는 식입니다. 이 예에서는 Sales 측정값이 있습니다.

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) -계산 항목에 대 한 식에서 이름별로 컨텍스트의 측정값을 결정 하는 데 사용 됩니다.

[Isselectedmeasure](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) -컨텍스트 내에 있는 측정값을 결정 하기 위해 계산 항목에 대해 식에서 사용 되는 측정값은 측정값 목록에 지정 됩니다.

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax) -계산 항목에서 컨텍스트에 있는 측정값의 형식 문자열을 검색 하는 데 사용 됩니다.

### <a name="time-intelligence-example"></a>시간 인텔리전스 예

테이블 이름- **시간 인텔리전스**   
열 이름- **시간 계산**   
우선 순위- **20**   

#### <a name="time-intelligence-calculation-items"></a>시간 인텔리전스 계산 항목

**Current**

```dax
SELECTEDMEASURE()
```

**MTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESMTD(DimDate[Date]))
```

**QTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESQTD(DimDate[Date]))
```

**YTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

**PY**

```dax
CALCULATE(SELECTEDMEASURE(), SAMEPERIODLASTYEAR(DimDate[Date]))
```

**PY MTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "MTD"
)
```

**PY QTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "QTD"
)
```

**PY YTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

**YOY**

```dax
SELECTEDMEASURE() –
CALCULATE(
    SELECTEDMEASURE(),
    'Time Intelligence'[Time Calculation] = "PY"
)
```

**YOY%**

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

이 계산 그룹을 테스트 하기 위해 SSMS 또는 오픈 소스 [Dax 스튜디오](http://daxstudio.org/)에서 dax 쿼리를 실행할 수 있습니다. YOY 및 YOY%는이 쿼리 예제에서 생략 됩니다.

#### <a name="time-intelligence-query"></a>시간 인텔리전스 쿼리

```dax
EVALUATE
CALCULATETABLE (
    SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Current", CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "Current" ),
        "QTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "QTD" ),
        "YTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "YTD" ),
        "PY",      CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY" ),
        "PY QTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY QTD" ),
        "PY YTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY YTD" )
    ),
    DimDate[CalendarYear] IN { 2012, 2013 }
)
```

#### <a name="time-intelligence-query-return"></a>시간 인텔리전스 쿼리 반환

반환 테이블은 적용 된 각 계산 항목에 대 한 계산을 보여 줍니다. 예를 들어 3 월 2012에 대 한 QTD는 1 월, 2 월 및 3 월 2012의 합계를 볼 수 있습니다.

![쿼리 반환](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>동적 서식 문자열

계산 그룹이 있는 *동적 형식 문자열* 을 사용 하면 문자열을 반환 하지 않고도 측정값에 서식 문자열을 적용할 수 있습니다.

테이블 형식 모델은 DAX의 [FORMAT](https://docs.microsoft.com/dax/format-function-dax) 함수를 사용 하 여 측정값의 동적 서식 지정을 지원 합니다. 그러나 FORMAT 함수는 문자열을 반환 하는 단점이 있으며 그렇지 않은 경우에도 문자열로 반환 되는 측정값이 되도록 합니다. 여기에는 차트와 같은 숫자 값에 따라 대부분의 Power BI 시각적 개체를 사용 하지 않는 것과 같은 몇 가지 제한 사항이 있을 수 있습니다.

### <a name="dynamic-format-strings-for-time-intelligence"></a>시계열에 대 한 동적 형식 문자열

위에 표시 된 시간 인텔리전스 예를 살펴보면 **YOY%** 를 제외한 모든 계산 항목이 컨텍스트에서 현재 측정값의 형식을 사용 해야 합니다. 예를 들어 Sales 기본 측정값에서 계산 된 **YTD** 는 통화 여야 합니다. 주문 기준 측정값과 같은 항목에 대 한 계산 그룹인 경우에는 숫자 형식입니다. 그러나 **YOY%** 는 기본 측정값의 형식에 관계 없이 백분율 이어야 합니다.

**YOY%** 의 경우 형식 문자열 식 속성을 **0.00%;-0.00%; 0.00%** 로 설정 하 여 서식 문자열을 재정의할 수 있습니다. 서식 문자열 식 속성에 대해 자세히 알아보려면 [MDX 셀 속성-형식 문자열 내용](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values)을 참조 하세요.

Power BI의이 행렬 시각적 개체에는 **Sales current/YOY** 가 표시 되 고 **ORDERS current/YOY** 는 해당 기본 측정값 형식 문자열을 유지 합니다. 그러나 **SALES YOY%** 와 **Orders YOY%** 는 형식 문자열을 사용 하 여 *백분율* 형식을 재정의 합니다.

![매트릭스 시각적 개체의 시간 인텔리전스](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>통화 변환에 대 한 동적 서식 문자열

동적 서식 문자열은 간편한 통화 변환을 제공 합니다. 다음 놀이 Works 데이터 모델을 고려 합니다. [변환 형식](../currency-conversions-analysis-services.md#conversion-types)에 의해 정의 된 대로 *일대다 통화 변환* 에 대해 모델링 됩니다.

![테이블 형식 모델의 통화 율](media/calculation-groups/calc-groups-currency-conversion.png)

**FormatString** 열은 **이 테이블에** 추가 되 고 해당 통화에 대 한 형식 문자열로 채워집니다.

![문자열 열 서식 지정](media/calculation-groups/calc-groups-formatstringcolumn.png)

이 예의 경우 다음 계산 그룹은 다음과 같이 정의 됩니다.

### <a name="currency-conversion-example"></a>통화 변환 예

테이블 이름- **통화 변환**   
열 이름- **변환 계산**   
우선 순위- **5**   

#### <a name="calculation-items-for-currency-conversion"></a>통화 변환에 대 한 계산 항목

**변환 안 함**

```dax
SELECTEDMEASURE()
```

**변환 된 통화**

```dax
IF(
    //Check one currency in context & not US Dollar, which is the pivot currency:
    SELECTEDVALUE( DimCurrency[CurrencyName], "US Dollar" ) = "US Dollar",
    SELECTEDMEASURE(),
    SUMX(
        VALUES(DimDate[Date]),
        CALCULATE( DIVIDE( SELECTEDMEASURE(), MAX(FactCurrencyRate[EndOfDayRate]) ) )
    )
)
```

서식 문자열 식

```dax
SELECTEDVALUE(
    DimCurrency[FormatString],
    SELECTEDMEASUREFORMATSTRING()
)
```
서식 문자열 식은 스칼라 문자열을 반환 해야 합니다. 필터 컨텍스트에 여러 통화가 있는 경우 new [SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax) 함수를 사용 하 여 기본 측정값 형식 문자열로 되돌립니다.

다음 애니메이션은 보고서에서 **판매** 측정값의 동적 형식 통화 변환을 보여 줍니다.

![통화 변환 동적 서식 문자열 적용 됨](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>우선 순위

우선 순위는 계산 그룹에 대해 정의 된 속성입니다. 계산 그룹이 둘 이상인 경우의 평가 순서를 지정 합니다. 숫자가 클수록 우선 순위가 높기 때문에 우선 순위가 낮은 계산 그룹이 계산 되기 전에 평가 됩니다.

이 예에서는 위의 시간 인텔리전스 예와 동일한 모델을 사용 하지만 **평균** 계산 그룹도 추가 합니다. 평균 계산 그룹에는 날짜 필터 컨텍스트를 변경 하지 않는 기존 시간 인텔리전스와 무관 한 평균 계산이 포함 되어 있습니다 .이 계산에는 평균 계산만 적용 됩니다.

이 예에서는 일일 평균 계산이 정의 되어 있습니다. 석유 및 가스 응용 프로그램에서 하루 평균 오일 평균 배럴과 같은 계산은 일반적입니다. 기타 일반적인 비즈니스 예제에는 소매점의 매장 판매 평균이 포함 됩니다.

이러한 계산은 시간 인텔리전스 계산과 독립적으로 계산 되지만 결합 해야 할 수도 있습니다. 예를 들어, 사용자는 연간 시작부터 현재 날짜 까지의 일일 석유를 볼 수 있도록 일별 석유의 배럴을 볼 수 있습니다. 이 시나리오에서는 계산 항목에 대해 우선 순위를 설정 해야 합니다.

### <a name="averages-example"></a>평균 예

테이블 이름은 **평균**입니다.   
열 이름은 **평균 계산**입니다.   
우선 순위는 **10**입니다.   

#### <a name="calculation-items-for-averages"></a>평균 계산 항목

**평균 없음**

```dax
SELECTEDMEASURE()
```

**일일 평균**

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

DAX 쿼리 및 반환 테이블의 예는 다음과 같습니다.

#### <a name="averages-query"></a>평균 쿼리

```dax
EVALUATE
    CALCULATETABLE (
        SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Sales", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "No Average"
        ),
        "YTD", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "No Average"
        ),
        "Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "Daily Average"
        ),
        "YTD Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "Daily Average"
        )
    ),
    DimDate[CalendarYear] = 2012
)
```

#### <a name="averages-query-return"></a>평균 쿼리 반환

![쿼리 반환](media/calculation-groups/calc-groups-ytd-daily-avg.png)

다음 표에서는 3 월 2012 값을 계산 하는 방법을 보여 줍니다.


|열 이름  |계산 |
|---------|---------|
|YTD     |    1 월, 2 월, 3 월 2012에 대 한 판매량 합계<br />= 495,364 + 506,994 + 373,483     |
|일일 평균    |     3 월의 일 수로 나눈 3 월 2012 판매<br />= 373,483 / 31       |
|YTD 일별 평균     | 1 월, 2 월, 3 월의 일 수로 나눈 3 월 2012의 YTD<br />= 1375841/(31 + 29 + 31)       |

다음은 우선 순위 **20**으로 적용 된 YTD 계산 항목의 정의입니다.

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

다음은 우선 순위 **10**으로 적용 되는 일일 평균입니다.

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

시간 인텔리전스 계산 그룹의 우선 순위는 평균 계산 그룹의 우선 순위 보다 높기 때문에 최대한 광범위 하 게 적용 됩니다. YTD 일일 평균 계산은 일일 평균 계산의 분자와 분모 (일 수) 모두에 YTD를 적용 합니다.

이는 다음 식과 같습니다.

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

이 식은 아닙니다.

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>사이드 재귀

위의 시간 인텔리전스 예제에서 일부 계산 항목은 동일한 계산 그룹의 다른 항목을 참조 합니다. 이를 *사이드 재귀*라고 합니다. 예를 들어 **YOY%** 는 **YOY** 및 **PY**를 모두 참조 합니다.

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

이 경우 두 식이 서로 다른 calculate 문을 사용 하 고 있으므로 별도로 계산 됩니다. 다른 유형의 재귀는 지원 되지 않습니다.

## <a name="single-calculation-item-in-filter-context"></a>필터 컨텍스트의 단일 계산 항목

시간 인텔리전스 예제에서 **PY YTD** 계산 항목에는 단일 calculate 식이 있습니다.

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

CALCULATE () 함수에 대 한 YTD 인수는 필터 컨텍스트를 재정의 하 여 YTD 계산 항목에 이미 정의 된 논리를 다시 사용 합니다. 단일 평가에서 PY 및 YTD를 모두 적용할 수는 없습니다. 계산 그룹은 계산 그룹의 단일 계산 항목이 필터 컨텍스트에 있는 경우에 *만 적용* 됩니다.

## <a name="mdx-support"></a>MDX 지원

계산 그룹은 MDX (Multidimensional Data Expressions) 쿼리를 지원 합니다. 즉, MDX를 사용 하 여 테이블 형식 데이터 모델을 쿼리 하는 Microsoft Excel 사용자는 워크시트 피벗 테이블 및 차트의 계산 그룹을 최대한 활용할 수 있습니다.

## <a name="tools"></a>Tools

계산 그룹은 Analysis Services 확장을 포함 하는 SQL Server Data Tools Visual Studio에서 아직 지원 되지 않습니다. 그러나 TMSL (Tabular Model Scripting Language) 또는 오픈 소스 [테이블 형식 편집기](https://github.com/otykier/TabularEditor)를 사용 하 여 계산 그룹을 만들 수 있습니다.

## <a name="limitations"></a>제한 사항

[개체 수준 보안](object-level-security.md) 계산 그룹 테이블에 정의 된 (OLS)는 지원 되지 않습니다. 그러나 동일한 모델의 다른 테이블에 대해 OLS를 정의할 수 있습니다. 계산 항목이 OLS 보안 개체를 참조 하는 경우 일반 오류가 반환 됩니다.

[행 수준 보안](roles-ssas-tabular.md#bkmk_rowfliters) (RLS)는 지원 되지 않습니다. 동일한 모델의 테이블에 RLS를 정의할 수 있지만 직접 또는 간접적으로 계산 그룹에는 정의할 수 없습니다.

## <a name="see-also"></a>참조  

[테이블 형식 모델의 DAX](understanding-dax-in-tabular-models-ssas-tabular.md)   
[DAX 참조](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  
