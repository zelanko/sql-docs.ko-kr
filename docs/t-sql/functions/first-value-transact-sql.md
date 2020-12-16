---
description: FIRST_VALUE(Transact-SQL)
title: FIRST_VALUE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/22/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FIRST_VALUE_TSQL
- FIRST_VALUE
dev_langs:
- TSQL
helpviewer_keywords:
- FIRST_VALUE function
- analytic functions, FIRST_VALUE
ms.assetid: 1990c3c7-dad2-48db-b2cd-3e8bd2c49d17
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7f4b4a3eb573020e84096b824b305a0085958d2a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484185"
---
# <a name="first_value-transact-sql"></a>FIRST_VALUE(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  정렬된 값 세트의 첫 번째 값을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
FIRST_VALUE ( [scalar_expression ] )  [ IGNORE NULLS | RESPECT NULLS ]
    OVER ( [ partition_by_clause ] order_by_clause [ rows_range_clause ] )
  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *scalar_expression*  
 반환할 값입니다. *scalar_expression* 은 열, 하위 쿼리 또는 결과로 반환되는 값이 하나뿐인 임의의 다른 식일 수 있습니다. 다른 분석 함수는 사용할 수 없습니다.  

 [ IGNORE NULLS | RESPECT NULLS ]     
 **적용 대상**: Azure SQL Edge

 IGNORE NULLS - 파티션의 첫 번째 값을 컴퓨팅할 때 데이터 세트의 null 값을 무시합니다.     
 RESPECT NULLS - 파티션의 첫 번째 값을 컴퓨팅할 때 데이터 세트의 null 값을 고려합니다.     
 
  자세한 내용은 [누락 값 입력](/azure/azure-sql-edge/imputing-missing-values/)을 참조하세요.
  
 OVER **(** [ *partition_by_clause* ] *order_by_clause* [ *rows_range_clause* ] **)**  
 *partition_by_clause* 는 FROM 절이 생성한 결과 집합을 함수가 적용되는 파티션으로 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause* 는 작업이 수행되는 논리적 순서를 결정합니다. *order_by_clause* 가 필요합니다. *rows_range_clause* 는 시작점 및 끝점을 지정하여 파티션 내에서 행을 추가로 제한합니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.  
  
## <a name="return-types"></a>반환 형식  
 *scalar_expression* 과 같은 유형입니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 FIRST_VALUE는 비결정적입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-first_value-over-a-query-result-set"></a>A. 쿼리 결과 집합에 FIRST_VALUE 사용  
 다음 예에서는 FIRST_VALUE를 사용하여 지정된 제품 범주에서 가격이 가장 저렴한 제품의 이름을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name, ListPrice,   
       FIRST_VALUE(Name) OVER (ORDER BY ListPrice ASC) AS LeastExpensive   
FROM Production.Product  
WHERE ProductSubcategoryID = 37;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Name                    ListPrice             LeastExpensive  
----------------------- --------------------- --------------------  
Patch Kit/8 Patches     2.29                  Patch Kit/8 Patches  
Road Tire Tube          3.99                  Patch Kit/8 Patches  
Touring Tire Tube       4.99                  Patch Kit/8 Patches  
Mountain Tire Tube      4.99                  Patch Kit/8 Patches  
LL Road Tire            21.49                 Patch Kit/8 Patches  
ML Road Tire            24.99                 Patch Kit/8 Patches  
LL Mountain Tire        24.99                 Patch Kit/8 Patches  
Touring Tire            28.99                 Patch Kit/8 Patches  
ML Mountain Tire        29.99                 Patch Kit/8 Patches  
HL Road Tire            32.60                 Patch Kit/8 Patches  
HL Mountain Tire        35.00                 Patch Kit/8 Patches  
  
```  
  
### <a name="b-using-first_value-over-partitions"></a>B. 파티션에 FIRST_VALUE 사용  
 다음 예에서는 FIRST_VALUE를 사용하여 직함이 같은 다른 직원과 비교해 휴가 일 수가 가장 적은 직원을 반환합니다. PARTITION BY 절은 직원을 직함별로 분할하며 FIRST_VALUE 함수는 각 파티션에 개별적으로 적용됩니다. OVER 절에 지정된 ORDER BY 절은 FIRST_VALUE 함수가 각 파티션의 행에 적용되는 논리적 순서를 결정합니다. ROWS UNBOUNDED PRECEDING 절은 창 시작점을 각 파티션의 첫 번째 행으로 지정합니다.  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT JobTitle, LastName, VacationHours,   
       FIRST_VALUE(LastName) OVER (PARTITION BY JobTitle   
                                   ORDER BY VacationHours ASC  
                                   ROWS UNBOUNDED PRECEDING  
                                  ) AS FewestVacationHours  
FROM HumanResources.Employee AS e  
INNER JOIN Person.Person AS p   
    ON e.BusinessEntityID = p.BusinessEntityID  
ORDER BY JobTitle;  
```  
  
 다음은 결과 집합의 일부입니다.  
  
```  
  
JobTitle                            LastName                  VacationHours FewestVacationHours  
----------------------------------- ------------------------- ------------- -------------------  
Accountant                          Moreland                  58            Moreland  
Accountant                          Seamans                   59            Moreland  
Accounts Manager                    Liu                       57            Liu  
Accounts Payable Specialist         Tomic                     63            Tomic  
Accounts Payable Specialist         Sheperdigian              64            Tomic  
Accounts Receivable Specialist      Poe                       60            Poe  
Accounts Receivable Specialist      Spoon                     61            Poe  
Accounts Receivable Specialist      Walton                    62            Poe  
```  
  
## <a name="see-also"></a>참고 항목  
 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
 [Last_Value&#40;Transact-SQL&#41;](last-value-transact-sql.md)  

