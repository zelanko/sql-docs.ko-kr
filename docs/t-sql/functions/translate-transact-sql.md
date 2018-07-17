---
title: TRANSLATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
caps.latest.revision: 5
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 6aa2621c9ff7a2ea9301384c9aab81df7f7144ad
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37784374"
---
# <a name="translate-transact-sql"></a>TRANSLATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

두 번째 인수에 지정된 몇 문자가 문자의 대상 집합으로 변환된 이후 첫 번째 인수로 제공된 문자열을 반환합니다.

## <a name="syntax"></a>구문   
```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>인수   

inputString   
모든 문자 형식(nvarchar, varchar, nchar, char)의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.

문자   
대체할 문자가 포함된 모든 문자 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.

번역   
두 번째 인수의 형식 및 길이가 일치하는 문자 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.

## <a name="return-types"></a>반환 형식   
`inputString`과 형식이 동일하면서 두 번째 인수의 문자가 세 번째 인수에서 일치하는 문자로 대체되는 문자 식을 반환합니다.

## <a name="remarks"></a>Remarks   

문자와 번역의 길이가 다를 경우 `TRANSLATE` 함수는 오류를 반환합니다. null 값이 문자 또는 교체 인수로 제공되는 경우 `TRANSLATE` 함수는 변경되지 않은 입력을 반환합니다. `TRANSLATE` 함수의 동작은 [REPLACE](../../t-sql/functions/replace-transact-sql.md) 함수와 동일해야 합니다.   

`TRANSLATE` 함수의 동작은 여러 개의 `REPLACE` 함수를 사용하는 경우와 동일합니다.

`TRANSLATE`은 언제나 SC 데이터 정렬을 인식합니다.

## <a name="examples"></a>예   

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>1. 대괄호 및 중괄호를 일반 괄호로 대체합니다.    
다음 쿼리는 입력 문자열의 대괄호와 중괄호를 괄호로 대체합니다.
```
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
2*(3+4)/(7-2)
```

>  [!NOTE]
>  이 예의 `TRANSLATE` 함수는 `REPLACE`를 사용하는 다음 명령문과 동일하지만 훨씬 간단합니다. `SELECT REPLACE(REPLACE(REPLACE(REPLACE('2*[3+4]/{7-2}','[','('), ']', ')'), '{', '('), '}', ')');` 


###  <a name="b-convert-geojson-points-into-wkt"></a>2. GeoJSON 포인트를 WKT로 변환    
GeoJSON은 다양한 지리 데이터 구조를 인코딩하는 형식입니다. `TRANSLATE` 함수에서는 개발자가 GeoJSON 포인트를 WKT 형식으로 변환하거나 그 반대로 쉽게 변환할 수 있습니다. 다음 쿼리는 입력 문자열의 대괄호와 중괄호를 괄호로 대체합니다.   
```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   


|점  |좌표 |  
---------|--------- |
(137.4  72.3) |[137.4,72.3] |


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

