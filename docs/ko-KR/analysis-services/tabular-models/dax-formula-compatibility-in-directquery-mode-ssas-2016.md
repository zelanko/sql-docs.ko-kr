---
title: DirectQuery 모드에서의 DAX 수식 호환성 | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: multidimensional-tabular
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d2fbafe6-d7fb-437b-b32b-fa2446023fa5
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 106e22e43ec0bb6003869cc264388c741d7528d0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dax-formula-compatibility-in-directquery-mode"></a>DirectQuery 모드에서의 DAX 수식 호환성 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
테이블 형식 1200 이상 모델에 DirectQuery 모드에서 이전 버전에서 많은 기능 제한 사항이 더 이상 적용 됩니다. 특히 DAX 수식에서:

- 이제 DirectQuery에서 더 단순한 쿼리를 생성하고 향상된 성능을 제공합니다.
- 행 수준 보안 (RLS)은 이제 DirectQuery 모드에서 지원 됩니다.
- 이제 DirectQuery 모드에서 테이블 형식 모델에 대 한 계산 된 열이 지원 됩니다.

## <a name="dax-functions-in-directquery-mode"></a>DirectQuery 모드의 DAX 함수

즉, 모든 DAX 함수는 DirectQuery 모델에 대해 지원 됩니다. 그러나 일부 함수는 모든 수식 유형에 대 한 지원 및 DirectQuery 모델에 대해 최적화 된 모든 함수입니다. 기본적으로 DAX 함수는 최적화된 함수와 최적화되지 않은 함수, 두 그룹으로 나뉩니다. 먼저 최적화된 함수를 살펴보겠습니다.


### <a name="optimized-for-directquery"></a>DirectQuery에 대해 최적화된 함수
주로 스칼라 또는 집계 결과를 반환하는 함수입니다. 이러한 함수는 모든 유형의 수식(측정값, 쿼리, 계산 열, 행 수준 보안)에서 지원되는 함수와 측정값 및 쿼리 수식에서만 지원되는 함수로 세분화됩니다. 이러한 개체는 다음과 같습니다.    

| 모든 DAX 수식에서 지원                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | 측정값 및 쿼리 수식에서 지원                                                                                                                                                                                                                                                                                                |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ABS</br>  ACOS</br>  ACOT</br>  및</br>  ASIN</br>  ATAN</br>  공백</br>  CEILING</br>  CONCATENATE</br>  COS</br>  COT</br>  Currency</br>  DATE</br>  DATEDIFF</br>  DATEVALUE</br>  DAY</br>  DEGREES</br>  DIVIDE</br>  EDATE</br>  EOMONTH</br>  EXACT</br>  EXP</br>  FALSE</br>  FIND</br>  HOUR</br>  IF</br>  INT</br>  ISBLANK</br>  ISO.CEILING</br>  KEEPFILTERS</br>  LEFT</br>  LEN</br>  LN</br>  LOG</br>  LOG10</br>  LOWER</br>  MAX</br>  MID</br>  MIN</br>  MINUTE</br>  MOD</br>  MONTH</br>  MROUND</br>  NOT</br>  NOW</br>  OR</br>  PI</br>  POWER</br>  QUOTIENT</br>  RADIANS</br>  RAND</br>  RELATED</br>  REPT</br>  RIGHT</br>  ROUND</br>  ROUNDDOWN</br>  ROUNDUP</br>  SEARCH</br>  SECOND</br>  SIGN</br>  SIN</br>  SQRT</br>  SQRTPI</br>  SUBSTITUTE</br>  SWITCH</br>  TAN</br>  TIME</br>  TIMEVALUE</br>  TODAY</br>  TRIM</br>  TRUE</br>  TRUNC</br>  UNICODE</br>  UPPER</br>  USERNAME</br>  USERELATIONSHIP</br>  값</br>  WEEKDAY</br>  WEEKNUM</br>  YEAR</br> | ALL</br> ALLEXCEPT</br> ALLNOBLANKROW</br> ALLSELECTED</br> AVERAGE</br> AVERAGEA</br> AVERAGEX</br> CALCULATE</br> CALCULATETABLE</br> COUNT</br> COUNTA</br> COUNTAX</br> COUNTROWS</br> COUNTX</br> DISTINCT</br> DISTINCTCOUNT</br> FILTER</br> FILTERS</br> HASONEFILTER</br> HASONEVALUE</br> ISCROSSFILTERED</br> ISFILTERED</br> MAXA</br> MAXX</br> MIN</br> MINA</br> MINX</br> RELATEDTABLE</br> STDEV.P</br> STDEV.S</br> STDEVX.P</br> STDEVX.S</br> SUM</br> SUMX</br> VALUES</br> VAR.P</br> VAR.S</br> VARX.P</br> VARX.S |



