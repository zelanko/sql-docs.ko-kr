---
title: PATINDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PATINDEX
- PATINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first occurrence of pattern [SQL Server]
- searches [SQL Server], pattern starting position
- starting position of patten search
- pattern searching [SQL Server]
- PATINDEX function
ms.assetid: c0dfb17f-2230-4e36-98da-a9b630bab656
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 51b18437976a9ecb192a69602ecbdc97054b9b47
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76831832"
---
# <a name="patindex-transact-sql"></a>PATINDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  유효한 모든 텍스트 및 문자 데이터 형식으로 지정한 식에서 패턴이 처음 나타나는 시작 위치를 반환하거나 패턴을 찾지 못하면 0을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## <a name="arguments"></a>인수  
 *pattern*  
 찾을 시퀀스가 포함된 문자 식 입니다. 와일드카드 문자를 사용할 수 있습니다. 그러나 % 문자가 앞에 오고 그 다음에 *패턴*이 와야 합니다. 단, 첫 문자 또는 마지막 문자를 검색하는 경우는 예외입니다. *패턴*은 문자열 데이터 형식 범주의 식입니다. *패턴*은 8,000자로 제한됩니다.

 > [!NOTE]
 > 기존 정규식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기본적으로 지원되지 않지만 다양한 와일드카드 식을 사용하여 비슷한 복합 패턴 일치를 실행할 수 있습니다. 와일드카드 구문에 대한 자세한 내용은 [문자열 연산자](../../t-sql/language-elements/string-operators-transact-sql.md) 문서를 참조하세요.
  
 *expression*  
 일반적으로 지정된 패턴이 검색되는 열을 나타내는 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *식*은 문자열 데이터 형식 범주입니다.  
  
## <a name="return-types"></a>반환 형식  
*식*의 데이터 형식이 **varchar(max)** 또는 **nvarchar(max)** 이면 **bigint**, 그렇지 않으면 **int**입니다.  
  
## <a name="remarks"></a>설명  
*패턴* 또는 *식*이 NULL인 경우 PATINDEX에서 NULL을 반환합니다.  
 
PATINDEX의 시작 위치는 1입니다.
 
PATINDEX는 입력 데이터 정렬에 따라 비교를 수행합니다. 지정된 데이터 정렬에서 비교를 수행하려면 COLLATE를 사용하여 입력에 명시적 데이터 정렬을 적용할 수 있습니다.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
SC 데이터 정렬을 사용하는 경우 반환 값은 *식* 매개 변수에 있는 UTF-16 서로게이트 쌍을 단일 문자로 계산합니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
0x0000 (**char(0)** )은 Windows 데이터 정렬에서 정의되지 않은 문자이며 PATINDEX에 포함할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-patindex-example"></a>A. 간단한 PATINDEX 예  
 다음 예는 짧은 문자열(`interesting data`)에서 `ter` 문자의 시작 위치를 검사합니다.  
  
```sql  
SELECT position = PATINDEX('%ter%', 'interesting data');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
position
--------
3
```
  
### <a name="b-using-a-pattern-with-patindex"></a>B. PATINDEX와 함께 패턴 사용  
다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `ensure` 테이블에 있는 `DocumentSummary` 열의 특정 행에서 `Document` 패턴이 시작하는 위치를 찾습니다.  
  
```sql  
SELECT position = PATINDEX('%ensure%',DocumentSummary)  
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
GO   
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
position
--------  
64  
```  
  
`WHERE` 절을 사용하여 검색할 행을 제한하지 않으면 쿼리는 테이블의 모든 행을 반환하고 패턴을 찾은 행에 대해서는 0이 아닌 값을 보고하고 패턴을 찾지 못한 모든 행에 대해서는 0을 보고합니다.  
  
### <a name="c-using-wildcard-characters-with-patindex"></a>C. PATINDEX와 함께 와일드카드 문자 사용  
 다음 예에서는 % 및 와일드카드를 사용하여 지정된 문자열에서 하나의 문자 및 `'en'`가 뒤에 오는 `'ure'` 패턴이 시작하는 위치를 찾습니다(인덱스가 1에서 시작함).  
  
```sql  
SELECT position = PATINDEX('%en_ure%', 'Please ensure the door is locked!');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
position
--------  
8  
```  
  
`PATINDEX`는 `LIKE`와 동일하게 작동하므로 와일드카드 중 하나를 사용할 수 있습니다. 패턴을 백분율로 묶을 필요는 없습니다. `PATINDEX('a%', 'abc')`는 1을 반환하고, `PATINDEX('%a', 'cba')`는 3을 반환합니다.  
  
 `LIKE`와 달리 `PATINDEX`는 위치를 반환하는데, 이는 `CHARINDEX`와 유사합니다.  

### <a name="d-using-complex-wildcard-expressions-with-patindex"></a>D. PATINDEX에 복합 와일드카드 식 사용 
다음 예제에서는 `[^]` [문자열 연산자](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)를 사용하여 숫자, 문자 또는 공백이 아닌 문자의 위치를 찾습니다.

```sql
SELECT position = PATINDEX('%[^ 0-9A-z]%', 'Please ensure the door is locked!'); 
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
position
--------
33
```

### <a name="e-using-collate-with-patindex"></a>E. PATINDEX와 함께 COLLATE 사용  
 다음 예에서는 `COLLATE` 함수를 사용하여 검색된 식의 데이터 정렬을 명시적으로 지정합니다.  
  
```sql  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
position
--------
9
```

### <a name="f-using-a-variable-to-specify-the-pattern"></a>F. 변수를 사용하여 패턴 지정  
다음 예에서는 변수를 사용하여 *패턴* 매개 변수로 값을 전달합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
DECLARE @MyValue varchar(10) = 'safety';   
SELECT position = PATINDEX('%' + @MyValue + '%', DocumentSummary)   
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
position
--------  
22
```  
  
## <a name="see-also"></a>참고 항목  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [CHARINDEX&#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [LEN&#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [&#40;와일드카드 - 일치하는 문자&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#40;와일드카드 - 일치하지 않는 문자&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)   
 [_ &#40;와일드카드 - 한 문자 일치&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)   
 [백분율 문자&#40;와일드카드 - 일치하는 문자&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)  
  
  


