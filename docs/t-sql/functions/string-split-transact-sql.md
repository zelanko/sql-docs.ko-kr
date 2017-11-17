---
title: STRING_SPLIT (Transact SQL) | Microsoft Docs
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
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 049bdf1021d57e28ed94e11c89aa997ee0eba5e5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  지정 된 구분 기호를 사용 하 여 문자 식을 분할 합니다.  
  
> [!NOTE]  
>  **STRING_SPLIT** 함수는 호환성 수준 130 에서만 사용할 수 있습니다. SQL Server를 찾아 실행 될 데이터베이스 호환성 수준이 130 보다 낮은 경우 **STRING_SPLIT** 함수입니다. 다음 명령을 사용하여 데이터베이스의 호환성 수준을 변경할 수 있습니다.  
> ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
>   
>  새 Azure SQL 데이터베이스에도 기본 호환성 수준 120 수 있음을 확인 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>인수  
 *string*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 모든 문자 형식의 (즉, **nvarchar**, **varchar**, **nchar** 또는 **char**).  
  
 *구분 기호*  
 단일 문자 [식](../../t-sql/language-elements/expressions-transact-sql.md) 모든 문자 형식 (예: **nvarchar(1)**, **varchar (1)**, **nchar(1)** 또는  **char(1)**) 연결 된 문자열에 대 한 구분 기호로 사용 되는 합니다.  
  
## <a name="return-types"></a>반환 형식  
 조각 사용 하 여 단일 열 테이블을 반환합니다. 열 이름은 **값**합니다. 반환 **nvarchar** 경우 입력된 인수 중 하나가 **nvarchar** 또는 **nchar**합니다. 그렇지 않으면 반환 **varchar**합니다. 반환 형식의 길이 문자열 인수의 길이와 같습니다.  
  
## <a name="remarks"></a>주의  
 **STRING_SPLIT** 나누어야 하는 문자열 및 문자열을 나누는 데 사용할 구분 기호를 사용 합니다. 부분 문자열이 있는 단일 열 테이블을 반환 합니다. 예를 들어 다음 문은 `SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');` 구분 기호로 공백 문자를 사용 하 여 결과 테이블에 다음 반환:  
  
|value|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|사이트|  
|amet 합니다.|  
  
 입력된 문자열의 형식이 **NULL**, **STRING_SPLIT** 테이블 반환 함수는 빈 테이블을 반환 합니다.  
  
 **STRING_SPLIT** 최소한 호환 모드 130입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-split-comma-separated-value-string"></a>1. 분할 쉼표로 구분 된 값 문자열로  
 값의 쉼표로 구분 된 목록을 구문 분석 하 고 있는 모든 비어 있지 않은 토큰을 반환 합니다.  
  
```  
  
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';  
  
```  
  
 STRING_SPLIT은 내용이 없는 경우 구분 기호 사이의 빈 문자열을 반환 합니다. 조건 RTRIM(value) <> ' 빈 토큰을 제거 합니다.  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>2. 분할 쉼표로 구분 된 열에 값 문자열로  
 제품 테이블에는 쉼표를 별도 태그 목록으로 다음 예제와 같이 지정 된 열을 있습니다.  
  
|productId|이름|Tags|  
|---------------|----------|----------|  
|1.|전체 손가락 Gloves|clothing touring bike 이동 중|  
|2|LL 헤드셋|자전거|  
|3|HL Mountain Frame|산악 자전거, 자전거|  
  
 다음 쿼리는 태그의 각 목록을 변환 하 고 원래 행으로 연결 합니다.  
  
```  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|productId|이름|value|  
|---------------|----------|-----------|  
|1.|전체 손가락 Gloves|의류|  
|1.|전체 손가락 Gloves|도|  
|1.|전체 손가락 Gloves|touring|  
|1.|전체 손가락 Gloves|자전거|  
|2|LL 헤드셋|자전거|  
|3|HL Mountain Frame|자전거|  
|3|HL Mountain Frame|mountain|  
  
### <a name="c-aggregation-by-values"></a>3. 값으로 집계  
 사용자가 제품을 2 개 이상 제품과 함께 태그만 필터링 하 고, 제품의 수로 정렬 된 각 태그의 수를 보여 주는 보고서를 만들어야 합니다.  
  
```  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```  
  
### <a name="d-search-by-tag-value"></a>4. 태그 값으로 검색  
 개발자는 키워드로 항목을 찾는 쿼리를 만들어야 합니다. 다음 쿼리를 사용할 수 있습니다.  
  
 단일 태그 (의류)와 제품을 찾으려면:  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```  
  
 지정 된 두 개의 태그 (clothing 및 road)와 높은 제품 검색:  
  
```  
  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>5. 값 목록으로 행을 찾습니다.  
 개발자가 id 목록에서 문서를 찾는 쿼리를 만들어야 합니다. 다음 쿼리를 사용할 수 있습니다.  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
 이 응용 프로그램 계층에는 동적 SQL 문자열 만들기와 같은 일반적인 안티패턴 대체 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)], 또는 LIKE 연산자를 사용 하 여:  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [부분 문자열 &#40; Transact SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
  
  

