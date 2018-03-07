---
title: DATETIMEOFFSETFROMPARTS (Transact SQL) | Microsoft Docs
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

반환 된 **datetimeoffset** 고 지정 된 오프셋 및 전체 자릿수 지정 된 날짜 및 시간에 대 한 값입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
```  
  
## <a name="arguments"></a>인수  
*연도*  
연도를 지정하는 정수 식입니다.
  
*월*  
월을 지정하는 정수 식입니다.
  
*일*  
일을 지정하는 정수 식입니다.
  
*1 시간*  
시간을 지정하는 정수 식입니다.
  
*분*  
분을 지정하는 정수 식입니다.
  
*초*  
초를 지정하는 정수 식입니다.
  
*분수*  
소수 자릿수를 지정하는 정수 식입니다.
  
*hour_offset*  
표준 시간대 오프셋의 시간 부분을 지정하는 정수 식입니다.
  
*minute_offset*  
표준 시간대 오프셋의 분 부분을 지정하는 정수 식입니다.
  
*전체 자릿수*  
정수 리터럴 자릿수를 지정 하는 **datetimeoffset** 값을 반환할 수 있습니다.
  
## <a name="return-types"></a>반환 형식
**datetimeoffset (** *정밀도* **)**
  
## <a name="remarks"></a>주의  
**DATETIMEOFFSETFROMPARTS** 는 완전히 초기화 된 반환 **datetimeoffset** 데이터 형식입니다. 오프셋 인수는 표준 시간대 오프셋을 나타내는 데 사용됩니다. 오프셋 인수를 생략하면 표준 시간대 오프셋이 00:00인 것으로 간주됩니다. 즉, 표준 시간대 오프셋이 없습니다. 오프셋 인수를 지정할 경우 두 인수를 모두 지정해야 하고 둘 모두 양수 또는 음수여야 합니다. 경우 *minute_offset* 없이 지정 된 *hour_offset*, 오류가 발생 합니다. 다른 인수가 유효하지 않으면 오류가 발생합니다. 필수 인수가 Null일 경우에는 Null이 반환됩니다. 그러나 경우는 *정밀도* 인수가 null 일 경우 다음 오류가 발생 합니다.
  
*분수* 인수에 따라 달라 집니다는 *정밀도* 인수입니다. 예를 들어 경우 *정밀도* 은 7, 다음 하는 경우 각 소수 자릿수가 100 나노초를 나타내고 *정밀도* 3 인 다음 각 소수 자릿수가 1 밀리초를 나타냅니다. 하는 경우의 값 *정밀도* 0의 값이 *분수* 또한 해야 0; 그렇지 않으면 오류가 발생 합니다.
  
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
다음 예제에서는 *분수* 및 *정밀도* 매개 변수:
1.   때 *분수* 5 값 및 *정밀도* 에 값이 1 항목이 값 *분수* 5/10 초를 나타냅니다.  
1.   때 *분수* 50 값 및 *정밀도* 에 값이 2 항목이 값 *분수* 50/100 초를 나타냅니다.  
1.   때 *분수* 값이 500 및 *정밀도* 값은 값은 값 3 다음 *분수* 500/1000 초를 나타냅니다.  
  
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
[표준 시간대 &AMP;#40; Transact SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  


