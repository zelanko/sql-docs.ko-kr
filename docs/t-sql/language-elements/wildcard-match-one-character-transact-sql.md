---
title: _(와일드카드 - 문자 하나와 일치)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- Match
- wildcard
- _TSQL
- Match One
- _
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb82b8abe1b5a7d37fc74945dfc82ccce1882740
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (와일드카드 - 문자 하나와 일치)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

밑줄 문자(_)를 사용하여 `LIKE` 및 `PATINDEX`와 같은 패턴 일치가 포함된 문자열 비교 작업에서 단일 문자와 일치하도록 합니다.  
  
## <a name="examples"></a>예  

## <a name="a-simple-example"></a>A: 간단한 예   

다음 예제에서는 문자 `m`로 시작하고 문자 `d`를 세 번째 문자로 가진 모든 데이터베이스 이름을 반환합니다. 밑줄 문자는 이름의 두 번째 문자가 임의의 문자가 될 수 있음을 나타냅니다. `model` 및 `msdb` 데이터베이스는 이 기준을 충족합니다. `master` 데이터베이스는 그렇지 않습니다.

```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm_d%';
```   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-----
model
msdb
```   
이 조건을 충족하는 추가 데이터베이스가 있을 수 있습니다.

여러 개의 밑줄을 사용하여 여러 문자를 나타낼 수 있습니다. 두 개의 밑줄 `'m__%`을 포함하도록 `LIKE` 조건을 변경하면 결과에 master 데이터베이스가 포함됩니다.

### <a name="b-more-complex-example"></a>B: 복잡한 예
 다음 예제에서는 _연산자를 사용하여 `Person` 테이블에서 `an`으로 끝나는 3개 문자로 된 이름을 가진 모든 사람을 찾습니다.  
  
```sql  
-- USE AdventureWorks2012
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C: 밑줄 문자 이스케이핑   
다음 예제에서는 `db_owner` 및 `db_ddladmin`와 같은 고정 데이터베이스 역할의 이름을 반환하지만 `dbo` 사용자도 반환합니다. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

세 번째 문자 위치의 밑줄은 와일드카드로 사용되며 `db_` 문자로 시작하는 보안 주체만 필터링하지 않습니다. 밑줄을 이스케이프하려면 대괄호 `[_]`로 묶습니다. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
이제 `dbo` 사용자는 제외됩니다.   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>참고 항목  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [%(와일드카드 - 일치하는 문자)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91 &#93;(와일드카드 - 일치하는 문자)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93;(와일드카드 - 일치하지 않는 문자)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
