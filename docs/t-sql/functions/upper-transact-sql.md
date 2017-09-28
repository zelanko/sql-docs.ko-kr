---
title: "위 (Transact SQL) | Microsoft Docs"
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
- UPPER_TSQL
- UPPER
dev_langs:
- TSQL
helpviewer_keywords:
- UPPER function
- characters [SQL Server], lowercase
- converting lowercase to uppercase
- uppercase characters [SQL Server]
- characters [SQL Server], uppercase
- lowercase characters
ms.assetid: 5ced55f7-ac89-4cf2-9465-f63f4dc480db
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7572e82178b211fba9967a88cb16c20d059c7b52
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="upper-transact-sql"></a>UPPER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  소문자 데이터를 대문자로 변환한 문자 식을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
UPPER ( character_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자 데이터입니다. *character_expression* 상수, 변수 또는 문자 또는 이진 데이터의 열 수 있습니다.  
  
 *character_expression* 로 암시적으로 변환할 수 있는 데이터 형식 이어야 합니다 **varchar**합니다. 그렇지 않은 경우 사용 하 여 [캐스트](../../t-sql/functions/cast-and-convert-transact-sql.md) 명시적으로 변환 하려면 *character_expression*합니다.  
  
## <a name="return-types"></a>반환 형식  
 **varchar** 또는 **nvarchar**  
  
## <a name="examples"></a>예  
 다음 예에서는 `UPPER` 및 `RTRIM` 함수를 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Person` 테이블에 있는 사람의 성을 반환합니다. 성은 대문자로 변환되고 잘린 다음 이름 부분과 연결됩니다.  
  
```  
SELECT UPPER(RTRIM(LastName)) + ', ' + FirstName AS Name  
FROM Person.Person  
ORDER BY LastName;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예제에서는 `UPPER` 및 `RTRIM` 있는 사람의 성을 반환 하는 함수는 `dbo.DimEmployee` 대문자이 고 잘린 이름 부분과 연결 된는 테이블입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT UPPER(RTRIM(LastName)) + ', ' + FirstName AS Name  
FROM dbo.DimEmployee  
ORDER BY LastName;  
```  
  
 다음은 결과 집합의 일부입니다.  
  
 `Name`  
  
 `------------------------------`  
  
 `ABBAS, Syed`  
  
 `ABERCROMBIE, Kim`  
  
 `ABOLROUS, Hazem`  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


