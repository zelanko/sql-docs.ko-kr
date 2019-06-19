---
title: RIGHT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 045f9af1cd88c83f4591e4c02f476712eebf234e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65944718"
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
 문자 또는 이진 데이터의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *character_expression*은 상수, 변수 또는 열일 수 있습니다. *character_expression*은 **varchar** 또는 **nvarchar**로 변환될 수 있으며 **text** 또는 **ntext**를 제외한 모든 데이터 형식일 수 있습니다. 그렇지 않을 경우 [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) 함수를 사용하여 *character_expression*으로 명시적으로 변환합니다.  
  
 *integer_expression*  
 반환될 *character_expression*의 문자 수를 지정하는 양의 정수입니다. *integer_expression*이 음수이면 오류가 반환됩니다. *integer_expression*이 **bigint** 형식이고 큰 값이 포함된 경우 *character_expression*은 **varchar(max)** 와 같은 큰 데이터 형식이어야 합니다.  
  
## <a name="return-types"></a>반환 형식  
 *character_expression*이 유니코드가 아닌 문자 데이터 형식인 경우 **varchar**를 반환합니다.  
  
 *character_expression*이 유니코드 문자 데이터 형식인 경우 **nvarchar**를 반환합니다.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 SC 데이터 정렬을 사용하는 경우 RIGHT 함수가 UTF-16 서로게이트 쌍을 단일 문자로 계산합니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-right-with-a-column"></a>A: 열에서 RIGHT 사용  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-right-with-a-column"></a>2\. 열에서 RIGHT 사용  
 다음 예는 각 성에서 가장 오른쪽 다섯 문자를 `DimEmployee` 표에 반환합니다.  
  
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
  
### <a name="c-using-right-with-a-character-string"></a>C. 문자열에서 RIGHT 사용  
 다음 예는 `RIGHT`를 사용하여 `abcdefg` 문자열의 가장 오른쪽 두 문자를 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(1) RIGHT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-------  
fg
```  
  
## <a name="see-also"></a>참고 항목  
 [LEFT&#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT&#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING&#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM&#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

