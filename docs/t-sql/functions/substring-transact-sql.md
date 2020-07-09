---
title: SUBSTRING(Transact-SQL) | Microsoft Docs
description: SUBSTRING 함수의 Transact-SQL 참조입니다. 이 함수는 지정된 문자, 이진, 텍스트 또는 이미지 식의 일부를 반환합니다.
ms.date: 10/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUBSTRING
- SUBSTRING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- portion of expression returned [SQL Server]
- part of expression returned [SQL Server]
- SUBSTRING function
- offsets [SQL Server]
- binary [SQL Server], returning part of
- expressions [SQL Server], part returned
- characters [SQL Server], returning part of
ms.assetid: a19c808f-aaf9-4a69-af59-b1a5fc3e5c4c
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cecc99e2612acb17013f47619f32d64b7968ebc9
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85994232"
---
# <a name="substring-transact-sql"></a>SUBSTRING(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 문자, 이진, 텍스트 또는 이미지 식의 일부를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SUBSTRING ( expression ,start , length )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 **character**, **binary**, **text**, **ntext** 또는 **image** [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
 *start*  
 반환된 문자가 시작되는 위치를 지정하는 정수 또는 **bigint** 식입니다. (번호 매기기는 식의 첫 번째 문자가 1을 의미하는 1 기준입니다). *start*가 1보다 작은 경우 반환되는 식은 *expression*에 지정된 첫째 문자에서 시작합니다. 이 경우 반환되는 문자 수는 *start* + *length*-1 또는 0 중에서 더 큰 값입니다. *start*가 값 식의 문자 수보다 큰 경우 길이가 0인 식이 반환됩니다.  
  
 *length*  
 반환될 *expression*의 문자 수를 지정하는 양의 정수 또는 **bigint** 식입니다. *length*가 음수이면 오류가 발생하면서 문이 종료됩니다. *start*와 *length*의 합계가 *expression*의 문자 수보다 크면 *start*에서 시작하는 전체 값 식이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
 *expression*이 지원되는 문자 데이터 형식 중 하나이면 문자 데이터를 반환합니다. *expression*이 지원되는 **binary** 데이터 형식 중 하나이면 이진 데이터를 반환합니다. 반환되는 문자열은 다음 표에 표시된 항목을 제외하고 지정된 식과 같은 형식입니다.  
  
|지정된 식|반환 형식|  
|--------------------------|-----------------|  
|**char**/**varchar**/**text**|**varchar**|  
|**nchar**/**nvarchar**/**ntext**|**nvarchar**|  
|**binary**/**varbinary**/**image**|**varbinary**|  
  
## <a name="remarks"></a>설명  
 **ntext**, **char** 또는 **varchar** 데이터 형식의 문자 수와 **text**, **image**, **binary** 또는 **varbinary** 데이터 형식의 바이트에 대해 *start* 및 *length* 값을 지정해야 합니다.  
  
 *start* 또는 *length*에 2147483647보다 큰 값이 포함된 경우 *expression*은 **varchar(max)** 또는 **varbinary(max)** 여야 합니다.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 SC(보조 문자) 데이터 정렬을 사용하는 경우 *start* 및 *length*가 *expression*의 각 서로게이트 쌍을 단일 문자로 계산합니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-substring-with-a-character-string"></a>A. 문자열과 SUBSTRING 사용  
 다음 예에서는 문자열의 일부를 반환하는 방법을 보여 줍니다. 이 쿼리는 `sys.databases` 테이블에서 첫 번째 열에 시스템 데이터베이스 이름, 두 번째 열에 데이터베이스의 첫 번째 문자, 마지막 열에 세 번째 및 네 번째 문자를 반환합니다.  
  
