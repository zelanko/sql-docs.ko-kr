---
title: DATETIMEOFFSETFROMPARTS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATETIMEOFFSETFROMPARTS_TSQL
- DATETIMEOFFSETFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEOFFSETFROMPARTS function
ms.assetid: 463da1f4-b4b6-45a3-9a95-ea1f99575542
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 21004da03ef694633b28518777c2ed2f0ac59d06
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85683350"
---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

지정된 날짜 및 시간 인수에 대한 **datetimeoffset** 값을 반환합니다. 반환된 값에는 전체 자릿수 인수에서 지정한 전체 자릿수 및 오프셋 인수에서 지정한 오프셋이 포함됩니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
```  
  
## <a name="arguments"></a>인수  

*year*  
년을 지정하는 정수 식입니다.  
  
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
소수 자릿수 초 값을 지정하는 정수 식입니다.  
  
*hour_offset*  
표준 시간대 오프셋의 시간 부분을 지정하는 정수 식입니다.  
  
*minute_offset*  
표준 시간대 오프셋의 분 부분을 지정하는 정수 식입니다.  
  
*전체 자릿수*  
**가 반환하는** datetimeoffset`DATETIMEOFFSETFROMPARTS` 값의 전체 자릿수를 지정하는 정수 리터럴 값입니다.  
  
## <a name="return-types"></a>반환 형식
**datetimeoffset(** *precision* **)**  
  
## <a name="remarks"></a>설명  

`DATETIMEOFFSETFROMPARTS`는 완전히 초기화된 **datetimeoffset** 데이터 형식을 반환합니다. 오프셋 인수는 표준 시간대 오프셋을 나타냅니다. 생략된 오프셋 인수의 경우 `DATETIMEOFFSETFROMPARTS`는 `00:00`의 표준 시간대 오프셋을 가정합니다. 즉 표준 시간대 오프셋이 없습니다. 지정된 오프셋 인수의 경우 `DATETIMEOFFSETFROMPARTS`는 두 인수의 값을 모두 예상하고 둘 다 양수 또는 음수 값으로 예상합니다. *minute_offset*에 값이 있고 *hour_offset*에 값이 없으면 `DATETIMEOFFSETFROMPARTS`에서 오류를 발생시킵니다. 다른 인수에 잘못된 값이 있으면 `DATETIMEOFFSETFROMPARTS`에서 오류를 발생시킵니다. 하나 이상의 필수 인수에 `NULL` 값이 있는 경우 `DATETIMEOFFSETFROMPARTS`는 `NULL`을 반환합니다. 그러나 *precision* 인수에 `NULL` 값이 있는 경우 `DATETIMEOFFSETFROMPARTS`에서 오류를 발생시킵니다.  
  
*fractions* 인수는 precision 인수에 의존합니다. 예를 들어 precision의 값이 7이면 각 소수 자릿수가 100나노초를 나타내고 precision이 3이면 각 소수 자릿수가 1밀리초를 나타냅니다. precision의 값이 0이면 fractions의 값도 0이어야 합니다. 그렇지 않으면 `DATETIMEOFFSETFROMPARTS`가 오류를 발생시킵니다.  
  
이 함수는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 서버 이상에 대한 원격 처리를 지원합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이전 버전이 설치되어 있는 서버에 대해서는 원격 처리를 지원하지 않습니다.
  
## <a name="examples"></a>예  
  
### <a name="a-an-example-without-fractions-of-a-second"></a>A. 소수 단위 초를 사용하지 않는 예  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2010, 12, 31, 14, 23, 23, 0, 12, 0, 7 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------
2010-12-31 14:23:23.0000000 +12:00  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. 소수 단위 초를 사용하는 예  

이 예에서는 *fractions* 및 *precision* 매개 변수의 사용 방법을 설명합니다.  

1. *fractions*의 값이 5이고 *precision*의 값이 1이면, *fractions*의 값은 1초의 5/10를 나타냅니다.  

2. *fractions*의 값이 50이고 *precision*의 값이 2이면, *fractions*의 값은 1초의 50/100을 나타냅니다.  

3. *fractions*의 값이 500이고 *precision*의 값이 3이면, *fractions*의 값은 1초의 500/1000을 나타냅니다.  
  
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
  
## <a name="see-also"></a>참고 항목
[datetimeoffset&#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
[AT TIME ZONE&#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  


