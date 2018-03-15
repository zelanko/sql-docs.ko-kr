---
title: DATETIMEOFFSETFROMPARTS(Transact-SQL) | Microsoft Docs
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
- DATETIMEOFFSETFROMPARTS_TSQL
- DATETIMEOFFSETFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEOFFSETFROMPARTS function
ms.assetid: 463da1f4-b4b6-45a3-9a95-ea1f99575542
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1c8a5f8bea3bf6ca97e0f7b4a35f8f78315716df
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

지정된 오프셋 및 전체 자릿수를 사용하여 지정된 날짜 및 시간에 대한 **datetimeoffset** 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
```  
  
## <a name="arguments"></a>인수  
*year*  
연도를 지정하는 정수 식입니다.
  
*month*  
월을 지정하는 정수 식입니다.
  
*day*  
일을 지정하는 정수 식입니다.
  
*hour*  
시간을 지정하는 정수 식입니다.
  
*minute*  
분을 지정하는 정수 식입니다.
  
*초*  
초를 지정하는 정수 식입니다.
  
*fractions*  
소수 자릿수를 지정하는 정수 식입니다.
  
*hour_offset*  
표준 시간대 오프셋의 시간 부분을 지정하는 정수 식입니다.
  
*minute_offset*  
표준 시간대 오프셋의 분 부분을 지정하는 정수 식입니다.
  
*전체 자릿수*  
반환할 **datetimeoffset** 값의 전체 자릿수를 지정하는 정수 리터럴입니다.
  
## <a name="return-types"></a>반환 형식
**datetimeoffset(** *precision* **)**
  
## <a name="remarks"></a>Remarks  
**DATETIMEOFFSETFROMPARTS**는 완전히 초기화된 **datetimeoffset** 데이터 형식을 반환합니다. 오프셋 인수는 표준 시간대 오프셋을 나타내는 데 사용됩니다. 오프셋 인수를 생략하면 표준 시간대 오프셋이 00:00인 것으로 간주됩니다. 즉, 표준 시간대 오프셋이 없습니다. 오프셋 인수를 지정할 경우 두 인수를 모두 지정해야 하고 둘 모두 양수 또는 음수여야 합니다. *minute_offset*이 *hour_offset*없이 지정되면 오류가 발생합니다. 다른 인수가 유효하지 않으면 오류가 발생합니다. 필수 인수가 Null일 경우에는 Null이 반환됩니다. 그러나 *precision* 인수가 Null일 경우에는, 오류가 발생합니다.
  
*fractions* 인수는 *precision* 인수에 의존합니다. 예를 들어 *precision*이 7이면 각 소수 자릿수가 100나노초를 나타내고 *precision*이 3이면 각 소수 자릿수가 1밀리초를 나타냅니다. *precision*의 값이 0이면 *fractions*의 값도 0이어야 합니다. 그렇지 않으면, 오류가 발생합니다.
  
이 함수는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이상 서버에 대해서는 원격으로 실행할 수 있지만 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이전 버전이 설치되어 있는 서버에 대해서는 원격으로 실행할 수 없습니다.
  
## <a name="examples"></a>예  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>1. 소수 단위 초를 사용하지 않는 간단한 예  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2010, 12, 31, 14, 23, 23, 0, 12, 0, 7 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------------------------  
2010-12-07 00:00:00.0000000 +00:00  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>2. 소수 단위 초를 사용하는 예  
다음 예에서는 *fractions* 및 *precision* 매개 변수의 사용 방법을 설명합니다.
1.   *fractions*의 값이 5이고 *precision*의 값이 1이면, *fractions*의 값은 1초의 5/10를 나타냅니다.  
1.   *fractions*의 값이 50이고 *precision*의 값이 2이면, *fractions*의 값은 1초의 50/100을 나타냅니다.  
1.   *fractions*의 값이 500이고 *precision*의 값이 3이면, *fractions*의 값은 1초의 500/1000을 나타냅니다.  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 5, 12, 30, 1 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 50, 12, 30, 2 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 500, 12, 30, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------------------  
2011-08-15 14:30:00.5 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.50 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.500 +12:30  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:
[datetimeoffset&#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  


