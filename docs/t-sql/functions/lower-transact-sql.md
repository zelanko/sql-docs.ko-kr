---
title: LOWER (Transact SQL) | Microsoft Docs
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
- LOWER
- LOWER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- characters [SQL Server], lowercase
- LOWER function
- uppercase characters [SQL Server]
- characters [SQL Server], uppercase
- lowercase characters
- converting uppercase to lowercase characters
ms.assetid: 1783352b-6852-4658-9d94-51963c59b9bf
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 545d3b5a0635c80f55aeb5b0a7a4e1804098e19c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="lower-transact-sql"></a>LOWER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  대문자 데이터를 소문자 데이터로 변환한 후에 문자 식을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
LOWER ( character_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자 또는 이진 데이터입니다. *character_expression* 상수, 변수 또는 열일 수 있습니다. *character_expression* 로 암시적으로 변환할 수 있는 데이터 형식 이어야 합니다 **varchar**합니다. 그렇지 않은 경우 사용 하 여 [캐스트](../../t-sql/functions/cast-and-convert-transact-sql.md) 명시적으로 변환 하려면 *character_expression*합니다.  
  
## <a name="return-types"></a>반환 형식  
 **varchar** 또는 **nvarchar**  
  
## <a name="examples"></a>예  
 다음 예에서는 가격이 $11에서 $20 사이인 제품 이름을 선택한 것에서 `LOWER` 함수, `UPPER` 함수를 사용하고 `UPPER` 함수 내에 `LOWER` 함수를 중첩하여 사용합니다. 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```  
SELECT LOWER(SUBSTRING(Name, 1, 20)) AS Lower,   
   UPPER(SUBSTRING(Name, 1, 20)) AS Upper,   
   LOWER(UPPER(SUBSTRING(Name, 1, 20))) As LowerUpper  
FROM Production.Product  
WHERE ListPrice between 11.00 and 20.00;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Lower                    Upper                    LowerUpper`  
  
 `---------------------    ---------------------    --------------------`  
  
 `minipump                 MINIPUMP                 minipump`  
  
 `taillights - battery     TAILLIGHTS - BATTERY     taillights - battery`  
  
 `(2 row(s) affected)`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 가격이 $11에서 $20 사이인 제품 이름을 선택한 것에서 `LOWER` 함수, `UPPER` 함수를 사용하고 `UPPER` 함수 내에 `LOWER` 함수를 중첩하여 사용합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT LOWER(SUBSTRING(EnglishProductName, 1, 20)) AS Lower,   
       UPPER(SUBSTRING(EnglishProductName, 1, 20)) AS Upper,   
       LOWER(UPPER(SUBSTRING(EnglishProductName, 1, 20))) As LowerUpper  
FROM dbo.DimProduct  
WHERE ListPrice between 11.00 and 20.00;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Lower                 Upper                  LowerUpper`  
  
 `--------------------  ---------------------  --------------------`  
  
 `minipump              MINIPUMP               minipump`  
  
 `taillights – battery  TAILLIGHTS – BATTERY   taillights - battery`  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


