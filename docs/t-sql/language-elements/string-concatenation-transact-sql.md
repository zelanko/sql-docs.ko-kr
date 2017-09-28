---
title: "+ (문자열 연결) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- concatenation
- +
- string
dev_langs:
- TSQL
helpviewer_keywords:
- concatenation [SQL Server]
- string concatenation operators
- + (string concatenation)
ms.assetid: 35cb3d7a-48f5-4b13-926c-a9d369e20ed7
caps.latest.revision: 51
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 66f482d424c6be56d89e8ec5b99cff30b2ddab0b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="-string-concatenation-transact-sql"></a>+(문자열 연결)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 개 이상의 문자 또는 이진 문자열, 열 또는 문자열 및 열 이름의 조합을 하나의 식(문자열 연산자)으로 연결하는 문자열 식의 연산자입니다.  예를 들어 `SELECT 'book'+'case';` 반환 `bookcase`합니다.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression + expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md) 의 유형 중 하나는 데이터 문자 및 이진 데이터 형식 범주를 제외 하 고는 **이미지**, **ntext**, 또는 **텍스트**데이터 형식입니다. 두 식이 모두 동일한 데이터 형식으로 되어 있거나 식 하나가 암시적으로 다른 식의 데이터 형식으로 변환될 수 있어야 합니다.  
  
 이진 문자열 사이에 문자가 있는 형태의 연결에서는 문자 데이터로의 명시적 변환이 필요합니다. 다음 예제에서는 때 `CONVERT`, 또는 `CAST`, 이진 연결에 사용 해야 합니다 및 시기 `CONVERT`, 또는 `CAST`, 사용할 필요는 없습니다.  
  
```  
DECLARE @mybin1 varbinary(5), @mybin2 varbinary(5)  
SET @mybin1 = 0xFF  
SET @mybin2 = 0xA5  
-- No CONVERT or CAST function is required because this example   
-- concatenates two binary strings.  
SELECT @mybin1 + @mybin2  
-- A CONVERT or CAST function is required because this example  
-- concatenates two binary strings plus a space.  
SELECT CONVERT(varchar(5), @mybin1) + ' '   
   + CONVERT(varchar(5), @mybin2)  
-- Here is the same conversion using CAST.  
SELECT CAST(@mybin1 AS varchar(5)) + ' '   
   + CAST(@mybin2 AS varchar(5))  
  
```  
  
## <a name="result-types"></a>결과 형식  
 결과는 우선 순위가 가장 높은 인수의 데이터 형식으로 반환됩니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>주의  
 + (문자열 연결) 연산자는 비어 있는 문자열, 즉 길이가 0인 문자열을 다룰 때와 NULL 또는 알 수 없는 값을 다룰 때 다르게 동작합니다. 길이가 0인 문자열은 문자가 포함되지 않은 두 개의 작은 따옴표로 지정할 수 있습니다. 길이가 0인 이진 문자열은 16진수 상수에 바이트 값이 지정되지 않은 0x로 지정할 수 있습니다. 길이가 0인 문자열을 연결하면 항상 지정된 문자열 2개가 연결됩니다. Null 값을 가진 문자열을 처리할 때는 세션 설정에 따라 연결 결과가 달라집니다. Null 값에 대해 수행되는 산술 연산에서 Null 값이 Null이 아닌 다른 값과 더해지면 대개 알 수 없는 값이 얻어지는 것처럼, Null 값을 다른 문자열과 연결하면 결과는 Null로 계산됩니다. 그러나의 설정을 변경 하 여이 동작을 변경할 수 있습니다 `CONCAT_NULL_YIELDS_NULL` 현재 세션에 대 한 합니다. 자세한 내용은 [SET CONCAT_NULL_YIELDS_NULL&#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)을 참조하세요.  
  
 문자열 연결의 결과가 제한치인 8,000바이트를 초과하면 결과가 잘립니다. 하지만 연결된 문자열 중 하나 이상이 큰 값 형식이면 잘림은 발생하지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-string-concatenation"></a>1. 문자열 연결 사용  
 다음 예에서는 여러 문자 열에서 사람의 성, 쉼표, 공백 및 사람의 이름을 사용하여 `Name`이라는 열 머리글의 단일 열을 만듭니다. 결과 집합에서 성과 이름이 사전 오름차순으로 정렬됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + FirstName) AS Name  
