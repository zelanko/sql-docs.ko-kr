---
description: DATETIME2FROMPARTS(Transact-SQL)
title: DATETIME2FROMPARTS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATETIME2FROMPARTS_TSQL
- DATETIME2FROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIME2FROMPARTS function
ms.assetid: 632b757d-d2d1-43a5-b870-792a779ae204
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 46dde800f82285639093b015f621902a727d33b1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478684"
---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 함수는 지정된 날짜 및 시간 인수에 대한 **datetime2** 값을 반환합니다. 반환된 값에는 전체 자릿수 인수에서 지정한 전체 자릿수가 있습니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

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
  
*전체 자릿수*  
`DATETIME2FROMPARTS`에서 반환하는 **datetime2** 값의 전체 자릿수를 지정하는 정수 식입니다.
  
## <a name="return-types"></a>반환 형식
**datetime2(** *precision* **)**
  
## <a name="remarks"></a>설명  
`DATETIME2FROMPARTS`는 완전히 초기화된 **datetime2** 값을 반환합니다. `DATETIME2FROMPARTS`는 적어도 하나 이상의 필수 인수에 잘못된 값이 있는 경우 오류를 발생시킵니다. `DATETIME2FROMPARTS`는 적어도 하나 이상의 필수 인수에 null 값이 있는 경우 null을 반환합니다. 그러나 *전체 자릿수* 인수에 null 값이 있는 경우 `DATETIME2FROMPARTS`에서 오류를 발생시킵니다.

*fractions* 인수는 *precision* 인수에 의존합니다. 예를 들어 *precision* 의 값이 7이면 각 소수 자릿수가 100나노초를 나타내고 *precision* 이 3이면 각 소수 자릿수가 1밀리초를 나타냅니다. *precision* 의 값이 0이면 *fractions* 의 값도 0이어야 합니다. 그렇지 않으면 `DATETIME2FROMPARTS`가 오류를 발생시킵니다.
  
이 함수는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 서버 이상에 대한 원격 처리를 지원합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이전 버전이 설치되어 있는 서버에 대해서는 원격 처리를 지원하지 않습니다.
  
## <a name="examples"></a>예제  
  
### <a name="a-an-example-without-fractions-of-a-second"></a>A. 소수 단위 초를 사용하지 않는 예  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. 소수 단위 초를 사용하는 예  
이 예에서는 *fractions* 및 *precision* 매개 변수의 사용 방법을 설명합니다.
  
1.  *fractions* 의 값이 5이고 *precision* 의 값이 1이면, *fractions* 의 값은 1초의 5/10를 나타냅니다.  
  
2.  *fractions* 의 값이 50이고 *precision* 의 값이 2이면, *fractions* 의 값은 1초의 50/100을 나타냅니다.  
  
3.  *fractions* 의 값이 500이고 *precision* 의 값이 3이면, *fractions* 의 값은 1초의 500/1000을 나타냅니다.  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목
[datetime2&#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)
  
  

