---
title: NCHAR(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- nchar
- nchar_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NCHAR function
- Unicode [SQL Server], NCHAR function
ms.assetid: 68cefc68-7c4f-4326-80c1-300f90cf19db
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: eec278aab588bece400b3ba5bfa32e583b594970
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33053900"
---
# <a name="nchar-transact-sql"></a>NCHAR(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  유니코드 표준에서 정의된 대로 지정된 정수 코드에 해당하는 유니코드 문자를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
NCHAR ( integer_expression )  
```  
  
## <a name="arguments"></a>인수  
 *integer_expression*  
 데이터베이스의 데이터 정렬에 SC(보조 문자) 플래그가 포함되어 있지 않은 경우 이 인수는 0에서 65535(0~0xFFFF) 사이의 양의 정수입니다. 이 범위 밖의 값을 지정한 경우 NULL이 반환됩니다. 보조 문자에 대한 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)를 참조하세요.  
  
 데이터베이스의 데이터 정렬이 SC(보조 문자) 플래그를 지원하는 경우 이 인수는 0에서 1114111(0~0x10FFFF) 사이의 양의 정수입니다. 이 범위 밖의 값을 지정한 경우 NULL이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **nchar(1)**: 기본 데이터베이스 데이터 정렬이 보조 문자를 지원하지 않는 경우  
  
 **nvarchar(2)**: 기본 데이터베이스 데이터 정렬이 보조 문자를 지원하는 경우  
  
 *integer_expression* 매개 변수가 0 - 0xFFFF 범위에 있을 경우 한 문자만 반환됩니다. 값이 더 높을 경우 NCHAR가 해당 서로게이트 쌍을 반환합니다. `NCHAR(<High surrogate>) + NCHAR(\<Low Surrogate>)`를 사용하여 서로게이트 쌍을 생성하지 마세요. 대신 보조 문자를 지원하는 데이터베이스 데이터 정렬을 사용한 다음 서로게이트 쌍에 대한 유니코드 코드 포인트를 지정합니다. 다음 예에서는 서로게이트 쌍을 생성하는 이전 스타일의 방법과 유니코드 코드 포인트를 지정하는 기본 방법을 모두 보여 줍니다.  
  
```  
CREATE DATABASE test COLLATE Finnish_Swedish_100_CS_AS_SC;  
DECLARE @d nvarchar(10) = N'𣅿';
-- Old style method.  
SELECT NCHAR(0xD84C) + NCHAR(0xDD7F);   
  
-- Preferred method.   
SELECT NCHAR(143743);   
  
-- Alternative preferred method.  
SELECT NCHAR(UNICODE(@d));    
```  
  
## <a name="examples"></a>예  
  
### <a name="a-using-nchar-and-unicode"></a>1. NCHAR 및 UNICODE 사용  
 다음 예에서는 `UNICODE` 및 `NCHAR` 함수를 사용하여 `UNICODE` 문자열에 있는 두 번째 문자의 `NCHAR` 값과 `København`(유니코드 문자)를 인쇄하고 실제 두 번째 문자인 `ø`를 인쇄합니다.  
  
```  
DECLARE @nstring nchar(8);  
SET @nstring = N'København';  
SELECT UNICODE(SUBSTRING(@nstring, 2, 1)),   
   NCHAR(UNICODE(SUBSTRING(@nstring, 2, 1)));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -   
248         ø  
(1 row(s) affected)  
```  
  
### <a name="b-using-substring-unicode-convert-and-nchar"></a>2. SUBSTRING, UNICODE, CONVERT 및 NCHAR 사용  
 다음 예에서는 `SUBSTRING`, `UNICODE`, `CONVERT` 및 `NCHAR` 함수를 사용하여 `København` 문자열에 있는 각 문자의 문자 번호, 유니코드 문자 및 UNICODE 값을 인쇄합니다.  
  
```  
-- The @position variable holds the position of the character currently  
-- being processed. The @nstring variable is the Unicode character   
-- string to process.  
DECLARE @position int, @nstring nchar(9);  
-- Initialize the current position variable to the first character in   
-- the string.  
SET @position = 1;  
-- Initialize the character string variable to the string to process.  
-- Notice that there is an N before the start of the string. This   
-- indicates that the data following the N is Unicode data.  
SET @nstring = N'København';  
-- Print the character number of the position of the string you are at,   
-- the actual Unicode character you are processing, and the UNICODE   
-- value for this particular character.  
PRINT 'Character #' + ' ' + 'Unicode Character' + ' ' + 'UNICODE Value';  
WHILE @position <= DATALENGTH(@nstring)  
   BEGIN  
   SELECT @position,   
      NCHAR(UNICODE(SUBSTRING(@nstring, @position, 1))),  
      CONVERT(NCHAR(17), SUBSTRING(@nstring, @position, 1)),  
      UNICODE(SUBSTRING(@nstring, @position, 1))  
   SELECT @position = @position + 1  
   END;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Character # Unicode Character UNICODE Value  
  
----------- ---- ----------------- -----------   
1           K    K                 75  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
2           ø    ø                 248  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
3           b    b                 98  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
4           e    e                 101  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
5           n    n                 110  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
6           h    h                 104  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
7           a    a                 97  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
8           v    v                 118  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
9           n    n                 110  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
10          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
11          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
12          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
13          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
14          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
15          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
16          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
17          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
18          NULL                   NULL  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [ASCII&#40;Transact-SQL&#41;](../../t-sql/functions/ascii-transact-sql.md)  
 [CHAR&#40;Transact-SQL&#41;](../../t-sql/functions/char-transact-sql.md)  
 [UNICODE&#40;Transact-SQL&#41;](../../t-sql/functions/unicode-transact-sql.md)  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  

