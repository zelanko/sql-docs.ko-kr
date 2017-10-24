---
title: "검색 조건 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- search
- Search Condition
- condition
dev_langs:
- TSQL
helpviewer_keywords:
- OR operator [Transact-SQL]
- CONTAINS predicate (Transact-SQL)
- ESCAPE keyword
- operators [Transact-SQL], search condition
- search conditions [SQL Server]
- WHERE clause, search conditions
- ALL keyword
- FREETEXT predicate (Transact-SQL)
- EXISTS keyword
- search conditions [SQL Server], about search conditions
- NOT operator [Transact-SQL]
- BETWEEN operator
- SOME | ANY keyword
- predicates [full-text search]
- AND, about search conditions
- logical operators [SQL Server], about search conditions
- precedence [SQL Server], logical operators
- logical operators [SQL Server], precedence
- LIKE comparisons
ms.assetid: 09974469-c5d2-4be8-bc5a-78e404660b2c
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: ad0a32f2f11c7b0ca781c7e01635204da38fcbdd
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="search-condition-transact-sql"></a>검색 조건(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  검색 조건은 논리 연산자 AND, OR 및 NOT을 사용하여 하나 이상의 조건자를 결합한 것입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
<search_condition> ::=   
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | ! > | < | < = | ! < } expression   
    | string_expression [ NOT ] LIKE string_expression   
  [ ESCAPE 'escape_character' ]   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | CONTAINS   
  ( { column | * } , '<contains_search_condition>' )   
    | FREETEXT ( { column | * } , 'freetext_string' )   
    | expression [ NOT ] IN ( subquery | expression [ ,...n ] )   
    | expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
  { ALL | SOME | ANY} ( subquery )   
    | EXISTS ( subquery )     }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
< search_condition > ::=   
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | < | < = } expression   
    | string_expression [ NOT ] LIKE string_expression   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | expression [ NOT ] IN (subquery | expression [ ,...n ] )   
    | expression [ NOT ] EXISTS (subquery)     }   
