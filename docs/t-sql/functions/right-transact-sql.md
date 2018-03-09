---
title: "오른쪽 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RIGHT_TSQL
- RIGHT
dev_langs:
- TSQL
helpviewer_keywords:
- rightmost character of expression
- RIGHT function
- character strings [SQL Server], RIGHT
ms.assetid: 43f1fe1f-aa18-47e3-ba20-e03e32254a6d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b6680078aff2e103655a94ec157371a0d09f79be
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="right-transact-sql"></a>RIGHT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정된 문자 수만큼 문자열의 오른쪽 부분을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
RIGHT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자 또는 이진 데이터입니다. *character_expression* 상수, 변수 또는 열일 수 있습니다. *character_expression* 제외한 데이터 형식일 수 있습니다 **텍스트** 또는 **ntext**로 암시적으로 변환할 수 있는 **varchar** 또는  **nvarchar**합니다. 그렇지 않은 경우 사용 하 여는 [캐스트](../../t-sql/functions/cast-and-convert-transact-sql.md) 함수를 명시적으로 변환 *character_expression*합니다.  
  
 *integer_expression*  
 문자 수를 지정 하는 양의 정수 *character_expression* 반환 됩니다. 경우 *integer_expression* 가 음수 이면 오류가 반환 됩니다. 경우 *integer_expression* 형식이 **bigint** 큰 값을 포함 하 고 *character_expression* 와 같은 큰 데이터 형식 이어야 합니다 **varchar (max)**.  
  
## <a name="return-types"></a>반환 형식  
 반환 **varchar** 때 *character_expression* 유니코드가 아닌 문자 데이터 형식이 있습니다.  
  
 반환 **nvarchar** 때 *character_expression* 유니코드 문자 데이터 형식이 있습니다.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 SC 데이터 정렬을 사용하는 경우 RIGHT 함수가 UTF-16 서로게이트 쌍을 단일 문자로 계산합니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-right-with-a-column"></a>A: 오른쪽 열으로 사용 하 여  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 각 사람의 이름에서 이 가장 오른쪽 다섯 문자를 반환합니다.  
  
```  
SELECT RIGHT(FirstName, 5) AS 'First Name'  
FROM Person.Person  
WHERE BusinessEntityID < 5  
ORDER BY FirstName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
First Name  
----------  
Ken  
Terri  
berto  
Rob  
  
(4 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-right-with-a-column"></a>2. 열이 있는 오른쪽을 사용 하 여  
 각 성의 가장 오른쪽 다섯 문자를 반환 하는 다음 예제는 `DimEmployee` 테이블입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT RIGHT(LastName, 5) AS Name  
FROM dbo.DimEmployee  
ORDER BY EmployeeKey;  
```  
  
 다음은 결과 집합의 일부입니다.  
  
 ```
Name
-----
lbert
Brown
rello
lters
 ```  
  
### <a name="c-using-right-with-a-character-string"></a>3. 문자열과 함께 오른쪽을 사용 하 여  
 다음 예제에서는 `RIGHT` 문자는 문자열의 오른쪽에 있는 두 개의 문자를 반환 하려면 `abcdefg`합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(1) RIGHT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-------  
fg
```  
  
## <a name="see-also"></a>관련 항목:  
 [왼쪽 &#40; Transact SQL &#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40; Transact SQL &#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RTRIM &#40; Transact SQL &#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40; Transact SQL &#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [부분 문자열 &#40; Transact SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40; Transact SQL &#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST 및 CONVERT &#40;TRANSACT-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

