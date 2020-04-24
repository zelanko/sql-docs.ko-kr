---
title: LEFT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LEFT
- LEFT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- character strings [SQL Server], LEFT
- characters [SQL Server], leftmost
- LEFT function
- leftmost character of expression
ms.assetid: 44a8c71b-63d8-458b-8b5d-99d570067c3c
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7fc7a7f6f8a79f699eb12580cf2d3d56622c8c4a
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635029"
---
# <a name="left-transact-sql"></a>LEFT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  문자열의 왼쪽부터 지정된 수만큼의 문자를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
LEFT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 문자 또는 이진 데이터의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *character_expression*은 상수, 변수 또는 열일 수 있습니다. *character_expression*은 **varchar** 또는 **nvarchar**로 변환될 수 있으며 **text** 또는 **ntext**를 제외한 모든 데이터 형식일 수 있습니다. 그렇지 않을 경우 [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) 함수를 사용하여 *character_expression*으로 명시적으로 변환합니다.  
  
 *integer_expression*  
 반환될 *character_expression*의 문자 수를 지정하는 양의 정수입니다. *integer_expression*이 음수이면 오류가 반환됩니다. *integer_expression*이 **bigint** 형식이고 큰 값이 포함된 경우 *character_expression*은 **varchar(max)** 와 같은 큰 데이터 형식이어야 합니다.  
  
 *integer_expression* 매개 변수는 UTF-16 서로게이트 문자를 한 문자로 계산합니다.  
  
## <a name="return-types"></a>반환 형식  
 **character_expression**이 유니코드가 아닌 문자 데이터 형식인 경우 *varchar*를 반환합니다.  
  
 **character_expression**이 유니코드 문자 데이터 형식인 경우 *nvarchar*를 반환합니다.  
  
## <a name="remarks"></a>설명  
 SC 데이터 정렬을 사용하는 경우 *integer_expression* 매개 변수가 UTF-16 서로게이트 쌍을 한 문자로 계산합니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-left-with-a-column"></a>A. 열에서 LEFT 사용  
 다음 예에서는 `Product` 데이터베이스의 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 테이블에서 각 제품 이름에서 가장 왼쪽에 있는 5문자를 반환합니다.  
  
```  
SELECT LEFT(Name, 5)   
FROM Production.Product  
ORDER BY ProductID;  
GO  
```  
  
### <a name="b-using-left-with-a-character-string"></a>B. 문자열에서 LEFT 사용  
 다음 예에서는 `LEFT`를 사용하여 `abcdefg` 문자열에서 가장 왼쪽에 있는 두 문자를 반환합니다.  
  
```  
SELECT LEFT('abcdefg',2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab   
  
(1 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-left-with-a-column"></a>C. 열에서 LEFT 사용  
 다음 예에서는 각 제품 이름에서 가장 왼쪽에 있는 5문자를 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT(EnglishProductName, 5)   
FROM dbo.DimProduct  
ORDER BY ProductKey;  
```  
  
### <a name="d-using-left-with-a-character-string"></a>D. 문자열에서 LEFT 사용  
 다음 예에서는 `LEFT`를 사용하여 `abcdefg` 문자열에서 가장 왼쪽에 있는 두 문자를 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab  
```  
  
## <a name="see-also"></a>참고 항목  
 [LTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT&#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT&#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING&#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM&#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

