---
title: DATENAME (Transact SQL) | Microsoft Docs
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d41bbf5a83f0dee8518ece6f074181b8412bad8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="datename-transact-sql"></a>DATENAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

지정 된을 나타내는 문자열을 반환 *datepart* 는 지정 된 *날짜*
  
모든 개요 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 데이터 형식 및 함수, 참조 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>인수  
*날짜 부분*  
일부는 *날짜* 돌아갑니다. 다음 표에서 모든 유효한 *datepart* 인수입니다. 해당하는 사용자 정의 변수는 사용할 수 없습니다.
  
|*날짜 부분*|약어|  
|---|---|
|**연도**|**yy, yyyy**|  
|**분기**|**qq, q**|  
|**월**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**일**|**dd, d**|  
|**주**|**wk, ww**|  
|**요일**|**dw, w**|  
|**1 시간**|**m**|  
|**분**|**mi, n**|  
|**두 번째**|**ss, s**|  
|**밀리초**|**ms**|  
|**(마이크로초)**|**mcs**|  
|**나노초**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**ISOWK, ISOWW**|  
  
*date*  
식으로 확인 될 수 있는 한 **시간**, **날짜**, **smalldatetime**, **datetime**, **datetime2**, 또는 **datetimeoffset** 값입니다. *날짜* 식, 열 식, 사용자 정의 변수 또는 문자열 리터럴일 수 있습니다.  
모호성을 피하려면 4자리 연도를 사용하세요. 에 대 한 정보에 대 한 두 자리 연도 참조 [두 자리 연도 구성 cutoff 서버 구성 옵션](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)합니다.
  
## <a name="return-type"></a>반환 형식  
**nvarchar**
  
## <a name="return-value"></a>반환 값  
  
-   각 *datepart* 해당 약어는 동일한 값을 반환 합니다.  
  
반환 값은 사용 하 여 설정 된 언어 환경에 따라 달라 집니다 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 및는 [default language 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) 로그인 합니다. 반환 값에 종속은 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) 경우 *날짜* 는 문자열 리터럴 형식이 있습니다. date가 날짜 또는 시간 데이터 형식의 열 식이면 SET DATEFORMAT은 반환 값에 영향을 주지 않습니다.
  
경우는 *날짜* 매개 변수에 **날짜** 반환 값 데이터 형식 인수를 사용 하 여 지정 된 설정에 따라 달라 집니다 [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)합니다.
  
## <a name="tzoffset-datepart-argument"></a>TZoffset datepart 인수  
경우 *datepart* 인수가 **TZoffset** (**tz**) 및 *날짜* 인수에 표준 시간대 오프셋 없이 0이 반환 됩니다.
  
## <a name="smalldatetime-date-argument"></a>smalldatetime date 인수  
때 *날짜* 은 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), 초는 00으로 반환 됩니다.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>date 인수에 포함되지 않은 datepart는 기본값이 반환됨  
데이터 형식이 고 *날짜* 인수에 지정 된 없는 *datepart*의 기본값이 *datepart* 리터럴이 에대한지정된경우에반환됩니다*날짜*합니다.
  
예를 들어는 기본 연도-월-일에 대 한 **날짜** 데이터 형식은 1900-01-01입니다. 다음 문은 한 날짜 부분 인수에 대 한 *datepart*에 대 한 시간 인수 *날짜*, 반환 `1900, January, 1, 1, Monday`합니다.
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
경우 *날짜* 변수 또는 테이블 열 및 데이터 형식에 대 한 변수 또는 열에 없는지 지정 된 대로 지정 *datepart*, 오류 9810이 반환 됩니다. 날짜 부분 연도가 대 한 유효한 없기 때문에 다음 코드 예제에서는 실패는 **시간** 변수의 선언 된 데이터 형식을  *@t* 합니다.
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>주의  
DATENAME은 SELECT 목록, WHERE, HAVING, GROUP BY 및 ORDER BY 절에서 사용할 수 있습니다.
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], datename은 문자열 리터럴을으로 암시적으로 캐스팅 한 **datetime2** 유형입니다. 즉 DATENAME은 데이터가 문자열로 전달될 때 형식 YDM을 지원하지 않습니다. 문자열을 명시적으로 캐스팅 해야는 **datetime** 또는 **smalldatetime** YDM 형식을 사용 하는 형식입니다.
  
## <a name="examples"></a>예  
다음 예는 지정된 날짜에 대한 날짜 부분을 반환합니다.
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*날짜 부분*|반환 값|  
|---|---|
|**yy, yyyy, year**|2007|  
|**분기, qq, q**|4|  
|**월, mm, m**|10월|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**주, wk, ww**|44|  
|**주중 매일, dw**|화요일|  
|**시간, hh**|12|  
|**분, n**|15|  
|**두 번째, ss, s**|32|  
|**밀리초, ms**|123|  
|**mcs (마이크로초)**|123456|  
|**나노초 ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

다음 예는 지정된 날짜에 대한 날짜 부분을 반환합니다.
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*날짜 부분*|반환 값|  
|---|---|
|**yy, yyyy, year**|2007|  
|**분기, qq, q**|4|  
|**월, mm, m**|10월|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**주, wk, ww**|44|  
|**주중 매일, dw**|화요일|  
|**시간, hh**|12|  
|**분, n**|15|  
|**두 번째, ss, s**|32|  
|**밀리초, ms**|123|  
|**mcs (마이크로초)**|123456|  
|**나노초 ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


