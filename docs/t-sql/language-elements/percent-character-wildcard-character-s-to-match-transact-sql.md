---
description: 백분율 문자(와일드카드 - 일치하는 문자)(Transact-SQL)
title: 와일드카드 검색(%)
ms.custom: seo-lt-2019
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '%'
- '%_TSQL'
- wildcard
dev_langs:
- TSQL
helpviewer_keywords:
- conditions [SQL Server], wildcards
- '% (wildcard - character(s) to match)'
- matching conditions [SQL Server]
- wildcard characters [SQL Server]
- characters [SQL Server], wildcard
ms.assetid: d4cbc1a9-37e1-4101-97fb-e6ac30c1223e
author: rothja
ms.author: jroth
ms.openlocfilehash: 3b9a47ebd388c5720a8016763d36eac3b913ce14
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92191246"
---
# <a name="percent-character-wildcard---characters-to-match-transact-sql"></a>백분율 문자(와일드카드 - 일치하는 문자)(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  0개 이상의 문자로 된 문자열에 대응합니다. 와일드카드 문자를 접두사 또는 접미사로 사용할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `Person`의 `AdventureWorks2012` 테이블에서 이름이 `Dan`으로 시작되는 모든 직원을 반환합니다.  
  
```syntaxsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Dan%';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [&#91 &#93;(와일드카드 - 일치하는 문자)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
  [&#91;^&#93;(와일드카드 - 일치하지 않는 문자)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_(와일드카드 - 한 문자 일치)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
