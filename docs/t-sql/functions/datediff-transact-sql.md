---
title: DATEDIFF(Transact-SQL) | Microsoft Docs
description: DATEDIFF 함수의 Transact-SQL 참조입니다. datepart를 기준으로 시작 날짜와 종료 날짜 사이의 숫자 차이를 반환합니다.
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATEDIFF_TSQL
- DATEDIFF
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATEDIFF function [SQL Server]
- time [SQL Server], crossed boundaries
- differences in date and time [SQL Server]
- counting crossed date time boundaries [SQL Server]
- date and time [SQL Server], DATEDIFF
- dates [SQL Server], crossed boundaries
- boundary differences date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- interval dates [SQL Server]
- time [SQL Server], functions
- crossing date time boundaries [SQL Server]
- calculating dates times [SQL Server]
ms.assetid: eba979f2-1a8d-4cce-9d75-b74f9b519b37
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d74f65d119de40a2a02902076eebe6ae42bf4ce5
ms.sourcegitcommit: 2426a5e1abf6ecf35b1e0c062dc1e1225494cbb0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80517515"
---
# <a name="datediff-transact-sql"></a>DATEDIFF(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이 기능은 지정된 *startdate*와 *enddate* 사이에 지정된 datepart 경계의 수(부호 있는 정수 값으로)를 반환합니다.
  
