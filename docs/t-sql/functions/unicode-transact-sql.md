---
title: UNICODE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UNICODE
- UNICODE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first character of input expression [SQL Server]
- UNICODE function
- Unicode [SQL Server], UNICODE function
ms.assetid: 5e3c40b2-8401-4741-9f2a-bae70eaa4da6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eeb1b58975e992445bdd26f90423908f9ee3234c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098626"
---
# <a name="unicode-transact-sql"></a>UNICODE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  유니코드 표준에서 정의한 대로 입력 식에 있는 첫 글자의 정수 값을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
UNICODE ( 'ncharacter_expression' )  
```  
  
## <a name="arguments"></a>인수  
**'** *ncharacter_expression* **'**  
**nchar** 또는 **nvarchar** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
**int**  
  
## <a name="remarks"></a>Remarks  
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 UNICODE 함수는 유니코드 BMP(Basic Multilingual Plane)로 65,535개 문자를 나타낼 수 있는 000000~00FFFF 범위의 UCS-2 코드 포인트를 반환합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [SC(보조 문자)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) 사용 데이터 정렬을 사용할 때 UNICODE가 000000에서 10FFFF까지 범위의 UTF-16 코드 포인트를 반환합니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)]의 유니코드 지원에 대한 자세한 내용은 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md#Unicode_Defn)을 참조하세요. 
  
## <a name="examples"></a>예  
  
### <a name="a-using-unicode-and-the-nchar-function"></a>1\. UNICODE 및 NCHAR 함수 사용  
 다음 예에서는 `UNICODE`와 `NCHAR` 함수를 사용하여 `Åkergatan` 24 문자열에 있는 첫 글자의 UNICODE 값을 인쇄하고 실제 첫 글자 `Å`를 인쇄합니다.  
  
```sql  
DECLARE @nstring nchar(12);  
SET @nstring = N'Åkergatan 24';  
SELECT UNICODE(@nstring), NCHAR(UNICODE(@nstring));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -   
197         Å  
```  
  
### <a name="b-using-substring-unicode-and-convert"></a>2\. SUBSTRING, UNICODE, CONVERT 사용  
 다음 예에서는 `SUBSTRING`, `UNICODE` 및 `CONVERT` 함수를 사용하여 `Åkergatan 24` 문자열에 있는 각 문자의 문자 번호, 유니코드 문자, UNICODE 값 등을 인쇄하는 방법을 보여 줍니다.  
  
```sql  
-- The @position variable holds the position of the character currently  
-- being processed. The @nstring variable is the Unicode character   
-- string to process.  
DECLARE @position int, @nstring nchar(12);  
-- Initialize the current position variable to the first character in   
-- the string.  
SET @position = 1;  
-- Initialize the character string variable to the string to process.   
-- Notice that there is an N before the start of the string, which   
-- indicates that the data following the N is Unicode data.  
SET @nstring = N'Åkergatan 24';  
-- Print the character number of the position of the string you are at,   
-- the actual Unicode character you are processing, and the UNICODE   
-- value for this particular character.  
PRINT 'Character #' + ' ' + 'Unicode Character' + ' ' + 'UNICODE Value';  
WHILE @position <= DATALENGTH(@nstring)  
-- While these are still characters in the character string,  
   BEGIN;  
   SELECT @position,   
      CONVERT(char(17), SUBSTRING(@nstring, @position, 1)),  
      UNICODE(SUBSTRING(@nstring, @position, 1));  
   SELECT @position = @position + 1;  
   END;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Character # Unicode Character UNICODE Value  
  
----------- ----------------- -----------   
1           Å                 197           
  
----------- ----------------- -----------   
2           k                 107           
  
----------- ----------------- -----------   
3           e                 101           
  
----------- ----------------- -----------   
4           r                 114           
  
----------- ----------------- -----------   
5           g                 103           
  
----------- ----------------- -----------   
6           a                 97            
  
----------- ----------------- -----------   
7           t                 116           
  
----------- ----------------- -----------   
8           a                 97            
  
----------- ----------------- -----------   
9           n                 110           
  
----------- ----------------- -----------   
10                            32            
  
----------- ----------------- -----------   
11          2                 50            
  
----------- ----------------- -----------   
12          4                 52  
```  
  
## <a name="see-also"></a>참고 항목  
 [ASCII&#40;Transact-SQL&#41;](../../t-sql/functions/ascii-transact-sql.md)  
 [CHAR&#40;Transact-SQL&#41;](../../t-sql/functions/char-transact-sql.md)  
 [NCHAR&#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  

