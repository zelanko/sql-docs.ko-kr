---
title: ASCII(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASCII_TSQL
- ASCII
dev_langs:
- TSQL
helpviewer_keywords:
- ASCII function
- characters [SQL Server], ASCII
- code [SQL Server], ASCII
- leftmost character of expression
ms.assetid: 45c2044a-0593-4805-8bae-0fad4bde2e6b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 792de11767c353977649e52a08e66c76f5833a9e
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633452"
---
# <a name="ascii-transact-sql"></a>ASCII(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

문자 식에서 가장 왼쪽 문자의 ASCII 코드 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ASCII ( character_expression )  
```  
  
## <a name="arguments"></a>인수  
*character_expression*  
[char](../../t-sql/language-elements/expressions-transact-sql.md) 또는 **varchar** 형식의 **식**입니다.
  
## <a name="return-types"></a>반환 형식
 **int**  
  
## <a name="remarks"></a>설명
ASCII는 **A**merican **S**tandard **C**ode for **I**nformation **I**nterchange를 나타냅니다. 최신 컴퓨터에 대한 문자 인코딩 표준으로 사용합니다. ASCII 문자 목록은 **ASCII**의 [인쇄 가능 문자](https://www.wikipedia.org/wiki/ASCII) 섹션을 참조하세요.

ASCII는 7비트 문자 집합입니다. 확장 ASCII 또는 상위 ASCII는 `ASCII` 함수에서 처리하지 않는 8비트 문자 집합입니다. 

## <a name="examples"></a>예 

### <a name="a-this-example-assumes-an-ascii-character-set-and-returns-the-ascii-value-for-6-characters"></a>A. 이 예에서는 대상 문자열이 ASCII 문자 집합을 사용함을 전제로 하여 6개 문자에 대한 `ASCII` 값을 반환합니다.
  
```sql
SELECT ASCII('A') AS A, ASCII('B') AS B,   
ASCII('a') AS a, ASCII('b') AS b,  
ASCII(1) AS [1], ASCII(2) AS [2];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
A           B           a           b           1           2  
----------- ----------- ----------- ----------- ----------- -----------  
65          66          97          98          49          50  
```  
  
### <a name="b-this-examples-shows-how-a-7-bit-ascii-value-is-returned-correctly-but-an-8-bit-extended-ascii-value-is-not-handled"></a>B. 이 예제에서는 7비트 ASCII 값이 올바르게 반환되는 방법을 보여 주지만 8비트 확장 ASCII 값은 처리되지 않습니다.

```sql
SELECT ASCII('P') AS [ASCII], ASCII('æ') AS [Extended_ASCII];
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
ASCII       Extended_ASCII
----------- --------------
80          195
```

위의 결과가 올바른 문자 코드 포인트에 매핑되는지 확인하려면 `CHAR` 또는 `NCHAR` 함수에서 출력 값을 사용합니다.

```sql
SELECT NCHAR(80) AS [CHARACTER], NCHAR(195) AS [CHARACTER];
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
CHARACTER CHARACTER
--------- ---------
P         Ã
```

이전 결과에서 코드 포인트 195에 대한 문자는 **æ**가 아니라 **Ã**입니다. `ASCII` 함수는 첫 번째 7비트 스트림을 읽을 수 있지만 추가 비트는 읽을 수 없기 때문입니다. 문자 `æ`에 대한 올바른 코드 포인트는 `UNICODE` 함수를 사용하여 찾을 수 있습니다. 이 함수는 올바른 문자 코드 포인트를 지원하거나 반환할 수 있습니다.

```sql
SELECT UNICODE('æ') AS [Extended_ASCII], NCHAR(230) AS [CHARACTER];
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
Extended_ASCII CHARACTER
-------------- ---------
230            æ
```

## <a name="see-also"></a>참고 항목
 [CHAR&#40;Transact-SQL&#41;](../../t-sql/functions/char-transact-sql.md)  
 [NCHAR&#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)  
 [UNICODE&#40;Transact-SQL&#41;](../../t-sql/functions/unicode-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
