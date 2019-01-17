---
title: DATEDIFF_BIG(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATEDIFF_BIG
- DATEDIFF_BIG_TSQL
helpviewer_keywords:
- DATEDIFF_BIG function [SQL Server]
- dates [SQL Server]. functions
- date and time [SQL Server], DATEDIFF_BIG
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 19ac1693-3cfa-400d-bf83-20a9cb46599a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9a2a6dfd98cef225e8ca612d3cce758087663f75
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046553"
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

이 기능은 지정된 *startdate*와 *enddate* 사이에 지정된 *datepart* 경계의 수(부호 있는 큰 정수 값으로)를 반환합니다.
  
모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>인수  
*datepart*  
겹쳐지는 범위의 유형을 지정하는 *startdate*와 *enddate* 부분입니다. `DATEDIFF_BIG`은 해당하는 사용자 정의 변수 항목을 허용하지 않습니다. 이 표에서는 올바른 *datepart* 인수가 모두 나열되어 있습니다.

> [!NOTE]
> `DATEDIFF_BIG`은 *datepart* 인수에 해당하는 사용자 정의 변수 항목을 허용하지 않습니다.
  
|*datepart*|약어|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
  
*startdate*  
다음 값 중 하나를 확인할 수 있는 식입니다.

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

*date*의 경우 `DATEDIFF_BIG`은 열 식, 식, 문자열 리터럴 또는 사용자 정의 변수를 허용합니다. 문자열 리터럴 값은 **datetime**을 확인해야 합니다. 모호성 문제를 피하려면 4자리 연도를 사용하세요. `DATEDIFF_BIG`는 *enddate*에서 *startdate*를 뺍니다. 모호성을 피하려면 4자리 연도를 사용하세요. 두 자리 연도에 대한 정보는 [두 자리 연도 구분 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.
  
*enddate*  
*startdate*를 참조하세요.
  
## <a name="return-type"></a>반환 형식  

서명된 **bigint**  
  
## <a name="return-value"></a>반환 값  
지정된 startdate와 enddate 사이에 지정된 datepart 경계의 수(부호 있는 큰 정수 값으로)를 반환합니다.
-   각 특정 *datepart* 및 해당 *datepart*에 대한 약어는 동일한 값을 반환합니다.  
  
**bigint**에 대한 범위를 벗어난 반환 값의 경우(-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807) `DATEDIFF_BIG`에서 오류를 반환합니다. **int**을 반환하여 **분** 이상의 정밀도로 오버플로할 수 있는 `DATEDIFF`와 달리, `DATEDIFF_BIG`은 *enddate*와 *startdate* 간의 차이가 292년, 3개월, 10일, 23시간, 47분 및 16.8547758초를 넘는 **나노초** 정밀도를 사용하는 경우에만 오버플로할 수 있습니다.
  
*startdate* 및 *enddate* 모두에 시간 값만 할당되고 *datepart*가 시간 *datepart*가 아니면 `DATEDIFF_BIG`는 0을 반환합니다.
  
`DATEDIFF_BIG`은 반환 값을 계산하기 위해 *startdate* 또는 *enddate*의 표준 시간대 오프셋 구성 요소를 사용하지 않습니다.
  
*startdate* 또는 *enddate*에 사용된 **smalldatetime** 값의 경우 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)은 분 단위까지만 정확하므로 `DATEDIFF_BIG`은 반환 값에서 초와 밀리초를 항상 0으로 설정합니다.
  
날짜 데이터 형식의 변수에 시간 값만 할당된 경우 `DATEDIFF_BIG`은 누락된 날짜 부분 값을 기본값인 `1900-01-01`로 설정합니다. 시간 또는 날짜 데이터 형식의 변수에 날짜 값만 할당될 경우 `DATEDIFF_BIG`는 누락된 시간 부분 값을 기본값인 `00:00:00`으로 설정합니다. *startdate* 또는 *enddate* 중 하나는 시간 부분만 있고 다른 하나는 날짜 부분만 있는 경우 `DATEDIFF_BIG`는 누락된 시간 및 날짜 부분을 기본값으로 설정합니다.
  
*startdate*와 *enddate*가 날짜 데이터 형식이 다르고 한 쪽의 시간 부분 또는 소수 자릿수 초의 전체 자릿수가 다른 쪽보다 많을 경우 `DATEDIFF_BIG`는 다른 쪽의 누락된 부분을 0으로 설정합니다.
  
## <a name="datepart-boundaries"></a>datepart 범위
다음 명령문은 동일한 *startdate*와 동일한 *endate* 값을 가집니다. 이러한 날짜는 서로 인접하며 1마이르코초(.0000001초)만큼 시간이 다릅니다. 각 문에서 *startdate*와 *endate* 사이의 차이는 해당 *datepart*에서 하나의 달력 또는 시간 범위를 넘어섭니다. 각 문은 1을 반환합니다. *startdate* 및 *enddate*의 연도 값이 다르지만 달력 주 값이 동일한 경우 `DATEDIFF_BIG`는 *datepart* **week**에 대해 0을 반환합니다.

```sql
SELECT DATEDIFF_BIG(year,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter,     '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month,       '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear,   '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day,         '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Remarks  
`SELECT <list>`, `WHERE`, `HAVING`, `GROUP BY` 및 `ORDER BY` 절에서 `DATEDIFF_BIG`를 사용합니다.
  
`DATEDIFF_BIG`는 문자열 리터럴을 **datetime2** 형식으로 암시적으로 캐스팅합니다. 즉 `DATEDIFF_BIG`는 데이터가 문자열로 전달될 때 형식 YDM을 지원하지 않습니다. YDM 형식을 사용하려면 문자열을 **datetime** 또는 **smalldatetime** 형식으로 명시적으로 캐스팅해야 합니다.
  
`SET DATEFIRST` 지정은 `DATEDIFF_BIG`에 영향을 주지 않습니다. `DATEDIFF_BIG`은 항상 일요일을 한 주의 첫 날로 사용하여 함수가 결정적으로 작동하게 합니다.

*enddate*와 *startdate* 간의 차이가 **bigint**의 범위를 벗어난 값을 반환하는 경우 `DATEDIFF_BIG`는 **나노초**의 정밀도로 오버플로할 수 있습니다.
  
## <a name="examples"></a>예 
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>startdate 및 enddate에 대한 열 지정  
이 예에서는 여러 유형의 식을 *startdate* 및 *enddate* 매개 변수에 대한 인수로 사용합니다. 테이블의 두 열 사이에 겹쳐지는 날짜 범위의 수를 계산합니다.
  
```sql
CREATE TABLE dbo.Duration  
    (startDate datetime2, endDate datetime2);  
    
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09', '2007-05-07 12:10:09');  
    
SELECT DATEDIFF_BIG(day, startDate, endDate) AS 'Duration'  
    FROM dbo.Duration;  
-- Returns: 1  
```  

### <a name="finding-difference-between-startdate-and-enddate-as-date-parts-strings"></a>날짜 부분 문자열로 startdate와 enddate 간의 차이점 찾기

```sql
DECLARE @date1 DATETIME2, @date2 DATETIME2, @result VARCHAR(100)
DECLARE @years BIGINT, @months BIGINT, @days BIGINT, @hours BIGINT, @minutes BIGINT, @seconds BIGINT, @milliseconds BIGINT

SET @date1 = '0001-01-01 00:00:00.00000000'
SET @date2 = '2018-12-12 07:08:01.12345678'

SELECT @years = DATEDIFF(yy, @date1, @date2)
IF DATEADD(yy, -@years, @date2) < @date1 
SELECT @years = @years-1
SET @date2 = DATEADD(yy, -@years, @date2)

SELECT @months = DATEDIFF(mm, @date1, @date2)
IF DATEADD(mm, -@months, @date2) < @date1 
SELECT @months=@months-1
SET @date2= DATEADD(mm, -@months, @date2)

SELECT @days=DATEDIFF(dd, @date1, @date2)
IF DATEADD(dd, -@days, @date2) < @date1 
SELECT @days=@days-1
SET @date2= DATEADD(dd, -@days, @date2)

SELECT @hours=DATEDIFF(hh, @date1, @date2)
IF DATEADD(hh, -@hours, @date2) < @date1 
SELECT @hours=@hours-1
SET @date2= DATEADD(hh, -@hours, @date2)

SELECT @minutes=DATEDIFF(mi, @date1, @date2)
IF DATEADD(mi, -@minutes, @date2) < @date1 
SELECT @minutes=@minutes-1
SET @date2= DATEADD(mi, -@minutes, @date2)

SELECT @seconds=DATEDIFF(s, @date1, @date2)
IF DATEADD(s, -@seconds, @date2) < @date1 
SELECT @seconds=@seconds-1
SET @date2= DATEADD(s, -@seconds, @date2)

SELECT @milliseconds=DATEDIFF(ms, @date1, @date2)

SELECT @result= ISNULL(CAST(NULLIF(@years,0) AS VARCHAR(10)) + ' years,','')
     + ISNULL(' ' + CAST(NULLIF(@months,0) AS VARCHAR(10)) + ' months,','')    
     + ISNULL(' ' + CAST(NULLIF(@days,0) AS VARCHAR(10)) + ' days,','')
     + ISNULL(' ' + CAST(NULLIF(@hours,0) AS VARCHAR(10)) + ' hours,','')
     + ISNULL(' ' + CAST(@minutes AS VARCHAR(10)) + ' minutes and','')
     + ISNULL(' ' + CAST(@seconds AS VARCHAR(10)) 
          + CASE WHEN @milliseconds > 0 THEN '.' + CAST(@milliseconds AS VARCHAR(10)) 
               ELSE '' END 
          + ' seconds','')

SELECT @result
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)] 

```
2017 years, 11 months, 11 days, 7 hours, 8 minutes and 1.123 seconds
```   

더 자세한 예는 [DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)를 참조합니다.
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
