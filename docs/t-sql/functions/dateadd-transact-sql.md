---
title: DATEADD(Transact-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8dcbc7ccfc8c94c28f3c8ba0df32b915440d76e4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dateadd-transact-sql"></a>DATEADD(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

*date*의 지정된 *datepart*에 특정 *number* 간격(부호 있는 정수)이 추가된 *date*를 반환합니다.
  
모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATEADD (datepart , number , date )  
```  
  
## <a name="arguments"></a>인수  
*datepart*  
**integer***number*가 추가되는 *date*의 일부입니다. 다음 표에는 올바른 *datepart* 인수가 모두 나열되어 있습니다. 해당하는 사용자 정의 변수는 사용할 수 없습니다.
  
|*datepart*|약어|  
|---|---|
|**year**|**yy**, **yyyy**|  
|**quarter**|**qq**, **q**|  
|**month**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**day**|**dd**, **d**|  
|**week**|**wk**, **ww**|  
|**weekday**|**dw**, **w**|  
|**hour**|**m**|  
|**minute**|**mi**, **n**|  
|**second**|**ss**, **s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
  
*number*  
*date*의 *datepart*에 추가된 [int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)로 확인될 수 있는 식입니다. 사용자 정의 변수는 유효합니다.  
소수점 이하가 포함된 값을 지정할 경우 소수점 이하는 반올림되지 않고 잘립니다.
  
*date*  
**time**, **date**, **smalldatetime**, **datetime**, **datetime2** 또는 **datetimeoffset** 값으로 확인할 수 있는 식입니다. *date*는 식, 열 식, 사용자 정의 변수 또는 문자열 리터럴일 수 있습니다. 식이 문자열 리터럴인 경우 **datetime**으로 확인되어야 합니다. 모호성을 피하려면 4자리 연도를 사용하세요. 두 자리 연도에 대한 정보는 [두 자리 연도 구분 구성 서버 구성 옵션](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.
  
## <a name="return-types"></a>반환 형식
문자열 리터럴을 제외하고 반환 데이터 형식은 *date* 인수의 데이터 형식입니다.
문자열 리터럴의 반환 데이터 형식은 **datetime**입니다. 문자열 리터럴 초의 소수 자릿수가 세 자리(.nnn)를 초과하거나 표준 시간대 오프셋 부분을 포함할 경우 오류가 발생합니다.
  
## <a name="return-value"></a>반환 값  
  
## <a name="datepart-argument"></a>datepart 인수  
**dayofyear**, **day**, **weekday**는 동일한 값을 반환합니다.
  
각 *datepart*와 해당 약어는 동일한 값을 반환합니다.
  
*datepart*가 **month**이고 *date*월의 일 수가 반환 월보다 많고 반환 월에 *date*일이 없을 경우 반환 월의 마지막 일이 반환됩니다. 예를 들어 9월에는 30일이 있으므로 다음 두 가지 문은 2006-09-30 00:00:00.000을 반환합니다.
  
```sql
SELECT DATEADD(month, 1, '20060830');
SELECT DATEADD(month, 1, '20060831');
```
  
## <a name="number-argument"></a>number 인수  
*number* 인수는 **int** 범위를 초과할 수 없습니다. 다음 명령문에서 *number*에 대한 인수는 **int** 범위를 1만큼 초과합니다. 이 경우 오류 메시지가 반환됩니다: "`Msg 8115, Level 16, State 2, Line 1. Arithmetic overflow error converting expression to data type int."`
  
```sql
SELECT DATEADD(year,2147483648, '20060731');  
SELECT DATEADD(year,-2147483649, '20060731');  
```  
  
## <a name="date-argument"></a>date 인수  
*date* 인수는 해당 데이터 형식 범위를 벗어나는 값으로 증가할 수 없습니다. 다음 명령문에서는 *date* 값에 추가된 *number* 값이 *date* 데이터 형식의 범위를 초과합니다. 이 경우 오류 메시지가 반환됩니다: "`Msg 517, Level 16, State 1, Line 1 Adding a value to a 'datetime' column caused overflow`."
  
```sql
SELECT DATEADD(year,2147483647, '20060731');  
SELECT DATEADD(year,-2147483647, '20060731');  
```  
  
## <a name="return-values-for-a-smalldatetime-date-and-a-second-or-fractional-seconds-datepart"></a>smalldatetime 날짜, 초 또는 소수 자릿수 초 datepart에 대한 반환 값  
[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 값의 초 부분은 항상 00입니다. *date*가 **smalldatetime**인 경우 다음이 적용됩니다.
-   *datepart*가 **second**이고 *number*가 -30 ~ +29 사이인 경우 추가가 수행되지 않습니다.  
-   *datepart*가 **second**이고 *number*가 -30보다 작거나 +29보다 클 경우 1분부터 추가가 수행됩니다.  
-   *datepart*가 **millisecond**이고 *number*가 -30001 ~ +29998 사이인 경우 추가가 수행되지 않습니다.  
-   *datepart*가 **millisecond**이고 *number*가 -30001보다 작거나 +29998보다 클 경우 1분부터 추가가 수행됩니다.  
  
## <a name="remarks"></a>Remarks  
DATEADD는 SELECT \<목록>, WHERE, HAVING, GROUP BY 및 ORDER BY 절에서 사용할 수 있습니다.
  
## <a name="fractional-seconds-precision"></a>소수 자릿수 초의 전체 자릿수
*date* 데이터 형식인 **smalldatetime**, **date**, **datetime**에는 **microsecond** 또는 **nanosecond**의 *datepart* 추가가 허용되지 않습니다.
  
밀리초의 소수 자릿수는 세 자리이며(.123) 마이크로초는 6자리(.123456), 나노초는 9자리(.123456789)입니다. **time**, **datetime2**, **datetimeoffset** 데이터 형식의 소수 자릿수는 7입니다(.1234567). *datepart*는 **nanosecond**이며 *date*의 소수 자릿수는 *number*가 100이 된 이후 증가합니다. *number*가 1에서 49 사이일 경우 0으로 버려지며 50에서 99 사이일 경우 100으로 반올림됩니다.
  
다음 명령문은 **millisecond**, **microsecond** 또는 **nanosecond**의 *datepart*를 추가합니다.
  
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
다음 각 명령문은 *datepart*를 1씩 증가시킵니다.
  
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
다음 각 명령문은 *date*에서 다음으로 높은 *datepart*도 증가시킬 수 있는 크기의 *number*만큼 *datepart*를 증가시킵니다.
  
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
다음 예에서는 여러 유형의 식을 *number* 및 *date* 매개 변수에 대한 인수로 사용합니다. 예제는 AdventureWorks 데이터베이스를 사용합니다.
  
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
다음 예에서는 사용자 정의 변수를 *number* 및 *date*에 대한 인수로 지정합니다.
  
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
다음 예에서는 *date*에 대한 `SYSDATETIME`을 지정합니다.
  
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
다음 예에서는 스칼라 하위 쿼리인 `MAX(ModifiedDate)`를 *number* 및 *date*에 대한 인수로 사용합니다. `(SELECT TOP 1 BusinessEntityID FROM Person.Person)`은 값 목록에서 *number* 인수를 선택하는 방법을 보여 주기 위하여 만든 숫자 매개 변수에 대한 인수입니다.
  
```sql
SELECT DATEADD(month,(SELECT TOP 1 BusinessEntityID FROM Person.Person),  
    (SELECT MAX(ModifiedDate) FROM Person.Person));  
```  
  
#### <a name="specifying-numeric-expressions-and-scalar-system-functions-as-number-and-date"></a>숫자 식 및 스칼라 시스템 함수를 숫자 및 날짜로 지정  
다음 예에서는 숫자 식(-`(10/2))`, [단항 연산자](../../mdx/unary-operators.md)(`-`), [산술 연산자](../../mdx/arithmetic-operators.md)(`/`), 스칼라 시스템 함수(`SYSDATETIME`)를 *number* 및 *date*에 대한 인수로 사용합니다.
  
```sql
SELECT DATEADD(month,-(10/2), SYSDATETIME());  
```  
  
#### <a name="specifying-ranking-functions-as-number"></a>순위 함수를 숫자로 지정  
다음 예에서는 순위 함수를 *number*에 대한 인수로 사용합니다.
  
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
다음 예에서는 집계 창 함수를 *number* 인수로 사용합니다.
  
```sql
SELECT SalesOrderID, ProductID, OrderQty  
    ,DATEADD(day,SUM(OrderQty)   
        OVER(PARTITION BY SalesOrderID),SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

