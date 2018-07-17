---
title: 검색 조건(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6ffe7a15fdaa81492cf0b993ba10a1ca555c6625
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36249245"
---
# <a name="search-condition-transact-sql"></a>검색 조건(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
 \<search_condition>  
 SELECT 문, 쿼리 식 또는 하위 쿼리에 대해 결과 집합에 반환되는 행의 조건을 지정합니다. UPDATE 문에는 업데이트할 행을 지정합니다. DELETE 문에는 삭제할 행을 지정합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 검색 조건에 포함할 수 있는 조건자의 개수에는 제한이 없습니다.  
  
 NOT  
 조건자에서 지정한 부울 식을 부정합니다. 자세한 내용은 [NOT&#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)을 참조하세요.  
  
 AND  
 두 조건이 TRUE일 때 두 조건을 결합하여 TRUE로 평가합니다. 자세한 내용은 [AND&#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md)를 참조하세요.  
  
 또는  
 두 조건 중 하나가 TRUE일 때 두 조건을 결합하여 TRUE로 평가합니다. 자세한 내용은 [OR&#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md)을 참조하세요.  
  
 \< predicate >  
 TRUE, FALSE 또는 UNKNOWN을 반환하는 식입니다.  
  
 *expression*  
 열 이름, 상수, 함수, 변수, 스칼라 하위 쿼리이거나 열 이름, 상수 및 연산자나 하위 쿼리로 연결된 함수의 결합입니다. 식에는 CASE 식도 포함될 수 있습니다.  
  
> [!NOTE]  
>  유니코드가 아닌 문자열 상수 및 변수는 데이터베이스의 기본 데이터 정렬에 해당하는 코드 페이지를 사용합니다. 코드 페이지 변환은 유니코드가 아닌 문자 데이터를 사용하고 유니코드가 아닌 **char**, **varchar** 및 **text** 문자 데이터 형식을 참조할 때 발생할 수 있습니다. 코드 페이지가 데이터베이스의 기본 데이터 정렬에 해당 하는 코드 페이지와 다른 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 유니코드가 아닌 문자열 상수와 변수를 참조된 열 또는 COLLATE를 사용하여 지정된 열의 데이터 정렬에 해당하는 코드 페이지로 변환합니다. [가장 적합한 매핑](http://www.unicode.org/Public/MAPPINGS/VENDORS/MICSFT/WindowsBestFit/)을 찾을 수 있으면 새 코드 페이지에서 찾을 수 없는 문자는 비슷한 문자로 변환됩니다. 그렇지 않으면 기본 대체 문자("?")로 변환됩니다.  
>  
> 여러 코드 페이지로 사용하는 경우 문자 상수 앞에 대문자 'N'을 붙일 수 있으며, 유니코드 변수를 사용하여 코드 페이지 변환을 방지할 수 있습니다.  
  
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
 다음에 나오는 문자열이 패턴 일치로 사용됨을 나타냅니다. 자세한 내용은 [LIKE&#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)를 참조하세요.  
  
 ESCAPE **'***escape_ character***'**  
 와일드카드 문자의 기능을 하지 않고 문자열에서 와일드카드 문자를 검색할 수 있도록 합니다. *escape_character*는 특별한 용도를 나타내기 위해 와일드카드 문자 앞에 놓이는 문자입니다.  
  
 [ NOT ] BETWEEN  
 값의 포함 범위를 지정합니다. AND를 사용하여 시작 값과 끝 값을 구분합니다. 자세한 내용은 [BETWEEN&#40;Transact-SQL&#41;](../../t-sql/language-elements/between-transact-sql.md)을 참조하세요.  
  
 IS [ NOT ] NULL  
 사용된 키워드에 따라 Null 값 또는 Null이 아닌 값이 검색되도록 지정합니다. 피연산자에 NULL이 있는 경우에 비트 연산자 또는 산술 연산자를 사용하는 식은 NULL로 평가됩니다.  
  
 CONTAINS  
 문자 기반 데이터가 포함된 열에서 단일 단어와 구, 특정 거리에 있는 단어의 근접성 및 가중치 일치 항목과 정확한 일치하거나 비슷하게 일치(*유사 일치*)하는 열을 검색합니다. 이 옵션은 SELECT 문에서만 사용할 수 있습니다. 자세한 내용은 [CONTAINS&#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)를 참조하세요.  
  
 FREETEXT  
 문자 기반 데이터가 포함된 열에서 조건자에 있는 정확한 단어 대신 의미가 일치하는 값을 검색함으로써 단순한 형태의 자연어 쿼리를 제공합니다. 이 옵션은 SELECT 문에서만 사용할 수 있습니다. 자세한 내용은 [FREETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)를 참조하세요.  
  
 [ NOT ] IN  
 식이 목록에 포함되는지 또는 제외되는지 여부에 따라 식을 검색하도록 지정합니다. 검색 식은 상수 또는 열 이름이 될 수 있으며 목록은 상수 집합 또는 더 일반적으로는 하위 쿼리가 될 수 있습니다. 값의 목록은 괄호로 묶어야 합니다. 자세한 내용은 [IN&#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)을 참조하세요.  
  
 *subquery*  
 제한된 SELECT 문으로 간주할 수 있고, SELECT 문에서 \<query_expresssion>과 비슷합니다. ORDER BY 절 및 INTO 키워드는 허용되지 않습니다. 자세한 내용은 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)를 참조하세요.  
  
 ALL  
 비교 연산자 및 하위 쿼리와 함께 사용됩니다. 하위 쿼리에 대해 검색된 모든 값이 비교 연산을 충족하면 \<predicate>에 대해 TRUE를 반환하고, 모든 값이 비교 연산을 충족하지 않거나 하위 쿼리에서 외부 문에 행을 반환하지 않으면 FALSE를 반환합니다. 자세한 내용은 [ALL&#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)을 참조하세요.  
  
 { SOME | ANY }  
 비교 연산자 및 하위 쿼리와 함께 사용됩니다. 하위 쿼리에 대해 검색된 값이 비교 연산을 충족하면 \<predicate>에 대해 TRUE를 반환하고, 하위 쿼리의 값이 비교 연산을 충족하지 않거나 하위 쿼리에서 외부 문에 행을 반환하지 않으면 FALSE를 반환합니다. 그렇지 않을 경우에 식은 UNKNOWN입니다. 자세한 내용은 [SOME &#124; ANY&#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)를 참조하세요.  
  
 EXISTS  
 하위 쿼리와 함께 사용되어 하위 쿼리에서 반환한 행의 존재 여부를 검사합니다. 자세한 내용은 [EXISTS&#40;Transact-SQL&#41;](../../t-sql/language-elements/exists-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 논리 연산자의 우선 순위는 NOT(가장 높음), AND, OR 순입니다. 검색 조건에 괄호를 사용하면 이 순서를 무시할 수 있습니다. 논리 연산자의 계산 순서는 쿼리 최적화 프로그램에서 선택한 내용에 따라 달라질 수 있습니다. 논리 연산자에서 논리 값을 조작하는 방법에 대한 자세한 내용은 [AND&#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md), [OR&#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md) 및 [NOT&#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-where-with-like-and-escape-syntax"></a>1. WHERE 절에 LIKE 및 ESCAPE 구문 사용  
 다음 예제에서는 `LargePhotoFileName` 열에 `green_` 문자가 있는 행을 검색하고, _이 와일드카드 문자이므로 `ESCAPE` 옵션을 사용합니다. `ESCAPE` 옵션을 지정하지 않으면 쿼리에서 `green` 단어 뒤에 _ 문자가 아닌 임의의 단일 문자가 포함된 설명 값을 검색합니다.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-where-with-like"></a>3. LIKE가 포함된 WHERE 사용  
 다음 예제에서는 `LastName` 열에 `and` 문자가 있는 행을 검색합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE '%and%';  
```  
  
### <a name="d-using-where-and-like-syntax-with-unicode-data"></a>4. WHERE 및 LIKE 구문에 유니코드 데이터 사용  
 다음 예제에서는 `WHERE` 절을 사용하여 `LastName` 열에서 유니코드 검색을 수행합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE N'%and%';  
```  
  
## <a name="see-also"></a>참고 항목  
 [집계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [커서&#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FREETEXTTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  

