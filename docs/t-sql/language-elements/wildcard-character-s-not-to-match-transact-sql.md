---
title: '[^] 문자를 제외하는 와일드카드'
description: 일치시키지 않을 문자의 T-SQL 와일드카드
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- wildcard
- '[^]_TSQL'
- '[^]'
- Not Match
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[^] (wildcard - character(s) not to match)'
ms.assetid: b970038f-f4e7-4a5d-96f6-51e3248c6aef
author: rothja
ms.author: jroth
ms.openlocfilehash: e7291bc39092d4f65fd69f8c4050bb52a512ef04
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76831732"
---
# <a name="-wildcard---characters-not-to-match-transact-sql"></a>\[^\](와일드카드 - 일치하지 않는 문자)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  대괄호 `[^]` 사이에 지정된 범위 또는 세트에 없는 하나의 문자를 찾습니다. 와일드카드 문자는 `LIKE` 및 `PATINDEX` 등의 패턴 일치를 포함하는 문자열 비교에 사용할 수 있습니다. 
  
## <a name="examples"></a>예  
### <a name="a-simple-example"></a>A: 간단한 예   
 다음 예제에서는 [^] 연산자를 사용하여 `Al`로 시작하고 세 번째 문자가 `a`가 아닌 이름을 가진 상위 5명의 사람을 `Contact` 테이블에서 찾습니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP 5 FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Al[^a]%';  
```  
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
FirstName     LastName
---------     --------
Alex          Adams
Alexandra     Adams
Allison       Adams
Alisha        Alan
Alexandra     Alexander
```
### <a name="b-searching-for-ranges-of-characters"></a>B: 문자 범위 검색

와일드카드 세트에 문자 및 범위의 조합뿐만 아니라 단일 문자 또는 문자 범위를 포함할 수 있습니다. 다음 예제에서는 [] 연산자를 사용하여 문자 또는 숫자로 시작하지 않는 문자열을 찾습니다.

```sql
SELECT [object_id], OBJECT_NAME(object_id) AS [object_name], name, column_id 
FROM sys.columns 
WHERE name LIKE '[^0-9A-z]%';
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
object_id     object_name   name    column_id
---------     -----------   ----    ---------
1591676718    JunkTable     _xyz    1
```
  
## <a name="see-also"></a>참고 항목  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX&#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [%&#40;와일드카드 - 일치하는 문자&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91;&#93; &#40;와일드카드 - 일치하는 문자&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [\_&#40;와일드카드 - 문자 하나와 일치&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
  
  
