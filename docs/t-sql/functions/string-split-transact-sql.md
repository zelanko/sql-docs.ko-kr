---
title: STRING_SPLIT(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 00debf90f1b79a0e38cb883f31479ae5731f40d3
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  지정된 구분 기호를 사용하여 문자 식을 분할합니다.  
  
> [!NOTE]  
>  **STRING_SPLIT** 함수는 호환성 수준 130에서만 사용할 수 있습니다. 데이터베이스 호환성 수준이 130보다 낮으면 SQL Server에서 **STRING_SPLIT** 함수를 찾아 실행할 수 없습니다. 다음 명령을 사용하여 데이터베이스의 호환성 수준을 변경할 수 있습니다.  
> ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
>   
>  새 Azure SQL Database에서도 호환성 수준 120이 기본값일 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>인수  
 *string*  
 모든 문자 형식(즉, **nvarchar**, **varchar**, **nchar** 또는 **char**)의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
 *separator*  
 연결된 문자열의 구분 기호로 사용되는 모든 문자 형식(예: **nvarchar(1)**, **varchar(1)**, **nchar(1)** 또는 **char(1)**)의 단일 문자 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="return-types"></a>반환 형식  
 조각이 포함된 단일 열 테이블을 반환합니다. 열의 이름은 **value**입니다. 입력 조각이 **nvarchar** 또는 **nchar**인 경우 **nvarchar**를 반환합니다. 그렇지 않으면 **varchar**를 반환합니다. 반환 형식의 길이는 문자열 인수의 길이와 동일합니다.  
  
## <a name="remarks"></a>Remarks  
 **STRING_SPLIT**은 나누어야 할 문자열과 문자열을 나누는 데 사용할 구분 기호를 사용합니다. 이 함수는 부분 문자열이 포함된 단일 열 테이블을 반환합니다. 예를 들어 공백 문자를 구분 기호로 사용하는 다음의 `SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');` 문은 다음과 같은 결과 테이블을 반환합니다.  
  
|value|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|amet.|  
  
 입력 문자열이 **NULL**인 경우 **STRING_SPLIT** 테이블 반환 함수는 빈 테이블을 반환합니다.  
  
 **STRING_SPLIT**은 130보다 높은 호환성 모드가 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-split-comma-separated-value-string"></a>1. CSV(쉼표로 구분된 값) 문자열 분할  
 쉼표로 구분된 값 목록을 구문 분석하고 비어 있지 않은 토큰을 모두 반환합니다.  
  
```  
  
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';  
  
```  
  
 구분 기호 사이에 아무 것도 없을 경우 STRING_SPLIT은 빈 문자열을 반환합니다. RTRIM(value) <> ''조건은 빈 토큰을 제거합니다.  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>2. 열에서 CSV(쉼표로 구분된 값) 문자열 분할  
 제품 테이블에는 다음 예제와 같이 쉼표로 구분된 태그 목록이 포함된 열이 있습니다.  
  
|ProductId|속성|Tags|  
|---------------|----------|----------|  
|1|Full-Finger Gloves|clothing,road,touring,bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike,mountain|  
  
 다음 쿼리는 각 태그 목록을 변환하고 원래 행과 결합합니다.  
  
```  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|ProductId|속성|value|  
|---------------|----------|-----------|  
|1|Full-Finger Gloves|clothing|  
|1|Full-Finger Gloves|road|  
|1|Full-Finger Gloves|touring|  
|1|Full-Finger Gloves|bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike|  
|3|HL Mountain Frame|mountain|  
  
### <a name="c-aggregation-by-values"></a>3. 값 기준 정렬  
 사용자는 각 태그별 제품의 수를 표시하고 제품 수 기준으로 정렬한 보고서를 생성하여 제품 수가 2개보다 많은 태그만 필터링해야 합니다.  
  
```  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```  
  
### <a name="d-search-by-tag-value"></a>4. 태그 값으로 검색  
 개발자는 키워드를 기준으로 물품을 찾는 쿼리를 만들어야 합니다. 다음과 같은 쿼리를 사용할 수 있습니다.  
  
 단일 태그(의복)가 포함된 제품 찾기:  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```  
  
 지정된 태그 2개(의복 및 도로)가 포함된 제품 찾기:  
  
```  
  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>5. 값 목록 기준으로 행 찾기  
 개발자는 ID 목록을 기준으로 물품을 찾는 쿼리를 만들어야 합니다. 다음과 같은 쿼리를 사용할 수 있습니다.  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
 이 함수는 응용 프로그램 계층 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 동적 SQL 문자열을 만들거나 LIKE 연산자를 사용하는 등의 일반적 안티 패턴을 대체합니다.  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>참고 항목  
 [LEFT&#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT&#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [SUBSTRING&#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM&#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
