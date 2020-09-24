---
title: DATEPART(Transact-SQL) | Microsoft Docs
description: DATEPART 함수의 Transact-SQL 참조입니다. 이 함수는 지정된 날짜의 datepart에 해당하는 정수를 반환합니다.
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATEPART_TSQL
- DATEPART
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], DATEPART
- dateparts [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dateparts [SQL Server], datepart
- comparing dates times [SQL Server]
- DATEPART function [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 15f1a5bc-4c0c-4c48-848d-8ec03473e6c1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bbd0ad445399fe45ddf704d0037bb7ee31a53b2c
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91117164"
---
# <a name="datepart-transact-sql"></a>DATEPART(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]


이 함수는 지정한 *date*의 지정한 *datepart*를 나타내는 정수를 반환합니다.
  
모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DATEPART ( datepart , date )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*datepart*  
`DATEPART`가 **정수**를 반환할 *date* 인수의 특정 부분입니다. 이 표에서는 올바른 *datepart* 인수가 모두 나열되어 있습니다.

> [!NOTE]
> `DATEPART`은 *datepart* 인수에 해당하는 사용자 정의 변수 항목을 허용하지 않습니다.
  
|*datepart*|약어|  
|---|---|
|**year**|**yy**, **yyyy**|  
|**quarter**|**qq**, **q**|  
|**month**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**day**|**dd**, **d**|  
|**week**|**wk**, **ww**|  
|**weekday**|**dw**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss**, **s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**tzoffset**|**tz**|  
|**iso_week**|**isowk**, **isoww**|  
  
*date*  
다음 데이터 형식 중 하나를 확인하는 식입니다. 

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

*date*의 경우 `DATEPART`은 열 식, 식, 문자열 리터럴 또는 사용자 정의 변수를 허용합니다. 모호성 문제를 피하려면 4자리 연도를 사용하세요. 두 자리 연도에 대한 정보는 [두 자리 연도 구분 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.
  
## <a name="return-type"></a>반환 형식  
 **int**  
  
## <a name="return-value"></a>Return Value  
각 *datepart*와 해당 약어는 동일한 값을 반환합니다.
  
반환 값은 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 및 로그인의 [기본 언어 구성 서버 구성 옵션](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)을 사용하여 설정한 언어 환경에 따라 다릅니다. *date*가 특정 형식의 문자열 리터럴인 경우 반환 값은 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)에 따라 다릅니다. date가 날짜 또는 시간 데이터 형식의 열 식이면 SET DATEFORMAT은 반환 값을 변경하지 않습니다.
  
이 표에서는 `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')` 문에 대한 모든 *datepart* 인수 및 해당 반환 값을 보여 줍니다. *date* 인수에는 **datetimeoffset(7)** 데이터 형식이 있습니다. **nanosecond** *datepart* 반환 값의 마지막 두 자리는 항상 `00`이며, 이 값의 소수 자릿수는 9입니다.

**.123456700**
  
|*datepart*|반환 값|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|10|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|3|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**tzoffset, tz**|310|  
|**iso_week, isowk, isoww**|44|  
  
## <a name="week-and-weekday-datepart-arguments"></a>week 및 weekday datepart 인수
**week**(**wk**, **ww**) 또는 **weekday**(**dw**) *datepart*의 경우 `DATEPART` 반환 값은 [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)로 설정된 값에 따라 달라집니다.
  
모든 연도의 1월 1일은 **week** _datepart_의 시작 값을 정의합니다. 다음은 그 예입니다.

DATEPART(**wk**, '1월 1일, *xxx*x') = 1

여기서 *xxxx*는 연도입니다.
  
이 테이블은 각 SET DATEFIRST 인수에 대한 ‘2007-04-21’의 **week** 및 **weekday** *datepart* 반환 값을 보여 줍니다. 2007년 1월 1일은 월요일에 해당합니다. 2007년 4월 21일은 토요일에 해당합니다. 미국 영어

`SET DATEFIRST 7 -- ( Sunday )`

기본값으로 사용됩니다. DATEFIRST를 설정한 후 datepart 테이블 값에 대한 이 제안된 SQL 문을 사용합니다.

`SELECT DATEPART(week, '2007-04-21 '), DATEPART(weekday, '2007-04-21 ')`
  
|SET DATEFIRST<br /><br /> 인수|week<br /><br /> 반환|weekday<br /><br /> 반환|  
|---|---|---|
|1|16|6|  
|2|17|5|  
|3|17|4|  
|4|17|3|  
|5|17|2|  
|6|17|1|  
|7|16|7|  
  
## <a name="year-month-and-day-datepart-arguments"></a>year, month 및 day datepart 인수  
DATEPART(**year**, *date*), DATEPART(**month**, *date*) 및 DATEPART (**day**, *date*)에 대해 반환되는 값은 각각 [YEAR](../../t-sql/functions/year-transact-sql.md), [MONTH](../../t-sql/functions/month-transact-sql.md), [DAY](../../t-sql/functions/day-transact-sql.md) 함수에서 반환하는 값과 동일합니다.
  
## <a name="iso_week-datepart"></a>iso_week datepart  
ISO 8601에는 주 번호 매기기 시스템인 ISO 주-일 시스템이 포함됩니다. 각 주는 목요일이 포함되는 연도에 연결됩니다. 예를 들어 2004년의 첫 주(2004W01)는 2003년 12월 29일 월요일부터 2004년 1월 4일 일요일까지입니다. 유럽 국가/지역은 일반적으로 이 번호 매기기 스타일을 사용합니다. 비유럽 국가/지역 일반적으로 이를 사용하지 않습니다.

참고: 1년에 가장 많은 주는 52주나 53주일 수 있습니다.
  
다른 국가/지역의 번호 매기기 시스템은 ISO 표준을 따르지 않을 수 있습니다. 이 표에서는 6가지 가능성을 보여 줍니다.
  
|시작 요일|연도의 첫째 주에 포함되는 항목|주가 두 번 할당됨|사용|  
|---|---|---|---|
|일요일|1월 1일<br /><br /> 첫 번째 토요일<br /><br /> 한 해의 1-7일|예|미국|  
|월요일|1월 1일<br /><br /> 첫 번째 일요일<br /><br /> 한 해의 1-7일|예|대부분의 유럽, 영국|  
|월요일|1월 4일,<br /><br /> 첫 번째 목요일<br /><br /> 한 해의 4-7일|예|ISO 8601, 노르웨이 및 스웨덴|  
|월요일|1월 7일,<br /><br /> 첫 번째 월요일<br /><br /> 한 해의 7일|예||  
|수요일|1월 1일<br /><br /> 첫 번째 화요일<br /><br /> 한 해의 1-7일|예||  
|토요일|1월 1일<br /><br /> 첫 번째 금요일<br /><br /> 한 해의 1-7일|예||  
  
## <a name="tzoffset"></a>tzoffset  
`DATEPART`는 **tzoffset**(**tz**) 값을 분 수(부호 있음)로 반환합니다. 이 명령문은 310분의 표준 시간대 오프셋을 반환합니다.
  
```sql
SELECT DATEPART (tzoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
`DATEPART`는 tzoffset 값을 다음과 같이 렌더링합니다.
- datetimeoffset 및 datetime2에 대해 tzoffset은 시간 오프셋을 분 단위로 반환하며, datetime2의 오프셋은 항상 0분입니다.
- 암시적으로 **datetimeoffset** 또는 **datetime2**로 변환할 수 있는 데이터 형식의 경우 `DATEPART`는 분으로 시간 오프셋을 반환합니다. 예외: 다른 날짜/시간 데이터 형식입니다.
- 다른 모든 형식의 매개 변수는 오류가 있습니다.
  
  
## <a name="smalldatetime-date-argument"></a>smalldatetime date 인수  
[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) *date* 값에 대해 `DATEPART`는 초를 00으로 반환합니다.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>date 인수에 없는 datepart에 대해서는 기본값이 반환됨  
*date* 인수 데이터 형식에 지정된 *datepart*가 없으면 `DATEPART`는 *date*에 대해 리터럴이 지정된 경우에만 해당 *datepart*의 기본값을 반환합니다.
  
예를 들어 모든 **date** 데이터 형식의 년-월-일 기본값은 1900-01-01입니다. 다음 명령문은 *datepart*에 대한 날짜 부분 인수, *date*에 대한 시간 인수를 가지며 `1900, 1, 1, 1, 2`를 반환합니다.
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
*date*가 변수 또는 테이블 열로 지정되고 해당 변수 또는 열의 데이터 형식에 지정된 *datepart*가 없으면 `DATEPART`은 오류 9810을 반환합니다. 이 예제에서 변수 *\@t*는 **time** 데이터 형식입니다. 날짜 부분 연도가 **time** 데이터 형식에 적합하지 않으므로 이 예제는 실패입니다.
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>소수 자릿수 초
이러한 명령문은 `DATEPART`가 소수 자릿수 초를 반환하는 것을 보여줍니다.
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>설명  
`DATEPART`는 DATEADD는 SELECT 목록, WHERE, HAVING, GROUP BY 및 ORDER BY 절에서 사용할 수 있습니다.
  
DATEPART는 문자열 리터럴을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 **datetime2** 형식으로 암시적으로 캐스팅합니다. 즉 DATENAME은 데이터가 문자열로 전달될 때 형식 YDM을 지원하지 않습니다. YDM 형식을 사용하려면 문자열을 **datetime** 또는 **smalldatetime** 형식으로 명시적으로 캐스팅해야 합니다.
  
## <a name="examples"></a>예  
이 예에서는 기본 연도를 반환합니다. 기본 연도는 날짜 계산에 도움이 됩니다. 예제에서 숫자는 날짜를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 0을 1900년 1월 1일로 해석합니다.
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  

-- Returns: 1900    1    1 
```  
  
이 예에서는 날짜 `12/20/1974`의 일 부분을 반환합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  

-- Returns: 20
```  
  
이 예에서는 날짜 `12/20/1974`의 년 부분을 반환합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (year,'12/20/1974') FROM dbo.DimCustomer;  

-- Returns: 1974
```  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
