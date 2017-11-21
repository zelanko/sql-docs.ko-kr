---
title: DATEDIFF (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 52
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: dba834b51bab48c2bd30d1bbbb4abe11694ab321
ms.contentlocale: ko-kr
ms.lasthandoff: 10/05/2017

---
# <a name="datediff-transact-sql"></a>DATEDIFF(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

지정 된 수 (부호 있는 정수)를 반환 *datepart* 지정 된 간에 겹쳐지는 *startdate* 및 *enddate*합니다.
  
더 큰 차이 대 한 참조 [DATEDIFF_BIG &#40; Transact SQL &#41; ](../../t-sql/functions/datediff-big-transact-sql.md). 모든 개요 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 데이터 형식 및 함수, 참조 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATEDIFF ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>인수  
*날짜 부분*  
일부인 *startdate* 및 *enddate* 겹쳐지는 범위의 유형을 지정 하는 합니다. 다음 표에서 모든 유효한 *datepart* 인수입니다. 해당하는 사용자 정의 변수는 사용할 수 없습니다.
  
|*날짜 부분*|약어|  
|---|---|
|**연도**|**yy, yyyy**|  
|**분기**|**qq, q**|  
|**월**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**일**|**dd, d**|  
|**주**|**wk, ww**|  
|**1 시간**|**m**|  
|**분**|**mi, n**|  
|**두 번째**|**ss, s**|  
|**밀리초**|**ms**|  
|**(마이크로초)**|**mcs**|  
|**나노초**|**ns**|  
  
*startdate*  
식으로 확인 될 수 있는 한 **시간**, **날짜**, **smalldatetime**, **datetime**, **datetime2**, 또는 **datetimeoffset** 값입니다. *날짜* 식, 열 식, 사용자 정의 변수 또는 문자열 리터럴일 수 있습니다. *startdate* 에서 뺀 *enddate*합니다.
  
모호성을 피하려면 4자리 연도를 사용하세요. 2 자리 연도 대 한 정보를 참조 하십시오. [구성 two digit year cutoff 서버 구성 옵션](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)합니다.
  
*종료 날짜*  
참조 *startdate*합니다.
  
## <a name="return-type"></a>반환 형식  
 **int**  
  
## <a name="return-value"></a>반환 값  
  
-   각 *datepart* 해당 약어는 동일한 값을 반환 합니다.  
  
반환 값은 범위를 벗어나는 경우 **int** (에서 + 2,147,483,647 사이-2147483648), 오류가 반환 됩니다. 에 대 한 **밀리초**, 사이의 최대 오차 *startdate* 및 *enddate* 은 24 일, 20 시간, 31 분 및 23.647 초입니다. 에 대 한 **두 번째**, 최대 차이 68 년입니다.
  
경우 *startdate* 및 *enddate* 둘 다 시간 값만 할당 되 고 *datepart* 은 시간이 아닙니다 *datepart*, 0이 반환 됩니다.
  
표준 시간대 오프셋의 구성 요소 *startdate* 또는 *endate* 반환 값을 계산한 다음에 사용 되지 않습니다.
  
때문에 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 분만에 때는 **smalldatetime** 에 값이 사용 *startdate* 또는 *enddate*, 초 및 밀리초는 항상 반환 값에 0으로 설정 됩니다.
  
날짜 데이터 형식의 변수에 시간 값만 할당된 경우 누락된 날짜 부분의 값은 기본값인 1900-01-01로 설정됩니다. 시간 또는 날짜 데이터 형식의 변수에 날짜 값만 할당될 경우 누락된 시간 부분의 값은 기본값인 00:00:00으로 설정됩니다. 어느 경우 *startdate* 또는 *enddate* 시간 부분만 있고 다른만 날짜 부분, 누락 된 시간 및 날짜 부분은 기본값으로 설정 했습니다.
  
경우 *startdate* 및 *enddate* 는 서로 다른 날짜 데이터 형식의 없고 하나 시간 부분 또는 소수 자릿수 초의 전체 자릿수가 다른에 다른 누락 된 부분은 0으로 설정 됩니다.
  
## <a name="datepart-boundaries"></a>datepart 경계  
다음 문에 동일한 *startdate* 과 동일한 *endate*합니다. 이러한 날짜는 서로 인접하며 차이는 .0000001초입니다. 차이 *startdate* 및 *endate* 각 문에서 하나의 달력 또는 시간 경계를 넘는 해당 *datepart*합니다. 각 문은 1을 반환합니다. 이 예에서 다른 연도가 사용 되 고 두 *startdate* 및 *endate* 달력 주에 대 한 반환 값에 **주** 0 이어야 합니다.
  
```sql
SELECT DATEDIFF(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>주의  
DATEDIFF는 SELECT 목록, WHERE, HAVING, GROUP BY 및 ORDER BY 절에서 사용할 수 있습니다.
  
DATEDIFF에 문자열 리터럴을으로 암시적으로 캐스팅 한 **datetime2** 유형입니다. 즉 DATEDIFF는 데이터가 문자열로 전달될 때 형식 YDM을 지원하지 않습니다. 문자열을 명시적으로 캐스팅 해야는 **datetime** 또는 **smalldatetime** YDM 형식을 사용 하는 형식입니다.
  
SET DATEFIRST를 지정해도 DATEDIFF에는 영향을 주지 않습니다. DATEDIFF는 항상 일요일을 한 주의 첫 날로 사용하여 결정적 함수가 되도록 합니다.
  
## <a name="examples"></a>예  
다음 예에서는 다양 한 유형의 식에 대 한 인수로 사용 하 여는 *startdate* 및 *enddate* 매개 변수입니다.
  
### <a name="a-specifying-columns-for-startdate-and-enddate"></a>1. startdate 및 enddate에 대한 열 지정  
다음 예에서는 테이블의 두 열 사이에 겹쳐지는 날짜 범위의 수를 계산합니다.
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="b-specifying-user-defined-variables-for-startdate-and-enddate"></a>2. startdate 및 enddate에 대한 사용자 정의 변수 지정  
다음 예제에서는 사용자 정의 변수를 사용 하 여에 대 한 인수로 *startdate* 및 *enddate*합니다.
  
```sql
DECLARE @startdate datetime2 = '2007-05-05 12:10:09.3312722';  
DECLARE @enddate datetime2 = '2007-05-04 12:10:09.3312722';   
SELECT DATEDIFF(day, @startdate, @enddate);  
```  
  
### <a name="c-specifying-scalar-system-functions-for-startdate-and-enddate"></a>3. startdate 및 enddate에 대한 스칼라 시스템 함수 지정  
다음 예에서는 스칼라 시스템 함수에 대 한 인수로 사용 하 여 *startdate* 및 *enddate*합니다.
  
```sql
SELECT DATEDIFF(millisecond, GETDATE(), SYSDATETIME());  
```  
  
### <a name="d-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>4. startdate 및 enddate에 대한 스칼라 하위 쿼리 및 스칼라 함수 지정  
다음 예에서는 스칼라 하위 쿼리 및 스칼라 함수를 사용 하 여에 대 한 인수로 *startdate* 및 *enddate*합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day,(SELECT MIN(OrderDate) FROM Sales.SalesOrderHeader),  
    (SELECT MAX(OrderDate) FROM Sales.SalesOrderHeader));  
```  
  
### <a name="e-specifying-constants-for-startdate-and-enddate"></a>5. startdate 및 enddate에 대한 상수 지정  
다음 예제에서는 문자 상수에 대 한 인수로 사용 하 여 *startdate* 및 *enddate*합니다.
  
```sql
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635');  
```  
  
### <a name="f-specifying-numeric-expressions-and-scalar-system-functions-for-enddate"></a>6. enddate에 대한 숫자 식 및 스칼라 시스템 함수 지정  
다음 예제에서는 숫자 식을 사용 하 여 `(GETDATE ()+ 1)`, 스칼라 시스템 함수 및 `GETDATE` 및 `SYSDATETIME`에 대 한 인수로 *enddate*합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', GETDATE()+ 1)   
    AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', DATEADD(day,1,SYSDATETIME())) AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
```  
  
### <a name="g-specifying-ranking-functions-for-startdate"></a>7. startdate에 대한 순위 함수 지정  
다음 예에서는 순위 함수에 대 한 인수로 사용 하 여 *startdate*합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson s   
    INNER JOIN Person.Person p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
### <a name="h-specifying-an-aggregate-window-function-for-startdate"></a>8. startdate에 대한 집계 창 함수 지정  
다음 예제에서는 집계 창 함수를 사용 하 여에 대 한 인수로 서 *startdate*합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT soh.SalesOrderID, sod.ProductID, sod.OrderQty,soh.OrderDate  
    ,DATEDIFF(day,MIN(soh.OrderDate)   
        OVER(PARTITION BY soh.SalesOrderID),SYSDATETIME() ) AS 'Total'  
FROM Sales.SalesOrderDetail sod  
    INNER JOIN Sales.SalesOrderHeader soh  
        ON sod.SalesOrderID = soh.SalesOrderID  
WHERE soh.SalesOrderID IN(43659,58918);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
다음 예에서는 다양 한 유형의 식에 대 한 인수로 사용 하 여는 *startdate* 및 *enddate* 매개 변수입니다.
  
### <a name="i-specifying-columns-for-startdate-and-enddate"></a>9. startdate 및 enddate에 대한 열 지정  
다음 예에서는 테이블의 두 열 사이에 겹쳐지는 날짜 범위의 수를 계산합니다.
  
```sql
CREATE TABLE dbo.Duration (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT TOP(1) DATEDIFF(day,startDate,endDate) AS Duration  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="j-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>10. startdate 및 enddate에 대한 스칼라 하위 쿼리 및 스칼라 함수 지정  
다음 예에서는 스칼라 하위 쿼리 및 스칼라 함수를 사용 하 여에 대 한 인수로 *startdate* 및 *enddate*합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day,(SELECT MIN(HireDate) FROM dbo.DimEmployee),  
    (SELECT MAX(HireDate) FROM dbo.DimEmployee))   
FROM dbo.DimEmployee;  
  
```  
  
### <a name="k-specifying-constants-for-startdate-and-enddate"></a>11. startdate 및 enddate에 대한 상수 지정  
다음 예제에서는 문자 상수에 대 한 인수로 사용 하 여 *startdate* 및 *enddate*합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635') FROM DimCustomer;  
```  
  
### <a name="l-specifying-ranking-functions-for-startdate"></a>12. startdate에 대한 순위 함수 지정  
다음 예에서는 순위 함수에 대 한 인수로 사용 하 여 *startdate*합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        DepartmentName),SYSDATETIME()) AS RowNumber  
FROM dbo.DimEmployee;  
```  
  
### <a name="m-specifying-an-aggregate-window-function-for-startdate"></a>13. startdate에 대한 집계 창 함수 지정  
다음 예제에서는 집계 창 함수를 사용 하 여에 대 한 인수로 서 *startdate*합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, DepartmentName  
    ,DATEDIFF(year,MAX(HireDate)  
             OVER (PARTITION BY DepartmentName),SYSDATETIME()) AS SomeValue  
FROM dbo.DimEmployee  
```  
  
## <a name="see-also"></a>참고 항목
[DATEDIFF_BIG &#40; Transact SQL &#41;](../../t-sql/functions/datediff-big-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  



