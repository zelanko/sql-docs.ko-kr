---
title: DATEADD (Transact SQL) | Microsoft Docs
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
- DATEADD
- DATEADD_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- add interval to date or time [SQL Server]
- subtract interval from date or time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], intervals
- date and time [SQL Server], DATEADD
- DATEADD function [SQL Server]
ms.assetid: 89c5ae32-89c6-47e1-979e-15d97908b9f1
caps.latest.revision: 71
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6a90b51a1ef2156a2a05b8d3dd4e15111872edf6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="dateadd-transact-sql"></a>DATEADD(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

지정 된 반환 *날짜* 지정 된 *번호* 간격 (부호 있는 정수)에 지정 된 추가 *datepart* 해당 *날짜*합니다.
  
모든 개요 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 데이터 형식 및 함수, 참조 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATEADD (datepart , number , date )  
```  
  
## <a name="arguments"></a>인수  
*날짜 부분*  
일부인 *날짜* 입니다는 **정수***번호* 추가 됩니다. 다음 표에서 모든 유효한 *datepart* 인수입니다. 해당하는 사용자 정의 변수는 사용할 수 없습니다.
  
|*날짜 부분*|약어|  
|---|---|
|**연도**|**yy**, **yyyy**|  
|**분기**|**qq**, **q**|  
|**월**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**일**|**dd**, **d**|  
|**주**|**wk**, **ww**|  
|**요일**|**dw**, **w**|  
|**1 시간**|**m**|  
|**분**|**mi**,**n**|  
|**두 번째**|**ss**, **s**|  
|**밀리초**|**ms**|  
|**(마이크로초)**|**mcs**|  
|**나노초**|**ns**|  
  
*number*  
식으로 확인 될 수 있는 프로그램 [int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md) 에 추가 되는 *datepart* 의 *날짜*합니다. 사용자 정의 변수는 유효합니다.  
소수점 이하가 포함된 값을 지정할 경우 소수점 이하는 반올림되지 않고 잘립니다.
  
*date*  
식으로 확인 될 수 있는 한 **시간**, **날짜**, **smalldatetime**, **datetime**, **datetime2**, 또는 **datetimeoffset** 값입니다. *날짜* 식, 열 식, 사용자 정의 변수 또는 문자열 리터럴일 수 있습니다. 식이 문자열 리터럴을 이면으로 확인 되어야는 **datetime**합니다. 모호성을 피하려면 4자리 연도를 사용하세요. 에 대 한 정보에 대 한 두 자리 연도 참조 [두 자리 연도 구성 cutoff 서버 구성 옵션](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)합니다.
  
## <a name="return-types"></a>반환 형식
반환 데이터 형식은 변수의 데이터 형식을 *날짜* 인수 문자열 리터럴 제외 하 고 있습니다.
문자열 리터럴은 반환 데이터 형식은 **datetime**합니다. 문자열 리터럴 초의 소수 자릿수가 세 자리(.nnn)를 초과하거나 표준 시간대 오프셋 부분을 포함할 경우 오류가 발생합니다.
  
## <a name="return-value"></a>반환 값  
  
## <a name="datepart-argument"></a>datepart 인수  
**dayofyear**, **일**, 및 **평일** 동일한 값을 반환 합니다.
  
각 *datepart* 해당 약어는 동일한 값을 반환 합니다.
  
경우 *datepart* 은 **월** 및 *날짜* 달은 반환 월 보다 더 많은 날짜 및 *날짜* 일 반환 월에 없습니다. 반환 월의 마지막 날이 반환 됩니다. 예를 들어 9월에는 30일이 있으므로 다음 두 가지 문은 2006-09-30 00:00:00.000을 반환합니다.
  
```sql
SELECT DATEADD(month, 1, '2006-08-30');
SELECT DATEADD(month, 1, '2006-08-31');
```
  
## <a name="number-argument"></a>number 인수  
*번호* 인수의 범위를 초과할 수 없습니다 **int**합니다. 다음 문에서 인수에 대 한 *번호* 의 범위를 초과 **int** 1입니다. 다음과 같은 오류 메시지가 반환 됩니다. "`Msg 8115, Level 16, State 2, Line 1. Arithmetic overflow error converting expression to data type int."`
  
```sql
SELECT DATEADD(year,2147483648, '2006-07-31');  
SELECT DATEADD(year,-2147483649, '2006-07-31');  
```  
  
## <a name="date-argument"></a>date 인수  
*날짜* 인수는 해당 데이터 형식의 범위를 벗어난 값으로 증가할 수 없습니다. 다음 문에서 *번호* 값에 추가 되는 *날짜* 값의 범위를 초과 *날짜* 데이터 형식입니다. 다음과 같은 오류 메시지가 반환 됩니다: "`Msg 517, Level 16, State 1, Line 1 Adding a value to a 'datetime' column caused overflow`."
  
```sql
SELECT DATEADD(year,2147483647, '2006-07-31');  
SELECT DATEADD(year,-2147483647, '2006-07-31');  
```  
  
## <a name="return-values-for-a-smalldatetime-date-and-a-second-or-fractional-seconds-datepart"></a>smalldatetime 날짜, 초 또는 소수 자릿수 초 datepart에 대한 반환 값  
초 부분은 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 값은 항상 00입니다. 경우 *날짜* 은 **smalldatetime**, 다음에 해당 합니다.
-   경우 *datepart* 은 **두 번째** 및 *번호* 가-30 사이의 + 29, 추가 되지 않습니다.  
-   경우 *datepart* 은 **두 번째** 및 *번호* 작은 보다 30 또는 + 29 개 이상의 추가 1 분부터 수행 됩니다.  
-   경우 *datepart* 은 **밀리초** 및 *번호* 범위에 속함-30001에서 + 29998, 추가 되지 않습니다.  
-   경우 *datepart* 은 **밀리초** 및 *번호* + 29998 보다 또는-30001 보다 작거나, 1 분부터 추가 수행 됩니다.  
  
## <a name="remarks"></a>주의  
DATEADD는 SELECT에서 사용할 수 있습니다 \<목록 >, 여기서 HAVING, GROUP BY 및 ORDER BY 절.
  
## <a name="fractional-seconds-precision"></a>소수 자릿수 초의 전체 자릿수
에 대 한 추가 *datepart* 의 **마이크로초** 또는 **나노초** 에 대 한 *날짜* 데이터 형식 **smalldatetime**, **날짜**, 및 **datetime** 허용 되지 않습니다.
  
밀리초의 소수 자릿수는 세 자리이며(.123) 마이크로초는 6자리(.123456), 나노초는 9자리(.123456789)입니다. **시간**, **datetime2**, 및 **datetimeoffset** 데이터 형식에는 최대 자릿수는 7 (. 1234567). 경우 *datepart* 은 **나노초**, *번호* 의 소수 자릿수 초 전에 100 해야 *날짜* 증가 합니다. A *번호* 1에서 49 사이 0에서 50에서 99 까지의 숫자로 반내림 됩니다는 100으로 합니다.
  
다음 문을 추가 *datepart* 의 **밀리초**, **마이크로초**, 또는 **나노초**합니다.
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT '1 millisecond', DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT '2 milliseconds', DATEADD(millisecond,2,@datetime2)  
UNION ALL  
SELECT '1 microsecond', DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT '2 microseconds', DATEADD(microsecond,2,@datetime2)  
UNION ALL  
SELECT '49 nanoseconds', DATEADD(nanosecond,49,@datetime2)  
UNION ALL  
SELECT '50 nanoseconds', DATEADD(nanosecond,50,@datetime2)  
UNION ALL  
SELECT '150 nanoseconds', DATEADD(nanosecond,150,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1 millisecond     2007-01-01 13:10:10.1121111  
2 milliseconds    2007-01-01 13:10:10.1131111  
1 microsecond     2007-01-01 13:10:10.1111121  
2 microseconds    2007-01-01 13:10:10.1111131  
49 nanoseconds    2007-01-01 13:10:10.1111111  
50 nanoseconds    2007-01-01 13:10:10.1111112  
150 nanoseconds   2007-01-01 13:10:10.1111113  
```  
  
## <a name="time-zone-offset"></a>표준 시간대 오프셋
표준 시간대 오프셋에 대한 추가는 허용되지 않습니다.
  
## <a name="examples"></a>예  

### <a name="a-incrementing-datepart-by-an-interval-of-1"></a>1. 1씩 datepart 증가  
다음 문은 간격의 각 *datepart* 1 씩 합니다.
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT 'year', DATEADD(year,1,@datetime2)  
UNION ALL  
SELECT 'quarter',DATEADD(quarter,1,@datetime2)  
UNION ALL  
SELECT 'month',DATEADD(month,1,@datetime2)  
UNION ALL  
SELECT 'dayofyear',DATEADD(dayofyear,1,@datetime2)  
UNION ALL  
SELECT 'day',DATEADD(day,1,@datetime2)  
UNION ALL  
SELECT 'week',DATEADD(week,1,@datetime2)  
UNION ALL  
SELECT 'weekday',DATEADD(weekday,1,@datetime2)  
UNION ALL  
SELECT 'hour',DATEADD(hour,1,@datetime2)  
UNION ALL  
SELECT 'minute',DATEADD(minute,1,@datetime2)  
UNION ALL  
SELECT 'second',DATEADD(second,1,@datetime2)  
UNION ALL  
SELECT 'millisecond',DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT 'microsecond',DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT 'nanosecond',DATEADD(nanosecond,1,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Year         2008-01-01 13:10:10.1111111  
quarter      2007-04-01 13:10:10.1111111  
month        2007-02-01 13:10:10.1111111  
dayofyear    2007-01-02 13:10:10.1111111  
day          2007-01-02 13:10:10.1111111  
week         2007-01-08 13:10:10.1111111  
weekday      2007-01-02 13:10:10.1111111  
hour         2007-01-01 14:10:10.1111111  
minute       2007-01-01 13:11:10.1111111  
second       2007-01-01 13:10:11.1111111  
millisecond  2007-01-01 13:10:10.1121111  
microsecond  2007-01-01 13:10:10.1111121  
nanosecond   2007-01-01 13:10:10.1111111  
```  
  
### <a name="b-incrementing-more-than-one-level-of-datepart-in-one-statement"></a>2. 하나의 문에서 datepart를 두 수준 이상 증가  
다음 문은 간격의 각 *datepart* 여는 *번호* 도 증가 수 있을 만큼 큰 높은 *datepart* 의 *날짜*.
  
```sql
DECLARE @datetime2 datetime2;  
SET @datetime2 = '2007-01-01 01:01:01.1111111';  
--Statement                                 Result     
-------------------------------------------------------------------   
SELECT DATEADD(quarter,4,@datetime2);     --2008-01-01 01:01:01.110  
SELECT DATEADD(month,13,@datetime2);      --2008-02-01 01:01:01.110  
SELECT DATEADD(dayofyear,365,@datetime2); --2008-01-01 01:01:01.110  
SELECT DATEADD(day,365,@datetime2);       --2008-01-01 01:01:01.110  
SELECT DATEADD(week,5,@datetime2);        --2007-02-05 01:01:01.110  
SELECT DATEADD(weekday,31,@datetime2);    --2007-02-01 01:01:01.110  
SELECT DATEADD(hour,23,@datetime2);       --2007-01-02 00:01:01.110  
SELECT DATEADD(minute,59,@datetime2);     --2007-01-01 02:00:01.110  
SELECT DATEADD(second,59,@datetime2);     --2007-01-01 01:02:00.110  
SELECT DATEADD(millisecond,1,@datetime2); --2007-01-01 01:01:01.110  
```  
  
### <a name="c-using-expressions-as-arguments-for-the-number-and-date-parameters"></a>3. 식을 숫자 및 날짜 매개 변수에 대한 인수로 사용  
다음 예에서는 다양 한 유형의 식에 대 한 인수로 사용 하 여는 *번호* 및 *날짜* 매개 변수입니다. 예제에서는 AdventureWorks 데이터베이스를 사용 합니다.
  
#### <a name="specifying-a-column-as-date"></a>열을 날짜로 지정  
다음 예제에서는 `2` 일수를 `OrderDate` 열의 각 값에 추가하여 이름이 `PromisedShipDate`인 새 열을 파생시킵니다.
  
```sql
SELECT SalesOrderID  
    ,OrderDate   
    ,DATEADD(day,2,OrderDate) AS PromisedShipDate  
FROM Sales.SalesOrderHeader;  
```  
  
다음은 결과 집합의 일부입니다.
  
```sql
SalesOrderID OrderDate               PromisedShipDate  
------------ ----------------------- -----------------------  
43659        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43660        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43661        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
...  
43702        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43703        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43704        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43705        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43706        2005-07-03 00:00:00.000 2005-07-05 00:00:00.000  
...  
43711        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
43712        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
...  
43740        2005-07-11 00:00:00.000 2005-07-13 00:00:00.000  
43741        2005-07-12 00:00:00.000 2005-07-14 00:00:00.000  
  
```  
  
#### <a name="specifying-user-defined-variables-as-number-and-date"></a>사용자 정의 변수를 숫자 및 날짜로 지정  
다음 예제에 대 한 인수로 사용자 정의 변수 지정 *번호* 및 *날짜*합니다.
  
```sql
DECLARE @days int = 365,   
        @datetime datetime = '2000-01-01 01:01:01.111'; /* 2000 was a leap year */;  
SELECT DATEADD(day, @days, @datetime);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------------------  
2000-12-31 01:01:01.110  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-system-function-as-date"></a>스칼라 시스템 함수를 날짜로 지정  
다음 예에서는 지정 `SYSDATETIME` 에 대 한 *날짜*합니다.
  
```sql
SELECT DATEADD(month, 1, SYSDATETIME());  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------  
2013-02-06 14:29:59.6727944  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-subqueries-and-scalar-functions-as-number-and-date"></a>스칼라 하위 쿼리 및 스칼라 함수를 숫자 및 날짜로 지정  
다음 예에서는 스칼라 하위 쿼리를 사용 하 여 `MAX(ModifiedDate)`에 대 한 인수로 *번호* 및 *날짜*합니다. `(SELECT TOP 1 BusinessEntityID FROM Person.Person)`선택 하는 방법을 보여 주는 숫자 매개 변수에 대 한 인공 인수로 *번호* 값 목록에서 인수입니다.
  
```sql
SELECT DATEADD(month,(SELECT TOP 1 BusinessEntityID FROM Person.Person),  
    (SELECT MAX(ModifiedDate) FROM Person.Person));  
```  
  
#### <a name="specifying-numeric-expressions-and-scalar-system-functions-as-number-and-date"></a>숫자 식 및 스칼라 시스템 함수를 숫자 및 날짜로 지정  
다음 예제에서는 숫자 식 (-`(10/2))`, [단항 연산자](../../mdx/unary-operators.md) (`-`), [산술 연산자](../../mdx/arithmetic-operators.md) (`/`), 스칼라 시스템 함수 (`SYSDATETIME`)에 대 한 인수로 *번호* 및 *날짜*합니다.
  
```sql
SELECT DATEADD(month,-(10/2), SYSDATETIME());  
```  
  
#### <a name="specifying-ranking-functions-as-number"></a>순위 함수를 숫자로 지정  
다음 예에서는 순위 함수에 대 한 인수로 사용 하 여 *번호*합니다.
  
```sql
SELECT p.FirstName, p.LastName  
    ,DATEADD(day,ROW_NUMBER() OVER (ORDER BY  
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
#### <a name="specifying-an-aggregate-window-function-as-number"></a>집계 창 함수를 숫자로 지정  
다음 예제에서는 집계 창 함수를 사용 하 여에 대 한 인수로 서 *번호*합니다.
  
```sql
SELECT SalesOrderID, ProductID, OrderQty  
    ,DATEADD(day,SUM(OrderQty)   
        OVER(PARTITION BY SalesOrderID),SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


