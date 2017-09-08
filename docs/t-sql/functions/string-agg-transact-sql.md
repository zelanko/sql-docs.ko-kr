---
title: STRING_AGG (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- STRING_AGG
- STRING_AGG_TSQL
helpviewer_keywords:
- STRING_AGG function
ms.assetid: 8860ef3f-142f-4cca-aa64-87a123e91206
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bf74698e9e61f456726b1e6a62126a8d78a09777
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stringagg-transact-sql"></a>STRING_AGG (Transact SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

문자열 식의 값을 연결 하 고 서로 구분 기호 값을 배치 합니다. 구분 기호 문자열의 끝에 추가 되지 않습니다.
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
STRING_AGG ( expression, separator ) [ <order_clause> ]

<order_clause> ::=   
    WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )   
```

## <a name="arguments"></a>인수 

*구분 기호*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 의 `NVARCHAR` 또는 `VARCHAR` 에 대 한 구분 기호로 사용 되는 형식 문자열을 연결 합니다. 리터럴 또는 변수 수 있습니다. 

*expression*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 모든 종류의 합니다. 식으로 변환 됩니다 `NVARCHAR` 또는 `VARCHAR` 연결 하는 동안 형식입니다. 문자열이 아닌 유형으로 변환 됩니다 `NVARCHAR` 유형입니다.


< order_clause >   
필요에 따라 사용 하 여 연결 된 결과의 순서를 지정할 `WITHIN GROUP` 절:
```
WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )
```   
< order_by_expression_list >   
 
  비상수 목록이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 결과 정렬에 사용할 수 있는 합니다. 하나의 `order_by_expression` 쿼리당 허용 됩니다. 기본 정렬 순서는 오름차순입니다.   
  

## <a name="return-types"></a>반환 형식 

반환 형식이 첫 번째 인수 (식)에 따라 달라 집니다. 입력된 인수에 문자열 형식인 경우 (`NVARCHAR`, `VARCHAR`), 결과 형식은 입력된 종류와 같게 됩니다. 다음 표에서 자동 변환을 보여 줍니다.  

|입력된 식 형식 |결과 | 
|-------|-------|
|NVARCHAR(MAX) |NVARCHAR(MAX) |
|VARCHAR(MAX) |VARCHAR(MAX) |
|NVARCHAR (1... 4000) |NVARCHAR (4000) |
|VARCHAR (1... 8000) |VARCHAR(8000) |
|int, bigint, smallint, tinyint, 숫자, float, real, 비트, decimal, smallmoney, money, datetime, datetime2, |NVARCHAR (4000) |


## <a name="remarks"></a>주의  
 
`STRING_AGG`집계 행에서 모든 식을 사용 하 고 단일 문자열로 연결 합니다. 식 값 문자열 형식으로 암시적으로 변환 되 고 연결 됩니다. 문자열에 대한 암시적 변환은 데이터 형식 변환에 대한 기존 규칙을 따릅니다. 데이터 형식 변환에 대 한 자세한 내용은 참조 [CAST 및 CONVERT (TRANSACT-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)합니다. 

입력된 식이 형식인 경우 `VARCHAR`, 구분 기호는 형식일 수 없습니다. `NVARCHAR`합니다. 

Null 값은 무시 되 고 해당 구분 기호가 추가 되지 않습니다. Null 값에 대 한 자리 표시자를 반환 하려면 사용 하 여는 `ISNULL` 2. 예제에서와 같이 작동 합니다.

`STRING_AGG`모든 호환성 수준에 나타납니다.


## <a name="examples"></a>예 

### <a name="a-generate-list-of-names-separated-in-new-lines"></a>1. 새 줄에 구분 된 목록이 생성 
다음 예제에서는 캐리지 리턴으로 구분 된 단일 결과 셀에 대 한 이름 목록을 생성 합니다.
```tsql
SELECT STRING_AGG (FirstName, CHAR(13)) AS csv 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Syed <br />Catherine <br />Kim <br />Kim <br />Kim <br />Hazem <br />... | 

