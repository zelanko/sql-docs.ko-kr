---
title: "(와일드 카드-일치 하지 않는 문자) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
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
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 96749cb88e4d98b112de2ce1eb9bff4c7e156e42
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="wildcard---characters-not-to-match-transact-sql"></a>(와일드 카드-일치 하지 않는 문자) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  대괄호 사이에 지정된 범위 또는 집합에 없는 하나의 문자에 대응합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [^] 연산자를 사용하여 `Contact`로 시작하고 세 번째 문자가 `Al`가 아닌 이름을 가진 사람을 `a` 테이블에서 모두 찾습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Al[^a]%'  
ORDER BY FirstName;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [마찬가지로 &#40; Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40; Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [% &#40; 와일드 카드-문자 &#40; s &#41; 일치 하는 항목 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (와일드 카드-하나 이상의 문자 일치)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [_ (와일드 카드-문자 하 나와 일치)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
  
  

