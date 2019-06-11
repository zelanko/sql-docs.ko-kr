---
title: Analysis Services 테이블 형식 모델에 계산 그룹 | Microsoft Docs
ms.date: 06/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: abc1f51d21613676fd94271f931e1a7692cc1efc
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822695"
---
# <a name="calculation-groups-preview"></a>계산 그룹 (미리 보기)
 
[!INCLUDE[ssas-appliesto-sql2019-aas](../../includes/ssas-appliesto-sql2019-aas.md)]

일반 측정값 식으로 그룹화 하 여 계산 그룹 중복 측정값의 수를 크게 줄일 수 있습니다 *계산 항목*합니다. 계산 그룹은 Azure Analysis Services에서 지원 및 SQL Server Analysis Services 2019 테이블 형식 모델 이상으로 1470 [호환성 수준](compatibility-level-for-tabular-models-in-analysis-services.md)합니다. 1470 호환성 수준의 모델은 현재 **미리 보기**합니다.  

이 문서에서는 다음에 대해 설명합니다. 

> [!div class="checklist"]
> * 이점 
> * 계산 그룹 작동 방식
> * 동적 형식 문자열
> * 우선 순위
> * Tools
> * 제한 사항



## <a name="benefits"></a>이점

계산 그룹에 있을 수 있는 복잡 한 모델의 문제를 해결할 시간 인텔리전스 계산을 사용 하 여 가장 일반적인과 같은 계산-를 사용 하 여 중복 측정값입니다. 예를 들어, 판매 분석가가 판매량 합계를 표시 하려고 하 고 월-날짜 (MTD) 분기 종료 날짜 (QTD)를 기준으로 정렬 연도-날짜 (YTD) 연도-날짜 이전 연도 (PY), 등에 대 한 정렬 합니다. 데이터 모델러는 수십 개의 측정값으로 이어질 수 있습니다 각 계산을 위해 별도 측정값을 만들 해야 합니다. 사용자에 대해이 만큼만 측정값을 통해 정렬 하는 것을 의미 하 고 해당 보고서에 개별적으로 적용할 수 있습니다. 

먼저 Power BI와 같은 보고 도구에서 사용자에 게 계산 그룹을 표시 하는 방법에 대해를 살펴보겠습니다. 계산 그룹을 구성 하는 요소 및 모델에서 생성 하는 방법 살펴보기 다음 알아보겠습니다.

계산 그룹은 보고하는 클라이언트에 단일 열이 있는 테이블로 표시됩니다. 열 같은 일반적인 열 또는 차원에 하나 이상의 다시 사용할 수 있는 계산을 나타내므로 대신 또는 *계산 항목* 는 시각화에 대 한 값 필터에 이미 추가 된 모든 측정값에 적용할 수 있습니다.

다음 애니메이션에서 사용자 2012 및 2013 년에 대 한 판매 데이터를 분석 됩니다. 계산 그룹에 일반적인 기본 측정값을 적용 하기 전에 **판매** 각 월에 대 한 총 판매액의 합계를 계산 합니다. 그런 다음 사용자는 월간 누계 분기 누계 연간 누계에 대 한 판매량 합계를 가져오고 등 시간 인텔리전스 계산을 적용 하려고 합니다. 계산 그룹 없이 사용자는 개별 시간 인텔리전스 측정값을 선택 해야 합니다.

이 예제에서는 명명 된 계산 그룹을 사용 하 여 **시간 인텔리전스**를 끌 때 합니다 **시간 계산** 항목을 **열** 영역에서 각 계산 항목 필터링 별도 열으로 표시 됩니다. 각 행에 대 한 값은 기본 측정값에서 계산 됩니다 **Sales**합니다.  

![Power BI에서 적용 되는 계산 그룹](media/calculation-groups/calc-groups-pbi.gif)


