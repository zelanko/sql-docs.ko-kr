---
title: CHAR(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- char_TSQL
- char
dev_langs:
- TSQL
helpviewer_keywords:
- converting int ASCII code to character
- control characters
- tab
- ASCII conversions
- CHAR function
- carriage return
- inserting control characters
- characters [SQL Server], control
- line feed
- printing ASCII values
ms.assetid: 955afe94-539c-465d-af22-16ec45da432a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: af2e71a4b4851e61176235b5615f0b7adbd553e2
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112155"
---
# <a name="char-transact-sql"></a>CHAR(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 함수는 **int** ASCII 코드를 문자 값으로 변환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CHAR ( integer_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*integer_expression*  
0에서 255 사이의 정수입니다. `CHAR`은 이 범위를 벗어나는 정수 식에 대해 또는 정수 식이 더블바이트 문자의 첫 번째 바이트인 경우에만 `NULL` 값을 반환합니다.

> [!NOTE]
> [Shift 일본어 산업 표준](https://www.wikipedia.org/wiki/Shift_JIS)처럼 일부 비유럽 문자 집합에는 싱글바이트 코딩 체계로 나타낼 수 있지만, 멀티바이트 인코딩이 필요한 문자가 포함됩니다. 문자 집합에 대한 자세한 내용은 [싱글바이트 및 멀티바이트 문자 집합](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)을 참조하세요. 
  
## <a name="return-types"></a>반환 형식
**char(1)**
  
## <a name="remarks"></a>설명  
문자열에 제어 문자를 삽입하는 데 `CHAR`를 사용합니다. 이 표에서는 자주 사용되는 제어 문자를 보여 줍니다.
  
|제어 문자|값|  
|---|---|
|탭|**char(9)**|  
|줄 바꿈|**char(10)**|  
|캐리지 리턴|**char(13)**|  
  
## <a name="examples"></a>예  
  
### <a name="a-using-ascii-and-char-to-print-ascii-values-from-a-string"></a>A. ASCII 및 CHAR를 사용하여 문자열의 ASCII 값 인쇄  
이 예에서는 `New Moon` 문자열에서 각 문자의 ASCII 값과 문자를 인쇄합니다.
  
```sql
SET TEXTSIZE 0;  
-- Create variables for the character string and for the current   
-- position in the string.  
DECLARE @position int, @string char(8);  
-- Initialize the current position and the string variables.  
SET @position = 1;  
SET @string = 'New Moon';  
WHILE @position <= DATALENGTH(@string)  
   BEGIN  
   SELECT ASCII(SUBSTRING(@string, @position, 1)),   
      CHAR(ASCII(SUBSTRING(@string, @position, 1)))  
   SET @position = @position + 1  
   END;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
----------- -
78          N  
----------- -  
101         e  
----------- -  
119         w  
----------- -  
32  
----------- -  
77          M  
----------- -  
111         o  
----------- -  
111         o  
----------- - 
110         n  
```
  
### <a name="b-using-char-to-insert-a-control-character"></a>B. CHAR를 사용하여 제어 문자 삽입  
이 예에서는 쿼리가 결과를 텍스트로 반환할 때 `CHAR(13)`를 사용하여 직원의 이름과 이메일 주소를 별도의 줄에 인쇄합니다. 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.
  
```sql
SELECT p.FirstName + ' ' + p.LastName, + CHAR(13)  + pe.EmailAddress   
FROM Person.Person p 
INNER JOIN Person.EmailAddress pe ON p.BusinessEntityID = pe.BusinessEntityID  
  AND p.BusinessEntityID = 1;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Ken Sanchez
ken0@adventure-works.com
  
(1 row(s) affected)
```
  
### <a name="c-using-ascii-and-char-to-print-ascii-values-from-a-string"></a>C. ASCII 및 CHAR를 사용하여 문자열의 ASCII 값 인쇄  
이 예에서는 ASCII 문자 집합이라고 가정합니다. 6가지 ASCII 문자 번호 값에 대해 문자 값을 반환합니다.
  
```sql
SELECT CHAR(65) AS [65], CHAR(66) AS [66],   
CHAR(97) AS [97], CHAR(98) AS [98],   
CHAR(49) AS [49], CHAR(50) AS [50];  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
65   66   97   98   49   50  
---- ---- ---- ---- ---- ----  
A    B    a    b    1    2  
```
  
### <a name="d-using-char-to-insert-a-control-character"></a>D. CHAR를 사용하여 제어 문자 삽입  
이 예에서는 쿼리가 결과를 텍스트로 반환할 때 `CHAR(13)`을 사용하여 데이터베이스에 대한 정보를 다른 줄에 반환합니다.
  
```sql
SELECT name, 'was created on ', create_date, CHAR(13), name, 'is currently ', state_desc   
FROM sys.databases;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
name                                      create_date               name                                  state_desc  
--------------------------------------------------------------------------------------------------------------------  
master                    was created on  2003-04-08 09:13:36.390   master                  is currently  ONLINE 
tempdb                    was created on  2014-01-10 17:24:24.023   tempdb                  is currently  ONLINE   
AdventureWorksPDW2012     was created on  2014-05-07 09:05:07.083   AdventureWorksPDW2012   is currently  ONLINE 
```

### <a name="e-using-char-to-return-single-byte-characters"></a>E. CHAR를 사용하여 싱글바이트 문자 반환  
이 예제에서는 ASCII에 대해 유효한 범위의 정수 및 16진수 값을 사용합니다. CHAR 함수는 싱글바이트 일본어 문자를 출력할 수 있습니다.
  
```sql
SELECT CHAR(188) AS single_byte_representing_complete_character, 
  CHAR(0xBC) AS single_byte_representing_complete_character;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
single_byte_representing_complete_character single_byte_representing_complete_character
------------------------------------------- -------------------------------------------
ｼ                                           ｼ                                         
```

### <a name="f-using-char-to-return-multibyte-characters"></a>F. CHAR를 사용하여 멀티바이트 문자 반환  
이 예제에서는 ASCII에 대해 유효한 범위의 정수 및 16진수 값을 사용합니다. 그러나 매개 변수가 멀티바이트 문자의 첫 번째 바이트만 나타내기 때문에 CHAR 함수는 NULL을 반환합니다.
  
```sql
SELECT CHAR(129) AS first_byte_of_double_byte_character, 
  CHAR(0x81) AS first_byte_of_double_byte_character;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
first_byte_of_double_byte_character first_byte_of_double_byte_character
----------------------------------- -----------------------------------
NULL                                NULL                                         
```
  
## <a name="see-also"></a>참고 항목
 [ASCII&#40;Transact-SQL&#41;](../../t-sql/functions/ascii-transact-sql.md)  
 [NCHAR&#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)  
 [UNICODE&#40;Transact-SQL&#41;](../../t-sql/functions/unicode-transact-sql.md)  
 [+ &#40;문자열 연결&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
  

