---
title: STRING_SPLIT(Transact-SQL) | Microsoft Docs
description: STRING_SPLIT 함수의 Transact-SQL 참조입니다. 이 테이블 반환 함수는 문자 구분 기호를 기준으로 문자열을 부분 문자열로 분할합니다.
ms.date: 11/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current||=azure-sqldw-latest||>= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions
ms.openlocfilehash: a7c3220138c0f375b043f41044d5023fdb355ff5
ms.sourcegitcommit: ef7539af262aad327270bb28752e420197e9e776
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93405050"
---
# <a name="string_split-transact-sql"></a>STRING_SPLIT(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

지정된 구분 기호 문자에 따라 문자열을 부분 문자열의 행으로 분할하는 테이블 반환 함수입니다.

#### <a name="compatibility-level-130"></a>호환성 수준 130

STRING_SPLIT에는 130 이상의 호환성 수준이 필요합니다. 130 미만 수준인 경우 SQL Server는 STRING_SPLIT 함수를 찾을 수 없습니다.

데이터베이스의 호환성 수준을 변경하려면 [데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)을 참조합니다.

> [!NOTE]
> Azure Synapse Analytics의 STRING_SPLIT에는 호환성 구성이 필요하지 않습니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  

```syntaxsql
STRING_SPLIT ( string , separator )  
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수

 *string*  
 모든 문자 형식(예: **nvarchar** , **varchar** , **nchar** 또는 **char** )의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
 *separator*  
 연결된 부분 문자열의 구분 기호로 사용되는 모든 문자 형식(예: **nvarchar(1)** , **varchar(1)** , **nchar(1)** 또는 **char(1)** )의 단일 문자 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="return-types"></a>반환 형식  

부분 문자열인 행의 단일 열 테이블을 반환합니다. 열의 이름은 **value** 입니다. 입력 조각이 **nvarchar** 또는 **nchar** 인 경우 **nvarchar** 를 반환합니다. 그렇지 않으면 **varchar** 를 반환합니다. 반환 형식의 길이는 문자열 인수의 길이와 동일합니다.  
  
## <a name="remarks"></a>설명  

**STRING_SPLIT** 는 부분 문자열을 구분 기호로 분리한 문자열을 입력하고 구분 기호로 사용될 문자 하나를 입력합니다. STRING_SPLIT는 부분 문자열이 포함된 행의 단일 열 테이블을 출력합니다. 출력 열의 이름은 **value** 입니다.

출력 행은 순서에 관계 없을 수 있습니다. 순서가 입력 문자열의 부분 문자열 순서와 일치하지 _않을 수_ 있습니다. SELECT 문(`ORDER BY value`)에서 ORDER BY 절을 사용하여 최종 정렬 순서를 재정의할 수 있습니다.

0x0000( **char(0)** )은 Windows 데이터 정렬에서 정의되지 않은 문자이며 STRING_SPLIT에 포함할 수 없습니다.

0 길이의 빈 부분 문자열은 입력 문자열에서 구분 기호 문자 두 개 이상이 연속되는 경우 존재합니다. 빈 부분 문자열은 일반 부분 문자열과 동일한 방식으로 처리됩니다. WHERE 절(`WHERE value <> ''`)을 사용하여 빈 부분 문자열을 포함하는 모든 행을 필터링할 수 있습니다. 입력 문자열이 NULL인 경우 STRING_SPLIT 테이블 반환 함수는 빈 테이블을 반환합니다.  

예를 들어 다음 SELECT 문은 구분 기호로 공백 문자를 사용합니다.

```sql
SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');
```

실제 실행에서 앞의 SELECT 문은 다음과 같은 결과 테이블을 반환했습니다.  
  
|값|  
| :-- |  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|amet.|  
| &nbsp; |

## <a name="examples"></a>예  
  
### <a name="a-split-comma-separated-value-string"></a>A. CSV(쉼표로 구분된 값) 문자열 분할

쉼표로 구분된 값 목록을 구문 분석하고 비어 있지 않은 토큰을 모두 반환합니다.  

```sql
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';
```

구분 기호 사이에 아무 것도 없을 경우 STRING_SPLIT은 빈 문자열을 반환합니다. RTRIM(value) <> ''조건은 빈 토큰을 제거합니다.  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. 열에서 CSV(쉼표로 구분된 값) 문자열 분할

제품 테이블에는 다음 예제와 같이 쉼표로 구분된 태그 목록이 포함된 열이 있습니다.  
  
|ProductId|속성|태그들|  
|---------------|----------|----------|  
|1|Full-Finger Gloves|clothing,road,touring,bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike,mountain|  
  
다음 쿼리는 각 태그 목록을 변환하고 원래 행과 결합합니다.  

```sql  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|ProductId|속성|값|  
|---------------|----------|-----------|  
|1|Full-Finger Gloves|clothing|  
|1|Full-Finger Gloves|도로|  
|1|Full-Finger Gloves|touring|  
|1|Full-Finger Gloves|bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike|  
|3|HL Mountain Frame|mountain|  

  >[!NOTE]
  > 출력 순서는 입력 문자열의 하위 문자열 순서와 일치하지 _않을 수_ 있으므로 순서가 달라질 수 있습니다.
  
### <a name="c-aggregation-by-values"></a>C. 값 기준 정렬

사용자는 각 태그별 제품의 수를 표시하고 제품 수 기준으로 정렬한 보고서를 생성하여 제품 수가 2 초과인 태그만 필터링해야 합니다.  

```sql  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```

### <a name="d-search-by-tag-value"></a>D. 태그 값으로 검색

개발자는 키워드를 기준으로 물품을 찾는 쿼리를 만들어야 합니다. 다음과 같은 쿼리를 사용할 수 있습니다.  
  
단일 태그(의복)가 포함된 제품 찾기:  

```sql
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```

지정된 태그 2개(의복 및 도로)가 포함된 제품 찾기:  

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road'));  
```

### <a name="e-find-rows-by-list-of-values"></a>E. 값 목록 기준으로 행 찾기

개발자는 ID 목록을 기준으로 물품을 찾는 쿼리를 만들어야 합니다. 다음과 같은 쿼리를 사용할 수 있습니다.  

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')
    ON value = ProductId;  
```  

이전 STRING_SPLIT 사용이 일반적인 안티패턴을 대체합니다. 이러한 안티패턴은 TRANSACT-SQL 또는 애플리케이션 계층에서 동적 SQL 문자열을 생성할 수 있습니다. 또는 LIKE 연산자를 사용하여 안티패턴을 구현할 수 있습니다. 다음 SELECT 문 예제를 참조하세요.

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```

## <a name="see-also"></a>참고 항목

- [LEFT&#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)
- [LTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)
- [RIGHT&#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)
- [RTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)
- [SUBSTRING&#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)
- [TRIM&#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)
- [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
