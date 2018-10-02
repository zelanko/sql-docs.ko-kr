---
title: CHARINDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHARINDEX
- CHARINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], pattern searching
- CHARINDEX function
- pattern searching [SQL Server]
- starting point of expression in character string
ms.assetid: 78c10341-8373-4b30-b404-3db20e1a3ac4
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 88f57c22df5b6a621b5133f56f79a16ede550d77
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703111"
---
# <a name="charindex-transact-sql"></a>CHARINDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이 함수는 두 번째 문자 식 내에서 하나의 문자 식을 찾고, 있는 경우 첫 번째 식의 시작 위치를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CHARINDEX ( expressionToFind , expressionToSearch [ , start_location ] )   
```  
  
## <a name="arguments"></a>인수  
*expressionToFind*  
찾으려는 시퀀스가 포함된 문자 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *expressionToFind*는 8,000자로 제한됩니다.
  
*expressionToSearch*  
검색할 문자 식입니다.
  
*start_location*  
검색이 시작되는 **integer** 또는 **bigint** 식입니다. *start_location*이 지정되지 않았거나 음수 값 또는 0 값이면, *expressionToSearch*의 시작 부분에서 검색이 시작됩니다.
  
## <a name="return-types"></a>반환 형식
*expressionToSearch*의 데이터 형식이 **nvarchar(max)**, **varbinary(max)** 또는 **varchar(max)** 이면 **bigint**이고, 그렇지 않으면 **int**입니다.
  
## <a name="remarks"></a>Remarks  
*expressionToFind* 또는 *expressionToSearch* 식에 유니코드 데이터 형식(**nchar** 또는 **nvarchar**)이 있고 다른 식에는 이러한 형식이 없으면, CHARINDEX 함수에서 다른 식을 유니코드 데이터 형식으로 변환합니다. CHARINDEX는 **image**, **ntext** 및 **text** 데이터 형식으로 사용할 수 없습니다.
  
*expressionToFind* 또는 *expressionToSearch* 식에 NULL 값이 있으면 CHARINDEX에서 NULL을 반환합니다.
  
CHARINDEX가 *expressionToSearch* 내에서 *expressionToFind*를 찾지 못하면 CHARINDEX에서 0을 반환합니다.
  
CHARINDEX는 입력 데이터 정렬을 기반으로 하는 비교를 수행합니다. 지정된 데이터 정렬에서 비교를 수행하려면 COLLATE를 사용하여 명시적 데이터 정렬을 입력에 적용합니다.
  
반환된 시작 위치는 0이 아닌 1부터 시작합니다.
  
0x0000(**char(0)**)은 Windows 데이터 정렬에서 정의되지 않은 문자이며 CHARINDEX에 포함할 수 없습니다.
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
SC 데이터 정렬을 사용하는 경우 *start_location*과 반환 값 둘 다 서로게이트 쌍을 둘이 아닌 한 문자로 계산합니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-starting-position-of-an-expression"></a>1. 식의 시작 위치 반환  
다음 예제에서는 검색된 `@document` 문자열 값 변수에서 `bicycle`을 검색합니다.
  
```sql
DECLARE @document varchar(64);  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bicycle', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
48            
```  
  
### <a name="b-searching-from-a-specific-position"></a>2. 특정 위치에서 검색  
다음 예제에서는 선택적 *start_location* 매개 변수를 사용하여 검색된 `@document` 문자열 값 변수의 다섯 번째 문자에서 `vital`에 대한 검색을 시작합니다.
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('vital', @document, 5);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
16            
  
(1 row(s) affected)  
```  
  
### <a name="c-searching-for-a-nonexistent-expression"></a>3. 존재하지 않는 식 검색  
다음 예제에서는 CHARINDEX가 *expressionToSearch* 내에서 *expressionToFind*를 찾지 못했을 때의 결과 집합을 보여 줍니다.
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bike', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
0
  
(1 row(s) affected)
```
  
### <a name="d-performing-a-case-sensitive-search"></a>4. 대/소문자 구분 검색 수행  
다음 예제에서는 `'This is a Test``'` 검색 문자열에서 `'TEST'` 문자열에 대한 대/소문자 구분 검색을 보여 줍니다.
  
```sql
USE tempdb;  
GO  
--perform a case sensitive search  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
0
```  
  
다음 예제에서는 `'This is a Test'`에서 `'Test'` 문자열에 대한 대/소문자 구분 검색을 보여 줍니다.
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'Test',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
11
```  
  
### <a name="e-performing-a-case-insensitive-search"></a>5. 대/소문자를 구분하지 않는 검색 수행  
다음 예제에서는 `'This is a Test'`에서 `'TEST'` 문자열에 대한 대/소문자를 구분하지 않는 검색을 보여 줍니다.
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CI_AS);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
11
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-searching-from-the-start-of-a-string-expression"></a>6. 문자열 식의 처음부터 검색  
다음 예제에서는 `This is a string`의 위치 1(첫 번째 문자)에서 시작하여 `This is a string` 문자열 중 `is` 문자열의 첫 번째 위치를 반환합니다.
  
```sql
SELECT CHARINDEX('is', 'This is a string');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
3
```  
  
### <a name="g-searching-from-a-position-other-than-the-first-position"></a>7. 첫 번째 위치 이외의 위치에서 검색  
다음 예제에서는 위치 4(네 번째 문자)에서 검색을 시작하여 `This is a string` 문자열 중 `is` 문자열의 첫 번째 위치를 반환합니다.
  
```sql
SELECT CHARINDEX('is', 'This is a string', 4);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
 6
 ```  
  
### <a name="h-results-when-the-string-is-not-found"></a>8. 문자열이 없을 경우 결과  
다음 예제에서는 CHARINDEX가 검색된 문자열에서 *string_pattern* 문자열을 찾지 못했을 때의 반환 값을 보여 줍니다.
  
```sql
SELECT TOP(1) CHARINDEX('at', 'This is a string') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
0
```  
  
## <a name="see-also"></a>관련 항목:
 [LEN&#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
 [PATINDEX&#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
 [+ &#40;문자열 연결&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  