*startdate*와 *enddate* 값 간의 더 큰 차이를 처리하는 함수는 [DATEDIFF_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-big-transact-sql.md)를 참조하세요. 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```
DATEDIFF ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>인수  

*datepart*  
**DATEDIFF**가 _startdate_와 _enddate_의 차이를 보고하는 단위입니다. 일반적으로 사용되는 _datepart_ 단위에는 `month` 또는 `second`가 포함됩니다.

_datepart_ 값은 변수나 `'month'` 같은 따옴표 문자열처럼 지정할 수 없습니다.

다음 표에는 올바른 _datepart_ 값이 모두 나열되어 있습니다. **DATEDIFF**는 _datepart_의 전체 이름 또는 전체 이름의 나열된 약어를 허용합니다.

|*datepart* 이름|*datepart* 약어|  
|-----------|------------|
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
| &nbsp; | &nbsp; |

> [!NOTE]
> 각 특정 *datepart* 이름과 해당 *datepart* 이름의 약어는 동일한 값을 반환합니다.

*startdate*  
다음 값 중 하나를 확인할 수 있는 식입니다.

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**
  
모호성을 피하려면 4자리 연도를 사용하세요. 두 자리 연도 값에 대한 정보는 [두 자리 연도 구분 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.
  
*enddate*  
*startdate*를 참조하세요.
  
## <a name="return-type"></a>반환 형식  
 **int**  
  
## <a name="return-value"></a>Return Value  

*startdate*와 *enddate* 사이의 **int** 차이로, *datepart*에 설정된 범위로 표시됩니다.
  
예를 들어 `SELECT DATEDIFF(day, '2036-03-01', '2036-02-28');`는 2036이 윤년이어야 한다는 것을 암시하는 -2를 반환합니다. 이 경우 _startdate_ '2036-03-01'에서 시작한 다음 -2일을 계산하면 '2036-02-28'의 _enddate_에 도달합니다.
  
**int**에 대한 범위를 벗어난 반환 값의 경우(-2,147,483,648 to +2,147,483,647) `DATEDIFF`에서 오류를 반환합니다.  **밀리초**의 경우 *startdate*와 *enddate*의 최대 차이는 24일, 20시간, 31분 및 23.647초입니다. **second**의 경우 최대 차이는 68년, 19일, 3시, 14분 7초입니다.
  
*startdate* 및 *enddate* 모두에 시간 값만 할당되고 *datepart*가 시간 *datepart*가 아니면 `DATEDIFF`는 0을 반환합니다.
  
`DATEDIFF`는 반환 값을 계산하기 위해 *startdate* 또는 *enddate*의 표준 시간대 오프셋 구성 요소를 사용합니다.
  
[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)은 분 단위까지만 정확하므로 *startdate* 또는 *enddate*에 **smalldatetime** 값이 있는 경우 반환 값에서 초와 밀리초는 항상 0으로 설정됩니다.
  
날짜 데이터 형식의 변수에 시간 값만 할당된 경우 `DATEDIFF`은 누락된 날짜 부분 값을 기본값인 `1900-01-01`로 설정합니다. 시간 또는 날짜 데이터 형식의 변수에 날짜 값만 할당될 경우 `DATEDIFF`는 누락된 시간 부분 값을 기본값인 `00:00:00`으로 설정합니다. *startdate* 또는 *enddate* 중 하나는 시간 부분만 있고 다른 하나는 날짜 부분만 있는 경우 `DATEDIFF`는 누락된 시간 및 날짜 부분을 기본값으로 설정합니다.
  
*startdate*와 *enddate*가 날짜 데이터 형식이 다르고 한 쪽의 시간 부분 또는 소수 자릿수 초의 전체 자릿수가 다른 쪽보다 많을 경우 `DATEDIFF`는 다른 쪽의 누락된 부분을 0으로 설정합니다.
  
## <a name="_datepart_-boundaries"></a>_datepart_ 범위

다음 명령문은 동일한 *startdate*와 동일한 *endate* 값을 가집니다. 이 날짜는 서로 인접하며 100나노초(.0000001초)만큼 시간이 다릅니다. 각 문에서 *startdate*와 *endate* 사이의 차이는 해당 *datepart*에서 하나의 달력 또는 시간 범위를 넘어섭니다. 각 문은 1을 반환합니다.
  
```sql
SELECT DATEDIFF(year,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(quarter,     '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(month,       '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(dayofyear,   '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(day,         '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(week,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(hour,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(minute,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(second,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(microsecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```

*startdate* 및 *enddate*의 연도 값이 다르지만 달력 주 값이 동일한 경우 `DATEDIFF`는 *datepart* **week**에 대해 0을 반환합니다.

## <a name="remarks"></a>설명  
`SELECT <list>`, `WHERE`, `HAVING`, `GROUP BY` 및 `ORDER BY` 절에서 `DATEDIFF`를 사용합니다.
  
`DATEDIFF`는 문자열 리터럴을 **datetime2** 형식으로 암시적으로 캐스팅합니다. 즉 `DATEDIFF`는 데이터가 문자열로 전달될 때 형식 YDM을 지원하지 않습니다. YDM 형식을 사용하려면 문자열을 **datetime** 또는 **smalldatetime** 형식으로 명시적으로 캐스팅해야 합니다.
  
`SET DATEFIRST` 지정은 `DATEDIFF`에 영향을 주지 않습니다. `DATEDIFF`은 항상 일요일을 한 주의 첫 날로 사용하여 함수가 결정적으로 작동하게 합니다.

*enddate*와 *startdate* 간의 차이가 **int**의 범위를 벗어난 값을 반환하는 경우 `DATEDIFF`는 **분** 이상의 정밀도로 오버플로할 수 있습니다.
  
## <a name="examples"></a>예  
이러한 예에서는 여러 유형의 식을 *startdate* 및 *enddate* 매개 변수에 대한 인수로 사용합니다.
  
### <a name="a-specifying-columns-for-startdate-and-enddate"></a>A. startdate 및 enddate에 대한 열 지정  
이 예에서는 테이블의 두 열 사이에 겹쳐지는 날짜 범위의 수를 계산합니다.
  
```sql
CREATE TABLE dbo.Duration  
    (startDate datetime2, endDate datetime2);  
    
INSERT INTO dbo.Duration(startDate, endDate)  
    VALUES ('2007-05-06 12:10:09', '2007-05-07 12:10:09');  
    
SELECT DATEDIFF(day, startDate, endDate) AS 'Duration'  
    FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="b-specifying-user-defined-variables-for-startdate-and-enddate"></a>B. startdate 및 enddate에 대한 사용자 정의 변수 지정  
이 예에서는 사용자 정의 변수가 *startdate* 및 *enddate* 인수로 작용합니다.
  
```sql
DECLARE @startdate datetime2 = '2007-05-05 12:10:09.3312722';  
DECLARE @enddate   datetime2 = '2007-05-04 12:10:09.3312722';   
SELECT DATEDIFF(day, @startdate, @enddate);  
```  
  
### <a name="c-specifying-scalar-system-functions-for-startdate-and-enddate"></a>C. startdate 및 enddate에 대한 스칼라 시스템 함수 지정  
이 예에서는 스칼라 시스템 함수를 *startdate* 및 *enddate* 인수로 사용합니다.
  
```sql
SELECT DATEDIFF(millisecond, GETDATE(), SYSDATETIME());  
```  
  
### <a name="d-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>D. startdate 및 enddate에 대한 스칼라 하위 쿼리 및 스칼라 함수 지정  
이 예에서는 스칼라 하위 쿼리 및 스칼라 함수를 *startdate* 및 *enddate* 인수로 사용합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day,
    (SELECT MIN(OrderDate) FROM Sales.SalesOrderHeader),  
    (SELECT MAX(OrderDate) FROM Sales.SalesOrderHeader));  
```  
  
### <a name="e-specifying-constants-for-startdate-and-enddate"></a>E. startdate 및 enddate에 대한 상수 지정  
이 예에서는 문자 상수를 *startdate* 및 *enddate* 인수로 사용합니다.
  
```sql
SELECT DATEDIFF(day,
   '2007-05-07 09:53:01.0376635',
   '2007-05-08 09:53:01.0376635');  
```  
  
### <a name="f-specifying-numeric-expressions-and-scalar-system-functions-for-enddate"></a>F. enddate에 대한 숫자 식 및 스칼라 시스템 함수 지정  
이 예에서는 `(GETDATE() + 1)` 숫자 식, `GETDATE` 스칼라 시스템 함수 및 `SYSDATETIME`을 *enddate* 인수로 사용합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', GETDATE() + 1)
    AS NumberOfDays  
    FROM Sales.SalesOrderHeader;  
GO  
USE AdventureWorks2012;  
GO  
SELECT
    DATEDIFF(
            day,
            '2007-05-07 09:53:01.0376635',
            DATEADD(day, 1, SYSDATETIME())
        ) AS NumberOfDays  
    FROM Sales.SalesOrderHeader;  
GO  
```  
  
### <a name="g-specifying-ranking-functions-for-startdate"></a>G. startdate에 대한 순위 함수 지정  
이 예제에서는 순위 함수를 *startdate* 인수로 사용합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,DATEDIFF(day, ROW_NUMBER() OVER (ORDER BY   
        a.PostalCode), SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson s   
    INNER JOIN Person.Person p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
### <a name="h-specifying-an-aggregate-window-function-for-startdate"></a>H. startdate에 대한 집계 창 함수 지정  
이 예에서는 집계 창 함수를 *startdate* 인수로 사용합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT soh.SalesOrderID, sod.ProductID, sod.OrderQty, soh.OrderDate,
    DATEDIFF(day, MIN(soh.OrderDate)   
        OVER(PARTITION BY soh.SalesOrderID), SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail sod  
    INNER JOIN Sales.SalesOrderHeader soh  
        ON sod.SalesOrderID = soh.SalesOrderID  
WHERE soh.SalesOrderID IN(43659, 58918);  
GO  
```  

### <a name="i-finding-difference-between-startdate-and-enddate-as-date-parts-strings"></a>9\. 날짜 부분 문자열로 startdate와 enddate 간의 차이점 찾기

```sql
-- DOES NOT ACCOUNT FOR LEAP YEARS
DECLARE @date1 DATETIME, @date2 DATETIME, @result VARCHAR(100);
DECLARE @years INT, @months INT, @days INT,
    @hours INT, @minutes INT, @seconds INT, @milliseconds INT;

SET @date1 = '1900-01-01 00:00:00.000'
SET @date2 = '2018-12-12 07:08:01.123'

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
     + CASE
            WHEN @milliseconds > 0
                THEN '.' + CAST(@milliseconds AS VARCHAR(10)) 
            ELSE ''
       END 
     + ' seconds','')

SELECT @result
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)] 

```
118 years, 11 months, 11 days, 7 hours, 8 minutes and 1.123 seconds
```
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
이러한 예에서는 여러 유형의 식을 *startdate* 및 *enddate* 매개 변수에 대한 인수로 사용합니다.
  
### <a name="j-specifying-columns-for-startdate-and-enddate"></a>J. startdate 및 enddate에 대한 열 지정  
이 예에서는 테이블의 두 열 사이에 겹쳐지는 날짜 범위의 수를 계산합니다.
  
```sql
CREATE TABLE dbo.Duration 
    (startDate datetime2, endDate datetime2);
    
INSERT INTO dbo.Duration (startDate, endDate)  
    VALUES ('2007-05-06 12:10:09', '2007-05-07 12:10:09');  
    
SELECT TOP(1) DATEDIFF(day, startDate, endDate) AS Duration  
    FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="k-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>11. startdate 및 enddate에 대한 스칼라 하위 쿼리 및 스칼라 함수 지정  
이 예에서는 스칼라 하위 쿼리 및 스칼라 함수를 *startdate* 및 *enddate* 인수로 사용합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day, (SELECT MIN(HireDate) FROM dbo.DimEmployee),  
    (SELECT MAX(HireDate) FROM dbo.DimEmployee))   
FROM dbo.DimEmployee;  
  
```  
  
### <a name="l-specifying-constants-for-startdate-and-enddate"></a>12. startdate 및 enddate에 대한 상수 지정  
이 예에서는 문자 상수를 *startdate* 및 *enddate* 인수로 사용합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day,
    '2007-05-07 09:53:01.0376635',
    '2007-05-08 09:53:01.0376635') FROM DimCustomer;  
```  
  
### <a name="m-specifying-ranking-functions-for-startdate"></a>13. startdate에 대한 순위 함수 지정  
이 예제에서는 순위 함수를 *startdate* 인수로 사용합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName,
    DATEDIFF(day, ROW_NUMBER() OVER (ORDER BY   
        DepartmentName), SYSDATETIME()) AS RowNumber  
FROM dbo.DimEmployee;  
```  
  
### <a name="n-specifying-an-aggregate-window-function-for-startdate"></a>14. startdate에 대한 집계 창 함수 지정  
이 예에서는 집계 창 함수를 *startdate* 인수로 사용합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, DepartmentName,
    DATEDIFF(year, MAX(HireDate)  
        OVER (PARTITION BY DepartmentName), SYSDATETIME()) AS SomeValue  
FROM dbo.DimEmployee  
```  
  
## <a name="see-also"></a>참고 항목
[DATEDIFF_BIG&#40;Transact-SQL&#41;](../../t-sql/functions/datediff-big-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
