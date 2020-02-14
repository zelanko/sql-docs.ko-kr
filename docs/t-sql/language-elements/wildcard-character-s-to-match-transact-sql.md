---
title: 하나 이상의 문자를 찾는 [] 와일드카드
description: 와일드카드를 사용하여 하나 이상의 문자를 찾습니다.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 82876d2f0e749163ced821bdc24797a6f71b6e7e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76831585"
---
# <a name="--wildcard---characters-to-match-transact-sql"></a>\[ \](와일드카드 - 하나 이상의 문자 일치)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

지정된 범위 또는 대괄호 `[ ]` 사이에 지정한 집합에 포함되는 하나의 문자와 일치됩니다. 와일드카드 문자는 `LIKE` 및 `PATINDEX` 등의 패턴 일치를 포함하는 문자열 비교에 사용할 수 있습니다.  

 
## <a name="examples"></a>예  
### <a name="a-simple-example"></a>A: 간단한 예   
다음 예에서는 `m` 문자로 시작하는 이름을 반환합니다. `[n-z]`는 두 번째 문자가 `n`부터 `z` 사이여야 함을 지정합니다. 백분율 와일드카드 `%`는 3 문자로 시작하는 모든 문자 또는 문자 없음을 허용합니다. `model` 및 `msdb` 데이터베이스는 이 기준을 충족합니다. `master` 데이터베이스는 기준을 충족하지 않으며 결과 집합에서 제외됩니다.
 
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
  
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  
  
```  
EmployeeID      FirstName      LastName      PostalCode  
----------      ---------      ---------     ----------  
290             Lynn           Tsoflias      3000  
```  

### <a name="c-using-a-set-that-combines-ranges-and-single-characters"></a>C: 범위 및 단일 문자를 결합하는 세트 사용

와일드카드 세트에 단일 문자와 범위를 모두 포함할 수 있습니다. 다음 예제에서는 [] 연산자를 사용하여 숫자 또는 일련의 특수 문자로 시작하는 문자열을 찾습니다.

```sql
SELECT [object_id], OBJECT_NAME(object_id) AS [object_name], name, column_id 
FROM sys.columns 
WHERE name LIKE '[0-9!@#$.,;_]%';
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
object_id     object_name                         name  column_id
---------     -----------                         ----  ---------
615673241     vSalesPersonSalesByFiscalYears      2002  5
615673241     vSalesPersonSalesByFiscalYears      2003  6
615673241     vSalesPersonSalesByFiscalYears      2004  7
1591676718    JunkTable                           _xyz  1
```
  
## <a name="see-also"></a>참고 항목  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX&#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [%&#40;와일드카드 - 일치하는 문자&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93;&#40;와일드카드 - 일치하는 문자&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [\_&#40;와일드카드 - 문자 하나와 일치&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
