---
title: DATEPART(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: eee173d268af8e18343c286bda29384b2a327860
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="datepart-transact-sql"></a>DATEPART(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

지정한 *date*에서 특정 *datepart*를 나타내는 정수를 반환합니다.
  
모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>인수  
*datepart*  
**정수**가 반환되기 위한 *date*(날짜 또는 시간 값)의 부분입니다. 다음 표에는 올바른 *datepart* 인수가 모두 나열되어 있습니다. 해당하는 사용자 정의 변수는 사용할 수 없습니다.
  
|*datepart*|약어|  
|---|---|
|**year**|**yy**, **yyyy**|  
|**quarter**|**qq**, **q**|  
|**month**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**day**|**dd**, **d**|  
|**week**|**wk**, **ww**|  
|**weekday**|**dw**|  
|**hour**|**m**|  
|**minute**|**mi, n**|  
|**second**|**ss**, **s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**isowk**, **isoww**|  
  
*date*  
**time**, **date**, **smalldatetime**, **datetime**, **datetime2** 또는 **datetimeoffset** 값으로 확인할 수 있는 식입니다. *date*는 식, 열 식, 사용자 정의 변수 또는 문자열 리터럴일 수 있습니다.  
모호성을 피하려면 4자리 연도를 사용하세요. 두 자리 연도에 대한 정보는 [Configure the two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.
  
## <a name="return-type"></a>반환 형식  
 **int**  
  
## <a name="return-value"></a>반환 값  
각 *datepart*와 해당 약어는 동일한 값을 반환합니다.
  
반환 값은 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)를 사용하여 설정한 언어 환경과 로그인의 [Configure the default language Server Configuartion Option](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)에 따라 다릅니다. *date*가 특정 형식에 대한 문자열 리터럴인 경우 반환 값은 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)을 사용하여 지정된 형식에 따라 달라집니다. date가 날짜 또는 시간 데이터 형식의 열 식이면 SET DATEFORMAT은 반환 값에 영향을 주지 않습니다.
  
다음 표에서는 `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')` 문에 대한 모든 *datepart* 인수 및 해당 반환 값을 보여 줍니다. *date* 인수의 데이터 형식이 **datetimeoffset(7)** 입니다. **nanosecond***datepart* 반환 값은 소수 자릿수는 9(.123456700)이며 마지막 두 자리는 항상 00입니다.
  
|*datepart*|반환 값|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|10|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|45|  
|**weekday, dw**|1|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>week 및 weekday datepart 인수
*datepart*가 **week**(**wk**, **ww**) 또는 **weekday**(**dw**)인 경우 반환 값은 [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)를 사용하여 설정된 값에 따라 달라집니다.
  
모든 해의 1월 1일은 **week***datepart*에 대한 시작 숫자를 정의합니다. 예를 들어 DATEPART (** wk**, 'Jan 1, *xxx*x') = 1이며 여기서 *xxxx*는 연도입니다.
  
다음 표에서는 각 SET DATEFIRST 인수의 '2007-04-21'에 대한 **week** 및 **weekday***datepart*의 반환 값을 보여줍니다. 2007년 1월 1일은 월요일입니다. 2007년 4월 21일은 토요일입니다. 미국 영어의 경우 SET DATEFIRST 7, 즉 일요일이 기본값입니다.
  
|SET DATEFIRST<br /><br /> 인수(argument)|week<br /><br /> 반환|weekday<br /><br /> 반환|  
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
  
## <a name="isoweek-datepart"></a>ISO_WEEK datepart  
ISO 8601에는 주 번호 매기기 시스템인 ISO 주-일 시스템이 포함됩니다. 각 주는 목요일이 포함되는 연도에 연결됩니다. 예를 들어 2004년의 첫 주(2004W01)는 2003년 12월 29일 월요일부터 2004년 1월 4일 일요일까지입니다. 1년의 가장 큰 주 번호는 52 또는 53입니다. 이러한 번호 매기기 스타일은 유럽 국가/지역에서 주로 사용되며 다른 국가에서는 거의 사용되지 않습니다.
  
다른 국가/지역의 번호 매기기 시스템은 ISO 표준을 따르지 않을 수도 있습니다. 가능한 값에는 다음 표와 같이 적어도 6가지가 있습니다.
  
|시작 요일|연도의 첫째 주에 포함되는 항목|주가 두 번 할당됨|사용|  
|---|---|---|---|
|일요일|1월 1일<br /><br /> 첫 번째 토요일<br /><br /> 한 해의 1-7일|예|United States|  
|월요일|1월 1일<br /><br /> 첫 번째 일요일<br /><br /> 한 해의 1-7일|예|대부분의 유럽, 영국|  
|월요일|1월 4일,<br /><br /> 첫 번째 목요일<br /><br /> 한 해의 4-7일|아니오|ISO 8601, 노르웨이 및 스웨덴|  
|월요일|1월 7일,<br /><br /> 첫 번째 월요일<br /><br /> 한 해의 7일|아니오||  
|수요일|1월 1일<br /><br /> 첫 번째 화요일<br /><br /> 한 해의 1-7일|예||  
|토요일|1월 1일<br /><br /> 첫 번째 금요일<br /><br /> 한 해의 1-7일|예||  
  
## <a name="tzoffset"></a>TZoffset  
**TZoffset** (**tz**)은 분 수(부호 있음)로 반환됩니다. 다음 문은 310분의 표준 시간대 오프셋을 반환합니다.
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
TZoffset 값은 다음과 같이 렌더링됩니다.
- Datetimeoffset 및 datetime2에 대해 datetime2의 오프셋은 항상 0분이 경우 TZoffset은 시간 오프셋을 분으로 반환합니다.
- 다른 날짜/시간 데이터 형식은 제외하고 datetime2 또는 datetimeoffset으로 암시적으로 변환될 수 있는 데이터 형식에 대해 TZoffset은 분으로 시간 오프셋을 반환 합니다.
- 다른 모든 형식의 매개 변수는 오류가 있습니다.
  
  
## <a name="smalldatetime-date-argument"></a>smalldatetime date 인수  
*date*가 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)이면 초는 00으로 반환됩니다.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>date 인수에 없는 datepart에 대해서는 기본값이 반환됨  
*date* 인수의 데이터 형식에 지정된 *datepart*가 없으면 *date*에 대해 리터럴이 지정된 경우에만 해당 *datepart*의 기본값이 반환됩니다.
  
