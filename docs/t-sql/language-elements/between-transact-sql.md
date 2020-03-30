---
title: BETWEEN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BETWEEN
- BETWEEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- inclusive ranges
- testing range
- exclusive ranges
- NOT BETWEEN operator
- BETWEEN operator
- range to test [SQL Server]
ms.assetid: a5d5b050-203e-4355-ac85-e08ef5ca7823
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d835e68c767866a130ebb62c26fd315f5448416e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67947769"
---
# <a name="between-transact-sql"></a>BETWEEN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  테스트할 범위를 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
test_expression [ NOT ] BETWEEN begin_expression AND end_expression  
```  
  
## <a name="arguments"></a>인수  
 *test_expression*  
 [begin_expression](../../t-sql/language-elements/expressions-transact-sql.md) 및 *end_expression*에 정의된 범위에서 테스트할 *식*입니다. *test_expression*은 *begin_expression* 및 *end_expression* 모두와 동일한 데이터 형식이어야 합니다.  
  
 NOT  
 조건자의 결과를 부정합니다.  
  
 *begin_expression*  
 유효한 식입니다. *begin_expression*은 *test_expression* 및 *end_expression* 모두와 동일한 데이터 형식이어야 합니다.  
  
 *end_expression*  
 유효한 식입니다. *end_expression*은 *test_expression* 및 *begin_expression* 모두와 동일한 데이터 형식이어야 합니다.  
  
 AND  
 *test_expression*이 *begin_expression* 및 *end_expression*으로 표시된 범위 내에 있어야 함을 나타내는 자리 표시자 역할을 합니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="result-value"></a>결과 값  
 **test_expression**의 값이 *begin_expression*의 값보다 크거나 같고 *end_expression*의 값보다 작거나 같으면, BETWEEN에서 *TRUE*를 반환합니다.  
  
 **test_expression**의 값이 *begin_expression*의 값보다 작거나 *end_expression*의 값보다 크면, NOT BETWEEN에서 *TRUE*를 반환합니다.  
  
## <a name="remarks"></a>설명  
 경계값이 포함되지 않는 범위를 지정하려면 보다 큼(>) 및 보다 작음 연산자(<)를 사용합니다. BETWEEN 또는 NOT BETWEEN 조건자에 입력한 값이 NULL이면 결과는 UNKNOWN이 됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-between"></a>A. BETWEEN 사용  
 다음 예제에서는 데이터베이스의 데이터베이스 역할에 대한 정보를 반환합니다. 첫 번째 쿼리는 모든 역할을 반환합니다. 두 번째 예제에서는 `BETWEEN` 절을 사용하여 역할을 지정한 `database_id` 값으로 제한합니다.  
  
```sql  
SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R';

SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R'
AND principal_id BETWEEN 16385 AND 16390;
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]   
```  
principal_id    name
------------  ---- 
0               public
16384           db_owner
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
16391           db_datawriter
16392           db_denydatareader
16393           db_denydatawriter
```  
```  
principal_id    name
------------  ---- 
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
```  
  
### <a name="b-using--and--instead-of-between"></a>B. BETWEEN 대신 > 및 < 사용  
 다음 예에서는 보다 큼(`>`) 및 보다 작음(`<`) 연산자를 사용합니다. 이 연산자는 경계값을 포함하지 않기 때문에 이전 예에서 10개의 행을 반환한 것과 달리 9개의 행을 반환합니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate > 27 AND ep.Rate < 30  
ORDER BY ep.Rate;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 FirstName   LastName             Rate  
 ---------   -------------------  ---------  
 Paula       Barreto de Mattos    27.1394  
 Janaina     Bueno                27.4038  
 Dan         Bacon                27.4038  
 Ramesh      Meyyappan            27.4038  
 Karen       Berg                 27.4038  
 David       Bradley              28.7500  
 Hazem       Abolrous             28.8462  
 Ovidiu      Cracium              28.8462  
 Rob         Walters              29.8462  
 ```    
  
### <a name="c-using-not-between"></a>C. NOT BETWEEN 사용  
 다음 예에서는 지정한 범위인 `27`에서 `30`사이에 속하지 않는 모든 행을 검색합니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate NOT BETWEEN 27 AND 30  
ORDER BY ep.Rate;  
GO  
```  
  
### <a name="d-using-between-with-datetime-values"></a>D. BETWEEN에 datetime 값 사용  
 다음 예제에서는 **datetime** 값이 `'20011212'` 이상 및 `'20020105'` 이하인 행을 검색합니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT BusinessEntityID, RateChangeDate  
FROM HumanResources.EmployeePayHistory  
WHERE RateChangeDate BETWEEN '20011212' AND '20020105';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 BusinessEntityID RateChangeDate  
 ----------- -----------------------  
 3           2001-12-12 00:00:00.000  
 4           2002-01-05 00:00:00.000  
 ```  
 
 쿼리의 날짜 값과 **열에 저장된**datetime`RateChangeDate` 값을 날짜의 시간 부분이 없이 지정했으므로 쿼리에서 예상되는 행을 검색합니다. 시간 부분을 지정하지 않으면 기본적으로 12:00 A.M.이 사용됩니다. 2002-01-05에서 12:00 A.M. 이후의 시간 부분이 포함된 행은 범위를 벗어났으므로 이 쿼리에서 반환되지 않습니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [&#62;&#40;보다 큼&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/greater-than-transact-sql.md)   
 [&#60;&#40;보다 작음&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/less-than-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


