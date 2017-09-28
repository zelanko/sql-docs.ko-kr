---
title: SUBSTRING (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 65
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f36ec82c65e5d52c2186c67033adddbf1700c4d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="substring-transact-sql"></a>SUBSTRING(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 문자, 이진, 텍스트 또는 이미지 식의 일부를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SUBSTRING ( expression ,start , length )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 이 **문자**, **이진**, **텍스트**, **ntext**, 또는 **이미지**[식](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *시작*  
 정수 또는 **bigint** 반환 되는 문자의 시작 위치를 지정 하는 식입니다. (1, 기반된은 식에서 첫 번째 문자는 1는 번호 매기기)입니다. 경우 *시작* 1 보다 작으면 반환 되는 식은에 지정 된 첫 번째 문자에서 시작 됩니다 *식*합니다. 이 경우 반환 되는 문자 수는 가장 큰 값의 합계의 *시작* + *길이*-1 또는 0입니다. 경우 *시작* 수보다 큰 값 식에 있는 문자의 길이가 0 인 식이 반환 됩니다.  
  
 *length*  
 양의 정수 또는 **bigint** 식의 문자 수를 지정 하는 *식* 반환 됩니다. 경우 *길이* 가 음수 이면 오류가 생성 되 고 문이 종료 됩니다. 경우 총 *시작* 및 *길이* 의 문자 수보다 크면 *식*에서 시작 하는 전체 값 식이 *시작*반환 됩니다.  
  
## <a name="return-types"></a>반환 형식  
 경우 문자 데이터를 반환 *식* 지원 되는 문자 데이터 형식 중 하나입니다. 경우에 이진 데이터를 반환 *식* 는 지원 되는 하나 **이진** 데이터 형식입니다. 반환되는 문자열은 다음 표에 표시된 항목을 제외하고 지정된 식과 같은 형식입니다.  
  
|지정된 식|반환 형식|  
|--------------------------|-----------------|  
|**char**/**varchar**/**텍스트**|**varchar**|  
|**nchar**/**nvarchar**/**ntext**|**nvarchar**|  
|**이진**/**varbinary**/**이미지**|**varbinary**|  
  
## <a name="remarks"></a>주의  
 에 대 한 값 *시작* 및 *길이* 의 문자 수를 지정 해야 **ntext**, **char**, 또는 **varchar**  데이터 형식 및에 대 한 바이트 **텍스트**, **이미지**, **이진**, 또는 **varbinary** 데이터 형식입니다.  
  
 *식* 해야 **varchar (max)** 또는 **varbinary (max)** 때는 *시작* 또는 *길이* 2147483647 보다 큰 값을 포함합니다.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 SC (보조 문자) 데이터 정렬을 사용할 때 둘 다 *시작* 및 *길이* 각 서로게이트 쌍의 수 *식* 는 단일 문자입니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-substring-with-a-character-string"></a>1. 문자열과 SUBSTRING 사용  
 다음 예에서는 문자열의 일부를 반환하는 방법을 보여 줍니다. `sys.databases` 테이블을이 쿼리는 시스템 데이터베이스의 이름을 반환 합니다 첫 번째 열의 두 번째 열에 데이터베이스 및 세 번째와 네 번째 문자는 마지막 열에서의 첫 번째 문자입니다.  
  
```  
SELECT name, SUBSTRING(name, 1, 1) AS Initial ,
SUBSTRING(name, 3, 2) AS ThirdAndFourthCharacters
FROM sys.databases  
WHERE database_id < 5;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

|name |Initial |ThirdAndFourthCharacters|
|---|--|--|
|master  |m  |st |
|tempdb  |t  |mp |
|model   |m  |de |
|msdb    |m  |db |


  
 다음 예에서는 문자열 상수 `abcdef`의 둘째, 셋째, 넷째 문자를 표시하는 방법을 보여 줍니다.  
  
```  
SELECT x = SUBSTRING('abcdef', 2, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `x`  
  
 `----------`  
  
 `bcd`  
  
 `(1 row(s) affected)`  
  
### <a name="b-using-substring-with-text-ntext-and-image-data"></a>2. text, ntext, image 데이터와 SUBSTRING 사용  
  
> [!NOTE]  
>  다음 예제를 실행 하려면 설치 해야는 **pubs** 데이터베이스입니다.  
  
 다음 예제에서는 각각의 처음 10 자를 반환 하는 방법을 보여 줍니다는 **텍스트** 및 **이미지** 데이터 열에는 `pub_info` 목차는 `pubs` 데이터베이스입니다. **텍스트** 데이터는 **varchar**, 및 **이미지** 데이터는 **varbinary**합니다.  
  
```  
USE pubs;  
SELECT pub_id, SUBSTRING(logo, 1, 10) AS logo,   
   SUBSTRING(pr_info, 1, 10) AS pr_info  
FROM pub_info  
WHERE pub_id = '1756';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `pub_id logo    pr_info`  
  
 `------ ---------------------- ----------`  
  
 `1756   0x474946383961E3002500 This is sa`  
  
 `(1 row(s) affected)`  
  
 다음 예제에서는 둘 다에서 부분 문자열의 효과 보여 줍니다. **텍스트** 및 **ntext** 데이터입니다. 이 예제는 먼저 `pubs` 데이터베이스에서 `npub_info`라는 새 테이블을 만듭니다. 다음 `pr_info` 열의 처음 80자로 `npub_info` 테이블의 `pub_info.pr_info` 열을 만들고 `ü`를 첫 번째 문자로 추가합니다. 마지막으로, 한 `INNER JOIN` 게시자 id 번호를 모두 검색 및 `SUBSTRING` 둘 다의 **텍스트** 및 **ntext** 게시자 정보 열의 합니다.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-substring-with-a-character-string"></a>3. 문자열과 SUBSTRING 사용  
 다음 예에서는 문자열의 일부를 반환하는 방법을 보여 줍니다. 이 쿼리는 `dbo.DimEmployee` 테이블에서 첫 번째 열에 이름을 반환하고 두 번째 열에 머리글자를 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUBSTRING(FirstName, 1, 1) AS Initial  
FROM dbo.DimEmployee  
WHERE LastName LIKE 'Bar%'  
ORDER BY LastName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `LastName             Initial`  
  
 `-------------------- -------`  
  
 `Barbariol            A`  
  
 `Barber               D`  
  
 `Barreto de Mattos    P`  
  
 다음 예제에서는 두 번째 반환 하는 방법을 보여 줍니다 문자열 상수의 세 번째 및 네 번째 문자 `abcdef`합니다.  
  
```  
USE ssawPDW;  
  
SELECT TOP 1 SUBSTRING('abcdef', 2, 3) AS x FROM dbo.DimCustomer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `x`  
  
 `-----`  
  
 `bcd`  
  
## <a name="see-also"></a>관련 항목:  
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  



