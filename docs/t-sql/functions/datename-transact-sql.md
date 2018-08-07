---
title: DATENAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATENAME_TSQL
- DATENAME
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATENAME function [SQL Server
- functions [SQL Server], time
- functions [SQL Server], date and time
- dateparts [SQL Server], datename
- date and time [SQL Server], DATENAME
- comparing dates times [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 11855b56-c554-495d-aad4-ba446990153b
caps.latest.revision: 59
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 4c698de73617643b9cf07ed094400336e98a04fa
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39457427"
---
# <a name="datename-transact-sql"></a>DATENAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이 함수는 지정한 *date*에서 특정 *datepart*를 나타내는 문자열을 반환합니다.

모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>인수  
*datepart*  
`DATENAME`이 반환할 *date* 인수의 특정 부분입니다. 이 표에서는 올바른 *datepart* 인수가 모두 나열되어 있습니다.

> [!NOTE]
> `DATENAME`은 *datepart* 인수에 해당하는 사용자 정의 변수 항목을 허용하지 않습니다.
  
|*datepart*|약어|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**weekday**|**dw, w**|  
|**hour**|**m**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**ISOWK, ISOWW**|  
  
*date*  

다음 데이터 형식 중 하나를 확인할 수 있는 식입니다. 

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

*date*의 경우 `DATENAME`은 열 식, 식, 문자열 리터럴 또는 사용자 정의 변수를 허용합니다. 모호성 문제를 피하려면 4자리 연도를 사용하세요. 두 자리 연도에 대한 정보는 [두 자리 연도 구분 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.
  
## <a name="return-type"></a>반환 형식  
**nvarchar**
  
## <a name="return-value"></a>반환 값  
  
-   각 *datepart*와 해당 약어는 동일한 값을 반환합니다.  
  
반환 값은 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 및 로그인의 [기본 언어 구성 서버 구성 옵션](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)을 사용하여 설정한 언어 환경에 따라 다릅니다. *date*가 특정 형식의 문자열 리터럴인 경우 반환 값은 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)에 따라 다릅니다. date가 날짜 또는 시간 데이터 형식의 열 식이면 SET DATEFORMAT은 반환 값을 변경하지 않습니다.
  
*date* 매개 변수에 **date** 데이터 형식 인수가 있으면 반환 값은 [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)에 의해 지정된 설정에 따라 달라집니다.
  
## <a name="tzoffset-datepart-argument"></a>TZoffset datepart 인수  
*datepart* 인수가 **TZoffset**(**tz**)이고 *date* 인수에 표준 시간대 오프셋이 없으면 `DATEADD`는 0을 반환합니다.
  
## <a name="smalldatetime-date-argument"></a>smalldatetime date 인수  
*date*가 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)이면 `DATENAME`은 초를 00으로 반환합니다.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>date 인수에 포함되지 않은 datepart는 기본값이 반환됨  
*date* 인수의 데이터 형식에 지정된 *datepart*가 없으면 `DATENAME`은 *date* 인수가 리터럴인 경우에만 해당 *datepart*의 기본값을 반환합니다.
  
예를 들어 모든 **date** 데이터 형식의 년-월-일 기본값은 1900-01-01입니다. 다음 명령문은 *datepart*에 대한 날짜 부분 인수, *date*에 대한 시간 인수를 가지며 `DATENAME`은 `1900, January, 1, 1, Monday`를 반환합니다.
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
*date*가 변수 또는 테이블 열로 지정되고 해당 변수 또는 열의 데이터 형식에 지정된 *datepart*가 없으면 `DATENAME`은 오류 9810을 반환합니다. 이 예제에서 변수 *@t*에는 **time** 데이터 형식이 있습니다. 날짜 부분 연도가 **time** 데이터 형식에 적합하지 않으므로 이 예제는 실패입니다.
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>Remarks  

다음 절에서 `DATENAME`를 사용합니다.

+ GROUP BY
+ HAVING
+ ORDER BY
+ SELECT \<list>
+ WHERE
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 DATENAME은 문자열 리터럴을 **datetime2** 형식으로 암시적으로 캐스팅합니다. 즉 `DATENAME`는 데이터가 문자열로 전달될 때 형식 YDM을 지원하지 않습니다. YDM 형식을 사용하려면 문자열을 **datetime** 또는 **smalldatetime** 형식으로 명시적으로 캐스팅해야 합니다.
  
## <a name="examples"></a>예  
이 예는 지정된 날짜에 대한 날짜 부분을 반환합니다. SELECT 문의 `datepart` 인수에 대한 테이블에서 *datepart* 값을 대체합니다.
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|반환 값|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|10월|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|화요일|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

이 예는 지정된 날짜에 대한 날짜 부분을 반환합니다. SELECT 문의 `datepart` 인수에 대한 테이블에서 *datepart* 값을 대체합니다.
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|반환 값|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|10월|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|화요일|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