FROM Person.Person  
ORDER BY LastName ASC, FirstName ASC;  
```  
  
### <a name="b-combining-numeric-and-date-data-types"></a>2. numeric 및 date 데이터 형식의 결합  
 다음 예제에서는 `CONVERT` 연결할 함수 **숫자** 및 **날짜** 데이터 형식입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT 'The order is due on ' + CONVERT(varchar(12), DueDate, 101)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID = 50001;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `------------------------------------------------`  
  
 `The order is due on 04/23/2007`  
  
 `(1 row(s) affected)`  
  
### <a name="c-using-multiple-string-concatenation"></a>3. 여러 문자열의 연결  
 다음 예에서는 여러 개의 문자열을 하나의 긴 문자열로 연결하여 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]에 부사장들의 성과 첫 번째 이니셜을 표시합니다. 성 뒤에는 쉼표, 그리고 첫 번째 이니셜 뒤에는 마침표가 추가됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ',' + SPACE(1) + SUBSTRING(FirstName, 1, 1) + '.') AS Name, e.JobTitle  
FROM Person.Person AS p  
    JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle LIKE 'Vice%'  
ORDER BY LastName ASC;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Name               Title`  
  
 `-------------      ---------------`  
  
 `Duffy, T.          Vice President of Engineering`  
  
 `Hamilton, J.       Vice President of Production`  
  
 `Welcker, B.        Vice President of Sales`  
  
 `(3 row(s) affected)`  
 
### <a name="d-using-large-strings-in-concatenation"></a>4. 연결의 큰 문자열을 사용 하 여
다음 예제에서는 여러 문자열을 하나의 긴 문자열로 연결 하 고 최종 문자열의 길이 계산 하려고 합니다. 결과 집합의 최종 길이 16000은, 식 평가 시작에서 유지 하는 때문 이면 @x + @z + @y = > (@x + @z) + @y합니다. 이 경우의 결과 (@x + @z) 8000 바이트로 잘립니다 차례로 @y 16000 최종 문자열 길이 결과 집합에 추가 됩니다. 이후 @y 이 큰 값 형식 문자열인 경우 잘림이 발생 하지 않습니다.

```
DECLARE @x varchar(8000) = replicate('x', 8000)
DECLARE @y varchar(max) = replicate('y', 8000)
DECLARE @z varchar(8000) = replicate('z',8000)
SET @y = @x + @z + @y
-- The result of following select is 16000
SELECT len(@y) AS y
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `y      `  
  
 `-------`  
  
 `16000`  
  
  `(1 row(s) affected)`  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-string-concatenation"></a>5. 문자열 연결 사용  
 다음 예제에서는 열 머리글의 단일 열 `Name` 에서 여러 문자 열을, 쉼표, 공백 및 연락처의 성 연락처의 성 사용 합니다. 결과 집합에서 성과 이름이 사전 오름차순으로 정렬됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + FirstName) AS Name  
FROM DimEmployee  
ORDER BY LastName ASC, FirstName ASC;  
```  
  
### <a name="f-using-multiple-string-concatenation"></a>6. 여러 문자열의 연결  
 다음 예제에서는 여러 개의 문자열 마지막 이름 및 성의 첫 이니셜 부사장 샘플 데이터베이스에서 표시 하는 하나의 긴 문자열을 연결 합니다. 성 뒤에는 쉼표, 그리고 첫 번째 이니셜 뒤에는 마침표가 추가됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + SUBSTRING(FirstName, 1, 1) + '.') AS Name, Title  
FROM DimEmployee  
WHERE Title LIKE '%Vice Pres%'  
ORDER BY LastName ASC;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name               Title                                           
-------------      ---------------  
Duffy, T.          Vice President of Engineering  
Hamilton, J.       Vice President of Production  
Welcker, B.        Vice President of Sales  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CAST 및 convert&#40; Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [데이터 형식 변환 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [+ = &#40; 문자열 연결 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/string-concatenation-equal-transact-sql.md)  
  
  




