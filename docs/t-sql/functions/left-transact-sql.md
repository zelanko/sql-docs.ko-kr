---
title: "왼쪽 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0b0ec58ed9e8bbaae6f4f4ae90834f415476b039
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="left-transact-sql"></a>LEFT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  문자열의 왼쪽부터 지정된 수만큼의 문자를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
LEFT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자 또는 이진 데이터입니다. *character_expression* 상수, 변수 또는 열일 수 있습니다. *character_expression* 제외한 데이터 형식일 수 있습니다 **텍스트** 또는 **ntext**로 암시적으로 변환할 수 있는 **varchar** 또는  **nvarchar**합니다. 그렇지 않은 경우 사용 하 여는 [캐스트](../../t-sql/functions/cast-and-convert-transact-sql.md) 함수를 명시적으로 변환 *character_expression*합니다.  
  
 *integer_expression*  
 문자 수를 지정 하는 양의 정수는 *character_expression* 반환 됩니다. 경우 *integer_expression* 가 음수 이면 오류가 반환 됩니다. 경우 *integer_expression* 형식이 **bigint** 큰 값을 포함 하 고 *character_expression* 와 같은 큰 데이터 형식 이어야 합니다 **varchar (max)**.  
  
 *integer_expression* 매개 변수를 utf-16 서로게이트 문자를 한 문자로 계산 합니다.  
  
## <a name="return-types"></a>반환 형식  
 반환 **varchar** 때 *character_expression* 유니코드가 아닌 문자 데이터 형식이 있습니다.  
  
 반환 **nvarchar** 때 *character_expression* 유니코드 문자 데이터 형식이 있습니다.  
  
## <a name="remarks"></a>주의  
 SC 데이터 정렬을 사용 하는 경우는 *integer_expression* 매개 변수는 한 문자로 utf-16 서로게이트 쌍을 계산 합니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-left-with-a-column"></a>1. 열에서 LEFT 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Product` 테이블에서 각 제품 이름에서 가장 왼쪽에 있는 5문자를 반환합니다.  
  
```  
SELECT LEFT(Name, 5)   
FROM Production.Product  
ORDER BY ProductID;  
GO  
```  
  
### <a name="b-using-left-with-a-character-string"></a>2. 문자열에서 LEFT 사용  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-left-with-a-column"></a>3. 열에서 LEFT 사용  
 다음 예에서는 각 제품 이름에서 가장 왼쪽에 있는 5문자를 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT(EnglishProductName, 5)   
FROM dbo.DimProduct  
ORDER BY ProductKey;  
```  
  
### <a name="d-using-left-with-a-character-string"></a>4. 문자열에서 LEFT 사용  
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
  
## <a name="see-also"></a>관련 항목:  
 [CAST 및 convert&#40; Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


