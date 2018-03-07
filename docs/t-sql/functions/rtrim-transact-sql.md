---
title: RTRIM (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/05/2017
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
- RTRIM_TSQL
- RTRIM
dev_langs:
- TSQL
helpviewer_keywords:
- RTRIM function
- character strings [SQL Server], trailing blanks
- blank characters [SQL Server]
- trailing blanks
ms.assetid: 52fd6e8d-650c-4f66-abcf-67765aa5aa83
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: f2b2725ce59ea577180732bdbd44a1a7a1ed5089
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="rtrim-transact-sql"></a>RTRIM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  후행 공백을 모두 잘라낸 문자열을 반환 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
RTRIM ( character_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자 데이터입니다. *character_expression* 상수, 변수 또는 문자 또는 이진 데이터의 열 수 있습니다.  
  
 *character_expression* 로 암시적으로 변환할 수 있는 데이터 형식 이어야 합니다 **varchar**합니다. 그렇지 않은 경우 사용 하 여 [캐스트](../../t-sql/functions/cast-and-convert-transact-sql.md) 명시적으로 변환 하려면 *character_expression*합니다.  
  
## <a name="return-types"></a>반환 형식  
 **varchar** 또는 **nvarchar**  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-example"></a>1. 간단한 예  
 다음 예는 문장 끝에 공백이 있는 문자열을 받아 문장 끝에 공백이 없는 텍스트를 반환합니다.  
  
```  
SELECT RTRIM('Removes trailing spaces.   ');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
  `Removes trailing spaces.`  
  
### <a name="b-simple-example"></a>B: 간단한 예  
 다음 예제에서는 사용 하는 방법을 `RTRIM` 에 후행 공백을 제거 합니다. 이 시간 간격이 공백은 삭제 표시 하려면 첫 번째 문자열에 연결할 다른 문자열입니다.  
  
```  
SELECT RTRIM('Four spaces are after the period in this sentence.    ') + 'Next string.';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
`Four spaces are after the period in this sentence.Next string.`  

### <a name="c-using-rtrim-with-a-variable"></a>3. 변수에 RTRIM 사용  
 다음 예에서는 `RTRIM`을 사용하여 문자 변수에서 후행 공백을 제거하는 방법을 보여 줍니다.  
  
```  
DECLARE @string_to_trim varchar(60);  
SET @string_to_trim = 'Four spaces are after the period in this sentence.    ';  
SELECT @string_to_trim + ' Next string.';  
SELECT RTRIM(@string_to_trim) + ' Next string.';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```sql   
 -------------------------------------------------------------------------  
 Four spaces are after the period in this sentence.     Next string.  
 
 (1 row(s) affected)`  
 
 -------------------------------------------------------------------------  
 Four spaces are after the period in this sentence. Next string.  
 
 (1 row(s) affected)
 ```  
  

  
## <a name="see-also"></a>관련 항목:  
 [왼쪽 &#40; Transact SQL &#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40; Transact SQL &#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [오른쪽 &#40; Transact SQL &#41;](../../t-sql/functions/right-transact-sql.md)  
 [STRING_SPLIT &#40; Transact SQL &#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [부분 문자열 &#40; Transact SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40; Transact SQL &#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST 및 CONVERT &#40;TRANSACT-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