`NULL`값을 찾을 수 `name` 셀 결과에 반환 되지 않습니다.   
> [!NOTE]  
>  Management Studio 쿼리 편집기를 사용 하는 경우는 **표 형태로 결과** 옵션에는 캐리지 리턴 구현할 수 없습니다. 로 전환 **텍스트로 결과 표시** 결과를 보려면 제대로 설정 해야 합니다.   


### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>2. NULL 값이 없는 쉼표로 구분 된 목록이 생성   
다음 예제에서는 해당 '없음'으로 null 값을 대체 하 고 단일 결과 셀에는 쉼표로 구분 하 여 이름을 반환 합니다.  
```tsql
SELECT STRING_AGG ( ISNULL(FirstName,'N/A'), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
 

|Csv | 
|--- |
|John, n/A, Mike, Peter, n/A, n/A, Alice, Bob |  


### <a name="c-generate-comma-separated-values"></a>3. 쉼표로 구분 된 값을 생성 합니다. 

```tsql   
SELECT 
STRING_AGG(CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')'), CHAR(13)) 
  AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|이름 | 
|--- |
|박 단은 Sánchez (2 월 8 2003 오전 12시) <br />Terri Duffy (2002 년 2 월 24 일 오전 12시) <br />Roberto Tamburello (5 2001 12 오전 12시) <br />Rob 받는 (29 2001 12 오전 12시) <br />... |

> [!NOTE]  
>  Management Studio 쿼리 편집기를 사용 하는 경우는 **표 형태로 결과** 옵션에는 캐리지 리턴 구현할 수 없습니다. 로 전환 **텍스트로 결과 표시** 결과를 보려면 제대로 설정 해야 합니다.   
 

### <a name="d-return-news-articles-with-related-tags"></a>4. 관련된 태그 데이터에 대 한 뉴스 기사를 반환 합니다. 

문서 및 태그 여러 테이블로 구분 됩니다. 개발자는 태그와 모두 연결 된 각 아티클에 당 한 개의 행을 반환 하려고 합니다. 다음 쿼리를 사용 하 여: 
```tsql
SELECT a.articleId, title, STRING_AGG (tag, ',') as tags 
FROM dbo.Article AS a       
LEFT JOIN dbo.ArticleTag AS t 
    ON a.ArticleId = t.ArticleId 
GROUP BY a.articleId, title;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|articleId |title |tags |
|--- |--- |--- |
|172 |여론 조사 닫기 선택 결과 나타냅니다. |정치, 여론 조사, 도시 council | 
|176 |새 고속도로 정체를 줄이기 위해 필요 합니다. |NULL |
|177 |Dogs 계속 cats 보다 더 인기가 수 |여론 조사, 동물| 

### <a name="e-generate-list-of-emails-per-towns"></a>5. 도심지 당 전자 메일 주소 목록을 생성 합니다.

다음 쿼리는 직원의 전자 메일 주소를 찾아서 도심지 별로 그룹화 합니다. 
```tsql
SELECT town, STRING_AGG (email, ';') AS emails 
FROM dbo.Employee 
GROUP BY town; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|동 |전자 메일 |
|--- |--- |
|Seattle |syed0@adventure-works.com;catherine0@adventure-works.com;kim2@adventure-works.com |
|LA |sam1@adventure-works.com;hazem0@adventure-works.com |

일부 특정 도시에 사용 하는 사용자의 그룹에 메일을 보냅니다 열을 직접 사용할 수는 전자 메일에서 전자 메일 반환 합니다. 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>6. 도심지 당 전자 메일의 정렬 된 목록을 생성합니다   
   
이전 예제와 마찬가지로 다음 쿼리 직원의 전자 메일 주소, 도시에 별로 그룹화 찾아서 전자 메일을 사전순으로 정렬 합니다.   
```tsql
SELECT town, 
    STRING_AGG (email, ';') WITHIN GROUP (ORDER BY email ASC) AS emails 
FROM dbo.Employee 
GROUP BY town; 
```
   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|동 |전자 메일 |
|--- |--- |
|Seattle |catherine0@adventure-works.com;kim2@adventure-works.com;syed0@adventure-works.com |
|LA |hazem0@adventure-works.com;sam1@adventure-works.com |


## <a name="see-also"></a>관련 항목:  

[문자열 함수 (Transact SQL)](../../t-sql/functions/string-functions-transact-sql.md)  