계산 그룹 작업할 **명시적** DAX 측정값입니다. 이 예에서 **Sales** 모델에서 이미 만든 명시적 측정값은입니다. 계산 그룹 암시적 DAX 측정값을 사용 하 여 작동 하지 않습니다. 예를 들어, Power BI에서 사용자가 집계 된 값을 명시적 측정값을 만들지 않고 표시할 시각적 개체에 열을 끌 때 암시적 측정값이 생성 됩니다. 지금은 Power BI는 암시적 측정값 즉 암시적 측정값 수 없습니다. 계산 그룹을 사용 하는 DAX 계산-인라인으로 작성에 대 한 DAX를 생성 합니다. 새 모델 속성이 표시에 개체 모델 TOM (테이블 형식)가 도입 되어 **DiscourageImplicitMeasures**합니다. 이 속성 계산 그룹을 만들기 위해 현재로 설정 되어야 합니다 **true**합니다. 모드를 Live Connect에서 Power BI Desktop을 true로 설정 하면 암시적 측정값의 생성을 사용 하지 않습니다.

## <a name="how-they-work"></a>작동 방식

계산 그룹 사용자를 활용 하는 방법을 살펴보았습니다 했으므로 표시 된 시간 인텔리전스 계산 그룹 예제를 만드는 방법을 살펴를 보겠습니다.

세부 정보를 살펴보기 전에 특별히 계산 그룹에 대 한 몇 가지 새 DAX 함수를 소개 하겠습니다. 

[SELECTEDMEASURE](https://docs.microsoft.com/dax/selectedmeasure-function-dax) -계산 컨텍스트에서 현재는 측정값을 참조 하는 항목에 대 한 식으로 사용 합니다. 이 예제에서는 판매를 측정 합니다.

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) -계산 컨텍스트에서 이름으로 사용할 측정값을 확인 하는 항목에 대 한 식으로 사용 합니다.

[ISSELECTEDMEASURE](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) -계산 컨텍스트에서 측정값의 측정값 목록에 지정 된 결정 하는 항목에 대 한 식으로 사용 합니다.

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax) -계산 컨텍스트에서 측정값의 형식 문자열을 검색 하는 항목에 대 한 식으로 사용 합니다.

### <a name="time-intelligence-example"></a>시간 인텔리전스 예제

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

