---
title: STRING_AGG(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- STRING_AGG
- STRING_AGG_TSQL
helpviewer_keywords:
- STRING_AGG function
ms.assetid: 8860ef3f-142f-4cca-aa64-87a123e91206
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1d7ef8b52e3ee31e688e51454a72c0f359bcb68b
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68632130"
---
# <a name="string_agg-transact-sql"></a>STRING_AGG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-asdw-xxx-md.md)]

문자열 식의 값을 연결하고 그 사이에 구분 기호 값을 추가합니다. 구분 기호는 문자열 끝에 추가되지 않습니다.
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
STRING_AGG ( expression, separator ) [ <order_clause> ]

<order_clause> ::=   
    WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )   
```

## <a name="arguments"></a>인수

*expression*  
모든 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 식은 연결 중 `NVARCHAR` 또는 `VARCHAR` 형식으로 변환됩니다. 문자열이 아닌 형식은 `NVARCHAR` 형식으로 변환됩니다.

*separator*  
연결된 문자열의 구분 기호로 사용되는 [ 또는 ](../../t-sql/language-elements/expressions-transact-sql.md) 형식의 `NVARCHAR`식`VARCHAR`입니다. 리터럴 또는 변수일 수 있습니다. 

<order_clause>   
또는 `WITHIN GROUP` 절을 사용하여 연결된 결과의 순서를 지정합니다.

```
WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )
```   
<order_by_expression_list>   
 
  결과 정렬에 사용할 수 있는 비상수 [식](../../t-sql/language-elements/expressions-transact-sql.md)의 목록입니다. `order_by_expression`은 하나만 허용됩니다. 기본 정렬 순서는 오름차순입니다.   
  
## <a name="return-types"></a>반환 형식

반환 형식은 첫 번째 인수(식)에 따라 다릅니다. 입력 인수가 문자열 형식(`NVARCHAR`, `VARCHAR`)인 경우 결과 형식은 입력 형식과 동일합니다. 다음 표에 자동 변환이 나열되어 있습니다.  

|입력 식 형식 |결과 | 
|-------|-------|
|NVARCHAR(MAX) |NVARCHAR(MAX) |
|VARCHAR(MAX) |VARCHAR(MAX) |
|NVARCHAR(1...4000) |NVARCHAR(4000) |
|VARCHAR(1...8000) |VARCHAR(8000) |
|int, bigint, smallint, tinyint, numeric, float, real, bit, decimal, smallmoney, money, datetime, datetime2, |NVARCHAR(4000) |

## <a name="remarks"></a>Remarks

`STRING_AGG`는 행의 모든 식을 하나의 문자열로 연결하는 집계 함수입니다. 식 값은 문자열 형식으로 암시적으로 변환된 다음, 연결됩니다. 문자열에 대한 암시적 변환은 데이터 형식 변환에 대한 기존 규칙을 따릅니다. 데이터 형식 변환에 대한 자세한 내용은 [CAST 및 CONVERT(Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하십시오. 

입력 식이 `VARCHAR` 형식인 경우 구분 기호의 형식은 `NVARCHAR`가 될 수 없습니다. 

Null 값이 무시되고 해당 구분 기호는 추가되지 않습니다. null 값의 자리 표시자를 반환하려면 예제 B와 같이 `ISNULL` 함수를 사용하세요.

`STRING_AGG`는 모든 호환성 수준에서 사용할 수 있습니다.

## <a name="examples"></a>예

### <a name="a-generate-list-of-names-separated-in-new-lines"></a>1\. 새 줄에 구분된 이름 목록 생성

다음 예에서는 단일 결과 셀에서 캐리지 리턴으로 구분된 이름 목록을 만듭니다.
```sql
SELECT STRING_AGG (FirstName, CHAR(13)) AS csv 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Syed <br />Catherine <br />Kim <br />Kim <br />Kim <br />Hazem <br />... | 

`name` 셀에 있는 `NULL` 값은 결과에 반환되지 않습니다.   

