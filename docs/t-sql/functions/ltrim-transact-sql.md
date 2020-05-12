---
title: LTRIM(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ea8d802e1d8434ead93a0bf637281565fabafc3c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82822665"
---
# <a name="ltrim-transact-sql"></a>LTRIM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  선행 공백을 제거한 문자 식을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
LTRIM ( character_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 문자 또는 이진 데이터의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *character_expression*은 상수, 변수 또는 열일 수 있습니다. *string_expression*은 **varchar**로 암시적으로 변환될 수 있는 데이터 형식이어야 하며 **text**, **ntext**, **image**는 제외됩니다. 그렇지 않은 경우 [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md)를 사용하여 *character_expression*을 명시적으로 변환하세요.  
  
## <a name="return-type"></a>반환 형식  
 **varchar** 또는 **nvarchar**  
  
## <a name="examples"></a>예  

### <a name="a-simple-example"></a>A. 간단한 예   

 다음 예에서는 LTRIM을 사용하여 문자 변수에서 선행 공백을 제거하는 방법을 보여 줍니다.  
  
```sql  
SELECT LTRIM('     Five spaces are at the beginning of this string.') FROM sys.databases;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ---------------------------------------------------------------  
  Five spaces are at the beginning of this string.
  ```  

### <a name="b-example-using-a-variable"></a>B: 변수 사용 예   
  
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
  
## <a name="see-also"></a>참고 항목  
 [LEFT&#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [RIGHT&#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT&#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING&#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM&#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


