---
title: =(같음)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- =
- = (Equals)
- Equals
- =_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- equals operator (=)
- = (equals operator)
ms.assetid: 18885245-5f55-4831-8f0b-7f2a3e82e246
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f60995e7741dd0ed7f420a07c7cd2aa2199ed3c
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65982374"
---
# <a name="-equals-transact-sql"></a>=(같음)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 두 식이 같은지 비교합니다(비교 연산자).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression = expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 두 식의 데이터 형식이 같지 않은 경우 한 식의 데이터 형식을 다른 식의 데이터 형식으로 암시적인 변환이 가능해야 합니다. 변환은 [데이터 형식 우선 순위](../../t-sql/data-types/data-type-precedence-transact-sql.md) 규칙을 기반으로 합니다.  
  
## <a name="result-types"></a>결과 형식  
 Boolean  
  
## <a name="remarks"></a>Remarks  
 NULL 식을 사용하여 비교하는 경우 결과는 `ANSI_NULLS` 설정에 따라 다음과 같이 달라집니다.  
  
-   `ANSI_NULLS`이 ON으로 설정된 경우 NULL은 알 수 없는 값이며 다른 Null을 포함한 다른 모든 값과 비교할 수 없다는 ANSI 규칙에 따라 NULL과 비교 결과는 UNKNOWN입니다.  
  
-   `ANSI_NULLS`이 OFF로 설정된 경우 NULL과 NULL을 비교한 결과는 TRUE이고 다른 값과 NULL을 비교한 결과는 FALSE입니다.  

자세한 내용은 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)를 참조하세요.
  
 결과적으로 UNKNOWN이 되는 부울 식은 모두는 아니지만 대부분의 경우 비슷하게 FALSE로 동작합니다. 자세한 내용은 [NULL 및 UNKNOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/null-and-unknown-transact-sql.md) 및 [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)을 참조하세요.  
  
  
## <a name="examples"></a>예  
  
### <a name="a-using--in-a-simple-query"></a>1. 간단한 쿼리에서 = 사용  
 다음 예에서는 Equals 연산자(=)를 사용하여 `HumanResources.Department` 열의 값이 'Manufacturing' 단어와 같은 `GroupName` 테이블의 모든 행을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE GroupName = 'Manufacturing';  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
DepartmentID Name  
------------ --------------------------------------------------  
7            Production  
8            Production Control  
  
(2 row(s) affected)  
  
```  
  
### <a name="b-comparing-null-and-non-null-values"></a>2. NULL 값과 NULL이 아닌 값 비교  
 다음 예에서는 Equals(`=`)와 Not Equal To(`<>`) 비교 연산자를 사용하여 테이블의 `NULL` 및 Null이 아닌 값에 비교를 수행합니다. 또한 `IS NULL`이 `SET ANSI_NULLS` 설정의 영향을 받지 않는다는 것을 보여 줍니다.  
  
```  
-- Create table t1 and insert 3 rows.  
CREATE TABLE dbo.t1 (a INT NULL);  
INSERT INTO dbo.t1 VALUES (NULL),(0),(1);  
GO  
  
-- Print message and perform SELECT statements.  
PRINT 'Testing default setting';  
DECLARE @varname int;   
SET @varname = NULL;  
  
SELECT a  
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to ON and test.  
PRINT 'Testing ANSI_NULLS ON';  
SET ANSI_NULLS ON;  
GO  
DECLARE @varname int;  
SET @varname = NULL  
  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to OFF and test.  
PRINT 'Testing SET ANSI_NULLS OFF';  
SET ANSI_NULLS OFF;  
GO  
DECLARE @varname int;  
SET @varname = NULL;  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- Drop table t1.  
DROP TABLE dbo.t1;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Testing default setting  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
a  
-----------  
0  
1  
  
(2 row(s) affected)  
  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
Testing ANSI_NULLS ON  
a  
-----------  
  
(0 row(s) affected)  
  
a  
-----------  
  
(0 row(s) affected)  
  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
Testing SET ANSI_NULLS OFF  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
a  
-----------  
0  
1  
  
(2 row(s) affected)  
  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
