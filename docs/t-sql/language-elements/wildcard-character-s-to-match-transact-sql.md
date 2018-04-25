---
title: '[ ](와일드카드 - 일치하는 문자)(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Match
- wildcard
- '[ ]'
- '[_]_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[ ] (wildcard - character(s) to match)'
ms.assetid: 57817576-0bf1-49ed-b05d-fac27e8fed7a
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 975848a7434badb238b91175cf29e5bfe09843cc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="--wildcard---characters-to-match-transact-sql"></a>\[ \](와일드카드 - 일치하는 문자)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정된 범위 또는 대괄호 `[ ]` 사이에 지정한 집합에 포함되는 하나의 문자와 일치됩니다. 와일드카드 문자는 `LIKE` 및 `PATINDEX` 등의 패턴 일치를 포함하는 문자열 비교에 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
### <a name="a-simple-example"></a>A: 간단한 예   
다음 예제에서는 `m` 문자로 시작하는 이름을 반환합니다. `[n-z]`는 두 번째 문자가 `n`부터 `z` 사이여야 함을 지정합니다. 백분율 와일드카드 `%`는 3 문자로 시작하는 모든 문자 또는 문자 없음을 허용합니다. `model` 및 `msdb` 데이터베이스는 이 기준을 충족합니다. `master` 데이터베이스는 충족하지 않으며 결과 집합에서 제외됩니다.
 
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
 조건에 맞는 추가적인 데이터베이스를 설치할 수 있습니다.


### <a name="b-more-complex-example"></a>B: 복잡한 예   
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



  
## <a name="see-also"></a>참고 항목  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX&#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [%&#40;와일드카드 - 일치하는 문자&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93;&#40;와일드카드 - 일치하는 문자&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [\_&#40;와일드카드 - 문자 하나와 일치&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
