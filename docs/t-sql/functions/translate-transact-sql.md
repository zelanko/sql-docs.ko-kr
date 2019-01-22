---
title: TRANSLATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 591d2dcbb8a14cff7e4595bdeeab93787f51c5cf
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54419878"
---
# <a name="translate-transact-sql"></a>TRANSLATE(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

두 번째 인수에 지정된 일부 문자가 세 번째 인수에 지정된 문자의 대상 세트로 변환된 이후 첫 번째 인수로 제공된 문자열을 반환합니다.

## <a name="syntax"></a>구문

```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>인수   

 *inputString*   
 검색할 문자열 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 모든 문자 데이터 형식(nvarchar, varchar, nchar, char)은 *inputString*이 될 수 있습니다.

 *characters*   
 바꿔야 하는 문자가 포함된 문자열 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 모든 문자 데이터 형식은 *characters*가 될 수 있습니다.

*translations*   
 대체 문자를 포함하는 문자열 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *translations*는 *characters*와 데이터 종류 및 길이가 같아야 합니다.

## <a name="return-types"></a>반환 형식

`inputString`과 데이터 형식이 동일하면서 두 번째 인수의 문자가 세 번째 인수에서 일치하는 문자로 대체되는 문자 식을 반환합니다.

## <a name="remarks"></a>Remarks   

*characters*와 *translations* 식이 다른 경우 `TRANSLATE`는 오류를 반환합니다. 인수 중에 NULL이 있는 경우 `TRANSLATE`는 NULL을 반환합니다.  

`TRANSLATE` 함수의 동작은 [REPLACE](../../t-sql/functions/replace-transact-sql.md) 함수를 여러 개 사용할 때와 유사합니다. 그러나 `TRANSLATE`는 문자를 두 번 이상 대체하지 않습니다. 이는 각각의 사용이 모든 관련 문자를 대체하기 때문에 여러 `REPLACE` 함수와 유사하지 않습니다. 


`TRANSLATE`은 언제나 SC 데이터 정렬을 인식합니다.

## <a name="examples"></a>예

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>1. 대괄호 및 중괄호를 일반 괄호로 대체합니다.

다음 쿼리는 입력 문자열의 대괄호와 중괄호를 괄호로 대체합니다.

```sql
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

```plain_text
2*(3+4)/(7-2)
```

#### <a name="equivalent-calls-to-replace"></a>동일한 REPLACE 호출

다음 SELECT 문에는 REPLACE 함수에 대한 4개의 중첩된 호출 그룹이 있습니다. 이 그룹은 앞의 SELECT에서 만든 TRANSLATE 함수에 대한 한 번의 호출과 동일합니다.

```sql
SELECT
REPLACE
(
      REPLACE
      (
            REPLACE
            (
                  REPLACE
                  (
                        '2*[3+4]/{7-2}',
                        '[',
                        '('
                  ),
                  ']',
                  ')'
            ),
            '{',
            '('
      ),
      '}',
      ')'
);
```

###  <a name="b-convert-geojson-points-into-wkt"></a>2. GeoJSON 포인트를 WKT로 변환

GeoJSON은 다양한 지리 데이터 구조를 인코딩하는 형식입니다. `TRANSLATE` 함수에서는 개발자가 GeoJSON 포인트를 WKT 형식으로 변환하거나 그 반대로 쉽게 변환할 수 있습니다. 다음 쿼리는 입력 문자열의 대괄호와 중괄호를 괄호로 대체합니다.

```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|점  |좌표 |  
|---------|--------- |
|(137.4  72.3) |[137.4,72.3] |

### <a name="c-use-the-translate-function"></a>3. TRANSLATE 함수 사용

```sql
SELECT TRANSLATE('abcdef','abc','bcd') AS Translated,
       REPLACE(REPLACE(REPLACE('abcdef','a','b'),'b','c'),'c','d') AS Replaced;
```

결과는 다음과 같습니다.

| 변역됨 | 대체됨 |  
| ---------|--------- |
| bcddef | ddddef |


## <a name="see-also"></a>참고 항목

 [CONCAT&#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS&#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME&#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE&#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE&#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG&#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE&#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF&#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [문자열 함수(Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   