> [!NOTE]  
>  Management Studio Query Editor를 사용하는 경우 **표 형태로 결과 표시** 옵션으로 캐리지 리턴을 구현할 수 없습니다. 결과 집합을 올바르게 보려면 **텍스트로 결과 표시**로 전환하세요.   

### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>2\. NULL 값 없이 쉼표로 구분된 이름 목록 생성

다음 예는 null 값을 '해당 없음'으로 대체하고 하나의 결과 셀에 쉼표로 구분된 이름을 반환합니다.  
```sql
SELECT STRING_AGG ( ISNULL(FirstName,'N/A'), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Csv | 
|--- |
|John,N/A,Mike,Peter,N/A,N/A,Alice,Bob |  

### <a name="c-generate-comma-separated-values"></a>C. 쉼표로 구분된 값 생성

```sql
SELECT 
STRING_AGG(CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')'), CHAR(13)) 
  AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|이름 |
|--- |
|Ken Sánchez (Feb  8 2003 12:00AM) <br />Terri Duffy (Feb 24 2002 12:00AM) <br />Roberto Tamburello (Dec  5 2001 12:00AM) <br />Rob Walters (Dec 29 2001 12:00AM) <br />... |

> [!NOTE]  
> Management Studio Query Editor를 사용하는 경우 **표 형태로 결과 표시** 옵션으로 캐리지 리턴을 구현할 수 없습니다. 결과 집합을 올바르게 보려면 **텍스트로 결과 표시**로 전환하세요.

### <a name="d-return-news-articles-with-related-tags"></a>D. 뉴스 기사 및 관련 태그 반환

기사와 태그가 다른 테이블로 구분됩니다. 개발자들은 각 기사당 관련 태그가 모두 포함된 하나의 행을 반환하려고 합니다. 다음 쿼리를 사용합니다.

```sql
SELECT a.articleId, title, STRING_AGG (tag, ',') as tags
FROM dbo.Article AS a
LEFT JOIN dbo.ArticleTag AS t
    ON a.ArticleId = t.ArticleId
GROUP BY a.articleId, title;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|articleId |title |tags |
|--- |--- |--- |
|172 |Polls indicate close election results |politics,polls,city council |
|176 |New highway expected to reduce congestion |NULL |
|177 |Dogs continue to be more popular than cats |polls,animals|

> [!NOTE]
> `STRING_AGG` 함수가 `SELECT` 목록의 유일한 항목이 아닌 경우 `GROUP BY` 절이 필요합니다.

### <a name="e-generate-list-of-emails-per-towns"></a>E. 도시별 이메일 목록 생성

다음 쿼리는 직원의 이메일 주소를 찾고 도시별로 그룹화합니다.

```sql
SELECT town, STRING_AGG (email, ';') AS emails 
FROM dbo.Employee 
GROUP BY town; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|도시 |이메일 |
|--- |--- |
|Seattle |syed0@adventure-works.com;catherine0@adventure-works.com;kim2@adventure-works.com |
|LA |sam1@adventure-works.com;hazem0@adventure-works.com |

이메일 열에 반환된 이메일은 특정 도시에서 근무하는 사람들에게 이메일을 전송하는 데 직접 사용할 수 있습니다. 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>F. 도시별 이메일 정렬 목록 생성   
다음 쿼리는 이전 예와 유사한 방식으로 직원의 이메일 주소를 찾고 도시별로 그룹화한 다음, 이메일을 사전순으로 정렬합니다.   
```sql
SELECT town, 
    STRING_AGG (email, ';') WITHIN GROUP (ORDER BY email ASC) AS emails 
FROM dbo.Employee 
GROUP BY town; 
```
   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|도시 |이메일 |
|--- |--- |
|Seattle |catherine0@adventure-works.com;kim2@adventure-works.com;syed0@adventure-works.com |
|LA |hazem0@adventure-works.com;sam1@adventure-works.com |

## <a name="see-also"></a>관련 항목:
 
 [CONCAT&#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS&#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME&#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE&#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE&#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_ESCAPE&#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF&#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE&#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [집계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  