```  
  
## <a name="arguments"></a>인수  
 \<c h _ c >  
 SELECT 문, 쿼리 식 또는 하위 쿼리에 대해 결과 집합에 반환되는 행의 조건을 지정합니다. UPDATE 문에는 업데이트할 행을 지정합니다. DELETE 문에는 삭제할 행을 지정합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 검색 조건에 포함할 수 있는 조건자의 개수에는 제한이 없습니다.  
  
 NOT  
 조건자에서 지정한 부울 식을 부정합니다. 자세한 내용은 참조 [하지 &#40; Transact SQL &#41; ](../../t-sql/language-elements/not-transact-sql.md).  
  
 및  
 두 조건이 TRUE일 때 두 조건을 결합하여 TRUE로 평가합니다. 자세한 내용은 참조 [AND &#40; Transact SQL &#41; ](../../t-sql/language-elements/and-transact-sql.md).  
  
 또는  
 두 조건 중 하나가 TRUE일 때 두 조건을 결합하여 TRUE로 평가합니다. 자세한 내용은 참조 [또는 &#40; Transact SQL &#41; ](../../t-sql/language-elements/or-transact-sql.md).  
  
 \<조건자 >  
 TRUE, FALSE 또는 UNKNOWN을 반환하는 식입니다.  
  
 *expression*  
 열 이름, 상수, 함수, 변수, 스칼라 하위 쿼리이거나 열 이름, 상수 및 연산자나 하위 쿼리로 연결된 함수의 결합입니다. 식에는 CASE 식도 포함될 수 있습니다.  
  
> [!NOTE]  
>  유니코드 문자 데이터 형식을 참조할 때는 **nchar**, **nvarchar**, 및 **ntext**, 'expression' 대문자 접두사로 추가 해야 ' N '입니다. 'N'을 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 또는 열의 기본 데이터 정렬에 해당하는 코드 페이지로 문자열을 변환합니다. 이 코드 페이지에 없는 문자는 모두 손실됩니다.  
  
 =  
 두 식이 같은지 여부를 검사하는 데 사용되는 연산자입니다.  
  
 <>  
 두 식이 서로 같지 않은지 조건을 검사하는 데 사용되는 연산자입니다.  
  
 !=  
 두 식이 서로 같지 않은지 조건을 검사하는 데 사용되는 연산자입니다.  
  
 \>  
 두 식 중 한 식이 다른 식보다 큰지 조건을 검사하는 데 사용되는 연산자입니다.  
  
 \>=  
 두 식 중 한 식이 다른 식보다 크거나 같은지 조건을 검사하는 데 사용되는 연산자입니다.  
  
 !>  
 두 식 중 한 식이 다른 식보다 크지 않은지 조건을 검사하는 데 사용되는 연산자입니다.  
  
 <  
 두 식 중 한 식이 다른 식보다 작은지 조건을 검사하는 데 사용되는 연산자입니다.  
  
 <=  
 두 식 중 한 식이 다른 식보다 작거나 같은지 조건을 검사하는 데 사용되는 연산자입니다.  
  
 !<  
 두 식 중 한 식이 다른 식보다 작지 않은지 조건을 검사하는 데 사용되는 연산자입니다.  
  
 *string_expression*  
 문자열과 와일드카드 문자입니다.  
  
 [ NOT ] LIKE  
 다음에 나오는 문자열이 패턴 일치로 사용됨을 나타냅니다. 자세한 내용은 참조 [같은 &#40; Transact SQL &#41; ](../../t-sql/language-elements/like-transact-sql.md).  
  
 이스케이프 **'***escape_ 문자***'**  
 와일드카드 문자의 기능을 하지 않고 문자열에서 와일드카드 문자를 검색할 수 있도록 합니다. *escape_character* 이 특별 한 용도로 사용을 나타내려면 와일드 카드 문자 앞에 배치 된 문자입니다.  
  
 [ NOT ] BETWEEN  
 값의 포함 범위를 지정합니다. AND를 사용하여 시작 값과 끝 값을 구분합니다. 자세한 내용은 참조 [BETWEEN &#40; Transact SQL &#41; ](../../t-sql/language-elements/between-transact-sql.md).  
  
 IS [NOT] NULL  
 사용된 키워드에 따라 Null 값 또는 Null이 아닌 값이 검색되도록 지정합니다. 피연산자에 NULL이 있는 경우에 비트 연산자 또는 산술 연산자를 사용하는 식은 NULL로 평가됩니다.  
  
 CONTAINS  
 검색 하거나에 대 한 문자 기반 데이터를 포함 하는 열 (*유사 항목*) 검색, 및가 중된 일치 하는 항목의 특정 단어나 구와 근접 한 단어를 찾습니다. 이 옵션은 SELECT 문에서만 사용할 수 있습니다. 자세한 내용은 참조 [contains&#40; Transact SQL &#41; ](../../t-sql/queries/contains-transact-sql.md).  
  
 FREETEXT  
 문자 기반 데이터가 포함된 열에서 조건자에 있는 정확한 단어 대신 의미가 일치하는 값을 검색함으로써 단순한 형태의 자연어 쿼리를 제공합니다. 이 옵션은 SELECT 문에서만 사용할 수 있습니다. 자세한 내용은 참조 [FREETEXT &#40; Transact SQL &#41; ](../../t-sql/queries/freetext-transact-sql.md).  
  
 [ NOT ] IN  
 식이 목록에 포함되는지 또는 제외되는지 여부에 따라 식을 검색하도록 지정합니다. 검색 식은 상수 또는 열 이름이 될 수 있으며 목록은 상수 집합 또는 더 일반적으로는 하위 쿼리가 될 수 있습니다. 값의 목록은 괄호로 묶어야 합니다. 자세한 내용은 참조 [&#40; Transact SQL &#41; ](../../t-sql/language-elements/in-transact-sql.md).  
  
 *하위 쿼리*  
 제한 된 SELECT 문이 간주할 수 있으며 비슷합니다 \<query_expresssion > SELECT 문의 합니다. ORDER BY 절 및 INTO 키워드는 허용되지 않습니다. 자세한 내용은 참조 [select&#40; Transact SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
 ALL  
 비교 연산자 및 하위 쿼리와 함께 사용됩니다. 에 대 한 TRUE를 반환 \<조건자 > 하위에 대 한 검색 된 모든 값을 비교 연산을 만족 하는 경우 또는 비교 또는 하위 쿼리에서 외부 문에 행을 반환 하는 경우를 충족 하는 경우 모든 값 FALSE입니다. 자세한 내용은 참조 [모든 &#40; Transact SQL &#41; ](../../t-sql/language-elements/all-transact-sql.md).  
  
 { SOME | ANY }  
 비교 연산자 및 하위 쿼리와 함께 사용됩니다. 에 대 한 TRUE를 반환 \<조건자 > 하위 쿼리에서 비교 연산을 만족 하거나 하위 쿼리에서 값이 없는 경우 FALSE 만족 비교 또는 하위 쿼리에서 외부 문에 행을 반환 하는 경우에 대 한 모든 값을 검색 하는 경우. 그렇지 않을 경우에 식은 UNKNOWN입니다. 자세한 내용은 참조 [일부 &#124; 모든 &#40; Transact SQL &#41; ](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 EXISTS  
 하위 쿼리와 함께 사용되어 하위 쿼리에서 반환한 행의 존재 여부를 검사합니다. 자세한 내용은 참조 [EXISTS &#40; Transact SQL &#41; ](../../t-sql/language-elements/exists-transact-sql.md).  
  
## <a name="remarks"></a>주의  
 논리 연산자의 우선 순위는 NOT(가장 높음), AND, OR 순입니다. 검색 조건에 괄호를 사용하면 이 순서를 무시할 수 있습니다. 논리 연산자의 계산 순서는 쿼리 최적화 프로그램에서 선택한 내용에 따라 달라질 수 있습니다. 논리 연산자 논리 값에 작동 하는 방법에 대 한 자세한 내용은 참조 [AND &#40; Transact SQL &#41; ](../../t-sql/language-elements/and-transact-sql.md), [또는 &#40; Transact SQL &#41; ](../../t-sql/language-elements/or-transact-sql.md), 및 [하지 &#40; Transact SQL &#41; ](../../t-sql/language-elements/not-transact-sql.md).  
  
## <a name="examples"></a>예  
  
### <a name="a-using-where-with-like-and-escape-syntax"></a>1. WHERE 절에 LIKE 및 ESCAPE 구문 사용  
 다음 예에서는 있는 행에 대 한 검색는 `LargePhotoFileName` 열에는 문자 `green_`를 사용 하 여는 `ESCAPE` _ 와일드 카드 문자 이므로 옵션입니다. 지정 하지 않고는 `ESCAPE` 옵션을 포함 하는 모든 설명 값에 대 한 쿼리를 검색 합니다 `green` _ 문자 이외의 모든 단일 문자입니다.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT *   
FROM Production.ProductPhoto  
WHERE LargePhotoFileName LIKE '%greena_%' ESCAPE 'a' ;  
```  
  
### <a name="b-using-where-and-like-syntax-with-unicode-data"></a>2. WHERE 및 LIKE 구문에 유니코드 데이터 사용  
 다음 예에서는 `WHERE` 절을 사용하여 미국(`US`) 이외의 국가에서 `Pa`으로 시작하는 시에 있는 모든 기업의 우편 주소를 검색합니다.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT AddressLine1, AddressLine2, City, PostalCode, CountryRegionCode    
FROM Person.Address AS a  
JOIN Person.StateProvince AS s ON a.StateProvinceID = s.StateProvinceID  
WHERE CountryRegionCode NOT IN ('US')  
AND City LIKE N'Pa%' ;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-where-with-like"></a>3. 사용 하 여 위치를 사용 하 여  
 다음 예에서는 있는 행에 대 한 검색은 `LastName` 열에는 문자 `and`합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE '%and%';  
```  
  
### <a name="d-using-where-and-like-syntax-with-unicode-data"></a>4. WHERE 및 LIKE 구문에 유니코드 데이터 사용  
 다음 예제에서는 `WHERE` 절에서 유니코드 검색을 수행 하는 `LastName` 열입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE N'%and%';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [집계 함수 &#40; Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [대/소문자 &#40; Transact SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [커서&#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FREETEXTTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  


