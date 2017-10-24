---
title: "백분율 문자 (와일드 카드-하나 이상의 문자 일치) (Transact SQL) | Microsoft Docs"
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
- Azure SQL Data Warehouse
- Azure SQL Database
- SQL Server (starting with 2008)
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
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 63891f4f25781d1a4e7f169d42c4db779d5a9c12
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="percent-character-wildcard---characters-to-match-transact-sql"></a>백분율 문자(와일드카드 - 일치하는 문자)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  0개 이상의 문자로 된 문자열에 대응합니다. 와일드카드 문자를 접두사 또는 접미사로 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Person`의 `AdventureWorks2012` 테이블에서 이름이 `Dan`으로 시작되는 모든 직원을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Dan%';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [마찬가지로 &#40; Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [&#91; &#93; (와일드 카드-하나 이상의 문자 일치)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
  [&#91; ^ &#93; (와일드 카드-일치 하지 않는 문자)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_ (와일드 카드-문자 하 나와 일치)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  