이 계산 그룹을 테스트 하려면 SSMS 또는 오픈 소스에서 DAX 쿼리를 실행할 수 있습니다 [DAX Studio](http://daxstudio.org/)합니다. YOY 및 YOY % 쿼리 예제에서 생략 됩니다.

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

반환 테이블 항목을 적용 하는 각 계산에 대 한 계산을 보여 줍니다. 예를 들어 2012 년 3 월에 대 한 QTD 값은 1 월, 년 2 월 및 2012 년 3 월 합계를 볼 수 있습니다.

![쿼리 반환](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>동적 형식 문자열

*동적 형식 문자열* 계산을 사용 하 여 그룹 문자열을 반환 하도록 하지 않고도 측정값 서식 문자열의 조건부 응용 프로그램을 사용 합니다.

테이블 형식 모델의 DAX를 사용 하 여 측정값을 동적 서식을 지원 [형식](https://docs.microsoft.com/dax/format-function-dax) 함수입니다. 그러나 FORMAT 함수의 단점이 숫자를 문자열로 반환 될 수 있는 측정값을 강제 적용 하는 문자열을 반환 합니다. 이 차트와 같은 숫자 값에 따라 대부분의 Power BI 시각적 개체를 사용 하 여 작동 하지 등의 몇 가지 제한 사항이 있습니다.

### <a name="dynamic-format-strings-for-time-intelligence"></a>시간 인텔리전스에 대 한 동적 서식 문자열

모든 계산을 제외한 항목 위에 표시 된 시간 인텔리전스 예제를 보면 **YOY %** 컨텍스트에서 현재 측정값의 형식을 사용 해야 합니다. 예를 들어 **YTD** 통화 Sales 기본 측정값으로 계산 해야 합니다. 같이 Orders 기본 측정값에 대 한 계산 그룹의 경우에 형식 숫자 것입니다. **그러나 YOY %** , 기본 측정값의 형식에 관계 없이 백분율로 있어야 합니다.

에 대 한 **yoy**, 형식 문자열을 형식 문자열 식 속성을 설정 하 여 재정의할 수 있습니다 **0.00%;-0.00%; 0.00%** 합니다. 형식 문자열 식 속성에 대 한 자세한 내용은 참조 하세요 [MDX 셀 속성-형식 문자열 내용을](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values)합니다.

Power BI에서 시각적이 행렬에 표시 **Sales 현재/YOY** 하 고 **주문 현재/YOY** 가 해당 기본 측정값 서식 문자열을 유지 합니다. **하지만 판매 YOY %** 및 **YOY % 정렬**를 사용 하는 형식 문자열을 재정의 *백분율* 형식입니다.

![행렬 시각적 개체에서 시간 인텔리전스](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>통화 변환에 대 한 동적 서식 문자열

동적 형식 문자열에는 쉽게 통화 변환을 제공합니다. 다음 Adventure Works 데이터 모델을 고려 합니다. 에 대 한 모델링 됩니다 *-일대다* 통화 변환 정의 된 대로 [변환 유형을](../currency-conversions-analysis-services.md#conversion-types)합니다.

![테이블 형식 모델에서 통화 요금](media/calculation-groups/calc-groups-currency-conversion.png)

**FormatString** 열에 추가 되는 **DimCurrency** 테이블 및 각 통화에 대 한 형식 문자열을 사용 하 여 채워집니다.

![문자열 열 서식 지정](media/calculation-groups/calc-groups-formatstringcolumn.png)

예를 들어 다음 계산 그룹 다음으로 정의 됩니다.

### <a name="currency-conversion-example"></a>통화 변환 예제

테이블 이름- **통화 변환**   
열 이름- **변환 계산**   
우선 순위- **5**   

#### <a name="calculation-items-for-currency-conversion"></a>통화 변환에 대 한 계산 항목

**변환 작업 없이**

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

형식 문자열 식

```dax
SELECTEDVALUE(
    DimCurrency[FormatString],
    SELECTEDMEASUREFORMATSTRING()
)
```
형식 문자열 식에는 스칼라 문자열을 반환 해야 합니다. 사용 하 여 새 [SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax) 필터 컨텍스트에 포함 된 여러 통화 없으면 기본 측정값 서식 문자열과 되돌리려면 함수입니다.

다음 애니메이션 형식의 동적 통화 변환을 보여 줍니다.는 **Sales** 보고서의 측정값입니다.

![통화 변환 동적 형식 문자열 적용](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>우선 순위

우선 순위에는 계산 그룹에 대해 정의 된 속성입니다. 계산 그룹 둘 이상의 경우 평가 순서를 지정 합니다. 더 큰 값을 우선 순위가 낮은 계산 그룹 보다 먼저 계산 되도록 하므로 큰 우선 순위를 나타냅니다.

예를 들어 시간 인텔리전스 위 예제에서와 동일한 모델을 사용 하지만 추가 됩니다 것를 **평균** 계산 그룹입니다. 평균 계산 그룹 날짜 필터 컨텍스트가 바뀌지는 않으며-평균 계산에만 적용 되는 기존의 시간 인텔리전스와 독립 된 평균 계산을 포함 합니다.

이 예제에서는 일별 평균 계산 정의 됩니다. 매일의 평균 통 같은 계산은 오일 및 가스 응용 프로그램에서 일반적입니다. 다른 일반적인 비즈니스 예로 저장소 판매 평균 소매에 있습니다.

이러한 계산 시간 인텔리전스 계산 독립적으로 계산 되는 동안 결합 하는 요구 사항이 수도 있습니다. 예를 들어, 사용자 수의 현재 날짜를 연도 초부터 일별 석유 요금을 보려면 YTD 하루 barrel 참조 하려고 합니다. 이 시나리오에서는 계산 항목에 대 한 우선 순위를 설정 해야 합니다.

### <a name="averages-example"></a>평균 예제

테이블 이름은 **평균**합니다.   
열 이름은 **평균 계산**합니다.   
우선 순위 **10**합니다.   

#### <a name="calculation-items-for-averages"></a>평균에 대 한 계산 항목

**평균 없음**

```dax
SELECTEDMEASURE()
```

**일별 평균**

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

다음 표에서 2012 년 3 월 값이 계산 되는 방법을 보여 줍니다.


|열 이름  |계산 |
|---------|---------|
|YTD     |    Jan, Feb, Mar 2012에 대 한 판매량 합계<br />= 495,364 + 506,994 + 373,483     |
|일별 평균    |     Mar 2012 년 3 월의 일 수로 나눈 값에 대 한 판매<br />= 373,483 / 31       |
|YTD 일일 평균     | 2012 년 3 월 YTD Jan, Feb, 및 3 월의 일 수로 나눈 값<br />=  1,375,841 / (31 + 29 + 31)       |

우선 순위를 사용 하 여 적용 YTD 계산 항목의 정의 같습니다 **20**합니다.

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

일일 평균의 우선 순위가 적용 다음과 같습니다 **10**합니다.

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

시간 인텔리전스 계산 그룹의 우선 순위 보다 평균 계산 그룹 이므로으로 최대한 광범위 하 게 적용 됩니다. YTD 일일 평균 계산에는 분자와 분모 (사용 일 수)의 일일 평균 계산에 YTD 적용 됩니다.

다음 식으로는 것과 같습니다.

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

이 식이 아닙니다.

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>옆쪽 재귀

위의 코드 예에서 시간 인텔리전스를 동일한 계산 그룹의 다른 사용자에 게 참조 계산 항목 중 일부입니다. 이 이라고 *옆쪽 재귀*합니다. 예를 들어 **yoy** 둘 다 참조 **YOY** 하 고 **PY**합니다.

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

두 식을 모두 개별적으로 계산이 경우 다른 사용 하기 때문에 문을 계산 합니다. 다른 유형의 재귀 지원 되지 않습니다.

## <a name="single-calculation-item-in-filter-context"></a>필터 컨텍스트에 있는 단일 계산 항목

시간 인텔리전스 예제의 합니다 **PY YTD** 계산 항목에는 단일 식 계산:

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

YTD CALCULATE() 함수 인수 YTD 계산 항목에 이미 정의 된 논리를 다시 사용 하려면 필터 컨텍스트를 재정의 합니다. 단일 평가에서 PY 수 및 YTD 모두 적용 하는 것이 불가능 합니다. 계산 그룹은 *에 적용* 항목이 있는 경우 단일 계산의 계산 그룹에서 필터 컨텍스트에서 합니다.

## <a name="mdx-support"></a>MDX 지원

계산 그룹 데이터 MDX (Multidimensional Expressions) 쿼리를 지원합니다. 즉, Microsoft Excel 사용자는 쿼리 테이블 형식 데이터 모델, MDX를 사용 하 여 피벗 테이블을 워크시트에 계산 그룹 및 차트 모두 사용할 수 있습니다.

## <a name="tools"></a>Tools

계산 그룹 SQL Server Data Tools, Analysis Services 확장을 사용 하 여 Visual Studio에서에서 아직 지원 되지 않습니다. 그러나 TMSL Tabular Model Scripting Language () 또는 오픈 소스를 사용 하 여 계산 그룹을 만들 수 있습니다 [테이블 형식 편집기](https://github.com/otykier/TabularEditor)합니다.

## <a name="limitations"></a>제한 사항

[개체 수준 보안](object-level-security.md) (OLS) 계산에 정의 된 그룹 테이블은 지원 되지 않습니다. 그러나 OLS 동일한 모델의 다른 테이블에 정의할 수 있습니다. 계산 항목 OLS 보안된 개체를 가리키는 경우 일반 오류가 반환 됩니다.

[행 수준 보안](roles-ssas-tabular.md#bkmk_rowfliters) (RLS) 지원 되지 않습니다. 정의한 RLS 계산 그룹 자체에 없지만 동일한 모델의 테이블에서 (직접 또는 간접적으로).

[행 식에 자세히 설명](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md) 계산 그룹은 지원 되지 않습니다.

## <a name="see-also"></a>참고자료  

[테이블 형식 모델의 DAX](understanding-dax-in-tabular-models-ssas-tabular.md)   
[DAX 참조](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  