### <a name="non-optimized-for-directquery"></a>DirectQuery에 대해 최적화되지 않은 함수
이러한 함수 DirectQuery 작업 때 최적화 되지 않습니다. 이러한 함수는 계산 열 및 행 수준 보안 수식에서 지원되지 *않습니다* . 측정값과 쿼리 수식에서 *지원되지만* 성능은 확실하지 않습니다.

 여기에서 모든 함수를 나열하지는 않습니다. 기본적으로 위의 최적화된 함수 목록에 없으면 DirectQuery에 대해 최적화되지 않은 것입니다.

특정 함수가 DirectQuery에 대해 최적화되지 않은 이유는 기본 관계형 엔진에서 xVelocity 엔진에서 수행한 것과 동일한 계산을 수행할 수 없거나 수식을 동등한 SQL 식으로 변환할 수 없기 때문입니다. 다른 경우에는 변환된 식 및 결과 계산의 성능이 허용 가능한 수준이 아닐 수 있습니다.

일부 DAX 함수에 대해 알아보려면 참조 [DAX 함수 참조]. (https://msdn.microsoft.com/en-us/library/ee634396.aspx)

## <a name="dax-operators-in-directquery-mode"></a>DirectQuery 모드의 DAX 연산자
모든 DAX 비교 및 산술 연산자는 DirectQuery 모드에서 완벽 하 게 지원 됩니다. 자세한 내용은 [DAX 연산자 참조](https://msdn.microsoft.com/library/ee634237.aspx)를 참조하세요.


 
## <a name="differences-between-in-memory-and-directquery-mode"></a>메모리 내 모드와 DirectQuery 모드 간의 차이점  
DirectQuery 모드로 배포된 모델에 대한 쿼리에서는 동일한 모델이 메모리 내 모드로 배포되었을 때와 다른 결과를 반환할 수 있습니다. 이는 DirectQuery를 사용할 경우 데이터가 관계형 데이터 저장소에서 직접 쿼리되고, 수식에 필요한 집계가 저장 및 계산용 xVelocity 메모리 내 분석 엔진 대신 관련된 관계형 엔진(SQL, Oracle, Teradata)을 사용하여 수행되기 때문입니다.  
  
예를 들어 일부 관계형 데이터 저장소는 숫자 값, 날짜, Null 등을 처리하는 방식에 차이점이 있습니다.  
  
반면 DAX 언어는 Microsoft Excel의 함수 동작을 가능한 한 비슷하게 에뮬레이트하기 위한 것입니다. 예를 들어 Null, 빈 문자열 및 0 값을 처리할 때 Excel에서는 정확한 데이터 형식에 관계없이 최상의 답을 제공하려고 하므로 xVelocity 엔진에서도 이와 동일하게 동작합니다. 그러나 DirectQuery 모드로 배포된 테이블 형식 모델에서 관계형 데이터 원본에 수식을 전달할 경우 데이터는 관계형 데이터 원본의 의미 체계에 따라 처리되어야 합니다. 이 경우 일반적으로 빈 문자열과 Null은 서로 다르게 처리되어야 합니다. 이 때문에 동일한 수식이라도 캐시된 데이터에 대해 실행될 때와 관계형 저장소에서만 인출된 데이터에 대해 실행될 때 서로 다른 결과를 반환할 수 있습니다.  
  
또한 일부 함수의 경우에는 계산 시 현재 컨텍스트의 데이터를 관계형 데이터 원본에 매개 변수로 보내야 하므로 DirectQuery 모드에 대해 최적화되지 않습니다. 예를 들어 달력 테이블에서 날짜 범위를 참조하는 시간 인텔리전스 함수를 사용하여 측정합니다. 관계형 데이터 원본에는 달력 테이블이 없거나 하나 이상 있을 수 있습니다.  
  
## <a name="semantic-differences"></a>의미 체계 차이점  
이 섹션에서는 예상 가능한 의미 체계 차이점의 유형을 나열하고 함수 사용 또는 쿼리 결과에 적용될 수 있는 제한 사항에 대해 설명합니다.  
  
### <a name="comparisons"></a>비교  
메모리 내 모델에서 DAX는 서로 다른 데이터 형식의 스칼라 값으로 확인되는 두 식의 비교를 지원합니다. 그러나 DirectQuery 모드로 배포된 모델에서는 관계형 엔진의 데이터 형식 및 비교 연산자를 사용하므로 다른 결과를 반환할 수 있습니다.  
  
다음 비교는 DirectQuery 데이터 원본에 대한 계산에 사용될 경우 항상 오류를 반환합니다.  
  
-   숫자 데이터 형식과 문자열 데이터 형식 비교  
  
-   숫자 데이터 형식과 부울 값 비교  
  
-   문자열 데이터 형식과 부울 값 비교  
  
일반적으로 메모리 내 모델에서 DAX는 데이터 형식 불일치에 보다 관대하며, 이 섹션에 설명된 것과 같이 최대 두 번까지 값을 암시적으로 캐스팅하려고 합니다. 그러나 DirectQuery 모드에서 관계형 데이터 저장소로 보내진 수식은 관계형 엔진의 규칙에 따라 더 엄격하게 평가되므로 실패할 가능성이 더 높습니다.  
  
**문자열과 숫자 비교**  
예: `“2” < 3`  
  
이 수식은 텍스트 문자열과 숫자를 비교합니다. 이 식은 DirectQuery 모드와 메모리 내 모델 모두에서 **true** 가 됩니다.  
  
메모리 내 모델에서는 문자열로 표현된 숫자가 다른 숫자와의 비교를 위해 숫자 데이터 형식으로 암시적으로 캐스팅되므로 결과가 **true** 가 됩니다. SQL에서도 텍스트 숫자를 숫자 데이터 형식과 비교하기 위해 암시적으로 숫자로 캐스팅합니다.  
  
이는 첫 번째 버전의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에서 변경된 동작으로, 이 버전에서는 텍스트 "2"가 항상 모든 숫자보다 큰 것으로 간주되기 때문에 **false**가 반환되었습니다.  
  
**텍스트와 부울 비교**  
예: `“VERDADERO” = TRUE`  
  
이 식은 텍스트 문자열을 부울 값과 비교합니다. 일반적으로 DirectQuery 또는 메모리 내 모델에서는 문자열 값을 부울 값과 비교하면 오류가 발생합니다. 이 규칙의 유일한 예외는 문자열에 **true** 또는 **false**라는 단어가 포함된 경우입니다. 문자열에 true 또는 false 값이 포함되어 있으면 부울로 변환 후 비교가 수행되어 논리적 결과가 반환됩니다.  
  
**Null 비교**  
예: `EVALUATE ROW("X", BLANK() = BLANK())`  
  
이 수식은 SQL에서 Null에 해당하는 값과 Null을 비교합니다. 메모리 내 모델과 DirectQuery 모델에서 반환 값은 **true** 이며, DirectQuery 모델에서는 메모리 내 모델과 비슷한 동작을 보장하기 위해 프로비전이 수행됩니다.  
  
Transact-SQL에서는 Null이 Null과 같을 수 없습니다. 그러나 DAX에서는 빈 값이 다른 빈 값과 같습니다. 이 동작은 모든 메모리 내 모델에 대해 동일합니다. DirectQuery 모드에서는 대부분의 SQL Server 의미 체계를 사용하지만 이 경우에는 NULL 비교에 새로운 동작을 제공하여 SQL Server 의미 체계와 구별된다는 점을 주의해야 합니다.  
  
### <a name="casts"></a>캐스팅  
  
DAX에는 일반적인 의미의 캐스팅 함수는 없지만 많은 비교 및 산술 연산에서 암시적 캐스팅이 수행됩니다. 결과의 데이터 형식은 비교 또는 산술 연산에 의해 결정됩니다. 예를 들면 다음과 같습니다.  
  
-   TRUE + 1과 같은 산술 연산이나 부울 값 열에 적용된 MIN 함수에서 부울 값은 숫자로 처리됩니다. NOT 연산에서도 숫자 값을 반환합니다.  
  
-   비교에 사용될 때와 EXACT, AND, OR, &amp;&amp;또는 ||와 함께 사용될 때 부울 값은 항상 논리적 값으로 처리됩니다.  
  
**문자열에서 부울로 캐스팅**  
메모리 내 모델과 DirectQuery 모델에서는 **“”** (빈 문자열), **“true”**및 **“false”**문자열만 부울 값으로 캐스팅할 수 있습니다. 빈 문자열은 false 값으로 캐스팅됩니다.  
  
다른 문자열을 부울 데이터 형식으로 캐스팅하면 오류가 발생합니다.  
  
**문자열에서 날짜/시간으로 캐스팅**  
DirectQuery 모드에서 날짜 및 시간의 문자열 표현을 실제 **datetime** 값으로 캐스팅하는 동작은 SQL Server에서와 동일합니다.   
  
메모리 내 데이터 저장소를 사용하는 모델에서 지원되는 텍스트 형식 날짜의 범위는 SQL Server에서 지원되는 문자열 형식 날짜의 범위보다 제한적입니다. 그러나 DAX에서는 사용자 지정 날짜 및 시간 형식이 지원됩니다.  
  
**문자열에서 부울이 아닌 다른 값으로 캐스팅**  
문자열에서 부울이 아닌 값으로 캐스팅할 때 DirectQuery 모드는 SQL Server와 동일하게 작동합니다. 자세한 내용은 [CAST 및 CONVERT(Transact-SQL)](http://msdn.microsoft.com/en-us/a87d0850-c670-4720-9ad5-6f5a22343ea8)를 참조하세요.  
  
**숫자에서 문자열로의 캐스팅이 허용되지 않음**  
예: `CONCATENATE(102,”,345”)`  
  
SQL Server에서는 숫자에서 문자열로의 캐스팅이 허용되지 않습니다.  
  
이 수식은 테이블 형식 모델과 DirectQuery 모드에서 오류를 반환하지만 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에서는 결과를 생성합니다.  
  
**DirectQuery에서 2번의 캐스팅 시도가 지원되지 않음**  
메모리 내 모델에서는 대개 첫 번째 캐스팅 시도가 실패하면 두 번째 캐스팅을 시도합니다. DirectQuery 모드에서는 두 번째 시도가 수행되지 않습니다.  
  
예: `TODAY() + “13:14:15”`  
  
이 식에서 첫 번째 매개 변수는 **datetime** 형식이고 두 번째 매개 변수는 **string**형식입니다. 그러나 피연산자를 결합할 때 캐스팅은 다르게 처리됩니다. DAX에서는 **string** 에서 **double**로의 암시적 캐스팅을 수행합니다. 메모리 내 모델에서는 수식 엔진이 **double**로 직접 캐스팅하려고 시도하고, 이 시도가 실패하면 문자열을 **datetime**으로 캐스팅하려고 시도합니다.  
  
DirectQuery 모드에서는 **string** 에서 **double** 로의 직접 캐스팅만 적용됩니다. 이 캐스팅이 실패하면 수식에서 오류가 반환됩니다.  
  
### <a name="math-functions-and-arithmetic-operations"></a>수학 함수 및 산술 연산  
일부 수학 함수의 경우 DirectQuery 모드에서는 기본 데이터 형식과 연산에서 적용할 수 있는 캐스팅에 차이가 있기 때문에 다른 결과를 반환합니다. 또한 위에서 설명한 허용되는 값 범위에 대한 제한으로 인해 산술 연산의 결과가 달라질 수 있습니다.  
  
**더하기 순서**  
일련의 숫자를 더하는 수식을 만들 때 메모리 내 모델에서는 DirectQuery 모델에서와 다른 순서로 숫자를 처리할 수 있습니다.  따라서 매우 큰 양수와 매우 큰 음수가 여러 개 있을 경우 연산에 따라 오류가 발생할 수도 있고 결과가 반환될 수도 있습니다.  
  
**POWER 함수 사용**  
예: `POWER(-64, 1/3)`  
  
DirectQuery 모드에서 POWER 함수는 분수 지수로 제곱할 경우 음수 값을 밑수로 사용할 수 없습니다. 이는 SQL Server에서 예상되는 동작입니다.  
  
메모리 내 모델에서 이 수식은 -4를 반환합니다.  
  
**숫자 오버플로 연산**  
Transact-SQL에서 숫자 오버플로를 발생시키는 연산을 수행하면 오버플로 오류가 반환됩니다. 따라서 오버플로를 발생시키는 수식은 DirectQuery 모드에서도 오류를 발생시킵니다.  
  
그러나 동일한 수식을 메모리 내 모델에서 사용할 경우에는 8바이트 정수가 반환됩니다. 이는 수식 엔진이 숫자 오버플로에 대한 검사를 수행하지 않기 때문입니다.  
  
**빈 값을 사용하는 LOG 함수에서 다른 결과가 반환됨**  
SQL Server에서는 Null과 빈 값을 xVelocity 엔진과는 다르게 처리합니다. 따라서 다음 수식은 DirectQuery 모드에서 오류를 반환하지만 메모리 내 모드에서는 무한대(–inf)를 반환합니다.  
  
`EXAMPLE: LOG(blank())`  
  
LOG10 및 LN 등의 다른 로그 함수에도 동일한 제한 사항이 적용됩니다.  
  
DAX에서의 **blank** 데이터 형식에 대한 자세한 내용은 [DAX 구문 참조](https://msdn.microsoft.com/library/ee634217.aspx)를 참조하세요.  
  
**0으로 나누기 및 빈 값으로 나누기**  
DirectQuery 모드에서 0으로 나누기나 빈 값으로 나누기는 항상 오류를 반환합니다. SQL Server에서는 무한대 개념이 지원되지 않으며 0으로 나누기의 자연적인 결과는 무한대이므로 결과가 오류가 됩니다. 그러나 SQL Server에서 Null로 나누기는 지원되므로 결과가 항상 Null과 같아야 합니다.  
  
DirectQuery 모드에서는 이러한 연산에 대해 다른 결과가 반환되지 않고 대신 두 유형의 연산(0으로 나누기 및 Null로 나누기) 모두 오류를 반환합니다.  
  
Excel 및 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 모델에서도 0으로 나누기는 오류를 반환합니다. 빈 값으로 나누기는 빈 값을 반환합니다.  
  
다음 식은 메모리 내 모델에서는 모두 유효하지만 DirectQuery 모드에서는 실패합니다.  
  
`1/BLANK`  
  
`1/0`  
  
`0.0/BLANK`  
  
`0/0`  
  
`BLANK/BLANK` 식은 메모리 내 모델과 DirectQuery 모드 모두에서 `BLANK` 를 반환하는 특수한 경우입니다.  
  
### <a name="supported-numeric-and-date-time-ranges"></a>지원되는 숫자 및 날짜-시간 범위  
메모리 내 테이블 형식 모델에서는 실수 및 날짜에 대한 최대 허용 값과 관련하여 Excel과 동일한 제한 사항이 수식에 적용됩니다. 그러나 계산 또는 쿼리에서 최대값이 반환되거나 값에 변환, 캐스팅, 반올림 또는 잘림이 적용되는 경우에는 차이점이 있을 수 있습니다.  
  
-   **Currency** 및 **Real** 형식의 값을 곱할 경우 결과가 가능한 최대값보다 크면 DirectQuery 모드에서는 오류가 발생하지 않고 Null이 반환됩니다.  
  
-   메모리 내 모델에서는 오류가 발생하지 않고 최대값이 반환됩니다.  
  
일반적으로 Excel과 SQL Server에서는 허용되는 날짜 범위가 다르므로 날짜가 다음 날짜를 포함하여 일반적인 날짜 범위 내에 있는 경우에만 결과가 일치할 수 있습니다.  
  
-   가장 빠른 날짜: 1990년 3월 1일  
  
-   가장 늦은 날짜: 9999년 12월 31일  
  
수식에 사용된 날짜가 이 범위를 벗어나면 수식에서 오류가 발생하거나 결과가 일치하지 않게 됩니다.  
  
**CEILING에서 지원되는 부동 소수점 값**  
예: `EVALUATE ROW("x", CEILING(-4.398488E+30, 1))`  
  
DAX CEILING에 해당하는 Transact-SQL 함수는 크기가 10^19 이하인 값만 지원합니다. 일반적으로 부동 소수점 값은 **bigint**에 맞출 수 있어야 합니다.  
  
**범위 외의 날짜를 사용하는 Datepart 함수**  
인수로 사용된 날짜가 유효한 날짜 범위에 있는 경우에만 DirectQuery 모드의 결과와 메모리 내 모델의 결과가 일치합니다. 이러한 조건이 충족되지 않으면 오류가 발생하거나, DirectQuery에서 반환되는 수식 결과와 메모리 내 모드에서 반환되는 수식 결과가 달라집니다.  
  
예: `MONTH(0)` 또는 `YEAR(0)`  
  
DirectQuery 모드에서 이 두 식은 각각 12와 1899를 반환합니다.  
  
메모리 내 모델에서 이 두 식은 각각 1과 1900을 반환합니다.  
  
예:  `EOMONTH(0.0001, 1)`  
  
이 식의 결과는 매개 변수로 제공된 데이터가 유효한 날짜 범위 내에 있는 경우에만 일치합니다.  
  
예: `EOMONTH(blank(), blank())` 또는 `EDATE(blank(), blank())`  
  
이 식의 결과는 DirectQuery 모드와 메모리 내 모드에서 동일해야 합니다.  
  
**시간 값 잘림**  
예: `SECOND(1231.04097222222)`  
  
DirectQuery 모드에서는 SQL Server 규칙에 따라 결과가 잘리고 식은 59로 계산됩니다.  
  
메모리 내 모델에서는 각 중간 연산의 결과가 반올림되므로 식이 0으로 계산됩니다.  
  
다음 예에서는 이 값이 계산되는 방식을 보여 줍니다.  
  
1.  입력의 소수 부분(0.04097222222)에 24를 곱합니다.  
  
2.  결과 시간 값(0.98333333328)에 60을 곱합니다.  
  
3.  결과 분 값은 58.9999999968입니다.  
  
4.  분 값의 소수 부분(0.9999999968)에 60을 곱합니다.  
  
5.  결과 초 값(59.999999808)이 60으로 반올림됩니다.  
  
6.  60은 0과 같습니다.  
  
**SQL Time 데이터 형식이 지원되지 않음**  
메모리 내 모델은 새로운 SQL **Time** 데이터 형식의 사용을 지원하지 않습니다. DirectQuery 모드에서 이 데이터 형식의 열을 참조하는 수식은 오류를 반환합니다. Time 데이터 열은 메모리 내 모델로 가져올 수 없습니다.  
  
그러나 엔진이 시간 값을 허용 가능한 데이터 형식으로 캐스팅하므로 수식에서 결과가 반환되는 경우도 있습니다.  
  
이 동작은 날짜 열을 매개 변수로 사용하는 모든 함수에 적용됩니다.  
  
### <a name="bkmk_Currency"></a>Currency  
DirectQuery 모드에서는 산술 연산의 결과가 **Currency**형식일 경우 값이 다음 범위 내에 있어야 합니다.  
  
-   최소: -922337203685477.5808  
  
-   최대: 922337203685477.5807  
  
**Currency 및 Real 데이터 형식 결합**  
예: `Currency sample 1`  
  
**Currency** 및 **Real** 형식을 곱할 경우 결과가 9223372036854774784(0x7ffffffffffffc00)보다 크면 DirectQuery 모드에서 오류가 발생하지 않습니다.  
  
메모리 내 모델에서는 결과의 절대값이 922337203685477.4784보다 크면 오류가 발생합니다.  
  
**연산 결과 값이 범위를 벗어남**  
예: `Currency sample 2`  
  
두 통화 값에 대한 연산 결과 값이 지정된 범위를 벗어날 경우 메모리 내 모델에서는 오류가 발생하지만 DirectQuery 모델에서는 오류가 발생하지 않습니다.  
  
**Currency 및 기타 데이터 형식 결합**  
통화 값을 다른 숫자 형식의 값으로 나눌 경우 다른 결과가 발생할 수 있습니다.  
  
### <a name="bkmk_Aggregations"></a>집계 함수  
한 개의 행이 있는 테이블에 대한 통계 함수는 다른 결과를 반환합니다. 빈 테이블에 대한 집계 함수도 메모리 내 모델과 DirectQuery 모드에서 서로 다르게 동작합니다.  
  
**단일 행이 있는 테이블에 대한 통계 함수**  
인수로 사용되는 테이블에 단일 행이 포함되어 있으면 DirectQuery 모드에서 STDEV 및 VARx 등의 통계 함수가 Null을 반환합니다.  
  
메모리 내 모델에서 단일 행이 있는 테이블에 대해 STDEV 또는 VARx를 사용하는 수식은 0으로 나누기 오류를 반환합니다.  
  
### <a name="bkmk_Text"></a>텍스트 함수  
관계형 데이터 저장소에서는 Excel과는 다른 텍스트 데이터 형식을 제공하므로 문자열을 검색하거나 부분 문자열에 대한 작업을 수행할 때 다른 결과가 나타날 수 있습니다. 문자열 길이도 다를 수 있습니다.  
  
일반적으로 고정 길이의 열을 인수로 사용하는 모든 문자열 조작 함수에서 다른 결과가 반환될 수 있습니다.  
  
또한 SQL Server에서 일부 텍스트 함수는 Excel에서 제공되지 않는 추가 인수를 지원합니다. 누락된 인수가 필요한 수식의 경우 메모리 내 모델에서는 다른 결과가 반환되거나 오류가 발생할 수 있습니다.  
  
**LEFT, RIGHT 등을 사용하여 문자를 반환하는 연산에서는 올바르지만 대/소문자가 다른 형태의 문자가 반환되거나 결과가 반환되지 않을 수 있습니다.**  
예: `LEFT([“text”], 2)`  
  
DirectQuery 모드에서는 반환되는 문자의 대/소문자가 항상 데이터베이스에 저장된 문자와 정확히 동일합니다. 그러나 xVelocity 엔진에서는 성능 향상을 위해 값 압축 및 인덱싱에 다른 알고리즘을 사용합니다.  
  
기본적으로는 대/소문자를 구분하지 않지만 악센트는 구분하는 Latin1_General 데이터 정렬이 사용됩니다. 따라서 소문자, 대문자 또는 대/소문자로 된 텍스트 문자열 인스턴스가 여러 개 있는 경우 모든 인스턴스가 동일한 문자열로 간주되어 첫 번째 문자열 인스턴스만 인덱스에 저장됩니다. 저장된 문자열에 대해 작동하는 모든 텍스트 함수는 인덱싱된 형태의 지정된 부분을 검색합니다. 따라서 위의 수식 예에서는 전체 열에 대해 첫 번째 인스턴스를 입력으로 사용하여 동일한 값이 반환됩니다.  
  
이 동작은 RIGHT, MID 등의 다른 텍스트 함수에도 적용됩니다.  
  
**문자열 길이가 결과에 영향을 줌**  
예: `SEARCH(“within string”, “sample target  text”, 1, 1)`  
  
SEARCH 함수를 사용하여 문자열을 검색할 경우 대상 문자열이 within string보다 길면 DirectQuery 모드에서 오류가 발생합니다.  
  
메모리 내 모델에서는 검색된 문자열이 반환되지만 문자열 길이는 &lt;텍스트 내&gt;의 길이로 잘립니다.  
  
예: `EVALUATE ROW("X", REPLACE("CA", 3, 2, "California") )`  
  
바꿀 문자열의 길이가 원래 문자열의 길이보다 길 경우 DirectQuery 모드에서 이 수식은 Null을 반환합니다.  
  
메모리 내 모델의 경우 이 수식은 원본 문자열과 바꿀 문자열을 연결하는 Excel의 동작을 따라 CACalifornia를 반환합니다.  
  
**문자열 중간에서 암시적 TRIM**  
예: `TRIM(“ A sample sentence with leading white space”)`  
  
DirectQuery 모드에서는 DAX TRIM 함수를 SQL 문 `LTRIM(RTRIM(<column>))`으로 변환합니다. 따라서 선행 및 후행 공백만 제거됩니다.  
  
반면, 메모리 내 모델에서는 동일한 수식이 Excel의 동작을 따라 문자열 내의 공백을 제거합니다.  
  
**LEN 함수 사용 시 암시적 RTRIM**  
예: `LEN(‘string_column’)`  
  
SQL Server와 마찬가지로, DirectQuery 모드에서는 문자열 열의 끝에서 공백을 제거합니다. 즉, 암시적 RTRIM을 수행합니다. 따라서 문자열에 후행 공백이 있는 경우 LEN 함수를 사용하는 수식에서 다른 값이 반환될 수 있습니다.  
  
**메모리 내 모드에서는 SUBSTITUTE에 대한 추가 매개 변수를 지원함**  
예: `SUBSTITUTE([Title],”Doctor”,”Dr.”)`  
  
예: `SUBSTITUTE([Title],”Doctor”,”Dr.”, 2)`  
  
DirectQuery 모드에서는 세 개의 매개 변수, 즉 열에 대한 참조, 이전 텍스트 및 새 텍스트만 사용하는 이 버전의 함수만 사용할 수 있습니다. 두 번째 수식을 사용하면 오류가 발생 합니다.  
  
메모리 내 모델에서는 선택적인 네 번째 매개 변수를 사용하여 바꿀 문자열의 인스턴스 번호를 지정할 수 있습니다. 예를 들어 두 번째 인스턴스만 바꾸는 등의 작업을 수행할 바꿀 수 있습니다.  
  
**REPT 연산의 문자열 길이에 대한 제한**  
메모리 내 모델에서 REPT를 사용하는 연산을 통해 반환되는 문자열의 길이는 32,767자보다 짧아야 합니다.  
  
DirectQuery 모드에서는 이 제한이 적용되지 않습니다.  
  
**부분 문자열 연산에서는 문자 형식에 따라 다른 결과가 반환됩니다.**  
예: `MID([col], 2, 5)`  
  
입력 텍스트가 **varchar** 또는 **nvarchar**일 경우 수식 결과는 항상 동일합니다.  
  
그러나 텍스트가 고정 길이의 문자이고 *&lt;num_chars&gt;* 의 값이 대상 문자열의 길이보다 길 경우 DirectQuery 모드에서는 결과 문자열의 끝에 공백이 추가됩니다.  
  
메모리 내 모델에서는 결과가 패딩 없이 마지막 문자열 문자에서 끝납니다.  


## <a name="see-also"></a>참고 항목  
[DirectQuery 모드](http://msdn.microsoft.com/en-us/45ad2965-05ec-4fb1-a164-d8060b562ea5)  
  


