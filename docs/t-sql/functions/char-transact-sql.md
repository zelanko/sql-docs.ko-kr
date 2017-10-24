---
title: CHAR (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- char_TSQL
- char
dev_langs:
- TSQL
helpviewer_keywords:
- converting int ACSII code to character
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
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: ff76342009f28aa66a398c0d0525c7d86391ed61
ms.contentlocale: ko-kr
ms.lasthandoff: 10/05/2017

---
# <a name="char-transact-sql"></a>CHAR(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

변환 된 **int** 문자로 ASCII 코드.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CHAR ( integer_expression )  
```  
  
## <a name="arguments"></a>인수  
*integer_expression*  
0에서 255 사이의 정수입니다. `NULL`정수 식이이 범위에 없으면 반환 됩니다.
  
## <a name="return-types"></a>반환 형식
**char(1)**
  
## <a name="remarks"></a>주의  
`CHAR`데 사용할 수는 문자열에 제어 문자를 삽입 합니다. 다음 표에서는 자주 사용되는 제어 문자를 보여 줍니다.
  
|제어 문자|값|  
|---|---|
|탭|**char (9)**|  
|줄 바꿈|**char (10)**|  
|캐리지 리턴|**char (13)**|  
  
## <a name="examples"></a>예  
  
### <a name="a-using-ascii-and-char-to-print-ascii-values-from-a-string"></a>1. ASCII 및 CHAR를 사용하여 문자열의 ASCII 값 인쇄  
다음 예에서는 `New Moon` 문자열에서 각 문자의 ASCII 값과 문자를 인쇄합니다.
  
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
  
```sql
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
  
### <a name="b-using-char-to-insert-a-control-character"></a>2. CHAR를 사용하여 제어 문자 삽입  
다음 예에서는 결과가 텍스트로 반환될 때 `CHAR(13)`를 사용하여 직원의 이름과 전자 메일 주소를 별도의 줄에 인쇄합니다. 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.
  
```sql
SELECT p.FirstName + ' ' + p.LastName, + CHAR(13)  + pe.EmailAddress   
FROM Person.Person p JOIN Person.EmailAddress pe  
ON p.BusinessEntityID = pe.BusinessEntityID  
AND p.BusinessEntityID = 1;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Ken Sanchez
ken0@adventure-works.com
  
(1 row(s) affected)
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-ascii-and-char-to-print-ascii-values-from-a-string"></a>3. ASCII 및 CHAR를 사용하여 문자열의 ASCII 값 인쇄  
다음 예제에서는 설정 하 고 6 개 ASCII 문자 숫자에 대 한 문자 값을 반환 하는 ASCII 문자를 가정 합니다.
  
```sql
SELECT CHAR(65) AS [65], CHAR(66) AS [66],   
CHAR(97) AS [97], CHAR(98) AS [98],   
CHAR(49) AS [49], CHAR(50) AS [50];  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
65   66   97   98   49   50  
---- ---- ---- ---- ---- ----  
A    B    a    b    1    2  
```
  
### <a name="d-using-char-to-insert-a-control-character"></a>4. CHAR를 사용하여 제어 문자 삽입  
다음 예제에서는 `CHAR(13)` 결과가 텍스트로 반환 될 때 별도 줄에는 데이터베이스에 대 한 정보를 반환 하 합니다.
  
```sql
SELECT name, 'was created on ', create_date, CHAR(13), name, 'is currently ', state_desc   
FROM sys.databases;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
name     create_date    name    state_desc  
------------------------------------------------------------  
master                   was created on  2003-04-08 09:13:36.390   
master                   is currently  ONLINE  
tempdb                   was created on  2014-01-10 17:24:24.023   
tempdb                   is currently  ONLINE  
AdventureWorksPDW2012    was created on  2014-05-07 09:05:07.083 
AdventureWorksPDW2012    is currently  ONLINE  
```
  
## <a name="see-also"></a>참고 항목
[+ &#40; 문자열 연결 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
[문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
  


