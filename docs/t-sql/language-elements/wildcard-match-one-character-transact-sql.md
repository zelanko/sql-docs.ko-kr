---
title: "_ (와일드 카드-문자 하 나와 일치) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
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
dev_langs: TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 96a529dd77d0d76ecf8fe85dba2d211c71b4c398
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (와일드카드 - 문자 하나와 일치)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

밑줄 문자 _를 사용 하 여 패턴 일치와 같은 포함 하는 문자열 비교 작업에서 임의의 단일 문자와 일치 하도록 `LIKE` 및 `PATINDEX`합니다.  
  
## <a name="examples"></a>예  

## <a name="a-simple-example"></a>A: 간단한 예   

다음 예에서는 모든 데이터베이스 이름이 문자로 시작 하는 반환 `m` 문자 있고 `d` 고 세 번째 문자입니다. 밑줄 문자는 이름의 두 번째 문자에 문자일 수를 지정 합니다. `model` 및 `msdb` 데이터베이스가이 기준을 충족 합니다. `master` 데이터베이스는 그렇지 않습니다.

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
이 조건을 충족 하는 추가 데이터베이스를 할 수 있습니다.

여러 개의 문자를 나타내는 여러 밑줄을 사용할 수 있습니다. 변경 된 `LIKE` 두 개의 밑줄을 포함 하는 조건을 `'m__%` master 데이터베이스의 결과에 포함 됩니다.

### <a name="b-more-complex-example"></a>B: 더 복잡 한 예제
 다음 예제에서는 _ 연산자를 사용 하 여 모든 사람에 찾을 수는 `Person` 끝나는 세 문자 이름을 가진 테이블 `an`합니다.  
  
```sql  
-- USE AdventureWorks2012
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C: 밑줄 문자를 이스케이프 처리   
다음 예제에서는 같은 고정된 데이터베이스 역할의 이름을 반환 `db_owner` 및 `db_ddladmin`를 반환 한다는 `dbo` 사용자입니다. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

세 번째 문자 위치에 밑줄은를 와일드 카드로 라인 상태가 되며 문자로 시작 하는 사용자만 필터링 되지 않도록 `db_`합니다. 값이 되도록 이스케이프 밑줄을 대괄호로 묶으십시오 `[_]`합니다. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
이제는 `dbo` 사용자 제외 됩니다.   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>관련 항목:  
 [마찬가지로 &#40; Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40; Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (와일드 카드-하나 이상의 문자 일치)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (와일드 카드-하나 이상의 문자 일치)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93; (와일드 카드-일치 하지 않는 문자)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
