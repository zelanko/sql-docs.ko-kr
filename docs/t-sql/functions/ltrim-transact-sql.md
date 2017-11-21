---
title: LTRIM (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/27/2017
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
- LTRIM
- LTRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- leading blanks
- deleting blank spaces
- characters [SQL Server], blanks
- removing blank spaces
- LTRIM function
- blank characters [SQL Server]
ms.assetid: 369ed340-1a09-4597-a9eb-6720156cd39a
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad63999f685b31848ea505fd5a671d1e163ddc91
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="ltrim-transact-sql"></a>LTRIM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  선행 공백을 제거한 문자 식을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
LTRIM ( character_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자 또는 이진 데이터입니다. *character_expression* 상수, 변수 또는 열일 수 있습니다. *character_expression* 제외 하 고 데이터 형식 이어야 합니다 **텍스트**, **ntext**, 및 **이미지**, 즉 암시적으로 변환할 **varchar** . 그렇지 않은 경우 사용 하 여 [캐스트](../../t-sql/functions/cast-and-convert-transact-sql.md) 명시적으로 변환 하려면 *character_expression*합니다.  
  
## <a name="return-type"></a>반환 형식  
 **varchar** 또는 **nvarchar**  
  
## <a name="examples"></a>예  

### <a name="a-simple-example"></a>1. 간단한 예   

 다음 예제에서는 문자 식에서 선행 공백을 제거 하려면 LTRIM을 사용 합니다.  
  
```tsql  
SELECT LTRIM('     Five spaces are at the beginning of this string.') FROM sys.databases;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ---------------------------------------------------------------  
  Five spaces are at the beginning of this string.
  ```  

### <a name="b-example-using-a-variable"></a>B: 변수 사용의 예   
  
 다음 예에서는 `LTRIM`을 사용하여 문자 변수에서 선행 공백을 제거하는 방법을 보여 줍니다.  
  
```  
DECLARE @string_to_trim varchar(60);  
SET @string_to_trim = '     5 spaces are at the beginning of this string.';  
SELECT 
    @string_to_trim AS 'Original string',
    LTRIM(@string_to_trim) AS 'Without spaces';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Original string Without spaces
--------------------------------------------------- ---------------------------------------------
     5 spaces are at the beginning of this string.  5 spaces are at the beginning of this string.
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  



