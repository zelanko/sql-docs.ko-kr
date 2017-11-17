---
title: PATINDEX (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/19/2016
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
caps.latest.revision: 53
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: abf357840512c1447f0977a151ca742b148f45d2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="patindex-transact-sql"></a>PATINDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  유효한 모든 텍스트 및 문자 데이터 형식으로 지정한 식에서 패턴이 처음 나타나는 시작 위치를 반환하거나 패턴을 찾지 못하면 0을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## <a name="arguments"></a>인수  
 *패턴*  
 찾을 시퀀스가 포함된 문자 식 입니다. 와일드 카드 문자를 사용할 수 있습니다. 그러나 % 문자가 앞에 야 하며 따라 *패턴* (제외 하 고 검색 하는 경우 첫 번째 또는 마지막 문자에 대 한). *패턴* 문자 문자열 데이터 형식 범주의 식입니다. *패턴* 8000 자로 제한 됩니다.  
  
 *expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md), 일반적으로 지정된 된 패턴에 대 한 검색 되는 열을 합니다. *식* 문자열 데이터 형식 범주입니다.  
  
## <a name="return-types"></a>반환 형식  
 **bigint** 경우 *식* 입니다는 **varchar (max)** 또는 **nvarchar (max)** 데이터 형식이 고, 그렇지 않으면 **int**합니다.  
  
## <a name="remarks"></a>주의  
 어느 경우 *패턴* 또는 *식* 가 NULL 이면 PATINDEX는 NULL을 반환 합니다.  
  
 PATINDEX는 입력 데이터 정렬에 따라 비교를 수행합니다. 지정된 데이터 정렬에서 비교를 수행하려면 COLLATE를 사용하여 입력에 명시적 데이터 정렬을 적용할 수 있습니다.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 반환 값 utf-16 서로게이트 쌍을 계산 합니다 SC 데이터 정렬을 사용 하는 경우는 *식* 매개 변수는 단일 문자입니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
 0x0000 (**char(0)**)은 Windows 데이터 정렬에서 정의 되지 않은 문자 이며 PATINDEX에 포함할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-patindex-example"></a>1. 간단한 PATINDEX 예  
 다음 예제에는 짧은 문자열을 검사 (`interesting data`) 문자의 시작 위치에 대 한 `ter`합니다.  
  
```  
SELECT PATINDEX('%ter%', 'interesting data');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `3`  
  
### <a name="b-using-a-pattern-with-patindex"></a>2. PATINDEX와 함께 패턴 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `ensure` 테이블에 있는 `DocumentSummary` 열의 특정 행에서 `Document` 패턴이 시작하는 위치를 찾습니다.  
  
```  
SELECT PATINDEX('%ensure%',DocumentSummary)  
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
GO   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
64  
(1 row(s) affected)
```  
  
 사용 하 여 검색할 행을 제한 하지 않는 경우는 `WHERE` 절 쿼리는 테이블의 모든 행을 반환 및 패턴이 발견 된 해당 행에 대해 0이 아닌 값 및 패턴 되지 발견 된 모든 행에 대해 0을 보고 합니다.  
  
### <a name="c-using-wildcard-characters-with-patindex"></a>3. PATINDEX와 함께 와일드카드 문자 사용  
 다음 예에서는 % 및 와일드카드를 사용하여 지정된 문자열에서 하나의 문자 및 `'en'`가 뒤에 오는 `'ure'` 패턴이 시작하는 위치를 찾습니다(인덱스가 1에서 시작함).  
  
```  
SELECT PATINDEX('%en_ure%', 'please ensure the door is locked');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
8  
```  
  
 `PATINDEX`는 `LIKE`와 동일하게 작동하므로 와일드카드 중 하나를 사용할 수 있습니다. 패턴을 백분율로 묶을 필요는 없습니다. `PATINDEX('a%', 'abc')`는 1을 반환하고, `PATINDEX('%a', 'cba')`는 3을 반환합니다.  
  
 `LIKE`와 달리 `PATINDEX`는 위치를 반환하는데, 이는 `CHARINDEX`와 유사합니다.  
  
### <a name="d-using-collate-with-patindex"></a>4. PATINDEX와 함께 COLLATE 사용  
 다음 예에서는 `COLLATE` 함수를 사용하여 검색된 식의 데이터 정렬을 명시적으로 지정합니다.  
  
```  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
  
### <a name="e-using-a-variable-to-specify-the-pattern"></a>5. 변수를 사용하여 패턴 지정  
 다음 예에서는 변수를 사용 하 여 값을 전달 하는 *패턴* 매개 변수입니다. 사용 하 여이 예제는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스입니다.  
  
```  
DECLARE @MyValue varchar(10) = 'safety';   
SELECT PATINDEX('%' + @MyValue + '%', DocumentSummary)   
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------------  
 22
 ```  
  

  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [&#40; 와일드 카드-문자 &#40; s &#41; 일치 하는 항목 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#40; 와일드 카드-문자 &#40; s &#41; 일치 하는 항목 &#41;에 없습니다 &#40; Transact SQL &#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)   
 [_ &#40; 와일드 카드-문자 하 나와 일치 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)   
 [백분율 문자 &#40; 와일드 카드-문자 &#40; s &#41; 일치 하는 항목 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)  
  
  



