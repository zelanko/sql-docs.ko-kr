---
title: DATEPART (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 57
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 05547f2dd50d7f130438d6a07b6952b8c29ec816
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="datepart-transact-sql"></a>DATEPART(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

지정 된을 나타내는 정수를 반환 *datepart* 는 지정 된 *날짜*합니다.
  
모든 개요 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 데이터 형식 및 함수, 참조 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>인수  
*날짜 부분*  
일부인 *날짜* (날짜 또는 시간 값)을는 **정수** 반환 됩니다. 다음 표에서 모든 유효한 *datepart* 인수입니다. 해당하는 사용자 정의 변수는 사용할 수 없습니다.
  
|*날짜 부분*|약어|  
|---|---|
|**연도**|**yy**, **yyyy**|  
|**분기**|**qq**, **q**|  
|**월**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**일**|**dd**, **d**|  
|**주**|**wk**, **ww**|  
|**요일**|**dw**|  
|**1 시간**|**m**|  
|**분**|**mi, n**|  
|**두 번째**|**ss**, **s**|  
|**밀리초**|**ms**|  
|**(마이크로초)**|**mcs**|  
|**나노초**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**isowk**, **isoww**|  
  
*date*  
식으로 확인 될 수 있는 한 **시간**, **날짜**, **smalldatetime**, **datetime**, **datetime2**, 또는 **datetimeoffset** 값입니다. *날짜* 식, 열 식, 사용자 정의 변수 또는 문자열 리터럴일 수 있습니다.  
모호성을 피하려면 4자리 연도를 사용하세요. 2 자리 연도 대 한 정보를 참조 하십시오. [구성 two digit year cutoff 서버 구성 옵션](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)합니다.
  
## <a name="return-type"></a>반환 형식  
 **int**  
  
## <a name="return-value"></a>반환 값  
각 *datepart* 해당 약어는 동일한 값을 반환 합니다.
  
반환 값은 사용 하 여 설정 된 언어 환경에 따라 달라 집니다 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 및는 [default language 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) 로그인 합니다. 경우 *날짜* 는 문자열 리터럴을 일부 형식에 대 한 반환 값에 따라 달라 집니다를 사용 하 여 지정 된 형식 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)합니다. date가 날짜 또는 시간 데이터 형식의 열 식이면 SET DATEFORMAT은 반환 값에 영향을 주지 않습니다.
  
다음 표는 모든 나열 *datepart* 문에 대 한 값을 반환 하는 인수 및 해당 `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')`합니다. 데이터 형식이 고 *날짜* 인수가 **(7)**합니다. **나노초***datepart* 반환 값의 소수 자릿수가 9 (. 123456700) 마지막 두 자리는 항상 00입니다.
  
|*날짜 부분*|반환 값|  
|---|---|
|**yy, yyyy, year**|2007|  
|**분기, qq, q**|4|  
|**월, mm, m**|10|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**주, wk, ww**|45|  
|**주중 매일, dw**|1.|  
|**시간, hh**|12|  
|**분, n**|15|  
|**두 번째, ss, s**|32|  
|**밀리초, ms**|123|  
|**mcs (마이크로초)**|123456|  
|**나노초 ns**|123456700|  
|**TZoffset, tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>Week 및 weekday datepart 인수
때 *datepart* 은 **주** (**wk**, **ww**) 또는 **평일** (**dw**)를 사용 하 여 설정 된 값에 따라 반환 값 [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)합니다.
  
모든 해의 1 월 1에 대 한 시작 숫자의 정의 **주***datepart*예를 들면: DATEPART (**wk**, ' Jan 1, *xxx*x') = 1, 여기서 *xxxx* 는 연도입니다.
  
다음 표에서 반환 값에 대 한 **주** 및 **평일***datepart* ' 2007-04-21' 각 SET DATEFIRST 인수에 대 한 합니다. 2007년 1월 1일은 월요일입니다. 2007년 4월 21일은 토요일입니다. 미국 영어의 경우 SET DATEFIRST 7, 즉 일요일이 기본값입니다.
  
|SET DATEFIRST<br /><br /> 인수(argument)|week<br /><br /> 반환|weekday<br /><br /> 반환|  
|---|---|---|
|1.|16|6|  
|2|17|5|  
|3|17|4|  
|4|17|3|  
|5|17|2|  
|6|17|1.|  
|7|16|7|  
  
## <a name="year-month-and-day-datepart-arguments"></a>year, month 및 day datepart 인수  
DATEPART에 대해 반환 되는 값 (**연도**, *날짜*), DATEPART (**월**, *날짜*), 및 DATEPART (**일** , *날짜*) 함수로 반환 하는 것과 같습니다 [연도](../../t-sql/functions/year-transact-sql.md), [월](../../t-sql/functions/month-transact-sql.md), 및 [일](../../t-sql/functions/day-transact-sql.md), f 각각.
  
## <a name="isoweek-datepart"></a>ISO_WEEK datepart  
ISO 8601에는 주 번호 매기기 시스템인 ISO 주-일 시스템이 포함됩니다. 각 주는 목요일이 포함되는 연도에 연결됩니다. 예를 들어 2004년의 첫 주(2004W01)는 2003년 12월 29일 월요일부터 2004년 1월 4일 일요일까지입니다. 1년의 가장 큰 주 번호는 52 또는 53입니다. 이러한 번호 매기기 스타일은 유럽 국가/지역에서 주로 사용되며 다른 국가에서는 거의 사용되지 않습니다.
  
다른 국가/지역의 번호 매기기 시스템은 ISO 표준을 따르지 않을 수도 있습니다. 가능한 값에는 다음 표와 같이 적어도 6가지가 있습니다.
  
|시작 요일|연도의 첫째 주에 포함되는 항목|주가 두 번 할당됨|사용|  
|---|---|---|---|
|일요일|1월 1일<br /><br /> 첫 번째 토요일<br /><br /> 한 해의 1-7일|예|United States|  
|월요일|1월 1일<br /><br /> 첫 번째 일요일<br /><br /> 한 해의 1-7일|예|대부분의 유럽, 영국|  
|월요일|4 년 1 월<br /><br /> 첫 번째 목요일<br /><br /> 한 해의 4-7 일|아니요|ISO 8601, 노르웨이 및 스웨덴|  
|월요일|7 월<br /><br /> 첫 번째 월요일<br /><br /> 한 해의 7일|아니요||  
|수요일|1월 1일<br /><br /> 첫 번째 화요일<br /><br /> 한 해의 1-7일|예||  
|토요일|1월 1일<br /><br /> 첫 번째 금요일<br /><br /> 한 해의 1-7일|예||  
  
## <a name="tzoffset"></a>TZoffset  
**TZoffset** (**tz**) (부호 있음) (분)로 반환 됩니다. 다음 문은 310분의 표준 시간대 오프셋을 반환합니다.
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
TZoffset 값은 다음과 같이 렌더링 됩니다.
- Datetimeoffset 및 datetime2 TZoffset 반환 시간 오프셋 (분) datetime2의 오프셋은 0 분 항상 합니다.
- 다른 날짜/시간 데이터 형식은 제외 하 고 datetime2 또는 datetimeoffset에 암시적으로 변환 될 수 있는 데이터 형식에 대 한 분에서의 시간 오프셋을 반환 합니다.
- 다른 모든 형식의 매개 변수는 오류가 발생 합니다.
  
  
## <a name="smalldatetime-date-argument"></a>smalldatetime date 인수  
때 *날짜* 은 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), 초는 00으로 반환 됩니다.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>date 인수에 없는 datepart에 대해서는 기본값이 반환됨  
데이터 형식이 고 *날짜* 인수에 지정 된 없는 *datepart*의 기본값이 *datepart* 리터럴이 에대한지정된경우에반환됩니다*날짜*합니다.
  
