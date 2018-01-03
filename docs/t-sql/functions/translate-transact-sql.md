---
title: "번역 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords: TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
caps.latest.revision: "5"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a498430f8af12bad1e5ec934dcb60c63aeb96e56
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="translate-transact-sql"></a>번역 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

두 번째 인수에 지정 된 일부 문자는 문자 대상 집합으로 변환 후 첫 번째 인수로 제공 된 문자열을 반환 합니다.

## <a name="syntax"></a>구문   
```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>인수   

inputString   
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 모든 문자 형식 (예: nvarchar, varchar, nchar, char).

문자   
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 교체 해야 하는 문자가 포함 된 모든 문자 형식의 합니다.

번역   
문자 [식](../../t-sql/language-elements/expressions-transact-sql.md) 두 번째 인수 유형 및 길이에서 일치 하는 합니다.

## <a name="return-types"></a>반환 형식   
와 동일한 형식의 문자 식을 반환 `inputString` 문자는 두 번째 인수를 세 번째 인수에서 일치 하는 문자가 바뀝니다.

## <a name="remarks"></a>주의   

`TRANSLATE`문자 및 번역 길이가 다른 경우 함수에서 오류가 반환 됩니다. `TRANSLATE`함수는 null 값은 문자 또는 교체 인수도 제공 되는 경우 변경 되지 않은 입력을 반환 합니다. 동작은 `TRANSLATE` 함수는 동일 해야 합니다.는 [대체](../../t-sql/functions/replace-transact-sql.md) 함수입니다.   

동작은 `TRANSLATE` 함수는 여러 사용 하 여 해당 `REPLACE` 함수입니다.

`TRANSLATE`항상 SC 데이터 정렬을 인식 합니다.

## <a name="examples"></a>예   

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>1. 일반 중괄호 정사각형와 둥근 중괄호 대체    
다음 쿼리는 괄호와 함께 입력된 문자열에서 사각형와 둥근 중괄호를 대체합니다.
```
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
2*(3+4)/(7-2)
```

>  [!NOTE]
>  `TRANSLATE` 예제의와 동일 하지만 다음 문을 사용할 때 보다 훨씬 간단 하 게 `REPLACE`:`SELECT REPLACE(REPLACE(REPLACE(REPLACE('2*[3+4]/{7-2}','[','('), ']', ')'), '{', '('), '}', ')');` 


###  <a name="b-convert-geojson-points-into-wkt"></a>2. GeoJSON 지점은 WKT으로 변환    
GeoJSON는 다양 한 지리적 데이터 구조를 인코딩에 대 한 형식입니다. 와 `TRANSLATE` 함수 개발자 GeoJSON 지점은 WKT 형식으로 또는 그 반대로 쉽게 변환할 수 있습니다. 다음 쿼리를 일반 중괄호 입력에 사각형와 둥근 중괄호를 대체합니다.   
```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   


|점  |좌표 |  
---------|--------- |
(137.4  72.3) |[137.4,72.3] |


## <a name="see-also"></a>관련 항목:

[문자열 함수 (Transact SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
[REPLACE (Transact SQL)](../../t-sql/functions/replace-transact-sql.md)   

