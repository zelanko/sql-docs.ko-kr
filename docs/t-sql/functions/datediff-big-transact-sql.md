---
title: DATEDIFF_BIG(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
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
ms.workload: On Demand
ms.openlocfilehash: 173daacfd95ec63789dde878e960d5a8b820a27c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

지정된 *startdate*와 *enddate* 사이에 지정된 *datepart* 경계의 수(부호 있는 큰 정수)를 반환합니다.
  
모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>인수  
*datepart*  
겹쳐지는 범위의 유형을 지정하는 *startdate*와 *enddate* 부분입니다. 다음 표에는 올바른 *datepart* 인수가 모두 나열되어 있습니다. 해당하는 사용자 정의 변수는 사용할 수 없습니다.
  
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
**time**, **date**, **smalldatetime**, **datetime**, **datetime2** 또는 **datetimeoffset** 값으로 확인할 수 있는 식입니다. *date*는 식, 열 식, 사용자 정의 변수 또는 문자열 리터럴일 수 있습니다. *startdate*은 *enddate*에서 뺍니다.  
모호성을 피하려면 4자리 연도를 사용하세요. 두 자리 연도에 대한 정보는 [Configure the two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.
  
*enddate*  
*startdate*를 참조하세요.
  
## <a name="return-type"></a>반환 형식  
 서명됨   
        **bigint**  
  
## <a name="return-value"></a>반환 값  
지정된 startdate와 enddate 사이에 겹쳐지는 지정된 datepart 경계의 갯수(부호있는 bigint)를 반환합니다.
-   각 *datepart*와 해당 약어는 동일한 값을 반환합니다.  
  
반환 값이 **bigint**에 대한 범위(-9,223,372,036,854,775,808에서 9,223,372,036,854,775,807 사이)를 벗어날 경우 오류가 반환됩니다. **밀리초**의 경우 *startdate*와 *enddate*의 최대 차이는 24일, 20시간, 31분 및 23.647초입니다. **초**의 경우 최대 차이는 68년입니다.
  
*startdate* 및 *enddate* 모두에 시간 값만 할당되고 *datepart*가 시간 *datepart*가 아니면 0이 반환됩니다.
  
*startdate* 또는 *endate*의 표준 시간대 오프셋 구성 요소는 반환 값을 계산하는 데 사용되지 않습니다.
  
[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)은 분 단위까지만 정확하므로 *startdate* 또는 *enddate*에 **smalldatetime** 값이 사용될 경우 반환 값에서 초와 밀리초는 항상 0으로 설정됩니다.
  
날짜 데이터 형식의 변수에 시간 값만 할당된 경우 누락된 날짜 부분의 값은 기본값인 1900-01-01로 설정됩니다. 시간 또는 날짜 데이터 형식의 변수에 날짜 값만 할당될 경우 누락된 시간 부분의 값은 기본값인 00:00:00으로 설정됩니다. *startdate* 또는 *enddate* 중 하나는 시간 부분만 있고 다른 하나는 날짜 부분만 있는 경우 누락된 시간 및 날짜 부분은 기본값으로 설정됩니다.
  
*startdate*와 *enddate*의 날짜 데이터 형식이 다르고 한 쪽의 시간 부분 또는 소수 자릿수 초의 전체 자릿수가 다른 쪽보다 많을 경우 다른 쪽에서 누락된 부분은 0으로 설정됩니다.
  
## <a name="datepart-boundaries"></a>datepart 범위
다음 명령문은 동일한 *startdate*와 동일한 *endate*를 가집니다. 이러한 날짜는 서로 인접하며 차이는 .0000001초입니다. 각 문에서 *startdate*와 *endate* 사이의 차이는 해당 *datepart*에서 하나의 달력 또는 시간 범위를 넘어섭니다. 각 문은 1을 반환합니다. 이 예에서 다른 연도가 사용되고 *startdate*와 *endate*가 달력의 같은 주에 있을 경우 **week**에 대한 반환 값은 0이 됩니다.

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
DATEDIFF_BIG은 SELECT 목록, WHERE, HAVING, GROUP BY 및 ORDER BY 절에서 사용할 수 있습니다.
  
DATEDIFF_BIG은 문자열 리터럴을 **datetime2** 형식으로 암시적으로 캐스팅합니다. 즉 DATEDIFF_BIG은 데이터가 문자열로 전달될 때 형식 YDM을 지원하지 않습니다. YDM 형식을 사용하려면 문자열을 **datetime** 또는 **smalldatetime** 형식으로 명시적으로 캐스팅해야 합니다.
  
SET DATEFIRST를 지정해도 DATEDIFF_BIG에는 영향을 주지 않습니다. DATEDIFF_BIG은 항상 일요일을 한 주의 첫 날로 사용하여 결정적 함수가 되도록 합니다.
  
## <a name="examples"></a>예  
다음 예에서는 여러 유형의 식을 *startdate* 및 *enddate* 매개 변수에 대한 인수로 사용합니다.
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>startdate 및 enddate에 대한 열 지정  
다음 예에서는 테이블의 두 열 사이에 겹쳐지는 날짜 범위의 수를 계산합니다.
  
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
  
추가 예제는 [DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)의 밀접한 관련 예제를 참조하세요.
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