예를 들어는 기본 연도-월-일에 대 한 **날짜** 데이터 형식은 1900-01-01입니다. 다음 문은 한 날짜 부분 인수에 대 한 *datepart*에 대 한 시간 인수 *날짜*, 반환 `1900, 1, 1, 1, 2`합니다.
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
경우 *날짜* 변수 또는 테이블 열 및 데이터 형식에 대 한 변수 또는 열에 없는지 지정 된 대로 지정 *datepart*, 오류 9810이 반환 됩니다. 날짜 부분 연도가 대 한 유효한 없기 때문에 다음 코드 예제에서는 실패는 **시간** 변수의 선언 된 데이터 형식을  *@t* 합니다.
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>소수 자릿수 초
소수 자릿수 초는 다음 문과 같이 반환됩니다.
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>주의  
DATEPART는 SELECT 목록, WHERE, HAVING, GROUP BY 및 ORDER BY 절에서 사용할 수 있습니다.
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], DATEPART에 문자열 리터럴을으로 암시적으로 캐스팅 한 **datetime2** 유형입니다. 즉 DATEPART는 데이터가 문자열로 전달될 때 형식 YDM을 지원하지 않습니다. 문자열을 명시적으로 캐스팅 해야는 **datetime** 또는 **smalldatetime** YDM 형식을 사용 하는 형식입니다.
  
## <a name="examples"></a>예  
다음 예에서는 기본 연도를 반환합니다. 기본 연도는 날짜 계산에 유용합니다. 예에서 날짜는 숫자로 지정됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 0을 1900년 1월 1일로 해석합니다.
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
다음 예제에서는 날짜의 일 부분을 반환 합니다. `12/20/1974`합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`--------`
  
 `20`  
  
다음 예에서는 날짜의 연도 부분을 반환 `12/20/1974`합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (year,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`--------`
  
 `1974`  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

