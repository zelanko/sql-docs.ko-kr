---
title: DATEDIFF_BIG (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5067ed8b36711b2f5cd39eea2cc16e0450efa996
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

지정 된 수 (부호 있는 큰 정수)를 반환 *datepart* 지정 된 간에 겹쳐지는 *startdate* 및 *enddate*합니다.
  
모든 개요 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 데이터 형식 및 함수, 참조 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
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
 서명됨   
        **bigint**  
  
## <a name="return-value"></a>반환 값  
지정 된 datepart 경계 반환 수 (부호 있는 bigint) 지정한 startdate와 enddate 사이 포함 합니다.
-   각 *datepart* 해당 약어는 동일한 값을 반환 합니다.  
  
반환 값은 범위를 벗어나는 경우 **bigint** (9223372036854775807에-9223372036854775808), 오류가 반환 됩니다. 에 대 한 **밀리초**, 사이의 최대 오차 *startdate* 및 *enddate* 은 24 일, 20 시간, 31 분 및 23.647 초입니다. 에 대 한 **두 번째**, 최대 차이 68 년입니다.
  
경우 *startdate* 및 *enddate* 둘 다 시간 값만 할당 되 고 *datepart* 은 시간이 아닙니다 *datepart*, 0이 반환 됩니다.
  
표준 시간대 오프셋의 구성 요소 *startdate* 또는 *endate* 반환 값을 계산한 다음에 사용 되지 않습니다.
  
때문에 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 분만에 때는 **smalldatetime** 에 값이 사용 *startdate* 또는 *enddate*, 초 및 밀리초는 항상 반환 값에 0으로 설정 됩니다.
  
날짜 데이터 형식의 변수에 시간 값만 할당된 경우 누락된 날짜 부분의 값은 기본값인 1900-01-01로 설정됩니다. 시간 또는 날짜 데이터 형식의 변수에 날짜 값만 할당될 경우 누락된 시간 부분의 값은 기본값인 00:00:00으로 설정됩니다. 어느 경우 *startdate* 또는 *enddate* 시간 부분만 있고 다른만 날짜 부분, 누락 된 시간 및 날짜 부분은 기본값으로 설정 했습니다.
  
경우 *startdate* 및 *enddate* 는 서로 다른 날짜 데이터 형식의 없고 하나 시간 부분 또는 소수 자릿수 초의 전체 자릿수가 다른에 다른 누락 된 부분은 0으로 설정 됩니다.
  
## <a name="datepart-boundaries"></a>datepart 경계
다음 문에 동일한 *startdate* 과 동일한 *endate*합니다. 이러한 날짜는 서로 인접하며 차이는 .0000001초입니다. 차이 *startdate* 및 *endate* 각 문에서 하나의 달력 또는 시간 경계를 넘는 해당 *datepart*합니다. 각 문은 1을 반환합니다. 이 예에서 다른 연도가 사용 되 고 두 *startdate* 및 *endate* 달력 주에 대 한 반환 값에 **주** 0 이어야 합니다.
  
`SELECT DATEDIFF_BIG(year, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF_BIG(quarter, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF_BIG(month, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF_BIG(dayofyear, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF_BIG(day, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF_BIG(week, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF_BIG(hour, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF_BIG(minute, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF_BIG(second, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
## <a name="remarks"></a>주의  
Select 목록에 사용할 수 DATEDIFF_BIG WHERE, HAVING, GROUP BY 및 ORDER BY 절.
  
DATEDIFF_BIG에 문자열 리터럴을으로 암시적으로 캐스팅 한 **datetime2** 유형입니다. 즉, DATEDIFF_BIG 문자열로 전달 될 때 형식 YDM 지원 하지 않습니다. 문자열을 명시적으로 캐스팅 해야는 **datetime** 또는 **smalldatetime** YDM 형식을 사용 하는 형식입니다.
  
SET DATEFIRST를 지정 해도 DATEDIFF_BIG에는 영향이 없습니다. DATEDIFF_BIG 항상 일요일을 첫 번째 요일을 사용 하 여 함수는 결정적 되도록 합니다.
  
## <a name="examples"></a>예  
다음 예에서는 다양 한 유형의 식에 대 한 인수로 사용 하 여는 *startdate* 및 *enddate* 매개 변수입니다.
  
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
  
많은 다른 예제를 보려면의 밀접 한 관련이 예제를 참조 [DATEDIFF &#40; Transact SQL &#41; ](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40; Transact SQL &#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  

