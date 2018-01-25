---
title: "(와일드 카드-하나 이상의 문자 일치) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Match
- wildcard
- '[ ]'
- '[_]_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[ ] (wildcard - character(s) to match)'
ms.assetid: 57817576-0bf1-49ed-b05d-fac27e8fed7a
caps.latest.revision: "32"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 04fcf0d9e76db380430bfbf4c4ed6e5fadf14afb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="--wildcard---characters-to-match-transact-sql"></a>\[\] (와일드 카드-일치 항목으로 자) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정 된 범위 또는 대괄호 사이 지정 된 집합 내 임의의 단일 문자와 일치 `[ ]`합니다. 패턴 일치를 포함 하는 문자열 비교에서 이러한 와일드 카드 문자를 사용할 수 있습니다 `LIKE` 및 `PATINDEX`합니다.  
  
## <a name="examples"></a>예  
### <a name="a-simple-example"></a>A: 간단한 예   
다음 예제에서는 문자로 시작 하는 이름을 반환 `m`합니다. `[n-z]`두 번째 문자 까지의 범위에 어딘가에 같아야 함을 지정 `n` 를 `z`합니다. 백분율 와일드 카드 `%` 3는 문자로 시작 하는 모든 없거나 자를 허용 합니다. `model` 및 `msdb` 데이터베이스가이 기준을 충족 합니다. `master` 데이터베이스 하지 않으며 결과 집합에서 제외 됩니다.
 
```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm[n-z]%';
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
name
-----
model
msdb
```   
 추가 조건에 맞는 데이터베이스 설치를 할 수 있습니다.


### <a name="b-more-complex-example"></a>B: 더 복잡 한 예제   
 다음 예에서는 [] 연산자를 사용하여 4자리 우편 번호 주소를 가지는 모든 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 직원의 ID와 이름을 찾는 방법을 보여 줍니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.BusinessEntityID, p.FirstName, p.LastName, a.PostalCode  
FROM HumanResources.Employee AS e  
INNER JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
INNER JOIN Person.Address AS a ON a.AddressID = ea.AddressID  
WHERE a.PostalCode LIKE '[0-9][0-9][0-9][0-9]';  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
EmployeeID      FirstName      LastName      PostalCode  
----------      ---------      ---------     ----------  
290             Lynn           Tsoflias      3000  
```  



  
## <a name="see-also"></a>관련 항목:  
 [마찬가지로 &#40; Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40; Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% &#40; 와일드 카드-문자 &#40; s &#41; 일치 하는 항목 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93; &#40; 와일드 카드-문자 &#40; s &#41; 일치 하는 항목 &#41;에 없습니다 &#40; Transact SQL &#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [\_&#40; 와일드 카드-문자 하 나와 일치 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
