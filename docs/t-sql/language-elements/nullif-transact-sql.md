---
description: NULLIF(Transact-SQL)
title: NULLIF(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NULLIF
- NULLIF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], equivalent expressions
- expressions [SQL Server], null values
- NULLIF function
- equivalent expressions [SQL Server]
ms.assetid: 44c7b67e-74c7-4bb9-93a4-7a3016bd2feb
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6ceef62e268cc34f036423b2e55b56152d24ea2e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88361329"
---
# <a name="nullif-transact-sql"></a>NULLIF(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지정된 두 식이 같으면 Null 값을 반환합니다. 예를 들어 `SELECT NULLIF(4,4) AS Same, NULLIF(5,7) AS Different;`는 두 입력 값이 동일하기 때문에 첫 번째 열(4 및 4)에 대해 NULL을 반환합니다. 두 번째 열은 두 입력 값이 다르기 때문에 첫 번째 값(5)을 반환합니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
NULLIF ( expression , expression )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 스칼라 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 첫 번째 *식*과 동일한 형식을 반환합니다.  
  
 NULLIF는 두 식이 같지 않으면 첫 번째 *식*을 반환합니다. 식이 같으면 NULLIF는 첫 번째 *식* 형식의 Null 값을 반환합니다.  
  
## <a name="remarks"></a>설명  
 NULLIF는 두 식이 동일하며 결과 식이 NULL인 검색된 CASE 식과 동일합니다.  
  
 NULLIF 함수 내에 RAND()와 같은 시간에 종속적인 함수를 사용하지 않는 것이 좋습니다. 이렇게 하면 함수가 두 번 평가되고 두 호출에서 다른 결과가 반환됩니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-returning-budget-amounts-that-have-not-changed"></a>A. 변경되지 않은 예산 반환  
 다음 예에서는 부서(`budgets`), 금년도 예산(`dept`) 및 전년도 예산(`current_year`)을 보여 주는 `previous_year` 테이블을 만듭니다. 금년 예산이 전년도 예산에서 변하지 않은 부서에는 `NULL`이 예산이 아직 결정되지 않은 부서에는 `0`이 사용됩니다. 예산이 결정된 부서만의 평균을 계산하고 이전 연도의 예산 값(`previous_year` 값 사용. 여기서 `current_year`는 `NULL`임)을 포함하려면 `NULLIF` 함수와 `COALESCE` 함수를 결합합니다.  
  
```sql  
CREATE TABLE dbo.budgets  
(  
   dept            TINYINT   IDENTITY,  
   current_year    DECIMAL   NULL,  
   previous_year   DECIMAL   NULL  
);  
INSERT budgets VALUES(100000, 150000);  
INSERT budgets VALUES(NULL, 300000);  
INSERT budgets VALUES(0, 100000);  
INSERT budgets VALUES(NULL, 150000);  
INSERT budgets VALUES(300000, 250000);  
GO    
SET NOCOUNT OFF;  
SELECT AVG(NULLIF(COALESCE(current_year,  
   previous_year), 0.00)) AS 'Average Budget'  
FROM budgets;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Average Budget  
 --------------  
 212500.000000  
 (1 row(s) affected)
 ```  
  
### <a name="b-comparing-nullif-and-case"></a>B. NULLIF 및 CASE 비교  
 `NULLIF`와 `CASE`의 유사점을 보여 주기 위해 다음 쿼리는 `MakeFlag` 및 `FinishedGoodsFlag` 열의 값이 같은지 여부를 평가합니다. 첫 번째 쿼리에서는 `NULLIF`를 사용합니다. 두 번째 쿼리에서는 `CASE` 식을 사용합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT ProductID, MakeFlag, FinishedGoodsFlag,   
   NULLIF(MakeFlag,FinishedGoodsFlag) AS 'Null if Equal'  
FROM Production.Product  
WHERE ProductID < 10;  
GO  
  
SELECT ProductID, MakeFlag, FinishedGoodsFlag,'Null if Equal' =  
   CASE  
       WHEN MakeFlag = FinishedGoodsFlag THEN NULL  
       ELSE MakeFlag  
   END  
FROM Production.Product  
WHERE ProductID < 10;  
GO  
```  

### <a name="c-returning-budget-amounts-that-contain-no-data"></a>C. 데이터가 포함되지 않은 예산 반환  
 다음 예제에서는 `budgets` 테이블을 만들고, 데이터를 로드하고, `NULLIF`를 사용하여 `current_year` 또는 `previous_year`에 데이터가 포함되지 않는 경우 Null을 반환합니다.  
  
```sql  
CREATE TABLE budgets (  
   dept           TINYINT,  
   current_year   DECIMAL(10,2),  
   previous_year  DECIMAL(10,2)  
);  
  
INSERT INTO budgets VALUES(1, 100000, 150000);  
INSERT INTO budgets VALUES(2, NULL, 300000);  
INSERT INTO budgets VALUES(3, 0, 100000);  
INSERT INTO budgets VALUES(4, NULL, 150000);  
INSERT INTO budgets VALUES(5, 300000, 300000);  
  
SELECT dept, NULLIF(current_year,  
   previous_year) AS LastBudget  
FROM budgets;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 dept   LastBudget  
 ----   -----------  
 1      100000.00  
 2      null 
 3      0.00  
 4      null  
 5      null
 ```  
  
## <a name="see-also"></a>참고 항목  
 [CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [decimal 및 numeric&#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  

