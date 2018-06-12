---
title: DATEDIFF_BIG(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 26ea16e8e80fd2b8febf8a95c848490b41f0408a
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34744102"
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
|**hour**|**m**|  
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

*date*의 경우 `DATEDIFF_BIG`은 열 식, 식, 문자열 리터럴 또는 사용자 정의 변수를 허용합니다. 문자열 리터럴 값은 **datetime**을 확인해야 합니다. 모호성 문제를 피하려면 4자리 연도를 사용하세요. `DATEDIFF_BIG`은 *startdate*에서 *enddate*를 뺍니다. 모호성을 피하려면 4자리 연도를 사용하세요. 두 자리 연도에 대한 정보는 [두 자리 연도 구분 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.
  
*enddate*  
*startdate*를 참조하세요.
  
## <a name="return-type"></a>반환 형식  

서명된 **bigint**  
  
## <a name="return-value"></a>반환 값  
지정된 startdate와 enddate 사이에 지정된 datepart 경계의 수(부호 있는 큰 정수 값으로)를 반환합니다.
-   각 특정 *datepart* 및 해당 *datepart*에 대한 약어는 동일한 값을 반환합니다.  
  
**bigint**에 대한 범위를 벗어난 반환 값의 경우(-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807) `DATEDIFF_BIG`에서 오류를 반환합니다. **밀리초**의 경우 *startdate*와 *enddate*의 최대 차이는 24일, 20시간, 31분 및 23.647초입니다. **초**의 경우 최대 차이는 68년입니다.
  
*startdate* 및 *enddate* 모두에 시간 값만 할당되고 *datepart*가 시간 *datepart*가 아니면 `DATEDIFF_BIG`는 0을 반환합니다.
  
`DATEDIFF_BIG`은 반환 값을 계산하기 위해 *startdate* 또는 *enddate*의 표준 시간대 오프셋 구성 요소를 사용하지 않습니다.
  
*startdate* 또는 *enddate*에 사용된 **smalldatetime** 값의 경우 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)은 분 단위까지만 정확하므로 `DATEDIFF_BIG`은 반환 값에서 초와 밀리초를 항상 0으로 설정합니다.
  
날짜 데이터 형식의 변수에 시간 값만 할당된 경우 `DATEDIFF_BIG`은 누락된 날짜 부분 값을 기본값인 1900-01-01로 설정합니다. 시간 또는 날짜 데이터 형식의 변수에 날짜 값만 할당될 경우 `DATEDIFF_BIG`은 누락된 시간 부분 값을 기본값인 00:00:00으로 설정합니다. *startdate* 또는 *enddate* 중 하나는 시간 부분만 있고 다른 하나는 날짜 부분만 있는 경우 `DATEDIFF_BIG`는 누락된 시간 및 날짜 부분을 기본값으로 설정합니다.
  
*startdate*와 *enddate*가 날짜 데이터 형식이 다르고 한 쪽의 시간 부분 또는 소수 자릿수 초의 전체 자릿수가 다른 쪽보다 많을 경우 `DATEDIFF_BIG`는 다른 쪽의 누락된 부분을 0으로 설정합니다.
  
## <a name="datepart-boundaries"></a>datepart 범위
다음 명령문은 동일한 *startdate*와 동일한 *endate* 값을 가집니다. 이러한 날짜는 서로 인접하며 차이는 .0000001초입니다. 각 문에서 *startdate*와 *endate* 사이의 차이는 해당 *datepart*에서 하나의 달력 또는 시간 범위를 넘어섭니다. 각 문은 1을 반환합니다. *startdate* 및 *enddate*의 연도 값이 다르지만 달력 주 값이 동일한 경우 `DATEDIFF_BIG`는 *datepart* **week**에 대해 0을 반환합니다.

```sql
SELECT DATEDIFF_BIG(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Remarks  
SELECT <list>, WHERE, HAVING, GROUP BY 및 ORDER BY 절에서 `DATEDIFF_BIG`을 사용합니다.
  
`DATEDIFF_BIG`는 문자열 리터럴을 **datetime2** 형식으로 암시적으로 캐스팅합니다. 즉 `DATEDIFF_BIG`는 데이터가 문자열로 전달될 때 형식 YDM을 지원하지 않습니다. YDM 형식을 사용하려면 문자열을 **datetime** 또는 **smalldatetime** 형식으로 명시적으로 캐스팅해야 합니다.
  
SET DATEFIRST를 지정해도 `DATEDIFF_BIG`에는 영향을 주지 않습니다. `DATEDIFF_BIG`은 항상 일요일을 한 주의 첫 날로 사용하여 함수가 결정적으로 작동하게 합니다.
  
## <a name="examples"></a>예 
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>startdate 및 enddate에 대한 열 지정  
이 예에서는 여러 유형의 식을 *startdate* 및 *enddate* 매개 변수에 대한 인수로 사용합니다. 테이블의 두 열 사이에 겹쳐지는 날짜 범위의 수를 계산합니다.
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF_BIG(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  

더 자세한 예는 [DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)를 참조합니다.
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