```  
SELECT name, SUBSTRING(name, 1, 1) AS Initial ,
SUBSTRING(name, 3, 2) AS ThirdAndFourthCharacters
FROM sys.databases  
WHERE database_id < 5;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

|name |Initial |ThirdAndFourthCharacters|
|---|--|--|
|master    |m    |st |
|tempdb    |t    |mp |
|model    |m    |de |
|msdb    |m    |db |


  
 다음 예에서는 문자열 상수 `abcdef`의 둘째, 셋째, 넷째 문자를 표시하는 방법을 보여 줍니다.  
  
```  
SELECT x = SUBSTRING('abcdef', 2, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x  
----------  
bcd  
  
(1 row(s) affected)
```  
  
### <a name="b-using-substring-with-text-ntext-and-image-data"></a>B. text, ntext, image 데이터와 SUBSTRING 사용  
  
> [!NOTE]  
>  다음 예를 실행하려면 **pubs** 데이터베이스를 설치해야 합니다.  
  
 다음 예에서는 `pubs` 데이터베이스의 `pub_info` 테이블에 있는 각각의 **text** 및 **image** 데이터 열에서 처음 10자를 반환하는 방법을 보여 줍니다. **text** 데이터는 **varchar**로 반환되며 **image** 데이터는 **varbinary**로 반환됩니다.  
  
```  
USE pubs;  
SELECT pub_id, SUBSTRING(logo, 1, 10) AS logo,   
   SUBSTRING(pr_info, 1, 10) AS pr_info  
FROM pub_info  
WHERE pub_id = '1756';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 pub_id logo    pr_info
------ ---------------------- ----------
1756   0x474946383961E3002500 This is sa

(1 row(s) affected)
```  
  
 다음 예에서는 **text** 및 **ntext** 데이터에 SUBSTRING을 사용한 결과를 보여 줍니다. 이 예제는 먼저 `pubs` 데이터베이스에서 `npub_info`라는 새 테이블을 만듭니다. 다음 `pr_info` 열의 처음 80자로 `npub_info` 테이블의 `pub_info.pr_info` 열을 만들고 `ü`를 첫 번째 문자로 추가합니다. 마지막으로 `INNER JOIN`을 사용해 모든 게시자 ID와 **text** 및 **ntext** 게시자 정보 열의 `SUBSTRING`을 검색합니다.  
  
```  
IF EXISTS (SELECT table_name FROM INFORMATION_SCHEMA.TABLES   
      WHERE table_name = 'npub_info')  
   DROP TABLE npub_info;  
GO  
-- Create npub_info table in pubs database. Borrowed from instpubs.sql.  
USE pubs;  
GO  
CREATE TABLE npub_info  
(  
 pub_id char(4) NOT NULL  
    REFERENCES publishers(pub_id)  
    CONSTRAINT UPKCL_npubinfo PRIMARY KEY CLUSTERED,  
pr_info ntext NULL  
);  
  
GO  
  
-- Fill the pr_info column in npub_info with international data.  
RAISERROR('Now at the inserts to pub_info...',0,1);  
  
GO  
  
INSERT npub_info VALUES('0736', N'üThis is sample text data for New Moon Books, publisher 0736 in the pubs database')  
,('0877', N'üThis is sample text data for Binnet & Hardley, publisher 0877 in the pubs databa')  
,('1389', N'üThis is sample text data for Algodata Infosystems, publisher 1389 in the pubs da')  
,('9952', N'üThis is sample text data for Scootney Books, publisher 9952 in the pubs database')  
,('1622', N'üThis is sample text data for Five Lakes Publishing, publisher 1622 in the pubs d')  
,('1756', N'üThis is sample text data for Ramona Publishers, publisher 1756 in the pubs datab')  
,('9901', N'üThis is sample text data for GGG&G, publisher 9901 in the pubs database. GGG&G i')  
,('9999', N'üThis is sample text data for Lucerne Publishing, publisher 9999 in the pubs data');  
GO  
-- Join between npub_info and pub_info on pub_id.  
SELECT pr.pub_id, SUBSTRING(pr.pr_info, 1, 35) AS pr_info,  
   SUBSTRING(npr.pr_info, 1, 35) AS npr_info  
FROM pub_info pr INNER JOIN npub_info npr  
   ON pr.pub_id = npr.pub_id  
ORDER BY pr.pub_id ASC;  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-substring-with-a-character-string"></a>C. 문자열과 SUBSTRING 사용  
 다음 예에서는 문자열의 일부를 반환하는 방법을 보여 줍니다. 이 쿼리는 `dbo.DimEmployee` 테이블에서 첫 번째 열에 이름을 반환하고 두 번째 열에 머리글자를 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUBSTRING(FirstName, 1, 1) AS Initial  
FROM dbo.DimEmployee  
WHERE LastName LIKE 'Bar%'  
ORDER BY LastName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName             Initial
-------------------- -------
Barbariol            A
Barber               D
Barreto de Mattos    P
```  
  
 다음 예는 문자열 상수 `abcdef`의 두 번째, 세 번째, 네 번째 문자를 반환하는 방법을 보여줍니다.  
  
```  
USE ssawPDW;  
  
SELECT TOP 1 SUBSTRING('abcdef', 2, 3) AS x FROM dbo.DimCustomer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x
-----
bcd
```  
  
## <a name="see-also"></a>참고 항목  
 [LEFT&#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT&#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT&#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [TRIM&#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