예를 들어 모든 **date** 데이터 형식의 년-월-일 기본값은 1900-01-01입니다. 다음 명령문은 *datepart*에 대한 날짜 부분 인수, *date*에 대한 시간 인수를 가지며 `1900, 1, 1, 1, 2`를 반환합니다.
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
*date*가 변수 또는 테이블 열로 지정되고 해당 변수 또는 열의 데이터 형식에 지정된 *datepart*가 없으면 오류 9810이 반환됩니다. 다음 코드 예는 날짜 부분 연도가 *@t* 변수로 선언된 **time** 데이터 형식에 유효하지 않기 때문에 실패합니다.
  
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
  
## <a name="remarks"></a>Remarks  
DATEPART는 SELECT 목록, WHERE, HAVING, GROUP BY 및 ORDER BY 절에서 사용할 수 있습니다.
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 DATEPART는 문자열 리터럴을 **datetime2** 형식으로 암시적으로 캐스팅합니다. 즉 DATEPART는 데이터가 문자열로 전달될 때 형식 YDM을 지원하지 않습니다. YDM 형식을 사용하려면 문자열을 **datetime** 또는 **smalldatetime** 형식으로 명시적으로 캐스팅해야 합니다.
  
## <a name="examples"></a>예  
다음 예에서는 기본 연도를 반환합니다. 기본 연도는 날짜 계산에 유용합니다. 예에서 날짜는 숫자로 지정됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 0을 1900년 1월 1일로 해석합니다.
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
다음 예에서는 날짜 `12/20/1974`의 일 부분을 반환합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
20
```  
  
다음 예에서는 날짜 `12/20/1974`의 연도 부분을 반환합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (year,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
1974
```  
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
